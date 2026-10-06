# Tema 5. Instalación, configuración y uso de servicios de acceso y administración remota
*Administración de Sistemas Operativos*

## Índice
Esquema · 5.1 Introducción y objetivos · 5.2 Protocolos de acceso remoto y puertos implicados · 5.3 Servicios de acceso remoto del propio sistema operativo · 5.4 SSH · 5.5 Telnet · A fondo · Entrenamientos

## Esquema
Herramientas esenciales en la administración de sistemas y redes que permiten a los administradores administrar y supervisar la infraestructura de TI desde ubicaciones remotas.

- **Protocolos de acceso**
  - SSH: acceso remoto seguro. Puerto 22.
  - VNC: interfaz gráfica. Puerto a partir del 5900.
  - RDP: escritorio remoto. Puerto 3389.
  - Telnet: conexión remota (no segura). Puerto 23.
  - FTP: transferencia de archivos. Puerto 21.
  - SFTP: transferencia de archivos segura. Puerto 22.
  - HTTP/HTTPS: puertos 80 y 443.
- **SSH**: transferencia de archivos y administración de sistemas de forma segura y remota; claves criptográficas y cifrado de datos con autenticación sólida; el puerto 22 normalmente se puede cambiar; algoritmos AES (cifrado de datos) y RSA o DSA (autenticación); redirección de puertos y túneles seguros para aplicaciones no seguras.
- **Telnet**: comunicación bidireccional, interactiva y basada en texto entre dos máquinas a través de la red; transmite datos (incluidas credenciales) en texto claro, vulnerable a intercepciones y ataques de intermediarios; puerto 23; reemplazado por SSH por su falta de seguridad.

---

## 5.1. Introducción y objetivos
Los servicios de acceso y administración remota reducen la necesidad de acceso físico y mejoran la capacidad de respuesta ante incidentes y mantenimiento. Los protocolos más populares son **Telnet** y **SSH**; además, los sistemas operativos modernos incluyen servicios nativos.

Objetivos:
- **Comprender los protocolos de acceso remoto y los puertos implicados**: fundamentos de SSH y Telnet; diferencias de seguridad y funcionalidad.
- **Investigar los servicios de acceso remoto que ofrecen los SO**: ventajas y limitaciones.
- **Evaluar y seleccionar herramientas adecuadas** según seguridad, coste y facilidad de uso.
- **Instalar y configurar SSH**: servidor SSH en Unix/Linux, opciones de seguridad, conexión con clientes desde distintas plataformas.
- **Instalar y configurar Telnet**: analizar sus limitaciones de seguridad y cuándo podría estar justificado.

---

## 5.2. Protocolos de acceso remoto y puertos implicados

**Secure Shell (SSH).** Uno de los protocolos más comunes y seguros en Linux. Proporciona canales seguros sobre redes inseguras con cifrado. **Puerto 22.** Permite acceso remoto y también servir de FTP. Se configura principalmente en `/etc/ssh/sshd_config` (claves de autenticación, permisos de usuario, opciones de cifrado).

**Virtual Network Computing (VNC).** Control de una computadora de forma remota con interfaz gráfica; útil para soporte técnico y administración. **Puerto a partir del 5900.** Servidores como tightvnc, tigervnc y x11vnc tienen sus propios archivos de configuración.

**Remote Desktop Protocol (RDP).** Propio de Windows; en Linux se puede usar con aplicaciones como **xrdp**. **Puerto 3389.** En Linux se configura en `/etc/xrdp/`.

**Telnet.** Acceso a una terminal remota y conexión punto a punto por el **puerto 23**. La comunicación es en **texto plano**, lo que pone en peligro la seguridad; su uso se ha reducido en favor de SSH. Se configura a través de `/etc/inetd.conf` o `/etc/xinetd.d/telnet`.

**File Transfer Protocol (FTP).** Transferencia de archivos; también acceso remoto a sistemas de archivos. **Puerto 21 (TCP)** para control y puertos de datos en el rango 1024-65535.

**SSH File Transfer Protocol (SFTP).** Parte del paquete SSH; transferencia y administración remota de archivos seguras. **Puerto 22 (TCP).**

**HTTP/HTTPS.** Administrar el servidor mediante interfaz web. HTTPS añade cifrado. **Puertos 80 (HTTP) y 443 (HTTPS).**

La CLI puede administrar puertos; por ejemplo, `firewall-cmd` permite abrir un puerto al tráfico entrante de forma persistente. Mantener puertos abiertos puede ser un **riesgo de seguridad**, por lo que se recomienda **mantenerlos cerrados** y abrir solo los necesarios.

| Protocolo | Puerto | Descripción |
|---|---|---|
| SSH | 22 | Protocolo de acceso remoto seguro. |
| VNC | a partir del 5900 | Permite interfaz gráfica. |
| RDP | 3389 | Escritorio remoto. |
| Telnet | 23 | Conexión remota (no encriptado). |
| FTP | 21 | Transferencia de archivos. |
| SFTP | 22 | Transferencia de archivos segura. |
| HTTP/HTTPS | 80 / 443 | Transferencia de hipertexto / seguro. |

