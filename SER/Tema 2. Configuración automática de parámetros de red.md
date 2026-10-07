## Tema 2

# Servicios en Red e Internet

# Tema 2. Configuración automática de parámetros

# de red

# Índice

Esquema Material de estudio

## 2.1. Introducción y objetivos

## 2.2. Características

## 2.3. Cliente y servidor DHCP

## 2.4. Tipos de asignaciones

## 2.5. Conceptos servidor DHCP

## 2.6. Configuraciones de red

## 2.7. Funcionamiento del protocolo DHCP

## 2.8. Ventajas y desventajas

A fondo Qué es el DHCP, funcionamiento y ejemplos de configuración Configurar servidor DHCP en Windows Server 2022 Guía de solución de problemas de DHCP Cómo habilitar y configurar un servidor DHCP Qué es DHCP y cómo instalar un servidor en Ubuntu Cómo gestionar tus ámbitos de DHCP El DHCP y la configuración de redes Entrenamientos Entrenamiento 1. Preguntas relacionadas con el servicio DHCP

Entrenamiento 2. Instalación y configuración de servicio DHCP en Windows

Entrenamiento 3. Instalación y configuración de servicio DHCP en Ubuntu

Entrenamiento 4. Configuración particular de un servidor DHCP con Windows

Entrenamiento 5. Configuración particular de un servidor DHCP con Ubuntu trabajando con un cliente Ubuntu

# Esquema

![image-2](images/image-2.png)

Servicios en Red e Internet 4 Tema 2. Esquema

# 2.1. Introducción y objetivos

La configuración automática de parámetros de red es una **solución esencial** para la gestión eficiente de una red, especialmente, en entornos grandes y complejos como empresas y organizaciones con múltiples dispositivos. En muchos casos, el administrador de red tiene la responsabilidad de configurar parámetros de red para decenas o, incluso, centenas de dispositivos, incluyendo estaciones de trabajo, servidores, impresoras en red, dispositivos inalámbricos, entre otros.

Estos dispositivos pueden estar ubicados en diferentes salas, pisos de un edificio o, incluso, ser dispositivos móviles. Configurar manualmente cada uno de estos dispositivos no solo sería una tarea tediosa y poco productiva, sino que también implicaría una carga de trabajo muy elevada para el administrador de red. Este proceso manual representaría una considerable pérdida de tiempo y no aprovecharía de manera óptima la disponibilidad del administrador para otras tareas posiblemente más importantes o urgentes.

La solución a este problema es la implementación del denominado **servicio de** **configuración automática de parámetros de red,** que permite la gestión de estos parámetros de manera automática y centralizada. Este servicio utiliza **protocolos** **específicos y tecnologías diseñadas** para simplificar y automatizar la configuración de los dispositivos de red. Un ejemplo destacado de esto es el protocolo DHCP (Dynamic Host Configuration Protocol), que permite asignar automáticamente direcciones IP y otros parámetros de red a los dispositivos.

E l **DHCP** es fundamental en cualquier red moderna. Cuando un dispositivo se conecta a la red, envía una solicitud de DHCP para obtener una dirección IP y otros parámetros necesarios, como la máscara de subred, la puerta de enlace predeterminada y los servidores DNS. El servidor DHCP responde a esta solicitud asignando una dirección IP disponible y proporcionando los demás parámetros. Este

Servicios en Red e Internet 5 Tema 2. Material de estudio proceso es completamente automático y se realiza en cuestión de segundos, lo que **ahorra tiempo** y **reduce** la posibilidad de **errores humanos** en la configuración manual.

Además del DHCP, existen otras herramientas y tecnologías que facilitan la configuración automática de parámetros de red. Por ejemplo, en redes más grandes y complejas, se pueden utilizar **sistemas de gestión de red (NMS),** que permiten supervisar y configurar dispositivos de manera centralizada. Estos sistemas pueden integrar diversas funciones, como la supervisión del rendimiento de la red, la gestión de configuraciones y la implementación de políticas de seguridad.

En el contexto de esta asignatura, la comprensión y aplicación de estas tecnologías es crucial. Los estudiantes deben aprender a implementar y gestionar servicios de configuración automática de parámetros de red, así como a solucionar problemas comunes asociados con la configuración de red. Esto incluye configurar y administrar servidores DHCP, implementar políticas de asignación de direcciones IP y utilizar herramientas de gestión de red para supervisar y mantener la infraestructura de red.

La automatización de la configuración de parámetros de red no solo mejora la eficiencia operativa, sino que también contribuye a una **mayor seguridad y** **estabilidad de la red.** Al reducir la intervención manual, se minimizan los errores de configuración que podrían dar lugar a vulnerabilidades de seguridad. Además, la capacidad de gestionar de manera centralizada permite una respuesta más rápida a incidentes y una mejor planificación y optimización de recursos de red.

En resumen, la configuración automática de parámetros de red es una práctica esencial en la administración moderna de redes. Permite una gestión más eficiente, reduce la carga de trabajo del administrador de red y mejora la seguridad y estabilidad de la infraestructura de red. En la formación de ASIR, adquirir habilidades en esta área prepara a los futuros administradores de sistemas para enfrentar los desafíos de redes complejas y dinámicas en el entorno laboral actual.

Los **objetivos** que se pretende alcanzar en este tema son: **▸** Permitir que las interfaces de red de los dispositivos obtengan los parámetros de red automáticamente y sin intervención del usuario. **▸** Facilitar la configuración y administración de la red. **▸** Reducir la carga de trabajo en la gestión de dispositivos conectados. **▸** Automatizar la asignación de configuraciones, simplificando la administración de redes. **▸** Gestionar la asignación de configuraciones de red, controlando cuántas configuraciones se han dado, a qué interfaces se han asignado y por cuánto tiempo. **▸** Evitar conflictos de dirección IP mediante la configuración cuidadosa de servidores DHCP. **▸** Implementar el servicio DHCP en diferentes sistemas operativos. **▸** Configurar correctamente los servidores DHCP comprendiendo conceptos clave, como ámbito, rango, exclusiones, tiempo de concesión, tiempo de renovación, tiempo de reconexión y reservas.

**▸** Optimizar el uso de direcciones IP.

**▸** Automatizar todo el proceso de gestión de la red.

**▸** Minimizar errores humanos y conflictos de IP.

# 2.2. Características

¿Qué es este servicio?

El servicio de configuración automática de parámetros de red, comúnmente conocido como DHCP (Dynamic Host Configuration Protocol), permite que las interfaces de red de los dispositivos (como estaciones de trabajo, servidores, impresoras en red y dispositivos inalámbricos) obtengan los **parámetros de red automáticamente** y **sin** **intervención del usuario.** Esto significa que cada dispositivo que necesite una configuración de red para comunicarse con otros dispositivos recibirá esa configuración de forma automática al encenderse, sin necesidad de ajustes manuales. El proceso es transparente para el usuario, quien no será consciente de esta configuración automática y podrá utilizar el dispositivo sin problemas.

Aunque no es obligatorio usar este servicio y, en algunos casos, puede ser preferible una configuración manual, generalmente facilita la configuración y administración de la red, reduciendo la carga de trabajo en la gestión de dispositivos conectados.

Historia y funcionalidad

El servicio DHCP se basa en un protocolo de la capa de aplicación que facilita la asignación automática de direcciones IP y otros parámetros de red a dispositivos dentro de una red. Este protocolo, diseñado por el **IETF** (Internet Engineering Task Force), fue publicado en 1993 y está especificado en el RFC 2131. Para redes IPv6, existe el protocolo DHCPv6, que está definido en el RFC 3315.

DHCP no es un protocolo completamente nuevo; es una **extensión del protocolo** **BOOTP** (Bootstrap Protocol), que era utilizado previamente para configurar redes en dispositivos sin almacenamiento suficiente para mantener su propio sistema operativo, como los primeros rúteres. Sin embargo, BOOTP resulta menos eficiente en redes modernas debido a su tamaño y a la necesidad de intervención manual para asignar direcciones IP, lo que lo hace menos adecuado para el entorno actual.

