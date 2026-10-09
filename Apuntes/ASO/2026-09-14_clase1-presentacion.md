---
asignatura: Administración de Sistemas Operativos (ASO)
fecha: 2026-09-14
tema: Clase 1 · presentación del módulo, organización y evaluación
fuente: transcripción de la clase en directo
---
# ASO · Clase 1 (14/09) · Presentación del módulo

> Siguiente: [Clase 2 (21/09): primera clase de contenido](2026-09-21_primera-clase-linux-basico.md)

Clase de presentación (sin contenido técnico de examen). Impartida por **Jairo Bahillo Calvo**, que este curso da también IAW (el año pasado daba SAD e IAW; este año SAD lo da Damián y IAW lo sigue dando él). Primera clase con contenido real: el lunes siguiente.

## El profesor y su valoración de la asignatura
Jairo considera ASO, junto con SAD, **el núcleo de la administración de sistemas** dentro del ciclo — lo remarca como la asignatura más importante del curso, más que IAW (que él también imparte y considera más fácil, aunque igualmente relevante). Palabras textuales: *"me parece un sacrilegio decir que una persona de ASIR no tiene que saber programar"* (en referencia al scripting, que no es "programar" en sentido estricto pero es imprescindible).

## Organización del curso
- **150 horas presenciales**, repartidas en 2 trimestres (de los 3 del curso).
- Una sesión semanal de **hora y media** los lunes (antes eran 2-2,5 horas; se redujo porque "es imposible dar todo lo que se pretende dar" en el tiempo asignado).
- Tutoría colectiva de **media hora**, cada 2 semanas, con horario aún por confirmar en el momento de esta clase (barajaba moverla de 9:30 para no coincidir con un hueco muerto). En la tutoría **no se avanza contenido nuevo**, solo se resuelven dudas de lo ya visto en clase.
- Solo se trabaja con **Linux** (ninguna máquina Windows en todo el curso). Distro recomendada: **Ubuntu** (el profesor usa 22.04 LTS; aclaró que 24.04/26.04 también funcionan, sobre todo en equipos sin virtualización — con virtualización no lo ha probado tanto). Recomendación explícita: usar siempre una versión **LTS**, nunca una versión "no LTS" para trabajar en clase. Importante por arquitectura: usar la versión ARM o Intel/AMD según el hardware real (el año pasado hubo problemas por mezclar esto).
- Se puede trabajar en máquina virtual (VirtualBox/VMware/UTM), en un servidor VPS, en un PC físico dedicado, o incluso con un Ubuntu Server sin entorno gráfico — todo vale, aunque en clase el profesor usará el escritorio de Ubuntu por comodidad visual. Recomendación práctica: crear primero una máquina virtual "limpia" recién instalada y **clonarla** (botón derecho → clonar, en VirtualBox/VMware) antes de empezar a trastear, para poder recuperar un entorno limpio en minutos si algo se rompe.
- Casi todo el trabajo del curso será por **línea de comandos (CLI)**, muy poco en modo gráfico.

## Editor de texto: por qué Nano y no VS Code
Decisión explícita del profesor: usará **Nano** en clase (no VS Code ni editores con autocompletado), porque el examen final es **presencial, con bolígrafo y papel** — no hay IDE el día del examen. Quien quiera trabajar en casa con otro editor (vim, VS Code, etc.) es libre de hacerlo, pero en clase se usa Nano para que el alumnado se acostumbre a la situación real del examen. Comentó una anécdota (sin verificar, mencionada como experiencia personal del profesor en educación online) sobre alumnos de otros años atascados sin saber salir de `vi`/`vim` por su complejidad.

## Temario: 10 temas, mismo temario que otros grupos, distinto reparto por trimestre
- Temario idéntico al de otros grupos/profesores del mismo módulo.
- **Trimestre 1 cubre 3 temas** (más que lo habitual) porque el Tema 3 (scripting) es, según el profesor, el más importante del curso y necesita mucho tiempo:
  1. Configuración y gestión básica (parte teórica: qué es el kernel, distribuciones, etc.)
  2. Administración de procesos del sistema (imagen virtual del proceso, con más profundidad)
  3. **Creación de Scripts** — se alarga hasta bien entrado el trimestre 2 por la poca frecuencia de clases.
