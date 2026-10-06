# Tema 7. Información del sistema. Dispositivos de almacenamiento
*Administración de Sistemas Operativos*

## Índice
Esquema · 7.1 Introducción y objetivos · 7.2 Particiones y discos · 7.3 Administración de particiones y esquemas de particionamiento · 7.4 Sistemas de ficheros · 7.5 Administrador de volúmenes lógicos · A fondo · Entrenamientos

## Esquema
Posibilidades para gestionar de forma eficiente los dispositivos de almacenamiento desde el punto de vista del software.

- **Particiones y discos**: conceptos de particiones; particiones en distintos sistemas operativos; particiones dedicadas vs. *swap file*.
- **Administración de particiones**: estándares MBR o GPT; comandos.
- **Sistemas de ficheros**: distribuciones y desglose de sistemas de ficheros.
- **Volúmenes lógicos**: grupo de volúmenes; herramienta lvm2.

---

## 7.1. Introducción y objetivos
La unidad explica cómo gestionar eficientemente los dispositivos de almacenamiento desde el software y profundiza en los volúmenes lógicos y en LVM, que permite crear volúmenes lógicos (LV) y grupos de volúmenes (VG) que utilizan varios discos físicos.

Objetivos:
- **Comprender qué es una partición, qué tipos hay y cómo se crean** (sin interfaz gráfica).
- **Entender qué es el sistema de ficheros y qué tipos hay**, con ventajas y desventajas.
- **Asignar un sistema de ficheros a una partición.**
- **Montar un sistema de ficheros** (punto de montaje).
- **Desfragmentar un sistema de ficheros.**
- **Administrar los volúmenes lógicos del sistema.**

---

## 7.2. Particiones y discos
El particionamiento permite dividir un disco en unidades de almacenamiento lógicas (**particiones**), con ventajas como organización y aislamiento de datos, copias de seguridad sencillas, distintos sistemas de archivos e instalación de distintos sistemas operativos.

En Windows, cada partición tiene un volumen representado por una letra (C:, D:, E:…) con su propia estructura de directorios.

En Linux, por defecto hay particionamiento simple: una única partición que ocupa todo el disco, con punto de montaje en el directorio raíz (`/`). Es recomendable crear otras particiones para directorios clave como `/boot`, `/home`, `/var` o `/usr`. Una característica de Linux es la flexibilidad de ubicar cada directorio en distintas particiones compartiendo todas una única estructura de directorios.

Dos estándares para estructurar particiones en HDD y SSD:
- **MBR**: hasta cuatro particiones primarias, o tres primarias y una extendida.
- **GPT**: número casi ilimitado; no distingue entre particiones lógicas o primarias.

**Swap.** Antes se hacía una partición dedicada para la zona de intercambio (*swap*), que aloja los datos que la RAM ya no puede absorber. Las distribuciones modernas usan un fichero llamado **swapfile**, que asigna espacio de la partición en uso.

---

## 7.3. Administración de particiones y esquemas de particionamiento
En un esquema de particiones:
- **Primarias**: parte del disco que almacena el sistema operativo.
- **Extendidas**: divisiones organizativas; pueden contener hasta once **particiones lógicas**, que se usan para organizar datos y archivos adicionales.

**MBR (Master Boot Record).** Esquema de los sistemas con BIOS. Más antiguo, mantiene compatibilidad. Con extendidas y lógicas se pueden crear un máximo de quince unidades: tres primarias y una extendida con hasta once lógicas. Limita la capacidad máxima a 2,2 TB.

**GPT (GUID/UUID Partition Table).** Esquema de los sistemas con **UEFI**. A cada partición se le asigna un identificador global único (UUID). Características según el material:
- Teóricamente número ilimitado de particiones; el límite de primarias en Linux es 256 (en Windows, 128).
- Soporta discos de tamaño superior a 2,2 TB.
- Mejora el tiempo de arranque y dispone de interfaz amigable.
- Más seguro que BIOS; hace copias de la tabla de particiones.
- Trabaja en modos de 32 y 64 bits.
- Se puede conectar a Internet.
- Gestor de arranque propio no vinculado al SO.

