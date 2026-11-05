---
asignatura: Servicios en Red e Internet
fecha: 2026-11-03
tema: "Tema 4 · Clase 8: requisitos DNS de la Actividad 1, instalar Apache, abrir el puerto 80 y sitios virtuales (virtual hosts) por nombre"
fuente: transcripción de la clase (1 h 27 min). Sin documentos nuevos (Dani). El profesor usó un documento de comandos y un Prezi que no tengo; contrastado con el material de la Clase 7 y con el Tema 4 del temario (4.5).
---
# SER · Clase 8 (3/11) · DNS para la Actividad 1 + Apache + virtual hosts

> Anterior: [Clase 7 (27/10): correcciones del Lab 3 e intro al servidor web](2026-10-27_correcciones-lab3-dns-e-intro-servidor-web.md) · Profesor: Damián Sualdea Soy

Clase práctica, de las "técnicas": se monta un servidor web desde cero sobre la misma máquina del Lab 3. Primero se aclara qué hay que entregar del DNS en la **Actividad 1**, luego se instala **Apache**, se abre el firewall y se llega a los **sitios virtuales por nombre**. WordPress y PHP no se hicieron: quedan para el Laboratorio 4 (4/11).

> [!important] Lo imprescindible
> - **Actividad 1: entrega el lunes 16 de noviembre.** El profesor creía que era el 9 y se corrigió en directo ("creía que era el 9… vale, entonces voy perfecto"). Esto zanja mi duda anterior: el "día 9" que oí en la clase de Ciber era un lapsus suyo.
> - **BIND9 solo tiene que funcionar una vez** para que te puntúe la parte de DNS. Después puedes volver al DNS de tu registrador (Namecheap, IONOS…) para el resto de la actividad.
> - **O BIND9, o el DNS del registrador. Nunca los dos a la vez.** Quien responde es el servidor de nombres que tenga delegado el dominio.
> - **Apache**: `sudo apt install apache2 -y`, y en el **Security Group** abrir el **80 TCP** (y más adelante el **443 TCP**).
> - **Un virtual host = un fichero en `sites-available` + una carpeta + `a2ensite` + `reload`.** Solo se tocan dos directivas: **`ServerName`** y **`DocumentRoot`**.
> - Para comprobar en el navegador, escribe **`http://`** a mano: hoy no hay HTTPS y muchos navegadores intentan `https://`.

---

## Tarea 1 · El DNS de la Actividad 1

### Qué hay que enseñar

Lo dijo el profesor al empezar y lo repitió al responder una duda:

1. **Dominio principal** apuntando a tu IP (el que ya tienes del Lab 3).
2. **Un subdominio `blog`** apuntando a tu IP.
3. **Un tercer dominio/subdominio** "como os dé la gana" (él puso `moodle`, "academia"). También a tu IP.
4. **Un registro TXT** en el dominio principal con el texto que quieras. Ejemplo suyo: *"Actividad 1, parte 1 realizada"*.

Todo con **evidencias**: capturas y la salida de `host`/`dig`. "Con que hagáis estos tres me vale", y con que "yo vea que funciona".

> [!warning] Sin confirmar
> No tengo el enunciado de la Actividad 1, solo lo que se oyó. No sé cuántos puntos tiene ni si el TXT lleva algún texto obligatorio (el audio sugiere que se menciona al profesor; no está claro). Cuando lo tengas, compruébalo contra él.

### Cómo se hace en BIND9 (lo que demostró en directo)

Sobre su servidor DNS, dentro de `/etc/bind`:

```bash
sudo systemctl status bind9          # (clase) comprobar que el servicio está en marcha
cd /etc/bind
ls
sudo nano db.<tu-dominio>            # zona directa (el nombre exacto es el que usaste en el Lab 3)
```

Registros que añadió (misma sintaxis que el Lab 3; la IP es la de **tu servidor web**):

```
blog     IN  A    <ELASTIC-IP>
moodle   IN  A    <ELASTIC-IP>
@        IN  TXT  "Actividad 1, parte 1 realizada"
```

Y los **PTR** de los nuevos nombres en la zona inversa (`sudo nano db.<tu-zona-inversa>`), con el **punto final** de cada FQDN:

```
<último-octeto>   IN  PTR  blog.<tu-dominio>.
<último-octeto>   IN  PTR  moodle.<tu-dominio>.
```

