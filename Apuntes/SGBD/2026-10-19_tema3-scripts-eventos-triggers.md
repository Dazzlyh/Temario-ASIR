---
asignatura: Sistemas Gestores de Bases de Datos (SGBD)
fecha: 2026-10-19
tema: Tema 3 · Automatización de tareas — Scripts, eventos y triggers (disparadores)
fuente: transcripción de la clase en directo
---
# SGBD · Tema 3: Scripts, eventos y triggers (19/10)

> Anterior: [Tema 2: repaso DDL/DML/DCL (05/10)](2026-10-05_tema2-repaso-ddl-dml-dcl.md) · Profesor: César Carrión

## Logística al inicio de clase

- **Actividad 1 (Tema 2)**: pendiente de entrega. César aclaró varios puntos:
  - No hace falta que todo se ejecute realmente; si algún comando falla por limitaciones del motor instalado (p. ej. una versión de SQL Server Express que no permite crear roles, o diferencias entre MariaDB y MySQL), vale con explicar la parte en forma de **marco teórico** (qué sentencia se usaría y para qué sirve) en vez de la ejecución y captura real.
  - Entrega recomendada: documento con introducción, explicación de las sentencias usadas, capturas de pantalla de los resultados y, si es posible, un fichero `.sql` aparte con las instrucciones (puede ir también embebido dentro del Word si no se genera aparte). No hace falta un documento extenso.
  - Se puede usar IA (ChatGPT, Claude, Copilot...) para apoyarse en la actividad — el profesor fue explícito en que **no le importa** que se use, porque lo que evalúa es la comprensión demostrada, no que la sentencia esté escrita de memoria.
  - El objetivo de la actividad es: crear una base de datos con una estructura inventada, crear vistas, asignar roles con `GRANT`/`REVOKE`, crear grupos de usuarios (admin, analista, etc.) y asignar roles.
  - El repaso práctico de esta actividad y de ejercicios de ejecución del Tema 2 se hará el **viernes** (23/10) en el laboratorio.

- **Calendario de la asignatura**: solo quedan 2 clases de SGBD este trimestre contando con la de hoy (19/10) y la de la semana que viene. El Tema 3 se ve íntegramente hoy, y la semana que viene se pasará directamente al **Tema 4** (transacciones).
- El cuestionario tipo test (Kahoot) del Tema 3 se lanzará el **viernes** (23/10), junto con el repaso práctico del Tema 2; el profesor siempre sube el material y el Kahoot a la plataforma después.
- Dudas de tutoría individual (ejemplo con un alumno, Manuel): el profesor ofrece huecos de tutoría por la mañana entre clases, compartiendo el enlace de la sala por correo.

## Introducción al Tema 3: scripts, automatización y por qué es "la parte más compleja" de la asignatura

César marcó el Tema 3 como, en su opinión, el más complejo de la asignatura — no por la dificultad conceptual en sí, sino por la variedad de formas de ejecutar ciertos elementos (triggers y su funcionalidad) según el motor de base de datos.

- **Script / guión**: una secuencia de sentencias SQL concadenadas con un fichero de ejecución. En los apuntes aparece traducido como "guión", aunque en la práctica casi nadie usa ese término y se habla directamente de *script*.
- **Trigger**: en español, la palabra correcta es **disparador** (apuntado en clase por una alumna, María Eugenia González). También se usan términos como "actuador" o "lanzador", pero lo habitual es quedarse con el anglicismo.
- El objetivo real del tema **no es memorizar sintaxis de scripting**, sino entender **automatización de tareas**: de qué forma se automatizan procesos sobre la base de datos y cómo esa automatización lanza tareas sobre ella. Esto es, según el profesor, la base de lo que significa "administración de sistemas de gestión de bases de datos".
- Cada motor tiene su propio lenguaje de scripting (todos parten de una base SQL común, pero con matices): no es objetivo del curso saberlos todos de memoria, sino entender **cómo se construye un script** y **cómo funcionan los triggers**, en términos generales y transferibles entre motores.

### Excepciones: por qué existen y quién las controla