A diferencia de BOOTP, DHCP funciona a nivel de la capa de aplicación del modelo OSI (Open System Interconnection) y opera bajo un modelo cliente/servidor. En este sistema, los dispositivos sin configuración de red (clientes) envían solicitudes de configuración a un servidor DHCP, que responde con los parámetros de red necesarios. Este enfoque simplifica la administración de redes al automatizar la asignación de configuraciones, lo que es particularmente útil en redes grandes o heterogéneas.

DHCP es un **protocolo multiplataforma,** lo que significa que puede ser implementado en una variedad de sistemas operativos, incluidos Windows, Linux, macOS y sistemas operativos móviles como Android. Los sistemas operativos deben ser posteriores a la introducción del protocolo para garantizar la compatibilidad; por ejemplo, Windows comenzó a usar DHCP con Windows 98 y Linux con versiones posteriores a 1993.

En términos de funcionamiento, DHCP utiliza el **protocolo UDP** (User Datagram Protocol) para la **comunicación de datos.** El servidor DHCP escucha en el puerto 67 para recibir solicitudes de los clientes y responde en el puerto 68. Por lo tanto, es importante gestionar adecuadamente los cortafuegos para permitir el tráfico en estos puertos tanto en el servidor como en los clientes. En la mayoría de los casos, estos puertos están abiertos por defecto debido a la popularidad del servicio, pero en redes con cortafuegos estrictos, puede ser necesario configurarlos manualmente para asegurar la correcta comunicación entre los dispositivos y el servidor DHCP.

# 2.3. Cliente y servidor DHCP

Cliente DHCP

El término cliente DHCP puede no ser ampliamente conocido, pero es una **función** **integral** en los sistemas operativos modernos, introducido en Windows 98 para los sistemas operativos de Microsoft y disponible desde 1993 en distribuciones de Linux, Un cliente DHCP es una aplicación que permite a un dispositivo solicitar automáticamente configuraciones de red a un servidor DHCP.

Esto facilita la configuración de los adaptadores de red de manera automática y transparente, sin necesidad de instalaciones adicionales en los dispositivos, ya que esta funcionalidad viene preinstalada en los sistemas operativos actuales.

![Figura 1. Configuración automática en Windows y Ubuntu. Fuente: elaboración propia.](images/image-3.png)

*Figura 1. Configuración automática en Windows y Ubuntu. Fuente: elaboración propia.*

Servidor DHCP

Los servidores DHCP son aplicaciones cruciales instaladas en dispositivos para proporcionar configuraciones de red a otros dispositivos que las soliciten. Estas aplicaciones **gestionan la asignación de configuraciones de red,** controlando

Servicios en Red e Internet 10 Tema 2. Material de estudio cuántas configuraciones se han dado, a qué interfaces se han asignado y por cuánto tiempo. En ocasiones, el término servidor DHCP, también, se refiere al dispositivo físico que alberga esta aplicación.

#### Tipos de Servidores DHCP

Actualmente, en el mercado del *software,* hay varias aplicaciones que permiten configurar un dispositivo como servidor DHCP y la elección de la aplicación adecuada depende del sistema operativo del dispositivo que se desea configurar.

Para **sistemas operativos** de la familia **Microsoft,** como Windows Server 2008 o Windows Server 2012, Microsoft proporciona herramientas nativas para implementar el servicio DHCP. En estos sistemas, se utiliza una **característica integrada** conocida como **rol o función,** dependiendo de la versión del sistema operativo.

**▸ Windows Server 2008 y versiones anteriores:** la funcionalidad DHCP se instala como un rol adicional que se puede agregar mediante el administrador del servidor.

Después de agregar el rol, se debe configurar el servidor DHCP mediante la consola de administración DHCP, donde se definen los rangos de direcciones IP, las opciones de configuración y las reservas de direcciones.

**▸ Windows Server 2012 y versiones posteriores:** el proceso es similar, pero la terminología puede variar ligeramente. Aquí, la funcionalidad se denomina función y se agrega a través del administrador del servidor. Una vez instalado, se utiliza la consola de administración DHCP para gestionar y configurar las direcciones IP y otras opciones relacionadas.

En ambos casos, el rol o función DHCP de Microsoft proporciona una **interfaz** **gráfica amigable** que facilita la configuración y gestión del servidor DHCP, permitiendo a los administradores configurar rangos de direcciones IP, opciones de red y gestionar la concesión de IP de manera eficiente.

Para **sistemas operativos basados en Linux,** como Ubuntu Server, CentOS, o Debian, la configuración del servidor DHCP se realiza mediante la instalación de paquetes específicos desde los repositorios de *software.*

**▸ Ubuntu Server y Debian:** en estas distribuciones, se puede instalar el servidor DHCP utilizando el paquete isc-dhcp-server . La instalación se realiza típicamente con el gestor de paquetes APT mediante el comando sudo apt-get install isc-dhcp-server . Una vez instalado, se debe configurar el archivo de configuración principal, usualmente ubicado en /etc/dhcp/dhcpd.conf , donde se definen los rangos de direcciones IP, las opciones de configuración y las políticas de concesión de IP.

**▸ CentOS y Red Hat Enterprise Linux (RHEL):** para estas distribuciones, el paquete recomendado es dhcp o dhcp-server . La instalación se realiza mediante el gestor de

paquetes YUM o DNF con el comando sudo yum install dhcp o sudo dnf install dhcp . Al

igual que en Ubuntu, la configuración se realiza en el archivo /etc/dhcp/dhcpd.conf . Después de configurar el archivo, se deben iniciar y habilitar los servicios DHCP

usando comandos como sudo systemctl start dhcpd y sudo systemctl enable dhcpd .

Por otro lado, la mayoría de los **rúteres comerciales** disponibles para redes empresariales y domésticas incluyen un *firmware* que permite que el rúter funcione como un servidor DHCP, proporcionando configuraciones de red a los dispositivos conectados a la red local. Este ***firmware*** **integrado** facilita la conexión y configuración de dispositivos sin necesidad de *software* adicional, lo que simplifica la gestión de redes locales conectadas a Internet.

Sin embargo, cuando se tienen múltiples dispositivos capaces de ofrecer el servicio DHCP, como varios rúteres, puntos de acceso inalámbrico o servidores en la misma red, es crucial configurarlos cuidadosamente para **evitar conflictos de dirección IP.** Estos conflictos pueden surgir porque un servidor DHCP no tiene conocimiento de las asignaciones realizadas por otro servidor DHCP, lo que puede resultar en que dos dispositivos reciban la misma dirección IP.

Para prevenir estos problemas, es recomendable seguir estas **prácticas:**

**▸ Único servidor DHCP:** mantener un único servidor DHCP activo en la red es la mejor práctica para evitar conflictos de IP. Este servidor será el único responsable de asignar direcciones IP a todos los dispositivos de la red.

**▸ Deshabilitar DHCP en otros dispositivos:** en rúteres y otros dispositivos que vienen con el servicio DHCP activado por defecto, se debe desactivar esta función si no se desea que actúen como servidores DHCP. Esto se realiza accediendo a la configuración del rúter y deshabilitando el servicio DHCP desde la interfaz de administración del *firmware.*

**▸ Configuraciones de fábrica:** muchos rúteres comerciales tienen el servicio DHCP activado de fábrica. Al instalar un nuevo rúter en una red existente, es esencial revisar la configuración por defecto y deshabilitar el servicio DHCP si ya existe otro servidor DHCP en la red.

**▸ Rangos de IP y reservas:** si por alguna razón se requiere más de un servidor

DHCP en la red, una alternativa es configurar cada servidor para que gestione rangos de IP distintos y no superpuestos. Adicionalmente, se pueden utilizar reservas de IP específicas para ciertos dispositivos para garantizar que cada dispositivo siempre reciba la misma dirección IP sin conflictos (todo esto lo veremos posteriormente).

# 2.4. Tipos de asignaciones

Los servidores DHCP utilizan el protocolo DHCP para asignar automáticamente configuraciones de red a los clientes que las solicitan. Además de realizar estas asignaciones, los servidores también las gestionan y supervisan, manteniendo un **registro de las asignaciones** realizadas.

El protocolo DHCP define **tres tipos** de asignación de configuraciones de red, permitiendo al administrador de la red seleccionar la más adecuada según las necesidades específicas de la red:

**▸** Asignación dinámica y limitada.

**▸** Asignación automática e ilimitada.

**▸** Asignación estática con reserva.

Asignación dinámica y limitada

