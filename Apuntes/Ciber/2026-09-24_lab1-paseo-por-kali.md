---
asignatura: Ciberseguridad
fecha: 2026-09-24
tema: Laboratorio 1 · un paseo por Kali (nmap, John, Hydra, Metasploit)
fuente: CIBER_Lab01_diapositivas.pdf + transcripción de la clase en directo
---
# Ciber · Laboratorio 1 (24/09) · Un paseo por Kali

> Anterior: [Clase 2](2026-09-22_clase2-pilares.md) · Siguiente: [Clase 3](2026-09-29_clase3-donde-falla-un-sistema.md)

## Cómo funcionan los laboratorios
- No se explica temario: se practica; lo no explicado se nombra y se aparca.
- No se entregan, no puntúan, no son segunda clase. Son **quincenales y se graban**.
- Hoy: ver «de qué es capaz la caja» de Kali.

## Qué es Kali y qué no
- **Es** un Debian con las herramientas de auditoría ya instaladas y configuradas (ahorra la tarde de instalar y ajustar ~40 programas).
- **No es** un sistema para el día a día, no te hace hacker y no hay que «aprendérselo»: lo que vale es saber qué herramienta coger y leer lo que devuelve.
- Regla del módulo: solo **scanme.nmap.org**, tu propia máquina/red y el servidor de prácticas. Lo demás puede ser delito (arts. 197 y 264).

## Cuatro herramientas de las seiscientas
| Herramienta | Para qué | Se ve a fondo en |
|---|---|---|
| nmap | Qué hay ahí fuera y qué versión | Actividad 2 |
| John the Ripper | Romper contraseñas a partir del hash | Clase 6 |
| Hydra | Probar contraseñas contra un servidor (SSH) | Actividad 3 |
| Metasploit | Explotar una vulnerabilidad | Clase 23 |

```bash
# nmap
nmap -sV scanme.nmap.org        # 22/tcp open ssh OpenSSH 6.6 · 80/tcp open http Apache 2.4.7
nmap -sn 192.168.1.0/24         # tu red: quién hay (host discovery)
# John the Ripper
echo '5f4dcc3b5aa765d61d8327deb882cf99' > hash.txt        # MD5 de "password"
john --format=raw-md5 --wordlist=rockyou.txt hash.txt
john --show --format=raw-md5 hash.txt                     # ?:password
# Hydra (contra el servidor de prácticas)
hydra -l padawan -P flojas.txt ssh://SERVIDOR             # 0 valid passwords found
hydra -l padawan -P fasttrack.txt ssh://SERVIDOR          # [22][ssh] login: padawan password: P@ssw0rd
# Metasploit
msf6 > search eternalblue
msf6 > use auxiliary/scanner/portscan/tcp                 # su propio nmap
msf6 > use auxiliary/scanner/ssh/ssh_login                # lo mismo que Hydra
msf6 > use exploit/.../ms17_010_eternalblue
msf6 > show options                                       # se configura; se lanza en la Clase 23
```
- Una contraseña débil cae porque **está en un diccionario**.
- En la nube (AWS) no se entra con contraseña sino con clave: por eso este ataque no vale ahí.
- «Kali trae seiscientas herramientas… usas tres y el resto están ahí por si acaso.»

Siguiente: Clase 3, apartados 1.3 a 1.5 (vulnerabilidades reales).

## Notas en directo (matices del profesor, no están en las diapositivas)

### Primer paso práctico: teclado en español
En Kali, por defecto el teclado viene en inglés (US). Antes de nada: abrir **Settings → Keyboard → Layout** y poner español, o los símbolos (como `@`) no salen donde se espera. Varios alumnos tuvieron problemas de conexión/escaneo en directo que resultaron ser de red local (routers, VPN, modo del adaptador de red de la VM), no de las herramientas en sí — el profesor insiste en que estas cosas "de directo" se depuran en casa con calma, no en clase.

### De dónde viene Kali (ampliación)
- Kali y Parrot son **Debian**; por eso `apt install`, `systemctl status`, etc. funcionan igual que en cualquier otra Debian — no es una distro con comportamiento raro.
- Otras familias de distros de seguridad que mencionó: **BlackArch** (basada en Arch), **BackBox**, **Parrot**, entre otras — todas con el mismo concepto: un sistema base + un montón de herramientas de auditoría preinstaladas.
- Opinión del profesor: como sistema operativo de uso diario, Kali "no le gusta nada" — es solo una caja de herramientas. Para el día a día prefiere Ubuntu o Manjaro.

### nmap — el escaneo real que se hizo en clase
```bash
nmap scanme.nmap.org              # básico: solo puertos abiertos (sin versión)
nmap -sV scanme.nmap.org          # añade un fingerprint: lanza tráfico extra para identificar
                                   # el software exacto detrás de cada puerto (Apache, OpenSSH...)
nmap -sn 192.168.1.0/24           # -sn: solo descubrir equipos vivos en la red local (sin puertos)
```
- `-sV` es más lento porque, además de ver el puerto abierto, manda tráfico adicional para intentar identificar la versión exacta del servicio.
- Al escanear la propia red de casa con `-sn`, aparecen todos los dispositivos conectados por wifi/cable (móviles, TV, robot aspirador, impresora, router...): con esto no se "sabe" qué es cada uno, nmap solo dice qué hay; identificar de qué dispositivo se trata es trabajo de deducción del auditor.
- Para saber el rango de la propia red: `ip a` o `ifconfig` y mirar la IP propia (ej. `192.168.1.64/24` → escanear `192.168.1.0/24`).
- Aviso práctico: copiar y pegar mal la URL de `scanme.nmap.org` (p. ej. con un espacio o parámetro de más) puede hacer que el escaneo se quede colgado indefinidamente — revisar bien el comando antes de lanzarlo.

