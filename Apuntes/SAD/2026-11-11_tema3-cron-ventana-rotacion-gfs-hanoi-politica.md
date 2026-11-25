---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-11-11
tema: "Tema 3 · Sesión 9: automatizar copias con cron, `tar` frente a `rsync`, RPO/RTO, ventana de copia, rotación (GFS y torres de Hanoi) y política de copias; simulacro y Actividad 2"
fuente: transcripción de la clase (1 h 30 min) + **PDFs del profesor recibidos el 25/11**: diapositivas `SAD_Clase09_diapositivas.pdf` (27 págs.) y guía `SAD_Clase09_Practica.pdf` (2 págs.). Contrastado con el Tema 3 del temario (3.2, 3.3, 3.4 y los entrenamientos 3 y 5) y con fuentes externas marcadas (web). Donde el PDF y el audio difieren, manda el PDF.
---
# SAD · Tema 3, sesión 9 (11/11) · cron, ventana de copia, rotación y política de copias

> Anterior: [Tema 3, sesión 8 (4/11): copias 3-2-1, tar, rsync, snapshot, S3](2026-11-04_tema3-copias-3-2-1-tar-rsync-snapshot.md) · Siguiente: [Repaso Temas 1-3 y simulacro (18/11)](2026-11-18_repaso-simulacro-temas-1-2-3.md) · Profesor: Damián Sualdea Soy

Es la **última clase con contenido nuevo** de SAD este trimestre: cierra el Tema 3. El 4/11 se hicieron las copias **a mano**; hoy se **automatizan** con `cron` y se deciden las preguntas de diseño: **cada cuánto** (RPO), **cuándo** (ventana de copia), **cuánto tiempo se guardan** y **cómo se rotan** (GFS u Hanoi). El profesor remata con la **política de copias** y con el simulacro y la Actividad 2.

Convención: **(clase)** = audio, **(temario)** = Tema 3 del repo, **(web)** = fuente externa, **(mío)** = añadido por mí.

> [!note] Actualización 25/11: PDFs recibidos
> Esta nota se hizo primero solo con el audio. Con las **diapositivas** y la **guía de la práctica** ya recibidas, he **corregido las líneas de `crontab`** (la completa es a las **3:00**; la «incremental» de lunes a sábado es **`rsync -a` sin `--delete`**; no hay subcarpeta `completa/`), he **cerrado la política de ejemplo** (hito mensual) y he **aclarado el calendario** (repaso el 18/11 y laboratorio movido a diciembre). La guía de la práctica está resumida en la **Tarea 5.9**.

## Lo imprescindible

> [!important] Chuleta
> - **`cron`** es el **demonio** que ejecuta tareas a su hora; **`crontab`** es el **comando** para editar (`-e`) y listar (`-l`) la tabla de tareas.
> - **5 campos, de izquierda a derecha:** `minuto hora díaDelMes mes díaDeLaSemana`. `*` = siempre. **Domingo = 0**, lunes = 1… sábado = 6. No hay año.
> - En `crontab`, **`%` hay que escribirlo `\%`** (si no, cron se lo "come"): `$(date +\%F)`.
> - **`tar` empaqueta** (con `z`, además comprime); **`rsync` sincroniza** y solo copia lo cambiado. **tar no es compresión.**
> - **RPO** = cuántos datos puedo perder → manda la **frecuencia**. **RTO** = cuánto tardo en volver.
> - **Ventana de copia** = franja en la que se puede copiar sin molestar (madrugada). **La copia tiene que caber en la ventana**; si no cabe, se hace **incremental**.
> - **Rotación:** **GFS** (abuelo-padre-hijo) = intuitiva; **torres de Hanoi** = más eficiente pero más difícil de llevar a mano.
> - **Hay que probar la restauración** (otra vez GitLab). "La mejor copia es la que se hace sola."
> - **Examen/simulacro:** el profesor **pondrá líneas de `crontab` para interpretar** (qué hace cada campo y cada opción).

## Tarea 1 · Diferencias entre `tar` y `rsync`

| | `tar` | `rsync` |
|---|---|---|
| **Qué hace** | **Empaqueta** una carpeta en **un único fichero**; con `z` lo **comprime** (gzip) | **Copia/sincroniza** una carpeta en otra ("espejo") |
| **Resultado** | Un fichero `.tar.gz`, con la fecha en el nombre | Una carpeta destino con los ficheros sueltos |
| **Al repetirlo** | Crea **otro paquete completo** cada vez | **Solo copia lo que ha cambiado**: la segunda vez apenas copia nada (muy rápido) |
| **Versiones** | Una por cada fichero fechado | **Una sola**: el estado actual (con `--delete`, también refleja los borrados) |
| **A otra máquina** | Se mueve el `.tar.gz` (p. ej. con `scp`) | Puede **conectarse a otra máquina** y copiar allí |
| **Uso en clase** | **"La foto completa"** de cada día | Copia **diaria** tipo espejo |

