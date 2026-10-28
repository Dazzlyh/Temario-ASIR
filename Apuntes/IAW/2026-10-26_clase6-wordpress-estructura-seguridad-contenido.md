---
asignatura: Implantación de Aplicaciones Web (IAW)
fecha: 2026-10-26
tema: Tema 3 · WordPress después de instalarlo: estructura de carpetas, wp-config.php, seguridad básica, entradas (categorías/etiquetas), Gutenberg, posts vs páginas, landing page
fuente: transcripción de la clase en directo + notas de Dani. El PDF «Tema 3 · Sesión 1 · Instalación de gestores de contenidos» enviado con esta clase corresponde a la clase del 19/10 (ver nota en ese día)
---
# IAW · Clase 6 (26/10) · WordPress por dentro: carpetas, `wp-config.php`, seguridad y contenido

> Anterior: [Clase 5 (19/10): CMS, licencias e instalación de WordPress](2026-10-19_clase5-cms-wordpress-instalacion.md) · Profesor: Jairo Bahillo Calvo

Se retoma el WordPress que se instaló "en blanco" el 19/10. Demo en la máquina virtual del profesor (XAMPP en Windows, carpeta `htdocs/wordpress`, base de datos `IAW`).

## Lo imprescindible

> [!important] Lo que el profesor marcó como importante
> - **Entrar al panel de administración**: `http://<servidor>/<carpeta>/wp-admin` (p. ej. `localhost/wordpress/wp-admin`). Mucha gente prueba `/admin` y no funciona. Si entras por la raíz eres usuario "normal" (visitante).
> - **`wp-config.php`**: dónde se guardan los datos de conexión a la base de datos. "Este fichero es muy importante que lo conozcamos."
> - **Diferencia entre categoría y etiqueta**: según el profesor **fue pregunta del examen del año pasado** (no asegura que se repita). Ver sección propia.
> - **Diferencia entre post (entrada) y página (page)** y qué es una **landing page**.
> - **Dónde se guarda el contenido**: en la tabla **`wp_posts`** de la base de datos (con el prefijo de tu instalación). Ojo: tus notas dicen "wp-post"; el nombre correcto es `wp_posts` (con guion bajo y en plural).
> - El examen de esta parte **no sabe aún cómo lo va a hacer práctico**; los últimos temas sí serán prácticos.

## 1. Estructura de WordPress: carpetas y ficheros

Dentro de la carpeta del sitio (`htdocs/wordpress`):

| Carpeta / fichero | Qué contiene | Quién lo toca |
|---|---|---|
| **`wp-admin/`** | Todo el panel de administración | Nadie: es del núcleo |
| **`wp-includes/`** | **Núcleo**: funciones y librerías en las que se basa WordPress (también certificados, plantillas internas, actualizaciones) | Un usuario normal **no debe tocarlo**; solo si desarrollas a fondo |
| **`wp-content/`** | **Tu parte**: `themes/` (temas), `plugins/`, `languages/` (idiomas) y lo que subes | Es donde se trabaja y donde se pone más énfasis en este módulo |
| **`index.php`** | Punto de entrada: cuando el navegador entra a una carpeta sin indicar fichero, busca `index.php` | |
| **`wp-config.php`** | Conexión a la BD, claves de seguridad, prefijo de tablas, depuración | **Importante** |
| **`.htaccess`** | Reglas de Apache | Útil para bloquear accesos (ver seguridad) |

- Habrá que conocer las funciones/librerías y **la versión de WordPress** sobre la que desarrollas temas o plugins.
- Plugins preinstalados que se vieron en `wp-content/plugins/`: **Akismet** (antispam, carpeta con muchas clases) y **Hello Dolly** (un solo `hello.php`; es una broma de la comunidad que sirve como ejemplo de plugin mínimo).
- Cada plugin completo trae un **`readme.txt`**: el profesor insiste en **leer y escribir siempre documentación** (README, changelog) en los proyectos propios, y en el TFC si usas Git/GitHub.
- **Traducciones**: en `wp-content/languages/` hay ficheros por idioma; se pueden editar para cambiar textos (ejemplo del profesor: cambiar "Sunday" por "domingo" para un dialecto concreto). Los ficheros de texto se "compilan" a otro formato para que WordPress los lea; el profesor dijo la extensión de forma confusa. Es probable que sea `.po` (editable) → `.mo` (compilado), pero **no está confirmado en la transcripción**.

