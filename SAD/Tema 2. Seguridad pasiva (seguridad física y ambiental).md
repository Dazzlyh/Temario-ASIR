## Tema

# Seguridad y Alta Disponibilidad

# Tema 2. Seguridad pasiva (seguridad física y ambiental)

# Índice

Esquema Material de estudio

## 2.1 Introducción y objetivos

## 2.2 Principios de la seguridad pasiva

## 2.3 Seguridad física y ambiental

## 2.4. Referencias bibliográficas

A fondo CPD. Las entrañas de Google BBVA instala «pasillos fríos» en sus centros de datos OuterVision power supply calculator Datos biométricos, ¿qué pueden hacer con tu información?

Biometría aplicada

¿Cuáles son los diferentes tipos de tecnologías de SAI?

(Vertiv, 2024)

Entrenamientos Entrenamiento 1: preguntas relacionadas con la seguridad física y ambiental de un centro de datos Entrenamiento 2: evaluación y mejora de la seguridad física y ambiental de un centro de datos Entrenamiento 3: cálculo de un sistema de alimentación ininterrumpida (SAI/UPS) para una instalación Entrenamiento 4: planificación y configuración de racks en un CPD Entrenamiento 5: implementación de un plan de recuperación ante desastres (DRP) en un CPD

# Esquema

![image-2](images/image-2.png)

Seguridad y Alta Disponibilidad 4 Tema . Esquema

# 2.1 Introducción y objetivos

En la era digital, donde la dependencia de la tecnología es omnipresente en las operaciones empresariales, la seguridad cibernética se ha erigido como una preocupación prioritaria para organizaciones de todos los tamaños y sectores. Sin embargo, la visión de la seguridad en este contexto ha evolucionado más allá de la mera protección contra ataques informáticos y *malware.* Se ha vuelto imperativo reconocer que la **seguridad efectiva** de los activos empresariales no puede limitarse exclusivamente al ámbito digital, sino que debe **abarcar un espectro más amplio** que incluya la seguridad pasiva y física.

La seguridad pasiva se refiere a las medidas diseñadas para **mitigar los efectos de** **los incidentes** una vez que ya han ocurrido. Desde cortes de energía hasta condiciones meteorológicas adversas, estas eventualidades pueden afectar significativamente la continuidad operativa y la integridad de los datos de una empresa. Para contrarrestar estas amenazas, se implementan soluciones concretas como los sistemas de alimentación ininterrumpida (SAI) y el control de acceso físico, con lo que se busca minimizar la pérdida de información y el mal funcionamiento del *hardware.*

Por otro lado, la seguridad física emerge como un componente esencial en la protección global de los activos empresariales. Aunque una organización puede contar con sólidas defensas contra ataques cibernéticos y vulnerabilidades digitales, estas son insuficientes sin una estrategia eficaz para **prevenir y manejar** **situaciones físicas** como robos e incendios. La seguridad física implica la implementación de barreras físicas y procedimientos de control para salvaguardar los recursos y la información confidencial de una empresa.

En este complejo panorama de seguridad, los **centros de procesamiento de datos** (CPD) o *data centers* desempeñan un papel crucial. Estas instalaciones, diseñadas específicamente para alojar los equipos informáticos y de comunicaciones, son vitales para las operaciones diarias de una organización. Sin embargo, su funcionamiento óptimo y la protección de los datos que albergan requieren de medidas específicas que garanticen su continuidad operativa y una alta disponibilidad del servicio.

La incorporación de sistemas biométricos y SAI en los CPD representa un paso significativo hacia una seguridad más robusta y una fiabilidad operativa mejorada. Los sistemas biométricos proporcionan métodos de identificación difíciles de falsificar, mientras que los SAI aseguran un suministro constante de energía, incluso en situaciones de cortes eléctricos, con lo cual se protegen los equipos críticos y la integridad de los datos.

En este contexto, este tema explora la importancia vital de **integrar estrategias de** **seguridad pasiva y física** en la protección de activos empresariales, especialmente en entornos digitales vulnerables a una amplia gama de amenazas. Se analizan las medidas específicas requeridas para proteger los CPD, para lo que se destaca su papel central en la continuidad operativa y la seguridad de la información en la era digital.

Los objetivos que se pretenden alcanzar en este tema son:

**▸** Comprender los principios de la seguridad pasiva.

**▸** Identificar las amenazas comunes.

**▸** Tomar conocimiento de medidas paliativas.

**▸** Promocionar la prevención y la planificación.

**▸** Resaltar la importancia de la seguridad física.

**▸** Definir y explicar los CPD.

**▸** Identificar las amenazas ambientales y las medidas preventivas.

**▸** Establecer los requisitos y las necesidades del CPD.

**▸** Describir los sistemas biométricos.

**▸** Explicar los sistemas de alimentación ininterrumpida (SAI).

# 2.2 Principios de la seguridad pasiva

Qué es la seguridad pasiva

La seguridad pasiva se refiere a un conjunto de medidas y acciones diseñadas para minimizar los efectos de los accidentes o incidentes una vez que estos han ocurrido, con el objetivo de **reducir al mínimo las consecuencias negativas** como pérdida de *hardware,* falta de disponibilidad de servicios o pérdida de información crítica. A diferencia de la seguridad activa, que busca prevenir o evitar los incidentes en primer lugar, la seguridad pasiva se centra en mitigar el impacto de dichos incidentes una vez que han ocurrido. A continuación, se presenta una descripción de varias amenazas comunes y las correspondientes medidas de seguridad pasiva que se pueden implementar:

**▸ Suministro eléctrico:** una amenaza frecuente son los cortes de energía, variaciones de tensión y la presencia de ruido en la red eléctrica. Para mitigar estos riesgos, se pueden implementar medidas como sistemas de alimentación ininterrumpida (SAI o UPS, del inglés *uninterruptible power supply),* que proporcionan energía de respaldo durante los cortes eléctricos. Además, el uso de generadores eléctricos autónomos y fuentes de alimentación redundantes asegura la continuidad operativa ante cualquier fluctuación o interrupción del suministro eléctrico principal.

**▸ Robos o sabotajes:** el acceso físico no autorizado a instalaciones, *hardware,* *software* y copias de seguridad puede comprometer seriamente la seguridad de la información y los sistemas. Las medidas paliativas incluyen el control estricto del acceso mediante sistemas de cerraduras, armarios seguros, uso de llaves o sistemas biométricos para autenticación. La vigilancia activa mediante circuitos cerrados de televisión (CCTV) y personal de seguridad también juega un papel crucial en la detección y prevención de intrusiones no autorizadas.

**▸ Condiciones atmosféricas adversas:** las amenazas como incendios, inundaciones, terremotos y otras condiciones climáticas severas pueden causar daños significativos a los sistemas y la infraestructura física. Para mitigar estos riesgos, es esencial elegir ubicaciones seguras que minimicen la exposición a estas amenazas naturales. Además, el establecimiento de centros de respaldo en ubicaciones geográficamente separadas y el equipamiento de los edificios con sistemas de detección y extinción de incendios, así como controles avanzados de temperatura y humedad, ayudan a proteger los activos críticos y a mantener la continuidad operativa.

**▸ Errores humanos o mal uso de sistemas:** a menudo subestimados, los errores humanos y el mal uso de los sistemas pueden causar problemas significativos. La capacitación regular del personal en prácticas de seguridad informática y procedimientos operativos seguros es esencial. Implementar políticas claras y procedimientos documentados ayuda a reducir la probabilidad de errores y minimiza el impacto de las acciones no intencionadas que podrían afectar la estabilidad y la seguridad de los sistemas.

**▸ Fallas de** ***hardware*** **o** ***software:*** estas fallas pueden ocurrir por diversas razones, las cuales incluyen problemas técnicos internos o defectos de fabricación. Para mitigar estos riesgos, es fundamental implementar redundancias tanto en *hardware* como en *software* críticos. Esto implica la duplicación de equipos y datos en múltiples dispositivos para garantizar la disponibilidad continua y la rápida recuperación ante fallos inesperados. Además, el monitoreo continuo de los sistemas permite una detección temprana de problemas potenciales, lo cual permite realizar acciones correctivas antes de que impacten negativamente en las operaciones.

**▸ Desastres naturales:** eventos como terremotos, tormentas severas o inundaciones pueden ser catastróficos para las operaciones empresariales si no se toman las precauciones adecuadas. Planificar y prepararse para la respuesta a desastres naturales es crucial. Esto incluye tener un plan de recuperación ante desastres detallado que cubra la recuperación de datos y sistemas esenciales, así como la ubicación de las copias de seguridad fuera del sitio para asegurar la protección de la información crítica en caso de que la ubicación principal sea comprometida.

Estas medidas paliativas forman parte de la seguridad pasiva y están destinadas a minimizar el impacto de los incidentes una vez que han ocurrido, con lo que se asegura la protección continua de los activos y la capacidad operativa de las organizaciones frente a diversas amenazas.

