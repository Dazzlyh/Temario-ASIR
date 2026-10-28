---
asignatura: Ciberseguridad
fecha: 2026-10-22
tema: "Tema 3/4 · Laboratorio 3: contraseñas — generar, identificar y romper (crunch, hashid/name-that-hash/hashcat, John the Ripper) + cifrado (gpg) + copias (rsync/cron)"
fuente: "CIBER_Lab03_Guia.pdf (8 páginas) + transcripción de la clase en directo"
---
# Ciber · Laboratorio 3 (22/10) · Contraseñas: generar, identificar y romper

> Anterior: [Clase 6: Contraseñas y copias (20/10)](2026-10-20_clase6-contrasenas-copias.md) · Siguiente: [Clase 7: análisis forense (27/10)](2026-10-27_clase7-analisis-forense.md) · Profesor: Damián Sualdea Soy

**Aviso legal de la guía** (recordado al inicio del documento oficial): todo lo que se hace aquí — generar, identificar y romper contraseñas — **solo está permitido contra tu propia máquina**. Hacerlo contra sistemas ajenos sin autorización puede incurrir en los **artículos 197 y 264 del Código Penal**.

## Qué se hizo realmente en vivo y qué quedó para casa

Esto es lo más importante de esta sesión, porque **no dio tiempo a toda la guía** (8 páginas, 3 partes). El propio Dani avisa de que hay pasos que completó él después de clase. Según la transcripción:

| Parte de la guía | ¿Se hizo en clase en directo? |
|---|---|
| **Parte 1** — Generar con `crunch` | **Sí**, completa y con bastante tiempo dedicado (incluye demo de escalado de tamaño) |
| **Parte 1** — Crear usuarios ana/luis/eva y ver el hash en `/etc/shadow` | **Sí**, en directo (`useradd` + `chpasswd` + `grep` sobre shadow) |
| **Parte 1** — Identificar con `hashid` | **Sí**, en directo, con varios hashes sueltos (MD5/SHA1/phpass/MySQL) y también con el hash yescrypt de ana/luis/eva (falló, como predice la guía) |
| **Parte 1** — Identificar con `name-that-hash` (nth) y `hashcat --identify` | **Sí**, en directo — con incidencias de instalación en varios portátiles (ver abajo) |
| **Parte 1** — Romper ana/luis/eva con John (`--format=crypt` + rockyou) | **Parcial**. Solo **ana cayó en clase** (instantáneo, "123456"). **Luis NO llegó a caer en directo** — el profesor tuvo que pararlo con Ctrl+C por falta de tiempo/CPU al 100 %, y lo dejó pendiente (confiaba en que caería "con reglas" pero no se confirmó en pantalla). **Eva, como estaba previsto, no cayó** |
| **Parte 1** — Romper un hash suelto con `--format=raw-md5`/`raw-sha1` | **Sí, intentado en directo**, con tropiezos reales (ver "Notas en directo") |
| **Parte 1** — `john --list=formats` y `john --test` (benchmark) | **Sí**, en directo |
| **Parte 1 bonus** — Romper un ZIP con `zip2john` | **Sí**, completo y en directo (contraseña `1234`) |
| **Parte 1 bonus** — `office2john`, `pdf2john`, `rar2john` | **Solo mencionados**, no se ejecutaron en clase (se explicó que siguen el mismo patrón que `zip2john`) |
| **Parte 1** — John vs Hashcat (CPU vs GPU, `--format=` vs `-m`) | **Explicado oralmente en directo**, sin demo adicional de hashcat crackeando nada (solo el `--identify` de antes) |
| John the Ripper aplicado a WPA/WiFi | **No**, mencionado solo como algo que se usará más adelante al dar la parte de Wifi |
| **Parte 2** — Cifrado con `gpg` | **No se hizo en clase.** El profesor lo asignó explícitamente para hacer en casa |
| **Parte 3** — Copias con `rsync` + `cron` | **No se hizo en clase.** También asignado para casa |

> Palabras del profesor al cierre, confirmando el reparto: *"Yo la quiero que lo probéis en casa [...] es por GPG [...] no me da tiempo a probarlo en casa [en clase] [...] y luego tenéis un rsync con Chrome, que también es muy interesante que lo hagáis."* (la transcripción automática confunde algunas palabras, pero el sentido — GPG y rsync quedan para hacer por cuenta propia — es claro y es justo lo que Dani ya avisaba).

Conclusión práctica: **lo que hiciste tú después de clase (GPG y rsync/cron) no es que te hayas "adelantado" ni que falte revisarlo con el profesor — es exactamente el tramo que él mismo dejó fuera de la sesión en vivo por falta de tiempo.** El cracking de la contraseña de Luis tampoco se vio caer en pantalla durante la clase; si lo completaste tú en casa, es la parte que quedó a medias en directo.

