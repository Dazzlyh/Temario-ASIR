## Tema 5

## Servicios en Red e Internet

# Tema 5. Transferencia de

# ficheros

# Índice

Esquema Material de estudio

## 5.1. Introducción y objetivos

## 5.2. Características

## 5.3. Cliente y servidor FTP

## 5.4. Sitio FTP, usuarios y grupos

## 5.5. Permisos

## 5.6. Ancho de banda y cuotas

## 5.7. Tipos de transmisión de datos

## 5.8. Modos de conexión

## 5.9. Referencias bibliográficas

A fondo FTP: qué es y cómo funciona (Fernández, 2024) Qué es un servidor FTP y cómo usarlo en nuestro hosting ¿Qué es el FTP y cómo puedo utilizarlo para transferir archivos?

Qué es un servidor FTP y para qué se utiliza

10 mejores clientes FTP para usuarios de WordPress

(Mac y Windows)

FTP activo vs. FTP pasivo

Qué es FTP y como utilizarlo

Administración de sistemas. Comandos FTP

Administración de sistemas. FTP Modos

Entrenamiento 1. Cuestiones por desarrollar sobre el servicio FTP

Entrenamiento 2. Clientes FTP

Entrenamiento 3. Servidores FTP en Windows

Entrenamiento 4. Servidores FTP en Ubuntu

Entrenamiento 5. Configuración y prueba de conexión de

un servidor FTP con cliente en Ubuntu usando VirtualBox

# Esquema

![image-2](images/image-2.png)

Servicios en Red e Internet 4 Tema 5. Esquema

## 5.1. Introducción y objetivos

Uno de los principales objetivos al implementar cualquier tipo de red de comunicaciones es permitir a los usuarios compartir información diversa, como textos, imágenes, vídeos y archivos de aplicaciones, entre otros. Este **intercambio** **de datos** es fundamental para la interacción en el entorno digital y se puede lograr mediante **diferentes sistemas y métodos** que facilitan la transmisión de información a través de la red.

En la unidad anterior, se exploró un método particular para compartir información: el uso de un servidor web para publicar y distribuir contenido a través de páginas web. Este enfoque es una solución ampliamente utilizada en la informática, ya que permite que la información esté disponible en línea, accesible para cualquier usuario con acceso a Internet. Sin embargo, es importante destacar que no es la única opción disponible para compartir información en una red de comunicaciones.

Existen múltiples métodos alternativos para la transferencia de datos entre usuarios, cada uno con sus propias características, ventajas y desventajas. Uno de los sistemas más conocidos es el **modelo de red P2P** *(Peer-to-Peer),* donde los usuarios comparten archivos directamente entre sí sin la necesidad de un servidor centralizado. Ejemplos clásicos de este tipo de sistemas incluyen Emule, Ares y BitTorrent. Estas plataformas permiten a los usuarios intercambiar archivos de manera directa, aprovechando la capacidad de cada dispositivo en la red para actuar tanto como cliente como servidor.

E s t e **enfoque descentralizado** tiene la ventaja de ser altamente escalable y resiliente, aunque, también, ha estado sujeto a controversias debido a su uso para la distribución de material protegido por derechos de autor.

Otro método popular para compartir archivos es a través de **sistemas de descarga** **directa.** En este modelo, los usuarios suben archivos a un servidor centralizado, desde el cual otros usuarios pueden descargar dichos archivos. Plataformas como la desaparecida Megaupload, Bitshare, Uploaded y Mega han sido ejemplos prominentes de este tipo de servicio. Estas plataformas son generalmente fáciles de usar, lo que las hace atractivas para una amplia base de usuarios. Sin embargo, también, han enfrentado desafíos legales relacionados con el almacenamiento y distribución de contenido ilegal.

Una alternativa más técnica y segura para compartir archivos es el uso de herramientas como **SCP (Secure Copy).** SCP permite la transferencia de archivos y carpetas entre dos dispositivos de manera segura utilizando el protocolo SSH (Secure Shell). Este método es muy valorado en entornos profesionales y académicos debido a su enfoque en la seguridad, ya que el **protocolo SSH** proporciona cifrado y autenticación, asegurando que la información transferida no sea interceptada por terceros no autorizados. SCP es especialmente útil cuando se necesita garantizar la integridad y confidencialidad de los datos durante la transferencia.

Además de estos métodos, existen muchas otras técnicas y herramientas para la transferencia de archivos a través de redes de comunicación. Por ejemplo, los servicios de **almacenamiento en la nube,** como Google Drive, Dropbox y OneDrive, permiten a los usuarios subir, compartir y acceder a archivos desde cualquier dispositivo con conexión a internet. Estos servicios no solo facilitan la transferencia de archivos, sino que, también, ofrecen funcionalidades adicionales, como la sincronización automática de archivos entre dispositivos y la colaboración en tiempo real en documentos.

Las **aplicaciones de mensajería instantánea,** como WhatsApp, Telegram y Slack, también se han convertido en herramientas populares para compartir archivos.

Aunque originalmente diseñadas para el intercambio de mensajes, estas plataformas han evolucionado para soportar la transferencia de archivos de diversos formatos, lo que las convierte en una opción conveniente para compartir información rápidamente entre individuos o grupos.

En el contexto de esta unidad, se profundizará en el **protocolo FTP** (File Transfer Protocol) como una de las formas más tradicionales y ampliamente utilizadas para la transferencia de archivos. FTP permite la transmisión de datos entre un cliente y un servidor a través de una **red TCP/IP.** A pesar de ser un protocolo antiguo, FTP sigue siendo relevante debido a su simplicidad y eficiencia en la transferencia de grandes volúmenes de datos.

En resumen, existen múltiples métodos y herramientas para compartir información en una red de comunicaciones, cada uno adecuado para diferentes necesidades y escenarios. Desde el uso de servidores web y redes P2P hasta la transferencia segura mediante SCP o el tradicional FTP, la elección del método adecuado depende de factores como la cantidad de datos que transferir, la necesidad de seguridad, la facilidad de uso y el contexto en el que se va a realizar la transferencia. Esta unidad se centrará en comprender y utilizar el protocolo FTP, una herramienta fundamental en la transferencia de archivos que sigue siendo relevante en el mundo digital actual.

Los **objetivos** que se pretende alcanzar en este tema son:

**▸** Comprender el propósito del servicio de transferencia de ficheros.

**▸** Conocer las aplicaciones del servicio.

**▸** Identificar diferentes métodos de transferencia de archivos.

**▸** Reconocer la historia del protocolo FTP.

**▸** Comprender la arquitectura FTP.

**▸** Distinguir entre clientes FTP en modo gráfico y texto. **▸** Configurar y utilizar clientes FTP. **▸** Implementar y administrar servidores FTP. **▸** Gestionar sitios FTP. **▸** Administrar usuarios y grupos en un servidor FTP. **▸** Aplicar medidas de seguridad en la transferencia de archivos. **▸** Optimizar la transferencia de datos. **▸** Establecer permisos de usuario adecuados. **▸** Optimizar el uso del ancho de banda. **▸** Implementar y gestionar cuotas de almacenamiento. **▸** Seleccionar el tipo adecuado de transmisión de datos. **▸** Elegir el modo de conexión apropiado (activo o pasivo).

## 5.2. Características

¿Qué es este servicio?

El servicio de transferencia de ficheros, como su nombre sugiere, se refiere a la **capacidad de intercambiar archivos** entre diferentes dispositivos conectados a una red. Este servicio se puede definir de la siguiente manera:

Es un servicio que facilita el intercambio de archivos entre dispositivos en una red de forma sencilla y transparente para el usuario, sin importar el tipo de sistema operativo que utilicen los dispositivos involucrados.

Esto implica que **cualquier dispositivo conectado a la red** tiene la capacidad de compartir todo tipo de archivos, como documentos de texto, imágenes, aplicaciones y archivos multimedia, entre otros, sin que el usuario tenga que preocuparse por los detalles técnicos del proceso.

En otras palabras, cuando un usuario decide transferir un archivo de un dispositivo a otro, el proceso ocurre de manera automática y sin que el usuario sea consciente de los detalles técnicos que están ocurriendo en segundo plano. Este proceso es indiferente a las diferencias entre los sistemas operativos de los dispositivos involucrados. Por ejemplo, es posible transferir archivos sin problemas entre un dispositivo que funcione con un sistema operativo de la familia Microsoft y otro que utilice alguna distribución de Linux y viceversa. De igual manera, este servicio es **compatible con otros sistemas operativos,** como Android o macOS, permitiendo un intercambio de archivos fluido y sin complicaciones.

El servicio de transferencia de ficheros, al igual que otros servicios de red, es opcional, pero su implementación es altamente recomendable en cualquier red donde se requiera compartir información entre múltiples usuarios.

Dada la creciente necesidad de las empresas y organizaciones modernas de facilitar el acceso y la distribución de datos entre sus miembros, contar con un servicio de **transferencia de ficheros** se convierte en una solución esencial para garantizar la **eficiencia y productividad** en el manejo de la información. La capacidad de compartir archivos de manera rápida y segura dentro de una red es una herramienta invaluable para cualquier entorno que requiera colaboración y comunicación constante entre dispositivos y usuarios.

¿Para qué sirve?

El servicio de transferencia de ficheros, como su nombre lo indica, tiene como propósito principal permitir la transferencia de archivos entre diferentes equipos conectados a una red. Sin embargo, sus aplicaciones van mucho más allá de simplemente mover datos de un dispositivo a otro, ofreciendo una amplia gama de usos y beneficios.

**▸ Uso de la red como un sistema virtual de archivos:** una de las aplicaciones más destacadas de este servicio es la posibilidad de utilizar la red como si fuera un sistema de archivos virtual. Esto se puede lograr mediante la implementación de un servidor de intercambio de archivos, como un servidor FTP (File Transfer Protocol).

Gracias a este servidor, los usuarios de la red pueden acceder y gestionar archivos como si estuvieran trabajando directamente en sus propios equipos locales.

Además, este tipo de servidor no solo permite acceder a los archivos, sino que, también, posibilita la creación y almacenamiento de nuevos ficheros, funcionando como un repositorio centralizado. Otra aplicación importante es la posibilidad de utilizar el servidor FTP como un espacio de almacenamiento para realizar copias de seguridad de los dispositivos locales, permitiendo que los datos de la red se respalden de manera periódica y segura.

**▸ Compartir archivos entre diferentes sistemas operativos y sistemas de** **archivos:** en entornos de red donde coexisten dispositivos con diferentes sistemas operativos, como Windows, Linux, macOS o Android y sistemas de archivos diversos

(FAT32, NTFS, EXT4, etc.), el servicio de transferencia de ficheros se convierte en una herramienta esencial. Este servicio permite el intercambio de información entre estos equipos sin preocuparse por las diferencias en los sistemas operativos o los formatos de archivo, facilitando la colaboración y el flujo de trabajo en redes heterogéneas.

**▸ Eficiencia en la transferencia de datos:** este servicio también destaca por su capacidad de realizar transferencias de datos de manera eficaz, independientemente de la ubicación geográfica de los dispositivos involucrados. Por ejemplo, es común utilizar este servicio en el contexto de los servicios de *hosting* para actualizar el contenido de los servidores web, como las páginas web. Asimismo, es ampliamente utilizado para descargar archivos de Internet, como actualizaciones de *software* y parches, o para intercambiar archivos a través de servicios de computación en la nube como Mega, Dropbox, Google Drive o plataformas educativas como Moodle. Estos ejemplos demuestran cómo el servicio de transferencia de ficheros facilita el acceso y la distribución de datos de manera rápida y segura, contribuyendo a la eficiencia operativa de las redes y sistemas actuales.

Historia y funcionalidad

Ya se ha mencionado previamente en esta unidad que un servicio de transferencia de ficheros puede implementarse de diversas maneras y con múltiples técnicas, siendo crucial elegir aquella que mejor se adapte a nuestras necesidades específicas. En lo que resta de la unidad, se pondrá el foco en la transferencia de ficheros más común y tradicional: la que se basa en el protocolo FTP (File Transfer Protocol).

El protocolo FTP surgió en la **década de 1970** gracias al **Massachusetts Institute of** **Technology (MIT),** una de las universidades más reconocidas a nivel mundial, ubicada en Estados Unidos. Su creación tuvo como objetivo facilitar una transferencia de información eficiente y rápida entre diferentes dispositivos. Actualmente, este protocolo está formalmente definido y descrito en el RFC (Request for Comments) 959.

Como se ha indicado, el protocolo FTP fue diseñado con la misión de ofrecer un servicio de transferencia de archivos rápido. La idea era que los datos pudieran transferirse entre dispositivos a una **velocidad razonable,** algo esencial en el contexto de la época.

Sin embargo, esta rapidez en la transferencia se logró sacrificando la seguridad.

Esto significa que, en el contexto original del protocolo, la autenticación de los usuarios en el servidor FTP se realiza **sin ningún tipo de cifrado.** Es decir, cualquier individuo con la capacidad de interceptar el tráfico de red podría potencialmente obtener nombres de usuario y contraseñas.

Además, la información que fluye entre los dispositivos conectados tampoco está cifrada, lo que implica que cualquier persona con acceso para escuchar la red podría acceder a los datos que se estén transfiriendo en ese momento, exponiendo así información sensible a posibles interceptaciones.

