---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-11-04
tema: "Tema 3 · Sesión 8: copias de seguridad (regla 3-2-1, completa/incremental/diferencial, en caliente o en frío, bases de datos), práctica con `tar`, `rsync` y snapshot de AWS, y S3"
fuente: transcripción de la clase (1 h 27 min) + **PDFs del profesor recibidos el 25/11**: diapositivas `SAD_Clase08_diapositivas.pdf` (27 págs.) y guía `SAD_Clase08_Practica.pdf` (2 págs.). Contrastado con el Tema 3 del temario (3.2) y con fuentes externas marcadas (web). Donde el PDF y el audio difieren, manda el PDF.
---
# SAD · Tema 3, sesión 8 (4/11) · Copias de seguridad

> Anterior: [Tema 2, 2ª parte (28/10): disponibilidad, RTO/RPO, Tiers](2026-10-28_tema2-disponibilidad-rto-rpo-tiers.md) · Siguiente: [Tema 3, sesión 9 (11/11): cron, ventana, rotación GFS/Hanoi, política](2026-11-11_tema3-cron-ventana-rotacion-gfs-hanoi-politica.md) · Profesor: Damián Sualdea Soy

Empieza el **Tema 3 (seguridad pasiva: copias de seguridad)**. La copia es una **medida pasiva**, "la más importante" para recuperarse de un ataque o un fallo, y encaja con el **RPO** del Tema 2 ("es el RPO de hoy hecho realidad"). Hoy: teoría de la regla **3-2-1** y de los tipos de copia, y una práctica pequeña sobre el servidor de AWS (copia completa con `tar`, `rsync`, snapshot de volumen) más una demostración de **S3**. La práctica "grande" (3-2-1 completo con un servidor montado) **queda para otro día**.

Convención: **(clase)** = audio, **(temario)** = Tema 3 del repo, **(web)** = fuente externa, **(mío)** = añadido por mí.

> [!note] Actualización 25/11: PDFs recibidos
> Esta nota se hizo primero solo con el audio. Con las **diapositivas** y la **guía de la práctica** ya recibidas se han **corregido los comandos de la Tarea 5** (el audio no los dictaba), la **política de ejemplo** (Tarea 8) y las **fechas del calendario**. Cambios importantes: **`rsync -av --delete`** (no `-avz` a secas), **`tar … -C ~`**, nombres con **guion** (`completa-AAAA-MM-DD.tar.gz`) y **`sha256sum` sí se ejecuta** en la práctica.

## Lo imprescindible

> [!important] Chuleta
> - **Regla 3-2-1:** **3** copias de los datos (original + 2 copias), en **2** medios o dispositivos distintos, y **1** fuera del sitio (nube u otro edificio).
> - **Una copia que no has restaurado "no es una copia, es una esperanza"** (clase). **Hay que probar la restauración**, siempre.
> - **No se copia todo el servidor:** se copia lo **irreemplazable o configurado por ti** (`/etc`, bases de datos, `/var/www/html`, logs). Lo que se reinstala con `apt` (Apache, programas, caché, temporales) no.
> - **Completa** = todo. **Incremental** = lo cambiado desde la **última copia de cualquier tipo**. **Diferencial** = lo cambiado desde la **última completa**.
> - **Bases de datos: no se copian en caliente a pelo.** Se usa su herramienta (**`mysqldump`**) o se para el servicio.
> - **RAID no es copia de seguridad** (postura del profesor).
> - **Snapshot** de AWS = copia exacta del volumen en ese instante (la excepción en que sí se copia "todo").

## Tarea 1 · Qué copiar y dónde guardarlo

### Qué se guarda en un servidor (clase)
Se guarda lo que **has trabajado tú**. Ejemplo con los servicios de SER:

| Servicio | Qué guardas | Qué NO |
|---|---|---|
| **DNS (BIND9)** | `named.conf.local`, los ficheros de zona (`db.<dominio>`…) | El paquete `bind9` |
| **Apache** | `sites-available`/`sites-enabled`, cualquier configuración que tocaste, y lo que cuelga de **`/var/www/html`** | El paquete `apache2`: si cambias de sistema, `apt install apache2` y vuelcas tu configuración encima |
| **Base de datos** | La BD (con `mysqldump`) | — |
| **General** | **Logs** (por si hay un problema), `/etc` | Binarios, programas, caché, temporales |

Si usas Moodle, `moodledata`; si usas WordPress, la BD, la configuración de los virtual hosts y la de seguridad ("como no la voy a cambiar, me la guardo y la puedo restaurar cuando quiera"). **Lo irreemplazable o customizado** (la misma idea del temario: "ordenar de mayor a menor prioridad qué archivos son difíciles de volver a hacer").

### Dónde guardarlas (clase)
- **NAS**: un disco duro en red.
- **Cinta**: "sí que existe y funciona", muy barata y buena para volúmenes enormes (grabaciones, llamadas); electromagnética.
- **Nube**: **buckets de S3** de AWS (lo que más usa el profesor para copias de seguridad y logs).
- **Cerca o lejos:** una copia cercana se restaura rápido; una lejana (otro edificio/región) tarda, pero protege contra el desastre del sitio. Es la base de la regla 3-2-1.
- El temario añade los soportes de almacenamiento (DAS, NAS, SAN) y recomienda que la copia esté **cifrada y comprimida en un único fichero**, con pruebas de restauración y **rotación** de medios (Tema 3, 3.2).

## Tarea 2 · La regla 3-2-1

Es "una de las reglas más importantes de las copias".

| Cifra | Significa (clase) |
|---|---|
| **3** | Tres copias en total: **el original y dos copias** |
| **2** | En **dos medios/dispositivos distintos** (por ejemplo, el disco del servidor y otro soporte) |
| **1** | **Una fuera** del centro de trabajo: la nube |

Ejemplo del profesor: **datos originales + una copia local + un snapshot en la nube** = 3 copias, 2 medios (disco y nube), 1 fuera. "Con esta regla conseguimos máxima seguridad."

> [!note] Precisión (mío, web)
> El profesor lo dijo como "las 2 copias tienen que estar en dispositivos diferentes". La formulación habitual es **dos tipos de medio distintos** (no solo dos copias en dos discos iguales). El ejemplo que puso sí cumple ambas.

### RAID no es copia de seguridad (clase)
Debate entre los alumnos y el profesor: ¿cuenta **RAID 1** (espejo) como copia? **Su postura: no**; "es una mejora de la **disponibilidad** en un disco", no una copia.
- RAID protege contra el **fallo de un disco**; la copia protege contra la **pérdida de datos** (borrado, malware, error humano). Con un espejo, **si borras un fichero, se borra también en el otro disco**, y si entra malware, "lo metes en todo".
- Citó una **guía de INCIBE sobre la regla 3-2-1** que dice que RAID solo protege contra fallo de disco y la copia contra la pérdida de datos, pero que incluye la **"copia en espejo"** (copia exacta en tiempo real, "no se almacenan archivos antiguos", con el defecto de que **un borrado accidental también se borra de la copia**) entre los tipos de copia. **El profesor no está de acuerdo** en llamarlo copia.
- **Mi puntualización (web, probable):** la "copia en espejo" de INCIBE es un **tipo de backup**; RAID 1 es un **mecanismo de hardware/disponibilidad**. Son cosas distintas, aunque se parezcan, y la posición mayoritaria es la del profesor: **RAID no es backup**. **No he abierto la guía de INCIBE**, solo la he buscado.
- Esto conecta con el Tema 2: RAID/N+1 es **redundancia para disponibilidad**, no una copia.

## Tarea 3 · Tipos de copia

