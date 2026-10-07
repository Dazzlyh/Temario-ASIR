## Tema 4

# Implantación de Aplicaciones Web

# Tema 4. Administración de gestores de contenidos

# índice

Esquema Material de estudio

## 4.1. Introducción y objetivos

## 4.2. Usuarios y grupos

## 4.3. Perfiles

## 4.4. Seguridad. Control de accesos

## 4.5. Integración de módulos

## 4.6. Gestión de temas

## 4.7. Plantillas

## 4.8. Copias de seguridad

## 4.9. Sindicación de contenidos

## 4.10. Importación y exportación de la información

## 4.11. Referencias bibliográficas

A fondo Manual completo Elementor Page Builder LIstado de los 41 mejores plugins para Wordpress Entrenamientos

Entrenamiento 1

Entrenamiento 2

Entrenamiento 3

Entrenamiento 4

Entrenamiento 5

Entrenamiento 6

# Esquema

![image-1](images/image-1.png)

Implantación de Aplicaciones Web 4 Tema 4. Esquema

# 4.1. Introducción y objetivos

La administración de CMS abarca un amplio configuración inicial y la instalación de *plugins* espectro de tareas, desde la hasta la gestión de usuarios, la seguridad y la optimización del rendimiento. Un administrador de CMS eficaz debe poseer habilidades técnicas y organizativas, así como una comprensión profunda de las necesidades y objetivos del sitio web.

Los objetivos principales que queremos conseguir con el estudio de este tema son:

**▸ Facilitar la creación y publicación de contenido:** el CMS debe permitir a los usuarios crear y publicar contenido de forma sencilla e intuitiva, sin necesidad de conocimientos de programación.

**▸ Mantener la seguridad del sitio web:** el administrador debe implementar medidas de seguridad para proteger el sitio web de ataques cibernéticos y garantizar la integridad de los datos.

**▸ Gestionar usuarios y permisos:** se debe controlar el acceso al CMS y asignar permisos a los usuarios según sus roles y responsabilidades.

**▸ Realizar copias de seguridad es fundamental:** deben ser planificadas y con una periodicidad adecuada en nuestro proyecto web, para poder restaurarlo en caso de pérdida de datos debido a diferentes causas.

# 4.2. Usuarios y grupos

La gestión de usuarios y grupos es fundamental para controlar el acceso y los permisos dentro de tu sitio web. WordPress ofrece un sistema flexible de roles y capacidades que permite asignar diferentes niveles de acceso a los usuarios, lo que garantiza la seguridad y la colaboración eficiente.

**▸ Roles de usuario predeterminados:** WordPress incluye seis roles de usuario predeterminados, cada uno con capacidades específicas:

- Super administrador: acceso completo a todas las funciones de la red de sitios en una instalación multisitio. Este tipo de instalación te permite gestionar varios sitios web en una red desde una única instalación de WordPress.

- Administrador: acceso completo a todas las funciones de un solo sitio. Puede instalar *plugins,* temas, crear usuarios y modificar cualquier contenido.

- Editor: puede publicar y gestionar todas las entradas y páginas, incluyendo las de otros usuarios.

- Autor: puede publicar y gestionar sus propias entradas y páginas.

- Colaborador: puede escribir y gestionar sus propias entradas, pero no puede publicarlas.

- Suscriptor: solo puede leer el contenido y gestionar su perfil.

**▸ Grupos de usuarios:** WordPress no incluye una función de grupos de usuarios integrada. Sin embargo, podemos lograr una funcionalidad similar utilizando *plugins* o personalizando el código. Algunos *plugins* populares para gestionar grupos de usuarios son:

- User role editor: permite crear roles de usuario personalizados y asignar capacidades específicas a cada rol.

- Groups: sirve para crear grupos de usuarios y asignarles roles y capacidades.

- Members: ofrece una interfaz sencilla para gestionar usuarios, roles y capacidades.

**▸ Mejores prácticas para gestionar usuarios y grupos.**

- Roles de usuario adecuados: asigna roles que se ajusten a las responsabilidades de cada usuario. Evita otorgar acceso de administrador a menos que sea absolutamente necesario.

- Roles personalizados, si es necesario: cuando los roles predeterminados no satisfacen tus necesidades, utiliza un *plugin* para crear roles personalizados con capacidades específicas.

- Gestiona los grupos de usuarios con plugins: en caso de necesitar agrupar usuarios y asignarles permisos específicos, utiliza un *plugin* de gestión de grupos.

- Revisa los permisos regularmente: realiza auditorías periódicas de los permisos de usuario para asegurarte de que siguen siendo apropiados.

**▸ Mantén contraseñas seguras.**

- Exige a los usuarios que utilicen contraseñas fuertes y cámbialas regularmente.

- Limita los intentos de inicio de sesión: utiliza un plugin para limitar los intentos de inicio de sesión y proteger tu sitio de ataques de fuerza bruta.

- La gestión eficaz de usuarios y grupos en WordPress es crucial para mantener la seguridad, la organización y la colaboración en tu sitio web. Al comprender los roles de usuario predeterminados, utilizar *plugins* para gestionar grupos y seguir las mejores prácticas. Puedes garantizar que cada usuario tenga el acceso adecuado y que tu sitio esté protegido.

# 4.3. Perfiles

Como hemos visto, hay seis roles/perfiles principales de asignación. Además, se pueden crear perfiles adicionales con capacidades añadidas por el administrador o por diferentes *plugins* de asignación de permisos en WP.

![image-2](images/image-2.png)

Tabla 1. Perfiles de usuario WordPress. Fuente: elaboración propia.

Es importante asignar el perfil de usuario adecuado a cada persona que colabora en tu sitio web. Esto garantiza la seguridad y el buen funcionamiento del sitio, al tiempo que permite a cada usuario realizar las tareas necesarias de manera eficiente.

# 4.4. Seguridad. Control de accesos

El control de accesos es un aspecto crucial en la administración de cualquier sitio web, y WordPress no es una excepción. Proteger tu sitio de ataques maliciosos y garantizar que solo los usuarios autorizados tengan acceso a áreas sensibles es fundamental para mantener la integridad de tus datos y la confianza de tus visitantes.

