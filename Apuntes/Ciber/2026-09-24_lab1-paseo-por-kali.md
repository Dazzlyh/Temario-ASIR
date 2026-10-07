---
asignatura: Ciberseguridad
fecha: 2026-09-24
tema: Laboratorio 1 · un paseo por Kali (nmap, John, Hydra, Metasploit)
fuente: CIBER_Lab01_diapositivas.pdf
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
