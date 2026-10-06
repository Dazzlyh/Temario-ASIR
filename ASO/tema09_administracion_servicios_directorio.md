# Tema 9. Administración de servicios de directorio
*Administración de Sistemas Operativos*

## Índice
Esquema · 9.1 Introducción y objetivos · 9.2 Servicios de directorio LDAP · 9.3 Instalación, configuración y personalización del servicio de directorio. OpenLDAP · 9.4 Directorios. Administración y operaciones. Dominios · 9.5 Referencias bibliográficas · A fondo · Entrenamientos

## Esquema
Los servicios de directorio ofrecen un método organizado y centralizado para gestionar la información relacionada con usuarios, dispositivos, recursos y políticas de seguridad.

- **Servicios de directorio LDAP**
  - Modelo jerárquico: organiza los datos en una estructura de árbol jerárquico.
  - Protocolos de red: utiliza TCP/IP.
  - Interoperabilidad: compatible con diversos sistemas operativos y aplicaciones.
  - Escalabilidad: desde pequeños grupos de usuarios hasta grandes organizaciones.
  - Seguridad: mecanismos sólidos de autenticación y autorización.
- **Instalación, configuración y personalización de OpenLDAP**
  - Instalación: `sudo apt update`, `sudo apt upgrade`, `sudo apt install slapd ldap-utils`.
  - Configuración del dominio: `sudo dpkg-reconfigure slapd`.
  - Personalización: crear archivos `.ldif`; añadir a LDAP con `ldapadd`.
- **Directorios. Operaciones**: `ldapadd` (agregar entradas), `ldapdelete` (eliminar), `ldapsearch` (buscar y recuperar), `ldapmodify` (modificar).

---

## 9.1. Introducción y objetivos
Los servicios de directorio son esenciales en la gestión de sistemas informáticos: una forma organizada y centralizada de manejar información sobre usuarios, dispositivos, recursos y políticas de seguridad; permiten regular el acceso a los recursos en una red.

Objetivos:
- Comprensión básica de los servicios de directorio y su importancia.
- Familiarizarse con el protocolo **LDAP**.
- Realizar la instalación, configuración y personalización de un servicio de directorio con **OpenLDAP**.
- Gestionar y operar directorios y dominios (usuarios, grupos y políticas).
- Aplicar prácticas recomendadas de seguridad y garantizar la integridad de la información.

---

## 9.2. Servicios de directorio LDAP
**Lightweight Directory Access Protocol (LDAP)** es un conjunto de protocolos de la capa de aplicación, multiplataforma y de código abierto, usado para acceder y mantener servicios de directorio distribuidos en una red. Proporciona un método eficiente y estructurado para almacenar y recuperar datos; es muy usado por su compatibilidad y su capacidad para manejar grandes volúmenes de información.

Un **servicio de directorio** es una base de datos centralizada que almacena información sobre usuarios, grupos, dispositivos y otros recursos de red.

Funciona con un modelo **cliente-servidor**: el servidor LDAP almacena la información y el cliente (aplicación o servicio) se conecta para consultar o modificar.

Características clave:
- **Modelo jerárquico**: estructura de árbol, similar a un sistema de archivos; cada nodo es una entrada (usuario, grupo) con atributos.
- **Protocolos de red**: TCP/IP.
- **Interoperabilidad**: diversos sistemas operativos y aplicaciones.
- **Escalabilidad**: desde pequeños grupos hasta millones de entradas.
- **Seguridad**: autenticación y autorización sólidas, y cifrado de datos durante la transmisión.

Desventajas:
- **Complejidad**: puede ser complejo de configurar y administrar.
- **Rendimiento**: en entornos con gran volumen de escrituras puede ser menos eficiente que otras bases de datos.

---

## 9.3. Instalación, configuración y personalización del servicio de directorio. OpenLDAP
LDAP permite interactuar con un directorio jerárquico eficiente en la recuperación y consulta de datos (similar a una base de datos, pero más rápido en búsquedas y lecturas). **OpenLDAP** es una solución reconocida y adaptable, software libre y de código abierto.

OpenLDAP permite: verificar la identidad de los usuarios en sistemas distribuidos por una red; consolidar la administración de usuarios y grupos; realizar búsquedas y recuperar datos eficazmente gracias a su estructura jerárquica.

### Instalación (Ubuntu Server)
```bash
sudo apt update
sudo apt upgrade
sudo apt install slapd ldap-utils
```
Durante la instalación se solicita la contraseña del administrador de LDAP (rootDN).

