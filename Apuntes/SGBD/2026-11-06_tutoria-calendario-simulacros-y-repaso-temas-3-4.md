---
asignatura: Sistemas Gestores de Bases de Datos
fecha: 2026-11-06
tema: "Tutoría colectiva (viernes): calendario hasta la evaluación, cómo serán los simulacros y repaso de los Temas 3 y 4"
fuente: transcripción de la tutoría (36 min). Sin material adicional. Gran parte de lo de los simulacros se amplía en la nota del 16/11.
---
# SGBD · Tutoría (6/11) · Calendario, simulacros y repaso de los Temas 3 y 4

> Anterior: [Tema 4: optimización, monitorización e índices (26/10)](2026-10-26_tema4-optimizacion-monitorizacion-indices.md) · Siguiente: [Repaso del trimestre y simulacro (16/11)](2026-11-16_repaso-trimestre-simulacro-que-entra-y-que-no.md) · Profesor: César Carrión

La primera parte es logística (calendario y simulacros, acordados en el claustro del día anterior) y la segunda un repaso rápido de los Temas 3 y 4.

> [!important] Lo imprescindible
> - **Los simulacros no son una prueba evaluativa**: se hacen **en clase, con el profesor, y no se entrega nada**. El motivo que da: se había comprobado que las pruebas de este tipo "no sirven" (se hacen con IA o se devuelven en minuto y medio con un 10).
> - **Formato en SGBD:** un **cajón (Kahoot) de 15-25 preguntas** (dijo "20 o 25") y **una pregunta de desarrollo por tema**; hace 3-4, o eliges 3 de 4. Tiempo: **30-45 minutos**, con música de fondo. **A mano, en un folio**; luego se corrige entre todos y da feedback.
> - **Calendario:** **semana del 9**: última con temario (SGBD no tuvo clase); **semana del 16**: solo **repaso**; **semana del 23**: **simulacros**; **semana del 30**: presentación del segundo trimestre, sin contenido.
> - **Actividad 1:** **todos los que la presentaron tienen un 10** ("ya tenéis 3 de los 10 puntos"). Falta subir la nota y el comentario individual.

## Calendario hasta la evaluación (según el profesor)

| Semana | Qué hay |
|---|---|
| **9/11** | Última semana de temario de otras asignaturas. En SGBD, **sin clase** ("volvemos a no tener") |
| **16/11** | **Solo repaso** en todos los módulos; **nadie da materia nueva** (si algún profesor lo hace, avisarle) |
| **23/11** | **Simulacros**: en cada módulo; si hay 2 clases, probablemente se use **una** |
| **30/11** | Inicio del segundo trimestre: presentaciones, poca carga (antes eran vacaciones) |
| **7/12 y 14/12** | Dos semanas de clase; luego parón hasta el **11/01** |
| **11/01-…** | Unas **8 clases** hasta la evaluación |

- El **tercer trimestre** es aún más corto (Semana Santa y defensa de proyectos en abril). Dice que el primero es "el más denso".
- **Tutorías colectivas:** desde el segundo trimestre se **reparten** para que cada semana tengáis una carga parecida (iniciativa de los alumnos; irá a todos los ciclos). Los alumnos pidieron que queden **lo más pegadas posible a las clases**.

## Repaso del Tema 3: scripts, triggers y procedimientos

- **Script:** conjunto de sentencias SQL que se ejecutan **cuando ocurre algo** en la base de datos. Si queda asociado a una tabla y salta solo, es un **trigger (disparador)**; si es código guardado que se lanza a mano o desde un trigger, es un **procedimiento almacenado**.
- **Usos del trigger:** duplicar una factura en otra tabla; **registrar un borrado en una tabla de log** (quién, qué contenía, a qué hora, desde qué IP) para tener **trazabilidad**.
- **Ejemplo de estructura:** `CREATE TRIGGER` + **nombre** + `ON tabla` + `AFTER INSERT` + `BEGIN ... END`. Dentro del `BEGIN` va lo que quieres que haga (p. ej., cambiar el estado del pedido).
- **Transacciones (`BEGIN TRAN` ... `ROLLBACK`/`COMMIT`):** cuando varias operaciones deben ir juntas, si **una falla, se revierte todo** y no se pierde información (ejemplo de la transferencia de 1 000 €: si no se resta de A pero sí se suma a B, el banco "regala" dinero).
- **Para el examen:** preguntará algo de **triggers o de procedimientos almacenados** del Tema 3, "la parte más importante". **No te pide escribir un trigger**: puede **ponerte uno** y que cuentes **qué es y qué hace**.

## Repaso del Tema 4: optimización

- **Lo más importante: la visión global (estrategia).** Cuando "la aplicación va lenta", el DBA debe **entender qué ha pasado, identificar dónde está el problema y definir cómo solucionarlo**. El problema puede estar **dentro o fuera de la base de datos**.
- **Causas fuera de la BD (ejemplos suyos):** tarjeta de red o cableado, el *switch* o un **bucle** en él, un equipo con virus que satura la red, **IP duplicadas**, portátiles no controlados, y **copias de seguridad que un usuario programa por su cuenta** a una hora punta (p. ej., a las 12). Un sistema de detección de actividad (SIEM, EDR) ayuda.
- **Causas dentro de la BD:** **mala optimización o definición de los índices**, tablas con más información de la que necesitan, etc.
- **Límite del DBA:** la base de datos suele venir **desarrollada por otro**: hay que **hablar con el desarrollador** y con la dirección, que suele querer pagar infraestructura pero no arreglar problemas.
- **`EXPLAIN` y `ANALYZE`:** `EXPLAIN` muestra **cómo se ejecuta** una consulta y **si usa los índices**; `ANALYZE` aporta **información real** de uso. Si un índice no se usa, hay que **redefinirlo**.
- **Índices:** `CREATE INDEX`, `CREATE CLUSTERED INDEX`, `DROP INDEX`. **No te los pide de memoria**: "hoy en día hay herramientas (y una IA lo hará), pero tú debes saber **que es necesario, por qué y dónde analizar la lentitud**".
- **Tipo de pregunta:** cómo **detectar y analizar un problema**, no sintaxis. (Coincide con lo que se anotó el [26/10](2026-10-26_tema4-optimizacion-monitorizacion-indices.md): describir los pasos para encontrar la causa de un sistema lento.)

## Dudas y cosas sin confirmar

- **Número de preguntas del cajón** del simulacro: dijo 15-16, "yo creo que 20" y, antes, 25. El 16/11 habló de unas 25. **Sin confirmar**.
- **Transacciones: ¿Tema 3 o Tema 4?** El 23/10 dijo que eran del Tema 4; hoy las trata en el Tema 3. Es probable que las encuadre donde le convenga; para el examen basta con entender su finalidad.
- **Fecha del simulacro de SGBD:** hoy no la da (solo la semana del 23); se concretó el 16/11 como el **lunes 23/11**.
- Omitido: la conversación inicial con un alumno, el reparto de delegados y las charlas sobre IA.

## Logística y para llevar a casa

- [ ] Preparar **papel y bolígrafo** para el simulacro de la semana del 23; no hay entrega.
- [ ] Repasar triggers (qué son, para qué, estructura), procedimientos y transacciones.
- [ ] Repasar `EXPLAIN`/`ANALYZE` y la estrategia de "va lenta".
- [ ] Mirar la nota de la Actividad 1 cuando la suba.