Al igual que otros protocolos que se han estudiado y trabajado a lo largo del curso, como el protocolo DHCP, el protocolo DNS o el protocolo HTTP, el **protocolo FTP** también opera en la **capa de aplicación,** que es la capa superior de la pila de protocolos del modelo OSI (Open System Interconnection). Este modelo divide las comunicaciones de red en siete capas, siendo la capa de aplicación la encargada de

Servicios en Red e Internet 12 Tema 5. Material de estudio proporcionar servicios directamente a las aplicaciones de *software,* facilitando la interacción del usuario con la red.

El protocolo FTP, al igual que otros servicios que hemos explorado en unidades anteriores, implementa el servicio de transferencia de archivos siguiendo un **modelo** **cliente/servidor.** Esto significa que existe un cliente FTP, que es el *software* o dispositivo que solicita un servicio y un servidor FTP, que es el que proporciona dicho servicio. Por ejemplo, el cliente FTP podría solicitar al servidor FTP la transferencia de un archivo, ya sea para subirlo o descargarlo, y si el servidor FTP está en condiciones de hacerlo, llevará a cabo la operación solicitada.

![Figura 1. Conexión FTP. Fuente: Conexión FTP: qué es, qué necesitas y programas populares, s. f.](images/image-3.png)

*Figura 1. Conexión FTP. Fuente: Conexión FTP: qué es, qué necesitas y programas populares, s. f.*

No obstante, a diferencia de otros servicios estudiados, la transferencia de datos mediante FTP requiere el uso de **dos conexiones** en lugar de una sola: la conexión de control y la conexión de datos.

L a **conexión de control** es la que utiliza el cliente FTP para enviar órdenes al servidor. Por esta conexión, el cliente puede indicar al servidor qué acción desea realizar, cómo subir un archivo, descargarlo o indicar el nombre del archivo en cuestión. Esta conexión se mantiene activa durante toda la sesión para gestionar las instrucciones y el control del proceso.

Por otro lado, la **conexión de datos** es la vía por la cual se realiza la transferencia efectiva de la información entre el cliente y el servidor FTP. Esta segunda conexión es crucial porque permite que, mientras los datos se están transfiriendo, el cliente continúe enviando órdenes al servidor. Esta capacidad es especialmente importante en situaciones donde los archivos a transferir son muy grandes, ya que, si solo se utilizara una única conexión, esta podría saturarse con la transferencia de datos, impidiendo que se envíen otras órdenes hasta que finalice la transmisión.

![Figura 2. Como funciona el FTP. Fuente: Kinsta, 2023.](images/image-4.png)

*Figura 2. Como funciona el FTP. Fuente: Kinsta, 2023.*

El protocolo **FTP opera** a nivel de **capa de transporte** utilizando el protocolo TCP (Transmission Control Protocol), que se encarga de garantizar que los datos se transfieran de manera confiable entre el cliente y el servidor. Por defecto, el servidor FTP utiliza el **puerto 21** para la conexión de control y el **puerto 20** para la conexión de datos. Esto significa que, al configurar un *firewall* en un servidor FTP, es necesario asegurarse de que estos dos puertos estén abiertos para permitir la comunicación adecuada entre el cliente y el servidor.

Además de su función principal de transferir archivos rápidamente entre dispositivos, el protocolo FTP también permite una administración efectiva del sitio FTP, que es la estructura de directorios dentro del servidor FTP. Esto significa que, además de transferir archivos, el usuario puede realizar otras acciones administrativas como crear o eliminar directorios, renombrar archivos y eliminarlos.

Estas funcionalidades hacen del protocolo FTP una herramienta no solo para la transferencia de datos, sino también para la gestión completa de archivos y directorios en un servidor.

Otra característica importante del protocolo FTP es su **capacidad multiplataforma.** Esto implica que un servidor FTP puede ser implementado en prácticamente cualquier dispositivo, siempre que el *hardware* lo permita, independientemente del sistema operativo que esté ejecutando, ya sea Microsoft Windows, Linux, macOS, o cualquier otro.

Asimismo, estos servidores FTP pueden atender a cualquier tipo de cliente, sin importar qué sistema operativo esté utilizando. Esta **flexibilidad** hace que el protocolo FTP sea una excelente opción para la transferencia de archivos en redes heterogéneas, donde coexisten diferentes sistemas operativos y configuraciones.

En resumen, el protocolo FTP es una herramienta fundamental en el ámbito de la transferencia de archivos, que ofrece un método eficaz y rápido para el intercambio de datos entre dispositivos en una red.

Aunque su diseño original no incluía consideraciones de seguridad, su modelo de funcionamiento mediante **dos conexiones separadas para control y datos,** su capacidad de administración de sitios y su naturaleza multiplataforma lo convierten en una solución robusta y versátil, especialmente en entornos donde se necesita un enfoque estándar y confiable para la gestión y transferencia de archivos.

La implementación y uso adecuado del protocolo FTP pueden marcar una gran diferencia en la eficiencia y organización de las operaciones de transferencia de datos en cualquier red informática, especialmente en aquellas que requieren soportar una variedad de dispositivos y sistemas operativos diferentes.

## 5.3. Cliente y servidor FTP

Cliente FTP

El término cliente FTP se refiere al ***software*** **especializado** que permite que un dispositivo, en el que dicho *software* ha sido instalado y configurado, se conecte a servidores FTP. A través de esta conexión, el dispositivo puede acceder al sitio FTP asociado al usuario que realiza la conexión. Este tipo de aplicaciones permite a los usuarios interactuar con su sitio FTP de varias maneras, como subir y descargar archivos, además de gestionar el contenido del sitio, lo que incluye borrar archivos o carpetas, renombrar elementos o, incluso, crear nuevos directorios.

Una de las características más sobresalientes de los clientes FTP en modo gráfico es que su uso y configuración se realiza a través de una **interfaz gráfica** y un **sistema** **de ventanas,** también conocido como ventana de administración. Esta característica ofrece una forma de conectarse a los servidores FTP que es extremadamente cómoda, sencilla e intuitiva. Solo es necesario configurar adecuadamente la ventana de administración proporcionada por el *software* para comenzar a operar.

Además, acciones como subir o descargar archivos al servidor FTP o gestionar el sitio FTP, como eliminar o renombrar archivos o carpetas o crear nuevos directorios, se pueden realizar fácilmente utilizando el ratón. En muchas aplicaciones, la transferencia de archivos se puede llevar a cabo mediante un **sistema de arrastrar y** **soltar** *(drag & drop),* lo que simplifica aún más el proceso.

Existen varias estrategias en el mercado para implementar un cliente FTP en cualquier tipo de dispositivo, ya sea un ordenador, un móvil, una tableta, entre otros, siempre que estos dispositivos puedan alojar el *software* específico que permite la conexión con el servidor FTP.

El término cliente FTP también se refiere a veces al **dispositivo físico** que aloja el *software* específico, es decir, al equipo desde el cual se realizan las solicitudes de recursos a los servidores web.

En cuanto a las **aplicaciones** d e *software* diseñadas para funcionar como clientes FTP, el mercado ofrece una **amplia variedad** aplicaciones libres y propietarias, gratuitas y

con características diversas. Hay de pago, más o menos seguras,

multiplataforma o específicas para ciertos sistemas operativos. Sin embargo, una de las clasificaciones más importantes que se puede hacer de los clientes FTP es según su **interfaz de usuario:** clientes FTP en modo gráfico y clientes FTP en modo texto.

#### Clientes FTP en modo gráfico

Los clientes FTP en modo gráfico se destacan, principalmente, por su **facilidad de** **uso,** ya que están diseñados para ser manejados a través de una interfaz gráfica que suele ser bastante intuitiva. Este tipo de clientes facilita enormemente el proceso de conectarse a servidores FTP y realizar diversas operaciones gracias a su sistema de ventanas. La configuración inicial puede hacerse sin complicaciones, simplemente siguiendo los pasos que la interfaz gráfica proporciona. Una vez configurado, el usuario puede subir y bajar archivos, así como gestionar el sitio FTP (eliminar, renombrar y crear archivos o carpetas) con gran facilidad, utilizando el ratón y otras herramientas gráficas del sistema operativo.

En el mercado se pueden encontrar diferentes enfoques para implementar un cliente FTP en dispositivos como ordenadores, móviles o tabletas. Algunos ejemplos de estas **estrategias** incluyen:

**▸** ***Software*** **específico:** estas son aplicaciones que se instalan directamente en los dispositivos y que pueden ser utilizadas como cualquier otro programa. Estas aplicaciones pueden ser multiplataforma, es decir, compatibles con varios sistemas operativos, o diseñadas específicamente para uno en particular. Ejemplos comunes de este tipo de *software* incluyen FileZilla Client, gFTP y CuteFTP, entre otros. Estos

Servicios en Red e Internet 18 Tema 5. Material de estudio programas ofrecen una interfaz gráfica que simplifica mucho el uso y permite una administración completa del sitio FTP.

![Figura 3. Cliente FTP modo gráfico FileZilla. Fuente: ¿Qué es el FTP y cómo puedo utilizarlo para](images/image-5.png)

*Figura 3. Cliente FTP modo gráfico FileZilla. Fuente: ¿Qué es el FTP y cómo puedo utilizarlo para*

transferir archivos?, 2023.

**▸ Clientes FTP integrados en navegadores web:** muchos navegadores web, como Internet Explorer o Firefox, tienen la capacidad de funcionar como clientes FTP básicos si se configuran adecuadamente. Además, estos navegadores suelen admitir complementos o extensiones que pueden convertirlos en clientes FTP más completos. Un ejemplo popular es FireFTP, una extensión de Firefox que permite a los usuarios gestionar archivos en servidores FTP directamente desde el navegador. Aunque esta opción puede ser útil, no es tan potente ni tan segura como un *software* especializado.

![Figura 4. Cliente FTP a través de un navegador. Fuente: ¿Qué es el FTP y cómo puedo utilizarlo para](images/image-6.png)

*Figura 4. Cliente FTP a través de un navegador. Fuente: ¿Qué es el FTP y cómo puedo utilizarlo para*

transferir archivos?, 2023.

**▸ Clientes FTP integrados en páginas web:** existen, también, servicios web que actúan como clientes FTP, que facilitan la conexión con servidores FTP y permiten el intercambio de archivos directamente desde una página web. Sin embargo, este método no es el más recomendable desde el punto de vista de la privacidad, ya que implica confiar en un tercero para el manejo de datos potencialmente sensibles. Es importante ser cauteloso al utilizar estos servicios, especialmente si se manejan archivos que contienen información personal o confidencial.

#### Clientes FTP en modo texto

Por otro lado, están los clientes FTP en modo texto, que, aunque no son tan visualmente atractivos ni fáciles de usar como sus contrapartes gráficas, son herramientas **extremadamente útiles.** La mayoría de los sistemas operativos ya incluyen un cliente FTP en modo texto integrado, lo que significa que no es necesario instalar *software* adicional. Este tipo de cliente se maneja directamente desde la **línea de comandos** del sistema operativo, como el CMD en Windows o la terminal en sistemas basados en Unix.

El manejo de un cliente FTP en modo texto requiere conocer una serie de **comandos** que se utilizan para realizar diversas operaciones, como conectarse al servidor FTP, subir y descargar archivos y gestionar el sitio FTP. Aunque la cantidad de comandos disponibles puede variar según el sistema operativo, en general, estos comandos se pueden agrupar en varias **categorías principales:**

**▸ Comandos de control:** estos comandos se utilizan principalmente para gestionar la conexión con el servidor FTP, como iniciar y finalizar la conexión. También, permiten configurar el modo de transferencia de datos, que puede ser binario o ASCII. Este grupo de comandos es esencial para establecer y mantener la conexión entre el cliente y el servidor.

**▸ Comandos de gestión:** son comandos que permiten la administración del sitio FTP. Con ellos, los usuarios pueden navegar a través de los directorios, borrar archivos, crear y eliminar carpetas y renombrar archivos y carpetas. Estos comandos son esenciales para organizar y mantener el contenido del servidor FTP.

**▸ Comandos de autenticación:** este conjunto de comandos está orientado a la verificación de las credenciales de los usuarios que se conectan al servidor FTP. A través de estos comandos, el sistema asegura que solo los usuarios autorizados puedan acceder y operar en el servidor FTP, aunque, como se mencionó anteriormente, en un entorno FTP tradicional esta autenticación no está cifrada.

**▸ Comandos de transferencia:** estos son los comandos que se utilizan para realizar el intercambio real de datos entre el cliente FTP y el servidor. Incluyen operaciones como subir archivos o carpetas al servidor FTP o descargarlos desde este. Son, en esencia, la base de la funcionalidad del cliente FTP.

Aunque los clientes FTP en modo texto pueden parecer menos accesibles que los clientes gráficos debido a su naturaleza basada en comandos ofrecen un **control** **total** sobre las operaciones FTP, y en muchos casos, pueden ser **más rápidos y** **eficientes** para usuarios avanzados o administradores de sistemas que están familiarizados con la línea de comandos.

En resumen, los clientes FTP, ya sean en modo gráfico o en modo texto, juegan un papel crucial en la administración de archivos en servidores FTP. Los **clientes en** **modo gráfico** son ideales para usuarios que prefieren una interfaz visual e intuitiva, facilitando el manejo y la configuración del FTP con herramientas como arrastrar y soltar. Por otro lado, los **clientes en modo texto,** aunque más rudimentarios, ofrecen un control detallado y una eficiencia que puede ser preferida por usuarios avanzados. Además, las **distintas opciones** para implementar un cliente FTP, ya sea mediante *software* específico, navegadores web o servicios basados en web, ofrecen una **flexibilidad** que permite a los usuarios elegir la solución que mejor se adapte a sus necesidades y habilidades técnicas. Con esta diversidad de opciones, el FTP es una herramienta fundamental en la gestión y transferencia de archivos a través de redes, destacándose por su versatilidad y adaptabilidad a diferentes entornos y requisitos de usuario.

