---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-10-21
tema: Laboratorio 3 · tu servidor DNS autoritativo con BIND9 (zona directa, zona inversa, transferencia y delegación)
fuente: "SER_Lab03_Guia.pdf (13 páginas) + SER_Lab03_Comandos (.txt y .pdf, contenido idéntico) + transcripción de la clase en directo (≈67 min) + notas propias de Dani"
---
# SER · Laboratorio 3 (21/10) · Tu nombre en Internet: DNS con BIND9

> Anterior: [DNS: archivo de zona, SOA y preparación de AWS (20/10)](2026-10-20_dns-zonas-soa-preparacion-bind9.md) · Profesor: Damián Sualdea Soy

Cierra el bloque que empezó el 13/10. Hoy se **escribe a mano** el archivo de zona de un dominio propio, se sirve desde una máquina de AWS con IP fija y se pregunta al servidor con `host` y `dig`. Es la base de la **Actividad 1** (opcional, 15 %, entrega **16/11**): al final de la guía se dice que lo de hoy, con capturas, es el criterio 1.

Lo que hay aquí sale de tres fuentes, marcadas como **(guía)**, **(clase)** y **(temario)**. Lo que es mío o dudoso va indicado.

> [!note] Cómo fue la clase
> El profesor pulsó por error el botón **Reset** del Learner Lab y se cargó su laboratorio, así que rehizo en directo el montaje de AWS. Su servidor no llegó a responder desde fuera porque la delegación no había propagado. Los compañeros con la delegación ya hecha de antes (María) sí vieron `host` funcionando. Lo útil de la grabación es el orden de pasos y los errores típicos; la referencia limpia es la guía.

## Las dos mitades que hacen falta (guía)

| Pieza | Dónde vive | Qué hace |
|---|---|---|
| **Servidor** | Tu máquina `srv_dns` en AWS, con BIND9 | Tiene el fichero de zona y contesta. Tú lo pruebas con `dig @<ELASTIC-IP> tu-dominio` |
| **Delegación** | El panel del **registrador** (Namecheap, IONOS...) | Dice al mundo "para este dominio, preguntad a `ns.tu-dominio`, que está en esta IP" (registro NS + **glue**) |

Una sin la otra no sirve: un servidor sin delegar no lo encuentra nadie, y una delegación sin servidor apunta a la nada. La delegación **propaga lenta** (de minutos a horas), por eso se lanza primero y se prueba al final.

```
Internet ──▶ Registrador ──(NS + glue)──▶ srv_dns (BIND9, Elastic IP)
 "¿quién es            delega              ├─ zona directa:  tu-dominio        (nombre → IP)
  tu-dominio?"                             └─ zona inversa:  31.172.in-addr.arpa (IP → nombre)
```

## Lo imprescindible (la chuleta)

1. **Elastic IP** asociada a la instancia, y **Security Group con el 53 abierto en UDP *y* en TCP** (más el 22 de SSH).
2. `sudo apt install -y bind9 bind9-utils bind9-dnsutils`.
3. `hostname -I` → apuntar los **dos últimos números** de la IP privada (172.31.**x.y**).
4. `named.conf.local`: declarar **dos zonas**. El nombre de la zona directa es **el dominio, sin `ns.`**.
5. Copiar `db.local` → fichero de zona directa y `db.127` → fichero de zona inversa, y editarlos.
6. **Todos los nombres completos acaban en punto.**
7. `named-checkconf` y `named-checkzone` **antes** de reiniciar. Silencio = bien; `OK` = bien.
8. `systemctl restart named`, `ss -ulpn | grep :53`, y a preguntar con `host`/`dig`.
9. Al cambiar algo en la zona, **subir el serial**.
10. Al acabar: **Stop** (nunca Terminate) y **no liberar la Elastic IP**.

## Paso 0 · Preparar AWS (guía + clase)

- AWS Academy → Learner Lab → **Start Lab** → EC2 → Launch instance.
- Nombre `srv_dns`, **Ubuntu Server 24.04 LTS**, tipo `t3.micro`, par de claves `vockey`.
- Security group `sg-dns` con **tres** reglas de entrada:

| Tipo | Protocolo | Puerto | Origen |
|---|---|---|---|
| SSH | TCP | 22 | 0.0.0.0/0 |
| DNS (UDP) | UDP | 53 | 0.0.0.0/0 |
| DNS (TCP) | TCP | 53 | 0.0.0.0/0 |

> [!warning] Las reglas del 53 son dos, no una
> UDP para las consultas normales y **TCP para respuestas grandes y transferencias de zona**. Con solo una, la mitad del laboratorio falla sin que se sepa por qué: es el fallo más repetido (guía).

- **Elastic IP**: EC2 → Elastic IPs → Allocate → **Actions → Associate** con `srv_dns`. Comprobar en *Instances* que «Public IPv4» ahora es esa dirección.
  - En clase se vio el fallo típico: la IP estaba **creada pero no asociada**, y la lista de instancias no la mostraba hasta asociarla y refrescar.
  - Motivo: la IP pública normal **cambia cada vez que paras y arrancas** la instancia; si delegas a esa, mañana la delegación apunta a una máquina que ya no es la tuya.
  - Coste: unos 0,005 $/hora por IPv4 pública (≈ 3,65 $/mes), asociada o no. **No se libera al acabar**: se reutiliza en el Tema 4 (servidor web).
- ⛔ **No pulses «Reset»** en el Learner Lab: borra todo lo hecho (clase).
- `chmod 400 labsuser.pem` y `ssh -i labsuser.pem ubuntu@<ELASTIC-IP>`.

## Paso 0b · La delegación en el registrador

Esto se lanza **ya, al principio**, porque tarda en propagar. Lo que se registra es tu **servidor de nombres**: `ns.tu-dominio` → tu **Elastic IP** (la fija, no la pública del día).

> [!important] El nombre del NS tiene que ser el mismo en todas partes
> El nombre que registras (`ns`, `ns1`...) es el que luego va en el **SOA**, en el **registro NS** de la zona y como **registro A** de esa misma zona (guía). Si en el registrador pones `ns1` y en la zona escribes `ns`, no cuadra.

| Registrador | Dónde se cambia (guía) |
|---|---|
| **Namecheap (.me)** | Domain List → Manage → **Advanced DNS** → abajo del todo, **Personal DNS Server** (registras `ns` + Elastic IP) → luego pestaña **Domain → Nameservers → Custom DNS** |
| IONOS | Dominios & SSL → tu dominio → Servidores de nombres → *Utilizar servidores DNS personalizados* |
| .TECH | Manage → DNS → Nameservers → Edit nameservers → Custom nameservers |
| Name.com | Nameservers / Custom DNS, con registro de host (glue) si el `ns` va dentro de tu propio dominio |

En Namecheap son **dos pantallas, en este orden**: primero se registra el nameserver con su IP (el *glue*) y después se le dice al dominio que use *Custom DNS*. Solo la segunda **no basta**: si pones un `ns.tu-dominio` que no has registrado antes con su IP, no resuelve. Algunos registradores piden **dos** nameservers (`ns1` y `ns2`): se ponen los dos a la **misma** Elastic IP (guía). En clase el profesor dijo que, en IONOS, el segundo puede llevar cualquier IP porque no se usa.

Tras guardar, la propagación es de minutos a un par de horas. Se comprueba con `dig +trace tu-dominio` y en whatsmydns.net (tipo **NS**).

## Paso 1 · Instalar BIND9 (guía)

```bash
sudo apt update
sudo apt install -y bind9 bind9-utils bind9-dnsutils
named -v                              # p. ej. "BIND 9.18.39-Ubuntu"
systemctl status named --no-pager
ls /etc/bind/
```

- **`named` es el programa (el demonio); BIND9 es el paquete.** El servicio responde a **los dos nombres** en systemctl (`named` y `bind9`). El temario también dice que `named` es "el nombre del demonio de bind9". En clase el profesor acabó usando `named` por ser más corto: "es exactamente lo mismo".
- Mi inferencia, sin confirmar en clase: `bind9-utils` trae `named-checkconf`/`named-checkzone` y `bind9-dnsutils` trae `dig`/`host`/`nslookup`. Se comprueba con `dpkg -L <paquete>`.
- Los **tres ficheros que importan** (guía):