Después: **definir el FQDN** del servidor; **personalizar la configuración** (ajustar `slapd.conf` si fuera necesario); **incorporar datos** con archivos LDIF (organizaciones, usuarios y grupos).

### Configuración
```bash
sudo dpkg-reconfigure slapd
```
Pasos del asistente:
1. **No** omitir la configuración del servidor OpenLDAP (se creará una base de datos y configuración inicial).
2. Indicar el **dominio** DNS (en el ejemplo, `midominio.com`).
3. **Nombre de la organización** (por defecto, el mismo que el dominio).
4. **Contraseña del administrador** de LDAP y su confirmación.
5. Borrar la base de datos anterior (la genera por defecto la instalación de slapd y no se necesita).
6. Mover los ficheros de la base de datos antigua.

Si todo va bien, el mensaje final indica «Creating LDAP directory… done».

Verificación con `slapcat`:
```bash
sudo slapcat
```
Muestra, entre otros, `dn: dc=midominio,dc=com` (organización) y `dn: cn=admin,dc=midominio,dc=com` (administrador de LDAP, con `objectClass: simpleSecurityObject` y `organizationalRole`).

### Personalización del servicio
Se crea una jerarquía en forma de árbol que representa la estructura de la organización. Ejemplo de árbol: `dc=com` / `dc=es` / `dc=net`; bajo `dc=es` está la entidad `dc=somebooks`; bajo ella, unidades organizativas `ou=medio` y `ou=superior`; y usuarios, p. ej. `uid=jlopez` (Ruiz, 2015).

Se elaboran **archivos LDIF** con la información necesaria antes de integrarla en el servidor, creados en el directorio *home*. Aunque es posible un único LDIF con unidad organizativa, grupos y usuarios, **incrementa el riesgo de errores**, por lo que se usa **un archivo por elemento**. **El orden es muy importante**: primero la unidad organizativa, luego el grupo y por último los usuarios.

**1) Unidad organizativa (OU)** — `nano ou.ldif`:
```
dn: ou=asir,dc=midominio,dc=com
objectClass: top
objectClass: organizationalUnit
ou: asir
```
- `dn`: la unidad organizativa se llama `asir`.
- `objectClass: top`: cuelga directamente de la raíz.
- `objectClass: organizationalUnit`: es una unidad organizativa.
- `ou`: nombre de la unidad organizativa.

Los atributos **objectClass** definen las características y propiedades del objeto. Opciones: `top` (clase superior de todas las entradas), `posixAccount` (cuenta POSIX: uidNumber, gidNumber, homeDirectory, loginShell), `inetOrgPerson` (elemento del esquema «Internet Organization»), `person` (persona genérica).

Importar con `ldapadd`:
```bash
sudo ldapadd -x -D cn=admin,dc=midominio,dc=com -W -f ou.ldif
```
Pide la contraseña del administrador LDAP y carga la información.

**2) Grupo** — `nano grupos.ldif`:
```
dn: cn=segundo,ou=asir,dc=midominio,dc=com
objectClass: top
objectClass: posixGroup
gidNumber: 2000
cn: segundo
```
`segundo` es el nombre del grupo dentro de la OU `asir`; `gidNumber` es el identificador (se recomienda empezar en 2000, porque los anteriores se usan para usuarios y grupos locales).
```bash
sudo ldapadd -x -D cn=admin,dc=midominio,dc=com -W -f grupos.ldif
```

**3) Usuario.** Primero se genera una contraseña cifrada con `slappasswd` (usa SSHA, *Salted Secure Hash Algorithm*):
```bash
slappasswd
# New password: / Re-enter new password: → {SSHA}6Y6Vw+1drf61+DgLYscMV05P29RrASGy
```
Fichero `usuarios.ldif`:
```
dn: uid=nuevoUsuario,ou=asir,dc=midominio,dc=com
objectClass: top
objectClass: posixAccount
objectClass: inetOrgPerson
objectClass: person
cn: nuevoUsuario
uid: nuevoUsuario
uidNumber: 2000
gidNumber: 2000
homeDirectory: /home/nuevoUsuario
loginShell: /bin/bash
userPassword: {SSHA}6Y6Vw+1drf61+DgLYscMV05P29RrASGy
sn: nuevoUsuario
mail: nuevoUsuario@midominio.com
givenName: nuevoUsuario
```
| Atributo | Descripción |
|---|---|
| `cn` | Nombre común del usuario. |
| `uid` | Identificador único del usuario. |
| `uidNumber` | Número identificativo del usuario (2000). |
| `gidNumber` | Número identificativo del grupo principal; debe coincidir con el `gidNumber` de un grupo ya configurado en LDAP. |
| `homeDirectory` | Directorio raíz del usuario (`/home/nuevoUsuario`). |
| `loginShell` | Shell de acceso (`/bin/bash`). |
| `userPassword` | Hash de la contraseña; `{SSHA}` indica el algoritmo Salted SHA-1 utilizado. |
| `sn` | Apellido. |
| `mail` | Correo electrónico. |
| `givenName` | Nombre de pila. |