| Tipo | Qué guarda | Para restaurar necesitas | Detalle |
|---|---|---|---|
| **Completa** | Todo lo seleccionado | Solo ella | Más lenta y pesada de hacer; es la base de las demás |
| **Incremental** | Solo lo cambiado **desde la última copia** (completa o incremental) | La completa **+ todas** las incrementales intermedias, en orden | Pesa poco; restaurar requiere una cadena larga |
| **Diferencial** | Todo lo cambiado **desde la última completa** | La completa **+ solo la última** diferencial | Va **creciendo**; "se convierte en una que pesa bastante"; restaurar es más sencillo |

**Ejemplo del profesor (completa el lunes, cambia algo cada día):**
- **Incremental:** lunes completa; martes solo lo del martes; miércoles solo lo del miércoles; jueves solo lo del jueves. Si falla el jueves, restauras **lunes + martes + miércoles + jueves**.
- **Diferencial:** lunes completa; martes = cambios del martes; miércoles = martes + miércoles; jueves = martes + miércoles + jueves. Si falla el jueves: **lunes + la del jueves** = **2 operaciones**.

> [!important] Consejos del profesor
> - **Completa + diferencial** suele ser lo más seguro para restaurar (menos piezas). Si la diferencial crece demasiado, haz otra completa. Si hay muchos cambios durante el día, **incrementales**.
> - **Si se corrompe la completa, todo lo que dependa de ella se pierde**, sea diferencial o incremental. Por eso hay que **verificar y probar**.
> - "Cada X tiempo ponemos una completa" para no depender de cadenas muy largas.

> [!warning] Posible fallo en el audio (restauración rápida)
> Al inicio dice que con incrementales "la restauración va a ser muy rápida". Es **probable** que quisiera decir que la **copia** es rápida y ocupa poco: **restaurar** una cadena de incrementales es **más lento** que con diferencial o completa, y así lo explica después y el temario (3.2). Quédate con la tabla de arriba.

El temario añade recomendaciones por volumen: **< 4 GB**, copia total; **> 50 GB con pocos cambios**, total + diferenciales; **> 50 GB con cambios frecuentes**, total + incrementales, y totales más a menudo (3.2). En **3.3** vienen los esquemas de frecuencia (incluida la **torre de Hanoi**) y en **3.4** la política de copias: **este es el material que cae en la Actividad 2**.

## Tarea 4 · Copias en caliente, en frío y bases de datos

- **En frío:** paras el servicio, copias, vuelves a arrancar. La copia es fiable, pero **el servicio no está disponible** mientras tanto.
- **En caliente:** copias con el servicio funcionando ("no se nota nada"), pero con una **base de datos** hay una alta probabilidad de **corrupción**: si pillas el copiado **en mitad de una operación** (un `INSERT`, un `DELETE`, un cambio de estructura), la copia queda a medias.
- Explicación del profesor con **transacciones**: una operación se agrupa con `COMMIT` y, si algo falla, `ROLLBACK`. Si copias **a mitad** de la transacción, la copia queda con algo que "espera un `INSERT` que no existe" y puede **corromperse**.
- **Arquitectura:** por eso, al diseñar sistemas, se **separa la base de datos del cómputo** (en AWS: la API en EC2 y la BD aparte, en RDS), para poder copiar los datos con cuidado y la configuración de la aplicación por otro lado.
- **Solución (clase):** usar la herramienta de la BD para volcarla: **`mysqldump`** ("la utilidad de MySQL para hacer una copia de toda la base de datos"). Lo hace "cada X tiempo" y deja el `.sql` en el sitio de respaldo; luego se monta en cualquier sitio ("son instrucciones supersencillas"). **Con bases de datos no uses `rsync` a pelo:** "utilizad su herramienta".

```bash
# (clase: se nombra, no se dicta; los parámetros son míos y sin confirmar)
mysqldump -u <usuario> -p --all-databases > respaldo_$(date +%F).sql   # (mío) con MariaDB, también mariadb-dump
mysql -u <usuario> -p < respaldo_AAAA-MM-DD.sql                        # (mío) restaurar
```
**(mío)** Con tablas InnoDB, `--single-transaction` da un volcado consistente sin parar el servicio.

