---
asignatura: Digitalización aplicada a los sectores productivos
fecha: 2026-10-29
tema: "Cierre del Tema 2 (IA y sostenibilidad) e inicio del Tema 3. Cloud y sistemas conectados: qué es (y qué no es) cloud, IaaS/PaaS/SaaS y responsabilidades, contrato, mist/edge/fog/cloud, caso 'ERP de las 5 tiendas'"
fuente: "Transcripción de la clase en directo + temario oficial (Digitalización/dig_tema03) + aportación propia marcada (mío)"
---
# Digitalización · Cierre Tema 2 (IA y sostenibilidad) + inicio Tema 3: cloud (29/10)

> Anterior: [Tema 2: tecnologías habilitadoras (15/10)](2026-10-15_clase3-digitalizacion.md) · Siguiente: [Repaso Temas 1-3 y caso ERP de las 5 tiendas (12/11)](2026-11-12_repaso-temas1-3-caso-erp-5-tiendas-simulacro.md) · Profesor: David Cantos

> [!info] Cómo leer estos apuntes
> Nota pensada para estudiar **sin ver la grabación**. El profesor proyectó diapositivas propias (con tablas comparativas) que **no están en la transcripción**: solo se oye lo que dice. Origen de cada cosa: **(clase)** = dicho en voz alta; **(temario)** = `Digitalización/dig_tema03_cloud_sistemas_conectados.md`; **(mío)** = conocimiento general mío, no dicho en clase ni en el PDF. Las tablas de la clase no se pueden reproducir; las que aparecen aquí las he reconstruido yo (mío) a partir de lo que él dijo y del temario.

## Lo imprescindible (qué estudiar de esta sesión)

1. **Test del Tema 3**: lo que cuenta es el **temario oficial** (el profesor lo repitió). De esta clase se pregunta casi seguro lo que está en el PDF: definición NIST y **5 características**, **4 tipos de nube** (pública, privada, híbrida, comunidad), **edge/fog/mist**, **ventajas** (6 bloques) y los 5 *Entrenamientos*. Ver la sección "Qué cuenta del temario" más abajo.
2. **Cloud = recursos de un tercero, accesibles por red, escalables bajo demanda** (clase). Acceder por VPN a un servidor propio **no es cloud** según el profesor (matiz importante con el temario, ver aviso).
3. **IaaS / PaaS / SaaS**: a más "aaS", menos responsabilidad del cliente. "ERP en la nube" puede ser cualquiera de los tres (clase).
4. **Aunque se migre a la nube, siguen quedando tareas del cliente**: usuarios y permisos, cumplimiento normativo/protección de datos, contraseñas, y conviene una **copia adicional propia y un plan B** (clase).
5. **No todo va a la nube**: procesar cerca del origen (mist/edge/fog) baja latencia, ahorra comunicaciones y se relaciona con la sostenibilidad (clase + temario 3.3).
6. Caso "ERP de las 5 tiendas": **sin terminar**; se retoma en la siguiente sesión.

> [!warning] Discrepancia clase vs. temario: ¿cuándo algo "es cloud"?
> - **Profesor (opinión personal, clase):** un servidor **propiedad de la empresa, en sus instalaciones y mantenido por ella** no es cloud, aunque los empleados accedan desde fuera por Internet con VPN. Para él cloud = infraestructura **de un proveedor externo** (AWS, Azure, Google Cloud...) y escalable según demanda.
> - **Temario (3.2, NIST SP 800-145):** cloud se define por **5 características** (autoservicio bajo demanda, acceso amplio a la red, agrupamiento de recursos, elasticidad rápida, servicio medido), **no** por quién es el dueño. De hecho el propio temario admite una **nube privada "alojada en sus propias instalaciones"** (o gestionada por un tercero).
> - **Consecuencia (inferencia mía):** el servidor con VPN **tampoco** es cloud según NIST (no hay autoservicio, ni agrupamiento, ni elasticidad rápida, ni servicio medido), así que la conclusión coincide; **el razonamiento no**. En un test, responde con el criterio del temario (las 5 características). La frase "es de un proveedor externo" vale para **nube pública**, no para toda la nube.

## Parte 1 · Cierre del Tema 2: ¿IA y sostenibilidad son compatibles?

