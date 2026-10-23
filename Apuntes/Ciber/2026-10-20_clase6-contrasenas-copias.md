---
asignatura: Ciberseguridad
fecha: 2026-10-20
tema: Tema 3 (apartados 3.3 y 3.4) · Contraseñas y copias de seguridad
fuente: CIBER_Clase06_diapositivas.pdf (23 páginas) + transcripción de la clase en directo
---
# Ciber · Clase 6 (20/10) · Contraseñas y copias

> Anterior: [Clase 5: Criptografía (13/10)](2026-10-13_clase5-criptografia.md) · Siguiente: [Laboratorio 3: contraseñas (22/10)](2026-10-22_lab3-contrasenas-generar-identificar-romper.md) · Profesor: Damián Sualdea Soy

Clase teórica con demo en vivo (romper una contraseña con John the Ripper); el montaje fino — cifrar con gpg, programar copias con rsync/cron — se deja para el **laboratorio del jueves** (que también es la Actividad 1 de este tema). El profesor se basa, según dice, "mucho" en el libro **Hash Crack: Password Cracking Manual** (tiene la versión 1, de 2016).

## De dónde venimos

En la Clase 5 ya se vio el **hash**: una huella de un solo sentido, que no se puede revertir (recordatorio rápido, no se repite aquí la explicación básica — ver [Clase 5](2026-10-13_clase5-criptografia.md)). Hoy se usa ese concepto para la aplicación práctica más habitual: así es como se guardan las contraseñas.

> «Nadie guarda tu contraseña en claro. Pero que no la guarden no significa que no la puedan averiguar.»

## Dónde vive tu contraseña

El sistema no guarda la contraseña: guarda su **huella (hash)**. Demo en vivo: el profesor pide a la clase hacer `sudo cat /etc/shadow` en su propia Kali y compartir pantallazo. Varios alumnos (Daniel, Francisco, María Eugenia) muestran el suyo; se ve en directo que el usuario **root** de la ISO de Kali aparece sin contraseña, y que varios alumnos con usuario `cali`/`kali` tienen el mismo hash porque no habían cambiado la contraseña por defecto (`$6$...` seguido de la huella) — el profesor usa esto para introducir en caliente la idea de la sal (ver más abajo), notando que aunque el contenido parecía "exactamente lo mismo" lo ideal es que cambie "por la sal, una pizca de sal".

| Sistema | Dónde se guardan | Qué huella |
|---|---|---|
| **Linux** | El fichero `/etc/shadow` | `$6$...` = SHA-512 con sal |
| **Windows** | El fichero **SAM** (en dominio, Active Directory) | NTLM (y el viejo LM) |
| **WordPress y muchas webs** | En su base de datos (la tabla de usuarios) | phpass `$P$...` (hoy, bcrypt) |
| **Una app chapucera** | En claro, o con MD5 pelado sin sal | La que NO debe guardar |

Cada huella tiene su "pinta" (longitud, prefijo) — en el laboratorio del jueves se practica identificarlas antes de romperlas. El profesor menciona que tiene una práctica aparte sobre WordPress (tomar el control vía `wpscan`) y que esto se trabajará con más detalle más adelante con Metasploitable, a nivel de pentest web.

## El hash y la sal

Lo que explican las diapositivas y lo que amplió el profesor en directo, combinado:

- **El hash**: al crear la cuenta, el sistema guarda la huella de tu contraseña, no la contraseña. Para comprobarte, hashea lo que escribes y lo compara con la huella guardada.
- **La sal (en inglés, *salt*)**: es un trozo **aleatorio** que el sistema añade a tu contraseña **antes de hashearla**. Así, dos personas con la misma contraseña obtienen huellas distintas, y una tabla de huellas ya calculadas no sirve.
- Matiz que dio el profesor en directo, no escrito literalmente en la diapositiva: la idea principal es que **los algoritmos modernos de hasheo para guardar contraseñas no hacen un hasheo "puro"**, sino que le meten hasheo + sal, precisamente para que con esa huella no se pueda ir "para atrás" fácilmente. Lo contrapone explícitamente a un "hash puro" (p. ej. aplicar directamente MD5 o SHA sin más), que es justo "lo que no se debe hacer" — lo puso como ejemplo de mala práctica de una "app chapucera".
- **Por qué frustra las rainbow tables**: sin sal, un atacante usaría una rainbow table (una tabla gigante de huellas ya calculadas de millones de contraseñas) — con eso "a nivel físico podrías romper cualquier tipo de contraseña, no habría ningún límite". La sal, al ser distinta en cada caso, **obliga a romper cada contraseña por separado** y "las tablas rainbow revientan" (se vuelven inútiles). Herramienta asociada a este ataque sin sal: **Ophcrack**.
- Apunte de Dani — *«la sal añade una capa de dificultad para las rainbow list, que son listas de contraseñas típicas ya hasheadas»* — es correcto y coincide con lo explicado: el matiz que añade el profesor es que la sal no solo dificulta, sino que **inutiliza por completo** las rainbow tables precalculadas, porque cada huella pasa a depender de un valor aleatorio único por usuario/contraseña, no solo de la contraseña en sí.

## Codificar, hashear y cifrar

Tres verbos que se confunden mucho, según insiste el profesor (regla rápida: ¿se deshace sin clave? *codificar*. ¿No se deshace? *hashear*. ¿Se deshace con una clave? *cifrar*):

| Verbo | Qué es | Ejemplo |
|---|---|---|
| **Codificar** | Pasa los datos a un formato conocido para poder manejarlos. Se deshace sin clave. **No protege nada.** | Base64 (p. ej. usuario/contraseña viajando en Base64 hacia un servidor de correo: "todo el mundo puede ver lo que hay") |
| **Hashear** | Huella de un solo sentido: no se puede volver atrás. Importante: el **tamaño del hash es fijo** aunque la entrada sea gigante (p. ej. un disco de 1 TB da el mismo tamaño de huella que una contraseña corta) — y eso también ahorra muchísima CPU. | SHA-256 |
| **Cifrar** | Transformación **reversible** con una clave: se cifra y luego se puede descifrar con esa clave. | AES |

El profesor insiste en que "romper a nivel físico" (con Ophcrack / rainbow tables) significa tener en un fichero todas las combinaciones precalculadas, en vez de generarlas al vuelo con un programa como John the Ripper.

## Cómo se roba una contraseña

Antes de romper el hash, hay que conseguirlo:

| Vía | En qué consiste |
|---|---|
| **Filtración / volcado de BD** | Una web vulnerable (p. ej. SQL injection) y te llevas su tabla de usuarios hasheada. La más común: lo de Have I Been Pwned. |
| **Phishing** | Una web falsa que imita el login; el usuario teclea la contraseña él mismo. No hay que romper nada. (Se trabajará con GoPhish más adelante). |
| **Malware / keylogger** | Un programa que registra lo que tecleas, o roba las guardadas en el navegador. (Se trabajará con Meterpreter: instrucción `keyscan`). |
| **Captura en red (MITM)** | Interceptar el tráfico. HTTPS lo corta en internet, pero en red interna se capturan los hashes NTLM de Windows. (Laboratorio futuro con Ettercap). |
| **Acceso al equipo** | Si ya estás dentro, lees el `/etc/shadow` (Linux) o la SAM (Windows). |
| **Archivos protegidos** | Un `.zip`, `.pdf` o documento de Office con contraseña también guarda un hash: se extrae (`zip2john`, `office2john`...) y se rompe igual — tiene una clave simétrica, se puede hacer fuerza bruta. Anécdota de un alumno (Francisco), sin verificar más allá de lo contado en clase: trabajando en una copistería de arquitectura, reventaban por fuerza bruta PDFs de proyectos protegidos para poder imprimirlos. |