## Parte 1 · Generar con `crunch`

```bash
crunch 4 4 0123456789            # PIN de 4 cifras: 10 000 combinaciones
crunch 4 4 0123456789 | wc -l    # cuenta combinaciones
crunch 4 4 0123456789 -o pins.txt
crunch 1 3 abc
crunch 6 6 -t ana%%%             # patrón: "ana" + 3 dígitos
crunch 8 8 abcdefghijklmnopqrstuvwxyz   # ~200 000 millones de combinaciones, Ctrl+C
```

Símbolos de patrón (`-t`): `@` = minúscula, `,` = MAYÚSCULA, `%` = número, `^` = símbolo.

**Demo de escalado de tamaño, hecha en directo** (este tramo tiene valor añadido sobre la guía, porque el profesor lo fue construyendo en vivo con la clase, incluyendo preguntas tipo "¿cuánto creéis que pesará esto?"):

| Juego de caracteres | Longitud | Tamaño aproximado (según la demo) |
|---|---|---|
| Solo dígitos (0-9) | 6 | unos pocos MB/GB — "0 megas 0 gigas 0 teras" según el profesor |
| Minúsculas a-z | 6 | ~14 GB |
| Minúsculas a-z | 7 | ~83 GB (con dígitos+letras mezclados daba cifras intermedias, p. ej. ~30-40 GB según la hipótesis previa de la clase) |
| Minúsculas+mayúsculas+dígitos | 8 | ~1 petabyte |
| Minúsculas+mayúsculas+dígitos | 12 (una frase) | ~10 674 petabytes |

El profesor fue preguntando a la clase antes de lanzar cada combinación ("¿creéis que esto va a cambiar una barbaridad o va a ser normal?"), para que la clase intuyera el crecimiento antes de verlo.

> **Conclusión del profesor**: *"Importa la longitud, la longitud. Hay que poner caracteres a mansalva, es decir, es mejor mil veces frases que empezar a hacer combinaciones por dentro, no tiene ningún sentido."*

### Por qué crece así (explicación de María Eugenia, no está en la guía oficial)

Una compañera explicó en voz alta, a petición del profesor, la fórmula que sigue el crecimiento del tamaño del diccionario:

> Tamaño ≈ C^L · (L + 1)

- **C** = la base: el número de caracteres posibles (10 si son solo números; 26 si son solo minúsculas; 26×2=52 si mayúsculas+minúsculas; +10 si además hay dígitos, etc.)
- **L** = la longitud de la contraseña (el exponente)
- **(L + 1)** = un factor de ajuste, relacionado con el peso en bytes de cada línea generada (el carácter de salto de línea, etc.)

El propio profesor reconoció en directo que no conocía bien esta fórmula y que al principio confundía la L con un "2" fijo (pensaba que siempre se elevaba al cuadrado); la alumna le corrigió explicando que es una función **exponencial** sobre la base C, no cuadrática, y que por eso una contraseña de 16 caracteres resulta tan difícil de abarcar ("una colgadera", en palabras de la alumna). El profesor preguntó de dónde había sacado esa fórmula y ella respondió simplemente "preguntando" — él valoró el gesto de haber indagado por su cuenta.

### Hive Systems: cuánto se tarda en romper

Tabla de referencia mencionada (ya vista en la Clase 6): 123456/nombre → al instante; 8 minúsculas → minutos; 8 con mayúsculas+números+símbolos → horas o días; 12+ mezclando todo → siglos; frase larga al azar → prácticamente nunca. Para buscarla: *Hive Systems, password table 2025*.

### Apunte personal del profesor sobre cómo elige sus propias contraseñas (dicho en directo, no en la guía)

El profesor explicó su método personal cuando un alumno le preguntó si recomendaba contraseñas "muy especiales" con símbolos:

> *"Yo primero tengo una frase y dentro de una frase hago cambios [...] para mí una 'e' es una cosa, y para mí una 'a' [...] ya te digo yo que es una arroba [...] Tengo mis frases ya pensadas, todas generadas. Lo único que hago es cambiar [...] entre 13 y 16 [caracteres], depende de muchas cosas."*

Es decir: frase base memorizada + sustitución de caracteres por símbolos (letra→símbolo parecido) que va cambiando con el tiempo, y longitud objetivo de 13 a 16 caracteres. Admite que, aun así, "al final nos pueden robar la contraseña" y que entonces hay que cambiarla.

## Parte 1 · El hash: cómo guarda el sistema tu contraseña (hecho en directo)

```bash
sudo useradd -m ana; echo 'ana:123456' | sudo chpasswd
sudo useradd -m luis; echo 'luis:Verano2026' | sudo chpasswd
sudo useradd -m eva; echo 'eva:x7$Kp9!qLmZ2vB' | sudo chpasswd
sudo grep -E 'ana|luis|eva' /etc/shadow
```

