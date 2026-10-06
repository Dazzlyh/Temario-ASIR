# Tema 4. Administración de software
*Administración de Sistemas Operativos*

## Índice
Esquema · 4.1 Introducción y objetivos · 4.2 Instalación de paquetes de software · 4.3 Acceso a directorios y gestión de repositorios · 4.4 Referencias bibliográficas · A fondo · Entrenamientos

## Esquema
En Linux, un **programa** se divide en unidades más pequeñas denominadas **paquetes**, cada uno con su función específica; los paquetes son un conjunto de archivos necesarios para instalar y ejecutar programas.

- **Instalación de paquetes de software**: comando `apt`; instalación manual.
- **Directorios y repositorios**: comando `cd` (acceso a directorios); gestión de repositorios (fichero `sources.list`); agregar repositorios (añadiendo manualmente al fichero o usando comandos del sistema).

---

## 4.1. Introducción y objetivos
En Linux un programa se divide en paquetes. La razón del uso de paquetes, en lugar del modelo de software de Windows, es la gran diversidad de distribuciones Linux, lo que hace imposible garantizar que una misma pieza de software se ejecute en todos los equipos. Linux lo soluciona con las **dependencias** o paquetes complementarios, que se adaptan a cada sistema.

La descarga se hace desde servidores especiales denominados **repositorios**, que almacenan los archivos necesarios.

Objetivos:
- **Comprender qué son los paquetes de software.**
- **Conocer qué son los repositorios de Linux** y cómo se relacionan con la administración de software.
- **Aprender cómo agregar, actualizar y eliminar paquetes**: `apt update`, `apt upgrade`, `apt install`, `apt remove`.
- **Familiarizarse con el fichero de configuración de repositorios** (acceso, estructura y función de sus elementos).
- **Conocer cómo se agregan y anulan repositorios** del sistema.

---

## 4.2. Instalación de paquetes de software
La **gestión de paquetes** es el proceso de descarga, instalación, actualización y eliminación de los paquetes necesarios para el funcionamiento del software.

**Repositorios:** servidores en Internet que guardan los ficheros (paquetes) necesarios. Son públicos y se consultan desde la consola.

Cada distribución trae ya instalados unos paquetes u otros (Ubuntu trae herramientas de edición de texto e imágenes y reproductor de música/vídeo; Kali Linux, centrada en ciberseguridad, trae software de análisis y explotación de vulnerabilidades).

Comando de gestión de paquetes según la familia:
- Basadas en Debian: `apt`
- Basadas en Fedora: `dnf`
- Basadas en Arch: `pacman`

Se necesitan **permisos de superusuario** (`sudo`).

| Comando | Función |
|---|---|
| `apt update` | Actualiza la lista de paquetes disponibles. |
| `apt upgrade` | Descarga las últimas versiones de los paquetes. |
| `apt full-upgrade` | Descarga las últimas versiones eliminando las antiguas. Precaución: puede modificar paquetes internos del sistema e incluso dejarlo inutilizable. |
| `apt install "paquete"` | Instala el paquete indicado (en `/usr/local/bin` o `/usr/bin` si son comunes a todos los usuarios). |
| `apt reinstall` | Reinstala un paquete ya instalado. |
| `apt remove "paquete"` | Desinstala el paquete indicado. |
| `apt purge "paquete"` | Desinstala y elimina todos los archivos del paquete. |
| `apt autoremove` | Elimina los paquetes dependientes de otros que ya no se encuentren instalados. |
| `apt list` | Lista nombre, versión y arquitectura de los paquetes instalados, ordenados alfabéticamente. |
| `apt search "cadena"` | Busca paquetes que tengan una cadena coincidente. |

`apt` (Advanced Package Tool) y `apt-get` son prácticamente equivalentes; este último funciona a un nivel más bajo.

### `sudo apt update`
Consulta el estado actual de los repositorios para actualizar la lista de paquetes disponibles y sus versiones, pero **no instala ni actualiza ningún paquete**. Recoge solo los repositorios definidos en `sources.list`.

