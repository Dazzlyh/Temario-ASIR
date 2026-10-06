# Tema 1. Adopción de pautas de seguridad informática
*Ciberseguridad*

## Índice
Esquema · 1.1 Introducción y objetivos · 1.2 Confidencialidad, integridad y disponibilidad · 1.3 Elementos vulnerables en el sistema informático: hardware, software y datos · 1.4 Análisis de las principales vulnerabilidades de un sistema informático · 1.5 Amenazas: tipos · 1.6 Referencias bibliográficas · A fondo · Entrenamientos

## Esquema
**Adopción de pautas de seguridad informática**

- **Seguridad**
  - Principios básicos: confidencialidad, integridad, disponibilidad, fiabilidad.
  - Controles de seguridad: **básicos** (accesos, monitoreo); **mejoras** (análisis de riesgos); **organizativos** (procesos y concienciación).
  - Gestión de incidentes: **prevención** (controles de acceso, medidas de seguridad adicionales y concienciación de los empleados) y **respuesta** (monitoreo de la actividad delictiva y mitigación de esta).
- **Vulnerabilidades y amenazas** (diferentes tipos de amenazas y vulnerabilidades)
  - Amenazas **físicas**: desastres naturales, robos, fallos eléctricos…
  - Amenazas **lógicas**: malware, phishing, DDoS…
  - ¿Qué elementos son vulnerables? **Hardware y datos** (servidores y dispositivos, así como la información crítica que contienen) y **software** (aplicaciones y sistemas operativos desactualizados).

---

## 1.1. Introducción y objetivos
En un contexto donde las amenazas evolucionan rápidamente, la asignatura aborda la protección integral de activos digitales mediante tres pilares: **confidencialidad, integridad y disponibilidad**. Combina metodologías técnicas (criptografía, análisis forense) con estrategias organizativas (gestión de riesgos), preparando a los profesionales para responder a incidentes como ransomware, phishing o ataques DDoS, con casos reales como WannaCry.

El objetivo principal es formar expertos capaces de diseñar e implementar arquitecturas de seguridad resilientes, priorizando controles críticos y mitigando riesgos físicos y lógicos. Objetivos específicos:
- **Dominar fundamentos de seguridad:** manejar los conceptos de CIA y conocer los controles CIS básicos y organizativos.
- **Gestionar amenazas:** mitigar riesgos físicos con planes de continuidad y sistemas UPS; conocer los tipos de amenazas lógicas.
- **Analizar y responder a incidentes:** conocer el proceso forense y crear líneas temporales para reconstruir ataques.
- **Optimizar estrategias organizativas:** priorizar las necesidades de ciberseguridad y automatizar defensas.

---

## 1.2. Confidencialidad, integridad y disponibilidad
La seguridad de la información se fundamenta en cuatro pilares básicos:

- **Un entorno fiable:** capacidad del sistema para operar sin fallos durante un periodo determinado. Un sistema fiable garantiza disponibilidad y correcta ejecución de procesos críticos, minimizando riesgos operativos y errores. La redundancia y los planes de recuperación ante fallos contribuyen a la fiabilidad.
- **Confidencialidad:** protege la información contra accesos no autorizados, tanto datos almacenados como transmitidos y en uso (en tránsito y en reposo). Técnicas: cifrado, autenticación y controles de acceso. Ej.: AES (Advanced Encryption Standard).
- **Integridad:** protección de los datos contra modificaciones no autorizadas o accidentales; garantiza que la información sea exacta y completa. Firmas digitales y mecanismos de hash, como SHA-256, verifican que los datos no se hayan alterado.
- **Disponibilidad:** sistemas e información accesibles cuando se necesiten; incluye resistir ataques DDoS o fallos de infraestructura. Los sistemas de alimentación ininterrumpida (UPS) y las copias de seguridad son clave.

### Principios fundamentales de una buena solución de ciberseguridad
- **Conocer bien el panorama de ciberamenazas:** usar el conocimiento de ataques reales (propios o de organizaciones similares) para aprender continuamente de eventos e incidentes y construir defensas efectivas.
- **Priorización del riesgo:** invertir primero en los controles que más reduzcan el riesgo y protejan contra los actores más peligrosos y que sean viables.
- **Métricas y KRI (Key Risk Indicators):** parámetros comunes como lenguaje compartido entre ejecutivos, IT, seguridad y auditores para medir la efectividad de las medidas.
- **Diagnóstico y mitigación continua:** mediciones continuas para validar la efectividad de las medidas y decidir según prioridad de negocio.
- **Automatización:** automatizar las defensas para lograr mediciones confiables, escalables y continuas de la adhesión a los controles y métricas, reduciendo trabajo manual.

