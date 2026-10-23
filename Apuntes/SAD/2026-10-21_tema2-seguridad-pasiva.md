---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-10-21
tema: "Corrección de la Actividad 1 + Tema 2 · Seguridad pasiva, física y ambiental"
fuente: "Transcripción de la clase en directo"
---
# SAD · Corrección Actividad 1 e inicio del Tema 2: seguridad pasiva (21/10)

> Anterior: [Laboratorio: primera foto del servidor (19/10)](2026-10-19_laboratorio-primera-foto-servidor.md) · Profesor: Damián Sualdea Soy

Clase sin PDF de apoyo adjunto: estos apuntes están extraídos íntegramente de la transcripción en directo. Arrancó con un repaso de una vulnerabilidad crítica de PHP publicada esa misma madrugada (usada como "incidente en directo" de cierre del Tema 1), siguió con la corrección oral de la Actividad 1, y cerró con el inicio del Tema 2: seguridad pasiva, física y ambiental. Al final de la clase se corta la grabación para pasar a la clase de Servicios en Red (SER) del mismo día.

## 1 · Apertura: vulnerabilidad crítica de PHP como "incidente en directo"

El profesor abrió la clase mostrando en pantalla una vulnerabilidad de PHP que "saltó la liebre" el día anterior (20/10) y que se formalizó con asignación de CVE el **21 de octubre** (el mismo día de la clase) — la usó como ejemplo de cierre del Tema 1 ("vamos a acabar la actividad viendo un incidente en directo").

- **Herramienta/fuente usada en directo:** `cve.org` para consultar el detalle oficial del CVE, y **W3Techs** (`w3techs.com`) como página de referencia para ver qué tecnologías (lenguajes de servidor, CMS, servidores web, sistemas operativos) son más usadas en internet — el profesor comentó que la consulta habitualmente para hacerse una idea rápida de la superficie de exposición global de una tecnología.
- **Detalle de la vulnerabilidad** (parte del audio es difícil de transcribir con precisión en los números exactos — se recoge lo que dijo explícitamente el profesor, marcando con cautela lo menos claro):
  - Categoría: ejecución de código remota, **sin necesidad de autenticación**.
  - Puntuación crítica (el profesor citó un **9,2** sobre 10 para las versiones de PHP 8.x afectadas; mencionó también de pasada una puntuación de 10 para PHP 5, pero aclaró que no es relevante porque "nadie tiene ya un PHP 5" en producción).
  - Afecta a instalaciones de PHP en combinación con **Apache + mod_php, PHP-FPM, PHP-CGI y LiteSpeed**.
  - Riesgo calificado como alto para los módulos PHP con prueba de concepto (exploit demostrativo) ya circulando: "las peticiones no parcheadas pueden disparar el ataque antes de que ninguna aplicación lo ejecute".
  - Recomendación: actualizar inmediatamente a la última versión; **no hay parche para PHP 8.1 y versiones anteriores** ("problemón gordo, no podemos hacer nada" para quien se haya quedado en esas versiones).
  - Se asignaron **dos códigos CVE** distintos ese mismo día (los números exactos citados en el audio salen cortados/poco claros, no se puede dar aquí el identificador exacto con garantías).
  - Dato de contexto: según la propia web de la vulnerabilidad, un ~45% de la web con PHP 8 podría necesitar aplicar parche.
- **Comentario tangencial sobre IA y pentesting** (sin confirmar como dato objetivo, es opinión/anécdota del profesor): considera que la IA generativa ha hecho a los atacantes "mucho más creativos", citando que algunos de los últimos incidentes conocidos de fuga/escalada de privilegios en agentes de IA se deben a jailbreaks ("antes la IA no tenía protección, le podías pedir cualquier cosa; ahora hay que currarse los prompts, pero el jailbreak lo consigue todo").
- **Anécdota personal del profesor (sin confirmar, relato de un tercero no verificable):** comentó que a un amigo suyo "le entraron en un servidor" en septiembre, y que lo que al profesor le hubiera costado resolver en 3-4 horas, lo resolvió en 15 minutos revisando/depurando código en busca de vulnerabilidades.

## 2 · Corrección de la Actividad 1 (feedback general)

El profesor insistió varias veces en que **no corrige el contenido elegido, sino el proceso seguido**:

> "Lo que yo voy a evaluar es cómo lo habéis hecho [...] no voy a mirar si has elegido un buen incidente o un mal incidente. Yo quiero ver el proceso completo."

