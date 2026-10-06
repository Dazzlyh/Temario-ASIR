# Tema 9. Hacking ético
*Ciberseguridad*

## Índice
Esquema · 9.1 Introducción y objetivos · 9.2 Herramientas de monitorización para la detección de vulnerabilidades · 9.3 Simulación de ataques y defensa en comunicaciones inalámbricas, redes y aplicaciones web · 9.4 Gestión de sistemas comprometidos y consolidación de defensas · A fondo · Entrenamientos

## Esquema
**Hacking ético**
- **Herramientas de monitorización y auditoría:** uso de Kali Linux para pruebas de penetración; escaneo de vulnerabilidades con Nessus y Nmap; análisis de tráfico de red con Wireshark.
- **Tipos de amenazas:** *humanas* (hackers, crackers, phreakers, insiders malintencionados); *lógicas* (malware —troyanos, gusanos, spyware—, ataques de fuerza bruta); *físicas* (fallos en hardware, sabotaje, accesos no autorizados).
- **Técnicas de ataque y defensa:** detectar ataques en redes desde el escaneo de puertos hasta ataques DDoS; explotación de aplicaciones web con inyecciones SQL; compromiso de los sistemas con implantación de *backdoors*.
- **Seguridad en redes y aplicaciones:** cortafuegos y sistemas IDS/IPS; segmentación de redes y cifrado de datos; protección de aplicaciones web con WAF y validaciones seguras.

---

## 9.1. Introducción y objetivos
El **hacking ético** (*penetration testing*) identifica, analiza y mitiga vulnerabilidades mediante **simulaciones controladas de ataque**, con autorización y con fines preventivos. Se trabaja en laboratorios controlados con herramientas reales (Nmap, Metasploit, Wireshark, Burp Suite…). Se abordan acceso no autorizado, ingeniería social, movimiento lateral, consolidación de sistemas comprometidos y defensas perimetrales.

Objetivos:
- Comprender el propósito, principios y **limitaciones legales** del hacking ético.
- Conocer y utilizar herramientas de detección y análisis de vulnerabilidades en redes cableadas e inalámbricas.
- Simular ataques en entornos controlados (escaneo de puertos, captura de tráfico, fuerza bruta, inyección de código, acceso persistente).
- Evaluar estrategias defensivas (firewalls, WAF, IDS/IPS, segmentación).
- Identificar vulnerabilidades comunes en aplicaciones web, redes Wi-Fi y dispositivos conectados.
- Aplicar ingeniería inversa, análisis forense y elaboración de reportes técnicos.
- Promover el uso responsable de los conocimientos y respetar el marco normativo y la ética profesional.

---

## 9.2. Herramientas de monitorización para la detección de vulnerabilidades
Conocer funcionalidades, ventajas, limitaciones y requerimientos de cada herramienta permite elegir las más adecuadas. Existen soluciones comerciales potentes pero costosas; este módulo se centra en herramientas **gratuitas incluidas en Kali Linux**, una distribución muy usada en ciberseguridad ofensiva.

### Clasificación general de amenazas
Cualquier agente o acción con potencial de afectar la confidencialidad, integridad o disponibilidad. Tres categorías:

**Amenazas humanas**
- **Hacker:** accede a sistemas por curiosidad o exploración, sin intenciones maliciosas.
- **Cracker:** con objetivos maliciosos (dañar o robar).
- **Phreaker:** explota redes de telefonía para obtener servicios gratuitos.
- **Ingeniería social:** manipulación de personas (suplantación de identidad).
- **Ingeniería social inversa:** el atacante simula ofrecer ayuda para inducir a revelar información.
- **Trashing:** recuperar credenciales o datos de papel o dispositivos desechados.
- **Intrusos remunerados:** profesionales contratados para infiltrarse.
- **Personal interno:** empleados que por negligencia o malicia comprometen la seguridad.
- **Exempleados:** con conocimiento de los sistemas, actúan por venganza.
- **Curiosos:** sin formación especializada, experimentan sin entender las consecuencias.

**Amenazas lógicas**
- **Adware:** publicidad no deseada. **Backdoors:** accesos ocultos insertados deliberadamente. **Bombas lógicas:** código que se activa ante condiciones específicas. **Troyanos:** apps que parecen legítimas pero incluyen funciones maliciosas. **Exploits:** técnicas que aprovechan vulnerabilidades específicas. **Gusanos:** se propagan automáticamente. **Malware:** término general (virus, troyanos, gusanos, spyware). **Pharming:** manipulación del DNS para redirigir a sitios falsos. **Phishing:** correos o mensajes falsificados. **Spam:** envío masivo de mensajes no solicitados. **Spyware:** recopila información sin consentimiento. **Virus:** se propagan alterando el funcionamiento o dañando datos.