```bash
sudo ldapadd -x -D cn=admin,dc=midominio,dc=com -W -f usuarios.ldif
```
`slapcat` devuelve los detalles de la jerarquía realizada.

---

## 9.4. Directorios. Administración y operaciones. Dominios

### Directorios. Administración y operaciones
La información en OpenLDAP se estructura en un árbol jerárquico llamado **DIT** (*Directory Information Tree*):
```
dc=midominio,dc=com
└── ou=asir
    ├── ou=usuarios
    │   ├── uid=nuevoUsuario
    │   └── uid=otroUsuario
    └── ou=grupos
        ├── cn=primero
        └── cn=segundo
```
Las entradas se generan con ficheros LDIF y estos comandos:

**`ldapadd`** — agrega nuevas entradas:
```bash
ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f archivo.ldif
```
`-x`: autenticación simple; `-D`: usuario administrador; `-W`: pide la contraseña; `-f`: archivo LDIF con las entradas. Contenido de ejemplo (crea el usuario `jdoe`):
```
dn: uid=jdoe,ou=people,dc=example,dc=com
objectClass: inetOrgPerson
objectClass: person
uid: jdoe
cn: John Doe
sn: Doe
mail: jdoe@example.com
userPassword: secret
```

**`ldapdelete`** — elimina entradas existentes:
```bash
ldapdelete -x -D "cn=admin,dc=example,dc=com" -W "uid=jdoe,ou=people,dc=example,dc=com"
```

**`ldapsearch`** — busca y recupera entradas:
```bash
ldapsearch -x -b "ou=people,dc=example,dc=com" "(uid=jdoe)"
```

**`ldapmodify`** — modifica entradas existentes:
```bash
ldapmodify -x -D "cn=admin,dc=example,dc=com" -W -f archivo_modificaciones.ldif
```
con un fichero como:
```
dn: uid=jdoe,ou=people,dc=example,dc=com
changetype: modify
replace: mail
mail: john.doe@example.com
```
Tipos de modificaciones posibles (según el material): agregar atributos `changetype: add`; reemplazar `changetype: modify`; eliminar `changetype: delete`.

### Dominios
En el contexto de LDAP y Ubuntu Server, un **dominio** es una unidad administrativa que agrupa recursos de red, usuarios y computadoras; en la práctica, un espacio de nombres LDAP con su propia base de datos y políticas de seguridad. Se organiza jerárquicamente con unidades organizativas (OU). Ya tenemos creado `midominio.com` con un grupo y un usuario.

LDAP permite crear **subdominios**: subdivisiones dentro del dominio principal, estructuradas jerárquicamente y gestionables de forma semindependiente. Se representan añadiendo un nuevo componente `dc` al principio del DN del dominio principal; por ejemplo, para `dc=midominio,dc=com` un subdominio podría ser `dc=ventas,dc=midominio,dc=com`. Permiten segmentar la información y facilitan la administración de estructuras complejas; pueden tener sus propias políticas, OU, usuarios y grupos.

**Ejemplo:** dominio raíz `midominio.com`, subdominio `ventas.midominio.com`. Fichero `add_ventas.ldif`:
```
dn: dc=ventas,dc=midominio,dc=com
objectClass: top
objectClass: domain
dc: ventas

dn: ou=users,dc=ventas,dc=midominio,dc=com
objectClass: organizationalUnit
ou: users

dn: ou=groups,dc=ventas,dc=midominio,dc=com
objectClass: organizationalUnit
ou: groups
```
```bash
sudo ldapadd -x -D "cn=admin,dc=midominio,dc=com" -W -f add_ventas.ldif
```
Verificar:
```bash
ldapsearch -x -LLL -b "dc=midominio,dc=com" "(objectClass=*)"
```
Realiza una búsqueda completa en el dominio `midominio.com`, recupera todas las entradas (`(objectClass=*)`) y muestra los resultados en formato conciso (`-LLL`).

