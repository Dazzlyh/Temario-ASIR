---
asignatura: Ciberseguridad
fecha: 2026-11-03
tema: "Tema 4 · Clase 8 / Laboratorio 4 (parte 1): adquisición de un disco con dd y Guymager, hash, y estructura del informe pericial"
fuente: transcripción de la clase (VTT) + CIBER_Clase08_Practica_adquisicion.pdf (3 págs.). El PDF NO lo facilitó el profesor (según Dani); es probable que sea el documento que un compañero compartió por el chat, sin confirmar. Tampoco se facilitó el .img.
---
# Ciber · 3/11 · Adquirir un disco (`dd` y Guymager) + informe pericial

> Anterior: [Clase 7: análisis forense (27/10)](2026-10-27_clase7-analisis-forense.md) · Profesor: Damián Sualdea Soy

Clase en dos tramos: **teoría del informe pericial** (la primera mitad) y **práctica de adquisición** con `dd` y Guymager sobre un disco de prácticas (`disco_practica.img.gz`). Con esto queda hecho el **apartado de adquisición de la Actividad 1**; falta el análisis de una máquina forense (jueves 5/11) y el informe técnico.

> [!important] Lo imprescindible
> - **Regla de oro:** nunca se escribe sobre la evidencia. Se **bloquea** (solo lectura), se hace una **copia bit a bit**, se calcula su **hash** y se trabaja sobre la copia.
> - **Orden de la práctica:** `gunzip` → `losetup -r` → `dd` → `sha256sum` → Guymager → comparar hashes → `losetup -d`.
> - **El SHA-256 de la imagen empieza por `fa9f1…`** (lo dijo el profesor en voz alta: "a todo el mundo os tiene que salir fa9f1"). El hash completo sale en el PDF (abajo).
> - **El hash del original (`disco_practica.img`) tiene que ser idéntico al de la copia `dd`.** Es lo que prueba que la copia es exacta.
> - **Con una de las dos herramientas basta para la Actividad 1** (palabras del profesor: "con uno de los 2 ya habéis hecho hoy"). Entrega: **capturas + el hash**.
> - **El `.E01` de Guymager NO da el mismo `sha256sum` que el `dd`**: es un contenedor con metadatos. El hash bueno para comparar está **dentro del `.info`**.
> - **Jueves 5/11:** análisis de una máquina Windows 7 (VirtualBox). Hay que traerla **descargada e importada**.

---

## Chuleta de comandos (todos, en orden)

> [!note] Cómo leerla
> Marco de dónde sale cada uno: **(clase)** lo ejecutó o dijo el profesor; **(PDF)** solo viene en el PDF; **(mío)** lo añado yo como dato técnico, no lo dijo nadie. Los que no ejecutó el profesor en directo no están comprobados en clase.

### 0 · Preparar la evidencia

```bash
cd ~/Downloads                    # (clase) botón derecho en la carpeta → "Abrir terminal aquí"
ls                                # (clase) comprobar que aparece disco_practica.img.gz
cp /media/share/disco_practica.img.gz ~/    # (PDF) si está en carpeta compartida, cópiala antes a tu home
cd ~                              # (PDF)
gunzip disco_practica.img.gz      # (clase; en el audio sale como "geocip") deja disco_practica.img
ls                                # (clase) ahora aparece disco_practica.img
```

- El `.gz` es solo compresión para poder moverlo. El `.img` descomprimido equivale al **disco que te entrega el cliente**: "es como si hubiéramos enganchado un USB o el disco duro que nos han pasado con la evidencia".

### 1 · Bloquearlo en solo lectura

```bash
sudo losetup -r -f --show disco_practica.img
# responde:  /dev/loop0      ← ese es el "disco" de prácticas
```

| Opción | Qué hace |
|---|---|
| `-r` | **Solo lectura.** Es lo importante: así no se puede alterar |
| `-f` | Usa el primer dispositivo `loop` libre |
| `--show` | Imprime cuál ha usado (`/dev/loop0`) |

