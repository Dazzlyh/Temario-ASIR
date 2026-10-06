# Tema 1. Configuración y gestión básica
*Administración de Sistemas Operativos*

## Índice
Esquema · 1.1 Introducción y objetivos · 1.2 El sistema operativo GNU/Linux. Características · 1.3 Distribuciones GNU/Linux · 1.4 Jerarquía de directorios. Utilidades · 1.5 Intérprete de comandos. Shell. Comandos básicos · 1.6 Configuración de red · 1.7 Permisos. Administración de usuarios · 1.8 Referencias bibliográficas · A fondo · Entrenamientos

## Esquema
**GNU/Linux** (sistema operativo, de código abierto, multitarea, multiusuario y multiplataforma):

- **Características principales**
  - Código abierto: código fuente público que puede ser modificado y distribuido.
  - Multiplataforma, multitarea y multiusuario: ejecución en paralelo de múltiples procesos; usuarios concurrentes; instalación en varios dispositivos.
  - Portable, estable y seguro: el núcleo puede ejecutarse en varias plataformas; SO muy robusto con control exhaustivo de permisos y usuarios.
- **Shell de comandos**: ejecución de comandos por parte de usuarios; automatización y *scripting* para ficheros con comandos repetitivos; redireccionamiento de entradas y salidas; gestión de procesos en ejecución; historial de comandos.
- **Utilidades**
  - Jerarquía de directorios: todos cuelgan del directorio raíz (/); cada directorio tiene su funcionalidad.
  - Configuración de red: direcciones IP, tablas de enrutamiento.
  - Administración de permisos: usuario, grupo, otros (ugo); lectura, escritura, ejecución (rwx).

---

## 1.1. Introducción y objetivos
Debido a su flexibilidad, seguridad y amplia gama de distribuciones, GNU/Linux se ha convertido en una opción popular y robusta tanto para usuarios domésticos como para entornos comerciales. Este tema aborda sus características distintivas, las distribuciones, la estructura y gestión del sistema de archivos, la gestión de usuarios y la configuración de redes.

Objetivos:
- **Comprender las características del sistema operativo GNU/Linux.** Definir lo que lo distingue de otros SO; analizar ventajas e inconvenientes.
- **Conocer las distribuciones GNU/Linux.**
- **Familiarizarse con la jerarquía de directorios y utilidades.**
- **Dominar el uso del intérprete de comandos (Shell) y los comandos básicos.**
- **Configurar redes en GNU/Linux.**
- **Administrar permisos y usuarios.**

---