## 2. `wp-config.php`

Se abre con un editor de texto (Notepad) y contiene los datos que se rellenaron en el instalador:

```php
define( 'DB_NAME', 'IAW' );
define( 'DB_USER', 'root' );
define( 'DB_PASSWORD', '' );
define( 'DB_HOST', 'localhost' );
$table_prefix = 'wp_';
```

- También: las **claves de seguridad (secret keys/salts)** y `WP_DEBUG` (el profesor dijo que lo vería al final de la clase, **no llegó a verlo**; queda pendiente).
- Si la instalación salió mal o hay que cambiar un dato (host, usuario, prefijo), se **edita aquí directamente**.
- **Los datos van en texto plano**; el profesor avisa de que en producción se ocultan o cifran y se rotan. Aquí solo hay que saber dónde están.
- Las líneas comentadas aparecen con `/* */` o `//` (el profesor dijo "asterisco").
- Según el PDF del 19/10: si cambias el puerto de MySQL, el host puede ser `localhost:3340` (ejemplo del PDF, no de esta clase).

## 3. Seguridad básica (de la clase y de la demo)

> [!important] Medidas que explicó, con su peso real
> 1. **Cambiar el prefijo de tablas** (`wp_` por defecto): "es un **1 % más** de seguridad; no penséis que os va a salvar de nada". Razón: con una inyección SQL el atacante sabe cómo se llaman las tablas. Se elige en la instalación (campo "prefijo") o en `$table_prefix` de `wp-config.php`.
> 2. **No dejes un usuario llamado `admin`**: es el primero que se prueba. En la demo el usuario era `Jairo`, no `admin`.
> 3. **No cambies la contraseña del administrador real en una auditoría/ataque**: el dueño lo notaría. Crea otro usuario con los mismos permisos (comentario de seguridad ofensiva del profesor).
> 4. **Bloquear el acceso con `.htaccess`** si una web tiene una versión vulnerable y no puedes parchearla (lo hizo con una web suya afectada por un fallo de PHP; **no detalló cuál**, sin confirmar).
> 5. En local, `root` sin contraseña es válido solo para pruebas.

### Recuperar el acceso: cambiar la contraseña desde phpMyAdmin (demo de clase)

El profesor no recordaba su contraseña (además había escrito mal el usuario: era `Jairo`, no `admin`). Lo arregló así:

1. phpMyAdmin → base de datos `IAW` → tabla **`wp_users`** → editar la fila del usuario.
2. En la columna **`user_pass`**, elegir la **función `MD5`** en el desplegable e introducir la contraseña **en claro**; guardar.
3. Al guardar, el campo queda convertido en un hash largo (letras y números) y ya se puede entrar con la contraseña nueva.

> [!warning] Matiz sobre "MD5"
> El profesor dijo que WordPress "encripta en MD5" y que MD5 no se podía "crackear". Dos matices: **MD5 es un hash, no cifrado**, y **sí se puede revertir** con tablas precomputadas/bases de datos de hashes (él mismo lo explicó con las webs de "verificador de hash"). Además, mi conocimiento es que las versiones modernas de WordPress guardan las contraseñas con otro formato (phpass o bcrypt) pero siguen aceptando un MD5 escrito a mano en `user_pass` y lo regeneran al iniciar sesión. Esto **no se vio en clase**. En el 19/10 el propio profesor ya había dicho que el formato no era exactamente MD5.

- Enlace con seguridad: si un atacante consigue lanzar una **SQL injection** (`UPDATE` sobre `wp_users`), puede cambiarse la contraseña de cualquier usuario.

## 4. Contenido: entradas, categorías y etiquetas

### Crear una entrada
Panel → **Entradas → Añadir nueva**. Se escribe el título y se construye el contenido con bloques.

### Categorías vs etiquetas (pregunta de examen del año pasado)

| | **Categoría** | **Etiqueta (tag)** |
|---|---|---|
| Estructura | **Jerárquica** (categoría padre y subcategorías) | **Plana**, sin jerarquía |
| Función | Grandes grupos para organizar (se suelen mostrar en un **menú desplegable**) | Palabras clave concretas que sirven para **buscar** (los buscadores internos indexan sobre todo las etiquetas) |
| Cantidad típica | **1, como mucho 2** por entrada/producto | **10-13** por producto (recomendación de Shopify y Etsy, según el profesor) |
| Ejemplo (clase) | `Clase` → `IAW` → `WordPress` | `camiseta verde`, `camiseta goku`, `oversize`, `algodón` |

