## Tema 7

# Implantación de Aplicaciones Web

# Tema 7. Diseño del

# contenido y apariencia de

# documentos web

# Índice

Esquema Material de estudio

## 7.1. Introducción y objetivos

7.2. Lenguajes de marcas para representar el contenido de un documento

## 7.3. HTML5

## 7.4. Hojas de estilos CSS

7.5. Framework Bootstrap A fondo

W3C HTML5

MDN Web Docs

Documentación official de Bootstrap

Entrenamientos

Entrenamiento 1

Entrenamiento 2

Entrenamiento 3

Entrenamiento 4

Entrenamiento 5

# Esquema

![image-1](images/image-1.png)

Implantación de Aplicaciones Web 3 Tema 7. Esquema

# 7.1. Introducción y objetivos

En la era digital actual, donde la información se consume principalmente a través de pantallas, el diseño de contenido y la apariencia de los documentos web se han vuelto cruciales para captar la atención del usuario y transmitir de manera eficaz el mensaje deseado. Ya no basta con tener información valiosa: es necesario presentarla de forma atractiva, accesible y organizada para que el usuario tenga una experiencia positiva.

Un buen diseño web implica la combinación de elementos visuales, estructura de la información y usabilidad, con el objetivo de crear una interfaz atractiva, intuitiva y funcional. Esto incluye aspectos como la tipografía, el uso de imágenes y colores, la organización del contenido, la jerarquía visual y la adaptabilidad a diferentes dispositivos.

Este tema se centrará en los siguientes objetivos:

**▸ Comprender la importancia del diseño de contenido web:** analizar cómo un buen diseño influye en la experiencia del usuario, la credibilidad del sitio y el logro de los objetivos de comunicación.

**▸ Conocer los principios básicos del diseño web:** estudiar los fundamentos de la composición visual, la tipografía, la teoría del color y la usabilidad para aplicarlos en la creación de documentos web efectivos.

**▸ Aplicar técnicas de diseño de contenido:** aprender a estructurar la información, utilizar elementos multimedia, crear jerarquías visuales y optimizar la legibilidad del texto para una mejor comprensión del contenido.

**▸ Explorar las herramientas y tecnologías para el diseño web:** familiarizarse con las herramientas de diseño gráfico, editores de código y *frameworks* que facilitan la creación de sitios web.

# 7.2. Lenguajes de marcas para representar el contenido de un documento

Un lenguaje de marcas es un sistema de codificación que utiliza etiquetas o marcas para añadir información adicional al texto. Estas etiquetas no se muestran al usuario final, pero indican al *software* cómo debe interpretarse y presentarse el contenido. Permiten definir la **estructura del documento,** como títulos, párrafos, listas, etc., así como el **formato,** como negrita, cursiva, tamaño de fuente, etc.

Existen diferentes tipos de lenguajes de marcas, cada uno con sus características y aplicaciones específicas. Algunos de los más comunes son:

**▸ HTML** (Hypertext Markup Language): es el lenguaje de marcas más utilizado en la web. Permite estructurar el contenido de las páginas web, definir su formato y añadir elementos interactivos como enlaces, imágenes y formularios.

**▸ XML** (eXtensible Markup Language): es un lenguaje de marcas más flexible y extensible que HTML. Se utiliza para almacenar y transportar datos de forma estructurada, independientemente de su formato de presentación.

**▸ Markdown:** es un lenguaje de marcas ligero y fácil de aprender. Se utiliza para crear documentos de texto con formato básico, como archivos README en GitHub o artículos en blogs.

**▸ JSON** (JavaScript Object Notation): es un formato de intercambio de datos ligero y legible. Se utiliza para representar datos estructurados, como objetos y *arrays,* y es muy usado en aplicaciones web y móviles.

El uso de lenguajes de marcas ofrece numerosas ventajas: **▸ Separación de contenido y presentación:** permiten separar el contenido del documento de su formato de presentación. Esto facilita la reutilización del contenido en diferentes contextos y la aplicación de diferentes estilos de formato. **▸ Estructuración de la información:** facilitan la organización y estructuración de la información en el documento, lo que mejora su legibilidad y comprensión. **▸ Accesibilidad:** permiten crear documentos accesibles para personas con discapacidades, como deficiencias visuales o auditivas. **▸ Interoperabilidad:** facilitan el intercambio de información entre diferentes sistemas y aplicaciones. **▸ Automatización:** permiten automatizar tareas, como la generación de documentos, la validación de datos y la transformación de formatos. Los lenguajes de marcas se utilizan en una amplia variedad de aplicaciones, como: **▸ Desarrollo web:** HTML es la base de todas las páginas web. **▸ Publicación digital:** XML se utiliza en la creación de libros electrónicos, revistas digitales y otros documentos electrónicos. **▸ Gestión de datos:** XML y JSON se utilizan para almacenar y transportar datos en aplicaciones empresariales y bases de datos. **▸ Documentación técnica:** Markdown se utiliza para crear documentación técnica, archivos de ayuda y manuales de usuario. **▸ Procesamiento de texto:** LaTeX se utiliza para crear documentos científicos y académicos con un alto grado de calidad tipográfica.

A continuación, se muestran algunos ejemplos de cómo se utilizan los lenguajes de marcas para representar el contenido de un documento.

HTML

<!DOCTYPE html>

<html>

<head>

<title>Mi página web</title> </head> <body> <h1>Este es un título</h1> <p>Este es un párrafo de texto.</p> <ul> <li>Elemento 1</li> <li>Elemento 2</li> </ul>