Los discos con formato GPT deben tener una **partición del sistema EFI**, formateada en FAT32 (suele ser la primera), que contiene los cargadores de arranque, firmware UEFI, imágenes de kernel y utilidades. Un disco GPT tiene un **Protective MBR** que evita que programas antiguos que no reconocen GPT dañen la estructura de datos.

Herramienta gráfica de edición de particiones: **gparted**.

### Comandos (requieren superusuario)
**`lsblk`**: información resumida de dispositivos y particiones.
```
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0   20G  0 disk
├─sda1   8:1    0   19G  0 part /
├─sda2   8:2    0    1K  0 part
└─sda5   8:5    0  975M  0 part [SWAP]
sdb      8:16   0    8G  0 disk
sr0     11:0    1   51M  0 rom  /media/cdrom0
```
Dos discos: `sda` (20 GB, tres particiones) y `sdb` (8 GB).

**`fdisk -l`**: lista todas las particiones existentes en el sistema, incluso de discos nuevos sin formatear. Para un solo disco: `fdisk -l /dev/sdb`.

**`gdisk`**: administra particiones con tabla GPT mediante un menú interactivo (`gdisk /dev/sdb`).

| Opción | Comando |
|---|---|
| `?` | Muestra la ayuda con las opciones. |
| `p` | Muestra información detallada de la tabla de particiones. |
| `d` | Borra una partición. |
| `n` | Crea una nueva partición (luego se indica primaria `p` o extendida `e`). |
| `t` | Cambia el tipo de partición. |
| `q` | Sale sin guardar cambios. |
| `w` | Confirma los cambios y sale. |
| `v` | Verifica el disco en busca de errores. |

**Crear una partición GPT en `sdb`:**
1. `gdisk /dev/sdb`
2. Opción `n`: número de partición (por defecto 1 → `sdb1`); primer sector (Enter = valor por defecto); tamaño (ej. `+2G`); código HEX (Enter = 8300, partición de Linux; `L` muestra todos).
3. Guardar con `w` y confirmar (Y).
4. Comprobar con `lsblk`.

**Formatear con `mkfs.<sistema de archivos>`:**
```bash
sudo mkfs.ext4 /dev/sdb1
```
Comprobar con `lsblk -fo NAME,FSTYPE,FSVER` (la opción `-o` permite especificar columnas).

### `mount` y `umount`
«Montar un disco» es adjuntar su sistema de ficheros a un directorio del árbol de Linux (**punto de montaje**). Dos tipos:

- **Montaje automático**: las particiones se montan al arrancar; se configura en `/etc/fstab`.
  - Ventaja: no requiere intervención manual.
  - Desventaja: si la partición no está disponible (ej. USB desconectado), puede generar un error durante el inicio.
- **Montaje manual**: con el comando `mount`.
  - Ventaja: control preciso.
  - Desventaja: requiere intervención cada vez; no persiste tras apagar.

Cada partición tiene un **UUID** único, que es el que se indica en `/etc/fstab`. `blkid` lo muestra:
```bash
sudo blkid
```

Línea de `/etc/fstab` para el montaje automático, con campos:
- `<file system>`: UUID.
- `<mount point>`: directorio de montaje.
- `<type>`: tipo de sistema de ficheros.
- `<options>`: opciones de montaje (`defaults`).
- `<dump>`: 0 (no copia) o 1 (hace copia).
- `<pass>`: orden de verificación con `fsck`: 0 no se comprueban; 1 prioridad más alta (raíz); 2 después del raíz.

Ejemplo:
```
UUID=3807a9e2-30bb-468f-9189-a45f1a660061 /mnt/particion_datos ext4 defaults 0 2
```
Hay que reiniciar para que persistan los cambios; verificar con `lsblk`. Para desmontar basta con comentar la línea con `#` y reiniciar.

