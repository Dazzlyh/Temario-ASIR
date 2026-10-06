# Tema 10. Autenticación centralizada
*Administración de Sistemas Operativos*

## Índice
Esquema · 10.1 Introducción y objetivos · 10.2 Autenticación centralizada: definición e importancia · 10.3 Fundamentos de LDAP · 10.4 SAMBA y su rol en la autenticación centralizada · 10.5 Configuración de SAMBA para la autenticación centralizada · 10.6 Comparación entre LDAP y SAMBA · A fondo · Entrenamientos

## Esquema
**Autenticación centralizada: LDAP y SAMBA**

- **Introducción a la autenticación centralizada**
  - Importancia en la gestión de TI: control riguroso y coherente de las credenciales.
  - Beneficios: simplificación del acceso mediante Single Sign-On (SSO); una sola base de datos para múltiples sistemas.
- **SAMBA y su rol en la autenticación centralizada**: LDAP como *backend*; uso de LDAP para autenticación de usuarios; unificación de credenciales y simplificación de la gestión.
- **Configuración de SAMBA para la autenticación centralizada**: configuración de SAMBA con LDAP; archivo `smb.conf`; usuarios y grupos sincronizados entre SAMBA y LDAP.

---

## 10.1. Introducción y objetivos
La gestión eficiente de identidades y autenticación es crucial para la seguridad y productividad organizacional. La autenticación centralizada gestiona las credenciales de forma segura y eficiente. Este tema se centra en servidores **LDAP** y **SAMBA**.

Objetivos:
- **Definir autenticación centralizada y su importancia en la gestión de TI.**
- **Explicar los fundamentos de LDAP** y su funcionamiento en la autenticación centralizada.
- **Describir la configuración y gestión de un servidor LDAP** para la autenticación centralizada.
- **Analizar el papel de SAMBA** en entornos mixtos Windows y Unix/Linux y su integración con LDAP.
- **Demostrar la configuración de SAMBA** como controlador de dominio con LDAP como *backend*.
- **Comparar LDAP y SAMBA** en rendimiento, seguridad y facilidad de gestión.
- **Explorar casos de uso y mejores prácticas** de la autenticación centralizada con LDAP y SAMBA.

---

## 10.2. Autenticación centralizada: definición e importancia
Permite administrar credenciales de usuario y permisos de acceso desde un **único punto centralizado**. Elimina la necesidad de múltiples bases de datos de usuarios y contraseñas en distintas aplicaciones, sustituyéndolas por una única base de datos central. Simplifica la gestión de usuarios y contraseñas, y mejora la seguridad y la eficiencia operativa.

**Seguridad.** Al centralizar el control de acceso se facilita implantar políticas coherentes y robustas (contraseñas fuertes, expiración regular) de forma uniforme en todos los sistemas. Al reducir el número de bases de datos de contraseñas se minimiza la superficie de ataque. Sin autenticación centralizada, los usuarios tienden a reutilizar la misma contraseña en múltiples sistemas, lo que aumenta el riesgo.

*Ejemplo — universidades:* estudiantes y personal acceden a correo, portales educativos, bibliotecas digitales y sistemas de gestión académica. Con **SSO** (*single sign-on*, inicio de sesión único) acceden a todo con una sola autenticación, lo que mejora la seguridad y simplifica la experiencia.

**Reducción de la sobrecarga administrativa.** Los administradores crean, modifican y eliminan cuentas en un solo lugar y los cambios se reflejan en todos los sistemas conectados. Especialmente beneficioso en organizaciones grandes.

*Ejemplo — multinacionales:* sin autenticación centralizada, TI tendría que gestionar cada cuenta individualmente en cada sistema; con una solución centralizada, crear una cuenta o cambiar una contraseña se hace una sola vez.

**Auditoría y cumplimiento normativo.** Con todas las actividades de autenticación gestionadas y registradas desde un único punto, la auditoría de accesos y los informes de cumplimiento se simplifican; importante en sectores regulados (financiero, sanitario).

*Ejemplo — instituciones financieras* (con normativas estrictas en EE. UU.): pueden monitorizar y registrar todos los accesos de los empleados desde un único sistema.

**En resumen:** mejora la seguridad, reduce la sobrecarga administrativa y facilita la auditoría y el cumplimiento normativo.

