---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-11-18
tema: "Repaso del trimestre (Temas 1, 2 y 3) y formato del simulacro del 25/11"
fuente: transcripción de la clase del **18/11** (1 h 7 min) + **PDFs de la Clase 10 recibidos el 25/11**: diapositivas `SAD_Clase10_diapositivas.pdf` (23 págs.) y `SAD_Clase10_Guia_repaso.pdf` (2 págs.) + lista de contenidos que copió Dani. Contrastado con los Temas 1-3 del temario y con las notas anteriores de SAD. Donde el PDF y el audio difieren, manda el PDF.
---
# SAD · Repaso Temas 1-3 y simulacro (18/11)

> Anterior: [Tema 3 (11/11): cron, ventana, rotación GFS/Hanoi, política](2026-11-11_tema3-cron-ventana-rotacion-gfs-hanoi-politica.md) · Profesor: Damián Sualdea Soy

Clase de repaso, sin contenido nuevo evaluable. El profesor recorre los tres temas, explica **cómo es el simulacro** y da consejos de estudio. Convención: **(clase)** = audio; **(PDF de Dani)** = la lista que pasó Dani; **(temario)** = Temas del repo; **(mío)** = añadido por mí.

> [!note] Actualización 25/11: PDFs recibidos
> La clase de repaso fue el **miércoles 18/11** («Clase 10 · 18 de noviembre» en las diapositivas del 11/11; el audio es del 18-11). El **20/11** que mencionabas es, como mucho, la fecha en que se publicaba el simulacro. Con la **guía de repaso** y las **diapositivas** recibidas he fijado qué entra, la **hora del simulacro (19:00)** y varias dudas; ver la sección «Lo que fija el PDF». **Sigo sin tener el simulacro.**

## Lo imprescindible

> [!important] Simulacro: lo que dijo
> - **Miércoles 25/11, en clase; lo corrige él allí mismo.** **No cuenta para la nota.**
> - Entra **solo lo de los Temas 1, 2 y 3** ("absolutamente todo lo que hemos visto en clase").
> - **Estructura:** **test de 15 preguntas** (cifra del audio) + **preguntas cortas** + **casos prácticos** (**interpretar un `crontab`**, **una restauración** o **dibujar un esquema**). **PDF (diapositiva 17 y 21): sí entra dibujar el esquema 3-2-1 de un servidor** («las tres copias, los dos soportes y la que va fuera»). Resuelto: **prepáralo**.
> - **Cuándo y dónde:** **miércoles 25/11 a las 19:00**, «en nuestra franja de siempre» (diapositiva 17). Lo tendrás **en Archivos y en el foro**; el audio decía que lo subía el 19/11 (mi nota anterior: 20/11): **no hay fecha en el PDF**, mira el aula.
> - **Cómo prepararlo (su consejo):** estudiar los apuntes, hacerlo **en papel, con cronómetro de 60 min**, sin mirar; fallar no penaliza.
> - **Estilo del examen:** de **comprensión, no de recitar**. «No quiero parrafadas». Preguntas cortas y **casos prácticos** tipo entrevista de trabajo («te pongo un caso y me lo resuelves»). El de mayo irá igual.

## Qué estudiar, según el profesor

Los apartados que cita (en el audio salen con números confusos; contrastados con el temario):

| Tema | Qué entra (lista del PDF de Dani) | Apartados (temario, **sin confirmar** el rango exacto) |
|---|---|---|
| **1** | Tríada **CID**; **activos, amenazas, vulnerabilidades y riesgo**; **medidas de protección** (preventiva/detectora/correctora); activa/pasiva y física/lógica | **1.2 a 1.7** (confirmado por la guía) |
| **2** | **CPD**; **SAI**; **climatización e incendios**; qué protege la pasiva física | **2.2 y 2.3** (confirmado por la guía) |
| **3** | **Copias**: tipos, regla **3-2-1** (con dibujo); **frecuencia, RPO y ventana de copia**; **`tar`/`rsync`/`cron`**; restauración y comprobaciones | **3.2, 3.3 y 3.4** (confirmado por la guía) |

> [!note] «Seguridad activa» en tu lista: resuelto
> La guía la sitúa en el **Tema 1**: «**diferenciar seguridad activa y pasiva, y física y lógica**». No es un bloque técnico aparte: solo la diferencia (ver la tabla de Tema 1 abajo).

## Lo que fija el PDF (guía de repaso y diapositivas de la Clase 10)

