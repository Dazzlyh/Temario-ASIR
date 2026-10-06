# Tema 8. Bastionado de redes y sistemas
*Ciberseguridad*

## Índice
Esquema · 8.1 Introducción y objetivos · 8.2 Diseño de planes de securización · 8.3 Configuración de sistemas de control de acceso y dispositivos informáticos · 8.4 Administración de credenciales y diseño de redes seguras · 8.5 Configuración avanzada de sistemas y dispositivos · A fondo · Entrenamientos

## Esquema
**Bastionado de redes y sistemas**
- **Administración de credenciales:** uso de gestores de contraseñas y almacenamiento seguro, todo sujeto a políticas de cambio; restricción de privilegios y segmentación de permisos.
- **Diseño:** *planes de securización* (evaluación de riesgos; definición de políticas de seguridad; implementación de normas y políticas; formación del personal); *redes seguras* (segmentación de redes; configuración de firewall y sistemas IPS/IDS).
- **Configuración de sistemas de control de acceso, sistemas y dispositivos:** aplicación de autenticación multifactorial (MFA); aplicación de parches de seguridad; actualizaciones constantes; monitorización de accesos y auditorías de seguridad; desactivación de servicios innecesarios; generación de registros de seguridad.

---

## 8.1. Introducción y objetivos
La adopción de pautas de seguridad es esencial para proteger los sistemas y preservar la integridad operativa. Se aborda desde el diseño de **planes de securización** y la configuración segura de sistemas hasta la **administración centralizada de credenciales**, con un enfoque integral técnico, humano y organizativo.

Objetivos:
- Comprender los fundamentos de la gestión de la seguridad de la información (políticas, estándares y procedimientos).
- Analizar la clasificación de la información y los roles asociados.
- Identificar controles de seguridad física, lógica y administrativa.
- Configurar sistemas de control de acceso y autenticación (contraseñas, MFA, certificados digitales, tokens).
- Evaluar modelos de control de acceso (DAC, MAC, RBAC) e integración con arquitecturas **AAA**.
- Conocer la gestión de claves criptográficas (simétricas y asimétricas).
- Diseñar redes seguras: segmentación, firewalls, DMZ y redundancia.
- Aplicar buenas prácticas de bastionado: desactivar servicios innecesarios, registro de eventos y protección física.

---

## 8.2. Diseño de planes de securización
Objetivo de la gestión de la seguridad: asegurar **confidencialidad, integridad y disponibilidad**. Se establece un **programa de gestión de seguridad**: conjunto estructurado de actividades planificadas y coordinadas, comprensible y accesible a todos los niveles. No es una acción puntual, sino una función estratégica y continua. Figuras clave: el **responsable de seguridad de la información (RSI)** o **CISO**.

Instrumentos normativos (Figura 1):
- **Políticas:** establecen las directrices generales.
- **Estándares:** establecen las herramientas requeridas.
- **Líneas base:** establecen los parámetros que se utilizarán.
- **Procedimientos:** guías paso a paso que se deben realizar diariamente.

Los **programas de concienciación y formación** son clave: la seguridad no depende solo de herramientas, sino del compromiso de quienes interactúan con sistemas y datos.

Todo programa parte de un proceso de **gestión de riesgos**: identificar amenazas, valorar su probabilidad y estimar su impacto sobre los activos. Sus resultados fundamentan los **controles de seguridad** (técnicos, físicos o administrativos). Las políticas son un control administrativo.

### Clasificación de la información
No toda la información tiene el mismo valor o sensibilidad (secretos industriales, algoritmos, estrategias comerciales). Clasificarla permite asignar protección proporcional al valor, criticidad o sensibilidad; demuestra compromiso con la seguridad (RGPD, ISO/IEC 27001) y facilita requisitos legales (datos personales, propiedad intelectual, información financiera).

**Niveles de clasificación — entorno gobierno:**

| Tipo | Definición |
|---|---|
| Sin clasificar | (En el material: «Puede ser menos seguro, ya que los propietarios podrían otorgar permisos inadvertidos» — texto copiado por error de otra tabla.) |
| Sensible pero no clasificada | Información con un impacto menor si se difunde. |
| Confidencial | Su difusión puede causar daño a la seguridad nacional. |
| Secreta | Su difusión causaría un daño importante. |
| Alto secreto | Su difusión causaría un daño extremadamente grave. |

**Entorno empresa:**

| Tipo | Definición |
|---|---|
| Uso público | Puede difundirse públicamente. |
| Uso interno | Se puede difundir internamente, no externamente (p. ej., información sobre proveedores y su eficiencia). |
| Confidencial | La más sensible (fórmulas de productos, productos nuevos, fusiones en curso). |

