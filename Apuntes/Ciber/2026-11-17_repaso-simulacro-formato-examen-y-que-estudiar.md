---
asignatura: Ciberseguridad
fecha: 2026-11-17
tema: "Repaso del primer trimestre (Temas 1-4) y simulacro: formato del examen, qué estudiar por apartado y tipo de preguntas"
fuente: transcripción de la clase (55 min) + lista de apuntes de Dani + **PDFs del profesor recibidos el 25/11**: `CIBER_Clase10_diapositivas.pdf` (20 diapositivas), `CIBER_Repaso_T1-4.pdf` (3 págs.), `CIBER_Guia_estudio_T1.pdf` (3) y `CIBER_Repaso_expres_simulacro.pdf` (1). Donde difieren del audio, manda el PDF. No recibido: el documento del simulacro del 24/11. Contrastado con el temario `Ciberseguridad/cs_tema01…04` y con mis notas anteriores de Ciber.
---
# Ciber · 17/11 · Repaso para el simulacro: qué entra y cómo se pregunta

> Anterior: [Cierre del trimestre y formato del examen (10/11)](2026-11-10_cierre-trimestre-repaso-lab4-y-formato-examen.md) · Profesor: Damián Sualdea Soy

El profesor repasa los cuatro temas del trimestre con unas diapositivas, indica **en qué apartados del temario hay que centrarse** y explica **cómo pregunta**. Lo que dijo del examen coincide con lo del 10/11 y añade detalles (sin penalización, hojas limitadas, qué comandos pueden salir).

> [!important] Lo imprescindible
> - **Estructura (la misma del examen presencial de mayo, "no la cambio"):** **15 preguntas de test** + **preguntas cortas** (3-4 líneas) + **bloque de interpretar comandos** (te da el comando y/o su salida y preguntas "¿qué está pasando aquí?"). "Preguntas cortas, bloque de interpretar código y fin."
> - **El test no penaliza nunca** ("no penalizo nunca").
> - **Hay que leer comandos, no escribirlos** ni memorizar parámetros: "no os voy a pedir crear instrucciones".
> - **El simulacro no puntúa**: antes valía, ahora "es para que entrenéis".
> - **Lo publica el viernes 20/11 y lo resuelve en clase el martes 24/11.** Está pensado para **50 minutos + 10 de revisión**. Puedes hacerlo en casa (a boli y papel, como práctica) y compararlo el martes.
> - **No se pide hacer forense**, solo conceptos: cadena de custodia, `dd`, hash y bloqueo en solo lectura.
> - **Jamás «encriptar»:** lo repitió en serio (−0,25 por aparición, y solo lo perdonaría con una sonrisa al lado, en broma). Usa **cifrar/descifrar**.

> [!warning] Actualización 25/11: los PDFs corrigen el audio en tres puntos
> 1. **«Dimensionar el SAI no entra» (audio) → SÍ entra (PDFs).** El repaso, la guía y la hoja exprés lo ponen en el test y en «interpretar»: **vatios ÷ 0,6 ≈ VA**; ejemplo: **170 W → ~283 VA → SAI de 500–650 VA**; en Linux se vigila con **NUT**. **Estúdialo**: si el audio tenía razón, solo has perdido un minuto.
> 2. **Tema 2: 2.2 y 2.3 «enteros»** (PDF), no «por encima» ni «solo los tipos de SAI» (audio). Son «pocas páginas».
> 3. **Autenticidad y no repudio «son complemento, no están en el material del Tema 1»** (PDF). Tus cuatro pilares (fiable, confidencial, íntegro, disponible) son los que entran.
> Además: el PDF añade **qué dejar** (MITRE ATT&CK, bug bounty, precios de Zerodium/Pwn2Own, CPD por el mundo, escítala/César/Vigenère/Enigma, detalle de Torres de Hanói, estándares forenses de memoria) y **«los cuatro que hay que saber leer»** (ver abajo).

## Qué estudiar por apartado del temario (según el profesor)

