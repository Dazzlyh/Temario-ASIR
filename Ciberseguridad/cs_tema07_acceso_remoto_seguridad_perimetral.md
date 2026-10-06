# Tema 7. Implantación de técnicas de acceso remoto. Seguridad perimetral
*Ciberseguridad*

## Índice
Esquema · 7.1 Introducción y objetivos · 7.2 Seguridad perimetral y zonas desmilitarizadas · 7.3 Arquitecturas de subred protegida · 7.4 Redes privadas virtuales (VPN) y técnicas de cifrado · A fondo · Entrenamientos

## Esquema
**Implantación de técnicas de acceso remoto y seguridad perimetral.** *Objetivo:* garantizar la seguridad en accesos remotos y perímetros de red mediante el uso de controles avanzados y segmentación de redes.
- **Seguridad perimetral:** implementación de firewalls de nueva generación (NGFW); uso de sistemas de detección y prevención de intrusiones (IDS/IPS); creación de zonas desmilitarizadas (DMZ) para aislamiento de servicios expuestos.
- **Arquitecturas de subred protegida:** *débil* (un único firewall sin segmentación); *fuerte* (firewalls multicapa y segmentación en VLAN).
- **Redes Privadas Virtuales (VPN):** las VPN con SSL e IPsec garantizan conexiones seguras mediante cifrado, protegiendo accesos remotos; su efectividad depende de una correcta configuración y gestión.
- **Estrategias de mitigación:** 1) aplicación de firewalls multicapa y segmentación de red; 2) MFA en accesos remotos; 3) auditorías periódicas, siempre acompañadas de configuración de reglas estrictas de acceso.

---

## 7.1. Introducción y objetivos
La seguridad perimetral es una de las principales líneas de defensa de las redes corporativas. Con la exposición a Internet y el teletrabajo, proteger los límites de una red es esencial. El módulo cubre firewalls, IDS/IPS, DMZ y VPN, y la evolución de las arquitecturas de red, de las débiles a las robustas con segmentación y monitoreo continuo.

Objetivos:
- Comprender los fundamentos de la seguridad perimetral como primera barrera.
- Analizar las arquitecturas de subred protegida (débil y fuerte).
- Estudiar la configuración y uso de **DMZ**.
- Identificar el papel de firewalls e **IDS/IPS**.
- Evaluar las tecnologías **VPN**, sus tipos y mecanismos de cifrado, frente a líneas dedicadas.
- Reconocer los principios de la criptografía asimétrica.
- Aplicar criterios de diseño seguros en entornos corporativos reales.

---

## 7.2. Seguridad perimetral y zonas desmilitarizadas
Medidas tecnológicas y de gestión para proteger los límites de una red, previniendo accesos no autorizados. Actúa como **primera línea de defensa**.

### Componentes clave
**Firewalls:** filtran y controlan el tráfico según reglas predefinidas; barrera entre redes internas seguras y externas.
- *Basados en hardware:* Cisco ASA, FortiGate.
- *Basados en software:* pfSense, ZoneAlarm.
- *Híbridos:* combinan ambos.
- *Funcionalidades avanzadas:* **DPI** (inspección profunda de paquetes); **NGFW** (detección de amenazas, VPN y control de aplicaciones).
- *Configuración recomendable:* reglas estrictas por puertos y protocolos; actualizar definiciones; registros y auditorías.

**IDS/IPS:** complementan al firewall analizando tráfico sospechoso en tiempo real.
- **IDS:** identifica actividades sospechosas y genera alertas. **IPS:** bloquea el tráfico malicioso antes de que alcance su destino.
- Ejemplos: **Snort** (IDS de código abierto) y **Suricata** (IPS con capacidades en tráfico cifrado).
- Beneficios: mitigación de DDoS y fuerza bruta; identificación de vulnerabilidades de configuración.