La guía dice: «**no hace falta estudiar "todo": esto es exactamente lo que entra en el simulacro**» y «no te aprendas la respuesta de memoria: entiende el porqué». Es el **ensayo del examen de verdad**.

**Tema 1 (Tema 01, 1.2-1.7) · tienes que saber:**
- Definir la **CID** con un ejemplo de cada una, **en especial la disponibilidad**.
- Decir **qué principio se rompe** en un caso (p. ej. se modifican datos sin permiso → **integridad**).
- Medidas según **cuándo actúan**: **preventiva** (antes: contraseñas, cortafuegos, formación, permisos), **detectora** (durante: logs, IDS, alertas, antivirus), **correctora** (después: restaurar copia, parche, aislar la máquina).
- **Cuándo un activo es crítico**: cuanto **más daño causaría perderlo o que fallara**.
- **Activa** (evita: antivirus, contraseñas, cortafuegos) frente a **pasiva** (reduce o repara el daño: copias, SAI); **física** (el sitio y el equipo: acceso, SAI, incendios) frente a **lógica** (software y datos: permisos, cifrado).

**Tema 2 (Tema 02, 2.2 y 2.3) · tienes que saber:**
- **Tres medidas físicas o ambientales** de un CPD (acceso, climatización, detección de incendios) y **reconocer cuál NO lo es** (**el cifrado es lógica**).
- Para qué el control de **temperatura y humedad**: que los equipos **no se sobrecalienten y fallen**.
- La pasiva física protege **el sitio y los equipos (el soporte físico)**.
- SAI (diapositiva 11): batería que mantiene los equipos encendidos; da tiempo a **apagar bien o a que arranque el grupo electrógeno**; «se elige por **potencia y autonomía**» (conceptual: el cálculo, según el audio, no entra).

**Tema 3 (Tema 03, 3.2-3.4) · tienes que saber:**
- Tipos de copia y **cuál restaura más rápido** (la **completa**; entre las otras dos, la **diferencial**). Truco: «**incremental mira a la copia de ayer; diferencial mira siempre a la última completa**».
- **RPO** (cuántos datos puedes perder; decide **cada cuánto** copiar) y **ventana de copia** (cuándo conviene), y cómo deciden tu política.
- **`tar`** empaqueta (con `-z`, comprime; **restaura con `-x`**) frente a **`rsync`** (espejo; **`--delete` deja la copia exacta**).
- **Leer una línea de `cron`** (5 campos) y ejemplo `0 2 * * *` = a las 2:00.
- **Comprobar una restauración con `sha256sum`** (huellas iguales = íntegra) y **ver si cron corrió con `grep CRON`** en el log.
- **Dibujar el esquema 3-2-1** de un servidor.

**Lo que «cae seguro» (diapositiva 22):** la **disponibilidad** (CID) y **las medidas**, **cuándo un activo es crítico**, **el RPO**, **incremental frente a diferencial** y **leer una línea de cron**. «En el examen de verdad te van a pedir **aplicar, no recitar**.»

> [!warning] Dos discrepancias entre el PDF y la clase
> 1. **«El original no cuenta» (diapositiva 14 de la Clase 10).** El PDF dice «3 copias de tus datos… **el original no cuenta: tres copias de verdad**». El profesor, en el audio del 18/11, vio esa frase, **no supo por qué** y dijo «original y 2 copias»; y la diapositiva 10 de la Clase 8 cuenta el **original** entre las 3. **Las fuentes se contradicen.** En un examen, escribe la regla **explicitando qué cuentas** («3 copias en total: el original y 2 copias, en 2 soportes, 1 fuera»), y si puedes, **pregúntalo en el foro** (la guía lo pide: «si algo no te sale, pregúntalo en el foro»).
> 2. **«`tar` empaqueta y comprime» (guía) frente a «`tar` NO comprime» (Clase 9).** Lo correcto: **`tar` solo empaqueta**; **`-z` (gzip) comprime**. En las diapositivas 14 de la Clase 10 lo dicen bien («con `-z` lo comprime»). Escribe «**empaqueta; con `-z` comprime**».
> - **Matiz (mío) en las medidas:** el **antivirus** sale como medida **activa** (diapositiva 6) y como **detectora** (diapositiva 8). **Activa/pasiva y preventiva/detectora/correctora** son dos clasificaciones distintas; en una pregunta, mira cuál te piden.


## Tema 1 · Principios de seguridad