| Tema | Apartados | Cómo los trató |
|---|---|---|
| 1 | **1.2** (confidencialidad, integridad, disponibilidad), **1.3** (elementos vulnerables), **1.5** (amenazas) | La 1.2 y la 1.5 son lo "gordo, gordo"; de la 1.3 "tampoco pregunto mucho". **PDF:** el **1.4 es contenido forense**: repásalo con el Tema 4; «A fondo» y Entrenamientos, fuera |
| 2 | **2.2** (protección física: incidentes, acceso físico, factores ambientales) y **2.3** (SAI: tipos) | La 2.2 tiene mucha información: léela por encima. De la 2.3 solo los **tipos de SAI**. ~~**Dimensionar no entra**~~ (audio: "olvidaros dimensionar"): **el PDF lo incluye, estúdialo**. **PDF:** 2.2 y 2.3 **enteros**. Los apartados "A fondo": ignóralos (el PDF dice que el de este tema es una errata del material) |
| 3 | **3.2** (criptografía y hash), **3.3** (contraseñas y almacenamiento), **3.4** (copias) | La 3.4 es **lectura ligera**: "4 puntitos básicos, el resto me da igual". **PDF:** estudia 3.2, 3.3 y 3.4; **la lectura ligera es la 3.5** (medios de almacenamiento). Es «el tema que más entra» (test e interpretar) |
| 4 | **4.2** (metodología forense), **4.3** (estándares), **4.4** (documentación e informe) | La 4.3 (ISO 27037, RFC 3227, UNE 71505/71506) es "muchísimo": solo **resumen básico**. La 4.4 (ficha técnica, informe): por encima |

- Mencionó un "1.8", que **no existe** en el temario (el Tema 1 acaba en la 1.6): audio confuso, **sin confirmar** a qué se refería (es probable que fuera la 1.2).
- **Cómo estudiar:** "repasar no es volver a leerlo". Haz **respuestas cortas de 2-3 líneas** a las preguntas de abajo y repasa las actividades/entrenamientos del temario (el audio es confuso aquí: **sin confirmar** si se refería a los Entrenamientos del temario o a los laboratorios). "No voy a salirme del texto."

## Tu lista, contrastada (notas de Dani)

| Tu nota | Veredicto |
|---|---|
| "Los 4 pilares: fiabilidad, confidencialidad, integridad y disponibilidad. Apoyar con no repudio" | **Correcto (corregido con el PDF).** El temario sí lista esos cuatro. Pero el profesor trabaja con la **tríada CIA** (confidencialidad, integridad, disponibilidad) y la **agrupa con autenticidad y no repudio**; **el PDF aclara que autenticidad y no repudio son complemento y no están en el material del Tema 1**: no te falta nada; tu «apoyar con no repudio» vale como extra. Además define "fiable" como "el sistema hace lo que debe, funciona correctamente", y recuerda la trampa de la [clase 2](2026-09-22_clase2-pilares.md): **fiabilidad ≠ disponibilidad** |
| "Vulnerabilidad, amenaza, riesgo, CVE y CVSS" | **Correcto.** Pregunta explícita: "diferencia entre vulnerabilidad, amenaza y riesgo", y "qué es un CVE y un CVSS y dónde se consultan" (ver abajo). Matiz: él pide **contrastarlos con tus palabras y un ejemplo** |
| "CPD: refrigeración, incendios, acceso físico" | Correcto. Añade: el CPD **tradicional frente al modular**, y que lo importante es la **seguridad física** |
| "Niveles tier: los nueves, la disponibilidad" | Correcto, y falta lo que añadió: **no solo los nueves**, también **redundancia** (nodos, doble acometida eléctrica). Es como una **certificación** del CPD. Pregunta: "qué niveles de Tier hay y qué mide cada uno" |
| "SAI: tipos" | Correcto (offline y online que citó; ver la [clase 4](2026-10-06_clase4-seguridad-fisica-sai.md) para los tres tipos). Pregunta: **para qué sirve un SAI y qué pasa cuando se va la luz**. **PDF:** tres tipos (**offline, línea interactiva, online**) y **dimensionado** (vatios ÷ 0,6 ≈ VA) |
| "Instrucciones de John the Ripper. Interpretarlas" | Correcto. Él dice que no hay que saber `-w` ni `-format`, sino **intuir**: "está rompiendo un hash MD5 con esta wordlist" |
| "Tipos de cifrados: simétrico, asimétrico, hash" | **Incorrecto en el tercero:** el **hash no es cifrado** ("no hay vuelta atrás"). Tampoco lo es **Base64** (es una codificación para transportar datos). Las familias son: simétrico, asimétrico y **hash (que no cifra)** |
| "Algoritmos de cada cifrado" | Te falta la lista (ver tabla abajo) |
| "Ubicación de las contraseñas: /etc/shadow" | Correcto (Linux). Es el hash con sal (`$6$…` = SHA-512), no la contraseña |
| "Sal para endurecer las contraseñas" | Correcto, con matiz técnico (ver abajo) |
| "Regla de copias 3-2-1" | Correcto. Falta lo que dijo que cae: **qué NO es copia de seguridad (RAID)** |
| "Cadena de custodia: quién toca y qué" | Falta el **cuándo y dónde**: "¿quién tocó la prueba, cuándo y dónde?". Si se rompe la cadena, "la prueba ya no vale absolutamente para nada" |
| "Imagen forense: copia bit a bit (dd)" | Correcto. Pregunta posible: "¿para qué se utiliza un `dd`?" |
| "Hash del disco y la copia" | Correcto. Pregunta literal: **"¿por qué se calcula el hash antes y después de copiar un disco?"** → para probar que la copia es idéntica |
| "Bloquear disco e imagen para trabajar" | Correcto como **concepto** (bloqueo en solo lectura). El profesor dijo que **probablemente no pone** la instrucción de bloqueo (`losetup -r`); si pone solo `dd`, "solo os pregunto temas del `dd`" |
| **Te falta** | 4.3 y 4.4 (resumen básico: ISO 27037, RFC 3227, UNE 71505/71506, ficha técnica); **Autopsy** como concepto (ver abajo); el formato del examen (15 test, sin penalización, comandos) y que **dimensionar el SAI no entra** |