Montaje manual:
```bash
sudo mount /dev/sdb1 /mnt/particion_datos2
sudo umount /dev/sdb1
```

---

## 7.4. Sistemas de ficheros
El **sistema de ficheros** organiza el modo en que se almacenan y recuperan los datos en un medio de almacenamiento. Sus tareas: gestionar la asignación de espacio a los archivos, gestionar errores en los discos, facilitar el acceso a los datos, almacenar metadatos de cada fichero y controlar el espacio libre y ocupado.

Sistemas más conocidos:
- **Ext2**: sistema de alto rendimiento que usaba Linux en el pasado; mejor velocidad de lectura/escritura.
- **Ext3**: versión mejorada de ext2, con previsión de pérdida de datos por fallos de disco o cortes de corriente; compatible con ext2.
- **Ext4**: última versión de la familia; estándar actual en GNU/Linux. Archivos de hasta 16 TB y sistema de ficheros hasta 1024 PB; mejoras en uso de CPU y velocidad.
- **FAT32**: desarrollado por Windows (evolución de FAT16); compatible con Linux; usado en unidades flash y discos extraíbles. Archivo individual máx. 4 GB y volumen máx. 2 TB.
- **NTFS**: usado por Windows desde NT 3.1; compatible con Linux. Más robusto, con encriptación, volúmenes y archivos de hasta 16 exabytes.

Todos los medios (HDD, SSD, USB, particiones) necesitan su sistema de ficheros, asignado en el proceso de **formateo**:
```bash
# Sintaxis
sudo mkfs.sistema_de_archivos <ruta_de_disco/particion>
# Ejemplo
sudo mkfs.ext4 /dev/sdb1
```

### Fragmentación
Ocurre cuando datos relacionados no se almacenan juntos, sino dispersos en posiciones no contiguas. En NTFS y FAT la desfragmentación es común. Los sistemas de archivos de Linux, en general, no necesitan desfragmentarse (dejan espacio de «n» bloques entre ficheros). No obstante, `e4defrag` desfragmenta ext4 (recomendado en dispositivos con poco espacio).

| Opción | Efecto |
|---|---|
| `-c` | Simulación: muestra un recuento de la desfragmentación sin efectuarla. |
| `-v` | Muestra el recuento para cada archivo antes y después de la desfragmentación. |

```bash
sudo e4defrag -v <ruta_partición>
sudo e4defrag -v /dev/sdb1
```

---

## 7.5. Administrador de volúmenes lógicos
Un **grupo de volúmenes (VG)** es la fusión lógica de dos o más volúmenes físicos para trabajar como una única unidad. Ejemplo: dos discos de 500 GB → volúmenes físicos → un VG de 1 TB.

No se puede convertir en volumen físico un disco particionado: hay que eliminar antes todas las particiones (opción `d` de gdisk).

Los **volúmenes lógicos (LV)** son las partes en que se divide un VG (equivalente a particiones de una unidad física). Un LV puede ser **más grande que cualquiera de los volúmenes físicos** que componen el grupo, pero siempre **más pequeño que el tamaño total del grupo**.

| Concepto | Función |
|---|---|
| Unidad de disco | Unidad de almacenamiento hardware o disco físico. |
| Volumen físico (PV) | Cada componente físico que forma parte de un grupo de volúmenes. |
| Grupo de volúmenes (VG) | Conjunto de volúmenes físicos que suman sus capacidades. |
| Volumen lógico (LV) | Partes en que se divide un VG; el límite lo marca la capacidad total del grupo. |

### Ejemplo con `lvm2`
Partimos de dos discos sin particionar: `sdb` (8 GB) y `sdc` (10 GB).