> [!important] Lo que repitió el profesor
> **`tar` no es compresión**: es **empaquetar todo en un paquete** para moverlo cómodamente; lo que se suele hacer es **comprimirlo además** (`z`). Y el "archivar" es un nombre engañoso: `tar` **empaqueta**.

### Comandos y opciones (clase)
```bash
tar -czf copia_$(date +%F).tar.gz carpeta     # (clase) completa, comprimida, con fecha en el nombre
rsync -a --delete origen/ destino/            # (clase) espejo exacto
```
- **`tar -czf`**: `c` crea el paquete, `z` lo comprime con gzip, `f` indica el fichero de salida. El nombre debe acabar en **`.tar.gz`**. Con `$(date +%F)` el nombre lleva la fecha y **no se pisan** las copias.
- **`rsync -a`** (modo archivo): copia las carpetas **recursivamente** y **conserva permisos, dueño y fecha**, para que la copia sea idéntica al original y no "ficheros sueltos con otra fecha". El temario lo desglosa: `-a` = `-rlptgoD` (temario, Entrenamiento 5).
- **`--delete`**: deja el destino como **espejo exacto**: **lo que borras en el origen desaparece de la copia**. "Útil, pero peligroso si te equivocas en el origen."
- **La barra final** del origen: `datos/` copia **el contenido**; `datos` (sin barra) copia **la carpeta dentro**. "Siempre ponemos la barra para copiar todo."

> [!warning] "Incremental" no es lo mismo que "solo transfiere lo cambiado"
> El profesor sigue llamando "incremental" al `rsync` ("como incremental: la segunda vez apenas copia nada"). Eso describe la **transferencia**, no el **tipo de copia** del temario (completa/incremental/diferencial). Con `rsync -a --delete` solo hay **una copia, la del último estado**, **sin historial**: si borras algo por error el lunes, la ejecución del martes **también lo borra de la copia**. **(mío)** Para versiones: `rsync --link-dest` (instantáneas con enlaces duros) o, con `tar`, `--listed-incremental` (incrementales reales de GNU tar). No los vimos ni los he probado.

> [!note] Cierra una duda del 4/11
> En la nota anterior quedó sin confirmar si había usado `--delete`. Hoy lo **dicta** (`rsync -a --delete`), así que es **probable** que el 4/11 fuera lo mismo.

## Tarea 2 · RPO y RTO

- **RPO** (*Recovery Point Objective*) = **cuántos datos podemos perder**, medido en tiempo. "Una cosa es el tiempo y otra lo que perdemos."
  - Si podemos perder hasta **24 h**: **copia diaria**.
  - Si no podemos perder más de **una hora**: **copia cada hora**.
  - **Cuanto menor es el RPO, más copias** hay que hacer.
- **RTO** (*Recovery Time Objective*) = **el tiempo que tardas en volver** a funcionar.
  - Lo que interesa es que **la copia más cercana sea la que antes levante**.
- **Cómo se decide:** depende del dato y de cuánto cambia. Los ejemplos de siempre: un **supermercado** (todas las ventas y devoluciones: RPO muy bajo), una **gestoría** (pocas cosas pero importantes) y una **academia normal** (solo importan los meses).
- **Cómo medir el RTO real (clase):** levantar **un servidor aparte** desde la copia y cronometrar. **(mío)** Para medir la copia, `time tar ...`.

> [!note] Audio confuso
> Dice que con una copia total "voy a tardar mucho" y que dos incrementales "ayudan", pero la frase no se entiende (no queda claro si habla de **hacer** la copia o de **restaurarla**). El temario (3.2) es claro: la **incremental es más rápida de hacer y más lenta de restaurar** (cadena completa + todas las incrementales), y la diferencial restaura con solo dos piezas.

## Tarea 3 · Ventana de copia: cuándo se hace y cuánto tarda

**Ventana de copia** = **a qué hora** se puede hacer la copia sin molestar. Es un punto que, según el profesor, "ojo, esto es muy importante".

- **Cuándo (clase):** de **madrugada** (2–3 h), "cuando nadie usa el sistema, la copia no compite con el trabajo y no compromete el servicio". **No a las 8 de la mañana.**
- **Depende del tipo de empresa:** si trabaja en **turnos que se encadenan por zonas horarias** (soporte "que no cubre el sol"), no hay madrugada tranquila. El profesor no recordaba el nombre de ese modelo; **(mío)** es **"follow the sun"** (sin confirmar que sea al que se refería).
- **Cuidado con las actualizaciones:** Windows actualiza el **segundo martes del mes** (*Patch Tuesday*) y **el miércoles** muchos equipos están actualizándose o reiniciando. Planifica la copia para no pisarse con eso. **(clase)** Y lo mismo con las actualizaciones del sistema ("a las 2 de la mañana").
- **Cuánto tarda (lo más importante):** la copia **tiene que caber en la ventana**.
  - Ejemplo del profesor: **si la copia total tarda 6 h y la ventana es de 4 h, no cabe: hay que hacer incrementales.** "Ya está, no hay más."