---

## 5.3. Servicios de acceso remoto del propio sistema operativo

### SSH
El servicio de acceso remoto más utilizado en Linux: ejecuta comandos, transfiere archivos y crea túneles seguros.

```bash
sudo apt-get install openssh-server   # Debian y derivadas
sudo yum install openssh-server       # Red Hat y derivadas
```
Compatible con otros SO: OpenSSH está incluido en Windows 10 y Windows Server; hay clientes/servidores de terceros como PuTTY y WinSCP.

### Virtual Network Computing (VNC)
```bash
sudo apt-get install tightvncserver   # Debian y derivadas
sudo yum install tigervnc-server      # Red Hat y derivadas
```

### Remote Desktop Protocol (RDP)
Acceso remoto al escritorio en Windows (activando «Escritorio remoto»). Usa siempre el puerto **3389** y transmite movimientos de ratón, pulsaciones de teclas, visualizaciones de escritorio, etc. vía TCP/IP; cifra todos los datos. En Linux:
```bash
sudo apt-get install xrdp   # Debian y derivadas
sudo yum install xrdp       # Red Hat y derivadas
```

### Telnet
Se usa principalmente en administración de redes privadas por ser menos seguro que SSH.
```bash
sudo apt-get install telnetd        # Debian y derivadas
sudo yum install telnet-server      # Red Hat y derivadas
```

### Abrir puertos en el firewall (ufw)
```bash
sudo ufw allow 22/tcp     # Permitir SSH
sudo ufw allow 5900/tcp   # Permitir VNC
sudo ufw allow 3389/tcp   # Permitir RDP
sudo ufw allow 80/tcp     # Permitir HTTP
sudo ufw allow 443/tcp    # Permitir HTTPS
```

---

## 5.4. SSH
**Secure Shell** es un protocolo de red criptográfico para operar servicios de red seguros sobre una red no segura. Se usa para acceso a servidores remotos y ejecución segura de comandos, transferencia de archivos y enrutamiento seguro de red. Es la base de **SCP** y **SFTP**, y permite **túneles seguros** (redirigir puertos y acceder a servicios internos).

**Protocolo y puerto:** normalmente puerto 22. Usa criptografía de clave pública para autenticar el servidor y, en algunos casos, al cliente: RSA o DSA para autenticación y AES para el cifrado de datos.

**Componentes:** cliente SSH, servidor SSH, shell remoto.

### Instalación y configuración
- **Cliente:** en Linux/Unix suele estar preinstalado. En Windows: PuTTY o activar el cliente OpenSSH en versiones recientes.
- **Servidor:** en Linux/Unix, `apt-get install openssh-server` (Debian). Configuración básica en `/etc/ssh/sshd_config`.

### Ejemplo de conexión básica (Windows → Ubuntu)
1. En el cliente Windows, abrir una consola de comandos.
2. Escribir `usuario@ipdestino`, por ejemplo `ssh usuario@192.168.230.19`.
3. Introducir la contraseña.
4. Se verá el *prompt* de la máquina Ubuntu.
5. Para salir: `exit`.

En el servidor debe estar instalado el servicio SSH. Si no, el error `ssh.service not found` lo indica, y se instala `openssh-server`:

```bash
sudo service ssh status    # estado del servicio
sudo service ssh start     # arrancarlo si estuviera caído
sudo apt install openssh-server
```

### Transferencia de archivos
```bash
scp archivo_local usuario@direccion_ip_del_servidor:/ruta/destino
# Ejemplo: copiar fichero1.txt a la carpeta dirUsuario
scp fichero1.txt usuario@192.168.230.19:/home/usuario/dirUsuario
```

### Cambiar el puerto por defecto
Da un nivel más de seguridad. En el servidor:
```bash
sudo nano /etc/ssh/sshd_config
```
Localizar `#Port 22`, cambiarlo al nuevo puerto (ej. 222) y guardar con Ctrl+O. Reiniciar el servicio:
```bash
sudo systemctl restart sshd
```
Puede ser necesario abrir el nuevo puerto en el firewall.

### Creación de túneles SSH
Túnel **local**: conecta un puerto local a otro en una máquina remota (útil, por ejemplo, para acceder a una base de datos tras un firewall).
```bash
ssh -L 3307:192.168.230.19:3306 usuario@host_ssh.com
```
Redirige el puerto 3307 de la máquina local al puerto 3306 de 192.168.230.19 a través de `host_ssh.com`; se accede al 3306 conectando a `localhost:3307`.

---

## 5.5. Telnet
Uno de los protocolos de red más antiguos que permitió la comunicación remota. En los ochenta y noventa fue vital para desarrolladores y administradores, pero la falta de seguridad lo hizo problemático. Hoy ha sido parcialmente sustituido por SSH, aunque aún se emplea en algunos sistemas. Telnet se refiere tanto al protocolo como al programa cliente.

