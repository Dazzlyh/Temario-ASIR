---
asignatura: Servicios en Red e Internet
fecha: 2026-11-03
tema: "Tema 4 · Clase 8: requisitos DNS de la Actividad 1, instalar Apache, abrir el puerto 80 y sitios virtuales (virtual hosts) por nombre"
fuente: transcripción de la clase (1 h 27 min) + **PDFs del profesor recibidos el 25/11**: diapositivas `SER_Clase08_diapositivas.pdf` (19 págs.), hoja `SER_Clase08_Instrucciones.pdf`, guía `SER_Clase08_VirtualHost_Guia.pdf`, comandos `SER_Clase08_Comandos` (.txt y .pdf, idénticos), guía maestra `SER_Guia_Web_de_punta_a_punta.pdf` y `SER_Apache_Proteger_un_sitio_Guia.pdf`. Contrastado con el material de la Clase 7, con el Tema 4 del temario y con la nota del Lab 4. Donde el PDF y el audio difieren, manda el PDF.
---
# SER · Clase 8 (3/11) · DNS para la Actividad 1 + Apache + virtual hosts

> Anterior: [Clase 7 (27/10): correcciones del Lab 3 e intro al servidor web](2026-10-27_correcciones-lab3-dns-e-intro-servidor-web.md) · Siguiente: [Laboratorio 4 (4/11): WordPress, PHP y MariaDB](2026-11-04_laboratorio4-wordpress-php-mariadb.md) · Profesor: Damián Sualdea Soy

> [!note] Actualización 25/11: PDFs recibidos
> Esta nota se hizo primero solo con el audio. Con los seis PDFs ya recibidos: (1) he añadido la **teoría de las diapositivas** (Tarea 5) y la **guía «VirtualHost de punta a punta»** con todos los comandos (Tarea 6), el DNS sin BIND9 (Tarea 7), el **HTTPS** de la guía maestra (Tarea 8) y la guía de **proteger un sitio** (Tarea 9); (2) he corregido la **ruta de las carpetas** (`/var/www/html/<nombre-completo>`); (3) ya tengo el **enunciado resumido de la Actividad 1** (3 puntos, entrega 16/11 a las 23:59, siete criterios con su peso; ver «Actividad 1»).

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

> [!note] Actualización con el PDF
> Las diapositivas (14) y la hoja de instrucciones dan el criterio como **«DNS con BIND9, dominio real y registro TXT: 15 %»**; la actividad vale **3 puntos** (ver «Actividad 1»). Lo que **sigue sin constar** es si el TXT lleva un texto obligatorio. El enunciado completo de la Actividad 1 sigue **sin recibir**: aquí solo está el resumen de las diapositivas.

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
 (blog3.dom)                                    └─ blog3.<dominio>  → /var/www/html/blog3.<dominio>
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
DocumentRoot  /var/www/html/blog3.<tu-dominio>    # la carpeta a la que se manda (PDF: dentro de /var/www/html)
```

3. **Crear la carpeta** y su `index.html`. La carpeta **no existe** hasta que la haces tú:

```bash
sudo mkdir -p /var/www/html/blog3.<tu-dominio>
cd /var/www/html/blog3.<tu-dominio>
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

> [!note] Ruta resuelta
> El audio era confuso sobre si la carpeta cuelga de `/var/www/` o de `/var/www/html/`. **Resuelto (guía del Lab 4 y PDFs de esta clase): `/var/www/html/<nombre-completo-del-sitio>/`**, «carpeta = ServerName, imposible confundirse». Mis comandos anteriores con `/var/www/<nombre>` estaban mal y ya están corregidos.

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

## Tarea 5 · La teoría de la clase · **(PDF: diapositivas e instrucciones, Tema 4.3-4.6)**

