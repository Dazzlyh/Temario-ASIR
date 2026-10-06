# Tema 4. Análisis forense en sistemas informáticos
*Ciberseguridad*

## Índice
Esquema · 4.1 Introducción y objetivos · 4.2 Metodologías de análisis forenses · 4.3 Metodología y estándares forenses · 4.4 Documentación y elaboración de informes de análisis forenses · 4.5 Referencias bibliográficas · A fondo · Entrenamientos

## Esquema
**Análisis forense en sistemas informáticos**
- **Objetivos del análisis forense:** determinar las alteraciones producidas en el sistema, la reconstrucción de estas y la identificación de los responsables.
- **Evidencias digitales:** registros del sistema y logs; archivos de usuario y caché; tráfico de red y memoria RAM.
- **Metodologías de análisis forense:** identificación de evidencias digitales; preservación y recolección; análisis y documentación.
- **Elaboración de informes forenses:** resumen ejecutivo y contexto; línea de tiempo de eventos; hallazgos y recomendaciones.
- **Normativas y estándares:** ISO 27037 (identificación y preservación de evidencias); RFC 3227 (recolección y almacenamiento seguro); UNE 71505 (metodología de análisis forense).
- **Herramientas clave:** FTK Imager, EnCase, Autopsy y Volatility (análisis de memoria), Wireshark (tráfico de red).

---

## 4.1. Introducción y objetivos
El análisis forense digital es esencial para resolver conflictos legales, incidentes de seguridad y proteger datos. Consiste en **identificación, preservación, adquisición, análisis y documentación** de evidencias digitales, asegurando su validez legal y fiabilidad técnica.

Al finalizar este tema el estudiante será capaz de:
- Definir qué es el análisis forense informático y qué constituye una evidencia digital.
- Identificar las fases fundamentales de un análisis forense.
- Explicar la relevancia y los requisitos de la evidencia digital en procedimientos judiciales.
- Conocer la importancia de la **cadena de custodia**.
- Reconocer las normativas y estándares (ISO 27037, RFC 3227, UNE 71505 y UNE 71506).
- Elaborar informes técnicos forenses.

---

## 4.2. Metodologías de análisis forenses

### ¿Qué es la informática forense?
El INCIBE la define como: *«El proceso de investigación de los sistemas de información para detectar toda evidencia que pueda ser presentada como medio de prueba fehaciente para la resolución de un litigio dentro de un procedimiento judicial.»*

Dos ideas clave: es un **proceso de investigación**, y las evidencias deben poder presentarse como **medio de prueba** en un procedimiento judicial.

Brown (2010): *«The art and science of applying computer science knowledge and skills to aid the legal process»* — arte y ciencia; los investigadores más eficaces anticipan las acciones y la lógica del individuo que intentan identificar.

Desde un punto de vista corporativo: facilita resolver conflictos de seguridad y protección de datos (vulneraciones de privacidad, competencia desleal, fraudes, robo de información confidencial, espionaje industrial) mediante procedimientos para identificar, asegurar, obtener, analizar y presentar evidencias de forma fiable y admisible judicialmente.

### Evidencias digitales
Cualquier elemento capaz de almacenar información electrónica, física o lógica, que pueda contribuir a esclarecer o confirmar un hecho investigado. Según **ISO/IEC 27037:2016**: *«el conjunto de información almacenada o transmitida en formato binario que puede utilizarse como medio de prueba».*

Tres aspectos: 1) la evidencia es la **información misma**, no el medio que la contiene; 2) debe estar almacenada o transmitida en formato binario; 3) debe poder usarse como prueba válida.

Requisitos adicionales: **relevancia** (relacionada con el caso), **confiabilidad** (procedimientos auditables, reproducibles y consistentes), **suficiencia** (información suficiente para sostener la investigación).

Ejemplos: documento electrónico de texto; archivos temporales de navegación; registros de eventos del SO; registros del tráfico de red; archivo de imagen o vídeo; cookies del explorador; ficheros de logs.

### Objetivos del análisis forense informático
Aclarar y entender los hechos basándose en las evidencias. Tres preguntas: **¿Qué se ha alterado? ¿Cómo se ha alterado? ¿Quién ha realizado la alteración?**