**Puertas de enlace seguras:** intermediarios entre usuarios y red. **DPI** para detectar malware o patrones sospechosos incluso en tráfico cifrado. Aplicaciones: filtros web y pasarelas de correo (anti-phishing).

### Zonas desmilitarizadas (DMZ)
Subred con servicios accesibles desde el exterior (web, FTP, DNS) que aísla estos servicios de la red interna, minimizando el impacto de un ataque.
- **Configuración ideal:** firewall entre la DMZ y la red interna; restringir tráfico con el principio de menor privilegio; monitorizar continuamente. Se pueden usar firewalls en ambos extremos de la DMZ; restringir al mínimo las conexiones DMZ↔red interna; auditorías regulares.
- **Ventajas:** contener ataques externos en un área aislada; reducir la superficie de ataque; segregar servicios públicos y privados.

### Arquitectura débil de subred protegida (resumen)
Configuración mínima de seguridad: un único firewall para toda la red, falta de segmentación, dependencia de configuraciones predeterminadas. Riesgos: alta vulnerabilidad a ataques dirigidos, difícil detección de movimientos laterales, limitada respuesta a incidentes.

---

## 7.3. Arquitecturas de subred protegida

### Arquitectura débil
Enfoque básico y limitado; puede bastar en entornos de bajo riesgo, pero es inadecuada para información crítica. Punto de partida de organizaciones con recursos limitados.

> **Nota:** en el material original, la «Tabla 1. Características de una arquitectura débil» contiene por error la tabla de protocolos inalámbricos (WEP/WPA/WPA2/WPA3) del Tema 6. Las características reales se resumen arriba en 7.2.

**Riesgos asociados:**

| Riesgo | Detalle |
|---|---|
| Alta vulnerabilidad frente a ataques dirigidos | La falta de segmentación facilita comprometer la red completa tras vulnerar un único punto; depender de un único firewall deja la red expuesta si falla. |
| Difícil detección de movimientos laterales | Sin monitoreo interno es complejo identificar a un atacante que se mueve entre dispositivos. |
| Capacidad de respuesta limitada | Ausencia de herramientas avanzadas; configuración simple sin bloqueo granular. |

**Ejemplo práctico:** una pequeña empresa de desarrollo web con un firewall que filtra conexiones básicas. Un atacante explota una vulnerabilidad en el servidor FTP; sin segmentación ni monitoreo, se mueve lateralmente a la base de datos de clientes y roba información. *Lecciones:* la segmentación podría haber aislado el FTP; un IDS habría alertado del tráfico sospechoso.

**Mejora de una arquitectura débil:**

| Acción | Detalle |
|---|---|
| Incorporar segmentación de redes | VLAN para separar servicios críticos; firewalls internos para subredes sensibles. |
| Adoptar IDS/IPS | Monitorear tráfico interno; respuestas automáticas de bloqueo. |
| Personalizar configuraciones | Cambiar contraseñas por defecto y limitar permisos; reglas por mínimo privilegio. |
| Capacitación del personal | Mejores prácticas de configuración y monitoreo. |

### Arquitectura fuerte
Modelo avanzado con controles y segmentaciones múltiples; esencial donde la protección de datos sensibles es prioritaria.

- **Segmentación de redes:** subredes aisladas con nivel de seguridad específico, mediante **VLAN**. *Ventajas:* contención de amenazas; mejora del rendimiento. *Ejemplo:* VLAN separadas para servidores, estaciones de trabajo e IoT.
- **Firewalls multicapa:** dedicados en puntos estratégicos; **NGFW** con DPI y control de aplicaciones; reglas específicas por subred; actualización regular.
- **Monitorización constante:** **SIEM** (*security information and event management*): recopilan y correlacionan eventos. *Beneficios:* respuesta rápida por alertas automáticas; análisis avanzado de patrones a largo plazo.

