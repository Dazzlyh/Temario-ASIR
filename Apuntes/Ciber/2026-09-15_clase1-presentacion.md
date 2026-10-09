---
asignatura: Ciberseguridad
fecha: 2026-09-15
tema: Clase 1 · presentación del módulo, organización y evaluación
fuente: transcripción de la clase en directo
---
# Ciber · Clase 1 (15/09) · Presentación del módulo

> Siguiente: [Clase 2](2026-09-22_clase2-pilares.md)

Clase introductoria, sin contenido técnico de examen. Organización del curso.

## El profesor
**Damián Sualdea Soy**. Da también **SAD** y **SER** (las tres asignaturas están pensadas para no solaparse en temario). Ingeniero de sistemas, máster en ciberseguridad (2013). Enfoque muy práctico: "la parte teórica, lo justo y necesario", porque en una entrevista de trabajo lo que cuenta es defenderse a nivel técnico.

## Cómo funciona la asignatura
- **Clases en directo los martes, de 19:00 a 20:00**, grabadas (si no puedes ir, no pierdes la sesión).
- **Tutorías colectivas quincenales**: para dudas y repaso, no para avanzar contenido nuevo. Según un compañero de 1º: el tutor resolvía dudas puntuales para todo el grupo, no daba temario nuevo.
- **Tutorías especiales**: las 2 últimas semanas de cada trimestre (revisión, citas).
- **Dudas**: las de clase van al foro **"Pregúntale al profesor"** (las ve todo el grupo, y así no se repite la respuesta); lo personal, por correo electrónico directo.
- 3 trimestres en el curso. Único festivo que afecta: **martes 8 de diciembre**.
- Terminología del módulo: se dice **"cifrar"**, no "encriptar" (el profesor es estricto con esto).

## Estructura del módulo: 10 temas en 3 trimestres
**Trimestre 1** — Tema 1: pautas de seguridad básicas. La tríada **CID** (confidencialidad, integridad, disponibilidad), seguridad física/ambiental, seguridad lógica (software), y cierra con **análisis forense** (1ª actividad, con una máquina Windows antiguo).

**Trimestre 2** — implementaciones: mecanismos de seguridad activa y corporativa (proxies, firewalls), seguridad perimetral, herramientas de bastionado, acceso remoto seguro por SSH, proxy inverso (Nginx).

**Trimestre 3** — bastionado de redes y de sistema (servidor web, FTP/SFTP, correo) + **normativa**: SGSI (ISO 27001), RGPD y, en España, la LOPDGDD.

Los 4 puntos del módulo, a grandes rasgos: **proteger la información**, **defender el sistema** (para defender hay que saber atacar), **asegurar el perímetro**, y **hacking ético en entorno controlado**.

## Entorno técnico
- Hace falta **Kali** (o cualquier Linux/Mac): ya trae John the Ripper y Wireshark listos. Para la parte wifi, **aircrack-ng** (la más complicada; el profesor aún no ha decidido cómo lo plantea).
- Todo el hacking se hace en **laboratorio aislado, sin salida a Internet**, con máquinas vulnerables ya preparadas por el profesor.
- **Regla clave repetida varias veces**: lo que separa una auditoría de un delito **no es la herramienta, es el permiso por escrito**. Sin contrato/autorización, no se toca nada (ejemplo real: en banca, conectar un USB sin permiso puede acabar en despido en el momento).
- Herramientas que se irán viendo: OpenSSL (cifrado simétrico/asimétrico), GPG/Kleopatra (certificados digitales), John the Ripper (contraseñas), crunch (diccionarios), rsync (copias de seguridad, "trabaja a muy bajo nivel"), dd (clonado de disco para forense), Autopsy (análisis forense), nmap, bases de datos de CVE, Metasploit, Snort/Suricata (IDS), pfSense (firewall/DMZ/VPN), Nginx (proxy inverso).
- Servidor de referencia para bastionado (compartido con SER): **Ubuntu Server 24 ("SRV")**.

## Evaluación
- **15 puntos de evaluación continua**: 3 actividades (3 + 3 + 4 = 10 puntos) + **10 test** (uno por unidad, 0,5 puntos cada uno = 5 puntos).
- Examen: **prueba obligatoria**, hay que sacar un 5. Si no se aprueba, convocatoria ordinaria en mayo y extraordinaria en junio. El examen tiene parte de conocimientos y parte de **desempeño práctico** (y alguna pregunta teórica concreta), siempre sobre lo trabajado en clase.
- El profesor distingue "modo aprendizaje" (la mayoría del curso) de **"modo examen"**: cuando algo es claramente examinable lo avisará explícitamente. Ejemplo que dio del año pasado: una instrucción completa de OpenSSL ya trabajada en clase, y había que explicar qué hace y por qué.
- En las semanas de repaso de cada trimestre (3er trimestre) se repasan posibles preguntas de los 3 trimestres.

## Actividades y fechas
- **Actividad 1** (análisis forense, contraseñas, cifrado, copias de seguridad — Temas 1 a 4): **entrega lunes 9 de noviembre, 20:59**. Se rellena por partes a lo largo del trimestre, a medida que se dan los temas; solo la parte de forense queda "más atrás".
- **Actividad 2** (tráfico wifi: nmap + Wireshark para detectar tráfico cifrado): se explica el **26 de enero**, a la vuelta.
- **Actividad 3** (laboratorio integrador: intrusión + informe, aplicando todo lo dado en clase): mencionada, sin fecha fijada todavía en esta clase.
- Indicación sobre las entregas: **no hace falta extenderse** — "con que esté bien ya está"; el profesor prefiere entregas cortas y correctas a informes de 20 páginas.

## Tema 1 (próxima clase, 22/09)
CID (confidencialidad, integridad, disponibilidad) con comandos: `sha256sum` y cifrado simétrico. Hace falta tener preparado Linux/Mac (Kali u otro).

## Notas sueltas
- El primer laboratorio es de análisis forense: adquisición de imagen de disco con `dd` ("copiar bit a bit"), hash (MD5/SHA) para la cadena de custodia.