### Tríada CID (clase + temario)
| | Qué garantiza | Ejemplos del profesor | Cómo se logra/mide |
|---|---|---|---|
| **Confidencialidad** | Solo lee quien debe | Nóminas impresas en una impresora común (fallo); RR. HH. con su propia impresora | Control de acceso, cifrado |
| **Integridad** | No se modifica en tránsito ni en reposo | Que nadie cambie el importe de una factura | **Hash** (comprueba que no cambió) |
| **Disponibilidad** | Accesible cuando se necesita | **Ransomware** ataca la disponibilidad: no puedes acceder a tus datos | Infraestructura, redundancia, copias |

- La **ISO 27001** (SGSI, sistema de gestión de seguridad de la información) parte de proteger la información con la tríada.
- **Dónde se pregunta (clase):** la CID se ve también en Ciberseguridad. El profesor dice que **en SAD preguntará la CID por su lado** (sobre todo confidencialidad y disponibilidad) y que en Ciber lo hace el otro; **las preguntas del examen no coinciden** (cada módulo tiene sus 10 temas). Cuando SAD y Ciber diverjan (2.º trimestre), ya no chocarán.
- **(mío, aviso)** El hash **comprueba** integridad; **no cifra**.

### Activo, amenaza, vulnerabilidad, riesgo, impacto
| Concepto | Qué es | Ejemplo (clase) |
|---|---|---|
| **Activo** | Lo que tiene valor en la empresa | Información de nóminas, el servidor, el ordenador del director (se trata distinto del equipo de recepción) |
| **Amenaza** | Lo que **puede** atacar o dañar el activo | Un **actor de amenaza** (atacante), **malware**, un **incendio**, el **error humano** («capa 8» del modelo OSI) |
| **Vulnerabilidad** | **Debilidad/fallo** que hace viable la amenaza | Contraseña débil, software sin parchear, **puerto abierto que no hace falta** |
| **Riesgo** | **Combinación de probabilidad e impacto** (PDF, diapositiva 7): cómo de probable es que la amenaza aproveche la vulnerabilidad y cuánto daño haría. Analizarlo = decidir qué proteger primero | Se reduce con medidas de protección |
| **Impacto** | Daño al activo cuando ocurre; baja su valor. Un **CVE** (PDF) = vulnerabilidad conocida con nombre | — |

Cadena: **activo → amenazas → vulnerabilidad → impacto → riesgo**; las **medidas de protección** (p. ej. una puerta con cerradura en la sala del servidor) **reducen el riesgo**; nunca lo dejan en cero («todos somos vulnerables a algo»).

- **Pregunta de una alumna, respuesta suya:** «virus = amenaza, puerto abierto = vulnerabilidad»: **correcto**. Regla práctica: **si no vas a usar un servicio (p. ej. PHP, FTP), no lo instales y cierra el puerto**; «cuantas menos puertas abiertas, mejor».
- **CVE (clase):** identificador público de una vulnerabilidad, formato **`CVE-año-número`** (el número es incremental). Un investigador la comunica, la empresa la reconoce y se publica con crédito al investigador.
- **Actores de amenaza (ENISA Threat Landscape, clase):** actores **alineados con Estados**, cibercriminales, **sector privado** y **hacktivistas**; ejemplos de grupos citados: **APT28 y APT29** (Rusia). El profesor lo muestra de pasada: **no es lo central**.
- **Análisis de riesgos (clase, fuera del temario):** menciona **MAGERIT** (metodología de la administración pública española, ligada al **Esquema Nacional de Seguridad**) y la herramienta **PILAR** (nombre **sin confirmar** por el audio): se listan los activos, la herramienta propone las amenazas y vas añadiendo medidas que bajan el riesgo. **Dijo que no lo ha preguntado nunca**; es cultura general.

### Medidas de protección (clase)
| Tipo | Ejemplos citados | ¿Visto ya? |
|---|---|---|
| **Prevención** | Política de **contraseñas** (largas), **firewall / security group** (abrir solo lo necesario), **ACL** (permisos por rol), **cultura de ciberseguridad** (formar al empleado) | En laboratorios (security group) |
| **Detección** | Leer logs (`/var/log/apache2/access.log`, `error.log`); un **SIEM** (cita **Wazuh**, nombre por el audio) ; **IDS** (**Suricata**, **Snort**); antivirus | **No** implantado todavía (2.º/3.er trimestre) |
| **Corrección** | **Restaurar copias**, aplicar parches, **aislar la máquina** (desconectarla de la red) | Solo **restaurar copias** |

