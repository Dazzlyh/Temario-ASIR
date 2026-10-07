## Tema 9

# Implantación de Aplicaciones Web

# Tema 9. Programación de documentos web utilizando lenguajes de script de

# servidor

# Índice

Esquema Material de estudio

## 9.1. Introducción y objetivos

## 9.2. Clasificación

## 9.3. Integración con los lenguajes de marcas

## 9.4. Sintaxis

## 9.5. Herramientas de edición de código

## 9.6. Elementos del lenguaje estructurado

## 9.7. Elementos de orientación a objeto

## 9.8. Comentarios

## 9.9. Funciones integradas y de usuario

## 9.10. Gestión de errores

9.11. Mecanismos de introducción de información 9.12. Métodos de envío de datos desde el cliente al servidor

## 9.13. Autenticación de usuarios

## 9.14. Control de accesos

9.15. Sesiones. Mecanismos para mantener el estado entre conexiones

## 9.16. Configuración del intérprete

A fondo Documentación oficial de PHP PHP: the right way

W3Schools PHP Tutorial Entrenamientos

Entrenamiento 1

Entrenamiento 2

Entrenamiento 3

Entrenamiento 4

Entrenamiento 5

# Esquema

![image-1](images/image-1.png)

Implantación de Aplicaciones Web 4 Tema 9. Esquema

# 9.1. Introducción y objetivos

La web ha evolucionado de páginas estáticas a experiencias dinámicas e interactivas. Esta transformación ha sido impulsada en gran medida por la programación de documentos web utilizando lenguajes de *script* de servidor. Estos lenguajes, como PHP, Python, Ruby y Node.js, se ejecutan en el servidor, lo que permite generar contenido personalizado, procesar datos de formularios, interactuar con bases de datos y mucho más.

En este tema explicaremos el fascinante mundo de la programación del lado del servidor. Aprenderemos cómo funcionan estos lenguajes, cuáles son sus ventajas y cómo podemos utilizarlos para crear sitios web dinámicos y aplicaciones web complejas.

Al finalizar esta lección seremos capaces de: **▸** Comprender el rol de los lenguajes de *script* de servidor en el desarrollo web. **▸** Conocer las características principales de los lenguajes de *script* de los servidores más populares. **▸** Identificar las diferencias entre la programación del lado del cliente y del lado del servidor. **▸** Escribir código básico en un lenguaje de *script* de servidor. **▸** Crear páginas web dinámicas que interactúen con bases de datos. **▸** Implementar funciones comunes en aplicaciones web, como autenticación de usuarios y gestión de sesiones. **▸** Desarrollar una comprensión fundamental de los conceptos de seguridad en la programación del lado del servidor.

# 9.2. Clasificación

Los lenguajes de *script* de servidor se pueden clasificar de diversas maneras, dependiendo del criterio que utilicemos.

#### Clasificaciones comunes

#### Por paradigma de programación

**▸ Imperativos:** el código se ejecuta en secuencia, línea por línea.

- Ejemplos: PHP, Perl.

**▸ Orientados a objetos:** el código se organiza en torno a objetos que contienen datos y métodos.

- Ejemplos: Python, Ruby, Java (utilizado a través de JSP).

**▸ Funcionales:** se basan en la evaluación de funciones matemáticas.

- Ejemplos: Node.js (JavaScript del lado del servidor).

**▸ Multiparadigma:** permiten combinar diferentes paradigmas de programación.

- Ejemplos: Python, Ruby.

#### Por tipo de licencia

**▸** ***Open source:*** son de código abierto y se pueden utilizar, modificar y distribuir libremente.

- Ejemplos: PHP, Python, Ruby, Node.js.

**▸ Comerciales:** requieren una licencia para su uso.

- Ejemplos: ASP.NET (aunque existe una versión gratuita con funcionalidades limitadas).

#### Por popularidad y uso

**▸ PHP:** uno de los lenguajes más populares para el desarrollo web, especialmente en el ámbito de los sistemas de gestión de contenido (CMS), como WordPress.

**▸ Python:** un lenguaje versátil utilizado en diversas áreas, que incluye el desarrollo web, la ciencia de datos y la inteligencia artificial. *Frameworks* como Django y Flask son muy populares.

**▸ Node.js:** un entorno de ejecución de JavaScript que permite utilizar este lenguaje en el servidor. Es conocido por su eficiencia y escalabilidad.

**▸ Ruby:** un lenguaje elegante y expresivo que se utiliza a menudo con el *framework* Ruby on Rails.

**▸ Java (con JSP):** un lenguaje robusto y ampliamente utilizado en el desarrollo de aplicaciones empresariales. Java Server Pages (JSP) permite incrustar código Java en páginas web.

**▸ ASP.NET:** un *framework* de Microsoft para el desarrollo de aplicaciones web.

#### Por entorno de ejecución

**▸ Lenguajes interpretados:** el código se ejecuta línea por línea por un intérprete.

- Ejemplos: PHP, Python, Ruby.

**▸ Lenguajes compilados:** el código se compila a un lenguaje de máquina antes de su ejecución.

- Ejemplos: Java (aunque se ejecuta en una máquina virtual).

#### Por especialización

- ▸ Lenguajes de propósito general: se pueden utilizar para diversas tareas,

    - incluyendo el desarrollo web.

- Ejemplos: Python, Java.

**▸ Lenguajes específicos para el desarrollo web:** están diseñados específicamente para la creación de aplicaciones web.

- Ejemplos: PHP, Ruby on Rails.

Es importante tener en cuenta que estas clasificaciones no son excluyentes entre sí. Un lenguaje puede pertenecer a varias categorías al mismo tiempo. Es recomendable explorar los diferentes lenguajes y frameworks para descubrir cuál se adapta mejor a tus necesidades y preferencias.

# 9.3. Integración con los lenguajes de marcas

Vamos a utilizar PHP como lenguaje de servidor, analizaremos cómo se integra con los lenguajes de marcas (por ejemplo, HTML, XML y otros) de una manera fluida y eficiente. Esta integración es fundamental

para la creación de páginas web

dinámicas, donde el contenido se genera y se adapta en tiempo real en función de diferentes factores.

Cómo funciona esta integración

#### Código PHP en HTML

PHP se puede incrustar directamente en

un documento HTML utilizando las

etiquetas especiales <?php y ?> , esto permite combinar código HTML estático con código PHP dinámico. El servidor web procesa el código PHP y lo reemplaza con el resultado de su ejecución, que puede ser texto, HTML u otro tipo de contenido.

<!DOCTYPE html>

<html>

<head>

<title>Ejemplo de integración PHP</title> </head> <body>

<h1>Hola, <?php echo "mundo"; ?>!</h1> </body> </html>

En este ejemplo, el código PHP se ejecuta en el servidor y se reemplaza por la cadena " mundo " en la página web resultante.

#### Separación de la lógica y la presentación

Aunque PHP se puede incrustar directamente en HTML es recomendable separar la lógica de la aplicación de la presentación. Esto se puede lograr utilizando plantillas o *frameworks* que permiten definir la estructura HTML por separado del código PHP. Esta separación facilita el mantenimiento y la modificación del código, y permite a los diseñadores trabajar en la presentación sin tener que modificar la lógica.

#### Generación de contenido dinámico

**▸** PHP puede generar contenido dinámico en función de diferentes factores, como la información almacenada en una base de datos, las preferencias del usuario, la hora del día, etc.

**▸** Esto permite crear páginas web personalizadas que se adaptan a las necesidades de cada usuario.

<?php

$$$hora = date("H");$$

if ($hora < 12) {

echo "Buenos días";

} else if ($hora < 18) {

echo "Buenas tardes";

} else {

echo "Buenas noches";

}

