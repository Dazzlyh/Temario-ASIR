## Tema 1

# Servicios en Red e Internet

# Tema 1. Conceptos básicos

# de redes e Internet

# índice

Esquema Material de estudio

## 1.1. Introducción y objetivos

## 1.2. Definiciones previas

## 1.3. Tipos de redes

## 1.4. Modelos OSI y TCP/IP

## 1.5. Protocolos del modelo TCP/IP

## 1.6. Diferencias entre el Modelo OSI y el Modelo TCP/IP

## 1.7. Referencias bibliográficas

A fondo

Conexión TCP y UDP pasos y diferencias

Modelo OSI explicación de las 7 capas

Redes de computadoras. Apuntes digitales

CCNA 1 and 2. (Cisco Networking Academy Program)

¿Qué es TCP/IP? La columna vertebral de Internet

Entrenamientos Entrenamiento 1. Cuestionario sobre el Modelo OSI Entrenamiento 2. Configuración y verificación de direcciones IPv4 e IPv6 Entrenamiento 3. Evaluación de conceptos sobre modelos TCP/IP, OSI y protocolos. Entrenamiento 4. Investiga los modelos TCP/IP y OSI a través de Cisco Packet Tracer Entrenamiento 5. Mostrar elementos de la suite de protocolos TCP/IP a través de Cisco Packet Tracer

# Esquema

![image-2](images/image-2.png)

Servicios en Red e Internet 4 Tema 1. Esquema

# 1.1. Introducción y objetivos

Las redes de ordenadores son la columna vertebral de la comunicación moderna, facilitando la **interconexión de dispositivos**

y el **intercambio de información** a

nivel local, nacional e internacional. En el corazón de estas redes se encuentran conceptos fundamentales como puertos físicos y lógicos, datagramas, NAT y protocolos. Estos elementos juegan un papel crucial en la forma en que se envían y reciben datos y en cómo se asegura la **conectividad y seguridad** de las redes.

Un **puerto físico** se refiere a una interfaz tangible en un dispositivo de red, como un rúter o *switch,* que permite la conexión de cables físicos para la transmisión de datos. Estos puertos, que pueden ser de diferentes tipos como Ethernet o USB, son esenciales para establecer la **infraestructura física de una red.**

Por otro lado, un **puerto lógico** es un concepto abstracto que identifica servicios y procesos específicos dentro de una red mediante números asignados. Los puertos lógicos permiten que múltiples aplicaciones

y servicios coexistan en un solo

dispositivo, por lo tanto, gestionan conexiones simultáneas de manera eficiente.

Los **datagramas,** unidades de datos independientes enviadas a través de una red, son fundamentales para el funcionamiento de los protocolos, como el protocolo de Internet (IP). Estos paquetes de datos no previamente y pueden tomar rutas diferentes

requieren una conexión establecida para llegar a su destino, lo que

proporciona flexibilidad y robustez a la red. Sin embargo, esto también presenta desafíos en términos de asegurar la entrega confiable y en orden de los datos.

La **traducción de direcciones de red** (NAT) es otro concepto crucial, que permite que múltiples dispositivos en una red local compartan una única dirección IP pública para acceder a Internet. NAT ayuda a conservar las direcciones IPv4 y proporciona una capa adicional de seguridad al ocultar las direcciones IP internas de la red.

Finalmente, los protocolos son conjuntos de reglas que facilitan la comunicación entre dispositivos diversos, garantizando la interoperabilidad y la correcta transmisión de datos. Desde el protocolo HTTP/HTTPS para la navegación web hasta TCP/IP para la transmisión de datos, cada protocolo cumple una función específica en el ecosistema de redes.

La comprensión de los **modelos OSI** y **TCP/IP** es esencial para el diseño, implementación y gestión efectiva de las redes modernas. Estos modelos, que surgieron en momentos históricos distintos y con propósitos variados, han influido profundamente en la forma en que los datos se transmiten y se gestionan a través de las redes globales.

Ambos modelos han dejado una huella duradera en la arquitectura de redes. El OSI proporciona una referencia conceptual que ayuda a entender los principios subyacentes de la comunicación en red, mientras que el TCP/IP ofrece una implementación práctica que facilita la conectividad global. Comprender estos modelos no solo es fundamental para el diseño de redes y la resolución de problemas, sino también para anticipar y adaptarse a las evoluciones tecnológicas en el campo de las redes de comunicación.

Comprender estos conceptos no solo es fundamental para la gestión y administración de redes, sino también para asegurar su funcionamiento eficiente y seguro en un entorno globalizado.

Los **objetivos** que se pretende alcanzar en este tema son:

**▸** Comprender la distinción entre puertos físicos y lógicos.

**▸** Identificar los rangos de puertos lógicos y sus usos.

**▸** Entender el concepto y funcionamiento de los datagramas.

**▸** Explorar el proceso de traducción de direcciones de red (NAT).

**▸** Definir y clasificar protocolos de comunicación.

**▸** Estudiar protocolos comunes y sus funciones.

**▸** Explorar los diferentes tipos de redes de ordenadores.

**▸** Comprender la estructura de redes.

**▸** Distinguir entre modelos OSI y TCP/IP.

**▸** Conocer las funciones de cada capa.

**▸** Aplicar protocolos y tecnologías.

**▸** Evaluar direccionamiento y enrutamiento.

**▸** Comparar métodos de acceso a la red.

**▸** Desarrollar habilidades de diagnóstico.

**▸** Prepararse para el futuro de las redes.

# 1.2. Definiciones previas

¿Qué es un puerto físico y lógico?

#### Puerto físico

Un puerto físico se refiere a una **interfaz tangible** en un dispositivo de red, como un rúter, un *switch* o una computadora, que permite la conexión de cables físicos para transmitir datos. Estos puertos son cruciales para establecer la **conectividad en una** **red** y pueden ser de diversos tipos, como Ethernet, puerto serie, USB, HDMI, entre otros. Cada tipo de puerto físico está diseñado para una **función específica** y cumple con ciertos **estándares** de transmisión de datos.

Por ejemplo, en un entorno de red local (LAN), los puertos Ethernet son los más comunes. Estos puertos permiten la conexión de dispositivos de red mediante cables Ethernet, que son capaces de transmitir datos a velocidades que pueden variar desde 10 Mbps hasta 100 Gbps, dependiendo de la tecnología utilizada. Los puertos físicos son esenciales para la infraestructura de la red, ya que sin ellos no sería posible establecer la conectividad física entre los diferentes dispositivos.

![Figura 1. Puertos de una computadora. Fuente: Proceso Fernandez, 2013.](images/image-3.png)

*Figura 1. Puertos de una computadora. Fuente: Proceso Fernandez, 2013.*

#### Puerto lógico

El puerto lógico, en cambio, es un **concepto abstracto** en el ámbito de las redes de computadoras, que se refiere a un número asignado de **procesos o servicios** **específicos** que se ejecutan en un dispositivo. Los puertos lógicos permiten que los dispositivos de red gestionen múltiples conexiones y servicios simultáneamente. Los puertos lógicos son **identificadores numéricos** que oscilan entre 0 y 65 535; cada puerto puede estar asociado a un protocolo o servicio específico. Se dividen en tres rangos principales: puertos reservados, puertos registrados y puertos efímeros.

**▸ Puertos reservados (0-1023).** Los puertos del 0 al 1023 se conocen como puertos reservados o puertos bien conocidos. Estos puertos están asignados a servicios y protocolos específicos que son estándar en toda la industria. Estos números de puerto están regulados por la Internet Assigned Numbers Authority (IANA), la organización encargada de la gestión global de los identificadores de Internet, incluidos los números de puerto.

Por ejemplo, el puerto 80 está generalmente asociado con el protocolo HTTP, que se utiliza para la navegación web, mientras que el puerto 443 se asocia con HTTPS, la versión segura de HTTP. Otros puertos comunes incluyen el puerto 21 para FTP (File Transfer Protocol) y el puerto 25 para SMTP (Simple Mail Transfer Protocol), que se utiliza para el envío de correos electrónicos.

Estos puertos lógicos permiten que los dispositivos diferencien entre varios servicios y aplicaciones que se ejecutan al mismo tiempo, asegurando que los datos lleguen al proceso o servicio correcto.

**▸ Puertos registrados (1024-49 151).** Los puertos del 1024 al 49 151 se denominan puertos registrados. Estos puertos no son estándar, pero están registrados en la IANA para su uso por aplicaciones o servicios específicos. A diferencia de los puertos reservados, los puertos registrados no están restringidos a protocolos fundamentales y pueden ser utilizados por aplicaciones desarrolladas por terceros.

Por ejemplo, muchas aplicaciones de *software* pueden solicitar un puerto registrado para garantizar que otros servicios asignado, lo que previene conflictos y asegura puedan funcionar correctamente en una red servicios.

no utilicen su puerto que las aplicaciones sin interferir con otros

**▸ Puertos efímeros (49 152-65 535).** Los puertos del 49 152 al 65 535 se conocen como puertos efímeros o puertos dinámicos. Estos puertos se utilizan temporalmente, principalmente por clientes de red, como navegadores web, clientes de correo electrónico o clientes de FTP, para establecer conexiones hacia los servidores. Cuando un cliente desea conectarse a un servidor, selecciona aleatoriamente un puerto efímero para iniciar la conexión. Este puerto temporal se utiliza durante la sesión de comunicación. Una vez que la sesión termina, el puerto se libera y puede ser reutilizado por otra aplicación o protocolo en una conexión posterior. Este mecanismo de puertos efímeros permite que los clientes manejen múltiples conexiones simultáneas sin conflicto.

La gestión de puertos lógicos es crucial para la seguridad de la red. Los administradores de sistemas pueden bloquear o abrir puertos según sea necesario para controlar qué servicios pueden ser accedidos desde fuera de la red, ayudando así a prevenir accesos no autorizados y ataques cibernéticos.

¿Qué es un datagrama?

Un datagrama es una **unidad de datos** que se transmite a través de una red de conmutación de paquetes, como Internet. Se puede entender como una «caja» que contiene la información que se quiere enviar, junto con la información necesaria para que llegue a su destino, como las direcciones IP de origen y destino y otros metadatos. Los datagramas son fundamentales en el funcionamiento de protocolos

Servicios en Red e Internet 11 Tema 1. Material de estudio como el protocolo de Internet (IP), que es la base sobre la cual se construye la transmisión de datos en la red.

A diferencia de una transmisión basada en circuitos, donde se establece una conexión directa y continua entre el emisor y el receptor, el envío de datagramas no requiere una conexión establecida previamente. Cada datagrama se envía de forma **independiente** y puede tomar diferentes rutas a través de la red para llegar a su destino. Este enfoque tiene la ventaja de ser más **robusto y flexible,** ya que la red puede adaptar el camino de los datagramas en función del tráfico y las condiciones actuales.

Sin embargo, el uso de datagramas también presenta **desafíos,** especialmente, en cuanto a la entrega confiable y en orden. Dado que los datagramas pueden llegar en cualquier orden y algunos pueden perderse durante el proceso, los protocolos de nivel superior, como TCP (Transmission Control Protocol), se utilizan para garantizar que los datos se reciban de manera completa y ordenada.

![Figura 2. Datagrama IP. Fuente: Higueras, 2023.](images/image-4.png)

*Figura 2. Datagrama IP. Fuente: Higueras, 2023.*

¿Qué es un NAT y cuáles son sus aplicaciones?

NAT o Network Address Translation (traducción de direcciones de red) es un proceso utilizado en redes de computadoras para **modificar la dirección IP** en los paquetes de datos que pasan a través de un rúter o un cortafuegos. Su principal **objetivo** es permitir que múltiples dispositivos en una red local (LAN) compartan una única dirección IP pública para acceder a Internet,

resolviendo, así, la escasez de

direcciones IPv4 y proporcionando un nivel adicional de seguridad.

#### Funcionamiento del NAT

El NAT funciona **interceptando los paquetes**

que salen de la red local hacia

Internet. Cuando un dispositivo dentro de la LAN envía un paquete a una dirección IP externa, el rúter NAT sustituye la dirección IP privada del dispositivo (por ejemplo, 192.168.1.2) con la dirección IP pública del rúter antes de enviar el paquete a su destino. Cuando se recibe la respuesta, el

rúter realiza el proceso inverso,

sustituyendo la dirección IP pública con la dirección IP privada del dispositivo que inició la solicitud y luego reenvía el paquete a ese dispositivo.

Existen diferentes **tipos de NAT,** entre los cuales los más comunes son:

**▸ NAT estático:** asocia una única dirección IP privada a una dirección IP pública específica. Se utiliza en casos donde se necesita una IP pública fija para un dispositivo en particular.

**▸ NAT dinámico:** asocia una dirección IP privada a una de un conjunto de direcciones IP públicas disponibles. Es más flexible que el NAT estático, pero requiere más direcciones IP públicas.

**▸ PAT (Port Address Translation):** también conocido como NAT sobrecargado, permite que múltiples dispositivos compartan una sola dirección IP pública utilizando números de puerto para diferenciar entre las conexiones. Es la forma más común de NAT utilizada en redes domésticas y pequeñas empresas.

