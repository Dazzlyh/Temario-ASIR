---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-11-04
tema: "Tema 3 · Sesión 8: copias de seguridad (regla 3-2-1, completa/incremental/diferencial, en caliente o en frío, bases de datos), práctica con `tar`, `rsync` y snapshot de AWS, y S3"
fuente: transcripción de la clase (1 h 27 min). Documento de la práctica citado por el profesor y presentación: no recibidos (en el audio se ve que la práctica tenía un documento aparte). Contrastado con el Tema 3 del temario (3.2) y con fuentes externas marcadas (web). Los comandos de la práctica no se dictan: ver el aviso.
---
# SAD · Tema 3, sesión 8 (4/11) · Copias de seguridad

> Anterior: [Tema 2, 2ª parte (28/10): disponibilidad, RTO/RPO, Tiers](2026-10-28_tema2-disponibilidad-rto-rpo-tiers.md) · Siguiente: [Tema 3, sesión 9 (11/11): cron, ventana, rotación GFS/Hanoi, política](2026-11-11_tema3-cron-ventana-rotacion-gfs-hanoi-politica.md) · Profesor: Damián Sualdea Soy

Empieza el **Tema 3 (seguridad pasiva: copias de seguridad)**. La copia es una **medida pasiva**, "la más importante" para recuperarse de un ataque o un fallo, y encaja con el **RPO** del Tema 2 ("es el RPO de hoy hecho realidad"). Hoy: teoría de la regla **3-2-1** y de los tipos de copia, y una práctica pequeña sobre el servidor de AWS (copia completa con `tar`, `rsync`, snapshot de volumen) más una demostración de **S3**. La práctica "grande" (3-2-1 completo con un servidor montado) **queda para otro día**.

Convención: **(clase)** = audio, **(temario)** = Tema 3 del repo, **(web)** = fuente externa, **(mío)** = añadido por mí.

> [!warning] Lo que NO tengo
> El profesor repartió **un documento de la práctica** que no me ha llegado, y los comandos **no se dictan** en el audio (se copian y pegan). Los de abajo son lo que se entiende más una reconstrucción mía y van marcados **(sin confirmar)**. Cuando tengas el PDF, **manda el PDF**.

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

## Tarea 5 · Práctica en el servidor (AWS, `sad1`)

Servidor de prácticas: el de SAD (EC2 de AWS Academy), conectándote por SSH. Idea de la práctica: **proteger lo importante, simular un desastre pequeño y restaurar.**

> [!warning] Comandos reconstruidos (sin confirmar)
> No tengo el documento de la práctica. Lo que sigue es lo que se entiende del audio más los parámetros habituales; **verifica contra el PDF**.

### 5.1 Preparar los datos de prueba
```bash
mkdir -p ~/datos ~/copias            # (clase) carpetas "datos" y "copias"
cd ~
echo "nóminas de octubre" > datos/nominas.txt        # (clase: "nóminas de octubre", "contrato 2026"; con echo en vez de nano)
echo "contrato 2026"      > datos/contratos.txt
ls datos
```
(Según el profesor: "lo importante son los datos"; la práctica final será un servidor completo con más cosas.)

### 5.2 Copia completa comprimida: `tar`
```bash
tar -czf copias/completa_$(date +%F).tar.gz datos      # (clase: "siempre z, c, z, f"; "dollar day con la F mayúscula" = fecha) (sin confirmar el comando exacto)
ls -lh copias
```
- `c` crea, `z` comprime con gzip, `f` indica el fichero de salida; `-C`… no se usó.
- **`$(date +%F)`** pone la fecha (`AAAA-MM-DD`) en el nombre: así **no se pisan** las copias. En clase a varios no les puso la fecha ("no ha puesto timestamp"); el profesor lo dejó pasar.
- El profesor insiste: **siempre `-czf`** ("siempre se me olvida: tiene que ir antes el formato, luego el fichero").

### 5.3 Copia "espejo" con `rsync`
```bash
sudo apt install -y tree          # (clase) para ver la estructura de carpetas
rsync -avz datos/ copias/espejo/  # (clase: "a, v, z") (sin confirmar el destino exacto)
tree
```
- `-a` archivo (conserva permisos, fechas…, recursivo), `-v` detalle, `-z` comprime. La salida dice **`sending incremental file list`** y lista lo copiado. Se puede repetir las veces que quieras: la segunda vez **solo copia lo que ha cambiado**.
- **`tree`**: `sudo apt install tree` (el profesor lo usa muchísimo para comprobar "qué hay").

> [!warning] Cómo lo llama el profesor y qué es en realidad
> En la clase llama al `rsync` **"copia incremental"**, **"diferencial"** y **"espejo"**, según el momento. Lo correcto: `rsync` es una **sincronización** que **transfiere solo las diferencias** (de ahí el mensaje "incremental file list"). Eso es una propiedad de la **transferencia**, no el tipo de copia: un `rsync` plano deja **una sola copia** del estado actual, **sin versiones anteriores** (a menos que uses opciones específicas, **(mío)** como `--backup` o `--link-dest`). Para el examen, quédate con los tres tipos del temario: completa, incremental, diferencial.

