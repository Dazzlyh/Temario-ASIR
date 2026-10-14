---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-09-21
tema: Laboratorio 0 · Día 0 del servidor sad1 · primera conexión y "foto" inicial
fuente: transcripción de la clase en directo
---
# SAD · Laboratorio 0 (21/09) · Día 0 del servidor sad1

> Anterior: [Clase 1](2026-09-16_clase1-presentacion.md) · Siguiente: [Clase 2](2026-09-23_clase2-principios-seguridad.md)

La primera clase "oficial" es una **tutoría = laboratorio**. Las hora y media son teoría + práctica siempre; los laboratorios se publican con una semana de antelación en el foro (Material de clase): diario de incidentes, guía paso a paso y un `.txt` con los comandos para copiar y pegar.

> Libros que recomienda el profesor (los irá citando durante el curso): *Bash/Bluetin Film Manual* (comandos Linux), *RTFM – Red Team Field Manual*, *Password Cracking Manual*, *Hash Crack*.

## Nombres de servidores (para no perderse entre asignaturas)
- **SAD**: `sad1` es el activo principal; `sad2` sería la réplica exacta para alta disponibilidad (si cae uno, sigue el otro).
- **SER** (para comparar): `srv1` monta servicios (correo, FTP, streaming); `srv2` sería un DNS secundario con BIND9.
- Idea clave repetida: en SER el objetivo es que el servicio funcione; en SAD el objetivo es que **siga funcionando aunque falle o lo ataquen**.

## Levantar sad1
AWS Academy → Learner Lab → Start Lab (esperar verde) → consola AWS → EC2 → lanzar instancia:
- Nombre: **sad1**, AMI **Ubuntu 24**, tipo **t3.micro**.
- Par de claves: usar el que trae por defecto AWS Academy (aparece como **"Vockey"/OK** en la consola, pero el fichero que se descarga se llama **`labuser.pem`**) — esto confundió a varios alumnos en clase, que escribían mal el nombre (`labsuser`, `abuser`...) o buscaban el `.pem` fuera de la carpeta de Descargas.
- Security Group: abrir **SSH (22)** y **HTTP (80)**.

```bash
# en el cliente, dentro de la carpeta donde está el .pem descargado
chmod 400 labuser.pem
ssh -i labuser.pem ubuntu@<IP-pública>
# responder "yes" al fingerprint del host
```
> En Mac, varios "Permission denied" fueron por no estar en el directorio correcto al ejecutar `chmod`/`ssh`, no por el propio comando.

## La "foto del día 0" (comprobación inicial, sin tocar nada)
Idea: antes de cambiar nada hay que dejar constancia de cómo llega el servidor, para poder distinguir después falsos positivos de incidentes reales.

```bash
whoami
id
cat /etc/passwd | grep nologin      # quién NO puede conectarse por shell
sudo su                             # no es "tener permiso de superusuario", te CONVIERTES en el único superusuario (UID 0)
cat /etc/ssh/sshd_config            # confirma que solo se entra por clave pública, no hay PasswordAuthentication
ss -tulpn                           # equivalente al "netstat"/"net start" de Windows: qué escucha la máquina
uname -a
dpkg -l | wc -l                     # nº de paquetes instalados
sudo apt update                     # SOLO compara el repo con lo que hay instalado, NO instala nada
apt list --upgradable 2>/dev/null | wc -l   # cuenta paquetes desactualizados (demo en clase: 152)
tail -f /var/log/auth.log           # log en vivo de intentos de conexión SSH
```

> `apt update` ≠ `apt upgrade`: el primero solo actualiza el índice de paquetes (comprobación), el segundo sí instala las actualizaciones.

## Qué se vio en el `auth.log` real (demo en directo)
Nada más exponer la IP del servidor, aparecieron en el log unas **80 peticiones**. Al clasificarlas por IP: ~13 de un **bot** operando desde un centro de datos, 1 posible atacante individual, y el resto (~8) eran los propios alumnos de clase probando a conectarse cuando se abrió la página. Los bots que escanean así buscan identificar **qué tipo de dispositivo** hay detrás (¿cámara IP?, ¿servidor de correo?, ¿sistema de ficheros?) para catalogarlo y usarlo más adelante — es reconocimiento, no ataque todavía.

## Objetivo de la sesión
Únicamente: **saber conectarse por SSH al servidor sad1** de forma repetible. El resto de órdenes se irán viendo con calma durante el curso.

## Al terminar
- Rellenar el diario de incidentes (fecha, qué se hizo, qué se encontró).
- **Apagar siempre la instancia** al terminar: EC2 → seleccionar instancia → Instance state → **Stop** (nunca Terminate).
