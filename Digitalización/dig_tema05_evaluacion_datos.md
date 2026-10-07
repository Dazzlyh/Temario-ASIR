# Tema 5. Evaluación de datos

*Digitalización aplicada a los Sectores Productivos (GS)*

## Índice

- Esquema
- Material de estudio
  - 5.1. Introducción y objetivos
  - 5.2. Análisis de datos: machine learning, deep learning, big data
  - 5.3. Aplicación a las empresas de la ciencia de datos
  - 5.4. Importancia de la seguridad en el manejo de datos
  - 5.5. Referencias bibliográficas
- A fondo
  - ¿Cómo impacta el big data en la industria?
  - Big data: el valor de nuestra información
- Entrenamientos
  - Entrenamiento 1. Identificación de aplicaciones de la ciencia de datos en un sector
  - Entrenamiento 2. Clasificación de datos con las siete V del big data
  - Entrenamiento 3. Ejemplo de aprendizaje supervisado y no supervisado
  - Entrenamiento 4. Amenazas en la nube
  - Entrenamiento 5. Evaluación de la fiabilidad de datos

---

## Esquema

*(Esquema original en imagen, de baja resolución; transcrito.)*

**Evaluación de datos**

- **Conceptos clave**
  - Economía impulsada por datos.
  - Objetivos: optimización; predicción; personalización; cumplimiento normativo.
- **Contenidos principales**
  - **Análisis de datos**
    - Ciencia de datos: métodos, procesos y sistemas para extracción de conocimiento. Profesionales: científicos de datos.
    - Inteligencia artificial: algoritmos matemáticos, PLN, visión artificial.
    - *Machine learning*: supervisado, no supervisado y por refuerzo. Algoritmos: regresión, árboles de decisión, vecinos más cercanos.
    - *Deep learning*: redes neuronales profundas, NLP, reconocimiento visual.
    - *Big data*: siete V: volumen, velocidad, variedad, veracidad, viabilidad, visualización, valor.
  - **Aplicación de la ciencia de datos en empresas**
    - Optimización de procesos y costes.
    - Mejora de productos y servicios.
    - Predicción y personalización.
    - Segmentación de clientes.
    - Detección de fraudes y riesgos.
    - Cumplimiento normativo.
    - Ejemplos por sectores: comercio, industria, sanidad, agricultura, logística.
  - **Importancia de la seguridad en el manejo de datos**
    - Tríada CIA: confidencialidad, integridad, disponibilidad.
    - Cultura organizacional y formación del personal.
    - Respaldo y recuperación ante incidentes.

---

## 5.1. Introducción y objetivos

Vivimos en una economía cada vez más impulsada por los datos. Las organizaciones recopilan, almacenan y analizan grandes cantidades de información con el fin de tomar decisiones fundamentadas, anticipar tendencias y optimizar procesos. Esta unidad tiene como finalidad introducir los conceptos fundamentales de análisis de datos y su aplicación a través de herramientas como *machine learning*, *deep learning* y *big data*, así como reflexionar sobre la importancia de la seguridad en la gestión de esta información.

Los objetivos que se esperan conseguir son los siguientes:

- Comprender los fundamentos del análisis de datos y su valor estratégico.
- Identificar qué es y cómo funciona el *machine learning*, el *deep learning* y el *big data*.
- Analizar el papel que juega la ciencia de datos en las empresas actuales.
- Concienciar sobre los riesgos asociados al mal manejo de datos y la importancia de su protección.
- Introducir buenas prácticas en la gestión segura de la información.

---

## 5.2. Análisis de datos: machine learning, deep learning, big data

El análisis de datos es un proceso que permite transformar datos en conocimiento útil. Este proceso puede abordarse desde distintas perspectivas al combinar técnicas estadísticas, algoritmos inteligentes y herramientas de procesamiento masivo. Esta sección aborda tres pilares fundamentales de la evaluación de datos: el *machine learning*, el *deep learning* y el *big data*.

### Ciencia de datos: una visión más amplia