#### Aplicaciones del NAT

**▸ Ahorro de direcciones IP.** En un contexto donde las direcciones IPv4 son limitadas, el NAT permite que múltiples dispositivos en una red privada utilicen una única dirección IP pública para acceder a Internet, optimizando así el uso de las direcciones IP disponibles.

**▸ Seguridad.** El NAT también proporciona una capa de seguridad básica, ya que oculta las direcciones IP internas de la red. Los dispositivos externos no pueden acceder directamente a los dispositivos en la red privada, a menos que se configure un reenvío de puertos específico.

**▸ Facilidad de administración de red.** Permite a las organizaciones cambiar las direcciones IP internas sin afectar la configuración externa o pública, lo que facilita la reestructuración de la red interna sin causar interrupciones en el acceso a Internet.

**▸ Implementación de políticas de acceso.** Las organizaciones pueden utilizar NAT para restringir el acceso a Internet de ciertos dispositivos o para priorizar el tráfico de datos, implementando políticas que optimicen el uso de los recursos de la red.

¿Qué es un protocolo?

Un protocolo, en el contexto de las redes de computadoras, es un conjunto de **reglas** **y convenciones** que determinan **cómo se transmiten los datos** entre diferentes dispositivos en una red. Los protocolos son esenciales para garantizar que los dispositivos —fabricados, a menudo, por diferentes proveedores y que utilizan diferentes sistemas operativos— puedan comunicarse de manera efectiva y sin errores.

#### Características de los protocolos

**▸ Estándares de comunicación:** los protocolos definen cómo se estructura, empaqueta y transmite la información. Esto incluye la sintaxis (estructura de los datos), la semántica (significado de cada parte de la información) y el tiempo (sincronización de la comunicación).

**▸ Interoperabilidad:** gracias a los protocolos, dispositivos de distintos fabricantes pueden comunicarse entre sí. Por ejemplo, un navegador web en una computadora puede solicitar información de un servidor web que corre en una arquitectura completamente diferente, siempre y cuando ambos utilicen el mismo protocolo, como HTTP o HTTPS.

**▸ Fiabilidad:** algunos protocolos, como TCP, incluyen mecanismos para asegurar que los datos lleguen a su destino de manera completa y en el orden correcto. Otros protocolos, como UDP, no garantizan la entrega, pero ofrecen una mayor velocidad en la transmisión, siendo útiles en aplicaciones donde la velocidad es más importante que la fiabilidad (por ejemplo, en transmisiones de vídeo en vivo).

Ejemplos de protocolos

-HTTP/HTTPS (HyperText Transfer

Protocol/Secure): utilizado,

principalmente, para la transmisión de páginas web. HTTPS es la versión segura de HTTP, en la que los datos están cifrados para proteger la privacidad y la integridad de la información.

-TCP/IP (Transmission Control Protocol/Internet Protocol): el conjunto de protocolos más importante en Internet. TCP se encarga de dividir los datos en pequeños paquetes y asegurarse de

que lleguen correctamente,

mientras que IP se encarga de enrutar los paquetes a su destino.

-FTP (File Transfer Protocol): utilizado para la transferencia de archivos entre sistemas en una red.

-SMTP (Simple Mail Transfer Protocol): usado para el envío de correos electrónicos.

¿Qué son las redes de ordenadores?

Una red de ordenadores es un conjunto de **dispositivos conectados entre sí para** **compartir recursos,** como archivos, impresoras, conexiones a Internet, etc., y permitir la comunicación entre los dispositivos. Las redes de ordenadores pueden variar en tamaño desde una red de área personal (PAN), como la que conecta dispositivos en un espacio muy reducido, hasta redes globales como Internet.

#### Tipos de redes

**▸ LAN (Local Area Network).** Una LAN conecta dispositivos en un área geográfica limitada, como una casa, oficina o edificio. Es el tipo de red más común que, generalmente, utiliza tecnologías como Ethernet o wifi para la transmisión de datos.

**▸ WAN (Wide Area Network).** Una WAN cubre una gran área geográfica, que puede incluir ciudades, países o, incluso, continentes. Las WAN conectan múltiples redes LAN y otras redes más pequeñas. Un ejemplo de WAN es Internet, la red global que conecta millones de redes y dispositivos en todo el mundo. Las WAN suelen utilizar enlaces de telecomunicaciones, como líneas telefónicas, cables de fibra óptica o enlaces satelitales para facilitar la conexión entre las redes distantes.

**▸ MAN (Metropolitan Area Network).** Una MAN es una red que cubre un área geográfica más grande que una LAN, pero más pequeña que una WAN, como una ciudad o un campus universitario. Las MAN conectan varias redes LAN dentro de una ciudad o una región, permitiendo una comunicación y una transferencia de datos más rápida y eficiente en comparación con una WAN.

**▸ PAN (Personal Area Network).** Una PAN es una red pequeña que conecta dispositivos en un área personal, generalmente dentro de unos pocos metros, como en una habitación. Un ejemplo típico de PAN es la conexión entre un teléfono móvil y unos auriculares *bluetooth* o la sincronización de un reloj inteligente con un teléfono.

**▸ SAN (Storage Area Network).** Una SAN es una red especializada que proporciona acceso a almacenamiento de datos a nivel de bloque. Las SAN son utilizadas, principalmente, en entornos empresariales para conectar servidores a dispositivos de almacenamiento, como matrices de discos, facilitando una gestión más eficiente y flexible de grandes volúmenes de datos.

**▸ VPN (Virtual Private Network).** Una VPN es una red privada que se extiende sobre una red pública, como Internet, y permite a los usuarios enviar y recibir datos como si sus dispositivos estuvieran conectados directamente a la red privada. Las VPN son utilizadas comúnmente para asegurar la conexión de datos y proteger la privacidad, especialmente cuando se accede a la red corporativa desde ubicaciones remotas.

# 1.3. Tipos de redes

Las redes de ordenadores pueden clasificarse de diversas maneras, según diferentes criterios. A continuación, se presentan las clasificaciones más comunes:

Tipos de redes por su alcance

**▸ PAN (Personal Area Network).** Son redes de corto alcance, generalmente dentro de un rango de unos pocos metros. Conectan dispositivos personales como teléfonos, tabletas, auriculares y otros accesorios. Ejemplo típico es la conexión *bluetooth* entre un móvil y unos auriculares.

**▸ LAN (Local Area Network).** Conecta dispositivos dentro de un área geográfica limitada, como una casa, oficina o edificio. Es común en entornos domésticos y empresariales, utilizando tecnologías como Ethernet o wifi. Facilita la comunicación interna y el acceso compartido a recursos como archivos o impresoras.

**▸ MAN (Metropolitan Area Network).** Cubre un área geográfica más extensa que una LAN, como una ciudad o un campus universitario. Conecta múltiples LAN en una región específica y ofrece servicios de red a gran escala.

**▸ WAN (Wide Area Network).** Se extiende sobre áreas geográficas amplias, como países o continentes. Interconecta varias LAN y MAN, y un ejemplo destacado es Internet, la red global que conecta millones de dispositivos y redes en todo el mundo.

**▸ GAN (Global Area Network).** Similar a una WAN, pero a una escala global. Interconecta redes a través de grandes distancias geográficas, utilizando una variedad de medios de transmisión, incluidos satélites.

Tipos de redes por su conexión

**▸ Redes cableadas:** utilizan cables físicos (como cables de cobre o fibra óptica) para conectar los dispositivos. Ofrecen alta velocidad y estabilidad en la transmisión de datos, siendo comunes en LAN.

**▸ Redes inalámbricas:** utilizan ondas de radio, infrarrojos o microondas para la transmisión de datos, sin necesidad de cables físicos. Las redes wifi son un ejemplo típico. Ofrecen movilidad y facilidad de instalación, aunque pueden estar sujetas a interferencias y fluctuaciones en la velocidad.

Tipos de redes por su topología

**▸ Topología en estrella:** todos los dispositivos están conectados a un dispositivo central (como un *switch* o hub). Es fácil de gestionar y escalar, aunque depende del nodo central; si esta falla, toda la red se ve afectada.

**▸ Topología en bus:** todos los dispositivos comparten un único canal de comunicación (generalmente un cable). Es sencilla y económica, pero el rendimiento disminuye a medida que se añaden más dispositivos.

**▸ Topología en anillo:** los dispositivos están conectados en un bucle cerrado, donde cada dispositivo está conectado a dos otros. El tráfico de datos circula en una dirección específica. Aunque es eficiente, un fallo en cualquier punto puede afectar a toda la red.

**▸ Topología en malla:** cada dispositivo se conecta a varios otros, creando múltiples rutas para el tráfico de datos. Ofrece alta redundancia y es robusta frente a fallos, pero es costosa y compleja de instalar.

**▸ Topología híbrida:** combina dos o más topologías para aprovechar sus ventajas respectivas. Por ejemplo, una red puede combinar una topología en estrella con una topología en bus.

![Figura 3. Topología de redes. Fuente: Topología de red, 2024.](images/image-5.png)

*Figura 3. Topología de redes. Fuente: Topología de red, 2024.*

Tipos de redes por su relación funcional

**▸ Redes** ***peer-to-peer*** **(P2P):** todos los dispositivos en la red tienen roles iguales. No hay servidores dedicados y cada dispositivo puede actuar como cliente y servidor. Es simple y adecuada para pequeñas redes, pero no escala bien.

**▸ Redes cliente-servidor:** se basa en uno o más servidores que proporcionan servicios a múltiples clientes. Es común en entornos empresariales, donde la seguridad, la administración centralizada y el acceso a recursos compartidos son críticos.

Tipos de redes por la dirección de los datos

**▸ Redes simplex:** la comunicación de datos es unidireccional, es decir, los datos solo fluyen en una dirección. Un ejemplo es la transmisión de televisión, donde las señales se envían desde la estación de transmisión al receptor, sin retorno de datos.

**▸ Redes** ***half-duplex:*** la comunicación es bidireccional, pero los datos solo pueden viajar en una dirección a la vez. Un ejemplo típico es el uso de *walkie-talkies.*

**▸ Redes** ***full-duplex:*** permiten la transmisión de datos en ambas direcciones simultáneamente. Este tipo de red es el más eficiente y se utiliza en la mayoría de las comunicaciones modernas, como las llamadas telefónicas y las conexiones de red.

Tipos de redes por su grado de autenticación y difusión

**▸ Redes privadas:** son redes cerradas donde solo los usuarios autenticados pueden acceder. Se utilizan en entornos empresariales para proteger datos sensibles y limitar el acceso a usuarios autorizados.

**▸ Redes públicas:** son accesibles por cualquier persona y generalmente no requieren autenticación. Un ejemplo son las redes wifi públicas, que se encuentran en lugares como cafeterías o aeropuertos.

**▸ Redes virtuales privadas (VPN):** utilizan infraestructuras públicas (como Internet) para crear una red privada. Ofrecen acceso remoto seguro a los recursos de la red interna, cifrando el tráfico de datos para proteger la información.

Tipos de redes por el servicio o función que desempeña

**▸ Redes de acceso:** proporcionan conectividad inicial a dispositivos y usuarios, permitiendo el acceso a una red más grande. Ejemplo de estas redes son las redes de acceso de banda ancha que conectan hogares y empresas a Internet.

**▸ Redes de distribución:** distribuyen el tráfico de datos entre diferentes áreas o segmentos de la red. Son esenciales en la infraestructura de redes empresariales para gestionar y dirigir el tráfico de manera eficiente.

**▸ Redes de core o núcleo:** son el corazón de una red grande, proporcionando alta capacidad y rendimiento para el enrutamiento y la transmisión de grandes volúmenes de datos. Estas redes interconectan diferentes redes de acceso y distribución.

**▸ Redes de almacenamiento (SAN):** diseñadas para manejar el tráfico de almacenamiento de datos, proporcionan acceso a dispositivos de almacenamiento compartido a través de redes de alta velocidad.

**▸ Redes de contenido (CDN):** optimizan la entrega de contenido digital, como vídeos o archivos grandes, distribuyendo el contenido en múltiples servidores para reducir la latencia y mejorar la experiencia del usuario.

# 1.4. Modelos OSI y TCP/IP

El modelo OSI (Open Systems Interconnection)

y el modelo TCP/IP son

fundamentales para la comunicación en redes de ordenadores, aunque su historia y desarrollo reflejan enfoques muy diferentes.

Modelo OSI (interconexión de sistemas abiertos)

#### Contexto y origen

El modelo OSI (Open Systems Interconnection) nació en la década de 1970, en un momento en que las redes de comunicación

estaban en auge, pero la

**interoperabilidad** entre diferentes sistemas de redes era un gran **desafío.** Cada fabricante de equipos de red desarrollaba sus propios protocolos y estándares, lo que resultaba en sistemas cerrados que no podían comunicarse entre sí.

Ante esta fragmentación, la Organización Internacional de Normalización (ISO) decidió desarrollar un **modelo de referencia** que pudiera ser adoptado globalmente para estandarizar la comunicación entre sistemas consolidó en **1984** con la publicación del modelo OSI.