- **Fórmula que prefiere (clase):** **completa el fin de semana** (hay más tiempo) e **incrementales entre semana**. "Me parece la más óptima que hay", pero "todo depende".
- Por eso `crontab` distingue los **días de la semana** (domingo = 0 … sábado = 6).
- **Servidor encendido o apagado:** con la copia **en frío** hay que parar el servicio, y eso cuenta para la ventana (ver la sesión del 4/11).

## Tarea 4 · Cuánto tiempo se guardan: retención y rotación

### El problema: "Diógenes digital"
No se puede guardar todo para siempre: **te quedas sin espacio**. Hay que **decidir cuánto vive cada copia** y organizarlas. Idea guía: **muchas copias recientes** (por si el fallo es de ayer) y **pocas antiguas**; cuanto más viejas, menos detalle.

### Cuánto tiempo conservar datos personales (clase + web)
El profesor lo plantea como pregunta abierta y lo liga a la normativa: **RGPD**, la **LOPDGDD** y la **AEPD**.
- **Lo que dijo:** "creo que son 3 años… habría que mirarlo"; los **vídeos e imágenes van por otro lado**. También habló de **notificar una brecha en "32 h"** (audio).
- **(web) Lo que encuentro:**
  - **No hay un plazo universal**: lo fija la finalidad y la normativa sectorial; rige el principio de **limitación del plazo de conservación** (art. 5.1.e del RGPD).
  - La **LOPDGDD (art. 32)** obliga a **bloquear** los datos al suprimirlos: se conservan, con acceso restringido, **solo para atender responsabilidades y durante el plazo de prescripción**; luego se destruyen. Las infracciones **muy graves prescriben a los 3 años**, las **graves a los 2** y las **leves al año** (arts. 72–74). **Es probable que de ahí venga su "3 años"**, pero no es una regla general.
  - **Videovigilancia:** supresión en **un mes** como máximo (art. 22.3 LOPDGDD).
  - **Brechas:** el plazo de notificación a la AEPD es de **72 horas** desde que se tiene constancia (art. 33 RGPD), **no 32**. **Es probable que sea un lapsus o un fallo de la transcripción**; para el examen, **72 h**.
- **Sin confirmar:** qué esperaría el profesor en el examen sobre esto; solo lo planteó como contexto.

### Técnica 1 · GFS (abuelo-padre-hijo)
GFS = *Grandfather-Father-Son*. (El audio lo transcribe "G. P. S.": **es el esquema abuelo-padre-hijo**.)

| Nivel | Copia | Se guardan (clase) | Cubre |
|---|---|---|---|
| **Hijo** (*son*) | **Diaria** | 5 o 7 | La semana |
| **Padre** (*father*) | **Semanal** (en el ejemplo, la del viernes) | 4 o 5 | El mes |
| **Abuelo** (*grandfather*) | **Mensual** ("la importante") | 12 | El año |

- Con **pocas copias** (**(mío)** unas 21–24) cubres **desde ayer hasta hace un año**, y puedes recuperar **un día de esa semana, una semana de ese mes o un mes del año**.
- Lo que valora el profesor: **está ya planificado, no hay que pensar**; se programa con `cron`.
- Su veredicto: **es muy intuitivo, pero no es el más eficiente.**
- **(web)** En la versión habitual, el hijo suele ser una incremental o diferencial, y el padre y el abuelo, completas; el abuelo suele guardarse **fuera del sitio**.
- **(temario)** Solo lo nombra en 3.4: "implementar esquemas de rotación (por ejemplo, el esquema de abuelo-padre-hijo)".

### Técnica 2 · Torres de Hanoi
Se basa en el **puzle de las torres de Hanoi**: cada **soporte (nivel)** equivale a un disco y cada **sesión de copia**, a un movimiento.

- **Idea (clase):** **cada soporte se reutiliza a un ritmo distinto**: uno **muy a menudo**, otro **a la mitad de ritmo**, y el siguiente **a la mitad que el anterior**.
- Con **muy pocos soportes** ("5 niveles") guardas **copias repartidas en el tiempo**: de ayer, de hace unos días, de hace unas semanas, **sin gastar un soporte por día**.
- Su veredicto: **es más eficiente en coste**, pero **es difícil llevarlo a mano** (audio confuso en esa frase).

