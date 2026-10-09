---
asignatura: Sistemas Gestores de Bases de Datos (SGBD)
fecha: 2026-09-28
tema: "Cierre del Tema 1 (cajón de repaso con preguntas reales de examen) + inicio del Tema 2 (objetos de la base de datos, triggers, usuarios y roles)"
fuente: transcripción de la clase en directo
---
# SGBD · Clase (28/09) · Cierre Tema 1 + inicio Tema 2

> Anterior: [Tutoría: instalación de SQL Express, MariaDB y Oracle](2026-09-25_tutoria-instalacion-sgbd.md) · Siguiente: [Tema 2: repaso DDL/DML/DCL (05/10)](2026-10-05_tema2-repaso-ddl-dml-dcl.md)

Calendario confirmado en esta clase: quedan los días 05/10, 19/10 y 26/10 para cubrir los temas 2, 3 y 4 de este trimestre (no hay clase los días 02/11 y 09/11 por el simulacro del 23/11).

## El cajón del Tema 1, lanzado con preguntas reales
César lanzó el cajón de preguntas del Tema 1 en clase (modo "tarjeta" con colores). **Importante para estudiar**: confirmó explícitamente que *"cualquier pregunta que os salga de tipo test en el examen de mayo va a salir de este test"* — es decir, el cajón de cada tema es literalmente el banco de donde sale el examen. Preguntas lanzadas y su respuesta correcta (quedan documentadas porque son examinables):
- **¿Qué significan las siglas SGBD?** → Sistema(s) de Gestión de Base(s) de Datos.
- **¿Cuál es el objetivo principal de un sistema de gestión de datos?** → Gestionar, almacenar y controlar los datos.
- **¿Cuántos niveles define la arquitectura ANSI/SPARC?** → 3.
- **¿Qué nivel de la arquitectura ANSI/SPARC describe la vista de usuarios?** → Externo.
- **¿Qué ventaja ofrece la arquitectura ANSI/SPARC?** → Independencia entre los niveles de datos (no reducción de tamaño, ni estética, ni más consultas).
- **¿Cuál de los siguientes SGBD es comercial?** → Oracle (frente a MariaDB/PostgreSQL, que son libres).
- **¿Cuál de los siguientes SGBD es libre?** → MySQL/PostgreSQL.
- **¿Qué función realiza el DBA (Database Administrator) con los permisos de acceso?** → Controla y asigna privilegios a los usuarios (no diseña la estructura, no crea informes, no administra sistemas operativos — distractor importante).
- **¿Qué parámetro es importante configurar al instalar el SGBD?** → La memoria caché (no el idioma, ni la interfaz, ni el tamaño de escritorio).
- **¿Qué componente del sistema operativo se relaciona directamente con el SGBD?** → El **sistema de ficheros** (no el firewall — distractor, el firewall es un elemento que se integra pero no es del sistema operativo en sí).
- **¿En qué se caracteriza la arquitectura de 2 capas?** → Marcada explícitamente por el profesor como **la pregunta más confusa y la que con más probabilidad cae en el examen**: la respuesta correcta es la **separación entre cliente y servidor** (no "la comunicación entre el cliente y la base de datos", que es la opción con la que más alumnos fallaron).
- **¿Qué es una instancia de base de datos?** → Un entorno operativo donde se gestiona una base de datos (no un archivo de respaldo, ni un conjunto de tablas, ni un lote de auditoría). Truco mencionado por un alumno y validado por el profesor: en preguntas tipo test cuando no se sabe la respuesta, probar con la opción más larga/completa.
- **¿Para qué sirve un diccionario de datos?** → Es un documento (tipo XML) que documenta la estructura de la base de datos y del fichero con el que se trabaja — todas las etiquetas que definen esa estructura. Concepto que tendrá más sentido cuando se vea Redis (que usa una estructura de diccionario similar).
- **¿Cuál es la función principal de los ficheros log?** → Registrar transacciones (no controlar permisos, no almacenar copias, no guardar estructura de tablas).
- **¿Qué nivel de la arquitectura ANSI/SPARC guarda el almacenamiento físico de los datos?** → Interno.

## Arquitectura cliente-servidor, aclarada con una demo en directo (confusión real en clase)
Varios alumnos (María Eugenia entre ellos) se confundieron con el concepto. César lo explicó con una demostración práctica paso a paso:
- Un **servidor** de base de datos no tiene normalmente interfaz visual propia — es un **servicio/demonio que corre por debajo** del sistema operativo, sin ventana. Lo demostró intentando buscar "SQL Server" como si fuera una aplicación en el navegador/menú de inicio: no aparece como programa porque no lo es, es una capa de servicio.
- El **cliente** (DBeaver, SSMS, phpMyAdmin, o incluso el modo comando `sqlcmd`/`mysql`) es la **herramienta visible** a través de la cual accedemos al servidor para consultar y manipular los datos.
- Demostración en modo comando (la forma "más básica que existe" de cliente, sin interfaz gráfica): `sqlcmd -S localhost\SQLEXPRESS`, luego `SELECT name FROM sys.databases; GO` — mostró el listado de bases de datos exactamente igual que aparecería en DBeaver.
- Conclusión remarcada: **da igual la herramienta** (modo comando, DBeaver, SSMS, phpMyAdmin) — la sentencia que se lanza es la misma; lo que cambia ligeramente es la interfaz, nunca el concepto de fondo (servidor que gestiona + cliente que accede).
- Nomenclatura jerárquica de acceso a un dato concreto: `servidor.basededatos.esquema.tabla` — comparado con la notación de referencia entre hojas de Excel (`fichero.hoja.celda`).