Debate abierto por el profesor (caso suyo: una alumna de otra formación se negaba a usar IA por su impacto ambiental). Es el tema de **sostenibilidad** que aparece en el temario como resultado de las tecnologías habilitadoras.

**Postura final del profesor (clase):**
- Hay **impacto ambiental real**: consumo eléctrico de los centros de datos, uso de agua, fabricación de los equipos.
- Pero la IA también **aporta beneficios**: optimizar consumo energético en industria y edificios, reducir desperdicios en producción y cadenas de suministro, mejorar procesos y decisiones.
- Conclusión: **ni buena ni mala por sí misma; el impacto depende del uso**. Una frase de una compañera que él suscribió: compatible "mientras se corte el grifo" al uso intensivo sin finalidad técnica, práctica o con sentido.
- **Pregunta que debe hacerse un profesional antes de usar una tecnología**: ¿es realmente necesaria?, ¿qué recursos consume?, ¿qué beneficios aporta?, ¿hay una alternativa mejor?
- Coherencia (argumento de alumnos y profesor): rechazar la IA por su consumo y usar sin problema correo, ordenador o redes sociales también implica servidores y consumo.
- **Sesgo de información**: hay que informarse bien; parte del rechazo viene de lo que se oye por ahí (clase).

> [!warning] Afirmaciones de un alumno, **sin verificar** (no estudiar como hechos)
> En el debate se dijo que una hora de IA equivale a unos minutos de microondas, que el agua de los centros de datos va en circuito cerrado, y que la IA ayudará con baterías y fusión nuclear. El profesor no las confirmó ni desmintió, y **no las he contrastado**. Lo único comprobable en el temario es lo que dice 3.4 (ver abajo). Tampoco se pueden dar por ciertas sin fuentes.

**Resumen de ideas clave del Tema 2 que dio el profesor al cerrar (clase):**
- Se habló de IoT, big data, IA... "a modo superficial", para que suenen y se vean sus aplicaciones.
- Las tecnologías **no son excluyentes: se combinan**.
- Ya están presentes en industria, servicios, comercio (y docencia, que olvidó poner) = **oportunidades profesionales**.
- Debate abierto sin resolver: si estas tecnologías **crean o destruyen empleo**. Opinión del profesor: en el sector TI, bien aprovechadas, serán **más oportunidad que amenaza**.
- Subirá las diapositivas de resumen a la plataforma (como siempre).

## Parte 2 · Tema 3: Cloud y sistemas conectados

Objetivos del tema (temario 3.1): comprender qué es el cloud; identificar **ventajas y riesgos**; reconocer ejemplos; valorar **conectividad, seguridad y disponibilidad**; relacionar cloud con otras tecnologías habilitadoras. Ejemplo del temario: gracias a la nube las pymes acceden a tecnologías antes reservadas a grandes organizaciones.

### 2.1 Definición y características (temario 3.2, para el test)

- **Definición NIST SP 800-145 (Mell y Grance, 2011):** modelo para permitir acceso **ubicuo, conveniente y bajo demanda** a través de la red a un **conjunto compartido de recursos informáticos configurables** (redes, servidores, almacenamiento, aplicaciones, servicios), que se **aprovisionan y liberan rápidamente** con mínimo esfuerzo de gestión o interacción con el proveedor.
- **Las 5 características** (preguntable):

| Característica | Idea |
|---|---|
| Autoservicio bajo demanda (*on-demand self service*) | El usuario aprovisiona sin intervención del proveedor |
| Acceso amplio a la red (*broad network access*) | Disponible por redes estándar desde distintos dispositivos |
| Agrupamiento de recursos (*resource pooling*) | Recursos compartidos entre varios clientes |
| Elasticidad rápida (*rapid elasticity*) | Se escala hacia arriba y hacia abajo, automática o bajo demanda |
| Servicio medido (*measured service*) | El uso se monitoriza, controla y registra |

- **Tipos de nube** (temario 3.2; el profesor **no** los desarrolló en clase, solo dijo que "lo tenéis de forma teórica"):

