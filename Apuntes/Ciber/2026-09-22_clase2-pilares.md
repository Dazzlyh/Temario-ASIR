---
asignatura: Ciberseguridad
fecha: 2026-09-22
tema: Tema 1 (1.1 y 1.2) · Clase 2 · los cuatro pilares desde el atacante
fuente: CIBER_Clase02_diapositivas.pdf + transcripción de la clase en directo
---
# Ciber · Clase 2 (22/09) · Pautas de seguridad

> Anterior: — · Siguiente: [Lab 1](2026-09-24_lab1-paseo-por-kali.md) · Práctica asociada: [Práctica 1](2026-09-22_practica1-tres-demostraciones.md)

## Qué se vio
1. Qué se protege: los **cuatro pilares** del material.
2. Cómo lo mira un atacante: qué pilar rompe cada ataque y cómo se demuestra.
3. Tres demostraciones en directo (confidencialidad, integridad, disponibilidad).

La Actividad 1 pide, por cada apartado, **evidencia**: hoy se aprende qué cuenta como evidencia.

> «El defensor tiene que acertar siempre. Al atacante le basta con acertar una vez.»

## Los cuatro pilares (según el material de la asignatura)
| Pilar | Significado |
|---|---|
| **Fiable** | Que funcione sin fallos el tiempo que tiene que durar |
| **Confidencial** | Que solo lo vea quien debe verlo, en reposo y en tránsito |
| **Íntegro** | Que nadie lo cambie sin que se note, ni siquiera por error |
| **Disponible** | Que esté ahí cuando hace falta, aunque te ataquen |

- OJO con la palabra: en otros libros «pilares» = hardware, software y datos. Aquí son estas cuatro propiedades.
- **La fiabilidad NO es lo mismo que la disponibilidad: es la «pregunta trampa» del examen** (lo dice la diapositiva).

## Cómo se rompe cada pilar y cómo se demuestra
| Pilar | Cómo lo rompe un atacante | Cómo se demuestra |
|---|---|---|
| Fiabilidad | Un proceso que se come la memoria y lo tumba a ratos | Registros del sistema y alertas de recursos |
| Confidencialidad | Escuchar tráfico sin cifrar o llevarse una copia | El dato aparece donde no debía: una captura |
| Integridad | Cambiar un fichero sin cambiar su tamaño | El hash ya no coincide |
| Disponibilidad | Saturar el servicio o cifrarle los datos | No responde, y queda en el registro |

Un auditor no dice «esto es inseguro»; dice **«esto se rompe así, y aquí está la prueba»**. Esa frase es la Actividad 1 entera.

## Las dos que se olvidan (no están en los cuatro pilares)
- **Autenticidad**: que quien dice ser el origen lo sea de verdad. Es lo que ataca la suplantación.
- **No repudio**: que quien hizo algo no pueda negarlo después. Convierte un registro en prueba (el Tema 4 gira en torno a la cadena de custodia).
- Ambas se consiguen con **criptografía asimétrica**: firmas con tu clave privada, cualquiera verifica con la pública. Se ve en la Clase 5.

## Las tres demostraciones (comandos)
**Confidencialidad: el dato viaja en claro**
```bash
sudo tcpdump -i lo -A port 8000                                  # terminal 1: escucha
curl 'localhost:8000/login?user=admin&pass=Verano2026'           # terminal 2
# aparece GET /login?user=admin&pass=Verano2026 -> contraseña legible. La prueba es la captura.
```
**Integridad: un byte cambiado, mismo tamaño, otro hash**
```bash
echo 'Transferir 1.000 euros a la cuenta ES12...' > orden.txt
sha256sum orden.txt | tee orden.sha256
sed -i 's/1.000/9.000/' orden.txt
ls -l orden.txt            # pesa exactamente lo mismo
sha256sum -c orden.sha256  # orden.txt: FAILED (la suma no coincide) -> la prueba es el hash
```
**Disponibilidad: una conexión sin terminar tumba el servicio**
```bash
curl -s localhost:8000            # responde al instante
nc localhost 8000                 # otra terminal: abre conexión y NO escribe nada
curl --max-time 5 localhost:8000  # SIN -s para ver el error: curl: (28) Operation timed out
```
Es un DoS: una sola conexión que no suelta (servidor de una sola cola a propósito).

