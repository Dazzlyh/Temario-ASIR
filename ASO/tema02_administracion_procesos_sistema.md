# Tema 2. Administración de procesos del sistema
*Administración de Sistemas Operativos*

## Índice
Esquema · 2.1 Introducción y objetivos · 2.2 Conceptos básicos del kernel · 2.3 Gestión de la memoria · 2.4 Gestión de procesos · 2.5 Gestión de dispositivos · 2.6 Gestión del sistema de archivos · 2.7 Seguridad y control de acceso · 2.8 Proceso de arranque del sistema Linux · A fondo · Entrenamientos

## Esquema
La administración del Kernel y los procesos en Linux es fundamental para cualquier administrador de sistemas. El Kernel es el núcleo del SO, gestiona recursos de hardware y proporciona servicios esenciales a las aplicaciones.

- **Funciones principales del Kernel**
  - Gestión de la memoria: asigna y libera memoria para aplicaciones y SO.
  - Gestión de procesos: crea, programa y finaliza procesos.
  - Gestión de dispositivos: controla la interacción con hardware mediante controladores.
  - Gestión de archivos: organiza y almacena datos en dispositivos de almacenamiento.
  - Seguridad y control de accesos: gestiona permisos y acceso a recursos.
- **Gestión de procesos**: creación, planificación, estado, señales y comunicación entre procesos.
- **Proceso de arranque**: secuencia de arranque; configuración y gestión de systemd y demonios de inicio automático.

---

## 2.1. Introducción y objetivos
El kernel de Linux es el núcleo del SO, responsable de gestionar los recursos del hardware y proporcionar servicios esenciales a todas las aplicaciones. Su correcta gestión y la de los procesos es crucial para el rendimiento, la estabilidad y la seguridad.

Objetivos:
- Comprender la arquitectura y el funcionamiento del kernel de Linux. Configurar y actualizar el kernel, y gestionar sus módulos.
- Gestionar hilos de ejecución: diferenciar procesos e hilos y administrar hilos y procesos concurrentes.
- Control de procesos: monitorizar y controlar procesos en ejecución.
- Entender el proceso de arranque. Gestionar servicios y demonios que se inician automáticamente. Apagar y reiniciar de forma segura.
- Configurar parámetros del kernel para optimizar el rendimiento. Realizar compilaciones personalizadas e implementar técnicas de *troubleshooting*.

---

## 2.2. Conceptos básicos del kernel
El kernel de Linux fue creado por **Linus Torvalds en 1991**. Su motivación fue la insatisfacción con MINIX (sistema educativo basado en Unix); quería un sistema libremente disponible que aprovechara las características de los procesadores 80386 de Intel, en particular la gestión de memoria virtual.

El **5 de octubre de 1991** lanzó la primera versión oficial. Podía ejecutar bash y gcc, pero no era muy funcional. El modelo de desarrollo abierto permitió que una comunidad global contribuyera, acelerando el desarrollo y mejorando la calidad.

Con los años incorporó soporte para múltiples arquitecturas, sistemas de archivos avanzados (ext3, ext4, XFS, Btrfs), capacidades de red robustas y enfoque en seguridad. Hoy es la base de Ubuntu, Fedora, CentOS, Debian, Android, sistemas embebidos y supercomputadoras.

El kernel actúa como intermediario entre el hardware y el software. Funciones principales:

- **Gestión de la memoria**: asigna y libera memoria para las aplicaciones y el SO.
- **Gestión de procesos**: creación, programación y terminación.
- **Gestión de dispositivos**: interacción con el hardware mediante controladores.
- **Sistema de archivos**: estructura para almacenar y organizar datos.
- **Seguridad y control de acceso**: usuarios y aplicaciones sólo acceden a recursos autorizados.

---

## 2.3. Gestión de la memoria
Garantiza que cada proceso tenga suficiente memoria y que el sistema use eficientemente los recursos. Abarca paginación, segmentación, memoria virtual y swap.

