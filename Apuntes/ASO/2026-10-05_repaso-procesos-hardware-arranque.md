---
asignatura: Administración de Sistemas Operativos (ASO)
fecha: 2026-10-05
tema: Tema 2 · repaso memoria/procesos, planificación, hardware, montaje y arranque
fuente: apuntes de clase de Dani + transcripción de la clase en directo
---
# ASO · Tema 2: repaso procesos, hardware y arranque (05/10)

> Anterior: [UD1](2026-09-28_ud1-linux-basico.md) · Siguiente: —

Clase de **Jairo Bahillo Calvo**, repaso explícito de contenidos ya vistos en primero (gestión de memoria, procesos, arranque) con algo más de profundidad. El profesor avisa varias veces de qué partes son "de repaso para el test" y cuáles entran en la práctica del examen.

Lo anotado en clase (nombres/conceptos base):
- **Memoria**: `free`, `vmstat`, `top` / `htop`, `/proc/meminfo`.
- **Procesos**: `ps`, `kill`, `nice` / `renice`; creación con `fork()` y `exec`; señales de `kill`: **9** (SIGKILL), **1** (SIGHUP), **15** (SIGTERM).
- **Hardware y módulos**: `lsblk`, `lspci`, `lsusb`, `lsmod`, `modprobe`.
- **Montaje**: puntos `/mnt/usb` o `/media/usb`; sistemas de archivos **ext4** y **ZFS**.
- **Arranque** de Linux completo; `systemctl` y **systemd**.

## Notas de apoyo (conocimiento general, no dicho en clase; verificar con el temario)
- 9 = termina sin posibilidad de limpieza; 15 = petición de terminación educada (el proceso puede capturarla); 1 = en muchos demonios, recarga la configuración.
- `fork()` duplica el proceso; `exec` reemplaza su imagen por otro programa.

## Notas en directo (matices del profesor, no están en las diapositivas)

### Memoria física y virtual
- La **RAM** es memoria física instalada; la **memoria virtual** no está en la RAM: es un trozo reservado del **disco duro**, mucho más lenta, que el kernel usa para información que no cabe en RAM pero que no se quiere descartar del todo. Ejemplo del profesor: abrir Word (pesado), cerrarlo y volver a abrirlo — la segunda carga es más rápida porque parte queda en esa zona.
- El disco duro es "el cuello de botella" del ordenador desde hace años, por rápido que sea el NVMe.
- **Direcciones virtuales vs físicas**: el procesador usa un formato de direcciones distinto (más rápido) para las virtuales; el kernel mantiene una **tabla de páginas** que mapea direcciones virtuales → físicas (lo describe como "un Excel" de correspondencias).

### Paginación y segmentación (va a entrar en el test)
- El profesor remarca que **"fijo cae una pregunta de test de paginación o segmentación"** en los dos modelos de examen de este tema, aunque no entra en detalle matemático (eso lo deja para los ejercicios del temario, que considera "de primero de carrera de matemáticas" y no imprescindibles).
- **Paginación** (la que usa Linux): la memoria física se divide en bloques de tamaño fijo, normalmente **4 kB**. El proceso se divide en "páginas" del mismo tamaño que se van cargando en esos bloques. La CPU es quien ejecuta la división/corte; el **kernel** decide cuándo y cómo.
- **Segmentación**: divide en bloques de tamaño variable según necesidad, representando regiones lógicas (datos, código, etc.). El profesor dice que **ya no se usa hoy en día** por ser ineficiente y compleja (desplazamientos), aunque los sistemas antiguos la usaban. Anécdota: avisa de que en un grado universitario clásico esto se trata mucho más a fondo ("pizarras enteras" de celdas).
- Lo que pide memorizar: **nombre de las dos técnicas y cuál es la que usa Linux (paginación)**, sin necesidad de calcular desplazamientos a mano.