En este tipo de asignación, el servidor DHCP asigna una configuración de red a un dispositivo de forma automática y por un tiempo limitado, conocido como **tiempo de** **concesión.** Durante este período, solo la interfaz de red del dispositivo puede usar dicha configuración.

Al finalizar el tiempo de concesión, pueden ocurrir dos situaciones:

**▸** La interfaz de red puede renovar y continuar usando la misma configuración.

**▸** La configuración puede ser reasignada a otra interfaz de red que lo necesite.

Este tipo de asignación es el más común, especialmente entre los proveedores de servicios de Internet (ISP), ya que permite **reutilizar configuraciones de red** que no están en uso, siendo ideal para redes con dispositivos móviles o con un número de dispositivos no predecible.

Asignación automática e ilimitada

En esta modalidad, el servidor DHCP también asigna configuraciones de red de forma automática, pero sin limitación temporal. La asignación es **permanente,** es decir, la interfaz de red retiene la configuración hasta que esta sea liberada por la propia interfaz.

Este tipo de asignación se usa en entornos con un **número fijo o casi fijo** de dispositivos, como en oficinas pequeñas y oficinas en casa (SOHO).

Asignación estática con reserva

La asignación estática con reserva se asemeja a una configuración manual, asignando siempre la misma configuración de red a ciertas interfaces. Para ello, se utilizan filtros MAC (Media Access Control), que identifican unívocamente a los adaptadores de red.

Este tipo de asignación se emplea para dispositivos que necesitan **identificarse** **consistentemente** en la red, como servidores, impresoras en red y rúteres. Al configurarse el servidor DHCP con reservas, estos dispositivos siempre reciben la misma configuración de red, evitando confusiones entre los clientes.

Las asignaciones estáticas con reserva se utilizan en combinación con asignaciones dinámicas y limitadas, reservándose para dispositivos críticos que requieren una identificación constante, mientras que el resto de los dispositivos utilizan asignaciones dinámicas y limitadas.

# 2.5. Conceptos servidor DHCP

Para configurar correctamente los servidores DHCP, es esencial comprender varios conceptos clave.

Ámbito

El concepto de ámbito proviene de los servidores DHCP en sistemas operativos de la familia Microsoft. En Linux, no se usa este término directamente. El ámbito se refiere al conjunto de direcciones IP que el servidor DHCP puede gestionar y asignar a los clientes que solicitan configuraciones de red. Es importante que el ámbito pertenezca a la misma red que el servidor DHCP.

Por ejemplo, si el servidor DHCP está en la red 192.168.110.0/24, considere un ámbito DHCP con una dirección IP inicial de 192.168.110.100 y una dirección IP final de 192.168.110.200. Este alcance proporcionaría un conjunto de 101 direcciones IP (192.168.110.100 – 192.168.110.200) que se pueden asignar dinámicamente a dispositivos cliente en la red.

Rango

El rango también se refiere a un conjunto de direcciones IP, pero específicamente al **subconjunto de direcciones** dentro del ámbito que el servidor DHCP asignará a los clientes. El rango debe estar dentro del ámbito.

Por ejemplo, si el servidor DHCP está en la red 192.168.110.0/24 y presenta un ámbito DHCP de 192.168.110.10 – 192.168.110.100, el rango puede estar formado por un conjunto continuo de direcciones IP (por ejemplo, 192.168.110.12 - 192.168.110.100) o por varios conjuntos contiguos (por ejemplo, 192.168.110.12 - 192.168.110.25, 192.168.110.30

- 192.168.110.40). Es crucial que en redes con varios servidores DHCP,

los rangos no se solapen para evitar conflictos de dirección IP.

Exclusiones

Las exclusiones, un concepto también de Microsoft, se refieren a direcciones IP dentro del rango que el servidor DHCP **no debe asignar.**

Por ejemplo, si el rango es 192.168.10.69 - 192.168.10.80 y se excluye la dirección 192.168.10.75, el servidor podrá asignar direcciones entre 192.168.10.69 y 192.168.10.80, excepto la 192.168.10.75. Esto es útil para ajustar configuraciones activas, como cambios en la puerta de enlace o nuevas reservas.

Tiempo de concesión

El tiempo de concesión, o *lease time,* es el período durante el cual el servidor DHCP a s i g n a **una configuración de red a un cliente.** Durante este tiempo, la configuración está bloqueada y no puede ser reasignada a otra interfaz de red. El administrador debe ajustar el tiempo de concesión según las características de la red: un tiempo corto aumenta el tráfico DHCP, mientras que un tiempo largo puede desaprovechar las direcciones IP disponibles.

Tiempo de renovación

El tiempo de renovación, o *renewal time,* es la **mitad del tiempo de concesión.** Cuando se alcanza este tiempo, el cliente intenta renovar la concesión de su configuración de red. Si la renovación es exitosa, se extiende la concesión por un nuevo período igual al tiempo de concesión. Si no, el cliente deberá solicitar una nueva configuración antes de que expire la concesión original.

Tiempo de reconexión

El tiempo de reconexión, o *rebinding time,* es el 87,5 % del tiempo de concesión. Si no se ha logrado renovar la concesión en el tiempo de renovación, el cliente debe solicitar una nueva configuración de red cuando alcanza el tiempo de reconexión. Esto garantiza que el cliente tenga suficiente tiempo para obtener una nueva configuración antes de que expire la concesión actual.

Reservas

Las reservas están relacionadas con la **asignación estática** con reserva y se definen como direcciones IP asignadas permanentemente a interfaces de **red** **específicas,** identificadas mediante su dirección MAC. Las reservas se utilizan para dispositivos que necesitan ser identificados consistentemente en la red, como servidores, puertas de enlace e impresoras en red.

Estos conceptos son fundamentales para una configuración eficiente y efectiva de un servidor DHCP, asegurando que las redes operen sin conflictos y con una gestión adecuada de las direcciones IP.

# 2.6. Configuraciones de red

El servidor DHCP (Dynamic Host Configuration Protocol) se encarga de asignar configuraciones de red automáticamente y de manera transparente a las interfaces de red de los dispositivos que las solicitan. Pero, ¿qué es exactamente una configuración de red?

Una configuración de red es un conjunto de parámetros necesarios para que las interfaces de red de los dispositivos puedan comunicarse entre

sí.

Estos parámetros se dividen en dos **categorías principales:** configuración básica y configuración extra.

Configuración básica

La configuración básica incluye los **parámetros mínimos** necesarios para que una interfaz de red pueda comunicarse con otra. Estos parámetros son:

**▸ Dirección IP:** un identificador único para la interfaz de red en la red.

**▸ Máscara de red:** define la porción de la dirección IP que identifica la red y la porción que identifica el host en esa red.

**▸ Tiempo de concesión:** en asignaciones dinámicas y limitadas, especifica el período durante el cual la dirección IP es válida. Los tiempos de renovación y reconexión están asociados al tiempo de concesión.

Configuración extra

La configuración extra, además de los parámetros de la configuración básica, incluye **parámetros adicionales** que proporcionan servicios adicionales a los adaptadores de red de los dispositivos que solicitan configuraciones. Algunos de estos parámetros pueden ser:

**▸ Direcciones IP de Servidores DNS(Domain Name Service):** permiten la resolución de nombres de dominio a direcciones IP.

**▸ Nombre de dominio:** el dominio al cual pertenece la red.

**▸** ***Gateway*** **o puerta de enlace:** la dirección IP del dispositivo que permite la comunicación con otras redes.

**▸ Direcciones IP de servidores SMTP (Simple Mail Transfer Protocol):** facilitan el envío de correos electrónicos.

**▸ Otros parámetros adicionales:** pueden incluir direcciones IP de servidores NTP (Network Time Protocol) para sincronización de tiempo, opciones de servidor de impresión, y otros servicios de red.

# 2.7. Funcionamiento del protocolo DHCP

El protocolo DHCP define un **proceso detallado** para que un cliente obtenga una configuración de red, renueve una concesión y se reconecte en caso de fallos. En cada caso, este proceso se gestiona mediante una serie de **mensajes específicos** entre el cliente y los servidores DHCP:

![Figura 2. Mensajes específicos entre el cliente y los servidores DHCP. Fuente: elaboración propia.](images/image-4.png)

*Figura 2. Mensajes específicos entre el cliente y los servidores DHCP. Fuente: elaboración propia.*

