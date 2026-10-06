# Tema 3. Seguridad lógica
*Ciberseguridad*

## Índice
Esquema · 3.1 Introducción y objetivos · 3.2 Criptografía y control de accesos · 3.3 Políticas de contraseñas y almacenamiento · 3.4 Gestión de copias de seguridad e imágenes de respaldo · 3.5 Medios de almacenamiento seguro · 3.6 Referencias bibliográficas · A fondo · Entrenamientos

## Esquema
**Seguridad lógica**
- **Criptografía:** confidencialidad, integridad, autenticidad y no repudio. Algoritmos clave: AES, RSA, SHA-256. Tipos: hashing, simétrica, asimétrica.
- **Control de acceso:** listas de control de acceso (ACL); políticas de contraseñas.
- **Almacenamiento:** *almacenamiento seguro* (cifrado de datos, control de acceso restringido, auditorías y monitoreo) y *copias de seguridad y recuperación* (métodos: completo, incremental, diferencial; estrategia **3-2-1**: 3 copias, 2 medios, 1 ubicación externa; automatización y pruebas periódicas).

---

## 3.1. Introducción y objetivos
La seguridad lógica es un pilar para proteger los sistemas de información y los datos digitales: evitar accesos no autorizados, garantizar la integridad y reforzar la confidencialidad. Incluye criptografía, listas de control de acceso (ACL), gestión de contraseñas, política de almacenamiento seguro y copias de seguridad.

Objetivos:
- Comprender la importancia de la seguridad lógica.
- Explicar los fundamentos de la criptografía (simétrica, asimétrica y hashing) y sus aplicaciones.
- Identificar la función de las ACL.
- Analizar políticas de contraseñas seguras (incluida la autenticación multifactor).
- Comprender la importancia de copias de seguridad e imágenes de respaldo.
- Evaluar la seguridad de los medios de almacenamiento.
- Desarrollar buenas prácticas en la administración de la seguridad lógica.

---

## 3.2. Criptografía y control de accesos
La **criptografía** garantiza la seguridad de las comunicaciones frente a interceptores no autorizados: transforma un mensaje original (**texto plano**) en un formato ininteligible (**texto cifrado**) mediante algoritmos; solo se revierte con una **clave**.

Cuatro objetivos fundamentales:
- **Confidencialidad:** solo el receptor previsto accede al contenido.
- **No repudio:** el emisor no puede retractarse del mensaje.
- **Integridad:** el mensaje no ha sido alterado.
- **Autenticidad:** emisor y receptor validan sus identidades.

### Hashing
Transforma un mensaje de longitud variable en una secuencia de tamaño fijo. **No oculta información: verifica integridad.**
- **Verificación de descargas:** el proveedor publica el hash; el usuario calcula el suyo y compara.
- **Detección de modificaciones:** si no coinciden, la descarga no se completó bien o el archivo fue alterado.
- **Funcionamiento:** unidireccional y muy sensible a cambios: una mínima alteración produce un hash completamente distinto.
- **Evolución:** MD5 y SHA-1 se usaban ampliamente; por vulnerabilidades se ha migrado a **SHA-256**.
- **Ventajas:** garantiza integridad de mensajes y archivos y permite verificar autenticidad. **Limitaciones:** no cifra; su función es verificar, no proteger el contenido. Se recomienda combinarlo con otras técnicas.

### Criptografía simétrica
Una **única clave secreta** para cifrar y descifrar, conocida por emisor y receptor. Es de los métodos más antiguos y sencillos.
- **Ventajas:** facilidad de uso y velocidad (menor complejidad matemática).
- **Desventajas:** hay que transmitir la clave de forma segura. Si un tercero la intercepta, accede a todos los datos cifrados (paradoja: para enviar mensajes cifrados primero hay que enviar la clave de forma no segura).
- **Uso:** principalmente datos almacenados localmente (cifrado de bases de datos en servidores, protección en dispositivos móviles), donde no hay problema de intercambio de claves.

