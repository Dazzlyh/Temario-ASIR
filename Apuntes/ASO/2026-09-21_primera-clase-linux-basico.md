---
asignatura: Administración de Sistemas Operativos (ASO)
fecha: 2026-09-21
tema: Clase 2 · primera clase de contenido real — distribuciones, shell, jerarquía, permisos y primer vistazo a scripting
fuente: transcripción de la clase en directo
---
# ASO · Clase 2 (21/09) · Primera clase de contenido: Linux básico

> Anterior: [Clase 1 (14/09)](2026-09-14_clase1-presentacion.md) · Siguiente: [UD1 (28/09)](2026-09-28_ud1-linux-basico.md)

Primera clase con contenido técnico real. Repaso de distribuciones y conceptos teóricos + primera toma de contacto práctica con la terminal (rutas, permisos, usuarios, primer vistazo a scripting).

## Aviso de examen sobre este bloque teórico
El profesor avisó explícitamente que de este bloque (distribuciones, shells, licencias) solo caen en el test **~2 preguntas por tema de media** (20 preguntas de test / 10 temas) y que **no hace falta relanzarlo en los repasos finales** — mejor dedicar el tiempo a scripting y a la parte práctica.

## Distribuciones y licencia (repaso rápido)
- Distros mencionadas: **Ubuntu, Debian, Fedora, SUSE, Mandrake, Linux Mint, Arch Linux** y **Alpine** (muy ligera, típica para contenedores Docker).
- Licencia **GPL**: el software es gratis; se puede cobrar por **instalación o formación**, nunca por la licencia en sí.
- Características: multiplataforma, multitarea, multiusuario, portabilidad.

## Jerarquía de directorios y shells
- Jerarquía desde `/`: `/bin`, `/sbin`, `/etc`, `/home`, `/var` (igual que en la UD1 de slides).
- Shell por defecto: **bash** en Ubuntu/Debian; **zsh** en Kali.

## Rutas, navegación y comodidades del shell (demo en vivo)
- `pwd` (ruta actual), `ls -l` (alias `ll`), `cd ruta`.
- `cd ..` (con espacio) sube un nivel — distinto de la sintaxis de Windows.
- `cd ~` (virgulilla) vuelve siempre al home del usuario.
- Ruta **absoluta**: se escribe desde la raíz o desde `~` (ej. `~/Escritorio/Iso`). Ruta **relativa**: se escribe desde donde ya estás (ej. `cp prueba.txt .` estando ya dentro de la carpeta).
- **Tabulador** autocompleta nombres de ficheros/carpetas — recomendado para no equivocarse al escribir rutas largas.
- `man comando` → ayuda completa (en inglés); `comando --help` → ayuda rápida con la sintaxis y argumentos.
- `cp [opciones] origen destino`; con `-r` se usa para copiar directorios.

## `ls -l` en detalle
Columnas que devuelve: tipo de archivo (`-` archivo, `d` directorio), permisos (3 grupos de 3: propietario/grupo/otros), número de enlaces, propietario, grupo, tamaño, fecha/hora de modificación y nombre. Recomendación del profesor: **nunca lanzar un `ls` a secas**, usar siempre `ls -l` o `ls -la` para tener esa información.

## Permisos: cálculo en octal
- `r` = 4 (lectura) · `w` = 2 (escritura) · `x` = 1 (ejecución). Se suman por grupo (propietario/grupo/otros).
- Ejemplos trabajados en clase: `rwx` = 7, `rw-` = 6, `r-x` = 5, `r--` = 4.
- **777** = todos los permisos a todos — usado solo como ejemplo didáctico de la suma máxima; aviso explícito de **no usarlo nunca en un fichero de producción**.
- Aviso de examen: puede pedir la conversión en **ambos sentidos** (de letras a octal y de octal a letras), ejemplo usado en clase: `754`.

## Gestión de permisos, usuarios y grupos
```bash
chmod u+x script.sh      # cambia permisos (letras u/g/o, u octal)
chown usuario archivo    # cambia el propietario
chgrp grupo archivo      # cambia el grupo
sudo useradd usuario
sudo usermod -aG grupo usuario   # añade a un grupo (NO modifica permisos del fichero)
sudo userdel -r usuario
passwd usuario
sudo groupadd grupo ; sudo groupdel grupo
sudo gpasswd -a usuario grupo    # -d para eliminar de un grupo
```
Recomendación de práctica del profesor: loguearse como `root`, crear varios ficheros y "jugar" cambiándoles el dueño, el grupo y moviéndolos para entender bien qué falla y por qué.

