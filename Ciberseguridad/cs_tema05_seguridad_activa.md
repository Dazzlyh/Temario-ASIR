# Tema 5. Implantación de mecanismos de seguridad activa
*Ciberseguridad*

## Índice
Esquema · 5.1 Introducción y objetivos · 5.2 Clasificación de ataques y análisis de amenazas · 5.3 Herramientas preventivas y paliativas: instalación y configuración · 5.4 Actualización de sistemas y aplicaciones · 5.5 Seguridad en redes públicas y aplicación de prácticas seguras · A fondo · Entrenamientos

## Esquema
**Implantación de mecanismos de seguridad activa**
- **Identificación y clasificación de ataques:** análisis de amenazas para diseñar defensas eficaces junto con detección de patrones de ataque.
- **Herramientas preventivas y paliativas:** *preventivas:* firewalls, antivirus, sistemas de detección de intrusos; *paliativas:* copias de seguridad, planes de recuperación, monitoreo en tiempo real.
- **Seguridad en redes públicas:** uso de VPN para cifrar tráfico; segmentación de redes para limitar exposición; protección contra ataques Man-in-the-Middle (MitM).
- **Prácticas seguras y gestión de credenciales:** autenticación multifactor acompañada de contraseñas robustas y, desde la directiva de empresa, generar auditorías periódicas.

---

## 5.1. Introducción y objetivos
La seguridad activa permite anticiparse y responder a amenazas como malware, phishing, fuerza bruta y explotación de vulnerabilidades, que comprometen confidencialidad, integridad y disponibilidad.

Objetivos:
- Identificar y clasificar los tipos de ataques y sus implicaciones.
- Conocer la anatomía de los ataques para implementar estrategias de detección y mitigación.
- Dominar la instalación, configuración y gestión de herramientas **preventivas y paliativas**.
- Implementar procesos de actualización de sistemas y aplicaciones.
- Aplicar pautas y prácticas seguras en redes públicas y actividades cotidianas.

---

## 5.2. Clasificación de ataques y análisis de amenazas
Los sistemas personales son objetivo recurrente por su amplia adopción y la información sensible que almacenan.

### Tipos de ataques
- **Malware:** *virus* (infectan ejecutables y se propagan al ejecutarlos), *ransomware* (bloquea los datos hasta el pago de un rescate), *spyware* (monitorea y recopila información sin consentimiento).
- **Phishing:** *spear phishing* (individuos específicos) y *whaling* (altos ejecutivos).
- **Fuerza bruta:** probar combinaciones de contraseñas hasta dar con la correcta.
- **Explotación de vulnerabilidades:** errores del software para acceder o comprometer la integridad.

### Contramedidas
- **Software de protección:** antivirus y antimalware avanzados (p. ej., CrowdStrike), con firmas actualizadas.
- **Prácticas del usuario:** no abrir correos de desconocidos; evitar enlaces sospechosos y descargas no confiables.
- **Seguridad de redes:** firewalls personales y VPN en redes públicas.

### Clasificación de ataques (NIST, ISO 27001)
**Según su naturaleza**
- *Activos* (interacción directa; cambios inmediatos): inyección SQL; *defacement* (modificación no autorizada del contenido web); malware.
- *Pasivos* (no alteran, recopilan): *sniffing* de tráfico; análisis de metadatos; *eavesdropping*.

**Por origen**
- *Internos* (acceso autorizado; muy peligrosos por conocimiento previo): exfiltración de datos; sabotaje interno; uso indebido de privilegios.
- *Externos:* phishing; fuerza bruta; DDoS.

**Por objetivo**
- *Confidencialidad:* robo de datos; *keylogging*; ataques **MitM**.
- *Disponibilidad:* DDoS; sabotaje físico; malware destructivo.
- *Integridad:* alteración de registros financieros; manipulación de sistemas **SCADA**; *spoofing*.

**Otras clasificaciones**
- *Por tipo de vector:* software, hardware, sociales (ingeniería social: phishing, baiting, pretexting).
- *Por nivel de automatización:* manual; automatizado (scripts, bots).
- *Por motivación:* económica; política o estatal; hacktivismo; competencia desleal.