Hay que considerar también la **información personal** (regulada por ley, p. ej. RGPD: salario, historial médico) y la **antigüedad** de la información (desclasificación, pérdida de valor estratégico).

**Roles y procedimientos:**
- **Propietario del activo (*owner*):** responsable último; define su criticidad y delega tareas operativas.
- **Responsable o custodio (*custodian*):** personal técnico; respaldos, acceso autorizado, integridad.
- **Usuario:** respeta las políticas y protege la información.

Pasos del proceso: identificar y asignar roles; definir criterios (valor, impacto, sensibilidad, vigencia); clasificación formal por el propietario; documentar excepciones; aplicar controles según el nivel; definir desclasificación o transferencia de custodia; programa de concienciación.

### Articulación de la seguridad a través de controles
**Riesgo** = probabilidad de que una amenaza explote una vulnerabilidad con consecuencias adversas. Se apoya en la **evaluación de riesgos** (*risk assessment*). Ej.: ISO/IEC 27001:2013 control **A.9.3.1** (buenas prácticas de contraseñas): se materializa en políticas y procedimientos, pero no elimina el riesgo (p. ej., phishing).

### Seguridad física y lógica
La seguridad física es crítica incluso con buenas configuraciones lógicas. Caso emblemático: el **búnker de Bahnhof en Estocolmo** (servidores de Wikileaks): estabilidad geológica, redundancia eléctrica, control de accesos y climatización. El principal riesgo sigue siendo el **acceso físico no autorizado**.

**Donn B. Parker (1998)** — siete fuentes principales de pérdida física: **temperatura** (fuego, sobrecalentamiento); **gases** (sustancias químicas o tóxicas); **líquidos** (inundaciones); **organismos** (virus, bacterias, plagas, intervención humana); **proyectiles** (impactos externos, balísticos o explosivos); **movimientos** (terremotos, vibraciones, caídas); **anomalías eléctricas** (picos de voltaje, campos magnéticos, fallos de alimentación).

**Controles de seguridad física:**
- *Administrativos:* planificación de requisitos de las instalaciones; gestión de la seguridad del entorno; control de acceso del personal.
- *Del entorno y habitabilidad:* suministro eléctrico estable y protegido; detección y extinción de incendios; climatización (HVAC).
- *Técnicos y físicos:* inventario y protección de equipos críticos; control de acceso físico (tarjetas, biometría); monitoreo de las instalaciones; alarmas contra intrusión y vigilancia electrónica; gestión segura de soportes de almacenamiento.

**Controles aplicados al personal:** el ser humano es uno de los elementos más vulnerables (ingeniería social). La seguridad debe concebirse como un **sistema sociotécnico**: políticas claras, formación continua y control sobre la actuación del personal.

---

## 8.3. Configuración de sistemas de control de acceso y dispositivos informáticos

### Mecanismos de autenticación
Verifican que un usuario es quien dice ser mediante uno o varios factores. Forman parte de la arquitectura **AAA**: **autenticación** (verifica identidad), **autorización** (determina a qué recursos accede), **auditoría** (registra y monitoriza actividades).

**Tipos de factores:** algo que **sabes** (contraseñas, PIN), algo que **tienes** (tokens, tarjetas inteligentes, OTP), algo que **eres** (huella, facial, retina), algún lugar **donde estás** (geolocalización, IP), algo que **haces** (dinámica de tecleo, movimiento del ratón).

### Modelos de control de acceso
- **Discrecional (DAC):** el propietario define quién accede. Flexible, pero más vulnerable a amenazas internas y a ataques indirectos como los caballos de Troya.
- **Obligatorio (MAC):** el sistema regula el acceso mediante etiquetas de seguridad clasificadas. Extremadamente seguro pero inflexible.
- **Basado en roles (RBAC):** privilegios según roles; facilita la gestión y el mínimo privilegio.

**Políticas de acceso:** roles claros; segmentar recursos sensibles; autorizaciones multinivel en operaciones críticas.

### Sistemas de autenticación
- **Contraseñas y OTP:** contraseñas almacenadas cifradas (SHA-256), con cambio periódico y combinación con doble autenticación. **OTP:** válidas solo para una sesión o transacción (hardware o app móvil).
- **Autenticación multifactor:** combinar factores dificulta los accesos no autorizados; protege contra phishing y fuerza bruta.
- **Tokens y tarjetas inteligentes:** tokens USB y dispositivos criptográficos generan códigos de un solo uso o firmas digitales; tarjetas con chips para almacenar claves criptográficas.
- **Certificados digitales:** emitidos por **autoridades de certificación (CA)**; verifican la identidad mediante un par de claves. Ejemplo: **DNI electrónico** (microchip con certificados de autenticación y firma digital).

