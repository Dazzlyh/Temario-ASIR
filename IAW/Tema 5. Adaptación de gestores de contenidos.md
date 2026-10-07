## Tema 5

# Implantación de Aplicaciones Web

# Tema 5. Adaptación de gestores de contenidos

# Índice

Esquema Material de estudio

## 5.1. Introducción y objetivos

## 5.2. Selección de modificaciones a realizar

## 5.3. Reconocimiento de elementos involucrados

## 5.4. Modificación de la apariencia

## 5.5. Incorporación y adaptación de funcionalidades

## 5.6. Verificación del funcionamiento

## 5.7. Documentación

5.8. Referencias bibliográficas A fondo Revista online con sección dedicada a WordPress CSS-Tricks estilos web Como crear un tema hijo Entrenamientos

Entrenamiento 1

Entrenamiento 2

Entrenamiento 3

Entrenamiento 4

Entrenamiento 5

# Esquema

![image-1](images/image-1.png)

Implantación de Aplicaciones Web 3 Tema 5. Esquema

# 5.1. Introducción y objetivos

Los gestores de contenidos (CMS) se han convertido en una herramienta esencial para la creación y administración de sitios web, lo que permite a usuarios sin conocimientos técnicos profundos publicar y gestionar contenido digital de forma eficiente. Sin embargo, en un entorno digital en constante evolución, donde las necesidades de los usuarios y las tendencias tecnológicas cambian rápidamente, la adaptación de los CMS se vuelve crucial para mantener la relevancia y el éxito de un sitio web. Esto implica no solo actualizar el *software* a sus últimas versiones, sino también personalizarlo y extenderlo para que se ajuste a los requerimientos específicos de cada proyecto, ya sea a través de la instalación de *plugins,* la modificación de plantillas o el desarrollo de funcionalidades a medida.

Este tema se centra en la adaptación de gestores de contenidos y explora las diferentes estrategias y herramientas disponibles para optimizar su rendimiento y funcionalidad. Se analizarán las mejores prácticas para la selección e implementación de *plugins,* la personalización de plantillas para lograr una apariencia única y la integración de funcionalidades específicas que respondan a las necesidades particulares de cada sitio web. Además, se examinarán las implicaciones de la adaptación de CMS en términos de seguridad, SEO y experiencia de usuario, con el objetivo de proporcionar una guía completa para aprovechar al máximo el potencial de estas plataformas y asegurar su adaptación a las demandas del entorno digital actual.

# 5.2. Selección de modificaciones a realizar

WordPress, como gestor de contenidos de código abierto, ofrece una gran flexibilidad para adaptarse a las necesidades de cada proyecto. A través de modificaciones, podemos transformar un sitio web básico en una plataforma compleja y personalizada. Estas modificaciones pueden ser superficiales (afectan solo a la apariencia) o profundas (alteran la funcionalidad misma del sitio). A continuación, exploramos las principales categorías de modificaciones en WordPress y cómo seleccionar las más adecuadas:

Temas

El tema define la apariencia visual del sitio web, porque controla la disposición del contenido, la tipografía, los colores y otros elementos estéticos.

#### Tipos de modificaciones

**▸ Selección de temas prediseñados:** WordPress ofrece una amplia gama de temas gratuitos y de pago, cada uno con un estilo y características diferentes.

**▸ Personalización de temas:** la mayoría de los temas permiten la personalización a través de opciones integradas, como la modificación de colores, fuentes y la disposición de *widgets.*

**▸ Creación de temas a medida:** para un control total sobre el diseño, se puede desarrollar un tema desde cero o modificar un tema existente a nivel de código.

#### Criterios de selección

**▸ Diseño:** elegir un tema que se ajuste a la estética deseada y a la identidad de la marca.

**▸ Funcionalidad:** asegurarse de que el tema ofrece las características necesarias, como la integración con redes sociales, formularios de contacto o un diseño adaptable a dispositivos móviles *(responsive).*

**▸ Rendimiento:** optar por temas ligeros y optimizados para la velocidad de carga.

**▸ Soporte y actualizaciones:** verificar que el tema cuenta con soporte del desarrollador y actualizaciones regulares para garantizar la seguridad y compatibilidad.

Plugins

Los *plugins* son extensiones que añaden funcionalidades específicas a WordPress.

#### Tipos de modificaciones

**▸ Ampliar la funcionalidad:** existen *plugins* para prácticamente cualquier necesidad, desde la creación de formularios de contacto hasta la integración de tiendas *online.* **▸ Mejorar el rendimiento:plugins** para la optimización de imágenes, caché y la seguridad del sitio.

**▸ Añadir características de diseño:plugins** para la creación de *sliders,* galerías de imágenes y otros elementos visuales.

#### Criterios de selección

**▸ Funcionalidad:** elegir *plugins* que satisfagan las necesidades específicas del sitio web.

**▸ Compatibilidad:** asegurarse de que el *plugin* es compatible con la versión de WordPress y el tema en uso.

**▸ Reputación y soporte:** optar por *plugins* con buenas valoraciones, actualizaciones regulares y soporte del desarrollador.

**▸**

**▸ Seguridad:** descargar *plugins* de fuentes confiables, como el repositorio oficial de WordPress, y verificar la reputación del desarrollador.

Contenido

El contenido es la esencia de cualquier sitio web, incluyendo texto, imágenes, vídeos y otros elementos multimedia.

#### Tipos de modificaciones

**▸ Creación de contenido:** generar contenido original y relevante para el público objetivo.

**▸ Optimización de contenido:** mejorar la legibilidad, el SEO y la estructura del contenido.

**▸ Gestión de contenido:** utilizar las herramientas de WordPress para organizar, programar y publicar contenido de manera eficiente.

#### Criterios de selección

**▸ Relevancia:** crear contenido que sea útil e interesante para el público objetivo.

**▸ Calidad:** asegurarse de que el contenido esté bien escrito, sea preciso y esté libre de errores.

**▸ SEO:** optimizar el contenido para los motores de búsqueda utilizando palabras clave relevantes y una estructura adecuada.

**▸ Formato:** utilizar diferentes formatos de contenido, como texto, imágenes y vídeos, para mantener el interés del usuario.

Código

WordPress está construido con código (PHP, HTML, CSS, JavaScript), y la modificación del código permite un control total sobre la funcionalidad y apariencia del sitio.

#### Tipos de modificaciones

