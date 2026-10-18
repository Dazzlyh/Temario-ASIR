---
asignatura: Ciberseguridad
fecha: 2026-10-13
tema: Tema 3 · Clase 5 · Criptografía (historia, conceptos, Kerckhoff, Shannon, simétrica vs asimétrica)
fuente: transcripción de la clase en directo
---
# Ciber · Clase 5 (13/10) · Criptografía: de Esparta al candado del navegador

> Anterior: [Lab 2 · Metasploitable (09/10)](2026-10-09_lab2-metasploitable.md) · Profesor: Damián Sualdea Soy

Clase teórica (sin "hazlo tú": se deja para el laboratorio de la semana siguiente, junto con la actividad de romper contraseñas). El profesor avisa de entrada que este tema se retomará en **Seguridad y Alta Disponibilidad (SAD)**, pero con "otro enfoque" — aquí lo da con "enfoque pirata", centrado en entender si algo cifrado se puede romper o no, de cara al trabajo de pentest/criptoanálisis.

> «Lo primero que hay que entender: encriptar no me vale. Encriptar para mí es meter en una cripta — prohibido ese nombre.»

## Aviso de examen: nunca usar "encriptar"

El profesor pide explícitamente no usar la palabra **"encriptar"** en el examen presencial: la palabra correcta en español (según la RAE) es **cifrar** / **descifrar**. Avisa que si alguien la usa en el examen, directamente resta **-0,25** por aparición, y dice que lo va a repetir durante todo el curso, "hasta el último día".

- *Encoding* (p. ej. pasar a Base64) **no es** cifrar: es representar el mismo contenido en otro formato, sin clave y sin ocultar nada. Cifrar siempre implica una **clave**.
- Cifrar viene del árabe (*cifra*, oculto), descifrar incorpora el prefijo griego *cripto* (oculto) + *grafía* (escritura) → "escritura oculta".

## Conceptos base del criptosistema

Un **criptosistema** es la forma de modelar cómo funciona una criptografía concreta. Ejemplo típico usado en clase (simétrico):

- **Ana** cifra un mensaje (texto en claro) con una clave → texto cifrado.
- El texto cifrado viaja por la red hasta **Bruno**, que lo descifra con la clave.
- **Eva** es la atacante que intercepta e intenta romperlo: a esa disciplina se la llama **criptoanálisis** — la ciencia que se encarga de romper criptosistemas (analizar lo necesario para recuperar el texto en claro sin tener la clave).

El profesor insiste en diferenciar bien, de cara al resto del curso: un cifrado puede ser **simétrico** o **asimétrico**, y un **hash** es otra cosa distinta (no es un cifrado).

## Historia de la criptografía (2.500 años de pelea)

> «Desde que existe el secreto, existe alguien intentando leerlo. La criptografía es esa pelea. Tiene 2.500 años.»

| Época / hito | Qué es | Idea clave |
|---|---|---|
| Grecia, **escítala espartana** | Una vara de grosor determinado + una cinta de cuero enrollada en espiral donde se escribe el mensaje; al desenrollar, las letras quedan desordenadas; solo con una vara del mismo grosor se puede releer | Primer cifrado por **transposición** |
| Roma, **cifrado César** | Rotación de todas las letras del abecedario un número fijo de posiciones (p. ej. 3) | Cifrado por **sustitución**, muy sencillo pero el más famoso de introducción |
| Bagdad, **Al-Kindi** | Primer criptoanalista de la historia; descubrió el **análisis de frecuencias** (contar qué letras se repiten más) para romper cifrados de sustitución | Nace el concepto de "romper códigos" |
| **Vigenère** | Cifrado **polialfabético**: usa varias claves a la vez, de forma que un mismo texto en claro puede dar lugar a muchísimos mensajes cifrados posibles | Mucho más difícil de romper que una sustitución simple |
| **Enigma** (Alemania, s. XX) | Máquina de cifrado mecánica con **rotores**: cada letra pulsada activa el primer rotor, que al completar una vuelta mueve el segundo, y este al tercero — generando millones de combinaciones posibles | El cifrado "máquina a máquina" más conocido de la historia |

El profesor recomienda, si da tiempo durante el curso, un **laboratorio de cifrados clásicos** (escítala, César, Vigenère, etc.) para "ver lo difícil que es romper códigos" de forma práctica.

### Enigma, Turing y Bletchley Park