## Resumen por tema (lo que dijo)

### Tema 1 · Qué se protege y dónde falla
- **Fiable**: el sistema hace lo que debe y funciona correctamente. **Confidencial**: solo lo ve quien debe (se rompe, p. ej., espiando el tráfico). **Íntegro**: nadie lo ha modificado; se comprueba con **hash (SHA-256)**. **Disponible**: accesible cuando hace falta; lo revienta un **DoS**. **No repudio**: quien hizo algo no puede negarlo. Él las agrupa con la **autenticidad**.
- **Vulnerabilidad**: un fallo, "una puerta mal cerrada" (ejemplo: **vsftpd 2.3.4**, el de Metasploitable). Si nadie la conoce es un **0-day**.
- **Amenaza**: lo que puede aprovecharla y afectar a un activo: un **malware** de cualquier tipo, un **atacante** o un **incendio** (natural). Es "el que quiere entrar por esa puerta".
- **Riesgo**: la **probabilidad** de que la amenaza se materialice y produzca un **impacto** sobre el activo.
- **CVE**: identificador (**año + número**) de una vulnerabilidad conocida. **CVSS**: la **puntuación de gravedad de 0 a 10** (rojo, amarillo, verde). Se consultan en **NVD** y **CVE Details** (audio confuso con "V de tails"; ver [clase 3](2026-09-29_clase3-donde-falla-un-sistema.md)).

### Tema 2 · Seguridad física y SAI
- **CPD**: edificio con salas para servidores, con **refrigeración**, **protección contra incendios** y **control de acceso físico**; hay **tradicional** y **modular** (lo más reciente).
- **Tier I-IV**: nivel de disponibilidad medido por el **número de nueves**, más la **redundancia** (nodos, doble acometida eléctrica). Funciona como una **certificación**.
- **SAI**: batería que **protege el equipo cuando falla la luz**, para que no sufra una caída brusca, mientras entra un generador. Tipos citados: **offline** y **online**.

> [!warning] Una cifra del audio que no cuadra
> Explicando los Tier, dijo que con un 99,99 % el servidor estaría "a lo mejor **2 horas** parado al año". **No cuadra:** el 99,99 % son **unos 53 minutos al año** (0,01 % de 8 760 h ≈ 0,88 h). Las cifras de la [clase 4](2026-10-06_clase4-seguridad-fisica-sai.md) (Tier 3 ≈ 1,6 h, Tier 4 ≈ 26 min) son las que manda tener. Para el test, quédate con la idea (**más nueves = menos tiempo caído**), no con el "2 h". (cálculo mío)

### Tema 3 · Cifrar, romper y salvar

| Familia | Idea | Algoritmos que citó |
|---|---|---|
| **Simétrico** | **Una misma clave** cifra y descifra. Rapidísimo; el mejor con muchos datos | **AES** (el actual), **DES** (vulnerable), **3DES** (menos vulnerable), **RC4** (dijo "creo que RC4"; **el PDF lo confirma como roto**, igual que DES, MD5 y SHA-1; bien: AES, RSA, SHA-256). Hay unos vulnerables y otros no |
| **Asimétrico** | **Clave pública y privada**; además de cifrar, **firma y autentica** | **RSA**, **curva elíptica** (lo ampliará en el 2.º trimestre con la PKI) |
| **Hash** | **No cifra**, no tiene vuelta atrás; huella de un contenido. Sirve para **integridad** y para **guardar contraseñas** | **SHA-256** (el que se ha usado; en el audio sale roto como "SHA 200…") |

