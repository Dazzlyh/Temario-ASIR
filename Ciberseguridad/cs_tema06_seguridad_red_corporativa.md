# Tema 6. Seguridad en la red corporativa
*Ciberseguridad*

## Índice
Esquema · 6.1 Introducción y objetivos · 6.2 Monitorización del tráfico en redes · 6.3 Seguridad en protocolos inalámbricos · 6.4 Identificación y mitigación de riesgos en servicios de red · 6.5 Gestión de intentos de penetración · A fondo · Entrenamientos

## Esquema
**Seguridad en la red corporativa.** *Objetivo:* garantizar la protección y disponibilidad de los sistemas corporativos mediante estrategias de monitoreo, protocolos seguros y medidas de mitigación ante amenazas.
- **Seguridad en protocolos de comunicación inalámbrica:** uso de protocolos seguros (WPA3, WPA2 con AES); configuración de redes ocultas y filtrado de direcciones MAC; auditorías periódicas de redes wifi corporativas.
- **Riesgos en servicios de red:** vulnerabilidades en software y configuraciones incorrectas; ataques DDoS y exfiltración de datos; implementación de firewalls y segmentación de red.
- **Intentos de penetración y defensa:** los intentos de penetración buscan explotar vulnerabilidades mediante técnicas como escaneo de puertos con Nmap, ataques de fuerza bruta, phishing e inyecciones de código en aplicaciones web. Para contrarrestarlos es clave implementar MFA y control de acceso riguroso. Además, el monitoreo continuo de logs permite identificar actividades sospechosas, mientras que la simulación de ataques mediante *honeypots* facilita la detección temprana y el estudio de tácticas de los atacantes.

---

## 6.1. Introducción y objetivos
La seguridad de la red corporativa es esencial en la estrategia integral de ciberseguridad. El tema se centra en monitorizar el tráfico, garantizar la seguridad inalámbrica, identificar y mitigar riesgos en servicios de red y prevenir intentos de penetración.

Objetivos:
- Aplicar técnicas avanzadas de **monitorización del tráfico**, facilitando la detección temprana de amenazas.
- Conocer los **protocolos de seguridad inalámbricos**, sus fortalezas y vulnerabilidades.
- Identificar los **riesgos de los servicios de red** y desarrollar estrategias preventivas y correctivas.
- Adquirir habilidades para **detectar, evaluar y responder a intentos de penetración**.
- Gestionar eficazmente los riesgos en redes corporativas.

---

## 6.2. Monitorización del tráfico en redes
Recopila, analiza y gestiona el flujo de datos en tiempo real: identifica amenazas de forma temprana, resuelve problemas y optimiza el rendimiento. Abarca el análisis de paquetes y el seguimiento de aplicaciones y dispositivos; los informes facilitan prever cuellos de botella, detectar actividad maliciosa y cumplir normativas (GDPR, ISO 27001). Ayuda a descubrir comportamientos anómalos antes de que se conviertan en incidentes (p. ej., una conexión inusual a un servidor externo podría indicar exfiltración).

### Herramientas de monitorización
| Herramienta | Descripción |
|---|---|
| **Wireshark** | Inspección en profundidad del tráfico y análisis detallado de paquetes; útil para resolver problemas de conexión y detectar tráfico malicioso. |
| **Nagios** | Monitoreo de la infraestructura y supervisión de dispositivos de red; alertas en eventos críticos o posibles fallos. |
| **Splunk** | Gestión y análisis de registros de eventos; correlación de datos para identificar patrones sospechosos. |
| **SolarWinds NPM** | Visión integral del rendimiento de la red; detecta problemas de latencia o conectividad. |
| **Zabbix** | Plataforma de monitoreo de código abierto para servidores, aplicaciones y dispositivos de red; umbrales de alerta y métricas a gran escala. |
| **PRTG Network Monitor** | Enfoque unificado para redes, servidores, aplicaciones y dispositivos IoT; paneles personalizables. |
| **Cisco Stealthwatch** | Visibilidad y seguridad mediante monitorización continua del tráfico e inteligencia de amenazas. |
| **Graylog** | Análisis de registros (logs) y correlación de eventos; alertas en tiempo real. |

### Prácticas recomendadas
- **Implementar sondas en puntos clave** de la red para una visión completa del tráfico.
- **Configurar alertas automáticas** para patrones anómalos.
- **Realizar auditorías y evaluaciones periódicas.**
- **Capacitar al personal** en la interpretación de reportes.
- **Adoptar Zero Trust y segmentación de red.**
- **Implementar cifrado y autenticación sólida** (TLS/SSL, MFA).
- **Planes de respuesta a incidentes y pruebas de penetración regulares.**