---

## 10.3. Fundamentos de LDAP
Repaso de la unidad anterior.

**LDAP** es un protocolo estándar de red para acceder y gestionar servicios de directorio distribuidos (bases de datos especializadas que almacenan información estructurada sobre usuarios, grupos, dispositivos y otros objetos). Su principal ventaja es organizar y acceder a grandes cantidades de datos de forma rápida y eficiente.

Modelo **cliente-servidor**: los clientes envían solicitudes de búsqueda y modificación al servidor, que responde con resultados o confirmaciones. Múltiples aplicaciones pueden autenticarse y acceder a los datos del directorio con credenciales y políticas comunes.

**Estructura jerárquica**, similar a un árbol: las entradas (usuario, grupo, dispositivo) se organizan bajo una raíz común y cada una tiene un identificador único llamado **distinguished name (DN)**, que actúa como ruta absoluta.

Ejemplo de DN: `uid=jdoe,ou=People,dc=example,dc=com`
- `uid=jdoe`: identifica al usuario.
- `ou=People`: unidad organizativa que agrupa a los usuarios.
- `dc=example,dc=com`: dominio de la organización.

Cada entrada es una colección de **atributos** (nombre y uno o más valores): `cn` (nombre común), `sn` (apellido), `mail`, `userPassword`… Los objetos se definen mediante **esquemas**, que determinan qué atributos son obligatorios y cuáles opcionales.

**Autenticación.** Se validan las credenciales contra los registros del servidor: el cliente envía una solicitud de enlace (*bind*) con el DN y la contraseña; el servidor responde con éxito o error. LDAP también se usa para **autorizar** el acceso a recursos (consultando permisos y roles).

**Configuración y gestión de un servidor LDAP:**
1. Instalar una implementación (como OpenLDAP).
2. Definir el esquema del directorio (tipos de objetos y atributos; unidades organizativas).
3. Configurar los permisos de acceso mediante políticas de control de acceso.
4. Gestionar usuarios y grupos (crear/modificar/eliminar entradas), mediante herramientas cliente o archivos **LDIF** (*LDAP Data Interchange Format*).

**Integración con aplicaciones y servicios.** Servidores de correo, aplicaciones web y servicios de red pueden autenticar usuarios contra LDAP, con gestión unificada de credenciales y permisos.

**Resumen:** su modelo jerárquico, su capacidad para manejar grandes datos y su integración con múltiples servicios lo hacen una herramienta poderosa de gestión de identidades.

---

## 10.4. SAMBA y su rol en la autenticación centralizada
**SAMBA** es una implementación libre del protocolo **SMB/CIFS** que permite la interoperabilidad entre Unix/Linux y Windows. Puede actuar como **controlador de dominio**, proporcionando autenticación centralizada y gestión de recursos compartidos. Permite compartir archivos e impresoras entre ambos mundos y puede integrarse con servicios de directorio como LDAP.

### Integración con LDAP
SAMBA puede usar LDAP como *backend* de autenticación. Beneficios:
- **Unificación de credenciales**: mismas credenciales para SAMBA y otros servicios autenticados por LDAP.
- **Simplificación de la gestión**: administración centralizada de usuarios y permisos.
- **Mejora de la seguridad**: políticas uniformes (contraseñas, control de acceso, auditorías).

### Configuración de SAMBA con LDAP
Implica definir el servidor LDAP como fuente de autenticación en `smb.conf` (normalmente `/etc/samba/smb.conf`) y sincronizar las bases de datos de usuarios.

```ini
[global]
    workgroup = WORKGROUP
    security = user
    passdb backend = ldapsam:ldap://ldap.example.com
    ldap admin dn = cn=admin,dc=example,dc=com
    ldap suffix = dc=example,dc=com
    ldap user suffix = ou=People
    ldap group suffix = ou=Groups
    ldap machine suffix = ou=Computers
    ldap password sync = yes
    idmap config * : backend = ldap
    idmap config * : range = 10000-20000
    ldap idmap suffix = ou=Idmap
    winbind use default domain = yes
```
- `workgroup`: nombre del grupo de trabajo para la red.
- `security`: modo de seguridad; `user` indica que SAMBA gestionará la autenticación.
- `passdb backend`: SAMBA usará LDAP como *backend* para la base de datos de contraseñas.
- `ldap admin dn`: DN del administrador LDAP.
- `ldap suffix`: sufijo base para todas las búsquedas LDAP.
- `ldap user suffix` / `ldap group suffix` / `ldap machine suffix`: sufijos para entradas de usuario, grupo y máquina.
- `ldap password sync`: sincroniza las contraseñas entre SAMBA y LDAP.
- `idmap config`: configura el *backend* de mapeo de identidades y el rango de UID/GID.