Las **consecuencias** producidas por las distintas amenazas previstas son:

**▸** Pérdida y/o mal funcionamiento del *hardware.*

**▸** Falta de disponibilidad de servicios.

**▸** Pérdida de información.

La pérdida de información es el aspecto fundamental por lo que la medida transversal y siempre recomendada es la realización de **copias de seguridad** que, ante una situación de desastre, permita recuperar los datos. Esta medida la trataremos en un tema posterior.

# 2.3 Seguridad física y ambiental

Qué es la seguridad física y ambiental

Ambos aspectos son fundamentales para **garantizar un entorno seguro y** **protegido** tanto para las personas que lo habitan como para los recursos físicos que se encuentran dentro de ese entorno. La implementación de medidas efectivas de seguridad física y ambiental ayuda a minimizar riesgos, proteger activos y promover un ambiente de trabajo o vida más seguro y sostenible.

**▸ Seguridad física:** se centra en la protección contra amenazas físicas directas, como intrusos, robos, vandalismo, o cualquier otro tipo de acción que pueda poner en riesgo la integridad física de las personas o la infraestructura. Involucra medidas como el control de accesos, sistemas de vigilancia (CCTV), seguridad perimetral, alarmas de intrusión, entre otras.

**▸ Seguridad ambiental:** se refiere a la protección del entorno físico en el que se desenvuelven las personas, lo que asegura condiciones seguras y saludables en términos ambientales. Esto incluye la prevención de accidentes relacionados con productos químicos, el manejo adecuado de los residuos, el control de la contaminación del aire y del agua, la gestión de riesgos naturales (como incendios o inundaciones) y el cumplimiento de las normativas ambientales.

Abordar la seguridad física y ambiental en diferentes entornos, desde hogares y pequeñas oficinas hasta servidores y centros de procesamiento de datos (CPD), implica implementar medidas específicas adaptadas a las necesidades y características de cada uno. Aquí te dejo un desglose de las medidas aplicables a cada entorno:

#### Hogares y pequeñas oficinas

Medidas para implementar más recomendadas:

**▸ Seguridad física:**

- Control de acceso: uso de cerraduras de alta seguridad en puertas y ventanas, sistemas de alarma y videovigilancia (CCTV).

- Dispositivos de seguridad: sensores de movimiento, alarmas contra intrusión y timbres inteligentes con cámaras.

- Protección de equipos: anclaje seguro de equipos como computadoras y servidores a muebles o paredes para evitar robos.

- Mantenimiento regular: realización de mantenimientos preventivos y correctivos en todos los sistemas de seguridad física para asegurar su correcto funcionamiento.

**▸ Seguridad ambiental:**

- Protección contra incendios: instalación de detectores de humo y sistemas de extinción de incendios, como extintores y rociadores automáticos.

- Gestión de residuos: correcta disposición de los residuos electrónicos y químicos para evitar riesgos ambientales.

- Control de temperatura y humedad: uso de aire acondicionado o deshumidificadores para mantener condiciones óptimas para los equipos electrónicos.

- Mantenimiento regular: realización de mantenimientos preventivos y correctivos en todos los sistemas de seguridad física para asegurar su correcto funcionamiento.

Centros de proceso de datos (CPD)

#### ¿Qué son?

Los CPD, también llamados *data center,* son instalaciones especializadas diseñadas p a r a **albergar sistemas de información** y **equipos relacionados,** tales como servidores, almacenamiento, redes y

otros componentes necesarios para el

procesamiento y la gestión de datos. Estos centros son esenciales para la operación de empresas y organizaciones, ya que permiten el procesamiento y almacenamiento seguro de grandes cantidades de información.

![Figura 1. CPD. Fuente: García, 2019.](images/image-3.png)

*Figura 1. CPD. Fuente: García, 2019.*

El CPD se encuentra en un edificio diseñado para soportar las cargas y los requisitos específicos de los equipos de TI. Pueden variar en tamaño, desde una sala pequeña hasta edificios enteros, dependiendo de las necesidades de la organización. Estas instalaciones están diseñadas para **garantizar la seguridad, eficiencia y** **disponibilidad continua** de los servicios tecnológicos.

Los CPD son el corazón tecnológico de muchas grandes organizaciones, ya que proporcionan la infraestructura necesaria para soportar sus operaciones diarias y asegurar el acceso fiable y seguro a la información crítica.

Cuando hablamos de un centro de respaldo,

también conocido como **sitio de**

**recuperación ante desastres** o sitio de contingencia, tenemos que pensar en una instalación diseñada para tomar el control y continuar las operaciones críticas de una organización en caso de que su centro de datos principal sufra una interrupción significativa. Estas interrupciones pueden ser causadas por desastres naturales, fallos técnicos, ataques cibernéticos, u otros eventos imprevistos.

El centro de respaldo deberá estar situado a una **distancia considerable** del centro de datos principal para evitar que ambos sitios sean afectados por el mismo desastre, además de estar ubicado en un lugar accesible para el personal clave y tener buenas conexiones de red. Deberá presentar las **mismas medidas de** **seguridad físicas y lógicas** que el principal y en muchos casos, será una réplica exacta del centro principal, para que pueda existir una replicación en tiempo real en caso de que suceda un desastre en el principal.

Para garantizar la integridad, la disponibilidad y la seguridad de los equipos y datos en un CPD, es fundamental implementar diversas medidas de seguridad física y ambiental. Aquí se detallan algunas de las más importantes:

#### Medidas de seguridad física

**▸ Control de acceso:**

- Tarjetas de acceso: uso de tarjetas de identificación con control de acceso para autorizar la entrada al CPD.

- Biometría: sistemas de autenticación biométrica (huellas dactilares, reconocimiento facial, etc.) para asegurar que solo el personal autorizado pueda acceder.

- Guardias de seguridad: personal de seguridad presente en el lugar para monitorear y controlar el acceso.

**▸ Vigilancia y monitoreo:**

- Cámaras de vigilancia: instalación de cámaras de seguridad (CCTV) en puntos estratégicos dentro y alrededor del CPD para monitorear actividades y detectar intrusiones.

- Sistemas de alarma: alarmas de seguridad para detectar y alertar sobre accesos no autorizados o actividades sospechosas.

**▸ Perímetro de seguridad:**

- Vallas y barreras: implementación de barreras físicas como vallas y puertas reforzadas para proteger el perímetro del CPD.

- Sensores de movimiento: instalación de sensores de movimiento para detectar intrusos en el perímetro del CPD.

**▸ Sistemas de identificación:**

- Registro de visitantes: mantenimiento de un registro detallado de todas las personas que ingresan y salen del CPD.

- Uniformes y credenciales: uso de uniformes y credenciales visibles para el personal autorizado.

#### Medidas de seguridad ambiental

**▸ Control de climatización:**

- Sistemas HVAC: implementación de sistemas de calefacción, ventilación y aire acondicionado (HVAC) para mantener una temperatura y humedad óptimas.

- Monitoreo ambiental: sensores para monitorear la temperatura y la humedad en tiempo real y ajustar los sistemas HVAC según sea necesario.

**▸ Protección contra incendios:**

- Sistemas de detección de humo y calor: instalación de detectores de humo y calor para identificar incendios en etapas tempranas.

- Sistemas de extinción de incendios: sistemas de rociadores automáticos y agentes extintores gaseosos (como FM200 o CO2) que no dañan los equipos electrónicos.

- Extintores portátiles: ubicación de extintores portátiles en puntos clave dentro del CPD.

**▸ Protección contra inundaciones:**

- Drenaje adecuado: sistemas de drenaje eficientes para prevenir la acumulación de agua en caso de inundaciones.

- Suelos elevados: instalación de suelos elevados para proteger los equipos en caso de filtraciones de agua.

**▸ Sistemas de alimentación eléctrica:**

- Uninterruptible power supply (UPS): fuentes de alimentación ininterrumpida para proteger contra cortes de energía.

- Generadores de respaldo: generadores eléctricos para proporcionar energía en caso de fallos prolongados en el suministro eléctrico.

- Redundancia de circuitos: implementación de circuitos eléctricos redundantes para garantizar la continuidad de la energía.

**▸ Monitoreo y gestión:**

- Sistema de gestión de infraestructura del centro de datos (DCIM): herramientas para la supervisión y gestión integral de la infraestructura del CPD.

- Alertas y notificaciones: sistemas de alertas automáticas para notificar al personal sobre cualquier anomalía o fallo en los sistemas ambientales.

Estas medidas de seguridad física y ambiental son cruciales para proteger los recursos y la información en un CPD, lo que asegura su operación continua y fiable en todo momento.

Sistemas biométricos

La seguridad física y la protección de la información son componentes cruciales para cualquier empresa que desee salvaguardar sus activos y datos confidenciales. Los avances en tecnología han facilitado la implementación de sistemas sofisticados para el control de acceso y la identificación del personal. A continuación, se detalla cómo se puede llevar a cabo un sistema eficaz de control de acceso físico utilizando diversos métodos de identificación.

