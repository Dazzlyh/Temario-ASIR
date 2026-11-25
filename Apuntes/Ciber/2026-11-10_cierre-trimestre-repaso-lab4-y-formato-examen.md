---
asignatura: Ciberseguridad
fecha: 2026-11-10
tema: "Cierre del primer trimestre: opinión sobre el ritmo, repaso del Laboratorio 4 (forense), formato del examen y simulacro"
fuente: transcripción de la clase (22 min) y, desde el 25/11, las diapositivas `CIBER_Clase09_diapositivas.pdf` (12 págs., «Tema 4 · cierre y corrección»). Donde difieren, manda el PDF. El audio del vídeo proyectado era ilegible; las diapositivas dicen cuál era (ver «Vídeo»).
---
# Ciber · 10/11 · Cierre del trimestre, repaso del Lab 4 y cómo será el examen

> Anterior: [Lab 4 parte 2 (5/11): Sleuth Kit y Autopsy](2026-11-05_lab4-analisis-forense-sleuthkit-autopsy-caso-rrhh.md) · Siguiente: [Repaso para el simulacro (17/11)](2026-11-17_repaso-simulacro-formato-examen-y-que-estudiar.md) · Profesor: Damián Sualdea Soy

Clase corta. La mayor parte se dedicó al ritmo del curso; lo técnico es poco: el cierre del tema forense y, sobre todo, **cómo será el examen** (esto último es lo útil).

> [!important] Lo imprescindible
> - **Examen de Ciber:** test + **preguntas cortas de desarrollo de 3-4 líneas**. El "caso práctico" **no es un caso real**: te dan una **instrucción con una herramienta** y tienes que **decir qué hace**. "No os voy a pedir crear instrucciones, os voy a pedir **leerlas**."
> - **Cómo se estudia (según él):** con el **repaso** y el **simulacro** "sería más que suficiente".
> - **Semana del 17/11:** una hora de **repaso de los puntos importantes de cada tema** con preguntas tipo examen. Después, el **simulacro**, que publica antes y resuelve en clase.
> - **Regla de oro del forense** (cierre del tema): "nunca hay que romper la prueba"; la evidencia se bloquea en **solo lectura** y se trabaja sobre una copia.

## Qué añaden las diapositivas (recibidas el 25/11)

> [!note] Correcciones a lo que anoté solo con el audio
> - **El vídeo proyectado era el de Deloitte** «Companies like yours» (unos 6 min, `youtube.com/watch?v=7UPe_fxOz8M`; no lo he abierto): un empleado pica, le roban las credenciales, entran, se llevan datos y borran el rastro. La diapositiva 6 lo presenta como «lo que acabáis de investigar, contado desde dentro» y pregunta «¿qué parte supisteis ver vosotros en la imagen del disco?». **Es probable que el vídeo cuya solución mencioné («Forense 3») sea ese**; no puedo confirmarlo: las diapositivas **no** hablan de la solución del Forense 3. Esa solución **sigue sin recibir**.
> - **La clase fue de cierre de la «Actividad 1» del Tema 4** (adquirir la imagen, recuperar borrados, escribir el informe), sin contenido nuevo.
> - **Caso práctico del examen: contradicción.** El audio decía que «no es un caso real, es una instrucción con una herramienta que hay que leer». Las diapositivas 10-11 dicen que es **un escenario (un log, una imagen, un CVE) que hay que interpretar**, con ejemplos: «aquí tienes un `auth.log`: ¿hubo acceso no autorizado, cuándo y desde dónde?», «interpreta este vector CVSS», «¿qué comando recupera un fichero borrado?». **Prepárate para las dos formas**; sin confirmar cuál prevalece (el 17/11 el profesor insistió en leer instrucciones: ver su [nota](2026-11-17_repaso-simulacro-formato-examen-y-que-estudiar.md)).
> - **Siguiente bloque:** el PDF dice «1 dic · Trimestre 2: **ataques y defensa de redes**»; el «phishing» del audio queda **sin confirmar**.

### El caso de la Actividad 1, en cuatro golpes (PDF, diapositiva 4)