?>

Este código PHP mostrará un saludo diferente en función de la hora del día.

#### Manipulación de formularios

PHP se utiliza a menudo para procesar datos de formularios HTML, puede recopilar la información enviada por el usuario, validarla, almacenarla en una base de datos y generar una respuesta adecuada.

#### Interacción con bases de datos

PHP proporciona funciones para conectarse a diferentes bases de datos, como MySQL, PostgreSQL y SQLite. Esto permite a los desarrolladores web crear aplicaciones que almacenan y recuperan información de manera eficiente.

#### Generación de contenido en diferentes formatos

Además de HTML, PHP puede generar contenido en otros formatos, como XML, JSON y CSV. Esto es útil para crear las API web y para intercambiar información con otras aplicaciones. La integración de PHP con los lenguajes de marcas es esencial para el desarrollo web moderno. Permite crear páginas web dinámicas, interactivas y personalizadas que se adaptan a las necesidades de cada usuario.

# 9.4. Sintaxis

Vamos a descubrir de la sintaxis básica y algunos de los comandos más importantes en PHP: **▸ Delimitadores:** el código PHP se incrusta en páginas web utilizando las siguientes etiquetas.

<?php // Aquí va el código PHP ?>

**▸ Variables:** las variables en PHP se declaran de forma implícita (con el dato que se almacena en ellas) con el símbolo $ seguido del nombre de la variable.

<?php

$$$nombre = "Juan";$$

$$$edad = 30;$$

?>

**▸ Tipos de datos:** PHP soporta varios tipos de datos, incluyendo enteros ( *int),* números de coma flotante *(float),* cadenas de texto *(string),* boolean *(bool), arrays* *(array),* objetos *(object)* y recursos *(resource).* **▸ Operadores:** PHP tiene una amplia variedad de operadores, incluyendo operadores aritméticos ( + , - , * , / ), operadores de comparación ( == , != , > , < ), operadores lógicos ( && , || , ! ) y operadores de asignación ( = , += , -= ). **▸ Salida de datos:** la función echo se utiliza para mostrar información en la página web.

<?php echo "Hola, mundo!"; ?>

**▸ Terminación de instrucciones:** las instrucciones en PHP terminan con un punto y coma ( ; ). Comandos PHP

echo - Imprime una o más cadenas de texto.

<?php echo "Hola, "; echo "mundo!"; ?> print - Similar a echo, pero solo imprime una cadena y siempre devuelve 1.

<?php print "Hola, mundo!"; ?> var_dump - Muestra información estructurada sobre una o más expresiones, incluyendo el tipo y valor. <?php

$$$variable = array(1, 2, 3);$$

var_dump($variable); ?> print_r - Imprime información legible para humanos sobre una variable. <?php

$$$variable = array(1, 2, 3);$$

print_r($variable); ?>

**▸ include/require:** incluyen y evalúan el código de otro archivo, include y require lo hace cada vez que se llama al archivo, y puede generar problemas de recarga, pero require_once solo carga una vez en cada recarga el archivo aunque haya varias peticiones.

<?php include 'mi_archivo.php'; ?>

**▸ Funciones:** bloques de código reutilizables que realizan una tarea específica.

<?php function saludar($nombre) { echo "Hola, " . $nombre . "!"; } saludar("Maria"); ?>

# 9.5. Herramientas de edición de código

A la hora de programar en PHP, contar con una buena herramienta de edición de código puede marcar la diferencia en tu productividad y eficiencia. Existen muchas opciones, desde simples editores de texto hasta IDE (entornos de desarrollo integrados) con funciones avanzadas. Aquí te presento algunas de las mejores herramientas para editar código PHP, clasificadas según tus necesidades:

Editores de texto

#### Visual studio code (VS Code)

**▸** Gratuito y de código abierto.

**▸** Ligero y rápido.

**▸** Extensible con una gran cantidad de *plugins* para PHP (resaltado de sintaxis,

autocompletado, *debugging,* etc.).

#### Sublime text

**▸** Rápido y con una interfaz minimalista.

**▸** Potente con muchas funciones para la edición de código.

**▸** Extensible mediante paquetes para PHP.

**▸** Versión de prueba gratuita, luego requiere licencia.

#### Atom

**▸** Desarrollado por GitHub.

**▸** Altamente personalizable y con una gran comunidad.

**▸** Muchos paquetes para PHP.

**▸** Gratuito y de código abierto.

#### Notepad++

**▸** Editor de código ligero y gratuito, exclusivo para Windows.

**▸** Resaltado de sintaxis para PHP y otros lenguajes.

**▸** Ideal para proyectos pequeños o para quienes buscan una opción sencilla.

**▸** IDE (entornos de desarrollo integrados).

#### PhpStorm

**▸** Desarrollado por JetBrains, es uno de los IDE más populares para PHP.

**▸** Ofrece un conjunto completo de herramientas: resaltado de sintaxis, autocompletado

inteligente, *debugging,* refactorización, análisis de código, integración con control de versiones, etc. **▸** Soporte para *frameworks* populares como Laravel, Symfony y WordPress. **▸** Versión de prueba gratuita, luego requiere licencia.

#### Netbeans

**▸** IDE gratuito y de código abierto con soporte para PHP.

**▸** Incluye herramientas para *debugging,* refactorización y pruebas unitarias.

**▸** Integración con *frameworks.*

#### Eclipse PDT (PHP development tools)

**▸** IDE gratuito y de código abierto basado en Eclipse.

**▸** Extensible mediante *plugins.*

**▸** Ofrece herramientas para desarrollo PHP, incluyendo *debugging,* refactorización y

pruebas.

#### Recomendaciones

**▸ Principiantes:** VS Code o Sublime Text son buenas opciones para empezar, ya que son fáciles de usar y configurar. **▸ Proyectos pequeños:** Notepad++ es una alternativa ligera y sencilla para proyectos pequeños. **▸ Proyectos grandes o profesionales:** PhpStorm ofrece un conjunto completo de herramientas que facilitan el desarrollo de aplicaciones complejas. **▸ Desarrollo con** ***frameworks:*** PhpStorm y NetBeans tienen buen soporte para *frameworks* populares como Laravel y Symfony. La mejor herramienta para tí dependerá de tus preferencias personales, tu nivel de experiencia y las necesidades de tu proyecto. Te recomiendo probar varias opciones y elegir la que mejor se adapte a tu flujo de trabajo.

# 9.6. Elementos del lenguaje estructurado

Los elementos de lenguaje estructurado en PHP son las construcciones básicas que te permiten controlar el flujo de ejecución de un programa y organizar el código de manera lógica y eficiente. Estos elementos son fundamentales para escribir programas robustos, legibles y fáciles de mantener. Ahora veremos los elementos clave para el control de flujo de programas del lenguaje estructurado en PHP:

Estructuras de control

#### Condicionales

Permiten ejecutar bloques de código sólo si se cumple una condición.

**▸** if : ejecuta un bloque de código si la condición es verdadera.

**▸** else : ejecuta un bloque de código si la condición del if es falsa.

**▸** elseif : permite evaluar múltiples condiciones de forma secuencial.

$$if ($edad >= 18) \{$$

echo "Eres mayor de edad."; } else { echo "Eres menor de edad."; }

#### Bucles

Permiten repetir un bloque de código varias veces. **▸** for : repite un bloque de código un número determinado de veces. **▸** while : repite un bloque de código mientras una condición sea verdadera. **▸** do-while : similar a while , pero el bloque de código se ejecuta al menos una vez. **▸** foreach : recorre los elementos de un *array.*

