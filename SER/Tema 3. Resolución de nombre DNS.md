## Tema 3

## Servicios en Red e Internet

# Tema 3. Resolución de

# nombre DNS

# Índice

Esquema Material de estudio

## 3.1. Introducción y objetivos

## 3.2. Características

## 3.3. Espacio de nombres de dominio

## 3.4. Cliente y servidor DNS

## 3.5. Tipos de servidores DNS

## 3.6. Archivos de zona

## 3.7. Registro de recursos

## 3.8. Replicación de zona

## 3.9. Servidores DNS dinámicos

## 3.10. Referencias bibliográficas

A fondo

Pobreza y migraciones

Tutorial del servicio DNS

ICANN

Mejores DNS privados y seguros de 2024

Cómo cambiar los DNS desde tu rúter y por qué deberías

hacerlo Compra y registra tu dominio ideal Registra tus dominios y protege tu marca Transferencia de zonas DNS Servidor DNS - Curso de Windows Server 2016

DNS como un servidor modular

DNS: los reenviadores puestos a prueba

DNS: zonas de búsqueda directa

Entrenamientos

Entrenamiento 1. Resolver DNS en Ubuntu

Entrenamiento 2. Resolver DNS en Windows

Entrenamiento 3. Instalación y configuración de servicios

DNS en Ubuntu

Entrenamiento 4. Instalación y configuración de servicio

DNS en Windows

Entrenamiento 5. Configuración servidor DNS caché en

Windows

# Esquema

![image-2](images/image-2.png)

Servicios en Red e Internet 4 Tema 3. Esquema

## 3.1. Introducción y objetivos

En el contexto de la administración de redes y la configuración de interfaces de red, uno de los aspectos fundamentales es la **asignación y gestión de direcciones IP.** Cada dispositivo en una red requiere una **dirección IP única** para poder comunicarse con otros dispositivos dentro de esa red y en redes externas.

La dirección IP sirve como un **identificador esencial** para la interfaz de red del dispositivo, permitiendo que la comunicación se dirija de manera precisa. Aunque la dirección IP es crucial, no es el único parámetro necesario; la máscara de red también juega un papel importante al determinar **el alcance** de la red y **cómo se** **segmenta.**

En el caso del protocolo **IP versión** 4 (IPv4), que es el más utilizado en la actualidad, las direcciones IP se componen de 32 bits, divididos en cuatro octetos de 8 bits cada uno. Estos 32 bits se representan, habitualmente, en formato decimal y se dividen en cuatro grupos de números separados por puntos, como en la dirección 192.168.1.1. Cada uno de estos octetos puede variar entre 0 y 255, lo que permite una gran cantidad de combinaciones posibles.

Para un administrador de red o cualquier usuario que necesite gestionar dispositivos en una red, **conocer la dirección IP exacta** de cada interfaz es crucial. Esto puede ser necesario para tareas como acceder a una interfaz web para configurar un dispositivo, realizar una conexión remota mediante SSH o para cualquier otra forma de gestión que requiera especificar una dirección IP. Recordar unas pocas direcciones IP no representa un gran desafío, ya que se asemeja a recordar números de teléfono, aunque son 32 bits en lugar de siete dígitos. Sin embargo, cuando se trata de manejar un número elevado de direcciones IP, la tarea puede volverse considerablemente más complicada.

La dificultad de recordar un gran número de direcciones IP se ve agravada si estas direcciones cambian con frecuencia. En redes donde se utiliza la asignación dinámica de direcciones IP, como es el caso de los **servidores DHCP** (Dynamic Host Configuration Protocol), las direcciones pueden variar con el tiempo. Esto significa que, incluso, si un usuario logra memorizar una dirección IP en un momento dado, esa dirección podría cambiar más adelante, requiriendo un nuevo esfuerzo para recordar la nueva dirección.

Afortunadamente, existe una estrategia eficaz para mitigar este problema: el uso del **servicio de resolución de nombres o DNS** (Domain Name System). El DNS actúa como un sistema de traducción que convierte nombres de dominio legibles por humanos en direcciones IP numéricas y viceversa. En lugar de recordar cadenas largas de números, los usuarios pueden utilizar nombres de dominio más fáciles de recordar, como www.ejemplo.com.

El proceso de resolución de nombres comienza cuando un usuario ingresa un nombre de dominio en un navegador web o en cualquier otro cliente de red. El cliente realiza una **solicitud DNS al servidor** DNS configurado en su red. Este servidor DNS, que funciona como un intermediario, busca la dirección IP asociada al nombre de dominio solicitado. Si el servidor DNS tiene la dirección IP en su caché, responde de inmediato. Si no, realiza una búsqueda recursiva a través de otros servidores DNS, desde los servidores raíz hasta los servidores autoritativos del dominio en cuestión, para obtener la dirección IP correcta.

Una vez que se ha resuelto el nombre de dominio y se ha obtenido la dirección IP correspondiente, esta **información se almacena** en la caché del servidor DNS para futuras consultas, lo que agiliza el proceso y reduce el tiempo de respuesta en solicitudes posteriores.

El uso del DNS no solo facilita la tarea de recordar direcciones IP, sino que también proporciona una capa adicional de flexibilidad y gestión.

Los nombres de dominio pueden ser más fácilmente actualizados o cambiados en los registros DNS, sin necesidad de ajustar manualmente las direcciones IP en los sistemas de los usuarios. Esto es especialmente útil en entornos donde las direcciones IP pueden cambiar con frecuencia debido a configuraciones dinámicas o cambios en la infraestructura de red.

En conclusión, el DNS representa una solución eficiente y práctica para el problema de memorizar direcciones IP. Permite a los usuarios y administradores de red trabajar con nombres de dominio más fáciles de recordar, mientras que el sistema DNS se encarga de traducir estos nombres en direcciones IP numéricas cuando es necesario. Esto simplifica la gestión de redes y mejora la accesibilidad a los recursos en Internet, facilitando la administración y el uso diario de las redes de comunicaciones.

Los **objetivos** que se pretende alcanzar en este tema son:

**▸** Entender el propósito del servicio de resolución de nombres.

**▸** Distinguir entre sistemas de nombres planos y jerárquicos.

**▸** Explicar el funcionamiento del archivo hosts.

**▸** Describir la estructura del sistema DNS.

**▸** Definir los tipos de servidores DNS y sus funciones.

**▸** Comprender el proceso de resolución de nombres en DNS.

**▸** Analizar la importancia del protocolo DNS en la red.

**▸** Explorar el espacio de nombres de dominio.

**▸** Identificar los componentes del protocolo DNS.

**▸** Distinguir entre resolución directa e inversa.

**▸** Examinar el rol de los servidores DNS raíz y TLD.

**▸** Evaluar la gestión y configuración de servidores DNS.

**▸** Comprender la función de los registros de recursos en DNS.

**▸** Explicar el proceso de replicación de zona en DNS.

**▸** Implementar servidores DNS dinámicos para actualización automática.

**▸** Integrar servidores DNS con servidores DHCP para actualización de registros

dinámicos.

## 3.2. Características

¿Qué es este servicio?

El servicio de resolución de nombres es una función que permite utilizar **nombres** **alfanuméricos** en lugar de direcciones IP para identificar dispositivos en una red. Esto significa que, en vez de tener que recordar y utilizar direcciones IP para interactuar con dispositivos como servidores web, impresoras o equipos de red, los usuarios pueden usar nombres más fáciles de recordar. Aunque las direcciones IP siguen siendo fundamentales, el servicio de resolución de nombres facilita la asociación entre nombres y direcciones IP.

Existen dos **enfoques principales** para realizar esta asociación:

**▸ Sistema de nombres planos:** utiliza una lista estática en la que cada nombre está directamente vinculado a una dirección IP. Este método es simple, pero menos flexible. Aunque sea un método obsoleto, actualmente este sistema se sigue utilizando, pero solo a nivel local, es decir, cada equipo tiene un archivo propio con información sobre los nombres de dispositivos y que únicamente lo consulta el propio equipo. El nombre de este archivo es *hosts* y su ubicación en el equipo dependiendo del sistema operativos, la versión o la distribución instalada. La estructura de este archivo es similar a la que se muestra en la Tabla 1.

![image-3](images/image-3.png)

Tabla 1. Ejemplo de fichero hosts. Fuente: elaboración propia.

![image-4](images/image-4.png)

Tabla 2. Características del sistema nombres planos. Fuente: elaboración propia.

![image-5](images/image-5.png)

Tabla 3. Ventajas/desventajas del sistema nombres planos. Fuente: elaboración propia.

**▸ Sistema de nombres jerárquicos:** utiliza un sistema más complejo, como el DNS (sistema de nombres de dominio), que organiza los nombres en una estructura jerárquica para resolver las consultas de manera más eficiente.

![image-6](images/image-6.png)

Tabla 4. Características del sistema nombres jerárquicos. Fuente: elaboración propia.

Ejemplo práctico

DNS (Domain Name System): el DNS es el sistema de nombres jerárquico más comúnmente utilizado. En un diagrama DNS, el dominio raíz (.) se encuentra en la cima del árbol, seguido por dominios de nivel superior (.com, .org, .net), y luego dominios de segundo nivel (ejemplo.com), con subdominios adicionales si es necesario (sub.example.com).

![image-7](images/image-7.png)

Tabla 5. Ventajas y desventajas del sistema nombres jerárquicos. Fuente: elaboración propia.

El servicio de resolución de nombres se encarga de **traducir nombres en** **direcciones IP** (resolución directa) y viceversa (resolución inversa). Por ejemplo, cuando se accede a una página web o se configura una red, se traduce un nombre de dominio a una dirección IP. Aunque este servicio no es estrictamente necesario (es posible usar solo direcciones IP), simplifica la identificación de dispositivos en una red, ya que es mucho más fácil recordar nombres que secuencias de números.

Aplicaciones del servicio de resolución de nombres

Se utiliza en diversas situaciones donde se necesita convertir nombres en direcciones IP, tales como:

**▸ Acceso a sitios web** (usando URL en navegadores). Cuando los usuarios ingresan una URL en un navegador, como www.ejemplo.com, el servicio de resolución de nombres convierte este nombre de dominio en una dirección IP, como 192.0.2.1.

Esta dirección IP permite al navegador localizar y conectarse al servidor web correspondiente, permitiendo la visualización del sitio web solicitado. Sin este servicio, los usuarios tendrían que recordar y utilizar direcciones IP numéricas, lo

Servicios en Red e Internet 12 Tema 3. Material de estudio que sería mucho más complejo y propenso a errores.