Consejos de seguridad

**▸ Mantén la aplicación, los temas y** ***plugins*** **actualizados:** las actualizaciones a menudo incluyen parches de seguridad que corrigen vulnerabilidades conocidas.

**▸ Utiliza contraseñas fuertes y únicas:** evita contraseñas fáciles de adivinar y utiliza un gestor de contraseñas para generar y almacenar contraseñas seguras.

**▸ Limita los intentos de inicio de sesión:** utiliza un *plugin* para bloquear direcciones IP después de varios intentos fallidos de inicio de sesión, lo que ayuda a prevenir ataques de fuerza bruta.

**▸ Realiza copias de seguridad periódicas:** asegúrate de tener copias de seguridad actualizadas de tu sitio web para poder restaurarlo en caso de un ataque o pérdida de datos.

**▸ Utiliza un** ***plugin*** **de seguridad:** un *plugin* te puede ayudar a escanear tu sitio para buscar vulnerabilidades, bloquear ataques maliciosos y monitorear la actividad sospechosa.

**▸ Protege el acceso al área de administración:** cambia la URL de inicio de sesión predeterminada de «/wp-admin» a algo único y utiliza un *plugin* para limitar el acceso a direcciones IP específicas.

**▸ Educa a tus usuarios:** asegúrate de que todos los usuarios de tu sitio web sigan buenas prácticas de seguridad, como utilizar contraseñas fuertes y no hacer clic en enlaces sospechosos.

**▸ Audita los permisos de usuario regularmente:** realiza revisiones periódicas de los permisos de usuario para asegurarte de que siguen siendo apropiados y no hay accesos no autorizados.

**▸ Habilita la autenticación de dos factores (2FA):** agrega una capa adicional de seguridad al requerir un segundo factor de verificación, como un código enviado a tu teléfono móvil, además de la contraseña.

![Figura 1. Resumen de los puertos de protocolos de aplicación. Fuente: Ayuda WordPress, s. f. a.](images/image-3.png)

*Figura 1. Resumen de los puertos de protocolos de aplicación. Fuente: Ayuda WordPress, s. f. a.*

La validación en dos pasos o de dos factores (2FA) añade una capa adicional de seguridad a tu sitio web de WordPress al requerir un segundo factor de verificación, además de la contraseña, para iniciar sesión. Esto dificulta significativamente el acceso no autorizado, incluso si alguien logra obtener tu contraseña.

Cómo implementar la validación en dos pasos para WordPress

Hay varios *plugins* con los que podemos añadir la validación 2FA, por ejemplo:

**▸** ***Two factor:*** ofrece varias opciones de segundo factor, incluyendo aplicaciones de autenticación, correo electrónico y códigos de respaldo.

**▸ Wordfence:** si ya utilizas Wordfence para seguridad, puedes habilitar la 2FA directamente desde el *plugin.*

**▸ Google Authenticator:** un *plugin* simple y efectivo que utiliza la aplicación Google Authenticator para generar códigos de verificación.

Instalar y activar el plugin elegido

Ve al menú «Plugins» después a «Añadir nuevo plugin» en el panel de administración de WordPress. Busca el *plugin* que elegiste, pulsamos «Instalar ahora» y actívalo una vez instalado.

![image-4](images/image-4.png)

Figura 2. Panel de administración WP, menú *plugins.* Fuente: elaboración propia.

![Figura 3. Ficha plugins de la validación en dos pasos. Fuente: elaboración propia.](images/image-5.png)

*Figura 3. Ficha plugins de la validación en dos pasos. Fuente: elaboración propia.*

Configura el plugin

Sigue las instrucciones específicas del *plugin* que hayas elegido. Las opciones de configuración generales de estos *plugins* son las siguientes:

**▸** Elegir el método de segundo factor (aplicación de autenticación, correo electrónico, etc.).

**▸** Configurar las opciones de respaldo en caso de que pierdas el acceso al segundo factor.

**▸** Habilitar la 2FA para los usuarios que desees (es aconsejable que lo hagas para todos).

# 4.5. Integración de módulos

La integración de módulos es fundamental para extender las funcionalidades y personalizar tu sitio web según tus necesidades específicas. Los *plugins* te permiten añadir características como formularios de contacto, galerías de imágenes, tiendas en línea, optimización para motores de búsqueda (SEO), seguridad mejorada y mucho más, sin necesidad de conocimientos de programación avanzados.

Proceso de integración de plugins

#### Búsqueda

**▸ Repositorio oficial de WordPress:** el directorio de *plugins* de WordPress es el lugar más seguro y confiable para encontrar *plugins.* Puedes buscar por palabras clave, categorías o filtrar por valoraciones y popularidad.

**▸ Sitios web de terceros:** algunos desarrolladores ofrecen *plugins premium* en sus propios sitios web. Asegúrate de investigar la reputación del desarrollador y leer reseñas antes de utilizar o comprar, ya que puede tratarse de un *malware* que comprometa tu sitio web.

#### Instalación

**▸** Desde el panel de administración: ve a «Plugins», «Añadir nuevo» y busca el *plugin* por su nombre. Haz clic en «Instalar ahora» y luego en «Activar».

**▸** Carga manual: si tienes el archivo .zip del *plugin,* puedes subirlo a través de «Plugins», «Añadir nuevo», «Subir plugin».

#### Configuración

Una vez activado, el *plugin,* generalmente, añadirá una nueva sección en el menú de administración. Accede a la configuración del *plugin* y ajústala según tus necesidades. Algunos *plugins* pueden requerir configuración adicional, como crear formularios, añadir *widgets* o configurar opciones de visualización.

#### Consejos importantes