#### Métodos de identificación del personal

**Algo que se posee.** Es uno de los métodos más comunes para la identificación del personal. Este método incluye:

**▸ Llaves:** tradicionalmente, las llaves han sido utilizadas para permitir la entrada a diferentes áreas dentro de una empresa. Aunque son simples y efectivas, su principal desventaja es que pueden ser fácilmente duplicadas o robadas, lo que representa un riesgo significativo para la seguridad.

**▸ Tarjetas de identificación o** ***SmartCard:*** las tarjetas de identificación, especialmente las tarjetas inteligentes *(SmartCard),* ofrecen una solución más segura. Estas tarjetas pueden contener chips electrónicos que almacenan la

Seguridad y Alta Disponibilidad 18 Tema . Material de estudio información del usuario, lo que permite un control de acceso más preciso. En caso de pérdida, las tarjetas pueden ser desactivadas rápidamente para prevenir accesos no autorizados.

**Algo que se sabe.** Es otro método de identificación, por ejemplo:

**▸ Número de identificación personal (PIN):** un PIN es un código numérico que los empleados deben ingresar para obtener acceso. Este método es efectivo, pero requiere que los PIN sean lo suficientemente complejos y cambiados periódicamente para evitar su deducción por parte de terceros.

**▸ Contraseñas:** similar a los PIN, las contraseñas pueden incluir una combinación de letras, números y caracteres especiales, lo que las hace más seguras. Es importante que las contraseñas se gestionen de manera adecuada, con cambios periódicos y sin compartirlas entre usuarios.

**Algo que se es.** El método más avanzado y seguro para la identificación del personal se basa en las características biométricas.

La **biometría** se define como el estudio cuantitativo de las características biológicas y de comportamiento de los seres vivos utilizando métodos estadísticos. En el contexto de la seguridad y la tecnología, la biometría se refiere a la utilización de estas características únicas para la identificación y verificación de individuos.

La identificación se realiza comparando las características físicas de una persona con un patrón registrado en una base de datos. Este enfoque no solo facilita el control de acceso físico, sino que también puede ser utilizado para la autenticación en sistemas operativos y aplicaciones. Dado que las características biométricas de cada individuo son únicas e intransferibles, estos sistemas ofrecen un **alto nivel de** **seguridad.**

Los sistemas biométricos son tecnologías que utilizan características físicas o comportamentales únicas de las personas para identificarlas o verificar su identidad.

Estos sistemas son cada vez más comunes en una variedad de aplicaciones debido a su capacidad para proporcionar una autenticación segura y conveniente.

Alguna de las formas de identificación biométricas más comunes:

**▸ Huellas dactilares:** este sistema utiliza las crestas y valles únicos de las yemas de los dedos. Los escáneres de huellas dactilares capturan una imagen de la huella, que luego se compara con una base de datos de huellas almacenadas. Las huellas dactilares son únicas para cada individuo y no cambian con el tiempo. Es fácil y rápido de usar. Los usuarios simplemente colocan su dedo en el escáner. Funciona bien en una variedad de condiciones ambientales. Todo ello hace que el método sea uno de los más empleados por su baja relación calidad/precio (por ejemplo, es ampliamente utilizado en teléfonos inteligentes, sistemas de control de acceso y otros dispositivos electrónicos).

**▸ Reconocimiento facial:** este sistema analiza características faciales como la distancia entre los ojos, la forma de la nariz y la estructura ósea para identificar a una persona. Su fiabilidad puede verse afectada por cambios en la iluminación, el ángulo y la expresión facial, por lo que puede fallar en condiciones de poca luz o cuando la persona lleva gafas o sombreros. Así todo, es uno de los métodos más usados ya que es rápido y no requiere contacto. Es usado sobre todo en *smartphones,* sistemas de vigilancia y control de acceso.

**▸ Verificación de voz:** identifica a una persona según sus características vocales, como el tono, la cadencia y la acentuación. Su fiabilidad puede verse afectada por el ruido de fondo, enfermedades o cambios en la voz (debemos tener presente que la voz puede variar debido a factores temporales). A pesar de todo, es cómodo y fácil de usar por lo que es un mecanismo muy adoptado en servicios telefónicos y asistentes virtuales (tipo Alexa…).

**▸ Reconocimiento del iris:** examina los patrones únicos en el iris del ojo, los cuales son altamente distintivos y no cambian con el tiempo. Es extremadamente precisa Funciona bien en diversas condiciones y es difícil de falsificar. Presenta una

Seguridad y Alta Disponibilidad 20 Tema . Material de estudio usabilidad media, entre otros motivos, porque requiere que el usuario mire directamente a una cámara a corta distancia y no es del todo agradable. Es utilizado principalmente en aplicaciones de alta seguridad y control de fronteras.

**▸ Reconocimiento de palma:** analiza las líneas y características de la palma de la mano. Las palmas tienen patrones únicos que son difíciles de falsificar y, además, funciona bien en diversas condiciones. Requiere que el usuario coloque su mano en un escáner. Así todo tiene una aceptación media-baja en el mercado, es utilizado preferentemente en algunas aplicaciones de control de acceso.

**▸ Reconocimiento de firma:** evalúa la forma en la que una persona firma su nombre, incluyendo la velocidad, la presión y el estilo. Requiere una superficie adecuada para firmar y la firma de una persona puede variar con el tiempo o incluso, puede ser falsificada por expertos. Por todo ello, su aceptación es baja, es usado en algunos sistemas de autenticación de documentos y transacciones.

Lo que sigue a continuación es una tabla en la que se recogen las diferentes características de los sistemas biométricos:

![image-4](images/image-4.png)

Tabla 1. Sistemas biométricos. Fuente: elaboración propia.

Sistemas de alimentación ininterrumpida

#### ¿Qué son?

Un sistema de alimentación ininterrumpida (SAI), conocido en inglés como *uninterruptible power supply* (UPS), es un dispositivo diseñado para **proporcionar** **energía eléctrica de manera continua** a los equipos conectados a él, incluso en caso de fallos o interrupciones en el suministro eléctrico. Los SAI están equipados con baterías que permiten mantener operativos los dispositivos durante un tiempo limitado después de un corte de electricidad, lo que permite apagar los equipos de manera segura y sin pérdida de datos o daños a los componentes.

![Figura 2. SAI. Fuente: Perez, 2021.](images/image-5.png)

*Figura 2. SAI. Fuente: Perez, 2021.*

#### Funcionamiento

Los dispositivos no se conectan directamente a la red eléctrica, sino que se enchufan al SAI, el cual actúa como intermediario al conectarse a su vez a la red eléctrica. Esta configuración le permite al SAI regular y mejorar la calidad de la energía que llega a los dispositivos conectados.

#### Modelos y capacidades

Existen diversos modelos de SAI que se adaptan a las diferentes necesidades energéticas de los equipos conectados. Estos pueden variar en:

**▸ Capacidad de carga:** determinada por la cantidad de energía que pueden suministrar.

**▸ Autonomía:** tiempo que pueden mantener los equipos funcionando durante un corte de energía.

**▸ Características adicionales:** funciones como regulación de voltaje, filtrado de armónicos y protección contra sobretensiones.

#### Funciones adicionales

Además de proporcionar energía durante cortes de suministro, los SAIs también mejoran la calidad de la energía eléctrica. Esto incluye:

**▸** Filtrado de subidas y bajadas de tensión: Protegiendo los equipos de picos o caídas de tensión.

**▸** Eliminación de armónicos: Mejorando la calidad de la energía y reduciendo las interferencias que pueden dañar los equipos.

A continuación, se muestra una tabla que resume las **características esenciales** de los SAI y proporciona una descripción clara de cada una de ellas para entender mejor su funcionamiento y ventajas.

![image-6](images/image-6.png)

![image-7](images/image-7.png)

Tabla 2. Características de un SAI. Fuente: elaboración propia.

#### Tipos de SAI

Existen varios tipos de SAI, cada uno diseñado para diferentes necesidades y niveles de protección eléctrica. A continuación, te explico los principales tipos:

**▸ SAI** ***offline (standby):*** el equipo está conectado directamente a la corriente eléctrica de la red. El SAI solo entra en acción cuando detecta una interrupción en el suministro eléctrico. Es ideal para equipos de consumo básico como computadoras personales y periféricos, al ser el tipo más económico.

**▸ SAI** ***line-interactive:*** el equipo monitoriza continuamente la calidad de la energía eléctrica. Ajusta automáticamente el voltaje para mantenerlo dentro de un rango seguro sin necesidad de cambiar a la batería. Es adecuado para entornos con fluctuaciones de voltaje frecuentes, como oficinas y pequeños servidores.