```bash
sudo apt install lvm2 -y
sudo pvcreate /dev/sd{b,c}              # convierte los discos en volúmenes físicos
sudo pvscan                             # comprueba los volúmenes físicos
sudo vgcreate grupo_prueba /dev/sd{b,c} # crea el grupo de volúmenes
sudo vgscan
sudo pvscan
sudo vgdisplay                          # información detallada del grupo
sudo lvcreate --size 11G grupo_prueba   # crea un volumen lógico de 11 GB
sudo lvdisplay                          # información de los volúmenes lógicos
```
Último paso: dar formato y montar el nuevo volumen lógico, como en el punto 7.3.

---

## A fondo
- **Creando particiones y volúmenes lógicos con LVM en Linux.** Sergio Geek. (2015, agosto 15). [Vídeo]. https://www.youtube.com/watch?v=NYYvFZPxxXo
- **Cómo crear particiones en Linux desde el terminal con Fdisk.** El Rincón del Hacker. (2022, marzo 10). [Vídeo]. https://www.youtube.com/watch?v=VDsfvHICZaU
- **Debian 12. The Universal Operating System.** Debian. (2024). https://wiki.debian.org/es/FrontPage

---

## Entrenamientos

### Entrenamiento 1
**Enunciado:** disco nuevo `sdb` de 10 GB; crea una partición de 5 GB llamada `sdb1` con sistema de ficheros ext4.

**Solución:**
```bash
gdisk /dev/sdb
# n → número de partición: Enter (1) → primer sector: Enter → tamaño: +5G → código hex: Enter (8300)
# w → confirmar con Y
mkfs.ext4 /dev/sdb1
```

### Entrenamiento 2
**Enunciado:** monta `sdb1` en `/mnt/entrenamiento1` de forma que persista tras apagar el equipo.

**Solución:** montaje automático con `/etc/fstab`.
```bash
sudo blkid    # consultar el UUID de la partición
```
Añadir una línea a `/etc/fstab` con la sintaxis `UUID  ruta_montaje  tipo  opciones  dump  pass`, por ejemplo:
```
UUID=3807a9e2-30bb-468f-9189-a45f1a660061 /mnt/particion_datos ext4 defaults 0 2
```
Reiniciar para que el sistema recorra `/etc/fstab` y actualice la configuración.
> Nota: el enunciado pide el punto de montaje `/mnt/entrenamiento1`, pero el ejemplo del material usa `/mnt/particion_datos`.

### Entrenamiento 3
**Enunciado:** desfragmenta `sdb1` y después elimínala.
```bash
sudo e4defrag -v /dev/sdb1
sudo gdisk /dev/sdb      # opción d para eliminar la partición
sudo lsblk               # comprobar que ya no existe
```
> Nota: el material usa `sudo gdisk /dev/sdb1`, pero `gdisk` debe recibir el **disco** (`/dev/sdb`), no la partición.

### Entrenamiento 4
**Enunciado:** con dos discos nuevos `sdb` (8 GB) y `sdc` (7 GB), crea un grupo de volúmenes de 15 GB llamado `grupo_entrenamiento`.
```bash
sudo apt install lvm2 -y
sudo pvcreate /dev/sd{b,c}
sudo vgcreate grupo_entrenamiento /dev/sd{b,c}
```
Comprobaciones: `vgscan` (grupos existentes), `pvscan` (volúmenes físicos), `vgdisplay` (información detallada).
> Nota: el material escribe `lsvm2` y `grupo_entrenamiento4` por error; el paquete es `lvm2` y el nombre pedido es `grupo_entrenamiento`.

### Entrenamiento 5
**Enunciado:** crea un volumen lógico de 12 GB en el grupo anterior, ¿es posible? ¿Y de 16 GB?

**Solución:** se pueden crear LV mayores que los volúmenes físicos individuales, pero nunca mayores que el grupo. Con un grupo de 15 GB: 12 GB **sí** es posible; 16 GB **no**.
```bash
sudo lvcreate --size 12G grupo_entrenamiento
sudo lvdisplay    # comprobar (el material indica "lvcreate", pero el comando de consulta es lvdisplay)
```
