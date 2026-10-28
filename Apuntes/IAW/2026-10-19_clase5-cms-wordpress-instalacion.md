---
asignatura: Implantación de Aplicaciones Web (IAW)
fecha: 2026-10-19
tema: Tema 3 · Sesión 1 · gestores de contenidos (CMS), licencias, instalación de WordPress sobre XAMPP
fuente: transcripción de la clase en directo + presentación «Tema 3 · Instalación de gestores de contenidos» (PDF, 15 págs.)
---
# IAW · Clase 5 (19/10) · Gestores de contenidos (CMS), licencias y primera instalación de WordPress

> Anterior: [Clase 4 (05/10): instalación de XAMPP y PHP básico](2026-10-05_clase4-xampp-php-basico.md) · Siguiente: [Clase 6 (26/10): WordPress por dentro](2026-10-26_clase6-wordpress-estructura-seguridad-contenido.md) · Profesor: Jairo Bahillo Calvo

> [!note] Corrección de etiquetado y discrepancia
> Esta clase es el **Tema 3 · Sesión 1** (así lo indica la presentación); una versión anterior la llamaba "Tema 2". El PDF del Tema 3 Sesión 1 se envió junto con la clase del 26/10, pero su contenido es el de esta clase del 19/10. **Discrepancia de requisitos**: en la transcripción se dijo "MariaDB 11", mientras que la presentación indica **MariaDB 10.11+** y **MySQL 8.0+** (PHP 8.3+ coincide). Prevalece lo que dice el PDF; el profesor lo leía en directo de la web de WordPress y puede haber citado otra versión.

Clase teórico-práctica: panorama de gestores de contenidos (CMS), tipos de licencia de software, requisitos técnicos de WordPress y, como colofón, **instalación en directo de WordPress sobre XAMPP** en la máquina del profesor (Windows).

## Logística y avisos
- El profesor confirmó que **no se ve Docker como contenido oficial del módulo** (el cronograma que él tenía aún lo marcaba, pero le han dicho que se quita). Aun así lo usa él personalmente y lo menciona de forma opcional durante la demo — "no es del módulo", quien quiera usarlo por su cuenta para practicar, perfecto, pero no es exigible.
- Recomienda aprovechar un curso de Docker ofrecido gratuitamente por otro profesor/módulo (mencionado como "Manu") para quien quiera profundizar.
- Recuerda que la presentación del Tema 2 ya está subida a la plataforma — insiste en que hay que leerla antes de clase.
- Avisa de que para la **próxima clase (el lunes siguiente)** cada alumno debe tener WordPress instalado y funcionando, **sea por el método que sea** (XAMPP local, Docker, hosting, dominio propio...): "me da igual la manera que lo hagáis, intentad al menos que sepáis que lo tenéis instalado, que es muy sencillo". El siguiente día se dedicará a instalar plugins y plantillas para mejorar el aspecto.
- Sobre el examen: el profesor repite que este es un módulo nuevo para él (lo imparte por primera vez) y que no sabe con certeza qué entrará en el examen final, que recuerda **es en papel**.

## Qué es un CMS (gestor de contenidos)
- **CMS** = Content Management System (sistema de gestión de contenidos). WordPress tiene una cuota de mercado enorme y mucha gente cree que es el único, pero existen muchos más.
- **Joomla**: todavía se enseña en algunos currículos e institutos, pero el profesor lo considera "atrasado" frente a WordPress, que se quedó como dominante del mercado.
- **Drupal**: se consideraba muy potente y "técnico", pero el profesor hace tiempo que no ve páginas reales hechas en Drupal (ni en Joomla).
- **Moodle**: también es un CMS, aunque se suele hablar de él como **LMS** (Learning Management System — cambia la "C" de Content por la "L" de Learning): es un gestor de contenidos especializado en centros educativos/cursos.
- **Wikipedia** también puede considerarse un tipo de gestor de contenidos (mención rápida, sin profundizar).
- Sistemas de **gestión documental** empresarial: ejemplo citado, SharePoint.
- Comparativa rápida de CMS "puros":

