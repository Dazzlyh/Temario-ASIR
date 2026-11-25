---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-11-04
tema: "Tema 4 · Laboratorio 4: WordPress sobre Apache (PHP + MariaDB + instalación por navegador)"
fuente: transcripción del laboratorio (50 min), guía oficial SER_Lab04_WordPress_Guia.pdf (3 páginas) y, desde el 25/11, SER_Lab04_Moodle_Guia.pdf (3 páginas). Donde difieren, manda la guía. Contrastado con wordpress.org/about/requirements y con documentación externa (marcada como (web)).
---
# SER · Laboratorio 4 (4/11) · WordPress sobre tu servidor

> Anterior: [Clase 8 (3/11): DNS de la Actividad 1, Apache y virtual hosts](2026-11-03_clase8-dns-actividad1-apache-virtual-hosts.md) · Siguiente: [Clase 9 (10/11): HTTPS con Certbot y Moodle](2026-11-10_clase9-https-certbot-moodle.md) · Profesor: Damián Sualdea Soy

Se monta WordPress de verdad (nube, dominio propio) sobre el `blog.<tu-dominio>` que quedó como virtual host el 3/11. Son cuatro piezas, en este orden: **PHP** → **MariaDB** → **ficheros de WordPress** → **asistente del navegador**. El profesor insistió en que **hacerlo con él equivale a haber hecho la actividad**: es el **criterio 4 de la Actividad 1 (20 %)** según la guía. Entrega: lunes 16/11.

Convención de la nota: **(guía)** = PDF, **(clase)** = audio, **(web)** = fuente externa, **(mío)** = añadido por mí. En los comandos uso `blog.desplegando123.com`, el dominio de ejemplo de la guía; sustitúyelo por el tuyo.

## Lo imprescindible

> [!important] Resumen en 10 líneas (guía)
> ```bash
> sudo apt update
> sudo apt install -y php libapache2-mod-php php-mysql
> sudo systemctl restart apache2
> sudo apt install -y mariadb-server
> sudo mysql                      # crear BD y usuario (ver Tarea 2)
> cd /tmp && wget https://wordpress.org/latest.tar.gz && tar xf latest.tar.gz
> sudo rm -f /var/www/html/blog.desplegando123.com/index.html
> sudo cp -r wordpress/* /var/www/html/blog.desplegando123.com/
> sudo chown -R www-data:www-data /var/www/html/blog.desplegando123.com
> # navegador: http://blog.desplegando123.com/  → asistente
> ```
> Al final: **borrar `info.php`** y **Stop** (nunca Terminate) a `srv_dns`, sin liberar la Elastic IP ni el dominio.

> [!note] Ruta de la carpeta (resuelve una duda del 3/11)
> La guía usa **`/var/www/html/<subdominio>/`** y el profesor dijo lo mismo en clase. Ya no queda duda con la ruta del 3/11. Si tu virtual host del 3/11 apunta a otra carpeta, o cambias el `DocumentRoot`, o copias WordPress donde apunte (comprueba con `grep DocumentRoot /etc/apache2/sites-available/*.conf`, **(mío)**).

## Punto de partida (guía)

- Servidor encendido con Apache y los VirtualHost funcionando en el puerto 80.
- `blog.<dominio>` resolviendo a tu Elastic IP.
- Conexión: `ssh -i labsuser.pem ubuntu@<TU-ELASTIC-IP>`.
- Antes de empezar, el profesor se conectó por SSH y repasó el estado de Apache y el fichero del virtual host en `/etc/apache2/sites-available/` (audio confuso en los detalles). Los pasos se hacen con `sudo`; no hace falta ser root.

> [!note] Cómo lo trabaja el profesor (clase)
> "Yo para instalar WordPress siempre pido información en la página web": **wordpress.org** → *Get WordPress* (descarga y requisitos recomendados: PHP y MySQL/MariaDB) y la documentación de instalación. Es la fuente oficial; la guía de hoy es esa receta adaptada.

