---
asignatura: Administración de Sistemas Operativos (ASO)
fecha: 2026-10-05
tema: Repaso Linux · memoria, procesos, hardware, montaje, arranque, systemd
fuente: apuntes de clase de Dani (lista de comandos y conceptos; sin material adjunto)
---
# ASO · Repaso Linux (05/10)

> Anterior: [UD1](2026-09-28_ud1-linux-basico.md)

Lo anotado en clase (solo nombres/conceptos; **detalle por ampliar** si se quiere):
- **Memoria**: `free`, `vmstat`, `top` / `htop`, `/proc/meminfo`.
- **Procesos**: `ps`, `kill`, `nice` / `renice`; creación con `fork()` y `exec`; señales de `kill`: **9** (SIGKILL), **1** (SIGHUP), **15** (SIGTERM).
- **Hardware y módulos**: `lsblk`, `lspci`, `lsusb`, `lsmod`, `modprobe`.
- **Montaje**: puntos `/mnt/usb` o `/media/usb`; sistemas de archivos **ext4** y **ZFS**.
- **Arranque** de Linux completo; `systemctl` y **systemd**.

## Notas de apoyo (conocimiento general, no dicho en clase; verificar con el temario)
- 9 = termina sin posibilidad de limpieza; 15 = petición de terminación educada (el proceso puede capturarla); 1 = en muchos demonios, recarga la configuración.
- `fork()` duplica el proceso; `exec` reemplaza su imagen por otro programa.
