---
asignatura: Ciberseguridad
fecha: 2026-10-27
tema: "Tema 4 · Clase 7: análisis forense (fases, evidencias digitales, cadena de custodia, hash, orden de volatilidad, herramientas, certificaciones)"
fuente: transcripción de la clase en directo (la presentación no se ha recibido)
---
# Ciber · Clase 7 (27/10) · Análisis forense: método, evidencias y herramientas

> Anterior: [Laboratorio 3: contraseñas (22/10)](2026-10-22_lab3-contrasenas-generar-identificar-romper.md) · Profesor: Damián Sualdea Soy

Clase 100 % teórica de introducción al análisis forense. El profesor dice que no le da tiempo a más y deja lo práctico (adquisición con `dd`/Guymager, hash y Autopsy) para el laboratorio del jueves 29/10. **Presentación no recibida**: lo que sigue sale de la transcripción.

## Lo imprescindible

> [!important] Resumen de lo que hay que saber
> - **4 fases** del forense, en este orden: **identificación → adquisición → análisis → documentación (informe)**.
> - **Nunca se trabaja sobre el original**: se hace una **imagen bit a bit**, se calcula su **hash** y se trabaja sobre **copias**.
> - **El hash demuestra que la prueba no se ha tocado** (cambia un solo bit y el hash cambia por completo). Se recomienda calcular **MD5 y SHA-256** (los dos).
> - **Cadena de custodia**: registro de quién tiene la evidencia en cada momento; sin ella la prueba se puede impugnar.
> - **Orden de volatilidad**: se recoge **de lo más volátil a lo menos volátil** (RAM antes que disco).
> - **No se apaga el equipo a la ligera** (se pierde la RAM) y **ni siquiera abrir un fichero es inocuo** (cambia la fecha de último acceso).
> - **Lo más importante del análisis es la línea temporal.**
> - Estándares que citó: **RFC 3227**, **ISO/IEC 27037**, **NIST** (el profesor sigue siempre NIST), y una norma **UNE** española.

## 1. Sobre tu duda: ¿"archiving" = buscar en archivos borrados?

Tu intuición va bien encaminada, pero la palabra casi seguro no es "archiving". La transcripción escribe "arcadiving"/"arcaivin" y el profesor lo describe así:

- Al "borrar" un fichero **no se borra, se marca como borrado**: el sistema deja libre el espacio, pero **los datos siguen ahí** hasta que se sobrescriben.
- Hay herramientas que **buscan en los clústeres** (trozos de disco) marcados como libres y **recuperan contenido**, por ejemplo **una imagen** por su formato, aunque esté borrada.
- Cita **PhotoRec** ("Fotorec"), y también **Recuva**: "pasad Recuva por cualquier disco de segunda mano y seguro que encontráis cosas".
- Dice que se puede buscar también en el **slack** (espacio residual).

> [!warning] Término probable (sin confirmar)
> Lo más probable es que diga **file carving** ("tallado de ficheros"): recuperar ficheros leyendo el disco directamente y reconociendo su **tipo por la cabecera/formato**, sin depender de la tabla del sistema de ficheros. Es el que usa PhotoRec. **No está confirmado por la transcripción.** "Archiving" aparece, curiosamente, en el título de la **RFC 3227** ("Guidelines for Evidence Collection and **Archiving**"), pero eso es otra cosa (guía de recogida y conservación de evidencias).
> **Slack space** (mi conocimiento, no explicado a fondo en clase): hueco entre el final real de un fichero y el final del clúster que ocupa; puede contener restos de datos antiguos.

Por eso la adquisición se hace **bit a bit** y **copiando también el espacio libre**: "te copia lo ocupado y lo libre", para poder hacer luego esta recuperación sobre la imagen.

## 2. Qué es el análisis forense (y qué NO puedes decir)

- **Reconstruir lo que pasó** de modo que **las pruebas aguanten un proceso judicial o interno** de la empresa. Ejemplos de incidente: intrusión en la red, fraude, *phishing*, robo de datos, un empleado descontento.
- Preguntas que se contestan: **qué ocurrió, cuándo, cómo** y, si se puede, quién.