| Tipo | Qué es | Ventajas | Desventajas | Uso típico |
|---|---|---|---|---|
| Pública | Proveedor externo, recursos compartidos entre clientes | Bajo coste inicial, escalabilidad, fácil acceso | Menos control sobre datos e infraestructura | (genérico) |
| Privada | De uso exclusivo de una organización; en sus instalaciones o gestionada por un tercero | Control, seguridad a medida, cumplimiento normativo | Más coste, mantenimiento complejo | Hospitales, bancos |
| Híbrida | Pública + privada, con movimiento de datos/apps entre ambas | Equilibrio seguridad/flexibilidad, optimiza costes | Complejidad de integración y gestión | Privacidad en procesos críticos + servicios públicos en el resto |
| De comunidad | Compartida por varias organizaciones con intereses o normativas comunes | Coste compartido, más control que la pública, colaboración sectorial | Más cara que la pública, escalabilidad limitada, dependencia entre organizaciones | Sanidad pública, universidades, organismos regionales |

### 2.2 Servidor propio vs. nube (clase; tabla reconstruida (mío))

El profesor mostró una comparativa con estos aspectos: **ubicación de los servidores, propiedad y control, escalabilidad, mantenimiento, disponibilidad, inversión inicial, coste recurrente y responsabilidades**. Los valores de su tabla no se oyen; esta es mi reconstrucción coherente con lo que dijo:

| Aspecto | Servidor propio (en la oficina) | Nube (proveedor externo) |
|---|---|---|
| Ubicación | Instalaciones de la empresa | Centros de datos del proveedor (a veces subcontratados) |
| Propiedad y control | De la empresa | Del proveedor; la empresa contrata el servicio |
| Escalabilidad | Limitada: hay que comprar hardware | Bajo demanda |
| Mantenimiento | Lo hace la empresa o su técnico | Lo hace el proveedor, según el modelo |
| Inversión inicial | Alta (hardware, instalación) | Baja |
| Coste recurrente | Menor, pero mantenimiento y renovación | Cuota periódica (mensual) |
| Responsabilidad | Toda de la empresa | Compartida según IaaS/PaaS/SaaS |

### 2.3 Modelos de servicio: IaaS, PaaS, SaaS y reparto de responsabilidades

Qué dijo el profesor (clase):
- **IaaS (infraestructura como servicio):** el proveedor da servidores, almacenamiento, red y virtualización. El cliente (**el técnico, tú**) **instala, configura y gestiona todo lo demás**, incluidas las **máquinas virtuales**.
- **PaaS (plataforma como servicio):** el proveedor ofrece un **entorno de desarrollo**; tú desarrollas o despliegas ahí tus aplicaciones.
- **SaaS (software como servicio):** una **aplicación completa y lista para usar**.
- "**ERP en la nube**" puede ser cualquiera de los tres, y de ello depende **quién se encarga de servidor, actualizaciones, seguridad y copias**. Su caso más habitual (industria): clientes con servidores antiguos a quienes el **propio proveedor del ERP** les propone SaaS ("olvídate de todo, migramos a la nube").
- Qué incluye normalmente el proveedor en SaaS: infraestructura física y virtualización, sistema instalado y la aplicación; muchas veces **subcontrata** los centros de datos, pero para el cliente es transparente.

Tabla de responsabilidades (el profesor la proyectó; esta es la clásica **(mío, conocimiento general)**; no está en el temario):

| Capa | Servidor propio | IaaS | PaaS | SaaS |
|---|---|---|---|---|
| Datos, usuarios y permisos | Cliente | Cliente | Cliente | **Cliente** (sigue siendo suyo) |
| Aplicación | Cliente | Cliente | Cliente | Proveedor |
| Sistema operativo y *middleware* | Cliente | Cliente | Proveedor | Proveedor |
| Virtualización, servidores, almacenamiento, red | Cliente | Proveedor | Proveedor | Proveedor |
| Centro de datos físico | Cliente | Proveedor | Proveedor | Proveedor |

> [!important] Qué sigue siendo del cliente aunque contrate SaaS (clase)
> Alta/baja de **usuarios y permisos**; **cumplimiento normativo y protección de datos**; **buenas prácticas de contraseñas y accesos**; y vigilar **qué tan seguras son las copias del proveedor**. El profesor recomienda **tener una copia adicional propia** (por ejemplo, descarga local) y **un plan B** (qué pasa si se pierde la conexión o falla el proveedor), sobre todo con datos muy críticos.

### 2.4 Checklist del contrato con un proveedor cloud (clase)