La ciencia de datos no se limita solo al análisis técnico de la información, sino que engloba el conjunto de métodos, procesos y sistemas que permiten interpretar y transformar grandes volúmenes de datos en conocimiento accionable. En este sentido, puede incluir técnicas estadísticas clásicas, minería de datos e incluso métodos avanzados de aprendizaje automático.

Los profesionales dedicados a esta disciplina, conocidos como científicos de datos, combinan habilidades en programación, estadística y pensamiento analítico para detectar patrones, correlaciones y modelos útiles. A diferencia de los expertos en inteligencia artificial, que buscan generalizar soluciones mediante sistemas que aprenden automáticamente, los científicos de datos suelen centrarse en extraer información precisa a partir de conjuntos de datos concretos.

### Inteligencia artificial: base para el análisis avanzado

La inteligencia artificial (IA) agrupa un conjunto de algoritmos que permiten a los sistemas informáticos aprender de los datos, extraer conclusiones y tomar decisiones. Aunque, según el Ministerio de Asuntos Económicos y Transformación Digital (2022), «la estrategia nacional de IA tiene como objetivo situar a España como un referente en el uso de la inteligencia artificial de manera ética, inclusiva y sostenible».

Tiene aplicaciones tan variadas como el procesamiento del lenguaje natural, la visión artificial, la clasificación de objetos, el etiquetado de datos, la agrupación o el sistema de recomendaciones.

Una característica esencial de la IA es que sus modelos pueden mejorar su rendimiento cuando se les exponen a nuevos datos no presentes en el entrenamiento inicial. Por ejemplo, un sistema de vigilancia inteligente podría analizar señales de tráfico, posiciones de vehículos y otros factores para detectar automáticamente una infracción y generar una sanción sin intervención humana.

### Machine learning: el aprendizaje automático

El *machine learning* (ML) es una de las implementaciones más representativas de la IA. Permite que los sistemas aprendan a partir de datos sin necesidad de ser programados para cada tarea específica.

Los principales métodos de ML son:

- **Aprendizaje supervisado:** el sistema aprende a partir de datos de entrada (variables independientes) y su resultado esperado (variable dependiente).
- **Aprendizaje no supervisado:** el modelo detecta patrones por sí mismo sin que se le indique cuál es la salida esperada.
- **Aprendizaje por refuerzo:** la máquina aprende a partir de la interacción con el entorno, recibiendo recompensas o penalizaciones.

El proceso de aprendizaje suele seguir estos pasos:

1. **Preprocesamiento de datos:** limpieza, transformación y preparación de los datos.
2. **Entrenamiento:** el modelo aprende a partir de un conjunto de datos de entrenamiento.
3. **Pruebas:** se validan los resultados del modelo con un conjunto nuevo de datos («conjunto de prueba»).
4. **Producción:** si el modelo alcanza la precisión esperada, puede usarse en entornos reales.

Algunos de los algoritmos más utilizados son regresión lineal, árboles de decisión, regresión polinómica o vecinos más cercanos (k-NN). Hoy en día, gracias a bibliotecas como Scikit-learn, es posible implementar estos modelos sin necesidad de tener conocimientos profundos en estadística, aunque entender los fundamentos siempre aporta valor.

### Deep learning: cuando el problema es más complejo

El *deep learning* (DL), o aprendizaje profundo, es una evolución del *machine learning* basada en redes neuronales artificiales con múltiples capas. Se emplea especialmente cuando se trabaja con grandes volúmenes de datos, muchos atributos o se requiere un nivel muy alto de precisión.

El DL se utiliza en sistemas como asistentes virtuales (Siri, Alexa), reconocimiento de imágenes (como en Facebook o Google Photos), detección de noticias falsas (*fake news*), vehículos autónomos o sistemas de recomendación (Netflix, Spotify, etc.).

Aunque ofrece resultados más precisos y es capaz de resolver problemas complejos, su implementación requiere más recursos técnicos: datos masivos, mayor tiempo de entrenamiento y hardware especializado (como tarjetas gráficas o GPU).

### Big data: el poder de los datos masivos

El *big data* hace referencia al tratamiento y análisis de enormes volúmenes de información que superan la capacidad de las herramientas tradicionales. Estos datos pueden estar estructurados, semiestructurados o sin estructura (texto, imágenes, vídeo, etc.).

