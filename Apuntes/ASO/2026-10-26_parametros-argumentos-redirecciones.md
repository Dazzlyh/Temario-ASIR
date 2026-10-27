---
asignatura: Administración de Sistemas Operativos (ASO)
fecha: 2026-10-26
tema: UD3 · Sesión 2 (sin confirmar el número; la presentación de esta sesión no se ha adjuntado) · Parámetros/argumentos del script ($0, $#, $@, $1…), repasos y redirecciones > y >>
fuente: transcripción de la clase en directo (la presentación de ESTA sesión no se ha recibido; el PDF "UD3 Sesión 1" enviado junto a la transcripción es de la clase del 19/10)
---
# ASO · Parámetros de un script (`$1`, `$#`, `$@`), repasos y redirecciones (26/10)

> Anterior: [Primera clase de scripting en Bash (19/10)](2026-10-19_scripting-bash-basico.md) · Profesor: Jairo Bahillo Calvo

## Lo imprescindible

> [!important] Lo que el profesor dijo literalmente que hay que saberse
> - **`$0`** → nombre del script. **`$#`** → número de argumentos pasados. **`$@`** → lista de todos los argumentos. (clase)
> - **`$1`, `$2`, `$3`…** → cada argumento por posición. (clase)
> - **"Por teclado" = `read`. "Por argumentos" = `$1`, `$2`…** En el examen no te dirá qué comando usar: te dirá "pídelo por teclado" o "pásalo por argumentos", y hay que saber a cuál corresponde cada uno. (clase)
> - Declarar una variable, pedir un dato (por teclado o argumento) y mostrarlo por pantalla es **"básico, básico, básico"** y se pide **de memoria en el examen escrito**. (clase)
> - Ejercicios tipo examen avisados: calculadora, área/perímetro de un rectángulo (te dará las fórmulas), Fahrenheit (te dará la fórmula), minutos → horas. Hay que saber **construir el programa**, no memorizar la fórmula. (clase)
> - En un **test** solo hay una respuesta correcta a "¿qué hace esta línea?": la **literal y exacta** (p. ej. `8 + 4 = 12`), no la genérica ("suma dos números"). (clase)
> - **Dos semanas sin clase** tras esta sesión (según el profesor; fecha exacta de la siguiente clase sin confirmar). Próximo tema: **`if`** (condicionales). (clase)

## Parámetros / argumentos de un script

Un **argumento** es un valor que se escribe al lanzar el script, en la misma línea:

```bash
./saludo2.sh Ana 19
#            └─┬─┘ └┬┘
#             $1   $2
```

| Variable | Contiene | Nota |
|---|---|---|
| `$0` | Nombre del script (tal cual se llamó, p. ej. `./parametros.sh`) | Siempre existe, aunque el script no use argumentos |
| `$1`, `$2`, `$3`… | Argumento en esa posición | Si no se pasó, la variable existe pero está **vacía** (no da error) |
| `$#` | Cuántos argumentos se pasaron | Clave para validar (con `if`, próxima clase) |
| `$@` | Todos los argumentos | |

### Demo de clase (`parametros.sh`)

Script con `echo` de `$0`, `$1`, `$2`, `$3`, `$#` y `$@`. Ejecución:

```bash
./parametros.sh Hola "¿qué" tal
```

Salida descrita en clase: nombre del script, primer parámetro `Hola`, segundo `¿qué`, tercero `tal`, número de parámetros `3` y la lista de los tres. (La salida exacta del `echo` no se vio completa en la transcripción; esto es lo que el profesor narró.)

### Cómo se cuentan los argumentos (lo que más confundió)

> [!important] Los argumentos se separan por **espacios**
> - `./saludo2.sh María Eugenia 25` → `$1`=María, `$2`=Eugenia, `$3`=25 (la edad "se corre" y el nombre sale partido).
> - `./saludo2.sh "María Eugenia" 25` → `$1`=María Eugenia, `$2`=25. **Las comillas agrupan en un solo argumento.**
> - Con 4 palabras sueltas, `$#` vale 4 aunque el script solo use `$1`–`$3`: **el cuarto existe aunque no se guarde ni se muestre**. (clase)

- **El orden importa**, pero lo importante es el orden en que **tú los usas dentro del script**: debes saber qué es el 1, el 2 y el 3, y dentro puedes usarlos en el orden que quieras.
- `$0` es el nombre del programa, **no** "el primer argumento". El profesor avisa: esto es distinto de los **arrays**, donde la posición 0 sí es un dato (se verán más adelante). Una alumna lo comparó con un índice 0 de array; el profesor dijo que a él no le molesta esa idea si te ayuda, pero que puede liar cuando lleguen los arrays.

### Guardar el argumento en una variable (hábito recomendado)

```bash
#!/bin/bash
# calculadora2.sh — por argumentos
num1=$1
num2=$2
echo "Suma: $((num1 + num2))"
```

- Ventaja: usas el dato en varios sitios y el script queda legible (ej.: una ruta que se necesita varias veces con `cp`). (clase)
- El profesor admite que no siempre es necesario, pero **"acostumbraos a guardarlos lo primero en una variable"**.

> [!important] Trampa: `$((1 + 2))` NO usa el argumento
> Dentro de `$(( ))` las variables van **sin `$`**, y un `1` suelto es el **número 1**, no el argumento 1. Si en vez de `num1` escribes `1`, Bash no busca ningún argumento: calcula con el número literal y devuelve `3`. Por eso se guarda antes en una variable con nombre. (clase; la explicación del profesor en la transcripción es confusa en este tramo, esto es la interpretación más probable)

### `read` frente a argumentos

| | `read -p` (por teclado) | Argumentos (`$1`…) |
|---|---|---|
| Cuándo pide el dato | Durante la ejecución (el script **se detiene** esperando) | Al lanzar el script |
| Automatización | Mala: hace falta alguien pulsando teclas (metáfora del profesor: Homer Simpson dándole a "yes") | Buena: el script corre solo |
| Seguridad | Menos | Más control |
| Uso en el examen | "Pídelo por teclado" | "Pásalo por argumentos" |

Los argumentos son además **cómo funcionan los comandos reales**: `cp origen destino` y `chmod modo fichero` son, por dentro, programas que reciben argumentos. (clase)

## Ejercicios hechos en clase

### Repaso: `minutos.sh` (tarea para casa del 19/10)

- Dividir los minutos entre 60 → **horas**; el **resto (`%`)** → minutos sueltos (0–59). Ejemplo del PDF: 125 → `2 h y 5 min`.
- Estilo de ejercicio que puede salir en el examen. (clase)

### Repaso: ticket de la compra

- Con `read -p` y `\n` (requiere `echo -e`). Producto, precio por unidad, unidades; imprime `Pan x3 6 €` (formato del PDF del 19/10).

### Repaso de aritmética entera

```bash
n=17
echo $((n/5))     # → 3  (división entera; Bash no tiene decimales)
```

- `echo "Hola, nombre"` sin `$` imprime la palabra `nombre`; con comillas simples `'$nombre'` imprime el literal `$nombre`. (repaso de errores típicos)

### Fahrenheit (`grados.sh`)

```bash
read -p "Grados Celsius: " grados
fahrenheit=$((grados*9/5+32))
echo "$grados ºC son $fahrenheit ºF"
```

| Celsius | Fahrenheit (comprobado con la fórmula) |
|---|---|
| 0 | 32 |
| 30 | 86 |
| 37 | 98 (98,6 real: la división es entera) |

- La fórmula **la dará el profesor en el examen**; lo evaluable es construir el programa. (clase)
- Concepto nuevo: **una variable puede recibir el resultado de una operación**. Cuatro formas de dar valor a una variable: un **literal**, una **operación**, **`read`**, o una **variable/ruta del sistema** (`$HOME`, `$PWD`…). (clase)

### Calculadora por argumentos (`calculadora2.sh`)

Se copia la calculadora de `read` (`cp calculadora.sh calculadora2.sh`) y **solo se cambian las 2 líneas de lectura**:

```bash
# Antes (por teclado)
read -p "Número 1: " num1
read -p "Número 2: " num2
# Después (por argumentos)
num1=$1
num2=$2
```

El resto del script no se toca. Pruebas:

```bash
./calculadora2.sh 7 3     # suma 10, resta 4, multiplicación 21, división 2
./calculadora2.sh 8 4     # 12, 4, 32, 2
```

- **Negativos funcionan** (`-1`, `-2`…); la división con resultado decimal se queda en la parte entera. (clase)
- **Dividir entre 0 da error** ("no se puede dividir entre 0"); solo falla esa línea, las demás siguen. (clase; el mensaje exacto de Bash no se mostró)
- Aclaración a una pregunta de Sol: en los `echo` el texto **sin `$` es literal** ("Suma: ", "Número 1:"…); solo lo que lleva `$` se sustituye. El profesor confesó que, por vago, reutilizó los mismos textos del ejercicio con `read`.

### Área y perímetro de un rectángulo (`area.sh`)

Por argumentos: `$1` = base, `$2` = altura.

```bash
base=$1
altura=$2
area=$((base*altura))
perimetro=$((2*base+2*altura))
echo "Rectángulo de $base por $altura"
echo "Área: $area"
echo "Perímetro: $perimetro"
```

```bash
./area.sh 10 4
# Rectángulo de 10 por 4 · Área 40 · Perímetro 28   (comprobado: 10·4=40; 2·10+2·4=28)
```

- Con o sin espacios dentro de `$(( ))` da igual (se probó).
- Prioridad de operaciones como en matemáticas: paréntesis → `*` `/` → `+` `-`.
- Se pueden poner unidades en el `echo` (cm, cm²) como texto literal.
- Se puede hacer también con `read`; el profesor lo pedirá con la fórmula dada.

### Copia de seguridad (`copia.sh`) — primer script "de administrador"

Enunciado: recibe el nombre de un fichero, hace una copia añadiendo `.bak` al nombre, avisa y lista con `ls -l`.

```bash
#!/bin/bash
fichero=$1
copia="$fichero.bak"      # solo construye el NOMBRE; todavía no copia nada
cp "$fichero" "$copia"    # cp origen destino
ls -l                     # lista la carpeta actual
```

```bash
touch pepe.txt
./copia.sh pepe.txt       # crea pepe.txt.bak
```

> [!important] Cosas que se vieron fallar
> - **Si el fichero no existe**, `cp` da error (no se puede copiar algo que no existe). Comprobarlo con `if` llega la próxima clase.
> - **`ls -l` sin ruta lista la carpeta donde estás**, no la del fichero. Recordar rutas relativas y absolutas.
> - **Construir el nombre ≠ hacer la copia**: la línea `copia="$fichero.bak"` solo guarda texto en una variable; el `cp` es lo que copia.
> - Sol acertó: en `cp origen destino`, origen = `$fichero`, destino = `$copia`.

- **Resultado `pepe.txt.bak`**: el nombre conserva la extensión original. Manuel preguntó cómo quitar el `.txt`; el profesor dijo que requeriría limpiar el nombre (expresión regular/otras herramientas, a ver más adelante) y que **ese tipo de filtrado aparece en el script de la actividad** (sin confirmar). Si el fichero se llama `pepe` sin extensión, sale `pepe.bak`.

## Redirecciones `>` y `>>`

Ya existían en clase de años anteriores; el profesor las introduce al final y avisa de que son **"superimportantes"**.

| Operador | Efecto | Ejemplo |
|---|---|---|
| `>` | Envía la salida a un fichero y **lo machaca** (borra lo que había) | `echo hola > pepe.txt` |
| `>>` | **Añade** al final del fichero | `echo adiós >> pepe.txt` |

```bash
echo hola > pepe.txt        # no muestra nada por pantalla
echo adiós >> pepe.txt
cat pepe.txt                # hola
                            # adiós
ls -l > pepe.txt            # guarda el listado con permisos en un fichero
ls -l >> pepe.txt           # y esto añade otro listado debajo
```

- Para un registro: **la primera vez `>` (empieza limpio) y después `>>`** (acumula). Si todas las líneas llevan `>`, solo queda la última (error que enseñó con `operaciones.txt`: solo guardaba el módulo). (clase)
- Utilidad de administración: guardar permisos, listados, informes en ficheros con fecha.
- En la demo el contador de `ls -l` pasó de 68 a 72 al repetir, sin que el profesor lo explicase (probablemente porque el propio `pepe.txt` crecía y se listaba a sí mismo; **inferencia mía, sin confirmar**).
- **Para probar en casa**: redirigir las salidas de la calculadora a `operaciones.txt`.

## Si algo no funciona

| Síntoma | Causa | Solución |
|---|---|---|
| Salen 3 en vez de lo esperado con `$((1+2))` | Escribiste el número en vez del argumento/variable | Guarda `$1` en `num1` y usa `num1` |
| `María Eugenia` sale partido | Argumentos separados por espacio | Entre comillas: `"María Eugenia"` |
| `./copia.sh` da error de cp | El fichero no existe | `touch fichero` primero (o `if` más adelante) |
| Un `echo` imprime `Número 1:` y no el valor | Falta el `$` | `$num1` |
| El log solo tiene la última línea | Todos los `echo` con `>` | `>` el primero, `>>` el resto |

## Dudas y cosas sin confirmar

- **Presentación de la sesión 26/10 no recibida**: el nombre exacto de la sesión (UD3 Sesión 2) y la tabla de "tipos de parámetros" están **inferidos**. En la transcripción el profesor enumera `$0`, `$#` y `$@` como lo imprescindible y deja en duda otros ("este me pongo un poco más en duda"), pero el audio está cortado y no queda claro si hay un cuarto (p. ej. `$*`, o `$1…$9` como grupo). **Sin confirmar**; conviene mirar la presentación de la clase.
- El "recordatorio" del profesor: la **Actividad UD2 se entrega el 2/11**. Está en PDF y por secciones. La "tarea 4" (`systemctl`) se eliminó del enunciado pero **sigue en la rúbrica**, así que quedan 4 criterios y el 20 % de `systemctl` se reparte entre los otros 4. Solo ~3 personas la habían entregado. **Hoy fue el último día de dudas.** (clase)
- Hay una **entrega de borrador del proyecto**: el profesor la mencionó de pasada ("tenemos que entregar borrador… ah, sí, cierto") y pidió que **quienes están con él en el proyecto se queden al final**. No sé si Dani está en ese grupo ni la fecha del borrador: **sin confirmar**.
- Faltó el mensaje exacto de error de Bash al dividir entre 0; no se mostró en clase.

## Logística y para llevar a casa

- [ ] Entregar la **Actividad UD2** el **2/11** (PDF, secciones, 4 criterios en la rúbrica).
- [ ] Practicar en estas 2 semanas: `calculadora2.sh` (argumentos), `area.sh`, `grados.sh`, `copia.sh`, `minutos.sh` y el ticket. El profesor sube el PDF con los ejercicios de hoy.
- [ ] Redirigir la salida de la calculadora a `operaciones.txt` (`>` y `>>`).
- [ ] Revisar la presentación de la sesión para confirmar los "tipos de parámetros".
- [ ] Comprobar si hay que entregar el borrador del proyecto y cuándo.
- Próxima clase (fecha sin confirmar): **`if`** (¿existe el fichero?, valores, letras…), validación de `$#`.