## Tarea 5 · Práctica en el servidor (AWS, `sad1`) · **(PDF: guía de la práctica)**

Idea: **hacer la copia de dos formas (completa con `tar` y espejo con `rsync`), provocar un desastre a propósito y restaurar comprobando que el dato recuperado es idéntico.** Requisitos (guía): laboratorio de AWS Academy arrancado (*Start Lab* en verde), instancia `sad1` en marcha, SSH con `labsuser.pem` y usuario `ubuntu`. La guía está hecha para poder seguirla solo si no te daba tiempo en directo.

### 5.1 Preparar los datos de prueba
```bash
mkdir -p ~/datos ~/copias
echo 'nóminas de octubre' > ~/datos/nominas.txt
echo 'contratos 2026'     > ~/datos/contratos.txt
ls ~/datos        # contratos.txt  nominas.txt
```

### 5.2 Copia completa con `tar`
```bash
tar -czf ~/copias/completa-$(date +%F).tar.gz -C ~ datos
ls -lh ~/copias
```
- `-c` crear, `-z` comprimir (gzip), `-f` fichero de salida. **`-C ~ datos`** = "entra en `~` y empaqueta `datos`": así el `.tar.gz` guarda la ruta relativa `datos/…` y al restaurar con `-C ~` vuelve a su sitio.
- **`$(date +%F)`** = fecha `AAAA-MM-DD` en el nombre (no se pisan las copias). Nombre en la guía: **`completa-2026-11-04.tar.gz`** (con guion; mi versión anterior ponía guion bajo).
- Audio: el profesor insiste en **`-czf`** («siempre se me olvida: primero el formato, luego el fichero»).

### 5.3 Copia espejo con `rsync`
```bash
rsync -av --delete ~/datos/ ~/copias/espejo/
rsync -av --delete ~/datos/ ~/copias/espejo/     # repetida: casi no copia nada
```
- `-a` archivo (recursivo, conserva permisos y fechas), `-v` detalle. La primera vez copia todo; la segunda **solo lo cambiado** (mensaje `sending incremental file list`).
- **`--delete` = espejo exacto**: lo que borras en el origen **también desaparece de la copia**. La guía: «úsalo con cabeza».
- **Barra final en `~/datos/`**: copia **el contenido** de `datos` dentro de `espejo/`. Sin barra, crearía `espejo/datos/`. **(mío)**
- *(Diapositiva 13; la salida de ejemplo lista `datos/contratos.txt` y `datos/nominas.txt`.)*

> [!warning] Corrección respecto a mi versión anterior
> Escribí que «con `rsync -avz` a secas los borrados no se propagan» y que el profesor se equivocaba al decir que se borraba del espejo. **La guía usa `--delete`, así que el profesor tenía razón para su comando.** Lo general sigue siendo cierto (**sin `--delete` un `rsync` nunca borra en destino**), pero en esta práctica **sí**.

> [!warning] Cómo lo llama el profesor y qué es en realidad
> En clase dice a ratos «copia incremental», «diferencial» y «espejo». Lo correcto: `rsync` es una **sincronización** que transfiere solo diferencias; con `--delete` es un **espejo**. No es uno de los tres tipos del temario (completa, incremental, diferencial). Un `rsync` plano deja **una sola copia** del estado actual, **sin versiones anteriores**.

### 5.4 Copia en otro servidor (opcional · guía, paso 4)
```bash
rsync -avz ~/datos/ ubuntu@<IP-SEGUNDA-MAQUINA>:~/copias/espejo/
```
`-z` comprime durante el envío. La guía usa una IP privada de ejemplo (`10.0.0.20`); cámbiala por la de tu segunda máquina **si la tienes**. Esa copia «vive en OTRA máquina»: es el «otro sitio» de la 3-2-1. *(En el audio el profesor no la hizo en vivo; quería montar esto con otro servidor o S3 otro día.)*