### Fragmentación y qué pasa cuando se acaba la memoria
- Existe fragmentación de RAM igual que en discos duros mecánicos (no en SSD). Al apagar el equipo, la RAM es **volátil**: se vacía y el problema desaparece.
- Si se agota la memoria: en Windows, pantallazo azul (demo mental: levantar 2 VMs que entre ambas superen la RAM física petan Windows). En Linux "no se suele llegar a ese punto" porque el sistema invoca procesos que eliminan tareas colgadas antes de agotar recursos — pero la recomendación real como administrador es **monitorizar con alertas/scripts/triggers** (lo compara con un trigger de BBDD) que actúen antes de llegar a ese extremo.

### Ciclo de vida de un proceso — aviso explícito de examen
El profesor insiste en que **"cuidado con el ciclo"**, es una de las preguntas de test más probables de este tema:
- Estados: **listo → ejecución → (parado | listo de nuevo) → zombi**.
- Creación → siempre pasa primero por **listo** (nunca directo a ejecución).
- **Listo → ejecución**: lo decide el planificador de CPU (parte del kernel), dando preferencia a los procesos con mayor prioridad.
- **Ejecución → parado**: por una señal, una interrupción, o porque el proceso necesita algo que no tiene (ejemplo dado: un proceso que necesita un dispositivo de E/S, como la webcam).
- **Parado → listo**: cuando la condición que lo bloqueaba se resuelve (señal de "Ok"), vuelve a la cola de listos — **nunca pasa directamente de parado a ejecución**.
- **Ejecución → zombi**: proceso ya terminado pero que sigue ocupando algo de recursos/memoria. Es un estado "peligroso" en servidores que llevan mucho tiempo encendidos. Ejemplo dado: procesos de un programa de facturación que se ejecuta una vez al mes — no hay que eliminarlos del sistema (se necesitan el mes siguiente), pero sí limpiar los que quedan colgados como zombis tras cada ejecución.
- Pregunta-trampa que el profesor dice que penaliza: contestar simplemente "si un proceso está atascado, lo mato" sin explicar el procedimiento real (lanzar `top`/`htop`, localizar el PID, aplicar `kill` con la señal adecuada).

### `fork()` y `exec` (ampliación)
- `fork()` duplica el proceso que lo invoca: crea un **proceso hijo** idéntico al padre **excepto en el PID** (dos procesos no pueden tener el mismo PID en Linux).
- Tras el `fork()`, ambos procesos (padre e hijo) siguen ejecutándose; el padre puede **esperar** a que el hijo termine o **continuar en paralelo**.
- `exec` se usa típicamente tras el `fork()` para **reemplazar el contenido del proceso hijo** por un programa nuevo (patrón `fork()` + `exec` muy habitual). El profesor avisa que esto se trabaja algo más en la práctica de la UD1 y lo deja parcialmente para que el alumnado "se pegue" con ello.

### Planificador de CPU: FIFO/LIFO y CFS
- Analogía con gestión de almacén: **FIFO** (first in, first out) — el que más tiempo lleva esperando es el primero en ser atendido, para que nadie se quede esperando indefinidamente. **LIFO** — el último en entrar tiene más prioridad.
- Linux usa por defecto el **CFS (Completely Fair Scheduler)**, diseñado para repartir tiempo de CPU de forma justa entre procesos (aunque el profesor matiza que "justo al 100%" es imposible; según él, el planificador de Linux cumple esto mejor que el de Windows).

### `nice` y `renice`: la prioridad es inversa a la intuición
- Rango de prioridad: **-20 a 19**. Cuanto **más bajo** el número, **mayor prioridad** (más ciclos de CPU, termina antes); cuanto más alto, menor prioridad. Esto es contraintuitivo y el profesor lo remarca explícitamente.
- `nice -n <valor>`: lanza un proceso con una prioridad específica desde el inicio.
- `renice <prioridad> <PID>`: cambia la prioridad de un proceso ya en ejecución (usa el PID, no el nombre).
- Caso de uso real: sistemas en tiempo real (ascensores, controladores aéreos, ciertos tipos de cirugía) necesitan que sus procesos críticos tengan siempre la máxima prioridad posible para que el procesador les dé recursos en el instante necesario.