Puntos clave de la corrección, por apartado:

### 2.1 · Uso de IA y redacción
- No penaliza usar IA para escribir, pero sí que se note que el texto está "lanzado" sin supervisión: "se ve a la legua" cuando un texto es puramente generado y no apetece leerlo.
- Valora positivamente los textos con imperfecciones visibles que demuestran dedicación real (aunque sean solo 5-15 minutos de trabajo esforzado) frente a un texto IA pulido pero vacío.
- **No le gustan los emojis/iconos** en resúmenes — bajan la percepción de calidad ("veo iconos emojis [...] y digo, madre mía. Te doy la nota, pero para mí ha sido un rollo leerlo"). Mencionó como anécdota de otro curso que el año pasado alguien entregó un examen con emojis.
- Importante citar bien las fuentes de información utilizadas.

### 2.2 · Apartados 1 y 2 — Contexto, activos y cadena de ataque
- El contexto del incidente debe estar resumido y entenderse "de un vistazo"; valora positivamente usar una tabla.
- Los **activos expuestos** deben tener sentido respecto al contexto: no vale listar activos genéricos — puede ser información de clientes, la propia web, una tecnología concreta, etc., pero tiene que estar justificado.
- En la **cadena de ataque** quiere ver código de técnica MITRE ATT&CK + fase, o bien que se diga explícitamente que no se ha encontrado un CVE asociado — "no vale poner un código [inventado], que es lo que directamente voy a buscar y testear".
- Idea de fondo repetida: la actividad busca que todos "habléis el mismo idioma" de MITRE ATT&CK para describir un incidente.

### 2.3 · Principios rotos, medidas y puntos de vista
- **Principios rotos:** aplicar la tríada CIA (confidencialidad, integridad, disponibilidad) de forma concreta — no vale poner algo genérico como "rompe la seguridad".
- **Medidas:** deben poder leerse claramente como preventiva, detectora o correctora. Ejemplo que dio el profesor para un ransomware: formar a los usuarios para que no pinchen en URLs/correos sospechosos = **preventiva**; tener copia de seguridad = **correctora**.
- **Puntos de vista:** lo ideal es dar los tres (organización, usuario, atacante). El profesor reconoció que la pregunta de la actividad pudo entenderse mal y aceptará respuestas que solo dieran un punto de vista, sin penalizar retroactivamente por ello.

### 2.4 · Ejemplo-modelo que puso el profesor (phishing)
A modo de ejemplo de cómo debería quedar un apartado bien resuelto (parte del detalle numérico de técnica/fase de MITRE se transcribió de forma poco clara en el audio):

- Vector: phishing — acceso inicial mediante correo falso suplantando a Microsoft 365, robo de credenciales de usuario.
- Principio roto: **confidencialidad** (el atacante usa una credencial válida que no es la suya).
- Medidas: autenticación multifactor (reduce el acceso indebido), formación anti-phishing como medida **preventiva**.
- Puntos de vista: organización / usuario / atacante.

### 2.5 · Calendario de corrección
- El profesor empezará a corregir **el fin de semana** y dará el feedback **lo antes posible** durante la semana.
- Comentó que, al ser la primera actividad del trimestre y tener los alumnos cuatro asignaturas a la vez, no se va a poner estricto con los plazos de entrega en este primer caso.

## 3 · Por qué el Tema 2 se solapa con Ciberseguridad y cómo está repartido el curso

El profesor explicó por qué empieza ahora con seguridad pasiva/física/ambiental, aunque parte de ese contenido ya se vio en la asignatura de Ciberseguridad:

- La programación (impuesta por la coordinación/UNIR) obliga a entregar la Actividad 1 en la 4ª semana, con fecha de entrega ya pasada (19/10), lo que limita el contenido a lo visto hasta el Tema 1.
- La Actividad 2, por la misma lógica de calendario, cae sobre contenido de seguridad **lógica** (plan de seguridad SAI, copias de seguridad, control de acceso) — **se entrega el 18 de enero**.
- La Actividad 3, ya de contenido más técnico (antimalware, seguridad en redes corporativas, VPN, firewall, DMZ, proxy Squid, pfSense, ClamAV), se da al final del curso porque es la parte más técnica y avanzada.
- Reconoce explícitamente el solape con Ciberseguridad en estos dos temas concretos (seguridad pasiva y la parte física/ambiental): "creo que estos son los dos únicos temas que chocan [...] el resto de los temas tanto de Ciber como de Sad se separan bastante, no se parecen mucho". No va a evitar dar el contenido, pero intentará darle un enfoque distinto.