Ciclo básico

El ciclo básico del protocolo DHCP abarca desde la solicitud inicial de una configuración de red hasta la asignación exitosa de dicha configuración.

**▸ Estado inicial:**

- Cuando una interfaz de red no tiene ninguna configuración asignada, su dirección IP es 0.0.0.0. En este estado, el cliente envía mensajes DHCPDISCOVER por difusión (255.255.255.255) para descubrir servidores DHCP disponibles en la red.

- Si no recibe una respuesta, el cliente continúa enviando mensajes DHCPDISCOVER hasta obtener una respuesta o hasta alcanzar el límite de reintentos. Si no se obtiene respuesta, el cliente puede usar el protocolo APIPA (RFC 3927) para autoasignarse una IP en el rango 169.254.x.x con máscara 255.255.0.0 (por lo tanto, si una interfaz de red presenta una dirección del rango expuesto anteriormente, es posible que haya algún problema con el servidor DHCP).

**▸ Estado de inicialización:**

- Los servidores DHCP que reciben mensajes DHCPDISCOVER envían DHCPOFFER con una propuesta de configuración de red.

**▸ Estado de selección:**

- El cliente selecciona la primera oferta recibida (por lo que el servidor más cercano o más rápido será el seleccionado) y envía un DHCPREQUEST por difusión indicando su elección.

**▸ Estado de solicitud:**

- El servidor DHCP correspondiente responde con un DHCPACK confirmando la asignación. Si hay un problema, el servidor envía un DHCPNACK, lo que hace que el cliente vuelva al estado inicial (1).

**▸ Estado de enlace:**

- Antes de aceptar la configuración, el cliente realiza una verificación ARP para asegurarse de que la dirección IP no está en uso. Si no hay respuesta, la IP se considera libre y se asigna al cliente. Si recibe una respuesta ARP, envía un DHCPDECLINE y vuelve al estado inicial (1).

![Figura 3. Ciclo básico de asignación de IP mediante DHCP. Fuente: elaboración propia.](images/image-5.png)

*Figura 3. Ciclo básico de asignación de IP mediante DHCP. Fuente: elaboración propia.*

Renovación

**▸ Estado de renovación:**

- Cuando se alcanza el 50 % del tiempo de concesión, el cliente envía un DHCPREQUEST unicast al servidor para renovar la concesión.

- Si el servidor responde con un DHCPACK, la concesión se renueva. Si no hay respuesta, el cliente no puede renovar la concesión.

Reenlace

![Figura 4. Proceso de renovación. Fuente: elaboración propia.](images/image-6.png)

*Figura 4. Proceso de renovación. Fuente: elaboración propia.*

**▸ Estado de reenlace:**

- Si la renovación falla y se alcanza el 87.5% del tiempo de concesión, el cliente entra en el estado de reenlace.

- El cliente inicia el ciclo básico de nuevo, pero con la IP actual en lugar de 0.0.0.0.

![Figura 5. Proceso de reenlace. Fuente: elaboración propia.](images/image-7.png)

*Figura 5. Proceso de reenlace. Fuente: elaboración propia.*

Mensajes del protocolo DHCP **▸ DHCPDISCOVER:** enviado por el cliente para encontrar servidores DHCP. **▸ DHCPOFFER:** enviado por los servidores en respuesta a DHCPDISCOVER, ofreciendo una configuración. **▸ DHCPREQUEST:** enviado por el cliente para aceptar una oferta y solicitar la asignación de la configuración. **▸ DHCPDECLINE:** enviado por el cliente si la IP ofrecida ya está en uso, rechazando la oferta.

**▸ DHCPACK:** enviado por el servidor para confirmar la asignación de la configuración solicitada.

**▸ DHCPNACK:** enviado por el servidor si la solicitud del cliente no puede ser cumplida, indicando que el cliente debe reiniciar el proceso.

**▸ DHCPRELEASE:** enviado por el cliente para liberar su configuración de red.

**▸ DHCPINFORM:** enviado por el cliente para solicitar parámetros de configuración sin la asignación de una dirección IP.

Estos mensajes y estados permiten una gestión eficiente y automatizada de las configuraciones de red en un entorno dinámico, adaptándose a las necesidades de renovación y reconexión conforme se desarrollan las condiciones de red.

# 2.8. Ventajas y desventajas

A continuación, se presentan unas tablas con las ventajas y desventajas del uso de servidores DHCP en la gestión de redes:

![Tabla 1. Ventajas. Fuente: elaboración propia.](images/image-8.png)

![Tabla 2. Desventajas. Fuente: elaboración propia.](images/image-9.png)

# protocolo-dhcp/

# Qué es el DHCP, funcionamiento y ejemplos de

# configuración

de Luz, S. (2024, octubre 9). Qué es el DHCP, funcionamiento y ejemplos de configuración. *Redes Zone.* <https://www.redeszone.net/tutoriales/internet/que-es-> En este artículo te explican perfectamente que es el DHCP y para qué sirve este protocolo. Además, te aportan diferentes ejemplos de uso y como se realiza una configuración de un servidor DHCP.

# Configurar servidor DHCP en Windows Server 2022

