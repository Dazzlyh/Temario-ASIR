---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-09-30
tema: Tema 1 · de quién y qué nos defendemos · MITRE ATT&CK, log de ataques reales, CID, MTTF/MTTR
fuente: transcripción de la clase en directo
---
# SAD · Defensa del servidor y MITRE ATT&CK (30/09)

> Anterior: [Clase 2](2026-09-23_clase2-principios-seguridad.md) · Siguiente: [Clase 3](2026-10-01_clase3-cid.md) · Profesor: Damián Sualdea

**Logística**: los laboratorios son solo práctica, no puntúan ni son obligatorios; lo único que puntúa es la **Actividad** (la primera, sobre MITRE, ver clase del 07/10). ⚠️ **Examen**: confirmado de nuevo — pondrá una instrucción de `openssl` y hay que explicar qué hace.

> Idea del día: **un servidor nunca está en reposo**. En el momento en que algo está en Internet, ya está siendo atacado — no es nada personal, son bots que barren rangos enteros de IP.

## 1 · Ver los ataques reales en el propio servidor (sad1)
```bash
tail -f /var/log/auth.log                 # intentos de login en vivo
grep "Invalid user" /var/log/auth.log     # usuarios probados por fuerza bruta
tail -f /var/log/apache2/error.log        # peticiones/errores del servidor web
```
Para saber de dónde vienen las IPs que atacan: web **ipinfo.io** (país, organización). En la demo salieron intentos desde Microsoft, Google y Taiwán entre otros — reconocimiento/fuerza bruta automatizados.

**fail2ban**: herramienta en Python que banea una IP durante (por defecto) 1 hora tras varios fallos de contraseña en distintos servicios. Se instalará más adelante en el servidor.

## 2 · MITRE ATT&CK
- Lo que se vio: **T1110 Fuerza bruta** (credential access).
- Terminología actualizada: **Man in the Middle → Adversary in the Middle** (lenguaje más inclusivo; si aparece "MITM" en documentación antigua es lo mismo).
- **Defacement**: cambiar el contenido visual de una web (afecta a la **integridad**). Archivo público de ataques: **zone-h.org** — se vio en directo un defacement real sobre un sitio `.aragon.es` (ya retirado al comprobarlo en clase).

## 3 · Casos reales (alguno sin verificar del todo, ojo)
| Caso | Qué pasó | Qué se rompió |
|---|---|---|
| Adif/Renfe | ~500 GB robados (nombres, correos, teléfonos, trayectos); los trenes **siguieron circulando** | Confidencialidad (solo capa web, no los sistemas de control) |
| Hospital de Cataluña | Robo + amenaza de publicar datos — ⚠️ no verificado del todo en la transcripción | Confidencialidad / disponibilidad |
| SolarWinds | Malware metido en una actualización de un software de conexión remota; se distribuyó a miles de empresas | Integridad (se detecta comparando el **hash** del paquete oficial) |
| AWS (Virginia, us-east-1) | Caída que afectó a Snapchat, Fortnite, bancos, Alexa — según el profesor, 20/10 | Disponibilidad |
| Microsoft/Azure (365, Xbox) | Caída 9 días después de la de AWS, ~29/10 — ⚠️ fechas y causa tal como las dio el profesor, sin verificar | Disponibilidad |
| Academia del profesor (anécdota personal) | Un Windows Server con Active Directory expuesto a Internet fue usado para un ataque de **reflexión UDP** (DDoS); llegó un aviso de abuso | Disponibilidad — ⚠️ no verificado, anécdota personal del profesor |

Infraestructuras críticas (Adif/Renfe, hospitales): les aplica el **ENS** (Esquema Nacional de Seguridad); hay que notificar el incidente en un plazo corto tras detectarlo y lo gestiona el CCN/CNI, no el equipo técnico de la empresa.

## 4 · Permisos de grupo en Linux (más allá de `chmod 600` ya visto)
```bash
touch saludo.txt
chmod 640 saludo.txt      # dueño rw, grupo r, otros nada
```
Si otro usuario necesita leerlo sin ser el dueño, la vía correcta es meterlo en el **mismo grupo** del propietario (no bajar más los permisos ni cambiar de dueño a lo loco).

## 5 · Integridad de descargas y malware (ampliación sobre el hash)
- Comprobar siempre el hash (SHA-256 u otro) de lo que te bajas, sobre todo ejecutables (ej. PuTTY) — el método de firmas es, en el fondo, cómo trabajan los antivirus.
- **VirusTotal**: sube el fichero y lo compara contra muchos motores/firmas.
- Problema real en empresas: un software legítimo (p. ej. una versión antigua de PuTTY) puede marcarse como malware si no está en la lista blanca interna de la empresa.
- "Troyanizado": descargas de páginas como SoftTonic que venían con malware camuflado encima del programa real.

## 6 · Disponibilidad: MTTF, MTTR y "los nueves"
- **MTTF** = tiempo medio hasta el fallo (cuánto aguanta el sistema).
- **MTTR** = tiempo medio de recuperación (cuánto se tarda en levantarlo).
- Objetivo: **resiliencia**.

| Disponibilidad | Caída al año (aprox.) | Ejemplo |
|---|---|---|
| 99% | ~3,65 días | servicio normal/interno |
| 99,9% | ~8,76 h | mayoría de servicios normales |
| 99,99% | ~52,56 min | comercio, banca, TPV |
| 99,999% | ~5,26 min | emergencias, control aéreo, hospitales |

El **SLA** (Service Level Agreement) es el contrato con el proveedor (AWS, OVH...) que promete uno de estos niveles; si no se cumple, se paga en dinero.

Dónde comprobar el estado de un proveedor: panel de estado propio de AWS, **downdetector.es**, y `uptime` en el propio servidor (ya visto) para la disponibilidad local.

## 7 · Equilibrio CID
Más confidencialidad (doble factor, contraseñas largas) casi siempre implica **menos disponibilidad** (más fricción para entrar), y al revés. La seguridad es siempre un equilibrio, no maximizar un único principio.

Ejemplos de qué principio se rompe:
- Roban 500 GB de datos → **confidencialidad**.
- Ransomware → los **tres** a la vez.
- Cae una región de AWS unas horas → **disponibilidad**.
- Te cambian una nota sin permiso → **integridad**.
- Pierdes un portátil sin cifrar → **confidencialidad**.

## Próximos temas (preview)
Autenticación y no repudio, firma digital con **Cleopatra** (Windows) y **Autofirma** (certificado FNMT), criptografía asimétrica. Lo veremos "con la menos teoría posible, lo justo y a trabajar".

> Consejo del profesor: usar la IA para aprender comandos está bien ("pregúntale, que te lo explique, y luego apúntalo tú"), pero no para que te resuelva todo sin entenderlo — llevar un cuaderno propio de comandos, como hacía él antes de que existiera la IA.
