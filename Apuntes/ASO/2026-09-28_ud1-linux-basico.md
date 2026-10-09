---
asignatura: Administración de Sistemas Operativos (ASO)
fecha: 2026-09-28
tema: UD1 · Tema 1 · Configuración y gestión básica en GNU/Linux
fuente: Presentación UD1 (Jairo Bahillo Calvo)
---
# ASO · UD1 (28/09) · Configuración y gestión básica en GNU/Linux

> Anterior: [Clase 2 (21/09)](2026-09-21_primera-clase-linux-basico.md) · Siguiente: [Repaso 05/10](2026-10-05_repaso-procesos-hardware-arranque.md)

Objetivos: entender GNU/Linux, conocer distribuciones, la jerarquía de directorios y dominar el shell.

## Qué es GNU/Linux
Código abierto (licencia **GPL**) · multiplataforma · multitarea y multiusuario · portable y estable (muy usado en servidores).

## Distribuciones
Una distro = SO + herramientas específicas.
| Distro | Perfil |
|---|---|
| Ubuntu | Usuarios nuevos y escritorio; gran comunidad |
| Debian | Base de muchas otras (incluido Ubuntu); estabilidad y seguridad |
| Fedora | Tecnologías de punta; desarrolladores |
| CentOS | Servidores; estabilidad a largo plazo |

## Jerarquía de directorios
Todo empieza en `/`.
| Directorio | Función |
|---|---|
| `/bin` | Comandos básicos (ls, mv, rm) |
| `/sbin` | Comandos exclusivos del administrador (root) |
| `/etc` | Archivos de configuración |
| `/home` | Directorios personales |
| `/var` | Logs y datos variables |

## Shell y comandos básicos
Shell = interfaz de línea de comandos (Bash, Zsh, Fish).
`pwd` (ruta actual) · `ls` (`ls -l` formato largo) · `cd /home/usuario` · `cp origen destino` · `mv origen destino` (mueve o renombra).

## Configuración de red
| Familia | Fichero de configuración |
|---|---|
| Debian/Ubuntu | `/etc/network/interfaces` o `/etc/netplan/` |
| Red Hat/CentOS/Fedora | `/etc/sysconfig/network-scripts` |
| SUSE/openSUSE | `/etc/sysconfig/network` |
| DNS (todas) | `/etc/resolv.conf` |
Comandos: `ifconfig eth0 192.168.1.100` (antiguo; requiere net-tools) · `ip addr add 192.168.1.100 dev eth0` (moderno y más completo) · `route add default gw 192.168.1.1 eth0` · `ping 8.8.8.8`.

## Permisos
`r` lectura (ver / listar) · `w` escritura (modificar / añadir-eliminar en directorios) · `x` ejecución (scripts, acceder a directorios). Se dividen entre propietario (**u**), grupo (**g**) y otros (**o**).
`chmod u+x script.sh` · `chown usuario archivo.txt` · `chgrp grupo archivo.txt`.

## Usuarios y grupos
```bash
sudo useradd -m -d /home/usuario usuario     # crea usuario
sudo usermod -aG grupo usuario               # añade a un grupo
sudo userdel -r usuario                      # borra usuario y su home
passwd usuario                               # cambia contraseña (otro usuario: root)
sudo groupadd grupo ; sudo groupdel grupo
sudo gpasswd -a usuario grupo                # añadir (-d eliminar) usuario de un grupo
```

## Scripting
- Script = fichero de texto con comandos que se ejecutan en secuencia (tareas repetitivas: configuraciones, copias, mantenimiento).
- Editores: **nano** (sencillo) y **vim** (potente, curva de aprendizaje alta).
- Empieza **SIEMPRE** con `#!/bin/bash`. Admite **variables** y comandos de información del sistema.
- Extensión `.sh`; `chmod +x nombreScript.sh`; ejecutar con `./nombreScript.sh`.

## Notas en directo (matices del profesor, no están en las diapositivas)
Esta clase se grabó en directo repasando el Tema 1 con ejercicios prácticos resueltos en la máquina virtual, además del contenido de las diapositivas de arriba.