Las siete V que definen el *big data* son:

- **Volumen:** cantidad masiva de datos generados constantemente.
- **Velocidad:** rapidez con la que los datos se producen y procesan.
- **Variedad:** diversidad en formatos y fuentes (texto, sensores, redes sociales, etc.).
- **Veracidad:** fiabilidad de los datos, su precisión y calidad.
- **Viabilidad:** capacidad de las organizaciones para aprovechar estos datos.
- **Visualización:** forma clara y accesible de representar datos complejos para detectar patrones.
- **Valor:** utilidad práctica de los datos, es decir, si ayudan en la toma de decisiones estratégicas.

Las tecnologías de *big data* (como Hadoop o Spark) y las plataformas de visualización (como Power BI o Tableau) están ayudando a empresas de todos los sectores a transformar datos en oportunidades. «Los datos son el nuevo petróleo. Son valiosos, pero si no se refinan, realmente no se pueden utilizar. […] Por eso, los datos deben descomponerse, analizarse, para que tengan valor» (Humby, 2006, citado en Murillo, 2021).

> En la sección A fondo hay un artículo sobre el impacto de la IA y la ciencia de datos en los desafíos de la industria moderna.

---

## 5.3. Aplicación a las empresas de la ciencia de datos

La ciencia de datos ha pasado de ser una disciplina reservada a grandes corporaciones tecnológicas, a convertirse en un recurso estratégico para todo tipo de empresas. La ciencia de datos no solo transforma los procesos productivos: redefine la relación entre las personas, la tecnología y la economía (Fundación COTEC, 2020).

> Su aplicación permite tomar decisiones mejor fundamentadas, mejorar la experiencia del cliente y optimizar procesos internos, todo ello mediante el análisis riguroso de los datos.

Los científicos de datos, que combinan conocimientos en estadística, programación y análisis de negocio, se encargan de identificar patrones ocultos, correlaciones relevantes y tendencias futuras. Gracias a sus aportaciones, muchas organizaciones han comenzado a utilizar los datos como base fundamental de su transformación digital. «Las empresas que logren extraer valor de sus datos tendrán una ventaja competitiva significativa frente a aquellas que no sepan hacerlo» (Marr, 2016).

### Principales objetivos de la ciencia de datos en las empresas

Aunque su implementación puede variar en función del sector o del tamaño de la empresa, los objetivos más comunes de aplicar ciencia de datos en el entorno empresarial incluyen:

- **Optimizar procesos:** mediante el análisis de datos operativos, se identifican cuellos de botella, redundancias y oportunidades para automatizar tareas, lo que reduce tiempos y costes.
- **Apoyar la toma de decisiones:** los datos permiten fundamentar las decisiones estratégicas y operativas, dejando atrás la intuición como único criterio.
- **Mejorar productos y servicios:** conociendo en profundidad las preferencias y el comportamiento del cliente, las empresas pueden adaptar su oferta para cubrir mejor sus necesidades.
- **Anticiparse a los cambios:** el análisis predictivo permite prever fluctuaciones de mercado, identificar oportunidades emergentes y detectar posibles amenazas.
- **Segmentar y personalizar:** al clasificar a los clientes en función de su comportamiento y características, es posible ofrecerles servicios más personalizados y relevantes.
- **Detectar fraudes y riesgos:** el análisis de patrones inusuales en los datos puede advertir sobre comportamientos anómalos y prevenir riesgos financieros o reputacionales.
- **Mejorar las campañas de marketing:** utilizando datos sobre hábitos de compra, navegación o interacción, se pueden diseñar campañas más efectivas y orientadas a públicos específicos.
- **Aumentar la satisfacción del cliente:** mediante el análisis de interacciones, quejas o valoraciones, se pueden detectar fallos en la atención y puntos críticos en la experiencia del usuario.
- **Optimizar la cadena de suministro:** desde la previsión de la demanda hasta la gestión del stock, los datos ayudan a hacer más eficiente la logística y reducir desperdicios.
- **Cumplir con normativas:** las herramientas de análisis también permiten monitorizar procesos para asegurar que se cumplan las leyes y regulaciones vigentes, como el RGPD.