Los controles (**CIS**) se agrupan en tres categorías (Figura 1, CIS, s. f.):
- **Básicos:** cuestiones clave que deben implantarse en cualquier organización, sea cual sea su tamaño.
- **Mejoras (Foundational):** aplicación de buenas prácticas de seguridad; implementación gradual.
- **Organizativos:** centrados en las dimensiones de procesos y personas.

La figura de los controles CIS v7 muestra: **Básicos** 1 Inventario y control de activos de hardware · 2 Inventario y control de activos de software · 3 Gestión continua de vulnerabilidades · 4 Uso controlado de privilegios administrativos · 5 Configuración segura de hardware y software en móviles, portátiles, estaciones y servidores · 6 Mantenimiento, monitorización y análisis de logs de auditoría. **Foundational** 7 Protecciones de correo y navegador · 8 Defensas contra malware · 9 Limitación y control de puertos, protocolos y servicios de red · 10 Capacidades de recuperación de datos · 11 Configuración segura de dispositivos de red (firewalls, routers, switches) · 12 Defensa perimetral · 13 Protección de datos · 14 Acceso controlado según necesidad de conocer · 15 Control de acceso inalámbrico · 16 Monitorización y control de cuentas. **Organizativos** 17 Programa de concienciación y formación · 18 Seguridad del software de aplicación · 19 Respuesta y gestión de incidentes · 20 Pruebas de penetración y ejercicios de Red Team.

---

## 1.3. Elementos vulnerables en el sistema informático: hardware, software y datos
- **Hardware:** servidores, estaciones de trabajo, dispositivos móviles y redes. Vulnerables a: fallos mecánicos o eléctricos; accesos no autorizados por protección física insuficiente; ataques específicos como la manipulación de dispositivos periféricos.
- **Software:** aplicaciones y sistemas operativos con errores de programación o configuraciones inadecuadas. Ej.: errores de implementación que facilitan inyección SQL; versiones desactualizadas o no parcheadas.
- **Datos:** el recurso más crítico; objeto de robo, corrupción y destrucción. Amenazas: exfiltración de información confidencial mediante phishing; pérdida de datos por errores humanos o desastres naturales.

**Bastionado del hardware y software de portátiles, estaciones de trabajo y servidores:** procesos y herramientas para el seguimiento, control, prevención y corrección de defectos y debilidades en las configuraciones de dispositivos, sobre la base de un proceso de control de configuración. Es importante porque las configuraciones predeterminadas de fabricantes y revendedores suelen orientarse a la facilidad de despliegue y uso, no a la seguridad: servicios y puertos abiertos, cuentas o contraseñas predeterminadas, protocolos antiguos vulnerables, software innecesario preinstalado… todo puede ser explotable.

---

## 1.4. Análisis de las principales vulnerabilidades de un sistema informático
El análisis de vulnerabilidades identifica debilidades explotables. Según su origen:
- **Fallos de implementación:** errores en el desarrollo. Ej.: desbordamientos de búfer (ejecución de código arbitrario) y errores de validación de entradas (cross-site scripting, XSS).
- **Fallos de configuración:** sistemas no configurados para resistir ataques. Ej.: contraseñas predeterminadas en dispositivos IoT; servicios innecesarios habilitados que amplían la superficie de ataque.
- **Fallos de diseño:** errores de planificación. Ejemplo clásico: el protocolo TELNET, diseñado sin considerar entornos hostiles.

Herramientas automatizadas como **Nessus** y **OpenVAS** identifican y categorizan estas vulnerabilidades, facilitando la priorización. El análisis también puede hacerse **postincidente**, con un análisis forense completo para detectar, documentar y hacer seguimiento, generando documentación útil, entre otros usos, para aprender y evitar ataques futuros.

### Etapas de un análisis forense
Además de los estándares, hay metodologías posteriores (Departamento de Justicia de EE. UU., Instituto SANS, Kevin Mandia y Chris Prosise…). Mínimos comunes: **1. Recolectar → 2. Preservar → 3. Analizar → 4. Presentar.**

#### Recolección
Obtener las evidencias de interés para su análisis posterior. Dos partes: identificación y recolección.

**Identificación de las evidencias.** Concepto clave: la **volatilidad** (periodo de tiempo en que los datos estarán accesibles en el equipo). Hay que identificar qué datos son más o menos volátiles y priorizar su recolección. Escala por orden de volatilidad (RFC 3227), de más a menos volátil:
1. Registros y contenidos de la memoria caché del equipo.
2. Tablas de enrutamiento, caché ARP, tabla de procesos, estadísticas de kernel y memoria.
3. Información temporal del sistema.
4. Datos contenidos en disco.
5. Logs del sistema.
6. Configuración física y topología de la red donde se encuentra el equipo.
7. Documentos.