Las excepciones son la forma en que cualquier lenguaje de programación controla los errores de ejecución (p. ej. una división por 0, o tratar un string como si fuera un número). Sin excepciones, el sistema "cascaría" (fallaría sin control) ante cualquier error, y se podría capturar el error y mostrar un mensaje alternativo en vez de romper la ejecución.

**Pregunta de un alumno (Jose Alejandro)**: ¿cuál es la diferencia entre controlar las excepciones a nivel de base de datos (motor) o a nivel de código (aplicación)? Respuesta del profesor:
- Es una cuestión de **ámbito de actuación**, no de "ventaja" de una sobre otra.
- Como administradores de sistemas, normalmente **no se tiene acceso al código de la aplicación** (eso es responsabilidad de quien la desarrolla), así que el control de excepciones que corresponde al DBA es el que ocurre **en los scripts propios contra la base de datos**: tareas de optimización, monitorización y chequeo (p. ej. errores al hacer un volcado de datos, una fila corrupta, etc.).
- Las excepciones del día a día de una aplicación (un usuario que mete una coma decimal en vez de un punto en un formulario, por ejemplo) son responsabilidad de quien programó esa aplicación, no del administrador de la base de datos.

## Planificación de tareas administrativas: por qué se necesitan scripts

La planificación de tareas administrativas obliga a desarrollar scripts con un listado de ejecuciones que se revisan periódicamente. Tipos de actividades habituales que un administrador automatiza (al margen de lo que haga la propia aplicación):

- **Copias de seguridad**: un script lanzado, por ejemplo, a la una de la mañana. Si la copia falla, capturando la excepción se puede saber por qué no se ha hecho.
- **Mantenimiento de índices**: reorganizar, reconstruir y limpiar índices sobre las tablas.
- **Generación de informes**: estadísticas, tamaño y rendimiento de la base de datos.
- **Actualizaciones, parcheos y otras tareas de limpieza**.

### Caso práctico contado en clase: fichajes de una empresa de fabricación

Ejemplo extenso usado por el profesor (presentado como caso real de su experiencia, sin verificar fuera de la clase): una empresa con sistema de fichajes por actividad (fichar al empezar y terminar cada tarea: barrer, mecanizar un molde, almorzar, etc.) generaba un volumen enorme de registros diarios, multiplicados por el número de operarios y los años acumulados. Cuando las consultas y cálculos empezaban a ir lentos porque arrastraban datos históricos que ya no eran relevantes, la tarea del administrador fue crear un **volcado histórico**: mover los fichajes de años anteriores (p. ej. 2024, 2025) a bases de datos/tablas históricas separadas, teniendo cuidado de **no afectar al cómputo de tareas aún en curso** que arrancaron en un año distinto al actual.

Puntos remarcados:
- **"Cuidado con los borrados"**: lo ideal no es borrar, sino **mover los datos a tablas históricas/de historial**, y recalcular lo que dependa de ellos si hace falta.
- Otro ejemplo citado: tablas con más de 100.000 registros en SQL empiezan a ir lentas porque una consulta recorre (potencialmente) toda la tabla antes de filtrar; esto se agrava si el ancho de banda es limitado (más aún en consultas remotas por Internet), generando transacciones "muy gordas" para resultados sencillos. Ejemplo citado: sistemas de contabilidad con facturas acumuladas desde hace 20+ años sin depurar, que acaban tardando minutos en una simple búsqueda.
- Parte del trabajo del DBA es limpiar lo que el desarrollador de la aplicación no hizo (el desarrollador "se la pela", en palabras del profesor, de si el sistema se satura con el tiempo): eliminar o rellenar `NULL`s, añadir campos tipo `activo` (sí/no) en vez de borrar registros, mover datos, etc. — para dejar la base de datos "más limpia, homogénea y decente".

### Buenas prácticas antes de lanzar un script en producción