### Criptografía asimétrica
O de **clave pública**: usa dos claves interdependientes, **pública** y **privada**. La pública se comparte y cifra mensajes; solo la privada, secreta, los descifra.
- **Ventajas:** confidencialidad sin riesgo de distribuir claves secretas; **firmas digitales** (autenticidad y no repudio).
- **Desventajas:** cifrado/descifrado considerablemente más lento; su seguridad depende de la dificultad de ciertos problemas matemáticos (factorización de números grandes), por lo que avances en matemáticas o computación cuántica podrían comprometerla.
- **Aplicaciones:** infraestructura de clave pública (**PKI**), HTTPS, correo seguro, firmas digitales, autenticación de software.
- **Sistemas híbridos:** la asimétrica intercambia una **clave de sesión simétrica** que cifra el grueso de los datos.

### Algoritmos de intercambio de claves
Permiten a dos partes establecer una clave compartida de forma segura a través de un canal inseguro. El más conocido: **Diffie-Hellman**. Explicación simplificada con colores: acuerdan un color base público; cada parte elige un color secreto; mezclan su secreto con el base; intercambian las mezclas; cada una mezcla lo recibido con su propio secreto; ambas obtienen el mismo color, la clave compartida, sin que un tercero pueda deducirla observando los intercambios.
- **Aplicaciones:** HTTPS, SSH, mensajería cifrada.
- **Consideraciones:** vulnerables a ataques de «hombre en el medio»; conviene usarlos con firmas digitales.
- **Futuro:** nuevos algoritmos resistentes a ataques cuánticos.

### Tipos de funciones criptográficas
- **Autenticación:** establece la identidad de un usuario o sistema remoto. Ej.: certificados SSL de servidores web. La identidad se basa en la clave criptográfica del usuario. Aplicación: **PGP** (cifrado y autenticación para archivos y correo).
- **No repudio:** crucial en finanzas y comercio electrónico: el usuario no puede negar una transacción.
- **Confidencialidad:** mantener la información privada mediante cifrado.
- **Integridad:** datos no vistos ni alterados en transmisión o almacenamiento; hashes criptográficos como suma de verificación segura.

### Listas de control de acceso (ACL)
Definen y regulan qué usuarios, sistemas o entidades pueden interactuar con recursos específicos.

**Componentes:**
- **Sujetos:** usuarios, aplicaciones o sistemas que intentan acceder.
- **Objetos:** archivos, carpetas, bases de datos, impresoras, aplicaciones.
- **Permisos:** lectura, escritura, ejecución, control total.

**Tipos:**
| Modelo | Descripción | Ventajas | Desventajas |
|---|---|---|---|
| **DAC** (discrecional) | El propietario del recurso decide quién accede y con qué permisos. | Fácil de implementar y administrar; flexible. | Menos seguro (permisos inadvertidos); difícil de escalar con muchos recursos y usuarios. |
| **RBAC** (basado en roles) | Permisos asignados a roles; los usuarios acceden según su rol. Ej.: "Administrador" lectura/escritura/ejecución; "Usuario" solo lectura. | Escalable; simplifica la gestión de permisos. | Menos flexible en entornos dinámicos donde los roles cambian con frecuencia. |
| **ABAC** (basado en atributos) | Acceso según atributos del sujeto, objeto y contexto. Ej.: "Departamento: Finanzas" accede a recursos "Acceso: Finanzas". | Gran flexibilidad y granularidad; políticas complejas por condiciones. | Configuración y mantenimiento más complejos; más exigente en procesamiento. |

**Implementación:**
- *Sistemas operativos:* Windows, Linux, macOS. En Linux: `chmod` (permisos básicos) y `setfacl` (ACL avanzadas).
- *Redes:* routers y switches. Ej.: permitir tráfico HTTP y bloquear todo lo demás desde una IP.
- *Bases de datos:* acceso a tablas, vistas y procedimientos. Ej.: «solo lectura» a un analista y «control total» a un desarrollador.
- *Nube:* AWS, Azure, Google Cloud. Ej.: ACL en S3 para buckets y objetos.