Lo que el profesor mira antes de aconsejar a un cliente (y debe quedar **por escrito**):
- **Qué incluye exactamente** el servicio y el modelo (IaaS/PaaS/SaaS).
- **Disponibilidad y redundancia**; **niveles y tiempos de recuperación**; **tiempos de respuesta**.
- **Copias de seguridad**: cómo se hacen y qué pasa si hay un problema.
- **Escalado**: **tarifas claras** de lo que cuesta crecer.
- **Dependencia del proveedor (*vendor lock-in*)** y **salida**: si cambio de software/ERP o me enfado con ellos, ¿recupero y migro los datos fácilmente o me ponen pegas?
- **Gestión de usuarios y permisos**: quién la hace.
- **Cumplimiento normativo y protección de datos**.
- **Integración**: si se podrán conectar otras aplicaciones o desarrollos propios.
- Importe mensual: **qué cubre exactamente**.

Cuidado (clase): lo que se da "por hecho" y luego causa problemas. Como técnico/consultor puedes tener que asumir configuraciones extra o la gestión de usuarios.

### 2.5 Capas: mist, edge, fog y cloud (clase + temario 3.3)

Pregunta del profesor: ¿tiene sentido enviar **todos** los datos a la nube? Respuesta: no siempre; depende de los requisitos de la aplicación y suele ser más eficiente **combinar varios niveles**. Procesar cerca del origen **reduce latencia** (tiempo de respuesta) y **ahorra comunicaciones innecesarias**, lo que enlaza con la sostenibilidad. Avisó de que no profundiza: es teoría para saber diferenciar los términos cuando salgan.

| Capa | Dónde procesa | Capacidad | Lo que dijo el profesor / temario |
|---|---|---|---|
| **Mist** | En los propios sensores y microdispositivos | Mínima; decisiones sencillas | No hace falta enviar todos los datos a la red; baja latencia. Temario: control autónomo **aunque no haya conexión** con la red superior. Ejemplo temario: el detector de humo activa la alarma él solo ("mist actúa") |
| **Edge** | Dispositivos más cerca del origen, en la propia instalación (en industria, dispositivos industriales) | Algo mayor que mist | Respuesta rápida y control local de datos. Ejemplo temario: cámara que revisa imágenes y solo avisa si ve algo raro ("edge analiza"). Temario: también mejora seguridad al mantener datos en local |
| **Fog** | Nodos intermedios entre dispositivos y nube, en la red de la empresa o del operador | Más que edge | Puede funcionar aunque falle la conexión a la nube; adecuado para varias sedes cercanas. Ejemplo temario: miniordenador que resume datos de sensores ("fog coordina"). El profesor **no recordó un caso real de cliente** con fog |
| **Cloud** | Centros de datos remotos, por Internet | La mayor, **más escalable** | Almacena grandes volúmenes, ejecuta aplicaciones complejas, ideal para analizar datos y copias ("cloud conecta y almacena") |

Frase-resumen del temario: **"mist actúa, edge analiza, fog coordina y cloud conecta y almacena"**.

> [!note] Nota sobre las definiciones
> El profesor y el temario no ordenan exactamente igual edge y fog (el temario define edge como "en el dispositivo o sistema cercano al origen" y fog como intermediario con "mayor potencia que un dispositivo edge"). Para el test, usa la frase-resumen y las definiciones del temario.

## Parte práctica

### Caso real: "El ERP de las 5 tiendas" (sin terminar)

Planteamiento (clase): un cliente real del profesor tiene un **servidor antiguo** con su ERP/programa de producción. Hay que decidir entre:
- **Renovar el servidor local** (nueva instalación local para mantener el sistema), o
- **Migrar a la nube**, p. ej. el propio proveedor del ERP ofrece **SaaS** por una **cuota mensual**.

Se pretende una **comparación económica y técnica**. El profesor hizo una estimación de importe en la diapositiva y avisó expresamente de que **no es real** (aún tiene que pedir presupuestos); el dato económico será "superimportante" para decidir. **No dio las cifras en voz alta**, así que no las tengo.

Se quedó **sin desarrollar por falta de tiempo**. Dijo que antes de la siguiente sesión hablará con el cliente y contará qué han decidido o si sigue pendiente; entonces se plantearán las preguntas y opciones. **No dio plazo ni entregable.**

