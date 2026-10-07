## Tema 10

# Servicios en Red e Internet

# Tema 10. Servicios de red, Internet y telefonía IP en la

# nube

# Índice

Esquema Material de estudio

## 10.1. Introducción y objetivos

## 10.2. Servicios de red en la nube

## 10.3. Servicios de Internet en la nube

## 10.4. Telefonía IP en la nube (VoIP)

## 10.5. Referencias bibliográficas

A fondo Cómo funciona Cloudflare con cualquier infraestructura de nube

Centro de aprendizaje

Tutorial Cloudflare: protege tu WEB contra ataques

La telefonía IP y VoIP

Dominio propio y CloudFlare

Entrenamientos Entrenamiento 1. Configuración de una VPN en Packet Tracer Entrenamiento 2. Configuración básica de Cloudflare para la protección y optimización de un sitio web Entrenamiento 3. Implementación y Comprensión de servicios de Internet en la nube (Parte 1) Entrenamiento 4. Configuración de una VPN Site-to-Site en Microsoft Azure Entrenamiento 5. Implementación y análisis de una solución de telefonía IP en la nube (VoIP)

# Esquema

![image-2](images/image-2.png)

Servicios en Red e Internet 4 Tema 10. Esquema

# 10.1. Introducción y objetivos

En la era digital, los servicios de red, Internet y telefonía IP en la nube son esenciales para las empresas que buscan operar de manera eficiente y competitiva. La infraestructura de TI ha evolucionado de los modelos tradicionales de *hardware* hacia soluciones basadas en la nube que proporcionan **flexibilidad, escalabilidad y** **accesibilidad global.** A medida que el entorno empresarial se vuelve más dinámico y distribuido, contar con servicios en la nube permite a las organizaciones responder de forma ágil a las cambiantes necesidades del mercado, así como facilitar el trabajo remoto y mejorar la experiencia de usuario.

Los **servicios de red en la nube** representan una base esencial para las empresas modernas al permitir la creación, gestión y seguridad de infraestructuras de red sin la necesidad de mantener *hardware* físico. Esto facilita la expansión de las redes corporativas a nivel mundial y reduce los costos de mantenimiento de infraestructura. Elementos como las **redes privadas virtuales** (VPN) permiten conexiones seguras entre dispositivos y redes corporativas a través de Internet, protegiendo la integridad de los datos y los accesos. Por otro lado, la tecnología SD-WAN (red de área amplia definida por *software)* optimiza el tráfico de red entre distintas ubicaciones mediante el control basado en *software,* mejorando la eficiencia y el rendimiento de las conexiones. Además, las conexiones dedicadas y los servicios de *firewall* como servicio (FWaaS) refuerzan la seguridad y el rendimiento de las redes, haciendo de la nube una opción ideal para la implementación de entornos de red flexibles y confiables.

En cuanto a los servicios de Internet en la nube, estos brindan tanto infraestructura para la conectividad como soluciones para optimizar el uso de la red. Los proveedores de servicios de Internet (ISP) en la nube ofrecen conexiones de banda ancha, 4G/5G y otras opciones de transmisión de datos que aprovechan la

Servicios en Red e Internet 5 Tema 10. Material de estudio infraestructura de la nube, aumentando la velocidad y disponibilidad del acceso a Internet para usuarios y empresas.

Servicios adicionales como las **redes de distribución de contenido** (CDN) ayudan a optimizar la entrega de contenido, asegurando tiempos de carga rápida y mejorando la experiencia de los usuarios finales, especialmente en plataformas globales. El DNS en la nube permite a las empresas gestionar nombres de dominio con alta disponibilidad y escalabilidad, un aspecto crucial para sitios web y aplicaciones con mucho tráfico. Por otro lado, los **servicios de protección DDoS** ofrecen defensas gestionadas contra ataques de denegación de servicio, fortaleciendo la ciberseguridad en una época de crecientes amenazas en línea.

La **telefonía IP en la nube** (VoIP) está revolucionando la comunicación empresarial al reemplazar las líneas telefónicas tradicionales con comunicaciones de voz basadas en Internet. La telefonía IP permite realizar y recibir llamadas desde cualquier ubicación con conexión a Internet, eliminando la dependencia de la infraestructura telefónica local.

Entre las soluciones más destacadas está el **PBX en la nube,** un sistema de conmutación privada que gestiona las llamadas internas y externas de la empresa sin necesidad de *hardware* físico. Además, esta tecnología ofrece funciones avanzadas como el desvío de llamadas, grabación y conferencias, consolidando la comunicación interna y externa en una sola plataforma.

La telefonía unificada, que integra llamadas de voz, videollamadas y mensajería instantánea, facilita la colaboración en tiempo real (RTC) a través de la nube. El SIP *trunking,* por su parte, permite conectar el sistema PBX de una empresa a la red telefónica a través de Internet, optimizando los recursos y abriendo posibilidades de expansión de la red telefónica sin complicaciones de infraestructura. Los beneficios de adoptar servicios de red, Internet y telefonía en la nube son significativos.

L a **escalabilidad** permite a las empresas aumentar o disminuir recursos según la demanda sin realizar grandes inversiones en infraestructura física, lo que resulta en una gestión de recursos flexible y eficiente.

La **reducción de costos** es otra ventaja clave: al eliminar la necesidad de adquirir y mantener *hardware,* las empresas pueden concentrar su inversión en el desarrollo de su negocio, lo cual es especialmente beneficioso para las pequeñas y medianas empresas.

La **accesibilidad global** es otro punto que destacar, ya que los servicios en la nube están disponibles desde cualquier lugar, facilitando el trabajo remoto y permitiendo que las empresas accedan a sus recursos desde cualquier parte del mundo.

Además, la **seguridad avanzada** es un factor decisivo, ya que los servicios en la nube suelen ofrecer opciones de cifrado de extremo a extremo y protección contra ciberataques, garantizando la integridad y privacidad de los datos.

En resumen, los servicios de red, Internet y telefonía IP en la nube han pasado de ser una opción a una necesidad para muchas empresas. Ofrecen una infraestructura flexible, accesible y escalable, adaptada a los desafíos del mercado actual y con un alto enfoque en la seguridad. Al facilitar una comunicación eficiente y proteger los datos corporativos, estos servicios contribuyen significativamente a la modernización de las operaciones empresariales y a la creación de un entorno de trabajo conectado y seguro.

Para las organizaciones que buscan optimizar su rendimiento y reducir sus costos operativos, los servicios en la nube representan una inversión estratégica que les permite no solo mantenerse a la par con las exigencias del mercado, sino también innovar y crecer en un entorno cada vez más competitivo.

Los **objetivos** clave que se pretenden alcanzar en este tema los siguientes: **▸** Comprender los conceptos básicos de los servicios de red en la nube y su rol en la infraestructura de TI moderna. **▸** Identificar los distintos tipos de servicios de red en la nube, como VPN, SD-WAN, conexiones dedicadas y FWaaS y analizar sus beneficios y aplicaciones. **▸** Reconocer los elementos y funciones de los servicios de Internet en la nube, como CDN, DNS gestionado y servicios de protección contra ataques DDoS. **▸** Explorar los beneficios de la telefonía IP en la nube (VoIP), incluyendo reducción de costos, accesibilidad y comunicaciones unificadas. **▸** Analizar las ventajas de escalabilidad y flexibilidad de los servicios en la nube para adaptarse a las necesidades cambiantes de las empresas. **▸** Evaluar los beneficios de seguridad de los servicios en la nube, como el cifrado y la protección contra ciberataques. **▸** Estudiar la tecnología detrás de la comunicación en tiempo real (RTC) y su importancia para la colaboración remota. **▸** Comprender el impacto de SIP *trunking* en la telefonía corporativa y su función en la conexión a la red telefónica pública. **▸** Explorar la accesibilidad global de los servicios en la nube para permitir el trabajo remoto y conectar equipos distribuidos. **▸** Desarrollar una visión estratégica sobre la migración a la nube y sus beneficios en costos, eficiencia y ciberseguridad.

# 10.2. Servicios de red en la nube

Los servicios de red en la nube ofrecen soluciones que permiten gestionar y asegurar infraestructuras de red sin la necesidad de disponer de *hardware* físico local. Esto simplifica el proceso de administración y mejora la flexibilidad de las organizaciones, ya que pueden escalar y adaptarse rápidamente a las necesidades cambiantes de su red. A continuación, se detallan algunos de los servicios más comunes en este ámbito.

Redes privadas virtuales (VPN)

Las redes privadas virtuales (VPN) son una tecnología crucial en el ámbito de la seguridad de redes. Permiten crear **conexiones seguras** entre dispositivos y la red corporativa a través de Internet, proporcionando un túnel virtual en el que los datos viajan de manera **cifrada y segura.** Esto asegura que la información sensible no sea interceptada por atacantes malintencionados. Las VPN son especialmente útiles para empresas que tienen empleados remotos o sucursales distribuidas geográficamente, ya que ofrecen una forma segura y flexible de acceder a recursos internos sin necesidad de infraestructura física compleja.

Ejemplos de aplicaciones y casos de uso:

**▸ Trabajo remoto seguro:** supongamos que una empresa tiene empleados trabajando desde diferentes ubicaciones del mundo. Con la VPN, estos empleados pueden conectarse a la red corporativa como si estuvieran en la oficina, utilizando una conexión cifrada que protege los datos que envían y reciben, incluso en redes wifi públicas. Por ejemplo, un trabajador en un café o en un aeropuerto puede acceder a archivos internos de la empresa o utilizar aplicaciones sensibles sin preocuparse por los riesgos de seguridad asociados con redes no seguras.

Ejemplo de trabajo remoto seguro

Un empleado de una empresa de consultoría se conecta a través de una VPN para acceder a documentos de clientes y herramientas internas mientras trabaja desde su casa. La VPN cifra toda su comunicación, asegurando que la información no sea vulnerable a la interceptación.

**▸ Interconexión segura de sucursales:** las empresas con múltiples oficinas o sucursales pueden usar VPN para conectar esas ubicaciones a través de Internet de manera segura. De esta forma, las oficinas remotas pueden acceder a los mismos recursos y aplicaciones como si estuvieran en la sede central, sin necesidad de arrendar líneas dedicadas costosas. Las VPN crean un «túnel» cifrado entre las sucursales que protege el tráfico entre ellas.

Ejemplo de VPN

Una cadena de restaurantes con sedes en varias ciudades utiliza una VPN para que sus oficinas centrales en Madrid se conecten de manera segura con las sucursales de Barcelona y Valencia. Esto permite a los gerentes de las sucursales acceder a la base de datos centralizada de inventarios y ventas sin comprometer la seguridad de la red.

![Figura 1. Cómo funciona una VPN. Fuente: Trevino, 2022.](images/image-3.png)

*Figura 1. Cómo funciona una VPN. Fuente: Trevino, 2022.*

#### Ventajas de usar una VPN

Las ventajas de usar una VPN (red privada virtual) son múltiples y van más allá de simplemente mejorar la seguridad de la red. A continuación te presento algunas de las principales ventajas:

![image-4](images/image-4.png)

Tabla 1. Tres beneficios clave de las VPN. Fuente: elaboración propia.

#### SD-WAN (red de área amplia definida por software)

La SD-WAN es una solución innovadora diseñada para optimizar y simplificar la gestión de las redes de área amplia (WAN). A diferencia de las redes tradicionales, que dependen de *hardware* físico como rúteres y conmutadores, SD-WAN utiliza un **enfoque basado en** ***software*** para gestionar el tráfico de red entre diversas ubicaciones de manera más eficiente. Esto permite que las empresas conecten múltiples sucursales o centros de datos a través de Internet o líneas privadas de una forma flexible, segura y rentable, adaptándose rápidamente a los cambios en la demanda de la red.

#### Cómo funciona SD-WAN

SD-WAN funciona dirigiendo el tráfico de datos a través de la red de manera más inteligente y eficiente. Utiliza **políticas configurables** basadas en *software* para determinar el mejor camino para los datos, ya sea a través de Internet o de conexiones privadas. A través de esta gestión dinámica, el tráfico se puede priorizar según la criticidad de las aplicaciones, lo que mejora el rendimiento general de la red y asegura que las aplicaciones más importantes, como videoconferencias o sistemas de gestión de clientes (CRM), tengan prioridad en el ancho de banda.

El sistema centralizado de SD-WAN también permite a los administradores de red gestionar y monitorizar de forma remota las conexiones y el rendimiento de la red, lo que simplifica la gestión y la resolución de problemas.

Ejemplos de aplicaciones y casos de uso:

**▸ Conexión entre oficinas distribuidas:** empresas con varias sucursales u oficinas en diferentes ubicaciones geográficas se benefician enormemente de SD-WAN, ya que facilita la interconexión de estas oficinas de forma segura y eficiente. La red definida por *software* asegura que el tráfico entre las oficinas se maneje de la manera más eficiente posible, utilizando Internet o conexiones privadas según sea necesario y priorizando las aplicaciones críticas de negocio.

Ejemplo

Una empresa global de *software* con oficinas en Madrid, Nueva York y Tokio utiliza SD-WAN para conectar sus tres oficinas. Gracias a la optimización del tráfico, las videoconferencias entre equipos de trabajo dispersos se realizan sin interrupciones y las aplicaciones empresariales esenciales, como los servidores de bases de datos, tienen prioridad en la red.

**▸ Optimización de aplicaciones empresariales:** las aplicaciones empresariales que requieren una alta disponibilidad y baja latencia, como ERP, CRM y sistemas de gestión de inventarios, pueden beneficiarse de SD-WAN, ya que el tráfico se enruta por los caminos más rápidos y fiables. Esto asegura un rendimiento más eficiente y una experiencia de usuario consistente, incluso en redes de área amplia (WAN) de alto tráfico.

Ejemplo

Una cadena de minoristas utiliza SD-WAN para optimizar el acceso a su sistema de punto de venta (POS) desde sus tiendas en diversas ciudades. Gracias a SD‑WAN, los datos de las transacciones se procesan rápidamente y de forma eficiente, incluso cuando el tráfico de Internet es alto.

**▸ Integración con servicios en la nube:** con la creciente adopción de servicios en la nube, SD‑WAN ofrece una integración más fluida y segura con estas plataformas. Las empresas que utilizan aplicaciones en la nube, como servicios de almacenamiento o sistemas de comunicación, pueden garantizar que su tráfico hacia y desde la nube sea optimizado, seguro y de bajo costo.

Ejemplo

Una empresa de *marketing* digital utiliza varios servicios de almacenamiento en la nube para almacenar grandes volúmenes de datos y ejecutar aplicaciones como la gestión de campañas. Mediante SD‑WAN, la empresa optimiza el acceso a estos servicios, mejorando la velocidad de transferencia de archivos y asegurando que las aplicaciones críticas funcionen sin interrupciones.

![Ventajas de SD-WAN](images/image-5.png)

Tabla 2. Tres beneficios clave de los SD-WAN. Fuente: elaboración propia.

Firewall como servicio (FWaaS)

El concepto de *firewall* como servicio (FWaaS) se refiere a una solución de **seguridad** de red **gestionada y basada en la nube** que actúa como un cortafuegos para proteger las infraestructuras informáticas contra amenazas externas. Este servicio es una alternativa moderna a los *firewalls* tradicionales, ya que elimina la necesidad de gestionar *hardware* físico y permite la protección de la red en entornos distribuidos, como aquellos que utilizan aplicaciones en la nube y servicios híbridos.

Características principales del FWaaS:

**▸ Protección en la nube:** FWaaS proporciona una protección robusta contra accesos no autorizados y ciberataques, como intrusiones, DDoS (ataques de denegación de servicio distribuido) y otras amenazas, todo ello gestionado desde la nube.

**▸ Gestión centralizada:** al ser un servicio gestionado, las organizaciones no necesitan instalar ni mantener *hardware* de *firewall,* lo que reduce el costo y la complejidad. La configuración y la administración de las reglas de tráfico se realizan de forma centralizada desde una consola web.

**▸ Escalabilidad:** al estar basado en la nube, el FWaaS puede adaptarse de manera flexible a las necesidades de la organización. Puede escalar fácilmente para manejar grandes volúmenes de tráfico y ofrecer protección continua sin las limitaciones de un *firewall* físico.

**▸ Visibilidad y control avanzados:** proporciona una visión detallada del tráfico de red, permitiendo a los administradores observar en tiempo real las amenazas y comportamientos anómalos. También, facilita el control granular sobre las reglas de acceso, proporcionando a las empresas mayor flexibilidad y seguridad.

**▸ Actualizaciones automáticas y mantenimiento:** los proveedores de FWaaS se encargan de actualizar regularmente las definiciones de amenazas y las configuraciones del *firewall,* asegurando que siempre se tenga la última protección disponible sin intervención manual.

**▸ Protección contra amenazas externas:** FWaaS está diseñado para proteger las redes de ataques externos, lo que lo hace particularmente útil para empresas que operan en la nube o que tienen infraestructura distribuida.

**▸ Integración con otras soluciones de seguridad:** FWaaS puede integrarse con otras soluciones de seguridad, como sistemas de detección y prevención de intrusiones (IDS/IPS), antivirus y soluciones de análisis de seguridad, para ofrecer una defensa en profundidad.

#### Ejemplos de proveedores de FWaaS

Algunos proveedores destacados de servicios FWaaS incluyen:

**▸ Zscaler:** ofrece un servicio de *firewall* robusto, escalable y fácil de gestionar.

**▸ Palo Alto Networks:** con su solución de *firewall* basado en la nube, proporciona una protección avanzada contra amenazas, control de aplicaciones y visibilidad.

**▸ Fortinet:** FortiGate Cloud es una solución de *firewall* que también se ofrece como servicio gestionado para entornos en la nube.

# 10.3. Servicios de Internet en la nube

La conectividad a Internet en la nube se basa en una infraestructura que no solo permite el acceso a Internet, sino que, también, **optimiza la distribución y** **seguridad de la red.** Aquí, detallamos algunos de los principales servicios de

Internet en la nube.

Proveedores de servicios de Internet (ISP) basados en la nube

Los proveedores de servicios de Internet (ISP) que operan con infraestructura

basada en la nube están innovando en la forma de ofrecer conexiones de banda ancha y servicios móviles como 4G y 5G. A diferencia de los ISP tradicionales, estos proveedores se benefician de la escalabilidad, flexibilidad y reducción de costos que ofrece la nube para proporcionar conexiones de alta calidad y eficientes en transmisión de datos. A continuación, exploramos las principales conexiones que los ISP basados en la nube pueden ofrecer.

