---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-11-18
tema: "Repaso del trimestre (Temas 1, 2 y 3) y formato del simulacro del 25/11"
fuente: transcripción de la clase (1 h 7 min) + lista de contenidos del PDF de repaso del profesor (copiada por Dani). El PDF/presentación en sí no se ha recibido. Contrastado con los Temas 1-3 del temario y con las notas anteriores de SAD.
---
# SAD · Repaso Temas 1-3 y simulacro (18/11)

> Anterior: [Tema 3 (11/11): cron, ventana, rotación GFS/Hanoi, política](2026-11-11_tema3-cron-ventana-rotacion-gfs-hanoi-politica.md) · Profesor: Damián Sualdea Soy

Clase de repaso, sin contenido nuevo evaluable. El profesor recorre los tres temas, explica **cómo es el simulacro** y da consejos de estudio. Convención: **(clase)** = audio; **(PDF de Dani)** = la lista que pasó Dani; **(temario)** = Temas del repo; **(mío)** = añadido por mí.

> [!warning] Lo que NO tengo
> No he recibido la **presentación de repaso**; solo la lista de contenidos que copió Dani. Tampoco el **simulacro** (todavía no publicado a esta hora). Las diapositivas con capturas de `crontab` que dice que proyectó no se ven en el audio.

## Lo imprescindible

> [!important] Simulacro: lo que dijo
> - **Miércoles 25/11, en clase; lo corrige él allí mismo.** **No cuenta para la nota.**
> - Entra **solo lo de los Temas 1, 2 y 3** ("absolutamente todo lo que hemos visto en clase").
> - **Estructura:** **test de 15 preguntas** + **preguntas cortas** + **casos prácticos** (ejemplos que dio: **interpretar un `crontab`**, **la restauración** de una copia y **dibujar un esquema**). Sobre el esquema se contradice: primero lo lista y luego dice «aquí nos entra esquema, no» (audio confuso); al final aconseja saber **dibujar la regla 3-2-1**. **Sin confirmar** si cae; **prepáralo** por si acaso.
> - Lo **publica en el foro/tablón** y avisa para que lo bajes. En el audio dice que **«mañana tenéis que disponer de los simulacros»** y que revisa y sube las diapositivas del Tema 2 «mañana por la mañana», o sea el **19/11**. Mi nota anterior decía **viernes 20/11** para el simulacro de SAD; **no coinciden, mira el aula**.
> - **Cómo prepararlo (su consejo):** estudiar los apuntes, hacerlo **en papel, con cronómetro de 60 min**, sin mirar; fallar no penaliza.
> - **Estilo del examen:** de **comprensión, no de recitar**. «No quiero parrafadas». Preguntas cortas y **casos prácticos** tipo entrevista de trabajo («te pongo un caso y me lo resuelves»). El de mayo irá igual.

## Qué estudiar, según el profesor

Los apartados que cita (en el audio salen con números confusos; contrastados con el temario):

| Tema | Qué entra (lista del PDF de Dani) | Apartados (temario, **sin confirmar** el rango exacto) |
|---|---|---|
| **1** | Tríada **CID**; **activos, amenazas, vulnerabilidades y riesgo**; **medidas de protección** | 1.2-1.7 (dice «del 1 al 7») |
| **2** | Seguridad **pasiva física y ambiental**; **CPD**; **SAI**; **climatización e incendios**; **seguridad activa** | 2.2 y 2.3 («el resto del tema que lo miráis») |
| **3** | **Copias**: tipos, regla **3-2-1**; **frecuencia**; **RPO y RTO**; **rotación y automatización con cron**; **restauración** | 3.2, 3.3 y 3.4, más `tar`, `rsync`, `cron` y verificar/dibujar la 3-2-1 |

> [!warning] «Seguridad activa» en tu lista
> En el audio **no** repasa la seguridad activa como bloque: dice que **«todavía no la hemos trabajado»** (la lógica/activa llega en el 2.º y 3.er trimestre). Es probable que solo entre **la diferencia activa/pasiva** (ver más abajo). Si la lista del PDF la incluye, no te la saltes, pero no esperes preguntas técnicas de firewalls o antivirus.

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
| **Riesgo** | **Probabilidad** de que la amenaza explote la vulnerabilidad | Se reduce con medidas de protección |
| **Impacto** | Daño al activo cuando ocurre; baja su valor | — |

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
**3** copias (**el original y 2 copias**) · **2** soportes/sitios distintos (disco del servidor y otro disco) · **1** fuera de sitio (p. ej. **la nube**). El profesor vio una diapositiva que decía que «el original no cuenta» y **no supo por qué**; su criterio, igual que en el 4/11: **original + 2 copias**. **Sin verificar** contra la diapositiva.

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

## Dudas y cosas sin confirmar
- **Fecha de publicación del simulacro:** el audio apunta al **19/11**; mi nota anterior decía **20/11**. Revisa el aula.
- **Laboratorio de restauración:** el profesor dice **«este viernes vamos a hacer una restauración en un servidor»** (¿**20/11**?), pero antes comenta (audio confuso) que **un laboratorio se mueve al siguiente trimestre y «no vale para la Actividad 2»**. **No coincide** con lo apuntado el 11/11 (Actividad 2 = laboratorio en SAD1, entrega 18/01). **Comprueba en el campus** qué laboratorio hay el viernes y qué pasa con la Actividad 2.
- **Puntos extra («plus»):** habla de **cibercooperantes/ciber voluntarios** (charla, hacer fotos…) y dice que da **«un plus de 1 punto en el examen»** por apuntarse. Audio confuso (**sin confirmar** si es 1 punto ni a qué examen aplica).
- **Esquema en el simulacro:** contradictorio, ver arriba.
- **Hora del simulacro del 25/11:** no se dice; consulta el aula (el **Inglés** también tiene simulacro ese mismo miércoles, a las 16:00).
- Omitido: charla sobre uso de la IA y su supervisión, anécdotas personales, memes, conversación sobre noticias y videojuegos y la demostración de un simulador de redes de un compañero.

## Logística y para llevar a casa
1. **Hoy o mañana:** bajar el simulacro del aula y las diapositivas del Tema 2 (19/11).
2. **Antes del 25/11:** hacer el autotest en papel, 60 min, y **cronometrado**; repasar leer `crontab` y la restauración con completa+incrementales/diferenciales.
3. Repasar **las notas del 28/10 (RTO/RPO, nueves, Tiers), 4/11 y 11/11** si fallas algo.
4. Confirmar en el aula: laboratorio del viernes, Actividad 2 y hora del simulacro.