</body>

</html>

XML

$$<?xml version="1.0"?>$$

<libro>

<titulo>El Quijote</titulo>

<autor>Miguel de Cervantes</autor> <año>1605</año>

</libro>

Markdown

# Título

Este es un párrafo de texto.

- Elemento 1

- Elemento 2

JSON

{

"nombre": "Juan Pérez", "edad": 30, "ciudad": "Madrid", "profesion": "Ingeniero", "intereses": [ "lectura", "cine", "viajar" ], "direccion": {

"calle": "Gran Vía", "numero": 45, "codigoPostal": 28013 }, "activo": true }

Los lenguajes de marcas son una herramienta fundamental para representar el contenido de los documentos electrónicos. Permiten estructurar la información, definir su formato y facilitar su procesamiento e intercambio. Su uso se ha extendido a una gran variedad de aplicaciones, desde el desarrollo web hasta la gestión de datos, y su importancia seguirá creciendo en el futuro.

# 7.3. HTML5

La historia del HTML comienza en 1980 con **Tim Berners-Lee,** un físico que trabajaba en el CERN (Organización Europea para la Investigación Nuclear). Berners-Lee propuso un sistema de hipertexto para facilitar el intercambio de información entre investigadores. Este sistema, basado en el lenguaje SGML (Standard Generalized Markup Language), daría origen al HTML (HyperText Markup Language).

En 1990, Berners-Lee creó el primer navegador web (World Wide Web) y el primer servidor web que alojaba la primera página web de la historia. Esta página contenía información básica sobre el proyecto World Wide Web y enlaces a otros documentos. El HTML utilizado era muy simple, con un conjunto limitado de etiquetas para estructurar el texto.

A lo largo de la década de 1990, el HTML evolucionó rápidamente. En 1995 se publicó el estándar HTML 2.0, que introdujo nuevas etiquetas para elementos como imágenes, formularios y tablas. Posteriormente, con la creación del W3C (World Wide Web Consortium) en 1994 se impulsó la estandarización del HTML y su desarrollo continuó con versiones como HTML 3.2, HTML 4.01 y XHTML 1.0.

HTML5 y la web dinámica

En 2014 se publicó la última versión del estándar HTML: HTML5. Esta versión introdujo importantes novedades, como:

**▸ Nuevas etiquetas semánticas:** <article> , <aside> , <nav> , <header> , <footer> ,

entre otras, que permiten estructurar el contenido de forma más significativa.

**▸ API para desarrollo web:** API para multimedia, gráficos 2D y 3D, almacenamiento local, geolocalización, etc., que permiten crear aplicaciones web más interactivas y dinámicas.

**▸ Mejoras en la accesibilidad:** atributos y elementos para mejorar la accesibilidad del contenido para personas con discapacidades. HTML5 marcó un hito en la historia del desarrollo web, proporcionando a los desarrolladores herramientas más potentes y flexibles para crear experiencias web más ricas y accesibles.

#### Estructura base de un documento HTML

Está formado por una serie de elementos, cada uno con una función específica. La estructura básica de un documento es la siguiente:

<!DOCTYPE html>

$$<html lang="es">$$

<head>

$$<meta charset="UTF-8">$$

<title>Título de la página</title> </head> <body> <h1>Título principal</h1> <p>Este es un párrafo de texto.</p> </body> </html>

**▸** <!DOCTYPE html> declara el tipo de documento, como HTML5, y elimina las revisiones adicionales de código por parte del navegador.

**▸** <html lang="es"> es el elemento raíz del documento, indica el idioma del contenido.

**▸** <head> contiene información sobre el documento, como el título, la codificación de caracteres, metadatos y enlaces a hojas de estilo.

**▸** <title> define el título de la página, que se muestra en la barra del navegador.

**▸** <body> representa el contenido visible de la página, como texto, imágenes, enlaces, etc.

**▸** <h1> define un encabezado o titular de nivel 1 de seis posibles.

**▸** <p> define un párrafo de texto.

Etiquetas y elementos HTML

Las etiquetas HTML son palabras clave que se encierran entre corchetes angulares (< y >). Se utilizan para marcar diferentes partes del contenido y definir cómo se deben mostrar. Un elemento HTML está formado por una etiqueta de apertura, el contenido y una etiqueta de cierre.

**▸** <h1> : etiqueta de apertura del encabezado de nivel 1.

**▸** </h1> : etiqueta de cierre del encabezado de nivel 1.

**▸** <h1>Este es un título</h1> : elemento HTML completo.

#### Atributos HTML