## Tema 2: los objetos de una base de datos (arranque)
Tema 2 = "acceso a la información": cómo se manipulan los datos usando los 3 lenguajes ya vistos (DDL/DML/DCL). Punto de partida: una base de datos relacional se compone de **objetos**. Los 3 más importantes:
- **Tablas**: la estructura real donde se almacena la información (filas y columnas, como una hoja Excel). En bases de datos no relacionales el concepto "tabla" existe pero con otro nombre — ejemplo dado: **MongoDB** (Tema 6 o 7) guarda la información en documentos **JSON**, una estructura mucho más flexible (no todas las filas necesitan tener todos los campos).
- **Índices**: permiten identificar cada fila de forma unívoca y acceder rápido a la información (analogía: el índice de un libro). El más simple es el **ID autoincremental** (cada fila nueva recibe automáticamente el siguiente número; si se borra una fila, el hueco no se reutiliza, se sigue incrementando). Dato importante de compatibilidad: **SQL Server Express no reconoce el comando `AUTO_INCREMENT`** de MariaDB — en SQL Server el equivalente es `IDENTITY(1,1)` (valor inicial 1, incremento de 1 en 1). Otras veces el índice es un valor propio con sentido de negocio (DNI para personas, número de factura para facturas). Los índices son la forma en que se **relacionan tablas entre sí** (clave foránea apuntando al índice/ID de otra tabla), evitando duplicar toda la información de una tabla en otra.
- **Vistas**: una composición de columnas de distintas tablas, pensada para mostrar o imprimir información combinada (ejemplo dado: un albarán de recogida en una tienda tipo IKEA, que junta nombre del cliente, producto, precio y estantería desde varias tablas distintas a partir de un simple ID de producto). Las vistas son "una evolución a pequeña escala de un trigger": `CREATE VIEW`, `ALTER VIEW`, `DROP VIEW` son del lenguaje DDL porque una vista es un contenedor (no almacena datos propios).

Otros objetos menos críticos pero mencionados: **sinónimos** (alias de una tabla para referirse a ella con un nombre más corto/cómodo), **secuencias** (valores únicos tipo marca temporal, útiles para evitar colisiones cuando dos usuarios acceden simultáneamente), **tablespace** (ubicación física de los ficheros de almacenamiento; en bases no relacionales se llama simplemente "space").

## Triggers, funciones y procedimientos almacenados: diferencias
Los 3 son "código de programación que se puede lanzar en la base de datos", pero con un matiz importante que preguntó un alumno (Francisco) y que César marcó como relevante:
- **Función** / **procedimiento almacenado**: un trozo de código reutilizable (mismo concepto que una función en programación orientada a objetos) que se **invoca explícitamente** cuando se necesita (p. ej. una rutina de copia de seguridad de 25 líneas que se llama con un solo nombre en vez de repetir el código cada vez).
- **Trigger** (disparador): un trozo de código que queda **permanentemente activo** en el sistema y se ejecuta automáticamente cuando ocurre un evento concreto (INSERT, UPDATE, DELETE) — no hace falta invocarlo, se dispara solo.
- Ejemplo de trigger desarrollado en clase para trazabilidad: cada vez que hay un `INSERT` en la tabla `pedido`, el trigger copia automáticamente ese registro en una tabla histórica `historico_pedidos`, añadiendo quién hizo el pedido y cuándo. Lo mismo para el detalle del pedido. Esto es clave para auditorías de calidad (ISO 9001): si un día preguntan "¿quién borró este documento y cuándo?", se consulta la tabla de trazabilidad en vez de no poder responder.
- Estructura pseudocódigo de un trigger (se desarrollará en el Tema 3): *"cuando ocurre [INSERT/UPDATE/DELETE] en la tabla X, ejecuta [acción]"*.

## Usuarios, permisos, roles y perfiles
- **Usuario**: cuenta individual que accede a la base de datos.
- **Permiso**: puede asignarse directamente al usuario o, de forma más correcta y habitual, a través de un **rol** o **perfil**.
- Distinción importante entre **perfil** y **rol** que remarcó el profesor (pueden confundirse si tienen el mismo nombre):
  - **Perfil** = conjunto de **recursos** (p. ej. "este perfil de administrador solo puede estar conectado 2 horas al día").
  - **Rol** = conjunto de **permisos** sobre objetos concretos (p. ej. "este rol puede leer esta tabla, escribir en esta otra, no puede acceder a aquella").
  - Aunque se llamen igual ("administrador"), perfil y rol controlan cosas administrativamente distintas: uno limita recursos, el otro asigna permisos.

## Deberes / cierre
Tener DBeaver instalado para el lunes siguiente (05/10), donde se empezaría a trastear en directo con acceso a los datos (DDL/DML práctico).
