---
asignatura: Sistemas Gestores de Bases de Datos (SGBD)
fecha: 2026-11-16
tema: "Repaso del primer trimestre (Temas 1-4) para el simulacro no puntuable del 23/11: qué es importante y qué no, y cómo se contesta"
fuente: "Transcripción de la clase en directo (1 h 25 min) + lista de importante/no importante de Dani + PDFs del profesor TEMA1, TEMA_2, TEMA_3 y TEMA4 (este último, solo imágenes, ya recogido en la nota del 26/10) + aportaciones propias marcadas (mío)"
---
# SGBD · Repaso del trimestre y simulacro del 23/11 (16/11)

> Anterior: [Tutoría 6/11: calendario y simulacros](2026-11-06_tutoria-calendario-simulacros-y-repaso-temas-3-4.md) · Profesor: César Carrión

Clase distinta: no hay materia nueva. El profesor repasó los Temas 1-4 diciendo **qué entra y qué no entra** en el simulacro de la semana siguiente y en el examen de mayo, y **cómo hay que contestar**. Esta nota contrasta tu lista con lo que dijo (transcripción) y con las diapositivas (PDF manda sobre el audio). Origen: **(clase)**, **(PDF TemaX)**, **(tu lista)**, **(mío)**.

## Lo imprescindible

1. **Simulacro del lunes 23/11 (no puntuable, no se entrega, no se corrige)** (clase). Mismo horario de clase. Dos partes:
   - **Test**: unas **25 preguntas** ya preparadas (dijo 25 y también 30; **sin confirmar**) tomadas de los *cajones* (Kahoot). Las lanza **una a una por pantalla** y contestas por el **chat** (azul/verde/roja...). No es el Kahoot competitivo.
   - **Desarrollo**: **3 preguntas (quizá 4)**, **a mano en folios** (lleva folios y bolígrafo), unos **30 min**, respuestas de **5-6 líneas** ("lo importante no son las líneas, es lo que se pone"). Las ofrece en pantalla o como Word sin logos. Luego él explica **qué esperaba** en cada una. Tú te autoevalúas.
2. **Examen de mayo** (clase): dos partes. **Test** de 25-30 preguntas (unas **3 por tema** con los 10 temas) y **3 (o 4) preguntas de desarrollo**, **escritas a mano**. El test sale de los **cajones** del profesor (≈150 preguntas, 10-15 por tema), **no** de los tests de la plataforma. Cada convocatoria tiene 3-4 versiones distintas de examen, así que **no puede decir qué preguntas caen**, solo qué temas o partes son menos útiles.
3. **No se pide sintaxis ni escribir un trigger/procedimiento de memoria.** Lo que se valora: **qué es, para qué sirve, cuándo se aplica, cómo se estructura** y **pensamiento crítico**. Un **ejemplo siempre suma**, aunque esté mal escrito (falte una coma o un `;`).
4. **Qué estudiar**: léete los temas y, sobre todo, los **PowerPoint que sube** (no los apuntes de memoria) y **repasa los cajones** para el test. Dijo que **desde Tema 5 ya no hay simulacro**: en tercer trimestre "se va con todo" y en las dos últimas semanas de abril se repasa otra vez.
5. **Para qué es el simulacro**: no te engañes con notas. El año pasado hubo "un bajón enorme" en mayo porque muchos resolvieron con ayuda externa durante el curso; ahora no hay nota, solo preparación.

## Contraste de tu lista con lo dicho en clase

### IMPORTANTE