### Ejercicio resuelto de permisos (repaso)
Crear `informe.txt` con permisos `rw-r-----` y `tarea.sh` con permisos `rwxr-x---`, calculando el octal en vivo sumando por grupos de 3 (`r`=4, `w`=2, `x`=1):
```bash
touch informe.txt
chmod 640 informe.txt
touch tarea.sh
chmod 750 tarea.sh
```
Aviso: nunca usar `chmod 777` en un fichero real de producción (se usó solo como ejemplo del permiso máximo). Los **scripts necesitan permiso de ejecución (`x`)** para poder lanzarse con `./script.sh` — esto se retoma en la parte de scripting de esta misma clase.

### Ejercicio resuelto de usuarios y grupos (repaso)
Crear el grupo `alumnosaso`, crear el usuario `pepe`, añadirlo a ese grupo y cambiar el propietario/grupo de `informe.txt`:
```bash
sudo groupadd alumnosaso
sudo useradd pepe
sudo usermod -aG alumnosaso pepe     # -aG añade sin quitarle otros grupos
sudo chown pepe:alumnosaso informe.txt   # usuario:grupo en una sola instrucción
id pepe    # comprueba en qué grupos quedó pepe
```
Orden importante: primero el grupo, luego el usuario, y por último añadir el usuario al grupo con `usermod -aG`.

### Primer script real: "Hola mundo"
```bash
mkdir scripts && cd scripts
touch saludo.sh
chmod +x saludo.sh      # se la da a todos los grupos; con "u+x" solo se la daría al propietario
nano saludo.sh
```
Contenido mínimo del script:
```bash
#!/bin/bash
echo "Hola Mundo"
```
Ejecutar con `./saludo.sh`. Avisos del profesor:
- La primera línea `#!/bin/bash` hay que llevarla **"tatuada a fuego"**: en clase se copia un esqueleto y se automatiza el `chmod +x`, pero en el examen hay que acordarse de escribirla a mano o el script "ni funciona ni arranca".
- **Tamaño máximo de script en el examen: un par de folios** (escritos a mano, con bolígrafo).
- Cuidado con acostumbrarse a entornos con autocompletado (VS Code): en el examen no hay IDE ni IA al lado.

### Variables y captura de fecha del sistema
Bash no es un lenguaje tipado: una variable es "una caja" que guarda lo que sea. Sintaxis: `nombre=valor` (sin espacios alrededor del `=`), se usa con `$nombre`.
```bash
echo "$(date +%d-%m-%Y)"
echo "$(date +%H-%M-%S)"
```
- Útil para loguear cuándo termina un proceso (ej. una copia de seguridad) y poder calcular cuánto tardó.
- Nuance visto en vivo (fallo real del profesor en clase): si el formato de `date` se escribe con un espacio sin comillas, da error de "operando extra" porque el shell separa por espacios como si fueran argumentos distintos — hay que entrecomillar o usar un separador sin espacios (p. ej. un guion).
- `date --help` / `man date` para ver todos los formatos disponibles.
- Ejemplo de utilidad real de las variables: guardar una ruta que cambia (p. ej. la carpeta de backups de cada mes) en una variable en vez de escribirla repetida en 10 sitios del script ("hardcodear"); así al cambiar de mes solo hay que tocar un sitio y se actualiza en todo el script.
- Aviso: **no se pueden usar palabras reservadas del sistema como nombre de variable** (p. ej. no se puede llamar `cd` a una variable), porque el shell las interpreta como sus propios comandos y rompe el script.
- Matiz importante: si una variable está mal escrita o no existe, el script normalmente **no se rompe**, simplemente no encuentra el valor y no muestra nada — "no rompe, pero no encuentra la variable".

### Otros matices sueltos
- `ll` es un **alias** de `ls -l` (no un comando real del sistema); en un entorno sin ese alias configurado (una sesión `screen`, un servidor recién instalado, o potencialmente el entorno del examen) `ll` puede no existir y hay que usar `ls -l`/`ls -la` directamente.
- Aviso de examen sobre `date`: si en el examen se pide mostrar una fecha, el profesor dará la sintaxis exacta de `date` al lado del enunciado — lo que hay que saber es **dónde colocarla dentro del script**, no memorizar el formato exacto.
- Recordatorio de seguridad: cuantos menos permisos tenga un fichero, más seguro es — "tiene que tenerlo quien tiene que tenerlo, nadie más".