**(temario y web, comprobado)** El patrón es el del puzle: el nivel 1 se usa cada **2** sesiones (1, 3, 5, 7…), el nivel 2 cada **4** (2, 6, 10…), el 3 cada **8** (4, 12, 20…), el 4 cada **16**, etc.

| Soportes (niveles) | Secuencia de uso | Retrocedes hasta |
|---|---|---|
| 3 | A B A C A B A C… | 4 días |
| 4 | A B A C A B A D… | 8 días |
| 5 | A B A C A B A D A B A C A B A E… | 16 días |

(Con *n* soportes tienes copias de hace 1, 2, 4, 8… 2^(n−1) días. **(mío)** Un ciclo completo de *n* niveles tiene 2^n − 1 sesiones: 31 para 5 niveles, que es el ejercicio del Entrenamiento 3 del temario.)

**Variante del temario (3.3):** asigna **tipos de copia a los niveles**. Con 4 niveles: el **último** nivel es **completa**, los **intermedios** (2 y 3) **diferenciales** y el **primero** (1) **incremental**. Una copia **no se borra mientras otras dependan de ella**. El **período de recuperación** (días garantizados) con 4 niveles va de **4 días** (peor caso) a **11 días** (mejor caso). Requiere **software especializado** (el temario cita Acronis Backup) y **sirve para pequeñas empresas que quieren ahorrar coste y necesitan restauraciones completas**.

### GFS frente a Hanoi
| | GFS | Hanoi |
|---|---|---|
| **Facilidad** | **Muy intuitiva** | Más compleja; en la práctica, con software |
| **Historial** | Escalonado y fácil de explicar: día / semana / mes | Repartido en potencias de 2 |
| **Soportes** | Más (≈ 21–24 copias en el ejemplo) | **Muy pocos** para el historial que da |
| **Cuándo** | La que más se usa y la que "siempre trabajamos" | La que "mejor gestiona" muchas copias |
| **Aviso (web)** | — | En la versión clásica hay un backup casi diario completo, y eso exige ventana de copia amplia |

> [!note] Elegir una
> El profesor: "elegimos una u otra"; si quieres algo más eficiente, Hanoi (y "seguro que habrá otra más eficiente por ahí"). Para el examen: **saber explicar las dos y cuándo conviene cada una.**

## Tarea 5 · `cron`: automatizar la copia

### 5.1 Qué es y por qué (clase)
- **`cron` es un demonio** (*daemon*): un programa que **corre siempre en segundo plano** y **lanza tareas a la hora que le digas**, sin que estés delante. Está en **todos los Linux**.
- **Por qué automatizar:** el **error humano**. Acordarse de conectarse por SSH, hacer el `tar`, comprimirlo… "a las 3 de la mañana un viernes" no es fiable. Lo que se hace: **probar la copia a mano, automatizarla y dejar guardado cómo se hace y cómo se recupera.**
- **Equivalentes (clase y diapositiva 24):** **Windows**: *Programador de tareas*, *Copias de seguridad* y `robocopy`. **macOS**: *Time Machine* y `launchd` (o `cron`). Hoy se centra en **Linux** porque es el servidor que hay que proteger (SAD1).
- **Diferencia:** `cron` = el servicio; **`crontab`** = la instrucción para **programarlo** (cada usuario tiene su tabla).

### 5.2 Comandos (clase)
```bash
crontab -e      # editar la tabla del usuario (la primera vez pide editor: elegir nano)
crontab -l      # listar lo programado (comprobar que está guardado)
```
- **(mío, web)** **`crontab -r` borra TODA la tabla sin pedir confirmación.** El profesor prefiere **desactivar** poniendo **`#` delante** de las líneas (los comentarios se ignoran), y así lo hizo al final de la clase.
- Cada línea = **una tarea**: los 5 campos de tiempo y después el **comando**.

### 5.3 Los cinco campos
```
┌───────── minuto (0–59)
│ ┌─────── hora (0–23)
│ │ ┌───── día del mes (1–31)
│ │ │ ┌─── mes (1–12)
│ │ │ │ ┌─ día de la semana (0–6, domingo = 0)
│ │ │ │ │
* * * * *  comando
```
- Se leen **de izquierda a derecha**; **`*` = "cada / siempre"**.
- El día de la semana empieza en **domingo (0)**, "como la semana en EE. UU." (el audio lo dice mezclado, pero la regla es esa). **(web)** El **7** también es domingo, y se admiten nombres (`sun`).
- **Operadores (clase y web):** `-` **rango** (`1-5`), `,` **lista** (`1,15`), `/` **paso** (`*/15` = cada 15).
- **(web)** Si restringes **a la vez** día del mes y día de la semana, la tarea corre cuando **cualquiera** de los dos coincide, no los dos.

