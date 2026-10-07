## Tema 10

# Implantación de Aplicaciones Web

# Tema 10. Acceso a bases de datos desde lenguajes de

# script de servidor

# Índice

Esquema Material de estudio

## 10.1. Introducción y objetivos

10.2. Integración de los lenguajes de script de servidor con los SGBD

## 10.3. Conexión a bases de datos

## 10.4. Creación de bases de datos y tablas

10.5. Creación de vistas. Creación de procedimientos almacenados 10.6. Recuperación de la información de la base de datos desde una página web

## 10.7. Modificación de la información almacenada:

inserciones, actualizaciones y borrados

## 10.8. Verificación de la información

## 10.9. Gestión de errores

10.10. Verificación del funcionamiento y pruebas de rendimiento

## 10.11. Mecanismos de seguridad y control de accesos

10.12. Documentación A fondo

PHP Manual - MySQLi

PHP Manual - PDO

OWASP - SQL Injection

Entrenamientos

Entrenamiento 1 Entrenamiento 2 Entrenamiento 3 Entrenamiento 4 Entrenamiento 5

# Esquema

![image-1](images/image-1.png)

Implantación de Aplicaciones Web 4 Tema 10. Esquema

# 10.1. Introducción y objetivos

El acceso a bases de datos es una parte fundamental del desarrollo web moderno. Permite a las aplicaciones web almacenar, recuperar y manipular datos de forma dinámica, lo que da lugar a sitios web interactivos y personalizados. Los lenguajes de *script* de servidor, como PHP, desempeñan un papel crucial en este proceso, actuando como intermediarios entre la aplicación web y la base de datos. Vamos a explorar cómo PHP se utiliza para interactuar con bases de datos, cubriendo conceptos esenciales como:

**▸ Conexión a la base de datos:** establecer una conexión entre el *script* PHP y el servidor de la base de datos (como MySQL, PostgreSQL, etc.).

**▸ Ejecución de consultas:** enviar consultas SQL a la base de datos para realizar operaciones como insertar, actualizar, eliminar y recuperar datos.

**▸ Manejo de resultados:** procesar los datos devueltos por la base de datos en respuesta a las consultas.

**▸ Seguridad:** implementar medidas de seguridad para proteger la base de datos de accesos no autorizados y ataques de inyección SQL.

Aprenderemos a utilizar las diferentes funciones y extensiones que ofrece PHP para trabajar con bases de datos, incluyendo MySQLi y PDO. Además, veremos ejemplos prácticos de cómo integrar el acceso a bases de datos en aplicaciones web reales.

# 10.2. Integración de los lenguajes de script de

# servidor con los SGBD

La integración de lenguajes de *script* de servidor con sistemas gestores de bases de datos (SGBD) es fundamental para el desarrollo de aplicaciones web dinámicas e interactivas. Permite a los desarrolladores conectar sus sitios web con bases de datos, lo que facilita el almacenamiento, la recuperación y la manipulación de datos de forma eficiente.

Los lenguajes de *script* de servidor, como PHP, Python, Ruby o Node.js, actúan como intermediarios entre la aplicación web y el SGBD (MySQL, PostgreSQL, MongoDB, etc.). Cuando un usuario interactúa con la aplicación web (por ejemplo, rellenando un formulario o realizando una búsqueda), el *script* de servidor se encarga de:

**▸ Conectar a la base de datos:** establecer una conexión con el SGBD utilizando las credenciales de acceso (nombre de usuario, contraseña, nombre de la base de datos).

**▸ Enviar consultas:** construir y ejecutar consultas SQL para realizar operaciones en la base de datos, como insertar nuevos datos, actualizar registros existentes, eliminar información o recuperar datos específicos.

**▸ Procesar resultados:** recibir los resultados de las consultas y procesarlos para mostrarlos al usuario en la página web, generar informes o realizar otras acciones.

Beneficios de integrar BBDD

**▸ Sitios web dinámicos:** permite crear sitios web que se actualizan con contenido dinámico en tiempo real, como noticias, catálogos de productos o perfiles de usuario. **▸ Personalización:** facilita la personalización de la experiencia del usuario, mostrando contenido relevante en función de sus preferencias o historial de interacción.

**▸ Gestión de datos eficiente:** permite almacenar y gestionar grandes volúmenes de datos de forma estructurada y eficiente.

**▸ Seguridad:** los SGBD ofrecen mecanismos de seguridad para proteger los datos de accesos no autorizados.

**▸ Escalabilidad:** las aplicaciones web que utilizan SGBD pueden escalar fácilmente para manejar un mayor número de usuarios y datos.

#### Ejemplos de integración

**▸ PHP con MySQL:** una combinación muy popular para el desarrollo web, utilizada en plataformas como WordPress.

**▸ Python con PostgreSQL:** empleada en aplicaciones web que requieren un alto rendimiento y seguridad, como sistemas de gestión empresarial.

**▸ Node.js con MongoDB:** ideal para aplicaciones web que manejan grandes volúmenes de datos no estructurados, como redes sociales o plataformas de comercio electrónico.

#### Herramientas y tecnologías

- ▸ Controladores de bases de datos: bibliotecas de software que facilitan la conexión

    - y la interacción con diferentes SGBD desde los lenguajes de script.

- ▸ ORM (object-relational mapping): herramientas que permiten trabajar con bases

    - de datos utilizando objetos, lo que simplifica el desarrollo.

- ▸ API REST: interfaces de programación que permiten a las aplicaciones web acceder

    - a datos de bases de datos de forma estandarizada.

        - Implantación de Aplicaciones Web 8

# 10.3. Conexión a bases de datos

Para conectar tu *script* PHP a una base de datos necesitas usar extensiones que te permitan comunicarte con el sistema gestor de bases de datos (SGBD). PHP ofrece dos extensiones principales para esto: **MySQLi** y **PDO.**

MySQLi (MySQL Improved)

MySQLi es una extensión específica para interactuar con bases de datos MySQL. Ofrece una interfaz procedimental y orientada a objetos. A continuación se muestra un ejemplo de conexión usando MySQLi orientado a objetos:

<?php

$servername = "localhost";

$username = "tu_usuario";

$password = "tu_contraseña";

$dbname = "nombre_de_la_base_de_datos";

// Crear conexión

$conn = new mysqli($servername, $username, $password, $dbname);

// Verificar la conexión