**▸ Personalización de funciones:** modificar el archivo functions.php para añadir o modificar funciones del tema.

**▸ Creación de plantillas personalizadas:** diseñar plantillas específicas para diferentes tipos de contenido.

**▸ Desarrollo de** ***plugins*** **a medida:** crear *plugins* para implementar funcionalidades únicas.

#### Criterios de selección

**▸ Experiencia técnica:** se requiere conocimiento de programación para realizar modificaciones de código.

**▸ Necesidad específica:** las modificaciones de código se justifican cuando las opciones de personalización estándar no son suficientes.

**▸ Mantenimiento:** es importante documentar las modificaciones de código para facilitar el mantenimiento y las actualizaciones.

Base de datos

La base de datos almacena toda la información del sitio web, incluyendo el contenido, la configuración y los datos de los usuarios.

#### Tipos de modificaciones

**▸ Optimización de la base de datos:** eliminar datos innecesarios y optimizar la estructura para mejorar el rendimiento. **▸ Migración de datos:** transferir la base de datos a un nuevo servidor o dominio. **▸ Gestión de usuarios:** controlar los permisos y roles de los usuarios.

#### Criterios de selección

**▸ Conocimiento técnico:** se requiere experiencia en la gestión de bases de datos. **▸ Seguridad:** realizar copias de seguridad de la base de datos antes de realizar cualquier modificación. **▸ Herramientas:** utilizar herramientas de gestión de bases de datos para facilitar la administración.

#### Recomendaciones

**▸ Planificación:** antes de realizar cualquier modificación, es importante planificar las necesidades del sitio web y definir los objetivos. **▸ Pruebas:** realizar pruebas exhaustivas después de cada modificación para asegurar que el sitio web funciona correctamente. **▸ Copias de seguridad:** crear copias de seguridad regulares del sitio web para evitar la pérdida de datos. **▸ Actualizaciones:** mantener WordPress, el tema y los *plugins* actualizados para

Implantación de Aplicaciones Web 9 garantizar la seguridad y compatibilidad.

**▸ Documentación:** documentar todas las modificaciones realizadas para facilitar el mantenimiento y la resolución de problemas.

Al elegir e implementar modificaciones en WordPress, es fundamental considerar las necesidades específicas del proyecto, el nivel de experiencia técnica y los recursos disponibles. Priorizar la seguridad, el rendimiento y la experiencia de usuario asegurará un sitio web funcional, atractivo y exitoso.

# 5.3. Reconocimiento de elementos involucrados

WordPress, con su flexibilidad y facilidad de uso, se ha convertido en una de las plataformas más populares para la creación de sitios web. Su capacidad para adaptarse a diversas necesidades, desde blogs personales hasta tiendas en línea complejas, se debe, en gran medida, a la posibilidad de realizar modificaciones. Sin embargo, para aprovechar al máximo esta flexibilidad es crucial comprender los elementos que intervienen en dichas modificaciones. Profundizamos en los elementos clave que permiten personalizar un sitio web de WordPress, brindando una visión completa para que puedas realizar cambios con confianza y obtener los resultados deseados.

Antes de sumergirnos en las modificaciones, es fundamental comprender la estructura básica de WordPress. Esto nos permitirá identificar los puntos de acceso para realizar cambios y comprender cómo nuestras acciones afectan al sitio web en su conjunto.

**▸ Archivos principales:** WordPress se basa en un conjunto de archivos principales que controlan su funcionamiento.

- index.php : el archivo principal que se encarga de mostrar el contenido de tu sitio web.

- wp-config.php : contiene la configuración esencial de tu sitio, como la conexión a la base de datos.

- .htaccess : un archivo que controla el comportamiento del servidor web, como redirecciones y permisos.

**▸ Base de datos:** WordPress almacena toda la información de tu sitio web en una base de datos MySQL. Esto incluye:

- Contenido: entradas, páginas, comentarios, etc.

- Configuración: opciones del tema, plugins instalados, etc.

- Usuarios: información sobre los usuarios registrados en tu sitio.

**▸ Panel de administración:** el panel de administración es la interfaz que te permite gestionar tu sitio web. Desde aquí puedes:

- Crear y editar contenido: escribir entradas, diseñar páginas, subir imágenes.

- Configurar el sitio: ajustar las opciones generales, instalar plugins, cambiar el tema.

- Gestionar usuarios: asignar roles, crear nuevos usuarios, etc.

El tema de WordPress es responsable de la apariencia visual de tu sitio. Define la disposición del contenido, los colores, las fuentes y el estilo general.

**▸ Archivos de plantilla:** los temas están compuestos por archivos de plantilla que controlan cómo se muestra el contenido en diferentes secciones del sitio web. Algunos ejemplos son:

- header.php : encabezado del sitio.

- footer.php : pie de página del sitio.

- single.php : plantilla para mostrar entradas individuales.

- page.php : plantilla para mostrar páginas estáticas.

**▸ Hojas de estilo (CSS):** el CSS define el estilo visual de los elementos del sitio web, como colores, fuentes, tamaños y espaciado.

**▸ Archivos de funciones (** functions.php **):** este archivo permite añadir funcionalidades al tema, como *widgets* personalizados, menús adicionales o código específico.

**▸ Modificaciones en temas:** puedes modificar un tema existente para adaptarlo a tus necesidades. Esto puede implicar editar los archivos de plantilla, el CSS o el archivo functions.php . Sin embargo, es importante tener en cuenta que las actualizaciones del tema pueden sobrescribir sus modificaciones. Para evitar esto, se recomienda crear un tema hijo que herede las características del tema principal y permita realizar modificaciones sin perderlas en las actualizaciones.

Modificaciones con plugins

L o s *plugins* son extensiones que añaden funcionalidades a tu sitio web. Existen *plugins* para prácticamente cualquier necesidad, desde formularios de contacto hasta tiendas en línea.

**▸** Directorio de *plugins:* WordPress cuenta con un directorio oficial con miles de *plugins* gratuitos y de pago. Puedes buscar e instalar *plugins* directamente desde el panel de administración.

**▸** *Plugins* personalizados: si necesitas una funcionalidad específica que no encuentras en el directorio, puedes desarrollar un *plugin* personalizado o contratar a un desarrollador para que lo haga por ti.

L o s *plugins* pueden modificar el comportamiento de tu sitio web de diversas maneras. Algunos ejemplos son:

**▸ Añadir nuevas funciones:** añadir un formulario de contacto, una galería de imágenes o un sistema de reservas.

**▸ Modificar el contenido:** cambiar la forma en que se muestra el contenido, añadir elementos adicionales o filtrar la información.

**▸ Mejorar el rendimiento:** optimizar la velocidad de carga del sitio, mejorar la seguridad o gestionar el caché.

Por otro lado, los *widgets* son bloques de contenido que se pueden añadir a las áreas designadas en tu tema, como las barras laterales o el pie de página. Permiten mostrar información dinámica, como entradas formularios de búsqueda.

recientes, listas de categorías o

**▸ Áreas de** ***widgets:*** los temas definen las áreas donde se pueden colocar los *widgets.*

**▸** ***Widgets*** **disponibles:** WordPress incluye una serie de *widgets* por defecto, y los *plugins* pueden añadir *widgets* adicionales.

**▸ Personalización:** puedes configurar los *widgets* para mostrar información específica y adaptarlos al diseño de tu sitio web.

Si bien los temas, *plugins* y *widgets* ofrecen una gran flexibilidad, a veces es necesario añadir código personalizado para lograr modificaciones específicas.

**▸ Código en archivos del tema:** puedes añadir código PHP, HTML, CSS o JavaScript en los archivos de tu tema para modificar su comportamiento o apariencia.

**▸** ***Plugins*** **personalizados:** si necesitas una funcionalidad compleja o quieres mantener tu código separado del tema, puedes crear un plugin personalizado.

**▸** ***Snippets:*** los *snippets* son fragmentos de código que se pueden añadir a tu sitio web para realizar pequeñas modificaciones sin necesidad de crear un *plugin* completo.

Reconocer los elementos involucrados en las modificaciones de WordPress te permite comprender cómo funciona tu sitio web a un nivel más profundo. Esto te da la capacidad de realizar cambios con confianza, ya sea utilizando las herramientas disponibles en el panel de administración, modificando los archivos del tema o añadiendo código personalizado.

Recuerda que la clave para realizar modificaciones exitosas en WordPress es la planificación y la comprensión. Antes de realizar cualquier cambio es importante tener claro el objetivo que quieres lograr y comprender, cómo tus acciones afectarán al sitio web en su conjunto.

Al embarcarte en la aventura de modificar tu sitio web WordPress, es fundamental familiarizarte con los archivos clave que dictan su estructura y funcionamiento. Estos archivos actúan como los pilares de tu sitio, y comprender su rol te permitirá realizar cambios con precisión y

confianza.

Aquí mostramos los archivos principales para tener en cuenta al realizar modificaciones en WordPress.

**▸ WP-CONFIG.PHP.** Este archivo es el corazón de tu instalación WordPress. Contiene información crucial sobre la configuración de tu sitio web, como las credenciales de la base de datos, las claves de seguridad, el prefijo de las tablas de la base de datos y otras configuraciones esenciales. Algunas modificaciones comunes son:

- Cambiar el prefijo de la base de datos para aumentar la seguridad.

- Aumentar el límite de memoria de PHP.

- Habilitar el modo de depuración para solucionar errores.

- Configurar las URL del sitio web.

**▸ .HTACCESS.** Este archivo controla la configuración del servidor web Apache. Influye en el acceso al sitio web, la redirección de URL, la configuración de la caché y la seguridad. Algunas modificaciones comunes son:

- Redirigir URL.

- Bloquear el acceso a determinadas direcciones IP.

- Habilitar la compresión GZIP.

- Configurar la caché del navegador.

**▸ FUNCTIONS.PHP.** Este archivo, ubicado en la carpeta del tema, contiene funciones personalizadas que amplían la funcionalidad del tema. Algunas modificaciones comunes son:

- Añadir nuevas funciones al tema.

- Modificar el comportamiento de las funciones existentes.

- Registrar menús personalizados.

- Añadir soporte para formatos de publicación personalizados.

**▸ HEADER.PHP.** Este archivo contiene el encabezado del sitio web, que se muestra en todas las páginas. Algunas modificaciones comunes son:

- Añadir código de seguimiento de Google Analytics.

- Insertar el código de verificación de Google Search Console.

- Modificar el título del sitio web.

**▸** Añadir enlaces a hojas de estilo externas.

**▸ FOOTER.PHP.** Este archivo contiene el pie de página del sitio web, que se muestra en todas las páginas. Algunas modificaciones comunes son:

**•** Añadir información de *copyright.*

- Insertar enlaces a las redes sociales.

- Añadir un formulario de contacto.

- Mostrar un mapa del sitio.

**▸ SINGLE.PHP.** Este archivo controla la visualización de las entradas individuales del blog. Algunas modificaciones comunes son:

- Cambiar la disposición del contenido de la entrada.

- Añadir o eliminar elementos, como la fecha de publicación, el autor o los comentarios.

- Mostrar contenido relacionado.

**▸ PAGE.PHP.** Este archivo controla la visualización de las páginas estáticas. Algunas modificaciones comunes son:

- Cambiar la disposición del contenido de la página.

- Añadir o eliminar elementos, como el título o la imagen destacada.

- Mostrar una barra lateral personalizada.

**▸ STYLE.CSS.** Este archivo contiene el código CSS, que define el estilo visual del tema. Algunas modificaciones comunes son:

- Cambiar los colores, las fuentes y el diseño del tema.

- Añadir estilos personalizados para elementos específicos.

- Ajustar el diseño responsive para diferentes dispositivos.

#### Recomendaciones

**▸ Crear copias de seguridad:** antes de realizar cualquier modificación, realiza una copia de seguridad completa de tu sitio web.

**▸ Utilizar un editor de código:** utiliza un editor de código con resaltado de sintaxis para facilitar la edición de los archivos.

**▸ Comentar los cambios:** añade comentarios en el código para explicar las modificaciones realizadas.

**▸ Probar las modificaciones:** después de realizar cualquier cambio, prueba el sitio web para asegurarte de que funciona correctamente.

Al comprender la función de estos archivos y seguir las recomendaciones, podrás realizar modificaciones en tu sitio web WordPress con mayor confianza y control, logrando la personalización y funcionalidad que deseas.

Los archivos robots.txt y sitemap.xml son herramientas fundamentales para la optimización de tu sitio web WordPress en los motores de búsqueda. Mientras que robots.txt les dice a los motores de búsqueda qué partes de tu sitio no deben rastrear, sitemap.xml les proporciona un mapa completo de tu sitio para que lo indexen de manera eficiente.