| Hallazgo | Cómo se pilla |
|---|---|
| Acceso por SSH de madrugada | `auth.log`: **`admin` desde una IP externa a las 03:14** |
| Script disfrazado de foto (`.jpg`) | `file` / Autopsy: **no es imagen, es un script de exfiltración** |
| Credenciales borradas + la *flag* | **`fls -r -d`** e **`icat 77`** (o en rojo dentro de Autopsy) |
| La línea temporal lo ata | **`mactime`**: credenciales → script → borrado del log |

Es el caso RRHH del [Lab 4 parte 2](2026-11-05_lab4-analisis-forense-sleuthkit-autopsy-caso-rrhh.md). **(Mío)** Compruébalo contra tu informe: la hora (03:14) y el nº de inodo (77) son los del PDF; si tu imagen da otros, manda tu imagen.

### Fallos típicos del informe (PDF, diapositiva 5)

1. **Resumen ejecutivo con jerga:** «inodo», «slack», «`fls`»… no van ahí; en el resumen, **qué pasó «en cristiano»**; lo técnico, en los hallazgos.
2. **Hallazgos sin evidencia:** afirmar sin la **captura o el hash** es una opinión, no un hallazgo.
3. **Mezclar hechos y conclusiones:** «el fichero se borró a las 03:20» es un **hecho**; «para ocultar el robo» es una **conclusión**. Cada cosa en su sitio.

«No es un suspenso»: los comete todo el mundo al empezar. «El informe es el producto, no el papeleo del final.»

### Qué nos llevamos del Tema 4 (PDF, diapositiva 8)

1. **No romper la prueba:** solo lectura, copia de trabajo y hash; se trabaja sobre la copia.
2. **Manda el método, no la herramienta** (`dd`, Sleuth Kit, Autopsy cambian): **identificar, adquirir, analizar y documentar**.
3. **Todo acaba en un informe.** Frase del profesor: «todo contacto deja rastro» (**principio de Locard**).

## El examen y el simulacro

| Dato | Qué dijo |
|---|---|
| Formato | **Test** + **preguntas cortas de desarrollo** (3-4 líneas; el PDF dice «dos o tres preguntas») + caso práctico |
| Ejemplos del PDF (diapositiva 11) | Test: «¿cuál **no** es un pilar de la seguridad?», «¿el **RAID** es una copia de seguridad?», «¿firmar: simétrico o asimétrico?». Cortas: «explica la **regla 3-2-1**», «qué es la **cadena de custodia** y por qué importa», «**orden de volatilidad**: por qué manda». «Lo que cae es lo que hemos hecho»; el simulacro del 24 tiene **la misma forma** y **no cuenta nota** |
| "Caso práctico" | (audio) Una **instrucción con nombre de herramienta** y la pregunta "¿qué crees que está haciendo?". **(PDF)** además, un **escenario** (log, imagen, CVE) que interpretar: ver arriba |
| Ejemplos que puso | Una línea de **John the Ripper** ("está rompiendo contraseñas con un diccionario"); una orden de cifrado con un modo **CBC** ("cifra con criptografía simétrica"). El audio del segundo ejemplo es confuso: **sin confirmar** el detalle exacto |
| Qué se exige | **Intuir/leer** qué hace la instrucción; **no** memorizar parámetros ni escribir comandos |
| Simulacro | Lo publica antes; se resuelve en clase en la hora de repaso. **Sin confirmar** si es en papel (el audio es confuso) |
| Alcance del examen | Cubre **los 3 trimestres**; de este trimestre solo hay una parte, y el profesor dice que "dará muchas vueltas" al **tipo de pregunta** que siempre pone |
| Aviso heredado | No escribir "encriptar" (−0,25 por aparición): ver nota de la [clase 5](2026-10-13_clase5-criptografia.md) |

> [!note] Coherencia con las notas previas
> Esto encaja con la práctica de leer comandos que ya aparecía en los laboratorios (John, `openssl`, `gpg`, `dd`, `fls`). Si repasas, practica **explicar en una frase qué hace** cada comando de las chuletas de [Lab 3](2026-10-22_lab3-contrasenas-generar-identificar-romper.md), [Lab 4 parte 1](2026-11-03_lab4-adquisicion-dd-guymager-e-informe-pericial.md) y [Lab 4 parte 2](2026-11-05_lab4-analisis-forense-sleuthkit-autopsy-caso-rrhh.md). (mío)

## Repaso del Laboratorio 4

