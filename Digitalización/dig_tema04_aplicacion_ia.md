# Tema 4. Aplicación de la IA

*Digitalización aplicada a los Sectores Productivos (GS)*

## Índice

- Esquema
- Material de estudio
  - 4.1. Introducción y objetivos
  - 4.2. IA: tipos y evolución
  - 4.3. IA y los datos: protección de datos, tratamiento de datos y minería de datos
  - 4.4. La IA en los sectores productivos
  - 4.5. Referencias bibliográficas
- A fondo
  - ¿Quién mandará en la inteligencia artificial?
  - Una pausa cuestionable en la inteligencia artificial
- Entrenamientos
  - Entrenamiento 1. Clasifica el tipo de IA
  - Entrenamiento 2. IA en sectores productivos
  - Entrenamiento 3. ¿Es legal? Análisis de un caso ético
  - Entrenamiento 4. Proceso de minería de datos
  - Entrenamiento 5. Debate guiado sobre la IA generativa

---

## Esquema

*(Esquema original en imagen; transcrito.)*

**Aplicación de la IA**

- **Inteligencia artificial. Conceptos. Evolución**
  - Tipos de IA: fuerte/débil; simbólica/subsimbólica.
  - Evolución de la IA: desde Turing (1950) a AGI actual.
  - Ámbitos de aplicación: finanzas, sanidad, industria, etc.
- **Principios clave**
  - Éticos y legales: transparencia, privacidad, derechos, normativa.
  - Técnicos y funcionales: supervisión humana, trazabilidad, precisión, evaluación del riesgo.
- **Datos y minería**
  - Protección de datos.
  - Minería de datos: extracción de patrones, series temporales, etc.
- **Vías de aplicación por sector**
  - Productivos (activos): industria, agricultura, logística. Mantenimiento predictivo, IA generativa, automatización.
  - Servicios (receptivos): sanidad, educación, turismo. Diagnóstico, atención personalizada, predicción de demanda.

---

## 4.1. Introducción y objetivos

La inteligencia artificial (IA) se ha consolidado como una de las tecnologías más disruptivas de la transformación digital. Su capacidad para analizar datos, automatizar procesos y tomar decisiones ha generado un impacto profundo en múltiples sectores productivos. Este tema tiene como finalidad introducir los conceptos básicos de la IA, su evolución y su aplicación práctica, haciendo énfasis en la gestión de los datos y en el marco ético y legal que regula su uso.

Los objetivos que se esperan conseguir son los siguientes:

- Comprender qué es la IA y cómo ha evolucionado.
- Identificar los principales tipos de IA y sus aplicaciones prácticas.
- Conocer la relación entre IA y el tratamiento de datos, así como los principios de la protección de datos.
- Analizar casos reales de aplicación de IA en distintos sectores productivos.
- Valorar los desafíos éticos, legales y sociales asociados a la implementación de la IA.

---

## 4.2. IA: tipos y evolución

La inteligencia artificial (IA) ha experimentado una evolución notable desde sus orígenes y con ella han surgido múltiples formas de clasificarla. Es habitual encontrar términos que se utilizan indistintamente —como IA débil, fuerte, simbólica o subsimbólica—, aunque en realidad hacen referencia a enfoques distintos. Muchos de estos conceptos, acuñados por científicos e ingenieros, están fuertemente ligados a debates filosóficos sobre la mente, la conciencia y la inteligencia. Según Russell (2020), la inteligencia artificial se ocupa del estudio de agentes que perciben, razonan y actúan.

### Tipos y clasificación de la IA

#### Clasificación funcional: IA débil y fuerte

Uno de los enfoques más difundidos distingue entre IA débil e IA fuerte:

- **IA débil (o estrecha):** consiste en sistemas diseñados para realizar tareas concretas. Estos modelos, ya sean de naturaleza simbólica (centrados en procesos mentales) o subsimbólica (inspirados en estructuras cerebrales), son útiles tanto para el desarrollo tecnológico como para la investigación científica. Se centran en la funcionalidad y no en simular una inteligencia completa.
- **IA fuerte:** va más allá de la ejecución de tareas específicas. Aspira a reproducir la mente humana en su totalidad o al menos a imitar su comportamiento general. Esta categoría plantea interrogantes complejos sobre la conciencia artificial y es objeto tanto de investigación avanzada como de narrativa en ciencia ficción.

A continuación, se muestra una tabla comparativa de estos dos tipos de IA *(Tabla 1, en imagen; transcrita)*:

| IA débil | IA fuerte |
|---|---|
| Es una aplicación estrecha con un alcance limitado. | Es una aplicación más amplia con un alcance más amplio. |
| Esta aplicación es buena en tareas específicas. | Esta aplicación tiene una increíble inteligencia a nivel humano. |
| Utiliza aprendizaje supervisado y no supervisado para procesar datos. | Utiliza agrupaciones y asociaciones para procesar datos. |
| Ejemplos: Siri, Alexa. | Ejemplos: robótica avanzada. |

*Tabla 1. Clasificación de IA débil e IA fuerte. Fuente: elaboración propia.*

> Nota: el contenido de la tabla se transcribe tal cual. La fila 3 es discutible desde el punto de vista técnico (el aprendizaje supervisado/no supervisado no es exclusivo de la IA débil, ni la agrupación/asociación de la IA fuerte; hoy no existe IA fuerte) y la fila 4 contradice el texto posterior, que sitúa la AGI como un ideal teórico.

En este marco también se incluyen otros conceptos relevantes:

- **ANI** (*artificial narrow intelligence*): inteligencia artificial especializada en una única tarea. No imita la cognición humana, pero es eficaz y precisa dentro de un contexto definido. Ejemplos comunes son los asistentes virtuales (como Siri o Alexa), sistemas de reconocimiento facial o filtros antispam.
- **AGI** (*artificial general intelligence*): hace referencia a sistemas hipotéticos con la capacidad de comprender, razonar y aprender en múltiples dominios, con una flexibilidad y profundidad similar a la de un ser humano. Hoy en día, sigue siendo un ideal teórico.

#### Clasificación técnica: IA simbólica y subsimbólica

Desde el punto de vista metodológico, la IA se divide en dos grandes corrientes:

- **IA simbólica:** se basa en representar el conocimiento mediante símbolos y reglas lógicas. Aspira a emular el pensamiento humano a través de procesos de razonamiento estructurados. Este enfoque trabaja de forma descendente (*top-down*): primero se define el problema y luego se diseña un sistema que lo resuelva. Los sistemas expertos son su principal exponente, utilizando reglas del tipo si-entonces para tomar decisiones similares a las que haría un especialista humano.
- **IA subsimbólica:** intenta reproducir el funcionamiento del cerebro humano, basándose en modelos como redes neuronales artificiales. En lugar de usar reglas explícitas, aprende a través de la experiencia, entrenando modelos con grandes cantidades de datos. Este enfoque trabaja de forma ascendente (*bottom-up*) y es el fundamento del aprendizaje automático (*machine learning*) y del aprendizaje profundo (*deep learning*).

> En la sección A fondo hay un artículo que plantea una reflexión crítica sobre el desarrollo acelerado de la IA y la necesidad (o no) de frenar su avance. Encaja muy bien con los conceptos de IA débil, fuerte y general, y con el debate sobre el rumbo futuro de esta tecnología.

### Evolución histórica de la IA

El desarrollo de la inteligencia artificial está lleno de hitos que marcan su progresiva sofisticación:

- **1637:** René Descartes plantea la posibilidad de que las máquinas puedan simular el comportamiento animal, introduciendo por primera vez la noción de autómatas sin alma.
- **1950:** Alan Turing publica su influyente artículo «Computing machinery and intelligence», donde propone el test de Turing como criterio para determinar la inteligencia en máquinas.
- **1956:** el término inteligencia artificial se acuña oficialmente durante la conferencia de Dartmouth, por el informático John McCarthy, considerada el punto de partida de la disciplina (National Geographic España, 2025).

  *Figura 1. Fotografía del informático John McCarthy junto a su ordenador. Fuente: National Geographic España, 2025. (Imagen omitida.)*

- **1964:** surge ELIZA, uno de los primeros chatbots capaces de mantener una conversación simple utilizando procesamiento de lenguaje natural.

  *Figura 2. Fotografía del primer chatbot del mundo. Fuente: National Geographic España, 2025. (Imagen omitida.)*