Con el hash en la mano, el atacante lo rompe **offline**, en su propia máquina y sin límite de intentos — por eso una filtración es tan grave.

### Google Dorking (demo en directo)

Explicación del profesor sobre el **dorking** como forma concreta de encontrar filtraciones vía navegador: consiste en usar en Google una serie de operadores/palabras de búsqueda muy concretos para encontrar páginas donde, por descuido, se han publicado contraseñas o credenciales en la parte pública e indexada de un sitio. Ejemplos mostrados en directo (sin pinchar los resultados, solo para ver qué aparece): `intitle:index of`, `intext:password`, páginas con `.txt` de contraseñas, dorks apuntando a **Pastebin** (página de copiar/pegar texto) usando `site:` e `intext:`. El profesor avisa varias veces de **no pinchar** los enlaces que salen (podrían llevar a sitios maliciosos) y admite que personalmente **no le gusta el dorking** — "porque no sé a dónde voy".

Apunte de Dani — *«se hace a través de páginas con ciertos argumentos para buscar en Google y así encontrar ciertas vulnerabilidades en páginas que lo han dejado abierto en sus enlaces indexados»* — correcto y verificado en la transcripción: coincide con la explicación en directo del profesor (dorks como `intitle`, `intext`, `site`, usados para encontrar credenciales filtradas en enlaces indexados públicamente).

### Honeypots (mención breve, no en diapositivas)

El profesor menciona los honeypots como advertencia, no como explicación de concepto, en el mismo contexto del dorking: *«tened cuidado, no lo hagáis, que hay mucho Honeypot y muchas trampas por ahí»*. Es decir, avisa de que al navegar por resultados de dorking puede haber honeypots y trampas deliberadamente colocados para atraer e identificar a quien curiosea. No se da en clase una definición formal del término.

Apunte de Dani — *«mecanismos que se dejan de manera deliberada a merced de los ciberdelincuentes para atraerlos»* — se confirma que el profesor mencionó los honeypots en este contexto de advertencia (dorking), pero no desarrolló una definición completa en clase; la definición que da Dani es coherente con el uso habitual del término (señuelos deliberados para atraer y detectar a un atacante) y con el tono de advertencia del profesor, aunque **la formulación exacta del concepto es aportación propia de Dani, no una cita textual ni una explicación desarrollada por el profesor en esta clase**.

## Cómo se rompe el hash

> «No se descifra: se adivina probando.»

| Técnica | En qué consiste |
|---|---|
| **Diccionario** | Prueba millones de contraseñas conocidas (la lista `rockyou.txt` tiene **14 millones**) y compara la huella. Las comunes caen al instante. |
| **Fuerza bruta** | Prueba todas las combinaciones posibles, una a una. Funciona con las cortas; con las largas, tardaría siglos. |
| **"La clave del asunto"** | El hash **NO se deshace** (Clase 5). El atacante no lo "descifra": hashea candidatas hasta que una huella coincide. |

Matiz útil que dio el profesor en directo: si la huella coincide con una contraseña candidata que **no es exactamente** la contraseña real del usuario (colisión), en la práctica para el atacante "tiene que ser esa" — de ahí que una contraseña filtrada de otra web sea "oro": si se reutiliza, ya no hay que romper nada, solo probarla donde más duele.

## Las herramientas · online y offline

| Herramienta | Tipo | Para qué sirve |
|---|---|---|
| **John the Ripper** | Offline | Rompe el hash que ya tienes: diccionario, fuerza bruta y reglas. |
| **Hashcat** | Offline | Lo mismo, pero con la GPU: muchísimo más rápido. El estándar hoy — usa los muchos microprocesadores y la memoria de la tarjeta gráfica, no la CPU. |
| **Hydra** | Online | Prueba usuario/contraseña en vivo contra un servicio (SSH, FTP, web). Ya se trabajó en una clase anterior con Metasploitable. |
| **Rainbow tables** | Offline | Hashes ya calculados de millones de claves. La sal las deja inútiles. |
| **Ophcrack** | Offline | Rainbow tables en acción: rompe contraseñas de Windows (la SAM, NTLM/LM). Arranca hasta con un Live CD. |
| **Responder** | En red | Se hace pasar por un servidor Windows en la red y recoge los hashes NTLM que le llegan. El profesor aclara que esta herramienta no la ha trabajado él mismo nunca en directo, la pone porque aparece en el libro *Hash Crack*. |

