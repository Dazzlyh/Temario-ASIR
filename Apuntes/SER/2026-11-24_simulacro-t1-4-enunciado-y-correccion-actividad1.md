---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-11-24
tema: "Simulacro de los Temas 1 a 4 (enunciado, guía de estudio y repaso del profesor) y corrección comentada de la Actividad 1"
fuente: PDFs del profesor recibidos el 25/11: SER_Simulacro_T1-4.pdf (5 págs., enunciado en blanco), SER_Simulacro_Guia_estudio.pdf (3), SER_Repaso_T1-4.pdf (3), SER_Repaso_T1-4_Presentacion.pdf (13) y SER_Actividad1_Correccion.pdf (1). No tengo la grabación del 24/11 ni la corrección oral del simulacro. Las respuestas de la hoja final son mías, derivadas de los PDFs del repaso (no hay clave oficial).
---
# SER · Simulacro T1-4 (martes 24/11) y corrección de la Actividad 1

> Anterior: [Repaso del 17/11: dibujos, zonas y comandos](2026-11-17_repaso-simulacro-dibujos-dns-apache-https.md) · Profesor: Damián Sualdea Soy

Convención: **(PDF)** = documento del profesor, **(mío)** = añadido o deducido por mí, **(web)** = conocimiento general no contrastado en esta sesión.

> [!important] Lo imprescindible
> - **Formato (PDF):** 60 min, sin ordenador, sobre papel, **no cuenta nota**. Test 15 × 0,2 = **3 puntos**; 3 cortas × 1 = **3**; 4 casos prácticos × 1 = **4**. Reparto sugerido: ~15 min test, 15 cortas, 20 casos. **El test no penaliza: contesta siempre.** Es «el mismo formato del examen de mayo».
> - **Casos (PDF):** leer una **zona DNS**, leer un **VirtualHost**, explicar **4 comandos** y **dibujar** un servidor con Elastic IP que es DNS y web a la vez, con tres sitios, un cliente por nombre y **leyenda**.
> - **Dónde estudiar (PDF):** T1 → Clases 2 y 3 + Lab 1; T2 → Clase 4 + Lab 2; T3 → Clases 5 y 6 + Lab 3; T4 → Clases 7 y 8, Lab 4 y Clase 9. «Si sabes montar y leer [DNS → Apache → VirtualHost → HTTPS], el simulacro te sale.»
> - **Actividad 1:** la corrección dice que el fallo más repetido fue **dejar la URL en `http` tras activar HTTPS**.

## Qué dicen los PDFs de repaso (resumen contra mi nota del 17/11)