Se confirmó en pantalla que el hash de los tres usuarios empieza por `$y$` (yescrypt), el algoritmo que usa Kali actualmente.

## Parte 1 · Identificar el tipo de hash (hecho en directo)

- **`hashid`**: probado con varios hashes sueltos del documento (tipo MD5/MD2/MD4, tipo SHA-1 — que también puede ser RIPEMD-160, Tiger o lo que usa LinkedIn —, tipo phpass/WordPress y tipo MySQL). Con estos hashes "clásicos" **sí funcionó** y dio varias opciones posibles. Con el hash yescrypt (`$y$`) de ana/luis/eva, **no lo reconoció** ("no es capaz de reconocerlo"), confirmando en vivo lo que ya anticipaba la guía: hashid es una herramienta antigua que no cubre los formatos más recientes.
- **`name-that-hash`** (comando `nth`) y **`hash-identifier`**: probados también contra el yescrypt — **tampoco lo detectaron**. Hubo incidencias reales de instalación: a varios alumnos les faltaba el paquete o tenían una versión antigua, y hubo que hacer `sudo apt update` primero; algún alumno sin conexión a Internet en ese momento no pudo instalarlo en el momento.
- **`hashcat --identify`**: probado sobre un fichero `.txt` con los hashes — este sí **autodetectó** varios tipos (MD4, MD5, y un tipo asociado al número de modo 72000, que según el profesor corresponde a un formato más reciente/menos común).
- **Conclusión explícita del profesor**: *"Ningún identificador es infalible."* Con lo más nuevo (yescrypt) fallan casi todos los identificadores automáticos; la pista definitiva pasa a ser el **prefijo** del hash y **de dónde se ha sacado**.
- **Base64 no es un hash**: demo en directo codificando y decodificando el texto "Hola a todos desde aquí" para mostrar que Base64 se deshace sin ninguna clave — es solo un codificador usado por ejemplo entre servidores de correo para transmitir usuario/contraseña, no una huella criptográfica. (Nota de clase: el profesor intentó gastar una broma codificando otra frase para un alumno y él mismo reconoció que se había "liado" al hacerlo — sin más valor pedagógico que ilustrar que Base64 es trivialmente reversible.)

## Parte 1 · Romper con John the Ripper (hecho en directo, con resultado parcial)

```bash
sudo unshadow /etc/passwd /etc/shadow | grep -E '^(ana|luis|eva):' > hashes.txt
cat hashes.txt
john --format=crypt --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
john --show --format=crypt hashes.txt
```

- `--format=crypt` le dice a John que use la función `crypt()` del sistema, que lee el prefijo del hash para elegir el algoritmo (`$6$`=SHA-512, `$y$`=yescrypt, `$2b$`=bcrypt, `$1$`=MD5-crypt).
- **Resultado real en clase**: Ana cayó casi al instante (`123456`). El ordenador del profesor empezó a ir "petando" (al 100 % de CPU); tuvo que parar con Ctrl+C y relanzar. **Luis no llegó a caer dentro del tiempo de la sesión** — el profesor confiaba en que acabaría cayendo "con reglas" (variación de palabras, porque Verano2026 sí está relacionado con el diccionario rockyou), pero no se vio caer en pantalla. Al hacer `john --show`, solo apareció Ana como resuelta. **Eva**, con 13 caracteres aleatorios con símbolos, confirmado que **no está en ninguna lista y no cae por diccionario**; el profesor fue tajante: *"Eva ni de coña [...] no se puede [romper así], a lo mejor utilizando la máquina encendida años [...] pero que no es suerte."*
- Pregunta de una alumna (María Eugenia) comprobando que entendía bien el experimento: preguntó si dejando correr el proceso un rato más saldría "la de Eva", y el profesor aclaró que no, que las dos que sí pueden caer son Ana y Luis porque están relacionadas con rockyou, mientras que Eva no está en ningún diccionario y requeriría fuerza bruta real.

### Romper un hash suelto (intentado en directo, con incidencias reales)

```bash
john --format=raw-md5 hash.txt
john --format=raw-sha1 hash.txt
john --list=formats | grep -i sha1
```

En el intento real de clase, el primer hash copiado (un MD5 "puro" de los de la fase de identificación) **no se rompió** a la primera (`--format=raw-md5`); el profesor sospechó un error de copiado de la contraseña/hash. Probó el siguiente (un SHA-1) y tampoco funcionó limpiamente al principio, de nuevo por un fallo de copiar/pegar que él mismo reconoció en voz alta: *"Sí, pues es un fallo mío en directo. Así que mientras ese funcione a mí me da igual."* La idea que queda de este tropiezo (más allá de la guía): si `--format=` concreto falla por cualquier motivo, siempre puedes caer de nuevo en `--format=crypt`, que detecta solo.