> [!note] Qué dicen los PDF de la clase
> La hoja de instrucciones y las diapositivas la presentan como **«teoría con la consola al lado»** y dicen que el montaje entero es el **Lab 4 (4/11)**; la **guía «VirtualHost»** (Tarea 6) y el audio sí hacen Apache y los virtual hosts en la propia clase. **Los PDF se contradicen en qué se monta hoy y qué mañana**: haz lo de la guía cuando quieras practicar.

### Cliente, servidor y sitio (4.3 y 4.4)
- **Cliente** = el navegador (Chrome, Firefox, Safari, Edge, o incluso en texto, *Links*): pide un recurso y lo muestra. **Servidor** = el software que lo sirve (o devuelve un error): **Apache** (Linux, v2.4, el nuestro), **Nginx**, **IIS** (Windows). «Servidor» es a la vez el programa y la máquina.
- **Un sitio web = una carpeta de archivos en árbol con su directorio raíz.** En Ubuntu, Apache sirve por defecto `/var/www/html` (`index.html`, `css/`, `img/`…).
- **Módulos (4.4):** Apache viene «pelado» y se amplía con módulos de **seguridad, monitorización, autenticación** y otros (**PHP, reescritura de URL, SSL**), que se activan con **`a2enmod`** (mañana, el de PHP para WordPress).

> [!warning] Errata del temario (4.3), confirmada en el repo
> El apartado del servidor web lleva de subtítulo **«Servidor DNS»**: es un **copia-pega**; debe decir **«Servidor web»**. El texto de debajo sí describe el servidor web. El DNS (Tema 3) da la **dirección**; el servidor web (Tema 4) da la **página**.

### Sitios virtuales: las tres técnicas (4.5)
Un servidor por web **desperdicia memoria y CPU**; con virtual hosts, un mismo Apache sirve varios sitios (así funciona todo el hosting). Apache decide por la cabecera **`Host:`** de la petición.

| Por… | Cómo distingue | Nota |
|---|---|---|
| **Nombre (FQDN)** | `www.x.com` frente a `blog.x.com` | **La más usada; la nuestra.** Necesita el DNS bien puesto |
| **Puerto** | `:8080` frente a `:9090` | Hay que abrir el puerto en el cortafuegos |
| **Dirección IP** | una IP por sitio | La menos usada; necesita varias IP o tarjetas |

Se pueden combinar. Ejemplo de la diapositiva 11 (por nombre): `ServerName tienda.desplegando123.com`, `DocumentRoot /var/www/html/tienda`, `a2ensite tienda.conf`, `systemctl reload apache2`. **(Matiz: la guía usa `tienda.desplegando123.com.conf` y carpeta `/var/www/html/tienda.desplegando123.com`; la diapositiva simplifica los nombres.)**

### El acceso tiene tres fases (4.6)
| Fase | Pregunta | Qué hace |
|---|---|---|
| **Autenticación** | ¿Quién eres? | Verifica la identidad (usuario y contraseña, o similar) |
| **Autorización** | ¿Puedes entrar **aquí**? | Ya autenticado, mira si tienes permiso para **ese** recurso |
| **Control de acceso** | ¿Desde dónde? | Qué equipos pueden conectar, **sin importar quién** (frena bots) |

| Tipo de autenticación | Qué hace |
|---|---|
| **Anónima** | Por defecto: ni usuario ni contraseña; zonas públicas |
| **Básica** | Usuario y contraseña **sin cifrar** (base64); sencilla pero insegura |
| **Digest** | Igual, con las credenciales **cifradas (MD5)**; más segura |
| **Otras** | Con servidor aparte: RADIUS, LDAP… |

> [!important] La básica solo es segura **dentro de HTTPS**. Otra razón para el candado.

## Tarea 6 · La guía «VirtualHost de punta a punta» · **(PDF: guía, comandos y guía maestra)**

Mismo flujo que el audio, con los comandos exactos. Se hace en `srv_dns` (la del Lab 3), con **un Apache y tres sitios**: el principal en el **apex** (`desplegando123.com`), `tienda` y `blog` en subdominios; **`www` no es un sitio: es un CNAME al apex** (el apex no puede ser CNAME; Clase 6). Sustituye `desplegando123.com` por **tu** dominio y `<ELASTIC-IP>` por tu IP.

