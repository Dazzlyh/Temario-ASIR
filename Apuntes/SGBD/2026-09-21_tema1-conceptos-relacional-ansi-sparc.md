---
asignatura: Sistemas Gestores de Bases de Datos (SGBD)
fecha: 2026-09-21
tema: "Tema 1 · modelo relacional (repaso), triggers/trazabilidad, arquitectura ANSI/SPARC, roles DBA, lenguajes DDL/DML/DCL, transacciones"
fuente: transcripción de la clase en directo
---
# SGBD · Tema 1 (21/09) · Repaso relacional, ANSI/SPARC y el rol del administrador

> Anterior: [Clase 1: presentación del módulo](2026-09-14_clase1-presentacion.md) · Siguiente: [Tutoría: instalación de SQL Express, MariaDB y Oracle (25/09)](2026-09-25_tutoria-instalacion-sgbd.md)

Primera clase con contenido real de la asignatura (la del 14/09 fue solo presentación). El propio profesor señaló al final de la clase cuáles son, literalmente, **las 3 cosas del Tema 1 más susceptibles de entrar en el examen de mayo**: los lenguajes (DDL/DML/DCL), los roles (DBA vs. desarrollador) y la arquitectura ANSI/SPARC — con ANSI/SPARC marcada explícitamente como la más importante de las tres.

## Repaso: modelado relacional (tablas, claves, relaciones 1-a-N, joins)
Repaso de lo visto en 1º: diseño de tablas con clave primaria, claves foráneas para relacionar tablas (relaciones uno-a-muchos), y consultas que cruzan tablas mediante joins. Vistas como forma de simplificar consultas repetidas. Contenido de repaso, sin matices nuevos relevantes más allá de lo que ya cubren las diapositivas/el temario oficial.

## Triggers y trazabilidad: el caso de uso real
Idea clave remarcada por el profesor (ya apuntada en la Clase 1, aquí con ejemplo concreto): un trigger no es solo "código que se dispara en un evento" en abstracto — el caso de uso típico para un administrador es la **trazabilidad y el archivado histórico**:
- Ejemplo dado: si una tabla tiene 100.000 registros y se quiere "cortar" los últimos años, se crea una tabla histórica (p. ej. `factura_2026`) y un trigger que, al producirse un `INSERT`/`DELETE`, vuelca los datos del periodo correspondiente (primer trimestre, segundo trimestre...) a esa tabla histórica.
- No hace falta memorizar la sintaxis exacta del trigger de cara al examen — sí entender **qué dispara el trigger, qué hace y por qué un DBA lo necesitaría** (limpieza, archivado, auditoría de cambios).

## Arquitectura ANSI/SPARC (las 3 capas) — lo más importante del tema
El profesor fue explícito: *"si en mayo os cae algo del tema 1... va a ser la arquitectura ANSI Spark"*. Las 3 capas:
- **Externa**: la vista que tiene cada usuario/aplicación de los datos — no todos ven lo mismo ni de la misma forma.
- **Conceptual**: el modelo lógico completo de la base de datos (todas las entidades y relaciones), independiente de cómo se muestre a cada usuario o de cómo se almacene físicamente.
- **Interna**: cómo se almacenan realmente los datos en disco (estructuras físicas, índices, ficheros).
Analogías usadas en clase para fijar el concepto:
- **Biblioteca/bibliotecario-socio**: el socio de la biblioteca (capa externa) solo ve el catálogo y los libros que puede consultar; el bibliotecario (capa conceptual) conoce toda la organización lógica del fondo; cómo están físicamente colocados los libros en las estanterías es la capa interna.
- **Amazon**: el usuario final (capa externa) solo ve su pantalla de producto/carrito; el modelo de datos completo de catálogo/pedidos/inventario es la capa conceptual; cómo se almacena realmente en los servidores de Amazon es la capa interna.
El profesor conectó esto explícitamente con contenido que se verá más adelante **en SAD con Damián**: alta disponibilidad y máquinas virtuales también se explican, en el fondo, con esta misma separación de capas (la capa interna es la que se replica/virtualiza sin que la capa externa note el cambio).