Servidor FTP

Para implementar un servicio de transferencia de archivos utilizando el protocolo FTP, no solo es necesario contar con clientes FTP, sino que, también, es fundamental disponer al menos de un servidor FTP.

El concepto de servidor FTP se refiere al ***software*** **especializado** que permite que un dispositivo comparta archivos con otros equipos (clientes FTP) que están conectados a la misma red. Este *software* facilita el intercambio de datos al gestionar y controlar las solicitudes de transferencia de archivos entre los dispositivos.

Adicionalmente, el término servidor FTP puede referirse, también, al **dispositivo** **físico** que alberga el *software* de servidor FTP. Este dispositivo actúa como el punto central en el cual se almacenan los archivos que se compartirán, creando así diferentes sitios FTP que los usuarios pueden acceder información.

para subir o descargar

En otras palabras, el servidor FTP es tanto el *software* que opera el servicio de transferencia de archivos como el *hardware* que lo ejecuta y que almacena los archivos disponibles para su intercambio.

En el mercado, existe una **amplia gama de aplicaciones** que proporcionan la funcionalidad de servidor FTP y estas varían en características y requisitos. Al igual que en otros servicios tecnológicos, las opciones

disponibles pueden ser

**multiplataforma o específicas** para sistemas operativos particulares, y pueden ser de **código abierto o comerciales, gratuitas o de pago.**

Entre las **opciones destacadas** para el servicio de transferencia de archivos, se pueden mencionar las siguientes dos aplicaciones:

**▸ Gene6 FTP Server:** este es un *software* diseñado para operar en sistemas operativos de la familia Microsoft, como Windows. Gene6 FTP Server es una aplicación comercial que requiere un pago para su uso completo, aunque ofrece una versión de prueba limitada en tiempo. La gestión de este servidor FTP se realiza a través de una interfaz gráfica intuitiva, lo que facilita su configuración y administración, incluso para usuarios que no tienen una gran experiencia técnica.

**▸ VSFTPD:** este es un servidor FTP tradicionalmente utilizado en sistemas basados en Linux. VSFTPD, que significa Very Secure FTP Daemon. Es una aplicación de código abierto y gratuita, conocida por su flexibilidad y su enfoque en la seguridad. Su configuración se realiza mediante el uso del intérprete de comandos y la edición de archivos de configuración específicos, lo que permite un control detallado y personalizado sobre cómo se gestionan las transferencias de archivos.

Ambos servidores FTP tienen características que los hacen adecuados para diferentes entornos y necesidades, destacando la versatilidad y la adaptabilidad de las soluciones disponibles en el mercado para implementar un servicio de transferencia de archivos eficiente y eficaz.

## 5.4. Sitio FTP, usuarios y grupos

Sitio FTP

El término sitio FTP se refiere a la **estructura organizativa** de directorios en un servidor FTP, donde se almacenan los archivos de los usuarios. Cada usuario tiene su propio conjunto de directorios dentro del servidor, creando un espacio de almacenamiento personalizado conocido como su sitio FTP. Este diseño facilita el acceso y la gestión de los archivos, ya que cada usuario puede organizar y mantener sus propios datos sin interferir con los de otros.

En la mayoría de los casos, los sitios FTP se organizan en una estructura jerárquica similar a un árbol, con un **directorio raíz** que actúa como el punto de entrada principal. Cuando los usuarios se conectan al servidor FTP, acceden a este directorio raíz, desde el cual pueden navegar por los diferentes directorios y archivos que les pertenecen. Esta estructura facilita la administración de los archivos y asegura que los usuarios solo puedan acceder a sus propios datos, protegiendo la integridad de la información en el servidor.

Usuarios del servidor FTP

Los usuarios del servidor FTP son las personas que tienen **permiso** para acceder y utilizar el servidor. Para ingresar, los usuarios generalmente necesitan un nombre de usuario y una contraseña. Estas **credenciales** permiten al servidor autenticar a los usuarios y garantizar que solo aquellos autorizados puedan acceder a sus respectivos sitios FTP. Existen **dos tipos** principales de usuarios en un servidor FTP: usuarios autenticados y usuarios genéricos.

Los **usuarios autenticados** son aquellos que tienen una cuenta específica en el servidor. Estos usuarios poseen un nombre de usuario único y una contraseña asociada, lo que garantiza que solo ellos puedan acceder a su sitio FTP. Los usuarios autenticados se dividen en dos **subcategorías:**

**▸ Usuarios locales:** son cuentas creadas en el propio dispositivo que ejecuta el servidor FTP. Estos usuarios utilizan las cuentas existentes en el sistema operativo del servidor y los permisos se gestionan a nivel del sistema operativo.

**▸ Usuarios virtuales:** estos usuarios se crean exclusivamente dentro de la aplicación del servidor FTP. No tienen cuentas locales en el dispositivo, sino que se gestionan a través de una base de datos interna del servidor FTP. Esto permite una mayor flexibilidad en la administración de usuarios sin depender de las cuentas del sistema operativo.

L o s **usuarios genéricos,** también conocidos como usuarios anónimos, no están asociados a personas específicas. Este tipo de usuarios puede ser accedido por cualquier persona y no requiere autenticación personalizada. Generalmente, utilizan un nombre de usuario común, como «anonymous», «guest» o «ftp». En algunos casos, se puede usar una dirección de correo electrónico (a veces ficticia) como contraseña, aunque en muchos servidores el acceso anónimo no requiere una contraseña.

Los usuarios genéricos son útiles para hacer accesibles partes públicas del servidor FTP, permitiendo que cualquier persona pueda acceder a esos recursos sin necesidad de gestionar credenciales individuales para cada usuario.

Grupos de usuarios en el servidor FTP

El concepto de grupo de usuarios está estrechamente relacionado con la administración de los usuarios en el servidor FTP. Un grupo de usuarios es una **colección de cuentas** que comparten ciertas características o permisos. Estos grupos pueden tener **configuraciones comunes,** como cuotas de almacenamiento, ancho de banda y permisos de acceso, lo que simplifica la gestión del servidor.

Crear grupos de usuarios permite a los administradores del servidor FTP manejar grandes cantidades de usuarios de manera más eficiente.

En lugar de configurar cada cuenta individualmente, los administradores pueden **crear grupos con características predefinidas** y luego agregar usuarios a estos grupos. Los usuarios heredan las características pertenecen, lo que facilita la administración y configuración.

y permisos del grupo al que garantiza la coherencia en la

En resumen, un sitio FTP proporciona una **estructura organizada** para el almacenamiento de archivos en un servidor FTP, mientras que los usuarios del servidor FTP y los grupos de usuarios ayudan capacidades del servidor.

a gestionar el acceso y las

Los usuarios autenticados tienen credenciales específicas, mientras que los usuarios genéricos permiten el acceso anónimo. La implementación de **grupos de usuarios** simplifica la administración al aplicar configuraciones comunes a varios usuarios simultáneamente. Estos elementos son esenciales para mantener un entorno de transferencia de archivos eficiente y seguro.

## 5.5. Permisos

El servidor FTP, al ser un punto de acceso central en una red donde usuarios de diversos dispositivos se conectan continuamente, requiere una **configuración de** **seguridad meticulosa** para prevenir usos indebidos o maliciosos. Los riesgos incluyen accesos no autorizados a otros equipos de la red, robo de datos o la eliminación de información crítica. Por lo tanto, una de las primeras medidas que tomar es **configurar adecuadamente los permisos** para cada usuario del servidor FTP. Estos permisos determinan las acciones que un usuario puede o no realizar dentro del servidor.

¿Qué son los permisos de usuario?

Los permisos de usuario en un servidor FTP **definen las acciones** que cada usuario puede llevar a cabo dentro del servidor. En función de la aplicación utilizada para configurar el servidor FTP, los permisos pueden variar, pero generalmente incluyen una serie de **configuraciones clave:**

**▸ Acceso al servidor:** este permiso establece quién puede o no conectarse al servidor FTP. Se puede restringir el acceso de ciertos usuarios para proteger el servidor de accesos no autorizados. Por ejemplo, es posible permitir el acceso solo a usuarios específicos que tengan credenciales válidas, garantizando que solo las personas designadas puedan interactuar con el servidor.

**▸ Acceso a directorios:** dentro del servidor FTP, los permisos pueden regular qué directorios son accesibles para los usuarios. Es común configurar el servidor para que los usuarios solo puedan acceder a directorios específicos, limitando su navegación y evitando que puedan moverse fuera de su área designada. Esta configuración es útil para mantener la organización y la seguridad, impidiendo que los usuarios vean o manipulen archivos que no deberían.

**▸ Modificación y eliminación de archivos:** los usuarios pueden necesitar la capacidad de modificar o eliminar archivos dentro del servidor. Esta opción debe ser configurada cuidadosamente. Permitir la modificación o eliminación de archivos puede ser útil para usuarios que necesitan actualizar o gestionar el contenido de manera activa. Sin embargo, si el objetivo del servidor es compartir archivos de forma segura, es posible que desee restringir estas capacidades para evitar alteraciones no autorizadas o la eliminación accidental de datos importantes.

**▸ Creación y eliminación de directorios:** otro permiso clave es la capacidad de crear o eliminar directorios dentro del servidor FTP. Permitir a los usuarios gestionar directorios puede ser beneficioso para aquellos que necesitan organizar el contenido de manera estructurada. Sin embargo, también es crucial controlar quién puede realizar estas acciones para evitar la creación de estructuras desordenadas o la eliminación accidental de directorios importantes.

**▸ Subida y descarga de archivos:** los permisos también pueden regular si los usuarios tienen la capacidad de subir (es decir, cargar) o descargar archivos del servidor FTP. Dependiendo de las necesidades del servidor, es posible permitir solo la subida de archivos, la descarga o ambas acciones. Por ejemplo, en un servidor FTP diseñado para compartir información, podríamos permitir a los usuarios subir archivos, pero restringirles la descarga para preservar el contenido compartido.

En resumen, la **correcta configuración de permisos** en un servidor FTP es fundamental para asegurar el **control adecuado del acceso** y la **gestión de los** **archivos** dentro del servidor. Ajustar estos permisos de manera precisa ayuda a proteger el servidor de accesos no deseados y a garantizar que solo las personas autorizadas puedan realizar acciones específicas. Implementar una estrategia de permisos bien definida es esencial para mantener la integridad, seguridad y funcionalidad del servidor FTP.

## 5.6. Ancho de banda y cuotas

Además de los permisos, otro aspecto crucial en la administración de un servidor FTP es la gestión del ancho de banda y las

cuotas. Estos dos factores son

fundamentales para garantizar un rendimiento óptimo y una distribución eficiente de los recursos del servidor. A continuación, se explica en detalle cada uno de estos conceptos y cómo su configuración puede afectar el funcionamiento del servidor

FTP.

Ancho de banda

El ancho de banda se refiere a la **cantidad de datos** que se pueden **transferir** entre

el cliente FTP y el servidor FTP en un periodo de tiempo determinado. Esta métrica es esencial porque **determina la velocidad y la eficiencia** de las transferencias de archivos. El ancho de banda disponible está limitado por la capacidad de la conexión a Internet del servidor y la tecnología empleada, ya sea WiFi, fibra óptica, ADSL u otra.

Como administradores del servidor FTP, es nuestra responsabilidad gestionar de manera eficaz el ancho de banda asignado a

cada usuario para asegurar un

rendimiento adecuado del servicio. Existen varias **estrategias para optimizar** el uso del ancho de banda:

**▸ Configuración de la tasa de transferencia:** una de las opciones más importantes es ajustar la tasa de transferencia para cada usuario. Esto se refiere a la velocidad máxima a la que un usuario puede subir o descargar archivos. La tasa de transferencia puede ser diferente para la subida y la descarga, permitiendo así una personalización más precisa. Por ejemplo, un administrador puede establecer una mayor velocidad de descarga para los usuarios que han pagado por un servicio prémium, mientras que los usuarios gratuitos pueden tener velocidades más bajas.

Esta segmentación ayuda a equilibrar el rendimiento del servidor y a incentivar la

Servicios en Red e Internet 30 Tema 5. Material de estudio suscripción a planes pagos.

**▸ Número máximo de conexiones:** dado que el ancho de banda debe ser compartido entre todos los usuarios conectados al servidor FTP, es aconsejable limitar el número máximo de conexiones simultáneas permitidas. Esto asegura que el ancho de banda se distribuya de manera equitativa y evita que unos pocos usuarios consuman de manera desproporcionada los recursos del servidor. Limitar el número de conexiones por usuario también ayuda a prevenir la congestión y mejora la experiencia general para todos los usuarios.

**▸ Tiempo máximo de conexión:** además de limitar el número de conexiones, es útil establecer un tiempo máximo de conexión para los usuarios. Esto evita que algunos usuarios monopolicen el servidor FTP durante períodos prolongados, lo que podría afectar negativamente a otros usuarios. Esta medida es especialmente importante en servidores FTP con alta demanda o cuando se ofrece un servicio a un gran número de usuarios.

Cuotas