**Cómo prepararlo (mío, no pedido en clase):** compara a 3-5 años el coste total de cada opción. Servidor local: hardware + licencias + instalación + mantenimiento + copias + electricidad + renovación + coste de caída. Nube/SaaS: cuota mensual x meses + cuotas por escalado + migración + formación + coste de salida. Y aplica el checklist 2.4 a ambas opciones.

## Qué cuenta del temario del Tema 3 (y qué NO se vio en clase)

Archivo oficial: `Digitalización/dig_tema03_cloud_sistemas_conectados.md`.

| Parte del temario | ¿Se vio en clase? | Qué hay que saber |
|---|---|---|
| 3.1 Introducción y objetivos | Sí, solo la lista de objetivos | Ver arriba |
| 3.2 Definición NIST + 5 características | **Mencionado de pasada** ("lo tenéis más teórico"); no se dijo la definición NIST ni las 5 características | Sección 2.1 |
| 3.2 Tipos: pública, privada, híbrida, comunidad (ventajas, desventajas, uso típico) | **No** | Tabla 2.1 |
| IaaS/PaaS/SaaS | Sí (con tabla de responsabilidades propia). **El PDF del Tema 3 no los desarrolla** (solo nombra "SaaS" de pasada en el Entrenamiento 2); es aportación del profesor | Es "fuera de temario" pero el profesor los usó en el caso práctico; **no asumas que caen en el test** |
| 3.3 Edge, fog, mist | Sí, de forma resumida y con tabla | Sección 2.5 |
| 3.4 Ventajas y rentabilidad (innovación, sostenibilidad, oportunidad de negocio, seguridad y TIC, operativas, económicas, datos que respaldan) | **No** | Ver abajo |
| A fondo (2 vídeos) y Entrenamientos 1-5 | **No** | Ver abajo |

### Ventajas del cloud (temario 3.4: **no visto en clase, sí evaluable**)

- **Innovación y aprendizaje continuo:** acceso a tecnologías emergentes (IA, BBDD, *e-learning*); digitalización progresiva sin grandes riesgos; cultura de mejora continua (medir rendimiento, probar soluciones); formación y actualización del personal.
- **Sostenibilidad:** reduce consumo energético (grandes centros de datos más eficientes que muchos servidores pequeños dispersos); minimiza residuos electrónicos; facilita teletrabajo y formación en línea (menos desplazamientos); uso compartido y bajo demanda de recursos.
- **Oportunidad de negocio:** lanzar servicios digitales rápido (e-commerce en días, campus virtual); integración con ERP, CRM...; agilidad comercial; analítica de datos integrada (*dashboards*).
- **Seguridad y TIC:** copias automáticas y programadas; protección avanzada frente a ciberataques (Google, AWS, Microsoft); *disaster recovery* en minutos u horas; control de accesos (usuarios con permisos, registro de actividad).
- **Operativas:** accesibilidad total; trabajo colaborativo y sincrónico; escalabilidad inmediata; mantenimiento invisible (actualizaciones y parches por el proveedor).
- **Económicas:** menos inversión inicial; pago flexible; ahorro en mantenimiento y soporte; evita la obsolescencia tecnológica.
- **Datos que cita el temario:** 49,2 % de las empresas españolas prevé aumentar su inversión cloud en más de un 20 % (Informe del Mercado Cloud en España 2023, Eraneos); el 85 % de las que migraron redujo costes operativos en un 56 % y ganó agilidad en un 57 % (IBM, citado por ITSitio 2024); hasta un 90 % de reducción de costes en LatAm (FTI, 2023). **Ojo**: el propio temario avisa de que no están verificadas de forma independiente y el informe FTI está publicado con logotipo de AWS. Para el test, **conocerlas como "cifras del temario"**.

> [!warning] Contraste temario vs. profesor (en sostenibilidad y seguridad)
> - **Sostenibilidad:** el temario presenta el cloud como **más sostenible** (3.4). El debate de clase matiza que **la IA/centros de datos sí tienen impacto ambiental** y que depende del uso. Para el test responde con el temario; para el criterio profesional, con el matiz.
> - **Copias:** el temario (Entrenamiento 4) da como **"sin riesgo"** que una pyme haga copias automáticas diarias en la nube. El profesor, en cambio, aconseja una **copia adicional propia** y plan B. Para tests, la solución del temario; en la práctica, la del profesor (mío: coincide con la regla 3-2-1 de SAD).