Offline: tienes el hash y lo rompes en tu máquina, sin límite de intentos ni que nadie se entere (hoy, demo y laboratorio: John). Online: pruebas contra el servicio en vivo, lento y con bloqueos.

## Cuánto aguanta tu contraseña

Tabla de la diapositiva más los datos concretos que el profesor mostró en directo (vídeo de Hive Systems, `youtu.be/opRMrEfAlil`, con hardware de referencia "12 RTX 5090"):

| La contraseña | Cuánto tarda en caer |
|---|---|
| 123456, password, tu nombre | Al instante (está en las listas) |
| 8 letras minúsculas (abcdefgh) | Minutos |
| 8 con mayúsculas, números y símbolos | Horas o días |
| 12 con mezcla de todo | Siglos |
| Una frase de 4 palabras al azar | Prácticamente, nunca |

Datos concretos que el profesor leyó en vivo de la tabla de Hive Systems (no están en la diapositiva, son ampliación en directo):

- Solo números, 8 caracteres: instantánea.
- Solo minúsculas, 8 caracteres: hasta **3 semanas**.
- Solo números, 18 caracteres: **284.000 años**.
- Los "verdes" (lo que hoy se considera seguro) rondan: solo minúsculas con 16 caracteres, mayúscula+minúscula con 14 caracteres, o número+mayúscula+minúscula con 13 caracteres.

## Qué la hace fuerte de verdad

| Idea | Qué significa |
|---|---|
| **Larga antes que rara** | Una frase larga (p. ej. «caballo-azul-mesa-trueno») aguanta más que «P@2x!» y se recuerda mejor. La longitud es lo que manda. |
| **Un gestor de contraseñas** | Una distinta y larga para cada sitio, y que las recuerde el gestor. Tú solo memorizas la clave maestra. El profesor dice que no hay un gestor "mejor o peor": cualquiera medianamente decente vale. |
| **Segundo factor (2FA)** | Aunque te roben la contraseña, sin el código del móvil no entran. Es la medida que más protege por lo poco que cuesta. |

El profesor recomienda en directo pensar en **frases propias** en vez de contraseñas con símbolos rebuscados — ejemplos que dio: *"la silla de mi casa es negra"*, o combinar el nombre de un familiar con otra idea personal — porque lo que de verdad cuenta para la resistencia es el número de caracteres, no la "rareza". Y nunca reutilices: si filtran una web (compruébalo en haveibeenpwned.com), esa clave ya no vale en ningún sitio.

## Demo · romper una contraseña con John the Ripper

El profesor explica y muestra en pantalla, siguiendo paso a paso los comandos de la diapositiva (no llegó a ejecutarlos todos en vivo delante de la clase por problemas para cargar la ventana del terminal en ese momento; quedan documentados como la receta exacta a seguir, y se subirán las instrucciones para que cada alumno los pruebe por su cuenta antes del jueves):

```bash
# Crear un usuario de prueba con una contraseña floja
sudo useradd -m pepe
echo 'pepe:password123' | sudo chpasswd    # una clave floja

# Extraer el hash combinando /etc/passwd y /etc/shadow
sudo unshadow /etc/passwd /etc/shadow > hashes.txt

# Romper con John the Ripper usando el diccionario rockyou
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt

# Mostrar la contraseña ya rota
john --show hashes.txt
# pepe:password123        # rota en segundos
```

El profesor insiste en que esto "va a aparecer a la primera" porque `password123` es una contraseña muy débil, justo para que el jueves no "pille de primeras" a nadie con el laboratorio de verdad.