| CMS | Tipo | Valoración del profesor |
|---|---|---|
| WordPress | CMS genérico, código abierto | El dominante actual, el más usado |
| Joomla | CMS genérico, código abierto | Uso residual, considerado "atrasado" |
| Drupal | CMS genérico, código abierto | Muy técnico/potente en teoría, poco visto en la práctica |
| Moodle | LMS (CMS educativo) | Estándar para centros educativos/cursos |

## Sistemas de e-commerce especializados
- **Magento**: e-commerce muy potente orientado a empresas grandes. El profesor comenta que ha sido comprado por Adobe (dato que descubrió él mismo mirando antes de clase), lo que genera incertidumbre sobre su futuro/licencia.
- **PrestaShop**: alternativa que "sigue gustando muchísimo" al profesor, funciona muy bien.
- **Shopify**: modelo SaaS — no instalas nada, ya viene con decenas de plantillas, gestión de pagos, logística de envíos, etc. Se paga una suscripción a cambio de no tener que mantener nada.
- **WooCommerce**: no es un CMS/sistema independiente, es un **plugin dentro de WordPress** que añade funcionalidad de comercio electrónico. Es, junto con Shopify, de lo que más predomina hoy en el mercado de e-commerce.
- Comentario de un alumno (Jose Alejandro): cuando WordPress lanzó WooCommerce le "pegó un pelotazo" a Joomla, que hasta entonces tenía más auge en e-commerce — hubo un antes y un después en el mercado.
- Mención de **oscommerce/osCommerce** por otro alumno (Manuel): sistema de e-commerce antiguo (de hace 10-20 años), hecho directamente en PHP, hoy en desuso. El profesor no llegó a trabajar con él.

## Salidas profesionales / casos de uso reales
El profesor insiste en que, aunque la IA está cambiando el mercado (cualquiera puede montarse hoy una web sencilla con IA), sigue habiendo nicho real para pequeñas y medianas empresas:
- Tiendas online y locales.
- Catálogos sin precios para negocios que no venden online directamente (ejemplo: tienda de bicicletas que solo repara, pero publica catálogo de piezas).
- Páginas de ayuntamientos/entidades públicas con plantilla genérica replicada para varios municipios de una provincia (anécdota personal del profesor durante sus propias prácticas de FP).
- TFG/TFC: montar tiendas genéricas con estas herramientas es un proyecto habitual y válido.

## Tipos de licencia de software
El profesor remarca que esto es importante tenerlo claro (aunque no se entre en mucho detalle):

| Tipo de licencia | Características | Ejemplos |
|---|---|---|
| **Propietaria** | Se compra la licencia; normalmente **prohibido modificar** el software; se paga por usarlo | Comparable a Microsoft |
| **GPL** | El usuario **puede modificar y distribuir** el software libremente | WordPress, Joomla, Drupal |
| **SaaS** (Software as a Service) | No se compra ni se instala nada; se paga una **suscripción**; el proveedor se encarga de todo el mantenimiento y la seguridad | Shopify |
| **MIT** | Licencia permisiva, con pocas condiciones (mencionada de pasada, sin profundizar) | Apache y otros proyectos |

- Ejemplo práctico de licencia GPL dado por el profesor: en sus prácticas de FP tuvo que programar en PHP funcionalidades a medida (menús, botones, subida de ficheros) y luego "subirlas" dentro de instalaciones de WordPress de distintos ayuntamientos, algo que la licencia GPL permite (modificar y distribuir código basado en WordPress).
- Reflexión del profesor sobre el modelo SaaS: cada vez se usa más porque mucha gente, al crear un producto, no quiere encargarse después de mantenerlo (dominio, servidor, balanceo de carga, soporte a usuarios...); el SaaS traslada ese mantenimiento al proveedor a cambio de una suscripción. Esto conecta directamente con las salidas profesionales de ASIR: gestionar esa infraestructura y mantenimiento es justamente a lo que se dedica buena parte del ciclo.

