## Tema 8

# Implantación de Aplicaciones Web

# Tema 8. Programación de documentos web utilizando lenguajes de script del

# cliente

# Índice

Esquema Material de estudio

## 8.1. Introducción y objetivos

8.2. Diferencias entre la ejecución en lado del cliente y del servidor

## 8.3. Modelo de objetos del documento DOM

## 8.4. Validación de formularios

## 8.5. Introducción de comportamientos dinámicos.

Captura de eventos 8.6. Limitaciones y riesgos de ataques A fondo

JavaScript Algorithms and Data Structures.

W3Schools Online Web Tutorials

Como crear un tema hijo

Entrenamientos

Entrenamiento 1

Entrenamiento 2

Entrenamiento 3

Entrenamiento 4

Entrenamiento 5

# Esquema

![image-1](images/image-1.png)

Implantación de Aplicaciones Web 3 Tema 8. Esquema

# 8.1. Introducción y objetivos

La web ha evolucionado de páginas

estáticas a experiencias dinámicas e

interactivas. Esta transformación ha sido impulsada en gran medida por los lenguajes d e *script* del lado del cliente y, entre ellos, **JavaScript** se destaca como el rey indiscutible.

JavaScript permite a los desarrolladores web dar vida a las páginas web, añadiendo funcionalidades que van desde simples animaciones hasta complejas aplicaciones web. A través de JavaScript podemos manipular el contenido, la estructura y el estilo de un documento HTML en tiempo real, respondiendo a las acciones del usuario y creando interfaces ricas y atractivas.

Este tema se adentra en el mundo de

la programación web con JavaScript.

Explicaremos los fundamentos de este lenguaje, su sintaxis y cómo utilizarlo para manipular el **Document Object Model**

(DOM). Aprenderemos a crear efectos

visuales, validar formularios, procesar datos y construir aplicaciones web interactivas.

Al finalizar este tema serás capaz de: **▸** Comprender los **conceptos básicos de JavaScript:** variables, tipos de datos, operadores, estructuras de control, funciones y objetos. **▸** Dominar la manipulación del DOM: acceder, modificar y crear elementos HTML dinámicamente. **▸** Utilizar JavaScript para responder a eventos del usuario: clics, movimientos del ratón, envío de formularios, etc. **▸** Implementar validación de formularios del lado del cliente. **▸** Utilizar JavaScript para realizar solicitudes asíncronas (AJAX) y actualizar el contenido de la página sin recargar.

# 8.2. Diferencias entre la ejecución en lado del cliente y del servidor

La ejecución de código en la web puede ocurrir en dos lugares principales: el cliente (tu navegador web) y el servidor (un ordenador remoto que aloja la página web, aunque también puede ser el *localhost* de tu equipo). Ambos juegan roles cruciales, pero tienen diferencias significativas.

Ejecución en el cliente (lado del cliente)

Se produce directamente en tu navegador web (Chrome, Firefox, Safari, etc.). Los lenguajes más comunes, en cliente son HTML, CSS y JavaScript.

**▸** Qué nos **ofrece:**

- Muestra la interfaz de usuario de la página web.

- Responde a tus interacciones (clics, desplazamiento, formularios).

- Realiza validaciones básicas de datos.

- Puede actualizar partes de la página sin recargar completamente (AJAX).

**▸** Que **obtenemos** con su utilización:

- Interactividad: permite crear interfaces dinámicas y responsivas.

- Menos carga del servidor: el navegador realiza parte del trabajo, liberando recursos del servidor.

- Experiencia de usuario más rápida: las acciones del usuario se procesan inmediatamente sin esperar respuestas del servidor.

**▸ Problemas** que resolver:

- Seguridad: el código es visible para el usuario, lo que puede generar vulnerabilidades.

- Dependencia del navegador: la ejecución puede variar según el navegador del usuario.

- Limitaciones de acceso: el acceso a recursos del sistema (como archivos) es limitado.

Ejecución en el servidor (lado del servidor)

Se produce en un ordenador remoto (servidor) que aloja la página web. Los lenguajes de programación más usados son Python, PHP, Java, Node.js, Ruby. **▸** Que nos **ofrece:**

- Procesa la lógica de la aplicación web.

- Accede y gestiona bases de datos.

- Genera contenido dinámico para la página web.

- Controla la seguridad y autenticación de usuarios.

**▸** Que **obtenemos** con su utilización:

- Seguridad: el código se ejecuta en el servidor y no es visible para el usuario.

- Acceso a recursos: tiene acceso a bases de datos, archivos del servidor y otros recursos.

- Mayor control: el desarrollador tiene mayor control sobre el entorno de ejecución.

**▸ Problemas** que resolver:

- Mayor carga del servidor: el servidor realiza la mayor parte del procesamiento.