**▸ ROBOTS.TXT.** Imagina que tu sitio web es una casa y robots.txt es el portero.

Decide quién puede entrar y a qué habitaciones tiene acceso.

Bloquear el acceso a una carpeta

User-agent: * Disallow: /wp-admin/

En este ejemplo, estamos bloqueando el acceso a la carpeta /wp-admin/ para todos los robots (*). Esto evita que los motores de búsqueda indexen la sección de administración de WordPress, que no es relevante para los usuarios.

Permitir el acceso a un archivo específico

User-agent: *

Disallow: /wp-content/uploads/

Allow: /wp-content/uploads/mi-imagen.jpg

Aquí bloqueamos el acceso a la carpeta de subidas («/wp-content/uploads/»), pero permitimos el acceso a un archivo específico dentro de esa carpeta ( mi-imagen.jpg ). Esto puede ser útil si quieres que una imagen en particular sea indexada.

Bloquear un robot específico

User-agent: Googlebot-Image

Disallow: /

En este caso, estamos bloqueando el robot de imágenes de Google (Googlebot- Image) para que no rastree ninguna parte del sitio (/). Esto puede ser útil si no quieres que tus imágenes aparezcan en la búsqueda de imágenes de Google.

**▸ SITEMAP.XML.** Ahora, imagina que sitemap.xml es un mapa detallado de tu casa que muestra todas las habitaciones y cómo llegar a ellas.

XML

$$<?xml version="1.0" encoding="UTF-8"?>$$

<urlset xmlns="<http://www.sitemaps.org/schemas/sitemap/0.9>">

<url>

<loc><https://www.mi-sitio-web.com/></loc>

<lastmod>2024-10-27T12:00:00+00:00</lastmod>

</url>

<url>

<loc><https://www.mi-sitio-web.com/acerca-de/></loc>

<lastmod>2024-10-26T18:00:00+00:00</lastmod>

</url>

</url>

<loc><https://www.mi-sitio-web.com/blog/mi-primera-entrada/></loc>

<lastmod>2024-10-25T10:00:00+00:00</lastmod>

</url>

</urlset>

# 5.4. Modificación de la apariencia

WordPress ofrece una amplia gama de posibilidades para modificar la apariencia de tu sitio web, permitiéndote crear un diseño único y adaptado a tus necesidades. Estas modificaciones pueden ser sencillas, como cambiar los colores o las fuentes, o más complejas, como reestructurar animaciones.

Posibilidades de modificación

la disposición del contenido o añadir

**▸ Cambiar el tema:** la forma más sencilla de modificar la apariencia es instalar un nuevo tema. WordPress ofrece miles de temas gratuitos y de pago, con diferentes estilos, diseños y funcionalidades.

**▸ Personalizar el tema:** la mayoría de los temas incluyen opciones de personalización que te permiten modificar colores, fuentes, imágenes de fondo y otros elementos sin necesidad de tocar código.

**▸ Editar el archivo** style.css **:** para un control más preciso sobre el diseño, puedes editar el archivo style.css del tema. Aquí puedes añadir, modificar o eliminar reglas CSS para cambiar el estilo de cualquier elemento del sitio web.

**▸ Crear un tema hijo** ***(child theme):*** un tema hijo hereda la funcionalidad y el estilo del tema padre, pero te permite realizar modificaciones sin afectar al tema original. Esto es útil para preservar tus cambios cuando actualizas el tema padre.

**▸ Utilizar** ***plugins:*** algunos *plugins* ofrecen opciones de personalización adicionales, como la creación de páginas de destino, la modificación de la cabecera, o el pie de página, o la adición de elementos visuales.

**▸ Añadir código CSS personalizado:** puedes añadir código CSS personalizado al tema a través del personalizador de WordPress o utilizando un *plugin* específico.

Supongamos que quieres cambiar el color de fondo del encabezado de tu sitio web. Puedes hacerlo añadiendo el siguiente código CSS al archivo style.css de tu tema o en la sección de CSS adicional del personalizador:

CSS

/* Cambiar el color de fondo del encabezado */