> [!warning] Dos imprecisiones del audio
> 1. Al explicar la **asimétrica** dijo "con la misma clave que cifro es con la misma con la que descifro". Eso describe la **simétrica**. Es probable que sea un lapsus o un fallo de transcripción; para el examen, **asimétrica = par de claves**.
> 2. Sobre la **sal** dijo que sirve "para que no se pueda ir hacia atrás". Lo que **impide ir hacia atrás es el hash**. La sal (un valor aleatorio añadido antes de hashear) hace que **dos contraseñas iguales den hashes distintos** y **inutiliza las tablas precalculadas** (mío, coherente con la [clase 6](2026-10-20_clase6-contrasenas-copias.md)). En un examen, puedes decir ambas: "evita ir hacia atrás con tablas y con diccionarios masivos".

- **Dónde están las contraseñas en Linux:** `/etc/shadow` (el audio dice "arrasado" y una segunda ubicación que no se entiende; sin confirmar). Guardan **hash + sal**.
- **Contraseña larga > corta y complicada** (por el espectro de combinaciones; se vio con `crunch` y Hive).
- **Copia 3-2-1:** **3 copias** (la original + 2), en **2 soportes distintos**, y **1 fuera del sitio** (p. ej. la nube).
- **Qué NO es copia de seguridad:** **RAID** (el profesor insiste: el INCIBE lo pone como copia y él no lo comparte). Confírmalo con la [clase 6](2026-10-20_clase6-contrasenas-copias.md): RAID protege de que falle un disco, no de borrar un fichero. **PDF:** hay tres cosas que **no** son copia: un **RAID**, **sincronizar con la nube** (replica también el borrado o el cifrado del ataque) y **una copia que nunca has restaurado**.

### Tema 4 · Forense
- **Cadena de custodia:** quién tocó la prueba, **cuándo y dónde**. Si se rompe, la prueba no vale.
- **Imagen forense:** copia **bit a bit** del disco (`dd`). **Hash** del disco y de la copia: si coinciden, es la misma.
- **Bloqueo:** se trabaja con la evidencia en **solo lectura**.
- **Autopsy**, como concepto: *software* forense que permite trabajar con la imagen, sacar la **línea temporal**, ver **ficheros borrados** y **metadatos**. **No habrá que analizar nada** en el examen.
- **Informe ejecutivo:** "tampoco os voy a pedir eso".

## Cómo preguntará (ejemplos suyos)

**Preguntas cortas** (3-4 líneas; "si ya me lo cuentas en 4 líneas, no me pongas 8"):
- Diferencia entre **vulnerabilidad, amenaza y riesgo** (con tus palabras).
- Qué es un **CVE** y un **CVSS** y **dónde se consultan**.
- Qué **niveles de Tier** hay y qué mide cada uno.
- **Para qué sirve un SAI** y qué pasa cuando se va la luz.
- **Cómo rompe un atacante una contraseña** y qué hace que **sea fuerte**.
- Qué dice la **regla 3-2-1** y qué **no** es una copia de seguridad.
- **Por qué se calcula el hash antes y después** de copiar un disco.

**Bloque de comandos** (te da el comando y la salida; tú lo lees):
- `nmap -sV`: leer **puerto, servicio y versión** de la salida.
- **John the Ripper** con wordlist (p. ej. `rockyou`) o con formato (p. ej. `md5`): "está rompiendo contraseñas de un fichero con un diccionario".
- `dd`: "una copia exacta de un disco".
- **Hash** (`sha256sum`, y el audio dice "los 5 o 6…" sin aclarar; **sin confirmar**).
- Los **datos de un CVE** y qué significa su CVSS.

