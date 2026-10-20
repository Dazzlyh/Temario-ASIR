---
asignatura: Administración de Sistemas Operativos (ASO)
fecha: 2026-10-19
tema: Tema 2 (continuación) · primera clase de scripting en Bash: scripts, echo, variables, comillas, read y aritmética
fuente: transcripción de la clase en directo
---
# ASO · Primera clase de scripting en Bash: scripts, variables, read y aritmética (19/10)

> Anterior: [Tema 2: repaso procesos, hardware y arranque (05/10)](2026-10-05_repaso-procesos-hardware-arranque.md) · Profesor: Jairo Bahillo Calvo

Primera clase "de verdad" de scripting (lo que el profesor llama **"la unidad fuerte del tema"**), empezando desde nivel 0 aunque parte del grupo ya tenga experiencia previa en programación (JavaScript de W, Go, etc.). Avisa explícitamente de que lo visto en estas 6 horas de clase programadas es solo la base: *"que nadie piense que con esto va a trabajar en el día a día; tenéis que seguir desarrollándoos vosotros por vuestra cuenta"*.

## Logística y avisos

- **Actividad de la UD2 (ASO)**: se confirma de nuevo la fecha de entrega, **2 de noviembre**, aunque ese día no haya clase. Entrega obligatoria **en PDF**, dividida en secciones para que sea más fácil de corregir.
- El profesor comenta que tenía calendadas 6 sesiones para esta unidad pero el calendario se ha quedado reducido por festivos en Madrid, así que ha "estirado" el temario lo máximo posible dentro de la programación.
- Usa en esta clase una **máquina virtual nueva con Ubuntu 26.04** (hasta ahora usaba 22.04), que durante la clase va notablemente lenta (la VM tiene asignados 6 núcleos y 8 GB de RAM); comenta que si le sigue dando problemas, volverá a 22.04. Insiste en que cada alumno puede usar la distribución que prefiera, avisando de que los comandos de instalación de paquetes cambian entre distribuciones basadas en Debian y otras.

## Qué es un script

- Un **script** es un fichero de texto plano que contiene **comandos secuenciales**: los ejecuta en el orden en que están escritos, sin control de flujo (nada de `if`/`for` todavía — eso llega en próximas sesiones/Tema 3). Punto remarcado como **imprescindible para el test**.
- Se puede escribir desde la propia terminal (`nano`, `vi`...) o desde cualquier IDE (Visual Studio Code, etc.). Lo que **no se puede hacer nunca** es escribirlo en un procesador de texto tipo Word y copiar/pegar — hay que usar el formato de texto plano correcto.
- En Linux se usa normalmente **Bash** como shell, aunque se pueden instalar y usar otros (zsh, etc.); lo importante es conocer las diferencias si se cambia de shell.
- Para qué sirven los scripts (según lo explicado en clase):
  - **Automatización**: ejecutar tareas de forma periódica (con cron — el profesor lo pronuncia "chrol" — cada X segundos/minutos/horas/días/meses/años).
  - **Reducir tareas repetitivas**: ejemplo del aula — no se puede crear usuario por usuario a mano con el ratón en 20 equipos, hay que automatizarlo.
  - **Gestión de sistemas**: lanzar scripts que liberen recursos, maten procesos atascados o limpien datos cuando el sistema está sobrecargado.
  - **Portabilidad**: un script escrito para Bash funciona en cualquier sistema que tenga Bash instalado.
- Nota aparte de un alumno (Manuel Doña García, sin verificar por el profesor): muchas herramientas de infraestructura/contenedores (menciona "Terraform" y similares) están programadas en **Go**, que se está volviendo relevante para este tipo de automatización junto a Python.

## Primer script: shebang y permisos de ejecución

Pasos mostrados en vivo para crear y lanzar el primer script (`holamundo.sh`):

```bash
nano holamundo.sh
```

Contenido mínimo:

```bash
#!/bin/bash
# comentario de ejemplo
echo "Hola mundo"
```

