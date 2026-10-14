---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-10-07
tema: Tema 1 · amenazas, ingeniería social, CVE/CVSS/NVD, MITRE ATT&CK · presentación de la Actividad 1
fuente: transcripción de la clase en directo
---
# SAD · Clase 4 (07/10) · Actividad 1: análisis forense con MITRE ATT&CK

> Anterior: [Laboratorio 2](2026-10-05_lab2-security-group.md) · Profesor: Damián Sualdea

**Entrega: lunes 19 de octubre.** Es la primera actividad de evaluación continua (vale el Tema 1 entero) y es **100% investigación, no hay que montar nada técnico**. Elegir el incidente en el foro cuanto antes (apartado del foro, no en "Dudas") para no repetir — repetir incidente con otro compañero no penaliza, pero se prefiere variedad.

> Idea clave del día: **no puedes defender lo que no conoces** — primero quién/qué nos ataca y por qué, luego cómo nos defendemos.

## 1 · Estructura exacta de la Actividad 1 (rúbrica)
1. **Contextualización**: qué pasó y qué consecuencias tuvo el incidente elegido.
2. **Tabla de activos** afectados.
3. **Cadena de ataque**: identificar las técnicas de MITRE ATT&CK empleadas, citadas **tal cual** (el nombre de la técnica, p. ej. "Phishing", no solo el código) junto con su código (p. ej. T1566). Si explota un CVE conocido, indicarlo. **Este apartado vale el 30% — es el que más puntúa.**
4. **Principios CID rotos**: cuáles de confidencialidad / integridad / disponibilidad se vieron afectados y por qué (solo estos 3, no hace falta más).
5. **Medidas de protección**: las que la propia página de la técnica en MITRE ATT&CK propone (mitigación) — no hay que inventarlas.
6. **Reflexión personal**: la parte que más valora el profesor para leer — contar el incidente desde el punto de vista de la organización, de un usuario afectado o del propio atacante, y una reflexión **propia** (usar IA para investigar y entender está bien, pero la reflexión final que sea vuestra, no copia/pega de la IA).

Formato: informe en PDF. Usar fuentes fiables: **INCIBE, CERT, el fabricante afectado, prensa técnica** — no titulares de prensa generalista.

## 2 · De dónde sacar el incidente
- **ENISA Threat Landscape** (agencia de ciberseguridad europea, enisa.europa.eu) — informe anual con miles de incidentes reales categorizados por sector (administración pública ~38%, transporte, finanzas, infraestructuras digitales) y por tipo de amenaza (ransomware, brecha de datos, fraude, DDoS, desinformación/deepfakes, ciberespionaje de estado). El profesor mostró en directo el informe del año: ~8.300 incidentes catalogados — "sois 30 personas, elegid el que más os guste".
- Casos sugeridos por el profesor como ejemplo o inspiración:
  - **WannaCry (2017)** — SMBv1 de Windows, explota **CVE-2017-0144** (EternalBlue), técnica MITRE T1210 (explotación remota de servicios) + T1486 (cifrado de datos para impacto/ransomware). Grupos relacionados: APT28, Lazarus.
  - **NotPetya** — también usó EternalBlue, combinado con otro exploit.
  - **SolarWinds** (ya visto el 30/09) — ataque a la cadena de suministro.
  - **Hospital Clínic de Barcelona** y **Hospital de Torrejón** (ransomware, enero 2020, en plena pandemia) — ⚠️ el profesor dice conocerlo "de primera mano" (tenía un familiar trabajando allí); detalle anecdótico, no verificado documentalmente.
  - **Stuxnet** — gusano dirigido a una central nuclear iraní, entró por USB; saltó la seguridad física precisamente en el sitio "imposible". Se comentó también la película/caso "Mission: Impossible"-like real (atribuido a Israel según un compañero en clase, sin confirmar).
  - **ILOVEYOU** (gusano en Visual Basic, vía macros de correo) y el **gusano Morris** (1988, ARPANET, el primer gusano de la historia, creado como prueba y descontrolado) — ejemplos "clásicos" si se quiere un caso más antiguo (cuanto más antiguo, más información hay publicada).
  - Pegasus (spyware moderno) también es válido.
  - El profesor aceptó también un tema no puramente informático propuesto por un alumno (hackeo "físico" desde una cárcel en los años 70, línea de teléfono pirateada) — confirma que **vale cualquier incidente de seguridad**, no solo ataques a servidores.