## Tarea 1 · PHP: que Apache ejecute código

WordPress está escrito en PHP. Sin el módulo, Apache **sirve el código como texto** en vez de ejecutarlo.

```bash
sudo apt update
sudo apt install -y php libapache2-mod-php php-mysql     # (guía)
sudo systemctl restart apache2
```

| Paquete | Para qué |
|---|---|
| `php` | El intérprete (en Ubuntu ya arrastra el módulo de Apache) |
| `libapache2-mod-php` | El módulo que enchufa PHP en Apache |
| `php-mysql` | La extensión que conecta PHP con MySQL/MariaDB (sin ella WordPress no habla con la base de datos) |

### Comprobar que PHP funciona (`info.php`)

```bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/blog.desplegando123.com/info.php   # (guía)
```
Abre `http://blog.desplegando123.com/info.php`:

| Lo que ves | Significa |
|---|---|
| Tabla azul/morada de PHP | PHP ejecutándose bien |
| El texto `<?php phpinfo(); ?>` tal cual | Apache **no** ejecuta PHP (falta el módulo o no reiniciaste) |
| Nada / no carga | Revisa que la URL empiece por `http://` |

> [!important] Demostración del profesor (clase)
> La hizo **antes** de instalar PHP a propósito: con `info.php` creado y sin PHP, el navegador muestra la instrucción en bruto, "lo lanza tal cual", o sea, **no se ha ejecutado en el servidor**. Tras `apt install php`, la misma URL muestra la tabla. Así se ve la diferencia entre **fichero estático** (se envía igual) y **web dinámica** (se ejecuta y genera el HTML).

> [!warning] Si no carga: tu navegador fuerza `https`
> A un alumno no le cargaba nada porque el navegador había puesto `https://`. Aún no hay certificado (llega en la Clase 9): escribe a mano `http://`. Si ves la página vieja, **caché**: prueba otro navegador o ventana privada (le pasó al profesor).

> [!important] Bórralo al terminar (guía y clase)
> `sudo rm /var/www/html/blog.desplegando123.com/info.php`. Es "uno de los peores archivos que podéis tener": revela **toda** la configuración del servidor a un atacante. En clase lo borró con `rm -rf` (basta `rm`).

### Error que se provocó a propósito: falta `php-mysql` (clase)

El profesor instaló solo `php` (sin la extensión de MySQL) para enseñar el fallo: al abrir WordPress dice que **falta la extensión MySQL de PHP**. Arreglo:

```bash
sudo apt install php-mysql -y
sudo systemctl restart apache2     # (mío; la guía lo reinicia tras instalar; él dijo "actualizad")
```
La guía lo instala todo de una vez, así que a ti no te saldrá.

## Tarea 2 · MariaDB: la base de datos

```bash
sudo apt install -y mariadb-server
sudo systemctl status mariadb          # (clase) comprobar que está activo; salir con q
sudo mysql                             # (guía) entra como root del sistema; el prompt cambia a MariaDB [(none)]>
```

