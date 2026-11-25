---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-11-10
tema: "Tema 4 · Clase 9: HTTPS con Certbot / Let's Encrypt (snap y apt) y un segundo CMS (Moodle) en un subdominio"
fuente: transcripción de la clase (1 h 39 min) y guía oficial SER_Guia_Web_de_punta_a_punta.pdf (5 páginas, "guía maestra de la Actividad 1"). Donde difieren, manda la guía. Documento del laboratorio de Moodle citado por el profesor: recibido el 25/11 (`SER_Lab04_Moodle_Guia.pdf`, resumido en la [nota del Lab 4](2026-11-04_laboratorio4-wordpress-php-mariadb.md)). Contraste externo marcado (web).
---
# SER · Clase 9 (10/11) · HTTPS con Certbot y segundo CMS

> Anterior: [Laboratorio 4 (4/11): WordPress sobre Apache](2026-11-04_laboratorio4-wordpress-php-mariadb.md) · Siguiente: [Repaso y simulacro (17/11)](2026-11-17_repaso-simulacro-dibujos-dns-apache-https.md) · Profesor: Damián Sualdea Soy

Cierre de la **Actividad 1** (entrega **lunes 16/11**). El profesor repasó el camino completo (DNS → Apache → VirtualHost → HTTPS), puso el **candado con Certbot** y montó **Moodle** en un subdominio nuevo (`academia`) para enseñar el proceso entero con un CMS. Un compañero resolvió en directo el fallo del Moodle (ver Tarea 4).

Convención: **(guía)** = PDF, **(clase)** = audio, **(web)** = fuente externa, **(mío)** = añadido por mí. Dominio de ejemplo de la guía: `desplegando123.com`; sustitúyelo por el tuyo.

## Lo imprescindible

> [!important] Orden de la Actividad 1 (guía): cada paso necesita el anterior
> 1. **DNS**: los nombres resuelven a tu Elastic IP (BIND9, Namecheap o IONOS).
> 2. **Apache** instalado y **puerto 80** abierto en el Security Group.
> 3. **VirtualHost** (uno por nombre).
> 4. **Probar por el 80** (`curl`/navegador).
> 5. **HTTPS con Certbot** (puerto **443** abierto antes).
>
> "Fijaros en el orden: DNS, luego virtual host y luego HTTPS; después ya instalas lo que quieras." Si el DNS no resuelve, ni los VirtualHost por nombre ni Certbot funcionan.

> [!important] Certbot en 3 líneas (apt, el de la guía)
> ```bash
> sudo apt install -y certbot python3-certbot-apache
> sudo certbot --apache -d desplegando123.com -d www.desplegando123.com -d tienda.desplegando123.com -d blog.desplegando123.com
> sudo certbot renew --dry-run
> ```
> Con **snap** (el de clase) solo cambia la instalación; ver Tarea 2.

> [!warning] Qué cuenta en la Actividad 1 (guía)
> Con este camino quedan hechos **3 de los 7 criterios**: DNS (**15 %**), tres VirtualHost (**10 %**) y HTTPS con Certbot (**10 %**). **Faltan**: WordPress (20 % según la guía del Lab 4), el segundo gestor de contenidos, **el «index con IA»** (aparece en la guía; no se explicó en clase, **sin confirmar** qué pide) y la **documentación**. El profesor: "entregarla con tiempo; dadle al botón de enviar".

## Tarea 1 · DNS y VirtualHost (repaso con las novedades de la guía)

Ya visto el 3/11 (ver [Clase 8](2026-11-03_clase8-dns-actividad1-apache-virtual-hosts.md)). Lo nuevo o precisado:

### Tres caminos para el DNS (guía)
Da igual **de dónde** salga la respuesta; elige **uno**:

| Camino | Dónde | Pasos |
|---|---|---|
| **A · BIND9** (el del Lab 3) | `/etc/bind/db.<dominio>` | Añade `tienda IN A <IP>` y `blog IN A <IP>` (el `@` y `www IN CNAME <dominio>.` ya estaban), **sube el serial** del SOA, `named-checkzone <dominio> /etc/bind/db.<dominio>` y `systemctl reload named` |
| **B · Namecheap** | *Domain List → Manage → Advanced DNS → Host Records* | A `@`, `tienda`, `blog` → tu Elastic IP; CNAME `www` → `<dominio>.` (con punto final). Nameservers en **BasicDNS**, no *Custom DNS* |
| **C · IONOS** | *Dominios & SSL → tu dominio → DNS* | Los mismos registros. Servidores de nombres los de IONOS, no «personalizados» |

Comprobación (los tres igual): `host tienda.<dominio>` y `host blog.<dominio>` dan tu IP; `host www.<dominio>` apunta al dominio; también `dig +short`. La propagación tarda de **minutos a un par de horas**: hasta que no resuelva, **no sigas**.

> [!note] Lo que se vio en directo (clase)
> - El profesor añadió un registro **A** `academia` en IONOS (su proveedor) con la misma IP, y comprobó con **`host academia.<dominio>`**. Para probar DNS se usa `host`/`dig`, **no `ping`** ("ping es ICMP, no DNS").
> - También un registro **TXT** en `academia` con un texto ("Es un Moodle"), para repasar el tipo TXT (sirven para verificar dominios: Facebook, Google…). Se comprueba con `host -t TXT academia.<dominio>` (**(mío)** la opción `-t`).
> - **Fallo de una compañera:** el nombre le resolvía a **dos IP** y ninguna era la suya. Causa: tenía el dominio **también en BIND9** y estaba interfiriendo con IONOS. Solución: dejar **una sola autoridad** (borrar/editar donde sobra). Misma regla que el 3/11: BIND9 **o** el registrador, nunca los dos.
> - Si usas BIND9, también habría que añadir la **zona inversa (PTR)** de la IP (ídem que en el Lab 3); lo mencionó de pasada.

### Apache: carpetas, `index.html` y `.conf` (guía)

```bash
sudo mkdir -p /var/www/html/desplegando123.com
sudo mkdir -p /var/www/html/tienda.desplegando123.com
sudo mkdir -p /var/www/html/blog.desplegando123.com

echo '<h1>desplegando123.com</h1><p>Sitio principal</p>' | sudo tee /var/www/html/desplegando123.com/index.html
echo '<h1>Esto es la TIENDA</h1>' | sudo tee /var/www/html/tienda.desplegando123.com/index.html
echo '<h1>Esto es el BLOG</h1>'   | sudo tee /var/www/html/blog.desplegando123.com/index.html
```
- `mkdir -p`: crea la ruta entera y **no falla si ya existe** (lo explicó el profesor).
- **Carpeta = `ServerName`**, con el nombre completo.

```apache
# /etc/apache2/sites-available/desplegando123.com.conf   (apex, con alias www)
<VirtualHost *:80>
    ServerName desplegando123.com
    ServerAlias www.desplegando123.com
    DocumentRoot /var/www/html/desplegando123.com
</VirtualHost>
```
`tienda.desplegando123.com.conf` y `blog.desplegando123.com.conf` igual, **sin** `ServerAlias`.

```bash
sudo a2ensite desplegando123.com.conf tienda.desplegando123.com.conf blog.desplegando123.com.conf
sudo a2dissite 000-default.conf          # (guía) desactiva el sitio por defecto
sudo apache2ctl configtest               # debe decir: Syntax OK
sudo systemctl reload apache2
curl -s http://tienda.desplegando123.com/   # Apache elige por la cabecera Host:
```

> [!important] Reglas del profesor (clase)
> - **Un `.conf` y una carpeta por dominio o subdominio** (como Nginx: "creamos varios archivos de configuración").
> - **Pon siempre el dominio completo** en el nombre del fichero y en `ServerName` ("aquí soléis fallar bastante"); y **crea la carpeta** del `DocumentRoot` **antes** de probar: si no existe, Apache sirve un error.
> - Para crear el sitio nuevo copió uno existente: `sudo cp blog3.<dominio>.conf academia.<dominio>.conf` (en `sites-available`), lo editó (`ServerName` y `DocumentRoot`), `sudo a2ensite academia.<dominio>.conf`, `sudo systemctl reload apache2`, creó la carpeta y un `index.html` y probó con `curl`. **Revisa que `sites-enabled` muestre tu sitio** (`ls -l /etc/apache2/sites-enabled`).