- **1972:** Hubert Dreyfus publica *Lo que las máquinas no pueden hacer*, donde cuestiona las capacidades futuras de la IA y sus limitaciones.
- **1979:** la máquina BKG 9.8 derrota a un campeón mundial de *backgammon*, lo que demuestra el potencial de la IA en juegos estratégicos.
- **1980:** se desarrollan los primeros vehículos capaces de responder a estímulos visuales, sentando las bases de los coches autónomos.
- **1988:** se implementan los primeros sistemas de traducción automática entre inglés y francés.
- **Década de 1990:** nacen los agentes inteligentes, sistemas capaces de percibir su entorno, tomar decisiones racionales y aprender de la experiencia.
- **1997:** Deep Blue, desarrollada por IBM, vence al campeón mundial de ajedrez Garry Kaspárov.
- **2008:** el reconocimiento de voz llega al mercado de consumo con el lanzamiento de la primera aplicación móvil de Google con esta funcionalidad.
- **2012:** gracias a la explosión del big data y la mejora de los algoritmos, una IA aprende por primera vez a reconocer imágenes complejas (como gatos), lo que marca un punto de inflexión en el aprendizaje profundo.
- **2023:** ante el avance acelerado de estas tecnologías, la Unión Europea aprueba la primera ley mundial sobre inteligencia artificial, que establece normas claras sobre su desarrollo y uso responsable.

> Nota: la referencia de RTVE incluida en este mismo tema indica que la Ley de IA entró en vigor el 1 de agosto de 2024. Lo que el texto sitúa en 2023 es, según mi información, un hito del proceso legislativo (acuerdo político/aprobación parlamentaria), no la entrada en vigor.

---

## 4.3. IA y los datos: protección de datos, tratamiento de datos y minería de datos

La inteligencia artificial y los datos están estrechamente vinculados. Los datos no solo constituyen la materia prima con la que los sistemas de IA aprenden y evolucionan, sino que también representan uno de los pilares fundamentales de la transformación digital en Europa. Según Domingos (2015), la base para el aprendizaje automático tiene como meta la construcción de un algoritmo guía que sea capaz de sacar todo el conocimiento en base a los datos.

En la actualidad, la digitalización afecta a todos los ámbitos de la sociedad y la economía, siendo los datos un motor esencial para la innovación, la sostenibilidad y la competitividad global.

### Datos como motor de la IA y la transformación digital

Los datos permiten que la IA genere mejoras significativas en múltiples sectores: desde una atención sanitaria más precisa hasta sistemas de transporte más seguros y servicios personalizados para los ciudadanos. Asimismo, facilitan la optimización de los procesos productivos, aportando ventajas competitivas en industrias clave para Europa como la agricultura, la economía circular, la maquinaria y el turismo.

En respuesta a estos avances, la Unión Europea promueve un enfoque centrado en el ser humano. Este modelo busca consolidar una inteligencia artificial confiable, transparente y ética, que respete los derechos fundamentales y refuerce el papel de Europa como líder en innovación tecnológica responsable.

### Marco legislativo europeo sobre datos e IA

El desarrollo exitoso de la IA en Europa depende en gran medida de una estrategia sólida para la gestión y uso de datos. Por ello, el Parlamento Europeo ha promovido la creación de espacios de datos europeos sectoriales, que permitan el intercambio controlado de información bajo marcos legales comunes y directrices estandarizadas.

En 2022 y 2023 se aprobaron dos leyes fundamentales:

- **Ley de Gobernanza de Datos**, para fomentar la disponibilidad de datos para empresas e investigadores.
- **Ley de Datos**, que establece principios de transparencia, seguridad y protección de los derechos fundamentales.

Ambas normativas tienen como objetivo estimular el uso de macrodatos en beneficio de la sociedad y la economía, sin poner en riesgo la privacidad individual. Solo pueden compartirse datos no personales o completamente anonimizados, lo que garantiza que los ciudadanos conserven el control total sobre su información. Especial atención merece el espacio europeo de datos sanitarios, impulsado a raíz de la pandemia de COVID-19, para facilitar el acceso seguro a información médica a gran escala.

Estas estrategias también dependen de infraestructuras tecnológicas robustas, como redes 5G y 6G, sistemas de ciberseguridad avanzados y capacidades de almacenamiento y procesamiento de datos a gran escala.

### Riesgos y protección de derechos en el entorno digital

El uso intensivo de datos por parte de servicios digitales puede generar desequilibrios de poder. A diferencia de los servicios tradicionales, los digitales permiten recopilar información muy detallada sobre el comportamiento y las preferencias de los usuarios. Esto plantea riesgos de manipulación, segmentación excesiva o discriminación, por ejemplo, en el acceso a empleo o servicios sanitarios. La publicidad personalizada extrema, basada en grandes volúmenes de datos, también ha generado preocupación por su potencial para influir de forma desproporcionada en decisiones individuales o colectivas.

### La Ley de Inteligencia Artificial de la UE

Con el fin de abordar estos retos, la Ley de Inteligencia Artificial de la Unión Europea establece un marco legal que regula el uso de esta tecnología en función del nivel de riesgo que presenta (RTVE, 2024). Por tanto, para la Comisión Europea (2019), una IA confiable debe ser legal, ética y robusta, incluso ante situaciones de incertidumbre.

