---
asignatura: Ciberseguridad
fecha: 2026-11-10
tema: "Cierre del primer trimestre: opinión sobre el ritmo, repaso del Laboratorio 4 (forense), formato del examen y simulacro"
fuente: transcripción de la clase (22 min). Sin PDF ni diapositivas. El vídeo que se proyectó tiene el audio ilegible en la transcripción; no se ha podido recoger su contenido.
---
# Ciber · 10/11 · Cierre del trimestre, repaso del Lab 4 y cómo será el examen

> Anterior: [Lab 4 parte 2 (5/11): Sleuth Kit y Autopsy](2026-11-05_lab4-analisis-forense-sleuthkit-autopsy-caso-rrhh.md) · Profesor: Damián Sualdea Soy

Clase corta. La mayor parte se dedicó al ritmo del curso; lo técnico es poco: el cierre del tema forense y, sobre todo, **cómo será el examen** (esto último es lo útil).

> [!important] Lo imprescindible
> - **Examen de Ciber:** test + **preguntas cortas de desarrollo de 3-4 líneas**. El "caso práctico" **no es un caso real**: te dan una **instrucción con una herramienta** y tienes que **decir qué hace**. "No os voy a pedir crear instrucciones, os voy a pedir **leerlas**."
> - **Cómo se estudia (según él):** con el **repaso** y el **simulacro** "sería más que suficiente".
> - **Semana del 17/11:** una hora de **repaso de los puntos importantes de cada tema** con preguntas tipo examen. Después, el **simulacro**, que publica antes y resuelve en clase.
> - **Regla de oro del forense** (cierre del tema): "nunca hay que romper la prueba"; la evidencia se bloquea en **solo lectura** y se trabaja sobre una copia.

## El examen y el simulacro

| Dato | Qué dijo |
|---|---|
| Formato | **Test** + **preguntas cortas de desarrollo** (no más de 3-4 líneas en Ciber) |
| "Caso práctico" | Una **instrucción con nombre de herramienta** y la pregunta "¿qué crees que está haciendo?" |
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
- **Vídeo de la solución del Forense 3:** el audio salió ilegible. No pude recoger la solución. El profesor dijo que pondría **el enlace en el foro**: pendiente.
- **Historia de fondo (la que contó):** un ataque típico en una empresa: un **empleado** abre un correo o conecta un **USB** (se citó que el malware puede ir dentro de un **JPG**), le **roban las credenciales**, el atacante **entra**, **se lleva los datos**, **borra el rastro** y luego "lo acabas de investigar". Es el mismo hilo del caso RRHH (ver [nota del 5/11](2026-11-05_lab4-analisis-forense-sleuthkit-autopsy-caso-rrhh.md)): acceso, script con extensión falsa, robo y borrado. Citó a **Deloitte** como fuente de los vídeos (sin confirmar cuáles).
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
- **Simulacro de Ciber:** fecha de publicación y formato, no precisados.
- **Contenido del vídeo** del Forense 3: ilegible en el audio.

## Logística y para llevar a casa

- [ ] Hacer el caso forense (RRHH o un Windows) y guardar **capturas + comandos** como evidencia.
- [ ] Mirar el **foro**: enlace al vídeo de la solución del Forense 3 y, el 17/11, el simulacro.
- [ ] Preparar el repaso: 4 fases del forense, orden de volatilidad, hash y cadena de custodia (examen, según la [clase 7](2026-10-27_clase7-analisis-forense.md)), más la lectura de comandos.
- [ ] La clase del **17/11** (repaso de temas) no la tengo: si la pasas, la integro.