El analista identifica las evidencias útiles y documenta, en la mayor medida posible, el aspecto de los equipos (como describir la escena de un crimen), acompañándolo de fotografías: estado (encendido/apagado), nombre, marca y modelo, direcciones IP, dominio corporativo (si aplica), sistema operativo, tamaño de RAM, número de discos, tipo de discos (marca, modelo, número de serie, capacidad), contraseñas y claves de desbloqueo si se han facilitado.

**Recolección de las evidencias.** Dos mecanismos de adquisición:

| Adquisición en remoto | Adquisición en físico |
|---|---|
| Mayormente en escenarios corporativos sin acceso directo a los equipos. Copias completas o adquisición parcial de artefactos; requiere que la máquina esté encendida. | Cuando se tiene el dispositivo. **Copias en caliente:** con la máquina encendida se extrae el contenido vivo; en la práctica es la única vía factible para extraer la RAM (existen otros métodos, como el chip-off). Toda acción sobre la máquina encendida altera su estado, por lo que debe describirse y justificarse. **Copias en frío:** máquina apagada; copia del almacenamiento (clonado o copia bit a bit, imagen forense, montaje y adquisición parcial de evidencias…). |

Buenas prácticas:
- Se suele solicitar **autorización por escrito** para recolectar evidencias (datos confidenciales, posible afectación a la disponibilidad). Salvo indicios suficientes y fundamentados, no se recopilan datos de lugares a los que no se accede normalmente (p. ej., ficheros con datos personales).
- Las adquisiciones en físico se hacen sobre un **disco destino limpio** (nuevo o con borrado seguro). Tras la copia se verifica su integridad calculando su **hash** (para evitar colisiones se recomienda adjuntar **dos hashes**). Con el hash del original y de la copia se puede certificar ante un juez que son idénticas.
- Si es probable presentar el informe en juicio, suele estar presente un **notario o secretario judicial** durante el copiado; el notario suele custodiar la evidencia original y una primera copia, y el analista conserva una segunda.
- La copia que va al laboratorio es la **copia de respaldo máster** y nunca se trabaja directamente sobre ella; para el análisis se hace una tercera copia y se comprueba su integridad.

Herramientas (tanto remotas como físicas) con bloqueo de escritura sobre la fuente, verificación de hash, copias en paralelo y estado del proceso:

| Herramientas de hardware | Herramientas de software |
|---|---|
| FRED Forensic Workstations – Digital Intelligence · Clonadoras/duplicadoras: Logicube, Tableau, Voom · Bloqueadores de escritura: Logicube, Tableau | FTK Imager · EnCase Imager · Comando DD · Arsenal Image Mounter |

#### Análisis
Termina, en cierto modo, cuando se determina **qué o quién** causó el incidente, **cómo** lo hizo, qué afectación tuvo en el sistema y el impacto. Es el núcleo duro de la investigación. Premisas: nunca trabajar con datos originales; respetar las leyes de la jurisdicción; los resultados deben ser **verificables y reproducibles**. No existe un proceso estándar: hay que estudiar cada caso (no es lo mismo Windows que Linux, ni una intrusión en el correo que un DoS).

**Preparar un entorno de trabajo:** máquina con recursos suficientes (pueden ser virtuales); *toolkit* con las herramientas con las que el analista se sienta cómodo; mecanismos para conectar las evidencias en modo solo lectura (bloqueo físico o lógico); laboratorio aislado para análisis de malware o acceso a sandboxes y servicios de inteligencia.

**Crear una línea temporal.** Dos tipos: la que crea el analista (hallazgos de interés, para el informe) y la que se crea a partir de las evidencias (histórico de actividad). **Timeline** = ordenación cronológica de eventos de una misma fuente; **supertimeline** = agrupación cronológica de eventos de distintas fuentes. Se basan en los tiempos **MACB**: Modificación, Acceso, Cambio y Creación (Birth). Ejemplo de línea de tiempo de WannaCry (ESET): ago. 2016 Shadow Brokers subastan herramientas; 14 mar. 2017 Microsoft publica el parche MS17-010; 14 abr. 2017 EternalBlue es desvelado por Shadow Brokers; 25 abr. 2017 ESET añade detección de red de EternalBlue; 12 may. 2017 brote global de WannaCryptor. Hay que tener en cuenta las **zonas horarias**; buena práctica: ubicar todas las fechas en **UTC**. Herramienta de ejemplo: Timeline Explorer.