**▸ Control remoto** (como Telnet y SSH). En entornos donde se requiere acceso remoto a sistemas o servidores, herramientas como Telnet, SSH o RDP (Remote Desktop Protocol) utilizan nombres de host para establecer conexiones. El servicio de resolución de nombres traduce el nombre del *host,* por ejemplo servidor.ejemplo.com, en una dirección IP. Esto permite a los usuarios conectarse a máquinas y redes a distancia sin necesidad de conocer las direcciones IP exactas, facilitando así la administración y el acceso a sistemas remotos.

**▸ Configuración de sistemas operativos** (añadiendo impresoras y otros dispositivos de red). Durante la configuración de redes y sistemas operativos, los nombres de dispositivos, impresoras y otros recursos de red se utilizan para simplificar la administración y el uso diario. Por ejemplo, al agregar una impresora a una red, en lugar de ingresar la dirección IP de la impresora, se puede usar un nombre como «impresora_oficina». El servicio de resolución de nombres traduce este nombre en una dirección IP que el sistema operativo puede utilizar para enviar trabajos de impresión a la impresora correcta. Esto no solo simplifica la configuración, sino que también facilita el mantenimiento y la gestión de los dispositivos en la red.

![Figura 1. Servidor DNS. Fuente: Servidor DNS, s. f.](images/image-8.png)

*Figura 1. Servidor DNS. Fuente: Servidor DNS, s. f.*

Historia y funcionalidad

En la actualidad, el servicio de resolución de nombres se basa principalmente en el protocolo de **capa de aplicación DNS** (Domain Name System), que comúnmente se conoce simplemente como servicio DNS.

Este protocolo fue creado en 1983 por el ISI (Information Science Institute) gracias al trabajo de los investigadores Paul Mockapetris y Jon Postel. En la actualidad, está especificado en los RFC 1034 y 1035.

Al igual que el protocolo DHCP, el protocolo DNS opera en la capa de aplicación del **modelo OSI** (Open System Interconnection), que es la capa más alta de esta arquitectura. Es un protocolo de **tipo cliente/servidor,** lo que significa que los clientes (dispositivos en una red que hacen consultas DNS) envían peticiones a un servidor (denominado servidor DNS), el cual responde a estas solicitudes. Las consultas DNS buscan resolver direcciones IP a partir de nombres o viceversa.

Además, el protocolo DNS utiliza tanto **UDP** (User Datagram Protocol) como **TCP** (Transmission Control Protocol) para la capa de transporte, según el modelo OSI, y tanto el cliente como el servidor operan a través del **puerto 53.** Es importante gestionar cuidadosamente este puerto en los cortafuegos tanto del servidor como de los clientes.

El protocolo DNS gestiona la resolución de nombres mediante una **base de datos** **distribuida.** Esto significa que la información sobre la resolución de nombres no está almacenada en un solo servidor, sino que está repartida entre una red de servidores. Esta distribución tiene varias justificaciones:

**▸ Capacidad de almacenamiento:** un único servidor no puede almacenar toda la información del DNS debido a la gran cantidad de datos involucrados.

**▸ Carga de trabajo:** un solo servidor no podría manejar todas las solicitudes debido al elevado número de clientes que utilizan el servicio. De existir solo un servidor, este podría colapsar o experimentar tiempos de respuesta muy altos.

**▸ Redundancia:** muchos servidores tienen copias de los datos de otros servidores para garantizar la continuidad del servicio en caso de fallos en los servidores originales, ya sea por balanceo de carga, fallos del servidor, ataques, etc.

Finalmente, el protocolo DNS organiza la resolución de nombres en una estructura jerárquica en forma de árbol, conocida como el **espacio de nombres de dominio.**

## 3.3. Espacio de nombres de dominio

El espacio de nombres de dominio se representa como un diagrama en forma de **árbol** que **organiza jerárquicamente** el sistema de resolución de nombres actual.

**▸ Nodo raíz:** el nodo superior en este árbol lleva la etiqueta especial de un punto (.).

**▸ Nodos terminales:** los nodos finales, como www, ftp, smr, etc., representan dispositivos específicos, también conocidos como nombres de dispositivo *(hostname).*

Este sistema jerárquico permite que dos nodos compartan la misma etiqueta, siempre que estén bajo nodos diferentes (por ejemplo, múltiples dispositivos pueden usar el mismo nombre [www], una flexibilidad que no era posible con el sistema de nombres plano).

Dominios

En el contexto del sistema jerárquico de resolución de nombres, el concepto de dominio se refiere a los **subárboles** dentro del espacio de nombres de dominio. Cada dominio puede contener varios **subdominios,** formando una estructura de árbol dentro de otro árbol.

**▸ Dominio raíz:** este dominio abarca todo el espacio de nombres de dominio.

**▸ Dominios de nivel superior o Top Level Domain (TLD):** directamente debajo del dominio raíz se encuentran los dominios de nivel superior, como .com, .org, etc.

Estos son muy conocidos en Internet.

**▸ Dominios de segundo nivel:** los TLD se subdividen en dominios de segundo nivel, que suelen ser usados por empresas y organizaciones.

**▸ Dominios de tercer nivel, cuarto nivel, etc.:** los dominios pueden seguir subdividiéndose en niveles adicionales. Dado el tamaño del espacio de nombres de dominio, hay una gran cantidad de dominios que se organizan jerárquicamente en hasta **127 niveles.**

![Figura 2. Estructura de árbol. Fuente: Gómez, 2017](images/image-9.png)

*Figura 2. Estructura de árbol. Fuente: Gómez, 2017*

Nombres de dominio

Cada dominio tiene un nombre de dominio que se forma a partir de las etiquetas de los nodos en el espacio de nombres de dominio, desde el nodo superior hasta el nodo raíz (identificado con un punto [.]), separados por puntos.

**▸ Sintaxis:** nodo_superior….nodo3nivel.nodo2nivel.TLD.

**▸ Ejemplo:** el dominio unir.net. Mostrado en la imagen de la sección anterior. Los nombres de dominio deben ser **registrados** (en la mayoría de los casos con un coste) por entidades registradoras por ICANN (1and1, Arsys, nominalia, etc.).

FQDN (Fully Qualified Domain Name)

El término FQDN (Fully Qualified Domain Name) se refiere a un tipo especial de nombre de dominio que designa dispositivos específicos dentro del espacio de nombres de dominio.

**▸ Características:** cada dispositivo tiene un FQDN único, garantizando que no haya dos dispositivos con el mismo FQDN.

**▸ Sintaxis:** hostname.nombre_de_dominio_al_que_pertenece.

**▸ Ejemplo:** <www.unir.net>.

## 3.4. Cliente y servidor DNS

Cliente DNS

Un cliente DNS se refiere al dispositivo o la aplicación encargada de solicitar la conversión de nombres de dominio a direcciones IP a un servidor DNS. En otras palabras, es el **componente que hace la petición** para que un nombre de dominio se traduzca en una dirección IP.

Hoy en día, todos los sistemas operativos vienen con un cliente DNS integrado. Esto significa que no es necesario instalar *software* adicional para realizar estas consultas. Comúnmente, este cliente se conoce como **DNS Resolver.** Así, cuando un dispositivo necesita buscar la dirección IP asociada a un nombre de dominio, utiliza su cliente DNS o DNS resolver.

E l **proceso de resolución** comienza localmente, utilizando los recursos del propio dispositivo. Esto puede implicar consultar el archivo hosts, que contiene una lista de nombres y direcciones en un formato simple o acceder a la caché DNS si esta está habilitada (no todos los sistemas operativos disponen de caché DNS). La caché DNS almacena temporalmente las respuestas a consultas recientes para acelerar futuras resoluciones. La prioridad entre consultar el archivo hosts o la caché DNS se puede configurar según las necesidades. Si el nombre no se puede resolver localmente, el cliente DNS se conecta a un servidor DNS externo para obtener la información.

![Figura 3. Consulta DNS desde el cliente. Fuente: Gómez, 2017.](images/image-10.png)

*Figura 3. Consulta DNS desde el cliente. Fuente: Gómez, 2017.*

Servidor DNS

Los servidores DNS son los dispositivos dedicados a procesar las solicitudes de resolución de nombres hechas por los clientes DNS.

Desde el punto de vista del *software,* un servidor DNS se define como la aplicación que debe instalarse en un dispositivo para permitir la resolución de consultas de nombres por parte de los clientes DNS. Esta aplicación debe ser capaz de manejar tanto **resoluciones directas** (que consisten en convertir un nombre de dominio en una dirección IP) como **resoluciones inversas** (que consisten en convertir una dirección IP en un nombre de dominio).

Existen varias aplicaciones para configurar

un dispositivo como servidor DNS,

dependiendo del sistema operativo en uso. Para sistemas operativos de Microsoft, como Windows Server 2008 o Windows

Server 2012, se ofrece una **función**

**integrada** llamada **rol o función** (dependiendo de la versión del sistema) que permite configurar el dispositivo como servidor DNS de manera directa.

En el caso de servidores basados en distribuciones Linux, como Ubuntu Server o CentOS, se pueden emplear aplicaciones

como Dnsmasq o Bind9, que están

disponibles para su descarga desde los repositorios del sistema.

## 3.5. Tipos de servidores DNS

Los servidores DNS se dividen en varios tipos según su función y el rol que desempeñan en el proceso de resolución de nombres. Aquí se presenta una descripción de los principales tipos de servidores DNS:

Servidor DNS principal (master)

El servidor DNS principal, también conocido como servidor maestro, es el que **almacena** la **base de datos de zona** para un **dominio específico.** Este servidor tiene la autoridad sobre la zona y contiene los registros de DNS necesarios para resolver los nombres de dominio dentro de esa zona. Los servidores secundarios obtienen la información de este servidor principal.

Servidor DNS secundario (slave)

Un servidor DNS secundario, o esclavo, **recibe y almacena una copia** de la base de datos de zona del servidor principal. Su función principal es proporcionar **redundancia y equilibrio de carga.** Si el servidor principal falla, el secundario puede seguir respondiendo a las consultas con la información replicada.

![Figura 4. Cómo funciona un DNS Secundario. Fuente: Romanos, 2024.](images/image-11.png)

*Figura 4. Cómo funciona un DNS Secundario. Fuente: Romanos, 2024.*

Servidor DNS autoritativo

Un servidor DNS autoritativo es el que

proporciona **respuestas definitivas y**

**autorizadas** sobre los registros de DNS para una zona. Este tipo de servidor puede ser tanto principal como secundario. La

