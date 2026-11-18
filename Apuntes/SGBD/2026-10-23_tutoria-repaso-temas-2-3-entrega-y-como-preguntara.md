---
asignatura: Sistemas Gestores de Bases de Datos
fecha: 2026-10-23
tema: "Tutoría colectiva (viernes): criterio de entrega de la Actividad 1, cómo preguntará el profesor, ejercicio opcional y repaso de los Temas 2 y 3"
fuente: transcripción de la tutoría (53 min). No recibidos: el documento Word de ~30 páginas, el PowerPoint y el fichero `.sql` del ejercicio opcional que se menciona. El profesor dice en esta tutoría que "no se da contenido nuevo": es refuerzo.
---
# SGBD · Tutoría (23/10) · Entrega, cómo preguntará y repaso de los Temas 2 y 3

> Anterior: [Tema 3: scripts, eventos y triggers (19/10)](2026-10-19_tema3-scripts-eventos-triggers.md) · Siguiente: [Tema 4: optimización, monitorización e índices (26/10)](2026-10-26_tema4-optimizacion-monitorizacion-indices.md) · Profesor: César Carrión

Tutoría de repaso. Lo nuevo y evaluable es el criterio de **entrega**, el **tipo de pregunta de examen** y un **repaso de los lenguajes SQL** (DDL, DML, DCL) y de la **estructura de un trigger**.

> [!important] Lo imprescindible
> - **Actividad 1:** lo que importa es que **lo intentes, lo entiendas y puedas explicar lo que has hecho**. Si te atascas, **manda capturas y la solución que hayas encontrado**, incluso con ayuda de IA: "en el mundo laboral no existe el dímelo de cabeza; existen soluciones".
> - **Entrega tardía:** teóricamente se quitaría la **mitad de los puntos**, pero él **solo quita 1 punto** (de la nota de la actividad). **Envía un correo justificando el motivo**: si es cierto, **no quita nada**.
> - **Formato de entrega:** vale un **ZIP** o los **ficheros sueltos** (PDF + `.sql`), "de una forma o de otra me vale".
> - **Examen de mayo:** **preguntas de razonamiento**: "qué pasa si...", "explícame qué ocurre con...". Serán **2-3 (a lo sumo 4) preguntas de desarrollo** sobre **los 10 temas**, de **6-9 líneas**. No es un examen práctico, "porque no tenéis nada delante".
> - **Sin código de memoria:** no te pide escribir un trigger; **puede darte uno y preguntarte qué hace**.

## Actividad 1: criterio de corrección

- Para él, la actividad está bien si **has intentado hacer todos los puntos** y no se te olvida ninguno. Corrige **él** (el curso pasado había revisores externos sin conocer las clases).
- **Entrega tardía (reconstrucción mía, cifras confusas en el audio):** el 1 punto se descuenta de la **nota de la actividad (sobre 10)**. Como la actividad vale 3 puntos y la evaluación continua pesa un 50 %, el efecto en la nota final sería de unos **0,15 puntos** ("ridículo"). Es un cálculo mío; él lo dijo de forma desordenada.
- **TFC:** menciona que las entregas del TFC se han adelantado este año (una en noviembre y otra en diciembre) y que lo importante del anteproyecto es la **idea**, y de la memoria, **cubrir los apartados**.

## Cómo preguntará (examen de mayo)

- Pone **2-3 preguntas, a lo sumo 4 si son muy sencillas**, **una de cada tema** (10 temas), y tú **desarrollas 6-9 líneas con tus palabras**. "Cuanto más información me pongáis, más rica es la respuesta."
- Ejemplo inventado en directo: *"Explícame qué es un trigger, cómo se conecta, y sus diferencias con un procedimiento ejecutado y con un evento."* Respuesta que valora: el trigger se crea con `CREATE`, se asocia a una tabla, lleva un `BEGIN` con lo que hace, y sirve para copias, trazabilidad, etc.
- **Qué no pedirá:** que escribas un trigger de borrado. Sí podría poner uno y preguntar **qué hace**.
- Cuando se acerque mayo irá **acotando el temario**: "esto interesa, esto no". No hace falta saberse los 10 temas de memoria.

## Repaso de los lenguajes SQL (Tema 2)

> [!important] Es una pregunta "muy fácil de que caiga"
> Cada lenguaje, **para qué sirve** y **con qué órdenes**, con un ejemplo aunque sea abstracto.

| Lenguaje | Para qué | Órdenes que citó |
|---|---|---|
| **DDL** (definición) | **Crear y modificar estructuras**: bases de datos, tablas, vistas, índices | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML** (manipulación) | Manipular y **leer los datos** (el "CRUD") | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| **DCL** (control) | **Usuarios y permisos** | `GRANT`, `REVOKE`; creación de usuarios (`CREATE USER`, `ALTER USER`: contraseña, renombrar) |