*(Tabla 1, en imagen; transcrita.)*

| Sector | Ejemplos de uso de ciencia de datos |
|---|---|
| Comercio | Análisis de compras, segmentación de clientes, fidelización. |
| Industria | Control de calidad, mantenimiento predictivo, productividad. |
| Sanidad | Diagnóstico asistido, análisis de historiales médicos. |
| Agricultura | Monitorización de cultivos, predicción de rendimientos. |
| Transporte y logística | Optimización de rutas, gestión de almacenes. |
| Banca y seguros | Análisis de riesgos, detección de fraudes. |
| Turismo y hostelería | Recomendaciones personalizadas, gestión de reservas. |

*Tabla 1. Aplicaciones de la ciencia de datos por sectores (título de la tabla: «Aplicaciones reales por sectores»). Fuente: elaboración propia.*

La capacidad de transformar los datos en decisiones prácticas está marcando una diferencia sustancial en la competitividad de las empresas. Aquellas que logran integrar la ciencia de datos en su estrategia empresarial están mejor preparadas para adaptarse, innovar y crecer en un entorno económico digital y cambiante.

La ciencia de datos ha adquirido un papel central en la transformación digital de las empresas al permitir convertir grandes volúmenes de datos en decisiones informadas. Esta disciplina no solo abarca técnicas estadísticas, sino que también se apoya en herramientas avanzadas de aprendizaje automático e inteligencia artificial, lo que multiplica su potencial estratégico en los sectores productivos.

### Decisiones basadas en datos: de lo operativo a lo estratégico

Las empresas ya no pueden tomar decisiones únicamente en base a la experiencia o la intuición. Los datos —cuando se recogen, procesan y analizan adecuadamente— se convierten en una fuente fiable para:

- Evaluar el rendimiento de productos o servicios.
- Medir la satisfacción del cliente mediante análisis de opiniones, valoraciones y hábitos de consumo.
- Reaccionar rápidamente ante cambios de mercado, gracias a modelos predictivos que anticipan escenarios futuros.
- Definir nuevas estrategias de negocio fundamentadas en evidencias cuantificables.

Por ejemplo, una empresa de *retail* puede emplear modelos de predicción para ajustar su *stock* a la demanda real, evitar pérdidas y mejorar la experiencia del cliente.

### Roles profesionales en torno a la ciencia de datos

El aprovechamiento real de los datos requiere de perfiles profesionales con conocimientos especializados. Entre los más destacados están *(Tabla 2, en imagen; transcrita)*:

| Perfil | Funciones principales |
|---|---|
| Científico de datos | Extraer conocimiento a partir de datos complejos, diseñar modelos predictivos. |
| Analista de datos | Interpretar datos históricos, generar informes, visualizar patrones. |
| Ingeniero/a de datos | Diseñar la infraestructura de datos, integrarlos desde distintas fuentes. |
| Especialista en BI | Transformar datos en indicadores clave (KPI) para la toma de decisiones ejecutivas. |

*Tabla 2. Roles profesionales en torno a la ciencia de datos con sus funciones principales. Fuente: elaboración propia.*

Aunque muchas pymes no disponen de estos perfiles internamente, cada vez más se recurre a servicios externos o plataformas de análisis accesibles en la nube para explotar sus propios datos.

### Herramientas de ciencia de datos accesibles para empresas

Hoy en día, existen herramientas que democratizan el acceso al análisis de datos incluso para profesionales sin formación técnica avanzada. Algunas de las más populares son:

- **Excel con Power Query y Power BI:** para crear paneles interactivos.
- **Tableau o Looker Studio:** plataformas de visualización intuitiva.
- **Python y bibliotecas como Pandas o Scikit-learn:** para proyectos más avanzados.
- **Plataformas de IA en la nube (Google Cloud, Azure AI, IBM Watson):** ofrecen modelos preentrenados listos para usar.

Estas herramientas permiten, por ejemplo, detectar caídas de ventas en una región específica, identificar productos que generan mayores beneficios o analizar los motivos más frecuentes de reclamaciones de clientes.

### La ciencia de datos como ventaja competitiva