## 4 · Tema 2: concepto de seguridad pasiva

- **Definición:** medidas que **no evitan** que el ataque ocurra (eso es seguridad activa), sino que **reducen el impacto/daño** una vez que el ataque ya se ha producido.
- Se apoya en el concepto de **resiliencia**: no es rendirse, es asumir que algo va a fallar en algún momento y estar preparado con un plan de prevención ante desastres.
- Analogía usada: el airbag o el cinturón de seguridad — no evitan el accidente, pero mitigan sus consecuencias.
- **Pregunta clave para distinguir activa de pasiva:** "¿esto lo puedo parar?"
  - Si la respuesta es sí → **seguridad activa** (contraseñas, cifrado, firewalls, antivirus, 2FA, sistemas de detección de intrusiones).
  - Si la respuesta es no (el problema ya ha ocurrido) → **seguridad pasiva** (SAI ante corte eléctrico, copias de seguridad, RAID, sistemas de extinción de incendios, seguros/transferencia del riesgo a terceros).
- Activa y pasiva **no compiten, se complementan**: siempre hace falta un plan de seguridad activa funcionando día a día, además del plan de seguridad pasiva.
- Punto de seguridad pasiva poco evidente que señaló el profesor: **los seguros** y la **delegación/transferencia del riesgo** a un tercero (contratar una empresa externa que asuma parte del riesgo).

> "La seguridad activa evita el golpe y la pasiva es la que te deja seguir cuando el golpe ha llegado hasta el final."

## 5 · Seguridad física y ambiental

- **Seguridad física:** conjunto de barreras reales/arquitectónicas que se ponen a los sistemas informáticos para que no les pase nada.
- Riesgos físicos repasados:
  - **Incendio / inundación:** pueden destruir el equipo entero; ejemplo usado: el incendio del CPD de OVH en Estrasburgo (ver sección 7).
  - **Energía eléctrica** (picos y caídas de tensión): solución, sistemas **SAI** (sistemas de alimentación ininterrumpida, UPS). Apagar un servidor de golpe por corte de luz es uno de los problemas más graves que puede evitar un SAI.
  - **Temperatura y humedad:** uno de los puntos más importantes; depende mucho de la ubicación geográfica del servidor (ejemplos citados: zonas costeras como Huelva o Canarias — humedad; Chile — riesgo sísmico). La idea no es evitar poner servidores en esas zonas, sino adaptar las medidas al entorno (salas climatizadas, rangos de temperatura recomendados, punto intermedio entre exceso de frío/calor).
  - **Acceso físico:** quién puede entrar en la sala/CPD y para qué. El profesor recomienda tener siempre una lista de control de acceso clara, sin excepciones (ver anécdota en sección 8).

## 6 · Clasificación rápida de ejemplos: activa vs. pasiva

Ejemplos dados en clase para fijar el criterio:

| Ejemplo | ¿Se puede "parar" antes? | Clasificación |
|---|---|---|
| SAI que aguanta un corte de luz | No, actúa cuando ya ha pasado | Pasiva |
| Doble factor de autenticación (2FA) | Sí, impide el acceso antes de que ocurra | Activa |
| Copia de seguridad en otra región de AWS | No, se usa para recuperarse después | Pasiva |
| Cortafuegos del servidor | Sí, bloquea tráfico antes de que entre | Activa |
| Sistema de detección de incendios que se activa tras un incendio | No, actúa una vez producido el incendio | Pasiva |

Otros conceptos de seguridad pasiva mencionados:
- **Snapshots (AWS)** / **puntos de restauración (Windows)**: "guárdame como está ahora" para poder volver atrás — el profesor comentó que en Windows la idea es buena pero la implementación histórica ha sido poco fiable.
- **RAID**: si muere un disco, el sistema debe aguantar sin parar el servicio (solo cambiar el disco roto).
- **Discos diferenciados**: separar el disco de arranque/sistema del disco de datos es la práctica habitual, para poder seguir trabajando sustituyendo solo la pieza averiada.
- **Continuidad del servicio**: el objetivo final es que el usuario note lo menos posible el problema — enlaza directamente con **alta disponibilidad** (balanceadores de carga, IP elástica, autoescalado), que se trabajará como tema siguiente del curso.
- **Borrado accidental de ficheros**: ejemplo de OneDrive, que guarda versiones anteriores durante unos 30 días desde que se guarda un archivo, como red de seguridad ante borrados por error.
- **Anécdota personal del profesor** (sin confirmar, relato propio sobre sus inicios con la informática hacia 1999-2000): compró un ordenador de segunda mano cuyo disco tenía los primeros sectores dañados (según le comentaron en la tienda, procedía de una embajada); la solución fue reinstalar el sistema operativo evitando los sectores defectuosos del disco.