> [!warning] Borrados y espejo: lo que dijo no es del todo exacto
> El profesor dijo: "si borras algo del origen, **también desaparece de la copia**, hay que tener cuidado" y, al sincronizar tras borrar, "me cargo nóminas del espejo". **Con `rsync -avz` a secas eso no ocurre**: los ficheros borrados del origen **siguen en el destino**; solo se eliminan con la opción **`--delete`** (web: tutorial de GoLinuxCloud: "`--delete` removes files on the destination that are not present on the source"). **Es probable que el espejo del que habla sea con `--delete`**, que no se oye. Si quieres un espejo exacto, añade `--delete` (y pruébalo antes con `--dry-run`, **(mío)**); si quieres que no te borre, no lo uses. **Sin confirmar** qué ejecutó él.

### 5.4 Desastre pequeño y restauración
```bash
tree datos
rm datos/nominas.txt               # (clase) "borramos las nóminas" (desastre pequeño)
tree datos                         # ya no está
rsync -avz copias/espejo/nominas.txt datos/    # (clase) recuperarlas del espejo
tree datos                         # vuelve a estar
```
- **Sacar un `sha256sum`** (hash) de los ficheros antes y después "para verificar que no ha cambiado nada" (el profesor lo mencionó y no lo ejecutó, **(mío)** `sha256sum datos/*`).
- **Desastre grande:** `rm -rf datos` y se pierde todo. Restauras desde la **completa**:
  ```bash
  tar -xzf copias/completa_<fecha>.tar.gz     # (clase: "primero descomprimirlo y copiarlo donde estaba") (sin confirmar)
  tree
  ```
  Con **todo** de vuelta (`contratos.txt` y `nominas.txt`).

> [!important] Lo que enseñó el fallo en directo (clase)
> Al profesor le salió mal: tras el desastre ejecutó otra sincronización y comprobó que el espejo **solo tenía lo que había en el momento** del `rsync` (había creado los ficheros **después**, o los actualizó con un estado ya borrado). Moraleja que repitió, con ayuda de un alumno que lo formuló bien: **el `rsync` captura "ese instante"**; si lo vuelves a ejecutar con el origen ya dañado, **copias el daño** (o pierdes lo que tenías). **La copia completa es la que te salva.**
> - **Uso que le da el profesor al `rsync`:** para **configuraciones que sabes que funcionan** (DNS, Apache con todos sus virtual hosts): lo hace **una vez** cuando el servidor está completo y lo guarda como "punto de retorno". **Para datos, no**: ahí van las completas/incrementales/diferenciales y los volcados.
> - Alternativa pensada: guardar la sincronización **comprimida con la fecha** ("espejo del 4/11, espejo del 5/11…"), porque si no pierdes versiones. Y ya apareció **Git** como ejemplo de "commits = snapshots de texto" para volver atrás; lo veremos otro día.

### 5.5 Sacar la copia del servidor: `scp`
- El profesor la baja a su equipo con **`scp`** (parte de SSH que **sube y baja ficheros**) o la sube a otro servidor por SSH. **(mío)**:
  ```bash
  scp -i labsuser.pem ubuntu@<TU-ELASTIC-IP>:/home/ubuntu/copias/completa_<fecha>.tar.gz .
  ```
  Lo ve "la semana siguiente" con más calma (**sin confirmar**; dijo que "no lo conocéis todavía").
- Quería montar una práctica con **copia en otro servidor** (conectarse por SSH a otra máquina) y, mejor, a un **bucket de S3**: "me quedaría guapísimo"; **lo prepara él** para otra clase.

## Tarea 6 · Snapshot de AWS (la copia "de fuera")

AWS permite una **copia exacta** del volumen del servidor en ese instante: es la excepción a "no copies todo el sistema". Se restaura de forma muy rápida y "te ahorra reinstalar y reconfigurar el servidor entero". Idea del profesor: **datos a diario, sistema con menos frecuencia**.

Pasos en la consola (clase):
1. **EC2 → Elastic Block Store → Volúmenes** (menú izquierdo). Quita el filtro si no ves tu volumen y localiza el de tu instancia (en la instancia, pestaña **Almacenamiento**; en clase, 8 GiB).
2. Selecciona el volumen → **Acciones → Crear instantánea**.
3. **Descripción** con la fecha (en clase: "copia del 4/11/2026") → **Crear instantánea**.
4. Mira en **Instantáneas** (menú izquierdo): aparece la creada. Si ves rojo por *Data Lifecycle Manager*, "da igual": es por no tener política.

> [!note] Mío (web, sin verificar hoy)
> Una instantánea de un volumen en marcha es **consistente ante fallos** (como si se cortara la luz), no consistente con la aplicación: la misma limitación de la base de datos de la Tarea 4. Para una BD, vuelca antes con `mysqldump` o para el servicio. En AWS las instantáneas posteriores guardan solo los bloques cambiados.

Un snapshot de AWS **sería la copia "1" (fuera, en otro sitio) de la regla 3-2-1**, dijo el profesor.

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