> [!important] Regla del perito
> **No puedes afirmar que "una persona" hizo algo**: dices que **desde ese equipo/usuario se hicieron X acciones**. "No tienes ni idea de quién estaba delante": podría ser otra persona con esas credenciales.

- Diferencia con el pentest: **no se trata de entrar, sino de recoger pruebas sin estropearlas**. Si rompes la prueba, ya no vale para un proceso judicial. Comparación del profesor con la policía científica: no se toca nada hasta que está registrado.
- El forense **es una rama aparte** de la seguridad y hay forense de **red, Windows, móvil, impresora (tiene memoria)…**: "se puede hacer forense de todo".

## 3. Las 4 fases

| Fase | Qué se hace | Detalles de clase |
|---|---|---|
| **1. Identificación** | Localizar y clasificar evidencias: **qué equipos y soportes** hay que recoger | Se meten los discos en **bolsas antiestáticas** y se les asigna un **número de serie/identificador** para referenciarlos en el informe. Ejemplo de error: ir a un juicio y decir "había 7 ordenadores" sin tenerlos inventariados |
| **2. Adquisición** | **Copiar las evidencias de forma exacta** y preservarlas | Una copia para el cliente, otra para el notario, etc. **Se calcula el hash** y se compara. Es lo que se hará en la **Actividad 1** |
| **3. Análisis** | Buscar qué pasó; **línea del tiempo** | Herramienta: Autopsy (laboratorio del jueves) |
| **4. Documentación** | **Informe** con evidencias bien preparadas | Como en el hacking ético: documento con evidencias. Dice que **usar IA ayuda** a organizar proyecto e informe, mientras el profesor solo revisará que **las instrucciones y capturas sean correctas** |

## 4. Evidencias digitales: son frágiles

- **Abrir o mirar un fichero ya cambia el original** (fecha de último acceso): contaminas la prueba.
- **Apagar el equipo destruye la RAM**, que contiene procesos, claves, variables y conexiones.
- **Memoria volátil (RAM)** frente a **no volátil (disco)**.
- **Frío** = equipo apagado; **caliente** = equipo encendido. Una adquisición **en caliente** puede ser necesaria si **el disco está cifrado** (apagado no podrías leerlo) o para capturar RAM, pero **el hash "no funciona bien"** en vivo, porque el sistema sigue cambiando.
- El **disco original** se **bloquea contra escritura** y se guarda; solo se trabaja con la **imagen**.
- Imagen **bitstream**: copia bit a bit de un disco entero, **ocupado y libre**. Tarda mucho; lo ideal es un equipo de hardware que lo haga solo ("te vas a tomar un café").

## 5. Hash, integridad y cadena de custodia

| Concepto | Qué dijo el profesor |
|---|---|
| **Hash** | Algoritmo que da un valor único por contenido. Cambia **un solo bit** de un disco de 1 TB y el valor es totalmente distinto |
| **Uso** | **Sello de integridad**: se calcula al adquirir y se recalcula al otro lado; si coincide, la prueba está intacta |
| **MD5** | **Se puede usar** en forense (aunque como contraseña ya no sirva). Un MD5 de un fichero o de un disco de 2 TB vale igual |
| **Recomendación** | Sacar **varios sellos** (MD5 **y** SHA-256) del mismo disco |
| **Cadena de custodia** | Aspecto **legal**: documento en el que se registra y firma cada traspaso (cliente → laboratorio…). El **notario** (o fedatario) certifica que el disco es ese. **Sin cadena, la prueba no vale**: "te pueden decir que la has manipulado" |

> [!warning] Matiz de vocabulario
> El profesor dice "notario" y la transcripción de ese tramo es confusa (parece distinguir entre un notario de verdad y "un notario informático"). La idea que se mantiene es la de una **entidad o persona certificadora** que da fe de que el disco es ese. Los detalles legales los dejó fuera de la clase.

## 6. Qué se busca y dónde (análisis)