- La **primera línea** (`#!/bin/bash`, el *shebang*) hay que "tatuársela": es obligatoria para que el sistema sepa con qué intérprete ejecutar el script.
- Las líneas que empiezan por `#` son **comentarios** y no se ejecutan.
- Después de guardar, hay que dar **permisos de ejecución**:

```bash
chmod +x holamundo.sh
# equivalente en notación octal: chmod 755 holamundo.sh
```

- Y ejecutarlo con ruta explícita:

```bash
./holamundo.sh
```

### Plantilla reutilizable (`esqueleto.sh`)

Para no perder tiempo repitiendo shebang + permisos en cada script nuevo, el profesor se crea una plantilla base una sola vez:

```bash
nano esqueleto.sh
# dentro: #!/bin/bash y comentarios base
chmod +x esqueleto.sh
```

Y a partir de ahí, para cada script nuevo simplemente la copia con otro nombre:

```bash
cp esqueleto.sh tarjeta.sh
nano tarjeta.sh
```

(los permisos de ejecución se heredan de la copia, así no hay que repetir el `chmod` cada vez).

## `echo`: las 3-4 opciones que hay que saber

El profesor pide conocer al menos estas variantes de `echo`:

| Opción | Efecto |
|---|---|
| `echo "texto"` | Imprime el texto y salta de línea al final (comportamiento por defecto) |
| `echo -n "texto"` | Imprime el texto **sin** salto de línea al final |
| `echo -e "texto"` | Habilita la interpretación de secuencias de escape con barra invertida (`\t`, `\n`...) dentro del texto |

Detalles mostrados en el ejemplo `tarjeta.sh`:

```bash
echo -e "Nombre: \t Pepe Garcia"
```

- `\t` genera una **tabulación**.
- `\n` genera un **salto de línea dentro de una misma cadena** de `echo -e` (el profesor aclara que es la barra "invertida", la misma dirección que usa Windows para rutas — no la barra normal `/`).
- Alternativa a `\n`: usar varios `echo` seguidos (uno con `-n` para no saltar línea y encadenar el texto, u otro `echo` normal en la siguiente línea) — el resultado final es el mismo; el profesor dice que a partir de ahora usará siempre la opción que más le gusta, sin que haya una única forma "correcta".
- **Importante**: hay que poner siempre **comillas dobles** (`" "`) alrededor del texto del `echo`; si no, el sistema puede interpretar mal espacios o caracteres y falla.

## Variables

- Una variable es, en palabras del profesor, **"una caja de zapatos"**: un nombre que guarda un valor, da igual el tipo de dato (texto, número, etc.).
- **Bash no es un lenguaje tipado**: no se declara el tipo de dato al crear la variable, acepta lo que se le meta.
- **Declaración** — regla de examen remarcada explícitamente: **nunca debe haber espacios antes ni después del signo `=`**.

```bash
nombre=Jairo        # correcto
nombre = Jairo       # INCORRECTO — da error al ejecutar
```

- **Acceso al valor**: con el símbolo `$` delante del nombre de la variable (`$nombre`). El símbolo `$` es el que transforma el nombre de la variable en su contenido al mostrarla.
- **Error típico marcado como "0 en la pregunta" (falla directamente en examen)**: poner el `$` al declarar la variable en vez de al leerla:

```bash
$nombre=Jairo   # INCORRECTO — el $ va solo al leer la variable, nunca al declararla
nombre=Jairo    # correcto
echo "$nombre"  # correcto, aquí sí lleva el $
```

- **Normas para el nombre de una variable**: sin tildes, sin eñe, sin espacios, **no puede empezar por un número** (igual que un nombre de usuario Linux no puede empezar por número), sí se permite guion bajo (`_`). Son **sensibles a mayúsculas/minúsculas** (`case sensitive`): `Carpeta` y `carpeta` son variables distintas, y confundirlas es un error muy habitual que el profesor reprodujo en directo.
- Convención de nombres que usa el profesor (no es obligatoria, cada alumno puede usar la suya): tipo *camelCase* — cuando el nombre tiene dos palabras, se juntan y la segunda empieza en mayúscula (ej. `nombreUsuario`). Pide nombres ni demasiado cortos (`a`, `b`, `c`) ni excesivamente largos tipo "nombreDelUsuarioDelFormularioDeLaPaginaDeNoSeQue".