### 5.5 Desastre pequeño: borrar un fichero y restaurarlo
```bash
rm ~/datos/nominas.txt
cat ~/datos/nominas.txt                      # No existe el archivo
rsync -av ~/copias/espejo/nominas.txt ~/datos/    # restaurar SOLO ese fichero (sin --delete)
cat ~/datos/nominas.txt                      # vuelve: nóminas de octubre
sha256sum ~/datos/nominas.txt ~/copias/espejo/nominas.txt
```
- **Si las dos huellas coinciden, la restauración es íntegra**: recuperaste «el MISMO fichero». La guía: **«recuperar sin verificar no vale»**. *(Mi versión anterior decía que el profesor no ejecutó el `sha256sum`; en la guía y la diapositiva 18 **sí** está.)*
- Ojo: aquí el **origen es la copia** y el destino tus datos, al revés que al copiar.

### 5.6 Desastre total: restaurar la carpeta entera con `tar`
```bash
rm -rf ~/datos            # se va la carpeta entera
ls ~/datos                # ya no existe
tar -xzf ~/copias/completa-$(date +%F).tar.gz -C ~
ls ~/datos                # contratos.txt  nominas.txt: restaurada entera
```
`-x` extraer. Con `$(date +%F)` la restauración **solo funciona el mismo día** de la copia; otro día, escribe la fecha a mano. **(mío)**

> [!important] Lo que enseñó el fallo en directo (audio)
> Al profesor le salió mal una restauración en clase: el `rsync --delete` repetido **tras** el borrado **propagó el borrado al espejo** («me cargo nóminas del espejo»). Moraleja suya: el `rsync` **captura ese instante**; si lo vuelves a lanzar con el origen ya dañado, **copias el daño**. **La copia completa (`tar`) es la que te salva.**
> - **Uso que le da el profesor al `rsync`:** para **configuraciones que sabes que funcionan** (DNS, Apache con virtual hosts): una vez, con el servidor completo, como «punto de retorno». **Para datos, no**: completas/incrementales/diferenciales y volcados.
> - Alternativa: guardar el espejo **comprimido con fecha** («espejo del 4/11, del 5/11…») para no perder versiones; apareció **Git** como ejemplo de «commits = snapshots de texto» (otro día).

### 5.7 Sacar la copia del servidor: `scp` (solo audio)
- El profesor la baja a su equipo con **`scp`** (parte de SSH que **sube y baja ficheros**) o la sube a otro servidor por SSH. **(mío)**:
  ```bash
  scp -i labsuser.pem ubuntu@<TU-ELASTIC-IP>:/home/ubuntu/copias/completa-<fecha>.tar.gz .
  ```
  Lo ve "la semana siguiente" con más calma (**sin confirmar**; dijo que "no lo conocéis todavía").
- Quería montar una práctica con **copia en otro servidor** (conectarse por SSH a otra máquina) y, mejor, a un **bucket de S3**: "me quedaría guapísimo"; **lo prepara él** para otra clase.

## Tarea 6 · Snapshot de AWS (la copia "de fuera")

AWS permite una **copia exacta** del volumen del servidor en ese instante: es la excepción a "no copies todo el sistema". Se restaura de forma muy rápida y "te ahorra reinstalar y reconfigurar el servidor entero". Idea del profesor: **datos a diario, sistema con menos frecuencia**.

Pasos en la consola (clase y guía, paso 7; la guía lo llama **Crear snapshot**, la consola en español **Crear instantánea**):
1. **EC2 → Elastic Block Store → Volúmenes** (menú izquierdo). Quita el filtro si no ves tu volumen y localiza el de tu instancia (en la instancia, pestaña **Almacenamiento**; en clase, 8 GiB).
2. Selecciona el volumen → **Acciones → Crear instantánea**.
3. **Descripción** con la fecha (en clase: «copia del 4/11/2026»; guía: «sad1 estado 4-nov») → **Crear instantánea**.
4. Mira en **Instantáneas** (menú izquierdo): aparece la creada. Si ves rojo por *Data Lifecycle Manager*, "da igual": es por no tener política.

