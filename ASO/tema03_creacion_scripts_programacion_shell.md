# Tema 3. Creación de scripts. Programación en Shell
*Administración de Sistemas Operativos*

## Índice
Esquema · 3.1 Introducción y objetivos · 3.2 Parámetros y variables · 3.3 Gestión de la entrada y la salida de datos · 3.4 Condicionales y otras estructuras de control · 3.5 Funciones · A fondo · Entrenamientos

## Esquema
Los comandos de la shell ofrecen funcionalidades que pueden potenciarse con variables, funciones o estructuras de control.

- **Parámetros y variables**: conceptos de parámetros, de variables y uso de arrays.
- **Gestión de la entrada y salida de datos**: comando `echo` (salida estándar por pantalla), comando `read` (solicitar información al usuario y guardarla en una variable), operadores de redirección (controlan el flujo de datos entre comandos, archivos y dispositivos).
- **Condicionales y funciones**: operadores lógicos, operadores aritméticos, estructuras if-else, case, repetición while, repetición for, definición y uso de funciones.

---

## 3.1. Introducción y objetivos
La programación en shell (*shell scripting*) consiste en integrar los comandos con elementos adicionales (variables, funciones, estructuras de control) dentro de scripts que ayudan, entre otras cosas, a automatizar tareas rutinarias. La finalidad es poder entender, modificar y reutilizar scripts de terceros y elaborar otros propios.

Objetivos:
- **Comprender y utilizar variables y parámetros**: declararlas y pasar argumentos a los scripts.
- **Manejar la entrada y salida de datos.**
- **Dominar las estructuras de control**: `if`, `for`, `while`.
- **Familiarizarse con las funciones**: organización y reutilización de código.
- **Crear scripts sencillos**: manipulación de archivos, automatización de tareas.
- **Depurar y optimizar scripts.**

---

## 3.2. Parámetros y variables
Son datos asociados a un nombre guardados en una posición de memoria. Se accede a su valor escribiendo su nombre precedido de `$`.

### Parámetros
- **Parámetros posicionales**: guardan los argumentos pasados al script desde la línea de comandos, en variables reservadas `$1`, `$2`, `$3`… (`$1` = primer argumento).
- **Parámetros especiales**:
  - `$#`: número total de parámetros pasados al script.
  - `$0`: nombre del script invocado.
  - `$$`: PID del shell que ejecuta el script.
  - `$@`: recoge en un array todos los parámetros aportados.

### Variables estándar
```bash
#Declaración de una variable (definición y asignación de valor).
nombre="Pepe"
#acceso e impresión por pantalla del valor de la variable
echo "hola $nombre"
```

### Arrays
Estructuras capaces de almacenar de forma estructurada varios datos en diferentes posiciones; son iterables.

```bash
#Declaración de un array (definición y asignación de valores)
array=(1 2 3 4 5 6 7 8 9 10)
#Declaración de array con diferentes tipos de dato
Array_mixta=(Uno 2 tres 4 cinco)
```
Con diez posiciones, la primera es `[0]` y la última `[9]`. Acceso: `${array[0]}`.

> Nota: en bash real no se pueden dejar espacios alrededor del `=` (`array=(...)`); el material los muestra con espacios en algunos ejemplos.

**Acceso a los elementos del array**

| Ejemplo | Descripción |
|---|---|
| `echo ${array[1]}` | Segunda posición del array. |
| `echo ${array[@]}` | Todas las posiciones en una línea. |
| `echo ${array[@]:1:3}` | Rango: desde la posición 1, un total de tres posiciones. |

**Conteo**

| Ejemplo | Descripción |
|---|---|
| `echo ${#array[@]}` | Número de elementos (longitud del array). |
| `echo ${#array[1]}` | Caracteres dentro de una posición. |

**Modificación:** `array[1]="dos"` cambia el segundo elemento (posición 1).

**Eliminación:** `unset array[2]` elimina el tercer elemento; `unset array` elimina el array completo.

---

## 3.3. Gestión de la entrada y la salida de datos

### Comando `echo`
Salida estándar de mensajes por pantalla; también imprime el valor de variables.

| Opción | Comando |
|---|---|
| `echo -n` | No genera el salto de línea tras el mensaje. |
| `echo -e` | Habilita opciones de barra invertida (si se usa -e, el texto va entre comillas dobles). |
| `echo -e "hola \\ adiós"` | Inserta una barra inclinada. |
| `echo -e "hola \c adiós"` | No muestra el texto escrito después de `\c`. |
| `echo -e "hola \r adiós"` | No muestra el texto escrito antes de `\r`. |
| `echo -e "hola \n adiós"` | Salto de línea entre palabras. |
| `echo -e "hola \t adiós"` | Tabulación. |
| `echo -e "hola \e adiós"` | Simula la pulsación de "escape". |
| `echo -e "hola \b adiós"` | Simula la pulsación de "retroceso". |