**Amenazas físicas:** fallos en discos duros, procesadores o memoria; sobrecargas eléctricas; daños por temperatura, humedad o impactos.

### Taxonomía de herramientas en Kali Linux
Trece categorías que cubren el ciclo de auditoría:
1. **Recopilación de información** (DNS, servicios, rutas, VPN, VoIP…)
2. **Análisis de vulnerabilidades** (sistemas, servidores, bases de datos)
3. **Sniffing y spoofing**
4. **Ataques inalámbricos** (Wi-Fi, Bluetooth, RFID, NFC)
5. **Ataques a contraseñas** (fuerza bruta y diccionario, online y offline)
6. **Aplicaciones web** (escaneo, inyección SQL, XSS)
7. **Herramientas de explotación**
8. **Persistencia** (mantenimiento de acceso, túneles, shells inversos)
9. **Pruebas de estrés**
10. **Ingeniería inversa**
11. **Hacking de hardware** (Android, Arduino…)
12. **Generación de reportes**
13. **Herramientas forenses**

---

## 9.3. Simulación de ataques y defensa en comunicaciones inalámbricas, redes y aplicaciones web
La fase inicial de una evaluación es **obtener la mayor información posible** sobre el objetivo: número y tipo de dispositivos, accesibilidad desde el exterior y servicios activos. Un administrador diligente debe controlar de forma permanente la **superficie de exposición**.

### Uso del protocolo ICMP
`ping` envía un mensaje ICMP **echo request** y espera un **echo reply**. Sirve para: verificar conectividad; obtener la latencia; estimar indirectamente el número de saltos (**TTL**). Puede bloquearse con firewalls que descartan ICMP.

**TTL (Time To Live):** campo del paquete IP que evita que circule indefinidamente. Valor inicial normalmente 64, 128 o 255 según el SO; cada enrutador lo decrementa en una unidad; si llega a cero, el paquete se descarta. Si se envió con TTL=64 y se recibe con 58, ha pasado por seis enrutadores. Herramientas más avanzadas: **nping** (personaliza encabezados, contenido y frecuencia).

### Escaneo de puertos
Detecta qué puertos TCP/UDP están abiertos (en escucha) y por tanto qué servicios están expuestos. Con esa información un atacante puede determinar qué software se ejecuta, inferir la versión y planificar un ataque. Hay 65.535 puertos por protocolo; hay que conocer los más comunes.

Técnica básica: paquete TCP con el bit **SYN**; el destino responde **SYN+ACK** si el puerto está abierto y **RST** si no. En UDP, un paquete ICMP *port unreachable* indica puerto cerrado; si no se recibe, se considera abierto.

Herramienta: **nmap** («navaja suiza» mínima de cualquier administrador o consultor de seguridad):
```bash
$ nmap -sS -F -O -sV host-de-destino
```
Ejemplo de salida del material: puertos 21/tcp ftp (FileZilla ftpd), 80/tcp http (Microsoft IIS 7.0), 443/tcp ssl/http (Microsoft HTTPAPI httpd 2.0), 554/tcp rtsp (Microsoft Windows Media Server 9.5.6001.18281).

> **No realices escaneos de puertos a sistemas en los que no tengas autorización.** Pueden existir detectores de este tipo de escaneos.

### Interceptación de tráfico: sniffers
El **sniffing** captura datos que circulan por una red local, aunque no vayan dirigidos al atacante; si no están cifrados, pueden verse y analizarse (riesgo para la **confidencialidad**). Es viable en redes **ethernet** (broadcast): con la interfaz en **modo promiscuo** se reciben todos los paquetes del dominio de difusión. TCP/IP carece de autenticación nativa a nivel de red.

**Usos legítimos:** diagnóstico de red en tiempo real; perfilado del tráfico; análisis de protocolos.

### Ataques de denegación de servicio
Los atacantes priorizan también la **indisponibilidad** deliberada. **DoS** y su variante **DDoS** impiden el acceso de usuarios legítimos.

**Antecedentes:** febrero de 2000: Yahoo! fuera de línea tres horas (pérdidas estimadas en 500 000 $); Amazon, eBay, Etrade, Buy.com con pérdidas superiores a 600 000 $; también FBI y New York Times.