**▸ SAI** ***online*** **(doble conversión):** la carga siempre se alimenta a través del inversor, lo que proporciona una energía constante y limpia independientemente de las fluctuaciones de la red. Es crítico para aplicaciones sensibles que requieren una calidad de energía ininterrumpida y muy alta, como centros de datos, servidores importantes y equipos médicos.

Cada tipo de SAI ofrece niveles diferentes de protección y gestión de la energía eléctrica, con lo que se adaptan a las necesidades específicas de los equipos y las aplicaciones que se desean proteger.

#### Potencia necesaria

Para adecuar las dimensiones y la capacidad eléctrica de la batería del SAI según los requisitos de nuestros equipos, es esencial calcular la potencia que consumen y, en consecuencia, la que debe ser suministrada por el SAI a través de sus salidas de batería. Este proceso nos permite garantizar que el SAI puede mantener operativos los dispositivos conectados durante el tiempo necesario en caso de un corte de suministro eléctrico, con lo que se asegura la continuidad operativa sin interrupciones

Seguridad y Alta Disponibilidad 25 Tema . Material de estudio perjudiciales.

Los SAI deben proporcionar toda la energía necesaria, es decir, la potencia aparente de la instalación. Vamos a ver a continuación los pasos que debemos seguir para calcular qué SAI es el más adecuado para nuestra instalación, para optimizar los costes.

#### Pasos

**▸** 1. Obtener los consumos de todos los equipos a los que les va a dar soporte el SAI en vatios.

**▸** 2. Sumar todos los vatios.

**▸** 3. Dividir el consumo en vatios entre el factor de potencia del SAI (0,5-0,7 dependiendo de la calidad del SAI).

**▸** 4. Se obtiene la potencia necesaria del SAI en voltamperios (VA).

**▸** 5. Es el valor **mínimo,** por tanto, habrá que buscar un SAI con más VA que ese valor para cubrir nuestras necesidades.

La potencia eléctrica se puede definir como la cantidad de energía eléctrica que se consume en una determinada unidad de tiempo.

En los circuitos eléctricos de corriente alterna (CA), como los que se encuentran en las tomas de corriente estándar, si nos referimos a potencia eléctrica, podemos estar hablando de la potencia aparente (VA), que es la potencia efectiva o consumida por el sistema, así como de la potencia real en vatios (W). Los dispositivos eléctricos presentan en sus hojas de características la potencia real en vatios (W). Los SAI comercializan su capacidad en voltiamperios (VA), que es la potencia aparente. Para convertir la potencia de vatios (W) a voltiamperios (VA) se multiplica aproximadamente por 1,4. Esto tiene en cuenta el pico máximo de potencia que puede requerir su equipo, con lo que se asegura una capacidad adecuada del SAI para manejar cargas variables.

Este factor es crucial al seleccionar un SAI para asegurarse de que pueda proporcionar suficiente energía, no solo para la carga nominal, sino también para los picos de potencia que puedan ocurrir durante el funcionamiento de los equipos conectados.

Por ejemplo:

Supongamos que tenemos una instalación que necesita una potencia de

400 W.

Si utilizamos un factor de potencia del SAI de 0,6, nos da que:

$$Psai = 400/0,6 = 666,66 VA.$$

Esa sería la potencia efectiva que debería tener el SAI para poder cubrir el

consumo exigido. En este caso, no existen SAI de esta potencia, por lo que elegiremos uno de los que nos ofrece el mercado que tenga más VA que lo calculado (p. ej., 7000 VA).

Se recomienda que la carga total conectada a la batería del SAI no exceda el 70 % de la potencia total suministrada. Este margen asegura que el SAI pueda manejar picos de demanda de manera efectiva y prolongue la vida útil de las baterías al operar dentro de un rango óptimo de carga.

#### Autonomía del SAI

Conociendo la potencia, hay que saber también durante cuánto tiempo nos va a poder proporcionar energía el SAI. Para ello se aplica la fórmula:

![image-8](images/image-8.png)

![image-9](images/image-9.png)

![image-10](images/image-10.png)

![image-11](images/image-11.png)

![image-12](images/image-12.png)

**▸** T: tiempo de autonomía total que tendrá el SAI.

**▸** N: número de baterías del SAI, normalmente el fabricante indica este parámetro. **▸** V: tensión que ofrecen las baterías.

**▸** Ah: capacidad de las baterías en amperios-hora (Ah).

**▸**

**▸** Ef: eficiencia de las baterías. Generalmente, es tomada como el 95 % para el cálculo de la autonomía.

**▸** S: potencia aparente del SAI.

**▸** 60: representa una hora en minutos para convertir el resultado en una unidad

manejable.

Esta ecuación permite determinar cuánto tiempo el SAI podrá **mantener la** **alimentación de los dispositivos** conectados durante un corte de energía eléctrica, considerando la capacidad de las baterías y la eficiencia de conversión de energía.

Ejemplo:

Supongamos que tenemos un SAI de 800 VA, con dos baterías, una

tensión de batería de 9 V y 6 Ah. Supongamos además una eficiencia del 95 %. Si metemos los datos en la fórmula, obtenemos:

=

![image-13](images/image-13.png)

![image-14](images/image-14.png)

![image-15](images/image-15.png)

![image-16](images/image-16.png)

![image-17](images/image-17.png)

Esto da como resultado un tiempo T= 7,69 minutos de autonomía.

Racks

#### ¿Qué son?

Un rack es un **soporte metálico** que se

destina al alojamiento del **equipo**

**electrónico, informático y de comunicaciones.** Las medidas para la anchura están normalizadas para que sean compatibles

con el equipamiento de distintos

fabricantes. También son llamados bastidores, cabinas, gabinetes o armarios.

![Figura 3. Rack. Fuente: adaptado de PNG All, (s. f.), y PNG Arts, (s. f.).](images/image-18.png)

*Figura 3. Rack. Fuente: adaptado de PNG All, (s. f.), y PNG Arts, (s. f.).*

#### Características de un rack

Los racks para montaje de servidores y

equipos de red son estructuras

estandarizadas esenciales en los centros de datos y otras instalaciones de TI. Aquí tienes un resumen de las especificaciones más comunes:

**▸ Anchura estándar:** los racks tienen una anchura estándar de 600 mm, que coincide con el tamaño estándar de las losetas en los centros de datos, lo que facilita la distribución del espacio.

**▸ Profundidades disponibles:** los racks pueden tener fondos de 600, 800, 900, 1000, y hasta 1200 mm. Esto proporciona flexibilidad para alojar diferentes tipos de equipos y facilitar el manejo del cableado.

**▸ Altura y unidades rack (U):**

- La altura de los racks se mide en unidades rack (U), donde 1 U es igual a 44,45 mm (1¾ pulgadas) de altura.

- Los racks pueden tener desde 4 U hasta 46/47 U de altura estándar, lo que permite ajustarse a diversas necesidades de espacio y capacidad.

**▸ Dimensiones verticales:**

- Verticalmente, los racks están divididos en unidades rack (U) de 44,45 mm de altura cada una.

- Las unidades rack están separadas verticalmente por 450,85 mm (17¾ pulgadas), lo que proporciona un total de 482,6 mm (19 pulgadas) de altura.

**▸ Alturas estándar disponibles:** los racks pueden tener alturas normalizadas de 800, 1000, 1200, 1400, 1600, 1800, 2000 y 2200 mm, según la normativa.

**▸ Flexibilidad de profundidad:** aunque la profundidad del bastidor no está completamente normalizada, es común encontrar opciones de 600, 800, 900, 1000 e incluso 1200 mm. Esto permite adaptar los racks al equipamiento específico y a las necesidades de espacio de cada instalación.

**▸ Estructura y configuración:**

- Estructura modular con paneles laterales, marco frontal y posterior, y posiblemente paneles de techo y base.

- Puertas frontales de cristal o metálicas y puertas traseras opcionales para acceso y gestión del cableado.

- Posibilidad de quitar los paneles laterales y unir con otros racks de medidas similares para crear una estructura de racks.

**▸ Ventilación y gestión térmica:**

- Opciones para ventilación pasiva y activa, como ventiladores integrados o paneles perforados.

- Espacio para la gestión de cables con pasacables y canales verticales.

**▸ Compatibilidad y estándares:**

- Cumplimiento con el estándar de montaje de 19 pulgadas (para equipos estándar).

- Cumplimiento con estándares de seguridad y capacidad de carga, como EIA-310-D.

**▸ Opciones de montaje:**

- Montaje de equipos estándar de TI y telecomunicaciones, como servidores, switches y otros dispositivos de red.

- Opciones para montaje en pared o en piso con kits de montaje adecuados.

**▸ Accesorios y personalización:**

- Estantes ajustables, bandejas deslizables y cajones para almacenamiento de equipos y herramientas.

- Kits de gestión de cableado, organizadores de cables verticales y horizontales.

Estas especificaciones están diseñadas para asegurar la compatibilidad entre diferentes fabricantes y facilitar la gestión del espacio y del cableado en entornos de centros de datos y otras instalaciones de TI.