El kernel usa memoria virtual: los procesos pueden usar más memoria de la físicamente disponible. Cada proceso tiene su propio espacio de direcciones virtuales (aislamiento y seguridad).

**Paginación.** Divide la memoria física y virtual en bloques de tamaño fijo llamados páginas (típicamente 4 KB). La **tabla de páginas** mapea direcciones virtuales a físicas. La **TLB** (Translation Lookaside Buffer) es una caché de hardware que almacena traducciones recientes.

**Segmentación.** Menos común en sistemas modernos; divide la memoria en segmentos de tamaño variable (código, datos, pila). En x86 se usa junto con la paginación.

**Memoria virtual.** Usa el disco como extensión de la RAM mediante *swapping*. Cuando la RAM está llena, el kernel mueve páginas inactivas al espacio de intercambio.

**Gestión de la memoria física.** Dividida en zonas (ZONE_DMA, ZONE_NORMAL, ZONE_HIGHMEM). El algoritmo **Buddy System** divide la memoria en bloques de tamaño potencia de dos, combinándolos o dividiéndolos según sea necesario.

**Memoria del usuario y del kernel.** El espacio virtual del usuario está protegido del acceso de otros procesos. La memoria del kernel no está paginada y es accesible mediante una parte especial del espacio de direcciones virtuales.

**Caché y buffer.** La caché de páginas almacena páginas leídas desde disco; el buffer caché almacena bloques de dispositivos.

**Memoria compartida y mapeo (mmap).** La memoria compartida permite a varios procesos compartir un segmento; `mmap` mapea archivos o dispositivos en el espacio virtual del proceso.

**Estructuras y herramientas.** Estructuras: `mm_struct` (gestión de memoria de un proceso), `vm_area_struct` (área contigua de memoria virtual), `page` (página física). Herramientas: `free`, `vmstat`, `top`/`htop`, `smem`, y el archivo `/proc/meminfo`.

**Optimización y problemas comunes.** Se ajustan parámetros en `/proc/sys/vm/`; por ejemplo `swappiness` define la tendencia del kernel a usar swap. `sysctl` modifica estos parámetros en tiempo de ejecución. Problemas: **fragmentación de memoria** y **OOM** (*out of memory*), en cuyo caso el kernel puede invocar el **OOM killer** para terminar procesos.

---

## 2.4. Gestión de procesos
El kernel crea, planifica y finaliza procesos.

Conceptos básicos:
- **Proceso**: instancia de un programa en ejecución, con su propio espacio de direcciones y recursos.
- **PID** (Process ID): identificador único.
- **PPID** (Parent Process ID): PID del proceso padre.

Comandos útiles:
- `ps`: lista de procesos en ejecución.
- `top`: vista en tiempo real de procesos y uso de recursos.
- `htop`: similar a top, interfaz más amigable e interactiva.
- `kill`: envía señales a procesos (comúnmente para terminarlos).
- `nice` y `renice`: ajustan la prioridad de los procesos.

**Creación de procesos.** Mediante `fork()` (duplica el proceso actual creando un hijo con su propio espacio de direcciones y PID) y `exec()` (reemplaza el espacio de direcciones del proceso con un nuevo programa).

**Planificación.** El kernel usa el **Completely Fair Scheduler (CFS)**, que asigna tiempo de CPU de manera justa. Las prioridades se ajustan con `nice` y `renice`.

**Estados de los procesos:**
- **Running (R)**: ejecutándose o listo para ejecutarse.
- **Sleeping (S)**: esperando un evento (ej. E/S).
- **Stopped (T)**: detenido, generalmente por una señal.
- **Zombie (Z)**: terminado, pero su entrada en la tabla de procesos aún no ha sido limpiada por el padre.