- Latencia: las acciones del usuario requieren una comunicación con el servidor, lo que puede generar retrasos.

- Escalabilidad: se requiere una infraestructura adecuada para manejar un gran número de usuarios.

![image-2](images/image-2.png)

Tabla 1. Características cliente-servidor Fuente: elaboración propia

Ambos lados, cliente y servidor, trabajan en conjunto para ofrecer una experiencia web completa. El cliente se encarga de la presentación y la interactividad, mientras que el servidor gestiona la lógica y los datos.

# 8.3. Modelo de objetos del documento DOM

El Modelo de Objetos del Documento (DOM) es una interfaz de programación para documentos HTML y XML. Imagina que es un JavaScript con la estructura de una página web. puente que conecta tu código

En esencia, el DOM representa el documento HTML como un árbol de objetos. Cada elemento HTML, atributo y texto en la página se convierte en un nodo en este árbol, y a través de JavaScript puedes acceder y manipular estos nodos para:

**▸ Cambiar el contenido de la página:** podemos modificar el texto de un párrafo, insertar nuevas imágenes o incluso eliminar elementos completos.

**▸ Modificar el estilo de la página:** se pueden cambiar colores, fuentes, tamaños y cualquier propiedad CSS de los elementos.

**▸ Reaccionar a las acciones del usuario:** podremos hacer que la página responda a eventos como clics, movimientos del ratón o el envío de un formulario.

¿Cómo funciona el DOM?

El navegador web analiza el código HTML y lo convierte en una estructura de datos en forma de árbol. Este árbol se conoce como

el **árbol DOM.** JavaScript te

proporciona métodos para acceder a cualquier nodo del árbol DOM, puedes buscar nodos por su nombre de etiqueta, ID, clase CSS o su posición en el árbol. Una vez que tienes acceso a un nodo es posible modificarlo de muchas maneras, por ejemplo: cambiar su contenido, sus atributos, su estilo o incluso eliminarlo del árbol.

Observa este código HTML:

<!DOCTYPE html>

<html>

<head>

<title>Ejemplo DOM</title>

</head>

<body>

<h1>Hola Mundo!</h1>

<p>Este es un párrafo.</p>

</body>

</html>

El DOM representaría este código como un árbol con nodos para html , head , title ,

body , h1 y p . Ahora, con JavaScript podrías hacer algo como:

// Obtener el elemento <h1> var titulo = document.querySelector("h1"); // Cambiar el texto del <h1> titulo.textContent = "Nuevo Título";

Esto cambiaría el contenido del <h1> en la página web a 'Nuevo Título' . El DOM es una herramienta esencial para la programación web con JS. Te permite interactuar con la página web de forma dinámica creando experiencias más ricas e interactivas para el usuario. JavaScript utiliza el DOM para hablar con la página web. Implantación de Aplicaciones Web 10

Es como si JS fuera un decorador con el plano de la casa (DOM) en la mano. Con ese plano puede:

**▸** Cambiar los muebles: modifica el contenido de la página, como el texto de un párrafo o una imagen.

**▸** Pintar las paredes: cambia los estilos de la página, como los colores, las fuentes o el tamaño de los elementos.

**▸** Abrir y cerrar puertas: responde a las acciones del usuario, como hacer que algo suceda cuando se hace clic en un botón o se pasa el ratón por encima de una imagen.

El DOM, para JavaScript, es:

**▸** Una representación de la página web: un modelo en forma de árbol de objetos que refleja la estructura del documento HTML.

**▸** Una interfaz de programación: es un conjunto de métodos y propiedades que JavaScript utiliza para interactuar con la página.

**▸** La clave para la interactividad: permite que JavaScript haga que las páginas web sean dinámicas y respondan a las acciones del usuario.

Mientras que el DOM se centra en el contenido de la página web, el BOM (Browser Object Model) se centra en el navegador web en sí. Piensa en el BOM como un conjunto de herramientas que JavaScript puede utilizar para interactuar con el navegador y hacer cosas que van más allá de la simple manipulación del contenido de la página.

¿Qué puede hacer JavaScript con el BOM?

**▸** Controlar la ventana del navegador: abrir nuevas ventanas, cerrar ventanas, cambiar el tamaño de la ventana, mover la ventana, etc.

**▸** Obtener información sobre el navegador: averiguar qué navegador está usando el usuario, qué versión del navegador, qué sistema operativo, etc. **▸** Manipular el historial de navegación: retroceder o avanzar en el historial o incluso redirigir al usuario a una página diferente. **▸** Trabajar con cookies: leer y escribir *cookies,* que son pequeños fragmentos de información que se almacenan en el ordenador del usuario. **▸** Acceder a la ubicación del usuario: con el permiso del usuario, JavaScript puede obtener la ubicación geográfica del usuario. **El objeto** window El objeto window es el objeto principal del BOM. Es como la raíz del BOM y todos los demás objetos son accesibles a través de él. Por ejemplo, para acceder al historial de navegación usarías window.history . Objetos importantes del BOM:

**▸** Navigator : proporciona información sobre el navegador web.

**▸** Screen : proporciona información sobre la pantalla del usuario.

**▸** Location : proporciona información sobre la URL actual.

**▸** History : permite acceder al historial de navegación.

**▸** Document : aunque técnicamente es parte del DOM, el objeto document también es

accesible a través del BOM, como window.document.

Ejemplo JavaScript:

// Mostrar una alerta con información del navegador alert("Estás usando " + navigator.userAgent);

// Redirigir al usuario a otra página window.location.href = "<https://www.ejemplo.com>";

El BOM es una parte importante de JavaScript, ya que permite a los desarrolladores web interactuar con el navegador web y crear experiencias más ricas y dinámicas para el usuario. Aunque no existe un estándar oficial para el BOM, la mayoría de los navegadores modernos implementan un conjunto similar de objetos y métodos.

# 8.4. Validación de formularios

La validación de formularios HTML con JavaScript te permite asegurar que la información ingresada por el usuario cumple con ciertos criterios antes de ser enviada al servidor. Esto no solo mejora la calidad de los datos, sino que también previene errores y ofrece una mejor experiencia de usuario.

¿Por qué usar JavaScript para validar formularios?

**▸ Retroalimentación inmediata:** JavaScript puede mostrar mensajes de error al usuario en tiempo real, sin necesidad de recargar la página.

**▸ Personalización:** puedes crear tus propias reglas de validación y mensajes de error para adaptarlas a las necesidades de tu formulario.

**▸ Mejor experiencia de usuario:** la validación del lado del cliente ayuda a prevenir errores frustrantes y guía al usuario para que ingrese la información correcta.

#### Pasos para la validación de un formulario

**▸** Capturar el evento submit : cuando el usuario envía el formulario se activa el evento submit . Debes usar JavaScript para capturar este evento y ejecutar tu código de validación.

**▸** Obtener los valores de los campos: utiliza JavaScript para acceder a los valores ingresados en los campos del formulario. Puedes usar métodos como

document.getElementById() o document.querySelector() para seleccionar los elementos

del formulario.

**▸** Aplicar las reglas de validación: define las reglas que deben cumplir los datos ingresados. Por ejemplo, puedes verificar que un campo no esté vacío, que tenga un formato de correo electrónico válido o que cumpla con un rango de valores.

**▸** Mostrar mensajes de error: si se encuentra un error, muestra un mensaje de error al usuario. Puedes usar elementos HTML como <span> o <div> para mostrar los mensajes o incluso usar alertas de JavaScript.

**▸** Prevenir el envío del formulario: si se encuentra algún error, debes prevenir que el formulario se envíe al servidor. Puedes usar event.preventDefault() para cancelar el envío del formulario.

Ejemplo HTML:

$$<form id="miFormulario" onsubmit="return validarFormulario()">$$

$$<label for="nombre">Nombre:</label>$$

$$<input type="text" id="nombre" name="nombre" required>$$

$$<span id="errorNombre"></span>$$

$$<button type="submit">Enviar</button>$$

</form>

<script>

function validarFormulario() { const nombre = document.getElementById("nombre").value; const errorNombre = document.getElementById("errorNombre");

$$if (nombre == "") \{$$

errorNombre.textContent = "Por favor ingresa tu nombre."; return false; // Prevenir el envío } else {

errorNombre.textContent = "";

return true; // Permitir el envío

}

}

</script>

#### Recomendaciones

**▸** Combina la validación del lado del cliente y del servidor: la validación del lado del cliente es importante para la experiencia del usuario, pero la validación del lado del servidor es esencial para la seguridad.

**▸** Utiliza HTML5 para la validación básica: HTML5 ofrece atributos como required , pattern y type="email" , que permiten realizar validaciones básicas sin JavaScript.

**▸** Usa bibliotecas de JavaScript: existen bibliotecas como jQuery Validate que facilitan la validación de formularios con JavaScript.

La validación de formularios con JavaScript es una técnica fundamental para crear aplicaciones web robustas y fáciles de usar. También podemos realizar la validación de formularios HTML con la etiqueta pattern ; expresiones regulares (regex) te permite definir reglas precisas sobre el formato de los datos que el usuario puede ingresar en un campo. Esto se hace directamente en el código HTML, sin necesidad de escribir JavaScript.

Pero, ¿cómo funciona?

**▸** Atributo pattern : dentro de la etiqueta <input> , puedes usar el atributo pattern para especificar una expresión regular.

**▸** Expresión regular: la expresión regular define el patrón que debe seguir el valor ingresado en el campo.