Ya no se trata solo de analizar lo que ha pasado, sino de predecir lo que ocurrirá y proponer acciones concretas. «El análisis de datos ha dejado de ser una cuestión técnica para convertirse en la base de decisiones de negocio inteligentes y sostenibles» (Provost y Fawcett, 2013). Esto convierte a la ciencia de datos en una herramienta clave para:

- Innovar en nuevos modelos de negocio (por ejemplo, suscripciones personalizadas).
- Reducir el impacto ambiental, mediante análisis de consumos energéticos o rutas logísticas más eficientes.
- Ganar agilidad, tomando decisiones más rápidas y basadas en hechos.

En resumen, toda empresa que quiera sobrevivir en un entorno competitivo y tecnológicamente avanzado debe considerar la ciencia de datos como un activo estratégico, capaz de impulsar la eficiencia, la innovación y la satisfacción del cliente.

---

## 5.4. Importancia de la seguridad en el manejo de datos

El tratamiento de datos en el entorno digital conlleva una responsabilidad significativa. Las empresas que hacen uso de tecnologías como la inteligencia artificial, el *big data* o el análisis predictivo dependen de datos precisos, íntegros y accesibles para tomar decisiones y ofrecer servicios. Por ello, la seguridad en su gestión no solo es una obligación ética y legal, sino también una necesidad estratégica para la supervivencia del negocio.

> En la sección A fondo hay un documental de la UNED sobre el poder de los datos masivos y el reto ético que supone su utilización.

### Confidencialidad, integridad y disponibilidad: el triángulo clave

La protección de datos personales es un derecho fundamental para toda persona y debe ser garantizada de manera efectiva en toda actividad económica y social (Reglamento (UE) 2016/679).

Los principios fundamentales de la seguridad informática —confidencialidad, integridad y disponibilidad (conocidos como la tríada CIA, por sus siglas en inglés)— se aplican de forma directa a la gestión de datos:

- **Confidencialidad:** garantizar que la información solo pueda ser consultada por personas autorizadas. Esto se logra mediante mecanismos como el cifrado, la autenticación de usuarios o los permisos de acceso.
- **Integridad:** asegurar que los datos no sean modificados sin autorización o por error. Las técnicas de validación, auditoría y trazabilidad son esenciales para detectar y prevenir alteraciones indebidas.
- **Disponibilidad:** asegurar que los datos estén accesibles en el momento necesario, incluso frente a incidencias técnicas o ataques informáticos. Las soluciones de alta disponibilidad y los sistemas de recuperación ante desastres son fundamentales en este aspecto.

### La seguridad en entornos de computación en la nube (*cloud computing*)

En el contexto actual, muchas empresas han migrado sus operaciones y almacenamiento de datos a plataformas de *cloud computing*. Según Marr (2016), «la seguridad de los datos no es solo una medida técnica: es una parte esencial de la confianza digital y del éxito empresarial a largo plazo».

Aunque esta solución ofrece escalabilidad y flexibilidad, también plantea desafíos específicos de seguridad:

- **Protección de datos sensibles:** la nube alberga información crítica como datos personales de clientes, facturación o propiedad intelectual. Es indispensable establecer medidas estrictas para garantizar que esta información no sea accesible por terceros no autorizados.
- **Control sobre los cambios:** cualquier modificación no autorizada, ya sea intencionada o accidental, puede comprometer la integridad de los datos. Para evitarlo, se implementan mecanismos de control de versiones, registros de cambios y monitorización constante.
- **Garantizar el acceso continuo:** ataques como los de denegación de servicio distribuido (DDoS) pueden dejar inoperativos los servicios basados en la nube. La redundancia y la distribución geográfica de los servidores son medidas clave para prevenir interrupciones.
- **Cumplimiento legal y normativo:** normativas como el Reglamento General de Protección de Datos (RGPD) en Europa o la HIPAA en Estados Unidos exigen que las organizaciones aseguren la protección de los datos personales. El uso de plataformas de nube debe garantizar este cumplimiento, tanto en el almacenamiento como en la transferencia de información.
- **Defensa frente a ciberataques:** el *malware*, el *ransomware* y los intentos de suplantación de identidad (*phishing*) son amenazas constantes. Las plataformas de nube deben ofrecer sistemas de defensa avanzados: *firewalls*, sistemas de detección de intrusiones, autenticación multifactor, etc.
- **Seguridad de la infraestructura física y digital:** la seguridad no se limita al software. También es necesario proteger físicamente los centros de datos, controlar el acceso físico, mantener sistemas de refrigeración, alimentación eléctrica redundante y protección frente a catástrofes.
- **Copias de seguridad y recuperación ante fallos:** un buen plan de seguridad incluye siempre *backups* automáticos y planes de recuperación ante desastres. Estas medidas son cruciales para evitar la pérdida de información ante fallos del sistema, errores humanos o eventos imprevistos como incendios o ciberataques.