- **Entorno de pruebas / sandbox**: hacer un volcado de la base de datos real a un entorno de pruebas y trastear los scripts ahí antes de lanzarlos a producción. Lanzar un script sin probarlo antes en producción es arriesgado ("lo normal es que no funcione bien").
- **Control de versiones** sobre los scripts que se van desarrollando.
- **Programación de la automatización**: mediante `cron` (Linux), scripts `.sh`/Bash, o `.ps1` de PowerShell si se trabaja con Windows/PowerShell — para programar la tarea a la hora deseada.
- **Documento de pruebas**: probar sistemáticamente antes de lanzar (p. ej. probar las facturas, probar tal proceso, etc.), porque un script puede parecer que funciona bien y luego tener comportamiento no esperado que no se llegó a probar.
- **Copia de seguridad antes de la ejecución** del script.
- **Control de manejo de errores** (excepciones).
- **Documentación**: remarcado como algo que "siempre se nos olvida" — documentar con las propias palabras lo que se ha hecho, porque al cabo de un mes nadie (ni uno mismo) recuerda los detalles si no quedó documentado.

### Herramientas de automatización según el motor

Cada motor/gestor tiene su propia herramienta nativa para programar y lanzar scripts:

| Motor | Herramienta de automatización |
|---|---|
| SQL Server | SQL Server Agent |
| Oracle | Oracle Scheduler |
| PostgreSQL | `pg_cron` |
| Sistema (Linux) | `cron` + scripts Bash |
| Sistema (Windows) | PowerShell (`.ps1`) |

## Eventos vs. Triggers: la diferencia clave

- **Evento**: se ejecuta **temporalizado** (en un momento programado).
- **Trigger (disparador)**: se ejecuta **cuando ocurre algo** (una condición/acción concreta lo dispara).

### Eventos: ejemplo de arranque/parada del motor antes de una copia de seguridad

Si se hace una copia de seguridad de la base de datos **con el motor en marcha**, la copia puede quedar corrupta (y por tanto inútil). Por eso, el procedimiento correcto es: parar el motor → hacer la copia → arrancar el motor de nuevo. Esto se puede automatizar en vez de hacerlo manualmente.

Herramientas mencionadas para automatizar copias de seguridad: **Cobian** (software que se instala para programar copias de seguridad y tareas) — se verá también en SAD (Seguridad y Alta Disponibilidad) con el profesor Damián.

Comandos para arrancar/parar el servicio del motor:
- En Windows/consola de comandos: `net start <servicio SQL Server>` / `net stop <servicio SQL Server>`.
- En PowerShell, ejemplo de evento sencillo:

```powershell
# Evento de arranque del motor (PowerShell)
Write-Output "Iniciando..."
Start-Service <nombre_del_servicio_SQL>
```

En PowerShell, cada variable se marca con `$`. El resultado del `Start-Service` genera un mensaje de éxito o fallo (variable booleana del tipo "se pudo hacer" / "no se pudo hacer").

### Otros tipos de eventos mencionados

- **Autorización/no autorización de conexión a un servicio**: en Linux, por ejemplo, un `kill` sobre el proceso correspondiente.
- **Transacciones** (se verá en detalle en el Tema 4): ejemplo de una transferencia bancaria con varias operaciones encadenadas — 2 `UPDATE` (restar de una cuenta, sumar a otra) + 1 `INSERT` (registrar la transacción). Si cualquiera de las 3 falla, se necesita un **ROLLBACK** para devolver el sistema a su estado inicial.

## Triggers en profundidad

Un trigger se puede lanzar contra:
- **Tablas**, ante eventos de tipo DML: `INSERT`, `UPDATE` o `DELETE` — especificando si se dispara `AFTER` (después) o `BEFORE` (antes) de la operación.
- **Vistas**: por ejemplo, cada vez que se consulta una vista, actualizar un valor en otra tabla (p. ej. un contador de consultas).
- **El sistema**: p. ej. ante sentencias de tipo DCL (`GRANT`, `REVOKE`), registrar en una tabla propia cuándo y a qué usuario se le han dado permisos — útil para detectar intentos de hackeo o cambios de contraseña no autorizados.

### Estructura básica de un trigger (la "trampa" más importante del tema)

El profesor remarcó esta tabla/estructura como la más importante para el examen — más que cualquier sintaxis exacta de un motor concreto:

| Elemento | Qué indica |
|---|---|
| `CREATE TRIGGER` | Creación del disparador |
| `ON <tabla/vista>` | A qué objeto se asocia |
| `AFTER` / `BEFORE` + evento (`INSERT`/`UPDATE`/`DELETE`) | Cuándo se ejecuta |
| `BEGIN ... END` | Qué ocurre cuando se dispara |

Ejemplo usado en clase, trigger sobre una tabla de pedidos (reconstrucción de la explicación oral, no dictado carácter a carácter):

```sql
-- Al insertar un pedido, lo marca automáticamente como "en proceso"
CREATE TRIGGER trg_pedido_insertado
ON pedidos
AFTER INSERT
AS
BEGIN
    UPDATE pedidos
    SET estado = 'en proceso'
    WHERE id_pedido = (SELECT id_pedido FROM inserted);
END;
```

El profesor reconoció que, en este caso concreto, sería más sencillo meter el estado directamente en el propio `INSERT`, pero lo dejó así porque es un **ejemplo didáctico** de la estructura, no la forma óptima de resolverlo.

Sobre el nivel de exigencia en el examen: César fue explícito en que **no va a preguntar código exacto** ("si se te olvida una coma, un punto y coma, o escribes *Foreing* en vez de *Foreign*, me da igual"). Lo que importa es demostrar que se entiende la estructura (`CREATE`, `ON`, `AFTER`/`BEFORE`, `BEGIN...END`) y saber explicarla con palabras propias, no recitarla de memoria. En el examen puede aparecer de dos formas: que pidan escribir (a grandes rasgos) un trigger, o que den un trigger ya escrito y haya que explicar qué hace — y el profesor apuntó que probablemente sea esta segunda opción.

### Anécdota del profesor: el trigger que detectaba fichajes "demasiado perfectos"

**Anécdota personal no verificable, contada como ejemplo**: en una empresa donde trabajó, el sistema de fichaje por tarjeta permitía, en aquella época, acceder directamente a la tabla de fichajes y modificarla manualmente (la base de datos no estaba protegida). Un empleado fichaba todos los días exactamente a las 8:23, algo que resultaba sospechoso para administración (el profesor señaló que lo normal es tener cierta variación: 8:21, 8:23, 8:25...). El profesor montó un trigger que, cada vez que se modificaba manualmente el registro de fichaje, marcaba automáticamente un campo como "modificado manualmente" (con una "X"). Esto no impidió el comportamiento, pero permitió detectarlo y hablarlo directamente con la persona implicada.

### Trigger de registro de eventos (log genérico de inserciones)

Ejemplo mostrado para ilustrar un trigger asociado **a toda la base de datos** (no a una tabla concreta), que salta ante cualquier `INSERT`:

```sql
-- Trigger simplificado de registro de eventos (ejemplo didáctico, nivel servidor/BD)
CREATE TRIGGER trg_registro_eventos
ON DATABASE
FOR INSERT
AS
BEGIN
    DECLARE @fecha DATETIME;
    SET @fecha = GETDATE();

    INSERT INTO registro_eventos (fecha)
    VALUES (@fecha);
END;
```

El propio profesor señaló que este ejemplo es intencionadamente simplista ("vaya castaña de disparador") y que, en un registro de eventos real y útil, también se debería guardar: **quién** hizo la acción (usuario), **a qué hora**, la **dirección IP**, la **sentencia completa ejecutada** y, si es posible, el **valor anterior** de lo modificado — para tener trazabilidad completa de qué se hizo, cómo y cuándo.

#### Pregunta de un alumno (Francisco Haldón) sobre la seguridad de estos registros

¿Cómo evitar que alguien con conocimiento del sistema manipule o borre esos registros de auditoría? Respuesta del profesor:
- Lo básico: no compartir usuario y contraseña con privilegios de administración salvo necesidad real.
- Su recomendación habitual: tener un **servidor de logs independiente y aislado en una red separada/oculta** (sin acceso directo desde la red normal), al que solo se accede mediante el trigger que inserta el registro remotamente. Así, aunque alguien comprometa la base de datos principal, no tiene visibilidad ni acceso directo al servidor de logs.
- Esto se relaciona con el concepto de **subnetting** (contenido que se ve en la asignatura de Seguridad y Alta Disponibilidad, en torno al Tema 4-6 según el propio profesor).
- **Anécdota no verificable** contada como ilustración: el profesor mencionó haber salvado a una empresa de un ataque de ransomware gracias a tener un equipo de copias de seguridad oculto fuera de la red principal; y otra anécdota (sin verificar) de una empresa que estuvo hackeada durante años (con mensajes/banderas insertados en el sistema) sin darse cuenta, por no tener monitorización adecuada.