| Fichero | Para qué |
|---|---|
| `named.conf` | Solo **incluye** a los otros; casi nunca se toca |
| `named.conf.options` | **Cómo se comporta** el servidor (recursión, quién puede preguntar...) |
| `named.conf.local` | **Qué zonas sirve**. Aquí se declaran las tuyas |

- Los `db.*` (en clase: `db.0`, `db.127`, `db.255`, `db.empty`, `db.local`) son **ejemplos** que trae el paquete. No se editan: **se copian con el nombre de tu zona y se edita la copia**.
- Regla general (clase): cada vez que cambias la configuración de un servicio hay que **reiniciarlo**; `systemctl` es la forma de arrancar, parar y reiniciar servicios.

## Paso 2 · La IP privada

```bash
hostname -I        # p. ej. 172.31.10.218  →  anota los DOS ÚLTIMOS números: 10 y 218
```

Es la IP de dentro de la VPC (empieza por **172.31**), **no** la Elastic IP. Se necesita solo para la zona inversa.

## Paso 3 · Declarar las dos zonas (guía)

```bash
sudo nano /etc/bind/named.conf.local
```

Se añade **al final** (lo que ya haya, se deja):

```
zone "desplegando123.com" {
        type master;
        file "/etc/bind/db.desplegando123.com";
        allow-transfer { any; };
};

zone "31.172.in-addr.arpa" {
        type master;
        file "/etc/bind/db.31.172";
};
```

> [!warning] El fallo número uno: la zona se llama como el DOMINIO, no lleva `ns.`
> `zone "desplegando123.com"` está bien; `zone "ns.desplegando123.com"` sale todo doblado (`www.ns...`, `correo.ns...`) y no resuelve. El `ns` es un **registro dentro de la zona**, no parte de su nombre. Prueba: en el `dig axfr` el apex tiene que salir como `desplegando123.com.` a secas.
> En clase esto generó confusión: un compañero (Manuel) argumentó que "por lógica tiene que ir el NS" y el profesor titubeó entre `ns.<dominio>` y el dominio (la transcripción es confusa en ese tramo). **Vale lo que dice la guía: zona = dominio.** Revisa que tu `named.conf.local` no tenga `ns.` en el nombre de la zona.

- `type master` = **servidor principal**, el que tiene el original (término del temario). En BIND ≥ 9.16 también se admite `primary` como sinónimo (dato mío, no dicho en clase).
- `allow-transfer { any; }` deja que **cualquiera** pida la zona entera. Se pone **a propósito** para verlo funcionar (paso 9); se cierra más adelante con la lista de secundarios (Tema 7, febrero).
- El **nombre del fichero** (`db.desplegando123.com`, `db.ns`...) es libre; lo único obligatorio es que coincida con el que luego creas. En clase se discutió que "este nombre da igual" y los alumnos usaron nombres distintos.
- La zona inversa se llama `31.172.in-addr.arpa` porque la red es `172.31.0.0/16` escrita **al revés**.

```bash
sudo named-checkconf        # silencio = sintaxis correcta
```

Todavía no existen los ficheros de zona (no pasa nada, `named-checkconf` no los mira). **No reinicies `named` aún.**

## Paso 4 · Zona directa (nombre → IP)

```bash
sudo cp /etc/bind/db.local /etc/bind/db.desplegando123.com
sudo named-checkzone desplegando123.com /etc/bind/db.desplegando123.com   # OK, con datos de localhost
sudo nano /etc/bind/db.desplegando123.com
```

Contenido final (cambia `<ELASTIC-IP>` y el dominio por los tuyos):