### Comando `read`
```bash
#Enviamos un mensaje por pantalla solicitando el dato al usuario
echo "Por favor, introduzca su nombre"
#Usamos read para guardar el valor en la variable nombre
read nombre
```
Con la opción `-p`: `read -p "por favor, introduzca su nombre" nombre`.

### Operadores de redirección
Controlan el flujo de datos entre comandos, archivos y dispositivos.

Listar un directorio y guardar el resultado:
```bash
ls -l ./alumnos/cursos > listado.txt
```
Leer líneas de un fichero externo con `while` y `<`:
```bash
while read linea; do
   echo "$linea"
done < archivo.txt
```

**Ejemplo de repaso (entrada, manipulación y salida).** Fichero `Prueba_paises.txt`:
```
España/Madrid
Alemania/Berlín
Argentina/Buenos_Aires
Austria/Viena
Japón/Tokio
Francia/París
Portugal/Lisboa
Reino_Unido/Londres
Italia/Roma
Estados_Unidos/Washington
```
Script que separa el fichero (recibido como parámetro) en `paises.txt` y `capitales.txt`:
```bash
#!/usr/bin/bash

cut -d/ -f 1 $1 >> paises.txt
cut -d/ -f 2 $1 >> capitales.txt

echo -e "\nSe ha dividido el fichero" $1
echo "en dos ficheros, países y capitales"
```

---

## 3.4. Condicionales y otras estructuras de control

### Operadores lógicos

| Operador | Significado |
|---|---|
| `-lt` | *less than*, menor que (`<`). Ej.: `1 -lt 2`. |
| `-gt` | *greater than*, mayor que (`>`). Ej.: `2 -gt 1`. |
| `-le` | *less equal*, menor o igual que (`<=`). |
| `-ge` | *greater equal*, mayor o igual que (`>=`). |
| `-eq` | *equal*, exactamente igual (`==`). |
| `!` | *not*, negación. |
| `-ne` | *not equal*, distinto de (`<>` o `!=`). (El material lo escribe como `-!eq`.) |
| `&&` | *and*, (y) o adicionalmente. |
| `\|\|` | *or*, opcionalidad. |

### Operadores aritméticos

| Operador | Función |
|---|---|
| `+` | Suma. |
| `-` | Resta. |
| `*` | Multiplicación. |
| `/` | División. |
| `%` | Módulo: resto de una división. |
| `**` | Exponente. |
| `num=$((num+1))` | Suma una unidad a `num` (a veces se admite `num++`). |
| `num=$((num-1))` | Resta una unidad (a veces `num--`). |

El operador de multiplicación puede escribirse con barra inclinada (`\*`) cuando no se quiere que bash lo confunda con el carácter comodín.

La ejecución normal de un script es de izquierda a derecha y de arriba abajo (**flujo del script**). Las **estructuras de control de flujo** (condicionales y bucles) lo alteran.

### Condicional IF ELSE
```bash
#SINTAXIS
if [ condición ]; then
  bloque de código
elif [ condicion ]; then
  bloque de código
else
  bloque de código
fi
```
Ejemplo:
```bash
read -p "introduzca su nombre" nombre
read -p "introduzca su edad" edad

if [ $edad -lt 18 ]; then
  echo $nombre "es menor de edad"
elif [ $edad -lt 100 ]; then
  echo $nombre "es mayor de edad"
else
  echo $nombre "tiene más de 100 años!!"
fi
```
- `if [ $edad -lt 18 ]`: si es menor de 18 se ejecuta su bloque; si no, pasa al `elif`.
- `elif [ $edad -lt 100 ]`: entre 18 y 99.
- `else`: engloba todo lo demás.
- La estructura termina con `fi`.

### Condicional CASE
```bash
#SINTAXIS
case $variable in
   1) código para variable=1 ;;
   2) código para variable=2 ;;
   3) código para variable=3 ;;
   *) código para un valor distinto
esac
```
Ejemplo:
```bash
read -p "Seleccione un número" opcion

case $opcion in
   1) echo "ha seleccionado la opción 1" ;;
   2) echo "ha seleccionado la opción 2" ;;
   3) echo "ha seleccionado la opción 3" ;;
   *) echo "Introduzca una opción correcta"
esac
```
Termina con `esac`.