### `sudo apt upgrade`
Instala las nuevas versiones detectadas, respetando la configuración del software cuando sea posible. Si se reutiliza una imagen .iso antigua para una máquina virtual, `apt upgrade` pondrá al día todos los paquetes, por lo que puede tardar más de lo esperado.

### `sudo apt install "nombre_paquete"`
Instala el paquete siempre que exista en uno de los repositorios configurados. Solicita confirmación mostrando paquetes y espacio necesario; se confirma con `S` + Enter. Para omitir la confirmación: `sudo apt install -y "nombre_paquete"`.

Pasos de la instalación: 1) lee la lista de paquetes; 2) crea la lista de dependencias; 3) confirma la información de estado; 4) informa de paquetes sugeridos, recomendados y su tamaño; 5) comienza la descarga; 6) finaliza la descarga y desempaqueta; 7) realiza la configuración inicial.

### `sudo apt remove "nombre del paquete"`
Elimina los ficheros binarios del paquete, pero **no** los ficheros de configuración, los de datos ni las dependencias. Útil para desinstalar conservando la configuración y los datos del usuario. Admite `-y`.

### `sudo apt purge "nombre_paquete"`
Elimina todos los ficheros relacionados con el paquete (binarios y configuración), pero **mantiene las dependencias**. Los ficheros de datos y configuración en las carpetas de los usuarios también se mantienen. Útil para empezar de cero.

### `sudo apt autoremove`
Elimina los paquetes «huérfanos» (dependencias instaladas automáticamente que ya no son necesarias). No es recomendable usarlo siempre, porque puede borrar paquetes importantes que comprometan la estabilidad.

### Herramientas gráficas
- Debian: aplicación **Software**.
- Ubuntu: **Ubuntu Software**.

Con tres pestañas: **Explorar** (la «tienda» de aplicaciones), **Instalado** (gestionar/eliminar) y **Actualizaciones**.

---

## 4.3. Acceso a directorios y gestión de repositorios
Para gestionar los repositorios hay que moverse por el árbol de directorios:

- `cd /ruta_destino`: moverse a una ruta.
- Rutas **relativas** (al punto actual) o **absolutas** (parten de `/`).
- `cd` sin ruta: directorio personal; `cd ..`: sube un nivel; `cd -`: vuelve a la última posición visitada.
- Un usuario estándar normalmente no puede crear ficheros fuera de su directorio; para eso se usa `sudo`.
- Editar con Nano o Vi: `sudo nano /etc/apt/sources.list`.

### Gestión de repositorios
Cada repositorio tiene una **URL pública**. Dos tipos:
- **Repositorios oficiales**: proporcionados por cada distribución.
- **Repositorios PPA** (*Personal Package Archives*): no oficiales, creados y mantenidos por la comunidad.

El fichero de configuración local es **`/etc/apt/sources.list`** (`/etc` guarda todos los ficheros de configuración del sistema).

Por defecto, un Debian 11 recién instalado trae tres líneas:

```
deb cdrom:[Debian GNU/Linux 11.6.0 _Bullseye_ - Official amd64 DVD Binary-1 20221217-...
deb http://security.debian.org/debian-security bullseye-security main contrib
deb-src http://security.debian.org/debian-security bullseye-security main contrib
```

**Primera línea.** Fuente de instalación primaria: el CD-ROM de instalación. A veces `sudo apt update` falla en una máquina virtual porque intenta consultar la unidad óptica y, si no la encuentra, emite un fallo e impide consultar el resto de repositorios. Solución: **comentar la línea** añadiendo `#` al principio (el sistema la ignora).

**Segunda línea** (repositorio real), partes:
- `deb`: buscar paquetes con extensión `.deb` (instaladores o binarios).
- URL: dirección del servidor.
- `bullseye-security`: versión de la distribución.
- `main` y `contrib`: secciones del servidor donde puede descargar paquetes (organizadas según soporte oficial y licencia de uso y distribución).

**Tercera línea.** Igual que la segunda, pero con `deb-src`: paquetes de **código fuente**. Si no interesa revisar el código fuente, se puede comentar para ahorrar ancho de banda y espacio.