Es necesario sincronizar las bases de datos de usuarios entre SAMBA y LDAP (con herramientas y scripts).

---

## 10.5. Configuración de SAMBA para la autenticación centralizada
Instalar SAMBA (Ubuntu):
```bash
sudo apt-get update
sudo apt-get install samba
```
SAMBA puede actuar como **controlador de dominio**, permitiendo autenticación centralizada para clientes Windows (políticas de grupo y gestión de recursos). Ejemplo en `smb.conf`:

```ini
[global]
    workgroup = MYDOMAIN
    realm = MYDOMAIN.LOCAL
    netbios name = MYDC
    server role = active directory domain controller
    dns forwarder = 8.8.8.8
    idmap_ldb:use rfc2307 = yes

[netlogon]
    path = /var/lib/samba/sysvol/mydomain.local/scripts
    read only = no

[sysvol]
    path = /var/lib/samba/sysvol
    read only = no
```

La integración con LDAP requiere configurar SAMBA para usar el servidor LDAP como *backend* de autenticación. Ejemplo de configuración completa:

```ini
[global]
    workgroup = MYDOMAIN
    security = user
    passdb backend = ldapsam:ldap://ldap.example.com
    ldap admin dn = cn=admin,dc=example,dc=com
    ldap suffix = dc=example,dc=com
    ldap user suffix = ou=People
    ldap group suffix = ou=Groups
    ldap machine suffix = ou=Computers
    ldap password sync = yes
    idmap config * : backend = ldap
    idmap config * : range = 10000-20000
    ldap idmap suffix = ou=Idmap
    winbind use default domain = yes

[netlogon]
    path = /var/lib/samba/sysvol/mydomain.local/scripts
    read only = no

[sysvol]
    path = /var/lib/samba/sysvol
    read only = no
```
- Los **sufijos LDAP** definen las rutas del directorio donde se almacenan usuarios, grupos y máquinas.
- `ldap password sync = yes`: cualquier cambio de contraseña en SAMBA se refleja automáticamente en LDAP.
- `idmap config * : backend = ldap`: SAMBA usa LDAP para mapear identidades de usuarios y grupos.

**Pruebas tras configurar:**
- *Prueba de autenticación*: los usuarios pueden autenticarse con sus credenciales LDAP.
- *Prueba de acceso a recursos*: pueden acceder a los recursos compartidos según sus permisos definidos en LDAP.
- *Monitorización de logs*: revisar logs de SAMBA y LDAP.

---

## 10.6. Comparación entre LDAP y SAMBA
**Rendimiento.** LDAP es eficiente en la gestión y búsqueda en directorios grandes gracias a su estructura jerárquica y su diseño optimizado para lectura y búsqueda. SAMBA integrado con LDAP se beneficia de esa eficiencia; su rendimiento también depende de la carga de la red y de la configuración del sistema.

**Seguridad.** LDAP permite cifrado en tránsito mediante TLS/SSL y políticas de contraseñas detalladas (complejidad, expiración). SAMBA también puede cifrar los datos compartidos y sincronizar políticas con LDAP. Su integración permite políticas uniformes en todos los sistemas.

**Facilidad de gestión.** La configuración inicial de LDAP puede ser compleja (esquemas y permisos), pero luego es eficiente y flexible; puede simplificarse con herramientas y scripts. SAMBA puede requerir configuración adicional al integrarse con LDAP, pero ofrece una potente gestión de recursos compartidos y autenticación en entornos Windows; mejora con interfaces gráficas y herramientas de administración.

**Grandes volúmenes de datos.** LDAP está optimizado para ello (estructura jerárquica e indexación); SAMBA con LDAP como *backend* aprovecha esa capacidad.

**Solución de problemas.** Puede ser compleja por la interacción entre múltiples sistemas; se resuelve con buena documentación, herramientas de diagnóstico y administradores bien capacitados.