```
$TTL 3600
@  IN SOA ns.desplegando123.com. admin.desplegando123.com. (
          2026102101    ; serial
          7200          ; refresh
          3600          ; retry
          1209600       ; expire
          86400 )       ; minimum TTL
;
@        IN NS    ns.desplegando123.com.
;
ns       IN A     <ELASTIC-IP>
@        IN A     <ELASTIC-IP>
correo   IN A     <ELASTIC-IP>
;
www      IN CNAME desplegando123.com.
ftp      IN CNAME desplegando123.com.
;
@        IN MX 10 correo.desplegando123.com.
;
@        IN TXT   "v=spf1 a mx -all"
```

Cómo leerlo:

| Línea | Qué dice |
|---|---|
| `$TTL 3600` | TTL por defecto: 1 hora en caché |
| `@ IN SOA ns... admin...` | **SOA**: quién es el servidor primario (`ns.<dominio>.`) y el contacto del administrador |
| `serial` `2026102101` | Versión de la zona. Convención: **AAAAMMDD + nº de cambio del día** (21/10/2026, primer cambio) |
| `7200 / 3600 / 1209600 / 86400` | refresh 2 h · retry 1 h · expire 14 días · TTL mínimo 1 día (campos explicados el 20/10: importan para un secundario) |
| `@ IN NS ns.<dominio>.` | El servidor de nombres de la zona |
| `ns IN A <ELASTIC-IP>` | La **IP del propio `ns`**. Sin esto, el NS de arriba apunta a un nombre que no resuelve |
| `@ IN A` y `correo IN A` | Dominio principal y el host del correo → IPv4. Pueden apuntar a **cualquier** IP (en clase el profesor apuntó `correo` a otra dirección distinta "porque es mío"; el audio no deja claro cuál) |
| `www`/`ftp` `IN CNAME` | **Alias**: apuntan a otro **nombre**, nunca a una IP |
| `@ IN MX 10 correo...` | Correo del dominio; `10` es la prioridad (menor = antes) |
| `@ IN TXT "v=spf1 a mx -all"` | Texto libre; aquí, política SPF de correo |

Reglas que te pueden hacer fallar (guía):
- **`@` lleva un A, no un CNAME** (no se puede).
- **El MX apunta a `correo`, que tiene su propio A**, no al CNAME de `www`.
- El **`;`** abre un comentario que dura **solo esa línea** (clase).
- En un registro, el **valor** puede ser una IP (A) o un nombre (NS, CNAME, MX, PTR).

> [!warning] Los puntos finales no son decoración
> Todo nombre completo acaba en punto. Un nombre **sin** punto es **relativo** y BIND le pega el nombre de la zona detrás: `ns.desplegando123.com` se convierte en `ns.desplegando123.com.desplegando123.com.` (guía). BIND **no avisa**. Es como una ruta absoluta frente a una relativa. En clase el profesor lo repitió varias veces ("todo tiene que acabar con punto") y los fallos de ese rato fueron de esto: a alguien le dijo "te has comido un punto seguro" y María resolvió el suyo con "era un punto".

Comprueba **después de cada edición**:

```bash
sudo named-checkzone desplegando123.com /etc/bind/db.desplegando123.com
# debe decir:  loaded serial 2026102101   y   OK
```

La sintaxis es `named-checkzone <zona> <fichero>`. Si falla, da el **número de línea** exacto; casi siempre es un punto final olvidado.

### El campo `admin` del SOA

Esto se quedó sin explicar el 20/10 ("¿por qué `admin.`?"). Es el **correo del administrador de la zona con un punto en lugar de la `@`**: `admin.desplegando123.com.` = `admin@desplegando123.com`. Lo dice el temario (Tema 3, §3.7, ejemplo `admin.unir.net.`). El nombre `admin` es libre: el profesor dijo "este admin nos da igual" y que no lo va a utilizar (lo que importa es el servidor primario).

## Paso 5 · Zona inversa (IP → nombre)

```bash
sudo cp /etc/bind/db.127 /etc/bind/db.31.172
sudo nano /etc/bind/db.31.172
```

```
$TTL 3600
@  IN SOA ns.desplegando123.com. admin.desplegando123.com. (
          2026102101    ; serial
          7200          ; refresh
          3600          ; retry
          1209600       ; expire
          86400 )       ; minimum TTL
;
@        IN NS  ns.desplegando123.com.
;
218.10   IN PTR ns.desplegando123.com.
```