**Ejemplos del profesor:**

| Línea de tiempo | Significa |
|---|---|
| `30 2 * * 1-5` | A las **2:30**, de **lunes a viernes**, todos los meses |
| `0 2 * * *` | **Todos los días a las 2:00** |
| `0 3 * * 0` | **Domingos a las 3:00** |
| `30 1 1 * *` | **El día 1 de cada mes** a la 1:30 |
| `*/15 * * * *` | **Cada 15 minutos** (para algo muy crítico) |
| `* * * * *` | **Cada minuto** (solo para pruebas) |

(En clase usaron un **generador de crontab** web, no dicho en el audio, que traduce la expresión y **muestra la siguiente ejecución**; sirve para comprobar.)

### 5.4 Prueba sencilla: una tarea cada minuto (clase)
```bash
crontab -e
# se añade esta línea (diapositiva 15; cada minuto):
* * * * * echo "hola, soy cron: $(date)" >> /home/ubuntu/cron_prueba.txt
```
- **`echo`** escribe el mensaje; **`$(date)`** lo sustituye por la **fecha y hora del sistema** (con **paréntesis**: el profesor se equivocó al principio con **llaves `${date}`**, "vengo de Java", y no funcionó hasta corregirlo).
- **`>>`** **añade al final** del fichero; con **un solo `>`** se **sobrescribe** ("se carga lo anterior").
- **Hay que esperar un minuto**: el fichero **no existe** hasta la primera ejecución.

Para ver cómo crece:
```bash
tail -f /home/ubuntu/cron_prueba.txt    # (clase) -f = "follow": se queda enganchado y muestra las líneas nuevas; salir con Ctrl+C
```
(Un alumno propuso **`watch -n <segundos> <comando>`**, que repite un comando cada cierto tiempo; el profesor prefiere `tail -f`.)

### 5.5 Comprobar que cron ha ejecutado la tarea
```bash
crontab -l                                  # (clase) lista lo programado
grep CRON /var/log/syslog | tail            # (clase) busca CRON en el log del sistema y muestra lo último
```
- `grep CRON /var/log/syslog` filtra las líneas de cron y **`tail`** deja **las últimas**. Se ve cuándo se lanzó cada tarea. Cuidado: en directo faltaba una `s` ("**syslog**").
- **(mío, sin probar)** En Ubuntu también: `journalctl -u cron`, y `systemctl status cron` para ver que el servicio corre.
- **(clase)** `ls -l` da el detalle y **`-h`** lo hace legible para humanos (tamaños).

### 5.6 La copia real con rsync cada 2 horas (clase)
```bash
crontab -e
0 */2 * * * rsync -a --delete /home/ubuntu/datos/ /home/ubuntu/copias/espejo/    # (solo audio: NO está en las diapositivas ni en la guía; el campo «cada 2 h» es audio confuso)
```
- Ya probado a mano: ahora solo es **meterlo en `cron`**. Se comprueba con `crontab -l`.

### 5.7 Política completa: completa semanal + diaria · **(PDF: diapositiva 21 y guía, paso 3)**
```cron
# completa cada domingo a las 3:00
0 3 * * 0 tar -czf /home/ubuntu/copias/completa-$(date +\%F).tar.gz -C /home/ubuntu datos
# incremental de lunes a sábado a las 2:00
0 2 * * 1-6 rsync -a /home/ubuntu/datos/ /home/ubuntu/copias/espejo/
```
- **Completa: domingos a las 3:00** (el audio dudaba entre 2:00 y 3:00; **el PDF dice 3:00**). Sin subcarpeta `completa/`: el fichero va directo a `~/copias/` con nombre **`completa-AAAA-MM-DD.tar.gz`** (con guion).
- **«Incremental»: `rsync -a` SIN `--delete`** (mi reconstrucción anterior lo ponía con `--delete`). La diaria del paso 2 (`0 2 * * * rsync -a --delete …`) **es la que se sustituye** por estas dos: la guía dice «edita otra vez el crontab y deja estas dos».
- **`-C /home/ubuntu datos`**: cambia a esa carpeta antes de empaquetar, así el paquete guarda la ruta **relativa** `datos/...`. En directo **se le olvidó el `-C`** y un alumno se lo señaló.
- **`\%F`**: en `crontab`, **`%` es un salto de línea**, así que se **escapa con `\`**. **Guía: «si te saltas la barra, la tarea de la copia completa fallará en silencio»**. **(web)** Está en `man 5 crontab`.
- **`+%F`** da **`AAAA-MM-DD`** (**(mío)**: el profesor lo llama «formato día mes año»; es año-mes-día).
- **Rutas absolutas** siempre en `cron` (el temario, Entrenamiento 5, lo exige: «usa la ruta completa»). **(mío)** Que `~/copias` exista.
- En la línea de la guía, el `crontab` se ve partido en dos líneas por el formato del PDF; en el fichero real va **todo en una sola línea**.

> [!warning] Matiz (mío)
> Un `rsync -a` sin `--delete` **no propaga borrados** al espejo (queda el fichero borrado), pero sigue siendo **un solo estado**, **sin historial de versiones**. La **completa del domingo** es la única copia **fechada**. Es una **política razonable de partida**, no la incremental del temario.

> [!important] El profesor lo pondrá en el examen
> "No os voy a pedir que hagáis esto. **Quiero que interpretéis comandos.**" Dijo que pondrá en el **simulacro** una línea de `crontab` que **comprime con `tar`** o usa `rsync` y que hay que explicar: "así va un poco el examen". Práctica: coge cada línea de arriba y explica **cuándo se ejecuta**, **qué hace cada opción** y **dónde deja el resultado**.

### 5.8 Para terminar la clase
- **Antes de irte, para el cron**: edita (`crontab -e`) y **pon `#` delante de cada línea**. Sobre todo la de **cada minuto**, que va llenando el fichero.
- Si dejas el resto encendido, **a la semana siguiente** puedes ver si ha funcionado (`grep CRON ...`, y la carpeta de copias).