| Tu lista | Lo que dijo el profesor (clase) | PDF / corrección |
|---|---|---|
| Definición de SGBD | **Sí.** Qué es un **gestor**: herramienta que controla **varias bases de datos**, administra usuarios, lanza triggers, manipula, monitoriza y optimiza, y tiene información sobre ellas. Se gestiona "de forma eficiente" | PDF Tema 1: el SGBD controla la BD y asegura **integridad, disponibilidad y confidencialidad** |
| Arquitectura ANSI-SPARC (3 capas) | **Muy importante.** Saber **dibujarla y explicarla**: externo (lo que ve el usuario: formularios, vistas, tablas), conceptual/medio (estructura lógica: tablas, vistas, uniones, triggers, eventos), interno (**dónde está físicamente**: equipo, disco, carpeta). No hace falta saber las siglas. Ventajas citadas: **datos independientes**, control de seguridad, BD más optimizada, escalable | PDF Tema 1: usa **externo / medio (conceptual) / interno**. Ejemplo de la biblioteca. **Independencia de datos** = un cambio en un nivel no obliga a reescribir los otros |
| Roles del DBA (DDL, DCL, DML, optimización, seguridad, mantenimiento y actualización) | **Sí.** "Papel de un DBA": definición, control y manipulación de datos, optimización, seguridad y respaldo, mantenimiento. No exige palabras exactas: si dices optimización y seguridad, se sobreentiende mantenimiento | **Corrección menor**: PDF Tema 1 dice **"Seguridad y respaldo"** (copias), no solo "seguridad", y "Mantenimiento y actualización". Tu lista pierde **respaldo/copias** |
| Lenguajes DCL, DML, DDL | **Sí.** Contestar con el contenido del **Tema 2** (profundiza más que el Tema 1). Si pregunta "todo lo que sepas de X", enumera comandos y pon **un ejemplo** | Ver tabla de abajo |
| Arquitectura cliente-servidor | **Sí.** Es lo mismo que ANSI-SPARC pero en **2 niveles**: presentación (lo que ve el usuario) y servidor (las dos capas inferiores juntas). Respuesta igual de válida | Detalle y demo de DBeaver en la [nota del 21/09](2026-09-21_tema1-conceptos-relacional-ansi-sparc.md) |
| Entender scripts y procedures | **Sí.** Lo central: **por qué existen** (tareas de mantenimiento repetitivas que no se hacen a mano e improvisadas en la consola, sino con guiones automatizados y preparados); qué son; ejemplos (copias, índices, limpieza). Lo repetirás en casi cualquier respuesta del Tema 3 | **PDF Tema 3 no desarrolla** `CREATE PROCEDURE` ni `COMMIT`/`ROLLBACK`: solo cita "procedimientos almacenados" al hablar de lenguajes. En clase dijo que `commit`/`rollback` existen (ver nota del 26/10: "superimportante") |
| Estructura de triggers | **Sí, pero más "para qué" que "cómo".** Estructura: `CREATE TRIGGER nombre` + **objeto** (tabla, vista o evento del sistema) + **cuándo** (antes/después) y **qué acción** (INSERT/UPDATE/DELETE) + `BEGIN ... END` con las instrucciones. Si no la escribes bien, no pasa nada | PDF Tema 3: 3 ejemplos en T-SQL (ver avisos) |
| SQL dinámico (saber que existe y qué es) | **Matiz importante**: hoy dijo expresamente que **no preguntará** diferencias entre SQL estático y dinámico ni cuál es mejor, ni lenguajes concretos. Sí explicó la idea: usar **parámetros** en vez de pegar valores en el texto protege de **inyección SQL** | PDF Tema 3: dinámico = sentencia que se **construye en tiempo de ejecución**; `EXEC` y `SP_EXECUTESQL` (con parámetros). Lo mínimo: que existe, qué es y la relación con inyección |
| Detección de errores en un sistema | **Sí, es el Tema 4**: razonamiento crítico, cómo abordar "va lenta". Y además, en el Tema 3, el **control de excepciones** (`TRY`/`CATCH`): saber que existe y para qué | PDF Tema 3: excepción = evento inesperado en ejecución. **No está en tu lista** |
| Ciclo de vida del rendimiento (comprender, identificar, establecer, aplicar, evaluar) | **Sí.** Primero **entender qué significa "va lento"**, medir **en vacío** y en picos, separar lo que es de la BD de lo que no (red, switches, disco...) | Tabla de 5 pasos en la [nota del 26/10](2026-10-26_tema4-optimizacion-monitorizacion-indices.md) |
| EXPLAIN y ANALYZE | **"Las dos sentencias más importantes"** del análisis de una BD. `EXPLAIN` + una consulta indica si se **usan los índices**; `ANALYZE` da **estadísticas** de la tabla | Misma nota del 26/10 |

### NO IMPORTANTE (confirmado en clase)

| Tu lista | Dicho en clase |
|---|---|
| Definición de una base de datos | "No es algo que vaya a preguntar" |
| Modelos comerciales y no comerciales | No lo preguntará en desarrollo. **Matiz**: "en el tipo test podría caer", con menos valor. Si lo citas como ejemplo en una respuesta, suma |
| Proceso de instalación de una BBDD | "No voy a preguntar nada" ni ahora ni en mayo |
| Ley de protección de datos (LOPDGDD) | "No va a caer en el examen" |

**Más cosas que dijo que no pregunta** (no están en tu lista): instancias de base de datos y sus jerarquías; el listado de tareas de planificación administrativa del Tema 3 ("dime las tareas que son"); diferencias entre lenguajes (T-SQL, PL/SQL...) y herramientas; cuándo es mejor SQL estático o dinámico.