- Los nazis usaban Enigma para cifrar sus comunicaciones militares, convencidos de que era irrompible. Antes de la guerra, los **polacos** ya trabajaban sobre esa máquina; esa información pasó primero a los franceses y luego a los **ingleses**.
- Las comunicaciones iban por **radio sin cifrado adicional de canal** (cualquiera podía escucharlas); lo único protegido era el contenido, cifrado con Enigma. El fallo decisivo fue siempre más humano que matemático: operadores que usaban claves predecibles (nombres de pareja, gustos personales conocidos por el otro operador), lo que facilitaba intuir configuraciones.
- En **Bletchley Park** (Reino Unido), **Alan Turing** y su equipo se dedicaban a romper esas comunicaciones. Construyeron las llamadas "bombas" (bombes), consideradas el germen del primer ordenador (concepto que cristaliza hacia 1945).
- El profesor matiza la narrativa popular de "Enigma acortó la guerra en años": él cree que el impacto real fue más concreto, por ejemplo en las comunicaciones en el norte de África, más que un acortamiento genérico de la contienda.
- Dato curioso: durante el franquismo, España tuvo **3 máquinas Enigma**, que posteriormente le fueron retiradas.
- El cifrado se rompió del todo hacia **1966** según la cronología que da el profesor, antes de la llegada de la criptografía asimétrica en los 70.

### Recomendaciones de material (el profesor insiste en verlas, no es para ahora)

- Películas: **Enigma** (con Tom Hanks... confirmado luego que la referencia correcta de Turing es **"Descifrando Enigma"**, 2014, con Benedict Cumberbatch, "el mago de Marvel" según lo describe en clase) y, como curiosidad relacionada con Native American code talkers, **"Windtalkers"** (navajos, código usado por EEUU, que confunde varias veces con "Cold Tolkien"/"Code Talkers" al dictarlo).
- El profesor pondrá disponible, para verlo en casa, la película y un **documental** sobre Enigma, y avisa de que hará preguntas sobre ese documental en la parte presencial.
- Libro **"Los códigos secretos" de Simon Singh** — lo recomienda muy efusivamente ("una auténtica pasada"), cuenta toda la historia de la criptografía y menciona que algunas ediciones (la que él tiene) incluyen un CD-ROM con una emulación de la máquina Enigma.
- Libro de **criptografía con Python** (código para copiar y ejecutar: permite montar un Enigma simulado, la escítala espartana, etc.) — recomendado como introducción práctica combinando historia y programación.
- Curiosidad: a lo largo de la historia se han usado libros "de uso común" como clave de cifrado (todo el mundo tiene ese libro, así nadie sospecha), citando el Kamasutra y pasajes bíblicos (p. ej. "artículo 3:7") como ejemplos históricos de libros usados así por los estadounidenses.

## El principio de Kerckhoff (1883)

> «La seguridad está en la clave, no en ocultar el método.»

- Formulado en 1883: un sistema criptográfico debe seguir siendo seguro **aunque el enemigo conozca exactamente cómo funciona el algoritmo**. Lo único que debe permanecer secreto es la **clave**.
- Por eso algoritmos como **AES** y **RSA** son públicos — "todo el mundo los puede ver" — y aun así se consideran seguros, porque la seguridad no depende de ocultar el algoritmo sino de proteger la clave.
- Consecuencia directa: la **seguridad por oscuridad** (confiar en que "nadie sabe cómo lo hice") no es seguridad real — tarde o temprano alguien lo averigua.
- El verdadero problema histórico no es diseñar la clave, sino **repartirla**: ¿cómo transmito la clave a la otra persona sin que el canal sea interceptado? Ahí nace el concepto de ataque **man-in-the-middle** (robar la clave antes de que se complete el intercambio) y el problema que la ingeniería social explota igual (hacerse pasar por un compañero de otro departamento para que alguien "confirme" o entregue su contraseña).

## La teoría de Shannon (1949)

El profesor la presenta junto a Kerckhoff como las dos ideas que "hay que quedarse" de toda la clase:

- **Cifrado perfecto (one-time pad)**: existe un cifrado teóricamente irrompible si la clave es **aleatoria, tan larga como el mensaje y se usa una sola vez**. Perfecto en teoría, poco práctico en el día a día.
- Consecuencia práctica que se aplica hoy: cuanto más se reutiliza una clave, más pistas se dan y más fácil es romperla o que se filtre — de ahí la recomendación de **rotar las claves** y de no reutilizar nunca la misma contraseña.
- Shannon también estudió cómo debía comportarse un buen cifrado en la repetición de operaciones de sustitución/transposición para ser robusto — idea que conecta con por qué algoritmos modernos como AES (que combina muchas rondas de sustitución y transposición) funcionan bien.

Con esto, el profesor resume la clase en dos nombres: **Kerckhoff** (la seguridad está en la clave) y **Shannon** (cuanto menos se reutiliza una clave, mejor).

## Criptografía simétrica vs. asimétrica

### Simétrica (una sola clave)

- Emisor y receptor usan la **misma clave** tanto para cifrar como para descifrar (es el caso de Enigma).
- Problema histórico de siempre: el **reparto de la clave** — cómo comunicarla de forma segura sin que se intercepte.

### Asimétrica (par de claves)

- Nace en **1976** con el algoritmo **RSA**, de **Rivest, Shamir y Adleman** (tres ingenieros; el profesor los menciona también mal transcritos como "Samir Adel y Ramis", pero se refiere a estos tres nombres).
- Cada participante tiene un **par de claves**: una **pública** (conocida por todo el mundo) y una **privada** (que nunca se comparte, solo la conoce su propietario).
- Esto resuelve el problema de reparto de clave de la criptografía simétrica: ya no hace falta transmitir ningún secreto compartido por un canal inseguro.
- Ejemplo de aplicación mencionado por un alumno en clase: subir una clave privada a un servidor y acceder después con la clave pública correspondiente (contexto de montar un túnel / acceso remoto tipo VPN/VNC).
- Mención relacionada: **Diffie-Hellman** (aparece transcrito como "Dizie Gelman" / "Dj Herrman") es el protocolo de **intercambio de claves** (dos desconocidos acuerdan una clave sin haberse visto antes); distinto de RSA pero de la misma familia asimétrica. También se menciona la **criptografía de curva elíptica (ECC)** como evolución posterior, usada hoy en HTTPS.
- Aplicaciones reales citadas: **HTTPS**, banca online, y **WhatsApp** (que usa, según comentan en clase, el algoritmo de cifrado de flujo **ChaCha20** — discusión en directo sin resolver del todo sobre si es WhatsApp o Android quien lo usa exactamente, pero confirman que es un algoritmo "muy ligero").

### Tabla resumen de algoritmos (tal como los enumeró el profesor)

| Tipo | Vigentes | Viejos o rotos |
|---|---|---|
| Simétricos (una clave) | **AES**, ChaCha20 | DES (roto por fuerza bruta: clave de 56 bits, reventado en los 90 probando todas las claves en días), 3DES (parche de DES, repetido 3 veces), RC4 |
| Asimétricos (par de claves) | RSA, curva elíptica (ECC), Diffie-Hellman | ElGamal (mencionado como "viejo o roto") |
| Hashes | SHA-256, SHA3-512, bcrypt/Argon2 (para contraseñas) | MD5, SHA-1 (rotos por colisiones) |

- Dato que da el profesor sin confirmar (pide que se verifique): el NIST podría prohibir el uso de RSA de cara a 2035 — no lo tiene confirmado, lo lanza como algo a vigilar.

## Hash: por qué no es lo mismo que cifrar

Punto que el profesor marca como importante porque generó dudas en directo (pregunta de una alumna, María Eugenia):

- Un cifrado **simétrico** o **asimétrico** siempre se puede revertir si se tiene la clave correcta (secreta o privada).
- Un **hash NO se puede revertir**: es una función de un solo sentido. No existe una "clave" que lo deshaga.
- Para "romper" una contraseña hasheada no se descifra: se usa fuerza bruta o diccionarios con herramientas como **John the Ripper**, probando contraseñas candidatas, calculando su hash y comparándolo con el hash objetivo — contenido que se trabajará en el laboratorio de la semana siguiente.
- **Colisiones**: dos entradas distintas que producen el mismo hash. Se demostraron colisiones en **MD5** y en **SHA-1** (el profesor menciona un caso con dos imágenes distintas que comparten el mismo hash MD5, usado como demostración histórica de la ruptura del algoritmo). Consecuencia real citada: el DNI electrónico español usaba SHA-1 para la firma electrónica y tuvo que migrar a **SHA-512**; durante la migración (hacia 2008-2009) la firma electrónica estuvo caída unos 20 días.