**¿Qué se ha alterado?** Detectar accesos o modificaciones no autorizados: elementos o recursos alterados o utilizados. La detección puede surgir del usuario que nota comportamientos anómalos o de alertas automáticas. No son solo cambios físicos (modificación, eliminación): también archivos consultados, copiados o accedidos sin autorización.
> *Borrado de información:* examen exhaustivo del equipo y sus discos para identificar qué datos se eliminaron y el método; si se sospecha extracción previa, investigar medios externos (USB, historial de navegación, correo…).

**¿Cómo se ha alterado?** Reconstruir total o parcialmente las acciones del responsable; ayuda a prevenir futuras incidencias y crea una secuencia precisa de acciones antes, durante y después.
> *Ciberataque:* identificar con precisión el momento del incidente y reconstruir acciones antes y después.

**¿Quién ha realizado la alteración?** Identificar al responsable; suele ser complejo por las técnicas para ocultar o falsear la identidad.
> *Cibercafé:* se identificó la IP del atacante (un proveedor de Internet) y, con orden judicial, se llegó a un cibercafé con proxy y NAT. Se determinó la MAC del equipo «Número 26», pero el acceso fue con un usuario local genérico y el cibercafé no registra qué usuario usa cada máquina. No se puede atribuir la autoría a una persona concreta, aunque sí a un equipo específico.

Generalmente la conclusión más precisa es el usuario (local o remoto) o la **IP/MAC** del equipo; la identidad física exige técnicas complementarias.

---

## 4.3. Metodología y estándares forenses
Fases: **identificación, preservación (evitar modificaciones), adquisición, análisis y documentación**. Las herramientas, de código abierto o comerciales, facilitan cada etapa. **No existe una única metodología estandarizada** aceptada por toda la comunidad internacional.

### ISO 27037
Familia ISO 27000: buenas prácticas de gestión de la seguridad de la información (SGSI). **ISO 27037** ofrece directrices para **identificación, recolección, adquisición y preservación** de evidencias digitales, para su admisibilidad legal. Cubre: medios de almacenamiento (discos duros, ópticos, magnetoópticos…), dispositivos móviles (teléfonos, PDA, tarjetas de memoria), navegación GPS, cámaras digitales y CCTV, ordenadores personales en red, redes TCP/IP y otros dispositivos que almacenen o transmitan información digital.

### RFC 3227 (IETF)
Recomendaciones para recopilar y almacenar evidencias minimizando el riesgo de alterarlas: prioridad de captura según la **volatilidad**; acciones a evitar durante la recolección; consideraciones de privacidad. El proceso debe estar claramente definido, sin improvisación, con especial atención a la **cadena de custodia**. Herramientas recomendadas: programas para listar procesos activos, software para evaluar el estado del sistema y aplicaciones de copia bit a bit. Inspirado en el **principio de intercambio de Locard**: *«cada vez que dos objetos entran en contacto, transfieren mutuamente parte del material que los constituye»*.

### UNE 71505 y UNE 71506 (AENOR)
Metodología completa para **preservación, adquisición, documentación, análisis y presentación** de evidencias digitales, para incidentes informáticos e infracciones legales en empresas e instituciones. Permiten determinar si el origen de un incidente es intencional o negligencia; aplicables a organizaciones de cualquier tamaño.

---

## 4.4. Documentación y elaboración de informes de análisis forenses
La estructura refleja la calidad y claridad del trabajo.

### Resumen ejecutivo
Breve, para audiencias no técnicas.
- **Contexto:** hechos que motivaron la investigación: qué y por qué, cuándo, quiénes, dónde.
- **Hallazgos y conclusiones:** descubrimientos principales, respondiendo a las preguntas iniciales.
- **Recomendaciones:** reducir el riesgo de incidentes similares, mejorar la respuesta, fortalecer la detección.

### Marco de trabajo
- **Investigadores involucrados:** investigador principal y equipo.
- **Objetivos y alcance:** propósito y delimitación de dispositivos, sistemas o áreas.
- **Entorno:** contexto técnico (nombres de equipos, IP, SO, aplicaciones…).
- **Líneas de investigación:** acciones concretas. Ejemplo: **IL01** identificar signos de presencia o ejecución de los ficheros sospechosos; **IL02** analizar el comportamiento de los ficheros sospechosos; **IL03** análisis de logs de actividad de red con foco en la filtración de información.