if ($conn->connect_error) { die("Conexión fallida: " . $conn->connect_error); } echo "Conexión exitosa"; // Cerrar la conexión (opcional en este ejemplo)

$conn->close(); ?>

#### Explicación

**▸** $servername , $username , $password , $dbname : reemplaza estos valores con las credenciales de tu servidor y base de datos.

**▸** new mysqli(...) : crea un nuevo objeto mysqli que representa la conexión.

**▸** $conn->connect_error : verifica si ha habido algún error al conectar.

**▸** $conn->close() : cierra la conexión.

PDO (PHP Data Objects)

PDO es una extensión más general que te permite conectar a diferentes SGBD, como MySQL, PostgreSQL, SQLite, etc. Ofrece una interfaz orientada a objetos y es recomendable por su flexibilidad y seguridad. Aquí te muestro un ejemplo de conexión a MySQL usando PDO:

<?php

$servername = "localhost";

$username = "tu_usuario";

$password = "tu_contraseña";

$dbname = "nombre_de_la_base_de_datos";

try { $conn = new PDO("mysql:host=$servername;dbname=$dbname", $username, $password); // Establecer el modo de error PDO a excepción

$conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION); echo "Conexión exitosa"; } catch(PDOException $e) { echo "Conexión fallida: " . $e->getMessage(); } // Cerrar la conexión (opcional en este ejemplo) $conn = null; ?>

#### Explicación

**▸** new PDO(...) : crea un nuevo objeto PDO con los parámetros de conexión. **▸** $conn->setAttribute(...) : configura PDO para que lance excepciones en caso de error. **▸** try...catch : maneja las posibles excepciones que pueden ocurrir durante la conexión.

#### Recomendaciones

**▸ Seguridad:** nunca almacenes las credenciales de la base de datos directamente en el código. Utiliza variables de entorno o archivos de configuración separados. **▸ Manejo de errores:** implementa un manejo de errores adecuado para capturar y gestionar las posibles excepciones o errores de conexión. **▸ PDO vs. MySQLi:** si solo trabajas con MySQL, MySQLi puede ser una opción válida.

Sin embargo, PDO es recomendable por su flexibilidad y portabilidad si necesitas trabajar con diferentes SGBD en el futuro.

Estos son ejemplos de conexión con la base de datos. Una vez establecida la comunicación, puedes usar las funciones de MySQLi o PDO para ejecutar consultas SQL y manipular los datos de la base de datos.

# 10.4. Creación de bases de datos y tablas

Si bien puedes gestionar bases de datos y tablas directamente con comandos SQL, PHP te permite hacerlo también a través de su código. Esto es especialmente útil para automatizar tareas o crear aplicaciones web que necesiten crear o modificar la estructura de la base de datos dinámicamente.

Crear una base de datos

Para crear una base de datos puedes usar la función mysqli_query() con la instrucción

SQL CREATE DATABASE .

<?php

$servername = "localhost";

$username = "tu_usuario";

$password = "tu_contraseña";

// Crear conexión

$conn = new mysqli($servername, $username, $password);

// Verificar la conexión

if ($conn->connect_error) { die("Conexión fallida: " . $conn->connect_error);

}

// Crear la base de datos

$sql = "CREATE DATABASE mi_nueva_base_de_datos";

$$if ($conn->query($sql) === TRUE) \{$$

echo "Base de datos creada con éxito"; } else { echo "Error al crear la base de datos: " . $conn->error;

}

$conn->close();

?>

Crear una tabla

Para crear una tabla también usas mysqli_query() con la instrucción SQL CREATE

TABLE .

<?php

$servername = "localhost";

$username = "tu_usuario";

$password = "tu_contraseña";

$dbname = "mi_nueva_base_de_datos";

// Crear conexión

$conn = new mysqli($servername, $username, $password, $dbname);

// Verificar la conexión

if ($conn->connect_error) { die("Conexión fallida: " . $conn->connect_error); }

// Crear la tabla

$$$sql = "CREATE TABLE usuarios ($$

id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY, nombre VARCHAR(30) NOT NULL, apellido VARCHAR(30) NOT NULL, email VARCHAR(50), reg_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP )";

$$if ($conn->query($sql) === TRUE) \{$$

echo "Tabla 'usuarios' creada con éxito"; } else { echo "Error al crear la tabla: " . $conn->error;

}

$conn->close();

?>

#### Explicación

**▸** CREATE TABLE usuarios : define el nombre de la tabla como " usuarios ".

**▸** Dentro de los paréntesis se definen las columnas de la tabla:

- id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY : una columna llamada " id " de tipo entero, sin signo, que se incrementa automáticamente y es la clave primaria de la tabla.

- nombre VARCHAR(30) NOT NULL : una columna llamada " nombre " de tipo texto (máximo treinta caracteres) que no puede ser nula.

- apellido VARCHAR(30) NOT NULL : similar a " nombre ".

- email VARCHAR(50) : una columna llamada " email " de tipo texto (máximo cincuenta caracteres).

- reg_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP : una columna llamada " reg_date " de tipo fecha y hora, que por defecto toma la fecha y hora actual y se actualiza automáticamente cada vez que se modifica la fila.

#### Recomendaciones

**▸ Seguridad:** es importante sanitizar las entradas del usuario antes de usarlas en las consultas SQL para prevenir inyecciones SQL.

**▸ PDO:** para una mayor flexibilidad y seguridad, considera usar PDO en lugar de MySQLi. La sintaxis para crear bases de datos y tablas con PDO es muy similar.

# 10.5. Creación de vistas. Creación de procedimientos almacenados

Tanto las vistas como los procedimientos almacenados son herramientas poderosas en las bases de datos que te permiten mejorar la gestión y el acceso a tus datos. A continuación, te explico cómo crearlas con PHP y MySQL:

Vistas

Una vista es una consulta SQL almacenada en la base de datos. Actúa como una tabla virtual, pero no almacena datos por sí misma. En su lugar, se basa en la consulta subyacente para obtener los datos.

<?php

$servername = "localhost";

$username = "tu_usuario";

$password = "tu_contraseña";

$dbname = "mi_base_de_datos";

// Crear conexión

$conn = new mysqli($servername, $username, $password, $dbname);

// Verificar la conexión

if ($conn->connect_error) { die("Conexión fallida: " . $conn->connect_error);

}

// Crear la vista

$sql = "CREATE VIEW vista_usuarios AS SELECT nombre, apellido FROM usuarios";