## Tres miradas sobre la misma máquina
| Rol | Pregunta |
|---|---|
| Administrador | ¿Está protegido y sigue funcionando? (desde dentro, para mantenerlo) |
| Atacante | ¿Por dónde se rompe? Busca el pilar **más débil**, no el más importante |
| Auditor | ¿Cómo lo demuestro? Es el atacante **con permiso por escrito y con informe**; es lo que seremos en el módulo |

Primer principio del apartado 1.2: conocer el panorama de ciberamenazas, a partir de ataques reales, para construir defensas que funcionen.

## Qué pilar rompe cada ataque
| Ataque | Pilar(es) | Cómo se nota |
|---|---|---|
| Phishing que roba credenciales | Confidencialidad y autenticidad | Accesos desde sitios u horas raras |
| Ransomware | Disponibilidad (y confidencialidad si antes se lleva los datos) | Ficheros ilegibles y nota de rescate |
| Alterar una web o una factura | Integridad | El hash o la firma ya no coinciden |
| Denegación de servicio | Disponibilidad | No responde y el tráfico se dispara |

Clásico que rompe los cuatro a la vez sin hacer ruido: la **contraseña por defecto**.

## Práctica de la semana (no se entrega ni puntúa)
- «¿Cuál han tocado?»: cinco ficheros, su fichero de sumas y un comando que altera uno al azar; encontrarlo y demostrarlo.
- Dos incidentes: **WannaCry** y el **incendio de OVH (2021)**: qué pilares rompe cada uno y con qué evidencia.

## Para la Clase 3 (deberes)
- Leer apartados 1.1 y 1.2 del campus.
- Instalar Kali (Práctica 0 del foro; solo Kali en el portátil) → se presenta en el Lab 1.
- **Test 1**: medio punto, diez preguntas, se abre la semana del 28. Los diez test suman **5 de los 15 puntos de la continua**.
- Clase 3: apartados 1.3, 1.4 y 1.5.

## Notas en directo (matices del profesor, no están en las diapositivas)

### Sobre los "pilares"
El profesor deja claro que la palabra "pilares" no le convence:
- Él trabaja con **5 propiedades**, no 4: confidencialidad, integridad, disponibilidad (la tríada clásica **CIA/CID** que se puede buscar así en internet) + **autenticidad** y **no repudio** (que el material mete en el Tema 4, junto a la firma electrónica).
- La **fiabilidad no le gusta como "pilar" de ciberseguridad**: para él es un concepto de alta disponibilidad (SAD), no algo que se "rompa" igual que los otros. Lo dice explícitamente en clase: "no me gusta cómo está, pero lo ha puesto [el material], y os lo digo en directo".
- El material también usa a veces "hardware, software y datos" como marco alternativo; el profesor lo llamaría **propiedades**, no pilares, y avisa: si en una entrevista de trabajo preguntan "los pilares de la ciberseguridad" y respondes "hardware, software y datos", es el pilar de la **seguridad en general**, no el de ciberseguridad — la respuesta correcta ahí es CID.
- Para el examen: aunque el material diga "pilares", lo que entra son **confidencialidad, integridad y disponibilidad** (más autenticidad y no repudio, que se ven más adelante).

### Confidencialidad — la demo en directo
Montó un servidor Python muy sencillo escuchando en `localhost:8000` (uno de los puntos del Certiprof/ejercicios de programación que iremos usando) y capturó el tráfico con **tcpdump** escuchando por la interfaz de loopback. Al navegar a una URL tipo `localhost:8000/login` con usuario y contraseña **en la propia URL** (método GET, que nunca se debería usar así para enviar credenciales), tcpdump mostró la petición completa en claro. Mencionó que con **Wireshark** (herramienta clave de redes, se ve a fondo el jueves) se vería lo mismo con interfaz gráfica, y que con POST se captura igual, solo que no va en la URL.