> [!note] Mío (web, sin verificar hoy)
> Una instantánea de un volumen en marcha es **consistente ante fallos** (como si se cortara la luz), no consistente con la aplicación: la misma limitación de la base de datos de la Tarea 4. Para una BD, vuelca antes con `mysqldump` o para el servicio. En AWS las instantáneas posteriores guardan solo los bloques cambiados.

**Diapositiva 19:** `tar` y `rsync` copian **ficheros**; el snapshot copia el **disco entero** (sistema incluido) y AWS lo guarda **aparte del servidor**: si el servidor desaparece, la foto sigue. **Se complementan: ficheros a diario, snapshot del sistema de vez en cuando.** Un snapshot de AWS **sería la copia "1" (fuera, en otro sitio) de la regla 3-2-1**, dijo el profesor.

## Tarea 7 · S3: buckets (demostración)

**S3** es el almacenamiento de objetos de AWS "para guardar cualquier cosa": copias, bases de datos, logs. El profesor: "es barato, lo dejas y pagas lo que ocupa".
- **Clases de almacenamiento:** **Standard** y **Glacier** (más barato; "tardas un poco más en recoger la información pero gastas muy poco").
- Demo (consola, clase): **Amazon S3 → Crear bucket** → de uso general, un **nombre** (él puso "copias semanales"; **(mío)** un bucket real no admite espacios y el nombre es único en todo AWS) → **Bloquear todo el acceso público** → crear. Luego **Cargar** el fichero (arrastrarlo) y **Cargar**.
- Para **enseñarlo**, quitó el bloqueo público y editó la **ACL de un objeto** para dejarlo de **lectura pública**; luego lo dejó **privado**. **(mío)** Para copias reales: **siempre privado**.
- Por la consola se sube **a mano**; "se hace por línea de comandos" (un alumno preguntó por automatizar la copia semanal de una BD; el profesor: "es lo que no estoy contando"; **lo hará otro día**).

## Tarea 8 · Política de copias: cuánto y cada cuánto (RPO)

Ejercicio en clase: **¿qué RPO para una pyme?** "La seguridad es muy adaptativa."

| Caso | Qué se guarda | RPO que se sugirió |
|---|---|---|
| **Academia de inglés** (presencial) | Moodle: apuntes, evaluaciones, recursos, MP3, matrículas, notas | Semanal (debate; los alumnos votaron entre diario y 15 días). **Si es una academia online con trabajo diario, más frecuente** |
| **Gestoría** | Documentos de muchas empresas | **1–2 al día**, y más en periodos fiscales (trimestral/IRPF) |
| **Banca** | Todo | "El top": **RPO mínimo**, "de las más críticas" |

Cómo calcularlo: "cuánto pierdes en una semana", mirar qué documentos cambian al día, si ya hay copia en OneDrive/servidor local, etc. Recuerda: **RPO = la antigüedad máxima de la última copia útil** (Tema 2).

**Política de ejemplo para `sad1` · diapositiva 23 (el detalle, «a fondo» en la Clase 9)**

| Qué se copia | Cada cuánto | Se guarda | Dónde |
|---|---|---|---|
| **Datos de trabajo** | Diaria · **incremental** | **30 días** | Disco aparte |
| **Sistema entero** | Semanal · **completa** | **4 semanas** | **Snapshot AWS** |
| **Configuración (`/etc`)** | **En cada cambio** | Histórico | Copia local |

«La política no se inventa: sale del **RTO y RPO**.» ¿Cuántos datos puedes perder? → marca **cada cuánto** copias. ¿Cuánto puedes tardar en volver? → marca **dónde y cómo** guardas. *(Mi versión anterior, hecha solo con audio, decía «sistema entero completa cada 4 semanas»: la tabla del PDF es semanal con retención de 4 semanas.)*