### Bucle WHILE
Repite un bloque de código mientras se cumpla una condición.
```bash
#SINTAXIS
while [ condición ]; do
   código del bucle
done
```
Ejemplo:
```bash
read -p "introduzca un número" num
while [ $num -le 100 ]; do
  echo "iteración while número: " $num
  num=$((num+1))
done
```
(Con la condición `-le 100` se ejecuta mientras `num` sea menor o igual que 100.) Se cierra con `done`.

### Bucle FOR
Repite un bloque un número determinado de veces.
```bash
#SINTAXIS
for variable in {rango de valores}; do
   código a repetir
done

#Saludo a los 10 jugadores
for numero in {1..10}; do
   echo "Hola jugador " $numero
done
```
Recorrer un array:
```bash
#Declaramos el array
array=("uno" "dos" "tres")

# Declaramos el bucle
for i in "${array[@]}"
do
  echo $i
done
```
Variante equivalente al while:
```bash
#SINTAXIS
for ((valor_base; condición; incremento)); do
   código del bucle
done

for ((i=1 ;i<=100 ;i++ )) do
  echo "iteración número: " $i
done
```

### `continue` y `break`
Se usan normalmente dentro de un condicional interno del bucle.

- **`break`**: rompe el bucle de inmediato.
```bash
for (( i=1 ; i<=100 ; i++ )) do
   if [ $i -eq 50 ]; then
     echo "salimos del bucle en 50"
     break
   else
     echo "iteración número: " $i
   fi
done
```
- **`continue`**: salta a la siguiente iteración obviando el código posterior.
```bash
for (( i=1 ; i<=100 ; i++ )) do
   if [ $i -eq 50 ]; then
     echo "saltamos el 50"
     continue
   fi
     echo "iteración número: " $i
done
```

> **Nota:** hay que prestar especial atención a los espacios en la sintaxis. Por ejemplo, `if [$i -eq 50]; then` (sin espacios dentro de los corchetes) no funciona correctamente.

---

## 3.5. Funciones
Encapsulan un bloque de código para reutilizarlo y evitar repetición. Dos formas de declararlas:

```bash
function mi_funcion {
   echo "hola mundo"
}

mi_funcion() {
   echo "hola mundo"
}
```
Se invocan tecleando su nombre. Pueden usar variables:
```bash
nombre="Pepe"
mi_funcion() {
   echo "hola mundo soy " $nombre
}
mi_funcion
```
Variables internas con `local`:
```bash
nombre="Pepe"

mi_funcion(){
   local saludo_ENG="Hello"
   local saludo_ES="Hola"

   echo "Inglés" $saludo_ENG $nombre
   echo "Español" $saludo_ES $nombre
}

mi_funcion
```

---

## A fondo
- **Curso de Linux: comandos básicos e introducción a la shell bash.** Antonio Sánchez Corbalán. Lista de reproducción: https://www.youtube.com/watch?v=qWrgoCP6q3M&list=PLN9u6FzF6DLTRhmLLT-ILqEtDQvVf-ChM
- **Curso básico de bash scripting desde cero.** El Rincón del Hacker. Lista (ocho vídeos cortos): https://www.youtube.com/playlist?list=PLTDhSVtYdnF7IbtGoKz9UTra4Dae8_tBK
- **Ejercicios resueltos de Linux Shell Script en Bash.** Antonio Sánchez Corbalán. Lista: https://www.youtube.com/watch?v=Y950V89-as&list=PLN9u6FzF6DLSdJLrA1U_ss6sPAm3DXDC4
- **Manual de referencia de bash.** GNU. https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html — la ayuda de un comando se consulta con `--help` o `man` (ej.: `read --help` o `man read`).

---

## Entrenamientos

### Entrenamiento 1 — `borrar_vacios.sh`
**Enunciado:** script al que se pasa como parámetro la ruta de un directorio; revisa si hay directorios vacíos y los elimina. Solo debe mostrar los `echo` (ningún error estándar).

Estructura de prueba:
```bash
mkdir -p prueba/dir1 prueba/dir2 prueba/dir3
```
Script:
```bash
#!/usr/bin/bash

echo Se borrarán todos los directorios vacios
echo de la ruta $1

# Utilizamos el comando find pasándole
# el parámetro introducido como ruta donde
# buscar directorios vacios y eliminarlos
find $1 -empty -type d -exec rmdir "{}" ";" 2>/dev/null
sleep 1
echo Fin del script
```
Ejecución: `bash borrar_vacios.sh ./prueba`

`$1` es la ruta del parámetro sobre la que se ejecuta `find`, y los errores estándar se anulan con `2>/dev/null`.