$$if ($conn->query($sql) === TRUE) \{$$

echo "Vista 'vista_usuarios' creada con éxito"; } else { echo "Error al crear la vista: " .

$conn->error;

}

$conn->close();

?>

#### Explicación

**▸** CREATE VIEW vista_usuarios : define el nombre de la vista como " vista_usuarios ".

**▸** SELECT nombre, apellido FROM usuarios : define la consulta SQL que la vista utilizará para obtener los datos. En este caso, la vista mostrará solo los nombres y apellidos de la tabla " usuarios ".

Procedimientos almacenados

Un procedimiento almacenado es un conjunto almacenan en la base de datos y se pueden

de instrucciones SQL que se ejecutar cuando sea necesario.

Permiten encapsular lógica compleja y utilizarla en diferentes partes de la aplicación.

#### Ejemplo

<?php

$servername = "localhost";

$username = "tu_usuario";

$password = "tu_contraseña";

$dbname = "mi_base_de_datos";

// Crear conexión

$conn = new mysqli($servername, $username, $password, $dbname);

// Verificar la conexión

if ($conn->connect_error) { die("Conexión fallida: " . $conn->connect_error); }

// Crear el procedimiento almacenado

$$$sql = "CREATE PROCEDURE obtener\_usuarios()$$

BEGIN

SELECT * FROM usuarios; END;";

$$if ($conn->query($sql) === TRUE) \{$$

echo "Procedimiento almacenado 'obtener_usuarios' creado con éxito"; } else { echo "Error al crear el procedimiento almacenado: " . $conn->error;

}

$conn->close();

?>

#### Explicación

**▸** CREATE PROCEDURE obtener_usuarios() : define el nombre del procedimiento almacenado como " obtener_usuarios ".

**▸** BEGIN ... END; : encierra el bloque de código SQL del procedimiento.

▸ SELECT * FROM usuarios; : la instrucción SQL que se ejecutará cuando se llame al procedimiento. En este caso, selecciona todos los datos de la tabla " usuarios ".

#### Recomendaciones

**▸ Delimitadores:** al crear procedimientos almacenados es posible que necesites cambiar el delimitador de consultas SQL de MySQL (que es " ; ") para evitar conflictos con el punto y coma dentro del procedimiento. Puedes usar DELIMITER // al principio y DELIMITER ; al final para cambiar el delimitador temporalmente.

**▸ Parámetros:** los procedimientos almacenados pueden aceptar parámetros de entrada y salida para hacerlos más flexibles.

**▸ Seguridad:** al igual que con las consultas SQL es importante sanitizar las entradas del usuario al usar procedimientos almacenados para prevenir inyecciones SQL.

Las vistas y los procedimientos almacenados son herramientas muy interesantes para simplificar el acceso a los datos, mejorar el rendimiento y la seguridad de las aplicaciones web.

# 10.6. Recuperación de la información de la base de

# datos desde una página web

Para recuperar información de una base de datos y mostrarla en una página web necesitas combinar código PHP con HTML. Aquí te presento un ejemplo sencillo usando MySQLi para obtener datos de la tabla " usuarios " y mostrarlos en una tabla

HTML:

<?php

$servername = "localhost";

$username = "tu_usuario";

$password = "tu_contraseña";

$dbname = "mi_base_de_datos";

// Crear conexión

$conn = new mysqli($servername, $username, $password, $dbname);

// Verificar la conexión

if ($conn->connect_error) { die("Conexión fallida: " . $conn->connect_error);

}

// Consulta SQL para obtener los datos

$sql = "SELECT id, nombre, apellido, email FROM usuarios";

$result = $conn->query($sql);

// Mostrar los datos en una tabla HTML

if ($result->num_rows > 0) { echo "<table><tr><th>ID</th><th>Nombre</th><th>Apellido</th><th>Email</th></tr>"; // Salida de datos de cada fila

$$while($row = $result->fetch\_assoc()) \{$$

echo "<tr><td>".$row["id"]."</td><td>".$row["nombre"]."</td><td>".$row["apellido"]."</td> <td>".$row["email"]."</td></tr>"; } echo "</table>"; } else { echo "0 resultados";

}

$conn->close();

?>

Mostrar los datos

**▸** Se verifica si hay resultados con $result->num_rows > 0 .

**▸** Si hay resultados se crea una tabla HTML con los encabezados correspondientes.

**▸** Se usa un bucle while para recorrer cada fila del resultado ( $result->fetch_assoc() obtiene un *array* asociativo con los datos de cada fila).

**▸** Dentro del bucle se imprime una fila de la tabla HTML con los datos de cada usuario.

**▸** Si no hay resultados se muestra un mensaje indicando " 0 resultados ".

#### Recomendaciones

**▸ Separar la lógica de la presentación:** es una buena práctica separar el código PHP del código HTML. Puedes usar include o require para incluir el código PHP en tu archivo HTML.

**▸ Escapar las salidas:** para evitar problemas de seguridad y mostrar correctamente los datos en la página web es importante escapar las salidas usando funciones

como htmlspecialchars() .

**▸ Formato y estilo:** puedes usar CSS para dar formato y estilo a la tabla HTML y mejorar la presentación de los datos.

**▸ Paginación:** si tienes muchos datos, considera implementar la paginación para mostrar los resultados en varias páginas.

# 10.7. Modificación de la información almacenada:

# inserciones, actualizaciones y borrados

La modificación de información en una base de datos es esencial para mantener los datos actualizados y relevantes. PHP, junto con SQL, te permite realizar inserciones, actualizaciones y borrados de forma eficiente. Veamos cómo:

Inserciones

Para insertar nuevos datos en una tabla se utiliza la instrucción SQL INSERT INTO .

<?php

$servername = "localhost";

$username = "tu_usuario";

$password = "tu_contraseña";

$dbname = "mi_base_de_datos";

// Crear conexión

$conn = new mysqli($servername, $username, $password, $dbname);

// Verificar la conexión

if ($conn->connect_error) { die("Conexión fallida: " . $conn->connect_error);

}

// Datos a insertar

$nombre = "Nuevo Usuario";

$apellido = "Apellido";

$email = "nuevo@email.com";

// Consulta SQL para insertar datos

$sql = "INSERT INTO usuarios (nombre, apellido, email) VALUES ('$nombre', '$apellido', '$email')";