## Comparativa de motores: comerciales vs. libres
Repaso rápido de motores, sin profundizar en ninguno:
- **Comerciales**: Oracle, SQL Server, IBM Lotus Notes, Access.
- **Libres/gratuitos**: MariaDB/MySQL, PostgreSQL.
- Tangente de un alumno (Manuel) sobre **Elasticsearch** y su concepto de índice invertido (inverted index) — mencionado como curiosidad, no como contenido de examen.
- Aviso de lo que viene en el **Tema 6**: bases de datos de grafos, con **Neo4j** como ejemplo — se tratará más adelante, no ahora.

## Los 3 lenguajes: DDL, DML y DCL, mapeados a los roles
Punto que el profesor desarrolló con más detalle que en la Clase 1, enlazándolo directamente con la pregunta "¿cuál es vuestro rol como administrador?":
- **DDL** (Data Definition Language): `CREATE`, `DROP` — creación/eliminación de estructuras (tablas, bases de datos).
- **DML** (Data Manipulation Language): `INSERT`, `SELECT`, `DELETE`, `UPDATE` — manipulación de los datos en sí. Es "lo que seguramente ya trabajasteis el año pasado".
- **DCL** (Data Control Language): permisos sobre usuarios — `GRANT`, y comandos equivalentes para revocar permisos sobre tablas o bases de datos.
- En la práctica, un script real casi nunca usa un solo lenguaje de forma aislada: un script de mantenimiento típico combina DCL (ajustar permisos) con DML (mover/insertar datos) y a veces DDL (crear la tabla destino si no existe). El profesor insiste en que **los 3 van entrelazados en el trabajo real de un DBA**, no son compartimentos estancos.
- Confirmado explícitamente: en el bloque distribuido (Tema 8-10, Cassandra/Redis...) también se tocará DCL, aunque sin profundizar mucho — "al final establecer permisos es siempre lo mismo: entrar a la base de datos y el grant".

### El rol: DBA (ASIR) vs. desarrollador (DAM/DA)
Reforzando lo ya dicho en la Clase 1, con un intercambio concreto en clase:
- **Diseñador/desarrollador**: se enfoca en la lógica de desarrollo de la base de datos (programarla, cargarla de datos).
- **Rol ASIR (el vuestro)**: operación, seguridad y mantenimiento — ser responsable de que el sistema esté en marcha y operativo; más orientado a monitorización y optimización de recursos que al desarrollo de la aplicación.
- Un alumno (Francisco) comentó que para su TFC tenía pensada una idea de desarrollo de aplicación; el profesor le advirtió explícitamente: **"cuidado con la orientación... tienes que irte siempre a este lado de la baraja y no al lado del desarrollo"** — mismo consejo de orientación de TFC que ya se dio en la Clase 1, aquí repetido con un caso concreto de un compañero.
- Anécdota breve del propio profesor: *"hace 2 semanas corregí una [base de datos] que dejaba transacciones abiertas porque le faltaba el commit y se saturaba"* — puesta como ejemplo de por qué ese rol de mantenimiento importa en el mundo real (si no se corrige, el DBA o el DAM responsable "se tiraría de los pelos").

## Transacciones: commit, rollback y atomicidad
Explicación del concepto de transacción con dos ejemplos:
- **Factura + detalle de factura**: al insertar una factura hay que insertar también varias líneas de detalle; el conjunto debe tratarse como **un único paquete** — si el sistema falla a mitad de la inserción de los detalles, hay que poder deshacer (rollback) toda la operación, no dejarla a medias.
- **Transferencia bancaria** (ejemplo "extremo" según el propio profesor): el dinero sale de la cuenta origen pero el sistema falla antes de que llegue a la cuenta destino — si las dos operaciones no se tratan como una unidad, se genera una inconsistencia grave (dinero que desaparece). De ahí la necesidad de **commit** (confirmar que todo el bloque se ejecutó correctamente) y **rollback** (deshacer si alguna parte del bloque falla).
- Conclusión del profesor: la optimización, la seguridad y el mantenimiento de una base de datos no son tareas "de programación" en el sentido estricto, sino una lista de responsabilidades operativas del DBA — y las transacciones son una de ellas.