#### Conexiones de banda ancha

Los ISP en la nube están facilitando el despliegue de conexiones de banda ancha en áreas urbanas y rurales al utilizar infraestructura en la nube que optimiza la transmisión de datos. Esto permite administrar el **tráfico de red en tiempo real,** lo que resulta en un servicio más estable y confiable para los usuarios finales. Los ISP en la nube aprovechan tecnologías como SD-WAN (Software-Defined Wide Area Network) para gestionar el enrutamiento y optimizar el uso del ancho de banda.

Ventajas:

**▸ Escalabilidad:** los ISP pueden aumentar la capacidad de la red de manera rápida para responder a la demanda de los usuarios.

**▸ Gestión centralizada:** la infraestructura en la nube permite supervisar y administrar redes desde ubicaciones remotas.

**▸ Optimización del ancho de banda:** con SD-WAN, los ISP basados en la nube pueden priorizar el tráfico de aplicaciones críticas, mejorando la experiencia del usuario.

#### Conexiones 4G/5G

Los servicios de 4G y 5G, que inicialmente eran gestionados por operadoras móviles tradicionales, ahora también son ofrecidos por ISP basados en la nube que utilizan infraestructura virtualizada. Esto permite la disponibilidad de redes de alta velocidad con baja latencia para aplicaciones de transmisión de datos en tiempo real, como videollamadas, *gaming* y servicios IoT (internet de las cosas).

Características clave:

**▸ Alta velocidad y baja latencia:** las conexiones 5G proporcionan velocidades hasta 100 veces mayores que el 4G, siendo ideales para aplicaciones que requieren una respuesta en tiempo real.

**▸ Cobertura extensa:** al utilizar nodos de red virtualizados en la nube, los ISP pueden ofrecer servicios en ubicaciones donde antes no había conectividad móvil.

**▸ Facilidad de expansión:** los ISP pueden implementar redes privadas 5G para empresas y despliegues industriales mediante infraestructura en la nube, reduciendo la necesidad de instalación física.

#### Otras opciones de transmisión de datos

Además de la banda ancha y las redes móviles, los ISP en la nube ofrecen una variedad de tecnologías de transmisión de datos innovadoras:

**▸ Wifi 6:** los ISP basados en la nube pueden desplegar puntos de acceso wifi 6 que se gestionan remotamente, mejorando el rendimiento en áreas densamente pobladas y optimizando la capacidad de la red.

**▸** ***IoT Networking:*** la nube permite a los ISP desplegar redes IoT escalables y seguras, necesarias para la conectividad de dispositivos en sectores como la salud, la agricultura y la industria.

**▸ Transmisión satelital basada en la nube:** algunos ISP utilizan satélites de órbita baja (LEO) combinados con infraestructura en la nube para proporcionar servicios de Internet en zonas remotas o de difícil acceso. La transmisión de datos se gestiona a través de centros de datos en la nube, asegurando mayor estabilidad en las conexiones satelitales.

CDN (red de distribución de contenido)

Las CDN son servicios basados en la nube que optimizan la entrega de contenido web y aseguran tiempos de carga rápida, incluso para usuarios situados en distintas partes del mundo. Una CDN distribuye el contenido en una **red de servidores** **distribuidos geográficamente** (nodos), que almacena copias del contenido estático y dinámico de los sitios web para servirlo desde el nodo más cercano al usuario final.

DNS en la nube

Los servicios de DNS en la nube han transformado la administración de nombres de dominio, proporcionando una manera avanzada de traducir nombres de dominio en direcciones IP y permitiendo que los usuarios accedan fácilmente a los sitios web y aplicaciones. A diferencia de los sistemas DNS tradicionales, el DNS en la nube utiliza infraestructura distribuida y capacidades avanzadas para garantizar un

Servicios en Red e Internet 19 Tema 10. Material de estudio rendimiento y disponibilidad de primer nivel. A continuación, se detallan las ventajas y características principales de los DNS en la nube.

#### Alta disponibilidad

La disponibilidad es esencial para los servicios DNS, ya que una falla puede impedir el acceso a sitios web y aplicaciones. Los proveedores de DNS en la nube distribuyen las consultas a través de centros de datos ubicados globalmente, lo que permite una resolución rápida y confiable.

**▸ Redundancia:** con múltiples servidores distribuidos por distintas regiones, el DNS en la nube garantiza la disponibilidad constante del servicio, incluso si uno o varios centros de datos fallan.

**▸ Resolución rápida de consultas:** la arquitectura distribuida permite que las consultas DNS sean redirigidas al centro de datos más cercano, mejorando los tiempos de respuesta y optimizando la experiencia del usuario final.

**▸** ***Failover*** **automático:** en caso de que un servidor de DNS experimente problemas, el tráfico se redirige automáticamente a otro servidor en la red, asegurando que las consultas no se vean interrumpidas.

#### Protección contra ciberataques

El DNS en la nube integra potentes medidas de seguridad que protegen contra una variedad de ciberataques, particularmente aquellos que buscan interrumpir el servicio o comprometer su seguridad.

**▸ Mitigación de DDoS:** los ataques de denegación de servicio distribuido (DDoS) que apuntan a los servidores DNS son comunes y pueden causar caídas de servicios. El DNS en la nube cuenta con tecnología para identificar y bloquear este tipo de tráfico malicioso, manteniendo el servicio estable.

**▸ Protección avanzada contra ataques de DNS:** los servicios en la nube pueden detectar y prevenir manipulaciones de DNS, como el envenenamiento de caché, asegurando la integridad de las respuestas y protegiendo a los usuarios de ataques de redireccionamiento malicioso.

**▸ Cifrado de consultas (DNS over HTTPS o DNS over TLS):** para proteger la privacidad y evitar la intercepción de consultas DNS, algunos proveedores de DNS en la nube cifran las solicitudes, aumentando la seguridad y la confidencialidad de la navegación de los usuarios.

#### Escalabilidad automática

La capacidad de escalar de manera automática es fundamental en los entornos digitales actuales, donde el tráfico puede variar significativamente.

**▸ Adaptación al aumento de demanda:** los servicios de DNS en la nube se ajustan automáticamente a los picos de tráfico, lo que permite manejar grandes volúmenes de consultas sin degradar el rendimiento.

**▸ Ajuste de recursos dinámico:** a medida que una aplicación o sitio web crece en popularidad, el DNS en la nube ajusta sus recursos de forma dinámica para mantener un nivel óptimo de servicio, sin necesidad de intervención manual.

**▸ Flexibilidad para proyectos temporales:** para empresas que lanzan eventos, campañas o promociones que requieren un aumento temporal en el tráfico, la escalabilidad automática del DNS en la nube es esencial para asegurar que estos períodos de alta demanda no afecten la disponibilidad.

Servicios de protección DDoS

Los servicios de protección DDoS en la nube son soluciones avanzadas diseñadas para **mitigar los ataques de denegación de servicio distribuido** (DDoS), un tipo de ciberataque en el cual los atacantes intentan saturar los recursos de un sistema o red, dejando los servicios inoperativos. A través de infraestructura y defensas gestionadas, estos servicios protegen aplicaciones, redes y sitios web al detectar y bloquear el tráfico malicioso en tiempo real.

# 10.4. Telefonía IP en la nube (VoIP)

La telefonía IP en la nube, también conocida como VoIP (voz sobre protocolo de Internet), **reemplaza las líneas telefónicas tradicionales** mediante el uso de comunicaciones de voz que funcionan sobre la infraestructura de Internet. Este enfoque ofrece una mayor flexibilidad y permite a las empresas optimizar sus sistemas de comunicación sin necesidad de costosos equipos de telefonía física. A continuación, se destacan las características y beneficios de la telefonía IP en la nube.

Llamadas de voz a través de Internet

La tecnología VoIP permite realizar y recibir llamadas de voz desde cualquier ubicación con conexión a Internet, eliminando la dependencia de una infraestructura telefónica local.

**▸ Acceso desde cualquier lugar:** los usuarios pueden hacer llamadas desde cualquier dispositivo conectado a Internet (computadora, teléfono móvil, tableta), lo que facilita el trabajo remoto y la movilidad.

**▸ Reducción de costos:** al no requerir líneas telefónicas físicas, VoIP reduce significativamente los costos de infraestructura y mantenimiento asociados con los sistemas telefónicos tradicionales.

**▸ Calidad de voz mejorada:** las conexiones VoIP ofrecen una calidad de voz HD siempre que la conexión a Internet sea estable, proporcionando una experiencia de llamada clara y nítida.

PBX en la nube

Un sistema PBX (Private Branch Exchange) en la nube es una centralita telefónica que opera sobre infraestructura en la nube, gestionando las llamadas internas y externas sin necesidad de *hardware* físico en las instalaciones.

**▸ Gestión de llamadas avanzada:** los PBX en la nube ofrecen funcionalidades avanzadas como desvío de llamadas, grabación, conferencia y manejo de extensiones, permitiendo un control flexible y profesional de las comunicaciones empresariales.

**▸ Sin requerimientos de mantenimiento físico:** al estar basado en la nube, un PBX en la nube no requiere mantenimiento físico ni actualizaciones de *hardware,* ya que estas tareas las gestiona el proveedor.