**Mejores prácticas:** principio de mínimo privilegio; auditoría regular; registro de accesos; capacitación.

---

## 3.3. Políticas de contraseñas y almacenamiento
Las contraseñas son la **primera línea de defensa**.

### Buenas prácticas
| Práctica | Detalle |
|---|---|
| Contraseñas largas y complejas | Mínimo **12 caracteres** con mayúsculas, minúsculas, números y símbolos. Ej.: en lugar de «WiktorN123», algo como «4J*kP@z!LmX8». |
| Periodicidad en el cambio | Renovar periódicamente, preferentemente cada **90 días**; evitar reutilizar antiguas o variantes fáciles. |
| Autenticación multifactorial (MFA) | Segundo factor: códigos temporales (Google Authenticator) o biometría. |
| Evitar contraseñas comunes | No «123456», «qwerty», «password»; herramientas que identifiquen contraseñas comprometidas en bases filtradas. |

### Herramientas de gestión
- **Administradores de contraseñas:** LastPass, Bitwarden, 1Password; generan, almacenan y gestionan contraseñas seguras, con almacenamiento cifrado.
- **Reglas automatizadas de expiración y rotación**, con notificaciones previas al vencimiento.
- **Integración con Single Sign-On (SSO):** autenticarse una vez para múltiples sistemas.

### Riesgos asociados a contraseñas mal administradas
| Riesgo | Detalle |
|---|---|
| Ataques de fuerza bruta | Probar todas las combinaciones; contraseñas extensas y complejas aumentan el tiempo necesario. |
| Robo de credenciales | Phishing o brechas; contraseñas únicas por servicio evitan la «propagación del compromiso». |
| Ingeniería social | Persuadir a usuarios para que revelen contraseñas; capacitar en detección de phishing. |

### Ejemplos de políticas
- **Empresa promedio:** al menos 12 caracteres; renovación cada 90 días; bloqueo tras 5 intentos fallidos.
- **Alta seguridad:** MFA obligatoria; historial de al menos 10 contraseñas anteriores; validación contra bases de contraseñas comprometidas.

### Mejores prácticas organizacionales
Capacitación regular; auditorías periódicas; políticas uniformes adaptadas a cada departamento.

### Políticas de almacenamiento
**Objetivos:** garantizar integridad y disponibilidad; acceso solo a personas autorizadas.
**Estrategias:** clasificación de datos (público, interno, confidencial, secreto); cifrado de almacenamiento; control de acceso robusto; retención de datos según necesidades legales y operativas; auditorías periódicas.

---

## 3.4. Gestión de copias de seguridad e imágenes de respaldo
**Tipos de respaldo:**
- **Completo:** copia de todos los datos.
- **Incremental:** cambios desde la última copia.
- **Diferencial:** cambios desde la última copia **completa**.

**Buenas prácticas:**
- Regla **3-2-1**: 3 copias en 2 formatos diferentes y 1 fuera del sitio.
- Pruebas periódicas de restauración.
- Automatizar el proceso.
- Almacenar en ubicaciones físicamente separadas.

**Imágenes de respaldo:** instantáneas completas del estado de un sistema en un momento. Ventajas: restauración más rápida; incluyen configuraciones del sistema, aplicaciones y datos. Estrategias: imágenes periódicas de sistemas críticos y almacenamiento en sistemas redundantes. Integración: software como **Veeam** o **Acronis**; compatibilidad con entornos virtualizados y en la nube.

---

## 3.5. Medios de almacenamiento seguro
- **HDD y SSD:** los HDD son económicos y de mayor capacidad; los SSD, más rápidos y confiables.
- **NAS (almacenamiento en red):** para compartir datos en entornos corporativos, con acceso remoto y redundancia **RAID**.
- **Nube:** flexibilidad y escalabilidad, acceso global.

**Consideraciones de seguridad:** cifrado **AES-256** o superior; eliminación segura (borrado seguro); redundancia y replicación; gestores de almacenamiento como NetApp o Dell EMC.