> [!warning] Corrección importante: `www` y el CNAME
> En clase se preguntó por qué `www.<dominio>` no funcionaba con un solo `ServerName`, y el profesor respondió que como `www` es un CNAME "llega a Apache con el dominio, nunca con www". **Eso no es correcto**: el CNAME es solo DNS y el navegador envía en la cabecera `Host:` **el nombre que escribiste** (`www.<dominio>`). Por eso la **guía** pone **`ServerAlias www.<dominio>`** en el `.conf` del apex, y su tabla de errores dice «www no carga pero el apex sí → falta `ServerAlias www`». **Sigue la guía.** Y sí es cierto lo que dijo antes: un virtual host solo admite **un** `ServerName` (los otros nombres van como `ServerAlias`) y en BIND9 el alias se hace con un **CNAME**.

## Tarea 2 · HTTPS con Certbot (el candado, puerto 443)

**Idea (clase):** sin HTTPS, la comunicación "se ve absolutamente entera" para quien esté en medio. **HTTPS** cifra (TLS). **Certbot** es un programa (hecho en Python) que habla con una **entidad certificadora (CA)**, **Let's Encrypt** (proyecto de la ISRG, sin ánimo de lucro, **certificados gratis**, reconocida por los navegadores), obtiene el certificado y **configura Apache solo**. Antes los certificados se pagaban.

> [!note] «Tener candado no significa que el sitio sea de fiar» (clase)
> Un alumno preguntó por qué se avisa de no entrar en webs sin certificado si sacarlo es tan fácil. Respuesta: HTTPS solo garantiza que **la comunicación va cifrada** entre navegador y servidor, **no que quien está detrás sea honrado**: una web fraudulenta también puede tener candado. Hay que mirar de dónde viene la web. Cada servidor (p. ej. uno de correo) necesita su propio certificado.