**Paso 1 · DNS.** En `/etc/bind/db.desplegando123.com` añade `tienda` y `blog` y **sube el serial** (ej. `2026110301 → 2026110302`):
```bind
@        IN A      <ELASTIC-IP>             ; principal (ya estaba)
www      IN CNAME  desplegando123.com.      ; ya estaba
tienda   IN A      <ELASTIC-IP>             ; NUEVO
blog     IN A      <ELASTIC-IP>             ; NUEVO
```
```bash
sudo named-checkzone desplegando123.com /etc/bind/db.desplegando123.com   # OK
sudo systemctl reload named                                               # (guía: reload; el audio: restart bind9)
host tienda.desplegando123.com        # tiene que dar tu Elastic IP
host blog.desplegando123.com
```
**Paso 2 · Puerto 80 (AWS):** EC2 → instancia → *Security* → grupo → *Inbound rules* → *Add rule*: **HTTP · TCP · 80 · 0.0.0.0/0**. «Nueve de cada diez "a mí no me va" son esta regla»: desde dentro funciona, desde fuera no.

**Paso 3 · Apache:**
```bash
sudo apt update
sudo apt install -y apache2
systemctl status apache2 --no-pager
# navegador: http://<ELASTIC-IP>/  -> página por defecto de Ubuntu/Apache
```
**Paso 4 · Una carpeta por sitio, con el nombre completo** (carpeta = `ServerName`) y un `index.html` distinto en cada una:
```bash
sudo mkdir -p /var/www/html/desplegando123.com
sudo mkdir -p /var/www/html/tienda.desplegando123.com
sudo mkdir -p /var/www/html/blog.desplegando123.com
echo '<h1>Bienvenido a desplegando123.com</h1><p>Sitio principal</p>' | sudo tee /var/www/html/desplegando123.com/index.html
echo '<h1>desplegando123.com</h1><p>Esto es la TIENDA</p>'           | sudo tee /var/www/html/tienda.desplegando123.com/index.html
echo '<h1>desplegando123.com</h1><p>Esto es el BLOG</p>'             | sudo tee /var/www/html/blog.desplegando123.com/index.html
```
**Paso 5 · Un VirtualHost por sitio** (fichero nuevo en `sites-available`, no hace falta copiar el de por defecto):
```apache
# /etc/apache2/sites-available/desplegando123.com.conf   (el principal lleva ServerAlias www)
<VirtualHost *:80>
        ServerName desplegando123.com
        ServerAlias www.desplegando123.com
        DocumentRoot /var/www/html/desplegando123.com
</VirtualHost>
# /etc/apache2/sites-available/tienda.desplegando123.com.conf   (blog igual, cambiando tienda por blog)
<VirtualHost *:80>
        ServerName tienda.desplegando123.com
        DocumentRoot /var/www/html/tienda.desplegando123.com
</VirtualHost>
```
```bash
sudo a2ensite desplegando123.com.conf tienda.desplegando123.com.conf blog.desplegando123.com.conf
sudo a2dissite 000-default.conf      # desactiva el de por defecto para que mande el tuyo
sudo apache2ctl configtest           # tiene que dar: Syntax OK
sudo systemctl reload apache2
```
> [!important] Por qué el apex lleva `ServerAlias www`
> `ServerName` es el nombre principal; `ServerAlias` son **otros nombres que sirven la MISMA carpeta**. Como `www` es un CNAME al apex, el navegador manda `Host: www...` y, **sin el alias, Apache no sabría que es el mismo sitio**. (Es lo que se cita el 10/11 con el CNAME.)

> [!note] Dos formas de crear el `.conf`
> **Audio:** copiar `000-default.conf` y editar solo `ServerName`/`DocumentRoot`. **Guía:** escribir el fichero desde cero (solo 3 líneas) y **desactivar** `000-default.conf` con `a2dissite`. Valen las dos; la guía añade `a2dissite` y `configtest`.