- Resto del temario: administración de software (instalación, uso), administración remota (**SSH**), automatización de tareas (**cron**, **crontab**, **systemd** — "lo más moderno", imprescindible en el sector real), y los 3 últimos temas sobre dispositivos de almacenamiento (montaje de volúmenes, permanentes y no permanentes), basados sobre todo en **Samba** y **LDAP**. El profesor avisó que estos últimos temas suelen darse "ya cansados" de curso y se cubren a tiro fijo con las 4-5 cosas esenciales de cada uno (montar LDAP, meter un usuario, crear un recurso Samba).
- Temas en los que el profesor se parará más si hace falta: **3, 5 y 6**. El Tema 7 (RAID) también es importante pero más complicado — hay una sesión de repaso de sistemas RAID preparada para alguna tutoría si hace falta.

## Evaluación
- **3 actividades + 10 test** → hasta 15 puntos posibles, pero solo hacen falta **10** para la máxima nota de evaluación continua.
- Aviso práctico dado en esta clase: en el momento de esta sesión, los test **aún no contaban puntuación en la plataforma** (fallo temporal de configuración a resolver esa semana) — el profesor pidió esperar antes de hacerlos para evitar errores de recálculo de notas. Los foros tampoco puntúan, solo las actividades.
- Fórmula: nota de evaluación continua + examen final presencial (boli y papel) — **hay que aprobar el examen con un 5 independientemente de la nota de continua**; si se aprueba el examen, la nota media puede subir considerablemente (ejemplo dado: con 10 de continua y 5 de examen, la nota del boletín puede salir en un 7,5).
- **Reparto del examen final**: 3 puntos de test + 7 puntos de práctica. De esos 7 puntos de práctica, **4 puntos son específicamente de la parte de Scripting (Tema 3)** — el profesor lo repitió varias veces como dato clave de cara a estudiar: "4 puntos si no son más, pero menos no van a ser". El año pasado fueron también 4 puntos (el primer año que dio el módulo fueron 7 puntos completos de scripting). Motivo: detectó que mucha gente podía aprobar solo con el test + otros 3 puntos de práctica sin dominar bien el scripting, y quiso corregir esa carencia.
- El proyecto/TFC es una asignatura independiente, no forma parte de la nota de ASO.

## TFC: grupos y figuras (aclaración puntual)
Discusión en clase sobre cómo se forman los grupos de TFC (3 personas, del mismo grupo/sección de clase — no se pueden mezclar alumnos de grupos distintos, p. ej. "grupo 3" con "grupo 7"). Se aclaró la diferencia entre **director** (al que se presenta la propuesta y guía el proyecto) y **coordinador** (César, que organiza administrativamente los grupos). Jairo mencionó que será director de algunos TFC y pidió explícitamente proyectos innovadores, no simplemente "máquinas virtuales".

## Charla sobre el sector y la IA (contexto, no examinable)
Conversación informal sobre el mercado laboral de informática: el profesor defendió que el sector de sistemas ("ASIR") va a tener más relevancia porque la IA genera código pero no resuelve por sí sola la integración y mantenimiento de sistemas reales. Remarcó la importancia de entender los conceptos de fondo (estructuras de control, recorrer ficheros, etc.) para poder pedirle bien las cosas a una IA, en vez de depender de ella sin saber qué pedir — si no se sabe lo que hay que hacer, "la IA te va a sacar un chorrón" y no se sabrá ni detectar el fallo. Anécdota de un alumno (Manuel) sobre una entrevista técnica reciente en la que no le evaluaron por escribir código sino por saber depurarlo y orientar la solución.

## Deberes / cierre
Por ahora, dejar actividades y test en pausa (hasta que se resuelva el problema de puntuación en la plataforma); se puede empezar a leer el temario libremente. Próxima clase (lunes siguiente): primer tema real de ASO (y de IAW en paralelo, con el mismo profesor).