**Resumen:** LDAP es altamente eficiente y seguro para la gestión de directorios y autenticación; SAMBA aporta interoperabilidad y gestión de recursos compartidos en entornos mixtos. Su integración proporciona una solución robusta, segura y eficiente para la autenticación centralizada.

---

## A fondo
- **Explicación servidor de archivos SAMBA para compartir archivos entre Windows y Linux.** Edge Seguridad Informática y SysAdmin. (2021, marzo 15). [Vídeo]. https://www.youtube.com/watch?v=SQPWHlDdYgE
- **Cómo instalar un servidor de LDAP con SAMBA.** JohnTi TF. (2021, febrero 5). *Servidor OpenLDAP con Samba en Ubuntu 20.04* [Vídeo]. https://www.youtube.com/watch?v=b7eLsmip0UM

---

## Entrenamientos

### Entrenamiento 1 — Instalar y configurar OpenLDAP en Ubuntu
Pasos: actualizar el sistema, instalar OpenLDAP, configurar la contraseña del administrador, verificar la instalación.
```bash
# 1. Actualiza el sistema
sudo apt-get update
# 2. Instala OpenLDAP y las utilidades LDAP
sudo apt-get install slapd ldap-utils
# 3. Configura la contraseña del administrador
sudo dpkg-reconfigure slapd
# Durante la configuración:
# - Omite la configuración de DNS
# - Establece el nombre de dominio (por ejemplo, example.com)
# - Configura la organización (por ejemplo, Example Inc.)
# - Establece la contraseña del administrador LDAP
# - Acepta las configuraciones predeterminadas restantes
# 4. Verifica la instalación
sudo systemctl status slapd
# La salida debe indicar que el servicio slapd está activo y funcionando.
```
> Nota: el material dice «Omite la configuración de DNS», pero en el asistente `dpkg-reconfigure slapd` la pregunta «¿Omitir configuración del servidor OpenLDAP?» debe responderse **No** (como indica el Tema 9); lo que se introduce es el nombre de dominio DNS.

### Entrenamiento 2 — Crear un usuario con LDIF
`new_user.ldif`:
```
dn: uid=jdoe,ou=People,dc=example,dc=com
objectClass: inetOrgPerson
cn: John Doe
sn: Doe
uid: jdoe
mail: jdoe@example.com
userPassword: {SSHA}hH6Z6pwpBp7g5r0Q8j9HkN3jZ3
```
```bash
sudo ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f new_user.ldif
# Se pedirá la contraseña del administrador LDAP configurada anteriormente.
```
> Nota: este LDIF presupone que existe la OU `ou=People`; hay que crearla antes (si no, `ldapadd` fallará).

### Entrenamiento 3 — Buscar el usuario en el directorio
```bash
ldapsearch -x -LLL -b "dc=example,dc=com" "(uid=jdoe)"
```
La salida debe mostrar los detalles del usuario `jdoe`.

### Entrenamiento 4 — Configurar SAMBA con LDAP como *backend*
Pasos: instalar SAMBA; editar `smb.conf`; reiniciar el servicio.
```bash
sudo apt-get install samba
```
```ini
[global]
 workgroup = WORKGROUP
 security = user
 passdb backend = ldapsam:ldap://127.0.0.1
 ldap admin dn = cn=admin,dc=example,dc=com
 ldap suffix = dc=example,dc=com
 ldap user suffix = ou=People
 ldap group suffix = ou=Groups
 ldap machine suffix = ou=Computers
 ldap password sync = yes
 idmap config * : backend = ldap
 idmap config * : range = 10000-20000
 ldap idmap suffix = ou=Idmap
 winbind use default domain = yes
```
```bash
sudo systemctl restart smbd
sudo systemctl restart nmbd
```

### Entrenamiento 5 — Verificar la autenticación de un usuario contra LDAP
Usar un cliente LDAP para autenticar al usuario creado en el Entrenamiento 2:
```bash
ldapwhoami -x -D "uid=jdoe,ou=People,dc=example,dc=com" -W
```
Introducir la contraseña de `jdoe` cuando se pida. Respuesta esperada:
```
dn:uid=jdoe,ou=People,dc=example,dc=com
```
Indica que la autenticación fue exitosa.