Cierre (diapositivas 24 y 27): **«una copia que no has restaurado nunca no es una copia: es una esperanza»**; **«hacer copias es fácil, restaurarlas el día malo, no»**.

## Lo que traen las diapositivas y no estaba claro en el audio

- **Diapositiva 3:** la copia **fija tu RPO** («si copias cada día, tu RPO es de un día»). Dice que la 3-2-1 y completa/incremental ya se vieron en **Ciber**: «hoy no las reexplicamos, las usamos» (aun así las repasó en clase).
- **Diapositiva 7:** además de disco, NAS, cinta o nube: **cerca** (rápida) y **lejos** («para cuando arde el edificio, como OVH»), y **RAID no es copia**: «si borras un fichero por error, se borra en todos a la vez; el RAID es disponibilidad».
- **Diapositiva 8, qué se copia:** **SÍ** datos de trabajo, configuración (`/etc`) y bases de datos; **NO** SO, programas, caché y `/tmp`; **excepción:** una imagen/snapshot del sistema «de vez en cuando».
- **Diapositiva 9, frío/caliente:** frío = paras, copias, arrancas; caliente = sin parar, con riesgo si hay BD en marcha; **solución: volcado (dump) o snapshot**. «La trampa clásica: copiar con `rsync` los ficheros de una BD en marcha.»
- **Diapositiva 10, 3-2-1:** 3 copias · 2 medios distintos · 1 fuera del edificio. Ejemplo en `sad1`: **datos + copia local + snapshot en la nube = 3 copias, 2 medios (disco y snapshot), 1 fuera**; «sobrevives a un borrado, un disco muerto, un ransomware e incluso un incendio». **Aquí el original SÍ cuenta como una de las 3**, pero la diapositiva 14 de la **Clase 10** (repaso del 18/11) dice «el original **no** cuenta»: **se contradicen**; ver [18/11](2026-11-18_repaso-simulacro-temas-1-2-3.md).
- **Diapositiva 6 (la semana):** completa el lunes; **incremental** = martes (solo martes), miércoles (solo miércoles), jueves (solo jueves) → restaurar el jueves = **completa + 3 incrementales (4 piezas; si falta una, no restauras)**; **diferencial** = martes, martes+miércoles, martes+miércoles+jueves → **completa + la del jueves (2 piezas)**: «la diferencial es más segura de restaurar».

> [!important] Antes de cerrar (guía de la práctica)
> 1. Comprueba que los datos están restaurados (`ls ~/datos` y `cat`).
> 2. **Apaga la instancia con *Stop* (NO *Terminate*)**; el snapshot se queda guardado.
> 3. **Apunta en el «diario de incidentes»**: qué copiaste, qué borraste, cómo restauraste y si la huella coincidía.

## Casos reales que citó

| Caso | Qué pasó | Verificado |
|---|---|---|
| **Toy Story 2 (1998)** | Alguien lanzó un borrado sobre el servidor de la película; las **copias llevaban semanas fallando** y nadie lo miraba; se salvó por la copia que una empleada tenía **en su casa** | Diapositiva 21 y audio; **no lo he verificado en fuente externa** |
| **GitLab (2017)** | Un técnico borró por error la base de datos de **producción** (era el servidor equivocado). Quedó ~**4,5 GB de unos 300 GB**. **Cinco** técnicas de copia/replicación **no funcionaban bien**. Restauraron desde una copia de unas **6 horas** antes y **perdieron 6 h de datos** | **Sí**, según el informe oficial de GitLab (web) |

Moraleja: **tener copia no basta, hay que verificar que se puede restaurar.**

## Próximas sesiones y logística