## Requisitos técnicos de WordPress
Antes de instalar, el profesor repasa los requisitos recomendados actuales (consultados en la propia web de WordPress.org en directo):
- **PHP 8.3 o superior** (se puede usar una versión más antigua, pero entonces hay que descargar una versión de WordPress compatible con ella).
- **MySQL 8** o **MariaDB 11** (o superior).
- WordPress **necesita obligatoriamente ambas cosas** para funcionar: un servidor con PHP (lógica/programación) y una base de datos (todo el contenido). Por eso hace falta un stack completo tipo **XAMPP** ("SAM" en la transcripción, apache + PHP + MySQL/MariaDB) — exactamente lo instalado en la clase anterior.
- Explicación conceptual remarcada por el profesor: **PHP es la programación/lógica** (formularios, validaciones, seguridad...); **la base de datos es el contenido** (posts, páginas, usuarios...). WordPress, en tiempo de ejecución, es quien junta ambas partes.
- Todo en WordPress se guarda en tablas de base de datos — nació originalmente para blogs, así que su estructura original pensaba en entradas (posts) con título, cuerpo, fecha, etc., aunque hoy sirve para páginas web completas.
- **Es obligatorio crear la base de datos antes de lanzar el instalador de WordPress** (el propio instalador crea las tablas necesarias automáticamente — el usuario no tiene que crearlas a mano).

## Alternativa sin instalar nada: WordPress Playground
El profesor mostró brevemente **WordPress Playground** (wordpress.org/playground o similar), una web que simula un WordPress recién instalado directamente en el navegador (incluye acceso a phpMyAdmin simulado y hasta terminal de comandos), útil para quien quiera probar WordPress sin instalar nada en local. Aclaró que es solo una demo/simulación, no se puede usar para un proyecto real.

## Instalación en directo de XAMPP + WordPress (demo del profesor, en Windows)

> Nota: la demo se hizo en Windows con XAMPP. El profesor repitió varias veces que **el proceso es exactamente igual en Linux**, cambiando únicamente la ruta de instalación y el nombre del stack (ver nota personal más abajo).

### 1. Preparar el software
1. Descargar XAMPP desde la web oficial (el profesor tuvo que reinstalarlo porque no tenía la máquina preparada de antes). Advirtió de nuevo del aviso de la clase anterior sobre el **Control de Cuentas de Usuario (UAC)** en Windows.
2. Descargar WordPress en español desde **wordpress.org** (insistencia fuerte: "WordPress gratuito, por favor, que nadie se baje WordPress pagando" — hay sitios de pago/falsos que hay que evitar, usar siempre la web oficial). El fichero descargado es un **.zip de unos 35 MB**.
3. El propio ZIP de WordPress incluye un `readme.html` con los requisitos de instalación (el profesor lo menciona pero no entra en detalle, dice que el proceso manual que van a hacer en clase es más directo).

### 2. Colocar los ficheros de WordPress en `htdocs`
1. Dentro de la carpeta `htdocs` de XAMPP, crear una carpeta nueva, por ejemplo **`wordpress`** (o el nombre de proyecto que se quiera: `proyecto1`, `proyecto2`...).
2. Descomprimir el ZIP descargado.
3. **Trampa/error típico señalado explícitamente por el profesor**: al descomprimir, el ZIP genera una carpeta interna adicional (p. ej. `wordpress/` dentro de `wordpress/`), de forma que los ficheros quedan anidados un nivel de más. Si se deja así, al entrar a `localhost/wordpress` el servidor no encuentra un `index.php` en la raíz de esa carpeta y no funciona — habría que acceder a `localhost/wordpress/wordpress/...`.
4. **Solución aplicada en directo**: sacar (mover) todos los ficheros y carpetas del WordPress descomprimido **a la raíz** de la carpeta de proyecto (`htdocs/wordpress`), de modo que `index.php` quede directamente ahí. El profesor eliminó también un par de ficheros/carpetas sobrantes del propio ZIP ("para que no haya problemas") durante esta operación de limpieza.
5. Lección general remarcada: **las rutas son fundamentales en cualquier despliegue** — el servidor siempre busca primero un `index` al entrar en una carpeta; si no lo encuentra en la raíz esperada, hay que apuntar explícitamente a la subcarpeta real.