### 5.9 La guía de la práctica, paso a paso · **(PDF: guía de la Clase 9)**
Requisitos: laboratorio de AWS Academy arrancado, `sad1` en marcha, SSH, y las carpetas `~/datos` y `~/copias` de la práctica anterior (si no, `mkdir -p ~/datos ~/copias` y mete algún fichero).

1. **Abrir la lista de tareas:** `crontab -e`. La primera vez pregunta el editor: **elige `nano` (opción 1)**.
2. **Copia diaria:** añade `0 2 * * * rsync -a --delete /home/ubuntu/datos/ /home/ubuntu/copias/espejo/` (espejo cada día a las 2:00). Guardar en nano: **Ctrl+O, Enter, Ctrl+X**. Comprobar con `crontab -l`.
3. **Política en dos líneas** (completa semanal + incremental diaria): las del apartado 5.7.
4. **Comprobar de verdad que se ejecuta:**
   ```bash
   date                                   # hora actual del servidor
   crontab -e                             # pon una copia para dentro de 2 minutos, p. ej.:
   37 14 * * * rsync -a /home/ubuntu/datos/ /home/ubuntu/copias/prueba/
   grep CRON /var/log/syslog | tail       # ¿la lanzó cron?
   ls -lh /home/ubuntu/copias/prueba/     # ¿están los ficheros, con la fecha de ahora?
   ```
   «Una tarea programada que nadie comprueba es una tarea que no existe» (diapositiva 22).
5. **Montar tu política** (es, literalmente, el apartado de copias de la **Actividad 2**; «no hay una única respuesta correcta», pero tiene que salir de tu **RPO** y tu **RTO**):

| Qué se copia | Cada cuánto | Se guarda | Dónde |
|---|---|---|---|
| **Datos (incremental)** | Diaria, 2:00 (`cron`) | **1 semana** | Disco aparte (diapositiva: «+ otra máquina») |
| **Sistema (completa)** | Semanal, domingo | **1 mes** (GFS) | **Snapshot de AWS** |
| **Hito mensual** | Día 1 de cada mes | **1 año** | **Snapshot archivado** |

Es un **GFS**: hijo = diaria (1 semana), padre = semanal (1 mes), abuelo = mensual (1 año).

> [!important] Antes de cerrar (guía)
> 1. **Deja en el crontab solo las tareas buenas** (quita la de prueba de los 2 minutos; la de «cada minuto» de clase, también).
> 2. **Apaga la instancia con *Stop* (NO *Terminate*).**
> 3. **Apunta en el «diario de incidentes»:** qué copias has programado, a qué hora y cómo comprobaste que corrían.

**Dos datos más de las diapositivas:** `cron` **no baja de un minuto** («no existe "cada 5 segundos"»), y hay webs como **crontab.guru** para no fallar con la sintaxis.

## Tarea 6 · La política de copias (cierre)

El profesor cierra: "con la información que tenemos somos capaces de ir a cualquier empresa y **montar una política completa de copias**", rellenando una **tabla**. Los elementos que se decidieron:

| Qué se decide | Cómo se resolvió en clase |
|---|---|
| **Tipo de datos** | Qué es crítico y cuánto cambia |
| **Sistema** | Con qué se copia: `tar`, `rsync`, snapshot de AWS, S3 |
| **Frecuencia** | Según el **RPO**: diaria + completa semanal |
| **Ventana** | **Madrugada**; y que **quepa** |
| **Rotación y retención** | **GFS** (o Hanoi) |
| **Dónde (3-2-1)** | **Disco aparte y otra máquina**, más una copia fuera |
| **Automatización** | **`cron`** |
| **Pruebas** | **Restaurar siempre**, de forma periódica |