Dentro de MariaDB (**(guía)**; cambia la contraseña):
```sql
CREATE DATABASE wordpress;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'UnaClaveFuerte';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

| Pieza | Valor de la guía | Nota |
|---|---|---|
| Base de datos | `wordpress` | |
| Usuario | `wpuser` | En clase lo llamó "wp user" |
| Contraseña | la que elijas | Usa una contraseña **propia y fuerte**; no copies la de ejemplo ni la de la clase |
| Permisos | `ON wordpress.*` | Solo sobre **su** base, no sobre todo el servidor: "eso es lo correcto" (guía) |

> [!important] Apunta los tres datos
> BD `wordpress`, usuario `wpuser` y tu contraseña: los pides en el paso siguiente. Además la guía pide anotar en tu documentación la BD, el usuario y el subdominio donde está WordPress.

> [!note] Orden de la clase (clase)
> El profesor instaló MariaDB, pero **dejó crear la BD para después**: primero lanzó el asistente de WordPress, vio el error de base de datos y entonces entró a `mariadb`. Es una forma de ver el error. **La guía te lo da en orden correcto**: crea la BD antes (si ya la tienes, no te saldrá el error).

## Tarea 3 · WordPress: descargar, copiar y dar permisos

```bash
cd /tmp                                              # carpeta temporal: "para dejar cosas y se va limpiando"
wget https://wordpress.org/latest.tar.gz             # (guía) siempre la última versión
tar xf latest.tar.gz                                 # se crea la carpeta wordpress/
ls wordpress                                         # (clase) wp-admin, wp-content, wp-includes...
```

- `wget` baja el fichero (el profesor copia el enlace de la web de WordPress, "para que veáis que no os miento").
- `tar xf` descomprime un `.tar.gz`. Si descargas el `.zip` (`latest.zip`), se usa `unzip` (en clase hubo un alumno con zip; **(mío)** puede que haya que instalar `unzip`).
- `/tmp` es una carpeta temporal: sirve para descargas ("yo lo descargo y luego lo muevo").

```bash
sudo rm -f /var/www/html/blog.desplegando123.com/index.html     # (guía) sin esto Apache sigue sirviendo tu página de ayer
sudo cp -r wordpress/* /var/www/html/blog.desplegando123.com/   # (guía) copia el CONTENIDO, no la carpeta wordpress
sudo chown -R www-data:www-data /var/www/html/blog.desplegando123.com
```

> [!important] Copiar el **contenido** (clase)
> "Yo no quiero WordPress puro", sino que lo de dentro cuelgue **directamente** de la carpeta del sitio (`wp-admin`, `wp-content`…, `index.php`). Por eso `wordpress/*` y por eso se borra el `index.html`. Si lo copias entero, tendrías `blog…/wordpress/` y el sitio sale en blanco o con la página vieja.

> [!warning] Confusión en el audio: borrar la carpeta
> El profesor empezó diciendo "borrarlo", luego "no borrarlo" y avisó "ten cuidado con `rm -rf` de `/var/www/html/blog…`". **Haz lo que dice la guía:** borrar **solo el `index.html`**, nunca la carpeta del sitio.

### `chown`: por qué hace falta (clase)

```bash
ls -l /var/www/html/               # ver propietario: root
sudo chown -R www-data:www-data /var/www/html/blog.desplegando123.com
ls -l /var/www/html/blog.desplegando123.com
```
Lo copiaste con `sudo`, así que todo es de **root**. WordPress se ejecuta como **`www-data`** (el usuario de Apache) y necesita **escribir** (crear `wp-config.php`, `.htaccess`, subidas, actualizaciones). Si es de root, falla o da *Forbidden*/permisos. `-R` = recursivo; formato `usuario:grupo`.

### Fichero de configuración (guía)

```bash
cd /var/www/html/blog.desplegando123.com
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php
```
Cambia estas tres líneas:
```php
define( 'DB_NAME', 'wordpress' );
define( 'DB_USER', 'wpuser' );
define( 'DB_PASSWORD', 'UnaClaveFuerte' );
```
Y sustituye el bloque de **claves únicas (salts)** por el que genera `https://api.wordpress.org/secret-key/1.1/salt/` (no obligatorio para arrancar, "pero sí para que sea seguro").

> [!important] Dos formas de dar los datos de la BD
> | Forma | Quién la usó | Cómo |
> |---|---|---|
> | Editar `wp-config.php` | **Guía** | A mano, como arriba |
> | Rellenar el formulario del asistente | **Profesor en clase** | WordPress genera `wp-config.php` solo (por eso el `chown` antes de abrir el navegador) |
>
> Valen las dos y acaban igual. Con el asistente, los datos son: **BD** `wordpress`, **usuario** `wpuser`, **contraseña** la tuya, **servidor** `localhost`, **prefijo** `wp_` (por defecto). El profesor avisó: "**ojo: pon `wordpress` en el nombre de la base de datos**" (hay quien dejaba otro valor y daba error de conexión). Es probable que el asistente también genere los salts por su cuenta (**(mío)**, sin verificar en la documentación de esta versión); con la guía hazlos a mano.