**▸** Validación automática: el navegador valida automáticamente el campo cuando el usuario intenta enviarlo. Si el valor no coincide con la expresión regular, el navegador mostrará un mensaje de error. Ejemplo de uso:

<form>

$$<label for="codigoPostal">Código Postal:</label>$$

$$<input type="text" id="codigoPostal" name="codigoPostal" pattern="[0-9]\{5\}" title="Por favor$$

ingresa un código postal de 5 dígitos.">

$$<button type="submit">Enviar</button>$$

</form>

En anterior ejemplo, el atributo pattern="[0-9]{5}" define una expresión regular que solo acepta cinco dígitos. Si el usuario ingresa algo que no cumple con este patrón, el navegador mostrará el mensaje «Por favor, ingresa un código postal de 5 dígitos».

Ventajas de validación con pattern y regex

**▸** Simplicidad: la validación se realiza directamente en el HTML, sin necesidad de escribir JavaScript.

**▸** Eficiencia: la validación se realiza en el navegador del cliente, lo que reduce la carga del servidor.

**▸** Flexibilidad: las expresiones regulares te permiten definir una amplia variedad de patrones de validación. **▸** Usabilidad: los mensajes de error predeterminados del navegador son generalmente claros y concisos. Ejemplos de expresiones regulares:

**▸** [a-zA-Z]+ : solo letras (mayúsculas y minúsculas).

**▸** [ 0-9]{3}-[0-9]{2}-[0-9]{4} : formato de número de teléfono (XXX-XX-XXXX).

**▸** \w+@\w+\.\w+: formato de correo electrónico básico.

#### Recomendaciones

- ▸ Usa el atributo title : proporciona un mensaje de error claro y conciso en el atributo

    - title para ayudar al usuario a corregir el error.

- ▸ Combina con JavaScript: puedes usar JavaScript para personalizar aún más la

    - validación y proporcionar una mejor experiencia de usuario.

- ▸ No confíes solo en la validación del cliente: recuerda que la validación del lado del

    - servidor es esencial para la seguridad de tu aplicación.

        - Implantación de Aplicaciones Web 18

# 8.5. Introducción de comportamientos dinámicos.

# Captura de eventos

JavaScript es la clave para crear comportamientos dinámicos en la web. A través de él puedes hacer que las páginas web respondan a las acciones del usuario, cambien su contenido y apariencia e incluso se comuniquen con el servidor sin necesidad de recargar la página. La captura de eventos es esencial para lograr esta interactividad.

¿Qué son los eventos?

Los eventos son acciones o sucesos que ocurren en la página web, como, por ejemplo:

**▸** Clics del ratón: cuando el usuario hace clic en un elemento.

**▸** Movimientos del ratón: cuando el usuario mueve el cursor sobre un elemento.

**▸** Pulsaciones de teclas: cuando el usuario presiona una tecla.

**▸** Envío de formularios: cuando el usuario envía un formulario.

**▸** Carga de la página: cuando la página web termina de cargar.

#### ¿Cómo capturar eventos con JavaScript?

**▸ Seleccionar el elemento:** primero debes seleccionar el elemento HTML al que quieres asociar el evento. Puedes usar métodos como document.getElementById() ,

document.querySelector() , etc.

**▸ Asociar el evento:** utiliza el método addEventListener() para asociar una función **(manejador de eventos)** al evento que quieres capturar.

Ejemplo de uso:

$$<button id="miBoton">Haz clic aquí</button>$$

<script> // Seleccionar el elemento let boton = document.getElementById("miBoton"); // Asociar el evento "click" boton.addEventListener("click", function() { alert("¡Has hecho clic en el botón!"); }); </script>

En este ejemplo, cuando el usuario hace clic en el botón, se ejecutará la función que muestra una alerta.

#### Tipos de eventos

Existen muchos tipos de eventos que puedes capturar con JavaScript. Algunos de los más comunes son:

**▸** onclick : clic del ratón.

**▸** onmouseover : el ratón entra en el área del elemento.

**▸** onmouseout : el ratón sale del área del elemento.

**▸** onsubmit : envío de un formulario.

**▸** onload : carga de la página o un recurso.

**▸** onkeydown : pulsación de una tecla.

#### Comportamientos dinámicos

La captura de eventos te permite crear una gran variedad de comportamientos dinámicos, como pueden ser:

**▸** Mostrar y ocultar contenido: puedes mostrar u ocultar elementos HTML en respuesta

a un evento. **▸** Cambiar el estilo de los elementos: puedes modificar el color, tamaño, posición, etc., de los elementos. **▸** Validar formularios: puedes verificar que la información ingresada por el usuario sea correcta. **▸** Enviar datos al servidor: puedes usar AJAX para enviar datos al servidor sin recargar la página. **▸** Crear animaciones: puedes crear animaciones y efectos visuales.

#### Ejemplo de dinamismo mediante eventos