### 3. Primer intento de arranque (fallo esperado: sin base de datos)
1. Con Apache y MySQL arrancados desde el panel de XAMPP, el profesor accede a `localhost/wordpress`.
2. `index.php` redirige automáticamente a `wp-admin/setup-config.php`, que es el instalador de configuración de WordPress.
3. El profesor demuestra deliberadamente el **error de conectar antes de tener base de datos**: en el formulario de configuración introduce a propósito un nombre de base de datos inventado ("Pepe"), usuario y contraseña inventados — WordPress responde que no puede conectar ("no hay manera").
4. Conclusión pedagógica explícita (reforzada también con una pregunta de una alumna, María Eugenia, sobre qué pasa si se levanta primero WordPress y luego la base de datos): **si la base de datos no existe/no está levantada antes, WordPress no puede completar la instalación** — por eso el orden correcto es siempre: 1º crear/levantar la base de datos, 2º instalar o conectar WordPress a ella.

### 4. Crear la base de datos en phpMyAdmin
1. Entrar a **phpMyAdmin** desde el panel de XAMPP (MySQL).
2. Crear una base de datos nueva, en el ejemplo llamada **`IAW`**.
3. El profesor avisa de prestar atención a la **nomenclatura y la codificación (charset/collation)** al crear la base de datos, sin entrar en detalle porque asume que ya se ha explicado en el módulo de bases de datos (SGBD).
4. **No es necesario crear tablas manualmente** — solo la base de datos vacía; WordPress generará las tablas que necesita durante la instalación.

### 5. Completar el instalador de WordPress (`wp-admin/setup-config.php`)
Datos pedidos por el formulario de configuración de la base de datos:
- **Nombre de la base de datos**: `IAW` (la creada en el paso anterior).
- **Usuario de la base de datos**: `root` (credencial por defecto de XAMPP/MySQL).
- **Contraseña**: vacía (sin contraseña) — credencial por defecto de XAMPP en local. El profesor y los alumnos bromean sobre lo insegura que es esta configuración, pero es la estándar en local para pruebas; **nunca debe dejarse así en un entorno real/producción**.
- **Servidor de la base de datos**: `localhost` (en un hosting real puede no estar en el mismo servidor; el proveedor indica la ruta/host si es distinto).
- **Prefijo de tablas**: se deja el valor por defecto (`wp_`) para la demo.

Tras validar estos datos, WordPress genera el fichero **`wp-config.php`** (configuración de conexión a BBDD, equivalente a lo visto la clase anterior con variables de servidor en PHP) y permite continuar con la instalación.

### 6. Instalación final (datos del sitio)
Pantalla siguiente, "Bienvenido a WordPress":
- **Título del sitio**: en el ejemplo, "Clase IAW".
- **Nombre de usuario**: "Jairo" (aviso del profesor: usar un nombre de usuario que no sea trivial, es importante para seguridad — evitar `admin`).
- **Contraseña**: se recomienda una contraseña robusta (el profesor usó una contraseña de ejemplo poco segura a propósito, con tono de broma, pero insiste en que en real debe ser fuerte).
- **Email**: campo obligatorio.
- Checkbox **"Pedir a los motores de búsqueda que no indexen este sitio"**: útil mientras se está montando la web (para no aparecer en buscadores con contenido a medio hacer), pero **aviso importante**: hay que recordar desmarcarlo cuando el sitio esté listo para publicarse, porque mucha gente se olvida y el sitio nunca llega a indexarse en Google.
- Tras rellenar y pulsar instalar: WordPress queda instalado. El navegador puede ofrecer guardar la contraseña.

### 7. Comprobación en phpMyAdmin tras la instalación
- Al volver a la base de datos `IAW` en phpMyAdmin, ahora aparecen **12 tablas creadas automáticamente**, todas con el prefijo `wp_` (`wp_users`, `wp_posts`, etc. — nombres concretos no deletreados en la transcripción, pero confirmado el patrón `wp_...`).
- **Primer consejo de seguridad explícito del profesor**: cambiar el prefijo de tablas por defecto (`wp_`) por otro personalizado es una de las primeras recomendaciones de cualquier guía de seguridad de WordPress, porque los ataques automatizados asumen ese prefijo por defecto.
- En la tabla de usuarios se puede ver el usuario creado y la contraseña **cifrada** (el profesor comenta de memoria que WordPress usaba un hash tipo MD5, aunque al comprobarlo en directo no es exactamente ese formato — lo deja como dato aproximado, no cerrado).
- En la tabla de posts ya aparecen los contenidos de ejemplo que WordPress crea por defecto: "Hola mundo" (entrada de blog), "Página de ejemplo" y "Política de privacidad".