Las cuotas se refieren al **espacio máximo de almacenamiento** asignado a cada usuario en el servidor FTP. Cada usuario tiene una cuota específica que **limita la** **cantidad de datos** que puede almacenar en el servidor. La configuración de cuotas es crucial para evitar que un solo usuario consuma todo el espacio disponible, lo que podría impedir que otros usuarios almacenen sus propios archivos.

Establecer cuotas ayuda a gestionar eficientemente el almacenamiento del servidor y a garantizar que todos los usuarios tengan acceso a un espacio adecuado. Si no se establecen límites, existe el riesgo de que un usuario pueda llenar el disco duro del servidor, lo que dejaría a los demás usuarios sin capacidad de almacenamiento. Por lo tanto, fijar cuotas adecuadas es una medida preventiva importante.

Muchas aplicaciones de servidor FTP modernas permiten configurar cuotas directamente desde su **interfaz de administración.** Sin embargo, en algunos casos,

Servicios en Red e Internet 31 Tema 5. Material de estudio la configuración de cuotas debe realizarse a nivel del **sistema operativo** o mediante **herramientas complementarias.** Estas herramientas adicionales pueden ofrecer opciones avanzadas para gestionar el espacio en disco y asignar cuotas de manera más flexible.

Además de los aspectos técnicos de la gestión del ancho de banda y las cuotas, es importante considerar cómo estos factores afectan la **experiencia del usuario.** Un buen equilibrio en la configuración puede mejorar la satisfacción de los usuarios y garantizar un servicio más confiable. Por ejemplo, ofrecer diferentes niveles de servicio basados en la tasa de transferencia y las cuotas puede permitir a los administradores atraer a una variedad de usuarios, desde aquellos que requieren un servicio básico hasta aquellos que necesitan capacidades avanzadas.

En conclusión, una gestión adecuada del ancho de banda y las cuotas es esencial para el funcionamiento eficiente de un servidor FTP. Ajustar estos parámetros según las necesidades específicas del servidor y de los usuarios ayuda a mantener un servicio de alta calidad, a prevenir problemas de rendimiento y a asegurar una experiencia satisfactoria para todos los usuarios. Implementar estrategias de configuración efectivas en estos aspectos contribuirá a la estabilidad y al éxito del servidor FTP en cualquier entorno de red.

## 5.7. Tipos de transmisión de datos

La transmisión de datos entre un cliente FTP y un servidor FTP puede variar según el tipo de archivos que se transfieren. Existen dos métodos principales de transmisión de datos: binario y ASCII (texto), cada uno adecuado para diferentes tipos de archivos.

Transmisión binaria

La transmisión binaria es ideal para la mayoría de los archivos. Este método es el adecuado para transferir archivos en formatos como imágenes de sistemas de almacenamiento (.iso, .nrg), archivos comprimidos y empaquetados (.zip, .rar), documentos de aplicación (.doc, .xls), ejecutables (.exe, .com) y archivos de vídeo (.avi, .mpeg). En la transmisión binaria, los datos se transfieren **bit a bit,** lo que asegura que el archivo se mantenga intacto durante la transferencia. Sin embargo, este método puede ser lento para archivos grandes debido a la naturaleza bit a bit de la transferencia.

Transmisión ASCII o texto

La transmisión ASCII, o de texto, se utiliza para archivos de texto puro, como documentos .txt, archivos HTML (.html) y XML (.xml). En este método, los datos se transfieren **byte a byte,** es decir, en bloques de ocho bits.

Este tipo de transmisión es más rápida que la binaria para archivos de texto porque maneja la información en unidades más grandes. Sin embargo, es crucial usar la transmisión ASCII solo para archivos de texto puro, ya que un uso incorrecto puede resultar en la alteración de corrompidos. archivos no textuales, haciéndolos ilegibles o

Muchos clientes y servidores FTP modernos pueden detectar automáticamente el formato del archivo y elegir el tipo de transmisión adecuado. Sin embargo, si esta detección automática no está disponible, el usuario debe seleccionar el tipo de transmisión correcto para evitar problemas en la transferencia de datos.

## 5.8. Modos de conexión

Una parte crucial en la configuración de un servidor FTP es el modo de conexión utilizado entre los clientes FTP y el servidor. Este aspecto determina cómo se **establece la conexión** para la transferencia de datos y puede afectar la seguridad y el rendimiento del servicio. Existen **dos modos principales** de conexión en FTP, que se diferencian en quién inicia la conexión de datos: el cliente o el servidor. Estos modos son el modo activo y el modo pasivo.

Modo activo (PORT)

El modo activo, también conocido como modo PORT, es el **modo de conexión** **predeterminado** en la mayoría de los servidores FTP. En este modo, el servidor FTP es responsable de iniciar la conexión de datos después de recibir una solicitud del cliente FTP. Por defecto, el servidor utiliza el **puerto 21** para la conexión de control y e l **puerto 20** para la conexión de datos. Cuando el cliente FTP solicita una transferencia de datos, el servidor abre una conexión de datos hacia un puerto aleatorio en el cliente, que siempre será un puerto superior al 1024.

Este enfoque puede presentar algunos **problemas,** especialmente cuando los clientes FTP están protegidos por un *firewall.* Dado que el servidor intenta establecer una conexión hacia un puerto alto y aleatorio en el cliente, el *firewall* del cliente debe estar configurado para aceptar conexiones entrantes en estos puertos no estándar. Esta configuración puede ser complicada y requiere que los usuarios del cliente FTP tengan **conocimientos técnicos suficientes** para ajustar adecuadamente las reglas del *firewall* sin comprometer la seguridad del sistema. La gestión de estos puertos aleatorios puede ser desafiante y propensa a errores si no se realiza con cuidado.

![Comparación de modos de conexión:](images/image-7.png)

Tabla 1. Ventajas y desventajas de los modos de conexión. Fuente: elaboración propia.

Esta tabla muestra de manera resumida las diferencias clave entre los modos activo y pasivo para ayudar a decidir cuál es el más adecuado, según las circunstancias específicas del entorno de red y los requisitos de seguridad.

![Figura 5. Modo Activo y Pasivo FTP. Fuente: ¿Qué es el FTP y cómo puedo utilizarlo para transferir](images/image-8.png)

*Figura 5. Modo Activo y Pasivo FTP. Fuente: ¿Qué es el FTP y cómo puedo utilizarlo para transferir*

archivos?, 2023.

## 5.9. Referencias bibliográficas

Conexión FTP: qué es, qué necesitas y programas populares. (s. f.). *Cloud Center* *A n d a l u c i a .* <https://www.cloudcenterandalucia.es/blog/conexion-ftp-que-es-quenecesitas-y-programas-populares/>