---

## 6.3. Seguridad en protocolos inalámbricos
La naturaleza abierta de las comunicaciones inalámbricas exige protocolos robustos y medidas adicionales.

| Protocolo | Descripción |
|---|---|
| **WEP** (Wired Equivalent Privacy) | Uno de los primeros protocolos; hoy obsoleto por sus numerosas vulnerabilidades; no se recomienda. |
| **WPA** (Wi-Fi Protected Access) | Introdujo **TKIP** como respuesta a las deficiencias de WEP; más seguro que WEP, pero con limitaciones conocidas. |
| **WPA2** | Emplea **AES** para cifrar el tráfico; sigue siendo el estándar más difundido en entornos corporativos. Modo **PSK** (Pre-Shared Key) o **Enterprise (802.1X/EAP)**, más seguro por incorporar un servidor **RADIUS**. |
| **WPA3** | Mejoras como *Forward Secrecy* y mayor solidez frente a ataques de diccionario; indicado para datos sensibles. |

**Medidas de seguridad:** WPA3 siempre que sea posible; cambiar contraseñas predeterminadas de puntos de acceso; controles de acceso basados en direcciones MAC; deshabilitar la transmisión del SSID; auditorías periódicas.

**Consideraciones adicionales:** las **redes mesh** deben gestionarse con herramientas que permitan monitorizar la conexión entre nodos y aplicar parches con eficiencia.

---

## 6.4. Identificación y mitigación de riesgos en servicios de red

### Riesgos potenciales
- **Vulnerabilidades de software:** fallos de código, configuraciones erróneas, parches pendientes. Ej.: exploits en Apache HTTP Server (CVE-2022-24637) o Microsoft Exchange (ProxyShell).
- **Configuraciones incorrectas:** contraseñas predeterminadas, puertos no esenciales abiertos, permisos excesivos, servicios expuestos a Internet por defecto.
- **Ataques DDoS:** saturan recursos; ej.: botnet **Mirai** (dispositivos IoT).
- **Intercepciones de tráfico:** sin protocolos seguros (HTTPS, cifrado) son posibles ataques **MITM**.

### Medidas preventivas principales
- **Actualizaciones y parches:** supervisión de boletines; WSUS y entornos de prueba.
- **Firewall y control de acceso:** reglas de filtrado minuciosas y segmentación (separar producción de pruebas); **WAF** para aplicaciones web.
- **IDS/IPS:** analizan patrones de tráfico y bloquean acciones maliciosas; integrados con el firewall mejoran la respuesta.
- **Pruebas de penetración:** Metasploit o Nessus; documentar hallazgos y ejecutar planes de remediación.

### Intentos de penetración en infraestructuras corporativas
- **Escaneo de puertos** (Nmap): identifica servicios activos y versiones obsoletas.
- **Fuerza bruta:** credenciales predeterminadas o débiles incrementan su efectividad.
- **Inyecciones de código:** SQL Injection, Cross-Site Scripting.
- **Phishing:** ingeniería social; uno de los métodos más frecuentes de acceso inicial.

### Defensas contra penetración
- **MFA:** segundo factor (token, SMS, app).
- **Alertas y monitoreo proactivo** de logins sospechosos y picos de tráfico; análisis de logs en tiempo real.
- **Capacitación del personal** (concienciación y simulaciones).
- **Honeypots y sistemas de decepción:** detección temprana de intrusiones y recopilación de información sobre tácticas de los atacantes.

---

## 6.5. Gestión de intentos de penetración
Buscan identificar y explotar puntos débiles; pueden ser externos o internos y requieren detección y mitigación proactivas.

**Métodos comunes:** escaneo de puertos (Nmap); ataques de fuerza bruta; inyecciones de código (SQL Injection, XSS); ataques de phishing.

---

## A fondo
- **¿Conoces las buenas prácticas para la gestión de redes corporativas?** INCIBE. (s. f.). *Guías de ciberseguridad.* https://www.incibe.es/ciudadania/formacion/guias — enfoque práctico sobre gestión de vulnerabilidades, análisis de riesgos y prevención de incidentes.
- **Profundiza en la seguridad en redes con las redes SDN y entornos cloud.** Stallings, W. (2020). *Foundations of modern networking: SDN, NFV, QoE, IoT, and cloud.* Pearson. El capítulo sobre supervisión de tráfico y calidad del servicio (QoE) conecta con trazabilidad, disponibilidad y detección de anomalías.