característica distintiva de un servidor

autoritativo es que tiene la **información original sobre el dominio** y no necesita consultar otros servidores para responder a las solicitudes.

Servidor DNS no autoritativo

A diferencia del servidor autoritativo, un servidor DNS no autoritativo no tiene la información original sobre el dominio. En lugar de ello, actúa como **intermediario** y **reenvía consultas** a otros servidores DNS para obtener la respuesta. Los servidores de caché y los resolutores suelen funcionar de esta manera.

Servidor DNS de reenvío (forwarding)

Un servidor DNS de reenvío es configurado para enviar todas las consultas a otro servidor DNS. En lugar de resolver las solicitudes directamente, el servidor de reenvío **delega la consulta** a un servidor DNS de mayor nivel, que puede ser un servidor de dominio o un servidor público.

Servidor DNS de caché

Un servidor DNS de caché **almacena las respuestas a consultas recientes** para acelerar la resolución de nombres en

futuras solicitudes. Cuando recibe una

consulta, primero verifica si la respuesta ya está en su caché. Si la información está almacenada, la devuelve rápidamente sin necesidad de hacer una consulta externa.

Servidor DNS recursivo

Un servidor DNS recursivo es responsable de realizar el proceso completo de resolución de nombres en nombre del cliente. Cuando recibe una solicitud, el servidor recursivo consulta otros servidores DNS hasta que obtiene una respuesta definitiva. Es decir, realiza una **búsqueda exhaustiva** para encontrar la información solicitada.

Servidor DNS Root (raíz)

Los servidores DNS raíz son los primeros en la jerarquía del sistema de nombres de dominio. Existen solo trece servidores raíz, designados por letras (A a M), que conocen la dirección de los servidores DNS de nivel superior (TLD). Son cruciales para la infraestructura de DNS porque dirigen las consultas a los servidores de dominio de nivel superior.

Servidor DNS de dominio de nivel superior (TLD)

Estos servidores **gestionan los dominios** de **nivel superior,** como .com, .org, o .net. Los servidores TLD proporcionan la dirección de los servidores autoritativos para los dominios específicos dentro de su zona de dominio. Son responsables de dirigir las consultas a los servidores DNS que conocen los detalles de los dominios específicos.

Servidor DNS de zona de búsqueda inversa

Estos servidores **gestionan la resolución inversa,** que implica obtener un nombre de dominio a partir de una dirección IP. La base de datos de zona de búsqueda inversa contiene registros que permiten realizar esta conversión.

Cada tipo de servidor DNS desempeña un papel esencial en la infraestructura global de nombres de dominio, contribuyendo a la eficiencia y la resiliencia del sistema de nombres de dominio (DNS).

![Figura 5. Cómo resuelve un Servidor DNS una solicitud. Fuente: ¿Qué es un servidor DNS?, 2022.](images/image-12.png)

*Figura 5. Cómo resuelve un Servidor DNS una solicitud. Fuente: ¿Qué es un servidor DNS?, 2022.*

## 3.6. Archivos de zona

La información esencial para ejecutar el servicio DNS (resolución de nombres) está distribuida en múltiples servidores DNS. Esto implica que los archivos que contienen dicha información no se encuentran en un único servidor, sino que están dispersos a través de **varios servidores DNS.** Estos archivos son conocidos como archivos de zona.

Cada archivo de zona abarca, únicamente, una **parte específica** del espacio de nombres de dominio, denominada **zona.** De aquí surge el término archivos de zona.

![Figura 6. Estructura de árbol. Fuente: Gómez, 2017.](images/image-13.png)

*Figura 6. Estructura de árbol. Fuente: Gómez, 2017.*

En la imagen anterior se muestra una parte del espacio de nombres de dominio. La zona superior es la zona raíz o zona (.), mientras que otra zona es la mi-sl.es. Las zonas se identifican también con el nombre del dominio más grande que abarcan.

Los servidores que contienen toda la información de la zona (.) son conocidos como **servidores raíz** o *root servers.* Estos solicitudes DNS para los dominios de

servidores se encargan de gestionar las nivel superior. Hay trece servidores raíz

distribuidos en diversos lugares del mundo, principalmente en Estados Unidos, bajo el dominio **root-servers.org.**

El sistema del servidor raíz incluye 919 instancias operadas por doce operadores independientes. Todos los servidores raíz utilizan **BIND** (Berkeley Internet Name Domain) como servidor DNS, excepto los servidores H, L y K, que utilizan NSD (Name Server Daemon). Los servidores raíz distribuidos emplean **Anycast** para mejorar y equilibrar la carga, proporcionando un servicio descentralizado.

En la siguiente imagen se puede ver

la distribución global de los diferentes

![Figura 7. Distribución de los Servidores Raíz. Fuente: Root-servers.org. servidores raíz (A – M).](images/image-14.png)

*Figura 7. Distribución de los Servidores Raíz. Fuente: Root-servers.org.*

Cuando se realiza una consulta de cualquier dominio, el servidor raíz ofrece, al menos, el nombre y la dirección del servidor autorizado de la zona de nivel superior del dominio buscado. Así, el servidor del dominio proporcionará una lista de los servidores autorizados para la zona de segundo nivel, hasta obtener una respuesta adecuada.

Tipos de zonas

Sabemos que las principales funciones del servicio DNS son realizar resoluciones directas (convertir nombres en direcciones IP) e inversas (convertir direcciones IP en nombres). Para estas acciones, cada servidor DNS utiliza diferentes archivos de zona. Para resoluciones directas se usan archivos de zona directa y para resoluciones inversas se utilizan archivos de zona inversa.

Los archivos de zona directa se utilizan para convertir nombres en direcciones IP. Se identifican con nombres de dominio como (.), com., marca.es. o elpais.es.

Por ejemplo:

- La zona (.) puede convertir nombres como xxxx.xxxx.xxxx.

- La zona com. puede convertir nombres como xxxx.xxxx.xxxx.com.

- La zona elpais.es. puede convertir nombres como xxxx.xxxx.xxxx.elpais.es.

El nombre de los archivos de zona directa coincide con la terminación de los nombres que pueden convertir.

Los archivos de zona inversa se utilizan para convertir direcciones IP en nombres. Se identifican con nombres de dominio como 192.in-addr.arpa., 21.172.in-addr.arpa. o 45.65.192.in-addr.arpa. para direcciones IPv4.

Por ejemplo:

- Los archivos de zona 192.in-addr.arpa. pueden convertir direcciones IP

como 192.X.X.X.

- Los archivos de zona 21.172.in-addr.arpa. convierten direcciones IP

como 172.21.X.X.

- Los 45.65.192.in-addr.arpa. convierten direcciones IP como 192.65.45.X.

Los números en el nombre de la zona son los primeros octetos de las direcciones IP que pueden resolver, escritos en orden inverso al original.

## 3.7. Registro de recursos

En los servidores DNS, toda la información necesaria para el servicio de resolución de nombres se guarda en archivos de texto plano en forma de registros de recursos (RR). Estos registros varían según su función y pueden ser de los siguientes tipos:

**▸** A y AAAA.

**▸** SOA.

**▸** NS.

**▸** CNAME.

**▸** MX.

**▸** PTR.

**▸** DHCPRELEASE.

**▸** Otros como SRV, TXT, etc. Los archivos de zona ya sean directos o indirectos, contienen una mezcla de estos tipos de registros. Sin embargo, en servidores DNS de caché, los registros de recursos pueden aparecer de forma individual sin formar parte de un archivo de zona.

Registro SOA

El registro SOA (Start Of Authority) es crucial, ya que especifica el servidor DNS primario de una zona y proporciona información para la sincronización con los servidores secundarios para facilitar la transferencia de zona.

Sintaxis del registro SOA:

<nombre de zona> TTL IN SOA <FQDN del servidor primario> <mail del administrador de zona>

(serial; refresh; retry; expire; minimum TTL)

Donde: **▸** <nombre de la zona> : nombre de la zona o el carácter @ como valor equivalente. **▸** TTL : tiempo de vida en segundos del registro en la caché. **▸** IN : clase de registro, siempre IN para Internet. **▸** SOA : tipo de registro. **▸** <FQDN del servidor primario> : nombre de dominio completo del servidor primario. **▸** <email del administrador de zona> : correo del administrador de la zona.

**▸** (serial; refresh; retry; expire; minimum TTL) : valores de sincronización.

- serial : número de versión de la zona.

- refresh : tiempo que un servidor secundario espera antes de verificar si necesita una actualización.

- retry : intervalo para reintentar la actualización en caso de fallo.

- expire : tiempo máximo que un servidor secundario puede estar sin actualizar antes de dejar de funcionar.

- minimum TTL : valor mínimo del TTL para los registros de la zona.

Ejemplo de registro SOA

unir.net. 86400 IN SOA ns1.unir.net. admin.unir.net. (

7200 ; refresh (2 hours)

3600 ; retry (1 hour)

1209600 ; expire (2 weeks)

86400 ) ; minimum TTL (1 day)

Donde:

unir.net. : nombre de la zona.

86400 : tiempo de vida (TTL) del registro en segundos (1 día).

IN : clase del registro, siempre IN para Internet.

SOA : tipo de registro, indicando que es un registro SOA.

ns1.unir.net. : FQDN del servidor DNS primario para la zona unir.net. admin.unir.net. : *email* del administrador de la zona, representado con un punto en lugar del símbolo @.

(2024080401 7200 3600 1209600 86400):

2024080401 : número de serie del registro SOA, que debe incrementarse con cada cambio en la zona. 7200 : intervalo en segundos para que un servidor secundario espere antes de comprobar si necesita actualizar la zona (2 horas). 3600 : intervalo en segundos para que un servidor secundario reintente la actualización en caso de fallo (1 hora).

1209600 : tiempo en segundos que un servidor secundario puede esperar antes de considerar la zona como expirada (2 semanas).

86400 : valor mínimo del TTL en segundos para todos los registros de la zona (1 día).

Registro NS

El registro NS indica los servidores DNS que tienen autoridad sobre una zona. Cada zona debe tener al menos un registro para el servidor primario y puede tener varios para los servidores secundarios. Sintaxis del registro NS:

```
<nombre de zona> TTL IN NS <FQDN del servidor>
```

Donde:

**▸** <nombre de la zona> : nombre de la zona o @.

**▸** TTL : tiempo de vida en segundos del registro en la caché.

**▸** IN : clase de registro, siempre IN para Internet.

**▸** NS : tipo de registro.

**▸** <FQDN del servidor> : nombre de dominio completo del servidor.

