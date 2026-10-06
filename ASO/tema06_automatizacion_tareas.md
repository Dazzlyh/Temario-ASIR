# Tema 6. Automatización de tareas
*Administración de Sistemas Operativos*

## Índice
Esquema · 6.1 Introducción y objetivos · 6.2 Introducción a la automatización de tareas en Linux · 6.3 Planificación y automatización de tareas · 6.4 Planificación de tareas diferidas en Linux · 6.5 Planificación de tareas periódicas en Linux · A fondo · Entrenamientos

## Esquema
La automatización de tareas en Linux permite programar y ejecutar tareas repetitivas sin intervención manual, mejorando la eficiencia y reduciendo errores.

- **Herramientas para la automatización**
  - **Cron**: programa tareas periódicas a intervalos regulares.
  - **At**: programa tareas para ejecutarse una sola vez en el futuro.
  - **Anacron**: asegura que las tareas periódicas se ejecuten incluso si el sistema no estaba encendido en el momento programado.
  - **Systemd Timers**: configuración flexible para tareas periódicas en sistemas que usan systemd.
- **Tareas diferidas**: se ejecutan una vez en el futuro con `at` y systemd timers.
- **Tareas periódicas**: recurrentes con cron, anacron y systemd timers, para asegurar el mantenimiento continuo del sistema.

---

## 6.1. Introducción y objetivos
Permite programar y ejecutar tareas repetitivas sin intervención manual, ahorrando tiempo y reduciendo el riesgo de errores humanos. Se logra con planificación (Cron y At), scripts de shell y tareas periódicas de mantenimiento.

Objetivos:
- **Comprender la importancia de la automatización de tareas.**
- **Identificar las tareas que pueden ser automatizadas**: copias de seguridad, actualizaciones de software, mantenimiento de logs.
- **Usar Cron y At**: sintaxis de crontab, programar tareas diarias/semanales/mensuales; `at` para ejecución única.
- **Configurar tareas periódicas con Cron y Anacron.**

---

## 6.2. Introducción a la automatización de tareas en Linux
Consiste en el uso de herramientas y scripts que permiten programar y ejecutar tareas repetitivas sin intervención manual. Ahorra tiempo, minimiza errores humanos, mejora la eficiencia operativa y garantiza que las tareas críticas se realicen oportunamente. Es esencial para el mantenimiento y la administración proactiva de servidores.

---

## 6.3. Planificación y automatización de tareas
Herramientas principales: **Cron, At, Anacron y Systemd timers**.

### Cron
Programa la ejecución de comandos o scripts en intervalos regulares (minutos, horas, días, semanas, meses). Los trabajos se definen en archivos llamados **crontabs** (*cron table*). Cada usuario tiene el suyo y hay un crontab del sistema gestionado por el administrador.

Sintaxis básica:
```
* * * * * comando
```
Los cinco asteriscos representan: **Minuto (0-59) · Hora (0-23) · Día del mes (1-31) · Mes (1-12) · Día de la semana (0-7, donde 0 y 7 son domingo).**

Ejemplo: ejecutar un comando a las 2:30 AM todos los días:
```
30 2 * * * /ruta/a/tu/comando
```

Comandos:
- `crontab -e`: editar el crontab del usuario actual.
- `crontab -l`: listar las tareas programadas.
- `crontab -r`: eliminar el crontab del usuario actual.
- `sudo crontab -u nombre_usuario -e`: editar el crontab de otro usuario (requiere superusuario).

Atajos:
- `@reboot`: una vez al iniciar el sistema.
- `@yearly` o `@annually`: una vez al año (`0 0 1 1 *`).
- `@monthly`: una vez al mes (`0 0 1 * *`).
- `@weekly`: una vez a la semana (`0 0 * * 0`).
- `@daily` o `@midnight`: una vez al día (`0 0 * * *`).
- `@hourly`: una vez a la hora (`0 * * * *`).

Ejemplo: `@reboot /ruta/a/tu/script.sh`

---

## 6.4. Planificación de tareas diferidas en Linux
Las **tareas diferidas** se programan para ejecutarse **en un momento específico en el futuro**, en lugar de repetirse. Herramienta ideal: **At**.

### At
Programa tareas que deben ejecutarse **una sola vez**.
```bash
echo "comando" | at time
```
`time` puede ser una hora específica («14:00») o expresiones relativas («now + 2 hours»). Ejemplo, ejecutar un script mañana a las 2 p. m.:
```bash
echo "/ruta/a/tu/script.sh" | at 2pm tomorrow
```

### Ver y administrar tareas programadas
- `atq`: muestra la cola de trabajos (número de trabajo, fecha y hora programadas, usuario).
```
1    2023-06-24 14:00 a username
2    2023-06-25 09:00 a username
```
- `atrm <número>`: elimina una tarea programada. Ej.: `atrm 1`.

### Archivos de configuración
- `/etc/at.allow`: si existe, solo los usuarios listados pueden usar `at`.
- `/etc/at.deny`: si `at.allow` no existe, los usuarios listados aquí no pueden usar `at`.
- Si ninguno existe, solo los superusuarios pueden usar `at`.

---

## 6.5. Planificación de tareas periódicas en Linux
Se ejecutan a intervalos regulares (diarios, semanales, mensuales…) para mantenimiento, monitoreo, copias de seguridad, etc. Herramientas más comunes: **Cron, Anacron y Systemd timers.**