**Tratar de identificar responsables.** Estudiar perfiles de atacantes: persona o grupo de personas, empleado disconforme o extorsionado, o actor externo. Un **actor externo (*threat actor*)** es un grupo organizado que genera intencionadamente un efecto adverso en una organización. (Ver MITRE ATT&CK: groups en A fondo.) En un peritaje con fines judiciales hay que intentar resolver quién es el autor o al menos aportar pistas fiables; con fines correctivos, interesa estudiar el impacto y las mejoras.

**Medir el impacto causado.** No hay método único; puede ayudar el **BIA (Business Impact Analysis)**. El coste puede ser reponer una máquina u horas de reinstalación (fácil de calcular), o robo de secreto industrial/daño reputacional (incalculable y muy elevado). También cuenta el tiempo de inactividad (p. ej., parada de una planta de fabricación automatizada).

---

## 1.5. Amenazas: tipos

### Amenazas físicas
Comprometen activos tangibles: instalaciones, equipos y personal.

**Desastres naturales**
- *Inundaciones:* un CPD en zona inundable puede sufrir daños irreparables. Ej.: inundaciones de Tailandia 2011 interrumpieron la producción global de discos duros.
- *Terremotos:* zonas sísmicas (Japón, California). Ej.: Christchurch 2011 afectó centros de datos locales.
- *Incendios:* fallas eléctricas o calor extremo. Ej.: incendio del CPD de OVH en Estrasburgo (2021), destruyó miles de servidores.
- Medidas: ubicación estratégica en zonas de bajo riesgo; aspersores con agentes químicos que no dañen equipos; planes de continuidad con respaldo geográfico (centros de datos espejo).

**Robo o sabotaje**
- Robo de hardware: en 2020, un empleado descontento de Tesla intentó robar datos confidenciales.
- Sabotaje interno: empleados con acceso privilegiado manipulan o destruyen información; caso de un exempleado de una empresa financiera suiza que borró registros sensibles.
- Medidas: videovigilancia con almacenamiento en la nube; controles de acceso biométricos (huella, iris, facial); guardias de seguridad apoyados por detección electrónica.

**Fallas de energía**
- Ej.: corte masivo en Texas (2021) por clima extremo.
- Medidas: generadores eléctricos; **UPS** (baterías para cortes breves); energía renovable para diversificar fuentes.

### Amenazas lógicas
Ataques contra sistemas digitales y activos intangibles (datos, aplicaciones): ciberataques, errores humanos, vulnerabilidades.

**Malware** (virus, gusanos, troyanos, ransomware, spyware, adware). Ej.: **WannaCry (2017)** cifró archivos en más de 200 000 sistemas. Tipos: *ransomware* (LockBit), *spyware* (Pegasus), *troyanos* (Emotet, para robar credenciales). Medidas: antivirus actualizado, actualizaciones constantes, segmentación de redes (limita el movimiento lateral).

**Phishing** (ingeniería social). Caso Twitter 2020: phishing dirigido a empleados permitió tomar cuentas verificadas. Tipos: tradicional, *spear phishing* (individuos específicos), *whaling* (altos ejecutivos). Medidas: filtros de correo, concienciación.

**Fuerza bruta.** Ej.: ataque a Zoom (2020) con listas de credenciales comprometidas. Medidas: contraseñas robustas, autenticación multifactorial.

**Denegación de servicio (DoS/DDoS).** Ej.: ataque DDoS a Dyn (2016), con una botnet de dispositivos IoT infectados con **Mirai**, interrumpió Netflix y Twitter. Medidas: firewalls, CDN.

**Exfiltración de datos.** Robo de datos sensibles por vulnerabilidades o *sniffing*. Ej.: Capital One (2019), configuración incorrecta en la nube. Prevención: cifrado en reposo y en tránsito, sistemas de detección en tiempo real, seguridad de API.

---

## 1.6. Referencias bibliográficas
- CIS. (s. f.). *CIS Critical Security Controls Version 7 – What's Old, What's New.* https://www.cisecurity.org/insights/blog/cis-controls-version-7-whats-old-whats-new
- Ondata. (s. f.). *Hardware Análisis Informático Forense.* https://www.ondata.es/recuperar/equipos-forensics.htm
- Indiamart. (s. f.). *Forensic Duplicator.* https://www.indiamart.com/proddetail/forensic-duplicator-4492908330.html
- MalBot. (2017, abril). *Introducing Timeline Explorer v0.4.0.0.* https://malware.news/t/introducing-timeline-explorer-v0-4-0-0/10879
- Página de ESET.