Después reinició (`sudo systemctl restart bind9`; el audio dice "restart", que tardó) y comprobó:

```bash
host -t TXT <tu-dominio>             # (clase) ver el registro TXT
host blog3.<tu-dominio>              # (clase) ver que un subdominio resuelve
```

> [!note] Punto por detalle
> La IP de los registros es la **pública del servidor web**. Con Elastic IP no cambia; si no, mírala siempre en EC2 → Instancias → Detalles. Al profesor se le coló una cifra mal al dictarla y tuvo que volver a mirarla. Cualquier IP mal escrita hace que el dominio apunte a otro sitio.

### Volver al DNS del registrador

Lo hizo en vivo con IONOS para enseñar que es posible:

1. En el panel del registrador, en la gestión de DNS del dominio, **restablecer** los servidores de nombres a los **por defecto** del registrador ("le doy a restablecer, y ya está").
2. A partir de ahí los registros se crean **en el panel del registrador**: **añadir registro → tipo A → nombre → IP**. "Es igual": el mismo A, los mismos campos, solo que en una web.
3. Hay que esperar la **propagación**; mientras tanto el nombre nuevo puede no resolver.

> [!important] La idea que le costó dos explicaciones
> - El registrador decide **quién gestiona el DNS** del dominio: o tus servidores (`ns.<dominio>`, que son tu BIND9) o los suyos por defecto.
> - Si vuelves a los del registrador, tu BIND9 **sigue funcionando pero nadie le pregunta**. "Yo, ahora mismo, **cerraría el puerto 53**, pararía mi servicio BIND9 y no lo utilizaría más."
> - Lo que hiciste a mano con BIND9 en consola **es lo mismo que se hace desde la web** del registrador. "Exactamente es lo mismo."
> - **No puedes tener las dos configuraciones activas**: "o haces una o la otra".

Esto es consistente con lo que ya anoté en el [Lab 3](2026-10-21_laboratorio3-dns-bind9.md): la delegación y el *glue* los lleva el registrador.

### Problema típico visto en directo

Una compañera que usa Namecheap veía en el navegador una página que no era la de su servidor. Causa: el registro A de su dominio apuntaba a **otra IP** (restos de los registros por defecto). Solución: en el panel de Namecheap, **cambiar el registro A a la IP de tu servidor**. Otra compañera no veía un subdominio en su equipo pero sí desde otras máquinas: era la **caché DNS local**, "funciona perfectamente".

---

## Tarea 2 · Instalar Apache y abrirle el puerto

### Instalación

El profesor creyó que ya estaba instalado y no: `systemctl status apache2` salió "not found" (al menos en el de una compañera). En la clase anterior solo se había hecho la parte conceptual (HTTP, `curl`).

```bash
sudo apt install apache2 -y          # (clase) -y = responde "sí" a todo
sudo systemctl status apache2        # (clase; mío el sudo) ver que está "active (running)"
```

### Firewall: el Security Group de AWS

Hasta hoy el grupo de seguridad solo permitía **SSH (22)** y **DNS (53)**. Con eso Apache no se ve desde fuera.

1. EC2 → tu instancia → pestaña **Seguridad** → **grupo de seguridad** → **Editar reglas de entrada** → **Agregar regla**.
2. Tipo **HTTP** (aparece el **puerto 80, TCP**), origen **Anywhere / 0.0.0.0/0**. Guardar.
3. Para HTTPS será otra regla, **HTTPS 443 TCP** (el profesor dijo que "los dos van por TCP").

> [!note] Por qué hoy solo el 80
> Una compañera preguntó por qué no añadir ya las dos reglas. Respuesta del profesor: "a nivel didáctico" y porque el HTTPS lo hará "el proceso entero" más adelante (según el material de la Clase 7, en la Clase 9). Mío: nada impide abrir las dos ahora.

### Comprobar que funciona

```bash
# en el navegador, con http:// escrito a mano:
http://blog3.<tu-dominio>
# debe salir la página por defecto de Apache
```

- Si no sale: mira primero **dónde apunta el dominio** (`host <nombre>` debe dar tu IP) y luego el puerto 80.
- Mío: una comprobación sin navegador es `curl -I http://<tu-dominio>` (visto en el [material de la Clase 7](2026-10-27_correcciones-lab3-dns-e-intro-servidor-web.md)).

---

## Tarea 3 · La carpeta pública, `index.html` y una página de prueba