Esta normativa exige que todos los sistemas de IA sean:

- Seguros y transparentes.
- Supervisados por humanos, no completamente automatizados.
- No discriminatorios.
- Ambientalmente sostenibles.

*Figura 3. Fotografía ilustrativa de la normativa en IA en Europa. Fuente: RTVE, 2024. (Imagen omitida.)*

La ley clasifica los sistemas de IA en las siguientes categorías:

- **Riesgo inaceptable:** tecnologías que se consideran peligrosas para los derechos fundamentales. Están prohibidas e incluyen:
  - Manipulación cognitiva de personas vulnerables (ejemplo, juguetes que incitan a comportamientos peligrosos).
  - Sistemas de puntuación social que clasifiquen a las personas según su comportamiento o situación socioeconómica.
  - Reconocimiento facial en tiempo real y a distancia (con algunas excepciones judiciales para la persecución de delitos graves).
- **Alto riesgo:** sistemas que afectan a la seguridad o los derechos fundamentales. Se dividen en:
  - Aquellos integrados en productos regulados (vehículos, juguetes, dispositivos médicos, etc.).
  - Ocho sectores específicos que deben cumplir requisitos estrictos y registrarse en una base de datos europea, incluyendo identificación biométrica, infraestructuras críticas, educación y empleo, servicios esenciales y públicos, aplicación de la ley, gestión de migraciones, asistencia judicial. Estos sistemas deben someterse a evaluaciones antes y durante su uso.
- **IA generativa:** como los modelos que crean textos, imágenes o música (por ejemplo, ChatGPT). Deben cumplir reglas específicas:
  - Informar que el contenido ha sido generado por IA.
  - Evitar la generación de material ilegal.
  - Publicar resúmenes de los datos con derechos de autor utilizados en el entrenamiento.
- **Riesgo limitado:** sistemas con funciones interactivas o creativas que deben informar claramente a los usuarios de que están interactuando con una IA. Esto aplica, por ejemplo, a ultrafalsos (*deepfakes*) y asistentes conversacionales.

> Nota: el texto enumera siete elementos para "ocho sectores específicos" de alto riesgo (biometría, infraestructuras críticas, educación y empleo, servicios esenciales y públicos, aplicación de la ley, gestión de migraciones, asistencia judicial). Se transcribe tal cual.

Para la Agencia Española de Protección de Datos (2020), «El enfoque de protección de datos debe estar integrado en todas las etapas del diseño de sistemas de IA».

### Inteligencia artificial y minería de datos

Un aspecto fundamental del vínculo entre los datos y la inteligencia artificial es la **minería de datos**, una disciplina centrada en descubrir patrones o conocimientos ocultos en grandes volúmenes de información. Este proceso no surge tanto por la aparición de técnicas totalmente nuevas, sino por la necesidad de gestionar y extraer valor de gigantescos almacenes de datos generados en la era digital.

> La minería de datos se apoya en herramientas y algoritmos desarrollados en el campo de la IA para identificar regularidades y relaciones que no son evidentes a simple vista. Su objetivo principal es facilitar la comprensión de los datos y convertirlos en conocimiento útil para la toma de decisiones.

Las etapas del proceso de minería de datos son las siguientes:

- **Definición de objetivos:** el proceso comienza con la identificación clara de las metas que el cliente o usuario espera alcanzar, guiado por el especialista en análisis de datos.
- **Preprocesamiento:** se realiza una preparación exhaustiva de los datos, que incluye su selección, limpieza, enriquecimiento, reducción y transformación. Esta fase garantiza que los datos sean aptos para el análisis posterior.
- **Modelado:** en esta etapa se construyen modelos analíticos a partir de los datos procesados. La inteligencia artificial interviene a través de algoritmos capaces de representar de manera gráfica o matemática los patrones detectados.
- **Evaluación de resultados:** finalmente, los hallazgos se validan para comprobar su coherencia y utilidad, comparándolos con métodos estadísticos tradicionales y técnicas de visualización.

> En la sección A fondo hay un recurso tipo documental sobre los aspectos éticos, legales y de gobernanza relacionados con la IA.

Técnicas comunes de minería de datos:

- **Análisis de cesta de mercado** (*market basket analysis*): permite identificar productos que suelen comprarse juntos y analizar patrones de consumo integrando variables como el lugar, la fecha o el método de pago. Es especialmente útil en comercio físico y digital.
- **Series temporales:** se utilizan para estudiar la evolución de datos a lo largo del tiempo y predecir comportamientos futuros, como ventas, consumo energético o demanda de servicios.
- **Previsión local:** basada en la premisa de que personas con características similares tienden a comportarse de forma parecida. Este enfoque utiliza el contexto de los individuos para generar predicciones más ajustadas.
- **Redes neuronales artificiales:** inspiradas en el funcionamiento del cerebro, estas estructuras pueden aprender patrones complejos mediante la transformación de variables y el aprendizaje progresivo. Son una evolución de modelos estadísticos tradicionales con gran capacidad predictiva.
- **Árboles de decisión:** representan decisiones mediante diagramas lógicos tipo si-entonces, permitiendo clasificar datos y predecir resultados en función de una secuencia de condiciones extraídas de bases de datos.

La minería de datos ha demostrado ser una herramienta poderosa, tanto en entornos empresariales como en la investigación científica, al facilitar el análisis de grandes volúmenes de información y ayudar a encontrar soluciones a problemas complejos.

> La aplicación conjunta de técnicas de IA permite automatizar muchas de estas tareas, optimizar los recursos empleados en el análisis de datos masivos y obtener resultados precisos de manera eficiente. Esto convierte a la minería de datos en un elemento clave para el desarrollo de tecnologías inteligentes y estrategias empresariales basadas en evidencia.

---

## 4.4. La IA en los sectores productivos

La inteligencia artificial está transformando de manera profunda y acelerada los diferentes sectores económicos. Su aplicación representa no solo una fuente de innovación, sino también una oportunidad estratégica de crecimiento y competitividad para empresas e industrias. Con ello, la Fundación COTEC (2025), asegura que la IA no sustituirá empleos por completo, pero transformará profundamente las tareas que realizamos y las habilidades que se requieren.

A medida que la adopción de tecnologías digitales se generaliza, la IA se convierte en un eje clave para la automatización, la optimización y la toma de decisiones basadas en datos.

### Sector manufacturero

La IA está revolucionando la fabricación industrial mediante la automatización de procesos, la implementación de fábricas inteligentes y la mejora continua del rendimiento. Gracias a la combinación de sensores avanzados, conectividad entre máquinas, análisis de datos en tiempo real y algoritmos predictivos, se han logrado importantes avances en eficiencia y control de calidad.

Aplicaciones destacadas:

- **Mantenimiento predictivo:** los sistemas basados en *machine learning* pueden analizar datos de funcionamiento para anticipar fallos y programar intervenciones antes de que ocurran interrupciones graves.
- **Control automático y autónomo:** robots inteligentes toman decisiones operativas sin intervención humana, adaptándose a condiciones cambiantes del entorno de producción.
- **Detección de daños:** dispositivos dotados de IA permiten identificar fallos estructurales y aplicar soluciones predefinidas de manera rápida.
- **Optimización de la cadena de suministro:** la visión artificial permite clasificar productos, detectar errores en el empaquetado y mejorar la logística.
- **Drones autónomos:** se utilizan para tareas de vigilancia, supervisión de infraestructuras o inspecciones de seguridad en plantas industriales.
- **Producción flexible y bajo demanda:** los sistemas gestionan la producción ajustándose en tiempo real a la demanda del mercado, gracias a sensores conectados que transmiten datos a plataformas inteligentes.
- **Diseño generativo:** herramientas de IA pueden simular y analizar virtualmente el comportamiento de productos antes de fabricarlos, reduciendo costes y tiempos de desarrollo.

### Sector sanitario

En el ámbito de la salud, la IA está marcando un antes y un después tanto en el diagnóstico como en la atención médica personalizada. Sus aplicaciones mejoran la precisión, reducen errores humanos y optimizan la gestión de recursos.

Algunas aplicaciones clave:

- **Apoyo en el diagnóstico clínico:** sistemas de IA pueden ofrecer diagnósticos con mayor precisión a partir del análisis de historiales médicos y patrones clínicos. Como por ejemplo la reducción del tiempo de espera del diagnóstico en enfermedades raras (El Español, 2023).

  *Figura 4. Fotografía de un hospital de Madrid usando IA. Fuente: El Español, 2023. (Imagen omitida.)*

- **Cirugía asistida por robots:** mejora la precisión quirúrgica en procedimientos delicados, lo que reduce riesgos y tiempos de recuperación.
- **Análisis de imágenes médicas:** la IA puede identificar anomalías en radiografías, resonancias o ecografías con un alto grado de fiabilidad.
- **Monitorización remota de pacientes:** dispositivos portátiles recopilan datos biométricos y los analizan en tiempo real para detectar cambios significativos en el estado de salud.
- **Gestión hospitalaria:** optimización de recursos humanos, planificación de turnos y distribución de espacios según necesidades dinámicas.