> [!important] Los cuatro de «interpretar» que «salen seguro» (PDF, diapositiva 16 y hoja exprés)
> El bloque 3 **«es el que más puntúa y el que delata quién hizo los laboratorios»**. Estructura del simulacro (PDF): **60 min, sobre 10, sin ordenador**; bloque 1 test de 15 (sin penalización), bloque 2 tres cortas (3-4 líneas) y **bloque 3: cuatro ejercicios de leer un comando o salida**.
> 1. **`nmap -sV`** → leer puerto, servicio y versión; detectar una **versión con fallo conocido** (vsftpd 2.3.4) y buscarla en el NVD.
> 2. **`unshadow /etc/passwd /etc/shadow` + `john --wordlist=rockyou.txt`** → por qué cae la contraseña **corta o de diccionario** y no la larga y aleatoria.
> 3. **`dd if=/dev/sdb of=evidencia.img` + `sha256sum` antes y después** → por qué los dos hash tienen que coincidir.
> 4. **Ficha CVSS:** **9.8 = crítico** (grave y fácil de explotar); qué herramienta usarías (**Metasploit**) y cómo te proteges (**parchear o mitigar**).
> **La guía añade** (Tema 3, «interpretar»): **`gpg -c`** para cifrar, **`rsync` + `cron`** para una copia programada y **probar la restauración**. **(Mío)** El PDF no cita `losetup -r` ni `openssl enc`, que sí aparecen en mi práctica: valen como ejercicio, no los des por examinados.

## Examen de mayo (para situarte)

- **Presencial.** Hay **ordinaria y extraordinaria**; la evaluación continua **se mete en la ordinaria**. La **extraordinaria** es solo examen (unos 15-20 días después), "vas a full con lo que saques".
- **10 temas** en mayo (hoy solo 4): mismo formato, pero con **más comandos** y preguntas de desarrollo cortas. Si un tema cae en el test, **no cae en el desarrollo**: "juego muchísimo".
- **Dos modelos** (A y B); "no tengo ni idea" de cuál tocará. Los exámenes "no tienen sorpresas".
- **Hojas:** el enunciado va seguido, luego una hoja en blanco y **2-3 hojas para responder; no hay más**. No te alargues.
- **Duración:** "es una hora de examen": no puede preguntar todo.

## Dudas y cosas sin confirmar

- ✅ **Diapositivas de repaso (20) y documentos de repaso:** recibidos el 25/11. **Documento del simulacro del 24/11:** sigue sin recibir (ni su corrección).
- ✅ **Fecha de la coordinación:** el PDF dice «En Archivos unos días antes, enlazado desde el tablón. **Coordinación avisa el 16**»; el simulacro es el **martes 24/11 a las 19:00** («esta misma hora»). El «viernes 20/11» del audio queda como fecha aproximada de publicación.
- **Clase del jueves 19/11:** preguntó si había clase y respondió con algo ininteligible: **sin confirmar** si hay clase de Ciber.
- **"Hay dos repasos":** se lió con la numeración de las clases (la de hoy es "clase 10", el repaso completo) y dijo que **no había subido** la anterior; irrelevante para el examen.
- **Sin confirmar:** el "1.8", el segundo ejemplo de comando de cifrado (CBC), la segunda ubicación de contraseñas y el comando de *hash* "de los 5 o 6".
- Dejé fuera las intervenciones de compañeros y el rato final de notas de otras actividades.

## Logística y para llevar a casa

- [ ] **Viernes 20/11:** bajar el simulacro del foro/tablón y hacerlo en casa (50 min, a boli y papel).
- [ ] **Martes 24/11:** llevarlo hecho a clase para la corrección.
- [ ] Preparar respuestas de 3-4 líneas a las 7 preguntas de arriba y practicar **leer comandos** (bloque de abajo).
- [ ] Leer **1.2, 1.3, 1.5 (y el 1.4 con el Tema 4), 2.2 y 2.3 enteros, 3.2-3.4, 4.2-4.4** (3.5 y 4.3 por encima). **Estudia el dimensionado del SAI.**
- [ ] Mirar si llega la nota de la actividad forense (la tiene corregida pero sin subir).

---

# Práctica

> Primero los ejercicios; **las pistas y las soluciones, al final**. Hazlos a boli y papel, sin mirar. Los niveles van de lo simple a lo complejo.

## Nivel 1 · Test (como las 15 del simulacro; sin penalización)