Aviso de examen: de los **7 puntos de práctica** del examen final, **4 son de scripting** (Tema 3); de los 3 restantes pueden caer ejercicios del tipo "modifícame los permisos de un usuario/grupo" o "añádeme un usuario".

## Primer acercamiento al scripting
- Definición: fichero de texto con una serie de comandos que se ejecutan de forma secuencial para automatizar tareas repetitivas (copias de seguridad, mantenimiento, configuraciones).
- Ejemplo de caso real dado en clase: en vez de configurar manualmente IP, usuarios y carpetas compartidas en decenas de equipos (p. ej. un aula de instituto), un script puede pedir los datos por teclado (menú interactivo) y hacer toda la configuración él solo.
- Editores: **nano** (sencillo, el que se usará en clase) y **vim** ("bing" en la transcripción — potente pero con curva de aprendizaje alta; anécdota sin verificar de alumnos de otros años atascados sin saber salir de él).
- Motivo de usar siempre nano en clase: el examen final es **presencial, con bolígrafo y papel**, sin IDE ni autocompletado. Quien quiera trabajar en casa con otro editor (vim, VS Code) puede, pero en clase se usa nano para acostumbrarse a la situación real del examen.

## Primer contacto con Nano, touch, cat y rm (demo en vivo)
- `nano fichero.txt` abre el editor; `Ctrl+O` guarda, `Ctrl+X` sale.
- `cat fichero` muestra el contenido de un fichero.
- `touch fichero.txt` crea un fichero **vacío de 0 bytes**. Si en vez de eso se crea con `nano` y se guarda vacío, el tamaño no es exactamente 0 (nano puede añadir un salto de línea) — detalle curioso sin relevancia práctica real, pero sirve para entender la diferencia entre ambos comandos.
- `touch` admite crear varios ficheros a la vez separando los nombres por espacios: `touch f1.txt f2.txt`.
- `rm fichero` borra un fichero concreto. Con el comodín **asterisco** (`*`), `rm *.txt` borra todos los `.txt` sin importar el nombre — primera introducción al carácter comodín.
- `rm -rf`: `-r` es recursivo (para borrar directorios con contenido), `-f` fuerza el borrado sin pedir confirmación.
- **Aviso importante sobre `-f` en scripts**: si un script se detiene esperando una confirmación (sí/no) y esa entrada nunca llega, el script se queda colgado para siempre ("el pajarito de Homer Simpson dando al yes"). Usar `-f` evita ese bloqueo, pero hay que ser consciente de que borra sin preguntar — cuidado en producción.

## Precisión de sintaxis: por qué importa tanto en el examen
Cita textual del profesor sobre el peso de los detalles triviales en el examen (papel, sin autocompletado): *"hasta un `cd` te puede valer un punto"* — un espacio de más o una barra mal puesta en una ruta (`cd ..`, `cd ~/...`) puede costar puntos aunque el concepto esté entendido.

## Logística del curso
- **Foro de la clase**: solo escribe el profesor (sube ahí los materiales/PDFs); pide explícitamente que los alumnos no escriban mensajes para mantenerlo limpio (si alguien escribe, los borra — no es nada personal). Para dudas o compartir recursos se puede crear un foro aparte si interesa.
- Recomendación de estudio: crear una **lista/chuleta propia de comandos básicos** (documento o ficha impresa) — no vale para usar en el examen, pero sirve como referencia de estudio para no depender de preguntarle a la IA cosas triviales como copiar un fichero.
- **Tutorías** los miércoles a las 21:30, de 60 min, **grupales** y solo para resolver dudas de lo ya visto — no se avanza contenido nuevo ni se hacen laboratorios en ellas; hay que pedir cita.
- Este curso hay acceso a **toda la plataforma Certidevs** (antes solo a 3 cursos concretos) como recurso adicional opcional.
- Próxima clase (28/09): primer script real, el clásico "Hola mundo".