**▸** Compatibilidad: asegúrate de que el *plugin* sea compatible con tu versión de WordPress y con otros *plugins* que estés utilizando. **▸** Actualizaciones: mantén tus *plugins* actualizados para garantizar la seguridad y el buen funcionamiento de tu sitio. **▸** Rendimiento: demasiados *plugins* pueden ralentizar tu sitio web. Elige *plugins* bien codificados y optimizados para el rendimiento. **▸** Seguridad: descarga *plugins* solo de fuentes confiables y lee reseñas antes de instalarlos. **▸** Soporte: elige *plugins* que ofrezcan buen soporte técnico en caso de que necesites ayuda.

#### Plugins populares

**▸** Yoast SEO: optimiza tu sitio web para aparecer en los resultados de los motores de búsqueda. **▸** Contact Form 7: crea formularios de contacto personalizados y almacena los datos que envían los usuarios. **▸** WooCommerce: convierte tu sitio en una tienda en línea, con todas las características necesarias.

**▸** Wordfence Security: mejora la seguridad de tu sitio web.

**▸** Elementor: diseña páginas y publicaciones con un editor visual intuitivo.

![Figura 4. Logotipos de plugins populares en WordPress. Fuente: Ayuda WordPress, s. f. b.](images/image-6.png)

*Figura 4. Logotipos de plugins populares en WordPress. Fuente: Ayuda WordPress, s. f. b.*

La integración de *plugins* es una forma poderosa de personalizar y mejorar tu sitio web de WordPress. Al elegir los *plugins* adecuados y configurarlos correctamente, puedes añadir funcionalidades esenciales, mejorar la experiencia del usuario y alcanzar tus objetivos en línea.

# 4.6. Gestión de temas

La gestión de temas es fundamental para definir la apariencia y el diseño de tu sitio web. Los temas controlan la presentación visual del contenido, incluyendo colores, fuentes, diseño de página y estructura general. Una buena gestión de temas te permite personalizar la apariencia de tu sitio, para adaptarlo a tu marca y objetivos.

Instalación y activación de temas

#### Desde el repositorio de WordPress

En «Apariencia» iremos a «Temas», en el panel de administración, haz clic en «Añadir nuevo» para explorar el repositorio oficial de temas gratuitos de WordPress. Busca el tema por palabras clave, filtra por características o navega por las categorías. Una vez localizado el tema adecuado, haz clic en «Vista previa» para ver cómo se vería el tema en tu sitio. Si te gusta, haz clic en «Instalar» y luego en «Activar».

![Figura 5. Menú apariencia con tema seleccionado. Fuente: elaboración propia.](images/image-7.png)

*Figura 5. Menú apariencia con tema seleccionado. Fuente: elaboración propia.*

#### Carga directa de fichero con el tema

Si tienes un archivo .zip de un tema *premium* o personalizado, puedes subirlo a través de «Apariencia», «Temas», «Añadir nuevo», «Subir tema».

![Figura 6. Menú apariencia con tema instalado. Fuente: elaboración propia.](images/image-8.png)

*Figura 6. Menú apariencia con tema instalado. Fuente: elaboración propia.*

Personalizador de WordPress

La mayoría de los temas modernos incluyen un personalizador integrado que te permite modificar aspectos como colores, fuentes, logo, imágenes de fondo y diseño de página, sin necesidad de conocimientos de código. Solo hay que acceder al personalizador a través de «Apariencia», «Temas», «Personalizar» (en el tema activo) o simplemente «Apariencia», «Editor» y entrarás en el personalizador del tema activo en ese momento.

#### Editor de bloques

El editor de bloques Gutenberg es el editor de contenido predeterminado en WordPress desde la versión 5.0, lanzado en diciembre de 2018. Reemplazó al antiguo editor clásico (TinyMCE) y trajo consigo un enfoque revolucionario para la creación y edición de contenido en WordPress, basado en el concepto de bloques. Este editor te permite crear y editar entradas y páginas, utilizando bloques de contenido reutilizables. Puedes personalizar la apariencia de cada bloque individualmente, lo que te brinda un mayor control sobre el diseño de tu contenido.

![Figura 7. Editor Gutenberg de WP. Fuente: elaboración propia.](images/image-9.png)

*Figura 7. Editor Gutenberg de WP. Fuente: elaboración propia.*

#### Plugins de creación de páginas

Si necesitas un mayor nivel de personalización, puedes utilizar *plugins* de creación de páginas como **Elementor** o **Beaver Builder.** Estos *plugins* te permiten crear diseños complejos con elementos de arrastrar y soltar, sin necesidad de código. Además, puedes incluir animaciones y efectos en textos e imágenes.

#### Consideraciones importantes

**▸** Compatibilidad: asegúrate de que el tema sea compatible con tu versión de WordPress y con los *plugins* que estás utilizando.

**▸** Rendimiento: elige temas bien codificados y optimizados para el rendimiento, ya que un tema lento puede afectar la velocidad de carga de tu sitio.

**▸** Funcionalidad: selecciona un tema que ofrezca las características y opciones de diseño que necesitas para tu tipo de sitio web.

**▸** Soporte: elige temas de desarrolladores confiables que ofrezcan actualizaciones regulares y buen soporte técnico.

**▸** Tema hijo: si planeas realizar modificaciones importantes en el código del tema, crea un tema hijo para proteger tus cambios en caso de actualizaciones del tema principal.

# 4.7. Plantillas

En WordPress, las plantillas son archivos PHP que determinan la estructura y el diseño de páginas específicas o tipos de contenido dentro de un tema. Cada tema puede incluir varias plantillas y cada plantilla controla cómo se muestra el contenido en diferentes secciones de tu sitio web, como la página de inicio, las entradas individuales, las páginas de archivo, las páginas de búsqueda y más.

Tipos de plantillas

**▸** index.php **:** la plantilla principal que se utiliza cuando no se encuentra una plantilla más específica.

**▸** single.php **:** controla la visualización de entradas individuales.

**▸** page.php **:** controla la visualización de páginas estáticas.

**▸** archive.php **:** se utiliza para mostrar archivos de categorías, etiquetas, autores y

fechas.

**▸** search.php **:** controla la visualización de los resultados de búsqueda.

**▸** 404.php **:** se muestra cuando se solicita una página que no existe.