## 7 · Análisis de riesgos

- **Riesgo** = probabilidad de que una amenaza se haga efectiva sobre un activo.
- **Impacto** (o "magnitud del daño") = cuánto se ve afectado/reducido el valor del activo si la amenaza se hace efectiva.
- **Matriz de riesgo** (probabilidad × magnitud del daño): el profesor mostró una matriz tipo semáforo con zonas verdes (riesgo bajo/aceptable) y rojas (riesgo alto, inaceptable). Las medidas de seguridad (activas o pasivas) actúan como "paraguas" para mover una amenaza de la zona roja a la verde.
- **Herramienta mencionada:** **PILAR**, herramienta de análisis de riesgos (vinculada al CCN — Centro Criptológico Nacional según lo que mostró el profesor en pantalla); permite introducir los activos a proteger, listar amenazas posibles (incendio, inundación, etc.) y aplicar medidas para reducir el riesgo de cada una.
- **Normativa/estándares citados** (algunos nombres se transcriben con reservas por la calidad del audio): **ISO 27001** (Sistema de Gestión de Seguridad de la Información, SGSI) como referencia de certificación oficial en este ámbito; mencionó también certificaciones de auditor/analista de riesgos (citó siglas poco claras en el audio, tipo "CISA"/"GRC", sin poder confirmar con precisión cuál dijo exactamente).
- **El mundo "corbatero"** (término coloquial del profesor): perfil profesional dedicado en exclusiva a la gestión de riesgos corporativa — procedente a menudo de consultoras grandes (citó Deloitte y, con dudas, Accenture/EY) y **sin formación técnica en informática**; su trabajo consiste en aplicar metodologías y planes de gestión de riesgo estandarizados, muy orientado a informes y resúmenes corporativos. El profesor lo contó para que el alumnado entienda que, en una empresa real, este tipo de perfiles no técnicos son los que acaban dictando qué medida de seguridad física o lógica se implementa.

### Ejemplo didáctico: el casco y la maceta (coste/beneficio del riesgo)
El profesor construyó en directo, con preguntas al alumnado, un ejemplo para entender cuándo merece la pena invertir en una medida de mitigación:

- Pregunta: ¿qué probabilidad hay de que te caiga una maceta en la cabeza paseando por la calle? → casi nula.
- Si vas por una gran ciudad rodeado de edificios con macetas en balcones → la probabilidad sube, pero sigue siendo baja.
- ¿Llevarías casco por la calle para protegerte de eso? → No, porque el coste (económico, social, de comodidad) no compensa un riesgo tan bajo.
- Pero en una **obra**, el casco es obligatorio (normativa PRL) porque ahí el riesgo de impacto en la cabeza es mucho mayor y el coste de llevarlo está justificado.
- Conclusión: el presupuesto de seguridad tiene que ser proporcional al riesgo real (probabilidad × impacto) del entorno concreto, buscando un punto intermedio — ni gastar de más donde el riesgo es bajo, ni dejar sin proteger donde el riesgo es alto.

Intervención de un alumno (Francisco) aplicando la misma lógica a un caso real: en un CPD situado en una zona costera (ej. Huelva) el riesgo de problemas por humedad es mayor, por lo que hay que aplicar medidas específicas para esa amenaza concreta, graduando el nivel de protección según la criticidad de los datos almacenados (p. ej. datos de clientes).

## 8 · Anécdota de acceso físico (sin confirmar — relato personal del profesor sobre un tercero)

El profesor contó, sin poder verificarse de forma independiente dentro de la propia transcripción, la historia de un antiguo alumno suyo que llegó a ser jefe de seguridad física de una empresa farmacéutica:

- Implantó un sistema estricto de control de acceso al CPD/instalaciones: solo podía entrar quien estuviera en una lista cerrada, sin excepciones.
- Durante una semana de pruebas, hizo comprobaciones enviando distintas personas a intentar entrar, y el sistema funcionó: solo pasaba quien estaba en la lista.
- El último día de pruebas, dejó pasar él mismo a una persona que **no estaba en la lista**, alegando una "última revisión" — y despidió a la persona que gestionaba el acceso ese turno por haberle dejado entrar, pese a no estar él mismo en la lista, como lección de que el protocolo debe cumplirse siempre, sin excepciones (incluso para el propio jefe).
- Comentó también que, después de invertir mucho dinero en seguridad física, a veces un directivo llamaba para pedir que le dejaran pasar con invitados sin estar en la lista, lo cual —según el profesor— hacía que "toda la seguridad implantada se fuera al garete" en la práctica.

## 9 · Caso real: incendio del CPD de OVH en Estrasburgo (2021)

Ejemplo que el profesor repite en varias clases como caso de estudio de seguridad física/pasiva:

- En **2021**, un incendio destruyó por completo el centro de datos **SBG2** de OVH en Estrasburgo — descrito como el incidente de este tipo más grande ocurrido en Europa.
- Cayeron de golpe del orden de **3,6 millones de sitios web**.
- No hubo ninguna medida de seguridad **activa** que pudiera evitar o contener el incendio.
- Se perdió información de clientes de forma irrecuperable en los casos sin copia de seguridad fuera del edificio; quienes sí tenían copia en otro servidor/región pudieron recuperarse, aunque tardando entre horas y días.
- Lección que remarcó el profesor: ni siquiera los grandes proveedores cloud (OVH, AWS, Azure) están exentos de este riesgo. Pueden indemnizar económicamente por el acuerdo de servicio, pero eso no siempre implica que la información se recupere. De ahí la importancia de aplicar la regla **3-2-1** de copias de seguridad, con al menos una copia fuera del propio edificio/región.

## 10 · Avisos de logística

- **Corrección Actividad 1:** el profesor empezará a corregir el fin de semana (24-25/10) y dará el feedback lo antes posible durante la semana siguiente.
- **Actividad 2** (seguridad lógica: plan de seguridad SAI, copias de seguridad, control de acceso, etc.): fecha de entrega **18 de enero**. El profesor recomienda ir echándole un vistazo con antelación, aunque no hace falta profundizar todavía.
- **Actividad 3** (contenido más técnico: antimalware, seguridad en redes corporativas, VPN, firewall, DMZ, proxy con Squid, pfSense, ClamAV): se entrega al final del curso, en el tercer trimestre.
- **Cursos AWS Academy** que el profesor quiere que el alumnado haga (dos cursos, uno orientado a operaciones/prevención ante desastres y otro de tipo "técnico de centro de datos" — los nombres exactos de los cursos se citaron de forma poco clara en el audio): tienen una duración de acceso de **3 meses** desde que se abren; el profesor planea abrirlos y dar de alta al alumnado en torno al **15 de diciembre**, antes de las vacaciones de Navidad.
- **Próxima sesión de SAD:** seguir con Tema 2 y empezar a hacer pruebas reales en el laboratorio AWS, simulando caídas/fallos del servidor (emulaciones de incidentes físicos/de disponibilidad) — pide tener el laboratorio levantado para la siguiente clase.
- Al final de la clase se corta la grabación para pasar directamente a la clase de **Servicios en Red (SER)** del mismo día (donde continúan con DNS y apuntado de dominio).
- Acción práctica puntual en directo: antes de empezar la corrección, el profesor hizo un **reset/reinicio de su instancia de laboratorio AWS** para evitar problemas de página colgada, sin más detalle técnico.

## 11 · Para llevar a casa

- Repasar bien los criterios de corrección de la Actividad 1 (sección 2) de cara a futuras actividades: proceso > contenido elegido, razonamiento visible, evitar emojis/iconos, justificar siempre con MITRE ATT&CK o explicar por qué no hay CVE.
- Entender la diferencia operativa entre seguridad activa y pasiva con la pregunta "¿esto lo puedo parar antes de que pase?".
- Repasar los riesgos físicos/ambientales (incendio, inundación, energía, temperatura/humedad, acceso físico) y cómo se adaptan según la ubicación geográfica del CPD.
- Familiarizarse con el concepto de matriz de riesgo (probabilidad × impacto) y la idea de "paraguas" de medidas para reducirlo — opcionalmente, buscar información sobre la herramienta **PILAR**.
- Tener el laboratorio AWS levantado para la próxima clase: va a haber pruebas reales de caída/fallo del servidor.
- Apuntar en el calendario: Actividad 2 → 18 de enero; altas en AWS Academy previstas hacia el 15 de diciembre.