Si un paquete no está en estos repositorios: buscar si la aplicación tiene página oficial con versión de Linux; si no, buscar el nombre concreto del paquete y en qué repositorio está. Para instalar un `.deb` descargado: `sudo apt install` + ruta del fichero.

### Agregar un repositorio al fichero de configuración
Dos formas:
1. Añadir manualmente la línea al fichero.
2. Usar el comando del sistema:
```bash
sudo add-apt-repository "repositorio_a_añadir"
sudo apt update
```

---

## 4.4. Referencias bibliográficas
- Debian. (s. f.). *Index of /debian-security*. https://security.debian.org/debian-security/
- Mutai, J. (2023, agosto 20). *Understanding the Linux File System Hierarchy*. Computing for Geeks. https://computingforgeeks.com/understanding-the-linux-filesystem-hierarchy/

---

## A fondo
- **Configurar repositorios en Debian.** Linux Full World. (2021, febrero 17). [Vídeo]. https://www.youtube.com/watch?v=RDXgsvCdhlg
- **Instalación de software en Linux: paquetes y repositorios.** Antonio Sánchez Corbalán. (2019, diciembre 2). [Vídeo]. https://www.youtube.com/watch?v=NTpSA9k5fV4
- **Repositorios de Linux: qué son y cómo instalar y actualizar aplicaciones.** El Rincón del Hacker. (2022, octubre 18). [Vídeo]. https://www.youtube.com/watch?v=ai8tt8rEoL0
- **Documentación oficial.** Ubuntu: https://help.ubuntu.com/stable/ubuntu-help/addremove-sources.html.es · Debian: https://www.debian.org/doc/index.es.html. Ayuda desde terminal: `apt --help` o `man apt`.

---

## Entrenamientos

### Entrenamiento 1
**Enunciado:** agrega la dirección del repositorio `https://deb-multimedia.org/` al fichero de configuración mediante el comando diseñado para ello. Explica una forma alternativa.

**Solución:**
```bash
sudo add-apt-repository http://deb-multimedia.org
```
Después hay que sincronizar y actualizar los paquetes disponibles.

Alternativa: añadir manualmente la línea al fichero de configuración:
```
deb http://deb-multimedia.org bullseye main
```
`deb`: ficheros `.deb` (binarios); `bullseye`: versión de la distribución (sustituir según el caso); `main`: sección del repositorio donde buscar.

### Entrenamiento 2
**Enunciado:** sincroniza con los repositorios y actualiza todos los paquetes. ¿Cuántos paquetes se han actualizado? ¿Cuántos nuevos se han instalado?

```bash
sudo apt update
sudo apt upgrade
```
Los datos se leen de la salida, p. ej.: `0 actualizados, 0 nuevos se instalarán, 0 para eliminar y 0 no actualizados.`

### Entrenamiento 3
**Enunciado:** instala VLC desde la consola. ¿Cuántos paquetes nuevos se instalarán? ¿Cuántos MB hay que descargar y cuánto espacio adicional se usará en disco?

```bash
sudo apt install vlc
```
Ejemplo de salida del material: `0 actualizados, 51 nuevos se instalarán, 0 para eliminar y 84 no actualizados. Se necesita descargar 30,3 MB de archivos. Se utilizarán 129 MB de espacio de disco adicional.`

### Entrenamiento 4
**Enunciado:** elimina VLC incluyendo el paquete y su fichero de configuración; después elimina los paquetes instalados de forma automática que ya no son necesarios. ¿Cuánto espacio se libera en cada paso?

```bash
sudo apt purge vlc
sudo apt autoremove
```
Ejemplo del material: tras `purge` se liberan 239 kB; tras `autoremove` se liberan 122 MB.

### Entrenamiento 5
**Enunciado:** ¿Cuál es el fichero de configuración de repositorios en Linux? ¿En qué ruta? Edítalo y explica cómo conseguir que el sistema ignore un repositorio sin eliminarlo.

**Solución:** el fichero es `sources.list`, en `/etc/apt/sources.list`.
```bash
sudo nano /etc/apt/sources.list
```
El sistema lee las líneas en orden descendente. Si se comenta una línea con `#` al inicio, el sistema la ignora como si no existiera.