---

## A fondo
- **Creación de una copia o imagen forense.** Duriva. (2019, noviembre 18). [Vídeo]. https://www.youtube.com/watch?v=Wn6e-ZEb2VA — cómo crear una copia forense en Windows.
- **MD5: The broken algorithm.** Ramírez, G. (2015, julio 28). Avira. https://www.avira.com/en/blog/md5-the-broken-algorithm — factores para elegir un algoritmo de hash y lista de los más usados.
- **MITRE ATT&CK: groups.** https://attack.mitre.org/groups/ — cómo se identifican y agrupan los actores de amenazas; limitaciones del enfoque basado en fuentes abiertas.

---

## Entrenamientos

### Entrenamiento 1: cifrado de disco completo con BitLocker
**Planteamiento:** el administrador debe implementar cifrado de disco completo en los portátiles de la empresa para proteger la información en caso de robo o pérdida.

**Desarrollo:**
1. Acceder a `gpedit.msc` en Windows para definir políticas de uso obligatorio de BitLocker.
2. Habilitar BitLocker en cada equipo: `manage-bde -on C:`
3. Configurar una clave de recuperación en Active Directory o en un USB.
4. Reiniciar y verificar el estado: `manage-bde -status`
5. Simular una extracción del disco y comprobar que no se puede acceder sin la clave.

**Solución:** BitLocker en los portátiles con almacenamiento seguro de claves en Active Directory; solo usuarios autorizados pueden descifrar los discos.

### Entrenamiento 2: mitigación de un ataque de inyección SQL
**Planteamiento:** una aplicación web es vulnerable a inyecciones SQL.

**Desarrollo:**
1. Analizar logs del servidor web y de la base de datos para identificar consultas maliciosas con patrones como `' OR '1'='1`.
2. Aplicar *Prepared Statements* en PHP: `$stmt = $conn->prepare("SELECT * FROM users WHERE username = ?")`
3. Habilitar un **WAF** (mod_security u otro).
4. Utilizar `escapeshellarg()` en PHP para sanitizar la entrada de usuario (*ver nota*).
5. Pruebas de penetración con **SQLMap** para verificar las contramedidas.

**Solución:** se eliminan las consultas dinámicas, se habilita un WAF y se protegen los campos con Prepared Statements.

> Nota: `escapeshellarg()` sirve para escapar argumentos de comandos de shell, no para evitar SQL injection; la defensa correcta son las consultas preparadas.

### Entrenamiento 3: análisis de memoria RAM con Volatility tras un ataque de malware
**Planteamiento:** actividad sospechosa en un servidor; analizar la RAM para identificar procesos maliciosos.

**Desarrollo:**
1. Volcado de memoria con winpmem (`winpmem.exe` o `memory.raw`).
2. Procesos: `volatility -f memory.raw --profile=Win10x64_19041 pslist`
3. Conexiones activas: `volatility -f memory.raw --profile=Win10x64_19041 netscan`
4. Módulos y archivos: `volatility -f memory.raw --profile=Win10x64_19041 dlllist`
5. Comparar hashes de procesos con VirusTotal.

**Solución:** se identifica un proceso desconocido ejecutando `mimikatz.exe`, se bloquea, se elimina el binario y se implementan reglas YARA.

### Entrenamiento 4: respuesta ante un ataque DDoS a un servidor web
**Planteamiento:** carga anómala y tiempos de respuesta elevados; se sospecha DDoS.

**Desarrollo:**
1. `tcpdump -i eth0 'port 80'`
2. `netstat -an | grep :80 | sort`
3. Bloquear IPs con alta tasa de peticiones: `iptables -A INPUT -s [IP] -j DROP`
4. *Rate limiting* con `mod_evasive` en Apache: `apt install libapache2-mod-evasive`
5. Verificar: `watch -n 1 "netstat -an | grep :80"`

**Solución:** se mitiga bloqueando IPs en el firewall y activando protecciones en el servidor web.

### Entrenamiento 5: recuperación de un servidor comprometido por ransomware
**Planteamiento:** servidor cifrado; recuperar datos sin pagar rescate.

**Desarrollo:**
1. Aislar el servidor de la red.
2. Identificar la variante: `strings encriptado.txt`
3. Consultar bases de descifrado como nomoreransom.org.
4. Restaurar desde copia offline: `rsync -a /mnt/backup /var/www`
5. Protección futura con *immutable bit*: `chattr +i /etc/important.conf`

**Solución:** archivos restaurados desde backup offline, ransomware eliminado con Malwarebytes y medidas de seguridad adicionales activadas.