> [!important] Qué hace `losetup` realmente
> Un compañero lo aclaró en clase y el profesor lo confirmó: `losetup` **no monta** el sistema de ficheros, **enlaza el fichero a un dispositivo** (`/dev/loop0`) para tratarlo como disco. El profesor lo comparó con `mount`. Lo que importa es el **`-r`**.
> Si cambias un solo bit, el hash cambia por completo; por eso se bloquea **antes** de tocar nada.

### 2 · Adquirir a mano con `dd`

```bash
sudo dd if=/dev/loop0 of=imagen_dd.dd bs=4M status=progress
```

| Parte | Significado |
|---|---|
| `if=` | *input file*: el **origen** (aquí `/dev/loop0`) |
| `of=` | *output file*: el **destino** (la imagen que creas) |
| `bs=` | *block size*: tamaño de bloque. El profesor dijo "es el tamaño del bloque"; **el valor `4M` viene del PDF** |
| `status=progress` | Muestra el avance en pantalla |

- Es una **copia bit a bit** (también copia el espacio libre). Tarda poco porque el disco de prácticas es pequeño; con discos grandes tarda mucho.
- Cuidado al teclear: el profesor avisó de que con `dd` hay que ir con ojo con origen y destino ("sin más… cuidado en dd"). Mío: si cambias `if` y `of` destruyes el origen.

### 3 · Sellarla con el hash

```bash
ls                                  # (clase) comprobar que existe imagen_dd.dd
sha256sum imagen_dd.dd              # (clase) hash de la copia
sha256sum disco_practica.img        # (clase) hash del original: debe salir el MISMO
md5sum imagen_dd.dd                 # (PDF da el MD5; el comando es mío)
```

| Qué | Valor | De dónde |
|---|---|---|
| **SHA-256** | `fa9f179ce1c31dd090c166b3a1d81321be511b95d2be17bd0142d5a834ecf40e` | PDF. El prefijo `fa9f1` lo confirmó el profesor |
| **MD5** | `77fbab58ff42037677811b6d7144001b` | Solo el PDF |

> [!note] Fuente de los valores
> El hash completo y el MD5 salen del PDF, y **ante duda se da por bueno el PDF antes que la transcripción** (regla de Dani para los laboratorios). El profesor confirmó en voz alta solo el prefijo `fa9f1`, coherente con el PDF. Si tu SHA-256 no coincide, algo falló al copiar.

### 4 · Adquirir en gráfico con Guymager

```bash
sudo guymager        # (clase y PDF) o desde el menú de Kali: Forense → Guymager
```

Contraseña de Kali pedida al abrirlo: en el audio sale "Cádiz Cádiz"; es casi seguro **`kali` / `kali`** (mío, sin confirmar).

Pasos, juntando clase y PDF:

1. En la lista de discos, busca el **`loop0`** (el pequeño).
2. **Botón derecho → Acquire image.**
3. **Formato:** el PDF dice "Expert Witness (.Exx) o Linux dd raw, da igual". En clase se vio **`.E01`** (Expert Witness); el profesor dijo que **también ofrece `dd` puro**.
4. Rellenar los **datos del caso** (clase): número de caso (p. ej. `001`), número de evidencia, examinador, descripción, notas. Es metainformación que queda dentro de la imagen.
5. **Nombre del fichero** de la imagen y del `.info` (p. ej. `copia_guymager`).
6. **Hash:** el profesor marcó **MD5 y SHA-256**. Un compañero marcó solo MD5 y luego no le salía el SHA-256: **marca SHA-256** para poder compararlo con el de `dd`.
7. Marcar **verificar la imagen tras la adquisición** ("Verify image after acquisition").
8. **Directorio de salida:** el profesor lo dejó en `/` (raíz). El PDF recomienda **escribir la ruta a mano** (p. ej. `/home/kali`) y **no usar el botón «…»**, que cierra Guymager (solo está en el PDF).
9. **Start.** Al acabar sale **"Finished - Verified"** en verde.

Ver los hashes:

```bash
ls /                                # (clase) aparecen copia_guymager.E01 y copia_guymager.info
cat /copia_guymager.info            # (clase) el .info contiene los hashes MD5 y SHA-256
grep -i sha256 /copia_guymager.info # (PDF) filtra solo el SHA-256
```

También: **botón derecho sobre el disco ya adquirido → Info** (datos de la adquisición y hashes dentro de Guymager).

> [!important] El detalle que el profesor se tuvo que corregir en directo
> Intentó `sha256sum` sobre la imagen de Guymager y **no salía el mismo** hash. Motivo: el **`.E01` no es la imagen pura**, es un formato forense que añade datos del caso y metadatos (un compañero lo comparó con pasar un Word a PDF: el contenido está dentro, pero el fichero es otro). Por eso:
> - El **`.E01`** (Expert Witness) es más grande que el `dd` y se puede **trocear** (`.E01`, `.E02`…) si el disco es muy grande.
> - Para comparar, **usa el SHA-256 que está dentro del `.info`**, no el `sha256sum` del `.E01`.
> - Si quieres una copia que dé el mismo `sha256sum` directamente, elige **dd raw** en Guymager.
> - Guymager **sí hace adquisición** (no solo análisis): "es como el `dd`, pero trabaja de otra forma". En su caso, el `dd` es "el más puro": copia bit a bit sin nada más.

### 5 · La comprobación

```bash
sha256sum imagen_dd.dd                          # el de dd
cat /home/kali/imagen_guymager.info | grep -i sha256   # el de Guymager (ruta de ejemplo del PDF)
```

**Tienen que ser el mismo.** "Mismo disco, dos herramientas, la misma huella: eso es la cadena de custodia" (PDF).

### 6 · Soltar el disco (al terminar)

```bash
sudo losetup -d /dev/loop0
```

El profesor lo nombró al final ("y luego soltar el disco"); el comando exacto es del PDF.

### Con un disco o USB de verdad (solo PDF; el profesor lo dejó para otro día)

```bash
lsblk                                            # ver los discos; el USB será sdb (o sdc)
sudo dd if=/dev/sdb of=imagen.dd bs=4M status=progress
sha256sum imagen.dd
```

- Lo **único que cambia** es el origen: en vez de `/dev/loop0`, el dispositivo real (`/dev/sdb`).
- La garantía de solo lectura que hoy da `-r` la daría en un caso real un **bloqueador de escritura por hardware** (*write-blocker*).
- El profesor adelantó que en la realidad necesitas **otro disco del mismo tamaño o un USB** donde guardar la copia exacta; lo contará otro día.

### Otros comandos y avisos (solo PDF, no se ejecutaron en clase)

```bash
sudo apt install dcfldd        # dcfldd = dd que calcula el hash a la vez (necesita red)
# Si da "command not found": no viene instalado → SÁLTATELO; Guymager hace lo mismo.

# Si apt da "NO_PUBKEY / signatures couldn't be verified" (clave de Kali caducada):
sudo wget https://archive.kali.org/archive-keyring.gpg -O /usr/share/keyrings/kali-archive-keyring.gpg
sudo apt update
```

**Si algo falla (PDF):**

| Síntoma | Solución |
|---|---|
| Guymager se cierra al pulsar «…» | No uses ese botón: escribe la ruta del *Image directory* a mano |
| `dcfldd: command not found` | No viene instalado; sáltatelo |
| `losetup` da *operation not permitted* desde la carpeta compartida | Copia antes el `.img` a tu home (`cp … ~/`) y trabaja ahí |
| `apt` da `NO_PUBKEY` | Reinstala el *keyring* (comandos de arriba) |

### Comandos solo mencionados de pasada (no ejecutados)

- `mount`: como analogía de `losetup`. El profesor recordó que antes trabajaba con `mount` y una orden tipo `mkfs` (crear el sistema de ficheros); el audio es confuso, **sin confirmar** cuál era.

---

## Material que no se recibió