Reglas prácticas del profesor para las etiquetas:
- Sé **específico**: `camiseta verde`, no solo `verde` ("no funciona bien").
- **Sin artículos ni determinantes** (`camiseta de ñu`, no `la camiseta del ñu`): se indexan peor.
- Los espacios están permitidos; WordPress los limpia internamente.
- Categorías = "de qué trata", etiquetas = detalles buscables.

### Gutenberg: el editor de bloques
- Es el sistema que **construye la página con bloques** (encabezado, párrafo, imagen, galería, botones, código…). Se pueden mover y reordenar. La presentación de la sesión explica Gutenberg (no recibida).
- **Elementor** (plugin constructor visual): "el más importante que existe" según el profesor, con millones de descargas.

### Imágenes y derechos de autor
- No enlaces imágenes por **URL externa**: si el otro sitio cambia o borra la imagen, la pierdes ("dejas de depender de ti"). WordPress avisó de que las imágenes de otros dominios pueden cargar lento, verse mal o desaparecer, e impidió publicar. **Descarga la imagen, súbela a la mediateca (en JPG/PNG…)**.
- **Cuidado con los derechos de autor**: te pueden reclamar. Usa bancos de imágenes gratuitos, lee su licencia y cita la fuente.
- **SEO de imágenes**: rellena siempre el atributo **`alt`** de `<img>`; renombra el fichero con sentido.
- Texto de relleno: **Lorem ipsum** (generador de "latín raro").
- **Extracto**: para que en el listado solo se vea el primer párrafo y "Leer más". **Vista previa** responsive: móvil, tableta, ordenador.
- En modo blog las entradas salen **de más nuevas a más antiguas**.

## 5. Dónde se guarda el contenido: `wp_posts`

```sql
SELECT ID, post_title, post_status, post_type FROM wp_posts;
```

- Columnas vistas en clase: `ID` (en mayúsculas; el profesor tuvo un error por escribirlo mal), `post_title`, `post_status`, `post_type`, además del autor.
- **Cada estado y cada tipo genera su propia fila**: borrador, en revisión, publicado… y `post_type` distingue **post** de **page**.
- Para recordar: **todo (entradas Y páginas) se guarda en la misma tabla**, y `post_type` dice cuál es cada una. Los valores concretos (`publish`, `draft`, `revision`, `auto-draft`) son mi conocimiento, no se leyeron todos en clase.
- El **autor** existe porque WordPress nació para blogs y revistas multiusuario: cada autor asume lo que firma.

## 6. Post vs página; landing page

| | **Entrada (post)** | **Página (page)** |
|---|---|---|
| Qué es | Una **noticia/artículo** del blog, ordenada por fecha | Contenido **estático** que casi no cambia |
| Ejemplos | Noticias de la empresa, novedades de producto | FAQ, términos y condiciones, política de privacidad, envíos, devoluciones, "Sobre nosotros" |
| Categorías/etiquetas | Sí (en la clase se usaron en entradas) | Normalmente no (mi conocimiento; no dicho en clase) |

- WordPress incluye por defecto "Hola mundo" (post), "Página de ejemplo" y "Política de privacidad".
- **Landing page** = página de entrada/portada de una web (ejemplo: la web de UNIR). Hoy casi todas las landings de empresa son **páginas**, no posts.
- **Una web sin blog es estática**: siempre igual hasta que la empresa cambie algo, y **el SEO baja** si no se actualiza. Solución: un **blog** con noticias nuevas ("la carnicería que cuenta que llega chuletón de vaca rubia gallega"). Cualquier sector puede hacerlo.
- **SEO**: posicionamiento orgánico en buscadores (puntuación). Se mejora con `alt` en imágenes, nombres de fichero, contenido actualizado y plugins como **Yoast SEO**.
- **BuiltWith**: web a la que le pasas una URL y te dice con qué tecnología está hecha (se vio que la web de UNIR usa WordPress; el profesor dijo que lo cree por los plugins detectados).

## 7. Plantillas y plugins (para casa)