Anécdota útil: ante un ciberataque, lo primero es **aislar** (en broma, «tirar del cable»).

### Activa vs. pasiva (clase)
- **Activa** = evita el ataque (contraseñas, firewall, antivirus, cifrado): **está siempre presente**.
- **Pasiva** = reduce el daño cuando ya ha pasado: **copias 3-2-1**, **CPD**, **SAI**. Lo visto este trimestre: **física/ambiental** y **copias**.
- **Lógica** (listas de control de acceso, cifrado TLS, simétrica/asimétrica, PKI): **todavía no** se ha trabajado.

## Tema 2 · Seguridad física y ambiental (CPD, SAI, clima, incendios)

> [!important] Lo que salió
> **CPD** = la infraestructura donde van los servidores. Si hay un problema físico, el objetivo es que **los datos permanezcan**.

| Pieza | Qué dijo (clase) |
|---|---|
| **Acceso y ubicación** | Acceso **controlado** (tarjeta, registro); **fuera de zonas inundables** |
| **Suelo técnico** | Elevado unos **50 cm**, con el cableado por debajo |
| **Edificio** | Seguro, industrializado |
| **Clima** | Control de **temperatura y humedad** |
| **SAI** (en inglés **UPS**) | **Batería** que mantiene los equipos si falla la alimentación; da tiempo a que **arranque el grupo electrógeno** sin perder datos. **Dimensionarlo no entra** («eso ya lo calculáis por vuestra cuenta») |
| **Incendios y desastres** | **Detección de incendios**, plan ante catástrofes naturales; el DRP se activa con la alarma (temario) |

- **(mío, aviso)** El profesor dijo «sistema de alimentación **interrumpida**» por un lapsus: es **ininterrumpida** (temario).
- Las **diapositivas del Tema 2** que él revisa se suben el **19/11** (según el audio).
- **RTO/RPO, nueves de disponibilidad y Tiers:** ver [Tema 2 (28/10)](2026-10-28_tema2-disponibilidad-rto-rpo-tiers.md). En esta clase dijo que lo del RPO/RTO «lo he puesto en la diapositiva», pero **no estaba seguro** de si entra en el Tema 2 o en el 3: por la lista de Dani, **entra** (Tema 3).

## Tema 3 · Copias de seguridad

### Tipos (clase; el criterio de restauración es lo que se pregunta)
| Tipo | Qué guarda | Tamaño | Para restaurar necesitas |
|---|---|---|---|
| **Completa** | Todo | Grande | Solo ella (restaura rápido) |
| **Incremental** | Lo que **cambió desde la última copia** (cualquiera) | Pequeña | **Completa + todas las incrementales** hasta el día |
| **Diferencial** | Lo que cambió **desde la última completa** | Crece cada día | **Completa + la última diferencial** |

Ejemplo (clase): completa el domingo; incrementales lunes, martes y miércoles; fallo el jueves → **completa + las 3 incrementales**. Con diferenciales, **completa + diferencial del miércoles** (la de miércoles ya incluye lunes y martes).
Truco suyo: *«la diferencial se carga sobre la completa; la incremental sobre las anteriores»*.
- **Abuelo-padre-hijo** (rotación, **GFS**): copias mensuales/semanales/diarias; ver la [nota del 11/11](2026-11-11_tema3-cron-ventana-rotacion-gfs-hanoi-politica.md).

### Regla 3-2-1 (clase)
**3** copias (**el original y 2 copias**, según el audio) · **2** soportes/sitios distintos (disco del servidor y otro disco) · **1** fuera de sitio (p. ej. **la nube**). **Las fuentes se contradicen:** la Clase 10 (diapositiva 14) dice «el original **no** cuenta»; el profesor, en clase, «original y 2 copias»; la Clase 8 (diapositiva 10) cuenta el original (ver [4/11](2026-11-04_tema3-copias-3-2-1-tar-rsync-snapshot.md)). Ver el aviso de arriba.

### `tar`, `gzip`, `rsync` (clase)
- **`tar` empaqueta** muchos ficheros en **uno solo**; **`gzip` (`.gz`) comprime**. «`tar` es el empaquetado, `gz` la compresión». Típico: **`.tar.gz`**.
- **`rsync` sincroniza**: copia solo lo que cambió. Con **`--delete`**, el destino queda como **espejo exacto** del origen (también borra lo borrado).
- **(mío, aviso)** El profesor llama a `rsync` «incremental/diferencial» a ratos y compara; en rigor es **sincronización**, no un tipo de copia por sí mismo (ver [4/11](2026-11-04_tema3-copias-3-2-1-tar-rsync-snapshot.md)).