- **Siguiente clase (diapositiva 25):** **Clase 9 · 11/11**: frecuencia y política a fondo (RPO/RTO, ventana de copia, retención y rotación con **Torres de Hanói**) y **automatizar con `cron`**. **Laboratorio · 16/11**: «la copia completa en serio: `rsync`, `tar` y `cron` sobre el servidor, y una **restauración real**; deja hecho el **apartado de copias de la Actividad 2**». **Actualización (11/11 y 18/11):** el 11/11 se hizo `cron` + rotación + política; **no hubo restauración real ni 3-2-1 completo**, y el 18/11 el profesor dijo que **un laboratorio se movía al siguiente trimestre**: es **probable** que sea este del 16/11 (**sin confirmar**). Las diapositivas del 11/11 lo sitúan «en el **laboratorio de diciembre**, al arrancar la Actividad 2»; ver [11/11](2026-11-11_tema3-cron-ventana-rotacion-gfs-hanoi-politica.md).
- **Para la próxima clase (diapositiva 26):** (1) **repetir la copia y la restauración** en tu `sad1` «sin mirar los apuntes»; (2) **hacer un snapshot** del volumen de `sad1` (lo necesitas «a punto para el laboratorio del 16»); (3) **leer 3.2 y 3.3** del campus (confirmado: **Tema 3, 3.2 Copias y 3.3 Frecuencia**). Audio: además, la **guía de INCIBE sobre la 3-2-1**.
- **Calendario:** el profesor preguntó si el **lunes** era festivo (en Madrid, el **9/11** es la festividad de la Almudena, lo dijo sin certeza) y si afectaba a UNIR; **sin confirmar** si hubo clase. La práctica grande se hace "cuando se pueda".
- **Actividad 2:** el PDF aclara el «16 de noviembre» confuso del audio: es la fecha del **laboratorio**, **no** de la entrega. Diapositiva 25: «tu plan de seguridad pasiva incluye el **plan de copias**; todo lo de hoy y de la Clase 9 es **material directo de esa actividad**». La entrega sigue siendo **18/01 (sin confirmar en el campus)**.
- **Conexión con otros módulos:** en **Ciber** se hicieron copias con `rsync`/`cron` y cifrado con `gpg` ([Clase 6](../Ciber/2026-10-20_clase6-contrasenas-copias.md)); en **SER** tienes la parte práctica de un servidor real.

## Si algo no funciona

| Síntoma | Causa | Arreglo |
|---|---|---|
| `tar` no pone la fecha en el nombre | La sustitución `$(date +%F)` mal escrita, o entre comillas simples | Comprueba que sea `$(date +%F)` y sin comillas simples |
| `rsync` no copia nada nuevo | No ha cambiado nada (es lo normal) | Modifica un fichero y repite |
| El espejo pierde un fichero tras un desastre | `--delete` propaga los borrados si relanzas el `rsync` | Restaura **antes** de relanzarlo; prueba con `--dry-run` |
| La restauración sale vacía | La copia se hizo después del borrado, o con el origen ya dañado | Restaura desde una **completa anterior**; haz copias **antes** del problema |
| `tree: command not found` | No está instalado | `sudo apt install tree` |
| La BD restaurada da errores | Copia en caliente a medias | Usa `mysqldump` o para el servicio |

## Dudas y cosas sin confirmar

- ✅ **Resueltas con los PDF:** comandos exactos de la práctica, uso de `--delete`, `sha256sum`, política de ejemplo, «16 de noviembre» (= laboratorio) y «leer 3.2 y 3.3».
- **Fecha de entrega de la Actividad 2:** 18/01, sin confirmar en el campus.
- **Si hubo clase el 9/11** (festivo local en Madrid, sin confirmar).
- **Si el laboratorio del 16/11 se celebró o se movió** (el 18/11 dijo que uno se movía; sin confirmar que sea este).
- **Cómo se restaura un snapshot** (crear volumen o AMI): no se mostró (solo la creación).

Fuentes (web): [GitLab: postmortem de la incidencia de 2017](https://about.gitlab.com/blog/gitlab-dot-com-database-incident) · [GoLinuxCloud: rsync](https://www.golinuxcloud.com/rsync-command-in-linux/)