**Lo principal: una línea temporal.** Fechas de creación, modificación y acceso de los ficheros; "todo iba bien hasta este momento, ¿qué pasó en ese momento?".

- Ficheros **nuevos**, **borrados** (recuperables), **slack**.
- **Logs**: Windows → **Visor de eventos**; Linux → `auth.log` (intentos de intrusión); Apache → `error.log` y `access.log`.
- **Conexiones de red**: Linux `ss` (el profesor dijo `ss` con las opciones `-ltn`, equivalente a `netstat`); Windows `netstat`.
- **USB conectados** (herramienta USBDeview de NirSoft) y **software instalado**.
- Navegación web, contraseñas guardadas en el navegador (herramientas NirSoft tipo "PasswordsView/WebBrowserPassView": con doble clic, según el profesor).

> [!warning] Corrección importante sobre `net start`
> En clase dijo de memoria que `net start` mostraba las conexiones. **No es así**: **`net start` lista los servicios de Windows en ejecución**; las conexiones de red se ven con **`netstat`** (p. ej. `netstat -ano`). Él mismo avisó de que lo decía "de memoria" y que no hiciera caso. En Linux, `ss` es el equivalente moderno de `netstat`.

## 7. Orden de volatilidad (RFC 3227)

Se recoge **de lo que antes se pierde a lo que más aguanta**. Lista que dictó el profesor (sale del RFC 3227):

1. **Registros y caché de la CPU**
2. **Memoria RAM** → procesos, claves, conexiones abiertas
3. **Estado de la red**: conexiones, **tabla de rutas**, **caché ARP**
4. **Procesos en ejecución**
5. **Disco**: ficheros, borrados, *slack*, recuperación
6. **Logs y monitorización remota**
7. **Soportes físicos**, copias de seguridad en papel, etc.

El RFC también insiste en: **no apagar el equipo, minimizar los cambios, documentar**. La RFC se denomina "Request for Comments".

## 8. Estándares y validez legal

- Hay que **seguir un método reconocido y citarlo**: si no, la otra parte **impugna** la prueba. Se redacta del tipo: *"He hecho este peritaje siguiendo la RFC 3227 y la norma UNE…"*.
- **RFC 3227**: el más conocido; orden de volatilidad.
- **ISO/IEC 27037**: cómo identificar, recoger, adquirir y preservar evidencia digital.
- **Norma UNE** (española): el profesor dijo "UNE 755" en la transcripción, que no existe con ese número; la que trata la evidencia electrónica y la metodología forense es de la serie **UNE 71505/71506** (mi conocimiento, **sin confirmar**).
- **NIST**: guía de respuesta a incidentes; el profesor **sigue siempre NIST** por ser el más universal.
- **Contraste de peritos ("comparación a pares")**: tú haces tu informe como perito de la empresa; el cliente/otra parte **contrata a otro perito**; si el juez no lo ve claro, **nombra un perito de oficio**. Con tres informes, el juez **lee las conclusiones**, que deberían coincidir; si no, hay "opinión". Es **imposible que los documentos sean idénticos**.

## 9. Herramientas

### Adquisición (la que se verá en el laboratorio)

| Herramienta | Tipo | Notas |
|---|---|---|
| **`dd`** | Línea de comandos (Kali) | Copia bit a bit. Se usa sobre dispositivos tipo `/dev/sda1`; el profesor habló de bloques de 4 K (`bs`) y de controlar el progreso. Necesitas **un disco destino del mismo tamaño** (el profesor dijo "del mismo tamaño") |
| **Guymager** ("Guy Mayer" en la transcripción) | Gráfico, viene en Kali | Hace la imagen y puede calcular **MD5/SHA-256 durante la adquisición** |
| **Kali "modo forense"** | Arranque | No monta ni toca los discos, solo lectura |
| **Distros forenses** | Live USB | **CAINE** (italiana, la favorita del profesor, protege contra escritura y trae herramientas), **SIFT** (SANS, sobre Ubuntu), Paladin y otras que **no ha probado** |
| **Bloqueadores hardware** | Dispositivo | Lo conectas entre el disco y el equipo para **impedir escribir**; "duplicadoras forenses" clonan y calculan el hash a la vez |