### Conexión/desconexión de usuarios: ejemplo con `@@SPID`

Ejemplo de trigger/script para registrar cuándo se conecta o desconecta un usuario (útil para detectar accesos sospechosos, p. ej. fuera de horario de oficina, lo que puede indicar una cuenta comprometida por phishing):

- Se consulta la sesión del usuario a través de su identificador de proceso: **`@@SPID`** (en SQL Server, identifica el proceso/demonio en ejecución asociado a la sesión del usuario).
- Para forzar la desconexión (matar la sesión) se ejecuta una sentencia dinámica contra ese `SPID`.

### `BEGIN TRY` / `BEGIN CATCH`: la segunda "trampa" importante del tema

La otra estructura que el profesor remarcó como posible pregunta de examen:

```sql
BEGIN TRY
    -- sentencia(s) que se intenta ejecutar, p. ej. un INSERT
    INSERT INTO ...
END TRY
BEGIN CATCH
    -- captura del error si algo falla en el TRY
    -- p. ej. devolver un mensaje por pantalla
END CATCH
```

De nuevo, lo importante no es la sintaxis exacta sino entender el concepto: un bloque `TRY` que intenta ejecutar algo, y un bloque `CATCH` que captura la excepción si falla, evitando que el sistema se rompa sin control.

## Consultas dinámicas (SQL dinámico)

Concepto marcado como otra "trampa" de examen importante.

- **Sentencia SQL estática**: el código SQL está fijo y escrito de antemano; siempre hace lo mismo (mismo número de campos, mismas tablas).
- **Sentencia SQL dinámica**: la sentencia se **recompone en tiempo de ejecución** en función de variables — puede cambiar el número de campos seleccionados, el nombre de la tabla sobre la que se consulta, los filtros aplicados, etc. Los componentes se generan en tiempo de ejecución, no están fijados de antemano (comparado en clase con pasar un parámetro distinto a un mismo método/constructor en programación orientada a objetos).

Aclaración importante hecha en clase (a raíz de una pregunta/ejemplo): una consulta con un simple filtro variable (p. ej. filtrar facturas por cliente/mes/año) **no es necesariamente** "dinámica" en este sentido — sigue siendo la misma sentencia con un parámetro de filtro. Lo que convierte una consulta en dinámica es que **la propia estructura de la sentencia cambia** (más o menos campos devueltos, o el nombre de la tabla consultada cambia).

### Ejecución de SQL dinámico: `EXEC`

Ejemplo de construcción y lanzamiento de una consulta dinámica (reconstrucción de la explicación oral):

```sql
-- Construcción de una consulta dinámica
DECLARE @consulta NVARCHAR(MAX);
SET @consulta = 'SELECT * FROM productos WHERE iva = 21';

EXEC(@consulta);
```

Si la sentencia está almacenada como procedimiento en el servidor, se lanza con `sp_executesql`; si forma parte de la línea de ejecución de un trigger, se usa `EXEC`. En el fondo es el mismo principio: una variable que contiene la sentencia más los valores que la completan, de forma que cada ejecución puede dar un resultado distinto.

### Ejemplo con nombre de tabla variable

Otro caso de consulta dinámica mostrado: el **nombre de la tabla** es la propia variable (por ejemplo, para consultar datos segmentados por año: `empleados`, `empleados2016`, `empleados2017`...). El procedimiento siempre es el mismo; lo que cambia es la tabla sobre la que se ejecuta — equivalente a pasar un parámetro distinto a un mismo método.

### Utilidad del SQL dinámico (posible pregunta de examen)