$$for ($i = 0; $i < 10; $i++) \{$$

echo $i . "<br>"; }

#### Sentencias de control

Permiten alterar el flujo de ejecución de un bucle. **▸** break : sale del bucle actual. **▸** continue : salta a la siguiente iteración del bucle. **▸** switch : permite ejecutar diferentes bloques de código según el valor de una variable.

switch ($dia) { case "lunes":

echo "Hoy es lunes."; break; case "martes":

echo "Hoy es martes.";

break; default:

echo "Hoy no es ni lunes ni martes."; }

#### Funciones

Son bloques de código que realizan una tarea específica, permiten modularizar el código haciéndolo más organizado y reutilizable. Se definen con la palabra clave function , pueden recibir parámetros y devolver valores.

function sumar($a, $b) { return $a + $b; }

$$$resultado = sumar(5, 3); // $resultado será igual a 8$$

#### Inclusión de archivos

**▸** include y require : permiten incluir el contenido de un archivo externo en el script actual.

**▸** include_once y require_once : aseguran que un archivo se incluya solo una vez, por ejecución o recarga del *script.*

#### Manejo de errores

PHP proporciona mecanismos para manejar errores, como excepciones y mensajes de error.

#### Beneficios de usar elementos de lenguaje estructurado

- ▸ Claridad y legibilidad: el código es más fácil de entender y seguir.

- ▸ Organización: el código se divide en bloques lógicos, lo que facilita su

    - mantenimiento.

- ▸ Reutilización: las funciones permiten reutilizar código en diferentes partes del

    - programa.

- ▸ Eficiencia: el código estructurado es más eficiente y fácil de depurar.

        - Implantación de Aplicaciones Web 22

# 9.7. Elementos de orientación a objeto

La programación orientada a objetos

(POO) es un paradigma que te permite

estructurar tu código en torno a " objetos ", que combinan datos (atributos) y acciones (métodos). PHP ofrece un conjunto completo de elementos para la POO, que te permiten crear aplicaciones más modulares, flexibles y fáciles de mantener. Estos son los elementos clave de la orientación a objetos en PHP:

Clases y objetos

#### Clase

Es una plantilla o modelo que define las características (atributos) y comportamientos

(métodos) de un objeto. Se define con la palabra clave class .

class Persona { // Atributos public $nombre; public $edad; // Método public function saludar() { echo "Hola, mi nombre es " . $this->nombre;

}

}

#### Objeto

Es una instancia de una clase. Se crea con la palabra clave new .

$persona1 = new Persona();

$persona1->nombre = "Juan";

$$$persona1->edad = 30;$$

$persona1->saludar(); // Output: "Hola, mi nombre es Juan"

#### Atributos

Son las variables que almacenan los datos del objeto y se definen dentro de la clase.

Pueden tener diferentes niveles de visibilidad:

**▸** public : accesible desde cualquier lugar.

**▸** protected : accesible desde la clase y sus subclases.

**▸** private : accesible solo desde la propia clase.

#### Métodos

Son las funciones que definen el comportamiento del objeto. Se definen dentro de la clase y pueden recibir parámetros y devolver valores.

$this: Variable especial que hace referencia al propio objeto.

#### Principios de la POO

**▸ Encapsulación:** agrupar datos y métodos en una unidad (la clase) y controlar el acceso a ellos mediante la visibilidad *(public, protected, private).*

**▸ Herencia:** crear nuevas clases (subclases) a partir de clases existentes (superclases) heredando sus atributos y métodos.

- Permite la reutilización de código y la creación de jerarquías de clases.

- Se usa la palabra clave extends.

**▸ Polimorfismo:** la capacidad de un objeto de tomar diferentes formas.

- Permite que objetos de diferentes clases respondan al mismo método de manera diferente.

- Se usa con la redefinición de métodos en las subclases.

**▸ Constructores y destructores.**

- Constructor: método especial que se ejecuta automáticamente al crear un objeto. Se usa para inicializar los atributos del objeto y se define con el nombre __construct() .

- Destructor: método especial que se ejecuta automáticamente al destruir un objeto. Se usa para liberar recursos o realizar tareas de limpieza y se define con el nombre __destruct() .

#### Otros elementos

**▸ Interfaces:** definen un conjunto de métodos que una clase debe implementar. **▸ Clases abstractas:** clases que no se pueden instanciar directamente, sirven como base para otras clases. **▸** ***Traits:*** mecanismo para reutilizar código entre clases sin usar herencia. **▸ Métodos mágicos:** métodos especiales con nombres predefinidos (como __get() , __set() , __toString() ) que permiten personalizar el comportamiento de los objetos. Ejemplo de herencia y polimorfismo:

class Animal { public function hacerSonido() { echo "Sonido genérico"; }

} class Perro extends Animal { public function hacerSonido() { echo "Guau!"; } } class Gato extends Animal { public function hacerSonido() { echo "Miau!"; }

}

$perro = new Perro();

$$$gato = new Gato();$$

$perro->hacerSonido(); // Output: "Guau!"

$gato->hacerSonido(); // Output: "Miau!"

En el ejemplo, Perro y G a t o heredan

de Animal pero redefinen el método

hacerSonido() para que se comporte de manera diferente. Utilizar la orientación a objetos en PHP te permite escribir código

más modular, reutilizable y fácil de

mantener. Te recomiendo estudiar estos elementos y practicar su aplicación en tus proyectos.

# 9.8. Comentarios

Los comentarios en PHP son líneas de código que el intérprete ignora. Sirven para documentar y explicar el código, lo que facilita su comprensión y mantenimiento, tanto para ti como para otros desarrolladores. PHP ofrece dos formas principales de añadir comentarios:

**▸ Comentarios de una línea.**

- Se utilizan para comentarios cortos que ocupan una sola línea.

- Se inician con // o #.

// Este es un comentario de una línea

$edad = 30; # También es un comentario de una línea

#### ▸ Comentarios multilínea

- Se utilizan para comentarios más extensos que ocupan varias líneas.

- Se inician con /* y se cierran con */ .

/*

Este es un comentario

multilínea que puede ocupar varias líneas. */

Buenas prácticas al usar comentarios

**▸ Claridad y concisión:** escribe comentarios claros y concisos que expliquen el propósito del código. **▸ Actualización:** mantener los comentarios actualizados cuando modifiques el código. **▸ No redundantes:** evitar comentarios que simplemente repiten lo que ya es evidente en el código. **▸ Documentación de funciones:** documenta las funciones con comentarios que expliquen sus parámetros, valores de retorno y funcionalidad. **▸ Comentarios para depuración:** puedes usar comentarios para comentar temporalmente partes del código durante la depuración.

#### Ejemplos de uso de comentarios

Explicar la lógica del código:

// Calcular el área de un triángulo

$$$base = 10;$$

$$$altura = 5;$$

$area = ($base * $altura) / 2; // Fórmula del área de un triángulo

Documentar una función

/*

Calcula la suma de dos números.

@param int $a El primer número.

@param int $b El segundo número.

@return int La suma de los dos números.

*/

function sumar($a, $b) { return $a + $b; }

Comentar código para depuración:

// echo "Valor de x: " . $x; // Comentar esta línea para depuración

Usar comentarios de forma efectiva es una práctica esencial para escribir código PHP de calidad. Te ayudará a crear código más legible, mantenible y comprensible para ti y para otros desarrolladores.

# 9.9. Funciones integradas y de usuario

Las funciones son bloques de código que realizan una tarea específica. Puedes usarlas para organizar tu código, hacerlo más reutilizable y evitar la repetición. PHP ofrece dos tipos de funciones:

Funciones integradas (built-in)