### Análisis

| Herramienta | Para qué |
|---|---|
| **Autopsy** | La más conocida, gráfica, para abrir imágenes y **crear la línea temporal**. Se verá en el laboratorio (no entra en la Actividad 1) |
| **Volatility** (en Python) | **Análisis de RAM**: procesos, conexiones, volcado |
| **EnCase** y **FTK** | Suites comerciales integradas; guardan metadatos en formato **E01/Ex01** (la transcripción dice "S01"; sin confirmar) |
| **NirSoft** | Utilidades portables de Windows para extraer contraseñas, USB, etc. |
| **PhotoRec / Recuva** | Recuperación de ficheros |
| **WinTriage y otras de triaje** | Herramientas de Windows de una empresa española (nombre del autor no recordado) |
| **Oxygen Forensic** (de pago), **Cellebrite** | Móviles. Cellebrite: usada por la Guardia Civil para abrir móviles bloqueados, **muy cara** |

> [!note] Libros recomendados
> *Blue Team Field Manual* (BTFM) y *Hash Crack* (de comandos, tamaño bolsillo). En BTFM hay un apartado de monitorización de red y captura (honeypots). Según el profesor: "supertécnicos, todo comandos".

## 10. Certificaciones y salidas profesionales (final de la unidad)

- **GIAC** y **SANS**: las más valoradas, "carísimas" (una a dos semanas de formación por unos 10 000 €).
- **CHFI** (EC-Council): "bastante bien", la que aconseja. Es de la misma casa que **CEH** (hacking ético).
- En **España no hay título oficial** de perito informático; hay asociaciones como la **ANPJ** (Asociación Nacional de Peritos Judiciales; nombre dicho de oído, **sin confirmar**) y cursos universitarios o másteres.
- Lo legal (peritaje ante juez) **lo ha dejado fuera de clase**; si hay interés, lo ampliará en el laboratorio.

## Logística y para llevar a casa

> [!important] Actividad 1 de Ciber: entrega el 9 de noviembre
> Ya tienes hechos: **John the Ripper** (laboratorio 3), **cifrado con GPG**, **copia de seguridad con rsync**. Faltan:
> 1. **Adquisición forense con hash** (se hace en el laboratorio del jueves).
> 2. **Informe técnico** (con capturas y las instrucciones correctas; recomienda hacerlo con IA).
> Lo que se vea en clase es lo que cae en la actividad, "menos preguntas, todo más claro".

- **Laboratorio del jueves (29/10)**: conectar un **USB/disco externo a la VM de Kali** (UTM, VirtualBox o VMware), hacer una imagen con **`dd`** (bloques de 4 K), **calcular el hash**, repetirlo con **Guymager**; abrir una imagen con **Autopsy** y **reconstruir un incidente**. Después dará **3 máquinas Windows 7** para practicar en casa.
- Para la próxima: leer fases y estándares (RFC 3227, ISO/IEC 27037, NIST) y **empezar la Actividad 1**, no hay que esperar.
- Pendiente del lab 3: el profesor insiste en que **le cuentes los problemas** que tuvieras (el de rsync/servidores salió "a duras penas" a un compañero): planifica la clase en función de ellos.
- **Clase 8**: parte técnica / informe técnico (según el profesor, sin concretar).
- [ ] Repasar el laboratorio 3 (GPG y rsync) si no lo hiciste.
- [ ] Instalar/comprobar Kali en VM con acceso a USB.
- [ ] Memorizar las 4 fases, el orden de volatilidad y qué demuestra el hash.

## Dudas y cosas sin confirmar

- La palabra exacta que dijo para "buscar en clústeres borrados" (**carving** probable).
- Número de la norma UNE y nombre de la asociación de peritos.
- El formato de imagen de EnCase (E01/Ex01).
- Qué quiso decir con "la clase 8 es la parte técnica".
- La presentación de la clase no se ha recibido: faltan sus esquemas y la lista de certificaciones del final.