Ejemplo de salida de `ps aux`:
```
USER       PID %CPU %MEM    VSZ   RSS TTY   STAT START TIME COMMAND
root         1  0.0  0.1 169000  6652 ?     Ss   Jun20 0:01 /sbin/init
root         2  0.0  0.0      0     0 ?     S    Jun20 0:00 [kthreadd]
username  1246  0.3  2.0 2438960 811200 ?   Sl   Jun20 2:46 /usr/lib/firefox/firefox
username  1278  0.0  0.1 107360  5768 pts/0 Ss   14:10 0:00 bash
username  1294  0.0  0.0  34412  3368 pts/0 R+   14:15 0:00 ps aux
```

**Señales y comunicación entre procesos.** Las señales permiten que los procesos se notifiquen eventos o soliciten acciones. Ejemplo común: `SIGTERM`, que pide a un proceso que termine. Se envían con `kill`. Los procesos pueden definir manejadores de señales.

---

## 2.5. Gestión de dispositivos
El kernel gestiona el hardware mediante **controladores de dispositivo** (*device drivers*), que operan en el espacio del kernel (acceso completo al hardware y la memoria).

Durante el arranque, el kernel detecta los dispositivos (ACPI, PnP) y carga los controladores (integrados o módulos dinámicos). El subsistema **udev** gestiona dinámicamente los dispositivos.

Tipos de controladores:
- **De caracteres**: flujo continuo (teclados, puertos serie).
- **De bloques**: almacenan datos en bloques (discos duros, SSD).
- **De red**: tarjetas Ethernet y adaptadores WiFi.

Los dispositivos se representan como archivos especiales en `/dev`. Utilidades:
- `lsmod`: lista los módulos del kernel cargados.
- `modprobe`: carga o descarga módulos del kernel.
- `lspci` y `lsusb`: información sobre dispositivos PCI y USB.
- `udevadm`: inspecciona y controla dispositivos gestionados por udev.

Ver particiones de un disco:
```bash
sudo fdisk -l /dev/sda
lsblk
```
Montar y desmontar:
```bash
sudo mount /dev/sda1 /mnt
sudo umount /mnt
```

---

## 2.6. Gestión del sistema de archivos
El kernel organiza los datos mediante sistemas de archivos. Al conectar un dispositivo, el kernel carga los controladores necesarios y puede **montar** su sistema de archivos.

Componentes:
- **Bloques de datos**: unidades básicas de almacenamiento (comúnmente 4 KB).
- **Superbloque**: información esencial del sistema de archivos (tamaño, número de bloques…).
- **Inodos**: estructura por archivo/directorio con tamaño, permisos y ubicación de los bloques de datos.
- **Directorios**: listas de inodos y nombres de archivo; estructura jerárquica en árbol.
- **Gestión del espacio libre**: lista de bloques libres.

Para acceder, el sistema de archivos se «monta» en un punto de montaje (ej. `/mnt/usb`). Linux soporta múltiples tipos (ext4, XFS, Btrfs), todos con bloques de datos, inodos y directorios.

---

## 2.7. Seguridad y control de acceso
El kernel asegura que usuarios y aplicaciones sólo accedan a recursos autorizados mediante permisos y control de acceso.

Cada archivo y directorio tiene permisos para **propietario (user)**, **grupo (group)** y **otros (others)**, con lectura (r), escritura (w) y ejecución (x). Ejemplo: `rwxr-xr--` → propietario lee/escribe/ejecuta; grupo lee y ejecuta; otros solo leen.

El kernel usa identificadores de usuario (**UID**) y de grupo (**GID**) para gestionar el acceso; compara el UID/GID del solicitante con los permisos del archivo. Cada proceso también tiene UID y GID.

Además, Linux usa el **modelo de capacidades**, que permite restringir las acciones incluso de root (por ejemplo, un proceso con permisos de administración de red pero sin permiso para modificar archivos del sistema).

---