Son funciones que ya están incluidas en el lenguaje PHP y proporcionan una amplia gama de funcionalidades para tareas comunes, como:

**▸** Manipulación de cadenas de texto ( strlen , strpos , substr ) **▸** Operaciones con arrays ( array_push , array_pop , sort ) **▸** Operaciones matemáticas ( abs , sqrt , round ) **▸** Manejo de fechas y horas ( date , strtotime ) **▸** Acceso a archivos ( fopen , fread , fclose ) Y muchas más... Puedes consultar la documentación oficial de PHP para obtener una lista completa de las funciones integradas y su uso.

$texto = "Hola mundo"; $longitud = strlen($texto); // $longitud será igual a 10 echo $longitud;

Funciones de usuario (user-defined)

**▸** Son funciones que creas tú mismo para realizar tareas específicas en tu aplicación.

**▸** Se definen con la palabra clave function , seguida del nombre de la función, paréntesis para los parámetros (si los hay) y llaves para el bloque de código.

function nombre_funcion($parametro1, $parametro2, ...) { // Bloque de código return $valor; // Opcional: devolver un valor } function calcular_area_rectangulo($base, $altura) {

$$$area = $base * $altura;$$

return $area; }

$$$base = 5;$$

$$$altura = 10;$$

$area = calcular_area_rectangulo($base, $altura); echo "El área del rectángulo es: " . $area; // Output: "El área del rectángulo es: 50"

Ventajas de usar funciones

**▸ Modularidad:** dividen el código en bloques lógicos, lo que facilita su organización y comprensión.

**▸ Reutilización:** puedes usar la misma función varias veces en tu código, para evitar la repetición.

**▸ Mantenimiento:** si necesitas modificar la funcionalidad, solo tienes que cambiar la función en un lugar.

**▸ Abstracción:** ocultan la complejidad de la implementación, esto permite que te centres en la lógica de la aplicación.

Tanto las funciones integradas como las de usuario son herramientas esenciales en PHP. Te recomiendo explorar las funciones integradas disponibles y aprender a crear tus propias funciones para desarrollar aplicaciones eficientes y bien estructuradas.

# 9.10. Gestión de errores

La gestión de errores en PHP es crucial para crear aplicaciones web robustas y fiables. Te permite controlar cómo responde tu aplicación ante situaciones inesperadas, como errores de código, problemas de conexión a la base de datos o archivos no encontrados. Vamos a presentar las principales herramientas y técnicas para gestionar errores en PHP.

Mostrar errores

#### Configuración de PHP

Puedes configurar PHP para que muestre los errores en pantalla. Esto es útil durante el desarrollo, pero no se recomienda en producción por motivos de seguridad.

**▸** Modifica el archivo php.ini :

- display_errors = On (para mostrar errores).

- error_reporting = E_ALL (para mostrar todos los tipos de errores).

**▸** O usa funciones en tu código:

- ini_set('display_errors', 1) ;

- error_reporting(E_ALL) ;

#### Tipos de errores

PHP tiene diferentes niveles de errores:

**▸** E_ERROR : errores fatales que detienen la ejecución del script.

**▸** E_WARNING : advertencias que no detienen la ejecución.

**▸** E_NOTICE : avisos de posibles errores o código no óptimo.

**▸** E_PARSE : errores de sintaxis. **▸** Puedes usar error_reporting() para controlar qué tipos de errores se muestran.

#### Manejadores de errores personalizados

**▸** Puedes crear tus propias funciones para manejar errores. **▸** Usa la función set_error_handler() para registrar tu función de manejo de errores. **▸** Tu función recibirá información sobre el error, como el tipo de error, el mensaje y la línea de código.