La página de Apache está en **`/var/www/html`** y el fichero principal es **`index.html`**.

```bash
cd /var/www/html
ls                                   # (clase) aparece index.html
sudo rm index.html                   # (clase) borrarlo; el profesor lo hizo para enseñar qué pasa
```

Sin `index.html`, el navegador enseña una **página de listado ("Index of /")**: Apache muestra los ficheros de la carpeta. El profesor lo señaló como un fallo ("te muestra todos los que quieres… te dice que no hay nada"). Mío: si en un servidor real hay ficheros sin `index`, quedan a la vista; por eso conviene tener siempre un `index`.

```bash
sudo nano index.html                 # (clase) crear uno nuevo y pegar el HTML
# Ctrl+O, Enter, Ctrl+X              # guardar y salir
ls                                   # ahora aparece index.html
```

- Tuvo que usar `sudo`: una compañera no podía escribir en esa carpeta ("no me lo permite") y la respuesta fue `sudo`.
- Recomendó pedirle a una **IA** una página web completa (un solo HTML con su CSS), copiar el código fuente y pegarlo en el `nano`. Su ejemplo: una web sobre Chuck Norris. Pide que meta el CSS **en el mismo fichero**, para no tener que montar carpetas de estilos.
- Resultado: tu dominio principal sirve esa página.

---

## Tarea 4 · Virtual hosts por nombre

### La idea

Varios dominios o subdominios apuntan a **la misma IP**; **Apache decide a qué carpeta mandar** según el nombre que pidió el navegador.

```
 navegador ──► DNS ──► una sola IP ──► Apache ──┬─ <dominio>        → /var/www/html
 (blog3.dom)                                    └─ blog3.<dominio>  → /var/www/blog3.<dominio>
```

- Tienen que existir antes en el **DNS** los registros A de cada subdominio (Tarea 1). "Tengo un montón de dominios que apuntan al mismo lado. Eso no importa."
- Esta es la técnica **basada en nombre**, la que se trabajó. El temario (4.5) describe tres: **por nombre** (FQDN; "la más popular"), **por puerto** (80, 8080, 9090…; hay que abrir cada puerto en el firewall) y **por dirección IP** (necesita varias IP o tarjetas; la menos popular).

### Dónde está la configuración

Todo en **`/etc/apache2`**:

```bash
cd /etc/apache2
ls
ls -l sites-available                # configuraciones disponibles: 000-default.conf y default-ssl.conf
ls -l sites-enabled                  # solo los activos; salen con una flecha ->
```

| Carpeta | Qué contiene |
|---|---|
| `sites-available/` | Los ficheros de configuración de **todos** los sitios (activos o no) |
| `sites-enabled/` | Un **enlace simbólico** (en el listado `ls -l` sale con `->`) a cada sitio que está **activo** |

El profesor lo comparó con un acceso directo y precisó que es un enlace **simbólico, "blando"**. Por eso se crea en `sites-available` y se *activa* después.

### Crear un virtual host (un subdominio)

1. **Copiar el fichero por defecto** con el nombre del sitio. Él usa el subdominio + dominio + `.conf` (el nombre es libre, pero este convenio ayuda):

```bash
cd /etc/apache2/sites-available
sudo cp 000-default.conf blog3.<tu-dominio>.conf
ls                                   # ahora hay dos
```

2. **Editarlo** y tocar solo dos directivas:

```bash
sudo nano blog3.<tu-dominio>.conf
```

```apache
ServerName    blog3.<tu-dominio>             # el nombre con el que llega la petición
DocumentRoot  /var/www/blog3.<tu-dominio>    # la carpeta a la que se manda
```

3. **Crear la carpeta** y su `index.html`. La carpeta **no existe** hasta que la haces tú:

```bash
sudo mkdir /var/www/blog3.<tu-dominio>
cd /var/www/blog3.<tu-dominio>
sudo nano index.html                 # p. ej. un <h1>Soy blog3.<tu-dominio></h1>
```

4. **Activar el sitio** y recargar Apache:

```bash
sudo a2ensite blog3.<tu-dominio>.conf     # (clase; también vale sin .conf)
sudo systemctl reload apache2             # lo pide el propio a2ensite
```

5. **Comprobar:** `ls -l /etc/apache2/sites-enabled` ahora muestra el nuevo enlace. En el navegador, `http://blog3.<tu-dominio>` enseña el `<h1>`; el dominio principal sigue enseñando la página de Chuck Norris.