### Análisis detallado
Núcleo del informe: procedimientos técnicos, herramientas, resultados, interpretaciones y hallazgos.
- **Línea de tiempo:** fecha y descripción de hallazgos relevantes (texto ordenado, gráfico o línea de tiempo animada).
- **MITRE ATT&CK: tácticas y técnicas:** identificar TTP relacionados con el incidente; se recomienda **ATT&CK Navigator** para resaltarlos.

### Inventario de evidencias
Tabla con, al menos: **ID de evidencia** (EV001, EV002…); **nombre del fichero**; **tipo de adquisición** (física o lógica); **tipo de datos** (imágenes de disco, RAM, registros…); **fuente** (equipo de origen); **descripción detallada**; **herramienta y versión**; **fecha**; **notas adicionales**; **checksum (hash)** (generalmente dos valores); **cifrado** (Sí/No).

---

## 4.5. Referencias bibliográficas
- MITRE ATT&CK GitHub. (s. f.). *MITRE ATT&CK® Navigator.* https://mitre-attack.github.io/attack-navigator/

---

## A fondo
- **Libro sobre evidencias digitales y crimen.** Casey, E. (2011). *Digital Evidence and Computer Crime: Forensic Science, Computers, and the Internet.* Elsevier. Fundamental para técnicas y metodologías; el capítulo sobre recolección y preservación es especialmente relevante para la cadena de custodia y la admisibilidad.
- **INCIBE: glosario de términos de ciberseguridad.** INCIBE. (2021, mayo 18). https://www.incibe.es/empresas/blog/glosario-terminos-ciberseguridad-guia-aproximacion-el-empresario

---

## Entrenamientos

### Entrenamiento 1: recuperación de imágenes borradas en un pendrive
1. Copia varias imágenes a un pendrive.
2. Bórralas de forma habitual (eliminación simple).
3. Descarga e instala **Recuva**.
4. Ejecuta Recuva, selecciona la unidad y realiza un escaneo rápido.
5. Selecciona y recupera las imágenes encontradas.

**Solución:** imágenes recuperadas en una carpeta segura, verificando la integridad.

### Entrenamiento 2: análisis de logs en un servidor web local
1. Instala **XAMPP**.
2. Inicia Apache desde el panel de control.
3. Visita `localhost` para generar actividad.
4. Abre los logs en `xampp/apache/logs/access.log`.
5. Busca entradas inusuales o errores.

**Solución:** listado breve de actividades, fechas, IP (localhost) y tipo de acceso.

### Entrenamiento 3: análisis sencillo de memoria RAM con una máquina virtual
1. Instala VMware Workstation Player y descarga una VM Windows gratuita de Microsoft.
2. Inicia la VM y abre varias aplicaciones.
3. Ejecuta **DumpIt** dentro de la VM para el volcado.
4. Transfiere el archivo al host y analízalo con **Volatility**.
5. Ejecuta comandos básicos como `pslist` y documenta los procesos.

**Solución:** informe breve de procesos, su ID y posible relevancia.

### Entrenamiento 4: investigación en un teléfono móvil
1. Conecta el móvil por cable USB.
2. Explora manualmente sus carpetas desde el explorador de archivos.
3. Identifica y documenta archivos recientes, descargas, imágenes y aplicaciones instaladas.
4. Verifica fechas, tamaños y nombres para detectar elementos sospechosos.

**Solución:** documento breve con hallazgos, tipo de archivos o apps sospechosas y recomendaciones.

### Entrenamiento 5: captura básica y análisis del tráfico de red local
1. Instala **Wireshark**.
2. Inicia una captura seleccionando la tarjeta de red activa.
3. Navega por varios sitios mientras capturas.
4. Detén la captura e identifica direcciones IP, protocolos HTTP y DNS.
5. Documenta patrones y actividad observada.

**Solución:** listado de sitios visitados, IP detectadas, protocolos y resumen de la actividad.