# 2.4. Referencias bibliográficas

García, D. (2019). *Inteligencia artificial aumenta la eficiencia de data centers* [ i m a g e n ] . <https://www.inteldig.com/2019/09/inteligencia-artificial-aumenta-laeficiencia-de-data-centers/>

Perez, S. C. (2021). *Sentinel Tower, el SAI más destacado del mercado* [imagen]. [https://fanaticosdelhardware.com/sentinel-tower-el-sai-mas-destacado-del-mercado/](https://fanaticosdelhardware.com/sentinel-tower-el-sai-mas-destacado-del-mercado/)

PNG All. (s. f.). *Server rack PNG file* [imagen]. <https://www.pngall.com/rackpng/download/48933>

PNG Arts. (s. f.). *Rack PNG Background Image* [imagen]. [https://www.pngarts.com/explore/17236](https://www.pngarts.com/explore/17236)

# estilo/tecnologia/2012/10/18/entranas-google-6742335.html

# CPD. Las entrañas de Google

Información. (2012). *Las entrañas de Google.* <https://www.informacion.es/vida-y-> Por curiosidad, ¿sabes cómo gestiona sus servidores una empresa tan puntera como Google? Accede a este artículo y veras cómo está diseñado uno de los CPD más punteros del mundo…

# mejorar la eficiencia energética (30 de Enero de 2023). BBVA.

# datos-para-mejorar-la-eficiencia-energetica/

# BBVA instala «pasillos fríos» en sus centros de

# datos

Baeza, C. (2023, enero 30). BBVA instala 'pasillos fríos' en sus centros de datos para <https://www.bbva.com/es/sostenibilidad/bbva-instala-pasillos-frios-en-sus-centros-de-> Esta es una noticia interesante en la que podrás ver lo importante que es implantar medidas de seguridad física adecuadas. Si no lo haces así, tu sistema puede verse afectado y sufrir las consecuencias.

Centro de proceso de datos-CPD

Unitel SLU. (s. f.). *Centro de Proceso de Datos-CPD.* <https://unitel-tc.com/centro-deproceso-de-datos-cpd/>

Este sitio web te mostrará soluciones y noticias actualizadas sobre la implementación de un CPD. Desde cuáles son los elementos más comunes, como mantener tu CPD limpio y ordenado, hasta cómo realizar una auditoria en tu CPD. Todo lo que deberías saber de un CPD.

# Extreme Outer Vision. (s. f.). OuterVision Power Supply Calculator.

# [https://outervision.com/power-supply-calculator](https://outervision.com/power-supply-calculator)

# OuterVision power supply calculator

Utiliza esta calculadora online para elegir el SAI adecuado en cada situación. Esta es una forma aproximada y rápida para realizar los cálculos, aunque no debes olvidar cómo hacer el cálculo de forma manual.

Datos biométricos, ¿qué pueden hacer con tu información?

DEF. (2023, noviembre 24). *Datos biométricos, ¿qué pueden hacer con tu* *información?* [vídeo]. YouTube.

![image-19](images/image-19.png)

Accede al vídeo: [https://www.youtube.com/embed/ff9d3KEuMho](https://www.youtube.com/embed/ff9d3KEuMho)

Ya no es suficiente con una contraseña o con preguntas de seguridad. Los métodos seguros están cambiando. Esta es una noticia de actualidad sobre lo importante que es custodiar tus datos biométricos y las consecuencias que tiene cederlos a un tercero.

Vender el iris por 25 criptomonedas

# Vender el iris por 25 criptomonedas. (2024, marzo 13). Cambio 16.

[https://www.cambio16.com/vender-el-iris-por-25-criptomonedas/](https://www.cambio16.com/vender-el-iris-por-25-criptomonedas/)

¿Estás pensado en vender tu iris? ¿Has oído la noticia sobre la gente que vende su iris y que consigue un beneficio económico? Antes de hacerlo, deberías leer este artículo y conocer las consecuencias.

# Biometría aplicada

Página web de Biometría Aplicada: [https://biometriaaplicada.com/](https://biometriaaplicada.com/)

Es una empresa puntera en aplicaciones biométricas con más de veintitrés años de experiencia. Esta página te mostrará casos reales y soluciones ideales para cada caso. Puedes contactar con ellos para que te faciliten un presupuesto ajustado a tus necesidades.

# articles/what-are-the-different-types-of-ups-

# %20de%20energ%C3%ADa.

# ¿Cuáles son los diferentes tipos de tecnologías de

# SAI? (Vertiv, 2024)

Vertiv. (s. f.). *¿Cuáles son los diferentes tipos de tecnologías de SAI?* <https://www.vertiv.com/es-emea/about/news-and-insights/articles/educational->

$$systems/#:~:text=Los%20tres%20principales%20tipos%20de,gestiona%20el%20flujo$$

¿No te quedó clara la explicación que te hemos dado sobre los SAI? Accede a este contenido donde, además, podrás conocer las últimas novedades que te ofrece el mercado.

# Entrenamiento 1: preguntas relacionadas con la seguridad física y ambiental de un centro de datos

#### ▸ Planteamiento del ejercicio

Deberás responder a una batería de preguntas relacionadas con la seguridad física y ambiental en un centro de procesamiento de datos (CPD):

**▸** ¿Cuáles son los principales riesgos de seguridad física a los que está expuesto un CPD y cómo se pueden mitigar?

**▸** ¿Qué medidas se deben tomar para proteger un CPD contra intrusiones físicas, como el acceso no autorizado o el robo de *hardware?*

**▸** ¿Cuál es la importancia de la ubicación física de un CPD en términos de seguridad? ¿Qué factores se deben considerar al seleccionar una ubicación para un CPD?

**▸** ¿Qué protocolos y procedimientos se deben seguir para garantizar la seguridad del acceso físico al CPD, como la autenticación de personal autorizado y la supervisión de los visitantes?

**▸** ¿Cómo se puede garantizar la seguridad contra incendios en un CPD? ¿Qué sistemas de detección y extinción de incendios son los más adecuados?

**▸** ¿Cuáles son las consideraciones clave para garantizar la seguridad eléctrica en un CPD, incluidos los SAI y la distribución de energía?

**▸** ¿Por qué es importante controlar la temperatura y la humedad en un CPD? ¿Qué efectos pueden tener las condiciones ambientales inadecuadas en el rendimiento y la fiabilidad de los sistemas

**▸** ¿Qué medidas se pueden implementar para proteger un CPD contra desastres naturales, como terremotos, inundaciones o tormentas?

**▸** ¿Cuál es el papel de la seguridad física en la certificación de estándares de calidad, como ISO 27001, en un entorno de CPD?

**▸** ¿Cómo se pueden integrar las políticas de seguridad física y ambiental en un enfoque más amplio de seguridad de la información y la gestión de riesgos en un CPD?

**▸ Desarrollo paso a paso:**

Haz una búsqueda exhaustiva y completa el documento con una bibliografía correcta.

**▸ Solución:**

- ¿Cuáles son los principales riesgos de seguridad física a los que está expuesto un CPD y cómo se pueden mitigar? Los CPD están expuestos a una variedad de riesgos físicos y ambientales que pueden comprometer la integridad y la disponibilidad de los datos. Estos incluyen el acceso no autorizado, robos, incendios, inundaciones, fallas eléctricas y desastres naturales. Para mitigar estos riesgos, es esencial implementar un enfoque integral de seguridad que incluya medidas como: sistemas de control de acceso biométricos y de tarjetas de proximidad, videovigilancia, sistemas de alarma contra incendios y detección de intrusos, controles de temperatura y humedad, respaldo de energía con SAI y generadores de emergencia, así como políticas y procedimientos de seguridad bien definidos y planes de continuidad del negocio.

- ¿Qué medidas se deben tomar para proteger un CPD contra intrusiones físicas, como el acceso no autorizado o el robo de *hardware?* Para protegerse contra intrusiones físicas es crucial implementar una combinación de medidas de seguridad que incluyan la instalación de cerraduras electrónicas de alta seguridad en puertas y ventanas, sistemas de alarma de intrusión conectados a servicios de monitoreo las veinticuatro horas, videovigilancia con grabación en tiempo real, control de acceso

Seguridad y Alta Disponibilidad 44 Tema . Entrenamientos basado en tarjetas de identificación o biométrico, y la limitación de los accesos físicos solo al personal autorizado.

- ¿Cuál es la importancia de la ubicación física de un CPD en términos de seguridad? ¿Qué factores se deben considerar al seleccionar una ubicación para un CPD? La ubicación del CPD juega un papel crítico en su seguridad física y ambiental. Idealmente, debe estar alejado de áreas de riesgo como zonas propensas a inundaciones, terremotos o actividad sísmica, y debe tener fácil acceso para el personal autorizado y los servicios de emergencia. Además, la ubicación debe contar con una infraestructura eléctrica confiable y conexiones de red redundantes para garantizar la disponibilidad continua de los servicios.

- ¿Qué protocolos y procedimientos se deben seguir para garantizar la seguridad del acceso físico al CPD, como la autenticación de personal autorizado y la supervisión de visitantes? Para garantizar la seguridad del acceso físico al CPD, se deben establecer políticas y procedimientos claros que incluyan la autenticación de dos factores, la identificación y autorización del personal autorizado, el registro de visitantes, la supervisión continua mediante sistemas de videovigilancia y la implementación de controles de acceso físico como puertas con cerraduras electrónicas y torniquetes.

- ¿Cómo se puede garantizar la seguridad contra incendios en un CPD? ¿Qué sistemas de detección y extinción de incendios son los más adecuados? La seguridad contra incendios es crucial y debe abordarse mediante la implementación de sistemas de detección temprana de incendios, extintores automáticos de gas o polvo, sistemas de supresión de incendios por agua, segregación de áreas de riesgo y la eliminación de materiales inflamables en el entorno del CPD.

- ¿Cuáles son las consideraciones clave para garantizar la seguridad eléctrica en un CPD, incluidos los sistemas de alimentación ininterrumpida (SAI) y la distribución de energía? Para garantizar la seguridad eléctrica en un CPD se deben implementar medidas como: SAI con capacidad de respaldo suficiente para mantener el funcionamiento de los equipos durante cortes de energía, generadores de

Seguridad y Alta Disponibilidad 45 Tema . Entrenamientos emergencia para casos de fallo prolongado del suministro eléctrico, sistemas de distribución de energía redundantes y reguladores de voltaje para proteger contra fluctuaciones eléctricas.

- ¿Por qué es importante controlar la temperatura y la humedad en un CPD? ¿Qué efectos pueden tener las condiciones ambientales inadecuadas en el rendimiento y la fiabilidad de los sistemas? El control de la temperatura y la humedad en un CPD es esencial para evitar el sobrecalentamiento y la condensación que pueden dañar los equipos y afectar su rendimiento. Se deben implementar sistemas de refrigeración eficientes, monitoreo continuo de temperatura y humedad, además de políticas de control ambiental para mantener las condiciones óptimas de funcionamiento.

- ¿Qué medidas se pueden implementar para proteger un CPD contra desastres naturales, como terremotos, inundaciones o tormentas? Para protegerse contra desastres naturales, como terremotos, inundaciones o tormentas, se deben implementar medidas como la selección cuidadosa de la ubicación del CPD, la elevación del equipo por encima del nivel de inundación esperado, la construcción de estructuras resistentes, la implementación de sistemas de alerta temprana y la elaboración de planes de evacuación y recuperación de desastres.

- ¿Cuál es el papel de la seguridad física en la certificación de los estándares de calidad, como ISO 27001, en un entorno de CPD? La seguridad física y ambiental es un aspecto crítico en la certificación de los estándares de calidad como ISO 27001. Para cumplir con los requisitos de esta certificación, se deben implementar controles y procesos que garanticen la protección de los activos de información y la continuidad de las operaciones en el CPD.

- ¿Cómo se pueden integrar las políticas de seguridad física y ambiental en un enfoque más amplio de seguridad de la información y gestión de riesgos en un CPD? Es fundamental integrar las políticas de seguridad física y ambiental en un marco más amplio de seguridad de la información y gestión de riesgos. Esto implica la alineación de los controles y procedimientos de seguridad física con los objetivos

Seguridad y Alta Disponibilidad 46 Tema . Entrenamientos de seguridad de la información, la asignación de responsabilidades claras, la realización de evaluaciones de riesgos periódicas y la actualización continua de las medidas de seguridad en respuesta a cambios en el entorno operativo y las amenazas emergentes.

# Entrenamiento 2: evaluación y mejora de la

# seguridad física y ambiental de un centro de datos

Deberás identificar y evaluar las medidas de seguridad física y ambiental en un centro de datos y propondrás mejoras para aumentar la seguridad y la disponibilidad del sistema.

1. Deberás responder a unas preguntas relacionadas con el tema:

**▸** ¿Qué elementos componen la seguridad física en un centro de datos?

**▸** ¿Por qué es importante el control ambiental en un centro de datos?

**▸** ¿Cuáles son las consecuencias de no tener un adecuado sistema de seguridad física y ambiental?

2. Imaginemos una empresa tecnológica llamada «TechSolutions», la cual ha

experimentado un crecimiento exponencial en los últimos dos años. Como resultado, el CPD de dicha empresa ha tenido que expandirse rápidamente para soportar el incremento en el volumen de datos y la cantidad de servicios ofrecidos. Hace dos años, TechSolutions contaba con un CPD de tamaño moderado con medidas de seguridad bien definidas para su tamaño: Seguridad física:

**▸** Puertas de acceso con cerraduras convencionales.

**▸** Cámaras de vigilancia en la entrada principal del CPD.

**▸** Control de acceso básico con tarjetas magnéticas.

Seguridad ambiental:

**▸** Aire acondicionado para mantener una temperatura constante.

**▸** Sensores de humo para detectar incendios.

**▸** Extintores manuales en puntos estratégicos.

Con el crecimiento, TechSolutions ha duplicado el tamaño de su CPD e incrementado significativamente la cantidad de equipos y personal. Sin embargo, las medidas de seguridad no se han actualizado para reflejar este crecimiento. Esto crea vulnerabilidades tanto en la seguridad física como ambiental.

**Análisis de seguridad física.** Deberás identificar las posibles vulnerabilidades en la seguridad física del centro de datos, considerando:

**▸** Controles de acceso.

**▸** Supervisión por CCTV.

**▸** Seguridad perimetral.

**▸** Procedimientos de entrada y salida.

**Análisis de seguridad ambiental.** Deberás identificar los posibles riesgos y las áreas de mejora, considerando:

**▸** Sistemas de climatización.

**▸** Sistemas de detección de incendios.

**▸** Alimentación eléctrica y sistemas SAI/UPS.

**▸** Medidas contra inundaciones y otros desastres naturales.

#### ▸ Desarrollo paso a paso

Localizar las posibles vulnerabilidades:

**▸** Medidas de seguridad física obsoletas.

**▸** Medidas de seguridad ambiental obsoletas.

Dar soluciones adecuadas para mejorar las situaciones desfavorables. Realizar un informe.

#### ▸ Solución

1) Preguntas de reflexión:

**▸ Elementos de la seguridad física en un centro de datos:** los elementos de la seguridad física en un centro de datos son fundamentales para proteger los activos y la información crítica de la empresa. Estos elementos incluyen controles de acceso físicos como puertas reforzadas, cerraduras avanzadas y sistemas de identificación mediante tarjetas, que aseguran que solo el personal autorizado pueda ingresar. La vigilancia también juega un papel crucial, al utilizar sistemas de CCTV para monitorear continuamente las instalaciones y guardias de seguridad que proporcionan una capa adicional de protección. Además, el diseño del edificio es esencial, una ubicación estratégica y estructuras reforzadas contribuyen a la resistencia del centro de datos frente a desastres naturales y posibles ataques.

**▸ Importancia del control ambiental:** el control ambiental es de vital importancia en un centro de datos, ya que previene que se generen, en el *hardware,* daños provocados por condiciones inadecuadas como temperaturas extremas, humedad excesiva o polvo. Mantener un ambiente controlado garantiza el funcionamiento continuo del equipo, al evitar el sobrecalentamiento y otros problemas que pueden afectar el rendimiento. Además, al asegurar las condiciones óptimas, se evitan interrupciones del servicio, lo que es crucial para mantener la disponibilidad y la confiabilidad de los sistemas y servicios que dependen del centro de datos.

#### ▸ Consecuencias de una inadecuada seguridad física y ambiental: las

consecuencias de una inadecuada seguridad física y ambiental en un centro de datos pueden ser graves y multifacéticas. La pérdida de datos es una de las principales preocupaciones, ya que puede afectar la integridad y la disponibilidad de la información crítica. Además, los daños al equipo debido a condiciones ambientales adversas, como sobrecalentamiento o humedad, pueden provocar fallos en los sistemas. Estas situaciones conllevan interrupciones del servicio, lo que afecta la continuidad operativa y la satisfacción del cliente. Por último, los costos adicionales por reparaciones y las pérdidas operativas resultantes pueden ser significativos, lo cual impacta negativamente en la rentabilidad y la reputación de la empresa.

2) Planteamiento práctico:

Localizar las deficiencias existentes en las medidas de seguridad del CPD planteado. Posibles vulnerabilidades:

Medidas de seguridad física obsoletas

**▸** Acceso no controlado: las cerraduras convencionales no son suficientes para proteger un CPD de mayor tamaño. En un incidente reciente, un exempleado pudo ingresar fácilmente al CPD usando una llave antigua, lo que expuso a los equipos a un posible sabotaje.

**▸** Cámaras insuficientes: la cantidad de cámaras de vigilancia no ha aumentado proporcionalmente al tamaño del CPD. Las áreas nuevas no están cubiertas, lo que genera puntos ciegos que pueden ser explotados por intrusos.

**▸** Control de acceso débil: el sistema de tarjetas magnéticas no ha sido actualizado para incluir la autenticación de dos factores. Además, no se ha implementado un registro detallado de accesos, lo que dificulta el seguimiento de quién entra y sale del CPD.

Medidas de seguridad ambiental obsoletas

**▸** Enfriamiento inadecuado: aunque el CPD se ha expandido, el sistema de aire acondicionado no ha sido mejorado. Recientemente, un aumento en la carga de trabajo provocó que la temperatura subiera peligrosamente, lo que puso en riesgo los servidores.

**▸** Detección de incendios insuficiente: la expansión no incluyó la instalación de más sensores de humo en las nuevas áreas. Durante un pequeño incendio en una sección no cubierta, el retraso en la detección permitió que el fuego causara más daños de los que debería.

**▸** Extinción de incendios manual: los extintores manuales siguen siendo los mismos, sin considerar que las nuevas áreas están más alejadas y no tienen fácil acceso a estos dispositivos en caso de emergencia.

**▸** Detección de agua y humedad insuficiente: los sensores de agua no se han instalado en las nuevas áreas. Una filtración reciente pasó desapercibida, lo que causó daños en el equipo.

**▸** Alimentación eléctrica y sistemas SAI/UPS insuficientes: los sistemas de alimentación ininterrumpida (SAI/UPS) no se han ampliado para soportar la carga adicional. Durante una reciente interrupción del suministro eléctrico, el CPD experimentó un apagón que provocó la pérdida de datos críticos.

**▸** Medidas contra inundaciones y otros desastres naturales insuficientes: no se han implementado medidas adicionales para proteger el CPD contra inundaciones o desastres naturales. Una tormenta reciente causó inundaciones en las áreas nuevas, lo cual dañó severamente el equipo y provocó interrupciones en el servicio.

En cuanto a las posibles implementaciones de mejora:

Actualización de la seguridad física

**▸** Puertas de alta seguridad: implementar puertas con cerraduras electrónicas y control de acceso biométrico.

**▸** Sistema de vigilancia completo: instalar cámaras adicionales para cubrir todas las áreas del CPD y utilizar *software* avanzado de monitoreo.

**▸** Control de acceso avanzado: implementar la autenticación de dos factores y un registro detallado de todos los accesos al CPD.

Mejoras en seguridad ambiental

**▸** Sistemas de enfriamiento redundantes: actualizar el sistema de aire acondicionado y añadir redundancia para evitar sobrecalentamientos.

**▸** Sensores de incendio ampliados: instalar sensores de humo adicionales y sistemas de detección temprana en todas las áreas nuevas.

**▸** Sistemas automáticos de extinción de incendios: implementar sistemas automáticos de extinción, como rociadores y gases inertes, para responder rápidamente a los incendios.

**▸** Detección de agua y humedad: instalar sensores de agua en todas las áreas críticas para detectar cualquier filtración o acumulación de agua de manera temprana.

**▸** Alimentación eléctrica y sistemas SAI/UPS: ampliar la capacidad de los sistemas SAI/UPS para soportar la carga adicional y garantizar la continuidad del suministro eléctrico durante interrupciones.

**▸** Medidas contra inundaciones y otros desastres naturales: implementar barreras contra inundaciones, sistemas de drenaje mejorados y planes de contingencia para otros desastres naturales, para asegurar la protección integral del CPD.

# Entrenamiento 3: cálculo de un sistema de

# alimentación ininterrumpida (SAI/UPS) para una

# instalación

#### ▸ Planteamiento del ejercicio

Una empresa desea instalar un SAI para su sala de servidores y equipos de red. La sala incluye los siguientes equipos:

**▸** Tres servidores, cada uno con un consumo de 500 W.

**▸** Dos *switches* de red, cada uno con un consumo de 100 W.

**▸** Un *router* con un consumo de 50 W.

**▸** Un sistema de climatización con un consumo de 200 W.

**▸** Una unidad de almacenamiento NAS con un consumo de 150 W.

Calcula la potencia total requerida (W) y la capacidad de la batería (Ah) del SAI.

Parámetros clave:

**▸** Potencia nominal: la capacidad máxima de potencia que puede proporcionar el SAI, medida en vatios (W).

**▸** Autonomía: el tiempo que el SAI puede suministrar energía durante una interrupción, medida en minutos u horas.

**▸** Factor de carga: relación entre la potencia total que consume la instalación y la capacidad del SAI, típicamente se añade un factor de seguridad (1,2 o 1,3).

#### ▸ Desarrollo paso a paso

Para calcular la potencia total requerida del SAI por un lado deberemos calcular el consumo total de todos los equipos y aplicarle el factor de seguridad (1,3 recomendado). Así obtenemos la potencia nominal en vatios.

Para obtener la capacidad de la batería, por ejemplo, para treinta minutos de autonomía, primero se calcula la capacidad de la batería (Wh) y después se convierte de Wh a Ah.

![▸ Solución Consumo total:](images/image-20.png)

Tabla 3. Consumo total. Fuente: elaboración propia.

Potencia Nominal con Factor de Seguridad Añadir un margen de seguridad (1,3) al cálculo de la potencia total para cubrir los posibles incrementos de carga.

$$▸ Potencia Nominal: 2100 W x 1,3 = 2730 W.$$

Capacidad de batería para treinta minutos de autonomía Debemos utilizar la fórmula para calcular la capacidad de la batería necesaria para el tiempo de autonomía deseado. Capacidad de batería (Wh) = potencia nominal (W) x tiempo de autonomía (h).

$$Capacidad de batería (Wh): 2730 W x 0,5 h = 1365 Wh$$

Convertir la capacidad de batería de Wh a Ah (Amperios-hora) según el voltaje de la batería (típicamente 12 V o 24 V). Capacidad de batería (Ah) para 12 V: 1365 Wh / 12 V = 113,75 Ah Resultados:

**▸** Potencia nominal requerida: 2730 W.

**▸** Capacidad de batería: 1365 Wh o 113,75 Ah a 12 V.

# Entrenamiento 4: planificación y configuración de

# racks en un CPD

#### ▸ Planteamiento del ejercicio

Una empresa está configurando un nuevo CPD y necesita planificar la disposición de los racks. El CPD tiene dimensiones de diez metros por cinco metros y necesita albergar los siguientes equipos:

**▸** Diez servidores (2 U cada uno).

**▸** Cinco *switches* de red (1 U cada uno).

**▸** Dos *routers* (1 U cada uno).

**▸** Tres unidades de almacenamiento (4 U cada una).

**▸** Dos paneles de parcheo (1 U cada uno).

**▸** Espacio adicional para crecimiento futuro (10 U). Determina cuántos racks son necesarios para alojar todos estos equipos y cómo los dispondrías. Deberás tener presente lo siguiente: tendrás que maximizar el uso del espacio disponible, optimizar la distribución de energía y enfriamiento, además de organizar y etiquetar adecuadamente para facilitar el mantenimiento y las actualizaciones. Parámetros clave:

**▸** Unidades de rack (U): medida estándar de altura en racks, donde 1 U = 1,75 pulgadas (44,45 mm).

**▸** Equipos comunes: servidores, *switches, routers,* unidades de almacenamiento, paneles de parcheo.

#### ▸ Desarrollo paso a paso

Se deberá calcular el espacio total requerido y seleccionar racks estándar de 42 U de altura. A partir de ahí, determinar el número de racks necesarios, considerando la disposición de los racks en el CPD para optimizar el flujo de aire y el acceso a los equipos, y planificar la ubicación de cada equipo dentro de los racks.

#### ▸ Solución

Calcular el espacio total requerido:

$$▸ Servidores: 10 x 2 U = 20 U.$$

$$▸ Switches: 5 x 1 U = 5 U.$$

$$▸ Routers: 2 x 1 U = 2 U.$$

$$▸ Unidades de almacenamiento: 3 x 4 U = 12 U.$$

$$▸ Paneles de parcheo: 2 x 1 U = 2 U.$$

**▸** Espacio adicional: 10 U.

**▸** Total: 20 U + 5 U + 2 U + 12 U + 2 U + 10 U = 51 U. Selección de racks:

**▸** Elegir racks estándar de 42 U de altura.

**▸** Determinar cuántos racks son necesarios para acomodar 51 U de equipos.

Cálculo: **▸** Racks necesarios = Total U / Capacidad del rack = 51 U / 42 U ≈ 2 racks (uno lleno y otro parcialmente lleno). Diseño de la distribución: **▸** Considerar la disposición de los racks en el CPD para optimizar el flujo de aire y el acceso a los equipos.

**▸** Planificar la ubicación de cada tipo de equipo dentro de los racks.

Asignación de equipos a los racks: distribuir los equipos calculando que todos los racks tengan una carga equilibrada.

Rack 1:

**▸** Cinco servidores (10 U).

**▸** Tres *switches* (3 U).

**▸** Un *router* (1 U).

**▸** Dos unidades de almacenamiento (8 U).

**▸** Un panel de parcheo (1 U).

**▸** Espacio para crecimiento (10 U).

**▸** Total: 33 U.

Rack 2:

**▸** Cinco servidores (10 U).

**▸** Dos *switches* (2 U).

**▸** Un *router* (1 U).

**▸** Una unidad de almacenamiento (4 U).

**▸** Un panel de parcheo (1 U).

**▸** Total: 18 U.

Justificación

**▸** Equilibrio de carga: distribuir los equipos para mantener un balance y evitar

sobrecargar un solo rack. **▸** Espacio para crecimiento: dejar espacio en ambos racks para futuras expansiones. **▸** Eficiencia energética y enfriamiento: ubicación estratégica para optimizar el flujo de aire y la distribución de la energía. **▸** Gestión del cableado: organización adecuada y etiquetado para facilitar el mantenimiento.

# Entrenamiento 5: implementación de un plan de

# recuperación ante desastres (DRP) en un CPD

#### ▸ Planteamiento del ejercicio

Un plan de recuperación ante desastres (DRP por sus siglas en inglés *disaster* *recovery plan)* es un conjunto de procedimientos y estrategias diseñadas para restaurar la infraestructura tecnológica y los sistemas críticos de una organización después de un desastre o incidente grave. El objetivo principal de un DRP es minimizar el impacto de un desastre en la continuidad del negocio y garantizar la recuperación rápida y efectiva de las operaciones clave.

Deberás realizar un plan DRP para un CPD, para minimizar los efectos causados por los siguientes desastres:

**▸** Escenario: incendio en el CPD.

**▸** Escenario: inundación en el CPD.

#### ▸ Desarrollo paso a paso

## 1. Preparación y planificación.

## 2. Respuesta inmediata.

## 3. Recuperación de datos y sistemas.

## 4. Mejora continua.

#### ▸ Solución

## 1. Preparación y planificación

Análisis de riesgos:

**▸** Identificación de los riesgos específicos relacionados con los incendios, como cortocircuitos eléctricos, sobrecalentamiento de equipos o negligencia humana.

**▸** Identificación de los riesgos relacionados con las inundaciones, como lluvias intensas, desbordamiento de ríos cercanos o fallas en sistemas de drenaje.

Medidas preventivas

Para el riesgo de incendio:

**▸** Instalación de sistemas automáticos de detección de incendios (sensores de humo y calor) con alertas integradas al centro de control de seguridad.

**▸** Implementación de sistemas de supresión de incendios adecuados para CPD, como sistemas de rociadores de agua o agentes extintores que no dañen los equipos electrónicos.

**▸** Mantenimiento regular de los sistemas eléctricos y los equipos para prevenir fallas que puedan provocar un incendio.

Para el riesgo de inundación:

**▸** Elevación de equipos críticos y de infraestructura fuera del nivel de inundación potencial.

**▸** Instalación de barreras físicas o sistemas de contención para proteger las entradas y las bocas de ventilación.

**▸** Implementación de bombas de agua o sistemas de drenaje para evacuar el agua de manera rápida y eficiente.

## 2. Respuesta inmediata

Para el riesgo de incendio:

**▸** Activación del DRP: en caso de activación de alarmas de incendio, el responsable del CPD activará de inmediato el DRP.

**▸** Evacuación y seguridad: se establecerán protocolos claros de evacuación y seguridad para el personal del CPD, para asegurar que todos salgan del edificio de manera segura y siguiendo los procedimientos establecidos.

Para el riesgo de inundación:

**▸** Activación del DRP: al detectarse una amenaza de inundación, activar de inmediato el DRP y notificar al personal relevante.

**▸** Protección de datos y equipos: desconectar los equipos eléctricos y los sistemas críticos para evitar daños por cortocircuitos o sobrecargas eléctricas.

## 3. Recuperación de datos y sistemas

Para el riesgo de incendio:

**▸** Evaluación de daños: después de que el incendio sea controlado y sea seguro ingresar al CPD, se realizará una evaluación exhaustiva de los daños físicos y operativos.

**▸** Recuperación de servicios críticos: utilización de copias de seguridad fuera del sitio para restaurar los datos y los sistemas críticos. Las copias de seguridad deben estar almacenadas en ubicaciones seguras y accesibles para facilitar la rápida recuperación.

**▸** Reemplazo de los equipos dañados: identificación y reemplazo de equipos dañados o destruidos por el incendio, lo que garantiza que la infraestructura física del CPD sea restaurada a plena capacidad operativa.

Para el riesgo de inundación:

**▸** Evaluación de daños: tras la inundación, evaluar los daños físicos y operativos para determinar la extensión de la recuperación necesaria.

**▸** Restauración de servicios: utilización de las copias de seguridad almacenadas fuera del sitio para restaurar los datos críticos y los sistemas esenciales lo más rápido posible.

## 4. Mejora continua

**▸** Revisión posterior al incidente: después de la recuperación, se llevará a cabo una revisión exhaustiva del incidente para identificar las áreas de mejora en el DRP y en las medidas preventivas implementadas.

**▸** Actualización del DRP: según las lecciones aprendidas del incidente, se actualizará y se perfeccionará el DRP para fortalecer la respuesta futura ante desastres similares.

Consideraciones adicionales:

**▸** Formación y concientización: es crucial capacitar regularmente al personal del CPD sobre los procedimientos de seguridad, evacuación y respuesta ante desastres.

**▸** Coordinación con autoridades locales: mantener una estrecha coordinación con los servicios de emergencia locales para una respuesta rápida y efectiva en caso de desastres.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–35)*
- A fondo  *(pp.36–42)*
- Entrenamientos  *(pp.43–66)*
- Seguridad y Alta Disponibilidad 5 Tema . Material de estudio · Seguridad y Alta Disponibilidad 6 Tema . Material de estudio · Seguridad y Alta Disponibilidad 7 Tema . Material de estudio · Seguridad y Alta Disponibilidad 8 Tema . Material de estudio · Seguridad y Alta Disponibilidad 9 Tema . Material de estudio · Seguridad y Alta Disponibilidad 10 Tema . Material de estudio · Seguridad y Alta Disponibilidad 11 Tema . Material de estudio · Seguridad y Alta Disponibilidad 12 Tema . Material de estudio · Seguridad y Alta Disponibilidad 13 Tema . Material de estudio · Seguridad y Alta Disponibilidad 14 Tema . Material de estudio · Seguridad y Alta Disponibilidad 15 Tema . Material de estudio · Seguridad y Alta Disponibilidad 16 Tema . Material de estudio · Seguridad y Alta Disponibilidad 17 Tema . Material de estudio · Seguridad y Alta Disponibilidad 19 Tema . Material de estudio · Seguridad y Alta Disponibilidad 21 Tema . Material de estudio · Seguridad y Alta Disponibilidad 22 Tema . Material de estudio · Seguridad y Alta Disponibilidad 23 Tema . Material de estudio · Seguridad y Alta Disponibilidad 24 Tema . Material de estudio · Seguridad y Alta Disponibilidad 26 Tema . Material de estudio · Seguridad y Alta Disponibilidad 27 Tema . Material de estudio · Seguridad y Alta Disponibilidad 28 Tema . Material de estudio · Seguridad y Alta Disponibilidad 29 Tema . Material de estudio · Seguridad y Alta Disponibilidad 30 Tema . Material de estudio · Seguridad y Alta Disponibilidad 31 Tema . Material de estudio · Seguridad y Alta Disponibilidad 32 Tema . Material de estudio · Seguridad y Alta Disponibilidad 33 Tema . Material de estudio · Seguridad y Alta Disponibilidad 34 Tema . Material de estudio · Seguridad y Alta Disponibilidad 35 Tema . Material de estudio  *(pp.5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 19, 21, 22, 23, 24, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35)*
- Seguridad y Alta Disponibilidad 36 Tema . A fondo · Seguridad y Alta Disponibilidad 37 Tema . A fondo · Seguridad y Alta Disponibilidad 38 Tema . A fondo · Seguridad y Alta Disponibilidad 39 Tema . A fondo · Seguridad y Alta Disponibilidad 40 Tema . A fondo · Seguridad y Alta Disponibilidad 41 Tema . A fondo · Seguridad y Alta Disponibilidad 42 Tema . A fondo  *(pp.36–42)*
- Seguridad y Alta Disponibilidad 43 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 47 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 48 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 49 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 50 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 51 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 52 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 53 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 54 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 55 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 56 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 57 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 58 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 59 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 60 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 61 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 62 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 63 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 64 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 65 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 66 Tema . Entrenamientos  *(pp.43, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66)*