**Política de ejemplo · diapositiva 25 y guía (cierra el audio confuso)**

| Qué | Cada cuánto | Se guarda | Dónde |
|---|---|---|---|
| Datos (incremental) | Diaria, 2:00 (`cron`) | 1 semana | Disco aparte **+ otra máquina** (regla 3-2-1) |
| Sistema (completa) | Semanal, domingo | 1 mes (GFS) | Snapshot de AWS |
| **Hito mensual** | **Día 1 de cada mes** | **1 año** | **Snapshot archivado** |

«Esta tabla es, entera, el apartado de copias de la Actividad 2. Si la sabes rellenar para un servidor, tienes esa parte hecha.» (En el audio dijo también **S3**; no está en la tabla del PDF.)

> [!important] Mensajes de cierre
> - **El backup es "la única medida" que permite levantarte dentro de un RPO y un RTO.** Esto es **seguridad pasiva**: "nos van a dar" un incidente, y hay que estar preparados.
> - **GitLab otra vez**: copias que se hacían y nunca se probaron. **Siempre pruebas de restauración cada cierto tiempo.** Todo esto se llama **política de copias**.
> - La alta disponibilidad aparece de pasada, pero **"no entra bien"** todavía: viene después.
> - **"La mejor copia es la que se hace sola, se guarda con cabeza y se prueba."** Y se hace despacio: dejarla una semana funcionando, y luego **levantar un servidor aparte y ver cuánto tardas**.
> - **No hubo restauración real ni 3-2-1 completo** hoy (el 4/11 se anunciaron): el profesor lo ata a la **Actividad 2**.

**En el temario (3.4)** la política tiene tres bloques: **evaluación inicial** (datos críticos, retención y requisitos legales, riesgos), **definición** (objetivos, frecuencia, tipos, medios, retención y rotación con el ejemplo abuelo-padre-hijo) e **implementación** (herramientas, configuración y automatización, seguridad de las copias). Es la lista que encaja con la tabla de arriba.

## Si algo no funciona

| Síntoma | Causa probable | Arreglo |
|---|---|---|
| La tarea no se ejecuta nunca | Sintaxis mal, o ruta relativa | `crontab -l`; rutas **absolutas**; comprobar el log (`grep CRON /var/log/syslog \| tail`) |
| Error con la fecha en `crontab` | `%` sin escapar | **`\%F`** |
| Sale `${date}` literal o vacío | Se usaron llaves | **`$(date)`** |
| El fichero de prueba no aparece | No ha pasado un minuto | Esperar; luego `tail -f` |
| `tar` no crea nada | La carpeta de destino **no existe**, o falta `-C` | `mkdir -p`; revisar la línea |
| `rsync` crea `espejo/datos/` | Falta la **barra final** en el origen | `datos/` con barra |
| `rsync` borra lo que no debía | `--delete` con origen equivocado | Probar antes con `--dry-run` (**(mío)**) |
| El fichero de prueba crece sin parar | La tarea cada minuto sigue activa | `crontab -e` y **comentar con `#`** |
| `grep` no encuentra nada | Falta una letra en **`syslog`**, o el sistema usa `journalctl` | Revisar el nombre; `journalctl -u cron` |

## Dudas y cosas sin confirmar

- ✅ **Resueltas con los PDF:** hora de la completa (**3:00**), nº de copias del GFS (**5-7 diarias, 4-5 semanales, 12 mensuales**), «clase 10 del 28» (= **miércoles 18/11**; la diapositiva 26 lo dice), hito mensual de la política (**día 1, 1 año, snapshot archivado**), hora/forma de la «incremental» (`rsync -a` sin `--delete`).
- **Campos de tiempo del `rsync` «cada 2 h»** (`0 */2 * * *`): **solo audio** (no está en los PDF), confuso.
- **Fecha de entrega de la Actividad 2** (ver abajo) y **visto bueno del simulacro**.
- **"Preguntas de solo 3 temas"** en el test del simulacro: no queda claro cuáles.
- **Una parte de la actividad que «con el SAD1 no se puede hacer»** (algo de control de acceso/grupos): audio confuso; los PDF no la mencionan.
- **Cuánto tiempo hay que conservar datos personales** y **plazo de brecha**: lo dicho en clase (3 años, 32 h) no coincide con lo contrastado (72 h; el 3 solo como plazo de prescripción).
- **Nombre del modelo de soporte "sin noche"**: **(mío)** *follow the sun*, sin confirmar.
- **Consejo de certificaciones** (no evaluable, audio confuso): recomendó la familia **LPIC** (1 y 2 para el sistema y los servicios, 3 para seguridad).