### Buenas prácticas
- **Seguridad de contraseñas:** longitud y complejidad mínimas; hashes seguros con *salting*; evitar reutilización.
- **Monitorización y auditoría:** registrar intentos fallidos y accesos sospechosos; alertas automáticas; revisiones regulares.
- **Sistemas estandarizados:** **EAP-TLS** o **RADIUS**; expiración de sesión.

---

## 8.4. Administración de credenciales y diseño de redes seguras
Los **almacenes de claves (*key vaults*)** gestionan el ciclo de vida completo de las claves: generación, uso, almacenamiento, archivado y destrucción, con protección física y lógica. Una buena gestión es indispensable aunque se usen algoritmos robustos: si el atacante obtiene la clave, descifra sin vulnerar el algoritmo (la clave es como la combinación de una caja fuerte).

**Requisitos de un sistema robusto de gestión de claves:**
- Control del ciclo de vida: generación, preactivación, activación, expiración, desactivación, custodia, destrucción.
- Protección del acceso físico y lógico a los servidores donde se almacenan.
- Gestión granular de permisos de usuario sobre las claves.

### Tipos de claves
- **Simétrica:** el mismo secreto cifra y descifra; para datos en reposo (bases de datos, archivos).
- **Asimétrica:** par pública/privada; para datos en tránsito (VPN, HTTPS). Ej.: una VPN cifra con la clave pública del servidor y este descifra con su clave privada.

### Sistemas de claves simétricas: conceptos clave
- **DEK** (*Data Encryption Key*): clave que cifra/descifra los datos directamente.
- **KEK** (*Key Encryption Key*): clave que cifra otras claves (como las DEK).
- **KM API** (*Key Management API*): interfaz para el intercambio seguro de claves entre servidores y aplicaciones.
- **CA** (autoridad de certificación): emite y gestiona certificados digitales.
- **TLS:** protocolo que asegura la transmisión con cifrado y autenticación mutua.
- **KMS** (*Key Management System*): creación, custodia, renovación y destrucción de claves.

### Sistemas de claves asimétricas: intercambio
1. El remitente envía su certificado digital al receptor.
2. El receptor verifica su validez mediante su **CA** o una autoridad de validación (**VA**).
3. Tras autenticarse, el receptor envía su propio certificado.
4. El remitente solicita la clave pública del receptor, que se la proporciona.
5. El remitente genera una **clave simétrica efímera** (solo para esa sesión), cifra el archivo con ella y cifra la clave simétrica con la clave pública del receptor.
6. El receptor descifra la clave simétrica con su clave privada y luego los datos.

Combina las ventajas de la asimétrica (intercambio seguro) y de la simétrica (rendimiento con grandes volúmenes).

### Modelos de gestión de claves
- **Descentralizado:** cada usuario o departamento gestiona sus claves; autonomía pero riesgos por falta de control.
- **Distribuido:** cada unidad define sus protocolos con cierta coordinación; puede causar inconsistencias.
- **Centralizado:** un sistema único con políticas homogéneas; **recomendado por ISO/IEC 27002** (trazabilidad, control de acceso, cumplimiento). Esencial en fusiones, adquisiciones o reestructuraciones.

**Implementación de un sistema centralizado:** *infraestructura* (servidores seguros); *políticas* (creación, caducidad, acceso, revocación); *procesos* (cómo gestionar claves en cada etapa del ciclo de vida). Hay que integrar los tres.

### Diseño de redes de computadores seguras
- **Segmentación de redes:** divide la red en secciones separadas; con **VLAN** (p. ej., IT, ventas, administración); reduce movimientos laterales y mejora el monitoreo.
- **Firewalls y DMZ:** firewall entre la DMZ y la red interna; limitar el acceso a servicios públicos.
- **Redundancia:** componentes redundantes para la continuidad (conexiones de respaldo entre routers; servidores en clúster con balanceo de carga).

---

## 8.5. Configuración avanzada de sistemas y dispositivos

### Pasos clave para una configuración segura
| Paso | Detalle |
|---|---|
| Aplicación de parches de seguridad | Mantener firmware y SO actualizados; parches automáticos en dispositivos menos críticos; probar en entornos de prueba antes de producción. |
| Restricción de puertos y servicios | Deshabilitar los innecesarios. Ej.: si un servidor no necesita FTP, deshabilitar el puerto 21. |
| Configuración de logs | Registro detallado de actividades; facilita auditorías e identificación de accesos no autorizados. |
| Contraseñas seguras | Políticas robustas; cambiar las predeterminadas en todos los dispositivos. |
| Segmentación física y lógica | Aislar o proteger dispositivos sensibles con control de acceso físico; segmentación lógica del tráfico crítico. |
| Seguridad adicional en dispositivos | Firewalls integrados; cifrado de discos; desactivar funciones no utilizadas. |