---

## 3.6. Referencias bibliográficas
- Stallings, W. (2018). *Criptografía y seguridad en redes.* Pearson.
- INCIBE. *Guías prácticas en seguridad lógica.*
- Ciberseguridad. (n.d.). *¿Qué es la criptografía?* https://ciberseguridad.com/guias/prevencion-proteccion/criptografia/
- Caballero, A. (2020). *Gestión segura de datos y políticas lógicas.* Wolters Kluwer.

---

## A fondo
> **Nota:** como en el Tema 2, el material original incluye aquí recursos *placeholder* que no corresponden al tema: «Pobreza y migraciones» (Castro, 2010) y el vídeo «Jaques Derrida: la huella» (Canal22, 2017), con texto de plantilla.

---

## Entrenamientos

### Entrenamiento 1: cifrado de datos con OpenSSL
**Planteamiento:** cifrar información sensible en un servidor con criptografía simétrica.
1. Instalar OpenSSL: `sudo apt install openssl`.
2. Algoritmo: AES-256-CBC.
3. Cifrar: `openssl enc -aes-256-cbc -salt -in datos_sensibles.txt -out datos_cifrados.enc -k clave_secreta`
4. Verificar que el archivo original ya no es accesible y que el cifrado se realizó.
5. Descifrar: `openssl enc -aes-256-cbc -d -in datos_cifrados.enc -out datos_descifrados.txt -k clave_secreta`
6. Comparar: `diff datos_sensibles.txt datos_descifrados.txt`

**Solución:** el archivo cifrado solo puede leerse con la clave correcta.

### Entrenamiento 2: ACL en Linux
**Planteamiento:** restringir un archivo crítico para que solo un usuario específico pueda leerlo.
1. `touch archivo_critico.txt`
2. `chmod 600 archivo_critico.txt`
3. `setfacl -m u:usuario_permitido:r archivo_critico.txt`
4. `getfacl archivo_critico.txt`
5. Probar con el usuario permitido y con otro no autorizado.

**Solución:** solo el usuario especificado puede leer; los demás reciben acceso denegado.

### Entrenamiento 3: políticas de contraseñas seguras en Windows Server
1. Ejecutar `gpedit.msc`.
2. Ir a *Configuración del equipo > Configuración de Windows > Configuración de seguridad > Directivas de cuenta > Directiva de contraseñas*.
3. Configurar: longitud mínima 12; complejidad habilitada; historial de al menos 10 contraseñas; duración máxima 90 días.
4. Aplicar y verificar con las nuevas cuentas.
5. Probar con contraseñas inseguras y comprobar que se rechazan.

**Solución:** las cuentas cumplen la política establecida.

### Entrenamiento 4: copias de seguridad automáticas en Linux con rsync
1. `sudo apt install rsync`
2. `mkdir -p /backup/servidor`
3. `rsync -av --delete /home/usuario/ /backup/servidor/`
4. Automatizar con cron: `crontab -e`
5. Añadir: `0 2 * * * rsync -av --delete /home/usuario/ /backup/servidor/` (diario a las 2 AM).
6. Probar la restauración de un archivo borrado copiándolo desde `/backup/servidor/`.

**Solución:** copias diarias automáticas y recuperación de archivos eliminados.

### Entrenamiento 5: cifrado de unidades con BitLocker
1. Conectar la unidad y abrir el Explorador de archivos.
2. Clic derecho → «Activar BitLocker».
3. Elegir método de desbloqueo: contraseña, tarjeta inteligente o cuenta de Microsoft.
4. Configurar la recuperación: guardar la clave en cuenta de Microsoft, archivo o imprimirla.
5. Elegir modo de cifrado: compatible (dispositivos antiguos) o nuevo (más seguridad).
6. Iniciar el cifrado y esperar.
7. Verificar que se requiere autenticación.

**Solución:** el disco pide la clave de acceso cada vez que se conecta.