> [!important] Reglas que repitió
> - **Un fichero y una carpeta por cada dominio o subdominio.** "Si tengo 3 subdominios, tengo que hacerlo 3 veces." No se ponen varios en el mismo fichero.
> - **Solo se tocan `ServerName` y `DocumentRoot`**; luego `a2ensite` y `reload`. "Con eso sería suficiente."
> - El nombre de la carpeta es libre; la práctica del Laboratorio 4 pedirá nombres concretos ("tiene que ser así, para que no haya problemas").
> - Mío: el comando contrario para desactivar un sitio es `a2dissite`; no lo nombró.

> [!warning] Sin confirmar
> El audio es confuso sobre si la carpeta cuelga de **`/var/www/`** o de **`/var/www/html/`**. Lo que se oye apunta a `/var/www/<nombre>`. Sigue la ruta que dé la guía del Laboratorio 4, que es lo que manda.

### Si algo no funciona

| Síntoma | Causa probable | Qué hacer |
|---|---|---|
| El navegador no carga nada | Puerto 80 sin abrir en el Security Group | Añadir la regla HTTP (80 TCP) |
| Sale una página que no es la tuya | El registro A apunta a otra IP (p. ej. restos de Namecheap) | Corregir el registro A a tu IP |
| El subdominio no resuelve en tu equipo pero sí en otros | Caché DNS local | Esperar o limpiar la caché |
| `404 Not Found` en el subdominio | La carpeta del `DocumentRoot` no existe o no tiene `index.html` | Crearla y meter el `index.html` |
| `sudo cp`/`nano` dice "permission denied" | Falta `sudo` en `/etc/apache2` o `/var/www` | Anteponer `sudo` |
| El subdominio sirve la página del principal | Falta `a2ensite` o `reload` | Activar el sitio y recargar Apache |
| El navegador intenta `https://` | No hay HTTPS todavía | Escribe `http://` a mano |

---

## Para llevar a casa

> [!important] Calendario y entregas
> - **Actividad 1: lunes 16 de noviembre.** Según el material de la Clase 7 incluye también **HTTPS con Let's Encrypt** (Clase 9, 10/11). El profesor no lo mencionó hoy.
> - **Laboratorio 4 (miércoles 4/11):** WordPress, PHP y MariaDB sobre Apache, con tres sitios virtuales. Hay que **arrancar `srv_dns`** y usar la misma Elastic IP. No tengo transcripción de ese laboratorio.
> - **Próxima semana:** "laboratorio y clase", unas 2 h y media para repasar. Sin confirmar qué días exactos.
> - **Material en el foro** (carpeta de PPT y material complementario): vídeos de virtual hosts, WordPress, PHP y la base de datos. El profesor pide verlos antes. También prometió pasar la URL del Prezi con la sesión iniciada.

### Checklist

- [ ] Tener los **registros A** del principal, `blog` y un tercer nombre, y el **TXT**, con capturas y salida de `host`/`dig`.
- [ ] `sudo apt install apache2 -y` y regla de entrada **HTTP 80 TCP**.
- [ ] Probar el dominio principal con `http://` y ver tu `index.html`.
- [ ] Crear al menos **un virtual host** (`blog`) con su fichero, carpeta e `index.html`.
- [ ] Ver los vídeos del foro antes del siguiente laboratorio.
- [ ] Si vuelves al DNS del registrador, **para BIND9** y no lo dejes como autoridad.

## Dudas y cosas sin confirmar

- **Enunciado de la Actividad 1**: no lo tengo (puntos, texto del TXT, qué evidencia exacta).
- **Ruta de la carpeta del virtual host** (`/var/www/` o `/var/www/html/`): audio confuso; manda la guía del Lab 4.
- **Documento de comandos del Laboratorio 4**: el profesor lo consultó en pantalla ("punto 1: `apt install apache2`") y no me ha llegado.
- **Hora del laboratorio** ("mañana a 8 y media" de una compañera): no sé si es la hora del SER o de otro módulo.
- **HTTPS**: el profesor dijo que lo haría "con el proceso entero" más adelante; el material de la Clase 7 lo sitúa en la Clase 9.
- **Qué CMS en la Clase 9**: ni hoy ni en la Clase 7 se concreta.