### Configuración de dispositivos para la instalación de sistemas informáticos
| Acción | Detalle |
|---|---|
| Validación de hardware | Compatibilidad de componentes con el SO y las aplicaciones; requisitos mínimos de RAM, CPU y almacenamiento; pruebas de funcionamiento. |
| Configuraciones básicas | **BIOS/UEFI:** contraseña de administrador; deshabilitar funciones innecesarias (arranque desde unidades externas); **secure boot**. **Firmware:** aplicar últimas actualizaciones. |
| Seguridad física | Ubicaciones protegidas (cerraduras, gabinetes, racks); SAI. |
| Configuraciones de red iniciales | IP estáticas para dispositivos críticos (servidores, routers); VLAN. |

### Elementos esenciales de la configuración
| Elemento | Detalle |
|---|---|
| **Hardening** | Deshabilitar servicios innecesarios y ajustar configuraciones predeterminadas; desactivar Telnet o FTP si no se usan; limitar el acceso con controles; reglas de firewall. |
| **Cifrado** | Cifrado de discos (**BitLocker** en Windows, **LUKS** en Linux); protocolos seguros como TLS; cifrado de bases de datos. |
| **Monitorización continua** | Nagios (red y sistemas); Splunk (análisis y correlación de registros); Zabbix (infraestructura). |
| **Políticas de seguridad** | Reglas claras sobre uso del sistema y gestión de usuarios; **RBAC**. |
| **Pruebas y validación** | Pruebas de rendimiento y seguridad antes de producción; documentar configuraciones. |

**Beneficios:** reducción de riesgos; optimización del rendimiento; cumplimiento normativo (GDPR, ISO 27001).

---

## A fondo
> **Nota:** en el material, el título «Cartografía aplicada» es un error: el libro recomendado trata de criptografía.

- **Criptografía aplicada** (en el material «Cartografía aplicada»). Schneier, B. (2015). *Applied Cryptography: Protocols, Algorithms, and Source Code in C.* Wiley. Fundamental para los mecanismos de cifrado y la gestión de claves simétricas y asimétricas.
- **Aprende a fondo a bastionar redes y a realizar configuraciones avanzadas.** Tanenbaum, A. S., y Wetherall, D. J. (2011). *Computer Networks.* Pearson. Útil para contextualizar VPN, cifrado en tránsito y bastionado.

---

## Entrenamientos

### Entrenamiento 1: clasificación básica de información
**Planteamiento:** esquema de clasificación para una pequeña empresa.
1. Tres tipos de información: contratos, nóminas, manuales técnicos.
2. Tres niveles: pública, interna, confidencial.
3. Asociación: contratos → confidencial; nóminas → confidencial; manuales técnicos → interna.
4. Controles por nivel: **confidencial** (cifrado, acceso restringido, copias limitadas); **interna** (solo empleados, no compartir por canales externos); **pública** (sin restricciones).

**Solución:** política simple pero funcional con protección proporcional al valor y sensibilidad.

### Entrenamiento 2: activar y gestionar el firewall de Windows
1. Panel de Control > Sistema y seguridad > Firewall de Windows Defender.
2. Verifica que esté activado para redes públicas y privadas.
3. «Permitir una aplicación a través del firewall».
4. Localiza la aplicación (p. ej., navegador) y desmarca las redes públicas.
5. Guarda los cambios.

**Solución:** el firewall sigue activo y la aplicación queda restringida a la red privada.

### Entrenamiento 3: comprobación de fortaleza de una contraseña
1. Abre https://haveibeenpwned.com/Passwords
2. Introduce una contraseña ficticia y observa si ha sido filtrada.
3. Si está comprometida, crea una nueva: mínimo 12 caracteres con mayúsculas, minúsculas, números y símbolos.
4. Vuelve a comprobarla.

**Solución:** entender la importancia de evitar contraseñas débiles o filtradas.

### Entrenamiento 4: generar y usar claves GPG
1. `sudo apt install gnupg`
2. `gpg --full-generate-key` (RSA, 4096 bits)
3. `echo "Texto confidencial" > secreto.txt`
4. Cifrar: `gpg -e -r "tu-nombre" secreto.txt`
5. Descifrar: `gpg -d secreto.txt.gpg`

**Solución:** la criptografía asimétrica protege archivos mediante clave pública (datos en reposo y privacidad personal).

### Entrenamiento 5: autenticación en dos pasos en una cuenta web
1. Accede a tu cuenta de Google.
2. Seguridad > Verificación en dos pasos.
3. Vincula tu teléfono o una app de autenticación (Google Authenticator).
4. Activa el segundo factor.
5. Cierra sesión y vuelve a entrar con contraseña + código temporal.

**Solución:** se refuerza el acceso incluso si la contraseña es robada; autenticación multifactor real, clave frente al phishing.