- **Mercado de plantillas**: el profesor mostró **Envato Market** (en la transcripción sale "Levanto"). Hay plantillas de pago (ejemplo ~29 $) y gratuitas con filtro. Se descarga, se instala en WordPress y queda el sitio con el aspecto de la vista previa.
- Flujo típico de un proyecto real: **hosting → instalar WordPress con un clic → plantilla → cambiar bloques, títulos y fotos**.
- **Marketplace de plugins** propio de WordPress. Ideas de plugins: SEO, formularios de contacto, pagos, transporte, seguridad, tienda (**WooCommerce** + PayPal/Stripe).
- Historia: hace unos años se vendían plugins a medida (ejemplo: el de **recordatorio de carrito abandonado**, ~350 €). Hoy la IA permite hacerlos, pero hay que valorar el tiempo de desarrollo.
- El profesor subirá plantillas gratuitas al foro si le llegan.

## 8. Logística y TFC (dicho en esta clase)

- **Actividad del trimestre de IAW**: **no la empieces todavía**. Las que están subidas son genéricas y las va a **cambiar** el profesor.
- **Dos semanas sin clase** de IAW (los dos lunes siguientes, 2/11 y 9/11; por tanto, la siguiente clase sería el **16/11**, sin confirmar). Quiere que a la vuelta **cada uno tenga su WordPress** con las cosas que quiera (no es obligatorio; que juguéis, instaléis una plantilla).
- Para casa: **Apariencia → cambiar tema y crear menú** (son los entrenamientos) y **añadir plugins**.
- **TFC (parte de IAW)**: el profesor pone la nota de IAW de **todos los grupos**, lleve o no él el proyecto.
  - Debe haber **alguna parte cliente** (front, landing page o interfaz) **desplegada**. WordPress cumple como mínimo.
  - **No vale instalar la web en XAMPP en el proyecto** ("te pongo mala nota"): **como mínimo en Docker**. XAMPP solo vale en clase.
  - Se puede usar otra tecnología (Vue, etc.); el JavaScript del curso no da para una web completa.
  - Pregunta de Sol sobre desplegar en un servicio tipo Netlify: aceptable para el requisito de despliegue (la transcripción dice "Netflix", es "Netlify" por contexto, **sin confirmar**).
- Próxima clase: terminar el Tema 3 (queda **rendimiento** y un par de cosas importantes), instalar plantillas y plugins, y `WP_DEBUG`.
- Tenía una "infografía" sobre un fallo de PHP de la semana pasada; **no llegó a enseñarla**.

## Si algo no funciona

| Síntoma | Causa probable | Qué hacer |
|---|---|---|
| No entras a `/admin` | La ruta correcta es `/wp-admin` | `http://localhost/<carpeta>/wp-admin` |
| La contraseña no entra | Usuario mal escrito (no era `admin`) o contraseña olvidada | Ver el usuario en `wp_users`; cambiar `user_pass` con función `MD5` |
| Error al consultar `wp_posts` | Columna mal escrita (`id` ≠ `ID`) | `ID`, `post_title`, `post_status`, `post_type` |
| La imagen no se publica | Enlazada por URL externa | Descargarla y subirla a la mediateca |

## Dudas y cosas sin confirmar

- La **presentación de esta sesión** (con Gutenberg y estructura de carpetas) no la he recibido. El PDF adjunto es de la sesión del 19/10.
- La extensión `.po`/`.mo` de las traducciones, el fallo de PHP del `.htaccess` y la fecha de la siguiente clase (16/11) están sin confirmar.
- El profesor no mostró cómo **cambiar el prefijo** en una instalación ya hecha. Cambiarlo después requiere renombrar tablas y actualizar opciones y metadatos internos (mi conocimiento, no visto en clase): lo más seguro es elegirlo al instalar.
- Examen: "en papel", formato práctico aún sin definir.

## Logística y para llevar a casa

- [ ] Tener **tu WordPress** funcionando, con una **plantilla** y un **menú** (Apariencia).
- [ ] Probar plugins (SEO, formulario de contacto, tienda con WooCommerce).
- [ ] Practicar la consulta `SELECT ID, post_title, post_status, post_type FROM wp_posts;`.
- [ ] Memorizar: **ruta `wp-admin`**, **qué hay en `wp-config.php`**, **categoría vs etiqueta**, **post vs página**, **dónde se guarda el contenido**.
- [ ] TFC: pensar en desplegar la parte web **en Docker**, no en XAMPP.
- [ ] No empezar la actividad del trimestre hasta que el profesor suba la nueva.
