---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-10-19
tema: Tutoría de dudas (Actividad 1) + Laboratorio "primera foto del servidor": comandos de triaje, logs, usuarios, procesos y herramientas
fuente: transcripción de la clase en directo
---
# SAD · Laboratorio: la primera foto del servidor (19/10)

> Anterior: [Actividad 1: MITRE y análisis forense (07/10)](2026-10-07_actividad1-mitre-forense.md) · Profesor: Damián Sualdea

**Hoy es el día de entrega de la Actividad 1 (23:59).** La clase empezó como tutoría de dudas de última hora sobre esa actividad y continuó con un laboratorio en directo sobre el servidor `sad1`: un recorrido práctico por los comandos y herramientas básicas para "hacerse una foto" del estado de un servidor Ubuntu recién abierto — quién ha entrado, qué procesos corren, qué puertos están abiertos, qué usuarios existen y qué herramientas facilitan ese trabajo del día a día. No hay contenido nuevo de teoría de amenazas; es continuación práctica de lo visto el 07/10.

## 1 · Dudas resueltas sobre la Actividad 1

- **No hay CVE para la técnica elegida:** no pasa nada. Se puede justificar diciendo explícitamente que para esa técnica no se ha encontrado CVE asociado (ejemplo que dio el profesor: un caso de Windows Server 2016/2019 ligado a "Hafnium Blue" — anotarlo como información del propio incidente, sin forzar un CVE que no existe).
- **El incidente público usa otra técnica distinta a la que yo había identificado en MITRE:** es válido citar esa otra técnica si está documentada en el informe oficial/público del incidente — "mientras justifiquéis, no hay problema; el problema es no justificar".
- **Complementar MITRE con fuentes o herramientas propias** (del día a día profesional del alumno) para rellenar lo que MITRE no cubre: aceptado sin problema, siempre indicando de dónde sale cada dato ("MITRE me faltaba información y lo he complementado con esto").
- **No hay una vulnerabilidad "oficial" detrás del ataque, solo el nombre del incidente:** también vale citarlo tal cual, sin inventar un CVE.
- Idea de fondo que repitió el profesor: la actividad busca que todos "habléis el mismo idioma" de MITRE ATT&CK (técnica, fase, grupo APT) para describir un incidente, no que exista una ficha perfecta y cerrada para cada caso.
- Dato de clase: una compañera comentó una vulnerabilidad real de routers domésticos conocida el 17/10 (varios chipsets Broadcom con WiFi vulnerable, afectando a routers de operadoras españolas como Movistar/Jazztel/MásMóvil) que **todavía no tenía CVE asignado** en ese momento — el profesor lo usó como ejemplo en vivo de que un fallo puede estar documentado y ser real sin tener aún un identificador CVE.
- Aviso de entrega (repetido dos veces en la clase): **23:59 de hoy, lunes 19**; el profesor la corregirá durante la semana.

## 2 · Laboratorio: metodología de "primera foto" de un servidor

Checklist que usó el profesor en directo sobre `sad1` (su propio servidor AWS) para explicar qué mirar nada más entrar a un servidor del que no se sabe nada, con comandos muy concretos en Ubuntu:

### 2.1 · Quién ha entrado y quién está dentro ahora

| Qué quiero saber | Comando | Notas |
|---|---|---|
| Quién está conectado ahora mismo | `w` | Solo muestra las sesiones activas en ese momento — si no aparece nadie, es que nadie más está dentro de tu propio servidor (cada compañero tiene el suyo). |
| Histórico de accesos correctos | `last` | Lista todos los accesos; por defecto empieza por los más antiguos. |
| Histórico ordenado del más reciente al más antiguo | `last -F` | Opción que usa el profesor para no tener que bajar hasta el final; muestra también el reboot y la IP de cada acceso (y si cambió de IP). |
| Intentos de acceso **fallidos** | `lastb` (requiere `sudo`) | Si no eres superusuario no se puede consultar. En la demo del profesor casi no había intentos porque el servidor solo se levanta cuando hay clase; dejarlo encendido permanentemente hace que crezcan mucho. |