### Variables del sistema (3 que hay que memorizar sí o sí)

Demostradas en vivo ejecutando el mismo script con distintos usuarios para ver cómo cambia el resultado:

| Variable | Qué devuelve |
|---|---|
| `$USER` | El usuario que está ejecutando el script |
| `$HOME` | La carpeta personal (home) de ese usuario |
| `$PWD` | El directorio desde el que se está ejecutando el script |

- El profesor remarca que estas **3 variables son examinables obligatoriamente** ("fijo que hay que estudiarlas") — a diferencia de las variables de fecha (vistas más adelante en la clase), que **no hace falta memorizar**.
- Utilidad real explicada: permiten escribir scripts **portables**, que funcionan igual para cualquier usuario sin tener que *hardcodear* un nombre concreto (ejemplo dado: generar una carpeta en el home de cada usuario de un aula sin tener que escribir una línea distinta por alumno).

### Comillas dobles vs. comillas simples

Diferencia mostrada con el mismo `echo`:

```bash
echo "$nombre"   # con comillas dobles: sustituye por el VALOR de la variable
echo '$nombre'   # con comillas simples: imprime el texto literal "$nombre", NO lo sustituye
```

- Con comillas simples, Bash no interpreta el `$`, lo muestra tal cual como texto.
- Regla práctica recomendada por un alumno (Manuel) y aceptada por el profesor: usar comillas dobles por defecto para todo, y recurrir a comillas simples solo cuando se quiera mostrar un símbolo especial (p. ej. un literal `$18`) sin que se interprete.

## Ejercicio en directo: encontrar los 3 errores

El profesor preparó un script con **3 fallos deliberados** y pidió al grupo que los identificara antes de ejecutarlo (lo compara con las preguntas de "detectar fallos en el código" del examen — el año pasado hubo un ejercicio con 5 fallos en un mismo bloque de código):

1. **Primera línea mal escrita** (el shebang/primera línea no estaba bien puesta) → al ejecutar, salía un error de "orden no encontrada" y solo devolvía una palabra suelta en vez del mensaje completo.
2. **Faltaba el `$` al leer la variable** dentro del `echo` (`echo "Hola, nombre"` en vez de `echo "Hola, $nombre"`) → imprimía literalmente la palabra "nombre" en vez del valor.
3. **Comillas simples en vez de dobles** alrededor de una variable → no sustituía el valor, mostraba el texto literal.

El profesor insiste en que este tipo de fallo (saber **explicar el procedimiento de depuración**, no solo "decir la respuesta") es justo lo que se evalúa en el examen, y avisa de que **el año que viene también habrá una pregunta de este estilo** con varios fallos a encontrar en un mismo script.

## Pedir datos al usuario: `read`

Dos formas equivalentes mostradas, con resultado funcional idéntico:

```bash
# Forma 1: en dos líneas
echo -n "Introduce tu nombre: "
read nombre

# Forma 2: en una sola línea con -p
read -p "Introduce tu nombre: " nombre
```

- `-p` muestra el mensaje y deja el cursor esperando la entrada en la misma línea (evita tener que poner un `echo -n` aparte).
- El profesor dice que, a partir de esta clase, él siempre usará la forma de una línea (`read -p`) porque le resulta "más limpia y más cómoda", pero aclara que **el resultado final es el mismo** y cada uno puede usar la que prefiera.
- Un alumno (Manuel) preguntó por el flag `read -n` (limitar el número de caracteres leídos sin necesidad de pulsar Intro); el profesor reconoció no haberlo usado nunca y lo dejó sin confirmar en clase.

### Ejemplo: crear una carpeta con el nombre que indique el usuario

Patrón de "pensamiento computacional" que el profesor pide aplicar siempre: **desgranar la tarea grande en tareas pequeñas** y traducir cada una a una instrucción.

```bash
read -p "Nombre de la carpeta: " carpeta
mkdir $carpeta
```