**SYN Flooding:** abusa del *handshake* TCP de tres pasos (SYN, SYN-ACK, ACK). El atacante no envía el ACK final y repite el proceso, generando conexiones semicompletas que desbordan la cola del servidor. Es difícil de mitigar porque todo ocurre **antes de la autenticación**, y autenticar antes agravaría el problema (consumo de CPU).

**Factores técnicos:** ausencia de control de recursos por cliente; déficit en la detección temprana; carencia de contención automática.

### Seguridad perimetral
Con la generalización de Internet, los dispositivos se exponen a amenazas externas. Servicios como HTTP, HTTPS o DNS necesitan ser accesibles. Un **cortafuegos** se sitúa entre la red local y la pública y filtra el tráfico entrante y saliente según políticas.

**Concepto:** sistema confiable entre dos redes, por el que circula todo el tráfico. Existen también **cortafuegos de host** (a nivel local).

**Funcionalidades:** filtrado de accesos (y bloqueo de suplantación de IP); ocultamiento de la red interna; monitoreo de eventos; servicios complementarios (NAT, gestión).

**Limitaciones:** no protegen contra ataques que no pasan por ellos (comunicación lateral); no evitan amenazas internas; no controlan accesos físicos o inalámbricos internos que eluden el perímetro; no protegen contra dispositivos comprometidos fuera de la red que se reconectan (portátiles).

**Tipos de cortafuegos:**
- **Filtrado de paquetes:** analizan cabeceras de red y transporte (IP, TCP, UDP); algunos con tablas de estado (*stateful*).
- **Pasarelas a nivel de aplicación (proxies):** intermediarios que analizan hasta el nivel de aplicación (HTTP, FTP, SMTP); filtrado granular, autenticación y registro.
- **Pasarelas a nivel de circuito:** conexiones proxy que redirigen tramas sin inspeccionar el contenido de aplicación; menos sobrecarga, menos control.

**Criterios de filtrado (NIST SP 800-41-1):** dirección IP y protocolo; protocolo de aplicación; identidad del usuario (p. ej., IPSec); actividad de red (peticiones por segundo, hora…).

### Cortafuegos de filtrado de paquetes
Operan en la capa de red y a veces en la de transporte, analizando cabeceras: IP origen/destino, puertos, protocolo (TCP, UDP, ICMP), interfaz, tamaño o tipo de servicio (ToS). Eficientes pero con capacidad limitada ante amenazas complejas de la capa de aplicación; son una primera línea de defensa.

Dos políticas por defecto:
- **Restrictiva (*deny by default*):** todo bloqueado salvo lo explícitamente permitido; más seguridad, configuración más exhaustiva.
- **Permisiva (*allow by default*):** todo permitido salvo lo prohibido; más sencilla pero menos segura.

### Cortafuegos con inspección de estado (*stateful*)
Rastrean y gestionan las **conexiones activas** en tiempo real: registran el estado (TCP, UDP, ICMP), asocian automáticamente paquetes a sesiones iniciadas y reconocen patrones de tráfico dinámicos. Eficaces con FTP, SIP o VoIP. Equilibrio entre eficiencia y robustez.

### Integración en arquitecturas de defensa en profundidad
Se combinan pasarelas de aplicación con cortafuegos de filtrado de paquetes: el firewall de paquetes bloquea tráfico no autorizado a nivel IP y la pasarela de aplicación inspecciona las peticiones válidas. Es el enfoque de **defensa en profundidad** (múltiples capas para detectar, contener y mitigar amenazas).

### Firewalls de próxima generación (NGFW)
Incorporan: **inspección profunda de paquetes (DPI)**; **control de aplicaciones** (independientemente del puerto); **IPS integrado**; análisis de amenazas en contexto (inteligencia externa, firmas, heurística); integración con sistemas de identidad; correlación de eventos de red. Son una plataforma consolidada de seguridad perimetral (firewall, IPS, control de aplicaciones, filtrado web).

### Defensa en profundidad y NGFW
Parte de la premisa de que algunos ataques evadirán las primeras barreras; se implementan controles redundantes y complementarios: firewalls de estado, pasarelas de aplicación, IDS/IPS, VPN, MFA, segmentación y microsegmentación. Una red bien diseñada puede no tener un NGFW como tal, pero debe integrar sus funcionalidades distribuidas en soluciones interoperables.

---

## 9.4. Gestión de sistemas comprometidos y consolidación de defensas
La consolidación de un sistema comprometido implica establecer **persistencia** y explotar recursos.