## Instalación de un SGBD (adelanto de la práctica del viernes)
El profesor adelantó, sin entrar en detalle (se hace el viernes en la práctica), los elementos clave a tener en cuenta al instalar cualquier motor:
- **Puerto de red** que queda abierto (cada motor tiene el suyo por defecto — ejemplo dado: MySQL usa el 3306).
- **Contraseña del superadministrador**.
- **Rutas** donde se va a guardar la información.
- Si el servicio queda expuesto o está detrás de un proxy/firewall que lo limita.
- Aviso práctico: **Redis no se puede instalar directamente en Windows** — necesita un sistema Ubuntu/Linux, o bien se instala vía **Docker** (confirmado en clase que así se puede sortear la limitación de sistema operativo).
- El objetivo de la práctica del viernes no es "aprender a fondo" ningún motor concreto, sino simplemente **sentirse cómodo instalando varios gestores distintos** (Oracle, SQL Server, MariaDB) y verlos todos unificados en DBeaver.

## Arquitectura cliente-servidor (2 capas) y por qué DBeaver
Casi todo sistema de gestión de bases de datos sigue una arquitectura cliente-servidor de 2 capas: un **servidor** que alberga la base de datos y un **cliente** (la herramienta con la que se accede a esos datos). Ejemplos de clientes nativos por motor: SSMS para SQL Server, phpMyAdmin para MySQL/MariaDB (vía PHP). La razón de usar **DBeaver** como cliente único para todos los motores en la práctica del viernes: evitar tener un cliente distinto por cada base de datos y centralizar el acceso en una sola herramienta — el profesor lo compara explícitamente con el patrón de usar una **API**: el cliente aísla al usuario de atacar directamente al servidor, en vez de interactuar sin control con él.

## El sistema de "cajones" (pools de preguntas) y cómo se construye el examen de mayo
Explicación importante de cara a la preparación del examen, dada al cierre de la clase: el profesor prepara un **"cajón"** (pool de preguntas tipo test, normalmente 10-15 por tema) al final de cada tema. Con 10 temas, esto da un banco total de aproximadamente **150 preguntas**. **El examen de mayo (tipo test) se construye eligiendo preguntas aleatoriamente de ese banco de 150** — generalmente 1 o 2 preguntas por tema, hasta completar el examen. Consecuencia práctica explícita: estudiar bien los cajones de cada tema (los comparte/sube tras cada clase) es, en la práctica, estudiar directamente las preguntas que pueden salir en mayo. Se pueden lanzar en modo concurso o en modo individual ("modo tarjeta", una pregunta a la vez con sus 4 opciones). El cajón del Tema 1 (con las ~12 preguntas vistas hoy) se dejó para lanzarlo al principio de la clase del viernes, a modo de repaso.

## Cierre y plan del viernes
- El profesor subiría el material de instalación esa misma noche (o a primera hora del día siguiente) para que el alumnado pudiera intentar instalar los sistemas por su cuenta antes del viernes.
- Plan del viernes: lanzar primero el cajón del Tema 1 (repaso rápido), y después cubrir la instalación de los sistemas de gestión y DBeaver, "hasta donde se llegue".

## Deberes
Sin entrega formal. Revisar el cajón de preguntas del Tema 1 cuando se comparta, e intentar instalar por cuenta propia los motores que se trabajarán el viernes (SQL Server Express, Oracle, MariaDB) antes de la práctica, para llegar con dudas ya identificadas.