## Logística y para llevar a casa

**Calendario (clase):**
- **Hoy, 11/11: última clase con temario nuevo.** **Semana siguiente (miércoles 18/11): repaso** (diapositiva 26: «Clase 10 · 18 de noviembre: repaso de los temas 1, 2 y 3 y preparación del simulacro»). Dará «pistas» de qué es importante.
- **Simulacro (diapositiva 26):** «examen de prueba de los temas 1 a 3, **en nuestra franja del miércoles**» (**25/11**), «sin sorpresas: lo que hemos dado». La **semana del 23 al 29/11**. Lo **publica el viernes 20/11** (para que haya fin de semana) y **lo resuelve en clase el miércoles 25/11**. Test con preguntas de **solo 3 temas** más preguntas de desarrollo. Está **pendiente del visto bueno** de coordinación ("a ver si me dan el visto bueno; ya la tengo preparada"). Habla de "todas las asignaturas": **sin confirmar si incluye SER y Ciber**.
- **Soluciones del simulacro:** no las publica de antemano; **resuelve en clase con su respuesta** y lo hace así a propósito.
- **Cómo contestar el desarrollo (clase):** **párrafos de 4–5 líneas como mucho**; quiere **los puntos principales con tus propias palabras**, "como en una entrevista", **no una respuesta aprendida de memoria**.

**Tema 3 en el examen (clase):** "muy importante, tanto **teórico como práctico**".
- **Teoría:** copia **completa, incremental, diferencial**, regla **3-2-1**, **buenas prácticas** (**restaurar siempre**: "por muchas copias que hagas, si no restauras no vale para nada").
- **Práctica/automatización:** **`cron` + rotación**, y **leer líneas de `crontab`**.

**Actividad 2 (clase):**
- **Laboratorio (diapositiva 26):** «el montaje de la política de copias sobre el servidor (rsync, tar, cron y la **restauración**) lo hacemos en el **laboratorio de diciembre**, al arrancar la Actividad 2». La diapositiva 27 dice a la vez «para el **laboratorio del lunes 16** arrancamos con la política completa»: **se contradice**; el 18/11 el profesor dijo que un laboratorio se movía, así que es **probable** que el del 16/11 pasara a diciembre (**sin confirmar**).
- La **adelanta** («para que en Navidades tengáis la actividad hecha»). Será un **laboratorio más "apretadito"**, sobre **SAD1**: un **servidor web** (Apache, etc.) con sus puntos importantes, una **copia completa** y un **bucket de S3** para guardarla. Es la **"copia guapa"** que anunció el 4/11.
- **Entrega: 18 de enero** (en el audio: "la actividad **no** se entrega el 18 de enero"; el "no" es probablemente un fallo, porque la frase siguiente solo tiene sentido si la entrega es **después** de Navidad). **Sin confirmar: mira el campus.** Con esto, el "16 de noviembre" del audio del 4/11 **no** parece ser esta fecha.

**Para hacer en casa** (diapositiva 27: «poca cosa, pero déjalo listo»: programa una copia diaria con `cron` y **comprueba al día siguiente** que ha corrido, en el log y mirando los ficheros; ten `sad1` a punto y que **no se te caduque la sesión de AWS**; empieza a repasar los Temas 1-3):
1. En **SAD1**, repetir en orden: tarea **cada minuto** → `rsync` **cada 2 h** → `tar` **dominical**, comprobando con `crontab -l` y `grep CRON /var/log/syslog | tail`. **Al acabar, comentar con `#`.**
2. **Practicar a interpretar `crontab`**: escribe 8–10 líneas (hora, días, opciones) y explícalas sin mirar.
3. Leer **Tema 3, 3.3** (torres de Hanoi, con sus tablas) y **3.4** (política), y los **entrenamientos 3 y 5** (Hanoi con 5 niveles; `rsync` + `cron` en Ubuntu).
4. Ver en el campus la **fecha de la Actividad 2** y el aviso del **simulacro**.

Fuentes (web): [AEPD: notificación de brechas (72 h)](https://www.aepd.es/es/derechos-y-deberes/cumple-tus-deberes/medidas-de-cumplimiento/brechas-de-seguridad) · [Debian: `crontab(5)`](https://manpages.debian.org/man/5/crontab) · [Wikipedia: esquemas de rotación de copias](https://en.wikipedia.org/wiki/Backup_rotation_scheme) · [TechTarget: rotación de cintas (GFS y Hanoi)](https://www.techtarget.com/searchdatabackup/tip/How-to-optimize-your-backup-tape-rotation-strategy) · [Legiscope: plazos de conservación (LOPDGDD)](https://www.legiscope.com/blog/plantilla-plazos-conservacion-datos.html)