function miManejadorDeErrores($errno, $errstr, $errfile, $errline) { echo "<b>Error:</b> [$errno] $errstr<br>"; echo "Línea: $errline en el archivo $errfile<br>"; // Puedes registrar el error en un archivo o base de datos } set_error_handler("miManejadorDeErrores"); // Ejemplo de código que genera un error

$$$x = 5 / 0;$$

#### Excepciones

Las excepciones son un mecanismo para manejar errores de forma estructurada. Se usan con las palabras clave try , catch y finally . **▸** try : bloque de código donde se espera que pueda ocurrir una excepción. **▸** catch : bloque de código que se ejecuta si se lanza una excepción en el bloque try.

**▸** finally : bloque de código que se ejecuta siempre, independientemente de si se lanzó o no una excepción.

try { // Código que puede lanzar una excepción

$$$resultado = 5 / 0;$$

} catch (DivisionByZeroError $e) { echo "Error: División por cero. " . $e->getMessage(); } finally { echo "Este código se ejecuta siempre."; }

#### Otras técnicas

**▸** Validación de datos: valida la entrada del usuario para prevenir errores.

**▸** Depuración *(debugging):* usa un depurador para identificar y corregir errores en tu código.

**▸** Registro de errores *(logging):* registra los errores en un archivo o base de datos para su posterior análisis.

#### Recomendaciones

- ▸ No uses @ para suprimir errores: el operador @ oculta los errores, lo que

    - dificulta la depuración.

- ▸ Maneja los errores de forma específica: no uses un manejador genérico para

    - todos los errores.

- ▸ Proporciona información útil al usuario: no muestres mensajes de error técnicos

    - al usuario final.

- ▸ Registra los errores importantes: registra los errores que pueden afectar la

    - funcionalidad de la aplicación.

        - Implantación de Aplicaciones Web 37

# 9.11. Mecanismos de introducción de información

PHP ofrece un conjunto de funciones para la gestión de archivos, lo que te permite crear, leer, escribir y manipular archivos en el servidor. Esto es útil para diversas tareas, como almacenar datos, generar informes, procesar imágenes y mucho más.

Vamos a ver cómo crear y leer archivos con PHP.

Creación de archivos

#### fopen() -

Esta función abre un archivo o lo crea si no existe.

**▸** Recibe dos parámetros: la ruta del archivo y el modo de apertura.

**▸** Modos de apertura comunes:

- 'w' : escritura (crea un nuevo archivo o sobreescribe uno existente).

- 'a' : añadir (añade datos al final del archivo).

- 'x' : crear (crea un nuevo archivo, falla si ya existe).

#### fwrite() –

Esta función escribe datos en un archivo abierto, recibe dos parámetros, el puntero al archivo (obtenido con fopen() ) y los datos a escribir.

#### fclose()

Esta función cierra un archivo abierto para que se confirmen realmente las acciones realizadas.

// Crear un archivo llamado "mi_archivo.txt" $archivo = fopen("mi_archivo.txt", "w");

// Escribir en el archivo fwrite($archivo, "Hola mundo!"); // Cerrar el archivo fclose($archivo);

Lectura de archivos

**▸** fopen() : abre el archivo en modo lectura ('r').

**▸** fread() : lee el contenido completo del archivo, recibe dos parámetros, el puntero al archivo y el tamaño máximo de bytes a leer.

**▸** fgets() : lee una sola línea del archivo.

**▸** feof() : comprueba si se ha llegado al final del archivo.

**▸** fclose() : cierra el archivo.

// Abrir el archivo "mi_archivo.txt" en modo lectura

$archivo = fopen("mi_archivo.txt", "r");

// Leer el contenido completo del archivo

$contenido = fread($archivo, filesize("mi_archivo.txt"));

// Mostrar el contenido

echo $contenido; // Output: "Hola mundo!" // Cerrar el archivo fclose($archivo);

Otras funciones útiles

**▸** file_exists() : comprueba si un archivo existe.

**▸** unlink() : elimina un archivo.

**▸** rename() : cambia el nombre de un archivo.

**▸** copy() : copia un archivo.

**▸** is_writable() : comprueba si un archivo tiene permisos de escritura.

**▸** file_get_contents() : lee el contenido completo de un archivo en una cadena.

**▸** file_put_contents() : escribe una cadena en un archivo.

Recomendaciones

**▸ Manejo de errores:** usa *try-catch* o verifica el valor de retorno de fopen() para

manejar posibles errores al abrir o escribir en un archivo. **▸ Permisos de archivos:** asegúrate de que el *script* PHP tiene los permisos necesarios para crear, leer o escribir en los archivos. **▸ Cierre de archivos:** siempre cierra los archivos con fclose() después de usarlos para liberar recursos. **▸ Seguridad:** ten cuidado al manejar archivos, especialmente si la información proviene del usuario, para evitar vulnerabilidades de seguridad.

# 9.12. Métodos de envío de datos desde el cliente

# al servidor

En PHP, los dos métodos principales para enviar datos desde el cliente (navegador web) al servidor son GET y POST. Ambos métodos se utilizan para enviar datos a través de formularios HTML, pero difieren en cómo se transmiten esos datos.

Método GET

**▸ Transmisión:** los datos se añaden a la URL como parámetros, visibles en la barra de direcciones del navegador.

**▸ Formato.**

$$• nombre\_pagina.php?variable1=valor1&variable2=valor2…$$

**•** <https://www.ejemplo.com/pagina.php?nombre=Juan&edad=30>.

**▸ Limitaciones.**

- La longitud de la URL es limitada, por lo que no se pueden enviar grandes cantidades de datos.

- No es adecuado para datos sensibles, ya que son visibles en la URL.

**▸ Usos comunes.**

- Búsquedas en sitios web.

- Paginación.

- Filtrado de resultados.

$$<form method="get" action="procesar.php">$$

$$<input type="text" name="nombre" placeholder="Nombre">$$

$$<input type="submit" value="Enviar">$$

</form>

Al enviar el formulario, la URL sería algo como: procesar.php?nombre=Juan

Método POST

**▸ Transmisión:** los datos se envían en el cuerpo de la petición HTTP, no son visibles en la URL.

**▸ Limitaciones:** no hay límite de tamaño para los datos enviados.

**▸ Usos comunes.**

- Envío de formularios con información sensible (contraseñas, datos personales).

- Subida de archivos.

- Envío de grandes cantidades de datos.

$$<form method="post" action="procesar.php">$$

$$<input type="password" name="clave" placeholder="Contraseña">$$

$$<input type="submit" value="Enviar">$$

</form>

Al enviar este formulario, la contraseña no se mostrará en la URL.

#### ¿Cómo acceder a los datos en PHP?

**▸** $_GET : *array* asociativo que contiene los datos enviados mediante GET. **▸** $_POST : *array* asociativo que contiene los datos enviados mediante POST. **▸** $_REQUEST : *array* asociativo que contiene los datos de $_GET , $_POST $_COOKIE .

// Acceder al nombre enviado por GET

$$$nombre = $\_GET["nombre"];$$

// Acceder a la contraseña enviada por POST

$$$clave = $\_POST["clave"];$$

#### Recomendaciones

- ▸ Usar POST para datos sensibles: siempre usa POST para enviar contraseñas,

    - información personal o cualquier dato que no deba ser visible en la URL.

- ▸ Validar los datos: siempre valida los datos recibidos del cliente para evitar

    - problemas de seguridad y errores en tu aplicación.

- ▸ Elegir el método adecuado: considera las limitaciones y usos comunes de cada

    - método para elegir el más adecuado para tu aplicación.

        - Implantación de Aplicaciones Web 43

# 9.13. Autenticación de usuarios

La autenticación de usuarios y el control de accesos son aspectos cruciales en el desarrollo de aplicaciones web con PHP. Permiten verificar la identidad de los usuarios y restringir el acceso a ciertas partes de tu aplicación según sus roles o permisos. Vamos a ver los pasos básicos para implementar la autenticación y el control de accesos en PHP:

Crear una base de datos de usuarios

**▸** Necesitas una base de datos para almacenar la información de los usuarios, como nombre de usuario, contraseña (hasheada), correo electrónico y roles o permisos.

**▸** Puedes usar MySQL, PostgreSQL o cualquier otro sistema de gestión de bases de datos (DBMS) compatible con PHP.

![Ejemplo de tabla de usuarios:](images/image-2.png)

Tabla 1. Campos tabla usuarios Fuente: elaboración propia

Crear un formulario de inicio de sesión

**▸** Crea un formulario HTML con campos para el nombre de usuario y la clave. **▸** Usa el método POST para enviar los datos al servidor de forma segura.

$$<form method="post" action="login.php">$$

$$<label for="nombre\_usuario">Nombre de usuario:</label>$$

$$<input type="text" name="nombre\_usuario" id="nombre\_usuario">$$

<br>

$$<label for="clave">Contraseña:</label>$$

$$<input type="password" name="clave" id="clave">$$

<br>

$$<input type="submit" value="Iniciar sesión">$$

</form>

Procesar el formulario de inicio de sesión

**▸** En el archivo login.php , recibe los datos del formulario mediante $_POST .

**▸** Conéctate a la base de datos y busca al usuario por su nombre de usuario.

**▸** Verifica si la contraseña ingresada coincide con la contraseña hasheada almacenada en la base de datos. Usa funciones como password_hash() y password_verify() para esto.

**▸** Si la autenticación es exitosa inicia una sesión y guarda la información del usuario en

variables de sesión ($_SESSION['usuario_id'], $_SESSION['rol']) .

// código para conectar a la base de datos

$nombre_usuario = $_POST["nombre_usuario"];

$$$clave = $\_POST["clave"];$$

// Buscar al usuario en la base de datos

$sql = "SELECT * FROM usuarios WHERE nombre_usuario = '$nombre_usuario'";

$resultado = $conexion->query($sql);

if ($resultado->num_rows > 0) { $usuario = $resultado->fetch_assoc(); // Verificar la contraseña if (password_verify($clave, $usuario["clave"])) {

// Autenticación exitosa session_start(); $_SESSION["usuario_id"] = $usuario["id"];

$$$\_SESSION["rol"] = $usuario["rol"];$$

// Redirigir al usuario a la página principal o a una página protegida header("Location: index.php"); } else { // Contraseña incorrecta echo "Contraseña incorrecta."; } } else { // Usuario no encontrado echo "Usuario no encontrado."; }

Implementar el control de accesos

**▸** En las páginas que requieren autenticación, verifica si el usuario ha iniciado sesión.

**▸** Puedes usar una función para verificar la sesión y redirigir al usuario a la página de inicio de sesión si no está autenticado.

function verificar_sesion() { session_start(); if (!isset($_SESSION["usuario_id"])) {

header("Location: login.php"); exit(); } } // En una página protegida: verificar_sesion(); // código de la página protegida

Control de acceso basado en roles

**▸** Puedes asignar roles a los usuarios (administrador, editor, usuario) y restringir el acceso a ciertas funcionalidades según su rol.

**▸** Verifica el rol del usuario en la variable de sesión $_SESSION['rol'] antes de mostrar o procesar información sensible.

verificar_sesion();

$$if ($\_SESSION["rol"] == "administrador") \{$$

// Mostrar opciones de administración

}

Recomendaciones

**▸ Usa contraseñas hasheadas:** nunca almacenes contraseñas en texto plano. **▸ Implementa un mecanismo para recuperar contraseñas:** permite a los usuarios recuperar sus contraseñas en caso de olvido. **▸ Usa sesiones seguras:** configura las opciones de sesión para prevenir ataques como la fijación de sesión *(session fixation).* **▸ Considera usar un** ***framework:*** los *frameworks* como Laravel y Symfony ofrecen herramientas y bibliotecas para facilitar la autenticación y el control de accesos.

# 9.14. Control de accesos

El control de accesos en PHP es fundamental para proteger tu aplicación web y asegurar que solo los usuarios autorizados puedan acceder a ciertas partes o funcionalidades. Implica verificar la identidad del usuario y luego determinar si tiene los permisos necesarios para realizar una acción o acceder a un recurso específico. Veamos los elementos clave para implementar el control de accesos:

Autenticación

**▸ Identificación del usuario:** el primer paso es identificar al usuario. Esto generalmente se hace a través de un formulario de inicio de sesión donde el usuario proporciona sus credenciales (nombre de usuario y contraseña).

**▸ Verificación de credenciales:** debes comparar las credenciales proporcionadas con las almacenadas de forma segura en tu base de datos (usualmente utilizando un *hash).*

**▸ Sesiones:** una vez que el usuario se autentica puedes usar sesiones para mantener su estado de autenticación en diferentes páginas de tu aplicación.

Autorización

**▸ Roles y permisos:** definir roles de usuario (administrador, editor, usuario) y asignar permisos específicos a cada rol. Esto te permite controlar qué acciones puede realizar cada tipo de usuario.

**▸ Verificación de permisos:** antes de permitir que un usuario acceda a un recurso o realice una acción, verifica si su rol tiene los permisos necesarios. Puedes usar estructuras condicionales (if) o funciones para esto.

Implementación

**▸ Páginas protegidas:** para las páginas que requieren autenticación, verifica si el usuario ha iniciado sesión al principio del script. Si no lo ha hecho, redirige al usuario a la página de inicio de sesión.

**▸ Control granular:** puedes implementar un control de acceso más granular verificando los permisos del usuario para acciones específicas, como crear, leer, actualizar o eliminar datos.

**▸ Jerarquía de roles:** puedes crear una jerarquía de roles donde algunos roles heredan permisos de otros.

// Verificar si el usuario ha iniciado sesión session_start(); if (!isset($_SESSION["usuario_id"])) { header("Location: login.php"); exit(); } // Verificar si el usuario tiene permiso para editar

$$if ($\_SESSION["rol"] == "administrador" || $\_SESSION["rol"] == "editor") \{$$

// Mostrar el formulario de edición } else { // Mostrar un mensaje de error o redirigir a otra página }

Herramientas y técnicas

**▸** Bases de datos: Almacena la información de usuarios, roles y permisos en una base de datos.

**▸** Sesiones: Utiliza sesiones para mantener el estado de autenticación del usuario.

**▸** Funciones: Crea funciones para verificar la autenticación y los permisos del usuario.

**▸** Frameworks: Frameworks como Laravel y Symfony ofrecen herramientas y bibliotecas que facilitan la implementación del control de accesos.

**▸** Middleware: En frameworks como Laravel, puedes usar middleware para filtrar las peticiones HTTP y verificar la autenticación y autorización antes de que lleguen a los controladores.

Recomendaciones

**▸ Principio de mínimo privilegio:** otorga a los usuarios solo los permisos necesarios para realizar sus tareas.

**▸ Validación de datos:** valida la entrada del usuario para evitar vulnerabilidades de seguridad.

**▸ Protección contra ataques:** implementa medidas de seguridad para proteger tu aplicación contra ataques como la inyección SQL y la falsificación de solicitudes entre sitios (CSRF).

Implementar un control de accesos robusto permite proteger tus datos y garantizar que solo los usuarios autorizados puedan acceder a la información y realizar acciones específicas. Implica verificar la identidad del usuario y luego determinar si tiene los permisos necesarios para realizar las acciones autorizadas en las vistas concedidas.

# 9.15. Sesiones. Mecanismos para mantener el

# estado entre conexiones

Las sesiones y las *cookies* son mecanismos utilizados en PHP (y en otros lenguajes de programación web) para almacenar información sobre los usuarios que visitan un sitio web. Permiten que el sitio web recuerde información sobre el usuario a medida que navega por diferentes páginas o incluso en visitas posteriores.

Cookies

**▸ Almacenamiento:** las cookies son pequeños archivos de texto que se almacenan en el ordenador del cliente (el navegador web).

**▸ Duración:** pueden ser persistentes (se almacenan en el disco duro) o de sesión (se eliminan al cerrar el navegador).

**▸ Acceso:** se acceden mediante la variable superglobal $_COOKIE en PHP.

**▸ Usos comunes.**

- Almacenar preferencias del usuario (idioma, tema).

- Recordar el estado del carrito de compras.

- Rastrear la actividad del usuario para análisis web o publicidad.

// Establecer una cookie setcookie("nombre_usuario", "Juan", time() + (86400 * 30), "/"); // Expira en 30 días // Acceder a una cookie if(isset($_COOKIE["nombre_usuario"])) { echo "Hola " . $_COOKIE["nombre_usuario"]; }

Sesiones

**▸ Almacenamiento:** las sesiones almacenan datos en el servidor, asociadas a un usuario específico mediante un ID de sesión único.

**▸ Duración:** generalmente expiran después de un período de inactividad o al cerrar el navegador.

**▸ Acceso:** se acceden mediante la variable superglobal $_SESSION en PHP.

**▸ Usos comunes.**

- Autenticación de usuarios (mantener al usuario conectado).

- Almacenar información temporal del usuario (datos del formulario, preferencias de sesión).

- Controlar el acceso a ciertas partes del sitio web.

// Iniciar una sesión session_start(); // Almacenar datos en la sesión $_SESSION["nombre_usuario"] = "Juan";

![// Acceder a datos de la sesión echo "Hola " . $_SESSION"nombre_usuario";](images/image-3.png)

Tabla 2. Características *cookies* y sesiones. Fuente: elaboración propia.

Recomendaciones

**▸ Seguridad:** no almacenes información sensible (como contraseñas) en *cookies.*

**▸ Privacidad:** informa a los usuarios sobre el uso de *cookies* y sesiones en tu sitio web.

**▸ Configuración:** puedes configurar las opciones de *cookies* y sesiones en el archivo

php.ini o mediante funciones como session_set_cookie_params() .

Las sesiones y las *cookies* son herramientas esenciales para el desarrollo web con PHP. Permiten crear sitios web más interactivos, personalizados y seguros.

# 9.16. Configuración del intérprete

La configuración del intérprete de PHP se realiza principalmente a través del archivo php.ini . Este archivo contiene directivas que controlan diversos aspectos del comportamiento de PHP, como el manejo de errores, la seguridad, el rendimiento y las extensiones.

Cómo configurar el intérprete de PHP

#### Localizar el archivo php.ini

**▸** La ubicación del archivo php.ini puede variar según el sistema operativo y la instalación de PHP.

**▸** Puedes usar la función phpinfo() para encontrar la ruta del archivo php.ini cargado.

**▸** En sistemas Linux suele estar en «/etc/php/» o «/usr/local/etc/php/».

**▸** En Windows, suele estar en la carpeta de instalación de PHP (C:\php).

#### Editar el archivo

Abre el archivo php.ini con un editor de texto y modifica las directivas según tus necesidades. Tras esto guardaremos los cambios y reiniciamos el servidor web para que los cambios surtan efecto.

#### Directivas importantes

**▸** error_reporting : controla qué tipos de errores se reportan.

- E_ALL : reportar todos los errores (recomendado para desarrollo).

- E_ALL & ~E_NOTICE : reportar todos los errores excepto notices .

**▸** display_errors : controla si los errores se muestran en pantalla.

- On : mostrar errores (recomendado para desarrollo).

- Off : no mostrar errores (recomendado para producción).

**▸** log_errors : controla si los errores se registran en un archivo.

- On : registrar errores.

- Off : no registrar errores.

**▸** error_log : especifica la ruta del archivo de registro de errores.

- upload_max_filesize : define el tamaño máximo de archivo permitido para subir.

- post_max_size : define el tamaño máximo de datos permitidos en una petición POST.

- memory_limit : define la cantidad máxima de memoria que un script PHP puede usar.

- max_execution_time : define el tiempo máximo de ejecución de un script PHP.

- date.timezone : define la zona horaria predeterminada.

Ini, TOML

; Mostrar todos los errores

$$error\_reporting = E\_ALL$$

; Mostrar errores en pantalla

$$display\_errors = On$$

; Registrar errores en un archivo

$$log\_errors = On$$

$$error\_log = /var/log/php\_errors.log$$

; Aumentar el límite de memoria

$$memory\_limit = 256M$$

#### Otras formas de configuración

**▸** .htaccess : puedes usar el archivo .htaccess para modificar la configuración de PHP para un directorio específico. **▸** ini_set() : puedes usar la función ini_set() en tu código PHP para modificar la configuración en tiempo de ejecución.

#### Recomendaciones

**▸** Crea una copia de seguridad del archivo

php.ini antes de modificarlo.

**▸** Comenta los cambios que realices para facilitar el mantenimiento.

**▸** Reinicia el servidor web después de realizar cambios en php.ini .

**▸** Consulta la documentación oficial de PHP para obtener información detallada sobre

las directivas.

Configurar correctamente el intérprete de PHP es esencial para el buen funcionamiento y la seguridad de tus aplicaciones web.

# Documentación oficial de PHP

The PHP Group. (s. f.). *Manual de PHP.* [https://www.php.net/manual/es/](https://www.php.net/manual/es/)

La documentación oficial es la fuente más completa y actualizada de información sobre PHP. Contiene la descripción detallada de todas las funciones, clases, extensiones y directivas de configuración, con ejemplos y explicaciones. Es fundamental para comprender a fondo cualquier aspecto del lenguaje y resolver dudas.

Implantación de Aplicaciones Web 59 Tema 9. A fondo

# PHP: the right way

Página web de PHP: the right way ([https://phptherightway.com/](https://phptherightway.com/)).

Este recurso *online* ofrece una guía completa de las mejores prácticas y técnicas modernas para el desarrollo web con PHP. Cubre temas como la seguridad, el rendimiento, la arquitectura de aplicaciones, el uso de *frameworks* y herramientas, y la gestión de dependencias. Es un recurso valioso para aprender a escribir código PHP de alta calidad siguiendo los estándares actuales.

Implantación de Aplicaciones Web 60 Tema 9. A fondo

# W3Schools Online Web Tutorials. (s. f.). PHP Tutorial.

# [https://www.w3schools.com/php/](https://www.w3schools.com/php/)

# W3Schools PHP Tutorial

W3Schools ofrece un tutorial interactivo y fácil de seguir para aprender PHP desde cero. Cubre los fundamentos del lenguaje, con ejemplos y ejercicios prácticos. Es ideal para principiantes que buscan una introducción rápida y práctica a PHP. Muchos de los conceptos básicos que hemos aprendido, como la sintaxis, las variables, las estructuras de control y las funciones se explican de forma clara y concisa en este tutorial.

Implantación de Aplicaciones Web 61 Tema 9. A fondo

# Entrenamiento 1

#### Planteamiento del ejercicio

Crea un formulario HTML con campos para nombre, *email* y mensaje, y un *script* PHP que procese el formulario, valide los datos y envíe un correo electrónico.

#### Desrrollo paso a paso

**▸** Crear el formulario HTML: define un formulario con campos para nombre ( nombre ), *email* ( email ) y mensaje ( mensaje ) utilizando el método POST.

**▸** Crear el script PHP ( procesar.php ):

- Recibe los datos del formulario con $_POST.

- Valida los datos: verifica que los campos no estén vacíos y valida el formato del correo electrónico con filter_var() .

- Si la validación es exitosa, construye el mensaje del correo electrónico.

- Usa la función mail() para enviar el correo.

- Muestra un mensaje de éxito o error al usuario.

#### Solución

$$<form method="post" action="procesar.php">$$

$$<label for="nombre">Nombre:</label>$$

$$<input type="text" name="nombre" id="nombre" required><br><br>$$

$$<label for="email">Email:</label>$$

$$<input type="email" name="email" id="email" required><br><br>$$

$$<label for="mensaje">Mensaje:</label>$$

$$<textarea name="mensaje" id="mensaje" required></textarea><br><br>$$

$$<input type="submit" value="Enviar">$$

</form> // procesar.php <?php

$$if ($\_SERVER["REQUEST\_METHOD"] == "POST") \{$$

$$$nombre = $\_POST["nombre"];$$

$$$email = $\_POST["email"];$$

$mensaje = $_POST["mensaje"]; // Validación

$$$errores = [];$$

if (empty($nombre)) { $errores[] = "El nombre es obligatorio."; } if (empty($email)) {

$errores[] = "El email es obligatorio."; } elseif (!filter_var($email, FILTER_VALIDATE_EMAIL)) { $errores[] = "El email no es válido."; } if (empty($mensaje)) { $errores[] = "El mensaje es obligatorio."; } if (empty($errores)) {

// Enviar correo electrónico

$para = "tu_correo@example.com";

$asunto = "Nuevo mensaje de contacto";

$cuerpo = "Nombre: $nombre\nEmail: $email\nMensaje: $mensaje";

$cabeceras = "From: $email";

if (mail($para, $asunto, $cuerpo, $cabeceras)) { echo "Mensaje enviado con éxito."; } else { echo "Error al enviar el mensaje."; } } else { // Mostrar errores

foreach ($errores as $error) { echo $error . "<br>"; } } } ?>

# Entrenamiento 2

#### Planteamiento del ejercicio

Crea un script PHP que genere una tabla HTML con los datos de un *array* de productos. Cada producto tiene un nombre, precio y cantidad.

#### Desarrollo paso a paso

Crear el *array* de productos:

**▸** Define un *array* con la información de los productos. Cada elemento del *array* será otro *array* asociativo con las claves nombre, precio y cantidad.

**▸** Generar la tabla HTML:

- Crea la estructura básica de la tabla

(<table> , <thead> , <tbody> ).

- Recorre el array de productos con un bucle foreach.

- Por cada producto se genera una fila datos del producto.

#### Solución

<?php

$$$productos = [$$

(<tr>) con celdas (<td>) que muestran los

$$["nombre" => "Manzanas", "precio" => 1.5, "cantidad" => 10],$$

$$["nombre" => "Naranjas", "precio" => 0.8, "cantidad" => 20],$$

$$["nombre" => "Plátanos", "precio" => 1.2, "cantidad" => 15],$$

];

?>

<table>

<thead> <tr>

<th>Nombre</th>

<th>Precio</th>

<th>Cantidad</th>

</tr>

</thead>

<tbody> <?php foreach ($productos as $producto): ?> <tr> <td><?php echo $producto["nombre"]; ?></td> <td><?php echo $producto["precio"]; ?></td> <td><?php echo $producto["cantidad"]; ?></td> </tr> <?php endforeach; ?> </tbody> </table>

# Entrenamiento 3

#### Planteamiento del ejercicio

Crea un script PHP que simule una calculadora simple. Define funciones para sumar, restar, multiplicar y dividir dos números.

#### Desarrollo paso a paso

**▸** Definir las funciones.

- Crea cuatro funciones: sumar() , restar() , multiplicar() y dividir() . Cada función recibirá dos parámetros (los números) y devolverá el resultado de la operación.

**▸** Obtener los números y la operación: usa

$_GET para obtener los números y la

operación del usuario (?num1=5&num2=3&operacion=sumar) .

**▸** Realizar la operación: usa una sentencia *switch* para llamar a la función correspondiente según la operación seleccionada.

**▸** Mostrar el resultado: muestra el resultado de la operación al usuario.

#### Solución

<?php function sumar($a, $b) { return $a + $b; } function restar($a, $b) { return $a - $b;

} function multiplicar($a, $b) { return $a * $b; } function dividir($a, $b) {

$$if ($b == 0) \{$$

return "Error: División por cero."; } else { return $a / $b; } }

$$$num1 = $\_GET["num1"];$$

$$$num2 = $\_GET["num2"];$$

$operacion = $_GET["operacion"]; switch ($operacion) { case "sumar":

$resultado = sumar($num1, $num2); break; case "restar":

$resultado = restar($num1, $num2);

break; case "multiplicar": $resultado = multiplicar($num1, $num2); break; case "dividir": $resultado = dividir($num1, $num2); break; default: $resultado = "Operación no válida."; } echo "Resultado: " . $resultado; ?>

# Entrenamiento 4

#### Planteamiento del ejercicio

Crea un script PHP que lea un archivo CSV llamado " datos.csv " y muestre los datos en una tabla HTML. El archivo CSV tiene la siguiente estructura: nombre,edad,ciudad .

#### Desarrollo paso a paso

**▸** Abrir el archivo CSV: usa fopen() para abrir el archivo " datos.csv " en modo lectura

('r') .

**▸** Leer el archivo línea por línea: usa fgets() dentro de un bucle *while* para leer el archivo línea por línea hasta llegar al final del archivo ( feof() ).

**▸** Procesar cada línea: usa explode() para separar los valores de cada línea por el delimitador (coma).

**▸** Generar la tabla HTML: crea la estructura básica de la tabla y genera una fila ( <tr> ) con celdas ( <td> ) para cada línea del archivo CSV.

**▸** Cerrar el archivo: usa fclose() para cerrar el archivo.

#### Solución

<?php

$$$archivo = fopen("datos.csv", "r");$$

?>

<table>

<thead> <tr>

<th>Nombre</th>

<th>Edad</th>

<th>Ciudad</th>

</tr>

</thead>

<tbody>

$$<?php while (($linea = fgets($archivo)) !== false): ?>$$

$$<?php $datos = explode(",", $linea); ?>$$

<tr> <td><?php echo $datos[0]; ?></td> <td><?php echo $datos[1]; ?></td> <td><?php echo $datos[2]; ?></td> </tr> <?php endwhile; ?> </tbody> </table> <?php fclose($archivo); ?>

# Entrenamiento 5

#### Planteamiento del ejercicio

**▸** Crea una clase PHP llamada " Usuario " con los siguientes atributos: nombre, *email* y contraseña. **▸** Implementa un constructor para inicializar los atributos y métodos para mostrar el nombre completo del usuario y cambiar la contraseña.

#### Desarrollo paso a paso

**▸** Definir la clase: crea una clase llamada Usuario . **▸** Definir los atributos: define los atributos nombre, *email* y contraseña con la visibilidad *private.* **▸** Crear el constructor: define el constructor __construct() que recibe tres parámetros para inicializar los atributos. **▸** Crear los métodos:

- mostrarNombreCompleto() : devuelve una cadena con el nombre completo del usuario (" Juan Pérez ").

- cambiarContrasena() : recibe una nueva contraseña como parámetro y actualiza el atributo contraseña.

#### Solución

<?php

class Usuario { private $nombre;

private $email; private $contrasena; public function __construct($nombre, $email, $contrasena) { $this->nombre = $nombre; $this->email = $email; $this->contrasena = $contrasena; } public function mostrarNombreCompleto() { return $this->nombre; } public function cambiarContrasena($nuevaContrasena) { $this->contrasena = $nuevaContrasena; } } ?>

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–58)*
- Tema 9. Material de estudio  *(pp.5–58)*
- A fondo  *(pp.59–61)*
- Entrenamientos  *(pp.62–74)*
- Implantación de Aplicaciones Web 5 · Implantación de Aplicaciones Web 6 · Implantación de Aplicaciones Web 7 · Implantación de Aplicaciones Web 8 · Implantación de Aplicaciones Web 9 · Implantación de Aplicaciones Web 10 · Implantación de Aplicaciones Web 11 · Implantación de Aplicaciones Web 12 · Implantación de Aplicaciones Web 13 · Implantación de Aplicaciones Web 14 · Implantación de Aplicaciones Web 15 · Implantación de Aplicaciones Web 16 · Implantación de Aplicaciones Web 17 · Implantación de Aplicaciones Web 18 · Implantación de Aplicaciones Web 19 · Implantación de Aplicaciones Web 20 · Implantación de Aplicaciones Web 21 · Implantación de Aplicaciones Web 23 · Implantación de Aplicaciones Web 24 · Implantación de Aplicaciones Web 25 · Implantación de Aplicaciones Web 26 · Implantación de Aplicaciones Web 27 · Implantación de Aplicaciones Web 28 · Implantación de Aplicaciones Web 29 · Implantación de Aplicaciones Web 30 · Implantación de Aplicaciones Web 31 · Implantación de Aplicaciones Web 32 · Implantación de Aplicaciones Web 33 · Implantación de Aplicaciones Web 34 · Implantación de Aplicaciones Web 35 · Implantación de Aplicaciones Web 36 · Implantación de Aplicaciones Web 38 · Implantación de Aplicaciones Web 39 · Implantación de Aplicaciones Web 40 · Implantación de Aplicaciones Web 41 · Implantación de Aplicaciones Web 42 · Implantación de Aplicaciones Web 44 · Implantación de Aplicaciones Web 45 · Implantación de Aplicaciones Web 46 · Implantación de Aplicaciones Web 47 · Implantación de Aplicaciones Web 48 · Implantación de Aplicaciones Web 49 · Implantación de Aplicaciones Web 50 · Implantación de Aplicaciones Web 51 · Implantación de Aplicaciones Web 52 · Implantación de Aplicaciones Web 53 · Implantación de Aplicaciones Web 54 · Implantación de Aplicaciones Web 55 · Implantación de Aplicaciones Web 56 · Implantación de Aplicaciones Web 57 · Implantación de Aplicaciones Web 58  *(pp.5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 38, 39, 40, 41, 42, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58)*
- Implantación de Aplicaciones Web 62 Tema 9. Entrenamientos · Implantación de Aplicaciones Web 63 Tema 9. Entrenamientos · Implantación de Aplicaciones Web 64 Tema 9. Entrenamientos · Implantación de Aplicaciones Web 65 Tema 9. Entrenamientos · Implantación de Aplicaciones Web 66 Tema 9. Entrenamientos · Implantación de Aplicaciones Web 67 Tema 9. Entrenamientos · Implantación de Aplicaciones Web 68 Tema 9. Entrenamientos · Implantación de Aplicaciones Web 69 Tema 9. Entrenamientos · Implantación de Aplicaciones Web 70 Tema 9. Entrenamientos · Implantación de Aplicaciones Web 71 Tema 9. Entrenamientos · Implantación de Aplicaciones Web 72 Tema 9. Entrenamientos · Implantación de Aplicaciones Web 73 Tema 9. Entrenamientos · Implantación de Aplicaciones Web 74 Tema 9. Entrenamientos  *(pp.62–74)*