### `cron` (clase)
Tarea programada de Linux. Cinco campos: **minuto · hora · día del mes · mes · día de la semana**. Dice que el día de la semana va **de 0 a 6** y que se admiten **rangos**. Ejemplos típicos que pidió saber leer: «cada día a la 1:30», «cada 15 minutos»… Detalles y ventana de copia en la [nota del 11/11](2026-11-11_tema3-cron-ventana-rotacion-gfs-hanoi-politica.md).
- **(mío)** En Debian/Ubuntu el día de la semana acepta **0-7** (0 y 7 = domingo); el 0-6 del profesor es válido.

### Restaurar siempre (clase)
> «Por mucha copia que hagas, tienes que **restaurarla para probar que funciona**.»
Una copia no probada no es una copia. **Pruébala en un servidor** (instalación nueva): si arranca y funciona, la copia es correcta.

## Autotest (hazlo en papel, 60 min, sin mirar) · soluciones al final

**Nivel 1 · Test**
1. Un ransomware cifra tus ficheros. ¿Qué pata de la CID afecta principalmente? 
2. Un puerto FTP abierto que nadie usa es una… (a) amenaza (b) vulnerabilidad (c) riesgo (d) activo.
3. ¿Qué sirve para comprobar que una factura no se modificó en el envío?
4. ¿SAI y UPS son lo mismo? ¿Qué hace el SAI ante un corte?
5. ¿Qué copia necesita **solo** la completa para restaurar?
6. Con completa del domingo e incrementales L-M-X, fallo el jueves: ¿qué restauras?
7. Misma situación con diferenciales: ¿qué restauras?

**Nivel 2 · Cortas (3-4 líneas)**
8. Diferencia entre **amenaza, vulnerabilidad y riesgo** con un ejemplo de servidor web.
9. Explica la **regla 3-2-1** con un ejemplo real tuyo (servidor en AWS).
10. ¿Por qué `tar` y `gzip` no son lo mismo?
11. ¿Por qué hay que **restaurar** las copias aunque se hagan bien?
12. Di dos medidas de **seguridad pasiva física** de un CPD.

**Nivel 3 · Casos prácticos**
13. Interpreta (di cuándo se ejecuta cada una):
    a) `30 1 * * 1-5 /usr/local/bin/backup.sh`
    b) `0 3 * * 0 tar -czf /backup/web_$(date +\%F).tar.gz /var/www`
    c) `*/15 * * * * rsync -a /datos/ /backup/datos/`
14. Una pyme tiene todo en un NAS en la misma oficina. Diseña, con la regla 3-2-1, qué añades y dónde.
15. **Dibujo:** esquema de la regla 3-2-1 (original, 2 copias, 2 soportes, 1 fuera de sitio) con flechas.
16. Un cliente pierde datos un jueves a las 10:00 y su última completa fue el domingo 02:00 con diferenciales diarias a las 02:00. ¿Qué restauras y cuánto trabajo pierde (RPO real en ese momento)?
17. Di de cada medida si es **preventiva, detectora o correctora**: (a) formación del usuario, (b) registros de acceso (logs), (c) restaurar una copia, (d) permisos de acceso.
18. Indica cuál de estas **NO** es una medida física o ambiental de un CPD: acceso con tarjeta, climatización, detección de incendios, cifrado de disco.
19. Tras restaurar un fichero, ¿cómo compruebas que es **idéntico** al de la copia? ¿Y cómo ves si una tarea de `cron` se ejecutó?
20. Un fallo en una BD modifica importes sin permiso: ¿qué principio de la CID se rompe? ¿Y si la BD no responde?