- **Actividades:** el profesor dice que **no ha corregido nada todavía**; repasará todas y dará las notas. Una entrega mal subida se gestiona **a través del tutor**.
- **Evidencia que se pide:** la actividad "se ha podido hacer durante todo el trimestre" y lo que necesita es **la evidencia** de lo hecho (capturas, informe). **No fijó fecha** en esta clase.
- **Qué se podía hacer:** el caso de **RRHH** de clase o los retos **Windows** (Forense 1-3). El profesor confirma que el **Forense 3 es "el chungo"** y que su solución "está muy chula"; lo proyectó **en vídeo**.
- **Retos Windows (máquinas):** el profesor las preparó para **x86**; él no puede ejecutarlas en su equipo con procesador **ARM64**. (mío, inferencia) Si tu equipo es ARM, es probable que no te arranquen en VirtualBox; compruébalo antes de bajarlas.
- **Vídeo proyectado:** el audio salió ilegible, pero las diapositivas lo identifican como el de **Deloitte** (ver arriba). La **solución del Forense 3** que el profesor prometió subir al foro: **sigue sin recibir**.
- **Historia de fondo (la que contó):** un ataque típico en una empresa: un **empleado** abre un correo o conecta un **USB** (se citó que el malware puede ir dentro de un **JPG**), le **roban las credenciales**, el atacante **entra**, **se lleva los datos**, **borra el rastro** y luego "lo acabas de investigar". Es el mismo hilo del caso RRHH (ver [nota del 5/11](2026-11-05_lab4-analisis-forense-sleuthkit-autopsy-caso-rrhh.md)): acceso, script con extensión falsa, robo y borrado. **Deloitte** es la fuente del vídeo: confirmado por el PDF.
- **Cierre del tema:** hay muchas herramientas para trabajar sobre copias, y "la parte de forense es muy, muy complicada"; lo visto es una **adaptación sencilla**. Con 1-2 h semanales "es imposible" cubrir el forense entero.

## Cómo seguirá el curso (feedback del trimestre)

El profesor recogió quejas del delegado: las clases son **muy técnicas y rápidas**, tanto en Ciber como en SER y otros módulos. La petición, tras una confusión inicial del propio profesor, es **más teoría y menos práctica**, o práctica "muy suavecita". Lo que se compromete a probar en el segundo trimestre:

- Laboratorios **mucho más explicados** (qué significa cada cosa), y dejados **antes de la clase**, para llegar con ellos vistos.
- **Más tiempo a la teoría** para que los puntos queden claros.
- Mantener lo esencial: romper contraseñas, ataques desde fuera, inicio del forense.
- Se puede hablar con él por **tutor, delegado o mensaje**; "no tomo represalias".
- **Siguiente bloque:** ataques de **phishing** y **redes** (audio: "fish and redes"; sin confirmar el título). Dice que "toca bastante Kali".

## Dudas y cosas sin confirmar

- **Los 3 intentos de un test:** un alumno preguntó si hay que hacer los 3 intentos para que cuente. Respuesta: **no, se queda la puntuación más alta**. No se dijo de qué test; es probable que fuera de otro módulo (en Sostenibilidad son 3 intentos, según el temario), **sin confirmar**.
- **Fecha de entrega** del apartado forense y **fecha de las notas**: no dadas.
- **Simulacro de Ciber:** precisado el 17/11 (publicado el viernes 20/11 y resuelto el martes 24/11).
- **Contenido del vídeo:** es el de Deloitte (PDF); no lo he visto. **Solución del Forense 3:** no recibida.
- **Forma del «caso práctico»:** audio (leer una instrucción) frente a PDF (interpretar un escenario). Sin confirmar.

## Logística y para llevar a casa

- [ ] Hacer el caso forense (RRHH o un Windows) y guardar **capturas + comandos** como evidencia.
- [ ] Mirar el **foro**: enlace al vídeo de la solución del Forense 3 y, el 17/11, el simulacro.
- [ ] Preparar el repaso: 4 fases del forense, orden de volatilidad, hash y cadena de custodia (examen, según la [clase 7](2026-10-27_clase7-analisis-forense.md)), más la lectura de comandos.
- [ ] La clase del **17/11** (repaso de temas y simulacro) ya está en su [nota](2026-11-17_repaso-simulacro-formato-examen-y-que-estudiar.md).