---

## Entrenamientos

> **Nota:** en el material original, el Entrenamiento 1 tenía el texto corrupto (la letra «d» sustituida por «p» en muchas palabras: «ipentificar», «pe prueba», «petallapo»…). Aquí está corregido.

### Entrenamiento 1: escaneo y análisis de puertos abiertos
**Planteamiento:** identificar los servicios activos en una máquina de prueba mediante escaneo de puertos, como lo haría un atacante en la fase de reconocimiento.
1. Instala Nmap: `sudo apt install nmap`
2. Elige una IP de destino (equipo de la red local o VM).
3. Escaneo de puertos: `nmap <IP_destino>`
4. Escaneo más detallado: `nmap -sS -sV -O -Pn <IP_destino>`
5. Anota los servicios detectados (puerto, protocolo, versión).
6. Investiga posibles vulnerabilidades en https://cve.mitre.org (búsqueda manual).

**Solución:** permite identificar qué servicios están expuestos, qué versiones usan y cómo un atacante podría elegir objetivos. Si aparece, p. ej., un Apache 2.4.49, puedes verificar si tiene CVE asociados y simular el análisis de riesgo.

### Entrenamiento 2: simulación de ataque de fuerza bruta
**Planteamiento:** sobre un servicio SSH mal configurado con credenciales débiles.
1. VM con SSH habilitado (Ubuntu LTS, por ejemplo).
2. Instala Hydra: `sudo apt install hydra`
3. Crea un archivo de contraseñas: `echo -e "admin\n123456\npassword\nadmin123" > passlist.txt`
4. Ejecuta: `hydra -l root -P passlist.txt ssh://<IP_vm>`
5. Observa si alguna contraseña es válida.

**Solución:** un SSH sin MFA y con contraseñas débiles se vulnera fácilmente. Recomendado: cambiar la contraseña por una segura y activar MFA.

### Entrenamiento 3: detección de configuración insegura y puertos expuestos
**Planteamiento:** auditar configuraciones básicas para detectar malas prácticas.
1. Accede a la máquina por consola o SSH.
2. Lista servicios y puertos: `sudo ss -tulnp`
3. Comprueba HTTP sin HTTPS, Telnet, FTP, o puertos como 23, 21, 3306 expuestos.
4. Revisa usuarios con contraseñas por defecto: `sudo cat /etc/shadow | grep -v '!*'`
5. Opcional: Lynis: `sudo apt install lynis` y `sudo lynis audit system`

**Solución:** cerrar puertos no usados, sustituir protocolos obsoletos y aplicar *hardening* básico.

### Entrenamiento 4: simulación de ataque Man-in-the-Middle en red local
**Planteamiento:** demostrar la necesidad del cifrado de tráfico.
1. Crea dos VM en la misma red (víctima y atacante).
2. En el atacante instala Ettercap o ARPspoof: `sudo apt install ettercap-text-only`
3. Ejecuta: `sudo ettercap -T -M arp:remote -i <interfaz> /victima_IP/ /router_IP/`
4. Desde la víctima abre una página HTTP (no HTTPS).
5. Observa si el atacante captura tráfico en claro.
6. Detén el ataque y analiza el resultado.

**Solución:** sin cifrado (HTTPS) las credenciales pueden interceptarse. Forzar HTTPS, usar protocolos seguros (SSH, FTPS) y segmentar la red.

### Entrenamiento 5: implementación de medidas defensivas básicas
**Planteamiento:** aplicar controles defensivos para mitigar los riesgos de los entrenamientos anteriores.
1. Firewall en Linux: `sudo ufw enable`, `sudo ufw default deny incoming`, `sudo ufw allow ssh`
2. fail2ban para SSH: `sudo apt install fail2ban`, `sudo systemctl enable fail2ban`
3. Revisa logs: `sudo journalctl -xe`, `sudo less /var/log/auth.log`
4. Cambia la contraseña de un usuario por una fuerte: `passwd usuario`
5. Backup semanal automatizado (cron + rsync): `crontab -e` y añadir `0 2 * * 1 rsync -av /datos/ /backup/`

**Solución:** refuerza el bastionado con firewall, protección ante fuerza bruta (fail2ban), contraseñas seguras, revisión de logs y políticas de backup, alineado con buenas prácticas como NIST e ISO 27001.