> [!warning] Dos cosas que faltan
> - El **`.img.gz`** no ha llegado (el profesor lo repartió en clase); sin él no puedo comprobar los hashes ni los tamaños. Los hashes que doy son los del PDF.
> - El **PDF no es del profesor** (según Dani). El audio describe un documento que un compañero pasó por el chat con "todos los comandos analizados y todos los parámetros"; es probable que sea ese, **sin confirmar**. Aun así, **en los laboratorios la transcripción no recoge todo lo del PDF**, así que si difieren, **manda el PDF**; lo señalo donde pasa.

---

## Teoría: el informe pericial

El profesor lo dio en la primera mitad, con diapositivas que **no tengo**; esto sale de la transcripción.

> [!important] Idea central
> **Un análisis forense que no sabes explicar no vale para nada.** El informe lo va a leer un juez, un abogado o recursos humanos, y no tienen por qué saber informática. "No puedes hablar del hash sin definir qué es un hash. No puedes decir que usaste una herramienta sin explicar con qué fin."

### Principio de Locard

"Quien comete un acto deja algo y se lleva algo." En lo digital: **si abres, copias, conectas un USB o borras un fichero, dejas huellas.** El audio dice "Loca"; casi seguro es **Locard** (mío). Es la base de todo el forense, incluido el informático.

### Estructura del informe (según el profesor, apoyada en la norma UNE)

La norma que citó se oye como "197 0 0 1": es probable que sea la **UNE 197001** (criterios para informes y dictámenes periciales; es mío, sin confirmar por el profesor).

1. **Datos y objeto:** quién lo firma, para quién y qué se pide resolver (alcance).
2. **Resumen ejecutivo:** **5 o 6 líneas**: qué pasó, cuándo, impacto. Es lo que lee el juez; "luego se va a las conclusiones".
3. **Metodología:** fases seguidas y **estándar** (el profesor citó la RFC 3227 en la clase anterior); hay que ponerlo.
4. **Cadena de custodia:** quién ha tenido la evidencia, cuándo y por qué.
5. **Hallazgos:** cada uno con su **evidencia**.
6. **Conclusiones:** lo más importante, **basadas en los hallazgos**.
7. **Anexos:** la parte técnica; casi nadie los lee, pero tienen que estar.

> [!important] Cómo se escribe un hallazgo
> Ejemplo del profesor: *"Fichero con credenciales borrado en Documentos, creado el 20/10 a las 3:16, borrado poco después, recuperado con [herramienta de Kali]."* Y cada hallazgo lleva: **qué se encontró, cuándo, con qué herramienta, sobre la imagen (no el original), el hash del fichero y la captura del comando.**

> [!warning] En las conclusiones, nunca a nivel personal
> **No puedes decir que "una persona ha hecho una cosa"**; dices que **"en ese ordenador se han hecho determinadas cosas"**. Solo se afirma lo que se puede **probar** ("una afirmación respaldada por una evidencia"); lo que no puedas demostrar, "ni se te ocurra ponerlo".

### Cómo redactarlo

- Lenguaje claro ("en cristiano") y frases cortas; sin tecnicismos sin explicar, porque "después te van a sacar y te van a decir: ¿me puedes explicar esto?".
- **Documentar desde el minuto 0**: el informe se construye mientras haces las evidencias; se anota todo sobre la marcha.
- **Cada evidencia con su hash** desde el principio (MD5, SHA-1 o SHA-256).
- Lo ideal es trabajar **siempre con la evidencia bloqueada**. En las máquinas de Windows 7 del jueves sí se "tocará" por dentro para ver cómo se saca información, pero lo ideal es bloquearlas.
- **Usa la IA** para dar forma al informe ejecutivo: alimentarla con las evidencias y pedirle un lenguaje comprensible. Es consejo del profesor de Ciber; ojo, en **SAD** el criterio de corrección penaliza el texto generado por IA sin supervisión (README, línea de SAD Actividad 1).

### Si vas a juicio (contexto, no examen según lo dicho)