## 3 · Bases de datos de vulnerabilidades (para el apartado de CVE)
- **NVD** (National Vulnerability Database, EE. UU.) — buscar por `CVE-YYYY-NNNNN`.
- **CVE Details** — buscador alternativo, útil para encontrar el listado de CVEs de un año/producto, aunque no explica el ataque en sí (para eso, NVD o el propio informe del incidente).
- **CVSS**: puntuación de 0 a 10 de gravedad de una vulnerabilidad (ya visto antes); 8-10 = crítico (rojo).
- Diferencia **vulnerabilidad / exploit / CVE**: vulnerabilidad = el fallo en sí (servicio sin parchear, contraseña por defecto, permiso mal puesto); exploit = el código que aprovecha esa vulnerabilidad; CVE = el identificador público de una vulnerabilidad ya conocida (si no está identificada, es un 0-day). Dato de ENISA: 1 de cada 5 intrusiones en la UE explotó un fallo que **ya tenía parche disponible**.
- Herramienta de ejemplo para detectar vulnerabilidades conocidas en un sistema: **Nexpose**.

## 4 · Cómo navegar MITRE ATT&CK para la actividad
En **attack.mitre.org**, cada técnica (p. ej. T1110 Fuerza bruta) tiene en su misma página:
- Descripción de la técnica.
- **Mitigación** (cómo protegerse) — usar esto para el apartado 5 de la actividad, no inventar medidas.
- **Detección** — cómo se detectaría (qué tipo de software/alerta lo vería).
- Ejemplos de procedimiento / grupos conocidos que la usan (APTs).

Hay varias matrices además de la "Enterprise" por defecto: **Mobile** (ataques a móviles) e **ICS** (Industrial Control Systems — hospitales, centrales eléctricas, fábricas), útiles si el incidente elegido afecta a infraestructuras industriales.

## 5 · Amenazas: de quién nos defendemos
Tres tipos de amenaza humana, de más a menos peligrosa según el profesor:
1. **Empleado descontento (insider)** — el más peligroso: tiene acceso legítimo y conoce el sistema por dentro.
2. **Error humano sin mala intención** — muy frecuente, pero evitable con formación.
3. **Atacante externo**.

> Concepto de la **gacela más débil**: los atacantes no van a por el objetivo más grande, van a por el eslabón más fácil de romper — casi siempre el factor humano ("capa 8").

**Ingeniería social** — para el profesor, más determinante que las vulnerabilidades técnicas puras. Ejemplos clásicos de estafa en España: tocomocho, timo de la estampita, príncipe nigeriano, "te ha tocado la lotería", estafa del CEO (ahora potenciada con IA generativa: voz clonada e incluso videollamadas falsas), phishing bancario por SMS, soporte técnico falso, "paga una fianza para empezar a trabajar" (ojo con esta: nunca hay que pagar por conseguir un empleo). Factores por los que funciona: **prisa, miedo y autoridad**. Referencia de lectura recomendada: **Kevin Mitnick**, libros *El arte de la intrusión* / *El arte de la invisibilidad* (editorial Anaya).
Dato real compartido por un alumno: las empresas envían correos de phishing simulado a sus propios empleados como entrenamiento — quien pica recibe un curso de concienciación.
Recurso del profesor para dar formación de concienciación: el **kit de concienciación de INCIBE** (carteles, temario y material de charlas sobre ransomware, phishing, etc.).

## 6 · Ciclo de defensa (para el apartado de medidas, además de lo que diga MITRE)
**Prevenir → detectar → corregir**, de forma cíclica, no puntual:
- Prevenir: cultura de ciberseguridad, formación, cifrado, firewalls.
- Detectar: IDS (sistemas de detección de intrusiones — se trabajará con **Snort** o **Suricata** más adelante en el curso).
- Corregir: cada incidente debe producir un cambio real en cómo se protege la empresa, tanto a nivel preventivo como de detección.
- **Threat hunting**: buscar amenazas de forma proactiva, anticipándose a posibles vías de ataque antes de que se materialicen.
- **Defensa en profundidad**: redundancia (otra región de AWS, otro proveedor cloud) para que un único fallo no tumbe el servicio entero.

## 7 · Bastionado de SSH (demo breve, surgida de una pregunta)
Para impedir el login remoto directo como `root` por SSH (medida preventiva frente a fuerza bruta):
```bash
sudo nano /etc/ssh/sshd_config
# buscar/poner: PermitRootLogin no
sudo systemctl restart ssh
```
`root` como tal **no se puede bloquear** (no se banea ni se elimina), pero sí se le puede **prohibir el login remoto directo** por SSH con esa directiva — es distinto de bloquear al usuario. El control de qué usuarios pueden hacer `sudo` se gestiona aparte con `visudo`.

## 8 · Sobre el ritmo de las clases y el examen (para no agobiarse)
- Antes de cada examen trimestral hay una **semana de repaso** y un **simulacro**; el examen solo entra sobre lo que se repasa esas semanas, no sobre todo lo dicho al vuelo en cada clase en directo.
- Contenido que se repite entre asignaturas (p. ej. RAID visto ya en Sistemas Operativos) se trata con un repaso rápido, no se vuelve a explicar desde cero — si algo ya se ha visto, avisar al profesor para que lo agilice.
- El profesor sube la presentación del Tema 1 completa al final del tema (no solo el trozo del día), y en las semanas de repaso sube todo ya simplificado.