```bash
sudo named-checkzone 31.172.in-addr.arpa /etc/bind/db.31.172    # OK
```

- **`218.10`** son los **dos últimos números de TU IP privada, del revés**: si tu IP es `172.31.4.77`, el registro es `77.4`.
- **Qué va en el nombre de la zona y qué en el registro** (guía): la **red** va al revés en el **nombre de la zona** (`31.172`) y el **host** va al revés en el **registro** (`218.10`). La dirección completa del revés es `218.10.31.172.in-addr.arpa.`, que es lo que pregunta `dig -x`.
- **¿Cuántos octetos?** Lo marca la **máscara**: tantos octetos en el nombre de la zona como octetos de red. `/16` = 2, `/24` = 3, `/8` = 1. La VPC de AWS es `172.31.0.0/16` → 2 octetos (guía).

> [!warning] Discrepancia con la clase
> En directo el profesor dijo "máscara `/24`" y a la vez "me quedo con los 2 primeros octetos". Es contradictorio: con `/24` serían 3. La guía dice **`/16`** y es lo coherente con 2 octetos. Quédate con la regla de la máscara.

- **Qué se registra como PTR**: un PTR por cada **host con registro A/AAAA** (`ns`, `correo`...), apuntando a su nombre completo y acabado en punto. **No** se hace PTR de los alias CNAME (`www`): el profesor, ante la pregunta de una alumna, lo dijo expresamente.
- Es la zona de la IP **privada**. La inversa de una IP **pública** la manda quien es dueño del bloque (Amazon): en AWS se pide por soporte. Por eso aquí se monta solo "para aprender a escribirla" y se prueba contra tu propio servidor (guía).

## Paso 6 · Autoritativo sí, recursivo no (solo guía)

```bash
sudo nano /etc/bind/named.conf.options
```

Justo debajo de `options {` se añaden dos líneas:

```
options {
        recursion no;
        allow-query { any; };
        directory "/var/cache/bind";
        ...el resto, tal como está
```

```bash
sudo named-checkconf
```

> [!note] Esto no se hizo en clase
> En la grabación no se toca `named.conf.options`; sale solo en la guía.

Por qué (guía): el servidor es **autoritativo** (tiene el original de la zona) pero **no recursivo** (no resuelve Internet entera para quien pregunte). Un recursivo abierto en IP pública se usa en horas para **ataques de amplificación**: alguien manda consultas pequeñas con la IP de la víctima falsificada y las respuestas, grandes, se las come la víctima. Con `recursion no` quedas como autoritativo y nada más. En los resultados lo verás: la cabecera lleva el flag **`aa`** (respuesta autoritativa) y el aviso *«recursion requested but not available»*, y son justo lo que se busca.

> [!note] Matiz con el temario
> El ejercicio del temario (Tema 3, Entrenamiento 3) enseña a habilitar la recursión en `named.conf.options` para un servidor que resuelva cualquier dominio. No contradice a la guía: **depende de qué papel quieras para el servidor**. Hoy es autoritativo.

## Paso 7 · Comprobar y arrancar

```bash
sudo named-checkconf
sudo named-checkzone desplegando123.com /etc/bind/db.desplegando123.com
sudo named-checkzone 31.172.in-addr.arpa /etc/bind/db.31.172

sudo systemctl restart named
sudo systemctl status named --no-pager           # active (running)
sudo ss -ulpn | grep :53                         # named escuchando en el 53
sudo journalctl -u named -n 30 --no-pager        # si algo falla, el motivo está aquí
```

- Orden: **primero los comprobadores, después reiniciar** ("la diferencia entre una tarde tranquila y una buscando a ciegas").
- En `ss` verás también un proceso en `127.0.0.53`: es el resolvedor del propio sistema (`systemd-resolved`, guía) y no estorba. Si en el log sale «address in use» con esa dirección, se ignora. En clase el profesor lo describió como "los otros son de AWS", pero la guía lo atribuye a systemd-resolved.
- Truco de terminal de clase: `history` y `!24` repite el comando nº 24; un compañero (Manuel) recomendó **Ctrl+R** y teclear el principio del comando para recuperarlo sin copiar y pegar.