**Paso 6 · Comprobar por nombre.** En el navegador (`http://`): `desplegando123.com` y `www.` → «Sitio principal» (el mismo, por el alias); `tienda.` → «TIENDA»; `blog.` → «BLOG». Por consola:
```bash
curl -s http://desplegando123.com/
curl -s http://tienda.desplegando123.com/
curl -s -H 'Host: blog.desplegando123.com' http://<ELASTIC-IP>/   # simula el nombre a mano (Apache elige por la cabecera Host)
```
**Qué tienes que ver:** tres páginas distintas con el mismo Apache y la misma IP. **Antes de cerrar:** guarda los `.conf`, **Stop** (nunca *Terminate*) a `srv_dns`, **no liberes la Elastic IP ni el dominio** (mañana, WordPress encima). **Guarda capturas:** es el criterio 2 de la Actividad 1.

| Síntoma | Casi siempre es… |
|---|---|
| Desde dentro va, desde fuera no | Puerto 80 (o 443) sin abrir en el *security group* |
| Todos los nombres dan la misma página | Falta `a2ensite` + `reload`, o `ServerName` repetido |
| `www` no carga pero el apex sí | Falta `ServerAlias www` en el `.conf` del apex |
| Un subdominio no resuelve | Falta su registro A, o no subiste el **serial** (BIND9) |
| `configtest` da error | Una llave `>` o una línea mal escrita |

## Tarea 7 · DNS sin BIND9 (Namecheap o IONOS) · **(PDF: guía maestra)**
La guía maestra ordena **todo el camino** (DNS → Apache y puerto 80 → VirtualHost → probar por el 80 → HTTPS) y avisa: «si el DNS no resuelve, ni los VirtualHost ni Certbot funcionan». Para el DNS hay **tres caminos; elige uno**: A) tu BIND9; B) Namecheap; C) IONOS. Apache solo necesita que los nombres resuelvan: «de dónde salga da igual».

| Camino B · Namecheap | Camino C · IONOS |
|---|---|
| Nameservers: **Namecheap BasicDNS** (no *Custom DNS*) | Servidores de nombres: **los de IONOS** (no «personalizados») |
| *Domain List → Manage → Advanced DNS → Host Records → Add New Record* | *Dominios & SSL → tu dominio → DNS* |
| `A @`, `A tienda`, `A blog` → Elastic IP; `CNAME www` → `desplegando123.com.` (**con punto final**); tic verde | Los mismos registros; guardar |

Comprueba: `host tienda.…` y `host blog.…` dan tu IP; `host www.…` apunta al dominio (también `dig +short`). **La propagación tarda de minutos a un par de horas:** hasta que no resuelva, no sigas con los VirtualHost por nombre.