1. Un fallo en un programa que un atacante puede aprovechar es: a) una amenaza · b) una vulnerabilidad · c) un riesgo · d) un activo.
2. La probabilidad de que una amenaza aproveche una vulnerabilidad y cause un impacto es: a) el riesgo · b) la amenaza · c) el CVE · d) el hash.
3. El **CVSS** es: a) un identificador de vulnerabilidad · b) una puntuación de gravedad de 0 a 10 · c) un antivirus · d) un algoritmo de cifrado.
4. Un ataque de denegación de servicio (DoS) afecta sobre todo a: a) la confidencialidad · b) la integridad · c) la disponibilidad · d) la autenticidad.
5. Un hash de un fichero sirve sobre todo para comprobar su: a) confidencialidad · b) integridad · c) disponibilidad · d) velocidad.
6. ¿Cuál de estos **no** cifra? a) AES · b) RSA · c) SHA-256 · d) 3DES.
7. Es un algoritmo **asimétrico**: a) AES · b) RSA · c) DES · d) RC4.
8. En Linux, los hashes de las contraseñas de los usuarios están en: a) `/etc/hosts` · b) `/etc/shadow` · c) `/var/log/auth.log` · d) `/home`.
9. Frente a un ataque por diccionario o fuerza bruta, es mejor: a) 8 caracteres con símbolos · b) una frase larga · c) el nombre de tu mascota con un 1 · d) la misma contraseña en todo.
10. La regla 3-2-1 dice: a) 3 copias, 2 soportes distintos, 1 fuera del sitio · b) 3 discos, 2 usuarios, 1 nube · c) 3 días, 2 semanas, 1 mes · d) 3 hashes, 2 claves, 1 sal.
11. ¿Cuál **no** es una copia de seguridad? a) Un `rsync` a otro disco · b) Una copia en la nube · c) Un RAID · d) Un snapshot guardado fuera.
12. Un SAI que da corriente constante, sin el pequeño salto al cortarse la luz, es el: a) offline · b) online (doble conversión) · c) un regulador de enchufe · d) un generador.
13. Los niveles **Tier** de un CPD miden: a) el número de salas · b) la disponibilidad y la redundancia · c) el tamaño · d) el consumo de agua.
14. `dd` se usa en forense para: a) borrar un disco · b) copiar bit a bit · c) romper contraseñas · d) cifrar.
15. Calcular el hash del disco y de su copia y ver que coinciden demuestra que: a) el disco está limpio de virus · b) la copia es idéntica · c) el disco no es sospechoso · d) el disco está cifrado.

## Nivel 2 · Preguntas cortas (3-4 líneas cada una)

16. Diferencia entre **vulnerabilidad, amenaza y riesgo**, con un ejemplo que los una.
17. Qué es un **CVE**, qué es un **CVSS** y **dónde** se consultan.
18. ¿Para qué sirve un **SAI** y qué pasa cuando se va la luz?
19. ¿Qué mide un **Tier** y por qué no basta con los nueves?
20. ¿Cómo rompe un atacante una contraseña y qué hace que sea fuerte?
21. ¿Por qué una contraseña **larga** aguanta más que una **corta y complicada**?
22. ¿Qué dice la regla 3-2-1 y por qué un **RAID** no es una copia de seguridad?
23. ¿Por qué se calcula el **hash antes y después** de copiar un disco?
24. ¿Qué es la **cadena de custodia** y qué pasa si se rompe?
25. Diferencia entre **cifrar**, **hashear** y **codificar en Base64**.

## Nivel 3 · Interpretar comandos (un comando o salida; ¿qué hace?)

26. ```
    $ nmap -sV 192.0.2.10
    PORT   STATE SERVICE VERSION
    21/tcp open  ftp     vsftpd 2.3.4
    22/tcp open  ssh     OpenSSH 4.7p1
    80/tcp open  http    Apache httpd 2.2.8
    ```
    a) ¿Qué ha hecho? b) ¿Qué servicios y versiones hay? c) ¿Qué conclusión de seguridad sacas del FTP, si supieras que esa versión tiene un CVE grave?
27. ```
    $ john --wordlist=/usr/share/wordlists/rockyou.txt --format=raw-md5 hash.txt
    ```
    ¿Qué está haciendo? ¿De qué es `rockyou`? ¿Qué te dice `raw-md5` del contenido de `hash.txt`?
28. ```
    $ sudo dd if=/dev/sdb of=imagen.dd bs=4M status=progress
    ```
    ¿Qué hace cada parte? ¿Qué es `sdb` en este caso y por qué escribir en un fichero `.dd`?
29. ```
    $ sha256sum disco.img imagen.dd
    7c1e4a…b930  disco.img
    7c1e4a…b930  imagen.dd
    ```
    ¿Qué demuestra? Y si el segundo acabara en `…b931`, ¿qué concluyes y qué haces?