### Sector financiero

La industria financiera ha adoptado la IA para automatizar procesos, gestionar riesgos y ofrecer servicios más personalizados. Desde la banca hasta los seguros, su impacto es significativo:

- **Asesoramiento financiero personalizado:** chatbots y asistentes virtuales ayudan a los clientes a tomar decisiones informadas sobre sus finanzas.
- **Automatización de procesos:** gestión de facturas, conciliación bancaria y otras tareas administrativas se realizan de manera autónoma.
- **Detección de fraudes:** algoritmos de IA analizan patrones inusuales para prevenir fraudes y asegurar transacciones.
- **Evaluación de riesgos y seguros:** la IA permite personalizar productos de seguros basándose en perfiles individuales.
- **Cumplimiento normativo:** sistemas inteligentes que revisan documentación y procesos legales para garantizar que se cumplen las regulaciones vigentes.

### Sector agrícola

La inteligencia artificial también está teniendo un impacto profundo en el sector agroalimentario y transforma la agricultura tradicional en agricultura de precisión. Esta evolución permite una gestión más eficiente de los cultivos, los recursos naturales y la maquinaria agrícola.

Principales aplicaciones:

- **Monitoreo de cultivos y predicción de rendimientos:** a través del análisis de imágenes satelitales y datos climáticos, la IA puede prever el crecimiento de las cosechas y detectar anomalías como plagas o enfermedades.
- **Gestión inteligente del riego:** sistemas automatizados que analizan el nivel de humedad, las condiciones del suelo y el pronóstico meteorológico para optimizar el consumo de agua.
- **Maquinaria autónoma:** tractores, cosechadoras y drones dotados de IA pueden operar sin conductor, con precisión milimétrica en la siembra, fertilización y recolección (Díaz Mohedano, 2024).

  *Figura 5. Innovación y tecnología en la agricultura. Fuente: Díaz Mohedano, 2024. (Imagen omitida.)*

- **Trazabilidad alimentaria:** algoritmos de IA permiten seguir todo el recorrido del producto, desde la semilla hasta el consumidor final, lo que garantiza la seguridad alimentaria.
- **Predicción de precios y demanda:** modelos predictivos ayudan a los agricultores a tomar decisiones estratégicas de producción y comercialización.

### Sector comercial

El comercio, tanto físico como digital, ha adoptado tecnologías de IA para personalizar la experiencia de compra, optimizar el inventario y mejorar la atención al cliente.

Aplicaciones más destacadas:

- **Recomendaciones personalizadas:** plataformas de comercio electrónico utilizan IA para analizar el comportamiento del usuario y ofrecer productos que se ajusten a sus preferencias.
- **Gestión de inventario en tiempo real:** los sistemas inteligentes permiten prever la demanda, evitar rupturas de stock y reducir el exceso de existencias.
- **Análisis de sentimiento:** herramientas de procesamiento de lenguaje natural que interpretan comentarios y reseñas de clientes para mejorar productos y servicios.
- **Automatización de tiendas físicas:** implementación de sistemas como cajas sin personal, reconocimiento facial o control de aforo mediante visión artificial.
- **Optimización del *pricing*:** algoritmos que ajustan los precios dinámicamente según la demanda, competencia o el comportamiento del consumidor.

### Sector de la hostelería y el turismo

La IA también está transformando la industria turística y hotelera al mejorar la experiencia del cliente, optimizar procesos y reducir costes operativos.

Aplicaciones clave:

- **Chatbots y asistentes virtuales:** disponibles 24/7 para responder consultas, gestionar reservas o solucionar incidencias, lo que mejora la atención al cliente.
- **Análisis de reputación online:** la IA puede rastrear y analizar reseñas y valoraciones en plataformas digitales, lo que ayuda a identificar fortalezas y áreas de mejora.
- **Optimización de precios y ocupación:** sistemas que ajustan tarifas en tiempo real teniendo en cuenta la temporada, eventos locales, competencia y tendencias de búsqueda.
- **Domótica inteligente en hoteles:** control automatizado de la iluminación, climatización y servicios personalizados en la habitación según las preferencias del huésped.
- **Predicción de demanda turística:** modelos que ayudan a planificar recursos y personal según la afluencia esperada de visitantes.

### Sector logístico y del transporte

Este sector se beneficia enormemente de la capacidad de la IA para procesar datos en tiempo real, mejorar la eficiencia de las operaciones y reducir costes:

- **Optimización de rutas de reparto:** software basado en IA analiza el tráfico, el clima y otros factores para determinar las rutas más eficientes.
- **Mantenimiento predictivo de vehículos:** análisis continuo de datos para prever fallos mecánicos antes de que ocurran.
- **Automatización de almacenes:** robots y sistemas inteligentes gestionan la entrada, ubicación y salida de productos, mejorando la productividad.
- **Transporte de pasajeros:** aplicaciones como Uber o Cabify utilizan IA para asignar viajes, predecir la demanda y mejorar la seguridad tanto del conductor como del pasajero.

### Industria química y farmacéutica

En este campo, la IA permite optimizar procesos de producción, mejorar la calidad de los productos y fomentar la innovación. Se emplea, por ejemplo, para:

- Modelado y simulación de procesos químicos.
- Control y supervisión en tiempo real.
- Diagnóstico de fallos operativos.
- Desarrollo de fármacos más eficientes, acelerando la etapa de investigación mediante el análisis inteligente de datos científicos.

### Industria de los videojuegos

La IA es fundamental en la creación de experiencias inmersivas. Los personajes no jugables (NPC) pueden responder de forma autónoma a las acciones del jugador, creando una sensación de interacción real. También se aplica en el diseño adaptativo de niveles o en juguetes robóticos que responden al comportamiento del usuario.

---

## 4.5. Referencias bibliográficas

Agencia Española de Protección de Datos (AEPD). (2020). *Guía sobre el uso de la inteligencia artificial.* AEPD.

Comisión Europea. (2019, abril 08). *Ethics guidelines for trustworthy AI.* https://digital-strategy.ec.europa.eu/en/library/ethics-guidelines-trustworthy-ai

Díaz Mohedano, J. D. (2024, junio 13). *La Inteligencia Artificial: una potente herramienta para los desafíos del sector agrícola.* Meteored. https://www.tiempo.com/noticias/actualidad/la-inteligencia-artificial-una-potente-herramienta-para-los-desafios-del-sector-agricola.html

Domingos, P. (2015). *The Master Algorithm.* Basic Books.

El Español. (2023, septiembre 15). *Madrid testa una inteligencia artificial que logra reducir el tiempo de diagnóstico de enfermedades raras.* https://www.elespanol.com/invertia/disruptores/autonomias/madrid/20230915/madrid-testa-inteligencia-artificial-logra-reducir-tiempo-diagnostico-enfermedades-raras/794670547_0.html

Fundación COTEC. (2025). *La IA en los procesos de I+D+I.* https://cotec.es/proyectos-cpt/taller-inteligencia-artificial-en-la-i-d-i/

National Geographic España. (2025, enero 16). *Breve historia visual de la inteligencia artificial.* https://www.nationalgeographic.com.es/ciencia/breve-historia-visual-inteligencia-artificial_14419

RTVE. (2024, agosto 01). *Entra en vigor en la UE la primera ley de inteligencia artificial del mundo: multas, fases de aplicación y otras claves.* https://www.rtve.es/noticias/20240801/entra-vigor-primera-ley-inteligencia-artificial-mundo-multas-fases-claves/16204756.shtml

Russell, S. J. y Norvig, P. (2020). *Artificial intelligence: a modern approach.* Pearson.

> Nota: las URL largas de la extracción estaban partidas por saltos de línea; se han reconstruido uniendo los fragmentos y puede haber algún guion mal restituido. Conviene comprobarlas antes de usarlas.

---

## A fondo

### ¿Quién mandará en la inteligencia artificial?

DW Documental. (2024, marzo 16). *¿Quién mandará en la inteligencia artificial? | DW Documental* [Vídeo]. YouTube. https://www.youtube.com/watch?v=PPMb_rrej5c

Este documental de DW explora las implicaciones éticas y sociales del avance de la inteligencia artificial, cuestionando quién controlará esta tecnología en el futuro. Permite al estudiantado reflexionar sobre los desafíos del uso de IA a gran escala, la privacidad, el poder tecnológico y el impacto social de los sistemas automatizados.

### Una pausa cuestionable en la inteligencia artificial

Oliver, N. (2023, mayo 03). Una pausa cuestionable en la inteligencia artificial. *El País.* https://elpais.com/opinion/2023-05-03/una-pausa-cuestionable-en-la-inteligencia-artificial.html