### Soluciones
1. **Disponibilidad** (no puedes acceder a la información).
2. **(b) Vulnerabilidad** (la amenaza sería quien/lo que la explota).
3. Un **hash** (integridad), comparando el del origen y el del destino.
4. **Sí**: SAI (español) = UPS (inglés). Mantiene con **batería** los equipos y da tiempo a que arranque el **grupo electrógeno** o a apagar bien.
5. La **completa**.
6. **Completa del domingo + incrementales de L, M y X**, en orden.
7. **Completa + diferencial del miércoles** (la última).
8. Ej.: *amenaza* = atacante que escanea el servidor; *vulnerabilidad* = Apache sin parchear o FTP abierto innecesario; *riesgo* = probabilidad de que lo explote y dañe el activo; se reduce con parches/cerrar puertos.
9. 3 copias = original en el servidor + copia en otro disco + copia en **S3** (otra región/nube) → 2 soportes (disco y nube) y 1 fuera de sitio.
10. `tar` **empaqueta** varios ficheros en uno; `gzip` **comprime**. Se combinan en `.tar.gz`.
11. Porque una copia sin probar puede estar corrupta, incompleta o ser imposible de restaurar; solo se sabe que sirve al restaurarla.
12. Dos de: acceso controlado con tarjeta, suelo técnico, ubicación no inundable, SAI, climatización, detección de incendios (temario/clase).
13. a) **01:30, de lunes a viernes**. b) **Domingos a las 03:00** (`0` = domingo), crea un `.tar.gz` con la fecha (`\%` por el escape de cron). c) **Cada 15 minutos**, sincroniza el directorio.
14. Ejemplo: copia local en un **segundo disco/NAS distinto** + **copia en la nube** (fuera de sitio). **(mío)** Completa semanal + incrementales/diferenciales diarias con `cron`, y **prueba de restauración** periódica.
15. Esqueleto (texto): `[Servidor: ORIGINAL] → [Disco B: copia 1] → [Nube: copia 2, fuera de sitio]`; etiqueta: **3 copias · 2 soportes · 1 fuera**.
16. **Completa del domingo + diferencial del jueves 02:00** (la última hecha antes de la caída). Se pierde lo trabajado entre las 02:00 y las 10:00: **8 h** de datos nuevos (el RPO real de ese momento). **(mío)** el cálculo.
17. (a) **Preventiva**; (b) **detectora**; (c) **correctora**; (d) **preventiva** (según la guía: «permisos»).
18. **El cifrado de disco** (es seguridad **lógica**).
19. Con **`sha256sum`** de ambos ficheros: **huellas iguales = íntegra**. Para `cron`: **`grep CRON /var/log/syslog | tail`** (y ver los ficheros con la fecha de hoy).
20. Se rompe la **integridad**; si no responde, la **disponibilidad**.

## Dudas y cosas sin confirmar
- **Fecha de publicación del simulacro:** el audio apunta al **19/11**; mi nota anterior decía **20/11**; los PDF solo dicen «en Archivos y en el foro». Revisa el aula.
- **Laboratorio de restauración:** el profesor dice **«este viernes vamos a hacer una restauración en un servidor»** y antes comenta (audio confuso) que **un laboratorio se mueve** y «no vale para la Actividad 2». Las diapositivas del 11/11 aclaran que el montaje de la política y **la restauración** se hacen **«en el laboratorio de diciembre, al arrancar la Actividad 2»** (aunque otra diapositiva citaba el lunes 16/11), ver [11/11](2026-11-11_tema3-cron-ventana-rotacion-gfs-hanoi-politica.md). Lo del viernes sigue **sin confirmar**; **comprueba en el campus** qué laboratorio hay y la entrega de la Actividad 2.
- **Puntos extra («plus»):** habla de **cibercooperantes/ciber voluntarios** (charla, hacer fotos…) y dice que da **«un plus de 1 punto en el examen»** por apuntarse. Audio confuso (**sin confirmar** si es 1 punto ni a qué examen aplica).
- ✅ **Esquema en el simulacro:** resuelto por el PDF: **sí entra dibujar la 3-2-1**.
- ✅ **Hora del simulacro del 25/11:** **19:00** (diapositiva 17), «nuestra franja de siempre». El de **Inglés** es ese mismo día a las 16:00: no se solapan.
- Omitido: charla sobre uso de la IA y su supervisión, anécdotas personales, memes, conversación sobre noticias y videojuegos y la demostración de un simulador de redes de un compañero.

## Logística y para llevar a casa
1. **Hoy o mañana:** bajar el simulacro del aula y las diapositivas del Tema 2 (19/11).
2. **Antes del 25/11:** hacer el autotest en papel, 60 min, y **cronometrado**; repasar leer `crontab` y la restauración con completa+incrementales/diferenciales.
3. Repasar **las notas del 28/10 (RTO/RPO, nueves, Tiers), 4/11 y 11/11** si fallas algo.
4. Confirmar en el aula: laboratorio del viernes, Actividad 2 y dónde está el simulacro (**miércoles 25/11, 19:00**). Si dudas de la 3-2-1, **pregunta en el foro**.