## 1.2. El sistema operativo GNU/Linux. Características
GNU/Linux es un sistema operativo conocido normalmente como Linux, de código abierto, multitarea, multiusuario y multiplataforma. Está compuesto por herramientas y comandos desarrollados bajo el Proyecto GNU (*GNU's Not Unix*).

Características principales:

- **Código abierto**: desarrollado y mantenido por una amplia comunidad. Licencia GPL: su código fuente es público y cualquier programador puede modificarlo y distribuirlo; existe gran cantidad de software disponible.
- **Multiplataforma**: puede instalarse y ejecutarse en multitud de dispositivos.
- **Multitarea y multiusuario**: ejecuta en paralelo múltiples programas y procesos; varios usuarios trabajan de forma concurrente y acceden a los recursos.
- **Portable**: el núcleo de Linux puede ser compilado y ejecutado en múltiples plataformas de CPU.
- **Muy estable**: uno de los SO más estables y robustos; utilizado en la mayoría de servidores de producción y sistemas críticos.
- **Seguro**: control estricto de permisos y usuarios; difícil de atacar por su arquitectura.
- **Interfaces**: interfaces gráficas (GUI) y línea de comandos (CLI), muy potente para administración.
- **Distribuciones**: Ubuntu, Debian, Fedora… permiten elegir la que mejor se adapte al proyecto.
- **Actualizaciones**: se producen de forma regular.
- **Desarrollo de software**: herramientas de desarrollo y compilación de serie; soporte para multitud de lenguajes de scripting.
- **Configuración de redes**: herramientas avanzadas para configuración y administración de redes y robustez para servicios en red.

---

## 1.3. Distribuciones GNU/Linux
Las distribuciones (**distros**) son versiones del SO GNU/Linux, cada una personalizada y optimizada para distintos propósitos (NBX Soluciones, 2024):

| Distribución | Características principales |
|---|---|
| **Ubuntu** | Basada en Debian y una de las más utilizadas. Objetivo: ser amigable para todos los usuarios. Muy utilizada en escritorio (GNOME) y servidores. |
| **Debian** | Una de las distribuciones más fiables. Muchas posteriores se originan en Debian por su estabilidad y calidad. Uso principal en escritorio (GNOME, KDE…) y, sobre todo, servidores. Gran cantidad de información y software. |
| **Fedora** | Basada en Red Hat Enterprise Linux. Orientada al usuario final: escritorio y desarrollo. Incorpora nuevas tecnologías; Red Hat colabora en la distro y en la mejora del kernel. |
| **CentOS** | Community Enterprise Operating System. Orientada al entorno empresarial; alternativa gratuita y libre de RHEL, garantizando compatibilidad y excluyendo servicios bajo suscripción. |
| **Arch Linux** | Base independiente de cualquier otra. Sin interfaz gráfica; orientada a usuarios avanzados. *Rolling release* (siempre actualizado sin reinstalar). Configuraciones múltiples y controles estrictos de usuario. |
| **SUSE** | Una de las más extendidas y la más antigua. Nació para el mundo empresarial; existe OpenSuse para usuario final. Muy estable, instalación sencilla, herramientas como Yast. |
| **Linux Mint** | Basada en Ubuntu. Interfaz sencilla muy similar a la de Windows; comodidad para el usuario final. |
| **Manjaro** | Núcleo basado en Arch Linux. Soporta varios entornos de escritorio (Gnome, Xfce); orientada al público general. *Rolling release*. |
| **Kali Linux** | Orientada a seguridad y pruebas de acceso malintencionado (hacking ético). Usada por profesionales avanzados de seguridad informática. |

> Puedes encontrar cómo instalar Ubuntu sobre VirtualBox en la sección A fondo.

---

## 1.4. Jerarquía de directorios. Utilidades
En GNU/Linux la organización de directorios es jerárquica. Todos los directorios y ficheros cuelgan del directorio raíz (`/`). Los más importantes (Caballero, 2017):

- `/bin` (Binaries): comandos esenciales (ls, cat, cd, mv, rm, cp…), shell bash y otras utilidades.
- `/sbin` (System Binaries): similar a /bin, pero comandos de administración que sólo puede usar root.
- `/boot`: archivos necesarios para el arranque, manejados por el gestor de arranque (configuración del kernel, del gestor, módulos…).
- `/dev` (Devices): archivos que representan dispositivos. `/dev/sda` = primer disco duro; `/dev/tty` = terminales; `/dev/random` produce números aleatorios; `/dev/null` descarta la salida de un comando.
- `/etc` (Etcetera): ficheros de configuración de todo el sistema, más scripts para iniciar/parar servidores o demonios. Ej.: `/etc/passwd` contiene los usuarios.
- `/home`: directorio específico de cada usuario (`/home/user`).
- `/lib` (Libraries): librerías necesarias para los binarios de /bin y /sbin; incluye librerías del kernel.
- `/lost+found`: archivos dañados encontrados por el sistema; en cada arranque se chequea el sistema de ficheros y los corruptos se dejan aquí.
- `/media`: un subdirectorio por cada dispositivo extraíble montado (ej. USB).
- `/mnt` (mount): punto de montaje temporal para sistemas de archivos.
- `/opt` (Optional): paquetes de software opcionales, comúnmente propietario.
- `/proc`: información del sistema desde el kernel hasta configuración y procesos. Ej.: `/proc/cpuinfo`.
- `/root`: equivalente a /home pero para el usuario root.
- `/run`: información sobre la ejecución del sistema (sockets, PIDs y su estado).
- `/tmp` (Temporary): ficheros temporales, eliminados en cada reinicio o en cualquier momento. Para datos que perduren, `/var/tmp`.
- `/usr` (User): aplicaciones y archivos de uso del usuario (solo lectura):
  - `/usr/bin`: binarios no esenciales.
  - `/usr/sbin`: binarios no esenciales para el administrador.
  - `/usr/lib`: bibliotecas no esenciales.
  - `/usr/local`: software y datos instalados localmente.
  - `/usr/share`: datos compartidos (documentación, configuración).
- `/var` (Variable): datos variables: logs (`/var/log`), caché (`/var/cache`), colas de correo (`/var/mail`).

---

## 1.5. Intérprete de comandos. Shell. Comandos básicos
El intérprete de comandos (**shell**) es un programa de Unix y similares que ofrece una interfaz para interactuar con el SO. Actúa de intermediario entre usuario y núcleo y permite la ejecución de comandos, la automatización de tareas y la gestión del sistema.

Shells más comunes:

- **Bash (Bourne Again Shell)**: el más usado, por defecto en muchas distribuciones; fácil y potente; compatible con Bourne Shell.
- **Sh (Bourne Shell)**: el primero; simple y básico; aún usado en scripts antiguos.
- **Zsh (Z Shell)**: como Bash con mejoras de usabilidad; popular entre usuarios avanzados.
- **Ksh (Korn Shell)**: antiguo, combina características de bash y sh.
- **Csh (C Shell)**: sintaxis similar a C.
- **Tcsh (Tenex C Shell)**: basado en csh; enfoque en programación y características interactivas avanzadas.
- **Fish (Friendly Interactive Shell)**: diseñado para ser fácil de usar y amigable.

### Funciones del Shell
**Ejecución de comandos.** Sintaxis: `comando [opciones] [argumentos]`.
Ejemplo: `ls -l /home/usuario` devuelve el listado de ficheros del directorio /home/usuario.

**Automatización y scripting.** Los scripts son archivos de texto con una serie de comandos para automatizar tareas repetitivas; pueden incorporar bucles, condicionales, funciones…

Ejemplo de script (`#!/bin/bash` indica a la shell que lo interprete Bash):

```bash
#!/bin/bash
echo "Hola mundo"
```
Ejecución: `./script.sh` → `Hola mundo`

**Redireccionamiento de entrada y salida**
- `>` redirige la salida a un archivo.
- `<` redirige la entrada desde un archivo.
- `|` (pipe) canaliza la salida de un comando como entrada de otro.
- Ejemplo: `ls -l > listado.txt`

**Gestión de procesos**
- `ps`: lista de procesos activos. Ej.: `ps aux`.
- `kill`: finaliza un proceso identificado con su pid.
- `bg`: reanuda un proceso detenido.
- `fg`: trae un proceso de segundo plano o detenido al primer plano.
- `jobs`: trabajos en curso en la sesión actual.

**Variables y alias.** Variables para almacenar datos y configuraciones; alias para atajos de comandos largos.

**Historial de comandos.** Se navega con las flechas; el comando `history` muestra el historial.

### Características avanzadas de Bash
- Autocompletado (tecla Tab).
- Historial de comandos.
- Alias.
- Scripts de inicio: `.bashrc`, `.bash_profile`, `.bash_logout`.
- Funciones.

### Ejemplo de script Bash (`backupDir.sh`)
Guarda el contenido de `/home/usuario` en `/backups/backup-fecha.tar.gz`:

```bash
#!/bin/bash
# Definir variables
backup_dir="/backups"
source_dir="/home/usuario"
date=$(date +%Y-%m-%d)
backup_file="$backup_dir/backup-$date.tar.gz"

# Crear el directorio de backup si no existe
mkdir -p $backup_dir

# Crear el archivo de backup
tar -czf $backup_file $source_dir

# Mostrar mensaje de éxito
echo "Backup de $source_dir completado en $backup_file"
```
Se ejecuta con `./backupDir.sh`.

### Comandos
**Comandos básicos**
- `ls` (List): lista archivos y directorios. `ls -l` formato largo; `ls -a` archivos ocultos.
- `cd` (Change Directory): `cd /ruta/al/directorio`; `cd ..` sube un nivel.
- `pwd`: muestra la ruta completa del directorio actual.
- `cp` (Copy): `cp archivo_origen archivo_destino`; `cp -r directorio_origen directorio_destino` (recursivo).
- `mv` (Move): mueve o renombra archivos y directorios.
- `mkdir`: crea un directorio.
- `rmdir`: elimina un directorio vacío.
- `rm nombre_archivo` elimina un archivo; `rm -r nombre_directorio` elimina un directorio y su contenido.

**Información del sistema**
- `uname`: información del sistema operativo.
- `top`: procesos en ejecución y uso del sistema en tiempo real.
- `df` (Disk Free): resumen del espacio en disco de los sistemas de archivos montados.
- `free`: uso de la memoria.

**Manipulación de archivos**
- `echo`: muestra un mensaje. `echo "Hola Mundo"`.
- `cat`: muestra el contenido de un archivo.
- `less`: contenido página por página.
- `head` / `tail`: primeras / últimas líneas.
- `touch`: crea archivos vacíos o actualiza marcas de tiempo.
- `vi`: editor de texto.

| Comando | Descripción |
|---|---|
| `vi nombreFichero` | Abre un editor para el archivo indicado. |
| `vi -r nombreFichero` | Abre en modo recuperación tras un fallo del sistema. |

Dentro del editor:

| Comando | Descripción |
|---|---|
| `:w` | Guarda el fichero (si se indica nombre, guarda en el fichero indicado). |
| `:q` | Sale del editor (para forzar sin guardar: `:q!`). |
| `:wq` | Sale guardando cambios (equivale a `:x`). |

**Búsqueda y filtros**
- `grep "patrón" archivo`: busca el patrón dentro del archivo.
- `find /ruta -name "nombre_archivo"`: busca un archivo por nombre.
- `sort`: ordena las líneas de un archivo.

---

## 1.6. Configuración de red
Depende de la distribución. Ficheros de configuración:

- **Debian/Ubuntu**: red `/etc/network/interfaces`; DNS `/etc/resolv.conf`.
- **Red Hat/CentOS/Fedora**: red `/etc/sysconfig/network-scripts` (directorio); DNS `/etc/resolv.conf`.
- **Suse/OpenSuse**: red `/etc/sysconfig/network`; DNS `/etc/resolv.conf`.

El nombre del servidor está en `/etc/hostname`; puede modificarse con `hostnamectl` con permisos de administrador.

`/etc/resolv.conf` es común a todas; el sistema busca antes en `/etc/hosts` las traducciones nombre→IP y, si no están, consulta el DNS.

**ifconfig** configura interfaces de red. Si no está instalado: `sudo apt install net-tools`. Sin parámetros muestra el informe de configuración de las interfaces.
- Establecer IP: `ifconfig eth0 192.1.100.22`
- Levantar: `ifconfig eth0 up`; desactivar: `ifconfig eth0 down`

**ip** (versión más completa de ifconfig; gestiona redes, rutas y túneles):
- Mostrar interfaces: `ip addr`
- Establecer IP: `ip address add ipcompleta dev eth0`
- Activar: `ip link set eth0 up`; desactivar: `ip link set eth0 down`
- Ruta por defecto: `ip route add default via ipcompleta dev eth0`
- Consultar tabla de rutas: `ip route show`

**route**: gestiona las tablas de enrutamiento. Sin parámetros muestra la tabla.
- Ruta por defecto: `route add default gw ipcompleta eth0`
- Ruta estática: `route -p add -net ipcompleta/24 -gateway ipcompleta/24`

**ping**: comprueba la conectividad enviando paquetes ICMP (solicitudes de eco); si la IP está levantada responde con ICMP Echo Reply.

**netstat**: conexiones de red (entrantes y salientes), tablas de enrutamiento y estadísticas de interfaces. También existe en Windows.

---

## 1.7. Permisos. Administración de usuarios
Cada archivo y directorio tiene permisos que especifican quién puede leer, escribir o ejecutar. Se clasifican en **usuario (propietario), grupo y otros**. Comandos: `chmod`, `chown`, `chgrp`. La gestión de cuentas incluye creación, modificación y eliminación, y asignación a grupos (`useradd`, `usermod`, `userdel`).

### Comandos para la gestión de usuarios
- `useradd`: crea un usuario. Ej.: `sudo useradd -m -d /home/username username`.
- `usermod`: modifica una cuenta. Añadir a grupo existente: `sudo usermod -aG groupname username`.
- `userdel`: borra un usuario. `userdel username`; con su home: `sudo userdel -r username`.
- `passwd`: modifica la contraseña (propia sin opciones; de otro usuario con root: `sudo passwd username`).
- `id`: muestra UID, GID y grupos de un usuario.
- `sudo`: ejecuta comandos con privilegios de superusuario.

### Comandos para la gestión de grupos
- `groupadd`: `sudo groupadd groupname`.
- `groupdel`: `sudo groupdel groupname`.
- `gpasswd`: `sudo gpasswd -a username groupname` (añade); `sudo gpasswd -d username groupname` (elimina).

### Permisos de archivos y directorios
- Lectura (**r**): ver el contenido del archivo / listar el directorio.
- Escritura (**w**): modificar el archivo / añadir o eliminar archivos del directorio.
- Ejecución (**x**): ejecutar el archivo / acceder al directorio.

Cada archivo tiene un grupo y un propietario; los permisos se definen para propietario, grupo y resto.

**chmod, notación simbólica**: `chmod u+x script.sh` añade ejecución al usuario. Miembros: **u** (usuario), **g** (grupo), **o** (resto). Ej.: `chmod ugo+rwx fichero.sh` da todos los permisos a todos.

**chmod, notación octal**

| Dígito | Descripción |
|---|---|
| 0 | Ningún permiso. |
| 1 | `--x` Ejecución de archivos o acceso a directorios. |
| 2 | `-w-` Permiso de escritura. |
| 3 | `-wx` Escritura y ejecución. |
| 4 | `r--` Solo lectura. |
| 5 | `r-x` Lectura y ejecución. |
| 6 | `rw-` Lectura y escritura. |
| 7 | Todos los permisos. |

**chown**: cambia el propietario y, opcionalmente, el grupo.
- `chown nuevo_usuario archivo.txt`
- `chown nuevo_usuario:nuevo_grupo archivo.txt`

---

## 1.8. Referencias bibliográficas
- Caballero, A. J. (2017). *Administración de Sistemas Operativos*. Ra-Ma.
- NBX Soluciones (2024, enero 18). *Las distribuciones Linux que marcarán 2024*. https://www.linkedin.com/pulse/las-distribuciones-linux-que-marcar%C3%A1n-2024-nbx-soluciones-bhadc/

---

## A fondo
**Comando Chmod: cómo cambiar permisos de archivo en Linux.** Rosa, D. (2024). FreeCodeCamp. https://www.freecodecamp.org/espanol/news/comando-chmodcomo-cambiar-permisos-de-archivo-en-linux/ — explica al detalle los permisos, cómo leerlos y cómo modificarlos.

**Manual de instalación de Ubuntu sobre VirtualBox.** ProgrammingKnowledge. (2024). *How to install Ubuntu 24.04 LTS on VirtualBox in Windows 11* [Vídeo]. https://www.youtube.com/watch?v=DhVjgI57Ino — instalar VirtualBox y añadir Ubuntu.

---

## Entrenamientos

### Entrenamiento 1
**Ejercicio:** Crea un nuevo fichero bajo tu ruta actual y dale todos los permisos al usuario y permisos de lectura y escritura (no ejecución) al grupo y resto.

**Solución:**
```bash
touch nuevo_archivo.txt   # Crea un nuevo archivo bajo tu ruta actual
chmod u+rwx,g+rw,o-rwx nuevo_archivo.txt
```
> Nota del material: el enunciado habla de "lectura y escritura al grupo y resto", pero el comando de la solución (`o-rwx`) deja al resto sin ningún permiso.

### Entrenamiento 2
**Ejercicio:** Crear `mi_directorio` en tu home; crear `archivo.txt` dentro, escribir "Hola, mundo!" y mostrar su contenido.

**Solución:**
```bash
cd ~
mkdir mi_directorio
cd mi_directorio
echo "Hola, mundo!" > archivo.txt
cat archivo.txt
```
(Alternativa: usar `vi` y escribir el texto en el editor.)

### Entrenamiento 3
**Ejercicio:** En tu home crea `proyecto_simple` (con varios .txt dentro). Crear subdirectorio `backup`, mover todos los `*.txt` a `backup` y guardar el listado de `backup` en `lista_backup.txt`.

**Solución:**
```bash
cd ~
mkdir proyecto_simple
cd proyecto_simple
mkdir backup
mv *.txt backup/
ls backup/ > lista_backup.txt
```

### Entrenamiento 4
**Ejercicio:** Script que cree un archivo con el listado (con características) del directorio actual, dé permisos de lectura y escritura (no ejecución) al usuario actual, y lanzarlo.

**Solución:**
```bash
#!/bin/bash
ls -l > lista_directorio.txt
chmod u+rw lista_directorio.txt
chmod go+r lista_directorio.txt
```
Para ejecutarlo:
```bash
chmod +x scriptListado.sh
./scriptListado.sh
```

### Entrenamiento 5
**Ejercicio:** Script que (1) respalde `/home/tuusuario/proyecto` en `/home/tuusuario/respaldo/respaldo_proyecto`; (2) cambie permisos del directorio de respaldo: propietario todos, grupo lectura y ejecución, otros solo lectura; (3) registre fecha y hora en `log_respaldo.txt` dentro del directorio de respaldo.

**Solución** (tal como aparece en el material):
```bash
#!/bin/bash
directorio_proyecto="/home/tuusuario/proyecto"
directorio_backup ="/home/tuusuario/respaldo/respaldo_proyecto"
archivo_log="$directorio_respaldo/log_respaldo.txt"
mkdir "$directorio_backup"
cp -r "$directorio_proyecto" "$directorio_backup"
chmod -R 750 "$directorio_backup"
echo "Fecha y hora del respaldo: $(date)" > "$archivo_log"
```
> Nota: el script del material tiene errores (hay un espacio en `directorio_backup =`, que en bash rompe la asignación, y la variable `$directorio_respaldo` del log no está definida; debería ser `$directorio_backup`). Además, `chmod 750` da a "otros" ningún permiso, y el enunciado pide lectura (755 sería lo coherente con el enunciado).