.site-header {

background-color: #f0f0f0; /* Color gris claro */ }

En este ejemplo, .site-header es la clase CSS que se utiliza para el encabezado del sitio web. Al añadir la regla background-color: #f0f0f0; estamos cambiando el color de fondo a gris claro.

#### Recomendaciones

**▸** Crea una copia de seguridad antes de realizar cualquier modificación. **▸** Utiliza un editor de código con resaltado de sintaxis para facilitar la edición de archivos. **▸** Comenta los cambios que realices en el código. **▸** Prueba las modificaciones en diferentes navegadores y dispositivos. **▸** Si no tienes experiencia con CSS, utiliza las opciones de personalización del tema o un *plugin.*

Cómo crear un tema hijo en WordPress

Crear un tema hijo en WordPress es una excelente práctica para personalizar tu sitio web de forma segura. Te permite modificar la apariencia y funcionalidad sin afectar el tema principal, lo que facilita las actualizaciones. Aquí te presento dos métodos para crear un tema hijo:

#### Método 1: usando un plugin

**▸ Instalar un** ***plugin:*** ve a «Plugins», «Añadir nuevo» en tu panel de WordPress y busca un *plugin* para crear temas hijo, como Child Theme Configurator. Instálalo y actívalo.

**▸ Configurar el tema hijo:** una vez activado el *plugin,* ve a «Herramientas», «Temas hijo».

**▸ Elegir el tema padre:** selecciona el tema que estás usando actualmente como tema padre.

**▸ Crear el tema hijo:** sigue las instrucciones del *plugin* para crear el tema hijo. Generalmente, solo necesitas darle un nombre y el *plugin* se encargará del resto.

#### Método 2: manualmente

**▸ Crear una carpeta:** accede a la carpeta de temas de tu WordPress a través de un cliente FTP o el administrador de archivos de tu *hosting.* La ruta suele ser «/wpcontent/themes/».

**▸ Nombrar la carpeta:** crea una nueva carpeta dentro de «/wp-content/themes/» y nómbrala con el nombre de tu tema hijo (por ejemplo, mi-tema-hijo ).

**▸ Crear el archivo** style.css **:** dentro de la carpeta del tema hijo, crea un archivo llamado style.css . Este archivo es esencial para que WordPress reconozca el tema hijo.

**▸**

**▸ Añadir el código en** style.css **:** pega el siguiente código en el archivo style.css y reemplaza la información entre corchetes con tus propios datos:

CSS

/*

Theme Name: [Nombre del tema hijo]

Theme URI: <https://webwp.com/blog/tema-hijo-wordpress/>

Description: [Descripción del tema hijo]

Author: [Tu nombre]

Author URI: [Tu sitio web (opcional)]

Template: [Nombre de la carpeta del tema padre]

Version: 1.0.0

License: GNU General Public License v2 or later

License URI: <http://www.gnu.org/licenses/gpl-2.0.html>

Text Domain:

[Nombre del tema hijo]

*/

**▸ Crear el archivo** functions.php **(opcional):** si necesitas añadir funciones PHP personalizadas, crea un archivo llamado functions.php dentro de la carpeta del tema hijo. Para enlazar el archivo functions.php del tema hijo con el del tema padre, añade el siguiente código:

PHP

<?php add_action( 'wp_enqueue_scripts', 'enqueue_parent_styles' );

function enqueue_parent_styles() { wp_enqueue_style( 'parent-style', get_template_directory_uri() . '/style.css'

);

}

?>

**▸ Activar el tema hijo:** en tu panel de WordPress, ve a «Apariencia», «Temas» y activa el tema hijo que acabas de crear.

#### Recomendaciones

**▸ Mantén la estructura de archivos:** si quieres modificar archivos del tema padre (como header.php , footer.php , etc.), cópialos a la carpeta del tema hijo y editarlos allí.

**▸ Documenta tus cambios:** anota las modificaciones que realices en el tema hijo para futuras referencias.

**▸ Actualiza el tema padre:** al actualizar el tema padre, las modificaciones en tu tema hijo se mantendrán intactas.

Siguiendo estos pasos, podrás crear un tema hijo en WordPress y personalizar tu sitio de forma segura y eficiente. Al explorar las diferentes opciones de modificación y utilizar el código CSS con cuidado, puedes transformar la apariencia de tu sitio web WordPress y crear un diseño que refleje tu estilo y tus objetivos.

# 5.5. Incorporación y adaptación de funcionalidades

WordPress, en su esencia, ofrece una base sólida para crear sitios web, pero su verdadera potencia reside en su flexibilidad para incorporar y adaptar funcionalidades. Esto se logra, principalmente, a través de dos elementos clave: *plugins* y temas.

Plugins

son como aplicaciones que extienden las capacidades de WordPress. Puedes encontrar *plugins* para casi cualquier cosa.

#### Funcionalidades

- ▸ SEO: mejorar el posicionamiento en buscadores (ej.: Yoast SEO).

- ▸ Ecommerce: crear tiendas online (ej.: WooCommerce).

- ▸ Seguridad: proteger tu sitio de ataques (ej.: Wordfence).

- ▸ Rendimiento: optimizar la velocidad de carga (ej.: WP Super Cache).

![Figura 1. Página de plugins oficiales Fuente: WordPress España, s. f. a.](images/image-2.png)

*Figura 1. Página de plugins oficiales Fuente: WordPress España, s. f. a.*

    - Implantación de Aplicaciones Web 28

**▸ Formularios:** crear formularios de contacto o encuestas (ej.: Contact Form 7). **▸ Redes sociales:** integrar botones de compartir o *feeds* (ej.: Social Warfare). **▸ Multimedia:** gestionar galerías de imágenes o vídeos (ej.: Envira Gallery). **▸ Analítica:** monitorizar el tráfico y el comportamiento de los usuarios (ej.: Google Analytics).

#### Adaptación

Muchos *plugins* ofrecen opciones de configuración para ajustarlos a tus necesidades. Puedes modificar su comportamiento, apariencia y la forma en que interactúan con tu sitio.

Figura 2. Página de temas oficiales Fuente: WordPress España, s. f. b.

Temas

Definen la apariencia de tu sitio web. Puedes encontrar temas para diferentes nichos y propósitos.

#### Funcionalidades

**▸ Diseño responsive:** adaptar el sitio a diferentes dispositivos.

**▸ Personalización:** cambiar colores, fuentes, imágenes y diseño.

**▸** ***Widgets:*** añadir bloques de contenido en áreas específicas.

**▸ Plantillas de página:** crear diseños únicos para páginas específicas.

**▸ Soporte para** ***plugins:*** integrarse con *plugins* específicos.

#### Adaptación

Puedes modificar los archivos del tema (preferiblemente un tema hijo), para personalizar aún más su apariencia y funcionalidad. Imagina que quieres crear un sitio web para una escuela de cocina.

**▸** ***Plugins.***

- Eventos: usar The Events Calendar para mostrar el calendario de cursos y talleres.

- Recetas: instalar WP Recipe Maker para publicar recetas con un formato atractivo.

- Formulario de inscripción: integrar Gravity Forms para que los usuarios se inscriban en los cursos.

**▸ Tema:** elegir un tema con diseño *responsive,* opciones de personalización para colores e imágenes, y soporte para los *plugins* mencionados.

**▸ Adaptación.**

- Modificar el tema para mostrar las próximas clases en la página de inicio.

- Añadir una sección en la barra lateral para mostrar las recetas más populares.

- Personalizar el formulario de inscripción para solicitar información específica a los alumnos.

Como ves, WordPress te permite combinar y adaptar *plugins* y temas para crear un sitio web con la funcionalidad y apariencia que necesitas. La clave está en explorar las opciones disponibles y encontrar las que mejor se adapten a tu proyecto.

Mostrar los últimos posts de una categoría específica en la barra lateral

Este código mostrará los tres últimos *posts* de la categoría «Noticias» en la barra lateral de tu sitio web. **Añadir el código al archivo** functions.php **del tema hijo** PHP

function mostrar_ultimas_noticias() {

$$$args = array($$

'category_name' => 'noticias', // Reemplaza "noticias" con el slug de tu categoría

$$'posts\_per\_page' => 3,$$

); $query = new WP_Query( $args ); if ( $query->have_posts() ) :

echo '<ul>'; while ( $query->have_posts() ) : $query->the_post();

$$echo '<li><a href="' . get\_permalink() . '">' . get\_the\_title() . '</a></li>';$$

endwhile; echo '</ul>'; endif; wp_reset_postdata(); } add_action( 'widgets_init', 'registrar_widget_ultimas_noticias' );

function registrar_widget_ultimas_noticias() { register_widget( 'Widget_Ultimas_Noticias' ); } class Widget_Ultimas_Noticias extends WP_Widget { function __construct() { parent::__construct( 'widget_ultimas_noticias', __( 'Últimas Noticias', 'textdomain' ), array( 'description' => __( 'Muestra las últimas noticias de una categoría específica', 'textdomain' ), ) ); } public function widget( $args, $instance ) { echo $args['before_widget']; if ( ! empty( $instance['title'] ) ) { echo $args['before_title'] . apply_filters( 'widget_title', $instance['title'] ) . $args['after_title']; } mostrar_ultimas_noticias(); echo $args['after_widget'];

} public function form( $instance ) { $title = ! empty( $instance['title'] ) ? $instance['title'] : __( 'Nuevas Noticias', 'textdomain' ); ?> <p> <label for="<?php echo esc_attr( $this->get_field_id( 'title' ) ); ?>"><?php _e( esc_attr( 'Title:' ) ); ?> </label> <input class="widefat" id="<?php echo esc_attr( $this->get_field_id( 'title' ) ); ?>" name="<?php echo esc_attr( $this->get_field_name(

$$'title' ) ); ?>" type="text" value="<?php echo esc\_attr( $title ); ?>">$$

</p> <?php } public function update( $new_instance, $old_instance ) { $instance = array(); $instance['title'] = ( ! empty( $new_instance['title'] ) ) ? strip_tags( $new_instance['title'] ) : ''; return $instance; } }