## El candado del navegador (HTTPS, resumen rápido)

El profesor avisa que se profundizará en SAD, pero da el esquema básico:

1. El navegador (cliente) pide una conexión segura al servidor ("hello").
2. El servidor responde con un **certificado que contiene su clave pública**.
3. El navegador genera una **clave secreta de sesión** (simétrica) y la cifra con la clave pública del servidor.
4. Esa clave viaja cifrada por la red — todo el mundo la puede ver pasar, pero solo el servidor, con su clave privada, puede descifrarla.
5. A partir de ahí, cliente y servidor usan esa clave secreta compartida para cifrar el resto de la comunicación con **criptografía simétrica** (más rápida que la asimétrica para grandes volúmenes de datos).

Es decir: la asimétrica se usa al principio solo para intercambiar de forma segura una clave simétrica, y luego toda la comunicación "pesada" va cifrada simétricamente.

## Cifrar vs. firmar

Introducido como adelanto de un tema que se tratará con más detalle en SAD (PKI):

- **Cifrar** y **firmar** no son lo mismo, aunque ambos usan criptografía asimétrica.
- Para **firmar** un documento: se calcula el hash del documento y se cifra ese hash con la **clave privada** del firmante.
- Cualquiera puede **verificar la firma** usando la **clave pública** del firmante (que es de conocimiento general) — si la verificación es correcta, se confirma que solo esa persona (poseedora de la clave privada) pudo haber firmado.
- Resumen: la criptografía asimétrica permite dos usos distintos — cifrar mensajes (confidencialidad) y firmar documentos (autenticidad/no repudio) — y ambos se trabajarán con más profundidad al llegar al PKI en SAD.

## El lado oscuro: ransomware

- El **ransomware** usa la criptografía (cifrado, normalmente con la clave del propio atacante) para cifrar todos los archivos de la víctima, atacando sobre todo la **integridad** y la **disponibilidad** de la información (más que la confidencialidad), y luego pide un rescate a cambio de la clave para descifrar.
- Si el cifrado usado está bien implementado, **no hay forma de recuperar la información sin la clave privada/secreta** — "la matemática te protege, pero también te puede secuestrar".
- Recurso recomendado por el profesor para este tema (lo tratará con más detalle en SAD): la web **"No More Ransom"** (citada como "nomo ransomware"), que recopila información y, en algunos casos, herramientas de descifrado para familias de ransomware concretas.
- Caso real aportado por un alumno en clase: ataque de ransomware a **Deloitte UK** el **10 de octubre de 2026**, con petición de rescate; España también estaría implicada en el incidente según el comentario del alumno (dato de clase, sin verificar por el profesor).

## Para llevar a casa

- **Examen presencial**: jamás escribir "encriptar" — la palabra correcta es **cifrar/descifrar**. Penalización que el profesor anuncia: **-0,25** por cada vez que aparezca.
- **Esta semana no hay "hazlo tú"** de esta clase: se deja para el laboratorio de la semana siguiente.
- **Semana que viene**: laboratorio de **romper contraseñas** (actividad 1 de Ciber) usando Kali — el profesor avisa que con Kali será suficiente, subirá todo el material e instrucciones con antelación. También se tocará copia de seguridad en ese bloque de laboratorios.
- Si da tiempo durante el curso: laboratorio aparte de **cifrados clásicos** (escítala, César, Vigenère, etc.).
- Lectura opcional sugerida: apartado 3.2 del material (no es obligatorio).
- Material recomendado para ampliar por cuenta propia:
  - Película **"Descifrando Enigma"** (2014) + documental sobre Enigma (el profesor hará preguntas sobre el documental en presencial).
  - Libro **"Los códigos secretos"**, de Simon Singh.
  - Libro de **criptografía con Python** (código práctico para replicar cifrados clásicos y Enigma).
  - Web **"No More Ransom"** para el tema de ransomware.
- Recordatorio práctico de higiene de seguridad band sobre contraseñas: nunca guardar claves en texto plano en un fichero tipo "clave.txt" en el propio ordenador ("es el final feliz para muchos atacantes") — usar un gestor de contraseñas.
- Este tema de criptografía se retomará en **SAD** con otro enfoque (PKI, firma digital, el dibujo detallado del candado HTTPS, Diffie-Hellman/IKE en profundidad).