**Política de ejemplo del profesor (audio confuso, sin confirmar):**
- **Datos de trabajo:** incrementales frecuentes más completa periódica, en disco aparte.
- **Sistema entero:** completa semanal/cada pocas semanas, con la frecuencia que convenga ("completa cada 4 semanas").
- **Configuración histórica** (`/etc`): una copia **cuando terminas de configurar** el servidor (y al cambiar algo importante).
- Cierre: **"una copia de seguridad que no has restaurado no es una copia, es una esperanza"** ("lo último que se pierde").

## Casos reales que citó

| Caso | Qué pasó | Verificado |
|---|---|---|
| **Toy Story 2** | Alguien lanzó un borrado sobre el servidor de la película y se perdió casi todo; las **copias llevaban semanas fallando** y nadie lo miraba; se salvó por la copia en casa de una empleada | Citado por el profesor; **no lo he verificado hoy** |
| **GitLab (2017)** | Un técnico borró por error la base de datos de **producción** (era el servidor equivocado). Quedó ~**4,5 GB de unos 300 GB**. **Cinco** técnicas de copia/replicación **no funcionaban bien**. Restauraron desde una copia de unas **6 horas** antes y **perdieron 6 h de datos** | **Sí**, según el informe oficial de GitLab (web) |

Moraleja: **tener copia no basta, hay que verificar que se puede restaurar.**

## Próximas sesiones y logística

- **Siguiente clase (según el profesor):** automatizar: **`cron` + `rsync`**, una **restauración real**, y la **política de copias** (frecuencia, **ventana de copia**, **rotación**). También montará un servidor con varios servicios para hacer un **3-2-1 completo** ("el desastre"). **Actualización (11/11, nota nueva):** se hizo `cron` + rotación (GFS/Hanoi) + ventana + política; **no hubo restauración real ni 3-2-1 completo**: el profesor lo ata a la Actividad 2 (ver [11/11](2026-11-11_tema3-cron-ventana-rotacion-gfs-hanoi-politica.md)).
- **Material a leer:** el profesor pidió leer "el 3.2 y el 3.3" del temario (es **probable** que sea el Tema 3, apartados **3.2 Copias de seguridad** y **3.3 Frecuencia**) y la **guía de INCIBE sobre la regla 3-2-1**.
- **Calendario:** el profesor preguntó si el **lunes** era festivo (en Madrid, el **9/11** es la festividad de la Almudena, lo dijo sin certeza) y si afectaba a UNIR; **sin confirmar** si hubo clase. La práctica grande se hace "cuando se pueda".
- **Actividad 2:** "la ponemos de fondo", "para que os vaya sonando; las de SAD son siempre las primeras"; lo dijo junto a una fecha, **16 de noviembre** (audio muy confuso: habla de "el 9 está mal", "clase el 9, el 11 no es clase"). Hasta ahora anoté **18/01** (sin confirmar). Con esto la fecha sigue **sin confirmar**: **mira la entrega en el campus**. **Actualización (11/11):** el audio apoya la entrega del **18/01** (con un "no" dudoso); sigue sin confirmar en el campus.
- **Conexión con otros módulos:** en **Ciber** se hicieron copias con `rsync`/`cron` y cifrado con `gpg` ([Clase 6](../Ciber/2026-10-20_clase6-contrasenas-copias.md)); en **SER** tienes la parte práctica de un servidor real.

## Si algo no funciona

| Síntoma | Causa | Arreglo |
|---|---|---|
| `tar` no pone la fecha en el nombre | La sustitución `$(date +%F)` mal escrita, o entre comillas simples | Comprueba que sea `$(date +%F)` y sin comillas simples |
| `rsync` no copia nada nuevo | No ha cambiado nada (es lo normal) | Modifica un fichero y repite |
| `rsync` se "pasa" borrando | Usaste `--delete` | Pruébalo con `--dry-run` antes |
| La restauración sale vacía | La copia se hizo después del borrado, o con el origen ya dañado | Restaura desde una **completa anterior**; haz copias **antes** del problema |
| `tree: command not found` | No está instalado | `sudo apt install tree` |
| La BD restaurada da errores | Copia en caliente a medias | Usa `mysqldump` o para el servicio |

## Dudas y cosas sin confirmar

- **Documento de la práctica** y presentación de la clase: no recibidos; comandos reconstruidos.
- **Fecha de entrega de la Actividad 2:** 18/01 (anterior) frente a un "16 de noviembre" confuso en el audio.
- **Si hubo clase el 9/11** (festivo local en Madrid, sin confirmar).
- **Qué ejecutó exactamente** con `rsync` (¿`--delete`?, ¿qué destino?). **11/11:** dicta `rsync -a --delete`, así que es probable que el 4/11 fuera lo mismo.
- **Política de ejemplo** (frecuencias): audio confuso.
- **"Leeros el 3.2 y el 3.3"**: interpretado como apartados del temario.
- **Cómo se restaura un snapshot** (crear volumen o AMI): no se mostró (solo la creación).

Fuentes (web): [GitLab: postmortem de la incidencia de 2017](https://about.gitlab.com/blog/gitlab-dot-com-database-incident) · [GoLinuxCloud: rsync](https://www.golinuxcloud.com/rsync-command-in-linux/)