#### Añadir el widget a la barra lateral

Ve a «Apariencia», «Widgets» y arrastra el *widget* «Últimas Noticias» a la barra Implantación de Aplicaciones Web 33

lateral. Puedes configurar el título del widget en esta sección.

Añadir un botón de WhatsApp flotante en las entradas

Este código añadirá un botón flotante de WhatsApp en las entradas de tu sitio web, lo

que permite a los usuarios contactarte fácilmente. **Añadir el código al archivo** functions.php **del tema hijo** PHP

function agregar_boton_whatsapp() { if ( is_single() ) { // Solo mostrar en entradas individuales ?> <a href="<https://wa.me/+[tu> número de teléfono]" target="_blank" class="boton-whatsapp">

$$<img src="[url\_icono\_whatsapp]" alt="WhatsApp">$$

</a> <style> .boton-whatsapp { position: fixed; bottom: 20px; right: 20px; z-index: 9999; } </style> <?php

} } add_action( 'wp_footer', 'agregar_boton_whatsapp' );

#### Reemplazar la información

**▸** Reemplaza «+[tu número de teléfono]» con tu número de teléfono en formato internacional (ej.: +34123456789).

**▸** Reemplaza «[URL de la imagen del icono de WhatsApp]» que quieras usar. Este código agrega un botón de WhatsApp flotante que aparece en la parte inferior derecha de la pantalla en las entradas individuales. Puedes personalizar la posición, el estilo y la imagen del botón modificando el código CSS. Recuerda que estos son solo ejemplos básicos. Puedes modificarlos y adaptarlos a tus necesidades específicas. Siempre es recomendable trabajar con un tema hijo para evitar perder tus cambios al actualizar el tema principal.

# 5.6. Verificación del funcionamiento

Verificar que las modificaciones que has hecho en WordPress funcionan correctamente es crucial para asegurar la experiencia de usuario y el rendimiento de tu sitio web. A continuación, se presentan algunas estrategias para comprobar tus cambios, tanto en apariencia como en funcionalidad.

Modificaciones de apariencia

**▸ Vista previa en vivo:** la forma más sencilla de verificar cambios de apariencia es usar la función «Vista previa en vivo» de WordPress. Al personalizar tu tema o editar el CSS, esta herramienta te permite ver los cambios en tiempo real sin afectar el sitio web publicado.

**▸ Diferentes navegadores y dispositivos:** asegúrate de que los cambios de apariencia se vean correctamente en diferentes navegadores (Chrome, Firefox, Safari, Edge) y dispositivos (ordenador, tablet, móvil). Las herramientas de desarrollo de los navegadores te permiten simular diferentes resoluciones y dispositivos.