### Disponibilidad — variante de la demo
Esta vez usó **netcat** (`nc`) en vez de solo `curl`: dejó un `nc localhost 8000` abierto sin escribir nada, ocupando el único socket del servidor de pruebas (hecho a propósito con una sola cola, "muy cutre"). Al llegar un usuario normal con `curl --max-time 5 localhost:8000`, se agota el tiempo: `Operation timed out`. Puntos que añadió:
- Esto es un **DoS** (un solo origen). Si lo hicieran muchos ordenadores a la vez (una **botnet** de "ordenadores zombi"), sería un **DDoS** (denegación de servicio distribuida).
- Un servidor "serio" (Apache, Nginx) no se comporta así: corta la conexión por timeout (código HTTP **408 Request Timeout**) para poder seguir atendiendo a otros. Esto se verá a fondo en Servicios en Red.

### Integridad — detalle que no está en la práctica escrita
- Repitió la demo del hash (`sha256sum`, `sed` para modificar, mismo tamaño con `ls -l` pero hash distinto) y añadió una comprobación: si se revierte el cambio (de 9.000 otra vez a 1.000), **el hash vuelve a ser exactamente el mismo que al principio** — confirma que el hash depende solo del contenido, no del historial.
- **Cualquier cambio, aunque sea un espacio al final del fichero, cambia el hash completo** (no un dígito: el número entero es distinto).
- Un compañero (Manuel) señaló un caso real: el salto de línea de **Windows (CRLF)** frente a **Linux/Unix (LF)** cambia el contenido binario del fichero aunque se vea igual en pantalla, así que basta mover un archivo entre sistemas para que su hash (y su firma/certificado) ya no coincidan.
- Algoritmos de hash mencionados: **MD5, SHA-1, SHA-256, SHA-512**. MD5 es "el de WordPress" históricamente (clave con bcrypt hoy, pero el profesor lo puso como ejemplo de MD5) y el profesor avisa de que **MD5 está considerado roto** (hay colisiones conocidas; referencia que mencionó: un artículo de Segu-Info titulado algo así como "MD5 ha muerto"). El tema de las colisiones se tratará más adelante.
- El hash se usa igual para **cadena de custodia forense** (comprobar que no se ha movido un solo bit de un disco de varios terabytes) y para firmas de ejecutables (**VirusTotal** y la mayoría de antivirus comparan hashes/firmas). Habrá una práctica específica de `sha256sum` sobre un ejecutable.

### Ataques y qué pilar rompen (ampliación)
- **Phishing**: ataca confidencialidad y autenticidad (te engañan sobre quién es el emisor). Se montará un servidor de phishing con **GoFish** más adelante, cuando se monte el servidor de correo.
- **Ransomware**: usa **criptografía asimétrica** para cifrar los ficheros; para descifrarlos hace falta la clave privada que los atacantes venden tras el pago. Rompe disponibilidad (no se puede acceder a los ficheros) y también confidencialidad si antes exfiltran los datos. El profesor cuenta una anécdota real: una empresa pagó el rescate y los propios atacantes se conectaron en remoto a ayudar a recuperar los ficheros — "lo que quieren es cobrar, no jorobar tu sistema", porque les interesa su reputación para que la próxima víctima también pague. Recurso mencionado: la web **No More Ransom**, para víctimas de ransomware.
- **Referencia anual** que se usará en la asignatura: el informe de amenazas de **ENISA** (edición 2026, "Enisa Threat Landscape").
- Analogía del profesor sobre "atacar el eslabón más débil": como los leones no van a por el ñu más fuerte sino a por la gacela más lenta, el atacante no busca el pilar más importante sino el más débil — y ese eslabón suele ser el usuario (**la "capa 8" del modelo OSI**, un chiste recurrente del profesor).

### Logística mencionada en esta clase
- El jueves (Lab 1) se trabaja con **Kali**: instrucciones en el foro para bajar una máquina virtual ya hecha (VirtualBox, UTM en Mac, o similar) en vez de instalar desde cero.
- Recomendó la web **DistroWatch** para consultar información y rankings de distribuciones Linux (siguió el hilo con Kali, BlackArch, etc., sin relevancia para el examen).
- Recordatorio de nomenclatura de materiales: todo lo que lleve la **franja roja** es de Ciberseguridad (frente al resto de asignaturas del mismo profesor).