**Técnicas:**
- **Puertas traseras (*backdoors*):** permiten volver a acceder sin repetir el ataque; a menudo scripts o programas ocultos en procesos legítimos.
- **Movimientos laterales:** explorar otros dispositivos; **BloodHound** mapea rutas de privilegio en Active Directory.
- **Extracción de datos:** copiar información sensible; exfiltración por canales cifrados (túneles SSH, HTTPS).

**Medidas de mitigación:** auditorías regulares; monitoreo de logs en tiempo real (Splunk, ELK Stack); **EDR** (*endpoint detection and response*).

### Ataque y defensa en aplicaciones web
**Ataques frecuentes:**
- **SQL Injection:** inyecta código SQL malicioso; **SQLmap** automatiza el descubrimiento y la explotación. Impacto: acceso no autorizado a bases de datos, manipulación o robo.
- **Cross-Site Scripting (XSS):** scripts maliciosos ejecutados en el navegador de los usuarios. Impacto: robo de cookies, redirección a sitios fraudulentos, comandos arbitrarios.
- **Fuerza bruta a formularios de login:** **Burp Suite** puede automatizar los intentos.

**Defensas:**
- **Validación de entradas:** estricta; parámetros preparados en consultas SQL.
- **WAF** (*Web Application Firewall*): filtra y monitoriza el tráfico HTTP.
- **CAPTCHA y bloqueos automáticos** tras varios intentos fallidos.
- **Cifrado de datos sensibles** en reposo y en tránsito.

---

## A fondo
- **¿Cómo mapearías con NIST las defensas necesarias para ataques de hacking ético?** NIST. (s. f.). *Framework for Improving Critical Infrastructure Cybersecurity.* https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.04162018.pdf — funciones: identificar, proteger, detectar, responder, recuperar.
- **¿Cómo utilizar OWASP Top 10 para identificar riesgos críticos en ejercicios de hacking ético?** OWASP. (2021). *OWASP Top Ten Web Application Security Risks.* https://owasp.org/www-project-top-ten/

---

## Entrenamientos
> *Todos los ejercicios deben realizarse solo en entornos de laboratorio propios o con autorización expresa.*

### Entrenamiento 1: enumeración de servicios con Nmap
1. `sudo apt install nmap`
2. Elige un objetivo dentro de tu red de pruebas (p. ej., 192.168.1.10).
3. `sudo nmap -sS -sV -O 192.168.1.10`
4. Analiza puertos abiertos, servicios identificados y SO estimado.

**Solución:** mapa básico del sistema objetivo, con servicios expuestos y posibles vectores de ataque.

### Entrenamiento 2: captura de tráfico con Wireshark
1. Abre Wireshark y selecciona la interfaz activa.
2. Inicia la captura y filtra: `http`
3. Desde otro equipo, accede a un formulario HTTP sin cifrar (login vulnerable de laboratorio).
4. Detén la captura y examina cabeceras y cuerpo de los paquetes.
5. Identifica campos como `username` y `password`.

**Solución:** los datos viajan en texto plano sin cifrado, lo que refuerza la importancia de TLS.

### Entrenamiento 3: ataque de fuerza bruta con Hydra
1. `sudo apt install hydra`
2. Prepara `passwords.txt`.
3. `hydra -l usuario -P passwords.txt ssh://192.168.1.10`
4. Espera a que Hydra pruebe el diccionario.

**Solución:** si el usuario tiene una contraseña débil, Hydra la encontrará; evidencia la necesidad de MFA y limitación de intentos.

### Entrenamiento 4: escalamiento de privilegios con Mimikatz
**Planteamiento:** extraer credenciales en texto plano de un sistema Windows vulnerable, en un entorno de pruebas.
1. Accede a un sistema Windows con permisos de administrador (máquina de pruebas).
2. Descarga y ejecuta Mimikatz con privilegios elevados.
3. Comandos: `privilege::debug` y `sekurlsa::logonpasswords`
4. Analiza los resultados.

**Solución:** muestra cómo un atacante con acceso puede recuperar credenciales si no hay medidas como *LSA Protection*; refuerza el hardening y la gestión de credenciales.

### Entrenamiento 5: SQL Injection con SQLmap
1. `sudo apt install sqlmap`
2. Localiza un formulario vulnerable (p. ej., `http://192.168.1.20/vulnerable.php?id=1`).
3. `sqlmap -u "http://192.168.1.20/vulnerable.php?id=1" --batch --dbs`
4. Extrae información de la base de datos.

**Solución:** se pueden extraer bases de datos sin autenticación si no se valida la entrada; se refuerzan sanitización, consultas preparadas y WAF.