## Un vistazo al jueves (adelanto del laboratorio)

El laboratorio del jueves seguirá esta mecánica (comandos de la diapositiva, igual que arriba):

```bash
# 1) RECONOCER el hash por su pinta (longitud y prefijo):
21232f297a57a5a743894a0e4a801fc3                 -> MD5
$P$9QGUsR07ob2qNMbmSCRh3Moi6ehJZR                -> phpass (WordPress)
*4ACFE3202A5FF5CF467898FC58AAB1D615029441        -> MySQL

# 2) ROMPERLO con John, de varias formas:
john --wordlist=rockyou.txt hashes.txt              # diccionario
john --wordlist=rockyou.txt --rules hashes.txt       # + reglas
john --mask='?d?d?d?d' hashes.txt                    # máscara (4 dígitos)
```

El profesor adelanta que será "una clase un pelín técnica, pero de acción": primero identificar el tipo de hash (MD5, phpass, MySQL...) y luego aplicar diccionario, reglas o máscara según convenga, siempre con `rockyou.txt` como wordlist base.

## Las copias · la última defensa

Lo que pasó a tratar el profesor, avisando de que el montaje técnico detallado (rsync, cron) se profundizará con el docente de **Seguridad y Alta Disponibilidad (SAD)**:

- **Contra qué te salvan**: un ransomware que cifra tus datos (Clase 5), un disco que muere, un borrado por error o un robo. La copia es lo único que lo deshace.
- **La regla de oro**: si tienes copia, el chantaje del ransomware no funciona — formateas y restauras. Sin copia, pagas o lo pierdes.

### La regla 3-2-1

| Elemento | Qué significa |
|---|---|
| **3 copias** | El original y dos copias más. Si una falla, aún te quedan otras. |
| **2 medios distintos** | En dos sitios de tipo distinto (p. ej. un disco externo y la nube), no las dos en el mismo disco. |
| **1 fuera de sitio** | Al menos una lejos físicamente: si hay fuego, robo o inundación, no se pierde con las demás. |

El profesor menciona de pasada que existe también una variante "regla 4-3-2-1", pero que la 3-2-1 es la típica que se trabaja. Ejemplo personal que cuenta: tiene sus fotos familiares en 3 discos duros — el original, una copia exacta en casa, y otra en casa de sus padres (fuera de sitio) — "en el peor de los casos, recupero todas las fotos".

### Tipos de copia

| Tipo | Qué copia | Ocupa / tarda |
|---|---|---|
| **Completa** | Todo, cada vez | Mucho, pero restaurar es fácil |
| **Incremental** | Solo lo cambiado desde la última copia | Poco; restaurar necesita toda la cadena |
| **Diferencial** | Lo cambiado desde la última completa | Término medio |

Lo normal: una completa de vez en cuando (semanal) e incrementales entre medias (diarias). La frecuencia depende del tipo de trabajo (el profesor pone el ejemplo de una gestoría: no es lo mismo en plena campaña de IVA/IRPF que en temporada tranquila).

### Así se hace una copia (rsync + cron)

```bash
# Copia a otro disco: -a conserva permisos y solo pasa lo nuevo
rsync -av ~/Documentos/  /media/backup/Documentos/

# Para que se repita sola
crontab -e
0 22 * * *  rsync -a ~/Documentos/ /media/backup/Documentos/
# cada día a las 22:00. A fondo, en el Laboratorio del jueves.
```

### Lo que NO es una copia

| Trampa | Por qué |
|---|---|
| **RAID no es copia** | El RAID protege de que se rompa un disco, no de que borres un fichero: si lo borras, desaparece de todos los discos a la vez. |
| **Sincronizar no es copia** | Si el ransomware cifra tu carpeta de OneDrive o Drive, la nube sincroniza... la versión cifrada. Copia es otra cosa. |
| **La que no se prueba, no existe** | Una copia que nunca has intentado restaurar no es una copia: es una suposición. Hay que probar la restauración. |