### Comandos de procesos (matices prácticos)
- `ps aux`: a diferencia de `top`/`htop` (interactivos, muestran una vista parcial que se puede desplazar), `ps aux` da una **foto fija** de todos los procesos del sistema de una vez, ordenados por PID — útil para buscar con `grep` o volcar a fichero.
- `htop` normalmente **no viene instalado por defecto** (hay que instalarlo aparte); `top` sí. El profesor recomienda acostumbrarse primero a las herramientas básicas que trae cualquier sistema antes de pasar a las "más bonitas".
- Para matar un proceso colgado en el terminal: **Ctrl+C** "soluciona la mitad de las cosas" en Linux antes de recurrir a `kill`.
- Tabla de señales de `kill`: el profesor remarca que **hay que saberse de memoria las diferencias entre `kill -1`, `kill -9` y `kill -15`** (no solo que "kill mata un proceso"); dice explícitamente que esto es examinable y que otras señales menos comunes no hace falta memorizarlas igual.

### Hardware, módulos y montaje
- `lsblk`: lista los dispositivos de almacenamiento (discos duros/particiones) con su nomenclatura (`sda`, `sdb`... para SSD/discos modernos, `hda` para discos mecánicos antiguos). El profesor admite que él mismo la escribe mal muy a menudo.
- `lsmod` / gestión de módulos del kernel: la considera menos usada en el día a día que `lsblk`; `lspci`/`lsusb` (listar dispositivos PCI/USB) dice que "se usan una vez en la vida", frente a `lsblk` que se usa "cientos de veces".
- **Montaje en Linux**: a diferencia de Windows (donde un pendrive se detecta y se usa automáticamente), en Linux toda unidad nueva necesita un **punto de montaje explícito** (anclaje), típicamente bajo `/mnt` o `/media`. Esto se trabaja en detalle en el Tema 7 (volúmenes/LVM). En un servidor sin interfaz gráfica, administrar correctamente los puntos de montaje es aún más crítico.

### BIOS/UEFI y arranque (repaso rápido)
- BIOS (legacy, modo texto, para sistemas antiguos) vs UEFI (moderna, con entorno gráfico y Secure Boot). Mnemotécnico usado en clase: Windows 10 solía ir con BIOS legacy en equipos antiguos; Windows 11 exige UEFI.
- `systemctl` es el comando central de arranque/gestión de servicios en los Linux modernos (basados en **systemd**). Sintaxis mostrada en clase: `sudo systemctl start sshd`, con `stop`/`restart` como variantes. El profesor insiste en que esto es tarea diaria de un administrador de sistemas real.

### Logística y actividad de la UD2
- **Cambio de fecha importante**: la actividad de ASO (UD2) se entrega el **2 de noviembre**, no el 19/10 que marcaba el cronograma originalmente — el profesor lo corrige en directo en esta clase porque no se había actualizado la plataforma.
- Contenido de la actividad (según lo explicado en clase, con lo visto hasta ahora): crear un usuario llamado exactamente **`auditor`** (no vale un nombre propio), crear un directorio y aplicar permisos con `chmod` en **octal y en notación simbólica** (asignar y luego quitar, en una sola captura de pantalla limpia, sin pasos intermedios), lanzar un proceso en segundo plano, localizar su PID y modificar su prioridad con `renice`, y matarlo. La parte de "crear un script" se deja parcial porque aún no se ha visto paso de argumentos (eso es Tema 3).
- Respuestas de la actividad: **cortas (4-5 líneas)**, sin extensión de página fijada; entrega obligatoria **en PDF** ("no corrijo nada que no esté en PDF"), usando la plantilla proporcionada.
- Aviso repetido sobre el uso de IA: para la parte de scripting del examen (papel y bolígrafo) no sirve de nada depender de la IA durante el curso — quien se apoye en ella sin entender las estructuras de control (`if`, `for`, `while`) llega al examen sin saber resolverlas. El profesor lo conecta con las correcciones de los TFC del año pasado: los peores resultados fueron de quienes usaron IA para "todo" y no sabían defender ni mejorar lo que presentaban.