diferentes. Este esfuerzo se

E l **modelo final** consta de siete capas (física, enlace de datos, red, transporte, sesión, presentación y aplicación), proporcionando un marco teórico que define cómo deben interactuar los diferentes componentes de la red. Aunque el modelo OSI no fue adoptado universalmente en su totalidad, se

convirtió en una herramienta

educativa crucial y en un referente conceptual para el diseño de protocolos y redes.

#### Capas modelo OSI

El modelo OSI (Open Systems Interconnection) organiza las funciones de red en siete capas, cada una de las cuales tiene un rol específico en la transmisión y recepción de datos. Estas capas trabajan en conjunto para permitir la comunicación entre dispositivos en una red. A continuación, te explico cada una de las capas del modelo OSI:

**▸ Capa física:** esta es la capa más baja del modelo OSI y se encarga de la transmisión de bits (0 y 1) a través del medio físico. Define las características del *hardware* de la red, como cables, conectores, voltajes, y señales eléctricas. Ejemplos: cables de cobre, fibra óptica, señales de radio (wifi), conectores, *hubs.*

**▸ Capa de enlace de datos:** proporciona una transferencia de datos fiable entre dos nodos conectados físicamente. Se encarga de la detección y corrección de errores en la capa física y del control de acceso al medio de transmisión. Ejemplos: direcciones MAC, *switches,* protocolos como Ethernet, PPP (Point-to-Point Protocol). Subcapas:

- Control de acceso al medio (MAC): maneja el acceso al medio físico y controla cómo los dispositivos en la red acceden al canal compartido.

- Control de enlace lógico (LLC): gestiona la comunicación entre las capas superiores y el subnivel MAC y proporciona servicios como el control de errores y el control de flujo.

**▸ Capa de red:** es responsable del enrutamiento y direccionamiento de los paquetes de datos entre nodos que pueden estar en diferentes redes. Esta capa determina la mejor ruta para que los datos lleguen a su destino. Elementos clave: dirección lógica (direcciones IP) y enrutamiento de paquetes. Ejemplos: Direcciones IP, rúteres, protocolos como IP (Internet Protocol), ICMP (Internet Control Message Protocol).

**▸ Capa de transporte:** asegura la transferencia fiable de datos entre dispositivos finales en la red. Esta capa gestiona el control de flujo, el control de errores y la segmentación de datos en paquetes que luego se reensamblan en el destino. Ejemplos: TCP, UDP, puertos de comunicación. Protocolos principales:

- TCP (Transmission Control Protocol): proporciona una comunicación fiable con control de flujo y corrección de errores.

- UDP (User Datagram Protocol): proporciona una comunicación rápida, pero no garantizada, sin control de flujo ni corrección de errores.

**▸ Capa de sesión:** establece, gestiona y finaliza las sesiones entre aplicaciones que se están comunicando en diferentes dispositivos. Permite la sincronización de la comunicación y el control de diálogo entre aplicaciones. Ejemplos: manejo de sesiones en protocolos como RPC (Remote Procedure Call), NetBIOS.

**▸ Capa de presentación:** traduce los datos entre el formato utilizado por la red y el formato utilizado por la aplicación. Se encarga del cifrado, compresión y conversión de formatos de datos (como de texto a binario y viceversa). Ejemplos: SSL/TLS para cifrado, JPEG para imágenes, ASCII para texto.

**▸ Capa de aplicación:** es la capa más alta del modelo OSI y proporciona servicios de red directamente a las aplicaciones del usuario. Esta capa interactúa con el *software* de la aplicación y gestiona la interacción del usuario con la red. Ejemplos: Protocolos como HTTP (para la web), FTP (para la transferencia de archivos), SMTP (para el correo electrónico), DNS (para la resolución de nombres de dominio).

![Figura 4. Capas modelo OSI. Fuente: Cyberprimo, s.f.](images/image-6.png)

*Figura 4. Capas modelo OSI. Fuente: Cyberprimo, s.f.*

Arquitectura TCP/IP. Arpanet

#### Contexto y origen

El modelo TCP/IP (Transmission Control Protocol/Internet Protocol) tiene su origen en un proyecto del Departamento de Defensa de Estados Unidos durante la Guerra Fría. A finales de la década de 1960, la Advanced Research Projects Agency (ARPA), una agencia del Pentágono, comenzó a trabajar en una red de comunicaciones que pudiera resistir fallos y continuara operando, incluso en caso de ataques nucleares. Este proyecto llevó al desarrollo de **ARPANET,** la primera red de conmutación de paquetes.

En 1973, **Vint Cerf** y **Bob Kahn,** dos pioneros en el campo de las redes de comunicación, desarrollaron los conceptos fundamentales del protocolo TCP/IP. La primera versión del TCP se completó en 1974 y en 1978 se separaron sus funciones en dos protocolos: TCP, que maneja el control de la transmisión e IP, que se encarga del direccionamiento y el enrutamiento.

A medida que ARPANET crecía, la necesidad de un estándar para la comunicación entre redes diferentes se hizo evidente. **TCP/IP** fue adoptado como el **estándar para** **la comunicación** en ARPANET en 1983, lo que marcó un hito crucial en su historia.

El modelo TCP/IP no fue diseñado como un modelo de capas teórico, sino como una solución pragmática a los problemas de interconexión de redes. Sus cuatro capas (acceso a la red, Internet, transporte y aplicación) son más simples y menos abstractas que las del modelo OSI, lo que contribuyó a su rápida adopción.

#### Capas modelo TCP/IP

El modelo TCP/IP, también conocido como el modelo de Internet, es una arquitectura de red fundamental que define cómo los datos se transmiten a través de las redes y de Internet. Se compone de cuatro capas, cada una con funciones específicas que aseguran la comunicación entre dispositivos. A continuación, se detalla cada una de estas capas:

**▸ Capa de acceso a la red:** la capa de acceso a la red es responsable de la transmisión de datos a través de la red local. Esta capa combina las funciones de las capas física y de enlace de datos del modelo OSI. Aspectos clave:

- Transmisión física: define cómo se transmiten los bits a través del medio físico, como cables de cobre, fibra óptica o señales de radio (wifi).

- Control de acceso al medio (MAC): gestiona cómo los dispositivos acceden al medio compartido, evitando colisiones y asegurando que los datos lleguen correctamente a su destino.

- Protocolos: incluye tecnologías y protocolos como Ethernet, wifi (802.11) y protocolos de acceso de red.

Ejemplos:

- Ethernet: utilizado en redes de área local (LAN).

- Wifi: usado para redes inalámbricas.

- Frame Relay y PPP (Point-to-Point Protocol): para redes más amplias.

**▸ Capa de Internet:** la capa de Internet se encarga del direccionamiento y enrutamiento de paquetes de datos entre dispositivos a través de diferentes redes. Es equivalente a la capa de red del modelo OSI. Aspectos clave:

- Direccionamiento lógico: utiliza direcciones IP para identificar dispositivos en diferentes redes.

- Enrutamiento: determina el mejor camino para los paquetes desde el origen hasta el destino a través de múltiples redes.

- Protocolos: protocolo de Internet (IP) y protocolo de control de mensajes de Internet (ICMP) para la comunicación y el manejo de errores.

Ejemplos:

- IPv4: la versión más común del protocolo de Internet.

- IPv6: la versión más reciente, que proporciona un mayor espacio de

direcciones.

- Rúteres: dispositivos que encaminan paquetes entre redes.

**▸ Capa de transporte:** la capa de transporte asegura la comunicación fiable entre dispositivos finales. Esta capa gestiona la segmentación de los datos, el control de flujo y la corrección de errores. Aspectos clave:

- Control de flujo: regula la velocidad de envío de datos para evitar la saturación del receptor.

- Corrección de errores: asegura que los datos lleguen sin errores y en el orden correcto.

- Protocolos: TCP (Transmission Control Protocol) para conexiones fiables y UDP (User Datagram Protocol) para conexiones rápidas, pero sin garantía de entrega.

Ejemplos:

- TCP: ofrece una comunicación fiable, ordenada y con control de flujo.

- UDP: proporciona una comunicación más rápida, pero sin garantías de

entrega, ideal para aplicaciones en tiempo real.

**▸ Capa de aplicación:** la capa de aplicación proporciona servicios de red directamente a las aplicaciones del usuario. Maneja las interfaces y protocolos que permiten a las aplicaciones comunicarse a través de la red. Aspectos clave:

**•**

**•** **Servicios:** incluye protocolos para la transferencia de archivos, el correo electrónico, la navegación web y más.

- Protocolos de aplicación: define cómo se realiza la comunicación entre aplicaciones y servicios en la red.

Ejemplos:

- HTTP (HyperText Transfer Protocol): utilizado para la navegación web.

- FTP (File Transfer Protocol): para la transferencia de archivos.

- SMTP (Simple Mail Transfer Protocol): para el envío de correos

electrónicos.

- DNS (Domain Name System): para la resolución de nombres de dominio

a direcciones IP.

![Figura 5. Capas modelo TCP/IP. Fuente: La capa de internet: cómo funciona la comunicación en red, s. f.](images/image-7.png)

*Figura 5. Capas modelo TCP/IP. Fuente: La capa de internet: cómo funciona la comunicación en red, s. f.*

# 1.5. Protocolos del modelo TCP/IP

El modelo TCP/IP (Transmission Control Protocol/Internet Protocol) es un conjunto de protocolos que permite la comunicación entre dispositivos en una red. Es la base de Internet y otras redes de computadoras. Se compone de cuatro capas principales, cada una con sus propios protocolos y funciones específicas.

![Figura 6. Capas modelo TCP/IP y protocolos. Fuente: Pajuelo, s. f.](images/image-8.png)

*Figura 6. Capas modelo TCP/IP y protocolos. Fuente: Pajuelo, s. f.*

Protocolos de la capa de aplicación

La capa de aplicación del modelo TCP/IP es la más cercana al usuario final y contiene una gran variedad de protocolos que permiten a las aplicaciones de *software* interactuar con la red para realizar diferentes funciones. Aquí te detallo algunos de los protocolos más importantes y sus usos:

![image-9](images/image-9.png)

Tabla 1. Protocolos capa aplicación. Fuente: elaboración propia.

Protocolos de la capa de transporte

La capa de transporte en el modelo TCP/IP es crucial para la comunicación entre las aplicaciones que se ejecutan en diferentes dispositivos de la red. Su **principal** **función** es garantizar que los datos se transfieran de manera eficiente, confiable y sin errores entre los sistemas. A continuación, la Tabla 2 detalla los **principales** **protocolos** de esta capa.

![image-10](images/image-10.png)

Tabla 2. Protocolos capa transporte. Fuente: elaboración propia.

Protocolos de la capa de Internet (protocolo IP)

La capa de Internet en el modelo TCP/IP es crucial para la comunicación en redes, ya que maneja el **direccionamiento** y el **enrutamiento de los datos** a través de diversas redes. En esta capa, el protocolo de

Internet (IP) juega un papel

fundamental, dado que es responsable de identificar y localizar dispositivos en una red.

#### Protocolo IP

El protocolo de Internet (IP) es el principal protocolo de la capa de Internet. Su función es el **encaminamiento de paquetes de datos** desde el origen hasta el destino a través de una red, independientemente de las redes intermedias. IP se encarga del **direccionamiento lógico,** que asigna una dirección única a cada dispositivo en una red para asegurar que los datos lleguen a su destino correcto. IP opera en dos versiones principales: IPv4 e IPv6.

#### Direccionamiento IP

El direccionamiento IP es el proceso de asignar direcciones únicas a cada dispositivo en una red. Estas direcciones permiten que los dispositivos se encuentren y se comuniquen entre sí. Existen dos versiones principales de direccionamiento IP:

**▸ IPv4 (Internet Protocol version 4):**

- Estructura: utiliza direcciones de 32 bits, que se dividen en cuatro octetos de 8 bits cada uno, representados en notación decimal separada por puntos (por ejemplo, 192.168.1.1). Esto permite un total de aproximadamente 4,3 mil millones de direcciones únicas.

- Formato: la dirección IPv4 se expresa como cuatro números decimales entre 0 y 255 (por ejemplo, 192.168.0.1). Cada octeto puede representar valores de 0 a 255.

- Limitaciones: la creciente demanda de dispositivos conectados a Internet ha agotado el espacio disponible de direcciones IPv4, llevando a la necesidad de una solución más amplia.

**▸ IPv6 (Internet Protocol version 6):**

- Estructura: utiliza direcciones de 128 bits, lo que permite un número prácticamente ilimitado de direcciones únicas (2^128, o aproximadamente 340 undecillones de direcciones). Esta expansión es esencial para soportar el crecimiento futuro de Internet.

- Formato: la dirección IPv6 se expresa en ocho grupos de cuatro dígitos hexadecimales, separados por dos puntos (por ejemplo, 2001:0db8:85a3:0000:0000:8a2e:0370:7334). Los ceros a la izquierda en los grupos pueden omitirse para simplificar la dirección.

**▸**

- Beneficios: IPv6 no solo ofrece una cantidad mucho mayor de direcciones, sino que también incluye mejoras en la eficiencia del enrutamiento y la configuración automática de direcciones.