30. ```
    ana:$6$Zx9k$Qp2…:19800:0:99999:7:::
    ```
    ¿De qué fichero es esta línea? ¿Qué contiene el segundo campo? ¿Qué significa `$6$` y qué es `Zx9k`?
31. ```
    $ sudo losetup -r -f --show disco.img
    /dev/loop0
    ```
    ¿Qué hace la opción `-r` y por qué es importante en forense?
32. ```
    $ openssl enc -aes-256-cbc -salt -in notas.txt -out notas.enc
    ```
    ¿Es simétrico o asimétrico? ¿Se puede deshacer y con qué? ¿Es un hash?

## Nivel 4 · Integración

33. **Caso:** te entregan un disco de un portátil con sospecha de fuga de datos. Ordena y justifica (5-6 líneas) los pasos hasta tener algo analizable, usando: cadena de custodia, bloqueo, `dd`, hash.
34. **CVE:** ves esta ficha (inventada): `CVE-2026-0000 · servidor web X 1.2 · CVSS 9.8 · crítica · ejecución remota`. Explica a un directivo qué es cada dato y qué riesgo supone.
35. **Redacta una respuesta de examen** de 4 líneas máximo a: «¿Qué pasa si un SAI se queda sin batería durante un corte largo, y qué más necesita un CPD de Tier alto?».


## Nivel 5 · Añadidos tras recibir los PDFs (25/11)

36. **Dimensionar:** un equipo consume 120 W. Con la regla del PDF, ¿cuántos VA necesitas como mínimo y qué SAI comprarías?
37. Lee y explica: `gpg -c informe.txt` y, en el `crontab`, `0 2 * * * rsync -a /datos/ /mnt/copia/`. ¿Qué te falta para fiarte de esa copia?
38. Ficha: «CVSS 9.8 · crítica». ¿Qué te dice la nota, qué herramienta usarías para comprobar si tu servidor es explotable y cómo te proteges?

---

## Pistas (antes de mirar las soluciones)

- **1-5:** recuerda las definiciones de una frase. En 4, piensa qué se ataca: que el servicio **funcione**.
- **6-7:** el hash **no cifra**; asimétrico = par de claves; en la lista, solo uno trabaja con par de claves.
- **8-11:** ruta de Linux con el **hash**, la sal y la regla de los números. El RAID falla al **borrar**.
- **12-13:** online = doble conversión; Tier = nueves **y** redundancia.
- **16:** ejemplo: una puerta mal cerrada (fallo), quien quiere entrar (amenaza) y la probabilidad de que lo haga (riesgo).
- **20-21:** piensa en cuántas combinaciones hay y en el diccionario.
- **26-32:** lee de izquierda a derecha: herramienta → opciones → entrada → salida. No tienes que saber qué hace cada opción: intuye.
- **29:** un solo carácter distinto cambia el hash entero.
- **33:** primero **no tocar** lo original.

## Soluciones

> No mires antes de haber intentado los ejercicios.

**Nivel 1:** 1-b · 2-a · 3-b · 4-c · 5-b · 6-c · 7-b · 8-b · 9-b · 10-a · 11-c · 12-b · 13-b · 14-b · 15-b.

**Nivel 2 (modelos de respuesta)**

16. **Vulnerabilidad:** un fallo (p. ej. vsftpd 2.3.4 con puerta trasera). **Amenaza:** lo que puede aprovecharlo (un atacante, un malware, un incendio). **Riesgo:** la probabilidad de que la amenaza aproveche la vulnerabilidad y cause un impacto sobre un activo.
17. **CVE:** identificador público de una vulnerabilidad conocida (año + número). **CVSS:** puntuación de gravedad de 0 a 10. Se consultan en **NVD** y **CVE Details**.
18. Un **SAI** es una batería que mantiene el equipo encendido si falla la luz, para evitar una caída brusca y dar tiempo a un apagado ordenado o a que arranque un generador. Cuando se va la luz, el SAI pasa a batería (el **online** sin salto, el **offline** con un pequeño corte).
19. Un **Tier** mide la **disponibilidad** (nueves) y la **redundancia** (nodos, doble acometida eléctrica); por eso funciona como una certificación del CPD. Los nueves solos no dicen cómo está montado.
20. Por **diccionario** (probar contraseñas habituales, p. ej. rockyou), **fuerza bruta** (probar combinaciones) o robando el hash. Es fuerte si es **larga**, no es previsible y está guardada con **hash + sal**.
21. Porque el número de combinaciones crece más rápido con la **longitud** que con añadir símbolos, y las cortas caen antes por fuerza bruta; además, las largas (frases) no suelen estar en diccionarios.
22. **3 copias** (original + 2), en **2 soportes distintos**, **1 fuera del sitio**. Un **RAID** protege de que un disco falle, pero si **borras** un fichero desaparece de todos los discos a la vez; no es una copia.
23. Para **probar que la copia es idéntica** al original; si coinciden, la evidencia no se ha alterado y se puede trabajar con la copia.
24. Es el registro de **quién tocó la prueba, cuándo y dónde**. Si se rompe, **la prueba deja de valer**.
25. **Cifrar:** transformar con una clave y poder **volver atrás** con la clave. **Hashear:** huella **sin vuelta atrás** (no cifra). **Base64:** **codificación** para transportar datos, **sin secreto**; cualquiera la revierte.