¿Qué es el FTP y cómo puedo utilizarlo para transferir archivos? (2023, enero 27). Kinsta. [https://kinsta.com/es/base-de-conocimiento/que-es-el-ftp/](https://kinsta.com/es/base-de-conocimiento/que-es-el-ftp/)

# Fernández, Y. (2024, abril 18). FTP: qué es y cómo funciona. Kataka.

# [https://www.xataka.com/basics/ftp-que-como-funciona](https://www.xataka.com/basics/ftp-que-como-funciona)

## FTP: qué es y cómo funciona (Fernández, 2024)

Este recurso es una forma sencilla de explicarte qué es el servicio FTP y cómo implementarlo, utilizando un cliente como Filezilla Client y un servidor como Filecilla Server en un entorno de Microsoft.

# 89yXgqGM

## Qué es un servidor FTP y cómo usarlo en nuestro

## hosting

Hurtado, D. (2021, junio 30). *Qué es un Servidor FTP y Cómo Usarlo en Nuestro* *Hosting - Dostin Hurtado* [Vídeo]. YouTube. <https://www.youtube.com/watch?v=d--> ¿Sabes la relación que existe entre el servicio web y el servicio ftp? ¿y cómo puedes configurar el servicio ftp para conectarte con tu *hosting?* En este vídeo vas a aprender a utilizar clientes de ftp conectándose al servidor ftp de tu *hosting.*

![image-9](images/image-9.png)

Accede al vídeo: [https://www.youtube.com/embed/d--89yXgqGM](https://www.youtube.com/embed/d--89yXgqGM)

¿Qué es el FTP y cómo puedo utilizarlo para transferir archivos?

¿Qué es el FTP y Cómo Puedo Utilizarlo para Transferir Archivos? (2023 febrero7). * insta.* [https://kinsta.com/es/base-de-conocimiento/que-es-el-ftp/](https://kinsta.com/es/base-de-conocimiento/que-es-el-ftp/)

Este recurso, además de explicar lo que significa este servicio y cómo funciona, hace una comparativa con otros protocolos de la capa de aplicación y muestra ejemplos de uso más habituales para dar un sentido al protocolo FTP.

# [https://www.dongee.com/tutoriales/que-es-ftp/](https://www.dongee.com/tutoriales/que-es-ftp/)

## Qué es un servidor FTP y para qué se utiliza

Jesús. (2021, noviembre 22). Qué es un servidor FTP y para qué se utiliza. *Dongee.* Dedica siete minutos para revisar este documento donde podrás ver diferentes usos que se pueden dar a un servidor FTP. Además, tienes la posibilidad de, en vez de leer, poder escuchar el contenido, por lo que puedes aprender haciendo otras cosas simultáneamente.

# 1). Kinsta. [https://kinsta.com/es/blog/mejores-clientes-ftp](https://kinsta.com/es/blog/mejores-clientes-ftp)

## 10 mejores clientes FTP para usuarios de WordPress (Mac y Windows)

10 mejores clientes FTP para usuarios de WordPress (Mac y Windows). (2022, julio ¿Estas buscado trabajar con un cliente FPT y no sabes cuál utilizar? Aquí te presento una relación de diferentes clientes FTP, que indican sus características, ventajas y desventajas y valora cuál ofrece mejores prestaciones.

# [https://blog.ahierro.es/ftp-activo-vs-ftp-pasivo/](https://blog.ahierro.es/ftp-activo-vs-ftp-pasivo/)

## FTP activo vs. FTP pasivo

Hernández, A. H. (2019, noviembre 19). FTP activo vs FTP pasivo. *Blog aHierro.* ¿Te quedaron dudas sobre cuándo usar el modo activo o pasivo en FTP? Aquí te explican lo que implica cada uno de los modos y diferentes situaciones donde poder usar uno u otro método.

# [https://www.youtube.com/watch?v=2fdNydEc7hw](https://www.youtube.com/watch?v=2fdNydEc7hw)

## Qué es FTP y como utilizarlo

Fierro, E. (2020, noviembre 9). *QUÉ ES FTP y como utilizarlo - ¿FTP, Hosting,* *Dominio, Proveedor y Filezilla? - Eduardo Fierro Pro* [Vídeo]. YouTube. Este interesante vídeo te explica qué es un servicio FTP y cómo lo puedes utilizar con los diferentes *hostings* donde tengas subido tu sitio web.

![image-10](images/image-10.png)

Accede al vídeo: [https://www.youtube.com/embed/2fdNydEc7hw](https://www.youtube.com/embed/2fdNydEc7hw)

# - Comandos FTP - Fernando Terroso [Vídeo]. YouTube.

# [https://www.youtube.com/watch?v=M61W3tabt0Q](https://www.youtube.com/watch?v=M61W3tabt0Q)

## Administración de sistemas. Comandos FTP

UCAM Universidad Católica de Murcia. (2018, mayo 23). *Administración de sistemas* Te presento una lista completa de todos los comandos que puedes utilizar en una conexión FTP. También tienes las diferentes respuestas que puede emitir el servidor y cuándo suceden situaciones anómalas.

![image-11](images/image-11.png)

Accede al vídeo: [https://www.youtube.com/embed/M61W3tabt0Q](https://www.youtube.com/embed/M61W3tabt0Q)

# v=oP-xsH4MCws

## Administración de sistemas. FTP Modos

UCAM Universidad Católica de Murcia. (2018, mayo 23). *Administración de sistemas* *- FTP Modos - Fernando Terroso* [Vídeo]. YouTube. <https://www.youtube.com/watch?> ¿Te han quedado dudas respecto al modo activo o modo pasivo de un servicio FTP? Aquí tienes la explicación perfectamente documentada, incluso extendido para que entiendas el proceso.

![image-12](images/image-12.png)

Accede al vídeo: [https://www.youtube.com/embed/oP-xsH4MCws](https://www.youtube.com/embed/oP-xsH4MCws)

## Entrenamiento 1. Cuestiones por desarrollar sobre

## el servicio FTP

**▸ Planteamiento del ejercicio**

Deberás responder de una manera precisa las siguientes cuestiones: **▸** ¿Qué es el servicio de transferencia de ficheros? ¿Qué características tiene? **▸** ¿En qué protocolo se basa este servicio? **▸** ¿Bajo qué modelo funciona este servicio? Explica cómo funciona este modelo para este servicio. ¿Cuántas conexiones hay? ¿Por qué puertos?

**▸** ¿En qué sistemas operativos funciona?

**▸** ¿Qué es un servidor FTP?

**▸** ¿Y un cliente FTP? ¿Funciona en modo gráfico o en modo texto?

**▸** ¿Cómo instalamos un servidor FTP en Windows Server 2008? ¿Y en Ubuntu, qué

aplicación debemos instalar? **▸** ¿Qué configuración de red debemos establecer al servidor? ¿Y al cliente? **▸** ¿Qué archivos se deben modificar en el servidor Ubuntu para configurarlo? ¿Y en el cliente Lubuntu?

**▸** Di cuatro ejemplos de servidores FTP conocidos.

**▸** ¿Qué es un sitio FTP? ¿Qué estructura tiene?

**▸** ¿Qué son los usuarios del servidor? ¿Qué dos tipos de usuarios hay? Explica en qué

se diferencian. **▸** ¿Qué diferencia hay entre un usuario autenticado local del servidor y uno virtual?

**▸** ¿Qué son los grupos? Explica en qué consisten. **▸** ¿Qué son los permisos? ¿Qué permisos deberían tener los usuarios genéricos para proteger al servidor?

**▸** ¿Qué es el ancho de banda? ¿De qué depende?

**▸** ¿Qué son las cuotas?

**▸** ¿Qué modos de conexión hay? Explica cada uno de ellos.

**▸** ¿Qué tipos de transmisión de datos hay? Explica cada uno de ellos.

**▸ Desarrollo paso a paso**

Podrás apoyarte en las búsquedas por Internet o consultar libros para responder correctamente estas cuestiones.

**▸ Solución**

#### ¿Qué es el servicio de transferencia de ficheros? ¿Qué características tiene?

El servicio de transferencia de ficheros, comúnmente conocido como FTP (File Transfer Protocol), es un protocolo de red estándar que se utiliza para transferir archivos entre un cliente y un servidor en una red TCP/IP, como Internet. Este servicio permite a los usuarios subir *(upload)* archivos desde su máquina local al servidor o descargar *(download)* archivos desde el servidor a su máquina local.

Características principales del servicio de transferencia de ficheros:

**▸** Intercambio de archivos: FTP permite tanto la carga como la descarga de archivos, lo que facilita la distribución de contenido.

**▸** Autenticación: aunque FTP puede funcionar en modo anónimo, es común que requiera autenticación con un nombre de usuario y contraseña.

**▸** Transferencia de archivos grandes: FTP es adecuado para la transferencia de archivos grandes, sin limitaciones específicas en el tamaño de archivo.

**▸** Compatibilidad con diversos sistemas de archivos: FTP puede transferir archivos entre diferentes sistemas operativos y tipos de archivos.

**▸** Modos de transferencia: FTP ofrece modos de transferencia activa y pasiva, que determinan cómo se establecen las conexiones entre el cliente y el servidor.

**▸** Control y seguridad: aunque FTP por defecto no es seguro (la información se envía sin cifrado), existen variantes como FTPS y SFTP que ofrecen opciones de seguridad mediante cifrado.

#### ¿En qué protocolo se basa este servicio?

El servicio de transferencia de ficheros se basa en el protocolo de transferencia de archivos (FTP). FTP es parte de la familia de protocolos TCP/IP y opera sobre una arquitectura cliente-servidor. Utiliza principalmente dos puertos: el puerto 21 para el control (envío de comandos y respuestas) y el puerto 20 para la transferencia de datos (en el modo activo).

#### ¿Bajo qué modelo funciona este servicio? Explica cómo funciona este modelo

#### para este servicio. ¿Cuántas conexiones hay? ¿Por qué puertos?

FTP funciona bajo un modelo cliente-servidor, donde el cliente FTP solicita servicios de transferencia de archivos al servidor FTP.

Funcionamiento del modelo:

**▸** Cliente-servidor: en este modelo, el cliente inicia la comunicación enviando comandos al servidor, que responde y ejecuta las acciones solicitadas (como subir o descargar un archivo).

**▸** Conexiones: FTP utiliza dos conexiones simultáneas:

- Conexión de control (puerto 21): utiliza el puerto 21 en el servidor para enviar comandos y recibir respuestas. Esta conexión se mantiene abierta durante toda la sesión.

- Conexión de datos (puerto 20 o puerto dinámico): se utiliza para transferir los datos propiamente dichos. En modo activo, el servidor abre esta conexión desde el puerto 20 hacia un puerto temporal en el cliente. En modo pasivo, el cliente abre una conexión hacia un puerto dinámico en el servidor.

#### ¿En qué sistemas operativos funciona?

FTP es un protocolo versátil y está disponible en prácticamente todos los sistemas operativos que soportan redes TCP/IP. Algunos ejemplos incluyen:

**▸** Windows (todas las versiones, incluyendo servidores y clientes).

**▸** Linux/Unix (cualquier distribución, como Ubuntu, Debian, CentOS, etc.).

**▸** macOS (incluyendo versiones de cliente y servidor).

**▸** Android e iOS (a través de aplicaciones de terceros).

**▸** Dispositivos de red como rúteres y NAS (Network Attached Storage), también suelen soportar FTP.

#### ¿Qué es un servidor FTP?

Un servidor FTP es un *software* que permite a un sistema actuar como servidor para ofrecer servicios de transferencia de archivos a clientes FTP. Este *software* escucha en el puerto 21 para conexiones entrantes y gestiona las solicitudes de los clientes para cargar, descargar, renombrar, mover o eliminar archivos en el sistema de archivos del servidor.

El servidor FTP se puede configurar para permitir accesos públicos (anónimos) o restringidos (mediante autenticación). Además, puede gestionar permisos, cuotas y control de acceso para usuarios o grupos específicos.

#### ¿Y un cliente FTP? ¿Funciona en modo gráfico o en modo texto?

Un cliente FTP es una aplicación que permite a un usuario conectarse a un servidor FTP para interactuar con sus archivos. Los clientes FTP pueden funcionar en:

**▸** Modo gráfico (GUI): ofrece una interfaz visual donde los usuarios pueden ver los archivos en el servidor y en su computadora local, arrastrar y soltar archivos para transferirlos, etc. Ejemplos incluyen FileZilla, Cyberduck y WinSCP.

**▸** Modo texto (CLI): los clientes en modo texto se ejecutan en una terminal y permiten a los usuarios introducir comandos manualmente para interactuar con el servidor FTP. Como ejemplos se incluyen el comando ftp nativo en Linux y macOS.

**¿Cómo instalamos un servidor FTP en Windows Server 2008? ¿Y en Ubuntu,**

#### qué aplicación debemos instalar?

Instalación en Windows Server 2008:

**▸** Abrir el Server Manager y seleccionar «Add Roles».

**▸** Seleccionar el rol «Web Server (IIS)» y avanzar hasta las opciones de instalación. **▸** En las opciones de roles del servidor, seleccionar «FTP Server» y sus dependencias. **▸** Continuar con la instalación y luego configurar el servicio FTP desde la consola de administración de IIS. Instalación en Ubuntu Para instalar un servidor FTP en Ubuntu, comúnmente se usa vsftpd (Very Secure FTP Daemon). Los pasos son: **▸** Abrir una terminal y ejecutar:

![image-13](images/image-13.png)

**▸** Una vez instalado, el servidor FTP puede ser configurado editando el archivo

/etc/vsftpd.conf .

#### ¿Qué configuración de red debemos establecer al servidor? ¿Y al cliente?

Configuración en el servidor: **▸** Dirección IP fija: es recomendable que el servidor tenga una IP estática para asegurar que los clientes puedan conectarse de manera consistente. **▸** Configuración del *firewall:* debe permitir el tráfico en los puertos 21 (para control) y 20 (para datos) o cualquier puerto adicional configurado para FTP pasivo. **▸** NAT y puertos abiertos: si el servidor está detrás de un rúter o *firewall,* es necesario configurar NAT para redirigir el tráfico externo hacia el servidor.

Configuración en el cliente:

**▸** Conexión a la red: asegurarse de que el cliente tenga acceso a la red y pueda resolver la IP o nombre del servidor.

**▸** Puertos: no es necesario abrir puertos en el cliente, pero el cliente debe permitir tráfico saliente a los puertos 21 y el rango de puertos utilizado para conexiones de datos.

**▸** Modo de transferencia: configurar el cliente para usar el modo activo o pasivo según la configuración del servidor y la red.

#### ¿Qué archivos se deben modificar en el servidor Ubuntu para configurarlo? ¿Y

#### en el cliente Lubuntu?

En el servidor Ubuntu: El archivo principal para configurar vsftpd es /etc/vsftpd.conf . Aquí se pueden modificar varias opciones como:

**▸** Permitir conexiones anónimas: anonymous_enable=YES/NO.

**▸** Habilitar el modo pasivo: configuración de pasv_min_port y pasv_max_port .

**▸** Control de usuarios: opciones como local_enable=YES , write_enable=YES y configuraciones de chroot para usuarios.

**▸** Tras modificar el archivo, es necesario reiniciar el servicio. En el cliente Lubuntu: Generalmente, no es necesario modificar archivos de configuración para un cliente FTP en Lubuntu, ya que los clientes FTP como ftp, lftp o FileZilla tienen interfaces y opciones que se configuran al momento de ejecutar. Sin embargo, en caso de usar lftp, el archivo de configuración puede ser /etc/lftp.conf o ~/.lftp/rc .

#### Da cuatro ejemplos de servidores FTP conocidos

**▸** FileZilla Server: popular por su facilidad de uso y configuración, compatible con Windows.

**▸** vsftpd: conocido por su seguridad, ampliamente utilizado en sistemas Linux.

**▸** ProFTPD: flexible y altamente configurable, también para Linux/Unix.

**▸** Pure-FTPd: seguro y fácil de usar, con un enfoque en la simplicidad y rendimiento, utilizado en Linux/Unix.

#### ¿Qué es un sitio FTP? ¿Qué estructura tiene?

Un sitio FTP es una instancia de un servidor FTP accesible a través de una dirección IP o un nombre de dominio. Representa un directorio raíz en el servidor donde los archivos y carpetas están organizados y disponibles para ser transferidos. Estructura:

**▸** Raíz del sitio: el directorio principal que contiene todos los archivos y subdirectorios.

**▸** Subdirectorios: carpetas organizadas dentro de la raíz para estructurar los datos.

**▸** Archivos: los archivos que se almacenan y transfieren desde o hacia el sitio FTP.

**▸** Permisos de acceso: controlan quién puede ver o modificar los archivos y directorios. **¿Qué son los usuarios del servidor? ¿Qué dos tipos de usuarios hay? Explica** **en qué se diferencian.** Los usuarios del servidor FTP son las cuentas que tienen permiso para acceder al servidor y realizar operaciones de transferencia de archivos.

Tipos de usuarios:

**▸** Usuarios autenticados: cuentas que requieren un nombre de usuario y contraseña para acceder al servidor FTP. Tienen permisos específicos según la configuración del administrador.

**▸** Usuarios anónimos: permiten acceso sin autenticación, generalmente con permisos limitados a solo lectura.

La principal diferencia es que los usuarios autenticados tienen un nivel de acceso controlado y pueden tener permisos de escritura, mientras que los usuarios anónimos suelen estar restringidos a ciertas áreas y funciones.

#### ¿Qué diferencia hay entre un usuario autenticado local del servidor y uno

#### virtual?

**▸** Usuario autenticado local: es una cuenta que existe en el sistema operativo del servidor, con un perfil de usuario real. El acceso y los permisos están directamente vinculados al sistema de archivos del servidor.

**▸** Usuario virtual: es una cuenta que no tiene un perfil real en el sistema operativo del servidor. Su acceso es gestionado por el *software* del servidor FTP y se usa para proporcionar acceso FTP sin crear usuarios en el sistema operativo.

**¿Qué son los grupos? Explica en qué consisten.**

En un servidor FTP, los grupos son conjuntos de usuarios que comparten los mismos permisos y restricciones. Los grupos facilitan la administración de permisos porque permiten asignar políticas de acceso a múltiples usuarios de una sola vez.

Por ejemplo, un grupo de lectores puede tener permisos solo para leer archivos, mientras que un grupo de editores puede tener permisos para leer y escribir.

#### ¿Qué son los permisos? ¿Qué permisos deberían tener los usuarios genéricos

#### para proteger al servidor?

Los permisos en un servidor FTP controlan lo que un usuario puede o no hacer dentro del sistema de archivos del servidor. Los permisos comunes incluyen:

**▸** Lectura: permitir ver y descargar archivos.

**▸** Escritura: permitir crear, modificar o eliminar archivos.

**▸** Ejecución: permitir ejecutar archivos (en casos específicos como *scripts).* Para proteger el servidor, los usuarios genéricos deberían tener:

**▸** Permisos mínimos necesarios: solo acceso de lectura si no se requiere modificar archivos.

**▸** Prohibir acceso de escritura: especialmente para usuarios anónimos.

**▸** Control de acceso granular: asignar permisos específicos por directorio o grupo de usuarios.

#### ¿Qué es el ancho de banda? ¿De qué depende?

El ancho de banda es la cantidad de datos que se puede transferir en una red durante un período de tiempo. Se mide, generalmente, en bits por segundo (bps). En un contexto FTP, el ancho de banda afecta la velocidad con la que se pueden cargar o descargar archivos. Depende de:

**▸** Capacidad de la red: la infraestructura física de la red y sus limitaciones.

**▸** Configuración del servidor y cliente: límites impuestos por *software* o configuraciones de red.

**▸**

**▸** Congestión de red: cuánto tráfico hay en la red en un momento dado.

**▸** Proveedores de servicios de Internet (ISP): las políticas del ISP y la calidad del servicio.

#### ¿Qué son las cuotas?

Las cuotas en un servidor FTP son límites impuestos sobre la cantidad de datos que un usuario o grupo de usuarios puede almacenar o transferir. Pueden aplicarse de diversas formas:

**▸** Cuotas de espacio en disco: límite en la cantidad total de datos que un usuario puede tener en el servidor.

**▸** Cuotas de transferencia: límite en la cantidad de datos que un usuario puede transferir en un período de tiempo.

**¿Qué modos de conexión? Explica cada uno de ellos.**

En FTP, existen dos modos de conexión principales:

**▸** Modo activo: el cliente abre un puerto y espera que el servidor se conecte a él desde el puerto 20 para transferir datos. El puerto de control sigue siendo 21. Este modo puede ser problemático detrás de *firewalls* o NAT.

**▸** Modo pasivo: el servidor abre un puerto dinámico para la transferencia de datos, y el cliente se conecta a este puerto. Este modo es más amigable con *firewalls* y NAT, ya que todas las conexiones son iniciadas por el cliente.

**¿Qué tipos de transmisión de datos hay? Explica cada uno de ellos.**

FTP soporta principalmente dos tipos de transmisión de datos:

**▸** Modo ASCII: transmite archivos como texto plano. Es adecuado para archivos de texto, donde las diferencias de codificación de fin de línea entre sistemas operativos (Windows, Unix) se manejan automáticamente.

**▸** Modo binario: transmite los archivos exactamente como son, bit por bit. Es necesario para archivos que no son de texto, como imágenes, vídeos o ejecutables, para evitar la corrupción de datos.

## Entrenamiento 2. Clientes FTP

**▸ Planteamiento del ejercicio**

#### Clientes FTP

**▸** Apartado 1. Se desea utilizar el cliente Ubuntu como Cliente FTP para que sea capaz de conectarse a diferentes servidores FTP y poder transferir archivos. Para ello se va a utilizar un cliente FTP en modo gráfico:

- Instalar la aplicación Filezilla Client en el cliente Ubuntu.

- Comprobar que la aplicación está instalada correctamente realizando una conexión al servidor FTP nic.funet.fi utilizando el usuario ftp sin *password.*

**▸** Apartado 2. Se desea utilizar el cliente Ubuntu como Cliente FTP para que sea capaz de conectarse a diferentes servidores FTP y poder transferir archivos. Para ello se va a utilizar un cliente FTP en modo texto:

- Verificar si el cliente Ubuntu posee un cliente FTP en modo texto instalado por defecto.

- Comprobar el correcto funcionamiento de la aplicación realizando una conexión al servidor FTP sunsite.unc.edu utilizando el usuario ftp sin *password.*

Realiza la misma operación con un cliente FTP en modo texto, en un entorno Windows.

**▸ Desarrollo paso a paso**

#### Clientes FTP

**▸** Apartado 1. Cliente FTP en modo gráfico:

- Instalar la aplicación Filezilla Client en Ubuntu.

- Comprobar que la aplicación está instalada correctamente.

**▸** Apartado 2. Cliente FTP en modo texto:

- Verificar si el cliente FTP en modo texto está instalado.

- Comprobar el correcto funcionamiento de la aplicación.

- Realizar la misma operación con un cliente FTP sobre Windows 10.

**▸ Solución**

Para realizar las tareas descritas, te proporciono una guía para cada apartado:

#### Clientes FTP

**Apartado 1.** Cliente FTP en modo gráfico:

**Instalar la aplicación Filezilla Client en Ubuntu:**

**▸** Abre una terminal en Ubuntu.

**▸** Actualiza los repositorios de paquetes:

![image-14](images/image-14.png)

**▸** Instala FileZilla con el siguiente comando:

![image-15](images/image-15.png)

**▸** Espera a que se complete la instalación.

**Comprobar que la aplicación está instalada correctamente:**

**▸** Abre FileZilla desde el menú de aplicaciones o ejecutando filezilla en la terminal. En

la interfaz de FileZilla, ingresa los siguientes detalles para conectarte al servidor FTP:

- Host: nic.funet.fi

- Nombre de usuario: ftp

- Contraseña: (dejar en blanco).

**▸** Haz clic en «Conexión rápida». **▸** Deberías ver la lista de directorios y archivos del servidor FTP si la conexión fue exitosa.

**Apartado 2.** Cliente FTP en modo texto:

**Verificar si el cliente FTP en modo texto está instalado:** **▸** En la terminal, ejecuta:

![image-16](images/image-16.png)

**▸** Si el comando está disponible, significa que el cliente FTP en modo texto está instalado. De lo contrario, deberás instalarlo con:

![image-17](images/image-17.png)

**Comprobar el correcto funcionamiento de la aplicación:** **▸** Conéctate al servidor FTP con el siguiente comando:

![image-18](images/image-18.png)

**▸** Cuando te solicite el nombre de usuario, ingresa ftp. **▸** Cuando te pida la contraseña, presiona «Enter» (sin escribir nada). **▸** Deberías ver un mensaje de bienvenida y la lista de archivos en el servidor si la conexión fue exitosa. **▸** Para salir del FTP, escribe «bye» o «quit».

#### Cliente FTP en modo texto bajo Windows

**▸** Abrir la línea de comandos:

- Presiona «Win + R», escribe «cmd» y presiona «Enter». Esto abrirá la ventana de la línea de comandos.

**▸** Iniciar la conexión FTP:

- En la ventana de comandos, escribe el siguiente comando para iniciar la conexión al servidor FTP:

![image-19](images/image-19.png)

**▸** Ingresar las credenciales:

- Nombre de usuario: cuando te pida el nombre de usuario, escribe «ftp» y presiona «Enter».

- Contraseña: cuando te pida la contraseña, simplemente presiona «Enter» (deja el campo en blanco).

**▸** Navegar y transferir archivos:

- Si la conexión fue exitosa, deberías ver el prompt de ftp>. Desde aquí, puedes usar comandos FTP para navegar y transferir archivos. Algunos comandos útiles son:

- ls o dir : lista los archivos y directorios en el servidor.

- cd (directorio): cambia de directorio.

- get (archivo): descarga un archivo del servidor.

- put (archivo): sube un archivo al servidor.

**▸** Cerrar la conexión:

- Cuando termines, escribe «bye» o «quit» para cerrar la conexión FTP y salir del cliente FTP.

![Ejemplo completo:](images/image-20.png)

Este proceso te permitirá conectarte a nic.funet.fi desde un entorno Windows usando el cliente FTP en modo texto.

## Entrenamiento 3. Servidores FTP en Windows

**▸ Planteamiento del ejercicio**

Se desea utilizar el servidor Windows Server 2008 Enterprise como servidor FTP para que sea capaz intercambiar archivos con diferentes clientes: **▸** Instalar la aplicación Gene6 FTP Server en el servidor Windows Server 2008 Enterprise. **▸** Comprobar que la aplicación está instalada correctamente. **▸** ¿Cómo se configura dicha aplicación? Crea un sitio, configura una cuenta de usuario, habilitar el acceso anónimo y establece cuotas.

**▸ Desarrollo paso a paso**

Servidor FTP en Windows Server 2008 Enterprise:

**▸** Instalar la aplicación Gene6 FTP Server.

**▸** Comprobar que la aplicación está instalada correctamente.

**▸** Configuración de Gene6 FTP Server.

**▸ Solución**

#### Servidor FTP en Windows Server 2008 Enterprise

Instalar la aplicación Gene6 FTP Server: **▸** Descarga la aplicación Gene6 FTP Server desde su página oficial o desde una fuente confiable. **▸** Ejecuta el instalador en Windows Server 2008 y sigue las instrucciones del asistente de instalación. Comprobar que la aplicación está instalada correctamente:

**▸** Después de la instalación, abre Gene6 FTP Server desde el menú de programas.

**▸** Verifica que la interfaz de Gene6 FTP Server se abra sin errores.

Configuración de Gene6 FTP Server:

**Crear un nuevo sitio FTP:**

**▸** Abrir Gene6 FTP Server:

- Abre la aplicación Gene6 FTP Server desde el menú de inicio.

**▸** Crear un nuevo sitio:

- Ve a «File» > «New Site» para iniciar el asistente de creación de un nuevo sitio.

- Nombre del sitio: asigna un nombre a tu nuevo sitio, por ejemplo, «MiServidorFTP».

**▸** Configuración de la IP y puerto:

- En la pestaña «General» del sitio que acabas de crear:

- Dirección IP: selecciona «0.0.0.0» para que el sitio escuche en todas las interfaces de red o especifica una IP particular.

- Puerto: mantén el puerto predeterminado 21 para conexiones FTP estándar.

**▸** Directorio raíz:

- Ir a la pestaña «Directories».

- Define el Root Directory (directorio raíz) donde se almacenarán los archivos. Por ejemplo, «C:\FTP_Site».

- Configura los permisos de lectura y escritura según tus necesidades.

**Crear una cuenta de usuario:**

**▸** Acceder a la gestión de usuarios:

- Selecciona el sitio que acabas de crear en el panel izquierdo de Gene6 FTP Server.

- Ve a la pestaña «Users».

**▸** Crear un nuevo usuario:

- Haz clic en «New User» para crear una cuenta de usuario.

- Nombre de usuario: especifica un nombre de usuario, por ejemplo, «usuario1».

- Contraseña: asigna una contraseña para este usuario.

**▸** Asignar directorio y permisos. Ve a la pestaña «Directories» dentro de la

configuración del usuario:

- Asigna el directorio específico para este usuario. Por ejemplo,

«C:\FTP_Site\usuario1».

- Configura los permisos de lectura, escritura y ejecución según sea necesario.

- Configurar acceso anónimo.

**▸** Habilitar acceso anónimo:

- Ve a la pestaña «Anonymous» del sitio que creaste.

- Activa la opción «Enable Anonymous Login» para permitir que usuarios sin cuenta puedan acceder.

**▸** Configurar permisos para acceso anónimo:

- En la pestaña «Directories» dentro de la configuración de acceso anónimo:

- Asigna un directorio para el acceso anónimo, por ejemplo, «C:\FTP_Site\Anonymous».

- Define permisos limitados como solo lectura para evitar modificaciones por usuarios anónimos.

**Establecer cuotas:**

**▸** Acceder a las opciones de cuotas:

- En la configuración del usuario (usuario1), ve a la pestaña «Quotas».

**▸** Configurar cuotas:

- Cuota máxima de espacio en disco: establece el límite de espacio que este usuario puede utilizar, por ejemplo, 100 MB.

- Número máximo de archivos: puedes establecer un límite en el número de archivos que el usuario puede subir, por ejemplo, 1000 archivos.

**Guardar y aplicar configuraciones:** **▸** Aplicar cambios:

- Después de configurar todos los ajustes necesarios, asegúrate de guardar los cambios haciendo clic en «Apply» o «OK».

**▸** Probar la conexión:

- Desde un cliente FTP, intenta conectarte al servidor usando tanto la cuenta de usuario1 como el acceso anónimo para asegurarte de que todo funcione correctamente.

#### Ejemplo práctico

Imagina que has configurado lo siguiente:

**▸** Sitio FTP: MiServidorFTP.

**▸** Dirección IP: 192.168.10.1.

**▸** Puerto: 21.

**▸** Directorio Raíz: C:\FTP_Site.

**▸** Usuario Creado: usuario1.

**▸** Contraseña del Usuario: password123.

**▸** Directorio de Usuario: C:\FTP_Site\usuario1.

**▸** Cuota para el Usuario: 100 MB y 1000 archivos.

**▸** Acceso Anónimo Habilitado: sí, con acceso solo lectura al directorio

C:\FTP_Site\Anonymous.

Probar conexión:

**▸** Para usuario1:

- Abre un cliente FTP como FileZilla.

- Conéctate al servidor.

- Host: dirección IP de tu servidor.

- Usuario: usuario1.

- Contraseña: password123.

- Navega y verifica que los permisos y cuotas funcionan como configuraste.

**▸** Para acceso anónimo:

- En el cliente FTP intenta conectar sin ingresar nombre de usuario o contraseña.

- Verifica que solo puedes leer archivos en el directorio C:\FTP_Site\Anonymous.

Con estas configuraciones, Gene6 FTP Server estará preparado para operar con usuarios específicos, acceso anónimo y gestión de cuotas, lo que te permitirá un control detallado sobre las operaciones de FTP en tu servidor.

## Entrenamiento 4. Servidores FTP en Ubuntu

**▸ Planteamiento del ejercicio**

Se desea utilizar el servidor Ubuntu como servidor FTP para que sea capaz de intercambiar archivos con diferentes clientes:

**▸** Instalar la aplicación vsftpd en el servidor Ubuntu.

**▸** Comprobar que la aplicación está instalada correctamente e indicar el PID del

proceso de dicha aplicación. **▸** ¿Cómo se configura dicha aplicación? Crea un sitio, configura una cuenta de usuario local, habilitar el acceso anónimo y establece cuotas y permisos. Habilitar FTP Pasivo (opcional).

**▸ Desarrollo paso a paso**

Servidor FTP en Ubuntu:

**▸** Instalar la aplicación vsftpd en Ubuntu.

**▸** Comprobar que la aplicación está instalada correctamente e indicar el PID del

proceso. **▸** Configuración de vsftpd.

**▸ Solución**

#### Servidor FTP en Ubuntu

Instalar la aplicación vsftpd en Ubuntu:

**▸** Abre una terminal y ejecuta el siguiente comando:

![image-21](images/image-21.png)

Comprobar que la aplicación está instalada correctamente e indicar el PID del proceso:

**▸** Verifica el estado del servicio vsftpd con:

![image-22](images/image-22.png)

**▸** Si el servicio está activo *(running),* la instalación fue exitosa.

**▸** Para obtener el PID del proceso, puedes ejecutar:

![image-23](images/image-23.png)

**▸** Esto devolverá el ID de proceso (PID) de vsftpd, confirmando que está en ejecución. Configuración de vsftpd: El archivo principal de configuración de vsftpd es /etc/vsftpd.conf. Realiza una copia de seguridad antes de hacer cambios:

![image-24](images/image-24.png)

**▸** Abre el archivo de configuración para editarlo:

![image-25](images/image-25.png)

Configuración básica:

Modifica las siguientes opciones en el archivo de configuración según tus necesidades:

**▸** Permitir usuarios locales:

![image-26](images/image-26.png)

**▸** Permitir escritura para usuarios locales:

![image-27](images/image-27.png)

**▸** Configurar umask para usuarios locales:

![image-28](images/image-28.png)

**▸** Configurar umask para usuarios locales:

![image-29](images/image-29.png)

**▸** Restringir usuarios a sus directorios de inicio:

![image-30](images/image-30.png)

Configurar una cuenta de usuario local:

**▸** Crear un nuevo usuario:

- Supongamos que quieres crear un usuario llamado ftpuser con el directorio de inicio /home/ftpuser/ftp :

![▸ Crear un directorio para subidas:](images/image-31.png)

- Crea un directorio para que el usuario pueda subir archivos:

![Habilitar el acceso anónimo:](images/image-32.png)

**▸** Permitir acceso anónimo: para habilitar el acceso anónimo, asegúrate de que esta línea esté presente y configurada como YES .

![image-33](images/image-33.png)

**▸** Configurar directorio anónimo: crea un directorio para los usuarios anónimos.

![image-34](images/image-34.png)

**▸** Luego, asegúrate de que los permisos en /srv/ftp sean solo de lectura para el acceso anónimo:

![image-35](images/image-35.png)

Restringir subidas para usuarios anónimos: Para evitar que los usuarios anónimos puedan subir archivos, asegúrate de que la opción anon_upload_enable esté deshabilitada (comentada o configurada como NO ):

![image-36](images/image-36.png)

Establecer cuotas: Para establecer cuotas, puedes utilizar el sistema de cuotas de Linux.

**▸** Instalar el paquete de cuotas:

![image-37](images/image-37.png)

**▸** Configurar el sistema de cuotas.

- Edita el archivo /etc/fstab para habilitar las cuotas en el sistema de archivos:

![image-38](images/image-38.png)

**▸** Añade las opciones usrquota y grpquota en la partición donde se encuentra /home o el directorio donde están los usuarios:

![image-39](images/image-39.png)

**▸** Remontar la partición y crear los archivos de cuotas:

![image-40](images/image-40.png)

**▸** Establecer cuotas para el usuario ftpuser .

- Configura las cuotas para el usuario ftpuser :

![image-41](images/image-41.png)

En el editor que se abre, establece los límites duros y blandos para el uso de bloques y el número de inodos. Habilitar FTP pasivo (opcional): Si necesitas habilitar el modo pasivo, añade las siguientes líneas al archivo de configuración:

![image-42](images/image-42.png)

Reiniciar el servicio:

Después de realizar todos los cambios, guarda y cierra el archivo de configuración.

Luego, reinicia vsftpd para aplicar las configuraciones:

![image-43](images/image-43.png)

Verificación y prueba de conexión:

**▸** Conectar como usuario local:

- Usa un cliente FTP (como ftp en la terminal o FileZilla) y conecta usando el nombre de usuario ftpuser y su contraseña.

**▸** Conectar como usuario anónimo:

- Conecta de forma anónima para verificar que puedes acceder a los archivos según las configuraciones realizadas.

#### Ejemplo completo

Imagina que has configurado lo siguiente:

**▸** Usuario FTP: ftpuser con directorio /home/ftpuser/ftp y subdirectorio

home/ftpuser/ftp/upload .

**▸** Acceso anónimo: habilitado con acceso a /srv/ftp y solo permisos de lectura.

**▸** Cuotas: ftpuser tiene una cuota establecida en el sistema.

**▸** Modo pasivo: habilitado con puertos entre 10 000 y 10 100. Al final, con estas configuraciones, tendrás un servidor FTP seguro y funcional que admite tanto usuarios locales como anónimos, con cuotas y restricciones específicas, y la opción de operar en modo pasivo.

## Entrenamiento 5. Configuración y prueba de

## conexión de un servidor FTP con cliente en Ubuntu

## usando VirtualBox

**▸ Planteamiento del ejercicio**

Se quiere utilizar el servidor Windows Server como un servidor FTP utilizando Gene6 FTP Server. El servidor deberá tener las siguientes especificaciones:

**▸** El servidor FTP será accesible por la dirección IP 192.168.100.3 y utilizando el puerto 3333.

**▸** El sitio FTP tendrá la siguiente estructura, donde la carpeta FTP estará ubicada en el escritorio del usuario administrador de Windows Server:

![Figura 6. Estructura del sitio FTP. Fuente: elaboración propia.](images/image-44.png)

*Figura 6. Estructura del sitio FTP. Fuente: elaboración propia.*

**▸** El servidor FTP deberá tener tres usuarios autenticados (virtuales) con nombres de usuario Pedro, Felipe y Ana cuyas contraseñas serán Pedro1234, Felipe1234 y Ana1234, respectivamente. Además, la carpeta *home* del usuario Pedro será la carpeta Pedro que se muestra en el esquema anterior, la del usuario Felipe será la carpeta Felipe y la de Ana, la carpeta Ana. Los usuarios genéricos deberán tener acceso al servidor FTP y su carpeta *home* será la carpeta genérica que se muestra en el esquema anterior.

**▸** Verificar el correcto funcionamiento de la configuración de los usuarios autenticados (Pedro, Felipe y Ana) y de genéricos. Para ello, utilizar el cliente en modo texto de Ubuntu y realizar accesos al servidor FTP con los diferentes usuarios creados, autenticados y genéricos.

**▸** Además, en el servidor existirá un grupo llamado alumnos. El usuario Pedro debe pertenecer a ese grupo. Utilizando el cliente en modo texto de Ubuntu, realizar accesos al servidor FTP con el usuario Pedro. ¿Qué configuración tiene prioridad, la del usuario o la de grupo?

**▸** El usuario Felipe podrá realizar únicamente las siguientes acciones sobre su carpeta *home:* subir, descargar y borrar archivos, ver el contenido de dicha carpeta y crear nuevos subdirectorios.

**▸** Utilizando el cliente en modo texto de Ubuntu, realizar accesos al servidor FTP con el usuario Felipe e intenta comprobar que los permisos otorgados funcionan correctamente. ¿Qué otro tipo de permisos se pueden gestionar en Gene6 FTP Server?

**▸** El número máximo de clientes conectados al servidor será cinco. Además, el usuario Ana podrá usar un máximo de 10KBytes/s en descarga de archivos y 5KBytes/s en descargade archivos por cada conexión y podrá usar un máximo de 1MBytes en descarga de archivos y 2MBytes en descarga de archivos en total (independientemente del número de conexiones realizadas con esta cuenta de usuario). Utilizando el cliente en modo texto de Ubuntu, realizar accesos al servidor FTP con el usuario Ana y comprobar el funcionamiento.

**▸** El usuario Pedro tendrá un espacio de disco máximo (cuota) de 50KBytes. Utilizando el cliente en modo texto de Ubuntu realizar accesos al servidor FTP con el usuario Pedro y transferir archivos hasta completar el máximo de cuota. ¿Qué es lo que ocurre cuando se alcanza el máximo establecido?

**▸** Establecer una conexión con el servidor en modo pasivo. Para ello, configurar un usuario en el servidor FTP y utilizando el cliente gráfico FileZilla de Ubuntu, realizar una conexión al servidor. A través de la consola del cliente FileZilla, verificar que se ha realizado una conexión en modo pasivo.

**▸** Deshabilitar el modo pasivo y realizar un nuevo acceso con el cliente gráfico FileZilla. ¿Se ha podido establecer la conexión? ¿Qué modo de conexión se ha utilizado?

**▸ Desarrollo paso a paso**

Deberás realizar todas las configuraciones y comprobaciones que te piden en el enunciado.

**▸ Solución**

Para configurar un servidor FTP utilizando Gene6 FTP Server en Windows Server con las especificaciones indicadas, sigue los pasos detallados a continuación:

#### Configuración del servidor FTP con la IP y puerto

**▸** Paso 1: instala Gene6 FTP Server en tu servidor Windows Server.

**▸** Paso 2: abre Gene6 FTP Server y crea un nuevo sitio FTP:

- Asigna un nombre descriptivo al sitio.

- Configura la IP como 192.168.100.3.

- Establece el puerto en 3333.

#### Configuración de la estructura de carpetas

**▸** Paso 1: en el escritorio del usuario administrador, crea una carpeta llamada FTP.

**▸** Paso 2: dentro de la carpeta FTP, crea las subcarpetas Pedro, Felipe, Ana, y

Genérico.

#### Creación de usuarios autenticados

Paso 1. En Gene6 FTP Server crea tres usuarios virtuales:

**▸** Pedro:

- Usuario: Pedro.

- Contraseña: Pedro1234.

- Carpeta home: C:\Users\Administrador\Desktop\FTP\Pedro

**▸** Felipe:

- Usuario: Felipe.

- Contraseña: Felipe1234.

- Carpeta Home: C:\Users\Administrador\Desktop\FTP\Felipe

**▸** Ana:

- Usuario: Ana

- Contraseña: Ana1234

- Carpeta Home: C:\Users\Administrador\Desktop\FTP\Ana

Para ello, en el panel izquierdo del Gene6FTP Server, selecciona el sitio FTP en el que deseas configurar el usuario y haz clic derecho en «Users» y selecciona «New User». Configuración del usuario Pedro:

**▸** Nombre de usuario: en el campo Login, ingresa «Pedro».

**▸** Contraseña: en el campo Password, ingresa «Pedro1234».

**▸**

**▸** Directorio *home:*

- En la sección Home Directory, selecciona «Browse.

- Navega hasta C:\Users\Administrador\Desktop\FTP\Pedro y selecciónala como el directorio principal del usuario.

Configuración de permisos: **▸** En la pestaña de permisos o Permissions, puedes configurar los permisos que el usuario Pedro tendrá en su carpeta *home.* Los permisos típicos incluyen:

- Listar directorios (List).

- Leer archivos (Read).

- Escribir archivos (Write).

- Eliminar archivos (Delete).

- Crear carpetas (Create).

**▸** Asegúrate de que Pedro tenga los permisos necesarios para trabajar en su carpeta *home.* **▸** Haremos lo mismo con el resto de los usuarios virtuales. Paso 2. Configura un usuario genérico: **▸** Establece un usuario genérico o anónimo con la carpeta home

C:\Users\Administrador\Desktop\FTP\Genérico .

**▸** Para ello, en el panel izquierdo del Gene6FTP Server, selecciona el sitio FTP en el que deseas configurar el usuario y haz clic derecho en «Users» y selecciona «New User».

Configuración del usuario genérico:

**▸** Nombre de usuario: en el campo Login, escribe «Anonymous» o «genérico» dependiendo de si quieres un usuario completamente anónimo o un usuario con nombre genérico.

**▸** Contraseña: para un usuario anónimo, deja el campo de la contraseña en blanco. Si estás creando un usuario con el nombre genérico, puedes dejar la contraseña vacía o asignar una contraseña, dependiendo de tus necesidades de seguridad.

**▸** Directorio *home:* establece la carpeta home del usuario:

- Selecciona la opción «Home Directory».

- Navega hasta C:\Users\Administrador\Desktop\FTP\Genérico y selecciónala como el directorio principal del usuario.

Configuración de permisos:

**▸** En la sección de permisos, configura los permisos que consideres necesarios para el usuario genérico. Por ejemplo:

- Listar directorios: permitir.

- Leer archivos: permitir.

- Escribir archivos: puedes permitir o denegar dependiendo de si quieres que los usuarios genéricos puedan subir archivos.

#### Verificación de la configuración desde Ubuntu

**▸** Paso 1: desde un cliente Ubuntu, abre una terminal y utiliza el siguiente comando para conectarte al servidor FTP:

![image-45](images/image-45.png)

**▸** Paso 2: prueba iniciar sesión con los usuarios Pedro, Felipe, Ana y el usuario genérico, verificando el acceso a las respectivas carpetas.

#### Creación del grupo Alumnos y asignación del usuario Pedro

**▸** Paso 1: en Gene6 FTP Server, crea un grupo llamado Alumnos.

- En el panel izquierdo, localiza y selecciona la sección «Groups».

- Haz clic derecho en «Groups» y selecciona «New Group» para crear un nuevo grupo.

- Nombre del grupo: en el campo Name, ingresa «Alumnos».

**▸** Paso 2: asigna el usuario Pedro al grupo Alumnos.

- Regresa a la sección «Users» y selecciona el usuario Pedro que creaste previamente.

- Haz clic derecho en «Pedro» y selecciona «Properties» (propiedades).

- En la ventana de propiedades del usuario Pedro, busca la opción para seleccionar un grupo.

- Asignar grupo: en el campo de selección de grupo, selecciona «Alumnos».

- Haz clic en «OK» o «Apply» para guardar los cambios.

En Gene6 FTP Server, la configuración de permisos específicos de un usuario individual tiene prioridad sobre los permisos establecidos a nivel de grupo. Esto significa que, si le das permisos específicos a Pedro, estos pueden sobrescribir los permisos generales del grupo Alumnos.

#### Configuración de permisos para el usuario Felipe

**▸** Paso 1. Configura los permisos para el usuario Felipe para permitir:

- Subir archivos.

- Descargar archivos.

- Borrar archivos.

- Ver el contenido de la carpeta.

- Crear subdirectorios.

Abrir Gene6 FTP Server Seleccionar el usuario Felipe:

**▸** En el panel izquierdo, localiza la sección «Users» y selecciona el usuario «Felipe».

**▸** Haz clic derecho en «Felipe» y selecciona «Properties» (propiedades). Configurar permisos del usuario Felipe: En la ventana de propiedades del usuario, navega a la pestaña «Permissions» o «Rights», dependiendo de la versión de Gene6 FTP Server que estés utilizando. Asegúrate de configurar los permisos necesarios en la carpeta *home* de Felipe (

C:\Users\Administrador\Desktop\FTP\Felipe ):

**▸** Permitir subir archivos *(Upload):*

- Marca la casilla «Write» (escritura).

- Esto permitirá que Felipe suba archivos a su carpeta home.

**▸** Permitir descargar archivos *(Download):*

- Marca la casilla «Read» (lectura).

- Esto permitirá que Felipe descargue archivos de su carpeta home.

**▸** Permitir borrar archivos *(Delete):*

- Marca la casilla «Delete».

- Esto permitirá que Felipe elimine archivos dentro de su carpeta home.

**▸** Ver el contenido de la carpeta *(List Directory):*

- Marca la casilla «List».

- Esto permitirá que Felipe vea el contenido de su carpeta home.

**▸** Permitir crear subdirectorios *(Create Directory):*

- Marca la casilla «Make Directory».

- Esto permitirá que Felipe cree nuevos subdirectorios dentro de su carpeta home.

#### Verificación con el cliente en modo texto en Ubuntu

**▸** Abre una terminal en Ubuntu en el cliente. **▸** Usa el comando ftp para conectarte al servidor FTP: **▸** Ingresa «Felipe» como nombre de usuario y la contraseña correspondiente cuando se te solicite. **▸** Verificar permisos. Subir archivos:

![image-46](images/image-46.png)

![image-47](images/image-47.png)

Verifica que el archivo se sube correctamente.

Descargar archivos:

![image-48](images/image-48.png)

Verifica que puedes descargar archivos.

Borrar archivos:

![image-49](images/image-49.png)

Verifica que puedes borrar archivos.

Ver contenido de la carpeta:

![image-50](images/image-50.png)

Crear subdirectorios:

![image-51](images/image-51.png)

En Gene6 FTP Server, además de los permisos básicos de lectura, escritura,

eliminación, listado y creación de directorios, puedes gestionar otros tipos de permisos, como:

**▸** Renombrar archivos: permite a los usuarios renombrar archivos y directorios.

**▸** Ajustes de permiso avanzado: permite configuraciones más detalladas, como restricciones por IP, limitación de velocidad y cuotas de disco.

**▸** Acceso a directorios específicos: puedes configurar permisos para que un usuario tenga acceso solo a ciertos subdirectorios específicos, en lugar de a todo el directorio home.

#### Configuración de límite de conexiones y ancho de banda para Ana

**▸** Paso 1: establece un límite máximo de cinco clientes conectados al servidor.

- En el panel izquierdo, selecciona el sitio FTP en el que deseas establecer el límite.

- Haz clic derecho en el nombre del sitio y selecciona «Properties» (propiedades).

- En la pestaña «General» o «Connection Settings» (dependiendo de la versión), busca la opción para limitar el número máximo de conexiones simultáneas.

- Límite máximo de conexiones: configura el valor en cinco.

- Haz clic en «OK» o "«Apply» para guardar los cambios.

#### Configuración de cuota de espacio en disco para Pedro

Paso 1: configura una cuota de espacio en disco para el usuario Pedro de 50 KBytes. Cuando configuras una cuota máxima de espacio en disco para un usuario en un servidor FTP, como es el caso del usuario Pedro, en Gene6 FTP Server, el servidor monitorea el tamaño total de los archivos que el usuario ha subido. Una vez que se alcanza la cuota máxima, el servidor FTP ya no permitirá que el usuario suba más archivos.

Cuando la cuota de 50 KBytes se alcance, el servidor FTP rechazará cualquier intento adicional de subir archivos. El mensaje de error podría ser algo similar a:

![image-52](images/image-52.png)

Esto indica que el usuario Pedro ha alcanzado su límite máximo de espacio en disco permitido y no podrá subir más archivos hasta que elimine algunos de los archivos existentes para liberar espacio.

#### Configuración de la conexión en modo pasivo

Paso 1: configura un usuario para el acceso en modo pasivo. **▸** En Gene6 FTP Server, ve a las propiedades del servidor. **▸** Asegúrate de que el modo pasivo (PASV) esté habilitado. Configura el rango de puertos para las conexiones pasivas, si es necesario.

**▸** Guarda los cambios.

Paso 2: desde FileZilla en Ubuntu, establece una conexión en modo pasivo y verifica a través de la consola de FileZilla.

**▸** En FileZilla, ve a «Archivo» > «Gestor de sitios».

**▸** Crea una nueva entrada para tu servidor FTP:

- Servidor: 192.168.100.3

- Puerto: 3333.

- Protocolo: FTP - protocolo de transferencia de archivos.

- Cifrado: usar solo FTP simple (sin cifrado).

- Modo de acceso: normal.

- Usuario: ingresa el nombre de usuario (por ejemplo, Pedro).

- Contraseña: ingresa la contraseña del usuario (por ejemplo, Pedro1234).

**▸** En el mismo cuadro de diálogo del gestor de sitios, selecciona la pestaña

Configuración de transferencia. **▸** Marca la opción «Modo de transferencia pasivo».

**▸** Una vez conectado, en la parte inferior de la interfaz de FileZilla, verás una consola que muestra los comandos y respuestas del servidor. **▸** Busca un mensaje similar a este:

![image-53](images/image-53.png)

Este mensaje confirma que la conexión se ha establecido en modo pasivo.

#### Deshabilitar el modo pasivo y verificar conexión

Paso 1: desactiva el modo pasivo en Gene6 FTP Server. **▸** En el panel de Gene6 FTP Server, selecciona el servidor FTP o el sitio que deseas configurar. **▸** Haz clic derecho sobre el servidor FTP y selecciona «Properties» (propiedades). **▸** Navega a la pestaña de configuración de conexiones, que generalmente se encuentra bajo «Connection Settings »o algo similar. **▸** Busca la opción que habilita el modo pasivo. Dependiendo de la versión, esta opción puede estar en una sección titulada «Passive Mode» o «PASV». **▸** Desmarca la opción para habilitar el modo pasivo. Esta acción deshabilitará el uso de puertos pasivos para la transferencia de datos. Paso 2: intenta conectar de nuevo con FileZilla y verifica si la conexión se realiza en modo activo. **▸** Inicia FileZilla desde el menú de aplicaciones o desde la terminal en Ubuntu usando FileZilla. **▸** Ve a «Archivo» > «Gestor de sitios».

**▸** Selecciona la configuración del servidor FTP que estás utilizando (o crea una nueva si es necesario). **▸** En la pestaña Configuración de transferencia selecciona «Modo activo» en lugar de modo pasivo. **▸** Haz clic en «Conectar» para establecer la conexión con el servidor FTP. **▸** Observa la consola de FileZilla en la parte inferior para los mensajes de conexión y transferencia. Deberías ver comandos como PORT en lugar de PASV.

![image-54](images/image-54.png)

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Entrenamientos  *(pp.3, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92)*
- Material de estudio  *(pp.5–38)*
- A fondo  *(pp.39–47)*
- Servicios en Red e Internet 5 Tema 5. Material de estudio · Servicios en Red e Internet 6 Tema 5. Material de estudio · Servicios en Red e Internet 7 Tema 5. Material de estudio · Servicios en Red e Internet 8 Tema 5. Material de estudio · Servicios en Red e Internet 9 Tema 5. Material de estudio · Servicios en Red e Internet 10 Tema 5. Material de estudio · Servicios en Red e Internet 11 Tema 5. Material de estudio · Servicios en Red e Internet 13 Tema 5. Material de estudio · Servicios en Red e Internet 14 Tema 5. Material de estudio · Servicios en Red e Internet 15 Tema 5. Material de estudio · Servicios en Red e Internet 16 Tema 5. Material de estudio · Servicios en Red e Internet 17 Tema 5. Material de estudio · Servicios en Red e Internet 19 Tema 5. Material de estudio · Servicios en Red e Internet 20 Tema 5. Material de estudio · Servicios en Red e Internet 21 Tema 5. Material de estudio · Servicios en Red e Internet 22 Tema 5. Material de estudio · Servicios en Red e Internet 23 Tema 5. Material de estudio · Servicios en Red e Internet 24 Tema 5. Material de estudio · Servicios en Red e Internet 25 Tema 5. Material de estudio · Servicios en Red e Internet 26 Tema 5. Material de estudio · Servicios en Red e Internet 27 Tema 5. Material de estudio · Servicios en Red e Internet 28 Tema 5. Material de estudio · Servicios en Red e Internet 29 Tema 5. Material de estudio · Servicios en Red e Internet 32 Tema 5. Material de estudio · Servicios en Red e Internet 33 Tema 5. Material de estudio · Servicios en Red e Internet 34 Tema 5. Material de estudio · Servicios en Red e Internet 35 Tema 5. Material de estudio · Servicios en Red e Internet 36 Tema 5. Material de estudio · Servicios en Red e Internet 37 Tema 5. Material de estudio · Servicios en Red e Internet 38 Tema 5. Material de estudio  *(pp.5, 6, 7, 8, 9, 10, 11, 13, 14, 15, 16, 17, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 32, 33, 34, 35, 36, 37, 38)*
- Servicios en Red e Internet 39 Tema 5. A fondo · Servicios en Red e Internet 40 Tema 5. A fondo · Servicios en Red e Internet 41 Tema 5. A fondo · Servicios en Red e Internet 42 Tema 5. A fondo · Servicios en Red e Internet 43 Tema 5. A fondo · Servicios en Red e Internet 44 Tema 5. A fondo · Servicios en Red e Internet 45 Tema 5. A fondo · Servicios en Red e Internet 46 Tema 5. A fondo · Servicios en Red e Internet 47 Tema 5. A fondo  *(pp.39–47)*
- Servicios en Red e Internet 48 Tema 5. Entrenamientos · Servicios en Red e Internet 49 Tema 5. Entrenamientos · Servicios en Red e Internet 50 Tema 5. Entrenamientos · Servicios en Red e Internet 51 Tema 5. Entrenamientos · Servicios en Red e Internet 52 Tema 5. Entrenamientos · Servicios en Red e Internet 53 Tema 5. Entrenamientos · Servicios en Red e Internet 54 Tema 5. Entrenamientos · Servicios en Red e Internet 55 Tema 5. Entrenamientos · Servicios en Red e Internet 56 Tema 5. Entrenamientos · Servicios en Red e Internet 57 Tema 5. Entrenamientos · Servicios en Red e Internet 58 Tema 5. Entrenamientos · Servicios en Red e Internet 59 Tema 5. Entrenamientos · Servicios en Red e Internet 60 Tema 5. Entrenamientos · Servicios en Red e Internet 61 Tema 5. Entrenamientos · Servicios en Red e Internet 62 Tema 5. Entrenamientos · Servicios en Red e Internet 63 Tema 5. Entrenamientos · Servicios en Red e Internet 64 Tema 5. Entrenamientos · Servicios en Red e Internet 65 Tema 5. Entrenamientos · Servicios en Red e Internet 66 Tema 5. Entrenamientos · Servicios en Red e Internet 67 Tema 5. Entrenamientos · Servicios en Red e Internet 68 Tema 5. Entrenamientos · Servicios en Red e Internet 69 Tema 5. Entrenamientos · Servicios en Red e Internet 70 Tema 5. Entrenamientos · Servicios en Red e Internet 71 Tema 5. Entrenamientos · Servicios en Red e Internet 72 Tema 5. Entrenamientos · Servicios en Red e Internet 73 Tema 5. Entrenamientos · Servicios en Red e Internet 74 Tema 5. Entrenamientos · Servicios en Red e Internet 75 Tema 5. Entrenamientos · Servicios en Red e Internet 76 Tema 5. Entrenamientos · Servicios en Red e Internet 77 Tema 5. Entrenamientos · Servicios en Red e Internet 78 Tema 5. Entrenamientos · Servicios en Red e Internet 79 Tema 5. Entrenamientos · Servicios en Red e Internet 80 Tema 5. Entrenamientos · Servicios en Red e Internet 81 Tema 5. Entrenamientos · Servicios en Red e Internet 82 Tema 5. Entrenamientos · Servicios en Red e Internet 83 Tema 5. Entrenamientos · Servicios en Red e Internet 84 Tema 5. Entrenamientos · Servicios en Red e Internet 85 Tema 5. Entrenamientos · Servicios en Red e Internet 86 Tema 5. Entrenamientos · Servicios en Red e Internet 87 Tema 5. Entrenamientos · Servicios en Red e Internet 88 Tema 5. Entrenamientos · Servicios en Red e Internet 89 Tema 5. Entrenamientos · Servicios en Red e Internet 90 Tema 5. Entrenamientos · Servicios en Red e Internet 91 Tema 5. Entrenamientos · Servicios en Red e Internet 92 Tema 5. Entrenamientos  *(pp.48–92)*