**Implementación (3 pasos):**
1. **Diseño de la red:** identificar activos críticos y clasificar datos por sensibilidad; esquema de segmentación que aísle recursos clave (bases de datos, sistemas financieros, correo).
2. **Configuración de firewalls multicapa:** firewalls entre subredes con reglas específicas; **DMZ** para servicios expuestos.
3. **Monitoreo y auditoría:** SIEM (Splunk, AlienVault); auditorías regulares.

**Beneficios:** reducción de la superficie de ataque; capacidad de respuesta mejorada; cumplimiento normativo (GDPR, HIPAA, ISO 27001).
**Limitaciones:** costo inicial; complejidad operativa (personal capacitado); necesidad de actualizaciones constantes.

---

## 7.4. Redes privadas virtuales (VPN) y técnicas de cifrado
Las **VPN** establecen conexiones seguras y cifradas entre dispositivos remotos y redes corporativas; protegen la información en tránsito (teletrabajo).

### Funcionamiento
Crea un **túnel cifrado** entre el dispositivo del usuario y la red corporativa.

| Fase | Descripción |
|---|---|
| Establecimiento de conexión | El cliente VPN se conecta a un servidor VPN mediante un protocolo (SSL, IPsec…); se negocia una clave de cifrado. |
| Cifrado de datos | Algoritmos avanzados como AES-256; la información es ilegible si se intercepta. |
| Redirección del tráfico | Todo el tráfico pasa por el túnel cifrado hacia el servidor VPN, que lo enruta a su destino. |

### Tipos de VPN
- **VPN SSL:** conexiones seguras a través de navegadores; ideal para acceso a aplicaciones específicas. *Ventajas:* fácil implementación; sin software adicional en el cliente. *Desventajas:* limitada a aplicaciones accesibles por navegador; menos flexible.
- **VPN IPsec:** asegura la comunicación a nivel de red. *Ventajas:* compatible con muchos dispositivos y SO; cifrado y autenticación robustos. *Desventajas:* configuración más compleja en el cliente; posibles problemas con redes NAT.
- **VPN híbridas:** combinan SSL e IPsec; alta seguridad con facilidad de acceso; adaptables.

### Aplicaciones
Teletrabajo; conexiones entre sedes (túneles cifrados); protección de la privacidad (enmascara la IP); acceso a recursos restringidos geográficamente.

### Beneficios y limitaciones
- **Beneficios:** seguridad (protección contra escuchas e intercepción); flexibilidad; cumplimiento normativo (GDPR).
- **Limitaciones:** velocidad (el cifrado y la redirección la reducen); dependencia de la infraestructura (una mala configuración del servidor VPN compromete la seguridad).

### Frente a líneas dedicadas
- *Beneficios:* coste significativamente menor; flexibilidad para conectar múltiples ubicaciones y usuarios; alta disponibilidad por redundancia.
- *Desventajas:* mayor dependencia de la conexión a Internet; requiere configuraciones avanzadas; potencialmente vulnerable a DDoS dirigidos al proveedor de Internet.

### Técnicas de cifrado: clave pública y clave privada
La **criptografía asimétrica** protege datos en tránsito y en reposo (confidencialidad, integridad y autenticidad).
- **Clave pública:** compartida libremente; cifra datos que solo la privada correspondiente puede descifrar.
- **Clave privada:** confidencial; descifra y genera **firmas digitales**.
- **Matemática subyacente:** factorización de números primos grandes o logaritmo discreto: costosos de resolver sin una de las claves.

**Funcionamiento:** 1) generación del par de claves (RSA, ECC, ElGamal); 2) cifrado: el remitente cifra con la clave pública del destinatario; 3) descifrado: el destinatario usa su clave privada.

**Aplicaciones principales:**

| Aplicación | Detalle |
|---|---|
| Firmas digitales | La clave privada del remitente genera la firma; el destinatario la valida con la pública (autenticidad y no repudio). |
| Cifrado de correos electrónicos | **PGP** (*pretty good privacy*): el contenido se cifra con la clave pública del destinatario. |
| Protocolos seguros | **TLS/SSL** (HTTPS): la clave pública negocia una clave simétrica que cifra la comunicación. **SSH**: conexiones remotas seguras mediante validación de claves. |

