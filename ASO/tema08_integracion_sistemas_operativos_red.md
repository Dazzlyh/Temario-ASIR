# Tema 8. Integración de sistemas operativos en red
*Administración de Sistemas Operativos*

## Índice
Esquema · 8.1 Introducción y objetivos · 8.2 NFS. Instalación y configuración · 8.3 Sistema de archivos y montaje de carpetas · 8.4 Gestión de permisos · 8.5 Intercambio de recursos entre sistemas operativos Windows/Linux · 8.6 Samba. Instalación y configuración · 8.7 Servidores de archivos · 8.8 Servidores de impresión · A fondo · Entrenamientos

## Esquema
Compartir archivos y directorios entre servidores y clientes de manera sencilla facilita la colaboración y el acceso a datos desde diferentes máquinas de la red.

- **NFS (Network File System)**: servicio de Linux para compartir archivos y directorios entre equipos; instalación; configuración.
- **Sistemas de archivos / Gestión de permisos**: pasos para montar el sistema de archivos; configuración de permisos.
- **Samba**: permite interconectar equipos con diferentes SO para compartir recursos en red; instalación y uso.
- **Servidores de archivos y de impresión**: función de los servidores; configuración y uso.

---

## 8.1. Introducción y objetivos
La inmensa mayoría de los servidores del mundo corren bajo Linux. Algunos servicios permiten compartir archivos y directorios; otros, usar una misma impresora desde múltiples equipos. Se estudian NFS, Samba y CUPS.

Objetivos:
- **Comprender la función del servicio NFS**: arquitectura, protocolo, ventajas e inconvenientes.
- **Instalar y configurar un servidor NFS**: fichero de configuración, estructura y opciones básicas.
- **Comprender la función del servicio Samba**: protocolo, arquitectura y ventajas sobre NFS.
- **Instalar y configurar un servidor Samba.**
- **Conocer, instalar y configurar el servicio CUPS**: servidor de impresión combinando Samba y CUPS.

---

## 8.2. NFS. Instalación y configuración
**NFS** (*Network File System*) es un servicio de Linux para compartir archivos y directorios entre equipos de una misma red. Funciona con arquitectura **cliente-servidor**: un PC actúa como servidor que ofrece directorios y archivos, y otros equipos son clientes. Basa su funcionamiento en el protocolo de transporte **TCP/IP**.

**Ventajas**
- *Rendimiento*: optimizado para transferir datos en redes locales; buena velocidad y baja latencia.
- *Compatibilidad con múltiples plataformas.*

**Desventajas**
- *Seguridad*: no cifra datos por defecto; sin configuración adicional, los datos pueden ser interceptados.
- *Complejidad de configuración*: ajustar permisos, exportaciones y opciones de montaje en los clientes.

En el ejemplo se usan dos máquinas Linux: `usuario` (servidor/host) y `usuario2` (cliente).

### Instalación en el servidor (usuario)
```bash
sudo apt upgrade
sudo apt install nfs-kernel-server
```
Su fichero de configuración es `/etc/exports`:
```bash
sudo nano /etc/exports
```
Estructura de una línea (ejemplos comentados en el fichero):
```
# Example for NFSv2 and NFSv3:
# /srv/homes   hostname1(rw,sync,no_subtree_check) hostname2(ro,sync,no_subtree_check)
# Example for NFSv4:
# /srv/nfs4        gss/krb5i(rw,sync,fsid=0,crossmnt,no_subtree_check)
# /srv/nfs4/homes  gss/krb5i(rw,sync,no_subtree_check)
```
- La primera ruta es el directorio que se comparte desde el servidor.
- La siguiente palabra (`hostname1`) es el nombre del equipo en la red (en el ejemplo se usa su dirección IP).
- Entre paréntesis, las opciones de compartición (permisos, sincronización).
- Para autorizar a otros equipos, se teclean a continuación (como `hostname2`).

### Instalación en el cliente (usuario2)
```bash
sudo apt upgrade
sudo apt install nfs-common
```
Debe hacerse en todos los equipos que actúen como clientes NFS.

### Identificación de las máquinas en la red
```bash
ip address    # ip a es la versión acotada
```
| Dirección IP | Pertenencia |
|---|---|
| 10.0.0.5 | Host o **servidor**, máquina `usuario`. |
| 10.0.0.4 | **Cliente**, máquina `usuario2`. |

Ambas están en el mismo segmento de red (máscara /24).