## Paso 8 · Preguntarle a tu servidor

Con `host` el servidor va **al final**; con `dig` va **delante con `@`**. Donde pone `ZONA`, tu dominio.

**A) Desde la propia máquina (al DNS local, `127.0.0.1`):**

| Quiero ver | `host` (rápido) | `dig` (detalle) |
|---|---|---|
| SOA | `host -t soa ZONA 127.0.0.1` | `dig @127.0.0.1 ZONA SOA +multiline` |
| Dirección (A) | `host ZONA 127.0.0.1` | `dig @127.0.0.1 ZONA A +short` |
| `www` (CNAME) | `host www.ZONA 127.0.0.1` | `dig @127.0.0.1 www.ZONA +short` |
| Correo (MX) | `host -t mx ZONA 127.0.0.1` | `dig @127.0.0.1 ZONA MX +short` |
| Texto (TXT) | `host -t txt ZONA 127.0.0.1` | `dig @127.0.0.1 ZONA TXT +short` |
| Servidores (NS) | `host -t ns ZONA 127.0.0.1` | `dig @127.0.0.1 ZONA NS +short` |
| Inversa (PTR) | `host 172.31.10.218 127.0.0.1` | `dig @127.0.0.1 -x 172.31.10.218 +short` |

En Windows: `nslookup -type=soa ZONA 127.0.0.1` (servidor también al final).

**B) Desde tu portátil, por Internet** (la prueba de verdad):

```bash
host desplegando123.com <ELASTIC-IP>
dig @<ELASTIC-IP> desplegando123.com A +short
dig @<ELASTIC-IP> desplegando123.com SOA
```

Qué deberías ver (guía): el SOA con sus cinco números; tu Elastic IP en el A; en `www` **dos líneas** (primero el CNAME, luego la IP a la que lleva); el MX con su `10`; y en la inversa el nombre de tu servidor.

> [!warning] Dos advertencias
> - **No pongas `127.0.0.1` como resolvedor del sistema** (resolv.conf/systemd-resolved). Tu BIND no es recursivo: la máquina solo resolvería tus zonas y dejaría de resolver el resto de Internet (te fallaría hasta `apt`). Preguntar con `@127.0.0.1` está bien. Para ver a quién pregunta la máquina por defecto: `resolvectl status` (sale el `172.31.0.2` de la VPC).
> - **Si desde dentro funciona y desde fuera no, el problema no es BIND: es el Security Group.** Faltan las dos reglas del 53, o falta la UDP.

En clase el profesor probó contra `127.0.0.1` el SOA, el NS, el TXT y la inversa: el SOA y el NS respondieron bien, y en alguna consulta (TXT o inversa; el audio no deja claro cuál ni de quién) apareció un error que atribuyó a un punto final olvidado. Después, varios compañeros no obtenían respuesta de `host -t ns` **desde fuera** y el profesor concluyó que **no había propagado todavía**: "hay que esperar, probarlo mañana".

## Paso 9 · La transferencia de zona

```bash
dig axfr desplegando123.com @<ELASTIC-IP>     # la zona entera, por TCP
dig axfr unir.net @ns1.unir.net               # REFUSED, y así debe ser (solo guía)
```

- Un **secundario** pediría la zona así; con `dig` hacemos lo mismo. Sale la zona **registro a registro, empezando y acabando por el SOA**, y al pie `XFR size: N records` y `(TCP)`: las transferencias van por **TCP**, por eso hacían falta las dos reglas.
- El apex debe salir `desplegando123.com.` **sin `ns.` delante** (comprobación del fallo número uno).
- Un dominio de verdad responde **REFUSED/Transfer failed**, y está bien: un AXFR abierto entrega a cualquiera el mapa completo de la red. Aquí queda abierto solo por la práctica.
- En clase un compañero (Adri) obtuvo *"transfer failed"*. No se resolvió en directo. Según la tabla de la guía, las causas habituales son que falte `allow-transfer { any; };` en la zona o la regla **TCP** del 53 (esto es la guía, no lo comprobó el profesor).
- **Replicación** (guía, fondo): un dominio serio tiene un **primario** (`type master`) y uno o varios **secundarios** que se copian la zona. El secundario mira el **serial** del SOA: si el del primario es mayor, pide la zona con un AXFR. Hoy no se monta secundario.