$$if ($conn->query($sql) === TRUE) \{$$

echo "Nuevo registro creado con éxito"; } else { echo "Error: " . $sql . "<br>" . $conn->error;

}

$conn->close();

?>

#### Explicación

**▸** INSERT INTO usuarios (nombre, apellido, email) : especifica la tabla (usuarios) y las

columnas donde se insertarán los datos.

**▸** VALUES ('$nombre', '$apellido', '$email') : proporciona los valores a insertar en las columnas correspondientes.

Actualizaciones

Para actualizar datos existentes en una tabla se utiliza la instrucción SQL UPDATE .

<?php

$servername = "localhost";

$username = "tu_usuario";

$password = "tu_contraseña";

$dbname = "mi_base_de_datos";

// Crear conexión

$conn = new mysqli($servername, $username, $password, $dbname);

// Verificar la conexión

if ($conn->connect_error) { die("Conexión fallida: " . $conn->connect_error);

}

// Datos a actualizar

$nuevo_email = "actualizado@email.com";

$id_usuario = 1; // ID del usuario a actualizar

// Consulta SQL para actualizar datos

$sql = "UPDATE usuarios SET email='$nuevo_email' WHERE id=$id_usuario";

$$if ($conn->query($sql) === TRUE) \{$$

echo "Registro actualizado con éxito";

} else { echo "Error al actualizar el registro: " . $conn->error;

}

$conn->close();

?>

#### Explicación

**▸** UPDATE usuarios SET email='$nuevo_email' : especifica la tabla (usuarios) y la columna a actualizar (email) con el nuevo valor.

**▸** WHERE id=$id_usuario : define la condición para seleccionar el registro a actualizar (en este caso, el usuario con id=1 ).

Borrados

Para eliminar datos de una tabla, se utiliza la instrucción SQL DELETE.

<?php

$servername = "localhost";

$username = "tu_usuario";

$password = "tu_contraseña";

$dbname = "mi_base_de_datos";

// Crear conexión

$conn = new mysqli($servername, $username, $password, $dbname);

// Verificar la conexión

if ($conn->connect_error) { die("Conexión fallida: " . $conn->connect_error);

}

// ID del usuario a eliminar

$$$id\_usuario = 1;$$

// Consulta SQL para eliminar datos

$sql = "DELETE FROM usuarios WHERE id=$id_usuario";

$$if ($conn->query($sql) === TRUE) \{$$

echo "Registro eliminado con éxito"; } else { echo "Error al eliminar el registro: " . $conn->error;

}

$conn->close();

?>

#### Explicación

- ▸ DELETE FROM usuarios : especifica la tabla (usuarios) de la que se eliminarán los

    - datos.

- ▸ WHERE id=$id_usuario : define la condición para seleccionar el registro a eliminar (en

    - este caso, el usuario con id=1 ).

#### Recomendaciones

**▸ Seguridad:** sanitiza las entradas del usuario para prevenir inyecciones SQL.

**▸ Transacciones:** para operaciones que involucran múltiples modificaciones, utiliza transacciones para asegurar la integridad de los datos.

**▸ PDO:** considera usar PDO para una mayor flexibilidad y seguridad. Con estas herramientas puedes crear aplicaciones web dinámicas que permitan a los usuarios interactuar con la base de datos y modificar la información de forma segura y eficiente.

# 10.8. Verificación de la información

La verificación de la información en el contexto del acceso a bases de datos con PHP se refiere a asegurar la integridad, validez y seguridad de los datos que se manejan. Esto implica validar los datos antes de insertarlos, actualizarlos o incluso mostrarlos al usuario.

Aspectos clave de la verificación de la información

#### Validación de datos

Antes de insertar o actualizar datos en la base de datos, es crucial validarlos para asegurar que cumplen con las reglas y restricciones definidas. Esto incluye:

**▸ Tipo de dato:** verificar que el dato ingresado corresponde al tipo de dato esperado (entero, texto, fecha, etc.).

**▸ Formato:** verificar que el dato cumple con un formato específico (ej.: una dirección de correo electrónico, un número de teléfono).

**▸ Longitud:** verificar que la longitud del dato está dentro de los límites permitidos.

**▸ Valores permitidos:** verificar que el dato se encuentra dentro de un conjunto de valores permitidos (ej.: un campo de selección con opciones predefinidas).

**▸ Restricciones de la base de datos:** asegurar que los datos cumplen con las restricciones definidas en la base de datos, como claves únicas, valores no nulos, etc.

<?php

// Validar un email

$$$email = $\_POST["email"];$$

if (!filter_var($email, FILTER_VALIDATE_EMAIL)) { echo "Email inválido";

}

?>

#### Sanitización de datos

La sanitización de datos se refiere a limpiar y escapar los datos para prevenir

ataques de inyección SQL y otros problemas de seguridad. Esto implica:

**▸ Escapar caracteres especiales:** usar funciones como mysqli_real_escape_string() o htmlspecialchars() para escapar caracteres especiales que podrían interferir con las consultas SQL o la visualización de datos en la página web.

**▸ Validar entradas del usuario:** no confiar en las entradas del usuario y validarlas cuidadosamente antes de usarlas en las consultas SQL.

#### Manejo de errores

Implementar un manejo de errores adecuado para capturar y gestionar las excepciones o errores que pueden ocurrir durante la interacción con la base de datos. Esto te permitirá:

**▸** Mostrar mensajes de error informativos al usuario.

**▸** Registrar los errores para su posterior análisis.

**▸** Prevenir que la aplicación se bloquee o muestre información sensible en caso de error.

#### Control de acceso

Implementar mecanismos de control de acceso para restringir el acceso a la información sensible y prevenir modificaciones no autorizadas. Esto puede incluir:

**▸ Autenticación de usuarios:** verificar la identidad de los usuarios antes de permitirles acceder a la base de datos.

**▸ Autorización:** otorgar diferentes niveles de acceso a los usuarios según sus roles y permisos.

La verificación de la información es un proceso crucial para garantizar la integridad, validez y seguridad de los datos en tus aplicaciones web. Implementar las medidas adecuadas te ayudará a proteger tu base de datos y a proporcionar una experiencia de usuario confiable y segura.

# 10.9. Gestión de errores

La gestión de errores en PHP es crucial para crear aplicaciones web robustas y confiables. Permite controlar cómo se comportará tu aplicación cuando ocurran errores, lo que previene fallos inesperados y proporcionando información útil para la depuración.