Los atributos proporcionan información adicional sobre los elementos HTML. Se colocan dentro de la etiqueta de apertura y se componen de un nombre y un valor separados por un signo igual (=). El valor del atributo se encierra entre comillas dobles (").

**▸** <a href="<https://www.google.com>">Enlace a Google </a > : el atributo href especifica la

URL del enlace.

**▸** <img src="imagen.jpg" alt="Descripción de la imagen"> : el atributo src especifica la ruta

de la imagen y el atributo alt proporciona una descripción textual de la imagen.

#### Tipos de elementos

**▸ Elementos de bloque:** ocupan todo el ancho disponible y generan saltos de línea antes y después del elemento. Ejemplos: < h1> , <p> , <div> , <ul> , <ol> , <table> .

**▸ Elementos en línea:** solo ocupan el espacio necesario para mostrar el contenido y no generan saltos de línea. Ejemplos: <strong> , <em> , <a> , <span> , <img> .

#### Validación HTML

Es importante validar el código HTML para asegurarse de que cumple con los estándares web. La validación ayuda a detectar errores en el código y a asegurar que la página se mostrará correctamente en diferentes navegadores. Existen herramientas *online,* como el validador del W3C, que permiten validar el código HTML.

#### Etiquetas de texto

**▸** <h1> a <h6> son etiquetas de encabezado que definen seis niveles de títulos, desde el más importante <h1> hasta el menos importante <h6>. Se usan para estructurar el contenido y mejorar la accesibilidad.

<h1>Este es el título principal</h1>

<h2>Este es un subtítulo</h2>

**▸** <strong> define texto importante, que se muestra típicamente en negrita. Se usa para enfatizar una palabra o frase clave.

<p>Esta es una frase <strong>muy</strong> importante.</p>

**▸** <em> define texto enfatizado, que se muestra típicamente en cursiva. Se usa para resaltar una parte del texto.

<p>Este texto está < em >enfatizado</em>.</p>

**▸** <abbr> define una abreviatura o acrónimo. Se puede usar el atributo title para proporcionar la versión completa del término.

<p>La <abbr title="Organización Mundial de la Salud">OMS</abbr> es una agencia de la ONU.</p>

**▸** <blockquote> define una cita larga. Suele mostrar el texto con sangría.

<blockquote> <p>La imaginación es más importante que el conocimiento.</p> <footer>- Albert Einstein</footer> </blockquote>

**▸** <p> define un párrafo de texto.

<p>Este es un párrafo de texto.</p>

**▸** <dfn> define un término que se está definiendo dentro del texto.

<p><dfn>HTML</dfn> es el lenguaje de marcado estándar para crear páginas web.</p>

**▸** <span> es un elemento en línea genérico sin un significado específico. Se usa para aplicar estilos o scripts a una parte del texto.

<p>Este texto tiene <span style="color: blue;">una parte en azul</span>.</p>

#### Etiquetas de estructura

**▸** <header> define la cabecera de una página o sección. Puede contener elementos como el título, el logotipo, la navegación, etc. **▸** <section> define una sección temática en un documento. **▸** <article> define una sección independiente de contenido, como una entrada de blog o un artículo de noticias. **▸** <aside> define contenido relacionado con el contenido principal, como una barra lateral o un cuadro de información. **▸** <footer> define el pie de página de una página o sección. Puede contener información como los derechos de autor, enlaces a redes sociales, etc.

#### Etiquetas de lista

**▸** <ul> define una lista desordenada (con viñetas).

<ul>

<li>Elemento 1</li>

<li>Elemento 2</li>

</ul>

**▸** <ol> define una lista ordenada (con números).

<ol>

<li>Primer elemento</li>

<li>Segundo elemento</li>

</ol>

#### Etiquetas de tabla

**▸** <table> define una tabla.

**▸** <tr> define una fila en una tabla.

**▸** <th> define una celda de encabezado en una tabla.

**▸** <td> define una celda de datos en una tabla.

<table>

<tr>

<th>Nombre</th> <th>Apellido</th> </tr> <tr> <td>Juan</td> <td>Pérez</td> </tr> </table>

#### Otras etiquetas usuales

**▸** <a> define un enlace (hipervínculo).

**•** <a href="<https://www.google.com>">Enlace a Google</a>

**▸** <img> define una imagen.

$$• <img src="imagen.jpg" alt="Descripción de la imagen">$$

**▸** <div> es un elemento de división genérico que se usa para agrupar otros elementos.

**▸** <form> define un formulario HTML para la entrada del usuario.

**▸** <input> define un control de entrada de formulario, como un campo de texto, un botón de radio o un botón de envío.

**▸** <br> inserta un salto de línea. Estas son solo algunas de las etiquetas HTML más comunes. Hay muchas otras etiquetas disponibles para crear diferentes tipos de contenido y estructuras en las páginas web. Te recomiendo consultar la documentación de HTML para obtener una lista completa y detallada de todas las etiquetas disponibles.

Estructuras complejas: construir la arquitectura web

A medida que las páginas web se vuelven más complejas es necesario utilizar una estructura HTML bien organizada para asegurar la legibilidad del código, la accesibilidad del contenido y la eficiencia del SEO. Para crear estructuras complejas se utilizan diferentes elementos HTML, como <div> , <article> , <aside> , <nav> ,

<header> , <footer> .

#### Ejemplo de estructura compleja

<!DOCTYPE html>

$$<html lang="es">$$

<head>

$$<meta charset="UTF-8">$$

<title>Mi sitio web</title> </head> <body>

<header> <h1>Mi sitio web</h1> <nav> <ul>

$$<li><a href="#">Inicio</a></li>$$

$$<li><a href="#">Acerca de</a></li>$$

$$<li><a href="#">Contacto</a></li>$$

</ul> </nav> </header> <article> <h2>Título del artículo</h2> <p>Contenido del artículo.</p> </article> <aside> <h3>Información adicional</h3> <p>Contenido relacionado con el artículo.</p> </aside> <footer> <p>Derechos de autor &copy; 2025</p>

</footer>

</body>

</html>

Etiquetado semántico: dar significado al contenido

Consiste en la utilización de las etiquetas HTML más adecuadas para representar el

significado del contenido. En lugar de utilizar etiquetas genéricas como <div> , para todo, se utilizan etiquetas específicas como <article> , <aside> , <nav> , etc.

#### Beneficios del etiquetado semántico

**▸ Mejora la accesibilidad:** facilita la navegación y la comprensión del contenido para personas con discapacidades que utilizan lectores de pantalla.

**▸ Mejora el SEO:** los motores de búsqueda pueden entender mejor la estructura y el contenido de la página, lo que puede mejorar su posicionamiento en los resultados de búsqueda.

**▸ Facilita el mantenimiento:** un código HTML semántico es más fácil de leer, comprender y mantener.

**▸ Mejora la experiencia de usuario:** un contenido bien estructurado es más fácil de leer y navegar.

#### Ejemplo de etiquetado semántico

<article> <header> <h1>Título del artículo</h1>

$$<p>Publicado por <span>Autor</span> el <time datetime="2025-01-02"> <time$$

$$datetime="2025-01-02"> 2 de enero de 2025 </time></p>$$

</header>

<p>Contenido del artículo.</p>

<footer>

$$<p>Categorías: <a href="#">Categoría 1</a>, <a href="#">Categoría 2 </a></p>$$

</footer>

</article>

En este ejemplo se utilizan etiquetas semánticas para representar las diferentes partes del artículo.

# 7.4. Hojas de estilos CSS

Con la combinación adecuada de selectores CSS puedes controlar con precisión la apariencia de tu página web y crear diseños atractivos y funcionales. Hay tres formas principales de aplicar estilos CSS en los documentos HTML. Son las siguientes:

CSS en línea (inline)

**▸** Se aplica directamente a un elemento HTML específico utilizando el atributo style . **▸** Se define dentro de la etiqueta de apertura del elemento. **▸** Tiene la mayor prioridad, sobreescribiendo cualquier otro estilo definido para ese elemento. **▸** Es útil para aplicar estilos únicos a un elemento específico, pero no es recomendable para estilos generales o reutilizables.

#### Ejemplo

<p style="color: red; font-size: 18px;">Este párrafo tiene estilo en línea.</p>

CSS interno (embedded)

**▸** Se define dentro de la sección <head> del documento HTML, utilizando la etiqueta

<style> .

**▸** Los estilos definidos dentro de <style> se aplican a todos los elementos del documento. **▸** Tiene mayor prioridad que el CSS externo, pero menor que el CSS en línea. **▸** Es útil para aplicar estilos específicos a un solo documento HTML.

#### Ejemplo

<!DOCTYPE html>

<html>

<head>

<style> p { color: blue; font-size: 16px; } </style> </head> <body> <p>Este párrafo tiene estilo interno.</p>

</body>

</html>

CSS externo (external)

**▸** Se define en un archivo CSS separado con la extensión .css.

**▸** Se vincula al documento HTML mediante la etiqueta <link> dentro de la sección

<head> .

**▸** Tiene la menor prioridad, pero es la forma más recomendable de aplicar estilos.

**▸** Permite separar el contenido (HTML) de la presentación (CSS), lo que facilita el mantenimiento y la reutilización de estilos en varios documentos.

#### Archivo estilos.css

p { color: green; font-size: 14px;

}

#### Archivo index.html

<!DOCTYPE html>

<html>

<head>

$$<link rel="stylesheet" href="estilos.css">$$

</head>

<body>

<p>Este párrafo tiene estilo externo.</p>

</body>

</html>

Prioridad de los estilos

En caso de conflicto entre estilos definidos de diferentes maneras, se aplica la siguiente regla de prioridad:

**▸ CSS en línea:** tiene la mayor prioridad.

**▸ CSS interno:** tiene mayor prioridad que el CSS externo.

**▸ CSS externo:** tiene la menor prioridad.

#### Recomendaciones

**▸** Utilizar CSS externo siempre que sea posible para facilitar el mantenimiento y la reutilización de estilos.

**▸** Utilizar CSS interno para estilos específicos de un solo documento.

**▸** Utilizar CSS en línea solo en casos excepcionales donde sea necesario aplicar un estilo único a un elemento específico.

**▸** Mantener una estructura HTML limpia y semántica para facilitar la aplicación de estilos CSS. Los selectores CSS son la clave para aplicar estilos a elementos específicos en tu página web. Actúan como un filtro, identificando las etiquetas HTML a las que quieres dar formato. Una vez que has seleccionado un elemento (o grupo de elementos), puedes modificar su apariencia (color, tamaño, posición, etc.) a través de las propiedades CSS.

Veamos los tipos de selectores más comunes y cómo se aplican:

#### Básicos

▸ Selector universal (*): selecciona todos los elementos del documento HTML. Útil para aplicar estilos generales o reiniciar estilos por defecto.

- {

margin: 0; padding: 0; }

**▸ Selector de tipo** ***(element):*** selecciona todos los elementos de un tipo específico.

Por ejemplo, p selecciona todos los párrafos, h1 todos los encabezados de nivel 1, etc.

p { color: blue; font-size: 16px; }

**▸ Selector de clase** (.classname) **:** selecciona todos los elementos que tienen un atributo class con el valor especificado. Permite aplicar estilos a grupos de elementos con características comunes.

$$<p class="destacado">Este párrafo es importante.</p>$$

.destacado { background-color: yellow;

font-weight: bold; }

**▸ Selector de ID (** #id **):** selecciona un único elemento con el atributo ID especificado.

Útil para aplicar estilos a elementos únicos en la página.

$$<h1 id="titulo-principal">Título principal</h1>$$

#titulo-principal { text-align: center; font-size: 36px;

}

Combinadores

Permiten seleccionar elementos en función de su relación con otros elementos en el

documento HTML.

**▸ Selector descendiente (** element element **):** selecciona todos los elementos descendientes de un elemento padre.

article p { line-height: 1.5; }

Esto seleccionaría todos los párrafos dentro de cualquier elemento <article> .

**▸ Selector hijo (** element > element **):** selecciona solo los elementos hijos directos de un elemento padre.

ul > li { list-style-type: square;

}

Esto seleccionaría solo los elementos <li> , que son hijos directos de un elemento

<ul> .

**▸ Selector hermano adyacente (** element + element **):** selecciona un elemento que está inmediatamente después de otro elemento hermano.

h2 + p { margin-top: 0; }

Esto seleccionaría el primer párrafo que aparece inmediatamente después de un encabezado <h2> .

**▸ Selector hermano general (** element ~ element **):** selecciona todos los elementos hermanos que aparecen después de un elemento específico.

h2 ~ p { font-size: 14px;

} Esto seleccionaría todos los párrafos que son hermanos de un <h2> y aparecen después de él.

Atributos

Permiten seleccionar elementos basándose en la presencia o valor de un atributo. **▸** [attribute] **:** selecciona todos los elementos que tienen el atributo especificado. **▸** [attribute=value] **:** selecciona todos los elementos que tienen el atributo especificado con el valor exacto. **▸** [attribute~=value] **:** selecciona todos los elementos que tienen el atributo especificado con un valor que contiene la palabra clave especificada. **▸** [attribute|=value] **:** selecciona todos los elementos que tienen el atributo especificado con un valor que comienza con la palabra clave especificada. **▸** [attribute^=value] **:** selecciona todos los elementos que tienen el atributo especificado con un valor que comienza con la cadena especificada. **▸** [attribute$=value] **:** selecciona todos los elementos que tienen el atributo especificado con un valor que termina con la cadena especificada. ▸ [attribute*=value] : selecciona todos los elementos que tienen el atributo especificado con un valor que contiene la cadena especificada.

Pseudoclases y pseudoelementos

**▸** Pseudoclases: permiten seleccionar elementos en función de su estado ( :hover,

:active, :focus, :visited ) o posición en el documento ( :first-child, :last-child, :nth-child(n) ). a:hover { text-decoration: underline; }

**▸** Pseudoelementos: permiten seleccionar y aplicar estilos a partes específicas de un

elemento ( :before, :after, ::first-letter, ::first-line ). p::first-letter { font-size: 2em; }

Consejos para aplicar selectores CSS

**▸ Sé específico:** utiliza selectores lo más específicos posible para evitar conflictos y asegurar que los estilos se apliquen correctamente. **▸ Utiliza clases para estilos reutilizables:** define clases para estilos que se van a aplicar a varios elementos. **▸ Mantén la estructura HTML limpia y semántica:** un buen HTML facilita la aplicación de selectores CSS. **▸ Utiliza herramientas de desarrollo:** las herramientas de desarrollo de los navegadores web te permiten inspeccionar el código HTML y CSS, y ver cómo se aplican los estilos a los elementos.

Flexbox

Es una herramienta poderosa de CSS que facilita la creación de *layouts* flexibles y dinámicos en HTML. Vamos a ver, a continuación, cómo usarla:

#### Conceptos básicos

Flexbox opera sobre dos ejes: **▸ Eje principal:** define la dirección en la que se disponen los elementos flexibles (horizontal o vertical). **▸ Eje transversal:** es perpendicular al eje principal.

Los elementos dentro de un contenedor Flexbox se llaman **elementos flexibles** *(flex* *items).* El contenedor que los contiene se llama **contenedor flexible** *(flex container).* Para usar Flexbox, primero debes definir un contenedor flexible. Esto se hace con la propiedad *display* en CSS:

.contenedor { display: flex; /* o inline-flex */ }

**▸** display: flex; crea un contenedor de bloque flexible.

**▸** display: inline-flex crea un contenedor de línea flexible. Estas propiedades se aplican al contenedor padre y afectan la disposición de los elementos flexibles:

**▸** flex-direction **:** define la dirección del eje principal.

- row (predeterminado): elementos dispuestos horizontalmente de izquierda a derecha.

- row-reverse : elementos dispuestos horizontalmente de derecha a izquierda.

- column : elementos dispuestos verticalmente de arriba a abajo.

- column-reverse : elementos dispuestos verticalmente de abajo a arriba.

**▸** flex-wrap **:** controla si los elementos flexibles deben ajustarse a una sola línea o pueden envolverse en varias líneas.

- nowrap (predeterminado): los elementos se mantienen en una sola línea.

- wrap : los elementos se envuelven en varias líneas si es necesario.

- wrap-reverse : los elementos se envuelven en varias líneas en orden inverso.

**▸** flex-flow **:** es una abreviatura para combinar flex-direction y flex-wrap . **▸** justify-content **:** alinea los elementos flexibles a lo largo del eje principal.

- flex-start (predeterminado): elementos alineados al inicio del eje.

- flex-end : elementos alineados al final del eje.

- center : elementos centrados en el eje.

- space-between : elementos distribuidos uniformemente con espacio entre ellos.

- space-around : elementos distribuidos uniformemente con espacio alrededor de cada uno.

- space-evenly : elementos distribuidos uniformemente con el mismo espacio entre ellos y a los bordes.

**▸** align-items **:** alinea los elementos flexibles a lo largo del eje transversal.

- flex-start : elementos alineados al inicio del eje transversal.

- flex-en d: elementos alineados al final del eje transversal.

- center : elementos centrados en el eje transversal.

- stretch (predeterminado): los elementos se estiran para llenar el contenedor en el eje transversal.

- baseline : los elementos se alinean según la línea base de su texto.

**▸** align-content **:** alinea las líneas de elementos flexibles cuando hay varias líneas debido a flex-wrap . Similar a justify-content , pero en el eje transversal.

#### Propiedades de los elementos flexibles

Estas propiedades se aplican a los elementos hijos dentro del contenedor flexible: **▸** order **:** controla el orden en que aparecen los elementos flexibles. El valor predeterminado es 0. Los elementos con valores más altos se colocan más tarde en el orden. **▸** flex-grow **:** define cuánto puede crecer un elemento flexible en relación con los demás elementos. **▸** flex-shrink **:** define cuánto puede encogerse un elemento flexible en relación con los demás elementos. **▸** flex-basis **:** define el tamaño inicial de un elemento flexible antes de que se distribuya el espacio restante. **▸** flex **:** es una abreviatura para combinar flex-grow , flex-shrink y flex-basis . **▸** align-self **:** permite anular la alineación del elemento flexible establecida por alignitems en el contenedor padre. Ejemplo de uso de Flexbox:

$$<div class="contenedor">$$

$$<div class="item">Item 1</div>$$

$$<div class="item">Item 2</div>$$

$$<div class="item">Item 3</div>$$

</div> .contenedor { display: flex;

justify-content: space-around; align-items: center; } .item { width: 100px; height: 100px; background-color: lightblue; border: 1px solid black; }

Este código creará un contenedor flexible con tres elementos. Los elementos se distribuirán con espacio alrededor de cada uno y estarán centrados verticalmente. Flexbox ofrece un control preciso sobre la disposición de los elementos en la página. Experimentando con las diferentes propiedades y valores puedes crear *layouts* complejos y adaptables a diferentes tamaños de pantalla. Es recomendable consultar la documentación de Flexbox en MDN Web Docs para obtener información más detallada y ejemplos avanzados.

# 7.5. Framework Bootstrap

Bootstrap es un *framework* CSS de código abierto muy popular que facilita el desarrollo web front-end. Proporciona una colección de clases CSS predefinidas y componentes JavaScript que puedes usar para crear rápidamente interfaces web atractivas, responsivas y consistentes. Vamos a ver cómo usar Bootstrap en un documento HTML:

Incluir Bootstrap en tu proyecto

Hay dos formas principales de incluir Bootstrap en tu proyecto:

**▸ Usando una CDN** *(content delivery network):* esta es la forma más sencilla.

Simplemente agrega los enlaces a las hojas de estilo CSS y los archivos JavaScript de Bootstrap en la sección <head> de tu documento HTML.

<!DOCTYPE html>

$$<html lang="es">$$

<head>

$$<meta charset="UTF-8">$$

$$<meta name="viewport" content="width=device-width, initial-$$

$$scale=1.0">$$

<title>Mi sitio web con Bootstrap</title>

<link href="<https://cdn.jsdelivr.net/npm/bootstrap@5.3.0->

$$alpha1/dist/css/bootstrap.min.css" rel="stylesheet"$$

$$integrity="sha384-$$

GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD"

$$crossorigin="anonymous">$$

<script src="<https://cdn.jsdelivr.net/npm/bootstrap@5.3.0>

$$alpha1/dist/js/bootstrap.bundle.min.js" integrity="sha384-$$

w76AqPfDkMBDXo30jS1Sgez6pr3x5MlQ1ZAGC+nuZB+EYdgRZgiwxhTBTkF7CXvN"

$$crossorigin="anonymous"></script>$$

</head>

<body>

</body>

</html>

**▸ Descargando los archivos:** puedes descargar los archivos CSS y JavaScript de Bootstrap desde su sitio web oficial y alojarlos en tu propio servidor. Luego, enlaza estos archivos en tu documento HTML.

Sistema de cuadrícula (grid)

El sistema de cuadrícula de Bootstrap es una de sus características más poderosas. Permite crear *layouts* responsivos dividiendo la página en doce columnas. Puedes definir el ancho de las columnas para diferentes tamaños de pantalla (xs, sm, md, lg, xl, xxl) usando clases predefinidas como col-sm-4 , col-md-8 , etc.

$$<div class="container">$$

$$<div class="row">$$

$$<div class="col-sm-6">Columna 1</div>$$

$$<div class="col-sm-6">Columna 2</div>$$

</div> </div>

Bootstrap ofrece una amplia gama de componentes predefinidos, como: **▸ Botones:** clases para crear botones con diferentes estilos y tamaños (btn, btn-

primary , btn-lg , etc.).

**▸ Formularios:** clases para estilizar formularios y sus elementos ( form-control , formlabel , etc.). **▸ Alertas:** clases para mostrar mensajes de alerta al usuario ( alert , alert-success , alertdanger , etc.). **▸ Tarjetas:** clases para crear tarjetas con contenido ( card , card-header , card-body , etc.). **▸ Modales:** componentes para crear ventanas modales ( modal , modal-dialog , modalcontent , etc.). **▸ Carruseles:** componentes para crear carruseles de imágenes ( carousel , carouselitem , etc.).

**▸** Y **muchos más:** navbar , dropdown , collapse , etc.

#### Utilidades

Bootstrap también proporciona una serie de clases de utilidad para aplicar estilos rápidamente, como: **▸ Márgenes y** ***paddings:*** clases para controlar los márgenes y *paddings* ( mt-3 , p-2 , etc.). **▸ Colores:** clases para aplicar colores de fondo y texto ( bg-primary , text-white , etc.). **▸ Alineación:** clases para alinear texto e imágenes ( text-center , align-items-center , etc.). **▸ Mostrar/ocultar:** clases para mostrar u ocultar elementos en diferentes tamaños de pantalla ( d-none , d-md-block , etc.).

#### Ventajas de usar Bootstrap

**▸ Ahorra tiempo:** no necesitas escribir CSS desde cero.

**▸ Responsivo:** crea *layouts* que se adaptan a diferentes dispositivos.

**▸ Consistente:** proporciona una apariencia uniforme en todas las páginas.

**▸ Fácil de usar:** tiene una documentación completa y una gran comunidad.

**▸ Accesible:** sigue las mejores prácticas de accesibilidad web.

En resumen, Bootstrap es una herramienta poderosa que te permite crear interfaces web atractivas y funcionales de forma rápida y eficiente, explora su documentación y ejemplos para aprovechar al máximo posibilidades. sus características y sus enormes

# Página web HTML5 ([https://www.w3.org/TR/html5/](https://www.w3.org/TR/html5/)).

# W3C HTML5

La especificación oficial de HTML5 del W3C es la fuente definitiva para comprender el lenguaje y sus características. Aquí encontrarás información detallada sobre todas las etiquetas HTML, sus atributos y su uso correcto. Es un recurso fundamental para cualquier desarrollador web que quiera escribir código HTML válido y semántico.

Implantación de Aplicaciones Web 39 Tema 7. A fondo

# HTML: HyperText Markup Language. (s. f.). MDN Web Docs.

# [https://developer.mozilla.org/en-US/docs/Web/HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)

# MDN Web Docs

Es una plataforma de documentación web completa y actualizada, mantenida por Mozilla. Ofrece tutoriales, referencias y ejemplos sobre una amplia gama de tecnologías web, incluyendo HTML, CSS y JavaScript. Es un recurso invaluable para aprender y resolver dudas sobre desarrollo web.

Implantación de Aplicaciones Web 40 Tema 7. A fondo

# Página web de Bootstrap ([https://getbootstrap.com/](https://getbootstrap.com/))

# Documentación official de Bootstrap

La documentación oficial de Bootstrap proporciona una guía completa sobre cómo usar este *framework* CSS. Incluye información sobre el sistema de cuadrícula, los componentes predefinidos, las clases de utilidad y la personalización. Es un recurso esencial para cualquier desarrollador que quiera aprovechar las ventajas de Bootstrap para crear interfaces web responsivas y atractivas.

Implantación de Aplicaciones Web 41 Tema 7. A fondo

# Entrenamiento 1

- ▸ Planteamiento del ejercicio: crea un documento HTML básico con un título, un

    - encabezado y un párrafo de texto.

- ▸ Desarrollo paso a paso.

- Abre un editor de texto.

- Escribe la estructura básica de un documento HTML, incluyendo las etiquetas <!DOCTYPE html> , <html> , <head> , <title> y <body> .

- Dentro de la etiqueta <title> escribe el título de tu página.

- Dentro de la etiqueta <body> agrega un encabezado <h1> con un texto y un párrafo <p> con otro texto.

- Guarda el archivo con la extensión .html y ejecuta para ver el resultado en tu navegador.

**▸ Solución:**

<!DOCTYPE html>

$$<html lang="es">$$

<head>

$$<meta charset="UTF-8">$$

<title>Mi página web</title> </head> <body> <h1>Este es mi título</h1> <p>Este es un párrafo de texto.</p> </body> </html>

# Entrenamiento 2

**▸ Planteamiento del ejercicio:** crea una lista desordenada en HTML y aplica estilos CSS para que las viñetas sean cuadradas y de color rojo.

**▸ Desarrollo paso a paso.**

- Crea un documento HTML con una lista desordenada <ul> que contenga al menos tres elementos <li> .

- Agrega una etiqueta <style> dentro de la sección <head> o crea un archivo CSS externo.

- Dentro de la etiqueta <style> o en el archivo CSS, escribe un selector CSS para la lista (ul) y usa las propiedades list-style-type para cambiar el tipo de viñeta y color para cambiar el color.

**▸ Solución:**

<!DOCTYPE html>

$$<html lang="es">$$

<head>

$$<meta charset="UTF-8">$$

<title>Lista con estilos</title> <style> ul { list-style-type: square; color: red;

} </style> </head> <body> <ul> <li>Elemento 1</li> <li>Elemento 2</li> <li>Elemento 3</li> </ul> </body> </html>

# Entrenamiento 3

**▸ Planteamiento del ejercicio:** crea un contenedor flexible con tres elementos. Los elementos deben estar dispuestos horizontalmente, centrados verticalmente y con espacio entre ellos. **▸ Desarrollo paso a paso.**

- Crea un documento HTML con un <div> que será el contenedor flexible y tres <div> dentro como elementos flexibles.

- Agrega una etiqueta <style> o un archivo CSS externo.

- Aplica la propiedad display: flex; al contenedor.

- Utiliza las propiedades justify-content y align-items para alinear los elementos.

**▸ Solución:**

<!DOCTYPE html>

$$<html lang="es">$$

<head>

$$<meta charset="UTF-8">$$

<title>Flexbox layout</title>

<style>

.contenedor { display: flex; justify-content: space-between;

align-items: center; height: 200px; /* Altura contenedor*/ border: 1px solid black; } </style> </head> <body>

$$<div class="contenedor">$$

<div>Elemento 1</div> <div>Elemento 2</div> <div>Elemento 3</div> </div> </body> </html>

# Entrenamiento 4

- ▸ Planteamiento del ejercicio: crea un botón en HTML y utiliza una clase de

    - Bootstrap para darle un estilo azul.

- ▸ Desarrollo paso a paso.

- Incluye la hoja de estilo de Bootstrap en tu documento HTML (usando el enlace o descargando el archivo bootstrap.min.css ).

- Crea un botón con la etiqueta <button> .

- Agrega la clase btn y btn-primary al botón.

**▸ Solución:**

<!DOCTYPE html>

$$<html lang="es">$$

<head>

$$<meta charset="UTF-8">$$

$$<meta name="viewport" content="width=device-width, initial-$$

$$scale=1.0">$$

<title>Botón con Bootstrap</title> <link href="<https://cdn.jsdelivr.net/npm/bootstrap@5.3.0->

$$alpha1/dist/css/bootstrap.min.css" rel="stylesheet"$$

$$integrity="sha384-$$

GLhlTQ8iRABdZLl6O3oVMWSktQOp6b7In1Zl3/Jr59b6EGGoI1aFkw7cmDA6j6gD"

$$crossorigin="anonymous">$$

</head>

<body>

$$<button class="btn btn-primary">Mi botón</button>$$

</body>

</html>

# Entrenamiento 5

**▸ Planteamiento del ejercicio:** crea un documento HTML con varios párrafos. Aplica un color de texto diferente a los párrafos que están dentro de un <article> y que además tienen la clase "destacado".

**▸ Desarrollo paso a paso.**

- Crea un documento HTML con un <article> que contenga varios párrafos <p>.

- Añade la clase "destacado" a algunos de los párrafos.

- En un archivo CSS o dentro de una etiqueta <style>, escribe un selector CSS que combine el selector de tipo p, el selector descendiente article p y el selector de clase .destacado.

- Aplica la propiedad color a este selector.

**▸ Solución:**

<!DOCTYPE html>

$$<html lang="es">$$

<head>

$$<meta charset="UTF-8">$$

<title>Selectores combinados</title> <style> article p.destacado { color: blue; } </style>

</head> <body> <article> <p>Párrafo normal.</p>

$$<p class="destacado">Párrafo destacado.</p>$$

<p>Otro párrafo normal.</p>

$$<p class="destacado">Otro párrafo destacado.</p>$$

</article> </body> </html>

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.4–38)*
- Tema 7. Material de estudio  *(pp.4–38)*
- A fondo  *(pp.39–41)*
- Entrenamientos  *(pp.42–51)*
- Implantación de Aplicaciones Web 4 · Implantación de Aplicaciones Web 5 · Implantación de Aplicaciones Web 6 · Implantación de Aplicaciones Web 7 · Implantación de Aplicaciones Web 8 · Implantación de Aplicaciones Web 9 · Implantación de Aplicaciones Web 10 · Implantación de Aplicaciones Web 11 · Implantación de Aplicaciones Web 12 · Implantación de Aplicaciones Web 13 · Implantación de Aplicaciones Web 14 · Implantación de Aplicaciones Web 15 · Implantación de Aplicaciones Web 16 · Implantación de Aplicaciones Web 17 · Implantación de Aplicaciones Web 18 · Implantación de Aplicaciones Web 19 · Implantación de Aplicaciones Web 20 · Implantación de Aplicaciones Web 21 · Implantación de Aplicaciones Web 22 · Implantación de Aplicaciones Web 23 · Implantación de Aplicaciones Web 24 · Implantación de Aplicaciones Web 25 · Implantación de Aplicaciones Web 26 · Implantación de Aplicaciones Web 27 · Implantación de Aplicaciones Web 28 · Implantación de Aplicaciones Web 29 · Implantación de Aplicaciones Web 30 · Implantación de Aplicaciones Web 31 · Implantación de Aplicaciones Web 32 · Implantación de Aplicaciones Web 33 · Implantación de Aplicaciones Web 34 · Implantación de Aplicaciones Web 35 · Implantación de Aplicaciones Web 36 · Implantación de Aplicaciones Web 37 · Implantación de Aplicaciones Web 38  *(pp.4–38)*
- Implantación de Aplicaciones Web 42 Tema 7. Entrenamientos · Implantación de Aplicaciones Web 43 Tema 7. Entrenamientos · Implantación de Aplicaciones Web 44 Tema 7. Entrenamientos · Implantación de Aplicaciones Web 45 Tema 7. Entrenamientos · Implantación de Aplicaciones Web 46 Tema 7. Entrenamientos · Implantación de Aplicaciones Web 47 Tema 7. Entrenamientos · Implantación de Aplicaciones Web 48 Tema 7. Entrenamientos · Implantación de Aplicaciones Web 49 Tema 7. Entrenamientos · Implantación de Aplicaciones Web 50 Tema 7. Entrenamientos · Implantación de Aplicaciones Web 51 Tema 7. Entrenamientos  *(pp.42–51)*