**▸ Herramientas de validación:** utiliza validadores de código HTML y CSS, como el validador del [W3C](https://validator.w3.org/), para comprobar que tu código esté libre de errores que puedan afectar la visualización.

Modificaciones de funcionalidad

**▸ Pruebas manuales:** la mejor manera de verificar nuevas funcionalidades es probarlas manualmente. Si has añadido un formulario, rellénalo y envíalo. Si has modificado el comportamiento de los comentarios, intenta publicar uno.

**▸ Depuración de código:** Si has añadido código PHP, utiliza la función error_reporting() para mostrar errores y advertencias durante las pruebas. También puedes usar *plugins* de depuración, como Query Monitor, para analizar el rendimiento del código y detectar posibles problemas.

**▸ Plugins de prueba:** existen *plugins* específicos para probar ciertas funcionalidades. Por ejemplo, si has implementado un sistema de caché, puedes usar un *plugin* como Cache Enabler para verificar su funcionamiento.

**▸ Revisiones de código:** si has realizado cambios significativos en el código, considera pedir a otro desarrollador que revise tu trabajo. Una segunda mirada puede detectar errores que hayas pasado por alto.

**▸ Monitorización del sitio web:** utiliza herramientas de monitorización, como Google Analytics o Google Search Console, para rastrear el rendimiento de tu sitio web después de las modificaciones. Presta atención a métricas como el tiempo de carga, la tasa de rebote y los errores 404 para identificar posibles problemas.

Consejos

**▸ Realiza copias de seguridad:** antes de realizar cualquier modificación, realiza una copia de seguridad completa de tu sitio web. Esto te permitirá restaurar la versión anterior en caso de problemas.

**▸ Trabaja con un tema hijo:** siempre que sea posible, realiza las modificaciones en un tema hijo para evitar perder tus cambios al actualizar el tema principal.

**▸ Documenta tus cambios:** anota las modificaciones que realices, incluyendo el código que has añadido o modificado. Esto te ayudará a solucionar problemas en el futuro.

Siguiendo estas recomendaciones, podrás verificar el correcto funcionamiento de tus modificaciones en WordPress y garantizar un sitio web estable y funcional.

# 5.7. Documentación

Documentar las adaptaciones que realizas en tu sitio WordPress es esencial, tanto si eres un desarrollador como si simplemente gestionas tu propio sitio web. Una buena documentación te ayudará a:

**▸ Recordar los cambios:** es fácil olvidar por qué hiciste una modificación específica hace meses o incluso semanas. La documentación te refrescará la memoria.

**▸ Solucionar problemas:** si algo deja de funcionar, la documentación te ayudará a identificar la causa del problema y a revertir los cambios si es necesario.

**▸ Colaborar con otros:** si trabajas en equipo, la documentación facilita la comunicación y la comprensión del trabajo realizado.

**▸ Ahorrar tiempo:** cuando necesites realizar modificaciones similares en el futuro, la documentación te servirá de guía y te ahorrará tiempo. Algunas estrategias para documentar tus adaptaciones en WordPress son las siguientes:

Comentarios en el código

**▸ CSS:** añade comentarios en tu archivo style.css (del tema hijo) para explicar las reglas de estilo que has añadido o modificado.

CSS

/* Estilos para el botón de WhatsApp */

.boton-whatsapp {

position: fixed; bottom: 20px;

right: 20px; z-index: 5; }.

**▸ PHP:** utiliza comentarios en el archivo functions.php para describir las funciones que has creado o modificado.

PHP

/**

- Muestra las últimas noticias de la categoría "noticias" en la barra lateral.

*/

function mostrar_ultimas_noticias() { // ... código ... }

Archivo readme.txt

**▸** Crea un archivo readme.txt en la carpeta del tema hijo para documentar las modificaciones más importantes. **▸** Incluye información como:

- Nombre del tema hijo

- Descripción de las modificaciones

- Fecha de las modificaciones

- Autor de las modificaciones

- Cualquier otra información relevante

Sistema de control de versiones (Git)

**▸** Utiliza un sistema de control de versiones como Git para llevar un registro de todos los cambios en el código. **▸** Cada vez que realices una modificación, crea un commit con un mensaje descriptivo que explique el cambio. **▸** Plataformas como GitHub, GitLab o Bitbucket facilitan el uso de Git.

Documentación externa

**▸** Si las modificaciones son complejas, puedes crear un documento aparte (en un procesador de texto o una herramienta de documentación *online)* para explicarlas con más detalle. **▸** Puedes incluir capturas de pantalla, diagramas o cualquier otra información que ayude a comprender los cambios.

Plugins de documentación

Existen *plugins* de WordPress que te ayudan a documentar las modificaciones, como WP Documentor. Estos *plugins* te permiten crear una base de conocimientos dentro de tu sitio web. Consejos:

**▸ Sé claro y conciso:** utiliza un lenguaje claro y conciso en tu documentación.

**▸ Organiza la información:** estructura la documentación de forma lógica para facilitar su lectura y comprensión.

**▸ Mantén la documentación actualizada:** actualiza la documentación cada vez que realices una modificación.

Recuerda que la documentación es una inversión, que te ahorrará tiempo y dolores de cabeza en el futuro. ¡No la subestimes!

# 5.8. Referencias bibliográficas

WordPress España (s. f. a.). *Plugins.* [https://es.wordpress.org/plugins/](https://es.wordpress.org/plugins/) WordPress España (s. f. b.). *Temas.* <https://es.wordpress.org/themes/>

# Smashing Magazine. (s. f.). WordPress.

# [https://www.smashingmagazine.com/category/wordpress/](https://www.smashingmagazine.com/category/wordpress/)

# Revista online con sección dedicada a WordPress

*Smashing Magazine* es una publicación *online* de referencia para diseñadores y desarrolladores web. Su sección dedicada a WordPress ofrece artículos de alta calidad sobre diseño, desarrollo, optimización y mejores prácticas. Encontrarás información valiosa sobre la adaptación visual y funcional, con ejemplos reales y consejos de expertos.

Implantación de Aplicaciones Web 43 Tema 5. A fondo

# Página web de CSS-Tricks ([https://css-tricks.com/](https://css-tricks.com/))

# CSS-Tricks estilos web

Es un sitio web con artículos, tutoriales y guías sobre CSS, diseño web y desarrollo *front-end.* Ofrece información valiosa sobre técnicas avanzadas de CSS, trucos para solucionar problemas comunes y ejemplos de diseños creativos. Es un recurso ideal para profundizar en la adaptación visual y llevar tus habilidades de diseño al siguiente nivel.

Implantación de Aplicaciones Web 44 Tema 5. A fondo

# Como crear un tema hijo

McCollin, R. (2019, Agosto 7). *How to Create a Child Theme in WordPress (Extended* *Guide).* Kinsta. [https://kinsta.com/blog/wordpress-child-theme/](https://kinsta.com/blog/wordpress-child-theme/)

Este artículo de Kinsta ofrece una guía completa sobre la creación de temas hijos. Explica paso a paso cómo crear un tema hijo, porqué es importante y cómo utilizarlo para personalizar la apariencia de tu sitio web de forma segura.

Implantación de Aplicaciones Web 45 Tema 5. A fondo

# Entrenamiento 1

**▸ Planteamiento del ejercicio:** necesitas crear una tienda *online* para vender ropa. Es fundamental que el sitio tenga un diseño atractivo, permita gestionar el inventario, procesar pagos y ofrecer diferentes opciones de envío.

**▸ Desarrollo paso a paso.**

- Plugins: e-commerce (instala un plugin de e-commerce como WooCommerce para gestionar la tienda *online),* pasarela de pago: (integra una pasarela de pago como Stripe o PayPal, para procesar los pagos de los clientes), envío (configura las opciones de envío con *plugins* como WooCommerce Shipping).

- Tema: elige un tema compatible con WooCommerce y que ofrezca un diseño atractivo para una tienda de ropa. Algunos ejemplos son Storefront (el tema oficial de WooCommerce), Astra o OceanWP.

- Contenido: añade productos a la tienda, con descripciones detalladas, imágenes de alta calidad y precios.

**▸ Solución.**

- Plugins: WooCommerce, Stripe y WooCommerce Shipping.

- Tema: Storefront.

- Contenido: fichas de productos con información detallada, imágenes y precios.

# Entrenamiento 2

**▸ Planteamiento del ejercicio:** eres un fotógrafo y quieres crear un portafolio *online* para mostrar tu trabajo. Necesitas un diseño que destaque las imágenes, la posibilidad de organizar las fotos en galerías y un formulario de contacto para que los clientes puedan solicitar tus servicios.

**▸ Desarrollo paso a paso.**

- Tema: busca un tema con diseño minimalista que centre la atención en las imágenes. Algunos temas populares para portafolios son OceanWP, GeneratePress y Kadence WP.

- Plugins: galerías (instala un plugin para crear galerías de imágenes atractivas, como Envira Gallery o NextGEN Gallery), formulario de contacto (utiliza un *plugin* como Contact Form 7 para crear un formulario de contacto), *watermark* (si quieres proteger tus imágenes, puedes usar un plugin para añadir marcas de agua, como Easy Watermark).

- Contenido: crea galerías con tus mejores fotos, organizadas por categorías o proyectos.

**▸ Solución.**

- Tema: OceanWP.

- Plugins: Envira Gallery, Contact Form 7 y Easy Watermark.

- Contenido: galerías de fotos con imágenes de alta calidad y descripciones.

# Entrenamiento 3

**▸ Planteamiento del ejercicio:** estás creando un sitio web para una ONG que quiere mostrar información sobre sus proyectos, recibir donaciones y reclutar voluntarios.

**▸ Desarrollo paso a paso.**

- Plugins: donaciones (instala un plugin para recibir donaciones online, como GiveWP o PayPal Donations), formulario de voluntariado (crea un formulario para que los interesados puedan inscribirse como voluntarios utilizando un plugin como WPForms).

- Tema: elige un tema que transmita la misión de la ONG y que permita mostrar información de forma clara y organizada. Algunos temas adecuados para ONG son Astra, GeneratePress y Neve.

- Contenido: crea páginas con información sobre la ONG, sus proyectos, cómo donar y cómo ser voluntario.

**▸ Solución.**

- Plugins: GiveWP y WPForms.

- Tema: GeneratePress.

- Contenido: páginas con información sobre la ONG, proyectos, donaciones y voluntariado.

# Entrenamiento 4

- ▸ Planteamiento del ejercicio: quieres crear un foro online donde los usuarios

    - puedan debatir sobre un tema específico. Es importante que el sitio permita crear

    - diferentes categorías de debate, gestionar usuarios y moderar el contenido.

- ▸ Desarrollo paso a paso.

- Foro: instala un plugin para crear el foro, como bbPress o Asgaros Forum.

- Tema: elige un tema compatible con el plugin de foro que hayas elegido. Algunos temas específicos para foros son BuddyBoss y Disputo.

- Contenido: crea categorías de debate y configura las opciones de moderación.

**▸ Solución.**

- Plugins: bbPress.

- Tema: BuddyBoss.

- Contenido: categorías de debate y normas de participación.

# Entrenamiento 5

**▸ Planteamiento del ejercicio:** estás creando un blog de viajes donde compartirás tus aventuras, fotos y consejos. Quieres un diseño atractivo, la posibilidad de integrar mapas interactivos y un formulario de contacto para que los lectores puedan hacerte preguntas.

**▸ Desarrollo paso a paso:**

- Tema: busca un tema con diseño responsive, galería de imágenes destacada y secciones para integrar mapas. Algunos temas populares para blogs de viajes son Astra, OceanWP y GeneratePress.

- Plugins: mapas (instala un plugin para integrar mapas interactivos, como WP Google Maps), formulario de contacto (utiliza un *plugin* como Contact Form 7 o WPForms, para crear un formulario de contacto), SEO (instala un *plugin* de SEO, como Yoast SEO o Rank Math, para optimizar tu contenido para los motores de búsqueda).

- Contenido: crea contenido original y relevante sobre tus viajes, incluyendo descripciones detalladas, fotos de alta calidad y consejos útiles.

**▸ Solución.**

- Tema: Astra (por su flexibilidad y opciones de personalización).

- Plugins: WP Google Maps, Contact Form 7 y Yoast SEO.

- Contenido: entradas de blog con relatos de viajes, galerías de fotos y consejos para viajeros.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.4–42)*
- Tema 5. Material de estudio  *(pp.4–42)*
- A fondo  *(pp.43–45)*
- Entrenamientos  *(pp.46–50)*
- Implantación de Aplicaciones Web 4 · Implantación de Aplicaciones Web 5 · Implantación de Aplicaciones Web 6 · Implantación de Aplicaciones Web 7 · Implantación de Aplicaciones Web 8 · Implantación de Aplicaciones Web 10 · Implantación de Aplicaciones Web 11 · Implantación de Aplicaciones Web 12 · Implantación de Aplicaciones Web 13 · Implantación de Aplicaciones Web 14 · Implantación de Aplicaciones Web 15 · Implantación de Aplicaciones Web 16 · Implantación de Aplicaciones Web 17 · Implantación de Aplicaciones Web 18 · Implantación de Aplicaciones Web 19 · Implantación de Aplicaciones Web 20 · Implantación de Aplicaciones Web 21 · Implantación de Aplicaciones Web 22 · Implantación de Aplicaciones Web 23 · Implantación de Aplicaciones Web 24 · Implantación de Aplicaciones Web 25 · Implantación de Aplicaciones Web 26 · Implantación de Aplicaciones Web 27 · Implantación de Aplicaciones Web 29 · Implantación de Aplicaciones Web 30 · Implantación de Aplicaciones Web 31 · Implantación de Aplicaciones Web 32 · Implantación de Aplicaciones Web 34 · Implantación de Aplicaciones Web 35 · Implantación de Aplicaciones Web 36 · Implantación de Aplicaciones Web 37 · Implantación de Aplicaciones Web 38 · Implantación de Aplicaciones Web 39 · Implantación de Aplicaciones Web 40 · Implantación de Aplicaciones Web 41 · Implantación de Aplicaciones Web 42  *(pp.4, 5, 6, 7, 8, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 29, 30, 31, 32, 34, 35, 36, 37, 38, 39, 40, 41, 42)*
- Implantación de Aplicaciones Web 46 Tema 5. Entrenamientos · Implantación de Aplicaciones Web 47 Tema 5. Entrenamientos · Implantación de Aplicaciones Web 48 Tema 5. Entrenamientos · Implantación de Aplicaciones Web 49 Tema 5. Entrenamientos · Implantación de Aplicaciones Web 50 Tema 5. Entrenamientos  *(pp.46–50)*