### Anatomía de ataques (Kill Chain)
1. **Reconocimiento:** recopilar información de objetivos (Nmap, redes sociales, DNS, WHOIS).
2. **Preparación:** seleccionar/desarrollar herramientas; malware dirigido (Metasploit); pruebas controladas.
3. **Entrega:** transportar el malware (phishing dirigido, sitios comprometidos, USB infectados, mensajería, P2P).
4. **Explotación:** ejecución activa del malware; *exploits* para ejecución remota de código; scripts automatizados.
5. **Instalación:** persistencia: puertas traseras (*backdoors*), *rootkits*, *keyloggers*.
6. **Acceso:** exfiltración, sabotaje o ataque a otros sistemas; movimientos laterales.
7. **Eliminación de evidencias:** borrar rastros; alterar registros de auditoría; modificar datos temporales y sellos de tiempo.

### Análisis de software malicioso
- **Análisis estático:** sin ejecutar el malware; desensambladores (IDA Pro, Ghidra); firmas digitales y estructuras de archivo sospechosas. *Ventaja:* detección rápida y segura, sin riesgo de infección.
- **Análisis dinámico:** ejecutar en entornos controlados (*sandboxes*, p. ej., Cuckoo Sandbox); monitoreo de cambios en archivos, procesos, registro y tráfico. *Ventaja:* comportamientos avanzados, generación de **IoC** y comprensión profunda.

---

## 5.3. Herramientas preventivas y paliativas: instalación y configuración
Las **herramientas preventivas** son la primera barrera defensiva; deben ser robustas, flexibles, adaptativas y estar integradas y actualizadas.

### Herramientas preventivas
**Firewall.** Controla el tráfico según reglas predefinidas. Tipos: de red, de aplicaciones, en la nube. Instalación en puntos críticos de la red. Configuración: reglas detalladas de acceso; **NAT** para proteger IP internas; listas blancas/negras; registro y monitoreo constante.

**IPS (sistemas de prevención de intrusiones).** Detectan y bloquean amenazas mediante análisis en tiempo real. Tipos: **HIPS** (host) y **NIPS** (red). Instalación en puertas de enlace y segmentos críticos. Configuración: actualización continua de firmas; reglas personalizadas; alertas automáticas; ajuste fino para minimizar falsos positivos.

**Antivirus.** Detección basada en comportamiento; protección contra amenazas de día cero mediante IA; integración con monitoreo de red. Instalación en todos los puntos finales. Configuración: escaneos automáticos regulares; exclusiones para reducir falsos positivos; protección en tiempo real; cuarentena automática.

**EPP (plataformas de protección de puntos finales).** Monitoreo continuo y detección de comportamientos sospechosos; **DLP** (prevención de fuga de datos); análisis forense y respuesta a incidentes. Agentes en todos los dispositivos, políticas unificadas sobre acceso y periféricos, integración con gestión centralizada.

### Herramientas paliativas
Mitigan efectos posteriores a incidentes y facilitan la recuperación.
- **Recuperación de desastres:** Veeam, Acronis, Commvault; infraestructura híbrida o en la nube; respaldo automático, almacenamiento redundante, planificación de **RTO** (tiempo de recuperación) y **RPO** (punto de recuperación), pruebas periódicas de restauración.
- **Monitoreo continuo:** Splunk, Nagios, SolarWinds, ELK Stack; dashboards personalizados, alertas automáticas, integración con respuesta automática.
- **Respuesta a incidentes:** IBM Resilient, ServiceNow Security Operations, TheHive; *playbooks* según tipo de incidente; simulacros periódicos.

### Consideraciones críticas
- **Capacitación del personal:** dominio de las herramientas, simulacros regulares, actualización sobre amenazas.
- **Auditorías y evaluaciones periódicas:** alineación de políticas, configuración efectiva, controles redundantes.

---

## 5.4. Actualización de sistemas y aplicaciones
El software desactualizado es una de las principales puertas de entrada.

**Importancia:** parcheo de vulnerabilidades; mejora del rendimiento; cumplimiento normativo (GDPR, ISO 27001).

**Estrategias:**
- **Automatización:** WSUS (Windows Server Update Services) y SCCM (System Center Configuration Manager).
- **Pruebas en entornos de prueba (*staging*)** antes de producción.
- **Planificación de horarios:** ventanas de mantenimiento.
- **Parcheo prioritario:** primero las críticas de seguridad.