### Elección de directorios para compartir
Se crea en la raíz `recurso_compartido`, con otros directorios y ficheros dentro:
```
/recurso_compartido/
├── compartido1
│   └── texto1.txt
├── compartido2
│   └── texto2.txt
└── compartido3
    └── texto2.txt
```

### Edición del fichero de configuración
En el servidor, añadir a `/etc/exports`:
```
/ruta/del/recurso/compartido  IP_cliente(opciones)
/recurso_compartido 10.0.0.4(rw,sync,no_subtree_check)
```
Para notificar los cambios a la red, dos opciones:

1. Reiniciar el servicio:
```bash
sudo systemctl restart nfs-kernel-server
```
2. Exportar sin reiniciar y comprobar:
```bash
sudo exportfs -a    # exportar los recursos compartidos
sudo exportfs       # comprobar los recursos exportados
```
(El material escribe `exportsfs`, pero el comando correcto es `exportfs`.)

Estado del servicio: `sudo systemctl status nfs-kernel-server`.

---

## 8.3. Sistema de archivos y montaje de carpetas
Para que el cliente vea los recursos compartidos, primero debe «montarlos» sobre un directorio existente en su sistema, como si accediera a un disco local.

En el cliente:
```bash
sudo mkdir -p /servidor/directorio_base
# Estructura: sudo mount IP_host:/ruta/del/recurso /ruta/punto/de/montaje
sudo mount 10.0.0.5:/recurso_compartido /servidor/directorio_base
sudo tree /servidor      # comprobar que se llega al contenido compartido
df -h                    # unidades montadas (-h: formato legible)
```
El montaje fallará si no se ha realizado antes la exportación en el servidor o no se ha reiniciado el servicio tras editar la configuración.

Desmontar:
```bash
sudo umount /servidor/directorio_base
```
El montaje con `mount` solo dura hasta apagar o reiniciar el cliente. Para el montaje **automático/permanente**, editar `/etc/fstab`:
```
# Estructura: IP_host:/ruta/del/recurso /ruta/punto/de/montaje tipo opciones
10.0.0.5:/recurso_compartido /servidor/directorio_base nfs rw,nosuid 0 0
```

### Algunas recomendaciones extra
Desde el cliente, consultar los recursos compartidos de un servidor:
```bash
sudo showmount -e 10.0.0.5
```
Compartir con **todos** los equipos de la red: sustituir la IP del cliente por `*` en `/etc/exports`:
```
/recurso_compartido *(rw,sync,no_subtree_check)
```
Lanzar el servicio automáticamente tras el arranque del servidor:
```bash
sudo systemctl enable nfs-kernel-server
```
`systemctl stop <servicio>` y `systemctl start <servicio>` detienen e inician el servicio.

---

## 8.4. Gestión de permisos
Se definen en la línea correspondiente de `/etc/exports`: **`rw`** (lectura y escritura) o **`ro`** (solo lectura).

Es vital usar `--help` o `man` para obtener más información. Se recomienda ejecutar `man` sobre estas palabras clave:
- `man nfs`: manual del servicio NFS.
- `man exports`: manual del fichero de configuración de NFS.
- `man samba`: manual del servicio Samba.
- `man smb.conf`: manual del fichero de configuración de Samba.
- `man cups`: manual del servicio CUPS.
- `man cupsd.conf`: manual del fichero de configuración de CUPS.

---

## 8.5. Intercambio de recursos entre sistemas operativos Windows/Linux
Cómo conectarse al servidor NFS desde un equipo Windows de la misma red.

1. Comprobar la IP en Windows (`ipconfig` en CMD). En el ejemplo: **10.0.0.6/24**.
2. Editar `/etc/exports` en el servidor para incluir el nuevo equipo y reiniciar el servicio:
```
/recurso_compartido 10.0.0.6(rw,sync,no_subtree_check)
```
```bash
sudo systemctl restart nfs-kernel-server
```
3. Habilitar los servicios para NFS en Windows (vienen desactivados): *Panel de control > Programas > Programas y características > Activar o desactivar las características de Windows* y marcar las tres características relacionadas con NFS (Servicios para NFS, Cliente para NFS, Herramientas administrativas). Esperar el mensaje «Windows completó los cambios solicitados».
4. Montar el directorio remoto en una unidad virtual (CMD):
```
# Estructura: mount -o anon IP_host:/ruta/del/recurso unidad_virtual
mount -o anon 10.0.0.5:/recurso_compartido H:
```
`mount` (sin parámetros) permite verificar las unidades antes y después.
5. En el explorador de archivos: clic derecho sobre «Este equipo» → **«Conectar a unidad de red»**, elegir la unidad (H:) e indicar la ruta del recurso. Comprobar que aparece la unidad H: montada en red.