### 8. Primer vistazo al panel de administración (wp-admin)
- Tras la instalación, se accede al login y luego al panel de administración (`wp-admin`).
- El profesor muestra brevemente que se puede editar el título del sitio directamente desde el panel de ajustes (y que, de hecho, ese mismo valor podría cambiarse manualmente desde la propia tabla de la base de datos).
- Menciona que en instalaciones antiguas de WordPress existía una carpeta residual que había que borrar tras el setup por motivos de seguridad (vulnerabilidad conocida); en la versión actual probada en clase ya no apareció ese problema.
- Se enseña brevemente la sección de "Entradas" (Posts) con la entrada "Hola mundo" ya creada, mostrando edición básica.
- Cierre conceptual: así de "sencillo" es tener una web funcionando con WordPress — de aquí en adelante todo depende de plugins y plantillas (se verán en próximas clases), que es donde WordPress "habla bastante" según el profesor.

### Después de tener WordPress instalado: qué falta para un proyecto real
El profesor enlaza la demo con una reflexión sobre despliegue real:
- Con la plantilla/diseño y un certificado SSL (menciona **Let's Encrypt** como opción gratuita) ya casi está todo, pero falta lo más básico que a veces se da por hecho: **un dominio** que apunte, vía DNS, a la IP/servidor donde está alojado WordPress.
- Si se usa un **hosting** normal (recomienda mirar ejemplos como Hostinger), gran parte de esto viene automatizado: el proveedor ya ofrece WordPress preinstalado con un clic, un panel de control, usuario y correo configurados.
- Si no se usa un hosting con todo automatizado, es el propio técnico (rol que se espera de un ASIR) quien debe configurar DNS, servidor, certificados, balanceo, etc.
- **Buena práctica insistida con fuerza**: nunca instalar plugins/plantillas nuevas y sin probar directamente en un entorno de **producción**. Siempre hay que tener un entorno **local** (o un dominio/entorno de pruebas aparte) donde probar antes de pasar cualquier cambio a producción. El profesor lo remarca con la frase "no hagáis estas locuras" al hablar de instalar un plugin visto en redes sociales directamente en producción.

### Docker como alternativa (mención breve, fuera del temario oficial)
- El profesor mostró en pantalla (sin explicar línea a línea, "no da tiempo" y "no es del módulo") un ejemplo de **Docker Compose** con un contenedor de base de datos (MySQL o MariaDB, a elegir) y un contenedor de WordPress conectado a él.
- Puntos que sí remarcó, aplicables también fuera de Docker:
  - **Orden de arranque obligatorio**: primero debe levantarse el contenedor de la base de datos con sus credenciales, y solo después el contenedor de WordPress apuntando a esa base de datos — si se intenta al revés, WordPress no encuentra la base de datos y falla la conexión (igual que en el fallo deliberado mostrado con XAMPP).
  - Comentario de un alumno (Manuel) sobre la elección de motor de base de datos en el contenedor: opinión personal de que **MySQL es más estable que MariaDB cuando el volumen de registros es muy grande**, mientras que MariaDB sería más ligera/rápida para volúmenes pequeños — cada profesor/alumno usa el motor que prefiere, ambos son válidos para WordPress.
  - El comando de `docker compose` levantaría automáticamente ambos contenedores conectados, pero no se explicó el fichero YAML en detalle en clase.
- Conclusión del profesor: quien quiera usar Docker para instalar WordPress puede hacerlo perfectamente (es un camino alternativo igual de válido), pero **no es exigible para el módulo** — lo mínimo exigido es tener XAMPP/Apache+PHP+base de datos funcionando, sea como sea que se monte por debajo.

## Datos de la presentación (PDF) que complementan la clase

- **Repaso del Tema 2 (XAMPP)**: Apache puertos **80 y 443**, MariaDB **3306**, phpMyAdmin en `localhost/phpmyadmin`, la web va en `C:\xampp\htdocs` y se abre en `localhost/<carpeta>/`.
- **Licencias (4 tipos del PDF)**: propietaria (AEM, Sitecore), **SaaS** (HubSpot, Shopify), **GPL** (WordPress, Joomla, Drupal; lo derivado sigue siendo GPL) y **MIT/Apache 2.0** (permisivas; Apache añade cláusulas de patentes; ejemplos Ghost, Strapi).
- **Tipos de CMS**: generalistas (WordPress, Joomla, Drupal) y especializados (e-commerce: Magento, Shopify, WooCommerce; *headless*: Contentful, Strapi; LMS: Moodle, Canvas, Blackboard; gestión documental: Alfresco, Nuxeo, SharePoint; membresías: MemberPress, Wild Apricot).
- **Requisitos recomendados (2026)**: PHP 8.3+, MySQL 8.0+ o MariaDB 10.11+, Apache o Nginx, HTTPS. Cliente: navegador actualizado, JavaScript activado.
- **Pregunta de la presentación**: "si WordPress son solo archivos PHP, ¿por qué hay que crear antes una base de datos?" (PHP = lógica; la BD guarda el contenido).
- **Demo de 5 pasos**: Start Apache y MySQL → `CREATE DATABASE miwordpress;` en la pestaña SQL de phpMyAdmin → descomprimir WordPress en `htdocs` → `localhost/<carpeta>/` → datos de BD, sitio y administrador.
- **`wp-config.php` (extracto)**: `DB_NAME`, `DB_USER` (`root`), `DB_PASSWORD` (vacía), `DB_HOST` (`localhost`, o `localhost:3340` si cambias el puerto) y `$table_prefix = 'wp_';` ("cámbialo si varias webs comparten base de datos").
- **Tablas creadas (12)**: `wp_posts` (entradas y páginas), `wp_users` y `wp_usermeta` (usuarios), `wp_comments`, `wp_options` (ajustes del sitio), `wp_terms…` (categorías y etiquetas).
- **Tarea del PDF**: entrenamientos **1 y 2** (crear la base de datos por SQL y los datos de conexión del asistente). Si el asistente falla: comprobar que MySQL esté en verde y que el nombre de la base de datos coincida.

## Mi propio montaje (alternativa a la demo de Windows)
En vez de seguir la demo en Windows con XAMPP, monté mi propio entorno en un **contenedor LXC dedicado en mi Proxmox** (accesible desde mi equipo principal), con **LAMP** (el equivalente en Linux de XAMPP: **L**inux + **A**pache + **M**ySQL/MariaDB + **P**HP) y WordPress instalado encima. Ya lo tengo levantado y funcionando. Es una vía alternativa igual de válida a la demo del profesor en Windows — el propio profesor confirmó en clase que el proceso es "exactamente igual" en Linux, solo cambia la ruta de instalación (equivalente a `htdocs`) y el nombre del stack.

## Para llevar a casa
- Tener claro el panorama de CMS: WordPress domina el mercado genérico; Joomla y Drupal, en declive; Moodle es el referente como LMS; Magento/PrestaShop/Shopify son los pesos pesados del e-commerce especializado, y WooCommerce es el plugin de e-commerce de WordPress.
- Distinguir bien los tipos de licencia: **propietaria** (no se puede modificar), **GPL** (se puede modificar y distribuir — caso de WordPress), **SaaS** (se paga suscripción, el proveedor mantiene todo).
- Requisitos mínimos para montar WordPress hoy: **PHP 8.3+** y **MySQL 8 / MariaDB 11+**, sobre un stack Apache+PHP+BBDD (XAMPP en Windows, LAMP en Linux, o Docker).
- Orden obligatorio al instalar: **primero la base de datos, después WordPress** apuntando a ella — si no, la instalación falla por no encontrar la base de datos.
- Cuidado con las rutas al descomprimir WordPress en `htdocs`: evitar carpetas anidadas de más; el servidor necesita el `index.php` en la raíz del proyecto.
- Buenas prácticas de seguridad básicas vistas: cambiar el prefijo de tablas (`wp_` por defecto) y nunca dejar usuario `root`/contraseña vacía fuera de un entorno local de pruebas.
- Para la próxima clase: tener WordPress instalado y funcionando por el método que sea (XAMPP, LAMP, Docker, hosting...), para empezar a ver plugins y plantillas.