## Tarea 4 · Terminar la instalación por el navegador

1. Abre `http://blog.desplegando123.com/` → asistente de WordPress (si pide datos de BD, los de la Tarea 2).
2. Rellena: **título del sitio**, **usuario administrador**, **contraseña**, **correo**.
3. Casilla de visibilidad en buscadores: el profesor la marcó para **disuadir a Google de indexar** (es un laboratorio).
4. *Instalar* → entra en `http://blog.desplegando123.com/wp-admin`.

> [!warning] Credenciales del administrador
> La contraseña de **administrador de WordPress** es distinta de la de la **base de datos**. Aunque en clase se usó la misma "por vagancia", en un servidor real no. Y el nombre de usuario `admin` es el que más se ataca: elige otro (**(mío)**, buena práctica general).

**Qué tienes que ver (guía):** el asistente (no página en blanco ni "Error de conexión"), y al acabar un blog en tu dominio. El profesor: "iros a vuestro **móvil** y ponéis el blog: ya tenéis una página subida en Internet". Es real, no "de mentira" como el XAMPP local de IAW.

### Verificar en la base de datos (clase)

```bash
sudo mariadb         # o: sudo mysql
```
```sql
SHOW DATABASES;                       -- aparece wordpress
USE wordpress;
SHOW TABLES;                          -- vacía antes del asistente; tras instalar, las tablas wp_...
SELECT user_login, user_pass FROM wp_users;   -- tu admin y su hash
```
- Antes del asistente la base **está vacía**; después aparecen las tablas (`wp_users`, `wp_posts`…).
- Lo de `user_pass` es un **hash con sal**. El profesor dijo **bcrypt**. Es **probable** que sea así en las versiones nuevas (WordPress 6.8 cambió a bcrypt; antes usaba "phpass"). Sin verificar con tu versión: mira si empieza por `$wp$2y$`.
- Se puede romper ese hash **solo si la contraseña está en el diccionario** (pregunta a la clase: *rockyou*) o por fuerza bruta (muy costosa con una contraseña larga). Conecta con **Ciber** (John the Ripper, diccionarios).

> [!important] Endurecimiento que comentó el profesor
> - **Cambiar los valores por defecto**: el prefijo `wp_` de las tablas y el nombre de usuario (por defecto `admin`). Con el prefijo conocido, una **inyección SQL** sabe qué tabla atacar (`wp_users`). En el laboratorio "da igual"; en un caso real se cambia en el asistente (campo *Prefijo de la tabla*).
> - **Borrar `info.php`.**
> - Es un sitio "muy vulnerable" porque es real y público.

## Si algo no funciona (guía + clase)

| Síntoma | Casi siempre es… | Arreglo |
|---|---|---|
| El navegador **descarga** el fichero o enseña código PHP | Falta `libapache2-mod-php` o no reiniciaste Apache | `sudo apt install libapache2-mod-php` + `sudo systemctl restart apache2` |
| «Falta la extensión MySQL de PHP» (clase) | No instalaste `php-mysql` | `sudo apt install php-mysql -y` + reiniciar Apache |
| «Error al establecer conexión con la base de datos» | Datos mal en `wp-config.php` (o en el asistente), o BD/usuario sin crear | Revisa nombre, usuario, contraseña y que exista (`SHOW DATABASES;`) |
| Sigue saliendo la página de ayer | No borraste `index.html` o no copiaste WordPress en **esa** carpeta | Borra el `index.html`; `ls` de la carpeta del sitio |
| «Forbidden» o permisos | Falta el `chown -R www-data:www-data` | Repite el `chown` |
| No carga el sitio con `https://` | Aún no hay certificado | Usa `http://` (HTTPS en la Clase 9) |
| Ves la página antigua tras cambiar | Caché del navegador | Otro navegador / ventana privada |