Ejemplos de registro NS

unir.net. 86400 IN NS ns1.unir.net. unir.net. 86400 IN NS ns2.unir.net.

Donde: unir.net. : nombre de la zona.

86400 : tiempo de vida (TTL) del registro en segundos (1 día).

IN : clase del registro, siempre IN para Internet.

NS : tipo de registro, indicando que es un registro NS.

ns1.unir.net : FQDN del servidor DNS primario para la zona unir.net. ns2.unir.net : FQDN del servidor DNS secundario para la zona unir.net.

Registro A

Los registros A son esenciales para las **resoluciones directas,** asociando nombres de dominio (FQDN) con **direcciones IPv4.**

Sintaxis del registro A:

```
<FQDN> TTL IN A <Dirección IPv4>
```

Donde: **▸** <FQDN> : nombre de dominio completo o parcial. **▸** TTL : tiempo de vida en segundos del registro en la caché. **▸** IN : clase de registro, siempre IN para Internet.

**▸** A : tipo de registro. **▸** <Dirección IPv4> : dirección IP asociada.

Ejemplo de registro A

www.unir.net. 86400 IN A 192.0.2.1

Donde: www.unir.net. : FQDN que está asociado a una dirección IPv4. 86400 : tiempo de vida (TTL) del registro en segundos (un día). IN : clase del registro, siempre IN para Internet. A : tipo de registro, indicando que es un registro A. 192.0.2.1 : dirección IPv4 asociada al FQDN «www.unir.net».

Registro CNAME

Los registros CNAME permiten asignar **múltiples nombres** a un mismo dispositivo, creando alias para un FQDN original.

Sintaxis del registro CNAME:

```
<alias> TTL IN CNAME <FQDN original>
```

Donde: **▸** <alias> : alias a asociar con el FQDN del dispositivo. **▸** TTL : tiempo de vida en segundos del registro en la caché.

**▸** IN : clase de registro, siempre IN para Internet. **▸** CNAME : tipo de registro. **▸** <FQDN original> : nombre de dominio completo del dispositivo.

Ejemplos de registro CNAME

www 86400 IN CNAME servidor1.unir.net. ftp 86400 IN CNAME servidor1.unir.net.

Donde: www : alias que se va a asociar al FQDN servidor1.unir.net. ftp : alias que se va a asociar al FQDN servidor1. unir.net. 86400 : tiempo de vida (TTL) del registro en segundos (un día). IN : clase del registro, siempre IN para Internet. CNAME : tipo de registro, indicando que es un registro CNAME. servidor1.unir.net. : FQDN original al que se le asigna los alias «www.unir.net» y «ftp.unir.net».

Registro MX

Los registros MX son críticos para el servicio de correo electrónico, indicando los servidores de correo para un dominio.

Sintaxis del registro MX:

<dominio> TTL IN MX prioridad <FQDN servidor mail>

Donde:

**▸** <dominio> : nombre del dominio.

**▸** TTL : tiempo de vida en segundos del registro en la caché.

**▸** IN : clase de registro, siempre IN para Internet.

**▸** MX : tipo de registro.

**▸** prioridad : prioridad del servidor de correo.

**▸** <FQDN servidor mail> : nombre de dominio completo del servidor de correo.

Ejemplo de registro MX

unir.net. 86400 IN MX 10 mail.unir.net. unir.net. 86400 IN MX 20 backupmail.unir.net.

Donde: unir.net .: nombre del dominio.

86400: tiempo de vida (TTL) del registro en segundos (1 día).

IN : clase del registro, siempre IN para Internet.

MX : tipo de registro, indicando que es un registro MX.

10 : prioridad del servidor de correo. Un valor más bajo indica una mayor

prioridad. mail.unir.net .: FQDN del servidor de correo primario. 20 : Prioridad del servidor de correo secundario. Un valor más alto indica una menor prioridad. backupmail.unir.net .: FQDN del servidor de correo secundario.

Registro PTR

Los registros PTR se usan para resoluciones inversas, asociando direcciones IP con nombres de dominio (FQDN).

Sintaxis del registro PTR:

<Dirección IPv4 o IPv6> TTL IN PTR <FQDN>

Donde: **▸** <Dirección IPv4 o IPv6> : dirección IP asociada. **▸** TTL : tiempo de vida en segundos del registro en la caché. **▸** IN : clase de registro, siempre IN para Internet. **▸** PTR : tipo de registro. **▸** <FQDN> : nombre de dominio completo asociado a la IP.

Ejemplo de registro PTR

10.113.0.203.in-addr.arpa. 86400 IN PTR server.unir.net.

Donde: 10.113.0.203.in-addr.arpa .: dirección IPv4 escrita en orden inverso y seguida de in-addr.arpa para las resoluciones inversas. 86400 : tiempo de vida (TTL) del registro en segundos (un día). IN : clase del registro, siempre IN para Internet. PTR : tipo de registro, indicando que es un registro PTR. server.unir.net. : FQDN asociado a la dirección IP 203.0.113.10.

## 3.8. Replicación de zona

La replicación de zona permite que un servidor DNS secundario adquiera una **copia** **de solo lectura** de los archivos de zona del servidor DNS primario al que está vinculado. Esto asegura que los servidores DNS secundarios puedan actualizar sus archivos de zona cuando se realicen cambios en el servidor DNS primario.

¿Cómo se realiza este proceso? Aquí, el registro SOA (Start of Authority) y su información de sincronización *(serial, refresh,*

*retry, expire, minimum* TTL) son

cruciales. Los servidores DNS secundarios verifican regularmente, según el intervalo d e *refresh,* si necesitan actualizarse comparando su número de *serial* con el del servidor DNS primario. Si los números coinciden, no es necesario actualizar. Si difieren, el servidor secundario debe realizar una replicación de zona porque los datos del servidor primario han cambiado.

Si el servidor secundario detecta que necesita actualizarse, pero no puede hacerlo debido a problemas de red o del servidor primario, intentará de nuevo según el intervalo de *retry.* Si después del tiempo especificado por *expire* no se ha completado la replicación, el servidor secundario dejará proporcionar datos desactualizados o incorrectos.

de funcionar como tal para evitar

En algunos casos, se realizan replicaciones de zona parciales, conocidas como replicaciones incrementales. Este tipo de replicación transfiere solo los datos que han cambiado desde la última replicación completa, reduciendo así la cantidad de datos transferidos y el tiempo necesario para la actualización.

![Figura 8. Transferencia de zona. Fuente: DNS transferencia de zona, 2014.](images/image-15.png)

*Figura 8. Transferencia de zona. Fuente: DNS transferencia de zona, 2014.*

## 3.9. Servidores DNS dinámicos

En el contexto anterior, se trató sobre la configuración automática de los parámetros de red, donde se observó que las direcciones IP de los adaptadores de red podían cambiar debido a un sistema de asignación dinámica y limitada. También, se mencionó la posibilidad de que los administradores cambien manualmente la configuración de red de un adaptador.

Esto plantea un desafío en la gestión de servidores DNS, ya que cualquier cambio en las direcciones IP de los adaptadores de red debe reflejarse de manera inmediata en los servidores DNS para garantizar que las consultas sobre esos dispositivos sean respondidas correctamente.

Una solución tradicional es que el administrador del servidor DNS primario actualice manualmente los registros cada vez que se realice un cambio en la configuración de red. Sin embargo, este enfoque es laborioso y susceptible a errores humanos.

Para abordar este problema, se utilizan servidores DNS dinámicos (DDNS). Estos sistemas permiten la **actualización automática y en tiempo real** de los registros de recursos en el servidor DNS cuando se producen cambios en la configuración de red de los adaptadores.

Existen herramientas diseñadas específicamente para implementar servidores DNS dinámicos, como DynDNS y No-IP. Alternativamente, se puede configurar conjuntamente el servidor DNS y el servidor DHCP en sistemas operativos como Windows Server y servidores Linux (por ejemplo, isc-dhcp-server y bind9) para crear una solución de DNS dinámico.

## 3.10. Referencias bibliográficas

¿Qué es un servidor DNS? (2022, noviembre 3). *Ionos.*

<https://www.ionos.es/digitalguide/servidores/know-how/que-es-el-servidor-dns-ycomo-funciona/>

DNS transferencia de zona. (2014, septiembre 28). En *Manuais Informática-IES San* *C l e m e n t e*

*.* <https://manuais.iessanclemente.net/index.php?>

$$title=Archivo:DNS\_Transferencia\_de\_zona.png$$

Gómez, F. P. (2017, enero 18).

*Tutorial del servicio DNS. ¿Cómo funciona?*