## 2.8. Proceso de arranque del sistema Linux
1. **BIOS/UEFI**: inicializa y prueba el hardware y busca un dispositivo de arranque.
2. **Cargador de arranque (bootloader)**: se carga en memoria; el más común es **GRUB**, que muestra un menú y carga el kernel seleccionado.
3. **Inicialización del kernel**: detecta y configura hardware, monta el sistema de archivos raíz y ejecuta el primer proceso de usuario (`init`).
4. **Sistema de inicialización (init system)**: systemd, SysVinit o Upstart. **systemd** es el más usado (Ubuntu, Fedora, Debian).

### systemd y demonios de inicio automático
Systemd es un sistema de inicialización y gestor de servicios que paraleliza el inicio de servicios. Los servicios (demonios) son programas en segundo plano.

- **Configuración**: archivos en `/etc/systemd/system/` y `/lib/systemd/system/`. Cada servicio tiene un *unit file*.
- **Inicialización de servicios**: según dependencias y el *target* predeterminado (`multi-user.target` sin interfaz gráfica; `graphical.target` con entorno gráfico).
- **Servicios comunes**: `systemd-journald` (logs), `systemd-udevd` (eventos de dispositivos), `NetworkManager` (conexiones de red), `cron` (tareas programadas), `sshd` (acceso remoto SSH), `cups` (impresión), `rsyslog` (registros).

Gestión con `systemctl`:
```bash
sudo systemctl start <nombre_del_servicio>    # iniciar
sudo systemctl enable <nombre_del_servicio>   # habilitar en el arranque
sudo systemctl status <nombre_del_servicio>   # verificar estado
```

---

## A fondo
- **Qué es el kernel de Linux y diferencias con el sistema operativo.** Contando Bits. (2024, abril 22). [Vídeo]. https://www.youtube.com/watch?v=RJ7VmaDDFHM
- **Gestión de procesos en Linux. Comando PS, estados y consumo de recursos.** Antonio Sánchez Corbalán. (2020, octubre 26). [Vídeo]. https://www.youtube.com/watch?v=3BNbj_qjPVM

---

## Entrenamientos

### Entrenamiento 1 — Exploración de los procesos del sistema
Pasos: abrir terminal; `ps` para listar procesos (PID, usuario, %CPU, %MEM, comando); identificar esos detalles; `top` para monitorizar en tiempo real.

```bash
ps aux
top
```

### Entrenamiento 2 — Manipulación de prioridades (nice y renice)
Pasos: ejecutar un proceso que consuma CPU (`yes`); buscar su PID con `ps`; ajustar prioridad con `renice`; observar con `top`; detener el proceso.

```bash
yes > /dev/null &
ps aux | grep yes
sudo renice 10 -p <PID>
sudo renice -10 -p <PID>
top
kill <PID>
```

### Entrenamiento 3 — Configuración y uso de sysctl
Visualizar parámetros, ajustar `swappiness` a 10 temporalmente, comprobarlo y hacerlo permanente en `/etc/sysctl.conf`.

```bash
sudo sysctl -a
sudo sysctl vm.swappiness=10
sudo sysctl vm.swappiness
sudo nano /etc/sysctl.conf
# añadir la línea:
vm.swappiness=10
```

### Entrenamiento 4 — Compilación de un kernel personalizado
Pasos: descargar el código fuente (kernel.org), copiar la configuración actual, `make menuconfig` (sin cambios importantes), compilar kernel y módulos, instalar, actualizar GRUB y reiniciar.

```bash
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.10.tar.xz
tar -xvf linux-5.10.tar.xz
cd linux-5.10
cp /boot/config-$(uname -r) .config
make menuconfig
make -j$(nproc)
make modules
sudo make modules_install
sudo make install
sudo update-grub
sudo reboot
```

### Entrenamiento 5 — Monitorización y solución de problemas
Pasos: `dmesg` para revisar mensajes del kernel; identificar errores/advertencias; `strace` para rastrear un comando (ej. `ls`); `lsmod` y `modprobe` para listar y cargar/descargar módulos.

```bash
dmesg | less
strace ls
lsmod
sudo modprobe -r <módulo>
sudo modprobe <módulo>
```