| Tema | Entra (PDF) | Diferencia con el audio del 17/11 |
|---|---|---|
| 1 | Rangos de puertos; NAT estático/dinámico/**PAT**; TCP (fiable, saludo SYN, SYN-ACK, ACK) frente a UDP; OSI 7 capas y TCP/IP 4; IPv4 32 bits, IPv6 128 | El audio no citaba el saludo de 3 pasos ni IPv4/IPv6: **sí entran** |
| 2 | DORA; ámbito, exclusión, reserva (IP fija por MAC) y concesión (*lease*); Ubuntu 24.04 usa `systemd-networkd`/netplan, no `dhclient` | El audio decía «solo el DORA»: los conceptos **también** |
| 3 | Registros A, AAAA, CNAME, MX, NS, TXT, PTR; leer una zona; directa frente a inversa | Coincide |
| 4 | `/var/www/html`, módulos (`a2enmod`), VirtualHost por nombre y cabecera `Host:`, `a2ensite` + reload, 80/443, GET, **autenticación básica = texto plano**, Certbot | La autenticación básica **sí** sale (pregunta 15), aunque `htpasswd` «no entre» como práctica |

**Comandos (PDF):** `host`, `host -t mx`, `host -t ns`, `dig +short`, `named-checkzone`, `a2ensite`, `systemctl reload apache2`, `curl -I`, `certbot --apache -d`.

> [!warning] Erratas del temario que «avisó» el profesor (PDF)
> `DHCPRELEASE` **no** es un registro DNS (es un mensaje de DHCP); **«HTTP 1.2» no existe** (las versiones son 1.1, 2 y 3); el subtítulo «Servidor DNS» del 4.3 debe decir «Servidor web». «Para el examen vale lo del temario, pero conviene saberlo.» **(Mío)** Si una pregunta de test te pone `DHCPRELEASE` entre los registros, no sé cuál querrá el corrector: yo marcaría lo correcto técnicamente y lo anotaría; **sin confirmar**.

---

# Corrección comentada de la Actividad 1 (PDF, 1 página)

Entregada el 16/11. Pesos (sobre 10): DNS 15 %, tres VirtualHost 10 %, HTTPS 10 %, WordPress 20 %, segundo CMS 20 %, `index.html` con IA 10 %, documentación 15 %. **Es el mismo reparto que ya constaba en las diapositivas del 3/11.** No trae notas ni la tuya.

| Criterio | Fallos que más restaron (PDF) | Cómo evitarlo |
|---|---|---|
| **DNS (15 %)** | Usar el archivo `hosts` en vez de un dominio real; **no subir el serial** al cambiar la zona; **faltar el TXT** | `host`/`dig` resolviendo a tu IP; serial +1 |
| **3 VirtualHost (10 %)** | Los tres sitios dan la misma página: falta `a2ensite` + reload, o `ServerName` repetido. **Desactivar `000-default.conf`** | `a2dissite 000-default.conf`, `configtest` |
| **HTTPS (10 %)** | **443 cerrado** en el grupo de seguridad; lanzar Certbot **antes de que propague** el dominio | Certbot valida por el 80 y sirve por el 443: ambos abiertos |
| **WordPress y 2.º CMS (20 % c/u)** | **URL en `http` tras activar HTTPS**: WordPress *Ajustes → Generales*; Moodle `$CFG->wwwroot` en `config.php`. **`moodledata` dentro del árbol web** (debe ir fuera). Extensiones de PHP sin instalar | Ver [Lab 4](2026-11-04_laboratorio4-wordpress-php-mariadb.md) |
| **`index.html` con IA (10 %)** | Tenía que estar hecho con IA **e indicarlo** (decir que se generó con IA y, mejor, **qué se pidió**) | Pon el *prompt* en la documentación |
| **Documentación (15 %)** | Sin capturas ni explicar decisiones, la nota baja | «El qué y el porqué» |

> [!important] Lo que te llevas (PDF)
> El orden salva la actividad: **DNS → Apache → VirtualHost → probar por el 80 → HTTPS**. Y al activar HTTPS, **cambia la URL del sitio a https**.

> [!warning] Contradicción con la clase del 10/11
> En clase el profesor creó `moodledata` en `/var/www/html/moodledata` (dentro de la carpeta pública), pero esta corrección lo cuenta como fallo. **Manda el PDF**, como ya recogen la guía del Lab 4 y su nota: `/var/moodledata`, `0770`.

---

# Simulacro del 24/11: enunciado (para practicar)

> Primero el enunciado completo; **mis respuestas están al final**. Hazlo a mano en 60 min sin mirar.

## Bloque 1 · Test (15 × 0,2)

1. Rango de puertos «bien conocidos»: a) 0–1023 · b) 1024–49151 · c) 49152–65535 · d) 1–65535.
2. Muchos equipos de una red privada salen con UNA IP pública, distinguidos por el puerto: a) NAT estático · b) PAT (NAT con sobrecarga) · c) NAT uno a uno · d) un proxy.
3. El modelo OSI tiene: a) 4 capas · b) 5 · c) 7 · d) 3.
4. Una dirección IPv6 mide: a) 32 bits · b) 48 · c) 64 · d) 128.
5. El tiempo que el servidor DHCP cede una dirección: a) concesión (lease) · b) exclusión · c) difusión · d) reserva.
6. Dirección fija que el DHCP entrega siempre al mismo equipo según su MAC: a) exclusión · b) ámbito · c) reserva · d) concesión.
7. Registro DNS nombre → IPv6: a) A · b) AAAA · c) PTR · d) CNAME.
8. Registro DNS IP → nombre (inversa): a) A · b) PTR · c) CNAME · d) MX.
9. Comando que pregunta por el MX: a) `host -t mx dominio` · b) `ping dominio` · c) `ss -t dominio` · d) `ip route dominio`.
10. `dig +short desplegando123.com` muestra: a) la ruta de red · b) solo la IP a la que resuelve · c) los puertos abiertos · d) el estado del servicio DNS.
11. Carpeta que sirve Apache por defecto en Ubuntu: a) `/var/www/html` · b) `/etc/apache2` · c) `/home/www` · d) `/srv/web`.
12. Comando que activa un VirtualHost: a) `named-checkzone` · b) `a2ensite` · c) `systemctl dns` · d) `htpasswd`.
13. Método HTTP que pide un recurso para mostrarlo: a) GET · b) POST · c) DELETE · d) PUT.
14. Un servidor web sirve HTTP en el puerto: a) 22 · b) 53 · c) 80 · d) 67.
15. La autenticación básica de Apache envía usuario y contraseña: a) cifrados con MD5 · b) en texto plano (base64) · c) dentro de un certificado · d) no los envía nunca.

## Bloque 2 · Cortas (3 × 1; 3-4 líneas cada una)

- **A.** Diferencia entre TCP y UDP y un servicio de cada uno.
- **B.** Proceso DORA: qué hace cada uno de los cuatro mensajes.
- **C.** Qué es un VirtualHost de Apache y por qué permite varias webs con una sola IP.

## Bloque 3 · Casos prácticos (4 × 1)

**D. Zona DNS** (`/etc/bind/db.desplegando123.com`):

```
$TTL 86400
@     IN SOA dns1.desplegando123.com. admin.desplegando123.com. (
          2026112402 ; serial
          3600 ; refresh
          1800 ; retry
          1209600 ; expire
          86400 ) ; minimum
@     IN NS    dns1.desplegando123.com.
@     IN NS    dns2.desplegando123.com.
@     IN MX 10 mail.desplegando123.com.
@     IN A     184.197.19.142
@     IN TXT   "v=spf1 mx -all"
dns1  IN A     184.197.19.142
dns2  IN A     184.197.19.150
mail  IN A     184.197.19.142
www   IN CNAME desplegando123.com.
blog  IN A     184.197.19.142
aula  IN A     184.197.19.142
```
1. ¿A qué IP resuelve `aula.desplegando123.com`? ¿Y `www.desplegando123.com` (fíjate en su tipo de registro)?
2. ¿Qué hacen la línea MX y la TXT con `"v=spf1 mx -all"`?

**E. VirtualHost** (`/etc/apache2/sites-available/desplegando123.com.conf`):

```apache
<VirtualHost *:80>
    ServerName desplegando123.com
    ServerAlias www.desplegando123.com
    ServerAdmin admin@desplegando123.com
    DocumentRoot /var/www/html/desplegando123.com
    <Directory /var/www/html/desplegando123.com>
        Options -Indexes +FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/desplegando123_error.log
    CustomLog ${APACHE_LOG_DIR}/desplegando123_access.log combined
</VirtualHost>
```
1. ¿Qué nombres atiende y desde qué carpeta?
2. ¿Qué hacen `Options -Indexes` y `AllowOverride All`?
3. Está en el 80: ¿qué pasos darías para servirlo también por HTTPS?

**F. Comandos:** explica cada uno: (1) `host -t ns desplegando123.com` · (2) `named-checkzone desplegando123.com /etc/bind/db.desplegando123.com` · (3) `sudo systemctl reload apache2` · (4) `curl -I http://desplegando123.com`.

**G. Dibujo:** un único servidor con Elastic IP que es DNS (BIND9) y web (Apache), tres sitios (principal, `blog`, `aula`) y un cliente que accede por nombre (primero al DNS, luego HTTP/HTTPS). **Con leyenda.**

---

# Mis respuestas (sin clave oficial; derivadas de los PDFs del repaso)

## Test

1-a · 2-b · 3-c · 4-d · 5-a · 6-c · 7-b · 8-b · 9-a · 10-b · 11-a · 12-b · 13-a · 14-c · 15-b.

## Cortas (esqueleto)

- **A.** **TCP**: orientado a conexión y fiable (saludo de 3 pasos SYN, SYN-ACK, ACK; garantiza entrega y orden): web, correo, SSH. **UDP**: sin conexión ni garantías, rápido y ligero: DNS, DHCP, streaming.
- **B.** **Discover**: el cliente, sin IP, pregunta por la red si hay servidor DHCP. **Offer**: el servidor ofrece una dirección libre. **Request**: el cliente pide esa dirección. **Ack**: el servidor confirma y entrega la concesión.
- **C.** Un VirtualHost es una configuración que permite a un mismo Apache servir varios sitios. Con una sola IP, Apache mira la cabecera `Host:` (el nombre que pide el navegador), la compara con el `ServerName`/`ServerAlias` de cada VirtualHost y sirve el `DocumentRoot` correspondiente. Por eso hace falta el DNS: los nombres resuelven todos a la misma IP.

## D · Zona

1. **`aula` → 184.197.19.142** (registro A directo). **`www` es un CNAME**: alias del dominio principal, no tiene IP propia; se resuelve a `desplegando123.com.` y de ahí a **184.197.19.142** (un salto más).
2. **MX 10:** el correo del dominio lo recibe `mail.desplegando123.com.` (el 10 es la prioridad; menor = antes), que resuelve por su A a 184.197.19.142. **TXT SPF** *(mío; el PDF solo dice «TXT, p. ej. SPF»)*: solo los servidores listados en el MX del dominio pueden enviar correo en su nombre (`mx`), y `-all` rechaza el resto (fallo duro).
- *Detalles que puede pedir el examen (mío):* serial `2026112402` (formato fecha + nº; se sube al cambiar); dos NS (`dns1` y `dns2`); **`dns2` tiene otra IP (.150)**, así que el secundario está en otra máquina; el punto final de los FQDN.

## E · VirtualHost

1. Atiende **`desplegando123.com` y `www.desplegando123.com`** (por `ServerAlias`), desde **`/var/www/html/desplegando123.com`**.
2. **`Options -Indexes`** *(mío)*: desactiva el listado de la carpeta cuando no hay `index` (el «Index of /» que se vio el 3/11). **`+FollowSymLinks`**: sigue enlaces simbólicos. **`AllowOverride All`**: permite que un `.htaccess` de esa carpeta sobrescriba cualquier directiva (la guía de «proteger un sitio» usa `AuthConfig` para limitarlo a autenticación; `All` es más permisivo y Apache lo relee en cada petición). `Require all granted`: acceso para todos. `ServerAdmin`: contacto; `ErrorLog`/`CustomLog`: ficheros de log de errores y accesos.
3. **HTTPS:** que el dominio resuelva y el sitio responda por el 80; abrir **443** en el grupo de seguridad; `sudo apt install -y certbot python3-certbot-apache`; `sudo certbot --apache -d desplegando123.com -d www.desplegando123.com`; aceptar la **redirección HTTP→HTTPS**. Certbot crea el VirtualHost `:443` con el certificado; probar `https://` y `sudo certbot renew --dry-run`.

## F · Comandos

1. Pregunta al DNS por los **registros NS** del dominio: qué servidores de nombres lo gestionan.
2. **Comprueba que el fichero de zona está bien escrito** (sintaxis y coherencia) para la zona `desplegando123.com`, **antes** de recargar BIND.
3. **Recarga la configuración de Apache sin cortar el servicio** (tras cambiar un sitio).
4. Pide **solo las cabeceras HTTP** (código 200/301/404…, servidor, etc.), sin descargar la página. *(Mío, (web): `-I` hace una petición HEAD.)*

## G · Dibujo (esqueleto)

```
Cliente ──(1) ¿blog.desplegando123.com? (UDP 53)──▶ Servidor con Elastic IP <IP>
        ◀─(2) A: <IP> ───────────────────────────  ├─ BIND9 (DNS, :53): zona desplegando123.com
Cliente ──(3) HTTP :80 / HTTPS :443, Host: blog… ─▶ └─ Apache (web)
                                                         ├─ desplegando123.com      → /var/www/html/desplegando123.com
                                                         ├─ blog.desplegando123.com → /var/www/html/blog.desplegando123.com
                                                         └─ aula.desplegando123.com → /var/www/html/aula.desplegando123.com
LEYENDA: flechas numeradas = orden de la consulta; :53 DNS, :80 HTTP, :443 HTTPS; <IP> = Elastic IP
```
Se corrige **por elementos y conexiones**, no por el arte (17/11).

---

## Sin confirmar / sin recibir

- **Corrección y nota del simulacro del 24/11** (qué respondió el profesor, qué falló la clase): sin recibir la grabación.
- **Clave oficial de las respuestas:** no hay; las de arriba son mías.
- **Tu nota de la Actividad 1:** no consta en ningún PDF.
- **Si el examen de mayo es igual** que el simulacro: lo dice el profesor; no lo he visto.
- **Examen de mayo y `DHCPRELEASE`:** ver aviso arriba.