### Un desafío estratégico, no solo técnico

Implementar una buena política de seguridad en el manejo de datos no es únicamente una cuestión tecnológica. También implica establecer una cultura organizacional centrada en la protección de la información, lo cual requiere:

- Formación continua de los trabajadores en buenas prácticas digitales.
- Políticas internas claras de acceso, uso y protección de datos.
- Evaluación continua de riesgos y auditorías de seguridad.

En resumen, la gestión segura de los datos se ha convertido en un pilar esencial para la continuidad y la competitividad de las empresas. La adopción de tecnologías en la nube y herramientas de análisis avanzado debe ir acompañada de estrategias sólidas de ciberseguridad y cumplimiento legal. Solo así es posible aprovechar el valor de los datos sin exponer la organización a amenazas, sanciones o pérdidas reputacionales.

---

## 5.5. Referencias bibliográficas

Fundación COTEC. (2020). *Compromisos para la privacidad y ética digital.* https://cotec.es/proyectos-cpt/compromisos-para-la-privacidad-y-etica-digital/

Marr, B. (2016). *Big data en la práctica: cómo 45 empresas de todo el mundo están usando big data para impulsar el éxito.* Editorial Reverté.

Ministro para la Transformación Digital y de la Función Pública. (2022). *Estrategia de Inteligencia Artificial 2024.* Gobierno de España. https://portal.mineco.gob.es/es-es/digitalizacionIA/Documents/Estrategia_IA_2024.pdf

Murillo, J. (2021, septiembre 06). *Los datos son el nuevo petróleo.* Forbes. https://forbes.com.mx/red-forbes-los-datos-son-el-nuevo-petroleo/

Provost, F. y Fawcett, T. (2013). *Data Science for Business.* O'Reilly Media.

REGLAMENTO (UE) 2016/679 del Parlamento Europeo y del Consejo, de 27 de abril de 2016, relativo a la protección de las personas físicas en lo que respecta al tratamiento de datos personales y a la libre circulación de estos datos y por el que se deroga la Directiva 95/46/CE (Reglamento general de protección de datos). *Diario Oficial de la Unión Europea*, de 04 de mayo de 2016. https://eur-lex.europa.eu/legal-content/ES/TXT/PDF/?uri=CELEX:32016R0679

> Nota: las URL largas estaban partidas por saltos de línea en la extracción; se han reconstruido y puede haber algún guion mal restituido. Conviene comprobarlas antes de usarlas.

---

## A fondo

### ¿Cómo impacta el big data en la industria?

Kost, N. (2024, noviembre 18). *El impacto de la IA y la ciencia de datos en los desafíos de la industria moderna.* DataSource.ai. https://www.datasource.ai/es/datascience-articles/el-impacto-de-la-ia-y-la-ciencia-de-datos-en-los-desafios-de-la-industria-moderna

Este artículo explora cómo la inteligencia artificial y la ciencia de datos están revolucionando diversos sectores industriales, desde la manufactura hasta la atención médica. Se destacan aplicaciones prácticas como el mantenimiento predictivo y la mejora de la eficiencia operativa.

### Big data: el valor de nuestra información

UNED Barbastro. (2017, diciembre 15). *Documental "Big Data: el valor de nuestra información" de Modesto Sierra* [Vídeo]. YouTube. https://www.youtube.com/watch?v=xDlV1jCW7n0