**Ventajas:** seguridad robusta sin compartir claves privadas; autenticación mediante firmas; adecuado para entornos abiertos sin intercambio previo de claves.
**Desventajas:** mayor potencia computacional que el cifrado simétrico; claves de longitud considerable para resistir ataques avanzados.

---

## A fondo
- **¿Conoces las configuraciones de VPN para entornos empresariales?** INCIBE. (s. f.). *Guías y manuales de ciberseguridad.* https://www.incibe.es — gestión de firewalls, segmentación de redes, configuración de VPN y detección de intrusiones.
- **¿Quieres profundizar en la seguridad de red a fondo?** Tanenbaum, A. S. y Wetherall, D. J. (2011). *Computer Networks.* Pearson. Capítulos sobre seguridad de red, firewalls, protocolos de cifrado y segmentación.

---

## Entrenamientos

### Entrenamiento 1: configuración de firewall con UFW
**Planteamiento:** permitir únicamente los servicios esenciales y bloquear el resto.
```bash
sudo apt install ufw
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
sudo ufw status numbered
```
**Solución:** firewall activo, solo servicios esenciales permitidos; refuerza el principio de mínimo privilegio.

### Entrenamiento 2: implementación de una DMZ virtual con dos firewalls
**Planteamiento:** simular una arquitectura con una DMZ entre dos firewalls para proteger un servidor web expuesto.
1. Tres VM: firewall frontal, DMZ (con servidor web) e interna.
2. Primer firewall: solo tráfico HTTP hacia la DMZ.
3. Segundo firewall: solo tráfico específico desde la DMZ hacia la red interna (p. ej., actualizaciones).
4. Simular acceso desde Internet al servidor web.
5. Probar conexión desde la DMZ hacia la red interna (debe estar limitada).

**Solución:** la DMZ actúa como amortiguador: el servidor web es accesible sin que la red interna lo sea.

### Entrenamiento 3: detección de amenazas con Snort (IDS)
**Planteamiento:** registrar intentos de escaneo de puertos.
1. `sudo apt install snort`
2. Configurar la interfaz de red a monitorizar.
3. Archivo de logs: `/var/log/snort/alert`
4. Ejecutar: `sudo snort -A console -q -c /etc/snort/snort.conf -i eth0`
5. Desde otra máquina, escaneo con Nmap al objetivo.
6. Observar alertas.

**Solución:** Snort detecta el escaneo y genera alertas.

### Entrenamiento 4: creación de una VPN con WireGuard
**Planteamiento:** VPN segura y ligera para acceso remoto cifrado a una red interna.
1. `sudo apt install wireguard` en servidor y cliente.
2. Generar claves pública y privada en ambas partes.
3. Configurar `/etc/wireguard/wg0.conf` en el servidor con IP interna y claves.
4. Configurar el cliente con los mismos parámetros en su `wg0.conf`.
5. Habilitar e iniciar: `sudo systemctl start wg-quick@wg0`
6. Verificar conectividad y cifrado.

**Solución:** el cliente accede de forma segura mediante un túnel cifrado.

### Entrenamiento 5: análisis de tráfico con Wireshark
**Planteamiento:** capturar y analizar tráfico para identificar comunicaciones inseguras o no autorizadas.
1. Instalar Wireshark.
2. Iniciar captura en la interfaz activa.
3. Generar tráfico: sitio HTTP, conexión SSH o escaneo Nmap.
4. Filtros: `http`, `tcp.port == 22`, `ip.addr == <IP objetivo>`
5. Identificar tráfico no cifrado y patrones sospechosos.

**Solución:** se ve el contenido en protocolos sin cifrado y actividad sospechosa (p. ej., múltiples SYN).