Principales aspectos de la gestión de errores en PHP

#### Tipos de errores

PHP tiene diferentes tipos de errores, entre ellos:

**▸ Errores fatales:** errores graves que detienen la ejecución del *script,* como llamar a una función inexistente o acceder a una variable no definida.

**▸ Advertencias:** errores no fatales que no detienen la ejecución, pero indican un posible problema, como incluir un archivo que no existe.

**▸ Avisos:** errores aún menos graves que las advertencias, cómo usar una variable sin inicializar.

#### Mostrar errores

Para facilitar el desarrollo puedes configurar PHP para que muestre los errores en pantalla. Esto se puede hacer en el archivo

error_reporting() e ini_set() .

<?php

// Mostrar todos los errores

error_reporting(E_ALL); ini_set('display_errors', 1); ?>

#### Manejadores de errores

Puedes definir tus propios manejadores

php.ini o usando funciones como

de errores usando la función

set_error_handler() . Esto te permite personalizar cómo se manejan los errores, por ejemplo, registrándolos en un archivo o personalizado.

mostrando un mensaje de error

<?php function miManejadorDeErrores($errno, $errstr, $errfile, $errline) { echo "<b>Error:</b> [$errno] $errstr<br>"; echo "Línea: $errline en el archivo $errfile<br>"; // Puedes registrar el error en un archivo o base de datos } set_error_handler("miManejadorDeErrores"); ?>

#### Excepciones

Las excepciones son un mecanismo para manejar errores de forma estructurada. Puedes lanzar excepciones usando throw new Exception() y capturarlas usando

bloques try...catch .

<?php try { // Código que puede lanzar una excepción

$$if ($divisor == 0) \{$$

throw new Exception("División por cero"); } $resultado = $dividendo / $divisor; } catch (Exception $e) { echo "Error: " . $e->getMessage(); } ?>

#### Buenas prácticas

- ▸ No mostrar errores en producción: en un entorno de producción es importante

    - desactivar la visualización de errores en pantalla por seguridad y para evitar que los

    - usuarios vean información sensible.

- ▸ Registrar errores: registrar los errores en un archivo o base de datos te permite

    - analizarlos y solucionar los problemas.

- ▸ Usar excepciones para errores graves: las excepciones son útiles para manejar

    - errores que requieren una atención especial o que pueden interrumpir el flujo normal

    - de la aplicación.

- ▸ Manejar errores de forma específica: no uses un manejador de errores genérico

    - para todos los tipos de errores. Define manejadores específicos para diferentes

    - situaciones.

        - Implantación de Aplicaciones Web 37

# 10.10. Verificación del funcionamiento y pruebas

# de rendimiento

La verificación del funcionamiento y las pruebas de rendimiento son cruciales para garantizar que tu aplicación web que interactúa con la base de datos funcione correctamente y de manera eficiente.

Estrategias y herramientas para llevar a cabo estas tareas

#### Verificación del funcionamiento

**▸ Pruebas unitarias:** crea pruebas unitarias para verificar el correcto funcionamiento de las funciones individuales que interactúan con la base de datos, como las funciones de conexión, inserción, actualización, eliminación y consulta.

**▸ Pruebas de integración:** verifica la interacción entre diferentes componentes de la aplicación y la base de datos. Por ejemplo, probar que un formulario web inserta correctamente los datos en la base de datos.

**▸ Pruebas de sistema:** prueba la aplicación web en su conjunto, incluyendo la interacción con la base de datos, para asegurar que cumple con los requisitos funcionales.

**▸ Pruebas de aceptación:** permite a los usuarios finales probar la aplicación y verificar que cumple con sus expectativas.

#### Herramientas para pruebas

**▸ PHPUnit:** un *framework* popular para pruebas unitarias en PHP.

**▸ Codeception:** un *framework* que permite realizar pruebas unitarias, de integración y de aceptación.

**▸ Selenium:** una herramienta para automatizar pruebas en navegadores web.

#### Rendimiento

**▸ Pruebas de carga:** simula el acceso concurrente de múltiples usuarios a la aplicación para evaluar su rendimiento bajo carga.

**▸ Pruebas de estrés:** somete a la aplicación a una carga extrema para identificar sus límites y puntos débiles.

**▸ Pruebas de resistencia:** evalúa el rendimiento de la aplicación durante un período prolongado bajo una carga constante.

**▸ Pruebas de escalabilidad:** determina cómo se comporta la aplicación al aumentar la carga de trabajo y la cantidad de datos.

#### Herramientas para pruebas de rendimiento

**▸ Apache JMeter:** una herramienta de código abierto para realizar pruebas de carga y rendimiento.

**▸ LoadRunner:** una herramienta comercial para pruebas de rendimiento.

**▸ WebPageTest:** una herramienta *online* para analizar el rendimiento de páginas web.

#### Monitorización

**▸ Monitoreo de la base de datos:** utiliza herramientas para monitorear el rendimiento de la base de datos, como MySQL Workbench o phpMyAdmin.

**▸ Monitoreo de la aplicación:** utiliza herramientas de Application Performance Monitoring (APM) para rastrear el rendimiento de la aplicación e identificar cuellos de botella.

**▸ Registro de consultas lentas:** configura la base de datos para registrar las consultas que tardan más de un tiempo determinado en ejecutarse.

#### Optimización

**▸ Optimizar consultas SQL:** utiliza herramientas de análisis de consultas para identificar y optimizar las consultas que afectan el rendimiento.

**▸ Indexar las columnas:** crea índices en las columnas que se utilizan con frecuencia en las consultas para acelerar la búsqueda de datos.

**▸ Cachear datos:** almacena en caché los datos que se acceden con frecuencia para reducir el número de consultas a la base de datos.

**▸ Optimizar la configuración del servidor:** ajusta la configuración del servidor web y de la base de datos para mejorar el rendimiento.

#### Recomendaciones

**▸ Realiza pruebas de forma regular:** integra las pruebas de funcionamiento y rendimiento en tu flujo de trabajo de desarrollo para detectar problemas de forma temprana.

**▸ Automatiza las pruebas:** automatiza las pruebas para ahorrar tiempo y asegurar la consistencia.

**▸ Utiliza herramientas de análisis:** utiliza herramientas de análisis para identificar cuellos de botella y áreas de mejora.

**▸ Documenta las pruebas:** documenta las pruebas realizadas y los resultados obtenidos para facilitar el mantenimiento y la resolución de problemas.

Al seguir todas estas recomendaciones, podrás asegurar que tu aplicación web que interactúa con la base de datos funcione de forma eficiente, confiable y satisfaga las necesidades de tus usuarios.

# 10.11. Mecanismos de seguridad y control de accesos

La seguridad y el control de accesos son aspectos fundamentales al trabajar con bases de datos, especialmente en aplicaciones web. Implementar mecanismos robustos te ayudará a proteger la información sensible de accesos no autorizados y a prevenir ataques maliciosos. Seguidamente presentamos algunos mecanismos de seguridad y control de accesos que puedes implementar en tus aplicaciones PHP que interactúan con bases de datos.

Autenticación de usuarios

**▸ Contraseñas seguras:** exige a los usuarios que creen contraseñas fuertes y que las almacene de forma segura utilizando funciones de hash como password_hash() .

**▸ Autenticación multifactor:** implementa la autenticación multifactor (MFA) para agregar una capa adicional de seguridad.

**▸ Sesiones:** utiliza sesiones para mantener la autenticación del usuario durante su interacción con la aplicación.

Control de acceso basado en roles

**▸ Roles de usuario:** define roles de usuario con diferentes niveles de acceso a la base de datos, según las autorizaciones de cada rol, debido a las necesidades que debe cubrir cada uno de ellos.

**▸ Permisos:** asigna permisos específicos a cada rol para controlar qué acciones pueden realizar (lectura, escritura, actualización, eliminación).

Prevención de inyección SQL

**▸ Consultas preparadas:** utiliza consultas preparadas con PDO o MySQLi para evitar que las entradas del usuario se interpreten como código SQL.

**▸ Escapar caracteres especiales:** escapa los caracteres especiales en las entradas del usuario antes de usarlas en las consultas SQL. **▸ Validación de datos:** valida las entradas del usuario para asegurar que cumplen con los tipos de datos y formatos esperados.

Cifrado de datos

**▸ Cifrado en tránsito:** utiliza HTTPS para cifrar la comunicación entre la aplicación web y el servidor de la base de datos. **▸ Cifrado en reposo:** cifra los datos sensibles en la base de datos utilizando el cifrado de disco o el cifrado a nivel de columna.

Otras medidas de seguridad

**▸ Principio de mínimo privilegio:** otorga a los usuarios y aplicaciones solo los permisos necesarios para realizar sus tareas. **▸ Actualizaciones de seguridad:** mantén el *software* actualizado, incluyendo PHP, el sistema gestor de bases de datos y las bibliotecas que utilizas. **▸ Monitoreo y registro:** monitorea la actividad de la base de datos y registra los eventos importantes para detectar posibles intrusiones. **▸** ***Firewalls:*** utiliza *firewalls* para controlar el acceso a la base de datos desde redes externas.

Ejemplo de consulta preparada con pdo

<?php

$stmt = $pdo->prepare("SELECT * FROM usuarios WHERE nombre = :nombre");

$stmt->bindParam(':nombre', $nombre);

$stmt->execute();

?>

Recomendaciones

**▸ No almacenar información sensible en texto plano:** utiliza funciones de hash o cifrado para proteger la información sensible, como contraseñas y datos de tarjetas de crédito.

**▸ Implementa una política de seguridad:** define una política de seguridad que incluya las mejores prácticas para el acceso a la base de datos y la gestión de usuarios.

**▸ Realiza auditorías de seguridad:** realiza auditorías de seguridad de forma regular para identificar vulnerabilidades y mejorar la seguridad de la aplicación. Al implementar estas medidas de seguridad y control de accesos, podrás proteger tu base de datos y la información sensible que contiene, minimizando el riesgo de ataques y garantizando la integridad de los datos.

# 10.12. Documentación

La documentación es una parte esencial del desarrollo de *software* y esto se aplica también al acceso a bases de datos con PHP. Una buena documentación facilita el entendimiento del código, el mantenimiento, la colaboración entre desarrolladores y la resolución de problemas.

Aspectos clave de la documentación

#### Tipos de documentación

**▸ Comentarios en el código:** utiliza comentarios en el código para explicar la lógica, el propósito de las funciones y las decisiones de diseño.

**▸ Documentación externa:** crea documentos separados para describir la arquitectura de la base de datos, el diseño de las tablas, las consultas SQL utilizadas y la API para acceder a los datos.

**▸ Diagramas:** utiliza diagramas entidad-relación (ERD) para visualizar la estructura de la base de datos y las relaciones entre las tablas.

**▸ Ejemplos de código:** proporciona ejemplos de código que muestran cómo usar las funciones y clases para interactuar con la base de datos.

#### Herramientas

**▸ PHPDoc:** un estándar para documentar código PHP que permite generar documentación en HTML a partir de los comentarios en el código.

**▸ Herramientas de generación de documentación:** existen herramientas que automatizan la generación de documentación a partir del código, como Doxygen y phpDocumentor.

#### Contenido de la documentación

**▸ Descripción de la base de datos:** nombre de la base de datos, propósito, versión, etc.

**▸ Diseño de las tablas:** nombre de las tablas, columnas, tipos de datos, claves primarias, claves foráneas, índices, etc.

**▸ Consultas SQL:** descripción de las consultas SQL utilizadas para acceder a los datos, incluyendo inserciones, actualizaciones, eliminaciones y consultas.

**▸ API:** descripción de las funciones y clases que se utilizan para interactuar con la base de datos, incluyendo parámetros, valores de retorno y ejemplos de uso.

**▸ Seguridad:** descripción de las medidas de seguridad implementadas, como la autenticación de usuarios, el control de acceso y la prevención de inyección SQL.

#### Buenas prácticas

**▸ Mantén la documentación actualizada:** actualiza la documentación cada vez que realices cambios en el código o en la base de datos.

**▸ Utiliza un lenguaje claro y conciso:** escribe la documentación de forma clara y concisa, utilizando un lenguaje que sea fácil de entender para otros desarrolladores. **▸ Documenta el código a medida que lo escribes:** no dejes la documentación para el final. Documenta el código a medida que lo escribes para evitar que se te olvide la lógica o el propósito de las funciones.

**▸ Utiliza un formato consistente:** utiliza un formato consistente para la documentación para facilitar la lectura y el mantenimiento.

#### Ejemplo de documentación con PHPDoc

<?php

/**

- Esta función conecta a la base de datos.

*

- @param string $servername Nombre del servidor de la base de datos.

- @param string $username Nombre de usuario de la base de datos.

- @param string $password Contraseña de la base de datos.

- @param string $dbname Nombre de la base de datos.

- @return mysqli Objeto mysqli que representa la conexión.

- @throws Exception Si la conexión falla.

*/

function conectar_a_la_base_de_datos($servername, $username, $password, $dbname) { // ... código para conectar a la base de datos ...

}

?>

Una buena documentación es fundamental para el éxito de cualquier proyecto de

desarrollo de *software.* Al documentar adecuadamente el código y la base de datos, facilitaremos el desarrollo, el mantenimiento y la colaboración de distintas personas del equipo, además nos aseguraremos que la aplicación sea robusta y confiable.

# The PHP Group. (s. f.). MySQL Improved Extension.

# [https://www.php.net/manual/en/book.mysqli.php](https://www.php.net/manual/en/book.mysqli.php)

# PHP Manual - MySQLi

Este recurso es la documentación oficial de la extensión MySQLi de PHP. Aquí encontrarás información detallada sobre las funciones, clases y métodos disponibles para interactuar con bases de datos MySQL. Es fundamental para comprender la sintaxis, los parámetros y el uso correcto de las funciones de MySQLi.

Implantación de Aplicaciones Web 47 Tema 10. A fondo

# The PHP Group. (2023). PHP Data Objects.

# [https://www.php.net/manual/en/book.pdo.php](https://www.php.net/manual/en/book.pdo.php)

# PHP Manual - PDO

Similar al recurso anterior, esta es la documentación oficial de la extensión PDO de PHP. Aquí encontrarás información completa sobre cómo usar PDO para conectarte a diferentes bases de datos, ejecutar consultas preparadas, manejar transacciones y más. Es esencial para comprender la flexibilidad y las ventajas de seguridad que ofrece PDO.

Implantación de Aplicaciones Web 48 Tema 10. A fondo

# OWASP Foundation. (s. f.). SQL Injection. <https://owasp.org/www->

# community/attacks/SQL_Injection

# OWASP - SQL Injection

OWASP (Open Web Application Security Project) es una organización sin fines de lucro dedicada a mejorar la seguridad de las aplicaciones web. Su página sobre inyección SQL explica en detalle este tipo de ataque, sus riesgos y cómo prevenirlo. Este sitio es crucial para comprender la importancia de la seguridad y las mejores prácticas para proteger las aplicaciones web.

Implantación de Aplicaciones Web 49 Tema 10. A fondo

# Entrenamiento 1

**▸ Planteamiento del ejercicio:** crea un *script* PHP que se conecte a una base de datos MySQL llamada " tienda_online " usando PDO, implementando medidas de seguridad para proteger las credenciales de acceso.

**▸ Desarrollo paso a paso.**

- Define las credenciales de acceso: almacena las credenciales (host, nombre de usuario, contraseña, nombre de la base de datos) en variables de entorno o en un archivo de configuración separado.

- Crea una instancia de PDO: utiliza la clase PDO para crear un nuevo objeto de conexión, pasando las credenciales como parámetros.

- Configura el manejo de errores: utiliza el método setAttribute() de PDO para configurar el modo de error a excepción ( PDO::ERRMODE_EXCEPTION ).

- Maneja las excepciones: utiliza un bloque try...catch para capturar y manejar las posibles excepciones que puedan ocurrir durante la conexión.

**▸ Solución.**

<?php

// Obtener las credenciales de las variables de entorno

$host = getenv('DB_HOST');

$dbname = getenv('DB_NAME');

$username = getenv('DB_USERNAME');

$password = getenv('DB_PASSWORD');

try { $conn = new PDO("mysql:host=$host;dbname=$dbname", $username, $password); $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION); echo "Conexión exitosa"; } catch(PDOException $e) { echo "Error de conexión: " . $e->getMessage(); } ?>

