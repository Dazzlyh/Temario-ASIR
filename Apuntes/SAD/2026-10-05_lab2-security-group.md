---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-10-05
tema: Laboratorio 2 · ¿Se llega al servidor? · security group, ICMP, puertos, TCP/UDP
fuente: SAD_Lab02_Practica.pdf + SAD_Lab02_Comandos.pdf + apuntes de clase de Dani
---
# SAD · Laboratorio 2 (05/10) · ¿Se llega al servidor?

> Anterior: [Clase 3](2026-10-01_clase3-cid.md) · Profesor: Damián Sualdea (UNIR FP, sala 16070-2)

**Idea que hay que llevarse**: para usar un servicio hacen falta **DOS cosas a la vez**: que algo **escuche por dentro** y que una **regla lo deje pasar por fuera**. Si falta una, no se llega.

Notas de Dani en clase: AWS trae el firewall de serie con **todos los puertos cerrados salvo el 22 (SSH)**; el **Security Group (SG)** es el firewall de AWS; se abrió un puerto vacío y se lanzó nmap.

## Paso 0 · abrir sad1
AWS Academy → curso → Modules → Learner Lab → **Start Lab** (punto verde) → «AWS» → EC2 → Instances → sad1 (si *stopped*: Instance state → Start) → copiar **Public IPv4** (**cambia cada vez que se arranca**). Si sad1 no aparece, se terminó (Terminate) por error. **Al final SIEMPRE Stop, nunca Terminate.**

## 1 · ¿Se llega? (desde tu portátil)
```bash
ping -c4 <IP>                         # NO responde: ICMP cerrado
ssh -i labsuser.pem ubuntu@<IP>       # el 22 sí: entras
nmap -Pn -F <IP>                      # -Pn sin ping previo, -F solo puertos comunes (rápido)
ss -tlnp                              # (dentro, por SSH) lo que ESCUCHA la máquina
```
La máquina nunca ofrece por fuera más de lo que escucha por dentro, y casi siempre menos: lo recorta el SG.

## 2 · Activar el ping (ICMP)
SG → Inbound rules → Edit → Add rule → tipo **All ICMP - IPv4**, origen 0.0.0.0/0. Después `ping -c4 <IP>` → 0% packet loss.
El ping **no usa puerto**: usa el protocolo ICMP. «No responde al ping» **NO** es «está caído».

## 3 · Puerto vacío (lo importante)
1. Añadir regla Custom TCP 8080, origen 0.0.0.0/0 (sin levantar nada).
2. `nmap -p 8080 <IP>` → **closed** (la regla deja pasar, pero no hay servicio).
3. Dentro de sad1: `python3 -m http.server 8080`.
4. `nmap -p 8080 <IP>` → **open** (regla abierta + servicio escuchando). Ctrl+C para parar.

| nmap | Significa |
|---|---|
| **filtered** | Problema de **REGLA** (el cortafuegos ni contesta) |
| **closed** | Problema de **SERVICIO** (llega, pero no hay nadie dentro) |
| **open** | Las dos cosas en orden |

## 4 · TCP y UDP · HTTP y DNS
- **TCP** = como una llamada: conexión + confirmación de cada trozo (fiable). HTTP, puerto 80.
- **UDP** = gritar una pregunta y esperar respuesta, sin conexión (rápido, sin garantías). DNS, puerto 53.
```bash
sudo apt install -y apache2          # dentro de sad1; abrir 80 TCP en el SG
curl http://<IP>                     # TCP: baja la página entera
dig @8.8.8.8 unir.net +short         # UDP: una pregunta, una respuesta
```
La regla del SG distingue protocolo: abrir el 53 en TCP no sirve para un DNS que habla UDP. **El protocolo también forma parte de la puerta.**

## 5 · Cortar el paso (caída de red) y MTTR de red
1. Comprobar SSH. 2. Borrar la regla del 22 y **arrancar cronómetro**. 3. `ssh ...` → `Operation timed out` (caído desde la red, máquina viva). 4. Reañadir el 22 (SSH, 0.0.0.0/0), reconectar y **parar cronómetro** = MTTR de red.
Comparación con el miércoles: entonces cayó el **SERVICIO** (`systemctl start`); hoy el **CAMINO** (regla). **Se diagnostica en orden: primero si se llega, luego si responde.**

## 6 · Telnet vs SSH
Telnet (23) manda usuario y contraseña **en claro**; SSH (22) cifrado. La imagen de AWS trae solo SSH y **solo con clave**. Disponibilidad no es abrir todo: es dejar el camino justo y seguro.

## Entrada 02 del diario de incidentes (con números)
- Reglas tocadas (ICMP, 8080, 80, 22) y qué vio nmap en cada caso (filtered/closed/open).
- Segundos que el 22 estuvo inalcanzable = MTTR de red.
- Una línea: ¿qué DOS cosas deben cumplirse para usar un servicio?

## Antes de cerrar
Quitar reglas de prueba (8080 y 80); dejar solo el 22 (y ICMP si se quiere). Comprobar SSH. **Stop, nunca Terminate.**
Los comandos (ssh, nmap, ss) se repiten a propósito durante el curso. Al enseñar pantalla, tapar el último número de la IP.

## Pendiente
**Actividad 1: entrega lunes 19 de octubre** (si no se ha elegido incidente, ponerlo en el foro). El profesor la explica el miércoles 7/10.