**▸ Escalabilidad y adaptación:** a medida que una empresa crece, su sistema PBX en la nube puede escalar sin problemas, permitiendo agregar o eliminar usuarios de forma sencilla y rápida.

Telefonía unificada

La telefonía unificada integra múltiples canales de comunicación en una sola plataforma, facilitando la colaboración y la gestión de comunicaciones.

**▸ Integración de servicios de voz y mensajería:** la telefonía unificada permite gestionar llamadas de voz, correo de voz, videollamadas y mensajería instantánea desde una misma aplicación, promoviendo la eficiencia en la comunicación.

**▸ Experiencia de usuario cohesiva:** los empleados pueden cambiar entre diferentes canales de comunicación (como llamadas de voz y videollamadas) sin interrupciones, lo cual facilita la comunicación fluida y en tiempo real.

**▸ Mejora de la productividad:** al centralizar todos los métodos de comunicación, los usuarios pueden trabajar de manera más ágil, sin tener que gestionar varias aplicaciones o dispositivos diferentes.

Comunicación en tiempo real (RTC)

Las plataformas de comunicación en tiempo real (RTC) permiten realizar videoconferencias, llamadas y mensajería instantánea directamente desde aplicaciones basadas en la nube.

**▸ Videoconferencias y reuniones virtuales:** las empresas pueden organizar videoconferencias y reuniones en línea desde cualquier lugar, lo que es ideal para equipos distribuidos o que trabajan de manera remota.

**▸ Interacción instantánea:** la mensajería instantánea y la capacidad de realizar llamadas en tiempo real facilitan la interacción rápida entre equipos y departamentos.

**▸ Colaboración mejorada:** con funciones de compartir pantalla y chat en vivo, las herramientas de RTC fortalecen la colaboración y reducen la necesidad de reuniones físicas.

SIP trunking

El SIP *trunking* es una tecnología que permite a las empresas conectar su sistema PBX, ya sea local o en la nube, con las redes de telefonía pública a través de Internet.

**▸ Conexión con la red telefónica pública (PSTN):** SIP *trunking* conecta las llamadas VoIP a la red telefónica tradicional, permitiendo llamadas a números fijos o móviles convencionales sin necesidad de una línea telefónica analógica.

**▸ Ahorro de costos y escalabilidad:** al eliminar las líneas telefónicas físicas, el SIP *trunking* reduce los costos y permite un crecimiento fácil, ya que el número de líneas puede ajustarse según las necesidades de la empresa.

**▸ Compatibilidad con sistemas PBX existentes:** las empresas que ya tienen una infraestructura PBX local pueden beneficiarse del SIP *trunking* para integrar su sistema de comunicaciones existente con VoIP, aprovechando las ventajas de la telefonía en la nube.

![Figura 2. Cómo funciona un Truck SIP. Fuente: GoTrunk, 2023.](images/image-6.png)

*Figura 2. Cómo funciona un Truck SIP. Fuente: GoTrunk, 2023.*

# 10.5. Referencias bibliográficas