**Buenas prácticas:** inventario actualizado de hardware y software; supervisar boletines de seguridad de los fabricantes; auditorías regulares de aplicación de actualizaciones.

---

## 5.5. Seguridad en redes públicas y aplicación de prácticas seguras
Las redes Wi-Fi públicas (cafeterías, aeropuertos, bibliotecas) son un riesgo significativo.

**Riesgos:** ataques **MITM**; *sniffing* de tráfico (Wireshark) en texto plano; redes falsas (puntos de acceso fraudulentos).

| Medida | Detalle |
|---|---|
| Uso de VPN | Cifrado de tráfico con OpenVPN o WireGuard; configurar para activarse automáticamente en redes públicas. |
| HTTPS Everywhere | Extensiones que fuerzan HTTPS. |
| Deshabilitar conexión automática | Evitar conexión automática a redes Wi-Fi no reconocidas. |
| Uso de redes móviles | Priorizar datos móviles en tareas sensibles. |
| Cuidado con redes abiertas | Evitar transacciones bancarias o información confidencial. |

**Herramientas recomendadas:** ExpressVPN y NordVPN (cifrado AES-256); Wireshark (también para detectar interceptaciones).

### Principios generales de las prácticas seguras
1. **Contraseñas robustas:** al menos 12 caracteres; gestores como LastPass o Bitwarden.
2. **Autenticación multifactorial (MFA):** tokens o apps como Google Authenticator.
3. **Actualizaciones regulares** con los parches más recientes.
4. **Cifrado de datos** en reposo y en tránsito (AES-256).
5. **Backup periódico:** regla **3-2-1**.

### Prácticas para administradores
- **Segmentación de redes:** limitar el movimiento lateral.
- **Monitoreo activo:** Splunk o Nagios.
- **Gestión de accesos:** principio de menor privilegio.

### Capacitación y concienciación
Programas de formación periódicos; simulaciones de ataques (phishing) controladas.

---

## A fondo
- **¿Conocemos todos los términos usados en ciberseguridad?** INCIBE. *Guías y manuales de ciberseguridad.* https://www.incibe.es/empresas/guias
- **¿Cómo nos ubicamos dentro de los frameworks internacionales?** NIST. *Framework for Improving Critical Infrastructure Cybersecurity.* https://www.nist.gov/cyberframework/framework

---

## Entrenamientos

### Entrenamiento 1: configuración básica de un firewall
1. Instala un firewall sencillo (Windows Defender Firewall o `ufw` en Linux).
2. Bloquea todo el tráfico entrante por defecto.
3. Permite solo tráfico entrante en HTTP (80) y HTTPS (443).
4. Prueba navegando y verificando que otros servicios estén bloqueados.

**Solución:** `sudo ufw status` (o el panel del firewall) debe mostrar solo abiertos los puertos 80 y 443.

### Entrenamiento 2: instalación y ejecución de un antivirus
1. Descarga un antivirus gratuito (Avast, AVG o Windows Defender).
2. Instálalo.
3. Actualiza la base de amenazas.
4. Ejecuta un análisis completo.
5. Revisa el reporte.

**Solución:** informe con las amenazas detectadas, mostrando la efectividad del antivirus.

### Entrenamiento 3: simulación de backup automático
1. Selecciona una carpeta con archivos importantes.
2. Usa Cobian Backup (Windows) o `rsync` (Linux).
3. Configura una tarea automática diaria a una hora específica.
4. Verifica manualmente que los respaldos se crean.

**Solución:** creación automática de respaldos en el destino, visualizando los archivos.

### Entrenamiento 4: configuración de alertas de monitoreo
1. Instala Nagios Core o Zabbix.
2. Añade un equipo o servicio para monitorear (disponibilidad de red o CPU).
3. Configura alertas automáticas por correo o mensaje.
4. Simula una alerta.

**Solución:** alerta recibida correctamente en el correo o sistema de notificaciones.

### Entrenamiento 5: creación de un playbook básico para incidentes
1. Identifica acciones ante un incidente de malware (aislar equipo, escanear con antivirus, recopilar logs).
2. Describe cada paso en un procesador de texto.
3. Incluye responsables y tiempos estimados.
4. Realiza una simulación siguiendo el playbook.

**Solución:** documento estructurado (playbook) que permite actuar rápido y evaluar su efectividad.