### Anacron
Complementa a Cron asegurando que las tareas periódicas se ejecuten incluso si el sistema no estaba encendido en el momento programado (útil en laptops y equipos no siempre encendidos). Configuración en `/etc/anacrontab`:

```
periodo retraso identificador comando
```
- `periodo`: frecuencia (en días).
- `retraso`: retraso en minutos tras el arranque del sistema.
- `identificador`: nombre único de la tarea.
- `comando`: comando o script a ejecutar.

Ejemplos:
```
1 5 backup.daily /ruta/a/tu/backup.sh     # diario, 5 min de retraso tras el arranque
7 10 clean.weekly /ruta/a/tu/clean.sh     # semanal, 10 min de retraso tras el arranque
```

### Systemd timers
Alternativa moderna a Cron y Anacron en sistemas con systemd; ofrecen una **configuración más flexible y detallada**. Requieren dos archivos: una **unidad de servicio** y una **unidad de temporizador**.

**Unidad de servicio** — `/etc/systemd/system/mi-servicio-diario.service`:
```ini
[Unit]
Description=Ejecutar Script Diario

[Service]
Type=oneshot
ExecStart=/ruta/a/tu/script-diario.sh
```

**Unidad de temporizador** — `/etc/systemd/system/mi-servicio-diario.timer`:
```ini
[Unit]
Description=Temporizador Diario para Script

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```

**Habilitar y activar:**
```bash
sudo systemctl enable mi-servicio-diario.timer
sudo systemctl start mi-servicio-diario.timer
```

### Comparación entre Cron, Anacron y Systemd timers
- **Cron**: ideal para tareas recurrentes en sistemas siempre encendidos. No asegura la ejecución si el sistema no estaba encendido.
- **Anacron**: asegura la ejecución de periódicas en sistemas que no están siempre encendidos (laptops y desktops).
- **Systemd timers**: configuración más flexible y detallada; ideal para sistemas modernos con systemd; combinan lo mejor de Cron y Anacron con capacidades adicionales.

---

## A fondo
- **Cómo usar Crontab en Ubuntu para automatizar tareas.** El Rincón del Hacker. (2022, marzo 3). [Vídeo]. https://www.youtube.com/watch?v=d2Q0NiyVO5M
- **Understand Systemd Timer Units and how to create them.** theurbanpenguin. (2023, agosto 9). [Vídeo]. https://www.youtube.com/watch?v=c20saf4q4pw — enumerar unidades de temporizador con `systemctl list-timers` y crear nuevas con `systemctl edit`.

---

## Entrenamientos

### Entrenamiento 1 — Tarea diaria con Cron
Crear un script que imprima la fecha y hora (`date.sh`), abrir el crontab y añadir una línea para ejecutarlo todos los días a las 8 a. m.; comprobar con `crontab -l`.
```bash
echo "#!/bin/bash" > /ruta/a/tu/date.sh
echo "date" >> /ruta/a/tu/date.sh
chmod +x /ruta/a/tu/date.sh
crontab -e
# línea a añadir:
0 8 * * * /ruta/a/tu/date.sh
crontab -l
```

### Entrenamiento 2 — Tarea con At
Script `hello.sh` que escriba "Hola, Mundo!" en un archivo de texto; programarlo para dentro de dos horas; verificar.
```bash
echo "#!/bin/bash" > /ruta/a/tu/hello.sh
echo 'echo "Hola, Mundo!" > /ruta/a/tu/hello.txt' >> /ruta/a/tu/hello.sh
chmod +x /ruta/a/tu/hello.sh
echo "/ruta/a/tu/hello.sh" | at now + 2 hours
atq
```

### Entrenamiento 3 — Tarea periódica con Systemd Timers
Script `clean_temp.sh` que limpie archivos temporales; unidad de servicio en `/etc/systemd/system/clean_temp.service`; unidad de temporizador en `/etc/systemd/system/clean_temp.timer`; habilitar y activar.
```bash
echo "#!/bin/bash" > /ruta/a/tu/clean_temp.sh
echo "rm -rf /ruta/a/temp/*" >> /ruta/a/tu/clean_temp.sh
chmod +x /ruta/a/tu/clean_temp.sh
```
`clean_temp.service`:
```ini
[Unit]
Description=Limpiar Archivos Temporales

[Service]
Type=oneshot
ExecStart=/ruta/a/tu/clean_temp.sh
```
`clean_temp.timer`:
```ini
[Unit]
Description=Temporizador para Limpiar Archivos Temporales

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```
```bash
sudo systemctl enable clean_temp.timer
sudo systemctl start clean_temp.timer
systemctl status clean_temp.timer
```

### Entrenamiento 4 — Tarea semanal con Anacron
Script `backup.sh` que haga una copia de seguridad de un directorio; editar `/etc/anacrontab` para añadir la tarea semanal.
```bash
echo "#!/bin/bash" > /ruta/a/tu/backup.sh
echo "tar -czf /ruta/a/backup.tgz /ruta/a/tu/directorio" >> /ruta/a/tu/backup.sh
chmod +x /ruta/a/tu/backup.sh
sudo nano /etc/anacrontab
# línea a añadir:
7 10 backup.weekly /ruta/a/tu/backup.sh
```

### Entrenamiento 5 — Listar y eliminar tareas programadas con At
Programar una tarea que imprima "Tarea programada con at" en un archivo de texto en una hora; listarlas; eliminarla.
```bash
echo 'echo "Tarea programada con at" > /ruta/a/tu/at_task.txt' | at now + 1 hour
atq
atrm [job_number]
```