# Entrenamiento 2

**▸ Planteamiento del ejercicio:** crea un *script* PHP que inserte un nuevo producto en la tabla " productos " de la base de datos "tienda online". La tabla tiene las siguientes columnas: id (autoincremental), nombre, descripción, precio.

**▸ Desarrollo paso a paso.**

- Conéctate a la base de datos: reutiliza el código del entrenamiento 1 para conectarte a la base de datos.

- Define los datos del producto: crea variables para almacenar los datos del nuevo producto (nombre, descripción, precio).

- Crea la consulta SQL: escribe una consulta SQL INSERT INTO para insertar los datos del producto en la tabla " productos ".

- Prepara la consulta: utiliza el método prepare() de PDO para preparar la consulta SQL.

- Vincula los parámetros: utiliza el método bindParam() para vincular los valores de las variables a los parámetros de la consulta.

- Ejecuta la consulta: utiliza el método execute() para ejecutar la consulta preparada.

**▸ Solución:**

<?php

// ... (código de conexión del entrenamiento 1) ...

// Datos del producto

$nombre = "Camiseta";

$descripcion = "Camiseta de algodón";

$$$precio = 15.99;$$

try {

$$$sql = "INSERT INTO productos (nombre, descripcion, precio)$$

VALUES (:nombre, :descripcion, :precio)";

$stmt = $conn->prepare($sql);

$stmt->bindParam(':nombre', $nombre);

$stmt->bindParam(':descripcion', $descripcion);

$stmt->bindParam(':precio', $precio);

$stmt->execute();

echo "Nuevo producto insertado con éxito"; } catch(PDOException $e) { echo "Error al insertar el producto: " . $e->getMessage(); } ?>