- `TRUNCATE`: **vacía** una tabla y **reinicia los autoincrementales**. (El profesor lo coloca en DDL.)
- Vistas: se manejan con `CREATE VIEW`, `ALTER VIEW`, `DROP VIEW`.
- Carga masiva: se pueden insertar **varias filas con un solo `INSERT`**, separándolas con coma y terminando con punto y coma.
- Es lo mismo en cualquier motor: "me da igual que no te sepas la sintaxis exacta; sabes que cada motor tiene su mecanismo y al final es lo mismo".
- **Permisos:** seleccionar, insertar, actualizar, borrar, modificar estructura y **dar permisos a otros** (`GRANT OPTION`). `GRANT ALL` los da todos. `FLUSH PRIVILEGES` (MySQL/MariaDB) hace que se apliquen los cambios.
- **Principio de mínimo privilegio** (ejemplo suyo): para una web de consulta de facturas para comerciales, **no se da el usuario administrador** al desarrollador. Se crea **un usuario con solo `SELECT`** y, mejor, sobre **una vista que filtre solo los clientes de ese comercial**.
- **Ley de protección de datos (Tema 2):** las bases de datos deben **estar controladas y dadas de alta**, con la **sensibilidad** de lo que guardan (datos médicos, de menores, económicos). Existe el **derecho al olvido**. Conviene que los servidores estén **dentro de la UE**. *Según la nota del [16/11](2026-11-16_repaso-trimestre-simulacro-que-entra-y-que-no.md), la ley de protección de datos **no entra** en el examen.*

## Repaso del Tema 3: triggers

- **Trigger (disparador):** un script **asociado a una tabla** que **salta automáticamente** cuando ocurre un evento (`INSERT`, `UPDATE`, `DELETE`). Sirve para **duplicar datos, copias de seguridad y trazabilidad**.
- Ejemplo de uso: una tabla de **log/auditoría** que, tras cada `UPDATE`, guarda **quién, cuándo, desde qué IP, qué había antes y qué hay después** (caso de un fichaje manipulado a mano).
- **Estructura en 4 bloques (si te la pide, es esta):**
  1. `CREATE TRIGGER <nombre>`
  2. `ON <tabla>`
  3. **Momento del evento:** `AFTER INSERT`, `AFTER UPDATE`, `AFTER DELETE` o `INSTEAD OF` (en lugar de; típico para vistas)
  4. `BEGIN ... END`: **lo que hace**
- Ejemplo: tras un `INSERT` en `pedido`, el trigger cambia el estado a "en marcha".
- Un trigger se ejecuta **fila a fila** si el `INSERT` es de varias filas (según el profesor, "dependerá del código"; sin más detalle).
- **Procedimiento almacenado** ≠ trigger: es código **guardado** que **no salta solo**; se lanza a mano o desde otro script.
- **Transacciones (`BEGIN TRAN`, `COMMIT`, `ROLLBACK`):** agrupar varias sentencias para que **o se hacen todas o ninguna**. Ejemplo del banco: restar 1 000 € a A y sumarlos a B; si falla la segunda, `ROLLBACK`. Lo ve como "superimportante". **Discrepancia de ubicación:** aquí dice que lo verá en el Tema 4; el [26/10](2026-10-26_tema4-optimizacion-monitorizacion-indices.md) el Tema 4 fue de optimización, y el 6/11 lo trata como parte del Tema 3. Sin confirmar a qué tema "pertenece"; para el examen, vale con saber para qué sirve.

## Ejercicio opcional (no puntúa)

- Propuesta suya: una base de datos **"tienda de prácticas"** con **2 tablas** (categorías y productos) en DBeaver, para practicar `CREATE`, `ALTER`, `INSERT`, vistas, usuarios y permisos, y **4 triggers** (control de stock, asignación de unidades, límite de subida de precios del 50 %, borrado). Va con un Word de ~30 páginas (copiar y pegar), un PowerPoint y un `.sql`.
- **No sirve para el examen** ni cuenta para la evaluación continua. **No recibido**.
- En DBeaver, **para actualizar el árbol tras crear una base de datos, pulsa F5**. En SQL Server Express la conexión se hace por **autenticación de Windows** si no has activado `sa`.

## Dudas y cosas sin confirmar

- **Calendario:** dijo que "la semana del 2 y la semana del 9 es festivo y no hay clase". Eso no cuadra con que otras asignaturas tuvieron clase el 3/11 y el 10/11. Es probable que hablara solo de SGBD; **audio confuso**. Con la tutoría del 6/11 queda claro que el módulo **no tuvo clase la semana del 9** ([ver nota](2026-11-06_tutoria-calendario-simulacros-y-repaso-temas-3-4.md)).
- No recibidos: Word, PowerPoint y `.sql` del ejercicio opcional.
- Omitido: charlas sobre IA local y comentarios sobre compañeros.

## Logística y para llevar a casa

- [ ] Entregar la Actividad 1 (semana del 26/10). Si es tarde, **escribe al profesor justificándolo**.
- [ ] Repasar **DDL/DML/DCL con un ejemplo cada uno** y la **estructura del trigger en 4 bloques**.
- [ ] Practicar respuestas de 6-9 líneas (ver los ejercicios de la [nota del 16/11](2026-11-16_repaso-trimestre-simulacro-que-entra-y-que-no.md)).