Este documental, producido por la Universidad Nacional de Educación a Distancia, aborda cómo el *big data* influye en nuestra vida cotidiana y en la toma de decisiones empresariales, y se destaca la importancia de la gestión y seguridad de los datos.

---

## Entrenamientos

### Entrenamiento 1. Identificación de aplicaciones de la ciencia de datos en un sector

**Planteamiento del ejercicio**

Elige un sector productivo (por ejemplo, agricultura, transporte, comercio o sanidad) e identifica al menos tres aplicaciones concretas de la ciencia de datos en dicho sector.

**Desarrollo paso a paso**

- Investiga el sector elegido y su funcionamiento actual.
- Busca cómo se están utilizando herramientas de análisis de datos (*machine learning*, *big data*, etc.).
- Redacta una breve descripción de cada aplicación (qué problema resuelve o qué ventaja ofrece).

**Solución**

Ejemplo en el sector de la sanidad:

- Diagnóstico médico asistido mediante análisis de imágenes con IA.
- Gestión de historiales clínicos para detectar patrones en enfermedades crónicas.
- Predicción de demanda de camas o recursos hospitalarios.

### Entrenamiento 2. Clasificación de datos con las siete V del big data

**Planteamiento del ejercicio**

A partir de un conjunto de datos sencillo (como una tabla de ventas de una tienda), clasifica la información según las siete V del *big data* (volumen, velocidad, variedad, veracidad, viabilidad, visualización y valor).

**Desarrollo paso a paso**

- Observa los datos (ventas diarias, productos, clientes, etc.).
- Clasifica la información en las siete categorías y justifica cada punto.

**Solución**

- **Volumen:** cantidad de registros (ventas diarias).
- **Velocidad:** actualización cada día.
- **Variedad:** datos de clientes, productos, ubicación.
- **Veracidad:** confiabilidad de los datos, errores de captura.
- **Viabilidad:** cómo usar estos datos para tomar decisiones.
- **Visualización:** gráficos de ventas por producto.
- **Valor:** aumentar las ventas a partir de patrones identificados.

### Entrenamiento 3. Ejemplo de aprendizaje supervisado y no supervisado

**Planteamiento del ejercicio**

Explica un ejemplo de aprendizaje supervisado y otro de no supervisado en el contexto de una empresa de comercio electrónico.

**Desarrollo paso a paso**

- Recuerda la diferencia entre aprendizaje supervisado (datos etiquetados) y no supervisado (patrones ocultos).
- Piensa en un ejemplo práctico para cada tipo.

**Solución**

- **Supervisado:** clasificación de correos como spam o no spam (datos de entrada y etiquetas conocidas).
- **No supervisado:** agrupación de clientes según su comportamiento de compra (descubrir segmentos de clientes automáticamente).

### Entrenamiento 4. Amenazas en la nube

**Planteamiento del ejercicio**

Menciona tres amenazas principales que afectan a la seguridad de los datos en entornos de *cloud computing* y explica una medida de protección para cada una.

**Desarrollo paso a paso**

- Identifica las amenazas (*malware*, accesos no autorizados, pérdida de datos, etc.).
- Para cada una, indica una solución técnica o de gestión.

**Solución**

- Accesos no autorizados → autenticación multifactor.
- Pérdida de datos → copias de seguridad automáticas.
- *Malware* y *ransomware* → *firewalls* y sistemas de detección de intrusiones.

### Entrenamiento 5. Evaluación de la fiabilidad de datos

**Planteamiento del ejercicio**

Tienes datos de un estudio de mercado sobre hábitos de compra. Enumera dos pasos para asegurar la veracidad y fiabilidad de esos datos antes de analizarlos.

**Desarrollo paso a paso**

- Comprobación de la fuente de los datos (¿provienen de un sistema fiable?).
- Validación de la consistencia y limpieza de datos (detección de duplicados o inconsistencias).

**Solución**

- **Paso 1:** revisar el origen de los datos (por ejemplo, un CRM fiable o una encuesta validada).
- **Paso 2:** eliminar registros duplicados o erróneos, estandarizar formatos y asegurarse de que no falten datos clave.