**▸ Personalizadas:** los temas pueden incluir plantillas adicionales para elementos

específicos, como encabezados, pies de página, barras laterales y secciones de contenido personalizadas.

Funcionamiento de las plantillas

**▸** Jerarquía_WordPress **:** utiliza una jerarquía de plantillas para determinar qué plantilla se utilizará para mostrar una página específica. Si no se encuentra una plantilla más específica, se utiliza la plantilla index.php .

**▸ Etiqueta** template_part **:** esta etiqueta permite incluir partes de plantillas reutilizables en otras plantillas, lo que facilita la organización y el mantenimiento del código.

**▸ Bucle de WordPress:** el bucle es un código PHP que consulta la base de datos y muestra el contenido relevante en la plantilla.

Beneficios de utilizar plantillas

Las plantillas son una herramienta poderosa

para personalizar y controlar la

apariencia de tu sitio web de WordPress. Al comprender cómo funcionan y cómo gestionarlas, puedes crear un sitio web que necesidades y objetivos.

se adapte perfectamente a tus

**▸ Control del diseño:** te permiten personalizar la apariencia de diferentes secciones de tu sitio web.

**▸ Organización del código:** facilitan la reutilización de código y la organización de tu tema.

**▸ Flexibilidad:** permiten crear diseños únicos para diferentes tipos de contenido.

# 4.8. Copias de seguridad

Las copias de seguridad son una práctica fundamental para garantizar la integridad y disponibilidad de tu sitio web. Un fallo técnico, un ataque malicioso o incluso un error humano pueden provocar la pérdida de datos y, sin una copia de seguridad, recuperar tu sitio puede ser extremadamente difícil o incluso imposible.

¿Qué se debe incluir en las copias de seguridad de WordPress?

**▸ Base de datos:** contiene toda la información de tu sitio web, incluyendo entradas, páginas, comentarios, usuarios y configuraciones.

**▸ Archivos del sitio:** los archivos de WordPress, como temas, *plugins,* imágenes y otros medios.

**▸ WordPress** guarda en su base de datos el contenido textual y el código de los documentos HTML que genera para presentar todo lo que vamos creando (como entradas, páginas, catálogos, galerías, etc.), ya que las imágenes y otros archivos son almacenados y referenciados en carpetas de la estructura inicialmente instalada. Nosotros actuamos como administradores o editores sobre la base de datos y los archivos; por lo tanto, con replicar ambos almacenes de información podemos respaldar, mover o reinstalar cualquier sitio web realizado con WP.

![Figura 8. Estructura de funcionamiento WordPress. Fuente: Laukatu, s. f.](images/image-10.png)

*Figura 8. Estructura de funcionamiento WordPress. Fuente: Laukatu, s. f.*

Métodos para realizar copias de seguridad en WordPress

#### Manual

Este método puede ser algo complejo y requiere algunos conocimientos técnicos. Además, es más propenso a errores humanos, pero es factible y se tiene el control total de las acciones que realicemos. Cuando lo hayamos realizado algunas veces, nos parecerá sencillo, fácil y seguro.

**▸ Base de datos:** puedes exportar la base de datos desde phpMyAdmin, la herramienta de administración de bases de datos que suele estar disponible en tu panel de control de *hosting* o en tu instalación local.

**▸ Archivos:** puedes descargar los archivos de tu sitio web a través de un cliente FTP, como FileZilla, o copiar todo el directorio del proyecto WP directamente desde el explorador local de archivos.

En phpMyAdmin pulsamos sobre la base de datos que queremos exportar y se pondrá como activa en la barra superior donde está la IP del servidor y el puerto.

![Figura 9. Exportación de tabla phpMyAdmin. Fuente: elaboración propia.](images/image-11.png)

*Figura 9. Exportación de tabla phpMyAdmin. Fuente: elaboración propia.*

Tras exportar el fichero podemos ver su estructura en SQL, con la definición de tablas y la inserción de los datos que contienen en el momento de la exportación.

![Figura 10. Edición fichero tablas exportadas. Fuente: elaboración propia.](images/image-12.png)

*Figura 10. Edición fichero tablas exportadas. Fuente: elaboración propia.*

Si probamos a importar el fichero que hemos exportado en la misma base de datos, todo funcionará perfectamente, pero no dará el error de la existencia de la base de datos que vamos a importar. Si la borramos y probamos nuevamente, veremos que todo funciona a la perfección.

Si lo que queremos es llevar nuestra página a otro servidor, debemos respetar los nombres de la base de datos, la IP y el puerto del servidor y lo podremos replicar todo sin problema. Si cambiase algún dato de los citados, tendremos que entrar en los ficheros de configuración general, como vimos, y poner la información correcta.

![Figura 11. Importación en phpMyAdmin. Fuente: elaboración propia.](images/image-13.png)

*Figura 11. Importación en phpMyAdmin. Fuente: elaboración propia.*

Aviso de la existencia de una base de datos como la que estamos importando.

![Figura 12. Aviso de base de datos existente. Fuente: elaboración propia.](images/image-14.png)

*Figura 12. Aviso de base de datos existente. Fuente: elaboración propia.*

#### Plugins para copias de seguridad

Automatizan el proceso, ofrecen almacenamiento en la nube y facilitan la restauración en caso de problemas. Son fáciles de manejar y dan total fiabilidad en el resultado de los *backups.*

**▸ UpdraftPlus:** gratuito y muy popular, permite realizar copias de seguridad automáticas y almacenarlas en la nube (Dropbox, Google Drive, etc.).

**▸ VaultPress:** un servicio *premium* de pago de Automattic (la empresa que está detrás de WordPress), que ofrece copias de seguridad automáticas, seguridad y soporte experto.

**▸ BackupBuddy:** un *plugin premium* con opciones avanzadas, como migración de sitios y restauración con un clic.

![Figura 13. Plugin de backup y migración WP. Fuente. elaboración propia.](images/image-15.png)

*Figura 13. Plugin de backup y migración WP. Fuente. elaboración propia.*