GoTrunk. (2023). *Manual usuario Truck SIP* . [https://gotrunk.es/docs/introducci%C3%B3n/](https://gotrunk.es/docs/introducci%25C3%25B3n/) Trevino, A. (2022, septiembre 15). ¿Qué es una VPN? *Keeper.* <https://www.keepersecurity.com/blog/es/2022/09/15/what-is-a-vpn/>

# Cómo funciona Cloudflare con cualquier infraestructura de nube

*Cómo funciona Cloudflare con cualquier infraestructura de nube.* (s. f.). Cloudflare. [https://www.cloudflare.com/es-es/learning/cloud/cloudflare-and-the-cloud/](https://www.cloudflare.com/es-es/learning/cloud/cloudflare-and-the-cloud/)

En este recurso encontrarás todo lo que te falta por saber relacionado con la nube y los servicios que te ofrece. Además, tendrás la visión desde Cloudflare, donde se protege y acelera cualquier cosa que se conecte a internet.

# Centro de aprendizaje

*Centro de aprendizaje.* (s. f.). Cloudfare. [https://www.cloudflare.com/es-es/learning/](https://www.cloudflare.com/es-es/learning/)

En este centro de aprendizaje profundizarás en temas como ataques DDoS, CDN, rendimiento de la CDN, seguridad SSL/TLS de la CDN, la nube, multinube, nube híbrida, *firewall* en la nube, SASE, NaaS, ZTNA, computación sin servidor, función como servicio (FaaS) y proceso perimetral.

# v=ue375N4JXXs

# Tutorial Cloudflare: protege tu WEB contra ataques

MoureDev TV. (2024, agosto 19). *Tutorial CLOUDFLARE: Protege tu WEB contra* *ATAQUES en minutos y gratis* [Vídeo]. YouTube. <https://www.youtube.com/watch?> ¿Cuáles son los problemas sufridos por los ataques más habituales para un servidor web? Aquí tienes un videotutorial de la herramienta Cloudflare, que actúa como un proxy y DNS para filtrar el tráfico y proteger la web antes de que alcance el servidor de *hosting.*

![image-7](images/image-7.png)

Accede al vídeo: [https://www.youtube.com/embed/ue375N4JXXs](https://www.youtube.com/embed/ue375N4JXXs)

# [https://www.youtube.com/watch?v=vMNCXtz8ePg](https://www.youtube.com/watch?v=vMNCXtz8ePg)

# La telefonía IP y VoIP

Pro Amperos. (2020, febrero 8). *La telefonía IP y VoIP* [Vídeo]. YouTube. El mundo de la telefonía se amplia y fusiona con la red de Internet dando un montón de posibilidades al usuario. Descubre las bases para que puedas introducirte en este campo.

![image-8](images/image-8.png)

Accede al vídeo: [https://www.youtube.com/embed/vMNCXtz8ePg](https://www.youtube.com/embed/vMNCXtz8ePg)

# jylQ

# Dominio propio y CloudFlare

Un loco y su tecnología. (2022, octubre 22). *Dominio Propio y CloudFlare: La mejor* *alternativa a DuckDNS* [Vídeo]. YouTube. <https://www.youtube.com/watch?v=kKwIIR-> Videotutorial donde te muestra cómo utilizar el CloudFlare y poder asociarlo con un DNS dinámico. DNS en la nube te ofrece servicios de nombres de dominio gestionados que proporcionan alta disponibilidad y escalabilidad para sitios web y aplicaciones.

![image-9](images/image-9.png)

Accede al vídeo: [https://www.youtube.com/embed/kKwIIR-jylQ](https://www.youtube.com/embed/kKwIIR-jylQ)

# Entrenamiento 1. Configuración de una VPN en

# Packet Tracer

#### ▸ Planteamiento del ejercicio

El objetivo de esta actividad es aprender a configurar una red privada virtual (VPN) utilizando el protocolo IPsec en Packet Tracer. Se establecerá una conexión segura entre dos redes separadas, permitiendo que los dispositivos de cada red se comuniquen de manera cifrada y protegida a través de un túnel VPN.

Requisitos:

**▸** Dos rúteres (R1 y R2).

**▸** Dos PC (PC1 y PC2).

**▸** Conexión serial entre los rúteres (WAN).

**▸** Conexión Ethernet entre los rúteres y las PC (LAN).

**▸** Conexiones y configuraciones de red básicas.

**▸** Configuración de una VPN entre los dos rúteres utilizando el protocolo IPsec.

#### ▸ Desarrollo paso a paso

Configuración de la red:

**▸** Conecta los rúteres (R1 y R2) mediante una interfaz serial.

**▸** Asigna direcciones IP a las interfaces Ethernet de los rúteres y las PC, asegurando

que cada red esté en una subred diferente.

**▸** Conecta las PC a los rúteres utilizando cables Ethernet.

Configuración de rutas estáticas: **▸** Configura rutas estáticas en los rúteres para permitir la comunicación entre las redes de cada uno. Configuración de la VPN (IPsec): **▸** En cada rúter, configura una VPN utilizando IPsec para establecer un túnel seguro entre R1 y R2. **▸** Configura políticas ISAKMP para la autenticación y cifrado y aplica un transform-set IPsec adecuado. **▸** Utiliza una clave precompartida para la autenticación de los rúteres. Verificación de la conexión: **▸** Realiza pruebas de conectividad (ping) entre las PC para asegurarte de que los dispositivos en ambas redes puedan comunicarse de forma segura a través de la VPN.

**▸** Utiliza los comandos show crypto isakmp sa y show crypto ipsec sa para verificar el

estado de la conexión VPN.

Informe: **▸** Elabora un informe en el que describas los pasos seguidos para configurar la VPN, los resultados obtenidos y cualquier problema o detalle relevante durante el proceso de configuración.

#### ▸ Solución

#### Paso 1. Configuración de la red básica

**▸** Añadir los dispositivos:

- Dos rúteres (R1 y R2): coloca los rúteres en el espacio de trabajo.

- Dos PC (PC1 y PC2): coloca las PC en el espacio de trabajo.

- Cablear las conexiones: conecta los PC a las interfaces Ethernet de los rúteres utilizando cables Straight-Through.

Asignar direcciones IP a las interfaces:

**▸** Para R1:

- Ethernet 0/0: 192.168.1.1 /24 (conectado a PC1).

- Serial 0/0/0: 10.0.0.1 /30 (conectado a R2).

**▸** Para R2:

- Ethernet 0/0: 192.168.2.1 /24 (conectado a PC2).

- Serial 0/0/0: 10.0.0.2 /30 (conectado a R1).

**▸** Para PC1:

- IP: 192.168.1.2 /24

- Gateway: 192.168.1.1

**▸** Para PC2:

- IP: 192.168.2.2 /24

- Gateway: 192.168.2.1

Configurar las rutas estáticas: **▸** En R1, configura la ruta hacia la red de R2:

![image-10](images/image-10.png)

**▸** En R2, configura la ruta hacia la red de R1:

![image-11](images/image-11.png)

#### Paso 2. Configuración de la VPN en R1

Configurar ISAKMP (Fase 1): **▸** Configura el protocolo ISAKMP para la autenticación y cifrado. En R1:

![image-12](images/image-12.png)

Definir la clave precompartida: **▸** Configura la clave precompartida que se utilizará para la autenticación de la VPN. En R1:

![image-13](images/image-13.png)

Configurar IPsec (Fase 2): **▸** Define el conjunto de transformaciones para la fase 2 de IPsec:

![image-14](images/image-14.png)

Aplicar el Crypto Map en la interfaz serial:

**▸** Crea un Crypto Map y asóciala con la interfaz serial de R1:

![image-15](images/image-15.png)

Crear una lista de acceso para definir el tráfico permitido por la VPN:

**▸** En R1, crea una lista de acceso para especificar las redes que estarán protegidas por el túnel:

![image-16](images/image-16.png)

#### Paso 3. Configuración de la VPN en R2

Configurar ISAKMP (Fase 1) en R2:

**▸** Repite la configuración de ISAKMP en R2 para establecer la autenticación y cifrado.

En R2:

![image-17](images/image-17.png)

Definir la clave precompartida en R2: **▸** Configura la misma clave precompartida que en R1:

![image-18](images/image-18.png)

Configurar IPsec (Fase 2) en R2: **▸** Define el mismo conjunto de transformaciones en R2:

![image-19](images/image-19.png)

Aplicar el Crypto Map en la interfaz serial de R2: **▸** Crea el Crypto Map y asócialo con la interfaz serial de R2:

![Crear una lista de acceso en R2:](images/image-20.png)

**▸** En R2, crea una lista de acceso similar a la de R1:

![image-21](images/image-21.png)

#### Paso 4. Verificación de la conexión

**▸** Verificar la conexión VPN:

- Realiza un ping desde PC1 (ping 192.168.2.2) hacia PC2.

- Si todo está correctamente configurado, los pings deberían ser exitosos.

**▸** Verificar el estado de la VPN:

- Usa los siguientes comandos en los rúteres para verificar el estado de la VPN.

- En R1: show crypto isakmp sa y show crypto ipsec sa .

- En R2: show crypto isakmp sa y show crypto ipsec sa .

- Estos comandos deben mostrar que el túnel ISAKMP está activo y el túnel IPsec está establecido.

![Donde:](images/image-22.png)

**▸** dst *(destination):* la dirección IP del dispositivo remoto (el *peer* con el que estás configurando la VPN). **▸** src *(source):* la dirección IP del dispositivo local. **▸** state (estado): el estado de la asociación ISAKMP. Algunos posibles estados son:

- QM_IDLE : el túnel VPN está establecido correctamente y está en espera de tráfico.

- MM_ACTIVE : el túnel está activo y se está utilizando para la transmisión de datos.

- WAIT_FOR_NOTIFY : el dispositivo está esperando la notificación de cierre de la conexión.

**▸** role : indica si el dispositivo es el iniciador o el receptor de la conexión. Los posibles valores son:

- initiator : el dispositivo ha iniciado la negociación.

- responder : el dispositivo ha respondido a la solicitud.

**▸** username : si se ha configurado autenticación mediante un nombre de usuario, se muestra aquí. Si se utiliza una clave precompartida (PSK), este campo, generalmente, estará vacío.

#### Resultado final

**▸** Conectividad asegurada: los PC en ambas redes (PC1 y PC2) pueden comunicarse de manera segura a través del túnel VPN.

**▸** Seguridad en el tráfico: la comunicación entre las redes se cifra y protege utilizando IPsec.

**▸** Verificación exitosa: el estado de la VPN es correcto en ambos rúteres y los pings entre las PC son exitosos.

Este es el resultado esperado de la actividad de configuración de una VPN en Packet Tracer.

# Entrenamiento 2. Configuración básica de

# Cloudflare para la protección y optimización de un

# sitio web

#### ▸ Planteamiento del ejercicio

Para realizar esta actividad utilizando máquinas virtuales en VirtualBox, te propondré un entorno de simulación en el que configuraremos un servidor web que representará el sitio y usaremos Cloudflare para mejorar su seguridad y rendimiento.

Objetivo: el estudiante aprenderá a integrar Cloudflare en un sitio web utilizando el plan gratuito. Explorará las características básicas que proporciona Cloudflare, tales como protección contra ataques DDoS, caché para mejorar la velocidad y seguridad básica con HTTPS.

Requisitos previos:

**▸** Acceso a un sitio web propio o de pruebas (puede ser una instalación en un servidor local o en la nube).

**▸** Una cuenta de Cloudflare (se puede crear gratuitamente en <https://www.cloudflare.com/>.

**▸** Conocimientos básicos de configuración de DNS.

#### ▸ Desarrollo paso a paso

#### Paso 1. Creación de cuenta y agregación del sitio web a Cloudflare

**▸** Registro en Cloudflare: si no tiene una cuenta, el estudiante debe registrarse en el plan gratuito.

**▸** Agregar el sitio web: tras iniciar sesión, hacer clic en «Add a Site» y seguir las instrucciones para agregar el dominio del sitio.

**▸** Verificación DNS: Cloudflare escaneará automáticamente los registros DNS del dominio. Revisar y confirmar que están correctos.

**▸** Cambiar los *nameservers:* seguir las indicaciones de Cloudflare para actualizar los *nameservers* en el proveedor de dominio. Esto permitirá que Cloudflare gestione el tráfico del sitio.

#### Paso 2. Configuración básica de seguridad y rendimiento

**▸** Activar HTTPS (SSL/TLS): en el menú de SSL/TLS, configurar el certificado SSL en «Flexible» (opción recomendada para sitios que no tienen certificado SSL propio). Esto permite que el sitio cargue con HTTPS sin necesidad de un certificado en el servidor.

**▸** Configurar *firewall* básico: en la sección de «Firewall», crear una regla básica para bloquear IP sospechosas, si se detectan. Explorar cómo bloquear tráfico de regiones específicas o aplicar otras configuraciones de seguridad.

**▸** Activar caché y optimización: en el menú «Caching», habilitar la opción de caché para acelerar la carga del sitio. Activar «Auto Minify» para reducir el tamaño de archivos CSS, JS y HTML.

#### Paso 3. Prueba de configuración y validación

**▸** Pruebas de HTTPS: acceder al sitio utilizando https:// y comprobar que carga sin advertencias de seguridad.

**▸** Pruebas de *firewall:* usar una herramienta de análisis como <https://securityheaders.com> <https://securityheaders.com> para verificar que Cloudflare esté filtrando correctamente las conexiones y aplicando seguridad básica.

**▸** Verificación de caché: comprobar que Cloudflare está almacenando en caché los

Servicios en Red e Internet 42 Tema 10. Entrenamientos elementos del sitio, revisando en las herramientas del navegador la información de los recursos (deberían mostrar cf-cache-status: HIT ).

#### Paso 4. Documentación y conclusiones

**▸** Capturas de pantalla: documentar cada paso con capturas de pantalla (registro en Cloudflare, configuración de SSL, *firewall,* caché, pruebas de HTTPS). **▸** Reflexión: elaborar un breve informe con conclusiones sobre cómo Cloudflare ayuda a mejorar el rendimiento y seguridad del sitio.

#### ▸ Solución

Requisitos previos:

**▸** VirtualBox instalado en el equipo anfitrión.

**▸** Conexión a Internet.

**▸** Una cuenta de Cloudflare.

**▸** Un dominio registrado (puede ser uno gratuito o de bajo costo) o un subdominio de

un dominio existente.

#### Paso 1. Crear una máquina virtual para el servidor web

Crear una nueva máquina virtual en VirtualBox: **▸** Nombre: ServidorWeb. **▸** Tipo: Linux (puede ser Ubuntu o Debian, ya que son opciones comunes y compatibles con servidores web). **▸** Memoria: 1 GB (ajustable según los recursos disponibles).

**▸** Disco duro virtual: 10 GB.

Instalar el sistema operativo:

**▸** Instalar la distribución Linux (Ubuntu o Debian) en la máquina virtual.

**▸** Durante la instalación, habilitar el soporte de red y el servidor SSH.

Configurar la red de la VM:

**▸** En la configuración de la máquina virtual, ir a «Red» y configurar el adaptador de red

en modo «Adaptador puente» para que la máquina pueda ser accesible desde la red local.

#### Paso 2. Configuración del servidor web en la máquina virtual

Instalar Apache (servidor web): **▸** Inicia sesión en la VM y abre la terminal. **▸** Ejecuta los siguientes comandos para actualizar los repositorios e instalar Apache:

![image-23](images/image-23.png)

Configurar Apache: **▸** Verifica que Apache esté en funcionamiento ingresando la IP local de la VM en un navegador desde tu máquina anfitriona (ejemplo: <http://192.168.x.x>). Deberías ver la página de inicio de Apache.

Asignar un nombre de dominio (opcional):

**▸** Si tienes un dominio, apúntalo a la IP pública de tu red (o usa un subdominio existente).

**▸** Asegúrate de que el dominio esté correctamente registrado en tu cuenta de Cloudflare para que puedas utilizar sus servicios.

#### Paso 3. Configuración de Cloudflare

Crear cuenta en Cloudflare e iniciar sesión:

**▸** Ve al sitio de Cloudflare <https://www.cloudflare.com/> y crea una cuenta gratuita si aún no tienes una.

Agregar el sitio web a Cloudflare:

**▸** En el panel de Cloudflare, selecciona «Add a Site฀» e introduce el nombre de tu dominio.

**▸** Elige el plan gratuito para configurar los servicios básicos.

Revisar y modificar los registros DNS:

**▸** Cloudflare escaneará automáticamente los registros DNS de tu dominio. Confirma que los registros A o CNAME apunten a la IP de la máquina virtual (o la IP de tu red en el caso de pruebas con dominio público).

Cambiar los *nameservers* en tu proveedor de dominio:

**▸** Cloudflare te proporcionará sus *nameservers.* Accede a la configuración de tu dominio en tu proveedor y reemplaza los *nameservers* actuales por los que indica Cloudflare. Esto redirigirá el tráfico a través de Cloudflare.

#### Paso 4. Configuración de seguridad y rendimiento en Cloudflare

Configurar SSL/TLS: **▸** En el panel de Cloudflare, ve a la sección SSL/TLS y selecciona la opción «Flexible». Esto permite que Cloudflare gestione el HTTPS sin necesidad de un certificado en el servidor local.

Configurar el *firewall* de Cloudflare: **▸** Accede a la sección de «Firewall» y crea una regla de seguridad básica. Por ejemplo, puedes bloquear tráfico sospechoso o regiones específicas como práctica. Activar caché y optimización: **▸** En «Caching», activa la caché para reducir la carga en el servidor. **▸** En la opción «Auto Minify», habilita la reducción de tamaño para archivos CSS, JavaScript y HTML.

#### Paso 5. Comprobación de la configuración

Prueba de HTTPS: **▸** Ingresa a tu dominio desde un navegador. Debería cargar utilizando https:// con un candado que indique que la conexión es segura. Prueba de seguridad *(Firewall):* **▸** Utiliza <https://securityheaders.com> o una herramienta similar para verificar que Cloudflare esté protegiendo correctamente tu sitio y aplicando medidas de seguridad.

Verificación de caché:

**▸** Inspecciona el sitio en el navegador usando la herramienta de desarrolladores. En los encabezados de red, deberías ver cf-cache-status: HIT en algunos archivos, lo cual indica que Cloudflare está almacenando en caché.

#### Paso 6. Documentación y conclusiones

Capturas de pantalla:

**▸** Toma capturas de pantalla de cada paso, especialmente:

- Página de bienvenida de Apache.

- Configuraciones en Cloudflare (SSL, firewall, caché).

- Resultado de la prueba de seguridad y caché en el navegador.

# Entrenamiento 3. Implementación y Comprensión

# de servicios de Internet en la nube (Parte 1)

#### ▸ Planteamiento del ejercicio

El objetivo de esta actividad es que los estudiantes comprendan los componentes y la importancia de los servicios de Internet en la nube. A través de simulaciones y actividades prácticas, los estudiantes aprenderán sobre los proveedores de servicios de Internet (ISP) en la nube, el uso de redes de distribución de contenido (CDN), la implementación de servicios de DNS en la nube y las soluciones de protección contra ataques DDoS.

#### ▸ Desarrollo paso a paso

Investigar sobre los siguientes servicios:

**▸** Proveedores de servicios de Internet basados en la nube. ¿Qué son? ¿Cuáles son los principales proveedores? ¿Qué tecnologías utilizan para ofrecer acceso a Internet (por ejemplo, banda ancha, 4G/5G)?

**▸** Redes de distribución de contenido (CDN). ¿Qué es una CDN? ¿Cómo mejora la experiencia del usuario en la web? ¿Cuáles son los beneficios de implementar una CDN en un sitio web?

**▸** DNS en la nube. Explicar qué es el DNS en la nube, cómo funciona y por qué es importante para garantizar la alta disponibilidad y escalabilidad de los sitios web y aplicaciones.

**▸** Protección DDoS en la nube. ¿Qué es un ataque DDoS? ¿Cómo los servicios de protección DDoS en la nube ayudan a mitigar estos ataques?

Preparar un informe de una a dos páginas, explicando los conceptos anteriores y sus aplicaciones en la infraestructura de servicios en la nube.

#### ▸ Solución

#### Informe sobre servicios basados en la nube: proveedores, CDN, DNS y

#### protección DDoS

Introducción:

La infraestructura de servicios en la nube ha transformado la forma en que las empresas operan y ofrecen servicios en línea, proporcionando una mayor escalabilidad, disponibilidad y seguridad. Este informe aborda cuatro componentes fundamentales en la nube: proveedores de servicios de Internet, redes de distribución de contenido (CDN), DNS en la nube y protección DDoS, que son esenciales para optimizar el rendimiento y la seguridad de los servicios en línea.

Proveedores de servicios de Internet basados en la nube:

Los proveedores de servicios de Internet en la nube ofrecen plataformas que facilitan el acceso a Internet y conectividad a través de diversas tecnologías, como banda ancha, fibra óptica y redes móviles 4G/5G. Entre los principales proveedores se encuentran Amazon Web Services (AWS), Google Cloud Platform (GCP) y Microsoft Azure. Estas plataformas no solo proporcionan conectividad, sino también soluciones para almacenamiento, procesamiento de datos y herramientas de redes avanzadas que permiten a las empresas administrar sus recursos de forma remota. La tecnología de nube utilizada por estos proveedores asegura una conectividad rápida y confiable, especialmente beneficiosa para empresas que operan a nivel global.

Redes de distribución de contenido (CDN):

Una red de distribución de contenido (CDN) consiste en una red de servidores distribuidos en diversas ubicaciones globales, que almacenan copias en caché del contenido de un sitio web. Esto reduce el tiempo de carga y mejora la experiencia del usuario al servir el contenido desde el servidor más cercano al usuario final. Las CDN, como Cloudflare y Akamai, son esenciales para sitios con un alto volumen de tráfico o con usuarios distribuidos geográficamente, ya que optimizan la disponibilidad y el rendimiento del contenido, al mismo tiempo que reducen la carga en el servidor principal.

DNS en la nube:

El DNS (sistema de nombres de dominio) en la nube permite que las solicitudes de nombre de dominio se resuelvan de manera eficiente y rápida, dirigiendo a los usuarios al servidor más cercano o menos congestionado. Al operar en la nube, los servicios de DNS, como Amazon Route 53 o Google Cloud DNS, ofrecen alta disponibilidad y escalabilidad. Esto es crucial para empresas que dependen de una respuesta rápida y una operación ininterrumpida de sus aplicaciones, ya que el DNS en la nube permite redirigir el tráfico en tiempo real según sea necesario para evitar problemas de sobrecarga.

Protección DDoS en la nube:

Los ataques de denegación de servicio distribuido (DDoS) buscan sobrecargar un servidor con tráfico malicioso, lo que puede hacer que un sitio web o servicio se vuelva inaccesible. Los servicios de protección DDoS en la nube, como AWS Shield o Cloudflare DDoS Protection, utilizan herramientas avanzadas de detección y filtrado de tráfico para identificar patrones de ataque y bloquear el tráfico malicioso antes de que alcance el servidor de destino. Este tipo de protección es esencial para empresas que necesitan mantener la disponibilidad de sus servicios y protegerse contra interrupciones que puedan afectar la experiencia del usuario y la reputación de la empresa.

Conclusión:

La integración de proveedores de servicios en la nube, CDN, DNS y protección DDoS crea una infraestructura robusta que mejora la experiencia del usuario, asegura la disponibilidad continua y protege los recursos en línea contra amenazas externas. Las empresas que implementan estos servicios están mejor preparadas para enfrentar los desafíos de un entorno digital global y altamente competitivo, asegurando tanto el rendimiento como la seguridad de sus operaciones en la nube.

# Entrenamiento 4. Configuración de una VPN Site-

# to-Site en Microsoft Azure

#### ▸ Planteamiento del ejercicio

El objetivo de esta actividad es que el estudiante aprenda a configurar una VPN *Site‑to‑Site* en Microsoft Azure para conectar una red local con una red virtual en la nube de manera segura. Mediante esta actividad, se pretende que los estudiantes comprendan el proceso de configuración de una red privada virtual (VPN), el uso de subredes en la nube y la creación de una conexión segura entre una red local y una red en Azure.

Descripción de la actividad

Imagina que trabajas como administrador de sistemas en una empresa que necesita conectar su infraestructura local con servicios en la nube de Azure para permitir el acceso seguro a recursos compartidos. Tu tarea es establecer una VPN *Site‑to‑Site* entre la red local y una red en la nube configurada en Azure.

Sigue los pasos para realizar la configuración y verifica la conectividad para asegurar que los datos se transmiten de forma segura a través de la VPN. Posteriormente, deberás documentar el proceso y analizar los resultados obtenidos en términos de seguridad y rendimiento de la conexión.

#### ▸ Desarrollo paso a paso

Configuración de una Red Virtual en Azure:

**▸** Crea una red virtual (VNet) en Microsoft Azure con el rango de direcciones especificado.

**▸** Configura una subred dentro de esta VNet para organizar los recursos que se conectarán a la red local.

Creación de una VPN Gateway en Azure: **▸** Configura una Virtual Network Gateway en Azure para actuar como punto de conexión en la nube. **▸** Asegúrate de asignar una dirección IP pública a la *gateway.* Establecimiento de una conexión VPN *Site‑to‑Site:* **▸** Configura una conexión VPN de tipo *Site-to-Site* en la *gateway* de Azure. **▸** Configura la dirección IP pública de la red local y el rango de direcciones de la red en un Local Network Gateway en Azure. **▸** Asegúrate de establecer una clave compartida para la autenticación entre ambas redes. Configuración del dispositivo de red local: **▸** Configura tu rúter o *firewall* local para establecer una conexión IPSec con la VPN Gateway de Azure utilizando los parámetros configurados. Verificación de la conexión: **▸** Realiza pruebas de conectividad desde la red local a la red en Azure (ping y traceroute) para asegurar que la VPN está funcionando correctamente.

Documentación y análisis: **▸** Redacta un informe en el que describas todos los pasos realizados, las dificultades encontradas y las soluciones aplicadas. **▸** Analiza el rendimiento de la VPN, describiendo cualquier latencia observada y valorando la seguridad de la conexión establecida. Entregables: **▸** Informe detallado con capturas de pantalla que demuestren cada paso de la configuración y los resultados de las pruebas de conectividad. **▸** Análisis del rendimiento y la seguridad de la VPN, incluyendo recomendaciones para optimizar o mejorar la configuración si es necesario.

#### ▸ Solución

#### Paso 1. Crear una red virtual (VNet)

**▸** Accede a Azure: inicia sesión en tu cuenta de Microsoft Azure. **▸** Crear una red virtual:

- En el portal de Azure, selecciona «Create a resource» y busca «Virtual Network».

- Asigna un nombre a la red virtual (por ejemplo, VNet-Azure).

- Selecciona la región donde deseas crear la red.

- Define el rango de direcciones IPv4 (por ejemplo, 10.1.0.0/16) y haz clic en «Review + Create».

Crear subredes: **▸** En la configuración de la VNet, selecciona «Subnets» y haz clic en «+ Subnet». **▸** Asigna un nombre a la subred (por ejemplo, Subnet-01) y define el rango de direcciones (por ejemplo, 10.1.1.0/24). **▸** Haz clic en «OK» para crear la subred.

#### Paso 2. Crear una Gateway de red virtual

**▸** Crear una Gateway de red virtual:

- En el portal de Azure, ve a «Create a resource» y busca «Virtual Network Gateway».

- Asigna un nombre (por ejemplo, VPN-Gateway).

- En «Gateway type», selecciona «VPN» y en «VPN type», selecciona «Route‑based».

- Selecciona la SKU que deseas (estándar o más alta si es necesario).

- Elige la VNet que creaste anteriormente y selecciona la subred «GatewaySubnet» (si no existe, créala con un rango como 10.1.2.0/24).

- Haz clic en «Review + Create».

**▸** Asignar una IP pública a la Gateway:

- En la configuración de la Gateway, selecciona «IP Configuration» y haz clic en «Public IP address».

- Elige «Create new» y asígnale un nombre.

- Haz clic en «OK» y luego en «Create».

#### Paso 3.Configurar la conexión VPN

**▸** Crear una conexión VPN *Site-to-Site:*

- En el portal de Azure, dirígete a la «Virtual Network Gateway» que creaste y selecciona «Connections».

- Haz clic en «+ Add».

- Asigna un nombre a la conexión (por ejemplo, SiteToSiteConnection).

- En «Connection type», selecciona «Site-to-site (IPSec)».

**▸** Configurar el sitio local (Local Network Gateway):

- Si no has configurado un Local Network Gateway, selecciona «+ New» para crear uno.

- Asigna un nombre (por ejemplo, LocalGateway).

- Ingresa la dirección IP pública del dispositivo de tu red local (rúter o firewall).

- Define el rango de direcciones IP de tu red local (por ejemplo, 192.168.1.0/24).

- Haz clic en «OK» para crear el Local Network Gateway.

**▸** Configurar las claves de la conexión:

- En la sección de «Shared Key», ingresa una clave compartida (asegúrate de que esta clave coincida en ambos extremos, tanto en Azure como en tu red local).

- Haz clic en «OK» para crear la conexión VPN.

#### Paso 4. Configurar el dispositivo de red local para la conexión VPN

**▸** Acceder a tu rúter o *firewall* local:

- Configura tu rúter o firewall para establecer la conexión IPSec VPN.

**▸** Cargar la configuración de la VPN:

- Utiliza la dirección IP pública de la VPN Gateway de Azure y la clave compartida que configuraste.

- Asegúrate de que los protocolos de encriptación y autenticación coincidan con los de Azure.

#### Paso 5. Verificar la conectividad de la VPN

**▸** Verificar el estado de la conexión:

- En el portal de Azure, dirígete a la «Virtual Network Gateway» y selecciona «Connections».

- Asegúrate de que la conexión tenga el estado «Connected».

**▸** Prueba de conectividad:

- Desde un dispositivo de la red local, intenta hacer un ping a una IP de la subred de Azure (por ejemplo, 10.1.1.4) para confirmar que la VPN está operativa.

- Opcionalmente, puedes realizar trazas de red (traceroute) para verificar que el tráfico pasa por la VPN.

#### Paso 6. Documentación y análisis

**▸** Escribir un informe:

- Documenta los pasos de configuración, las pruebas de conectividad y cualquier problema o ajuste necesario para el correcto funcionamiento de la VPN.

**▸** Reflexionar sobre el rendimiento y seguridad:

- Describe el rendimiento de la VPN, así como los beneficios y limitaciones observados.

Esta solución permite establecer una conexión segura entre una red local y una red virtual en Azure, familiarizando a los usuarios con la configuración y uso de VPN en un entorno de nube.

# Entrenamiento 5. Implementación y análisis de

# una solución de telefonía IP en la nube (VoIP)

#### ▸ Planteamiento del ejercicio

En esta actividad, configuraremos un sistema de telefonía IP (VoIP) simulando una infraestructura básica de comunicaciones empresariales. Utilizando Packet Tracer, deberás implementar una PBX local que permita gestionar llamadas entre teléfonos IP dentro de una red simulada. Esta configuración imita las funcionalidades de un sistema de telefonía IP en la nube, destacando los beneficios de llamadas de voz sobre IP, administración centralizada de extensiones y funciones avanzadas de una PBX.

Objetivos:

**▸** Configurar un entorno de VoIP en una red interna, simulando las funciones de una PBX en la nube.

**▸** Asignar extensiones y establecer llamadas entre varios teléfonos IP.

**▸** Aplicar y entender conceptos como PBX, SIP *trunking* (opcional) y sus ventajas sobre los sistemas telefónicos tradicionales.

#### ▸ Desarrollo paso a paso

**▸** Configura una red en Packet Tracer que incluya un rúter, un *switch,* teléfonos IP, una computadora de administración y un servidor de CME (Call Manager Express) para gestionar las llamadas.

**▸** Asigna direcciones IP y configura el servicio de DHCP para que los teléfonos reciban su configuración IP automáticamente.

**▸** Configura el rúter como PBX, creando extensiones para cada teléfono y estableciendo las opciones básicas de comunicación.

**▸** Verifica la conectividad y funcionalidad haciendo llamadas entre los teléfonos IP configurados.

**▸** Documenta los pasos de configuración y realiza una breve reflexión sobre cómo una PBX en la nube ofrecería ventajas adicionales en un entorno de trabajo real. Contesta las siguientes preguntas: ¿Qué ventajas prácticas ofrece la telefonía IP en la nube en términos de movilidad, coste y mantenimiento? ¿Cómo beneficia la comunicación unificada a una empresa?

**Entrega:** capturas de pantalla de la configuración y respuestas a las preguntas de reflexión sobre los beneficios de una PBX en la nube frente a un sistema de telefonía tradicional.

#### ▸ Solución

#### Paso 1. Configuración del entorno

**▸** Abrir Packet Tracer y crear un nuevo proyecto.

**▸** Agregar dispositivos de red:

- Arrastra y suelta un rúter compatible con VoIP (por ejemplo, Cisco 2811).

- Añade un switch (por ejemplo, el modelo 2960).

- Añade tres teléfonos IP (Cisco IP Phone).

- Agrega una computadora para simular la consola de administración del servidor.

- Añade un servidor para usarlo como el Call Manager Express (CME), que actuará como nuestro sistema de conmutación PBX.

#### Paso 2. Conexión de dispositivos

**▸** Conecta los teléfonos IP y el servidor al *switch* mediante cables directos. **▸** Conecta el *switch* al rúter con un cable directo. **▸** Conecta la computadora al *switch* para configuraciones adicionales.

#### Paso 3. Configuración de direcciones IP

**▸** Asigna direcciones IP a los dispositivos en la misma red. Por ejemplo:

- Rúter (interfaz conectada al switch): IP 192.168.1.1

- Servidor: IP 192.168.1.10

- Teléfono IP1: IP 192.168.1.11

- Teléfono IP2: IP 192.168.1.12

- Teléfono IP3: IP 192.168.1.13

- Computadora: IP 192.168.1.20

**▸** Configura la puerta de enlace en los teléfonos y en el servidor como 192.168.1.1.

#### Paso 4. Configuración del rúter para CME (PBX)

- ▸ Haz clic en el rúter y ve a la pestaña de CLI.

- ▸ Ejecuta los siguientes comandos para habilitar el servicio VoIP:

![image-24](images/image-24.png)

- ▸ Estos comandos configuran el servicio de telefonía en el rúter, limitan a cinco

    - teléfonos IP y asignan automáticamente extensiones de llamada.

#### Paso 5. Configuración de extensiones para los teléfonos IP

- ▸ En el modo de configuración del rúter, asigna los números de directorio (DN) o

    - extensiones para los teléfonos:

        - Servicios en Red e Internet 62 Tema 10. Entrenamientos

![image-25](images/image-25.png)

**▸** Configura los teléfonos IP *(ephones)* para que utilicen las extensiones asignadas:

![image-26](images/image-26.png)

**Nota:** la dirección MAC de cada teléfono IP se puede obtener haciendo clic en el teléfono y revisando sus configuraciones.

#### Paso 6. Configuración de las opciones de DHCP en el rúter

- ▸ Habilita DHCP en el rúter para que los teléfonos reciban automáticamente sus

![image-27](images/image-27.png)

    - configuraciones IP y de TFTP.

- ▸ Esta configuración envía las direcciones IP y la dirección del TFTP (en este caso, la

    - dirección del rúter) a los teléfonos para que puedan acceder al CME.

#### Paso 7. Verificación de la configuración

- ▸ Guarda la configuración en el rúter:

![image-28](images/image-28.png)

- ▸ Ve a cada teléfono IP y verifica que haya recibido una dirección IP y el número de

    - extensión configurado.

- ▸ Realiza llamadas de prueba entre los teléfonos para verificar que las llamadas se

    - conecten correctamente. Intenta hacer una llamada de Teléfono IP1 (1001) a

    - Teléfono IP2 (1002) y verifica que suene.

        - Servicios en Red e Internet 64 Tema 10. Entrenamientos

#### Paso 8. Configuración de funciones adicionales

**▸** Para configurar funciones como reenvío de llamadas o conferencias, revisa la sección de «telephony-service» y ajusta los parámetros según sea necesario.

#### Paso 9. Reflexión y documentación

**▸** Documenta los pasos realizados y explica cómo la configuración simulada de una PBX en este entorno puede adaptarse a una configuración en la nube (PBX en la nube).

**¿Qué ventajas prácticas ofrece la telefonía IP en la nube en términos de**

#### movilidad, coste y mantenimiento?

**▸** Movilidad: la telefonía IP en la nube permite realizar y recibir llamadas desde cualquier lugar con una conexión a Internet, lo que ofrece una gran flexibilidad para los empleados que trabajan de forma remota o en diferentes ubicaciones. No se necesita estar conectado a una línea telefónica fija o a un dispositivo físico, como ocurre con la telefonía tradicional.

**▸** Coste: al basarse en Internet para la transmisión de voz, la telefonía IP en la nube reduce significativamente los costes asociados a las líneas telefónicas tradicionales y la infraestructura física de telecomunicaciones (por ejemplo, cables, centralitas, y equipos de mantenimiento). Además, las llamadas internacionales o de larga distancia suelen tener un coste mucho más bajo que en los sistemas tradicionales.

**▸** Mantenimiento: la telefonía en la nube elimina la necesidad de mantener *hardware* físico en las instalaciones, ya que el proveedor de servicios se encarga de la gestión, actualizaciones y soporte del sistema. Esto reduce los costes de mantenimiento interno y asegura que el sistema esté siempre actualizado sin intervención directa del personal de IT.

#### ¿Cómo beneficia la comunicación unificada a una empresa?

La comunicación unificada integra diferentes canales de comunicación (como llamadas de voz, correo de voz, videollamadas, mensajería instantánea y conferencias) en una sola plataforma, lo cual ofrece varias ventajas a las empresas:

**▸** Mejora de la eficiencia: los empleados pueden acceder a todas las herramientas de comunicación desde una sola interfaz, lo que ahorra tiempo al evitar la necesidad de cambiar entre diferentes aplicaciones o dispositivos.

**▸** Mayor colaboración: facilita la colaboración en tiempo real entre equipos, incluso si están distribuidos geográficamente. La posibilidad de realizar videollamadas, compartir documentos y mantener conversaciones instantáneas mejora la rapidez y la efectividad de las decisiones.

**▸** Reducción de costos: al centralizar todas las formas de comunicación, las empresas pueden reducir la necesidad de varias plataformas de mensajería, sistemas de correo electrónico y otros servicios de comunicación, lo que disminuye los costes de licencias y mantenimiento.

**▸** Mejor experiencia para el cliente: los equipos de atención al cliente pueden gestionar solicitudes a través de múltiples canales (voz, chat, correo electrónico) sin perder la continuidad de la interacción, mejorando la calidad del servicio al cliente.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–27)*
- A fondo  *(pp.28–32)*
- Entrenamientos  *(pp.33–66)*
- Servicios en Red e Internet 6 Tema 10. Material de estudio · Servicios en Red e Internet 7 Tema 10. Material de estudio · Servicios en Red e Internet 8 Tema 10. Material de estudio · Servicios en Red e Internet 9 Tema 10. Material de estudio · Servicios en Red e Internet 10 Tema 10. Material de estudio · Servicios en Red e Internet 11 Tema 10. Material de estudio · Servicios en Red e Internet 12 Tema 10. Material de estudio · Servicios en Red e Internet 13 Tema 10. Material de estudio · Servicios en Red e Internet 14 Tema 10. Material de estudio · Servicios en Red e Internet 15 Tema 10. Material de estudio · Servicios en Red e Internet 16 Tema 10. Material de estudio · Servicios en Red e Internet 17 Tema 10. Material de estudio · Servicios en Red e Internet 18 Tema 10. Material de estudio · Servicios en Red e Internet 20 Tema 10. Material de estudio · Servicios en Red e Internet 21 Tema 10. Material de estudio · Servicios en Red e Internet 22 Tema 10. Material de estudio · Servicios en Red e Internet 23 Tema 10. Material de estudio · Servicios en Red e Internet 24 Tema 10. Material de estudio · Servicios en Red e Internet 25 Tema 10. Material de estudio · Servicios en Red e Internet 26 Tema 10. Material de estudio · Servicios en Red e Internet 27 Tema 10. Material de estudio  *(pp.6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 20, 21, 22, 23, 24, 25, 26, 27)*
- Servicios en Red e Internet 28 Tema 10. A fondo · Servicios en Red e Internet 29 Tema 10. A fondo · Servicios en Red e Internet 30 Tema 10. A fondo · Servicios en Red e Internet 31 Tema 10. A fondo · Servicios en Red e Internet 32 Tema 10. A fondo  *(pp.28–32)*
- Servicios en Red e Internet 33 Tema 10. Entrenamientos · Servicios en Red e Internet 34 Tema 10. Entrenamientos · Servicios en Red e Internet 35 Tema 10. Entrenamientos · Servicios en Red e Internet 36 Tema 10. Entrenamientos · Servicios en Red e Internet 37 Tema 10. Entrenamientos · Servicios en Red e Internet 38 Tema 10. Entrenamientos · Servicios en Red e Internet 39 Tema 10. Entrenamientos · Servicios en Red e Internet 40 Tema 10. Entrenamientos · Servicios en Red e Internet 41 Tema 10. Entrenamientos · Servicios en Red e Internet 43 Tema 10. Entrenamientos · Servicios en Red e Internet 44 Tema 10. Entrenamientos · Servicios en Red e Internet 45 Tema 10. Entrenamientos · Servicios en Red e Internet 46 Tema 10. Entrenamientos · Servicios en Red e Internet 47 Tema 10. Entrenamientos · Servicios en Red e Internet 48 Tema 10. Entrenamientos · Servicios en Red e Internet 49 Tema 10. Entrenamientos · Servicios en Red e Internet 50 Tema 10. Entrenamientos · Servicios en Red e Internet 51 Tema 10. Entrenamientos · Servicios en Red e Internet 52 Tema 10. Entrenamientos · Servicios en Red e Internet 53 Tema 10. Entrenamientos · Servicios en Red e Internet 54 Tema 10. Entrenamientos · Servicios en Red e Internet 55 Tema 10. Entrenamientos · Servicios en Red e Internet 56 Tema 10. Entrenamientos · Servicios en Red e Internet 57 Tema 10. Entrenamientos · Servicios en Red e Internet 58 Tema 10. Entrenamientos · Servicios en Red e Internet 59 Tema 10. Entrenamientos · Servicios en Red e Internet 60 Tema 10. Entrenamientos · Servicios en Red e Internet 61 Tema 10. Entrenamientos · Servicios en Red e Internet 63 Tema 10. Entrenamientos · Servicios en Red e Internet 65 Tema 10. Entrenamientos · Servicios en Red e Internet 66 Tema 10. Entrenamientos  *(pp.33, 34, 35, 36, 37, 38, 39, 40, 41, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 63, 65, 66)*