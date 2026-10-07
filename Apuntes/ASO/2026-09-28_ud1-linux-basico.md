---
asignatura: Administración de Sistemas Operativos (ASO)
fecha: 2026-09-28
tema: UD1 · Tema 1 · Configuración y gestión básica en GNU/Linux
fuente: Presentación UD1 (Jairo Bahillo Calvo)
---
# ASO · UD1 (28/09) · Configuración y gestión básica en GNU/Linux

> Siguiente: [Repaso 05/10](2026-10-05_repaso-procesos-hardware-arranque.md)

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