El profesor remarcó que esta pregunta ("¿qué es una consulta dinámica? ¿para qué sirve?") sí puede salir en el examen, con estas ventajas como respuesta esperada:
- **Reutilización de código** / programación.
- **Adaptabilidad**.
- **Rendimiento**.
- **Flexibilidad**.

## Nota aparte: qué es un "fetch" (aclaración puntual, no entra en examen)

A raíz de una referencia que hizo el profesor (el término viene de JavaScript, según él mismo aclaró que no hace falta saberlo), explicó brevemente el concepto por curiosidad, sin que vaya a preguntarse: un `fetch` es una consulta/petición de información contra un servidor, que puede estar en 3 estados: ejecutándose (estatus 0), ejecutado correctamente, o ejecutado con error/sin respuesta. Lo comparó con los códigos de respuesta HTTP típicos: **200** (OK), **404** (no encontrado — el "Ups" de Amazon cuando no hay conexión), **500** (error de servidor/conexión).

## Lenguajes de scripting y herramientas cliente por motor

Cada motor tiene su propio lenguaje para programar triggers/eventos/procedimientos (todos parten de SQL, pero con sintaxis distinta):

| Motor | Lenguaje de scripting | Herramienta cliente típica |
|---|---|---|
| SQL Server | **T-SQL** (Transact-SQL) | SSMS (SQL Server Management Studio) |
| Oracle | **PL/SQL** | SQL Developer |
| PostgreSQL | **PL/pgSQL** | pgAdmin |
| MySQL/MariaDB | — | MySQL Workbench (herramienta más antigua, aún en uso) |
| Sistema (automatización general) | Bash / PowerShell (`.ps1`) | — |

El profesor insistió varias veces en que **no va a preguntar por la sintaxis específica de ningún lenguaje concreto** (T-SQL vs PL/SQL vs PL/pgSQL) — lo único relevante de cara al examen es tener claro que **cada base de datos tiene su propio lenguaje**, y entender los conceptos generales (estructura de un trigger, try/catch, SQL dinámico) que son transferibles entre motores.

El cuestionario tipo test (Kahoot) de este tema ya está preparado y se lanzará el viernes junto con el material subido a la plataforma.

## Para llevar a casa

- El Tema 3 trata de **automatización de tareas** sobre la base de datos mediante **scripts**: temporizados (**eventos**) o condicionados a una acción (**triggers/disparadores**), con control de errores mediante excepciones y, opcionalmente, sentencias dinámicas.
- En el examen de mayo, como mucho habrá **3 preguntas** de este tema, y **no se pedirá sintaxis exacta de código**: lo que se evalúa es comprender y explicar con palabras propias.
- Las **dos estructuras clave** a saber explicar de memoria (conceptualmente, no carácter a carácter):
  1. Estructura de un trigger: `CREATE TRIGGER ... ON <tabla/vista> AFTER/BEFORE <evento> AS BEGIN ... END`.
  2. Captura de excepciones: `BEGIN TRY ... END TRY BEGIN CATCH ... END CATCH`.
- Diferenciar **excepciones a nivel de BD** (responsabilidad del DBA, en los scripts/triggers propios) de **excepciones a nivel de aplicación** (responsabilidad del desarrollador).
- Diferenciar **SQL estático** (sentencia fija) de **SQL dinámico** (la sentencia se recompone en tiempo de ejecución; se lanza con `EXEC`/`sp_executesql`), y saber dar sus ventajas: reutilización, adaptabilidad, rendimiento, flexibilidad.
- Buena práctica recurrente del profesor: antes de tocar producción, usar un **entorno de pruebas (sandbox)**, control de versiones, copia de seguridad previa y documentación — y, ante borrados masivos, preferir **mover a tablas históricas** en vez de `DELETE` directo.
- Cada motor tiene su propio lenguaje de triggers (T-SQL, PL/SQL, PL/pgSQL) y su propia herramienta de automatización (SQL Server Agent, Oracle Scheduler, pg_cron) — no hay que memorizarlos, solo saber que existen y que cada motor difiere.
- Pendiente: entrega de la Actividad 1 (Tema 2) y repaso práctico el viernes 23/10, junto con el lanzamiento del Kahoot del Tema 3. La semana siguiente arranca el **Tema 4** (transacciones).