## Qué toca esta semana

- **Comprueba tus cuentas**: entra en haveibeenpwned.com y mira si tu correo ha salido en alguna filtración; cambia lo que haga falta.
- **Mira tu estrategia de copias**: ¿cumples el 3-2-1 con tus cosas? ¿Cuándo restauraste una copia por última vez?
- **El jueves, Laboratorio**: se rompen contraseñas con John, se cifra con `gpg` y se programa una copia. Es el grueso de la **Actividad 1**.
- **Entrega de la Actividad 1: 9 de noviembre.**

## Anexo: para más adelante (extracción de hashes más avanzada)

No se trabaja hoy, son formas reales de *conseguir* hashes (la columna "cómo se roba" de antes), para laboratorios de más adelante:

| Técnica | Dónde se verá |
|---|---|
| Volcar la SAM de Windows | Sacar los hashes NTLM del propio sistema, ya con acceso de administrador — bloque de bastionado (Tema 8) |
| Romper un WiFi (WPA2) | Del "handshake" capturado a la contraseña de la red — seguridad de red (Tema 6) |
| Dumpear una base de datos | Por una inyección SQL, llevarse la tabla de usuarios hasheada — ataques web (Tema 6) |

## Curiosidades y otras recomendaciones mencionadas en clase

- El profesor puso un vídeo satírico (parodia tipo doblaje gracioso) sobre un supuesto mensaje de Barack Obama hablando de contraseñas, en tono de humor, para ilustrar lo poco seguras que son las contraseñas típicas tipo "password123" — contenido de entretenimiento, no material oficial verificado.
- Manuel recomendó un libro de **ingeniería social** de un autor que tuvo un programa en la BBC robando datos/tarjetas con técnicas de ingeniería social en directo; no se confirma el título exacto en la transcripción (se menciona de pasada "el arte de hacking" como posible traducción), por lo que se deja como referencia sin verificar.
- Se avisa de que la **Clase 7 empieza el Tema 4: análisis forense.**

## Fuentes y enlaces (de las diapositivas)

| Qué es | Enlace |
|---|---|
| INCIBE · ciberseguridad para ciudadanía | www.incibe.es/ciudadania |
| ¿Han filtrado tu cuenta? · Have I Been Pwned | haveibeenpwned.com |
| Cuánto tarda en romperse una contraseña · Hive Systems | www.hivesystems.com/password-table |
| Complejidad de adivinar una contraseña · vídeo | youtu.be/opRMrEfAlil |
| John the Ripper · la herramienta de la demo | www.openwall.com/john/ |
| Rainbow tables para descargar · Ophcrack | ophcrack.sourceforge.io/tables.php |

## Para llevar a casa

- El sistema **nunca** guarda tu contraseña en claro: guarda su hash (con sal, si está bien hecho).
- La **sal** es lo que impide que dos contraseñas iguales den la misma huella, y lo que inutiliza las rainbow tables.
- Codificar, hashear y cifrar **no son lo mismo**: codificar se deshace sin clave (no protege), hashear no se deshace nunca, cifrar se deshace con una clave.
- Una contraseña no se descifra: se **adivina** (diccionario o fuerza bruta), comparando huellas.
- Cuidado con el **dorking**: útil para entender cómo se filtran credenciales, pero nunca pinches enlaces encontrados así — puede haber honeypots y trampas.
- La **longitud** manda más que la "rareza": mejor una frase larga que un símbolo raro. Gestor de contraseñas + 2FA, siempre.
- Las copias de seguridad son la **última defensa**: regla 3-2-1, y recordar que RAID no es copia, sincronizar no es copia, y una copia que no se prueba no existe.
- **Esta semana**: comprobar cuentas en haveibeenpwned.com, revisar la propia estrategia 3-2-1, y preparar el laboratorio del jueves (romper contraseñas + cifrar con gpg + programar una copia) — Actividad 1, se entrega el **9 de noviembre**.