### 2.2 · Logs de autenticación (`/var/log`)

```bash
cd /var/log
ls
# auth.log (actual, sin comprimir)
# auth.log.1 (rotado, sin comprimir)
# auth.log.2.gz, auth.log.3.gz ... (rotados y comprimidos)
```

- Cuantos más ficheros `auth.log.N.gz` comprimidos acumulados, más intentos de intrusión ha recibido el servidor (en servidores que se dejan siempre levantados se acumulan muchísimos — "son bots, no os preocupéis").
- Para contar/buscar dentro de los logs (hace falta `sudo` si no eres el dueño del fichero):
```bash
sudo grep -i "invalid user" /var/log/auth.log       # usuarios inválidos probados por los atacantes
sudo grep -ci "invalid user" /var/log/auth.log       # -c cuenta, -i ignora mayúsculas/minúsculas
sudo grep -i "user" /var/log/auth.log                # más genérico, trae también accesos legítimos
```
- Cada línea de `auth.log` dice: cuándo ocurrió, desde qué servidor, qué usuario (válido o inválido) intentó entrar y desde qué IP/puerto — si te lo bajas por `scp` se lee igual de bien.
- **Geolocalizar una IP atacante**: a partir de una IP vista en el log, el profesor localizó un intento de acceso real proveniente de **Filipinas** con un servicio de geolocalización de IPs — ejemplo de cómo enriquecer un log con contexto (quién, desde dónde).

### 2.3 · Superficie de ataque: puertos abiertos

```bash
ss -tnlp
```
- En el servidor del profesor aparecían **22 (SSH), 53 (DNS local) y 80 (HTTP)**; los que escuchan solo en loopback/localhost (`127.0.0.1`) no cuentan como superficie de ataque externa — solo importan los que escuchan en todas las interfaces.
- El **22 es imprescindible** (es como entramos todos); el resto depende del servicio que tengáis montado.
- **Aviso para la semana que viene:** el objetivo va a ser dejar el servidor con **0 servicios expuestos en red** aparte del 22 — es decir, bastionarlo al mínimo.

### 2.4 · Usuarios del sistema y quién tiene shell real

```bash
cat /etc/passwd                 # lista todos los usuarios, uno por servicio/proceso del SO
sudo grep 'sh$' /etc/passwd     # filtra solo las cuentas cuyo shell termina en .../bin/*sh (login interactivo real)
```
- Linux (cualquier distro con kernel Linux, no solo Ubuntu) crea un usuario de sistema por cada servicio que necesita ejecutarse, pero la mayoría tienen `nologin` o `false` como shell — **no pueden iniciar sesión**.
- Lo que de verdad importa es filtrar los que sí tienen una shell real (acaban en `sh`): en la demo del profesor, solo **`root`** y **`ubuntu`** la tenían.

### 2.5 · Quién puede convertirse en superusuario

```bash
cat /etc/group | grep sudo      # (alternativa mencionada: getent group sudo)
```
- Importante distinguir **tener una cuenta de sistema** de **poder convertirse en superusuario**: solo hay un `root`, pero varios usuarios pueden pertenecer al grupo `sudo` y "convertirse" en él. Un usuario de servicio (ejemplo del profesor: un usuario `vmail` en un servidor de correo, para gestionar Postfix) puede necesitar acceder a algo muy concreto sin tener privilegios de administración completos.

**Demo en vivo (creación de un usuario de prueba, `paco`):**
```bash
sudo adduser paco
su paco                 # cualquiera puede intentar convertirse en otro usuario normal si tiene su contraseña
sudo su                 # paco lo intenta y falla: "no estás en los sudoers" -> no puede escalar a superusuario
```
Confirma en vivo que crear un usuario nuevo **no** lo mete automáticamente en el grupo `sudo` — hay que añadirlo explícitamente si se quiere que tenga privilegios de administrador.