---

## 8.6. Samba. Instalación y configuración
**Samba** también permite interconectar equipos con distintos SO para compartir recursos, con arquitectura cliente-servidor como NFS, pero con diferencias (según el material):
- **Protocolo**: utiliza **SMB** (*Server Message Block*).
- **Funcionalidad ampliada**: comparte archivos y servicios de impresión.
- **Mayor seguridad**: autenticación requerida para conectar.
- **Facilidad de uso y configuración**: requiere menos configuración.

Basta instalarlo en el servidor (los clientes pueden ver los archivos sin instalar el servicio):
```bash
sudo apt install samba
```
Fichero de configuración: `/etc/samba/smb.conf`. Tiene secciones y subsecciones; la primera es «Global Settings» (`[global]`). La segunda gran sección es «Share Definitions», para configurar ficheros y directorios compartidos o impresoras en red. Manual: `man smb.conf`.

---

## 8.7. Servidores de archivos
Un **servidor de archivos** es un equipo dedicado a almacenar y gestionar archivos en una red, permitiendo a los usuarios acceder, compartir y gestionarlos. Esencial en entornos empresariales y educativos.

En Samba, dentro de «Share Definitions» de `smb.conf`, se especifican los recursos compartidos y sus opciones. Plantilla de opciones básicas:

```ini
[Etiqueta_recurso_compartido_1]
   comment = Home Directories      # breve descripción del recurso
   path = /ruta/del/recurso/compartido   # ruta interna del servidor
   browseable = no                 # si el recurso puede alcanzarse via web o no
   read only = yes                 # compartir solo en modo lectura (o writeable = yes)
   create mask = 0700              # máscara de permisos para archivos (por defecto 0700; 0775 si necesitan lectura y escritura compartida)
   directory mask = 0700           # máscara de permisos para directorios creados
   valid users = nombre_usuario    # usuarios con permiso (con contraseña establecida con smbpasswd)
   guest ok = no                   # niega el acceso a usuarios invitados
```

### Crear el recurso compartido en Samba
```bash
sudo mkdir /compartido1_samba
sudo touch samba1.txt
```
Configuración añadida a `smb.conf`:
```ini
[recurso1]
   comment = Mi primer recurso
   path = /compartido1_samba
   browseable = yes
   writeable = yes
   guest ok = no
   valid user = usuarioSamba
   create mask = 0775
   directory mask = 0775
```
`usuarioSamba` debe estar dado de alta como usuario válido en el servidor. Para dar acceso a un grupo: `@grupo` en la opción de usuarios válidos.

Reiniciar el servicio y comprobar:
```bash
sudo systemctl restart smbd
testparm       # muestra el estado del servicio y de los recursos compartidos
```
Contraseña de acceso al servicio para el usuario autorizado:
```bash
sudo smbpasswd -a usuarioSamba
```
(El material muestra `usuario2` en el texto, pero `usuarioSamba` en la captura y la configuración.)

### Acceso al recurso
Desde otro equipo Linux, en el explorador de archivos → «Otras ubicaciones» → `smb://10.0.0.5`, e introducir usuario y contraseña. También funciona desde el explorador de Windows en el mismo segmento de red.

Por línea de comandos, instalar el cliente y conectar:
```bash
sudo apt install smbclient
# Estructura: smbclient -U <usuario> //IP_servidor/ruta/del/recurso
smbclient -U usuarioSamba //10.0.0.5/compartido1_samba
```
Pide la contraseña y el *prompt* pasa a `smb:\>`, es decir, estamos en el directorio compartido.

---

## 8.8. Servidores de impresión
Un **servidor de impresión** administra las solicitudes de impresión de múltiples usuarios en una red: recibe las tareas, las organiza y las envía a la impresora adecuada.

Para montarlo en Linux:

1. Modificar la sección `[printers]` del fichero de Samba (`browseable = no` → `yes` y `guest ok = no` → `yes`):
```ini
[printers]
   comment = All Printers
   browseable = yes
   path = /var/spool/samba
   printable = yes
   guest ok = yes
   read only = yes
   create mask = 0700
```
2. Instalar CUPS y editar su fichero `/etc/cups/cupsd.conf`:
```bash
sudo apt install cups
```
   - Sustituir `Listen localhost:631` por la IP del servidor.
   - Añadir `Allow all` en las tres secciones señaladas (`<Location />`, `<Location /admin>`, `<Location /admin/conf>`).
3. Reiniciar los dos servicios:
```bash
sudo systemctl restart smbd
sudo systemctl restart cups
```
4. Acceder al panel de control de CUPS desde el navegador de cualquier equipo de la red: `10.0.0.5:631`. Desde la pestaña de administración se añaden impresoras.
5. En Windows: *Configuración > Dispositivos > Impresoras y escáneres > Agregar una impresora o un escáner* → «La impresora que deseo no se encuentra en esta lista» → «Agregar una impresora con una dirección IP o un nombre de host» → indicar IP del servidor y puerto de escucha de CUPS → seleccionar el modelo para asociar el controlador.

---

## A fondo
- **NFS SERVER | Instalar NFS y configurar recursos.** Marc Venteo. (2022, marzo 1). [Vídeo]. https://www.youtube.com/watch?v=IoWyq2ddZjc
- **SAMBA SERVER | Instalar Samba y configurar recursos.** Marc Venteo. (2022, febrero 22). [Vídeo]. https://www.youtube.com/watch?v=86Q30-JroJY
- **Servidor de Impresión con CUPS y SAMBA a través de Linux y Windows.** CosasdeInges. (2020, marzo 20). [Vídeo]. https://www.youtube.com/watch?v=S_XrLYoIiqg
- **Manuales de Linux (manpages).** Man-pages. (2022). https://man.cx/man(1)/es

---

## Entrenamientos

### Entrenamiento 1
**Enunciado:** actualiza los repositorios, instala los paquetes de NFS (cliente y servidor). ¿Cuál es el fichero de configuración de NFS?
```bash
sudo apt update
sudo apt install nfs-kernel-server   # servidor
sudo apt install nfs-common          # cliente
```
(El material escribe `sudo apt nfs-common`, falta `install`.) El fichero de configuración se llama `exports` y está en `/etc/exports`, en el equipo servidor; se descarga junto al paquete `nfs-kernel-server`.

### Entrenamiento 2
**Enunciado:** explica la estructura del fichero de NFS y añade un recurso: ruta `/compartidos/recurso1`, compartido con la IP `192.168.10.2`, solo lectura y sincronización.

Cada línea (un recurso) consta de tres partes: ruta local del directorio; nombre/IP del equipo (o `*` para todos); y, junto al host, sin espacios y entre paréntesis, las opciones (permisos, sincronización).
```
/compartidos/recurso1 192.168.10.2(ro,sync)
```

### Entrenamiento 3
**Enunciado:** actualiza repositorios e instala Samba (cliente y servidor). ¿Fichero de configuración?
```bash
sudo apt update
sudo apt install samba        # servidor
sudo apt install smbclient    # cliente
```
(El material escribe `sudo apt smbclient` y menciona «NFS» por error.) El fichero es `smb.conf`, en `/etc/samba/smb.conf` del servidor; se descarga junto con el paquete `samba`.

### Entrenamiento 4
**Enunciado:** explica la estructura del fichero de Samba y añade un recurso: etiqueta `recurso_samba`; ruta `/compartido/recurso_samba`; comentario `entrenamiento_4`; accesible como recurso de red; solo lectura; único usuario `usuario1` sin anónimos; máscara de archivos 0700 y de directorios 0775.

Estructura: secciones divididas por un comentario a modo de título, seguidas de una etiqueta entre corchetes que agrupa en sangría las opciones; la primera es «Global Settings».
```ini
[recurso_samba]
 path = /compartido/recurso_samba
 comment = entrenamiento_4
 browseable = yes
 read only = yes
 valid user = usuario1
 guest ok = no
 create mask = 0700
 directory mask = 0775
```

### Entrenamiento 5
**Enunciado:** actualiza repositorios e instala el paquete de CUPS. ¿Fichero de configuración? Edítalo estableciendo la IP del servidor.
```bash
sudo apt update
sudo apt install cups
```
El fichero es `cupsd.conf`, en `/etc/cups/cupsd.conf` del servidor; se descarga con el paquete CUPS. Se edita sustituyendo `localhost` en `Listen localhost:631` por la IP del servidor.