### `john --list=formats` y `john --test` (hechos en directo)

`john --list=formats` mostró en pantalla la lista completa de formatos soportados (más de 400): Kerberos, SQL con SHA-1, ZIP, NTLM, etc.

`john --test` lanzó el benchmark real sobre la máquina del profesor, mostrando contraseñas/segundo (c/s) para yescrypt, bcrypt y MD5-crypt, entre otros. Regla repetida en clase: **número alto = hash rápido de probar = débil** (p. ej. MD5 crudo); **número bajo = diseñado para ir lento = fuerte** (yescrypt, bcrypt).

### Bonus: romper un ZIP (hecho en directo, completo)

```bash
echo 'secreto' > dato.txt
zip --password 1234 cofre.zip dato.txt
zip2john cofre.zip > zip.hash
john --wordlist=/usr/share/wordlists/rockyou.txt zip.hash
john --show zip.hash
```

Resultado confirmado en pantalla: `password = 1234`. `office2john`, `pdf2john` y `rar2john` se mencionaron como herramientas que siguen el mismo patrón, pero **no se ejecutaron** en clase.

## Tipos de hash (chuleta)

| Tipo | Dónde aparece |
|---|---|
| MD5 | Genérico |
| SHA-512 `$6$` | Linux antiguo |
| yescrypt `$y$` | Linux/Kali actual |
| NTLM | Windows |
| phpass `$P$` | WordPress/PHP |
| bcrypt `$2y$` | Apps modernas |
| MySQL `*...` | Bases de datos MySQL |
| WPA/WPA2 handshake `.cap` | Redes WiFi |
| Base64 | NO es un hash (reversible sin clave) |

## John vs Hashcat (equivalencias, explicadas oralmente en directo)

| Algoritmo | John (`--format=`) | Hashcat (`-m`) |
|---|---|---|
| MD5 | raw-md5 | 0 |
| SHA-1 | raw-sha1 | 100 |
| SHA-256 | raw-sha256 | 1400 |
| sha512crypt `$6$` | crypt | 1800 |
| NTLM | nt | 1000 |
| bcrypt `$2y$` | bcrypt | 3200 |
| phpass `$P$` | phpass | 400 |
| yescrypt `$y$` | crypt (solo John) | no soportado en Hashcat |

- **John the Ripper** va por CPU, identifica el tipo por **nombre** (`--format=`).
- **Hashcat** va por GPU (mucho más rápido), identifica el tipo por **número** (`-m`, que se obtiene con `--identify` o mirando la columna que da `hashid`).
- Dato señalado explícitamente: **yescrypt no lo rompe Hashcat**, solo John (con `crypt`).

## Parte 2 · Cifrar con `gpg` — NO se hizo en clase, queda para casa

```bash
mkdir -p ~/evidencias && echo 'prueba' > ~/evidencias/nota.txt
tar czf evidencias.tar.gz -C ~ evidencias
gpg -c evidencias.tar.gz          # cifra, pide una clave -> .gpg
gpg -d evidencias.tar.gz.gpg > recuperado.tar.gz   # descifra
```

Cifrar es reversible con clave (a diferencia del hash, que no se puede revertir). El profesor comentó que pensaba que daría tiempo a verlo en el laboratorio, pero finalmente no fue así, y lo dejó asignado para hacer por cuenta propia en casa.

## Parte 3 · Copias con `rsync` + `cron` — NO se hizo en clase, queda para casa

```bash
mkdir -p ~/copias
rsync -av ~/evidencias/ ~/copias/evidencias/
crontab -e
0 22 * * * rsync -a ~/evidencias/ ~/copias/evidencias/
crontab -l
rm ~/evidencias/nota.txt
rsync -av ~/copias/evidencias/ ~/evidencias/    # restaurar y comprobar
```

Regla de oro de la guía: *una copia que no se ha probado a restaurar no es una copia, es una suposición.*

## Logística

- Lo que se entrega para la **Actividad 1** con las capturas de este laboratorio: auditoría de contraseñas (generar/identificar/romper), cifrado y copias.
- Fuente de referencia que cita el propio profesor para casi toda la información de John the Ripper: la web de **Openwall** (los desarrolladores de John).
- Al cierre menciona también una herramienta web adicional para comprobar fuerza de contraseñas (mencionada de pasada, sin nombre claro en la transcripción), y anima a seguir investigando el tema de las reglas de John (`--rules`) "más adelante".
- Próximo contenido relacionado: el uso de John the Ripper contra capturas WiFi (handshakes WPA/WPA2) se verá cuando se trate la parte de WiFi, no en este laboratorio.