---

## 9.5. Referencias bibliográficas
- Ruiz, P. (2015, enero 3). *Capítulo 12: instalar y configurar OpenLDAP en Ubuntu*. SomeBooks. https://somebooks.es/capitulo-11-instalar-y-configurar-openldap-en-ubuntu-14-04-lts/2/

---

## A fondo
- **Introducción a LDAP.** Linux al Sur. (2023, septiembre 21). *Introducción al protocolo LDAP* [Vídeo]. https://www.youtube.com/watch?v=ONb3XmplCVY
- **Instalar y configurar OpenLDAP.** Clockwork Computer. (2023, enero 31). *Instalar y configurar OpenLDAP en servidor y cliente en Ubuntu Server y Desktop 22.04* [Vídeo]. https://www.youtube.com/watch?v=Rl032gHFu88

---

## Entrenamientos

### Entrenamiento 1 — Instalar y configurar OpenLDAP en Ubuntu
Pasos: actualizar la lista de paquetes; instalar `slapd` y `ldap-utils`; configurar el dominio «aso.com» y la contraseña del administrador.
```bash
sudo apt update
sudo apt upgrade
sudo apt install slapd ldap-utils
sudo dpkg-reconfigure slapd
```

### Entrenamiento 2 — Crear una OU «administración» en el dominio «aso»
```bash
nano ou.ldif
```
Contenido de `ou.ldif`:
```
dn: ou=administracion,dc=aso,dc=com
objectClass: organizationalUnit
ou: administración
```
```bash
sudo ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f ou.ldif
ldapsearch -x -LLL -b "dc=aso,dc=com" "ou=administracion"
```
> Nota: el DN del administrador en el comando del material es `dc=example,dc=com`, pero el dominio del ejercicio es `aso.com`; debería ser `cn=admin,dc=aso,dc=com`. Además `ou: administración` (con tilde) no coincide con `ou=administracion` del DN.

### Entrenamiento 3 — Añadir el grupo «directivos» a la OU «administración»
Contenido de `grupos.ldif`:
```
dn: cn=directivos,ou=administracion,dc=aso,dc=com
objectClass: top
objectClass: posixGroup
cn: directivos
gidNumber: 5000
```
```bash
sudo ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f grupos.ldif
ldapsearch -x -LLL -b "ou=administracion,dc=example,dc=com" "cn=directivos"
```
(Mismo problema: el material usa `dc=example` en lugar de `dc=aso`.)

### Entrenamiento 4 — Incorporar al usuario «Maria» al grupo «directivos»
Pasos: crear contraseña cifrada con `slappasswd`; crear `usuarios.ldif`; `ldapadd`; crear `add_to_group.ldif` y `ldapmodify`.

`usuarios.ldif`:
```
dn: uid=maria,ou=administracion,dc=aso,dc=com
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: top
cn: Maria
sn: User
uid: maria
uidNumber: 1001
gidNumber: 5000
homeDirectory: /home/maria
loginShell: /bin/bash
userPassword: {SSHA}5ENcrZCyRmWAGqY1E8y4KNleG7+Yb87y   # contraseña generada con slappasswd
```
```bash
sudo ldapadd -x -D "cn=admin,dc=aso,dc=com" -W -f usuarios.ldif
```
`add_to_group.ldif`:
```
dn: cn=directivos,ou=administracion,dc=aso,dc=com
changetype: modify
add: memberUid
memberUid: maria
```
```bash
sudo ldapmodify -x -D "cn=admin,dc=aso,dc=com" -W -f add_to_group.ldif
```
(Nota: la línea de `userPassword` del material incluye un comentario en la misma línea; en un LDIF real no puede ir así y debe quitarse.)

### Entrenamiento 5 — Crear el subdominio «entrega» dentro de «aso»
`add_entrega.ldif`:
```
dn: dc=entrega,dc=aso,dc=com
objectClass: top
objectClass: domain
dc: entrega
```
```bash
sudo ldapadd -x -D "cn=admin,dc=aso,dc=com" -W -f add_entrega.ldif
ldapsearch -x -LLL -b "dc=entrega,dc=aso,dc=com"
```