### John the Ripper — de dónde salen los hashes y cómo se rompen
- Las contraseñas de los usuarios de Linux están **hasheadas** (no cifradas) en `/etc/shadow` (solo root puede leerlo: `sudo cat /etc/shadow`). El equivalente en Windows es el fichero **SAM**; en una base de datos, la tabla de usuarios (p. ej. `mysql.user`).
- Diccionarios de Kali: están en `/usr/share/wordlists/` y normalmente vienen comprimidos (hay que descomprimir `rockyou.txt.gz` la primera vez que se usan — en algunas versiones de Kali esto se hace desde un acceso directo llamado **Wordlists** dentro de la categoría **Password Attacks**, en otras hay que descomprimir a mano).
- Flujo real en clase: se copió un **hash MD5** en un fichero `hash.txt` dentro del directorio personal, y se rompió así:
```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou/rockyou.txt hash.txt
john --show --format=raw-md5 hash.txt     # muestra la contraseña ya rota: patchwork
```
- Cómo funciona por dentro: John coge una palabra del diccionario, le calcula el hash, lo compara con el hash objetivo; si no coincide, prueba la siguiente — así con todo el diccionario hasta encontrar coincidencia (o agotarlo).
- El profesor adelanta que más adelante se verá cómo **detectar automáticamente el tipo de hash** sin tener que saberlo de antemano.

### Hydra — fuerza bruta contra el SSH del servidor del profesor
Demo en directo contra el servidor del profesor (usuario creado al vuelo: `padawan`):
```bash
# diccionario de contraseñas "flojas" (pocas, de prueba) creado a mano con printf
hydra -l padawan -P flojas.txt ssh://IP_SERVIDOR          # con un diccionario pequeño: 0 resultados
hydra -l padawan -P /usr/share/wordlists/fasttrack.txt ssh://IP_SERVIDOR   # diccionario más grande: sí
```
- Resultado real: con el diccionario grande (fasttrack), Hydra encontró la contraseña del usuario `padawan` (contraseña usada en la demo: `patchword`/`passwork` según el momento — el profesor tecleó variantes en directo). Varios alumnos consiguieron entrar por SSH con la contraseña encontrada:
```bash
ssh padawan@IP_SERVIDOR     # y la contraseña que ha sacado Hydra
```
- El propio profesor avisó de que su antivirus/IDS podía saltar por el ataque de fuerza bruta en directo (varios alumnos atacando el mismo servidor a la vez desde IPs distintas).
- Tras la demo, el profesor **borró el usuario de prueba** del servidor (no persiste para hacerlo en casa con ese mismo servidor).

### Metasploit (`msfconsole`) — primer vistazo
```bash
msfconsole
search vsftpd                                    # buscar por nombre de servicio/versión encontrados con nmap
search eternalblue                               # o por el nombre del fallo
use exploit/windows/smb/ms17_010_eternalblue      # EternalBlue (el de WannaCry)
show options                                      # qué datos pide el módulo
set LPORT 3333                                    # cambiar el puerto local de la conexión de vuelta, por ejemplo
show options                                       # comprobar que ha quedado configurado
exit                                               # salir de msfconsole
```
- Al arrancar, Metasploit carga más de **2.355 exploits** (cifra que dio en clase) más un montón de **módulos auxiliares** (escaneo de puertos, fuerza bruta de login — lo mismo que hace Hydra, pero integrado), **payloads**, **encoders** (evasión) — "una caja dentro de una caja": una vez dentro, se hace casi todo con la sintaxis propia de Metasploit sin salir de la consola.
- Flujo de trabajo típico: 1) recon con nmap → 2) con el servicio/versión encontrado, `search <nombre>` en Metasploit → 3) `use <módulo>` → 4) `show options` → 5) `set <OPCIÓN> <valor>` → 6) (lanzar, solo con permiso).
- Libros que mencionó el profesor sobre Metasploit: **"Metasploit para Pentesters"**, de **Pablo González** (0xWord) — hay varias ediciones.

### Repaso del orden de trabajo (lo confirma el profesor al final)
Antes del `fingerprinting` (identificar versiones con `nmap -sV`), hay una fase de **reconocimiento/footprinting** (qué hay, desde fuera); después de identificar versiones se buscan vulnerabilidades (NVD/CVE Details, ya visto en la Clase 3) y solo entonces se explota (Metasploit). Esa secuencia completa —descubrimiento → footprinting → fingerprinting → vulnerabilidades → explotación— es la que se irá viendo pieza a pieza en las siguientes clases y laboratorios.