Cambio de contenido:

$$<p id="miParrafo">Este es un párrafo.</p>$$

$$<button onclick="cambiarTexto()">Cambiar texto</button>$$

<script> function cambiarTexto() { document.getElementById("miParrafo").textContent = "¡El texto ha cambiado!";

}

</script>

CREACIÓN DE NUEVOS ELEMENTOS HTML

$$<ul id="miLista">$$

<li>Elemento 1</li> <li>Elemento 2</li> </ul>

$$<button onclick="agregarElemento()">Agregar elemento</button>$$

<script> function agregarElemento() { let nuevoElemento = document.createElement("li"); nuevoElemento.textContent = "Nuevo elemento"; document.getElementById("miLista").appendChild(nuevoElemento);

}

</script>

ELIMINAR CONTENIDO

$$<div id="miDiv">$$

<p>Este párrafo será eliminado.</p>

</div>

$$<button onclick="eliminarParrafo()">Eliminar párrafo</button>$$

<script>

function eliminarParrafo() { let parrafo = document.querySelector("#miDiv p"); parrafo.remove();

}

</script>

Modificación de estilos:

<div id="miDiv" style="background-color: blue;">Este div cambiará de color.</div>

$$<button onclick="cambiarColor()">Cambiar color</button>$$

<script>

function cambiarColor() { document.getElementById("miDiv").style.backgroundColor = "red";

}

</script>

Modificar tamaño de la fuente:

$$<p id="miParrafo">Este texto cambiará de tamaño.</p>$$

$$<button onclick="cambiarTamaño()">Cambiar tamaño</button>$$

<script>

function cambiarTamaño() { document.getElementById("miParrafo").style.fontSize = "24px";

}

</script>

Añadir una clase css:

<style>

.resaltado {

background-color: yellow; font-weight: bold;

}

</style>

$$<p id="miParrafo">Este texto será resaltado.</p>$$

$$<button onclick="resaltarTexto()">Resaltar texto</button>$$

<script>

function resaltarTexto() { document.getElementById("miParrafo").classList.add("resaltado");

}

</script>

Estos son solo algunos ejemplos básicos con JavaScript, las posibilidades de

modificar el contenido y los estilos de una página web son prácticamente ilimitadas. Otra funcionalidad importantísima que nos ofrece JS consiste en crear contenido de una web mediante la lectura de datos de un fichero JSON, para hacerlo seguiremos los siguientes pasos:

Obtener los datos del archivo JSON

**▸ Fetch:** la forma moderna de obtener datos de un archivo JSON es usar la API Fetch.

Esta API realiza una solicitud al archivo (que debe estar alojado en el servidor web para poder leerlo) y devuelve una promesa que se resuelve con la respuesta. Luego, puedes usar el método json() para analizar la respuesta como un objeto JavaScript.

fetch('datos.json')

$$.then(response => response.json())$$