- El informe lo **firma el perito** (cada hoja, en el lateral) y lo **defiende** ante el juez y los abogados. Puede haber un **interrogatorio**. Hay una "lucha de peritos": la otra parte trae el suyo; si el juez no lo ve claro, nombra otro.
- **Criterio de Daubert** (si tu prueba vale o no): técnica **probada y repetible**, **revisión por pares**, **tasa de error** y **aceptación científica**. Problema que planteó: una herramienta **privativa** de la que no puedes ver el código, ¿qué aceptación científica tiene? Mío: Daubert es un criterio estadounidense; el profesor lo presentó como referencia general, sin decir que se aplique en España.
- **No hay título oficial de perito.** Hoy se suele pedir ingeniería informática, pero él empezó en 2013 sin que existiera el grado. Hay listas de peritos judiciales y colegios profesionales.
- Lo ve como un **plan B** para un extra; personalmente no le gusta por los juicios y el seguro de responsabilidad civil que hay que tener.
- **Certificaciones:** las caras (el audio dice algo como GIAC, GCFE…; **nombres sin confirmar**) y las accesibles: **CHFI** y **BTL1** (Blue Team Level 1). Su consejo: empezar por **BTL1 o CHFI** y que las empresas te paguen las caras.

---

## Logística y para llevar a casa

> [!important] Calendario y entregas
> - **Lunes 9/11: entrega de la Actividad 1 de Ciber.** Dijo que no hay que agobiarse, que lo que se hace en clase es suficiente y que se pierde poco tiempo.
> - **Jueves 5/11 (laboratorio 4, parte 2):** análisis de una **máquina forense Windows 7**. Tiene **3** (`forense 1`, `2` y `3`) en formato **.ova para VirtualBox**: se bajan (por un enlace de transferencia de ficheros) y se importan con **doble clic**. Él hace una o dos en clase; "hasta donde lleguéis". Dijo que los enlaces los publicará en el **foro**. **Sin confirmar** si es obligatorio tener las tres montadas: en un momento dijo "tienen que ser las 3".
> - El **informe técnico** se redacta **después del jueves**, según lo que el profesor vaya indicando; "todas las soluciones las hacemos en clase" y eso alimenta el informe ejecutivo.

### Qué entregar del apartado de adquisición

- **El hash de la imagen** y **capturas de la adquisición**: la de `dd` con su `sha256sum` y/o la de Guymager con su `.info` o con botón derecho → Info.
- Hacer **una de las dos** herramientas basta; hacer las dos y comparar es la mejor prueba.

### Checklist

- [ ] Descargar las 3 máquinas forenses (`.ova`) y **importarlas en VirtualBox** antes del jueves.
- [ ] Conseguir el `disco_practica.img.gz` y repetir la práctica en casa si no la hiciste en clase.
- [ ] Guardar capturas: `sha256sum` de la copia `dd`, y Guymager (*Finished - Verified* + Info/.info).
- [ ] Empezar el esquema del informe técnico con los apartados de arriba.
- [ ] Repasar: 4 fases, orden de volatilidad, qué demuestra el hash, cadena de custodia (examen).

## Dudas y cosas sin confirmar

- **El PDF no es del profesor** y yo no tengo el `.img`: los hashes completos y el MD5 no los he podido comprobar yo (se dan por buenos según el PDF).
- **Fecha de entrega de SER:** el profesor dijo en clase que "también coincide con una entrega de SER el día 9". El material de SER dice **lunes 16/11**. No lo doy por resuelto. Posible malentendido del audio (la "entrega intermodular" también cae esa semana).
- **El laboratorio del 29/10**, anunciado en la clase 7, **no tiene nota**: no sé si se hizo. Esta clase dice "lo he adelantado". La práctica de adquisición se hizo hoy (3/11).
- Nombres de las certificaciones caras y la asociación de peritos (audio ilegible).
- Si es obligatorio tener las 3 máquinas el jueves.
- Qué se pide exactamente como "informe técnico" (extensión, formato): lo concretará el jueves.