Ejemplo de copia de seguridad con UpdraftPlus

Instalar y activar el *plugin* UpdraftPlus.

Ir a «Ajustes», «UpdraftPlus Backups».

Configurar las opciones de copia de seguridad:

Archivos que incluir: selecciona todos los archivos de WordPress para

asegurarte de incluir todo lo necesario. Destino de la copia de seguridad: elige un almacenamiento remoto seguro, como Dropbox o Google Drive. Programación: configura copias de seguridad automáticas diarias o semanales según tus necesidades. Hacer clic en «Respaldar ahora» para crear una copia de seguridad inmediata.

#### Proveedor de hosting

Los proveedores de *hosting* ofrecen copias de seguridad automáticas como parte de sus planes. Es un servicio muy seguro, además de conveniente, y no requiere configuración adicional. Solo debemos asegurarnos de comprender las políticas de copia de seguridad de nuestro proveedor y si ofrece opciones de restauración.

#### Recomendaciones

**▸** Realiza copias de seguridad periódicas: la frecuencia depende de la cantidad de cambios que realices en tu sitio. Para sitios con actualizaciones frecuentes se recomienda realizar copias de seguridad diarias o semanales.

**▸** Almacena las copias de seguridad en un lugar seguro: como servicios de almacenamiento en la nube o un disco duro externo para proteger tus copias de seguridad de fallos locales.

**▸** Prueba la restauración: realiza pruebas periódicas de restauración para asegurarte de que tus copias de seguridad funcionan correctamente.

**▸** Considera un *plugin* de seguridad: puede ayudarte a proteger tu sitio de ataques y minimizar el riesgo de pérdida de datos.

Las copias de seguridad son una inversión esencial para proteger tu sitio web. Al realizar copias de seguridad periódicas y almacenarlas en un lugar seguro, puedes tener la tranquilidad de saber que puedes restaurar tu sitio en caso de cualquier problema.

# 4.9. Sindicación de contenidos

Consiste principalmente a través de RSS feeds. Permite a los usuarios suscribirse a tu sitio y recibir actualizaciones automáticas cada vez que publicas nuevo contenido. Esto facilita que tus lectores se mantengan al día con tus últimas entradas, noticias o cualquier otro tipo de contenido que generes.

**▸ ¿Qué es un RSS** ***feed?:*** un RSS *feed (really simple syndication)* es un archivo XML que contiene información sobre tus publicaciones, como títulos, descripciones, enlaces y fechas de publicación. Los lectores de *feeds* o agregadores de noticias pueden leer estos archivos y mostrar el contenido de forma organizada. Los usuarios pueden suscribirse a tu *feed* RSS utilizando su lector de *feeds* favorito o agregador de noticias.

**▸ Ventajas de la sindicación de contenidos.**

- Mayor alcance: permite que tu contenido llegue a un público más amplio, ya que los usuarios pueden acceder a él desde diferentes plataformas y dispositivos.

- Comodidad para los usuarios: los usuarios reciben actualizaciones automáticas sin tener que visitar tu sitio web manualmente.

- Mejora el SEO: los motores de búsqueda pueden indexar tus feeds RSS, lo que puede aumentar la visibilidad de tu sitio.

- Fomenta la interacción: los usuarios pueden compartir fácilmente tu contenido en redes sociales u otras plataformas.

**▸ Gestión de RSS** ***feeds.***

- Feeds predeterminados: WordPress genera automáticamente feeds RSS para tus entradas, comentarios y categorías. Puedes acceder a ellos añadiendo /feed/ al final de la URL de tu sitio o de una categoría específica.

- Personalización de feeds: puedes personalizar el contenido y la apariencia de tus *feeds* RSS utilizando *plugins* o editando el archivo

functions.php de tu tema.

- Promoción de feeds: incluye enlaces a tus feeds RSS en tu sitio web, redes sociales y otros canales de comunicación para animar a los usuarios a suscribirse.

**▸** ***Plugins*** **útiles para la sindicación de contenidos.**

- RSS Feed Widget: te permite mostrar un feed RSS en la barra lateral o pie de página de tu sitio.

- FeedBurner: un servicio de Google que te permite gestionar y analizar tus feeds RSS.

- WP RSS Aggregator: te permite mostrar feeds RSS de otros sitios web en tu propio sitio.

# 4.10. Importación y exportación de la información

La importación y exportación de información es esencial para conseguir contenido y datos de una forma fácil, para transferir información entre diferentes sitios web o para realizar copias de seguridad de datos especialmente importantes. WordPress ofrece herramientas integradas y *plugins* que facilitan estos procesos. Es muy importante comprender sus capacidades y limitaciones.

Exportación de información

WP permite exportar todo tu contenido, o una selección específica, en un archivo XML. Este archivo contiene entradas, páginas, comentarios, categorías, etiquetas y otros datos relevantes.

#### Pasos para exportar información

**▸** Accede a la herramienta de exportación: ve a «Herramientas», «Exportar en tu panel de administración».

**▸** Selecciona el contenido: elige qué deseas exportar todo el contenido o solo ciertos tipos de contenido (entradas, páginas, etc.).

![Figura 14. Exportar contenido en WP. Fuente: elaboración propia.](images/image-16.png)

*Figura 14. Exportar contenido en WP. Fuente: elaboración propia.*

**▸** Descarga el archivo XML: haz clic en «Descargar archivo de exportación» para guardar el archivo en tu ordenador. Tendrá el siguiente aspecto:

![Figura 15. Fichero XML exportado. Fuente: elaboración propia.](images/image-17.png)

*Figura 15. Fichero XML exportado. Fuente: elaboración propia.*

Importación de información

Podemos importar contenido desde un archivo XML exportado previamente. Sin embargo, es importante tener en cuenta que la importación puede tener limitaciones, especialmente con temas y *plugins* personalizados.

#### Pasos para importar información

**▸** Accede a la herramienta de importación, ve a «Herramientas», «Importar en tu panel de administración».

![Figura 16. Importación en WP. Fuente: elaboración propia.](images/image-18.png)