![Comparativa entre IPv4 e IPv6](images/image-11.png)

Tabla 3. Comparativa IPv4-IPv6. Fuente: elaboración propia.

Protocolos de la capa de acceso a la red (Token Ring, Ethernet)

La capa de acceso a la red en el modelo TCP/IP se encarga de la transmisión de datos a través del **medio físico** y del **control de acceso al medio.** Dos de los protocolos más importantes en esta capa son Token Ring y Ethernet. Ambos juegan un papel crucial en la forma en que los datos se transmiten dentro de una red local (LAN), pero tienen características y mecanismos operativos distintos.

#### Token Ring

Token Ring es un protocolo de red desarrollado por IBM en la década de 1980. Su diseño se basa en un método de acceso al medio conocido como **Token Passing.**

**▸ Estructura de la red:** en una red Token Ring, los dispositivos están conectados en un anillo físico o lógico. Cada dispositivo está conectado a dos otros dispositivos, formando un bucle cerrado.

**▸ Método de acceso:** Token Ring utiliza un token (paquete de datos especial) que circula continuamente por el anillo. Solo el dispositivo que posee el token puede transmitir datos. Cuando un dispositivo quiere enviar datos, debe esperar a recibir el token. Una vez que lo recibe, lo utiliza para enviar sus datos al dispositivo destino. Tras la transmisión, el token se libera y continúa su circulación, permitiendo a otros dispositivos la oportunidad de transmitir.

**▸ Ventajas:** el método de token *passing* minimiza las colisiones de datos, ya que solo un dispositivo puede transmitir a la vez. Esto proporciona un control de acceso al medio muy ordenado y reduce las probabilidades de pérdida de datos.

**▸ Desventajas:** la principal desventaja de Token Ring es su costo y complejidad en comparación con Ethernet. Además, la red puede verse afectada si un único dispositivo o cable falla, ya que interrumpe la circulación del token.

#### Ethernet

Ethernet es el protocolo de red más ampliamente utilizado en la mayoría de las redes locales modernas. Fue desarrollado por Xerox en la década de 1970 y, posteriormente, estandarizado por IEEE en el estándar 802.3.

**▸ Estructura de la red:** Ethernet inicialmente se basaba en una topología de bus, donde todos los dispositivos estaban conectados a un cable coaxial compartido. Hoy en día, Ethernet se implementa, principalmente, utilizando una topología de estrella, donde los dispositivos están conectados a un *switch* central o *hub* mediante cables de par trenzado o fibra óptica.

**▸ Método de acceso:** Ethernet utiliza un método de acceso denominado CSMA/CD (Carrier Sense Multiple Access with Collision Detection). En este método, los dispositivos escuchan el medio para asegurarse de que esté libre antes de transmitir datos. Si dos dispositivos transmiten simultáneamente, se produce una colisión. Cuando esto ocurre, los dispositivos interrumpen la transmisión, esperan un tiempo aleatorio y luego intentan retransmitir los datos.

**▸ Ventajas:** Ethernet es menos costoso y más sencillo de implementar que Token Ring. Su capacidad para manejar múltiples dispositivos en un solo segmento y la evolución hacia conmutadores *(switches)* y tecnologías de alta velocidad (como Gigabit y 10 Gigabit Ethernet) han hecho de Ethernet la opción preferida para redes modernas.

**▸ Desventajas:** aunque Ethernet ha evolucionado para ser más eficiente, las colisiones pueden ocurrir en redes congestionadas, especialmente en redes con *hubs.* Sin embargo, la transición a *switches* Ethernet ha mitigado significativamente este problema al segmentar el tráfico y reducir las colisiones.

#### Comparación de Ethernet y Token Ring

Aquí tienes una tabla comparativa entre Token Ring y Ethernet, destacando las diferencias clave entre estos dos protocolos de la capa de acceso a la red:

![image-12](images/image-12.png)

Tabla 4. Comparativa Ethernet-Token Ring. Fuente: elaboración propia.

# 1.6. Diferencias entre el Modelo OSI y el Modelo

# TCP/IP

Aquí tienes una tabla comparativa entre el modelo OSI y el modelo TCP/IP:

![image-13](images/image-13.png)

Tabla 5. Comparativa OSI-TCP/IP. Fuente: elaboración propia.

![Figura 7. Correspondencia del modelo OSI con el modelo TCP/IP. Fuente: Matango, 2016.](images/image-14.png)

*Figura 7. Correspondencia del modelo OSI con el modelo TCP/IP. Fuente: Matango, 2016.*

# 1.7. Referencias bibliográficas