- Error en directo de una alumna (Sol): usó un nombre de variable distinto en el `read` y en el `mkdir` (ej. leyó en `nombre` pero usó `$carpeta` en el `mkdir`) → el comando fallaba porque la variable que realmente usaba el `mkdir` estaba vacía (error de "no se proporcionaron los argumentos"). Lección remarcada: el nombre de la variable debe ser **exactamente el mismo** (mayúsculas incluidas) en todo el script.
- El profesor adelanta que repetir esta misma tarea muchas veces (p. ej. crear varias carpetas) se resolverá más adelante con una estructura de control tipo **`for`** (todavía no vista).

## Operaciones aritméticas en Bash

- Bash **no suma directamente** escribiendo `echo 7 + 2`; hay que usar la sintaxis de expansión aritmética: **doble paréntesis** precedido de `$`.

```bash
suma=$((a + b))
resta=$((a - b))
```

- **Dentro de los dobles paréntesis `$(( ))`, las variables se escriben SIN el signo `$`** (es la excepción a la regla general de leer variables con `$`).
- Operadores mostrados como imprescindibles: `+` (suma), `-` (resta), `*` (multiplicación — se probó específicamente porque el asterisco es un carácter reservado del shell y puede dar problemas fuera de `$(( ))`, pero funciona bien dentro), `/` (división), `%` (módulo: el resto de la división — el profesor adelanta que se usará más adelante para el ejercicio de calcular la letra del DNI, cuando se vea el tema de arrays), y `**` (exponente). Mencionó también de pasada el incremento de una variable sobre sí misma (sumar y volver a guardar en la misma variable) como algo para practicar esta semana, sin entrar en detalle en esta clase.
- Demo en vivo: pide dos números al usuario (10 y 5), calcula `suma` (15, correcto) y `resta`; en un primer intento la resta salió **0** porque el profesor no había vuelto a leer/actualizar los datos antes de calcularla — ejemplo real de cómo un dato no actualizado rompe el resultado.

### Ejercicio final: "¿cuántos meses has vivido?"

Último ejercicio de la clase, combinando todo lo anterior (`read`, variables, operadores aritméticos):

- Se pide el año de nacimiento al usuario.
- Se extrae el año con una expresión regular ya preparada por el profesor — remarca explícitamente que **esta expresión regular concreta no hay que memorizarla**, la daría él mismo en el examen si hiciera falta.
- Se calcula la edad aproximada con `año_actual - año_nacimiento` y se usa el operador módulo (`%`) para obtener un resto (meses aproximados).
- Bug corregido en directo: faltaba un espacio entre variables concatenadas en el `echo`, lo que juntaba los números sin separación en el mensaje final ("has vivido un..." sin espacio antes del número).
- El profesor remata la demo pidiendo también la edad "a mano" (sin fecha) y recalculando con los mismos operadores, a modo de repaso conjunto de variables + aritmética.

## Para llevar a casa

- Primera clase real de scripting en Bash: fichero de texto con comandos secuenciales, sin estructuras de control todavía (eso llega en próximas clases/Tema 3).
- Memorizar sin falta: la primera línea del script (`#!/bin/bash`), cómo dar permisos de ejecución (`chmod +x` / `chmod 755`), las 3 variables de sistema (`$USER`, `$HOME`, `$PWD`), la diferencia entre comillas simples y dobles, y la sintaxis de aritmética con `$(( ))` (variables sin `$` dentro).
- Errores de examen ya avisados explícitamente: espacios alrededor del `=` al declarar una variable, poner el `$` al declarar en vez de al leer, y confundir el nombre de una variable entre distintas líneas del script (mayúsculas incluidas).
- Habrá en el examen un ejercicio de "encontrar los fallos" en un script ya escrito — este tipo de pregunta es examinable de forma explícita.
- Actividad UD2: entrega el **2 de noviembre**, en PDF, dividida en secciones.
- Pendiente para próximas clases: estructuras de control (`if`, `for`), paso de argumentos y módulo (arrays, del algoritmo del DNI).