[https://www.fpgenred.es/DNS/_cmo_funciona_.html](https://www.fpgenred.es/DNS/_cmo_funciona_.html)

Romanos, J. (2024, octubre 14). Mejores DNS privados y seguros de 2024. *Adsl* *Zone.* [https://www.adslzone.net/reportajes/internet/mejores-dns/](https://www.adslzone.net/reportajes/internet/mejores-dns/)

Servidor DNS. (s. f.). *Seobility Wiki.* [https://www.seobility.net/es/wiki/Servidor_DNS](https://www.seobility.net/es/wiki/Servidor_DNS)

# ¿Qué es un servidor DNS? (2022, noviembre 3). IONOS.

# como-funciona/

## Pobreza y migraciones

<https://www.ionos.es/digitalguide/servidores/know-how/que-es-el-servidor-dns-y->

¿Sabes qué tipos de servidores DNS existen? ¿y cuáles son los servidores DNS públicos más usados? Tardarás tan solo siete minutos en leer este artículo y te resolverá todas las dudas que tengas o, si no tienes dudas, te reafirmará en los contenidos que has aprendido.

# profesional. [https://www.fpgenred.es/DNS/index.html](https://www.fpgenred.es/DNS/index.html)

## Tutorial del servicio DNS

Gómez, F. P. (2017, enero 18). Tutorial del servicio DNS. *Blog Formación* Si visitas este sitio web podrás ver todo lo relacionado con el Servicio DNS, desde consultas DNS, transferencias de zona, instalación de servidor DNS hasta configuración de un servidor DNS maestro, esclavo, caché, autoritario o solo de reenvío.

# Página de ICANN. [https://www.icann.org/](https://www.icann.org/)

## ICANN

| ¿Conoces la | ICANN? | Esta corporación sin ánimo |  |  | de lucro |  |  | tiene como función |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| principal coordinar la |  | administración | de | los elementos técnicos |  |  | del | DNS para |
| garantizar la |  | resolución unívoca de | los | nombres | y evitar | que | se | repitan las |

direcciones. De este modo, los usuarios podrán encontrarlas.

## Mejores DNS privados y seguros de 2024

Romanos, J. (2024, octubre 14). Mejores DNS privados y seguros de 2024. *Adsl* *Zone.* [https://www.adslzone.net/reportajes/internet/mejores-dns/](https://www.adslzone.net/reportajes/internet/mejores-dns/)

¿Cuáles son los mejores DNS de 2024? ¿Por qué es importante elegir bien un servidor DNS? ¿Cómo podemos cambiar la configuración para que nuestros servidores DNS sean los que elegimos? ¿Por qué es importante limpiar la caché DNS en nuestros dispositivos? Todas esas preguntas y más son respondidas en este artículo.

## Cómo cambiar los DNS desde tu rúter y por qué

## deberías hacerlo

Rubio, R. G. (2024, septiembre 30). Cómo cambiar los DNS desde tu router. *Adsl* *Zone.* [https://www.adslzone.net/como-se-hace/internet/cambiar-dns-router/](https://www.adslzone.net/como-se-hace/internet/cambiar-dns-router/)

Si quieres mejorar la privacidad o seguridad de tu conexión deberías leer este artículo que te enseña a utilizar los servidores DNS más adecuados en este momento, realizando cambios en la configuración de tu rúter.

## Compra y registra tu dominio ideal

Compra y registra tu dominio ideal. (s. f.). *IONOS.* <https://www.ionos.es/dominios/dominios?>

$$ac=OM.WE.WE287K417298T7073a&itc=LBZUBIGD--$$

$$&utm\_source=google&utm\_medium=cpc&utm\_campaign=SBG-ES-DOM-CTLD-------$$

$$&utm\_term=1and1%20dominios&matchtype=p&utm\_content=1%261+Dominio&gad\_$$

$$source=1&gclid=CjwKCAjw\_Na1BhAlEiwAM$$

Si lo que quieres es comprar un dominio, puedes buscar su disponibilidad y su precio en el sitio web de Ionos. Incluso, podrás contratar subdominios del dominio elegido, para tener estructuras como <www.tudominio.com>, <mail.tudominio.com>, etc.

# Registra tus dominios y protege tu marca. (s. f.). Hostalia.

# <https://www.hostalia.com/dominios/?>

# gad_source=1&gclid=CjwKCAjw_Na1BhAlEiwAM-dm7L7Ims-

# X__5adEpAMxyRsEHU2w3xPDfTJAGjhPSqSY2jfAmdTeWnRxoC4cwQAvD_BwE

## Registra tus dominios y protege tu marca

¿Tienes una marca o dominio que quieres registrar para que nadie te lo quite? En este sitio web te dan la oportunidad de elegir tu dominio, incluso con la posibilidad de que sea de forma gratuita durante el primer año.

## Transferencia de zonas DNS

Julio Iglesias Pérez (NonFungibleHacker). (2014, junio 14). *Transferencia de zonas* *DNS* [Vídeo]. YouTube. [https://www.youtube.com/watch?v=1a1pOE3ah14](https://www.youtube.com/watch?v=1a1pOE3ah14)

¿Sabes cómo realizar una transferencia de zona DNS en Windows Server 2012? Este vídeo te llevará menos de diez minutos y podrás contemplar como realizar esta operación entre servidores Windows.

![image-16](images/image-16.png)

Accede al vídeo: [https://www.youtube.com/embed/1a1pOE3ah14](https://www.youtube.com/embed/1a1pOE3ah14)

# v=X6Ru8SOrKxE

## Servidor DNS - Curso de Windows Server 2016

Pablo Martínez (NonFungibleHacker). (2017, junio 15). *Introducción a los DNS -* *Curso de Windows Server 2016* [Vídeo]. YouTube. <https://www.youtube.com/watch?> Primer vídeo de una selección que nos enseña desde lo que es un servidor DNS, los reenviadores hasta lo que son las zonas de búsqueda directa e inversa, todo ello aplicado al entorno de Windows.

![image-17](images/image-17.png)

Accede al vídeo: [https://www.youtube.com/embed/X6Ru8SOrKxE](https://www.youtube.com/embed/X6Ru8SOrKxE)

# modular - Curso de Windows Server 2016 [Vídeo]. YouTube.

# [https://www.youtube.com/watch?v=cwU3MLRoJKI](https://www.youtube.com/watch?v=cwU3MLRoJKI)

## DNS como un servidor modular

Pablo Martínez (NonFungibleHacker). (2017, julio 28). *DNS como un servicio* Segundo vídeo de una selección que nos enseña desde lo que es un servidor DNS, los reenviadores hasta lo que son las zonas de búsqueda directa e inversa, todo ello aplicado al entorno de Windows.

![image-18](images/image-18.png)

Accede al vídeo: [https://www.youtube.com/embed/cwU3MLRoJKI](https://www.youtube.com/embed/cwU3MLRoJKI)

# puestos a prueba - Curso de Windows Server 2016 [Vídeo]. YouTube.

# [https://www.youtube.com/watch?v=vx8XB7rIF-E&t=131s](https://www.youtube.com/watch?v=vx8XB7rIF-E%2526t=131s)

## DNS: los reenviadores puestos a prueba

Pablo Martínez (NonFungibleHacker). (2017, agosto 14). *DNS - Los reenviadores* Tercer vídeo de una selección que nos enseña desde lo que es un servidor DNS, los reenviadores hasta lo que son las zonas de búsqueda directa e inversa, todo ello aplicado al entorno de Windows.

# v=M8KLbR2fIFE&t=36s

## DNS: zonas de búsqueda directa

Pablo Martínez (NonFungibleHacker). (2017, agosto 17). *DNS - Zonas de búsqueda* *directa IMPORTANTE* [Vídeo]. YouTube. <https://www.youtube.com/watch?> Último vídeo de una selección que nos enseña desde lo que es un servidor DNS, los reenviadores hasta lo que son las zonas de búsqueda directa e inversa, todo ello aplicado al entorno de Windows.

## Entrenamiento 1. Resolver DNS en Ubuntu

**▸ Planteamiento del ejercicio**

Utilizando un equipo Ubuntu se desea comprobar el funcionamiento del archivo host como opción para resolver nombres de dominio.

**▸** Averigua cuáles son las direcciones IP asociadas a los siguientes nombres de dominio: <www.unir.net>, el periódico que más te guste, una universidad, una tienda. Se pueden utilizar las herramientas nslookup, dig o ping para obtener estos datos.

**▸** Editar el archivo host para que sea capaz de resolver consultas a los nombres de dominio anteriores. Por ejemplo, en mi navegador pongo micentro.com y vaya a la página de la Unir, si pongo miperiodico.com vaya a la página del periódico.

**▸** Comprobar que este método de resolución de nombres funciona correctamente. Para la comprobación se sugiere realizar una configuración manual de la configuración de red del cliente y utilizar la herramienta ping. ¿Cómo has diseñado la comprobación?

Puedes trabajar con el entorno de VirtualBox, instalando una máquina Ubuntu 20.04.

**▸ Desarrollo paso a paso**

- Paso 1: obtener las direcciones IP de los dominios.

- Paso 2: editar el archivo hosts y modifícale para cumplir con lo solicitado.

- Paso 3: comprobar la configuración (verificar que el archivo hosts esté funcionado y utilizar el navegado para ver el resultado).

- Paso 4: configurar la prioridad de resolución de nombres (opcional).

**▸ Solución**

#### Paso 1. Obtener las direcciones IP de los dominios

**▸** Abre una terminal en tu Ubuntu.

**▸** Utiliza las herramientas nslookup, dig o ping para averiguar las direcciones IP asociadas a los dominios. A continuación, se muestran ejemplos utilizando nslookup.

**▸** Obtener la IP de UNIR:

Verás una salida similar a esta:

![image-19](images/image-19.png)

Anota la dirección IP que aparece en la sección Address, que en este caso es

185.56.73.23.

**▸** Obtener la IP de un periódico (por ejemplo, El País):

![image-20](images/image-20.png)

La salida puede ser algo así:

![image-21](images/image-21.png)

Anota la IP, que en este caso es 23.216.147.154.

**▸** Obtener la IP de una universidad (por ejemplo, Harvard): La salida podría ser algo así:

![image-22](images/image-22.png)

Anota la IP, que en este caso es 23.22.156.110.

**▸** Obtener la IP de una tienda (por ejemplo, Amazon):

La salida puede ser algo así:

![image-23](images/image-23.png)

**Paso 2. Editar el archivo hosts y modifícale para cumplir con lo solicitado** **▸** Abre el archivo hosts con permisos de superusuario:

![image-24](images/image-24.png)

**▸** Añade las líneas correspondientes a las IP y los dominios personalizados:

- Desplázate al final del archivo y añade las siguientes líneas (reemplaza las IP con las que obtuviste en el Paso 1):

![▸ Archivo hosts modificado: ▸ Guarda y cierra el archivo:](images/image-25.png)

- Para guardar en nano, presiona «Ctrl + O», luego «Enter», y para salir, presiona «Ctrl + X».

#### Paso 3. Comprobar la configuración

**▸** Verificar que el archivo hosts esté funcionando:

- Usa el comando ping para verificar que los nombres personalizados están resolviendo correctamente:

![▸ Deberías ver algo similar a esto:](images/image-26.png)

Si ves respuestas desde las IP correspondientes, la configuración está funcionando correctamente.

**▸** Verificar con el navegador:

- Abre tu navegador web y escribe en la barra de direcciones los dominios personalizados que configuraste (micentro.com, miperiodico.com, etc.).

- Deberías ser redirigido a las páginas web correspondientes de UNIR, El País, Harvard, y Amazon.

#### Paso 4. Configurar la prioridad de resolución de nombres (opcional)

**▸** Edita el archivo /etc/nsswitch.conf para asegurar que se use hosts antes de DNS:

![image-27](images/image-27.png)

**▸** Verifica que la línea hosts: se vea así:

![image-28](images/image-28.png)

**▸** Esto asegura que primero se revise el archivo hosts antes de intentar resolver mediante DNS.

Siguiendo estos pasos, habrás configurado correctamente el archivo hosts para resolver nombres de dominio personalizados en tu sistema Ubuntu. Si los comandos ping y la navegación en el navegador funcionan como se espera, habrás verificado con éxito que la configuración es correcta.

## Entrenamiento 2. Resolver DNS en Windows

**▸ Planteamiento del ejercicio**

Utilizando un equipo Windows se desea comprobar el funcionamiento del archivo host como opción para resolver nombres de dominio.

**▸** Averigua cuáles son las direcciones IP asociadas a los siguientes nombres de dominio: <www.unir.net>, el periódico que más te guste, una universidad, una tienda. Se pueden utilizar las herramientas nslookup, dig o ping para obtener estos datos. ¿Podemos utilizar el comando dig en Windows?

**▸** Editar el archivo host para que sea capaz de resolver consultas a los nombres de dominio anteriores. Por ejemplo, en mi navegador pongo micentro.com y vaya a la página de Unir, si pongo miperiodico.com vaya a la página del periódico.

**▸** Comprobar que este método de resolución de nombres funciona correctamente. Para la comprobación se sugiere realizar una configuración manual de la configuración de red del cliente y utilizar la herramienta ping. ¿Cómo has diseñado la comprobación?

**▸** Se deberá conseguir que el equipo no consiga entrar a las siguiente tres páginas web, redirigiendo a la página de Unir:

- YouTube.

- Netflix.

- Marca.

Para ello puedes valerte de máquinas virtuales en un entorno virtual como VirtualBox.

**▸ Desarrollo paso a paso**

- Paso 1: obtener las direcciones IP de los dominios usando ping.

- Paso 2: editar el archivo hosts en Windows.

- Paso 3: comprobar la configuración.

- Paso 4: bloquear el acceso a YouTube, Netflix, y Marca.

**▸ Solución**

#### Paso 1. Obtener las direcciones IP de los dominios usando ping

Abrir la terminal de comandos (CMD): presiona «Win + R», escribe «cmd» y presiona «Enter».

**▸** Obtener la IP de UNIR.

Ejecuta el siguiente comando:

![image-29](images/image-29.png)

Verás una salida similar a esta:

![image-30](images/image-30.png)

Anota la IP: 185.56.73.23.

**▸** Obtener la IP de un periódico (ejemplo: El País). Ejecuta:

![image-31](images/image-31.png)

La salida puede ser algo como:

![image-32](images/image-32.png)

Anota la IP: 23.216.147.154.

**▸** Obtener la IP de una universidad (ejemplo: Harvard).

Ejecuta:

![image-33](images/image-33.png)

La salida puede ser:

![image-34](images/image-34.png)

Anota la IP: 23.22.156.110.

**▸** Obtener la IP de una tienda (ejemplo: Amazon).

Ejecuta:

![image-35](images/image-35.png)

La salida puede ser:

![image-36](images/image-36.png)

Anota la IP: 205.251.242.103.

En Windows, el comando dig no está disponible por defecto como lo está en

sistemas basados en Unix, pero se puede usar a través de herramientas adicionales como BIND para Windows o utilizando el subsistema de Windows para Linux (WSL).

#### Paso 2. Editar el archivo hosts en Windows

El archivo hosts se encuentra en C:\Windows\System32\drivers\etc\hosts . Necesitas permisos de administrador para editarlo.

**▸** Abrir el archivo hosts con permisos de administrador.

- Presiona «Win + R», escribe «Notepad», y luego presiona «Ctrl + Shift + Enter» para abrir el bloc de notas como administrador.

- En el bloc de notas, haz clic en «Archivo», «Abrir» y navega a C:\Windows\System32\drivers\etc\.

- Cambia «Tipo de archivo» a «Todos de archivos» para ver el archivo hosts.

- Selecciona «hosts» y haz clic en «Abrir».

**▸** Añadir las entradas personalizadas al archivo hosts. Desplázate hasta el final del archivo y añade las siguientes líneas (usando las IP que obtuviste en el Paso 1):

![image-37](images/image-37.png)

**▸** Añade también las entradas para redirigir YouTube, Netflix y marca a la página de UNIR:

![image-38](images/image-38.png)

**▸** Guardar el archivo y cerrar el bloc de notas. Guarda los cambios (Ctrl + S) y cierra el editor.

#### Paso 3. Comprobar la configuración

Verificar que el archivo hosts esté funcionando correctamente. Abre una terminal de comandos (CMD) y realiza un ping a los nombres de dominio personalizados que configuraste en el archivo hosts:

Para micentro.com:

![image-39](images/image-39.png)

Para miperiodico.com:

![image-40](images/image-40.png)

Para miuniversidad.com:

![image-41](images/image-41.png)

Para mitienda.com:

![image-42](images/image-42.png)

Los pings deben devolver respuestas desde las IP que configuraste (las mismas que

obtuviste en el Paso 1).

Para verificar la redirección de YouTube, Netflix y marca:

![image-43](images/image-43.png)

Todos estos comandos deberían devolver la IP 185.56.73.23 (la IP de UNIR que configuraste).

**▸** Verificar en el navegador:

- Abre un navegador web y escribe en la barra de direcciones los dominios personalizados (micentro.com, miperiodico.com, etc.) y verifica que te redirigen a las páginas reales de UNIR, El País, Harvard y Amazon.

- Intenta acceder a YouTube, Netflix y a la marca y verifica que te redirige a la página de UNIR.

#### Paso 4. Bloquear el acceso a YouTube, Netflix y marca

Este paso ya lo has realizado en el Paso 2 al añadir las entradas correspondientes en el archivo hosts. Esto bloquea efectivamente el acceso a esos sitios redirigiendo a la página de UNIR.

Siguiendo estos pasos, has configurado correctamente el archivo hosts en Windows para resolver nombres de dominio personalizados y redirigir ciertos sitios web a la página de UNIR. Esto te permite comprobar el funcionamiento del archivo hosts como método de resolución de nombres en tu sistema Windows.

## Entrenamiento 3. Instalación y configuración de

## servicios DNS en Ubuntu

**▸ Planteamiento del ejercicio**

Como parte del equipo avanzado en la gestión de sistemas informáticos en red, tu habilidad para implementar servicios esenciales de infraestructura es fundamental. El servicio de DNS es una piedra angular en la administración de redes y es esencial establecer una base sólida antes de proceder a su configuración. Tu tarea es preparar un servidor en un entorno Ubuntu, para operar como servidor DNS.

Se desea utilizar el servidor Ubuntu como servidor DNS para que sea capaz de atender consultas de resolución de nombres de dominio. Para ello puedes valerte de máquinas virtuales en un entorno virtual como VirtualBox.

**▸ Desarrollo paso a paso**

- Instalación de Bind9: procede con la instalación del software Bind9 en Ubuntu para su utilización como servidor DNS.

- Confirmación de operatividad: verifica la correcta instalación de Bind9 y determina el PID del proceso para asegurar su funcionamiento.

- Planeación estratégica: describe, en términos generales, los pasos para la configuración de Bind9 en el servidor Ubuntu, sin entrar en detalles técnicos específicos.

- Exploración de alternativas: investiga y presenta una opción diferente a Bind9 para el servidor DNS en Ubuntu, incluyendo una breve evaluación de sus ventajas y desventajas.

**▸ Solución**

#### Instalación de Bind9

**▸ Paso 1. Actualizar el sistema operativo.** Antes de comenzar con la instalación de bind9, asegúrate de que tu sistema operativo esté actualizado. Ejecuta los siguientes comandos en tu terminal:

![image-44](images/image-44.png)

**▸ Paso 2. Instalación de Bind9.** Para instalar bind9, utiliza el siguiente comando:

![image-45](images/image-45.png)

Este comando instalará el servidor DNS bind9, junto con las utilidades y la documentación relacionadas.

#### Confirmación de operatividad

**▸ Paso 1. Verificar el estado de Bind9.** Una vez que se complete la instalación, es importante verificar que el servicio de bind9 esté en funcionamiento. Para ello, puedes utilizar el siguiente comando:

![image-46](images/image-46.png)

Deberías ver una salida que indique que el servicio está *active (running).*

![image-47](images/image-47.png)

**▸ Paso 2. Verificar el PID.** Para obtener el PID del proceso de bind9, puedes utilizar el siguiente comando:

Este comando devolverá el PID del proceso named, que es el nombre del demonio de bind9.

![image-48](images/image-48.png)

#### Planeación estratégica

**▸ Paso 1. Configuración básica de Bind9.**

**Configuración del archivo named.conf.local.** Aquí se define la zona DNS que el servidor administrará, tanto para la resolución directa (de nombre a IP) como inversa (de IP a nombre). A continuación, se muestra un ejemplo de cómo configurar zonas para un dominio ficticio example.com y su correspondiente resolución inversa.

**▸** Edita el archivo named.conf.local.

**▸** Abre el archivo en un editor de texto, por ejemplo, usando nano:

![image-49](images/image-49.png)

**Añade la configuración para las zonas.** Aquí se definen las zonas directa e inversa. Asegúrate de adaptar los nombres de dominio y direcciones IP a tu propia configuración.

![image-50](images/image-50.png)

**Creación de archivos de zona.** Estos archivos contienen los registros DNS como A, CNAME, MX, etc., que definen cómo se debe resolver el nombre de dominio.

Necesitarás crear dos archivos de zona: uno para la resolución directa (db.example.com) y otro para la resolución inversa (db.192.168.1). Estos archivos contienen los registros DNS.

Crea el directorio para las zonas (si aún no existe):

![image-51](images/image-51.png)

Crea y edita el archivo de zona directa ( db.example.com ):

![image-52](images/image-52.png)

Ejemplo de contenido para db.example.com :

![image-53](images/image-53.png)

Crea y edita el archivo de zona inversa ( db.192.168.1 ):

![image-54](images/image-54.png)

![Ejemplo de contenido para db.192.168.1 :](images/image-55.png)

**Configuración de la resolución recursiva.** Si el servidor DNS actuará como un servidor recursivo (capaz de resolver cualquier dominio, no solo aquellos definidos en sus zonas), se debe habilitar esta función en la configuración.

Para habilitar la resolución recursiva, necesitarás ajustar la configuración en el

archivo named.conf.options , que se encuentra en /etc/bind/named.conf.options .

Edita el archivo named.conf.options:

![image-56](images/image-56.png)

Asegúrate de que la resolución recursiva esté habilitada: verifica o añade la sección Options para habilitar la resolución recursiva. Asegúrate de que la sección se parezca a esto:

![image-57](images/image-57.png)

**Verificación de la configuración.** Antes de reiniciar el servicio, es importante verificar que la configuración de bind9 no contenga errores usando:

Verifica la configuración de named:

![image-58](images/image-58.png)

Verifica los archivos de zona:

![image-59](images/image-59.png)

Estos comandos te informarán si hay errores en la configuración o en los archivos de

zona.

**Reinicio del servicio.** Luego de realizar la configuración, reinicia el servicio para aplicar los cambios:

![image-60](images/image-60.png)

#### Exploración de alternativas a Bind9

**▸ Unbound:** es un servidor DNS recursivo, validado y con soporte de DNSSEC. Es ligero, eficiente y diseñado principalmente para resolver nombres de dominio y proporcionar seguridad adicional mediante la validación DNSSEC.

**▸ Ventajas de Unbound:**

- Simplicidad: es más fácil de configurar en comparación con bind9, especialmente si solo necesitas un servidor DNS recursivo.

- Rendimiento: generalmente, Unbound es más rápido y consume menos recursos que bind9.

- Seguridad: ofrece soporte nativo para DNSSEC, proporcionando una capa adicional de seguridad al validar las respuestas DNS.

**▸ Desventajas de Unbound:**

- Menos flexible: Unbound es excelente como un servidor DNS recursivo, pero es menos flexible que bind9 para configuraciones más complejas o autoritativas.

- Menos documentado: Unbound tiene menos documentación y una comunidad más pequeña en comparación con bind9, lo que puede ser un obstáculo para la resolución de problemas.

**▸ Conclusión:** si necesitas un servidor DNS autoritativo, bind9 sigue siendo la opción más robusta y flexible. Sin embargo, si buscas un servidor recursivo ligero y rápido, Unbound es una excelente alternativa.

Con estos pasos y consideraciones, tendrás una buena base para la implementación de un servidor DNS en Ubuntu utilizando bind9, así como una comprensión de una alternativa viable con Unbound.

## Entrenamiento 4. Instalación y configuración de

## servicio DNS en Windows

**▸ Planteamiento del ejercicio**

Se desea utilizar un servidor Windows Server como servidor DNS para que sea capaz de atender consultas de resolución de nombres de dominio.

Imagina que tu empresa, MiEmpresa, necesita un servidor DNS interno para gestionar la resolución de nombres de dominio en su red local. El dominio que deseas usar es miempresa.local y tienes algunos servidores y dispositivos que quieres configurar en este dominio. Además, deseas que el servidor DNS reenvíe las consultas externas a servidores DNS públicos, como los de Google.

**▸ Desarrollo paso a paso**

- Implementación de servicios: instala la característica de servidor DNS en Windows Server y asegúrate de que está lista para ser configurada.

- Verificación de implementación: comprueba que el servicio DNS se ha instalado correctamente y está operativo.

- Análisis técnico: sin entrar en detalles de configuración, redacta una descripción del proceso de configuración del servicio DNS en Windows Server.

- Investigación complementaria: identifica al menos una alternativa al servicio DNS incorporado de Microsoft que pueda ser implementado en Windows Server, proporcionando una justificación técnica para su uso.

**▸ Solución**

#### Implementación de servicios: instalación de la característica de servidor DNS

**▸ Paso 1. Acceder al servidor Windows.** Inicia sesión en el servidor Windows Server con una cuenta que tenga privilegios de administrador.

**▸ Paso 2. Abrir el administrador del servidor.** Una vez dentro del sistema, abre el administrador del servidor desde el menú de inicio.

**▸ Paso 3. Agregar roles y características.** En el administrador del servidor, selecciona la opción «Administrar» en la esquina superior derecha y luego elige «Agregar roles y características».

**▸ Paso 4. Seleccionar tipo de instalación.** En el asistente que se abre, selecciona «Instalación basada en roles o en características» y haz clic en «Siguiente».

**▸ Paso 5. Seleccionar el servidor.** Selecciona el servidor en el que deseas instalar el rol de DNS de la lista que aparece. Generalmente, este será el servidor local.

**▸ Paso 6.Seleccionar rol de servidor.** En la lista de roles, marca la casilla «Servidor DNS». Si aparecen ventanas emergentes pidiendo instalar características adicionales necesarias, haz clic en «Agregar características».

**▸ Paso 7. Confirmar la instalación.** Revisa las selecciones hechas y haz clic en «Instalar». La instalación comenzará y puede tomar varios minutos.

**▸ Paso 8. Finalizar la instalación.** Una vez completada la instalación, aparecerá una notificación. Haz clic en «Cerrar» para salir del asistente.

#### Verificación de implementación

**▸ Paso 1. Revisar que el servidor DNS aparece en el administrador del servidor.** Vuelve al administrador del servidor y verifica en el panel de la izquierda que el rol de servidor DNS aparece instalado.

**▸ Paso 2. Abrir la consola de administración de DNS.** Desde el administrador del servidor, selecciona «Herramientas» en la parte superior derecha y luego elige «DNS» para abrir la consola de administración de DNS.

**▸ Paso 3. Verificar el estado del servicio DNS.** En la consola de DNS, verifica que el servicio DNS está en ejecución. Puedes hacerlo revisando las zonas de búsqueda directa e inversa que se encuentran en el árbol de navegación a la izquierda.

**▸ Paso 4. Consultar registros existentes.** Expande las zonas de búsqueda directa e inversa para asegurarte de que puedes ver los registros predeterminados sin errores.

**▸ Paso 5. Comprobar el servicio.** Como verificación final, puedes usar el comando nslookup en la línea de comandos de Windows para realizar una consulta DNS. Por ejemplo, abre «Símbolo del sistema» y escribe «nslookup nombre_dominio». Deberías recibir una respuesta del servidor DNS que acabas de configurar.

#### Proceso de configuración del servicio DNS en Windows Server

Paso 1. Crear zonas DNS:

**▸ Abrir la consola DNS:**

- Inicia sesión en tu Windows Server y abre la consola de administración DNS desde el «Administrador del servidor» > «Herramientas» > «DNS».

**▸ Crear una zona de búsqueda directa:**

- En la consola DNS, haz clic derecho sobre «Zonas de búsqueda directa» y selecciona «Nueva zona».

- En el asistente que se abre, selecciona «Primaria» como el tipo de zona.

- Asigna un nombre a la zona, por ejemplo, miempresa.local.

- Configura la zona para que se replique si tienes otros servidores DNS o selecciona la opción «No replicar esta zona» si es un único servidor.

- El archivo de la zona se creará automáticamente con un nombre basado en la zona (miempresa.local.dns). Confirma y finaliza el asistente.

Paso 2. Configurar zonas de búsqueda inversa:

**▸ Crear una zona de búsqueda inversa:**

- Haz clic derecho sobre «Zonas de búsqueda inversa» en la consola DNS y selecciona «Nueva zona».

- Nuevamente, selecciona «Primaria» como el tipo de zona.

- En el asistente, define el prefijo de la dirección IP para la zona inversa. Por ejemplo, si tu red utiliza direcciones IP en el rango 192.168.1.0/24, el prefijo sería 192.168.1.

- Completa el asistente, lo que creará una zona inversa para las direcciones IP de tu red interna.

Paso 3. Agregar registros DNS:

**▸ Agregar un registro A:**

- Supongamos que tienes un servidor web en 192.168.1.10. Para que este servidor sea accesible como www.miempresa.local, haz clic derecho en la zona miempresa.local y selecciona «Nuevo host (A o AAAA)».

- En el campo «Nombre», introduce www y en «Dirección IP», introduce 192.168.1.10.

- Haz clic en «Agregar host» para crear el registro.

**▸ Agregar un registro MX:**

- Si tienes un servidor de correo en 192.168.1.20, puedes agregar un registro MX (Mail Exchange).

- Haz clic derecho en la zona miempresa.local y selecciona «Nuevo registro MX».

- En «Nombre», deja el campo en blanco para que el registro MX aplique al dominio completo (miempresa.local).

- En «Nombre del servidor de correo», introduce mail.miempresa.local.

- Luego, agrega un registro A para mail.miempresa.local apuntando a 192.168.1.20.

Paso 4. Configurar reenviadores:

**▸ Configurar reenviadores para consultas externas:**

- Haz clic derecho sobre el nombre del servidor en la consola DNS y selecciona «Propiedades».

- Ve a la pestaña «Reenviadores».

- Agrega las direcciones IP de servidores DNS públicos, como 8.8.8.8 y 8.8.4.4 (los servidores DNS de Google).

- Esto permite que las consultas DNS que no puedan ser resueltas internamente (como www.google.com) sean enviadas a estos servidores externos.

Paso 5. Configurar políticas y seguridad:

**▸ Habilitar DNSSEC (opcional):**

- Si deseas habilitar DNSSEC para una mayor seguridad, selecciona la zona miempresa.local, haz clic derecho y selecciona «DNSSEC» > «Configurar firma de zona».

- Sigue el asistente para configurar las firmas DNSSEC, lo que protegerá la integridad de las respuestas DNS en tu dominio.

**▸ Configurar TTL y acceso:**

- Desde la consola DNS, puedes ajustar el TTL (Time to Live) en las propiedades de cada zona para controlar cuánto tiempo se deben almacenar en caché las respuestas.

- También, puedes establecer políticas de acceso para limitar quién puede realizar consultas DNS en tu red.

Paso 6. Realizar pruebas de resolución:

**▸ Pruebas con nslookup:**

- Abre una ventana de «Símbolo del sistema» en cualquier máquina conectada a la red.

**•** Escribe nslookup www.miempresa.local y verifica que devuelve la IP 192.168.1.10.

- También, puedes probar nslookup mail.miempresa.local para confirmar que el servidor de correo está configurado correctamente.

#### Alternativa al servicio DNS incorporado: BIND en Windows Server

**▸ Alternativa propuesta: BIND** (Berkeley Internet Name Domain)

- Descarga e instalación: aunque BIND es, tradicionalmente, un servicio que se ejecuta en sistemas UNIX/Linux, existe una versión compatible con Windows que puede descargarse desde el sitio oficial de ISC.

**▸ Justificación técnica:**

- Flexibilidad y control: BIND permite una configuración muy detallada y personalizada, lo cual es útil en entornos donde se requiere un control granular de las políticas DNS.

- Compatibilidad multiplataforma: puedes integrar BIND en un entorno mixto de servidores Windows y Linux, facilitando la administración de DNS en redes heterogéneas.

- Seguridad: BIND ofrece opciones avanzadas de seguridad, incluyendo soporte robusto para DNSSEC y TSIG, que permiten proteger las transacciones DNS y asegurar la integridad de la resolución de nombres.

**▸ Configuración básica:**

- Configurar BIND en Windows implica editar archivos de configuración manualmente, como named.conf, y definir zonas de manera similar a cómo lo harías en la consola DNS de Windows, pero con mayor control sobre las opciones avanzadas.

**▸ Pruebas y validación:**

- Una vez configurado, BIND se comportará como cualquier otro servidor DNSy permitirá realizar consultas y validar las configuraciones utilizando herramientas como nslookup.

## Entrenamiento 5. Configuración servidor DNS caché en Windows

**▸ Planteamiento del ejercicio** Se desea utilizar un servidor Windows Server como servidor DNS cache. Es decir, este servidor debe ser capaz de almacenar las consultas de nombres resueltas desde el exterior para poder ofrecerlas localmente.

**▸ Desarrollo paso a paso**

- Configura el servidor Windows Server para funcionar como servidor DNS caché.

- Utiliza el cliente Ubuntu y configura sus parámetros de red para que el servidor Windows Server sea su servidor DNS.

- El servidor DNS utilizará como servidores reenviadores los servidores DNS de Google (8.8.8.8 y 8.8.4.4).

- Usa la herramienta nslookup con el cliente Ubuntu y realiza las siguientes consultas: <www.youtube.es>, <www.unican.es>, <www.decroly.com> y <www.as.com>.

- Muestra la caché de consultas del servidor Windows Server y comprueba que las consultas anteriores están almacenadas en el propio servidor.

**▸ Solución**

#### Configura el servidor Windows Server para funcionar como servidor DNS

#### caché

Paso 1. Instalar el rol de servidor DNS en Windows Server

**▸** Abre «Administrador del servidor» en tu Windows Server.

**▸** Haz clic en «Agregar roles y características».

**▸** En «Seleccionar tipo de instalación», elige «Instalación basada en características o

en roles». **▸** Selecciona tu servidor en la lista y haz clic en «Siguiente». **▸** Marca la casilla «Servidor DNS» en la lista de roles disponibles y sigue las instrucciones para completar la instalación. Paso 2. Configurar el DNS para actuar como caché **▸** Abre la consola «Administrador DNS» (dnsmgmt.msc). **▸** Haz clic derecho sobre tu servidor DNS (en la parte superior del árbol) y selecciona «Propiedades». **▸** En la pestaña de «Reenviadores», haz clic en «Editar». **▸** Añade las direcciones IP de los servidores DNS de Google (8.8.8.8 y 8.8.4.4). **▸** Asegúrate de que no haya otras zonas configuradas que puedan interferir y que el servidor esté configurado para reenviar cualquier consulta no resuelta localmente a los servidores de Google. **▸** Guarda los cambios.

#### Configuración del cliente Ubuntu para usar el servidor DNS Windows

Paso 1. Configurar los parámetros de red **▸** Edita el archivo /etc/netplan/01-netcfg.yaml (el archivo puede tener un nombre diferente dependiendo de tu configuración de red).

**▸** Asegúrate de que el contenido del archivo esté configurado para usar el servidor DNS de Windows Server. Por ejemplo:

![image-61](images/image-61.png)

**▸** Reemplaza <IP_DEL_SERVIDOR_WINDOWS> con la dirección IP del servidor DNS de Windows Server.

Paso 2. Aplicar la configuración

**▸** Guarda el archivo y ejecuta el siguiente comando para aplicar la nueva configuración:

![image-62](images/image-62.png)

**▸** Verifica que la configuración haya sido aplicada correctamente ejecutando:

![image-63](images/image-63.png)

Asegúrate de que la IP del servidor DNS sea la del servidor Windows.

**▸** Realizar consultas DNS desde Ubuntu. Utiliza la herramienta nslookup en Ubuntu para hacer las consultas DNS:

- Abre una terminal en Ubuntu.

- Realiza las consultas:

![Y se debería obtener lo siguiente: Verificar la caché en el servidor Windows Server Paso 1. Verificar la caché DNS:](images/image-64.png)

**▸** Entra en el «Administrador DNS» en Windows Server.

**▸** Haz clic derecho sobre tu servidor en la parte superior del árbol y selecciona «Propiedades».

**▸** Navega a la pestaña «Monitorización» y asegúrate de que la caché DNS esté habilitada.

**▸** También, puedes utilizar la consola DNS para ver directamente las entradas en la caché. Haz clic en la opción «Ver caché» para revisar las entradas que están almacenadas.

#### Verificar las entradas caché de las consultas realizadas

- ▸ Dentro del «Administrador DNS» ve a «Caché de búsquedas directas».

- ▸ Busca las entradas para <www.youtube.es>, <www.unican.es>, <www.decroly.com>

    - y <www.as.com>.

- ▸ Si las entradas están presentes, significa que las consultas fueron resueltas y

    - almacenadas correctamente en la caché DNS del servidor Windows.

#### Conclusión

Siguiendo estos pasos, habrás configurado un servidor Windows Server como un servidor DNS caché, configurado un cliente Ubuntu para utilizar este servidor como su DNS y verificado que las consultas DNS se almacenan en la caché del servidor. Si todo ha sido configurado correctamente, las entradas de las consultas realizadas con nslookup deberían aparecer en la caché del servidor DNS en Windows.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–42)*
- A fondo  *(pp.43–54)*
- Entrenamientos  *(pp.55–85)*
- Servicios en Red e Internet 5 Tema 3. Material de estudio · Servicios en Red e Internet 6 Tema 3. Material de estudio · Servicios en Red e Internet 7 Tema 3. Material de estudio · Servicios en Red e Internet 8 Tema 3. Material de estudio · Servicios en Red e Internet 9 Tema 3. Material de estudio · Servicios en Red e Internet 10 Tema 3. Material de estudio · Servicios en Red e Internet 11 Tema 3. Material de estudio · Servicios en Red e Internet 13 Tema 3. Material de estudio · Servicios en Red e Internet 14 Tema 3. Material de estudio · Servicios en Red e Internet 15 Tema 3. Material de estudio · Servicios en Red e Internet 16 Tema 3. Material de estudio · Servicios en Red e Internet 17 Tema 3. Material de estudio · Servicios en Red e Internet 18 Tema 3. Material de estudio · Servicios en Red e Internet 19 Tema 3. Material de estudio · Servicios en Red e Internet 20 Tema 3. Material de estudio · Servicios en Red e Internet 21 Tema 3. Material de estudio · Servicios en Red e Internet 22 Tema 3. Material de estudio · Servicios en Red e Internet 23 Tema 3. Material de estudio · Servicios en Red e Internet 24 Tema 3. Material de estudio · Servicios en Red e Internet 25 Tema 3. Material de estudio · Servicios en Red e Internet 26 Tema 3. Material de estudio · Servicios en Red e Internet 27 Tema 3. Material de estudio · Servicios en Red e Internet 28 Tema 3. Material de estudio · Servicios en Red e Internet 29 Tema 3. Material de estudio · Servicios en Red e Internet 30 Tema 3. Material de estudio · Servicios en Red e Internet 31 Tema 3. Material de estudio · Servicios en Red e Internet 32 Tema 3. Material de estudio · Servicios en Red e Internet 33 Tema 3. Material de estudio · Servicios en Red e Internet 34 Tema 3. Material de estudio · Servicios en Red e Internet 35 Tema 3. Material de estudio · Servicios en Red e Internet 36 Tema 3. Material de estudio · Servicios en Red e Internet 37 Tema 3. Material de estudio · Servicios en Red e Internet 38 Tema 3. Material de estudio · Servicios en Red e Internet 39 Tema 3. Material de estudio · Servicios en Red e Internet 40 Tema 3. Material de estudio · Servicios en Red e Internet 41 Tema 3. Material de estudio · Servicios en Red e Internet 42 Tema 3. Material de estudio  *(pp.5, 6, 7, 8, 9, 10, 11, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42)*
- Servicios en Red e Internet 43 Tema 3. A fondo · Servicios en Red e Internet 44 Tema 3. A fondo · Servicios en Red e Internet 45 Tema 3. A fondo · Servicios en Red e Internet 46 Tema 3. A fondo · Servicios en Red e Internet 47 Tema 3. A fondo · Servicios en Red e Internet 48 Tema 3. A fondo · Servicios en Red e Internet 49 Tema 3. A fondo · Servicios en Red e Internet 50 Tema 3. A fondo · Servicios en Red e Internet 51 Tema 3. A fondo · Servicios en Red e Internet 52 Tema 3. A fondo · Servicios en Red e Internet 53 Tema 3. A fondo · Servicios en Red e Internet 54 Tema 3. A fondo  *(pp.43–54)*
- Servicios en Red e Internet 55 Tema 3. Entrenamientos · Servicios en Red e Internet 56 Tema 3. Entrenamientos · Servicios en Red e Internet 57 Tema 3. Entrenamientos · Servicios en Red e Internet 58 Tema 3. Entrenamientos · Servicios en Red e Internet 59 Tema 3. Entrenamientos · Servicios en Red e Internet 60 Tema 3. Entrenamientos · Servicios en Red e Internet 61 Tema 3. Entrenamientos · Servicios en Red e Internet 62 Tema 3. Entrenamientos · Servicios en Red e Internet 63 Tema 3. Entrenamientos · Servicios en Red e Internet 64 Tema 3. Entrenamientos · Servicios en Red e Internet 65 Tema 3. Entrenamientos · Servicios en Red e Internet 66 Tema 3. Entrenamientos · Servicios en Red e Internet 67 Tema 3. Entrenamientos · Servicios en Red e Internet 68 Tema 3. Entrenamientos · Servicios en Red e Internet 69 Tema 3. Entrenamientos · Servicios en Red e Internet 70 Tema 3. Entrenamientos · Servicios en Red e Internet 71 Tema 3. Entrenamientos · Servicios en Red e Internet 72 Tema 3. Entrenamientos · Servicios en Red e Internet 73 Tema 3. Entrenamientos · Servicios en Red e Internet 74 Tema 3. Entrenamientos · Servicios en Red e Internet 75 Tema 3. Entrenamientos · Servicios en Red e Internet 76 Tema 3. Entrenamientos · Servicios en Red e Internet 77 Tema 3. Entrenamientos · Servicios en Red e Internet 78 Tema 3. Entrenamientos · Servicios en Red e Internet 79 Tema 3. Entrenamientos · Servicios en Red e Internet 80 Tema 3. Entrenamientos · Servicios en Red e Internet 81 Tema 3. Entrenamientos · Servicios en Red e Internet 82 Tema 3. Entrenamientos · Servicios en Red e Internet 83 Tema 3. Entrenamientos · Servicios en Red e Internet 84 Tema 3. Entrenamientos · Servicios en Red e Internet 85 Tema 3. Entrenamientos  *(pp.55–85)*