En este artículo de opinión publicado en El País, la autora reflexiona sobre la propuesta de pausar el desarrollo de sistemas de inteligencia artificial avanzados, analizando sus implicaciones y cuestionando su viabilidad. Es útil para fomentar el pensamiento crítico sobre el progreso tecnológico y los dilemas éticos, además de relacionar el contenido teórico con una visión actual y argumentada de una experta en el campo.

---

## Entrenamientos

### Entrenamiento 1. Clasifica el tipo de IA

**Planteamiento del ejercicio**

Se presentan tres escenarios. El estudiantado debe determinar si se trata de IA débil, fuerte o general (AGI).

Escenarios:

- Un asistente virtual que responde a preguntas sobre el clima.
- Un robot capaz de aprender múltiples tareas cognitivas como lenguaje, visión y razonamiento abstracto.
- Un sistema que controla automáticamente la temperatura de una fábrica con base en condiciones ambientales en tiempo real.

**Desarrollo paso a paso**

- Identificar la finalidad del sistema.
- Valorar si se trata de tareas específicas o generales.
- Determinar si simula capacidades humanas complejas.

**Solución**

1. IA débil.
2. AGI (inteligencia artificial general).
3. IA débil.

### Entrenamiento 2. IA en sectores productivos

**Planteamiento del ejercicio**

Relaciona las siguientes tecnologías de IA con el sector productivo al que más probablemente pertenecen:

- Tecnologías:
  - Diagnóstico médico por imagen.
  - Recomendaciones personalizadas en e-commerce.
  - Optimización de rutas de reparto.
  - Mantenimiento predictivo en maquinaria.
  - Control de calidad con visión artificial.
- Sectores:
  - Comercio.
  - Transporte y logística.
  - Industria manufacturera.
  - Sanidad.
  - Agricultura.

**Desarrollo paso a paso**

Analizar qué actividad resuelve cada tecnología. Asociar con el sector productivo correspondiente.

**Solución**

- Diagnóstico médico por imagen → sanidad.
- Recomendaciones personalizadas en e-commerce → comercio.
- Optimización de rutas de reparto → transporte y logística.
- Mantenimiento predictivo en maquinaria → industria manufacturera.
- Control de calidad con visión artificial → industria manufacturera.

### Entrenamiento 3. ¿Es legal? Análisis de un caso ético

**Planteamiento del ejercicio**

Una empresa usa reconocimiento facial en su oficina para registrar la asistencia del personal. No informa adecuadamente a los empleados ni pide consentimiento explícito. ¿Se está cumpliendo con la normativa de protección de datos (RGPD)?

**Desarrollo paso a paso**

- Identificar si los datos biométricos son considerados datos personales (sí).
- Revisar si hay base legal, consentimiento informado y propósito legítimo.
- Evaluar si se respeta el principio de transparencia y minimización.

**Solución**

No, la empresa no cumple con el RGPD. El uso de reconocimiento facial requiere consentimiento explícito y debe cumplir principios de legalidad, necesidad y proporcionalidad. La falta de información a los empleados vulnera sus derechos.

> Nota: en el ámbito laboral, la AEPD ha considerado que el consentimiento del trabajador difícilmente es libre por el desequilibrio con el empleador, por lo que la base jurídica del control biométrico de asistencia suele ser el punto discutido. La solución del tema se limita a lo indicado arriba.

### Entrenamiento 4. Proceso de minería de datos

**Planteamiento del ejercicio**

Ordena correctamente las siguientes fases del proceso de minería de datos:

- Evaluación de resultados.
- Preprocesamiento de datos.
- Definición de objetivos.
- Modelado.

**Desarrollo paso a paso**

- Recordar el flujo típico de un proyecto de análisis de datos.
- Identificar la lógica temporal de las etapas: de la planificación a la validación.

**Solución**

1. Definición de objetivos.
2. Preprocesamiento de datos.
3. Modelado.
4. Evaluación de resultados.

### Entrenamiento 5. Debate guiado sobre la IA generativa

**Planteamiento del ejercicio**

Redacta un breve argumento (máximo 100 palabras) a favor o en contra del uso de IA generativa (como ChatGPT) en sectores como la educación o los medios de comunicación.

**Desarrollo paso a paso**

- Elegir una postura: a favor o en contra.
- Usar ejemplos concretos: ventajas o riesgos.
- Incluir un componente ético, técnico o social.

**Ejemplo de solución a favor**

«La IA generativa puede enriquecer la educación al ofrecer contenidos adaptados al nivel del estudiante, fomentar la creatividad y agilizar procesos docentes. Si se usa de manera responsable, con supervisión humana, puede ser una herramienta transformadora que reduce desigualdades en el acceso al conocimiento».