Cyberprimo. (s. f.). Conociendo el modelo OSI. *Cyberprimo.* [https://www.cyberprimo.com/2009/08/conociendo-el-modelo-osi.html](https://www.cyberprimo.com/2009/08/conociendo-el-modelo-osi.html)

Higueras, L. (2023). Formato de

datagramas IP. *Wix.*

[https://srluishigueras.wixsite.com/2fpb/formato-de-datagramas](https://srluishigueras.wixsite.com/2fpb/formato-de-datagramas) La capa de internet: cómo funciona la comunicación en red. (s.f.). *Coop La Lonja.* <https://cooplalonja.com.ar/tcp-ip-capa-de-internet/> Matango, F. (2016, agosto 18). Conceptos básicos protocolo TCP/IP. *Server VoIP.* <http://www.servervoip.com/blog/conceptos-basicos-protocolo-tcpip/>

Pajuelo, F. J. (s. f.). PROTOCOLO

TCP/IP. *Microinformática.*

[https://microinformatica.jimdofree.com/inicio/protocolo-tcp-ip/](https://microinformatica.jimdofree.com/inicio/protocolo-tcp-ip/) Proceso Fernandez. (2013, diciembre 13). Puertos. *Ensamblajes de PC.* <https://informatics-ensamblaje.blogspot.com/2013/12/9-puertos.html>

Topología de red. (2024, octubre [https://es.wikipedia.org/wiki/Topolog%C3%ADa_de_red](https://es.wikipedia.org/wiki/Topolog%25C3%25ADa_de_red)

24). En *Wikipedia.*

# YouTube. [https://www.youtube.com/watch?v=sdzKhSWmMm0](https://www.youtube.com/watch?v=sdzKhSWmMm0)

# Conexión TCP y UDP pasos y diferencias

El profe García (2013, marzo 12). *Conexión TCP y UDP pasos y diferencias* [Vídeo]. Hemos hablado de los protocolos TCP y UDP y explicado por encima sus diferencias, pero en este vídeo se enseñan estos protocolos de una manera más dinámica e intuitiva.

![image-15](images/image-15.png)

Accede al vídeo: [https://www.youtube.com/embed/sdzKhSWmMm0](https://www.youtube.com/embed/sdzKhSWmMm0)

# YouTube. [https://www.youtube.com/watch?v=gmFv4ZD_h4w](https://www.youtube.com/watch?v=gmFv4ZD_h4w)

# Modelo OSI explicación de las 7 capas

El profe García. (2013, marzo 11). *Modelo OSI explicación de las 7 capas* [Vídeo]. Si te quedaron dudas respecto a las capas del modelo OSI, aquí te presento un vídeo de tan solo ocho minutos donde podrás aclarar todas ellas. Todo ello explicado con diferentes ejemplos para que te resulte más fácil.

![image-16](images/image-16.png)

Accede al vídeo: [https://www.youtube.com/embed/gmFv4ZD_h4w](https://www.youtube.com/embed/gmFv4ZD_h4w)

# Redes de computadoras. Apuntes digitales

Hernández Solís, F. y Lugo Martínez, J. E. (2014). *Redes de Computadoras. Apuntes* *Digitales.* [http://cidecame.uaeh.edu.mx/lcc/mapa/PROYECTO/libro35/index.html](http://cidecame.uaeh.edu.mx/lcc/mapa/PROYECTO/libro35/index.html)

Te presento un trabajo elaborado en la Universidad autónoma del Estado de Hidalgo de México, con el que podrás profundizar en todos los contenidos vistos durante este tema.

# Cisco Networking Academy Program. (s. f.). CCNA 1 and 2. Versión 3.1.

# CCNA 1 and 2. (Cisco Networking Academy Program)

[https://betosamaniego.wordpress.com/wp-content/uploads/2011/09/ccna-1-y-2.pdf](https://betosamaniego.wordpress.com/wp-content/uploads/2011/09/ccna-1-y-2.pdf)

Libro de cabecera, que abarca todos los contenidos relacionados con las redes de computadoras. Aquí tienes prácticamente todo lo que necesites saber, ya que este documento es la guía para certificarte en Cisco tanto en CCNA1 como en CCNA2.

# y-para-que-sirven-los-protocolos-tcp-ip/

# ¿Qué es TCP/IP? La columna vertebral de Internet

Lamorte, J. M. (2024, octubre 3). TCP/IP Explicado: Cómo funciona el protocolo que soporta Internet. *IT Masters.* <https://www.itmastersmag.com/ciberseguridad/que-son-> Descubre que es el modelo TCP/IP y cómo el protocolo TCP/IP proyecta Internet. Conoce sus capas, funciones y por qué es esencial para la comunicación y los negocios en línea.

# Entrenamiento 1. Cuestionario sobre el Modelo

# OSI

#### ▸ Planteamiento del ejercicio

Deberás responder diferentes cuestiones sobre el modelo OSI.

**▸ Definiciones y funciones:**

- Pregunta 1. ¿Cuál es la función principal de la capa física en el modelo OSI?

- Pregunta 2. ¿Qué tipo de errores puede detectar y corregir la capa de enlace de datos?

- Pregunta 3. Explica cómo la capa de red se encarga de la dirección y el enrutamiento de los datos.

- Pregunta 4. ¿Qué información de control se maneja en la capa de transporte y cómo asegura la entrega de datos?

- Pregunta 5. Describe cómo la capa de sesión facilita la comunicación entre aplicaciones.

- Pregunta 6. ¿Qué papel juega la capa de presentación en la interpretación de datos?

- Pregunta 7. ¿Cuál es la función de la capa de aplicación y cómo interactúa con las aplicaciones del usuario?

**▸ Aplicaciones y ejemplos prácticos:**

- Pregunta 8. Da un ejemplo de un protocolo o servicio asociado con cada una de las capas del modelo OSI.

- Pregunta 9. Explica cómo un mensaje de correo electrónico viaja a través de las diferentes capas del modelo OSI.

- Pregunta 10. Imagina que tienes un problema con una conexión de red y los datos no llegan a su destino. ¿Qué capa del modelo OSI podría estar involucrada en este problema y por qué?

**▸ Escenarios de problemas:**

- Pregunta 11. Si un dispositivo no puede comunicarse con otro en una red, ¿qué capas del modelo OSI debes revisar primero y qué tipos de problemas podrías buscar en esas capas?

- Pregunta 12. ¿Cómo podrían los problemas en la capa de enlace de datos afectar la capa de red?

**▸ Reflexión crítica:**

- Pregunta 13. ¿Por qué es importante que el modelo OSI esté dividido en capas? ¿Cómo facilita esto la solución de problemas y la implementación de redes?

- Pregunta 14. Comenta un escenario en el que un entendimiento profundo del modelo OSI puede ser crucial para la configuración o mantenimiento de una red.

#### ▸ Desarrollo paso a paso

Deberás consultar estas cuestiones ayudándote de libros y de Internet.

#### ▸ Solución

#### Definiciones y funciones

Pregunta 1. ¿Cuál es la función principal de la capa física en el modelo OSI?

La capa física se encarga de la transmisión de bits a través de un medio físico. Define las características eléctricas, mecánicas incluyendo cables, tarjetas de red y conectores.

y de señalización del *hardware,*

Pregunta 2. ¿Qué tipo de errores puede detectar y corregir la capa de enlace de datos?

La capa de enlace de datos puede detectar errores de transmisión utilizando técnicas como la comprobación de redundancia cíclica

(CRC). Además, puede corregir

errores mediante el uso de técnicas de control de errores, como el control de flujo y el reintento de paquetes.

Pregunta 3. Explica cómo la capa de red se encarga de la dirección y el enrutamiento de los datos.

La capa de red se encarga de la dirección y el enrutamiento de los datos a través de redes diferentes. Utiliza direcciones lógicas (como las direcciones IP) para identificar y enviar paquetes de datos desde el origen hasta el destino a través de múltiples redes. Los rúteres operan en esta capa para dirigir los paquetes a su destino final.

Pregunta 4: ¿Qué información de control se maneja en la capa de transporte y cómo asegura la entrega de datos?

La capa de transporte maneja la información de control como números de secuencia, confirmaciones *(acknowledgments)* y el control de flujo. Utiliza protocolos como TCP (Transmission Control Protocol) para garantizar una entrega fiable y ordenada de los datos, realizando la retransmisión de paquetes perdidos y asegurando la integridad de la transmisión.

Pregunta 5. Describe cómo la capa de sesión facilita la comunicación entre aplicaciones.

La capa de sesión establece, mantiene y termina las sesiones entre aplicaciones. Facilita la comunicación entre procesos y aplicaciones permitiendo la sincronización y el manejo de diálogos, así como la recuperación de errores en las sesiones. También, administra la comunicación de datos de manera ordenada y coherente.

Pregunta 6. ¿Qué papel juega la capa de presentación en la interpretación de datos? La capa de presentación se encarga de la traducción de datos entre el formato de la red y el formato que puede entender la aplicación. Realiza tareas como la compresión y descompresión de datos y la codificación y decodificación de datos para que sean comprensibles para el *software* de aplicación, asegurando que los datos sean presentados correctamente.

Pregunta 7. ¿Cuál es la función de la capa de aplicación y cómo interactúa con las aplicaciones del usuario?

La capa de aplicación proporciona servicios y funciones directamente a las aplicaciones del usuario. Facilita la interacción entre las aplicaciones y la red, permitiendo que programas como navegadores web, clientes de correo electrónico y otros servicios de red puedan comunicarse a través de la red. Los protocolos de esta

Servicios en Red e Internet 51 Tema 1. Entrenamientos capa incluyen HTTP, FTP, SMTP, entre otros.

#### Aplicaciones y ejemplos prácticos

Pregunta 8. Da un ejemplo de un protocolo o servicio asociado con cada una de las capas del modelo OSI.

**▸** Capa física: Ethernet (para la transmisión de datos en redes locales).

**▸** Capa de enlace de datos: PPP (Point-to-Point Protocol).

**▸** Capa de red: IP (Internet Protocol).

**▸** Capa de transporte: TCP (Transmission Control Protocol).

**▸** Capa de sesión: SMB (Server Message Block).

**▸** Capa de presentación: SSL/TLS (Secure Sockets Layer / Transport Layer Security).

**▸** Capa de aplicación: HTTP (Hypertext Transfer Protocol). Pregunta 9. Explica cómo un mensaje de correo electrónico viaja a través de las diferentes capas del modelo OSI. Cuando envías un correo electrónico, el mensaje se origina en la capa de aplicación con el protocolo SMTP. Luego, pasa a la capa de presentación, donde se puede codificar o cifrar. En la capa de sesión, se establece una conexión con el servidor de correo. A continuación, el mensaje se envía a la capa de transporte (TCP) para asegurar la entrega fiable. La capa de red (IP) se encarga de enrutar el mensaje a través de la red. El mensaje llega a la capa de enlace de datos, donde se realiza el control de errores y el direccionamiento a nivel de enlace. Finalmente, la capa física transmite los datos a través del medio físico.

Pregunta 10. Imagina que tienes un problema con una conexión de red y los datos no llegan a su destino. ¿Qué capa del modelo OSI podría estar involucrada en este problema y por qué?

El problema podría estar involucrando varias capas, pero si los datos no llegan a su destino, se debe revisar principalmente la capa de red (IP) para problemas de enrutamiento y direccionamiento, la capa de transporte (TCP) para problemas con la entrega y confirmación de paquetes y la capa física para problemas con el medio de transmisión. Cada capa tiene un rol crucial en asegurar que los datos sean correctamente transmitidos y entregados.

#### Escenarios de problemas

Pregunta 11. Si un dispositivo no puede comunicarse con otro en una red, ¿qué capas del modelo OSI debes revisar primero y qué tipos de problemas podrías buscar en esas capas?

Primero, revisa la capa física para asegurarte de que los cables y conectores estén funcionando correctamente. Luego, revisa

la capa de enlace de datos para

problemas de configuración de direcciones MAC o errores de comunicación en el enlace. Después, verifica la capa de red para problemas de direccionamiento IP y enrutamiento. Si estas capas están funcionando correctamente, verifica la capa de Transporte para problemas en la entrega de datos.

Pregunta 12. ¿Cómo podrían los problemas en la capa de enlace de datos afectar la capa de red?

Los problemas en la capa de enlace de datos, como errores en la transmisión o problemas con el direccionamiento MAC, pueden causar la pérdida de paquetes o errores en la comunicación entre dispositivos en la misma red local. Esto afectará la capa de red, ya que los paquetes no podrán ser entregados correctamente a los rúteres o dispositivos de red para su enrutamiento a través de redes más amplias.

#### Reflexión crítica

Pregunta 13: ¿Por qué es importante que el modelo OSI esté dividido en capas? ¿Cómo facilita esto la solución de problemas y la implementación de redes?

La división en capas del modelo OSI permite una modularidad en el diseño de redes, lo que facilita la implementación y el mantenimiento. Cada capa tiene funciones específicas y bien definidas, lo que permite que los problemas sean aislados y solucionados sin afectar a otras capas.

Además, esta división permite la

interoperabilidad entre diferentes sistemas y tecnologías, ya que cada capa puede ser implementada y actualizada de forma independiente.

Pregunta 14. Comenta un escenario en el que un entendimiento profundo del modelo OSI puede ser crucial para la configuración o mantenimiento de una red.

Un entendimiento profundo del modelo OSI

es crucial cuando se realiza la

configuración de una red compleja que involucra múltiples protocolos y dispositivos. Por ejemplo, al configurar una red empresarial con múltiples subredes, rúteres, *switches* y *firewalls,* el conocimiento del modelo OSI permite a los administradores de red identificar y solucionar problemas de conectividad, enrutamiento y seguridad de manera eficiente, garantizando que todos los dispositivos y protocolos funcionen correctamente en su capa respectiva.

# Entrenamiento 2. Configuración y verificación de

# direcciones IPv4 e IPv6

#### ▸ Planteamiento del ejercicio

En este ejercicio, trabajarás en dos segmentos de red: uno utilizando IPv4 y otro utilizando IPv6. El objetivo es configurar direcciones IP en estos segmentos y verificar la conectividad entre los dispositivos dentro de cada segmento y entre segmentos. Para ello puedes valerte del simulador de redes Packet Tracer.

#### ▸ Desarrollo paso a paso

Parte 1. Configuración de direcciones IPv4:

**▸** Crear y configurar la red IPv4. Parte 2. Configuración de direcciones IPv6:

**▸** Crear y configurar la red IPv6. Parte 3. Configuración de una red mixta IPv4 e IPv6:

**▸** Crear y configurar la red mixta.

**▸** Verificar la conectividad entre redes IPv4 e IPv6. Parte 4. Documentar configuración:

**▸** Toma nota de las direcciones IP y configuraciones de los dispositivos.

**▸** Incluye capturas de pantalla de la configuración y resultados de los comandos de ping.

Parte 5. Analizar la configuración IPv4 e IPv6: **▸** Explica cómo cada dirección IP se asigna y opera en la red. **▸** Discute las diferencias en la configuración y el manejo de IPv4 e IPv6. Parte 6. Responder preguntas: **▸** ¿Qué diferencias observaste en la configuración y verificación de IPv4 y IPv6? **▸** ¿Cuáles son los principales beneficios de IPv6 sobre IPv4?

#### ▸ Solución

#### Parte 1. Configuración de direcciones IPv4. Crear y configurar la red IPv4

Crear el escenario: **▸** Abre Packet Tracer y crea una nueva red. **▸** Añade dos PC y un *switch* al espacio de trabajo. **▸** Conecta los PC al *switch* usando cables directos. Configurar direcciones IPv4: **▸** PC1:

- IP Address: 192.168.1.10.

- Subnet Mask: 255.255.255.0.

**▸** PC2:

- IP Address: 192.168.1.20.

- Subnet Mask: 255.255.255.0.

Verificar Conectividad IPv4: **▸** Desde PC1, abre el Command Prompt y realiza un ping a 192.168.1.20. **▸** Asegúrate de que los paquetes lleguen a PC2.

#### Parte 2. Configuración de direcciones IPv6. Crear y configurar la red IPv6

Crear el escenario: **▸** Añade dos PC y un *switch* al espacio de trabajo (en una nueva sección o red del proyecto).

**▸** Conecta los PC al *switch* usando cables directos.

Configurar direcciones IPv6:

**▸** PC3:

- IPv6 Address: 2001:0db8:85a3:0000:0000:8a2e:0370:7334/64

**▸** PC4:

- IPv6 Address: 2001:0db8:85a3:0000:0000:8a2e:0370:7335/64

Verificar conectividad IPv6:

**▸** Desde PC3, abre el Command Prompt y realiza un ping a

2001:0db8:85a3:0000:0000:8a2e:0370:7335. **▸** Asegúrate de que los paquetes lleguen a PC4.

**Parte 3. Configuración de una red mixta IPv4 e IPv6. Crear y configurar la red**

#### mixta

Añadir el rúter y conectar redes. **▸** Añade un rúter al espacio de trabajo y conéctalo a ambos *switches* con cables directos (uno para IPv4 y otro para IPv6).

**▸** Configura dos interfaces en el rúter: una para IPv4 y otra para IPv6.

Configurar interfaces del rúter.

**▸** Interface en la red IPv4 (por ejemplo, FastEthernet0/0):

- IP Address: 192.168.1.1.

- Subnet Mask: 255.255.255.0.

**▸** Interface en la red IPv6 (por ejemplo, FastEthernet0/1):

- IPv6 Address: `2001:0db8:85a3:0000:0000:8a2e:0370:7336/64`

Configurar el rúter para IPv6.

Habilita el enrutamiento IPv6 en el rúter:

**▸** Accede al modo de configuración global en el rúter:

![image-17](images/image-17.png)

**▸** Habilita el enrutamiento IPv6:

![image-18](images/image-18.png)

Configura las interfaces del rúter con las direcciones IPv6 adecuadas.

**▸** Configura la interfaz FastEthernet0/0 con la dirección IPv4:

![image-19](images/image-19.png)

**▸** Configura la interfaz FastEthernet0/1 con la dirección IPv6:

![Verificar la conectividad entre redes IPv4 e IPv6.](images/image-20.png)

**▸** Desde PC1 en la red IPv4, realiza un ping a PC3 en la red IPv6.

**▸** Desde PC4 en la red IPv6, realiza un ping a PC2 en la red IPv4.

Nota: en una configuración real, esta comunicación requeriría un proceso de traducción de direcciones o un dispositivo de intermediario para manejar IPv4 e IPv6.

#### Parte 4. Documentar configuración

**▸** Toma nota de las direcciones IP y configuraciones de los dispositivos.

**▸** Incluye capturas de pantalla de la configuración y resultados de los comandos de

ping.

#### Parte 5. Analizar la configuración IPv4 e IPv6

**▸** Explica cómo cada dirección IP se asigna y opera en la red.

Para entender cómo cada dirección IP se asigna y opera en una red, es útil desglosar tanto el funcionamiento de IPv4 como de IPv6. A continuación, se explica el proceso para cada protocolo y se destacan las diferencias clave entre ellos.

#### Direcciones IPv4. Asignación de direcciones IPv4

Estructura de la Dirección IPv4:

**▸** Una dirección IPv4 consta de 32 bits, que se dividen en 4 octetos de 8 bits cada uno.

Se representa en formato decimal punteado, por ejemplo, `192.168.1.10`.

**▸** La dirección se divide en dos partes:

- Red: identifica la red a la que pertenece la dirección.

- Host: identifica el dispositivo específico dentro de esa red.

Configuración de la dirección:

**▸** Dirección IP: asignada manualmente por el administrador de red o automáticamente por un servidor DHCP (protocolo de configuración dinámica de *host).*

**▸** Máscara de subred: utilizada para determinar qué parte de la dirección IP corresponde a la red y qué parte corresponde al *host.* Por ejemplo, 255.255.255.0 en la notación de máscara de subred significa que los primeros 24 bits son la parte de la red.

Proceso de comunicación:

Asignación manual: un administrador asigna direcciones IP estáticas a dispositivos en la red. Cada dispositivo en la misma red debe tener una dirección única.

**▸** Asignación dinámica: un servidor DHCP asigna automáticamente direcciones IP a los dispositivos cuando se conectan a la red. El servidor DHCP mantiene un grupo de direcciones IP disponibles y las asigna temporalmente a los dispositivos.

Enrutamiento:

**▸** Cuando un dispositivo envía un paquete a una dirección IP, la máscara de subred determina si el paquete se envía dentro de la misma red local o si debe ser enviado a través de un rúter para llegar a una red diferente.

#### Direcciones IPv6. Asignación de direcciones IPv6

Estructura de la dirección IPv6:

**▸** Una dirección IPv6 consta de 128 bits, que se dividen en 8 bloques de 16 bits cada uno. Se representa en formato hexadecimal, por ejemplo, 2001:0db8:85a3:0000:0000:8a2e:0370:7334.

**▸** Al igual que en IPv4, la dirección se divide en dos partes:

- Red: identifica la red a la que pertenece la dirección.

- Host: identifica el dispositivo específico dentro de esa red.

Configuración de la dirección:

**▸** Dirección IP: puede ser asignada manual o automáticamente. En IPv6, la configuración automática es más común y se realiza mediante SLAAC (autoconfiguración de dirección sin estado) o DHCPv6.

**▸** Prefijo de red: en IPv6, el prefijo de red (por ejemplo, /64) indica los primeros bits que representan la parte de la red y el resto se utiliza para la parte de *host.*

Proceso de comunicación:

**▸** Autoconfiguración (SLAAC): los dispositivos pueden autoconfigurarse automáticamente utilizando la información de red proporcionada por los rúteres en la red. Esto simplifica la administración y evita la necesidad de un servidor DHCP.

**▸** Configuración manual: también se pueden asignar direcciones IPv6 manualmente si es necesario.

Enrutamiento:

**▸** Al igual que en IPv4, la dirección IPv6 se utiliza para determinar si un paquete debe ser enviado dentro de la misma red local o a través de rúteres hacia otras redes. La longitud del prefijo de red determina la parte de la dirección que se utiliza para el enrutamiento.

#### Comparación de IPv4 e IPv6

**▸** Longitud de la dirección: IPv4 usa direcciones de 32 bits (4 octetos), mientras que IPv6 usa direcciones de 128 bits (8 bloques de 16 bits).

**▸** Espacio de direcciones: IPv6 ofrece un espacio de direcciones mucho mayor que IPv4, resolviendo el problema de agotamiento de direcciones en IPv4.

**▸** Autoconfiguración: IPv6 soporta la autoconfiguración de direcciones mediante SLAAC, lo que facilita la administración de redes sin necesidad de servidores DHCP

Servicios en Red e Internet 63 Tema 1. Entrenamientos para direcciones IP.

**▸** Formato: IPv4 usa formato decimal punteado, mientras que IPv6 usa formato hexadecimal con dos puntos.

**▸** Máscara de subred vs. prefijo de red: en IPv4 se utiliza una máscara de subred para determinar las partes de red y *host,* mientras que en IPv6 se utiliza un prefijo de red que se especifica al final de la dirección.

#### Conclusión

**▸** Dirección IPv4: se asigna manual o dinámicamente, con una estructura de 32 bits y máscara de subred que divide la dirección en red y host.

**▸** Dirección IPv6: se asigna manual o automáticamente mediante SLAAC o DHCPv6, con una estructura de 128 bits y un prefijo de red que define la parte de red de la dirección.

**Discute las diferencias en la configuración y el manejo de IPv4 e IPv6**

Aquí tienes una tabla que resume las diferencias clave entre IPv4 e IPv6 en términos de configuración y manejo:

![image-21](images/image-21.png)

Tabla 6. Diferencias en la configuración y el manejo de IPv4 e IPv6. Fuente: elaboración propia.

Esta tabla proporciona una visión clara de cómo IPv4 e IPv6 se diferencian en varios aspectos clave relacionados con la asignación, configuración y manejo de direcciones IP en redes.

#### Responder preguntas

**▸** ¿Qué diferencias observaste en la configuración y verificación de IPv4 y IPv6?

- Configuración de IPv4: incluye una dirección de 32 bits con máscara de subred para dividir la dirección en partes de red y *host.* La configuración puede ser manual o

Servicios en Red e Internet 65 Tema 1. Entrenamientos dinámica mediante DHCP. Verificación se realiza mediante comandos específicos y ARP para resolución de direcciones.

- Configuración de IPv6: utiliza una dirección de 128 bits con prefijo de red para definir la parte de red. La configuración puede ser manual o automática mediante SLAAC o DHCPv6. Verificación se realiza mediante comandos específicos y NDP para resolución de direcciones.

Ambos protocolos tienen métodos de configuración y verificación distintos que se adaptan a sus características específicas, con IPv6 se proporciona un enfoque más automatizado y simplificado debido a su diseño moderno y expansión del espacio de direcciones.

#### ¿Cuáles son los principales beneficios de IPv6 sobre IPv4?

IPv6 ofrece varios beneficios significativos sobre IPv4, abordando muchas de las limitaciones del protocolo anterior. Aquí se presentan los principales beneficios de IPv6:

**▸** Espacio de direcciones ampliado.

- IPv4: tiene un espacio de direcciones limitado de aproximadamente 4,3 mil millones de direcciones únicas. Este espacio se ha agotado debido al creciente número de dispositivos conectados a Internet.

- IPv6: ofrece un espacio de direcciones mucho más grande, con aproximadamente 340 undecillones (3,4 × 10^38) de direcciones únicas. Esto elimina la preocupación por el agotamiento de direcciones y permite una asignación más flexible y escalable.

**▸** Simplificación del encabezado.

- IPv4: el encabezado del paquete IPv4 tiene varios campos opcionales y una longitud variable, lo que puede complicar el procesamiento.

- IPv6: el encabezado de IPv6 es fijo en 40 bytes y simplificado, con campos

Servicios en Red e Internet 66 Tema 1. Entrenamientos eliminados o combinados para reducir la sobrecarga de procesamiento. Esto mejora la eficiencia en el enrutamiento y el procesamiento de paquetes.

**▸** Autoconfiguración y simplificación del protocolo de configuración.

- IPv4: la configuración automática requiere el uso de DHCP para asignar direcciones IP dinámicamente, lo que puede ser complejo en redes grandes.

- IPv6: incluye autoconfiguración sin estado (SLAAC), que permite a los dispositivos autoconfigurarse automáticamente mediante la información de los routers. Esto simplifica la configuración de dispositivos y reduce la necesidad de servidores DHCP.

**▸** Mejora en la seguridad.

- IPv4: la seguridad en IPv4, como IPsec, es opcional y debe ser implementada y configurada manualmente.

- IPv6: IPsec está integrado y se considera obligatorio, proporcionando cifrado y autenticación a nivel de protocolo de forma predeterminada. Esto mejora la seguridad en las comunicaciones de red.

**▸** Soporte mejorado para la movilidad.

- IPv4: la movilidad puede requerir soluciones adicionales como NAT (traducción de direcciones de red) para permitir la movilidad de los dispositivos entre redes.

- IPv6: tiene soporte nativo para la movilidad, facilitando la conexión de dispositivos que cambian de red sin necesidad de usar NAT. Esto mejora la experiencia del usuario en dispositivos móviles.

**▸** Mejor gestión del tráfico de red.

- IPv4: la fragmentación de paquetes puede ser realizada por rúteres, lo que puede introducir sobrecarga en la red.

- IPv6: la fragmentación se realiza únicamente en el origen, lo que reduce la carga en los rúteres y mejora el rendimiento de la red. Además, los encabezados de IPv6 pueden incluir extensiones para optimizar la gestión del tráfico.

**▸** Mayor eficiencia en el enrutamiento.

- IPv4: los rúteres deben manejar información adicional en los encabezados y realizar búsquedas complejas en las tablas de enrutamiento.

- IPv6: las tablas de enrutamiento son más eficientes debido a la simplificación del encabezado y el uso de prefijos de red más largos, lo que facilita la agregación de rutas y mejora la eficiencia del enrutamiento.

**▸** Eliminación de NAT (traducción de direcciones de red).

- IPv4: la escasez de direcciones IP ha llevado al uso generalizado de NAT, que puede complicar la comunicación y la administración de red.

- IPv6: con un espacio de direcciones suficientemente grande, NAT no es necesario en la mayoría de los casos, lo que permite una comunicación más directa y simplificada entre dispositivos.

**▸** Mejoras en el manejo de direcciones.

- IPv4: las direcciones IP deben ser gestionadas y asignadas cuidadosamente debido al espacio limitado.

- IPv6: el gran espacio de direcciones permite una asignación más flexible y una planificación de red más simple, con la posibilidad de tener direcciones únicas para cada dispositivo sin necesidad de reutilización o NAT.

**▸** Soporte para nuevas tecnologías.

- IPv4: puede no ser compatible con tecnologías emergentes debido a su diseño y limitaciones.

- IPv6: está diseñado para soportar tecnologías emergentes y futuras aplicaciones de red, proporcionando una base sólida para la evolución de Internet.

Entrenamiento 3. Evaluación de conceptos sobre modelos TCP/IP, OSI y protocolos.

#### ▸ Planteamiento del ejercicio

En esta actividad se evalúan los conocimientos de los estudiantes sobre los modelos de referencia TCP/IP y OSI, el proceso de encapsulamiento y los protocolos asociados a las capas del modelo TCP/IP.

**▸ Comparación entre modelos TCP/IP y OSI:** explica las diferencias y similitudes entre el modelo TCP/IP y el modelo OSI. En tu respuesta, menciona las capas de cada modelo, cómo se relacionan entre sí y la importancia de cada modelo en el diseño y la comprensión de las redes de computadoras.

**▸ Proceso de encapsulamiento:** describe el proceso de encapsulamiento de datos en el modelo TCP/IP desde la capa de aplicación hasta la capa de enlace de datos. Explica cómo cada capa añade su propio encabezado y cómo este proceso facilita la transmisión de datos a través de la red.

**▸ Protocolos de la capa de transporte:** en el modelo TCP/IP, la capa de transporte utiliza, principalmente, dos protocolos: TCP y UDP. Explica las diferencias fundamentales entre estos dos protocolos, incluyendo cómo manejan la confiabilidad, el control de flujo y la segmentación de datos. Proporciona ejemplos de aplicaciones o servicios que usan cada uno de estos protocolos.

**▸ Función de las capas de red y de enlace de datos:** analiza la función de las capas de red y de enlace de datos en el modelo TCP/IP. En tu respuesta, describe cómo estas capas trabajan juntas para asegurar que los datos lleguen correctamente a su destino, mencionando los protocolos y dispositivos que operan en cada capa.

**▸ Importancia y ejemplos de protocolos en la capa de aplicación:** la capa de aplicación en el modelo TCP/IP es crucial para la interacción de los usuarios con la red. Selecciona tres protocolos que operen en esta capa (por ejemplo, HTTP, FTP, DNS) y explica su función y cómo contribuyen al funcionamiento general de la red. Además, discute la importancia de esta capa en la experiencia del usuario final.

#### ▸ Desarrollo paso a paso

Responde detalladamente las siguientes preguntas, proporcionando ejemplos y explicaciones claras para cada una de tus respuestas. Se evaluará la comprensión conceptual, la claridad en la explicación y el uso adecuado de la terminología técnica.

#### ▸ Solución

#### Comparación entre modelos TCP/IP y OSI

**▸ Modelo TCP/IP.** El modelo TCP/IP, también conocido como el conjunto de protocolos de Internet, se desarrolla a partir de la necesidad de crear un sistema de comunicación robusto y flexible para redes. Se basa en cuatro capas:

- Capa de aplicación: maneja las interacciones con el usuario y las aplicaciones. Ejemplos de protocolos en esta capa incluyen HTTP, FTP y SMTP.

- Capa de transporte: se encarga de la entrega de datos entre sistemas finales y ofrece servicios como control de flujo y corrección de errores. Los protocolos principales son TCP (Transmission Control Protocol) y UDP (User Datagram Protocol).

- Capa de Internet: esta capa maneja el direccionamiento y el enrutamiento de los paquetes de datos. El protocolo principal es IP (Internet Protocol).

- Capa de enlace de datos: se ocupa de la comunicación entre dispositivos en la misma red física. Incluye protocolos como Ethernet y ARP (Address Resolution Protocol).

**▸ Modelo OSI.** El modelo OSI (Open Systems Interconnection) es un marco de referencia conceptual desarrollado por la ISO (International Organization for Standardization) que describe cómo los datos se transmiten en una red. Se compone de siete capas:

- Capa física: define las características eléctricas y mecánicas de los equipos de red, como cables y conectores.

- Capa de enlace de datos: proporciona la transmisión de datos en la red local y controla errores. Protocolos como Ethernet operan en esta capa.

- Capa de red: se encarga del direccionamiento y enrutamiento de paquetes. IP es el protocolo más destacado en esta capa.

- Capa de transporte: asegura la entrega completa y correcta de datos entre aplicaciones, con protocolos como TCP y UDP.

- Capa de sesión: maneja las sesiones de comunicación entre aplicaciones, incluyendo la apertura, cierre y gestión de sesiones.

- Capa de presentación: se encarga de la representación de datos, la codificación y la traducción entre diferentes formatos de datos.

- Capa de aplicación: proporciona servicios de red a las aplicaciones del usuario, tales como HTTP para navegación web y SMTP para correo electrónico.

#### Similitudes y diferencias

**▸ Similitudes:** ambos modelos se utilizan para estructurar y entender las redes de computadoras y cómo los datos se transfieren a través de ellas. Ambos describen un conjunto de capas que separan las funciones de red para simplificar el diseño y la gestión.

**▸ Diferencias:** el modelo TCP/IP tiene cuatro capas más amplias y prácticas, orientadas a los protocolos reales implementados en Internet. En contraste, el modelo OSI tiene siete capas más detalladas y conceptuales, lo que facilita el entendimiento teórico, pero puede ser menos práctico en la implementación directa. El modelo TCP/IP se desarrolló a partir de la práctica y el desarrollo real de Internet, mientras que el modelo OSI se desarrolló como un marco teórico que se diseñó para ser aplicable a una amplia gama de tecnologías de red.

#### Proceso de encapsulamiento

El encapsulamiento es el proceso por el cual los datos se envuelven en capas de información a medida que se transmiten a través de la red. En el modelo TCP/IP, el encapsulamiento ocurre a nivel de cada capa para proporcionar el contexto necesario para la correcta transmisión y recepción de datos.

**▸ Capa de aplicación:** los datos generados por una aplicación se envían a la capa de aplicación. Aquí, los datos se preparan en el formato adecuado para la red, como una solicitud HTTP o un mensaje de correo electrónico.

**▸ Capa de transporte:** los datos de la capa de aplicación se pasan a la capa de transporte, donde se dividen en segmentos (en el caso de TCP) o datagramas (en el caso de UDP). La capa de transporte añade un encabezado que incluye información crucial como números de puerto (para identificar las aplicaciones de origen y destino), así como información sobre el control de flujo y corrección de errores.

**▸ Capa de Internet:** los segmentos o datagramas de la capa de transporte se envían a la capa de Internet. Aquí, los datos se encapsulan en paquetes y se añade un encabezado IP que incluye las direcciones IP de origen y destino. Este encabezado es crucial para el enrutamiento correcto de los paquetes a través de la red.

**▸ Capa de enlace de datos:** finalmente, los paquetes se envían a la capa de enlace de datos. En esta capa, los datos se encapsulan en tramas y se añade un encabezado y, a veces, un tráiler que contiene información de control de errores y dirección física (MAC). Las tramas son transmitidas a través del medio físico, como cables Ethernet u ondas de radio en una red wifi.

#### Proceso de desencapsulamiento

Al llegar al destino, el proceso de desencapsulamiento ocurre en orden inverso. Cada capa elimina su encabezado y pasa los datos a la capa superior, hasta que los datos originales son reconstruidos y entregados a la aplicación final.

#### Protocolos de la capa de transporte

La capa de transporte en el modelo TCP/IP es responsable de la entrega de datos de manera eficiente y confiable entre sistemas finales. Los dos principales protocolos en esta capa son TCP y UDP.

**▸ TCP (Transmission Control Protocol).**

- Confiabilidad: TCP proporciona una comunicación fiable. Asegura que los datos lleguen correctamente y en el orden correcto mediante la retransmisión de paquetes perdidos y la reorganización de paquetes desordenados.

- Control de flujo: TCP utiliza un mecanismo de control de flujo para evitar que un remitente envíe datos más rápido de lo que el receptor puede procesar. Este control se realiza mediante ventanas de congestión y ventanas de recepción.

- Segmentación y reensamblaje: los datos se dividen en segmentos TCP, cada uno de

Servicios en Red e Internet 74 Tema 1. Entrenamientos los cuales se envía por separado. TCP se encarga de reensamblar estos segmentos en el orden correcto al llegar al destino.

- Ejemplos de uso: aplicaciones que requieren alta fiabilidad, como la navegación web (HTTP/HTTPS), el correo electrónico (SMTP) y la transferencia de archivos (FTP).

**▸ UDP (User Datagram Protocol).**

- No confiabilidad: UDP proporciona una comunicación no fiable. No garantiza la entrega de paquetes, el orden de los paquetes ni la corrección de errores. Esto significa que los datos pueden llegar desordenados o perderse sin aviso.

- Control de flujo: UDP no incluye mecanismos de control de flujo o de congestión, lo que lo hace más rápido, pero menos seguro.

- Segmentación y reensamblaje: los datos se envían en datagramas independientes. No hay un proceso de reensamblaje garantizado en el destino.

- Ejemplos de uso: aplicaciones que pueden tolerar pérdidas de datos o que requieren baja latencia, como el *streaming* de vídeo en vivo, juegos en línea, y servicios de voz sobre IP (VoIP).

#### Función de las capas de red y de enlace de datos

**▸ Capa de red (Internet).** La capa de red se encarga del direccionamiento y enrutamiento de los paquetes a través de diferentes redes. Su objetivo principal es garantizar que los datos lleguen desde el origen hasta el destino a través de múltiples redes intermedias.

- Dirección IP: los paquetes en esta capa contienen una dirección IP de origen y una dirección IP de destino. Estas direcciones permiten a los rúteres y otros dispositivos de red identificar y enviar los paquetes hacia su destino correcto.

**▸**

- Enrutamiento: los rúteres operan en esta capa para decidir la mejor ruta para los paquetes de datos. Utilizan tablas de enrutamiento y algoritmos para determinar la ruta más eficiente.

- Protocolos: el principal protocolo de esta capa es IP (Internet Protocol), que puede ser IPv4 o IPv6. IPv4 es la versión más común, pero IPv6 está en expansión debido a la necesidad de más direcciones IP.

**▸ Capa de enlace de datos.** La capa de enlace de datos se ocupa de la transmisión de datos en una red local o punto a punto. Su función es proporcionar una comunicación libre de errores entre los dispositivos que están directamente conectados en la misma red física.

- Encapsulación en tramas: los paquetes de la capa de red se encapsulan en tramas de datos en esta capa. Las tramas incluyen información como direcciones MAC, que identifican los dispositivos en la red local.

- Control de errores: esta capa, a menudo, incluye mecanismos para detectar y corregir errores de transmisión mediante técnicas como el chequeo de redundancia cíclica (CRC).

- Protocolos: protocolos comunes en esta capa incluyen Ethernet para redes cableadas y 802.11 para redes inalámbricas. Ambos protocolos manejan el acceso al medio y la entrega de tramas a través de la red local.

#### Interacción entre capas

Las capas de red y de enlace de datos trabajan juntas para asegurar que los datos sean correctamente enviados desde un dispositivo en una red local hasta un destino en otra red, posiblemente a través de múltiples redes intermedias. Mientras la capa de red se encarga del enrutamiento y direccionamiento a nivel global, la capa de enlace de datos se enfoca en la transmisión local y la corrección de errores en el

Servicios en Red e Internet 76 Tema 1. Entrenamientos nivel de enlace físico.

#### Importancia y ejemplos de protocolos en la capa de aplicación

La capa de aplicación es la capa más cercana al usuario final y es responsable de proporcionar servicios de red directamente a las aplicaciones. Los protocolos en esta capa permiten la comunicación entre aplicaciones a través de la red, facilitando la interacción con los usuarios y otros sistemas.

Protocolos de la capa de aplicación:

**▸ HTTP (Hypertext Transfer Protocol).**

- Función: HTTP es el protocolo fundamental para la transferencia de datos en la web. Permite la transmisión de páginas web y otros recursos entre servidores web y navegadores.

- Importancia: es esencial para la navegación web y la entrega de contenido multimedia. Las solicitudes HTTP permiten a los usuarios acceder a sitios web, imágenes, vídeos y otros recursos en línea.

- Ejemplo de uso: navegadores web como Google Chrome y Mozilla Firefox utilizan HTTP para solicitar y recibir páginas web desde servidores.

**▸ FTP (File Transfer Protocol).**

- Función: FTP se utiliza para la transferencia de archivos entre sistemas a través de una red. Permite a los usuarios subir y descargar archivos desde y hacia un servidor FTP.

- Importancia: es crucial para la gestión de archivos en servidores, facilitando la transferencia de grandes volúmenes de datos.

- Ejemplo de uso: administradores de sistemas y desarrolladores utilizan FTP para cargar archivos a servidores web o descargar archivos de ellos.

**▸ DNS (Domain Name System).**

- Función: DNS traduce nombres de dominio legibles por humanos (como www.ejemplo.com) en direcciones IP numéricas que los dispositivos de red utilizan para identificar y comunicarse con otros sistemas.

- Importancia: es vital para la navegación web y la comunicación en red, ya que permite a los usuarios acceder a recursos utilizando nombres de dominio en lugar de direcciones IP.

- Ejemplo de uso: cuando un usuario escribe una URL en su navegador, DNS resuelve el nombre de dominio en una dirección IP para que el navegador pueda contactar al servidor web.

# Entrenamiento 4. Investiga los modelos TCP/IP y

# OSI a través de Cisco Packet Tracer

#### ▸ Planteamiento del ejercicio

Esta actividad de simulación tiene como objetivo ayudar a comprender el protocolo HTTP para TCP/IP y su relación con el modelo OSI. Usando el modo de simulación de Packet Tracer, se puede observar cómo los datos se envían a través de la red, dividiéndose en partes más pequeñas (unidades de datos de protocolo, PDU) que se identifican y asocian a capas específicas de los modelos TCP/IP y OSI. Esta simulación permite ver cada capa y su PDU correspondiente. Los pasos guían al usuario en el proceso de solicitar una página web desde un servidor utilizando un navegador en una PC cliente, brindando la oportunidad de explorar la funcionalidad de Packet Tracer y el proceso de encapsulación de datos.

#### ▸ Desarrollo paso a paso

- Examinar el tráfico Web HTTP.

- Cambiar al modo de simulación.

- Generar tráfico web (HTTP).

- Explorar el contenido del paquete HTTP.

#### ▸ Solución

#### Examinar el Tráfico Web HTTP

Debemos configurar un escenario simple en Packet Tracer que incluye un cliente y un servidor para generar y analizar tráfico HTTP. **▸ Abrir Packet Tracer.** Inicia el programa Packet Tracer en tu computadora. **▸ Añadir dispositivos.** En el área de trabajo, agrega los siguientes dispositivos:

- Un PC (desde la sección de end devices).

- Un server (desde la sección de end devices).

- Un switch (desde la sección de switches).

**▸ Conectar los dispositivos.**

- Usa un cable de cobre (`Copper Straight-Through`) para conectar:

- El PC a uno de los puertos del switch.

- El server a otro puerto del switch.

**▸ Configurar la IP del PC.**

- Haz clic en el PC.

- Ve a la pestaña Desktop y selecciona IP Configuration.

- Asigna la dirección IP: `192.168.1.2` y la máscara de subred: `255.255.255.0`.

- Cierra la ventana.

**▸ Configurar la IP del servidor.**

- Haz clic en el server.

- Ve a la pestaña Desktop y selecciona IP Configuration.

- Asigna la dirección IP: `192.168.1.1` y la máscara de subred: `255.255.255.0`.

- Cierra la ventana.

**▸ Activar el servicio HTTP.**

- Haz clic en el Server.

- Ve a la pestaña Services.

- Selecciona HTTP en el menú de la izquierda.

- Asegúrate de que la opción HTTP esté habilitada.

**▸ Crear una página web simple.**

- En la misma sección de HTTP en Services, puedes editar el contenido de la página de inicio (opcional) o dejar el contenido por defecto.

#### Cambiar al modo de simulación

Utilizaremos el modo de simulación de Packet Tracer (PT) para generar tráfico Web y examinar HTTP. PT siempre se inicia en el modo Realtime, en el que los protocolos de red operan con intervalos realistas. Sin embargo, una excelente característica de Packet Tracer permite que el usuario «detenga el tiempo» al cambiar al modo de simulación. En el modo de simulación, los paquetes se muestran como sobres animados, el tiempo se desencadena por eventos y el usuario puede avanzar por eventos de red.

**▸ Cambiar al modo de simulación.**

- Haga clic en el ícono de Simulation (Simulación) en la esquina inferior derecha de Packet Tracer.

**▸** Configurar los filtros de evento.

- En el panel de simulación, haga clic en Edit Filters (Editar filtros).

- Desmarque la opción Show All/None (mostrar todo/ninguno) para ocultar todos los eventos.

- Luego, seleccione HTTP para mostrar solo los eventos HTTP.

- Haga clic fuera del cuadro Edit Filters (editar filtros) para aplicar la configuración.

- Los eventos visibles ahora deben mostrar solo HTTP.

#### Generar tráfico web (HTTP)

El panel de simulación actualmente está vacío. En la parte superior de Event List (Lista de eventos) dentro del panel de simulación, se indican seis columnas. A medida que se genera y se revisa el tráfico, aparecen los eventos en la lista. La columna Info (Información) se utiliza para examinar el contenido de un evento determinado. Nota: el servidor Web y el cliente Web se muestran en el panel de la izquierda. Se puede ajustar el tamaño de los paneles manteniendo el ratón junto a la barra de desplazamiento y arrastrando a la izquierda o a la derecha cuando aparece la flecha de dos puntas.

**▸** Abrir el navegador web del cliente:

- Haga clic en el Web Client (cliente web) en el panel izquierdo.

- Seleccione la ficha Desktop (escritorio) y haga clic en el ícono Web Browser (explorador web).

**▸** Navegar a una URL:

**•** Introduzca www.osi.local en el campo de dirección URL y haga clic en Go (Ir).

- Use el botón Capture/Forward (capturar/avanzar) cuatro veces para generar y capturar los eventos HTTP.

**▸** Observaciones:

- Debe haber cuatro eventos en la lista de eventos. Observe la página del navegador web del cliente para verificar si ha cambiado.

#### Explorar el contenido del paquete HTTP

**▸** Ver el primer evento:

- Haga clic en el primer cuadro coloreado debajo de Event List > Info (Lista de eventos > Información).

Quizá sea necesario expandir el panel de simulación o usar la barra de desplazamiento que se encuentra directamente debajo de la lista de eventos. Se muestra la ventana PDU Information at Device: Web Client (Información de PDU en dispositivo: cliente Web). En esta ventana, solo hay dos fichas, OSI Model (Modelo OSI) y Outbound PDU Details (Detalles de PDU saliente), debido a que este es el inicio de la transmisión. A medida que se analizan más eventos, se muestran tres fichas, ya que se agrega la ficha Inbound PDU Details (Detalles de PDU entrante). Cuando un evento es el último evento del stream de tráfico, solo se muestran las fichas OSI Model e Inbound PDU Details.

**▸ Examinar el modelo OSI.**

- Asegúrese de que esté seleccionada la ficha OSI Model (Modelo OSI).

- Layer 7 (capa 7) debe estar resaltado. El texto junto a Layer 7, generalmente, indica HTTP.

- En Outbound PDU Details (Detalles de PDU saliente):

- Layer 4 (capa 4): el valor de Dst Port (Puerto de destino) es típicamente 80 para HTTP.

- Layer 3 (capa 3): el valor de Dest. IP (IP de destino) es la dirección IP del servidor web.

- Layer 2 (capa 2): la información mostrada incluirá Dest MAC (MAC de destino) y Src MAC (MAC de origen).

**▸ Detalles de PDU saliente.**

- Compare la información en la sección IP con la ficha OSI Model para identificar la correspondencia con Layer 3.

- Compare la información en la sección TCP con la ficha OSI Model para identificar la correspondencia con Layer 4.

- En la sección HTTP, el host indicado es el nombre del servidor web y se relaciona con Layer 7 en la ficha OSI Model.

**▸ Eventos de respuesta.**

- Haga clic en el siguiente cuadro de la columna Event List > Info.

- Compare In Layers (capas de entrada) con Out Layers (capas de salida) para ver las diferencias entre la solicitud enviada y la respuesta recibida.

- En el evento de respuesta, observe la primera línea del mensaje HTTP en la sección HTTP.

**▸ Último evento.**

- Haga clic en el último cuadro coloreado de Info.

- El número de fichas mostradas con este evento generalmente refleja el número de capas involucradas en la transmisión del paquete final.

Este procedimiento le permite examinar el tráfico HTTP de manera detallada en Packet Tracer, observando cómo los datos se encapsulan y se transmiten a través de las diferentes capas del modelo OSI.

# Entrenamiento 5. Mostrar elementos de la suite

# de protocolos TCP/IP a través de Cisco Packet Tracer

#### ▸ Planteamiento del ejercicio

Esta actividad de simulación tiene como objetivo ayudar a comprender la *suite* de protocolos TCP/IP. Usando el modo de simulación de Packet Tracer, se puede observar cómo los datos se envían a través de la red, dividiéndose en partes más pequeñas (unidades de datos de protocolo, PDU). Partiendo del ejercicio anterior, utilizaremos el modo de simulación de Packet Tracer para ver y examinar algunos de los otros protocolos que componen la *suite* TCP/IP.

#### ▸ Desarrollo paso a paso

- Configurar cliente y servidor en Packet Tracer.

- Configurar Filtros Evento. Ver eventos adicionales.

- Generar tráfico y analizar los paquetes.

#### ▸ Solución

Partiendo del escenario anterior en Packet Tracer, debemos configurar al servidor activando los servicios HTTP y DNS:

**▸ En el servidor:**

- Haz clic en el servidor.

- Ve a la pestaña Services.

- Activa los servicios de HTTP y DNS.

**•** En la configuración del servicio DNS, añade un registro: Name: www.osi.local; Address: 192.168.1.1 **▸ En el PC cliente:**

- Haz clic en el PC.

- Ve a la pestaña Desktop y selecciona Web Browser.

**•** Introduce la URL www.osi.local y deja la ventana abierta. Cambiar a modo simulación:

**▸** En la esquina inferior derecha de Packet Tracer, cambia el modo de Realtime (Tiempo Real) a Simulation (Simulación). Cierre todas las ventanas de información de PDU abiertas.

Configurar filtros de evento: **▸** Haz clic en Edit Filters en el panel de simulación. **▸** Selecciona Show All/None para desactivar todos los filtros. **▸** Luego selecciona ARP, DNS, TCP, HTTP para mostrar solo estos eventos. Tipos de eventos adicionales que se muestran: cuando haces clic en Show All (mostrar todo) en los filtros de eventos, puedes ver varios tipos de eventos adicionales que pertenecen a la *suite* de protocolos TCP/IP. Algunos de estos eventos pueden incluir: **▸** ARP (protocolo de resolución de direcciones): se utiliza para asociar una dirección IP con una dirección MAC. **▸** DNS (sistema de nombres de dominio): convierte nombres de dominio en direcciones IP. **▸** TCP (protocolo de control de transmisión): se encarga de establecer, gestionar y cerrar conexiones entre dispositivos. **▸** ICMP (protocolo de mensajes de control de Internet): utilizado por herramientas como ping para enviar mensajes de error y otros tipos de notificaciones. Generar tráfico: **▸** En la ventana del navegador web del PC, haz clic en Go para intentar acceder a www.osi.local. **▸** Usa el botón Capture/Forward en el modo de simulación para capturar y analizar los paquetes. Información de la consulta DNS (primer evento DNS): al hacer clic en el primer evento de DNS en la columna Info, en la ficha OSI Model con la capa 7 resaltada, se

Servicios en Red e Internet 88 Tema 1. Entrenamientos muestra una descripción que dice: «El cliente DNS envía una consulta DNS al servidor DNS».

Información en la sección DNS QUERY: en la ficha Outbound PDU Details (detalles de PDU saliente), en la sección DNS QUERY (consulta DNS), la información que se indica en NAME: (NOMBRE:) es el dominio que el cliente está intentando resolver, por ejemplo, www.osi.local.

Último evento de DNS en la lista de eventos:

**▸** Dispositivo mostrado:

- El dispositivo que se muestra es el servidor DNS.

**▸** Valor junto a ADDRESS: (dirección) en DNS ANSWER:

- El valor que se indica junto a ADDRESS: (DIRECCIÓN:) en la sección DNS ANSWER (Respuesta de DNS) en Inbound PDU Details es la dirección IP asociada con el nombre de dominio que fue solicitado, por ejemplo, 192.168.1.1.

Información en los elementos 4 y 5 del evento TCP:

**▸** Al buscar el primer evento de HTTP en la lista y hacer clic en el cuadro coloreado del evento de TCP que le sigue inmediatamente.

**▸** En la Layer 4 (capa 4) del modelo OSI, los elementos 4 y 5 que se muestran, generalmente, son:

- Elemento 4: detalles del puerto de destino, que típicamente es el puerto 80 para el protocolo HTTP.

- Elemento 5: detalles del puerto de origen, que es un puerto dinámico asignado para la comunicación.

Propósito del último evento TCP:

**▸** Al hacer clic en el último evento de TCP y resaltar la Layer 4 (capa 4) en la ficha OSI Model:

- El propósito del evento, según la información proporcionada en el último elemento de la lista, es cerrar la conexión TCP. Este paso indica que la sesión de comunicación entre el cliente y el servidor es finalizada correctamente, con un mensaje como «La sesión TCP se cierra», lo que asegura que la comunicación se ha completado y la conexión termina de manera ordenada.

Después de realizar estos pasos, deberías ver cómo se resuelve la dirección www.osi.local a una IP, cómo se establece la conexión TCP y cómo se envían y reciben paquetes HTTP. En el modo de simulación, podrás analizar cada uno de estos eventos en detalle.

Este escenario te permitirá capturar y analizar los diferentes protocolos que componen la *suite* TCP/IP, cumpliendo con los requisitos de la segunda parte del ejercicio.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–42)*
- A fondo  *(pp.43–47)*
- Entrenamientos  *(pp.48–91)*
- Servicios en Red e Internet 5 Tema 1. Material de estudio · Servicios en Red e Internet 6 Tema 1. Material de estudio · Servicios en Red e Internet 7 Tema 1. Material de estudio · Servicios en Red e Internet 8 Tema 1. Material de estudio · Servicios en Red e Internet 9 Tema 1. Material de estudio · Servicios en Red e Internet 10 Tema 1. Material de estudio · Servicios en Red e Internet 12 Tema 1. Material de estudio · Servicios en Red e Internet 13 Tema 1. Material de estudio · Servicios en Red e Internet 14 Tema 1. Material de estudio · Servicios en Red e Internet 15 Tema 1. Material de estudio · Servicios en Red e Internet 16 Tema 1. Material de estudio · Servicios en Red e Internet 17 Tema 1. Material de estudio · Servicios en Red e Internet 18 Tema 1. Material de estudio · Servicios en Red e Internet 19 Tema 1. Material de estudio · Servicios en Red e Internet 20 Tema 1. Material de estudio · Servicios en Red e Internet 21 Tema 1. Material de estudio · Servicios en Red e Internet 22 Tema 1. Material de estudio · Servicios en Red e Internet 23 Tema 1. Material de estudio · Servicios en Red e Internet 24 Tema 1. Material de estudio · Servicios en Red e Internet 25 Tema 1. Material de estudio · Servicios en Red e Internet 26 Tema 1. Material de estudio · Servicios en Red e Internet 27 Tema 1. Material de estudio · Servicios en Red e Internet 28 Tema 1. Material de estudio · Servicios en Red e Internet 29 Tema 1. Material de estudio · Servicios en Red e Internet 30 Tema 1. Material de estudio · Servicios en Red e Internet 31 Tema 1. Material de estudio · Servicios en Red e Internet 32 Tema 1. Material de estudio · Servicios en Red e Internet 33 Tema 1. Material de estudio · Servicios en Red e Internet 34 Tema 1. Material de estudio · Servicios en Red e Internet 35 Tema 1. Material de estudio · Servicios en Red e Internet 36 Tema 1. Material de estudio · Servicios en Red e Internet 37 Tema 1. Material de estudio · Servicios en Red e Internet 38 Tema 1. Material de estudio · Servicios en Red e Internet 39 Tema 1. Material de estudio · Servicios en Red e Internet 40 Tema 1. Material de estudio · Servicios en Red e Internet 41 Tema 1. Material de estudio · Servicios en Red e Internet 42 Tema 1. Material de estudio  *(pp.5, 6, 7, 8, 9, 10, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42)*
- Servicios en Red e Internet 43 Tema 1. A fondo · Servicios en Red e Internet 44 Tema 1. A fondo · Servicios en Red e Internet 45 Tema 1. A fondo · Servicios en Red e Internet 46 Tema 1. A fondo · Servicios en Red e Internet 47 Tema 1. A fondo  *(pp.43–47)*
- Servicios en Red e Internet 48 Tema 1. Entrenamientos · Servicios en Red e Internet 49 Tema 1. Entrenamientos · Servicios en Red e Internet 50 Tema 1. Entrenamientos · Servicios en Red e Internet 52 Tema 1. Entrenamientos · Servicios en Red e Internet 53 Tema 1. Entrenamientos · Servicios en Red e Internet 54 Tema 1. Entrenamientos · Servicios en Red e Internet 55 Tema 1. Entrenamientos · Servicios en Red e Internet 56 Tema 1. Entrenamientos · Servicios en Red e Internet 57 Tema 1. Entrenamientos · Servicios en Red e Internet 58 Tema 1. Entrenamientos · Servicios en Red e Internet 59 Tema 1. Entrenamientos · Servicios en Red e Internet 60 Tema 1. Entrenamientos · Servicios en Red e Internet 61 Tema 1. Entrenamientos · Servicios en Red e Internet 62 Tema 1. Entrenamientos · Servicios en Red e Internet 64 Tema 1. Entrenamientos · Servicios en Red e Internet 67 Tema 1. Entrenamientos · Servicios en Red e Internet 68 Tema 1. Entrenamientos · Servicios en Red e Internet 69 Tema 1. Entrenamientos · Servicios en Red e Internet 70 Tema 1. Entrenamientos · Servicios en Red e Internet 71 Tema 1. Entrenamientos · Servicios en Red e Internet 72 Tema 1. Entrenamientos · Servicios en Red e Internet 73 Tema 1. Entrenamientos · Servicios en Red e Internet 75 Tema 1. Entrenamientos · Servicios en Red e Internet 77 Tema 1. Entrenamientos · Servicios en Red e Internet 78 Tema 1. Entrenamientos · Servicios en Red e Internet 79 Tema 1. Entrenamientos · Servicios en Red e Internet 80 Tema 1. Entrenamientos · Servicios en Red e Internet 81 Tema 1. Entrenamientos · Servicios en Red e Internet 82 Tema 1. Entrenamientos · Servicios en Red e Internet 83 Tema 1. Entrenamientos · Servicios en Red e Internet 84 Tema 1. Entrenamientos · Servicios en Red e Internet 85 Tema 1. Entrenamientos · Servicios en Red e Internet 86 Tema 1. Entrenamientos · Servicios en Red e Internet 87 Tema 1. Entrenamientos · Servicios en Red e Internet 89 Tema 1. Entrenamientos · Servicios en Red e Internet 90 Tema 1. Entrenamientos · Servicios en Red e Internet 91 Tema 1. Entrenamientos  *(pp.48, 49, 50, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 64, 67, 68, 69, 70, 71, 72, 73, 75, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 89, 90, 91)*