## Tarea 8 · HTTPS con Certbot (el candado) · **(PDF: guía maestra, paso 6)**
Se detalla en la [nota del 10/11](2026-11-10_clase9-https-certbot-moodle.md); aquí lo que fija esta guía. **Requisitos:** el dominio resuelve y el sitio responde por el **80** (Let's Encrypt valida por ahí). Abre antes el **443** (*HTTPS · TCP · 443 · 0.0.0.0/0*).
```bash
sudo apt install -y certbot python3-certbot-apache
sudo certbot --apache -d desplegando123.com -d www.desplegando123.com -d tienda.desplegando123.com -d blog.desplegando123.com
sudo certbot renew --dry-run       # prueba la renovación automática
```
Certbot pide correo, condiciones y si **redirigir HTTP a HTTPS** (**sí**); crea solo los VirtualHost `:443`. **Fallos típicos:** *DNS problem / NXDOMAIN* (el nombre aún no resuelve) y *Timeout durante la validación* (**80 o 443 cerrados**).
> [!important] Orden con un CMS
> Lo más limpio es **HTTPS primero y el CMS después** (guarda su URL ya con `https`). Si lo haces al revés, cambia la **URL del sitio en WordPress** (*Ajustes → Generales*) y **`$CFG->wwwroot` en el `config.php` de Moodle**; si no, contenido mixto o bucle de redirección.

## Tarea 9 · Proteger un sitio en Apache (4.6) · **(PDF: guía aparte)**
> [!warning] Aviso de examen
> Esta guía es el apartado 4.6 «en la consola». **El 17/11 el profesor dijo que la autenticación básica (`htpasswd`) «lo tenéis como ejercicio, pero no os entra»** (ver [17/11](2026-11-17_repaso-simulacro-dibujos-dns-apache-https.md)). El **concepto** (3 fases, tipos de autenticación) sí está en el temario. La fortificación (versión, HSTS, fail2ban…) es del Tema 7 y de SAD.

**1 · Autenticación básica** (usuario y contraseña; **`-c` solo la primera vez**: si lo repites, borra el fichero):
```bash
sudo htpasswd -c /etc/apache2/.htpasswd alumno      # crea el fichero y el usuario
sudo htpasswd /etc/apache2/.htpasswd profesor       # añade otro (SIN -c)
cat /etc/apache2/.htpasswd                          # usuario:contraseña cifrada
sudo mkdir -p /var/www/html/blog.desplegando123.com/privado
echo '<h1>Zona restringida</h1>' | sudo tee /var/www/html/blog.desplegando123.com/privado/index.html
```
En el `.conf` del sitio (recomendado: se lee una vez al arrancar), y `sudo systemctl reload apache2`:
```apache
<Directory /var/www/html/blog.desplegando123.com/privado>
        AuthType Basic
        AuthName "Zona restringida"
        AuthUserFile /etc/apache2/.htpasswd
        Require valid-user
</Directory>
```
`AuthName` = el texto del *popup*; `Require valid-user` = cualquier usuario válido del fichero. **Contraseñas:** usa las tuyas; no las pongas en la documentación.

**2 · `.htaccess`** (la misma regla, por carpeta; **lo relee en cada petición**, más lento; es lo que usas en un hosting compartido). Por defecto Ubuntu **lo ignora**: hay que permitirlo con `AllowOverride AuthConfig` (o `All`) en el `<Directory>` del `.conf`, y el mismo bloque `AuthType…Require` va en `privado/.htaccess`.

**3 · Control de acceso por IP** (da igual quién seas: desde dónde). Útil para el **panel de administración** (`wp-admin`, phpMyAdmin) restringido a tu IP:
```apache
<Directory /var/www/html/blog.desplegando123.com/admin>
        Require ip 88.1.2.3            # solo el ordenador del administrador (IP de ejemplo)
        # Require ip 192.168.1.0/24    # o toda una red
        # Require local                # o solo desde la propia máquina
</Directory>
<RequireAll>                            # las dos cosas a la vez
        Require valid-user
        Require ip 88.1.2.3
</RequireAll>
```
`Require valid-user` = autenticación + autorización; `Require ip` = control de acceso; `Require all denied` cierra todo, `Require all granted` abre todo.

**4 · VirtualHost por puerto** (la 3.ª técnica): `Listen 8080` en `/etc/apache2/ports.conf`, `<VirtualHost *:8080>` con su `DocumentRoot`, `a2ensite` + `reload`, y **abrir el 8080 en el *security group***; se entra con `http://desplegando123.com:8080`. Se usa poco para webs públicas, sí para paneles internos.

**Resumen Apache del Tema 4:** instalar y servir (`apt install apache2`, `/var/www/html`, 80) · por nombre (`ServerName` + `DocumentRoot`, `a2ensite`) · por puerto (`Listen 8080`) · módulos y PHP (`a2enmod`, `libapache2-mod-php`) · HTTPS (`certbot --apache`, 443) · autenticación (`htpasswd`, `AuthType Basic`/`Require valid-user`) · `.htaccess` (`AllowOverride`) · control de acceso (`Require ip/local/all denied`).

## Actividad 1 · qué se puntúa · **(PDF: diapositivas 13-15 e instrucciones)**
**Vale 3 puntos; entrega el lunes 16/11/2026 a las 23:59**, sobre **tu servidor (AWS o VPS)** con **tu dominio real del Lab 3** (**el archivo `hosts` no vale**). Siete piezas:

| Pieza | Peso | Dónde se monta |
|---|---|---|
| **DNS con BIND9, dominio real y registro TXT** | 15 % | Lab 3 + clase 8 |
| **Apache con tres VirtualHost** | 10 % | Clase 8 / Lab 4 |
| **HTTPS con Let's Encrypt (Certbot)** | 10 % | En casa (campus) |
| **WordPress en un subdominio** | 20 % | Lab 4 |
| **Un segundo gestor de contenidos (CMS) a elección** | 20 % | En casa (campus) |
| **`index.html` hecho con IA** | 10 % | — |
| **Documentación** | 15 % | En casa (campus) |

«Las dos gordas son los gestores de contenido.» **En el audio** de esta clase el profesor pidió, para el DNS, el dominio principal, `blog`, un tercer nombre y un TXT (Tarea 1); la guía maestra monta `tienda` y `blog`: **no se contradicen**, son los tres sitios. **Con la guía maestra llevas hechos tres criterios (DNS 15 %, VirtualHost 10 %, HTTPS 10 %)**; faltan WordPress, el segundo CMS, el `index` con IA y la documentación. **Documentación:** guarda tus `.conf` y **anota qué camino de DNS usaste** (A, B o C).

**Enlaces de las diapositivas (no abiertos por mí):** vídeo del profesor «VirtualHost en Apache2» (`youtube.com/watch?v=vj_Yq3Ap-3w`), manual de Apache (`httpd.apache.org/docs/2.4/vhosts`), autenticación y acceso (`httpd.apache.org/docs/2.4/howto/auth.html`), Apache en Ubuntu (`ubuntu.com/server/docs/web-servers-apache`), pack de GitHub Education (dominio).

## Para llevar a casa

> [!important] Calendario y entregas
> - **Actividad 1: lunes 16 de noviembre, 23:59; 3 puntos.** Incluye también **HTTPS con Let's Encrypt** (criterio de las diapositivas; Clase 9, 10/11). Pesos en «Actividad 1».
> - **Laboratorio 4 (miércoles 4/11):** WordPress, PHP y MariaDB sobre Apache, con tres sitios virtuales. Hay que **arrancar `srv_dns`** y usar la misma Elastic IP. Ya está en su nota (guía y transcripción).
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

- ✅ **Resueltas con los PDF:** ruta de las carpetas, puntos y hora de entrega de la Actividad 1 (3 puntos, 16/11 23:59), peso de los siete criterios, lista de comandos y documento de comandos de la clase.
- **Enunciado completo de la Actividad 1:** sigue sin recibir (solo el resumen de las diapositivas). Si el TXT lleva texto obligatorio: sin confirmar.
- **Qué se montaba el 3/11 y qué el 4/11:** la hoja de instrucciones dice «Montar Apache es mañana»; la guía «VirtualHost» y el audio lo hacen hoy. **Se contradicen.**
- **`reload named` (guía) frente a `restart bind9` (audio):** ambos válidos en Ubuntu (el servicio `bind9` es el alias de `named`); `reload` basta tras tocar una zona.
- **Hora del laboratorio** («mañana a 8 y media» de una compañera): no sé si es la hora del SER o de otro módulo.
- **Prezi / documento de comandos que usó el profesor:** el documento de comandos ya está (`SER_Clase08_Comandos`); el Prezi no.
- **Autenticación básica en el examen:** el 17/11 dijo que no entra; la guía de proteger un sitio no trae fecha ni indica en qué clase se vio. Lo he dejado como material, con aviso.