**Nivel 3**

26. a) Escanea los puertos de esa IP y **detecta servicio y versión** (`-sV`). b) FTP **vsftpd 2.3.4**, SSH **OpenSSH 4.7p1**, web **Apache 2.2.8**. c) Si esa versión de vsftpd tiene un CVE grave, es **vulnerable**: se debería actualizar o cerrar el servicio.
27. Intenta **romper hashes** de `hash.txt` probando palabras de un **diccionario** (`rockyou` es una lista muy usada de contraseñas filtradas). `raw-md5` indica que son **hashes MD5 sin sal**.
28. `dd`: copia bit a bit; `if=` entrada, `of=` salida, `bs=4M` bloques de 4 MB, `status=progress` muestra el avance. `/dev/sdb` es **un disco** (la evidencia, o un dispositivo loop). Se guarda en un fichero para **trabajar sobre la copia**.
29. Coinciden: **la copia es idéntica**. Si cambia: **no es idéntica**; **no sirve como evidencia**: repites la copia y documentas el fallo.
30. Es de **`/etc/shadow`** (Linux). El segundo campo es el **hash de la contraseña con sal**. `$6$` indica **SHA-512**; `Zx9k` es la **sal**.
31. `-r` la abre en **solo lectura**: no se puede alterar la evidencia (el bloqueo). Además enlaza el fichero como dispositivo (`/dev/loop0`) **sin montar el sistema de ficheros**.
32. **Simétrico** (AES, una clave). Se deshace con la **misma clave** (`openssl enc -d …`). **No** es un hash.

**Nivel 4**

33. 1) Documentar la **cadena de custodia** (quién lo recibe, cuándo y dónde). 2) **Bloquear** el disco en solo lectura. 3) Calcular el **hash** del original. 4) Hacer la **copia bit a bit** con `dd`. 5) Calcular el hash de la copia y comprobar que **coincide**. 6) Trabajar **solo sobre la copia** y guardar el original.
34. **CVE:** identificador del fallo. **CVSS 9.8:** gravedad de 0 a 10; es **crítica**. **Ejecución remota:** un atacante podría ejecutar órdenes sin estar en la red local. **Riesgo:** alto si el servidor es accesible y no está parcheado; hay que **actualizar** o **mitigar** ya.
35. Si la batería se agota, el equipo **cae** salvo que entre un **generador**. Un CPD de Tier alto tiene **redundancia** (varios SAI, **doble acometida eléctrica**, nodos duplicados), para mantener la disponibilidad ante un fallo.

**Nivel 5 (modelos; mis soluciones, aplicando la regla del PDF)**

36. 120 W ÷ 0,6 = **200 VA** como mínimo; comprarías un SAI con margen (el ejemplo del PDF pasa de 283 VA a un SAI de 500-650 VA; por analogía, uno de ~500 VA). (mío: la elección comercial concreta.)
37. `gpg -c` cifra el fichero con **una contraseña (cifrado simétrico)** y crea `informe.txt.gpg`. La línea de cron copia con `rsync -a` **cada día a las 02:00** `/datos/` en `/mnt/copia/`. Para fiarte, **hay que probar la restauración**: una copia que nunca has restaurado no cuenta (PDF); y falta aplicar la 3-2-1 (un soporte y una copia fuera).
38. **9.8 sobre 10 = crítico**: grave y fácil de explotar. Con **Metasploit** compruebas si tu servidor es explotable. Te proteges **parcheando** (actualizar) o **mitigando** (cerrar el servicio, cortafuegos…).