**Protocolo y puerto:** conexión remota y gestión de dispositivos de red. Usa **TCP, puerto 23** por defecto. Transmite los datos **sin encriptar**.

**Componentes:** cliente Telnet (conecta e interactúa con el sistema remoto) y servidor Telnet (recibe conexiones y ejecuta comandos). Solo se usa en modo comando; el puerto 23 debe estar abierto en la máquina remota.

**Pasos de una conexión:**
1. Configuración de conexión: el cliente establece una conexión TCP con el servidor en el puerto 23.
2. Negociación: tipo de terminal, tamaño de pantalla y manejo de caracteres especiales.
3. Transmisión de datos: el cliente envía comandos y el servidor devuelve el resultado.
4. Cierre de conexión.

Para comprobar el cliente Telnet en Windows, abrir una consola en modo administrador y escribir `telnet IP puerto`. Si da error («"telnet" no se reconoce como un comando interno o externo»), hay que habilitarlo: *Panel de control > Programas > Programas y características > Activar o desactivar características de Windows* y marcar **«Cliente Telnet»**.

Ejemplo: `telnet 192.168.230.19 222`. Si el puerto 222 no está abierto: *Conectándose a 192.168.230.19...No se puede abrir la conexión al host, en puerto 222: Error en la conexión.* Si está abierto, aparece una consola con el *prompt* de Telnet.

**Resumen:** los datos (incluidos usuarios y contraseñas) viajan en texto plano, susceptibles de interceptación; por ello su uso ha sido limitado y sustituido en gran parte por SSH.

---

## A fondo
- **Conexión SSH Windows-Ubuntu.** El Rincón del Hacker. (2021, diciembre 3). [Vídeo]. https://www.youtube.com/watch?v=isqtKUFfV4k
- **Cómo crear un túnel SSH.** Tony Teaches Tech. (2022, mayo 17). *How to Make an SSH Proxy Tunnel* [Vídeo]. https://www.youtube.com/watch?v=F-ubwghsWPM
- **Comprobar puertos TCP remotos con un cliente Telnet.** DaveTutoriales. (2020, febrero 17). [Vídeo]. https://www.youtube.com/watch?v=vUURv74OPMU

---

## Entrenamientos
*Observación: los entrenamientos se realizan desde un cliente Windows hacia un servidor Ubuntu.*

### Entrenamiento 1 — Conexión Telnet al puerto 2224
Pasos: abrir consola (cmd) como administrador; usar `telnet direccion_ip_o_hostname puerto`; puede solicitar usuario o contraseña.
```
telnet 192.168.230.19 2224
```

### Entrenamiento 2 — Conexión SSH y cambio del puerto predeterminado
Pasos: establecer la conexión SSH; editar `sshd_config` (ej. con nano).
```bash
ssh usario@192.168.230.19
sudo nano /etc/ssh/sshd_config
```
Modificar `#Port 22` cambiando el 22 por el nuevo puerto; guardar con Ctrl+O.

### Entrenamiento 3 — Conexión SSH con el nuevo puerto
```bash
ssh -p 222 usuario@192.168.230.19
exit
```
`-p 222` especifica el puerto; `usuario` es el nombre de usuario en el servidor; `192.168.230.19` es la IP o el hostname.

### Entrenamiento 4 — Crear directorio y copiar un fichero
```bash
ssh usuario@192.168.230.19 -p 222
mkdir ~/nuevo_directorio     # crea el dir en home/usuario
exit                         # sale de la conexión ssh
scp /ruta/al/archivo/local.txt usuario@192.168.230.19:/home/usuario/nuevo_directorio/
```
> Nota: con `scp` y un puerto no estándar hay que indicar el puerto con `-P` (mayúscula), p. ej. `scp -P 222 ...`; el ejemplo del material no lo incluye.

### Entrenamiento 5 — Habilitar SSH, Telnet y VNC en Debian + firewall
**Tareas:** instalar y configurar SSH, Telnet y VNC; abrir los puertos en el firewall; verificar que cada servicio funciona con una conexión remota desde otra máquina.

```bash
# Instalación
sudo apt-get install openssh-server
sudo apt-get install telnetd
sudo apt-get install tightvncserver

# Firewall
sudo ufw allow 22/tcp
sudo ufw allow 23/tcp
sudo ufw allow 5900/tcp

# Estado de los servicios
sudo service ssh status
sudo service telnet status
sudo service vncserver status

# Conexión desde otro equipo
ssh usuario@ip_destino
telnet ip_destino 23
# VNC: cliente VNC con IP del servidor y puerto 5900
```
**Solución del material:** los servicios se instalan correctamente; los puertos 22, 23 y 5900 se abren con ufw; cada servicio puede verificarse y está activo; las conexiones remotas desde otra máquina de la red son exitosas.