# Entrenamiento 3

**▸ Planteamiento del ejercicio:** crea un *script* PHP que recupere todos los productos de la tabla " productos " y los muestre en una tabla HTML.

**▸ Desarrollo paso a paso.**

- Conéctate a la base de datos: reutiliza el código del entrenamiento 1.

- Crea la consulta SQL: escribe una consulta SQL SELECT para obtener todos los productos de la tabla " productos ".

- Ejecuta la consulta: utiliza el método query() de PDO para ejecutar la consulta.

- Recorre los resultados: utiliza un bucle foreach para recorrer los resultados de la consulta.

- Genera la tabla HTML: crea una tabla HTML con los encabezados correspondientes y muestra los datos de cada producto en una fila.

**▸ Solución:**

<?php

// ... (código de conexión del entrenamiento 1) ...

try {

$sql = "SELECT * FROM productos";

$$$stmt = $conn->query($sql);$$

echo "<table>";

echo "<tr><th>ID</th><th>Nombre</th><th>Descripción</th><th>Precio</th></tr>";

foreach ($stmt as $row) {

echo "<tr>"; echo "<td>" . $row['id'] . "</td>"; echo "<td>" . $row['nombre'] . "</td>"; echo "<td>" . $row['descripcion'] . "</td>"; echo "<td>" . $row['precio'] . "</td>"; echo "</tr>"; } echo "</table>"; } catch(PDOException $e) { echo "Error al obtener los productos: " . $e->getMessage(); }