### Entrenamientos del temario (resumen; ejemplos de lo que puede salir)

1. **Elige tu nube ideal** (por perfil de empresa): clínica veterinaria rural -> privada o híbrida; centro de formación online (500 alumnos) -> híbrida; startup de videojuegos -> pública; ayuntamiento con varias sedes -> **comunidad**; asesoría fiscal -> privada; logística internacional -> híbrida; escuela infantil concertada -> comunidad o híbrida; comercio minorista con web -> pública o híbrida.
2. **Verdadero/falso**: nube pública menos segura por defecto = **F**; solo útil en grandes empresas = **F**; permite trabajar desde cualquier sitio = **V**; no necesita copia de seguridad = **F**; requiere obligatoriamente conexión a Internet = **V**; no puede almacenar software, solo archivos = **F** (SaaS); permite escalar según demanda = **V**; migrar elimina todos los riesgos de ciberseguridad = **F**.
3. **Frase/metáfora creativa** sobre el cloud (sin solución única).
4. **La nube bajo amenaza**: WiFi público sin VPN, misma contraseña en todos los servicios, proveedor sin revisar política de datos/RGPD, datos sin cifrar, contraseña de un solo paso (usar doble factor), enlace público sin caducidad, configuración por defecto sin roles (mínimo privilegio) = **riesgo**. La pyme con copias automáticas diarias = **sin riesgo** según el temario (ver contraste).
5. **Antes y después** de incorporar la nube en 7 elementos: gestión documental, trabajo en equipo, coste de mantenimiento, accesibilidad, escalabilidad, seguridad y sostenibilidad. Ejemplos de la solución: antes = archivos locales, e-mail, servidores propios y acceso solo en oficina; después = archivos centralizados, trabajo colaborativo en tiempo real, pago por uso, acceso 24/7 y escalado automático. Las filas de seguridad y sostenibilidad están en el PDF.

## Avisos de logística

- **Grabación**: sesión grabada y disponible en diferido.
- **Diapositivas**: el profesor las subirá a la plataforma "como siempre" (sin fecha). Contienen las tablas comparativas que no se oyen.
- **Participación**: voluntaria; no hay preguntas tontas; puede dirigirse a alumnos por su nombre.
- **Evaluación**: se repite que el **temario oficial** es lo que sirve para evaluar. **No se dio ninguna fecha, tarea ni plazo** en esta sesión.
- **Siguiente sesión**: continúa el caso del ERP de las 5 tiendas. **Sin confirmar** la fecha (sesiones quincenales: lo más probable es el 12/11, inferencia mía).
- Contacto: dudas por correo al profesor.

## Para llevar a casa

1. **Leer el Tema 3 completo** (`Digitalización/dig_tema03_cloud_sistemas_conectados.md`, unas 6-7 páginas de contenido): casi todo el contenido evaluable **no se vio en clase**.
2. Memorizar: **definición NIST**, **5 características**, **4 tipos de nube** con ventaja/desventaja/uso típico, **mist/edge/fog/cloud** y la frase "mist actúa, edge analiza, fog coordina y cloud conecta y almacena".
3. Hacer los **Entrenamientos 1, 2 y 4** (los más preguntables).
4. Entender IaaS/PaaS/SaaS y qué se queda el cliente (útil para la FCT y para SAD aunque no sea del temario).
5. **Comprobar en el aula virtual** si ya está abierto el **test del Tema 3** y su fecha límite (sin confirmar).
6. Revisar el test del Tema 2 si aún no lo has hecho (pendiente de notas anteriores).

> [!warning] Dudas del audio
> - Términos mal transcritos, interpretados por contexto: "Ias" y "P. A, S" (= IaaS, PaaS), "Clow" (= cloud), "Float" (= Google Cloud), "Azul" (= Azure), "Rp" (= ERP).
> - "Fort computing", "miss computing" y "F. O C." = fog y mist computing (transcripción).
> - Se citó un caso de cliente con "servidores antiguos" y se hizo un aparte sobre una alumna de otra formación; el resto de charla con alumnos y los debates personales se omiten.
> - No se oyen las cifras de la estimación del caso (el profesor dijo que además no eran reales).