## Cómo contestar (criterios del profesor)

- **Preguntas ambiguas a propósito** ("explícame qué hace este trigger y su importancia"): te dejan **contar todo lo que sepas**. Si está bien hilado y justificado, vale.
- **Un ejemplo vale más que no ponerlo**, aunque esté mal escrito: demuestra que lo entiendes.
- Si dices menos pero es "efectivo y resultadista", **no te penaliza** (3 líneas bastan; 5 de relleno no).
- Preguntas posibles que dio como muestra (no son necesariamente las del examen):
  1. "Explícame la **arquitectura ANSI-SPARC** y cómo se relacionan sus niveles."
  2. "¿Cuál es el **papel de un administrador** de BD en un SGBD?"
  3. "Dime todo lo que sepas sobre **DDL / DML / DCL**."
  4. "Explícame qué hace este **trigger** y su importancia."
  5. BD de **fichajes** con usuarios que la manipulan: ¿qué herramientas usarías para asegurar los datos?
  6. BD con **historial de correcciones de un documento de calidad**: ¿cómo la harías más efectiva?
  7. Empresa con **lentitud al mediodía**: pasos para encontrar el problema y soluciones.

### Lenguajes de datos (Tema 2; contestar con esto)

| Lenguaje | Para qué | Comandos (PDF Tema 2) | Ejemplo |
|---|---|---|---|
| **DDL** (definición) | Crear, modificar y destruir la **estructura** | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` | `CREATE TABLE clientes (id_cliente INT AUTO_INCREMENT PRIMARY KEY, nombre VARCHAR(100) NOT NULL);` |
| **DML** (manipulación) | Manejar los **datos** (CRUD) | `SELECT`, `INSERT`, `UPDATE`, `DELETE` | `UPDATE clientes SET ciudad='Málaga' WHERE id_cliente=1;` |
| **DCL** (control) | **Permisos** de usuarios | `GRANT`, `REVOKE` (y crear usuarios y roles) | `GRANT SELECT ON empresa.* TO 'operador'@'localhost';` |

Matices del PDF Tema 2: `DROP` borra estructura y contenido; `TRUNCATE` vacía la tabla y conserva la estructura (reinicia `AUTO_INCREMENT`); `UPDATE`/`DELETE` van con `WHERE`; dar **solo los permisos mínimos**; se pueden agrupar permisos en **roles** (`CREATE ROLE`, `GRANT ... TO rol`); ver permisos con `SHOW GRANTS FOR ...`.

> [!warning] Avisos sobre las diapositivas (mío; no hay que memorizar sintaxis)
> - **`CREATE USER` ¿DDL o DCL?** El PDF Tema 2 dice "para crear un usuario utilizamos comandos **DDL**", pero el profesor lo cuenta dentro del **DCL**. En el simulacro, pon el contexto: "el DCL gestiona usuarios y permisos".
> - `ALTER USER Ana ADD TO ROLE Administradores` (PDF Tema 2): es probable que **no sea sintaxis válida** en MySQL/MariaDB, donde se asigna un rol con `GRANT rol TO usuario`. Como no piden sintaxis, no es evaluable.
> - PDF Tema 3, tercer trigger (`ON DATABASE FOR INSERT`): es probable que **no funcione tal cual** en SQL Server, porque los triggers de base de datos responden a eventos **DDL** (como `CREATE_TABLE`), no a `INSERT`. Sirve como idea ("trigger sobre evento del sistema"), no como código. **Sin verificar** en la documentación de Microsoft.
> - **SQL dinámico**: el profesor lo explicó de forma confusa. Según el PDF Tema 3 y mi conocimiento: concatenar texto y ejecutarlo con `EXEC(@texto)` es lo **vulnerable** a inyección; `SP_EXECUTESQL` con **parámetros** es la forma segura (mío).
> - `EXPLAIN` en SQL Server: ya anotado en la nota del 26/10 (no es lo habitual en T-SQL).

### Triggers: qué debes saber contar

- **Qué es**: conjunto de instrucciones que se ejecutan **automáticamente cuando ocurre algo**: `INSERT`/`UPDATE`/`DELETE` sobre tablas o vistas, o eventos del sistema (logins, creación de objetos, `GRANT`/`REVOKE`).
- **Para qué** (lo que más puntúa): **auditoría/trazabilidad**, integridad, automatizar tareas.
- **Ejemplos del profesor** (útiles para pegar en una respuesta):
  - **Fichajes**: un fichaje no debería actualizarse. Un trigger sobre `UPDATE` guarda en una tabla de **log** quién (usuario), desde dónde (IP), cuándo, y el **valor antes del cambio**, para poder recuperarlo.
  - **Cuentas bancarias**: control de movimientos sobre la tabla de cuentas.
  - **Documento de calidad** con historial de correcciones: quién modificó y cuándo.
  - **Permisos**: guardar en una tabla de trazabilidad cada `GRANT`/`REVOKE` (quién dio control total a Juan, cuándo).
- **Coste** (Tema 4): un trigger que duplica cada `INSERT` en otra tabla **duplica la carga**; puede ralentizar la BD.
- **Excepciones**: toda tarea automática debería controlar errores (`TRY`/`CATCH`) para que no "casque" y dé una salida paralela (por ejemplo, campo vacío o dato duplicado).
- **Estructura** (no hace falta exactitud): nombre -> objeto -> antes/después de qué acción -> `BEGIN` ... `END`.

### Diagnóstico de lentitud (Tema 4)

Resumen del profesor, para una respuesta de 5-6 líneas:
1. **Comprender**: qué significa "va lenta" (¿30 s es mucho o lo normal?). Medir **en vacío** (nadie conectado) y en **uso normal y picos** (9:00 frente a 12:00).
2. **Separar** lo que es de la BD de lo que no: red/switch (bucles, ancho de banda de 100 Mb, servidor compartido con otros servicios), tarjeta de red, disco, RAM, accesos simultáneos, una `JOIN` mal montada en la aplicación (ahí no puedes tocar).
3. **Dentro de la BD**: `EXPLAIN` (¿se usan los índices?), `ANALYZE` (estadísticas), índices correctos, triggers que duplican carga.
4. **Aplicar** y **evaluar**: medir, cambiar, volver a medir.
- Ejemplo: aislar la BD de facturación en un switch propio o VLAN para que sus 5 usuarios no compitan con el tráfico de los otros 150.
- Su opinión: "el 90 % de las veces no se resuelve con `EXPLAIN` y `ANALYZE`" (cifra suya, no verificada).

## Práctica para el simulacro (mío; el profesor no ha dado ejercicios)

Primero los ejercicios; las pistas, al final. Contesta **a mano, 5-6 líneas**, sin mirar los apuntes.

**Nivel 1 (reconocer)**
1. Dibuja y explica la arquitectura ANSI-SPARC con un ejemplo (una biblioteca o una tienda). ¿Qué es la independencia de datos?
2. Clasifica en DDL, DML o DCL: `TRUNCATE`, `GRANT`, `INSERT`, `ALTER`, `REVOKE`, `SELECT`.
3. ¿En qué se diferencia la arquitectura cliente-servidor de 2 capas de ANSI-SPARC?
4. Enumera las funciones del DBA.

**Nivel 2 (aplicar)**
5. "Explícame qué hace este trigger y su importancia": `CREATE TRIGGER tr_log AFTER UPDATE ON fichajes ... INSERT INTO log(usuario, ip, fecha, valor_anterior) ...`.
6. Una empresa tiene una BD de pedidos y le preocupa que alguien dé permisos de más. ¿Qué harías con DCL y con triggers?
7. ¿Por qué un administrador usa scripts en vez de lanzar sentencias a mano? Pon dos tareas automatizables.
8. ¿Qué es una excepción y por qué conviene controlarla en un script o trigger?

**Nivel 3 (razonar)**
9. Una empresa se queja de que "la BD va lenta a las 12:00". Describe tu plan de diagnóstico completo (físico y lógico) y cómo sabrás si has mejorado.
10. Tienes un trigger que duplica cada `INSERT` en una tabla de histórico y el sistema empieza a ir lento. ¿Qué haces?
11. Explica cómo la inyección SQL se relaciona con SQL dinámico y parámetros. ¿Qué harías para evitarla?
12. Una tienda con 5 sucursales quiere detectar manipulaciones en sus ventas diarias. Diseña (en palabras) la solución en la BD.

**Pistas y soluciones**
1. Externo (vistas/usuarios), conceptual (tablas y relaciones), interno (discos, ficheros, índices). Independencia: cambiar un nivel no obliga a reescribir los otros (si cambio el almacenamiento, las vistas no se rompen).
2. DDL: `TRUNCATE`, `ALTER`. DCL: `GRANT`, `REVOKE`. DML: `INSERT`, `SELECT`. (`TRUNCATE` es DDL según el PDF Tema 2.)
3. 2 capas = presentación + servidor (conceptual e interno juntos). Es la misma idea con menos niveles.
4. Definición, control y manipulación de datos; optimización del rendimiento; seguridad y **respaldo**; mantenimiento y actualización.
5. Cada vez que se actualiza un fichaje se guarda quién, desde dónde, cuándo y el valor anterior. Importancia: trazabilidad y poder recuperar el dato original.
6. `GRANT`/`REVOKE` con mínimo privilegio y roles; trigger sobre eventos de permisos que guarde quién concedió qué y cuándo en una tabla de trazabilidad.
7. Tareas repetitivas y de mantenimiento: copias, limpieza de datos antiguos, mantenimiento de índices, informes. Evita errores manuales y se pueden programar (cron/Task Scheduler).
8. Evento inesperado en ejecución (dato duplicado, campo vacío). Con `TRY`/`CATCH` el proceso no se cae y se registra el fallo.
9. Ciclo: comprender (medir en vacío y picos), identificar (red, disco, consultas, bloqueos), establecer meta (p. ej. < 5 s), aplicar (índices, aislar red, etc.), evaluar (volver a medir). Dentro de la BD: `EXPLAIN`, `ANALYZE`.
10. Medir el coste del trigger, valorar si el histórico se puede hacer por lotes o en otra ventana, optimizar (índices del histórico), y comparar antes y después.
11. Si el valor se pega en el texto de la sentencia, un atacante puede inyectar código; con parámetros el valor se trata como dato. Parametrizar y dar permisos mínimos.
12. Trigger de auditoría (usuario, IP, fecha, valor anterior), permisos mínimos y copias de seguridad.

## Calendario y logística

- **Esta semana (16-20/11)**: clases de repaso en todas las asignaturas. Las **clases de contenido terminaron el viernes 13/11** y se retoman **la semana del 7/12**.
- **Lunes 23/11**: simulacro (ver arriba). **Semana del 30/11**: "presentación del segundo trimestre", sin materia nueva. El trimestre "empieza" el 7/12 y habrá **2 semanas efectivas** (7 y 14/12) antes de Navidad.
- **Temario siguiente** (clase; **numeración sin confirmar**, el audio se mezcla): Tema 5 = copias de seguridad con sentencias SQL (acaba SQL); Tema 6 = bases de datos distribuidas; Tema 7 = MongoDB; Tema 8 = Cassandra; Tema 9 = Redis. El Tema 10 no se mencionó.
- **Más práctica**: varios alumnos pidieron más práctica. El profesor dijo que intentará dar **más práctica en las 2 semanas de diciembre** y que **no se tocarán temas nuevos** a cambio; también tiene una **tutoría de 1 h cada 15 días**, que usa para el resumen del tema. No hay compromiso firme.
- **TFC**: el feedback de la primera entrega se publicó **ayer (15/11)**. Solo responde **a uno de los miembros de cada grupo**: si no ves respuesta, es probable que la tenga tu compañero. **Segunda entrega en diciembre** (fecha sin precisar).

## Para llevar a casa

- [ ] Repasar los **cajones (Kahoot)** de los Temas 1-4: de ahí sale el test del simulacro y de mayo.
- [ ] Preparar **folios y bolígrafo** para el lunes 23/11 y practicar 2-3 respuestas a mano de 5-6 líneas (ejercicios de arriba).
- [ ] Dominar: ANSI-SPARC (dibujo), funciones del DBA, DDL/DML/DCL con un ejemplo cada uno, para qué sirven scripts y triggers (con un ejemplo de auditoría), ciclo de 5 pasos, `EXPLAIN`/`ANALYZE`, cliente-servidor (2 niveles).
- [ ] Saber **que existen** (sin sintaxis): SQL dinámico (`EXEC`, `SP_EXECUTESQL`), `TRY`/`CATCH`, `COMMIT`/`ROLLBACK`.
- [ ] Mirar el feedback del TFC y preparar la segunda entrega (diciembre).

> [!warning] Dudas del audio
> - Transcripción: "Ansie Spark / Sies Park" = ANSI-SPARC; "Splain / Analys" = EXPLAIN / ANALYZE; "cajún / cajút" = Kahoot; "S. Q. L." = SQL; "A V la" = VLAN.
> - Nº de preguntas del simulacro: 25 (varias veces) o 30 (una vez). **Sin confirmar.**
> - Tema 6-9 en el calendario siguiente: el audio mezcla "distribuidas" y "Mongo" para el Tema 6. Es probable que sea la lista de arriba, pero **no está confirmado**.
> - Se omite el diálogo sobre el estado del TFC de otros alumnos y las menciones a los resultados del año pasado salvo lo que explica el objetivo del simulacro.