?>

# Entrenamiento 4

**▸ Planteamiento del ejercicio:** crea un *script* PHP que actualice el precio de un producto específico en la tabla " productos ".

**▸ Desarrollo paso a paso:**

- Conéctate a la base de datos: reutiliza el código del entrenamiento 1.

- Define el nuevo precio y el ID del producto: crea variables para almacenar el nuevo precio y el ID del producto que se va a actualizar.

- Crea la consulta SQL: escribe una consulta SQL UPDATE para actualizar el precio del producto en la tabla " productos ", utilizando una cláusula WHERE para especificar el ID del producto.

- Prepara la consulta: utiliza el método prepare()

de PDO.

- Vincula los parámetros: utiliza el método bindParam() para vincular los valores de las variables a los parámetros de la consulta.

- Ejecuta la consulta: utiliza el método execute()

**▸ Solución:**

<?php

// ... (código de conexión del entrenamiento 1) ...

// Nuevo precio y ID del producto

$$$nuevo\_precio = 19.99;$$

$$$id\_producto = 1;$$

try {

para ejecutar la consulta preparada.

$sql = "UPDATE productos SET precio = :precio WHERE id = :id";

$stmt = $conn->prepare($sql);

$stmt->bindParam(':precio', $nuevo_precio);

$stmt->bindParam(':id', $id_producto);

$stmt->execute();

echo "Precio del producto actualizado con éxito"; } catch(PDOException $e) { echo "Error al actualizar el precio del producto: " . $e->getMessage(); }

?>

# Entrenamiento 5

**▸ Planteamiento del ejercicio:** crea un *script* PHP que elimine un producto específico de la tabla " productos ".

**▸ Desarrollo paso a paso:**

- Conéctate a la base de datos: reutiliza el código del entrenamiento 1.

- Define el ID del producto: crea una variable para almacenar el ID del producto que se va a eliminar.

- Crea la consulta SQL: escribe una consulta SQL DELETE para eliminar el producto de la tabla " productos " utilizando una cláusula producto.

- Prepara la consulta: utiliza el método prepare()

WHERE para especificar el ID del

de PDO.

- Vincula los parámetros: utiliza el método bindParam() para vincular el valor de la variable al parámetro de la consulta.

- Ejecuta la consulta: utiliza el método execute()

**▸ Solución:**

<?php

// ... (código de conexión del entrenamiento 1) ...

// ID del producto a eliminar

$$$id\_producto = 1;$$

try {

$sql = "DELETE FROM productos WHERE id = :id";

para ejecutar la consulta preparada.

$stmt = $conn->prepare($sql);

$stmt->bindParam(':id', $id_producto);

$stmt->execute();

echo "Producto eliminado con éxito"; } catch(PDOException $e) { echo "Error al eliminar el producto: " . $e->getMessage(); }

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–46)*
- Tema 10. Material de estudio  *(pp.5–46)*
- A fondo  *(pp.47–49)*
- Entrenamientos  *(pp.50–59)*
- Implantación de Aplicaciones Web 5 · Implantación de Aplicaciones Web 6 · Implantación de Aplicaciones Web 7 · Implantación de Aplicaciones Web 9 · Implantación de Aplicaciones Web 10 · Implantación de Aplicaciones Web 11 · Implantación de Aplicaciones Web 12 · Implantación de Aplicaciones Web 13 · Implantación de Aplicaciones Web 14 · Implantación de Aplicaciones Web 15 · Implantación de Aplicaciones Web 16 · Implantación de Aplicaciones Web 17 · Implantación de Aplicaciones Web 18 · Implantación de Aplicaciones Web 19 · Implantación de Aplicaciones Web 20 · Implantación de Aplicaciones Web 21 · Implantación de Aplicaciones Web 22 · Implantación de Aplicaciones Web 23 · Implantación de Aplicaciones Web 24 · Implantación de Aplicaciones Web 25 · Implantación de Aplicaciones Web 26 · Implantación de Aplicaciones Web 27 · Implantación de Aplicaciones Web 28 · Implantación de Aplicaciones Web 29 · Implantación de Aplicaciones Web 30 · Implantación de Aplicaciones Web 31 · Implantación de Aplicaciones Web 32 · Implantación de Aplicaciones Web 33 · Implantación de Aplicaciones Web 34 · Implantación de Aplicaciones Web 35 · Implantación de Aplicaciones Web 36 · Implantación de Aplicaciones Web 38 · Implantación de Aplicaciones Web 39 · Implantación de Aplicaciones Web 40 · Implantación de Aplicaciones Web 41 · Implantación de Aplicaciones Web 42 · Implantación de Aplicaciones Web 43 · Implantación de Aplicaciones Web 44 · Implantación de Aplicaciones Web 45 · Implantación de Aplicaciones Web 46  *(pp.5, 6, 7, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 38, 39, 40, 41, 42, 43, 44, 45, 46)*
- Implantación de Aplicaciones Web 50 Tema 10. Entrenamientos · Implantación de Aplicaciones Web 51 Tema 10. Entrenamientos · Implantación de Aplicaciones Web 52 Tema 10. Entrenamientos · Implantación de Aplicaciones Web 53 Tema 10. Entrenamientos · Implantación de Aplicaciones Web 54 Tema 10. Entrenamientos · Implantación de Aplicaciones Web 55 Tema 10. Entrenamientos · Implantación de Aplicaciones Web 56 Tema 10. Entrenamientos · Implantación de Aplicaciones Web 57 Tema 10. Entrenamientos · Implantación de Aplicaciones Web 58 Tema 10. Entrenamientos · Implantación de Aplicaciones Web 59 Tema 10. Entrenamientos  *(pp.50–59)*