### 2.6 · Actualizaciones pendientes

```bash
sudo apt update
apt list --upgradable
```
- En la demo salieron **82 paquetes** pendientes de actualizar, incluyendo Apache, Python y componentes de `systemd` — comprobación que recomienda mirar con regularidad, no solo cuando hay un incidente.

### 2.7 · Procesos: `htop`

```bash
sudo apt install htop   # si no lo tenéis ya
htop
```
Atajos útiles que mostró el profesor dentro de `htop`:
- **F6** — ordenar por columna (PID, usuario, CPU, memoria, estado...).
- **F5** — vista en árbol (`tree`), muestra de qué proceso padre cuelga cada proceso hijo.
- **F4** — filtrar procesos por nombre.
- **F9** — matar un proceso (`SIGKILL`); solo funciona si tienes privilegios sobre ese proceso — en la demo, al intentar matar un proceso de Apache sin ser superusuario, `htop` lo deniega.
- **F10** — salir.
- Útil también para ver de un vistazo memoria/CPU libres y número total de procesos e hilos corriendo.

### 2.8 · Cortafuegos del propio sistema: `ufw`

```bash
sudo ufw status
```
- Es el firewall que trae Ubuntu por defecto (distinto del Security Group de AWS, que es el que habéis trabajado hasta ahora). En el servidor de la demo estaba **inactivo**, porque el Security Group de AWS ya cumple esa función en el laboratorio actual. `ufw` se trabajará más a fondo en un tema posterior del curso.

## 3 · Herramientas que facilitan el día a día (recomendadas, no obligatorias)

| Herramienta | Instalación | Para qué |
|---|---|---|
| **Midnight Commander (`mc`)** | `sudo apt install mc` | Gestor de ficheros en modo texto, interfaz de dos paneles (origen/destino) para navegar, copiar, renombrar, borrar y editar ficheros sin ir escribiendo rutas completas. F3 ver, F4 editar (elige editor, p. ej. `nano`), F10 salir. |
| **ncdu** | `sudo apt install ncdu` | Visor de uso de disco en modo texto — en la demo reveló que lo que más espacio ocupaba era el *journal* de `systemd`. |
| **lnav** (el profesor lo llama "Elena" por el acento del STT) | `sudo apt install lnav` | Visor de logs más cómodo que `cat`/`less`, con colores y navegación — se abrió apuntando a `/var/log/auth.log`. |
| **Cockpit** | Instalación + servicio `cockpit`, puerto **9090** | Panel de administración gráfico basado en web (usuarios, red, servicios, systemd...) para quien no esté cómodo todavía solo con terminal. **Tarea para casa, no obligatoria ni evaluable**: instalarlo, abrir el puerto 9090 en el Security Group de AWS, entrar con usuario/contraseña por `https://<ip-del-server>:9090`, y luego desinstalarlo/cerrar el puerto otra vez. |

Tanto `mc` como estas herramientas consumen muy poca CPU/memoria, según el profesor, así que no hay problema en tenerlas instaladas de forma permanente.

## 4 · Para llevar a casa

- Repasar que la Actividad 1 cumple la estructura de 5 apartados de la rúbrica oficial (ver nota del 07/10) antes de subirla hoy a las 23:59 — no hace falta tener un CVE para cada técnica, pero sí justificar cuando no lo hay.
- Practicar en vuestro propio servidor `sad1` la checklist completa de esta clase: `w` / `last -F` / `lastb`, revisar `/var/log/auth.log*` con `grep`, `ss -tnlp`, `cat /etc/passwd` filtrando por shell, quién está en el grupo `sudo`, `apt update` + `apt list --upgradable`, y echar un vistazo con `htop`.
- Objetivo de la próxima sesión práctica: dejar el servidor con **0 servicios expuestos en red** salvo el puerto 22.
- Opcional en casa: instalar Cockpit (puerto 9090) solo para probarlo, y quitarlo después.