$$.then(data => \{$$

// Procesar los datos JSON aquí console.log(data); }) .catch(error => console.error('Error al cargar el archivo JSON:', error));

**▸ XMLHttpRequest** (método antiguo): también puedes usar el objeto XMLHttpRequest para hacer la solicitud. Este método es más antiguo, pero aún funciona en todos los

Implantación de Aplicaciones Web 25 navegadores.

let xhr = new XMLHttpRequest(); xhr.open('GET', 'datos.json', true);

$$xhr.onload = function() \{$$

$$if (xhr.status === 200) \{$$

let data = JSON.parse(xhr.responseText); // Procesar los datos JSON aquí console.log(data); } }; xhr.send();

#### Procesar los datos JSON

Una vez que tengas los datos JSON como un objeto JavaScript puedes acceder a sus propiedades y usarlas para crear contenido HTML. Puedes usar métodos como

document.createElement() , textContent , appendChild() , etc., para crear y agregar

elementos a la página.

Imagina que tienes un archivo datos.json con la siguiente estructura:

[

{ "nombre": "Producto 1", "descripción": "Descripción del producto 1", "precio": 10 },

{ "nombre": "Producto 2", "descripción": "Descripción del producto 2", "precio": 20 }

]

Puedes usar el siguiente código JavaScript para leer los datos y crear una lista de productos en la página:

fetch('datos.json')

$$.then(response => response.json())$$

$$.then(productos => \{$$

const lista = document.getElementById('lista-productos');

$$productos.forEach(producto => \{$$

const elementoLista = document.createElement('li');

$$elementoLista.innerHTML = `$$

<h3>${producto.nombre}</h3> <p>${producto.descripcion}</p> <p>Precio: ${producto.precio} €</p> `; lista.appendChild(elementoLista); }); }) .catch(error => console.error('Error al cargar el archivo JSON:', error));

Y en tu HTML tendrías un elemento para mostrar la lista:

$$<ul id="lista-productos"></ul>$$

#### Recomendaciones

**▸** Formato del JSON: asegúrate de que el archivo JSON tenga un formato válido.

Puedes usar un validador de JSON *online* para comprobarlo.

**▸** Manejo de errores: implementa un manejo de errores adecuado para capturar cualquier problema al cargar o procesar el archivo JSON.

**▸** Seguridad: si los datos del JSON provienen de una fuente externa, asegúrate de que la fuente sea confiable y de que los datos estén sanitizados para evitar vulnerabilidades de seguridad.

**▸** Rendimiento: si el archivo JSON es muy grande, considera cargarlo de forma asíncrona para no bloquear la renderización de la página.

A continuación podrás ver otros ejemplos de cómo leer un fichero JSON, tanto si los datos están almacenados en una variable como si se encuentran en un archivo local, utilizando una función async con Fetch.

#### Datos JSON en una variable

En este ejemplo, los datos JSON se almacenan en la variable datosJSON . La función JSON.parse() convierte la cadena JSON en un objeto JavaScript.

$$const datosJSON = `$$

[

{ "nombre": "Producto 1", "precio": 10 },

{ "nombre": "Producto 2", "precio": 20 }

] `; async function leerJSONDesdeVariable() { try { const data = await JSON.parse(datosJSON); console.log("Datos JSON desde variable:", data); // Procesar los datos aquí, por ejemplo, mostrarlos en la página } catch (error) { console.error("Error al procesar los datos JSON:", error); } } leerJSONDesdeVariable();

#### Datos JSON en archivo local

En este caso, la función Fetch se utiliza para obtener los datos del archivo datos.json . El método response.json() analiza la respuesta como un objeto JavaScript.

async function leerJSONDesdeArchivo(rutaArchivo) { try { const response = await fetch(rutaArchivo); const data = await response.json(); console.log("Datos JSON desde archivo:", data);

// Procesar los datos aquí, por ejemplo, mostrarlos en la página } catch (error) { console.error("Error al cargar o procesar el archivo JSON:", error); } } leerJSONDesdeArchivo('datos.json');

#### Ventajas de usar async/await

**▸** Código más legible: el código es más fácil de leer y entender, ya que se parece más a la escritura síncrona. **▸** Manejo de errores más sencillo: El bloque try...catch permite manejar los errores de forma más clara y concisa. **▸** Mejor organización del código: facilita la escritura de código asíncrono que se ejecuta en secuencia. **▸** Recuerda que para que este código funcione correctamente, el archivo datos.json debe estar en la misma carpeta que tu archivo HTML, y ambos deben estar alojados en el servidor web y ejecutándose en él, para que pueda ser manipulado el contenido del fichero JSON.

# 8.6. Limitaciones y riesgos de ataques

JavaScript, a pesar de ser fundamental para la web moderna, tiene limitaciones inherentes y plantea desafíos de seguridad que los desarrolladores deben tener en cuenta. Estas son algunas de esas limitaciones:

**▸ Acceso limitado al sistema del cliente:** por razones de seguridad, JavaScript, que se ejecuta en el navegador, tiene un acceso muy limitado al sistema del usuario. No puede acceder a archivos del sistema, ejecutar programas arbitrariamente o controlar *hardware* como la webcam sin permiso explícito. JavaScript no puede leer el contenido del disco duro del usuario sin su consentimiento a través de un

elemento <input type="file"> .

**▸ Dependencia del navegador:** la ejecución de JavaScript puede variar ligeramente entre diferentes navegadores web. Esto puede causar problemas de compatibilidad y requerir que los desarrolladores escriban código específico para cada navegador o utilicen bibliotecas que manejen estas diferencias. El soporte para ciertas características de HTML5 o API puede variar entre navegadores, lo que obliga a realizar comprobaciones de compatibilidad.

**▸ Rendimiento:** aunque JavaScript es generalmente rápido, un código mal escrito o el uso excesivo de JavaScript puede afectar negativamente al rendimiento de la página web, especialmente en dispositivos móviles o con conexiones lentas. Animaciones complejas con JavaScript pueden consumir muchos recursos y ralentizar la página.

Seguridad

**▸** ***Cross-site scripting*** (XSS): es una vulnerabilidad que permite a atacantes inyectar código malicioso en una página web. Este código puede robar información del usuario, redirigirlo a sitios maliciosos o realizar acciones no deseadas en su nombre. Un atacante podría inyectar un *script* que robe las *cookies* del usuario cuando este introduce datos en un formulario.

**▸** La **inyección de código:** es similar al XSS. Esta vulnerabilidad ocurre cuando un atacante puede inyectar código que se ejecuta en el servidor, lo que puede permitirle acceder a bases de datos, modificar archivos o tomar el control del servidor. Si una aplicación web no sanitiza correctamente las entradas del usuario, un atacante podría inyectar código SQL malicioso en un formulario para acceder a la base de datos.

**▸ Acceso a información sensible:** JavaScript puede acceder a cierta información sensible del usuario, como *cookies,* historial de navegación o ubicación. Es importante que los desarrolladores manejen esta información con cuidado y solo la accedan cuando sea necesario y con el consentimiento del usuario. Una aplicación web que solicita la ubicación del usuario debe explicar por qué necesita esa información y obtener su permiso antes de acceder a ella.

#### Buenas prácticas de seguridad

**▸ Validar y sanitizar** las entradas del usuario: siempre valida y sanitiza las entradas del usuario en el lado del servidor para prevenir inyecciones de código.

**▸ Usar HTTPS:** HTTPS encripta la comunicación entre el navegador y el servidor, lo que dificulta que los atacantes puedan interceptar información sensible.

**▸ Implementar Content Security Policy** (CSP): CSP permite definir qué recursos externos puede cargar el navegador, lo que ayuda a prevenir ataques XSS.

**▸** Mantener **JavaScript actualizado:** las actualizaciones de JavaScript a menudo incluyen parches de seguridad que corrigen vulnerabilidades conocidas.

Los desarrolladores deben ser conscientes de las limitaciones y los desafíos de seguridad de JavaScript. Siguiendo las buenas prácticas y tomando medidas de seguridad adecuadas se pueden crear aplicaciones web más seguras y robustas.

# FreeCodeCamp. (s. f.). JavaScript Algorithms and Data Structures.

# [https://www.freecodecamp.org/learn](https://www.freecodecamp.org/learn)

# JavaScript Algorithms and Data Structures.

Ofrece un currículo interactivo gratuito para aprender desarrollo web, que incluye una sección completa sobre algoritmos y estructuras de datos en JavaScript. Esto es relevante para comprender la lógica detrás de la programación y para resolver problemas más complejos con JavaScript.

Implantación de Aplicaciones Web 33 Tema 8. A fondo

# W3Schools Online Web Tutorials. (s. f.). JavaScript Tutorial.

# [https://www.w3schools.com/js/](https://www.w3schools.com/js/)

# W3Schools Online Web Tutorials

Es otro sitio web popular con tutoriales y referencias sobre JavaScript y desarrollo web. Ofrece explicaciones claras, ejemplos interactivos y ejercicios para practicar. Es un recurso útil para aprender y comprender los conceptos básicos de JavaScript.

Implantación de Aplicaciones Web 34 Tema 8. A fondo

# Como crear un tema hijo

Flanagan, D. (2021). *JavaScript: The Definitive Guide.* O'Reilly Media.

Este libro es una referencia completa sobre JavaScript, que abarca desde los fundamentos hasta las características más avanzadas. Es útil para profundizar en la sintaxis del lenguaje, la manipulación del DOM, el manejo de eventos y otros conceptos clave que hemos mencionado.

Implantación de Aplicaciones Web 35 Tema 8. A fondo

# Entrenamiento 1

**▸ Planteamiento del ejercicio:** crea un formulario HTML con un campo para ingresar un número de teléfono con el formato XXX-XXX-XXX, donde X es un dígito. Utiliza el atributo pattern para validar el formato.

**▸ Desarrollo paso a paso:**

- Crear un formulario HTML con un campo de entrada de tipo " tel ".

- Añadir el atributo pattern al campo de entrada con la expresión regular que define el formato deseado.

- Añadir un atributo title para mostrar un mensaje de error si el formato no es válido.

**▸ Solución:**

<form>

$$<label for="telefono">Teléfono:</label>$$

$$<input type="tel" id="telefono" name="telefono" pattern="[0-9]\{3\}-[0-9]\{3\}-[0-9]\{3\}" title="Por favor,$$

introduce un número de teléfono con el formato XXX-XXX-XXX">

$$<button type="submit">Enviar</button>$$

</form>

# Entrenamiento 2

**▸ Planteamiento del ejercicio:** crea una página web con un párrafo y un botón. Al hacer clic en el botón, el texto del párrafo debe cambiar a «Hola Mundo!».

**▸ Desarrollo paso a paso:**

- Crear un párrafo con un texto inicial.

- Crear un botón.

- Añadir un evento clic al botón que ejecute una función JavaScript.

- En la función, usar document.getElementById() para seleccionar el párrafo y modificar su contenido con textContent .

**▸ Solución:**

$$<p id="miParrafo">Este texto cambiará.</p>$$

$$<button onclick="cambiarTexto()">Cambiar texto</button>$$

<script> function cambiarTexto() { document.getElementById("miParrafo").textContent = "Hola Mundo!"; }; </script>

# Entrenamiento 3

**▸ Planteamiento del ejercicio:** crea una página web que lea datos de un archivo JSON llamado datos.json y muestre los nombres de los productos en una lista. **▸ Desarrollo paso a paso:**

- Crear un archivo datos.json con una lista de productos (nombre, precio, etc.).

- Crear una lista vacía ( <ul> ) en el archivo HTML.

- Usar Fetch para leer el archivo datos.json .

- Recorrer los datos JSON y crear elementos de lista ( <li> ) con los nombres de los productos.

- Añadir los elementos de lista a la lista vacía.

**▸ Solución:**

$$<ul id="lista-productos"></ul>$$

<script>

fetch('datos.json')

$$.then(response => response.json())$$

$$.then(productos => \{$$

const lista = document.getElementById('lista-productos');

$$productos.forEach(producto => \{$$

const elementoLista = document.createElement('li'); elementoLista.textContent = producto.nombre;

lista.appendChild(elementoLista); }); }) .catch(error => console.error('Error al cargar el archivo JSON:', error)); </script>

# Entrenamiento 4

- ▸ Planteamiento del ejercicio: crea una página web con un cuadrado rojo. Cuando el

    - ratón pase por encima, el cuadrado debe cambiar de color a azul. Cuando el ratón

    - salga del cuadrado, debe volver a ser rojo.

- ▸ Desarrollo paso a paso:

- Crear un elemento div con un estilo CSS para que sea un cuadrado rojo.

- Añadir un evento mouseover al div que ejecute una función JavaScript.

- En la función, cambiar el color de fondo del div a azul.

- Añadir un evento mouseout al div que ejecute otra función JavaScript.

- En la segunda función, cambiar el color de fondo del div a rojo.

**▸ Solución:**

<div id="miCuadrado" style="width: 100px; height: 100px; background-color: red;"></div> <script> let cuadrado = document.getElementById("miCuadrado"); cuadrado.addEventListener("mouseover", function() { this.style.backgroundColor = "blue"; });

cuadrado.addEventListener("mouseout", function() { this.style.backgroundColor = "red"; }); </script>

# Entrenamiento 5

**▸ Planteamiento del ejercicio:** crea un formulario con un botón de envío. Utiliza JavaScript para prevenir el envío del formulario cuando se hace clic en el botón.

**▸ Desarrollo paso a paso:**

- Crear un formulario HTML con un botón de envío.

- Añadir un evento submit al formulario que ejecute una función JavaScript.

- En la función, usar event.preventDefault() para cancelar el envío del formulario.

**▸ Solución:**

$$<form onsubmit="prevenirEnvio(event)">$$

$$<button type="submit">Enviar</button>$$

</form>

<script> function prevenirEnvio(event) { event.preventDefault(); alert("Envío del formulario cancelado."); }; </script>

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.4–32)*
- Tema 8. Material de estudio  *(pp.4–32)*
- A fondo  *(pp.33–35)*
- Entrenamientos  *(pp.36–42)*
- Implantación de Aplicaciones Web 4 · Implantación de Aplicaciones Web 5 · Implantación de Aplicaciones Web 6 · Implantación de Aplicaciones Web 7 · Implantación de Aplicaciones Web 8 · Implantación de Aplicaciones Web 9 · Implantación de Aplicaciones Web 11 · Implantación de Aplicaciones Web 12 · Implantación de Aplicaciones Web 13 · Implantación de Aplicaciones Web 14 · Implantación de Aplicaciones Web 15 · Implantación de Aplicaciones Web 16 · Implantación de Aplicaciones Web 17 · Implantación de Aplicaciones Web 19 · Implantación de Aplicaciones Web 20 · Implantación de Aplicaciones Web 21 · Implantación de Aplicaciones Web 22 · Implantación de Aplicaciones Web 23 · Implantación de Aplicaciones Web 24 · Implantación de Aplicaciones Web 26 · Implantación de Aplicaciones Web 27 · Implantación de Aplicaciones Web 28 · Implantación de Aplicaciones Web 29 · Implantación de Aplicaciones Web 30 · Implantación de Aplicaciones Web 31 · Implantación de Aplicaciones Web 32  *(pp.4, 5, 6, 7, 8, 9, 11, 12, 13, 14, 15, 16, 17, 19, 20, 21, 22, 23, 24, 26, 27, 28, 29, 30, 31, 32)*
- Implantación de Aplicaciones Web 36 Tema 8. Entrenamientos · Implantación de Aplicaciones Web 37 Tema 8. Entrenamientos · Implantación de Aplicaciones Web 38 Tema 8. Entrenamientos · Implantación de Aplicaciones Web 39 Tema 8. Entrenamientos · Implantación de Aplicaciones Web 40 Tema 8. Entrenamientos · Implantación de Aplicaciones Web 41 Tema 8. Entrenamientos · Implantación de Aplicaciones Web 42 Tema 8. Entrenamientos  *(pp.36–42)*