*Figura 16. Importación en WP. Fuente: elaboración propia.*

**▸** Instalamos el importador de WordPress: si no lo estaba (haz clic en «Instalar ahora» debajo de WordPress). Al tenerlo instalado, hacemos clic en «Ejecutar el importador».

![Figura 17. Selección de ficheros a importar. Fuente: elaboración propia.](images/image-19.png)

*Figura 17. Selección de ficheros a importar. Fuente: elaboración propia.*

**▸** Selecciona el archivo XML: haz clic en «Seleccionar archivo», pulsa sobre el fichero XML que deseas importar y pulsa «Subir archivo e importar».

**▸** Asigna autores: si el archivo incluye contenido de varios autores, puedes asignarlos a usuarios existentes en tu sitio o crear nuevos usuarios.

**▸** Importar archivos adjuntos: marca esta opción si deseas importar imágenes y otros medios incluidos en el archivo XML, para iniciar la importación haremos clic en «Enviar» y comenzará el proceso.

Consejos importantes

**▸ Temas y plugins:** la importación puede no incluir la configuración de temas y *plugins* personalizados. Es posible que debas configurarlos manualmente después de la importación.

**▸ Imágenes y medios:** si el archivo XML no incluye las URL completas de las imágenes y medios, es posible que debas utilizar un plugin para importarlas por separado.

**▸ Tamaño del archivo:** si el archivo XML es muy grande, la importación puede tardar mucho tiempo o incluso fallar. En ese caso, puedes dividir el archivo en partes más pequeñas o utilizar un *plugin* de importación especializado.

Plugins de importación y exportación

Existen varios *plugins* que pueden facilitarte el proceso y ofrecerte funcionalidades adicionales. A continuación, se presentan algunos de los más populares y efectivos.

#### WP All Import & Export

Es un *plugin* extremadamente versátil, capaz de importar y exportar casi cualquier tipo de datos, incluyendo entradas, páginas, productos de WooCommerce, usuarios, taxonomías y campos personalizados. Permite mapear los datos de tu archivo XML a los campos correspondientes en WordPress. Ofrece, también, opciones avanzadas, como la programación de importaciones y la capacidad de actualizar contenido existente. Hay una versión gratuita disponible con funcionalidades básicas, pero suficientes para casi todas las acciones que necesites, salvo en la cantidad de datos a importar, ya que en esta versión tiene limitaciones.

#### WP Ultimate CSV Importer

Se especializa en la importación de datos desde archivos CSV, pero también puede manejar archivos XML. Además, sirve para mapear los datos de tu archivo a los campos de WordPress y tiene opciones para programar importaciones y actualizar contenido existente. Hay una versión funcionalidades. Este *plugin* es menos

gratuita disponible, con todas las intuitivo que otros, especialmente para

usuarios no técnicos. La funcionalidad de exportación es limitada en comparación con otras herramientas.

#### Import Users from CSV with Meta

Se trata de un *plugin* diseñado específicamente

para **importar usuarios** desde

archivos CSV o XML, incluyendo metadatos personalizados. Permite asignar roles y contraseñas a los usuarios importados y es ideal para migrar usuarios desde otra plataforma o crear usuarios masivamente. La versión gratuita está disponible.

#### Customizer Export/Import

Es un *plugin* que permite exportar e importar la configuración del personalizador de WordPress, esto incluye colores, fuentes, diseños y *widgets.* Es muy útil para migrar la apariencia de un sitio o crear copias de seguridad de la configuración del personalizador, pero no para importar contenidos o usuarios. La versión gratuita se encuentra disponible.

#### JSON Content Importer

*Plugin* especializado en la importación de contenido desde archivos JSON, pero también puede manejar archivos XML. Permite mapear los datos de tu archivo a los campos de WordPress y programar las importaciones y actualizar el contenido existente, aunque la funcionalidad de exportación es limitada. Hay una versión gratuita disponible.

Siempre realiza una copia de seguridad completa de tu sitio web antes de importar o exportar datos, podrás solucionar los problemas en caso de que algo salga mal.

# 4.11. Referencias bibliográficas