### Entrenamiento 2 — `compara_numeros.sh`
**Enunciado:** solicitar dos números (num1 y num2) y decir si num1 es mayor, menor o igual que num2.

```bash
#!/usr/bin/bash

echo Vamos a comparar dos números
sleep 1
read -p "Introduzca el primer número: " num1
read -p "Introduzca el segundo número: " num2
echo -e "\n"

if [ $num1 -gt $num2 ]; then
  echo $num1 es mayor que $num2

elif [ $num1 -lt $num2 ]; then
  echo $num1 es menor que $num2

else
  echo $num1 y $num2 son el mismo número
fi

echo Fin del script
```
Cubre las tres opciones con `-lt` y `-gt`; y `read -p` evita ejecutar dos líneas (echo + read).

### Entrenamiento 3 — `consulta_dias_mes.sh`
**Enunciado:** mostrar los meses del año y pedir el número del mes; devolver el número de días (usar `case`); repetir hasta que se seleccione «salir».

```bash
#!/usr/bin/bash

echo COMIENZA LA EJECUCION DEL SCRIPT
echo =================================
echo      ===== MESES DEL AÑO =====
echo =================================

echo 1. enero
echo 2. febrero
echo 3. marzo
echo 4. abril
echo 5. mayo
echo 6. junio
echo 7. julio
echo 8. agosto
echo 9. septiembre
echo 10. octubre
echo 11. noviembre
echo 12. diciembre
echo 13. SALIR
echo =================================

while [ $mes != 13 ]; do
  read -p "seleccione un numero de mes: " mes
  case $mes in
     1) echo ha seleccionado Enero con 31 dias ;;
     2) echo ha seleccionado Febrero con 28 dias ;;
     3) echo ha seleccionado Marzo con 31 dias ;;
     4) echo ha seleccionado Abril con 30 dias ;;
     5) echo ha seleccionado Mayo con 31 dias ;;
     6) echo ha seleccionado Junio con 30 dias ;;
     7) echo ha seleccionado Julio con 31 dias ;;
     8) echo ha seleccionado Agosto con 31 dias ;;
     9) echo ha seleccionado Septiembre con 30 dias ;;
     10) echo ha seleccionado Octubre con 31 dias ;;
     11) echo ha seleccionado Noviembre con 30 dias ;;
     12) echo ha seleccionado Diciembre con 31 dias ;;
     13) exit ;;
     *) echo por favor, selecciones mes válido
  esac
done

echo FIN DEL SCRIPT
```
> Nota: en el material la captura inicializa `VARIABLE=HOLA` antes del bucle, así que `$mes` está vacío y `[ $mes != 13 ]` falla en la primera comprobación; conviene inicializar `mes` o usar comillas (`[ "$mes" != 13 ]`).

El `case` está dentro de un `while` cuya condición es que el usuario no elija la opción 13 («salir»).

### Entrenamiento 4 — `crear_carpetas.sh`
**Enunciado:** recibe un año como parámetro; crea el directorio `año_parámetro` y dentro doce carpetas (mes + año); lista el contenido del directorio. Usar `for`.

```bash
#!/usr/bin/bash

# Recogemos el parametro en la variable año
año=$1

# Declaramos el array de meses
meses=("Enero" "Febrero" "Marzo" "Abril" "Mayo"
"Junio" "Julio" "Agosto" "Septiembre" "Octubre"
"Noviembre" "Diciembre")

# Creamos el directorio con el año recogido como parámetro
mkdir "año_$1"

# Iniciamos el bucle for que creará las carpetas en el
# directorio correspondiente
for (( i=0; i<12; i++ )) do
      mkdir "año_$1/${meses[i]}_$1"
done

# Listamos los directorios creados
echo Se han creado las siguientes carpetas
echo =================================
ls -l año_$1
```

### Entrenamiento 5 — `cuenta_atras.sh`
**Enunciado:** función que recoja el dato enviado como parámetro y simule una cuenta atrás por pantalla; controlar que el parámetro no sea cero ni negativo.

```bash
#!/usr/bin/bash

# Declaramos la funcion
cuenta_atras(){
  numero=$1
  while [ $numero -ge 0 ]; do
      echo $numero
      numero=$((numero-1))
  done
  echo Fin de la cuenta atrás
}

# Declaramos un condicional para validar que
# el parámetro que desencadena la cuenta atrás
# no sea 0 o un número negativo
if [ $1 -le 0 ]; then
  echo por favor, introduzca un parámetro válido
else
  echo La cuenta atrás comeinza desde $1
        cuenta_atras $1
fi

echo Fin del script
```
(La captura del material indica `nano crear_carpetas.sh` por error; debería ser `nano cuenta_atras.sh`.)