Clockwork Computer. (2022, octubre 30). *Configurar ฀ servidor DHCP en Windows* *Server 2022* [Vídeo]. YouTube. [https://www.youtube.com/watch?v=ItmHj-j5spI](https://www.youtube.com/watch?v=ItmHj-j5spI)

¿Quieres ver cómo se configura un servidor DHCP en WS 2022? Aquí te presento un vídeo donde se explica paso a paso como preparar el servidor para que asigne direcciones IP de forma automática.

![image-10](images/image-10.png)

Accede al vídeo: [https://www.youtube.com/embed/ItmHj-j5spI](https://www.youtube.com/embed/ItmHj-j5spI)

# server/networking/troubleshoot-dhcp-guidance

# Guía de solución de problemas de DHCP

Liang, H., Xu, S., y Li, A. (2024, agosto 9). Guía de solución de problemas de DHCP. *Microsoft Learn.* <https://learn.microsoft.com/es-es/troubleshoot/windows->

Si te presenta algún problema asociado con el servicio DHCP, puedes consultar este artículo donde te muestra los errores encontrados más comunes y como solucionarlos, además de disponer de un agente virtual que te facilitará la resolución de problemas.

# servidor-dhcp/

# Cómo habilitar y configurar un servidor DHCP

Parada, M. (2019, octubre 1). Cómo habilitar y configurar un Servidor DHCP. *OpenWebinars.* <https://openwebinars.net/blog/como-habilitar-y-configurar-un->

Si quieres aprender a instalar un servidor DHCP en Linux puedes consultar este artículo donde además te indicará cuales son los errores más habituales que te puedes encontrar en la instalación y su solución.

# [https://aprendolinux.com/que-es-dhcp-y-como-instalar/](https://aprendolinux.com/que-es-dhcp-y-como-instalar/)

# Qué es DHCP y cómo instalar un servidor en Ubuntu

Qué es DHCP y cómo instalar un servidor en Ubuntu. (2024). *Aprendo Linux.* Ahora toca aprender a instalar un servidor DHCP en un entorno Ubuntu. Es muy parecido al aporte anterior, pero con pequeñas diferencias personalizadas a este sistema operativo.

# Cómo gestionar tus ámbitos de DHCP

Oller Aznar, J. I. (s. f.). Cómo gestionar tus ámbitos de DHCP. *Jotelulu.* [https://jotelulu.com/soporte/tutoriales/como-gestionar-tus-ambitos-de-dhcp/](https://jotelulu.com/soporte/tutoriales/como-gestionar-tus-ambitos-de-dhcp/)

¿Te han quedado dudas sobre la diferencia entre ámbito y rango? ¿Quieres aprender a gestionarlos en un entorno Windows? En este artículo vas a aprender a revisar, crear, configurar y modificar tus ámbitos de DHCP.

# dhcp-y-como-funciona/

# El DHCP y la configuración de redes

El DHCP (Dynamic Host Configuration Protocol). (2024, septiembre 25). *IONOS.* *Digital Guide.* <https://www.ionos.es/digitalguide/servidores/configuracion/que-es-el-> El sitio web de IONOS te muestra una explicación muy completa de cómo funciona el servicio DHCP y cómo activar y desactivar esta funcionalidad en los diferentes clientes.

.

# Entrenamiento 1. Preguntas relacionadas con el

# servicio DHCP

#### ▸ Planteamiento del ejercicio

Deberás responder a las siguientes preguntas relacionadas con el servicio DHCP: **▸** Explica las ventajas e inconvenientes que proporciona utilizar un servicio DHCP.

Debes utilizar una tabla para representarlo. **▸** Enumera los tipos de asignaciones que existen y explica cada uno de ellos. **▸** ¿En qué consisten los ámbitos? Explica para qué se pueden utilizar. **▸** Explica las ventajas proporcionadas por DHCP Failover Protocol. **▸** ¿Qué son las reservas? ¿Para qué se utilizan? **▸** ¿Qué tiempos de concesión son más adecuados dependiendo de las características de la red? **▸** Enumera las situaciones en las que se produce una solicitud de la renovación de la configuración de la red por parte del equipo cliente. **▸** Explica qué es un agente de retransmisión y qué tipos existen. **▸** ¿Qué ocurre si equipos cliente con Windows intentan solicitar una configuración de red y el servidor no está disponible? **▸** ¿Qué ocurre cuando un equipo se cambia de subred? ¿Cómo se libera la dirección IP que tenía concedida?

#### ▸ Desarrollo paso a paso

Haz una búsqueda exhaustiva y completa el documento con una correcta bibliografía.

#### ▸ Solución

#### Explica las ventajas e inconvenientes que proporciona utilizar un servicio

![image-11](images/image-11.png)

**DHCP. Debes utilizar una tabla para representarlo.**

**Enumera los tipos de asignaciones que existen y explica cada uno de ellos.**

**▸** Asignación automática: el servidor DHCP asigna una dirección IP permanente a un cliente desde un rango específico de direcciones IP configuradas.

**▸** Asignación dinámica: el servidor DHCP asigna una dirección IP a un cliente por un tiempo limitado o hasta que el cliente ya no necesite la dirección. Esta es la forma más común de asignación.

**▸** Asignación manual (o estática): el administrador de la red asigna manualmente una dirección IP específica a un dispositivo específico. Esto se puede configurar en el servidor DHCP para que ciertos dispositivos siempre reciban la misma IP.

**¿En qué consisten los ámbitos? Explica para qué se pueden utilizar.**

Los ámbitos en DHCP son un rango definido de direcciones IP que el servidor DHCP puede asignar a los clientes de la red. Cada ámbito está asociado con una subred específica y contiene una serie de configuraciones como la máscara de subred, puerta de enlace predeterminada y otros parámetros. Se utilizan para:

**▸** Administrar direcciones IP de manera organizada.

**▸** Separar y gestionar diferentes segmentos de red.

**▸** Aplicar configuraciones específicas a diferentes subredes.

**Explica las ventajas proporcionadas por DHCP Failover Protocol.**

**▸** Alta disponibilidad: permite que dos servidores DHCP operen en conjunto para

proporcionar direcciones IP y otros parámetros de configuración, garantizando la continuidad del servicio si uno de los servidores falla. **▸** Balanceo de carga: distribuye las solicitudes de DHCP entre dos servidores, lo que reduce la carga en un único servidor y mejora la eficiencia. **▸** Resiliencia: mejora la resiliencia de la red al permitir que los clientes sigan recibiendo configuraciones IP, incluso, durante fallos del servidor. **▸** Recuperación rápida: facilita la recuperación de fallos al sincronizar los datos de los dos servidores.

#### ¿Qué son las reservas? ¿Para qué se utilizan?

Las reservas en DHCP son configuraciones que permiten a un servidor DHCP asignar siempre la misma dirección IP a un dispositivo específico, basado en la dirección MAC del dispositivo. Se utilizan para:

**▸** Dispositivos que requieren una dirección IP fija, como servidores, impresoras y otros dispositivos de red críticos.

**▸** Garantizar que ciertos dispositivos siempre reciban la misma configuración de red.

**▸** Facilitar la administración y el seguimiento de dispositivos importantes en la red.

#### ¿Qué tiempos de concesión son más adecuados dependiendo de las

#### características de la red?

**▸** Redes con alta movilidad (como redes wifi públicas): tiempos de concesión cortos (de unas pocas horas a un día) para asegurar que las direcciones IP no se queden bloqueadas en dispositivos que ya no están en la red.

**▸** Redes estables con pocos cambios (como redes corporativas): tiempos de concesión largos (de varios días a semanas) para reducir el tráfico DHCP y la carga administrativa.

**▸** Entornos mixtos: tiempos de concesión intermedios (de uno a varios días) para equilibrar la disponibilidad de direcciones IP y la estabilidad de la red.

**Enumera las situaciones en las que se produce una solicitud de la renovación** **de la configuración de la red por parte del equipo cliente.**

**▸** Renovación del tiempo de concesión: cuando el 50 % del tiempo de concesión ha pasado, el cliente intenta renovar la dirección IP para extender su validez.

**▸** Reinicio del equipo cliente: al reiniciar, el cliente puede solicitar renovar la dirección IP si la concesión anterior sigue siendo válida.

**▸** Cambio de red o de subred: si el cliente se mueve a una nueva subred, solicitará una nueva configuración.

**▸** Expiración de la concesión: si la concesión expira, el cliente solicitará una nueva dirección IP.

**Explica qué es un agente de retransmisión y qué tipos existen.**

Un agente de retransmisión DHCP (DHCP Relay Agent) es un dispositivo de red que reenvía las solicitudes DHCP entre clientes y servidores en diferentes subredes. Tipos de agentes de retransmisión incluyen:

**▸** Agentes de retransmisión basados en rúteres: integrados en rúteres para facilitar la comunicación entre clientes y servidores DHCP a través de diferentes subredes.

**▸** Agentes de retransmisión dedicados: dispositivos o *softwares* dedicados a la función de retransmisión DHCP.

#### ¿Qué ocurre si equipos cliente con Windows intentan solicitar una

#### configuración de red y el servidor no está disponible?

Si un cliente Windows no puede contactar con un servidor DHCP, intentará utilizar la última configuración válida obtenida anteriormente. Si no tiene una configuración previa válida, el cliente utilizará una dirección IP autoconfigurada (APIPA) en el rango 169.254.x.x. Esto permite una conectividad básica en la misma subred, pero no acceso a recursos fuera de la subred local.

**¿Qué ocurre cuando un equipo se cambia de subred? ¿Cómo se libera la**

#### dirección IP que tenía concedida?

Cuando un equipo se cambia a una nueva subred:

**▸** Liberación de la IP anterior: el equipo envía un mensaje DHCPRELEASE al servidor DHCP para liberar la dirección IP anterior.

**▸** Solicitud de nueva IP: el equipo realiza una nueva solicitud DHCPDISCOVER para obtener una dirección IP adecuada para la nueva subred.

**▸** Configuración de la nueva IP: el servidor DHCP en la nueva subred asigna una nueva dirección IP y otros parámetros de red al equipo.

# Entrenamiento 2. Instalación y configuración de

# servicio DHCP en Windows

#### ▸ Planteamiento del ejercicio

- Realizar la instalación y configuración de un servidor DHCP en un servidor con Windows Server 2019 y un cliente con Windows 10, documentando los pasos y proporcionando imágenes de la configuración TCP/IP y el resultado de ping satisfactorio entre las dos máquinas.

- Como nombre de red, usar cualquiera propio de una LAN, pero como último bloque pon las dos últimas cifras de tu DNI y como anteúltimo número tu edad.

- Para ello puedes valerte de máquinas virtuales en un entorno virtual como VirtualBox.

#### ▸ Desarrollo paso a paso

Instalación y configuración del servidor DHCP:

**▸** Realizar la instalación de Windows Server 2019.

**▸** Configurar el servidor DHCP en Windows Server 2019.

**▸** Configurar la tarjeta de red del servidor con una IP estática.

Instalación y configuración del cliente:

**▸** Realizar la instalación de Windows 10.

**▸** Configurar la tarjeta de red del cliente para obtener una IP automáticamente desde el servidor DHCP.

**▸**

**▸** Conectar el cliente al servidor DHCP.

Configuración de la red:

**▸** Utilizar un nombre de red propio de una LAN.

**▸** Como último bloque del nombre de red, usar las dos últimas cifras de tu DNI.

**▸** Como anteúltimo número del nombre de red, usar tu edad.

#### ▸ Solución

#### Instalación y configuración del servidor DHCP

**▸** Preparación del servidor:

- En el VirtualBox, después de instalar la ISO del Windows Server 2019, configura el adaptador de red como adaptador puente.

- Iniciar sesión en Windows Server 2019 con una cuenta de administrador.

- Abrir el administrador del Servidor.

- Agregar el rol de servidor DHCP usando el asistente de agregar roles y características.

- Completar la configuración posterior a la instalación del DHCP.

**▸** Configuración de la tarjeta de red del servidor:

- Asignar una IP estática a la tarjeta de red del servidor, la máscara de subred y la puerta de enlace predeterminada, por ejemplo, IP 192.168.25.56, máscara de subred 255.255.255.0 y puerta de enlace 192.168.25.1.

#### Instalación y configuración del cliente

**▸** Preparación del cliente:

- En el VirtualBox, después de instalar la ISO del Windows 10, configura el adaptador de red como adaptador puente.

**▸** Configuración de la tarjeta de red del cliente:

- Configurar la tarjeta de red de Windows 10 para obtener una dirección IP automáticamente.

**▸** Verificar la asignación de una IP desde el servidor DHCP:

- En el cliente Windows 10, abre un símbolo del sistema y ejecuta ipconfig para verificar que ha recibido una IP del servidor DHCP.

**▸** Probar la conectividad:

- En el servidor, abre un símbolo del sistema y ejecuta ping [IP del cliente].

- En el cliente, abre un símbolo del sistema y ejecuta ping [IP del servidor].

Asegúrate de ajustar las direcciones IP según el último bloque de tu DNI y tu edad. Siguiendo estos pasos, habrás configurado correctamente un servidor DHCP en Windows Server 2019 y un cliente en Windows 10, permitiendo la asignación dinámica de direcciones IP en tu red.

# Entrenamiento 3. Instalación y configuración de

# servicio DHCP en Ubuntu

#### ▸ Planteamiento del ejercicio

- Realizar la instalación y configuración de un servidor DHCP en un servidor con Ubuntu 20.04 y un cliente con Ubuntu 20.04, documentando los pasos y proporcionando imágenes de la configuración TCP/IP y el resultado de ping satisfactorio entre las dos máquinas.

- Como nombre de red, usar cualquiera propio de una LAN pero como último bloque pon las dos últimas cifras de tu DNI y como anteúltimo número, tu edad.

- Para ello puedes valerte de máquinas virtuales en un entorno virtual como virtualbox.

#### ▸ Desarrollo paso a paso

**▸** Instalación y configuración del servidor DHCP:

- Realizar la instalación de Ubuntu 20.04.

- Configurar el servidor DHCP en Ubuntu 20.04.

- Configurar la tarjeta de red del servidor con una IP estática.

**▸** Instalación y configuración del cliente:

- Realizar la instalación de Ubuntu 20.04.

- Configurar la tarjeta de red del cliente para obtener una IP automáticamente desde el servidor DHCP.

- Conectar el cliente al servidor DHCP.

**▸** Configuración de la red:

- Utilizar un nombre de red propio de una LAN.

- Como último bloque del nombre de red, usar las dos últimas cifras de tu DNI.

- Como anteúltimo número del nombre de red, usar tu edad.

#### ▸ Solución

#### Instalación y configuración del servidor DHCP

Preparación del servidor: **▸** En el VirtualBox, después de instalar la ISO del Ubuntu 20.04, debemos configurar el adaptador de red como Red NAT, para poder instalar los paquetes del DHCP. **▸** Actualizar el sistema e instalar el paquete de DHCP.

![image-12](images/image-12.png)

**▸** Configurar el archivo de configuración del servidor dhcp.conf . Edita el archivo

/etc/dhcp/dhcpd.conf :

![image-13](images/image-13.png)

**▸** Añade o modifica las siguientes líneas (ajustando según tu DNI y edad):

![Explicación de cada componente:](images/image-14.png)

**▸** subnet 192.168.[edad].0 netmask 255.255.255.0 {

- subnet 192.168.[edad].0: define el rango de direcciones IP que el servidor DHCP manejará. La red 192.168.[edad].0 representa la red local a la que pertenecen las direcciones IP.

- netmask 255.255.255.0 : especifica la máscara de subred para la red. Esta máscara de subred permite hasta 254 direcciones IP válidas en esta red.

**▸** range 192.168.[edad].10 192.168.[edad].100;

- Define el rango de direcciones IP que el servidor DHCP puede asignar a los clientes. En este caso, el servidor puede asignar direcciones desde 192.168.[edad].10 hasta 192.168.[edad].100 .

**▸** option routers 192.168.[edad].1;`

- Especifica la dirección IP del rúter (puerta de enlace) para la red. Los clientes recibirán esta IP como su puerta de enlace predeterminada. En este ejemplo, la IP del router es 192.168.[edad].1 .

**▸** option subnet-mask 255.255.255.0;

- Indica la máscara de subred que se debe utilizar en los clientes. Aquí se especifica la misma máscara de subred 255.255.255.0 que se definió en la red.

**▸** option domain-name-servers 8.8.8.8, 8.8.4.4;

- Proporciona las direcciones IP de los servidores DNS que los clientes deben usar para resolver nombres de dominio. En este caso, se están utilizando los servidores DNS públicos de Google ( 8.8.8.8 y 8.8.4.4 ).

**▸** option domain-name "mi-red-[DNI]";

- Define el nombre de dominio que los clientes deben usar. Puedes usar cualquier nombre de dominio para tu red local, por ejemplo, `"mi-red-[DNI]"`, donde `[DNI]` es un identificador único como las dos últimas cifras de tu DNI.

Configurar la interfaz de red para el servidor DHCP:

**▸** Edita el archivo /etc/default/isc-dhcp-server :

![image-15](images/image-15.png)

**▸** Añade o modifica la siguiente línea para especificar la interfaz de red:

![image-16](images/image-16.png)

**▸** Reiniciar el servicio para aplicar los cambios:

![image-17](images/image-17.png)

**▸** Habilitarlo para que se inicie automáticamente:

![image-18](images/image-18.png)

Configuración de la tarjeta de red del servidor:

**▸** Asignar una IP estática a la tarjeta de red del servidor, la máscara de subred y la

puerta de enlace predeterminada. **▸** Edita el archivo de configuración de la red:

![▸ Configura la IP estática: ▸ Aplica la configuración de red: Instalación y configuración del cliente ▸ Configuración de la red del cliente](images/image-19.png)

- En el VirtualBox, debemos configurar el adaptador de red como adaptador puente, para que se pueda comunicar con el cliente.

**▸** Configurar la tarjeta de red del cliente para obtener una IP automáticamente desde el servidor DHCP.

- Edita el archivo de configuración de la red:

![image-20](images/image-20.png)

**▸** Configura la interfaz para DHCP:

**▸** Aplica la configuración de red:

![image-21](images/image-21.png)

#### Verificación de la configuración

**▸** Verificación en el cliente:

- Obtener la dirección IP asignada por el servidor DHCP:

![image-22](images/image-22.png)

**▸** Verificar la conectividad mediante ping hacia el servidor:

![image-23](images/image-23.png)

**▸** Verificación en el servidor:

- Verificar que el servidor DHCP está asignando direcciones:

![image-24](images/image-24.png)

Este comando te permitirá observar en tiempo real cómo el servidor DHCP responde a las solicitudes de los clientes y asigna direcciones IP. Podemos obtener algo similar a lo siguiente:

![Descripción de la salida:](images/image-25.png)

**▸** DHCPDISCOVER: indica que un cliente DHCP está buscando un servidor DHCP para obtener una dirección IP. **▸** DHCPOFFER: el servidor DHCP ofrece una dirección IP al cliente. **▸** DHCPREQUEST: el cliente DHCP solicita la dirección IP ofrecida por el servidor. **▸** DHCPACK: el servidor DHCP confirma que el cliente puede usar la dirección IP asignada. ¿Cómo interpretar estos registros? **▸** Dirección MAC: cada registro incluye la dirección MAC del cliente (por ejemplo, 08:00:27:89:5b:c5). **▸** Dirección IP asignada: se muestra la dirección IP asignada al cliente (por ejemplo, 192.168.30.10). **▸** Interfaz de red: se indica la interfaz de red a través de la cual se está realizando la asignación (por ejemplo, eth0).

# Entrenamiento 4. Configuración particular de un

# servidor DHCP con Windows

#### ▸ Planteamiento del ejercicio

Se quiere utilizar el servidor Windows Server 2019 como servidor DHCP para que sea capaz de entregar configuraciones de red al resto de equipos de dicha red. La configuración del servidor tiene que cumplir las siguientes especificaciones:

**▸** El servidor DHCP debe tener una dirección IP fija, la 192.168.120.101 con máscara de red personalizada.

**▸** El servidor DHCP debe ser capaz de repartir exactamente un total de 200 direcciones IP.

**▸** El tiempo de concesión será de dos horas y cincuenta minutos.

**▸** En la red hay configurado un *gateway* con una dirección IP fija, la 192.168.120.55.

Los clientes de la red deberán usar este dispositivo para salir hacia Internet. Por lo tanto, el servidor DHCP deberá asignarles este parámetro.

**▸** El servicio DNS es proporcionado por dos servidores DNS internos en la red con las siguientes direcciones IP: 192.168.120.22 y 192.168.120.29. El servidor DHCP también deberá asignarles este parámetro.

Después de la configuración anterior será necesario comprobar el correcto funcionamiento del servidor. Configurar el cliente Windows 10 para que pueda obtener la configuración de red mediante el servidor DHCP y comprobar si obtiene los parámetros de red.

#### ▸ Desarrollo paso a paso

- Configuración de la dirección IP fija en el servidor DHCP.

- Instalación del rol de servidor DHCP.

- Configuración del servidor DHCP.

- Activación del ámbito.

- Configuración del cliente Windows 10

- Comprobación del funcionamiento del servidor DHCP.

#### ▸ Solución

#### Configuración de la dirección IP fija en el servidor DHCP

**▸** Inicia la máquina virtual con Windows Server 2019 en VirtualBox. **▸** Abre «Administrador del servidor» desde el menú de inicio. **▸** Ve a «Administrador de equipos» y selecciona «Configuración de red». **▸** Configura la dirección IP estática:

- Dirección IP: 192.168.120.101

- Máscara de subred: configura la máscara personalizada (por ejemplo, 255.255.255.0).

- Puerta de enlace predeterminada: 192.168.120.55

#### Instalación del rol de servidor DHCP

**▸** En el administrador del servidor, selecciona «Agregar roles y características». **▸** Sigue el asistente hasta llegar a la selección de roles y selecciona «Servidor DHCP». **▸** Completa el asistente y permite que el servidor se reinicie si es necesario.

#### Configuración del servidor DHCP

**▸** Abre la consola «Administrador DHCP». **▸** Crea un nuevo ámbito. **▸** Haz clic derecho en «IPv4» y selecciona «Nuevo ámbito». **▸** Sigue el asistente y configura las siguientes opciones:

- Nombre del ámbito: por ejemplo, «Red Local». Rango de direcciones IP: IP inicial: 192.168.120.150. IP final: 192.168.120.349 (esto proporciona exactamente 200 direcciones). Máscara de subred: 255.255.255.0 o la máscara personalizada que estés utilizando.

- Puerta de enlace (gateway): 192.168.120.55

- Servidores DNS: DNS primario: 192.168.120.22. DNS secundario: 192.168.120.29.

**▸** Configura el tiempo de concesión:

- En el mismo asistente o después de crear el ámbito, haz clic derecho en el ámbito y selecciona «Propiedades».

- Ve a la pestaña «General» y ajusta el tiempo de concesión a dos horas y cincuenta minutos (170 minutos).

#### Activación del ámbito

Haz clic derecho en el nuevo ámbito y selecciona «Activar».

#### Configuración del Cliente Windows 10

**▸** Inicia la máquina virtual con Windows 10 en VirtualBox.

**▸** Configura la red del cliente Windows 10 para usar DHCP:

- Abre «Configuración de red e Internet» desde el menú de inicio.

- Ve a «Ethernet» y selecciona «Cambiar opciones de adaptador».

- Haz clic derecho en tu conexión de red y selecciona «Propiedades».

- Selecciona «Protocolo de Internet versión 4 (TCP/IPv4)» y haz clic en «Propiedades».

- Asegúrate de que las opciones «Obtener una dirección IP automáticamente» y «Obtener la dirección del servidor DNS automáticamente» están seleccionadas.

- Comprobar la configuración de red.

- Abre una ventana de «Símbolo del sistema».

- Ejecuta el comando ipconfig /all y verifica que: la dirección IP está en el rango 192.168.120.150 - 192.168.120.349. La puerta de enlace predeterminada es 192.168.120.55. Los servidores DNS son 192.168.120.22 y 192.168.120.29.

Comprobación del funcionamiento del servidor DHCP:

**▸** Ping a la puerta de enlace:

- En la ventana de «Símbolo del sistema» del cliente Windows 10, ejecuta: ping 192.168.120.55

**▸** Verificación de acceso a Internet:

- Abre un navegador web en el cliente Windows 10 y verifica que puedes acceder a páginas web.

Siguiendo estos pasos, habrás configurado correctamente un servidor DHCP en Windows Server 2019 y comprobado su funcionamiento mediante un cliente Windows 10 en un entorno de VirtualBox.

# Entrenamiento 5. Configuración particular de un

# servidor DHCP con Ubuntu trabajando con un cliente Ubuntu

#### ▸ Planteamiento del ejercicio

Configurar un servidor Ubuntu como servidor DHCP para que pueda proporcionar configuraciones de red a los dispositivos de la red conforme a las siguientes especificaciones:

**▸** El servidor DHCP debe tener una dirección IP fija, la 192.168.60.121 con máscara de red personalizada.

**▸** El servidor DHCP debe ser capaz de repartir exactamente un total de 210 direcciones IP.

**▸** El tiempo de concesión será de trece horas.

**▸** En la red hay configurado un *gateway* con una dirección IP fija, la 192.168.60.62.

Los clientes de la red deberán usar este dispositivo para salir hacia Internet. Por lo tanto, el servidor DHCP deberá asignarles este parámetro.

**▸** El servicio DNS es proporcionado por dos servidores DNS internos en la red con las siguientes direcciones IP: 192.168.60.13 y 192.168.60.33. El servidor DHCP también deberá asignarles este parámetro.

#### ▸ Desarrollo paso a paso

#### Instalación del servidor DHCP

**▸** Instalar el paquete DHCP en el servidor Ubuntu.

#### Configuración de la IP fija del servidor

**▸** Configurar la dirección IP fija 192.168.60.121 en el servidor Ubuntu.

#### Configuración del servidor DHCP

**▸** Editar el archivo de configuración del DHCP para cumplir con las especificaciones mencionadas.

- Configurar el rango de direcciones IP que repartir.

- Configurar el tiempo de concesión.

- Configurar la puerta de enlace predeterminada.

- Configurar los servidores DNS.

#### Ajustes de la interfaz del servidor DHCP

**▸** Asegurarse de que el servidor DHCP esté escuchando en la interfaz de red correcta.

#### Inicio y comprobación del servicio DHCP

**▸** Reiniciar el servicio DHCP.

**▸** Verificar el estado del servicio DHCP para asegurarse de que está funcionando correctamente.

#### Configuración del cliente Ubuntu

**▸** Configurar el cliente Ubuntu para obtener su configuración de red a través del servidor DHCP.

**▸** Verificar que el cliente recibe los parámetros de red correctos del servidor DHCP.

#### Comprobación

**▸** Comprobar el correcto funcionamiento del servidor DHCP y verificar que los clientes reciben la configuración de red esperada, incluyendo la dirección IP, la puerta de enlace y los servidores DNS.

#### ▸ Solución

#### Instalación del servidor DHCP

**▸** Inicia tu máquina virtual de Ubuntu que actuará como servidor DHCP. **▸** Abre una terminal e instala el paquete DHCP:

![image-26](images/image-26.png)

#### Configuración de la IP fija del servidor

**▸** Edita el archivo de configuración de netplan. Primero, encuentra el archivo correcto, usualmente es /etc/netplan/01-netcfg.yaml o algo similar:

![image-27](images/image-27.png)

**▸** Configura la IP fija 192.168.60.121.

Configuración del servidor DHCP

**▸** Edita el archivo de configuración del DHCP:

**▸** Aplica los cambios:

![image-28](images/image-28.png)

#### Configuración del servidor DHCP

- ▸ Edita el archivo de configuración del DHCP:

![image-29](images/image-29.png)

- ▸ Agrega la configuración específica que se indica en el enunciado:

![Ajustes de la interfaz del servidor DHCP](images/image-30.png)

- ▸ Asegúrate de que el servidor DHCP esté escuchando en la interfaz de red correcta.

    - Edita el archivo /etc/default/isc-dhcp-server :

![image-31](images/image-31.png)

- ▸ Ajusta la interfaz (por ejemplo, enp0s3 ):

![image-32](images/image-32.png)

#### Inicio y comprobación del servicio DHCP

- ▸ Reinicia el servicio DHCP:

![image-33](images/image-33.png)

    - Servicios en Red e Internet 61

    - Tema 2. Entrenamientos

**▸** Comprueba el estado del servicio:

![image-34](images/image-34.png)

#### Configuración del cliente Ubuntu

**▸** Inicia tu máquina virtual de Ubuntu que actuará como cliente.

**▸** Abre una terminal y edita el archivo de configuración de netplan en el cliente, por

![▸ Modifícalo para usar DHCP: ▸ Aplica los cambios: Verificación](images/image-35.png)

ejemplo, /etc/netplan/01-netcfg.yaml :

**▸** Verifica que el cliente haya recibido los parámetros de red correctos del servidor DHCP:

![image-36](images/image-36.png)

**▸** Deberías ver que la interfaz enp0s3 tiene una IP en el rango 192.168.60.10- 192.168.60.219.

**▸** Verifica la configuración de la ruta y el DNS:

![image-37](images/image-37.png)

**▸** Asegúrate de que la puerta de enlace y los servidores DNS estén configurados correctamente.

**▸** El comando ip route muestra la tabla de enrutamiento de IP del sistema, la cual incluye información sobre las rutas de red configuradas. Una salida típica podría verse así:

![image-38](images/image-38.png)

**▸** Donde:

- default via 192.168.60.62 dev enp0s3 proto dhcp metric 100 : indica que la ruta predeterminada *(gateway)* para salir a Internet es 192.168.60.62, y que está configurada a través de DHCP en la interfaz enp0s3.

- 192.168.60.0/24 dev enp0s3 proto kernel scope link src 192.168.60.x metric 100 : indica que la red 192.168.60.0/24 está directamente conectada a la interfaz enp0s3 y que la IP asignada a esta interfaz es 192.168.60.x (donde x es un número dentro del rango asignado por el servidor DHCP, por ejemplo, 10 a 219).

Si el comando ip route muestra que la ruta predeterminada *(gateway)* es 192.168.60.62 y que la IP asignada está en el rango 192.168.60.10 a 192.168.60.219, significa que el cliente ha recibido correctamente la configuración del servidor DHCP.

El comando cat /etc/resolv.conf muestra el archivo de configuración del resolutor de DNS, que contiene las direcciones de los servidores DNS que el cliente utiliza para resolver nombres de dominio. Una salida típica podría verse así:

**▸** Donde:

- nameserver 192.168.60.13 : indica que uno de los servidores DNS configurados es 192.168.60.13.

- nameserver 192.168.60.33 : indica que otro servidor DNS configurado es 192.168.60.33.

Si el archivo /etc/resolv.conf contiene las direcciones de los servidores DNS 192.168.60.13 y 192.168.60.33, significa que el cliente también ha recibido correctamente la configuración DNS del servidor DHCP.

#### Nota adicional

Asegúrate de que ambas máquinas virtuales (servidor y cliente) estén en la misma red interna de VirtualBox para que puedan comunicarse entre sí. Puedes configurar esto en la configuración de red de cada máquina virtual en VirtualBox, seleccionando la misma red interna (por ejemplo, «intnet») para ambas.

Con estos pasos, deberías tener un servidor DHCP funcionando en Ubuntu y un cliente que recibe su configuración de red automáticamente.

![image-39](images/image-39.png)

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–29)*
- A fondo  *(pp.30–36)*
- Entrenamientos  *(pp.37–64)*
- Servicios en Red e Internet 6 Tema 2. Material de estudio · Servicios en Red e Internet 7 Tema 2. Material de estudio · Servicios en Red e Internet 8 Tema 2. Material de estudio · Servicios en Red e Internet 9 Tema 2. Material de estudio · Servicios en Red e Internet 11 Tema 2. Material de estudio · Servicios en Red e Internet 12 Tema 2. Material de estudio · Servicios en Red e Internet 13 Tema 2. Material de estudio · Servicios en Red e Internet 14 Tema 2. Material de estudio · Servicios en Red e Internet 15 Tema 2. Material de estudio · Servicios en Red e Internet 16 Tema 2. Material de estudio · Servicios en Red e Internet 17 Tema 2. Material de estudio · Servicios en Red e Internet 18 Tema 2. Material de estudio · Servicios en Red e Internet 19 Tema 2. Material de estudio · Servicios en Red e Internet 20 Tema 2. Material de estudio · Servicios en Red e Internet 21 Tema 2. Material de estudio · Servicios en Red e Internet 22 Tema 2. Material de estudio · Servicios en Red e Internet 23 Tema 2. Material de estudio · Servicios en Red e Internet 24 Tema 2. Material de estudio · Servicios en Red e Internet 25 Tema 2. Material de estudio · Servicios en Red e Internet 26 Tema 2. Material de estudio · Servicios en Red e Internet 27 Tema 2. Material de estudio · Servicios en Red e Internet 28 Tema 2. Material de estudio · Servicios en Red e Internet 29 Tema 2. Material de estudio  *(pp.6, 7, 8, 9, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29)*
- Servicios en Red e Internet 30 Tema 2. A fondo · Servicios en Red e Internet 31 Tema 2. A fondo · Servicios en Red e Internet 32 Tema 2. A fondo · Servicios en Red e Internet 33 Tema 2. A fondo · Servicios en Red e Internet 34 Tema 2. A fondo · Servicios en Red e Internet 35 Tema 2. A fondo · Servicios en Red e Internet 36 Tema 2. A fondo  *(pp.30–36)*
- Servicios en Red e Internet 37 Tema 2. Entrenamientos · Servicios en Red e Internet 38 Tema 2. Entrenamientos · Servicios en Red e Internet 39 Tema 2. Entrenamientos · Servicios en Red e Internet 40 Tema 2. Entrenamientos · Servicios en Red e Internet 41 Tema 2. Entrenamientos · Servicios en Red e Internet 42 Tema 2. Entrenamientos · Servicios en Red e Internet 43 Tema 2. Entrenamientos · Servicios en Red e Internet 44 Tema 2. Entrenamientos · Servicios en Red e Internet 45 Tema 2. Entrenamientos · Servicios en Red e Internet 46 Tema 2. Entrenamientos · Servicios en Red e Internet 47 Tema 2. Entrenamientos · Servicios en Red e Internet 48 Tema 2. Entrenamientos · Servicios en Red e Internet 49 Tema 2. Entrenamientos · Servicios en Red e Internet 50 Tema 2. Entrenamientos · Servicios en Red e Internet 51 Tema 2. Entrenamientos · Servicios en Red e Internet 52 Tema 2. Entrenamientos · Servicios en Red e Internet 53 Tema 2. Entrenamientos · Servicios en Red e Internet 54 Tema 2. Entrenamientos · Servicios en Red e Internet 55 Tema 2. Entrenamientos · Servicios en Red e Internet 56 Tema 2. Entrenamientos · Servicios en Red e Internet 57 Tema 2. Entrenamientos · Servicios en Red e Internet 58 Tema 2. Entrenamientos · Servicios en Red e Internet 59 Tema 2. Entrenamientos · Servicios en Red e Internet 60 Tema 2. Entrenamientos · Servicios en Red e Internet 62 Tema 2. Entrenamientos · Servicios en Red e Internet 63 Tema 2. Entrenamientos · Servicios en Red e Internet 64 Tema 2. Entrenamientos  *(pp.37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 62, 63, 64)*