### Requisitos previos (guía)
1. El nombre **resuelve** (Tarea 1).
2. El sitio responde por el **80** (Let's Encrypt **valida por el 80**).
3. **Abrir el 443** en el Security Group: *EC2 → tu instancia → Security → el grupo → Edit inbound rules → Add rule → HTTPS · TCP · 443 · 0.0.0.0/0*.

> [!warning] El fallo que pasó en directo (clase)
> El profesor lanzó Certbot y al abrir `https://` no cargaba: **tenía el 443 cerrado** ("nuestro firewall está tirado"). Añadió la regla HTTPS (le puso descripción "Apache con TLS") y borró otra que había creado sin querer. Certbot **valida por el 80 y sirve por el 443: los dos abiertos**.

### Dos formas de instalar Certbot: apt y snap

| | **apt** (guía; el de Dani) | **snap** (el que usó el profesor en clase) |
|---|---|---|
| Instalación | `sudo apt install -y certbot python3-certbot-apache` | `sudo snap install --classic certbot` y `sudo ln -s /snap/bin/certbot /usr/bin/certbot` |
| Qué instala | Paquete de Ubuntu + plugin de Apache (`python3-certbot-apache`) | Certbot completo (con el plugin de Apache) como snap |
| Versión | La que traiga el repositorio de tu Ubuntu; suele ir **por detrás** (web) | La **más reciente** (web) |
| Qué recomienda Certbot | Es un camino alternativo | Es el que enlazan sus instrucciones oficiales para Ubuntu (web, ver nota) |
| Comando para pedir el certificado | `sudo certbot --apache …` | `sudo certbot --apache …` (idéntico) |
| Renovación automática | Se programa sola (**(mío)** con un temporizador de systemd; compruébalo) | Servicio de systemd del snap que se ejecuta **dos veces al día** (web) |
| Prueba de renovación | `sudo certbot renew --dry-run` | `sudo certbot renew --dry-run` |

**Pasos del profesor con snap (clase):**
1. Buscó en la web de **Certbot** (certbot.eff.org): *software* **Apache**, *sistema* **Ubuntu (snap)**, y siguió las instrucciones. Comprobó que `snapd` estuviera (`sudo apt install snapd`, **(mío)** en las AMI de Ubuntu suele venir ya instalado).
2. `sudo snap install --classic certbot` → "se ha instalado certbot".
3. Enlace simbólico para que baste escribir `certbot`: `sudo ln -s /snap/bin/certbot /usr/bin/certbot`.
4. `sudo certbot --apache` (interactivo, ver abajo).

> [!note] Los comandos exactos de snap
> El profesor los **copió y pegó de la web** y el audio no los dicta. Lo de arriba es lo que se entiende más lo que recuerdo de las instrucciones de Certbot; la web oficial puede añadir un `snap install core`/`snap refresh core` previo. Compruébalo en **certbot.eff.org** antes de usarlo (no he podido abrir esa página hoy).

> [!warning] No mezcles los dos (web)
> Según un voluntario de la comunidad de Let's Encrypt (no es documentación oficial), **no conviene tener a la vez el Certbot de apt y el de snap**: si pasas de uno a otro, quita primero el de apt (`sudo apt remove certbot python3-certbot-apache`, **(mío)** los nombres exactos) y comprueba que `/usr/bin/certbot` apunta al del snap. Comprobaciones **(mío)**:
> ```bash
> which certbot              # /usr/bin/certbot
> certbot --version
> snap list | grep certbot   # solo existe si es snap
> dpkg -l | grep certbot     # solo existe si es apt
> sudo systemctl list-timers | grep -i certbot   # el temporizador de renovación
> ```

### Lanzar Certbot: dos formas

| Forma | Comando | Qué pasa |
|---|---|---|
| **Con `-d` (guía)** | `sudo certbot --apache -d desplegando123.com -d www.desplegando123.com -d tienda.desplegando123.com -d blog.desplegando123.com` | Un solo certificado para **todos** los nombres de la lista |
| **Interactivo (clase)** | `sudo certbot --apache` | **Detecta los virtual hosts** y te deja elegir por número cuáles protegen |

Preguntas de Certbot (clase y guía):
1. **Correo** (real: avisa antes de que caduque el certificado).
2. **Aceptar las condiciones** (si dices que no, el programa sale).
3. Recibir novedades de la EFF: **No**.
4. (Interactivo) elegir el/los virtual host por número. El profesor eligió uno (`academia`).
5. **Redirigir HTTP a HTTPS: «sí»** (guía). Con esto, entrar por `http://` te manda a `https://`.

Resultado: "Congratulations…". Prueba en el navegador con **`https://`** y el candado.

> [!important] Qué ha cambiado en Apache (clase)
> Certbot **no es magia**; mira en `/etc/apache2`:
> - En `sites-available` aparece un **fichero nuevo** acabado en **`-le-ssl.conf`** (de *Let's Encrypt*), también en `sites-enabled`: es el **virtual host del puerto 443** con el certificado y la clave.
> - En el `.conf` original (puerto 80) **añadió al final una redirección** (módulo *rewrite*): "si llega `http`, mándalo a `https://<ServerName>…`". Por eso **ya no puedes entrar por `http`**.
> - Los certificados se guardan aparte. **(mío)** en `/etc/letsencrypt/live/<dominio>/` (`fullchain.pem` y `privkey.pem`).
> - Para **cada dominio nuevo** basta repetir `sudo certbot --apache`: el profesor dijo "metemos un dominio nuevo, ejecutamos Certbot y a correr".

```bash
sudo certbot renew --dry-run      # (guía) prueba la renovación automática, sin renovar de verdad
```
Los certificados de Let's Encrypt caducan a los **~3 meses** (clase); por eso el correo y la renovación automática.

### Los dos fallos típicos (guía)
| Síntoma | Causa | Arreglo |
|---|---|---|
| «DNS problem / NXDOMAIN» | El nombre aún no resuelve | Vuelve al DNS y espera la propagación |
| «Timeout durante la validación» | **80 o 443 cerrados** en el Security Group | Abre los dos |

### Si hay un CMS: el orden del HTTPS (guía)
Lo más limpio es **HTTPS primero** y el CMS después (guarda su URL ya con `https`). Si lo hiciste al revés (**tu WordPress del Lab 4 se instaló por HTTP**):
- **WordPress:** panel → *Ajustes → Generales* → pon `https://` en **las dos URLs** (o en `wp-config.php`).
- **Moodle:** `$CFG->wwwroot` en su `config.php` con `https://`.
Si no, **contenido mixto** o **bucle de redirecciones**.

## Tarea 3 · Segundo CMS: Moodle en `academia.<dominio>` (clase)

El profesor eligió **Moodle** y mostró el proceso completo (tiene una guía de laboratorio de Moodle, **no recibida**). Orden: **DNS (registro A `academia`) → VirtualHost → HTTPS → instalar el CMS**. La parte de WordPress ya está en el [Lab 4](2026-11-04_laboratorio4-wordpress-php-mariadb.md); aquí lo que cambia.

```bash
cd /tmp
wget <enlace copiado de la web de Moodle>        # el .tgz de la versión estable
file moodle*                                     # (alumno) comprobar qué has bajado
tar xzf <fichero>.tgz        # o: unzip <fichero>.zip
ls                                               # carpeta moodle/
sudo cp -r moodle/* /var/www/html/academia.<dominio>/
sudo chown -R www-data:www-data /var/www/html/academia.<dominio>
sudo rm -f /var/www/html/academia.<dominio>/index.html       # el index.html de prueba
```

> [!warning] «No me descomprime»: casi siempre bajaste una página HTML
> Al profesor `tar` le dio error. Un alumno comprobó con **`file`** que lo descargado era un **documento HTML**, no un `.tgz`: copió la URL de la **página de descarga**, no del fichero. Solución: copiar el **enlace directo** al archivo, o el profesor usó la versión `.zip`/otro enlace. Con `file` ves el tipo real de un fichero. (Dijo que él suele usar **`git clone`** del repositorio de Moodle y una **rama estable**; **(mío)** p. ej. `git clone -b MOODLE_501_STABLE https://github.com/moodle/moodle.git`: el nombre de la rama a verificar.)

> [!important] **Moodle 5.1+: el `DocumentRoot` es la carpeta `public`** (alumno, confirmado por (web))
> Tras copiar, la web salía **en blanco**. El profesor buscó la causa en versiones de PHP/MariaDB y en `max_input_vars`, **sin éxito**. **Lo resolvió un compañero:** en las versiones nuevas de Moodle el `index.php` está **dentro de `public/`**, así que el `DocumentRoot` debe apuntar ahí. Hay que cambiarlo en **los dos** ficheros:
> ```apache
> DocumentRoot /var/www/html/academia.<dominio>/public
> ```
> 1. El `.conf` del puerto 80 (`academia.<dominio>.conf`).
> 2. El `…-le-ssl.conf` que creó Certbot (el del 443).
> Y `sudo systemctl reload apache2`. Las notas de versión de Moodle 5.1 lo confirman: el servidor debe tener el *document root* apuntando a `/public` (web). Moraleja del profesor: "esto lo hace gente que lo va modificando cada día; es normal que pase".

Otros pasos y datos de la clase:
- **PHP:** `max_input_vars` ≥ **5000** (Moodle lo exige, web); el profesor lo subió en el `php.ini` de Apache y reinició. **(mío)** ruta: `/etc/php/<versión>/apache2/php.ini`. La máquina de clase tenía **PHP 8.3.6**.
- **Base de datos** (como en el Lab 4, pero nueva): una **BD**, un **usuario** propio (en clase `moodle_user`; BD `moodle`) y **contraseña fuerte**:
  ```sql
  CREATE DATABASE moodle DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;   -- (guía del Lab 4) utf8mb4 es obligatorio
  CREATE USER 'moodle_user'@'localhost' IDENTIFIED BY '<clave-fuerte>';
  GRANT ALL PRIVILEGES ON moodle.* TO 'moodle_user'@'localhost';
  FLUSH PRIVILEGES;
  ```
- **Carpeta `moodledata`** (donde Moodle guarda ficheros): el instalador pide una ruta. El profesor la creó en `/var/www/html/moodledata`, la puso a **`www-data`** y permisos amplios (en el audio "0, 7, 7, 0": **sin confirmar** si fue `0770` o `0777`); justificó que "no tiene acceso desde fuera". **La guía del Lab 4 (PDF, manda) lo contradice:** `moodledata` va **fuera de `/var/www`**, en **`/var/moodledata`**, con `chown www-data:www-data` y **`chmod 0770`** (si estuviera en el sitio web, sus ficheros privados se descargarían por HTTP). El `0770` zanja el audio confuso; no hace falta `0777`.
- **Asistente web** de Moodle: idioma **Español (España)**, ruta de `moodledata`, tipo de BD **MariaDB**, datos de la BD, *Continuar*; instalación de tablas (muy larga: "`htop` a tope"), después usuario administrador (`admin`), nombre del sitio ("Academia") y correo.
- **Versión de MariaDB (audio confuso, sin confirmar):** el instalador rechazó la MariaDB de la máquina por **versión**; el profesor la **cambió a otra** (habla de 11.4 y de 10.11.14) para continuar y dijo que "bajar así de versión es una barbaridad" en un servidor real. Moodle 5.1 pide **MariaDB ≥ 10.11.0** y **PHP ≥ 8.2** (web). **Es probable** que bajara una versión de Moodle más reciente de la que soportaba su stack; la lección es **mirar los requisitos de versión antes de instalar** y, si no encaja, usar una **rama estable anterior**. Con la versión de MariaDB de tu máquina (`mariadb --version`) comprueba que cumple lo que pide el Moodle que descargues.

## Si algo no funciona (guía + clase)

| Síntoma | Casi siempre es… |
|---|---|
| `host` no da tu IP | Falta el registro, no ha propagado o (BIND9) no subiste el **serial** |
| Va desde dentro, no desde fuera | **80** (o **443**) sin abrir en el Security Group |
| Todos los nombres dan la misma página | Falta `a2ensite` + `reload`, o `ServerName` repetido |
| `www` no carga pero el apex sí | Falta `ServerAlias www.<dominio>` en el `.conf` del apex |
| Certbot falla en la validación | El nombre no resuelve aún, o 80/443 cerrados |
| `https://` no carga, `http://` sí | 443 cerrado (Security Group) |
| Moodle en blanco | `DocumentRoot` sin `/public` (80 **y** 443) |
| `tar` falla al descomprimir | Bajaste una página HTML; `file` lo confirma |
| Nombre con dos IP distintas | DNS en **dos sitios a la vez** (BIND9 y registrador) |

## Cierre y entrega (guía)

- [ ] Guarda tus ficheros `.conf` y **anota qué camino de DNS usaste** (A, B o C): va en la documentación de la Actividad 1.
- [ ] **EC2 → `srv_dns` → Stop** (nunca *Terminate*). **No liberes** la Elastic IP ni el dominio.
- [ ] **Tu WordPress:** tras Certbot, cambiar las URLs a `https://` (ver arriba).
- [ ] **Segundo CMS** (Moodle u otro) en otro subdominio, con su HTTPS.
- [ ] Documentación con capturas. **Entrega: lunes 16/11.**

## Dudas y cosas sin confirmar

- **Comandos exactos de la instalación por snap**: no se oyen; ver aviso arriba y certbot.eff.org.
- ✅ **Permisos de `moodledata`:** `0770`, según la guía del Lab 4.
- **Versión de MariaDB y de Moodle** usadas y por qué falló: audio confuso.
- **«Index con IA»** (criterio de la guía) y el contenido exacto de la **documentación**: sin enunciado.
- **Documento del laboratorio de Moodle:** ya recibido (25/11). La **guía de comandos Linux** que citó el profesor: sigue sin recibir.
- **Renovación con apt:** lo he descrito de memoria; verifica con `systemctl list-timers`.
- Dijo que "más adelante" enseñará "algo que lo hace todo automático" (sin concretar) y que el correo electrónico llegará en temas posteriores; sin valor evaluable por ahora.

Fuentes (web): [Moodle 5.1 release notes](https://moodledev.io/general/releases/5.1) · [Let's Encrypt community: apt vs snap](https://community.letsencrypt.org/t/a-question-about-certbot-apt-vs-snap-on-ubuntu/190127)