Ayuda WordPress (s. f. a.). *Identificación de 2 factores (2FA) en WordPress – Qué es* *y cómo configurarla* [Imagen]. [https://ayudawp.com/2fa-wordpress/](https://ayudawp.com/2fa-wordpress/)

Ayuda WordPress (s. f. b.). *Los plugins WordPress más utilizados en España – ¡Ni te* *lo imaginas!* [ I m a g e n ] . <https://ayudawp.com/plugins-wordpress-mas-utilizadosespana-2024/>

Laukatu (s. f.). *Qué es WordPress y para qué sirve* [Imagen]. [https://laukatu.com/blog/que-es-wordpress-y-para-que-sirve.html](https://laukatu.com/blog/que-es-wordpress-y-para-que-sirve.html)

# page-builder/

# A fondo

# Manual completo Elementor Page Builder

Carreño, J. A. (2023, 24 abril). *Elementor: review y tutorial en español. José Antonio* *Carreño.* Jose Antonio Carreño. <https://www.joseantoniocarreno.com/elementor-> Este completísimo manual *online* sobre Elementor nos ofrece muchísima información sobre la creación de contenidos para WordPress. La creación de módulos y la asignación de información, formatos visuales y dinamismo de presentación en la página web. Elementor es uno de los más conocidos editores de contenido web en WP, y es esencial conocerlo y controlarlo para realizar trabajos impecables en nuestros sitios web. Los vídeos que encontraremos en el recurso, ordenados y progresivos, harán que estemos en otro nivel a la hora de crear y modificar nuestros contenidos publicados.

Implantación de Aplicaciones Web 38 Tema 4. A fondo

# A fondo

# LIstado de los 41 mejores plugins para Wordpress

Gustavo B. (abril 24, 2024). *41 de los mejores plugins de WordPress en 2024.* Hostinger Tutoriales. [https://www.hostinger.es/tutoriales/mejores-plugins-wordpress/](https://www.hostinger.es/tutoriales/mejores-plugins-wordpress/)

En la página correspondiente al enlace asignado a este recurso podremos ver una muy buena lista de *plugins,* que seguro necesitaremos en algún momento, para casi todas las actividades que se nos puedan ocurrir en WP. Veremos datos importantes de cada *plugin,* sus puntos fuertes y enlaces a su vista previa (si tiene presencia visual en la web), así como su enlace de descarga al sitio oficial de la comunidad WP ([https://es.wordpress.org/plugins/](https://es.wordpress.org/plugins/)).

Implantación de Aplicaciones Web 39 Tema 4. A fondo

# Entrenamiento 1

**▸ Planteamiento del ejercicio:** vamos a definir URL amigables para SEO en WordPress configurando los enlaces permanentes *(permalinks)* de nuestras entradas de contenido.

**▸ Desarrollo paso a paso:**

- En el administrador de WP vamos a «Ajustes» y vemos que hay una opción de «Enlaces permanentes».

- La opción anterior nos muestra información sobre los enlaces permanentes y diferentes patrones que podemos seleccionar para que conforme la estructura de nuestros enlaces.

- Eligiendo las diferentes opciones o creando un permalink amigable conseguiremos mejorar el posicionamiento de nuestros artículos o entradas en los buscadores, ya que mejoramos el SEO de los contenidos.

**▸ Solución:** es muy importante que las URL contengan información adecuada para ser leída y reconocida por los buscadores, incluir el nombre de la entrada es básico (mucho mejor que su ID). Además del nombre, podemos añadir el año, mes u otros datos fáciles de indexar por los motores de búsqueda.

![Figura 18. Gestor permalinks de WP. Fuente. elaboración propia.](images/image-20.png)

*Figura 18. Gestor permalinks de WP. Fuente. elaboración propia.*

# Entrenamiento 2

**▸ Planteamiento del ejercicio:** crearemos una entrada simple con bloques en el editor por defecto de WP, conocido como Gutenberg.

**▸ Desarrollo paso a paso:**

- En el administrador de WP, iremos a la opción «Entradas» y pulsaremos en «Añadir» una nueva entrada.

- Pasaremos a la interfaz del editor Gutenberg, donde podemos crear una entrada íntegramente utilizando los diferentes bloques disponibles para su composición.

- Añadiremos un bloque de imagen después del título y buscaremos una imagen para incluirla en él.

- Después de incluir la imagen, añadiremos tres bloques de párrafos debajo de esta. Ya tenemos una entrada para guardar y publicar en nuestro sitio, donde se indicará la categoría a la que pertenece y otros detalles de publicación y gestión.

**▸ Solución:** este sería el resultado de las anteriores acciones, la imagen la hemos añadido mediante la copia de su dirección URL. La entrada la guardaremos (para tenerla disponible en cualquier momento) y la publicaremos para verla en nuestra página web.

![Figura 19. Post creado con WP Fuente: elaboración propia.](images/image-21.png)

*Figura 19. Post creado con WP Fuente: elaboración propia.*

![Figura 20. Gestor de entradas de WP. Fuente: elaboración propia.](images/image-22.png)

*Figura 20. Gestor de entradas de WP. Fuente: elaboración propia.*

# Entrenamiento 3

- ▸ Planteamiento del ejercicio: procederemos a cambiar el tema principal de WP y

    - veremos su proceso de búsqueda y activación.

- ▸ Desarrollo paso a paso:

- En el administrador pulsaremos «Apariencia» y veremos los temas que hay cargados, además del tema activo en ese momento.

- Vamos a «Añadir nuevo tema» y veremos los temas que tenemos disponibles. Podemos filtrarlos para buscar el tema que más nos guste (populares, recientes o filtrados por palabras clave).

- Instalaremos el tema Twenty Seventeen, por ejemplo.

- Por último, lo activaremos y podremos editar los aspectos que necesitemos.

**▸ Solución:** cuando hemos instalado y activado el nuevo tema, nos aparecerá en »Temas» y podremos personalizar cualquiera de los aspectos visuales y de navegación.

![Figura 21. Gestor de temas de WP. Fuente: elaboración propia.](images/image-23.png)

*Figura 21. Gestor de temas de WP. Fuente: elaboración propia.*

![Figura 22. Editor de tema de WP Fuente: elaboración propia.](images/image-24.png)

*Figura 22. Editor de tema de WP Fuente: elaboración propia.*

# Entrenamiento 4

- ▸ Planteamiento del ejercicio: buscaremos e instalaremos un plugin de gran

    - importancia en Wordpress, ya que se encarga de analizar e informar de la

    - optimización de nuestro sitio web de cara al SEO (Yoast SEO).

- ▸ Desarrollo paso a paso:

- Accederemos al menú «Plugins» del administrador de WP.

- Pulsaremos sobre «Añadir nuevo plugin» y buscaremos Yoast SEO.

- Procedemos a instalar el plugin encontrado y lo activaremos.

- Veremos que en el menú lateral del administrador aparece, al final, la opción Yoast SEO y su menú integrado.

**▸ Solución:** vemos los dos pasos más importantes en las siguientes imágenes.

![Figura 23. Selector plugins. Fuente: elaboración propia.](images/image-25.png)

*Figura 23. Selector plugins. Fuente: elaboración propia.*

![Figura 24. Configuración Yoast SEO. Fuente: elaboración propia.](images/image-26.png)

*Figura 24. Configuración Yoast SEO. Fuente: elaboración propia.*

# Entrenamiento 5

- ▸ Planteamiento del ejercicio: vamos a crear un sencillo menú en el tema que hemos

    - activado en el Entrenamiento 3.

- ▸ Desarrollo paso a paso:

- Vamos al personalizador del tema activo o al editor en el menú «Apariencia».

- Pulsaremos sobre la opción «Menús» del tema y después crearemos un menú al que llamaremos «Principal».

- Añadiremos un elemento «Entrada», que será la entrada que hemos creado anteriormente, llamada «Mi primera entrada WP».

- Al crear el nuevo elemento, veremos que aparece en la previsualización del tema.

**▸ Solución:** vemos el proceso de creación del nuevo menú en las siguientes imágenes.

![Figura 25. Editor tema. Fuente: elaboración propia.](images/image-27.png)

*Figura 25. Editor tema. Fuente: elaboración propia.*

![Figura 26. Editor tema. Fuente: elaboración propia.](images/image-28.png)

*Figura 26. Editor tema. Fuente: elaboración propia.*

![Figura 27. Editor tema. Fuente: elaboración propia.](images/image-29.png)

*Figura 27. Editor tema. Fuente: elaboración propia.*

![Figura 28. Editor tema. Fuente: elaboración propia.](images/image-30.png)

*Figura 28. Editor tema. Fuente: elaboración propia.*

# Entrenamiento 6

- ▸ Planteamiento del ejercicio: vamos a generar dos ficheros de respaldo de nuestro

    - sitio web en WP, uno con la base de datos y otro con todos los archivos de WP en el

    - servidor.

- ▸ Desarrollo paso a paso:

- Vamos a phpMyAdmin, seleccionamos y exportamos la base de datos en SQL.

- En este caso, creamos un usuario admin con contraseña 1234 mediante el servidor FileZilla, que tiene XAMPP. En un *hosting* solo tendríamos que crearlo en su control panel o, si no fuera administrado por nosotros, solo necesitamos los datos de conexión.

- Nos conectaremos al servidor mediante FTP y descargamos todos los ficheros a nuestro disco local.

**▸ Solución:** vemos el proceso en las siguientes imágenes.

![Figura 29. Exportación phpMyAdmin. Fuente: elaboración propia.](images/image-31.png)

*Figura 29. Exportación phpMyAdmin. Fuente: elaboración propia.*

![Figura 30. Panel de control XAMPP. Fuente: elaboración propia.](images/image-32.png)

*Figura 30. Panel de control XAMPP. Fuente: elaboración propia.*

En general, pulsamos sobre «Add», creamos el usuario «admin» y le asignamos una contraseña (1234) y cambiamos a la página «Shared folders», para asignarle a nuestro usuario la carpeta a la que tiene que tener permisos (en este caso, le hemos dado todos, pero los podemos restringir).

![Figura 30. Configuración de usuarios FTP. Fuente: elaboración propia.](images/image-33.png)

*Figura 30. Configuración de usuarios FTP. Fuente: elaboración propia.*

Instalaremos FileZilla Client en nuestro equipo, configuramos el servidor, usuario, contraseña y puerto, para seleccionar y transferir todos los archivos de WP. Una vez transferidos podemos hacer un fichero comprimido con todo lo descargado y dejarlo en la ubicación que deseemos junto al fichero exportado de la base de datos para poder utilizar ambos cuando necesitemos.

![Figura 31. Consola FileZilla Client. Fuente: elaboración propia.](images/image-34.png)

*Figura 31. Consola FileZilla Client. Fuente: elaboración propia.*

![Figura 32. Ficheros de exportación de back-up de WP. Fuente: elaboración propia.](images/image-35.png)

*Figura 32. Ficheros de exportación de back-up de WP. Fuente: elaboración propia.*

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–37)*
- Entrenamientos  *(pp.40–53)*
- Implantación de Aplicaciones Web 5 Tema 4. Material de estudio · Implantación de Aplicaciones Web 6 Tema 4. Material de estudio · Implantación de Aplicaciones Web 7 Tema 4. Material de estudio · Implantación de Aplicaciones Web 8 Tema 4. Material de estudio · Implantación de Aplicaciones Web 9 Tema 4. Material de estudio · Implantación de Aplicaciones Web 10 Tema 4. Material de estudio · Implantación de Aplicaciones Web 11 Tema 4. Material de estudio · Implantación de Aplicaciones Web 12 Tema 4. Material de estudio · Implantación de Aplicaciones Web 13 Tema 4. Material de estudio · Implantación de Aplicaciones Web 14 Tema 4. Material de estudio · Implantación de Aplicaciones Web 15 Tema 4. Material de estudio · Implantación de Aplicaciones Web 16 Tema 4. Material de estudio · Implantación de Aplicaciones Web 17 Tema 4. Material de estudio · Implantación de Aplicaciones Web 18 Tema 4. Material de estudio · Implantación de Aplicaciones Web 19 Tema 4. Material de estudio · Implantación de Aplicaciones Web 20 Tema 4. Material de estudio · Implantación de Aplicaciones Web 21 Tema 4. Material de estudio · Implantación de Aplicaciones Web 22 Tema 4. Material de estudio · Implantación de Aplicaciones Web 23 Tema 4. Material de estudio · Implantación de Aplicaciones Web 24 Tema 4. Material de estudio · Implantación de Aplicaciones Web 25 Tema 4. Material de estudio · Implantación de Aplicaciones Web 26 Tema 4. Material de estudio · Implantación de Aplicaciones Web 27 Tema 4. Material de estudio · Implantación de Aplicaciones Web 28 Tema 4. Material de estudio · Implantación de Aplicaciones Web 29 Tema 4. Material de estudio · Implantación de Aplicaciones Web 30 Tema 4. Material de estudio · Implantación de Aplicaciones Web 31 Tema 4. Material de estudio · Implantación de Aplicaciones Web 32 Tema 4. Material de estudio · Implantación de Aplicaciones Web 33 Tema 4. Material de estudio · Implantación de Aplicaciones Web 34 Tema 4. Material de estudio · Implantación de Aplicaciones Web 35 Tema 4. Material de estudio · Implantación de Aplicaciones Web 36 Tema 4. Material de estudio · Implantación de Aplicaciones Web 37 Tema 4. Material de estudio  *(pp.5–37)*
- Implantación de Aplicaciones Web 40 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 41 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 42 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 43 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 44 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 45 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 46 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 47 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 48 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 49 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 50 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 51 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 52 Tema 4. Entrenamientos · Implantación de Aplicaciones Web 53 Tema 4. Entrenamientos  *(pp.40–53)*