## Paso 10 · Comprobar la delegación

No se hace nada nuevo; **solo se comprueba** (la acción ya se lanzó en el 0b).

```bash
# 1) Contra tu servidor: responde ya, sin esperar a nada
host desplegando123.com <ELASTIC-IP>
dig @<ELASTIC-IP> desplegando123.com +short
dig @<ELASTIC-IP> desplegando123.com NS +short

# 2) Desde fuera, sin decir a quién preguntar (la delegación de verdad)
dig +trace desplegando123.com
dig desplegando123.com NS +short
# y en el navegador: whatsmydns.net, tu dominio, tipo NS
```

- Cuando la delegación haya propagado, `+trace` llega solo hasta el servidor delegado y el último «Received ... from» es **tu Elastic IP**. En clase el profesor lo recomendó expresamente: "importante haceros este `dig +trace`", y lo hizo sin éxito completo porque aún no había propagado.
- El registro que pone el registrador es el `@ IN NS ns.<dominio>.` y el `ns IN A <Elastic IP>`, que es el **glue** (registro de pegamento).

## Paso 11 · Cambiar algo (opcional) y por qué se sube el serial

```bash
sudo nano /etc/bind/db.desplegando123.com
#   añadir al final:   blog    IN  A   <ELASTIC-IP>
#   y SUBIR el serial: 2026102101 -> 2026102102
sudo named-checkzone desplegando123.com /etc/bind/db.desplegando123.com
sudo systemctl restart named
dig @127.0.0.1 blog.desplegando123.com +short
dig @127.0.0.1 desplegando123.com SOA +short       # ahora con el serial 2026102102
```

En tu propio servidor el cambio se ve **aunque no subas el serial**. Quien no se enteraría es un **secundario**. Por eso se sube siempre: para acostumbrarse (guía). En clase el profesor planteó la prueba de tocar un registro y ver el cambio.

## Si algo no funciona (guía)

| Lo que ves | Qué pasa y cómo se arregla |
|---|---|
| `named` no arranca | Casi siempre `named.conf.local`: una llave o un `;` de menos. `sudo named-checkconf` lo dice; el detalle, en `journalctl -u named -n 30 --no-pager` |
| Arranca, pero `dig` no devuelve nada | La zona no se cargó y el servidor no avisa. `named-checkzone <zona> <fichero>` da el nº de línea |
| El nombre sale repetido: `www.x.desplegando123.com.x.desplegando123.com` | Falta un **punto final** en el fichero de zona |
| `status: REFUSED` | Preguntas por una zona que no es suya. Al no ser recursivo, solo contesta por lo suyo, y está bien |
| Desde dentro va, desde fuera no | Security Group: faltan las dos reglas del 53 o la UDP |
| «address in use» con 127.0.0.53 en el log | Es systemd-resolved; ignorarlo |
| `dig axfr` dice «Transfer failed» | Falta `allow-transfer { any; };` en la zona, o falta la regla TCP del 53 |

## Repetirlo de cero en casa (guía)

```bash
sudo systemctl stop named
sudo apt purge -y bind9 bind9-utils
sudo rm -rf /etc/bind
sudo apt install -y bind9 bind9-utils bind9-dnsutils
```

La Elastic IP y el Security Group **no hace falta tocarlos**: siguen igual.

## Matices a tus apuntes

Lo que apuntaste está bien en lo esencial. Esto es lo que conviene afinar:

| Tu nota | Veredicto / matiz |
|---|---|
| "named es lo mismo que bind9" | Casi. **`named` es el demonio y `bind9` el paquete**; como nombre de servicio en `systemctl` valen los dos |
| "Archivos importantes: named.conf, .options y todos los db (plantillas)" | Los tres importantes son **`named.conf`** (solo incluye), **`named.conf.options`** y **`named.conf.local`**. Los `db.*` son ejemplos que se **copian**, no se rellenan en su sitio |
| "SOA indica quién lo gestiona... ¿por qué `admin.`?" | Indica el **servidor primario** y el **correo del admin con un punto en lugar de `@`** (`admin.dominio.` = `admin@dominio`). Si usaste `admin.ns1.<dominio>.`, equivale a `admin@ns1.<dominio>`: funciona, pero la guía usa `admin.<dominio>.` |
| "ns se registra con la IP pública" | Con la **Elastic IP** (la fija). Y distingue: el **registro NS** (`@ IN NS ns.dominio.`) dice **quién** es el servidor; el **registro A de `ns`** da su **IP** |
| "cname es para apuntar a dominios" | Correcto: apunta a un **nombre**, nunca a una IP. Límites: `@` no puede ser CNAME y el MX no puede apuntar a un CNAME |
| "zona inversa: PTR a los dominios (no txt ni CNAME, solo A o AAAA)" | Redacción confusa. La zona inversa **solo lleva PTR** (`IP → nombre`). Lo que dices es que **solo se hace PTR de los hosts que tienen A/AAAA**, no de los alias CNAME. Eso sí es cierto |
| "el ptr va al revés la IP, pero es el host, no la red" | Correcto. La **red** va al revés en el **nombre de la zona**; el **host** va al revés en el **registro** |
| *(no estaba)* | `named.conf.options` con `recursion no` y `allow-query` (paso 6), la comprobación con `ss`, el `dig axfr`, el `dig +trace` y **subir el serial** al cambiar la zona |
| `ns1.dbvlabme` | Entiendo que es `ns1.dbvlab.me`. Si usas `ns1`, ese nombre tiene que ser el mismo en el SOA, en el NS y en el A de tu zona |

## Dudas y cosas sin confirmar

- **Máscara**: el profesor dijo `/24` y 2 octetos a la vez; vale la guía (`/16`, 2 octetos).
- **Audio confuso**: al instalar, el profesor mencionó un paquete adicional con un nombre que la transcripción no recoge bien. La guía solo instala `bind9`, `bind9-utils` y `bind9-dnsutils`; usa esos.
- **Nombres de fichero**: en clase se usaron `db.ns` / `db.31.172`; la guía usa `db.desplegando123.com`. Es indiferente si coincide con `named.conf.local`.
- **No se vio en clase** (solo guía): `named.conf.options`/`recursion no`, `dig axfr unir.net`, el resultado de `+trace` ya propagado y la tabla de errores.
- **No se llegó a verificar desde fuera** el resultado real en clase: el profesor terminó esperando a la propagación. Lo comprobado en vivo fue `named-checkzone` en OK, `named` activo y escuchando en el 53, y `host`/`dig` locales.
- No he visto qué **entra en el examen** de este laboratorio. Lo que el profesor marcó el 20/10 es que de la parte teórica importan los campos del SOA y los tipos de registro; este laboratorio es la práctica de eso.

## Logística y para llevar a casa

- **Al acabar (guía):** EC2 → `srv_dns` → Instance state → **Stop** (nunca Terminate). **No liberar la Elastic IP**: se usa en el Tema 4 con el servidor web. En clase el profesor recomendó **dejar el servidor encendido hasta comprobar la propagación** ("lo dejaría encendido y probaría a última hora para ver si es viable"). Mi lectura de ambas cosas: déjalo encendido hasta verificar el `dig +trace` y entonces hazle Stop.
- **Guarda una copia de tus dos ficheros de zona** (`db.<dominio>` y `db.31.172`) y las **capturas**: te hacen falta para la **Actividad 1 (entrega lunes 16/11)**, y la guía dice que lo de hoy cubre su criterio 1.
- Pendiente tuyo: repetir el paso 10 cuando la delegación haya propagado (`dig +trace`, whatsmydns.net) y hacer una captura.
- Siguiente clase de SER: semana tranquila de comprobaciones y avance de teoría con práctica (el profesor, sin más detalle).