## HTTPS: dos formas (guía)

El candado se pone con **Certbot** (Let's Encrypt), que se explicó en la **Clase 9** (10/11): ver [su nota](2026-11-10_clase9-https-certbot-moodle.md), con Certbot por apt y por snap.

| Forma | Cuándo | Qué hay que hacer |
|---|---|---|
| **HTTPS al final** (lo normal) | Instalas por HTTP y pones el certificado al terminar | Tras Certbot: panel → *Ajustes → Generales* → pon `https://` en las **dos** URLs (o en `wp-config.php`). Si no, "contenido mixto" y fallos de recursos |
| **HTTPS primero** (más limpio, si da tiempo) | Montas el certificado con Certbot **antes** de instalar WordPress | WordPress guarda ya su URL con `https` y no hay que tocar nada. **Recomendada si vais sobrados de tiempo** |

El profesor dijo que lo explica el próximo día ("cómo sería la instalación del HTTPS").

## Extras (web), por si quieres dejarlo más completo

> [!note] Todo lo de esta sección es **(web)/(mío)** y no lo hizo el profesor.

- **Versiones recomendadas por WordPress (oficial, wordpress.org/about/requirements):** PHP **8.3 o superior**, **MariaDB 10.11+** o MySQL 8.0+, Apache o Nginx con `mod_rewrite`, y HTTPS recomendado. PHP 7.4 y MySQL 5.5.5 siguen funcionando pero están fuera de soporte. Comprueba las tuyas: `php -v` y `mariadb --version`. Con Ubuntu 24.04 es **probable** que cumplan, pero no lo he verificado en tu máquina.
- **Enlaces permanentes (permalinks) bonitos:** necesitan `mod_rewrite` y que Apache respete el `.htaccess`:
  ```bash
  sudo a2enmod rewrite
  sudo systemctl restart apache2
  ```
  y en el `<VirtualHost>` del sitio (o `apache2.conf`), la directiva `AllowOverride All` (por defecto está en `None`). Fuente: IONOS, *How to install and configure Apache for WordPress*. Si los enlaces bonitos dan 404, es casi siempre esto.
- **Permisos de ficheros (convención general de WordPress, sin verificar en la fuente oficial hoy):** carpetas `755`, ficheros `644` y `wp-config.php` más restrictivo (`640` o `600`). **Nunca `777`.** `chown -R www-data` es cómodo en laboratorio; en producción se suele dejar el código a otro usuario y dar escritura a `www-data` solo donde haga falta (`wp-content/uploads`).
- **Endurecer MariaDB:** `sudo mysql_secure_installation` (quita usuarios anónimos y la BD de prueba). La guía no lo pide.
- **Tras instalar:** *Ajustes → Enlaces permanentes*; actualizar WordPress, temas y plugins; usar solo plugins de confianza.

## El segundo gestor de contenidos y las ideas del profesor

- **Actividad 1:** WordPress aquí = criterio 4 (20 %). **Un segundo CMS** (Joomla, Drupal, PrestaShop… o Moodle) se monta **igual**, en **otro subdominio** y se hace en el campus (guía). El profesor propone **Moodle** como trabajo en casa ("para montar una academia"): **lo subirá al foro**. También dijo que en clase hará otros CMS más adelante. Texto de la guía: "lo montas igual".
- **Estado de la actividad:** al revisar el enunciado en pantalla, el profesor concluyó que con esto "estaría acabadísimo" y que le faltaría el HTTPS (audio confuso, sin confirmar). El enunciado no lo tengo.
- **Softaculous (audio confuso, "soft locos")**: es **probable** que sea **Softaculous**, un autoinstalador **de pago** que el profesor usa como **catálogo de aplicaciones web instalables**. Menciona, a modo de ideas (varias en audio confuso, **sin confirmar** los nombres):

  | Tipo | Ejemplos citados |
  |---|---|
  | Blogs / CMS | WordPress, Joomla, PrestaShop (tienda), Open Real Estate (inmobiliaria), AbanteCart (¿"ante car"?) |
  | Educación | Moodle, Chamilo |
  | Foros | phpBB, SMF |
  | Nube privada | ownCloud |
  | Correo | Roundcube ("ronquiube") |
  | Wiki | MediaWiki |
  | Base de datos | phpMyAdmin |
  | Otros | tickets/soporte, encuestas, calendario, galería, chat, música (Ampache)… |

  "Todo esto lo podéis tener en vuestro servidor", todo gratuito. Algunas (ownCloud, correo) volverán en temas posteriores.

## Segundo gestor: Moodle · guía oficial `SER_Lab04_Moodle_Guia.pdf` (3 págs., recibida el 25/11)

> [!note] Qué es esta guía
> Es el documento de Moodle que el profesor dijo que subiría. Es del Lab 4 (4/11), pero no se hizo en directo: **la clase de Moodle en directo fue el 10/11** (ver [nota del 10/11](2026-11-10_clase9-https-certbot-moodle.md)). Sirve como **segundo gestor** (criterio de 20 %). **(Mío)** La guía usa el subdominio `aula.`; en clase se usó `academia.`; el nombre es libre.

Moodle es un **LMS** (gestor de aprendizaje): cursos, usuarios, tareas, cuestionarios. Mismo tipo de web dinámica que WordPress (PHP + BD) pero **más exigente**: más extensiones de PHP y carpeta de datos propia. Orden: **sitio (DNS + VirtualHost) → PHP y extensiones → MariaDB → `moodledata` → descargar Moodle → asistente**.

```bash
# Paso 0 · sitio: registro A "aula" -> <ELASTIC-IP> (BIND9 o registrador) y su VirtualHost
sudo mkdir -p /var/www/html/aula.desplegando123.com
sudo nano /etc/apache2/sites-available/aula.desplegando123.com.conf
#   <VirtualHost *:80>
#       ServerName aula.desplegando123.com
#       DocumentRoot /var/www/html/aula.desplegando123.com
#   </VirtualHost>
sudo a2ensite aula.desplegando123.com.conf
sudo systemctl reload apache2
host aula.desplegando123.com            # tiene que dar tu Elastic IP

# Paso 1 · PHP y extensiones (más que WordPress)
sudo apt update
sudo apt install -y php libapache2-mod-php php-mysql \
    php-xml php-mbstring php-curl php-zip php-gd php-intl php-soap
sudo systemctl restart apache2
# max_input_vars >= 5000 en /etc/php/8.3/apache2/php.ini (ajusta la versión), luego restart apache2

# Paso 2 · MariaDB en utf8mb4 (lo exige Moodle)
sudo apt install -y mariadb-server       # si no la instalaste con WordPress
sudo mysql
```
```sql
CREATE DATABASE moodle DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'moodleuser'@'localhost' IDENTIFIED BY '<TU-CLAVE-FUERTE>';
GRANT ALL PRIVILEGES ON moodle.* TO 'moodleuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
```bash
# Paso 3 · carpeta de datos FUERA del sitio web
sudo mkdir -p /var/moodledata
sudo chown -R www-data:www-data /var/moodledata
sudo chmod -R 0770 /var/moodledata

# Paso 4 · descargar y colocar (enlace .tgz de download.moodle.org; cambia según la versión)
cd /tmp
wget <enlace-del-.tgz>
tar xf moodle-latest-*.tgz
sudo cp -r moodle/* /var/www/html/aula.desplegando123.com/
sudo chown -R www-data:www-data /var/www/html/aula.desplegando123.com
# Paso 5 · navegador: http://aula.desplegando123.com/  -> asistente
```
> [!important] Datos que pide el asistente (guía)
> Ruta de `moodledata` = **`/var/moodledata`**; tipo de BD = **MariaDB**; BD `moodle`, usuario `moodleuser` y su contraseña. Acepta las comprobaciones, deja crear las tablas y crea el administrador. **Qué tienes que ver:** la página de requisitos (casi todo en verde) y después el panel.

> [!important] Por qué `moodledata` fuera de `/var/www` (guía)
> Si estuviera dentro del sitio, cualquiera podría **descargar por HTTP** los ficheros privados (tareas, copias). Fuera del `DocumentRoot`, Apache no los sirve. **Permisos: `0770`** (la guía zanja la duda del audio del 10/11, donde se oyó «0, 7, 7, 0»).

| Síntoma | Casi siempre es… |
|---|---|
| Requisito de PHP en rojo | Falta una extensión (`php-xml`, `php-intl`, `php-zip`, `php-gd`…): instálala y reinicia Apache |
| `max_input_vars` en rojo | Ajuste de `php.ini` del paso 1 |
| «No se puede conectar a la base de datos» | BD/usuario mal, o no la creaste en **utf8mb4** |
| «No se puede escribir en moodledata» | `chown www-data` y `chmod 0770` |
| El sitio no abre por su nombre | Falta el registro A o su VirtualHost |

**HTTPS (guía):** con Moodle importa más que con WordPress. *Al final:* tras Certbot, edita **`$CFG->wwwroot`** en `config.php` con `https://`; tiene que ser **exactamente la URL real** o no arranca (**bucle de redirección**). *Primero (recomendada):* Certbot antes de instalar, y el `wwwroot` nace con `https`. Un único `certbot --apache` cubre todos los subdominios. **Antes de cerrar:** anota subdominio, BD, usuario y ruta de `moodledata`; **Stop** (nunca Terminate).

> [!warning] Aviso (mío, con la nota del 10/11): la guía puede quedarse corta con versiones nuevas
> La guía **no menciona** que en **Moodle 5.1+** el `DocumentRoot` debe apuntar a **`.../public`**; en clase del 10/11 la web salió **en blanco** por eso (ver nota del 10/11). Si descargas la «última versión estable» y te sale en blanco, no es un fallo tuyo: revisa ese `DocumentRoot` (en el `.conf` del 80 **y** en el del 443). Es probable que la guía esté escrita para una versión anterior; **no lo he verificado con la versión actual**.

## WordPress: la guía ya estaba aplicada
`SER_Lab04_WordPress_Guia.pdf` (3 págs.) es la que ya usaba esta nota como fuente; la he vuelto a comparar y **no hay cambios** respecto a lo anotado (PHP, MariaDB, ficheros, asistente, tabla de síntomas, las dos formas de HTTPS y el cierre).

## Cierre del laboratorio

- [ ] Borrar `info.php`.
- [ ] Apuntar en tu documentación: **BD, usuario y subdominio** de WordPress, y capturas (asistente, panel, el blog visto desde fuera).
- [ ] **EC2 → `srv_dns` → Stop** (nunca *Terminate*). **No liberes** la Elastic IP ni el dominio.
- [ ] (En casa) Moodle u otro CMS en otro subdominio.

## Dudas y cosas sin confirmar

- ✅ **Guía de Moodle**: recibida el 25/11 (sección propia arriba). Sigue sin recibir **el enunciado de la Actividad 1**.
- **HTTPS en la Actividad 1**: sin confirmar el alcance (el material de la Clase 7 y esta guía lo incluyen).
- **Hash**: bcrypt/`$wp$2y$` es probable, no verificado en tu instancia.
- **Nombres de aplicaciones** de la lista (audio confuso): ver tabla.
- **Tutorías** (aparte): el profesor planteó si las tutorías deben seguir siendo laboratorios/actividades en lugar de teoría; pide que se lo digáis directamente o a través del delegado. No es evaluable.
- Frase del final: pidió dudas "de sistemas" a él antes que a otros profesores; sin valor de estudio.
