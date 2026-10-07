## Tema 4

## Servicios en Red e Internet

# Tema 4. Servidor web

# Índice

Esquema Material de estudio

## 4.1. Introducción y objetivos

## 4.2. Características

## 4.3. Cliente y servidor web

## 4.4. Conceptos del servidor

## 4.5. Sitios web virtuales

## 4.6. Acceso al servidor web

## 4.7. Referencias bibliográficas

A fondo ¿Qué es un hosting y cómo funciona? ¿Qué es un servidor web? Mejores servicios de alojamiento web de 2024 ¿Qué es un servidor web y cómo funciona? ¿Qué es Apache y para qué sirve? Alquila un servidor online y céntrate en lo importante Curso de servidores web gratis | zoneclass.com Entrenamientos Entrenamiento 1. Instalación y configuración de servicio DHCP en Windows Entrenamiento 2. Instalación y configuración de servicio web en Ubuntu

Entrenamiento 3. Configuración particular de un servidor web con Windows

Entrenamiento 4. Autenticación, autorización y control de acceso de un servidor Web con Windows

Entrenamiento 5. Autenticación, autorización y control de acceso de un servidor Web con Ubuntu

# Esquema

![image-2](images/image-2.png)

Servicios en Red e Internet 4 Tema 4. Esquema

## 4.1. Introducción y objetivos

Uno de los motivos, por no decir el motivo principal o más importante, para la implementación de una red de comunicaciones (Internet, Intranet o cualquier tipo de red) es que un conjunto de usuarios o dispositivos pueda compartir información. En este caso, con información nos referimos a cualquier conjunto de datos en forma de textos, imágenes, vídeos, archivos de

aplicaciones, etc. Esta **capacidad de**

**compartir y distribuir datos** es fundamental para la funcionalidad de la red, ya que permite la colaboración, el acceso a recursos y la comunicación entre usuarios.

Para poder compartir esa información a lo largo de la red se pueden utilizar muchas **estrategias o sistemas diferentes,** algunas muy familiares a los usuarios de una red, como por ejemplo sistemas P2P *(peer-to-peer),* sistemas de descarga directa, medios de comunicación *online* y aplicaciones de mensajería. Cada uno de estos métodos tiene sus propias **ventajas y limitaciones.** Por ejemplo, los sistemas P2P permiten a los usuarios compartir archivos directamente entre sí sin necesidad de un servidor central, mientras que las descargas directas suelen implicar la transferencia de archivos desde un servidor central a un cliente.

Pero, sin duda, la forma más común y eficaz de compartir información a lo largo de una red es utilizando lo que se conoce como **páginas web.** Las páginas web se han convertido en la piedra angular de la comunicación en línea, permitiendo a los usuarios acceder a una amplia variedad de contenidos desde cualquier lugar del mundo con una conexión a Internet. Este acceso se facilita a través de **navegadores** web, que interpretan el código HTML, información de manera visual y funcional.

CSS y JavaScript para presentar la

En este caso, para poder compartir información mediante páginas web es necesario publicar dicha información (texto, imágenes, vídeos, etc.) a través de servidores web, de este modo, nace lo que hoy se conoce como servicio web. Un **servidor web** es

Servicios en Red e Internet 5 Tema 4. Material de estudio u n *software* o *hardware* que recibe solicitudes de los navegadores de los usuarios, procesa esas solicitudes y entrega el contenido solicitado. Los servidores web funcionan utilizando el **protocolo HTTP** (Hypertext Transfer Protocol) o su versión segura, HTTPS (HTTP Secure), para establecer una comunicación efectiva entre el servidor y el cliente.

Existen **múltiples tipos de servidores web,** cada uno con sus características y ventajas específicas. Entre los más conocidos se encuentran Apache HTTP Server, Nginx y Microsoft Internet Information Services (IIS). Apache, por ejemplo, es uno de los servidores web más utilizados debido a su flexibilidad y extensibilidad a través de módulos. Nginx, por su parte, es conocido por su eficiencia en la gestión de un gran número de conexiones concurrentes y por su capacidad para actuar como proxy inverso y balanceador de carga. IIS, desarrollado por Microsoft, es popular en entornos que utilizan tecnologías de Microsoft como ASP.NET.

La **elección** del **servidor web adecuado** depende de varios factores, incluyendo el tipo de contenido que se va a servir, el volumen de tráfico esperado, y las necesidades específicas de seguridad y rendimiento. Además, los servidores web deben configurarse correctamente para asegurar su funcionamiento óptimo y la protección de los datos que manejan. Esto incluye la gestión de certificados SSL/TLS para habilitar HTTPS, la configuración de reglas de *firewall* y la implementación de medidas para prevenir ataques cibernéticos como los ataques de denegación de servicio (DDoS) y las vulnerabilidades de seguridad.

En resumen, los servidores web son componentes cruciales en la infraestructura de redes y en la prestación de servicios web. Facilitan la publicación y distribución de información a través de Internet y otras redes, permitiendo a los usuarios acceder a contenido de manera rápida y eficiente. La correcta implementación y gestión de estos servidores es esencial para garantizar una experiencia de usuario satisfactoria y la seguridad de la información compartida. Sin estos servidores, el intercambio de datos en la web no sería posible y gran parte de la funcionalidad moderna de Internet

Servicios en Red e Internet 6 Tema 4. Material de estudio se vería gravemente afectada.

Los **objetivos** que se pretende alcanzar en este tema son:

**▸** Comprender la importancia de compartir información en redes de comunicaciones.

**▸** Identificar diferentes métodos de compartir información en una red.

**▸** Entender el rol de las páginas web en la comunicación en línea.

**▸** Conocer el funcionamiento de los servidores web.

**▸** Diferenciar entre tipos de servidores web.

**▸** Evaluar factores para la elección de un servidor web adecuado.

**▸** Configurar y gestionar servidores web para asegurar su funcionamiento óptimo.

**▸** Entender qué es un servicio web.

**▸** Aprender sobre la estructura y sintaxis de las URL.

**▸** Explorar las aplicaciones del servicio web.

**▸** Conocer la historia y funcionalidad del protocolo HTTP.

**▸** Distinguir entre páginas web estáticas y dinámicas.

**▸** Entender la seguridad en HTTP y HTTPS.

**▸** Diferenciar entre cliente web y servidor web.

**▸** Comprender el concepto de sitios web virtuales.

## 4.2. Características

¿Qué es este servicio?

Un servicio web se puede definir como:

Un servicio que facilita la compartición de recursos (como datos, vídeos, etc.) en forma de páginas web (HTML, XHTML, etc.) a través de una red

(Internet o Intranet).

Esto significa que la información o los recursos (datos, imágenes, vídeos, etc.) que se desean compartir entre usuarios se publican en forma de páginas web, utilizando formatos específicos como HTML o XHTML.

Todo el contenido publicado como páginas web forma lo que conocemos como la WWW (World Wide Web), por lo que muchas direcciones de páginas web comienzan con www.

Es importante no confundir Internet con la

WWW. Internet es una **red de**

**comunicación** compuesta por dispositivos conectados entre sí, mientras que la WWW es un **conjunto de páginas web** alojadas en servidores web; no todos los dispositivos de Internet son servidores web.

Dentro de la red informática mundial, cada recurso (datos, imágenes, vídeos, etc.) publicado en las páginas web tiene un **identificador único,** similar a un DNI. Este identificador se llama **URL (Uniform Resource Locator)** y es el que aparece en la barra de navegación de los navegadores web (como Internet Explorer, Firefox y Google Chrome) al acceder a una página web.

![Figura 1. URL obtenida del navegador Chrome. Fuente: elaboración propia.](images/image-3.png)

*Figura 1. URL obtenida del navegador Chrome. Fuente: elaboración propia.*

La sintaxis de una URL es la siguiente:

```
protocol://[user:password@]host[:port]/path/resource
```

Normalmente, protocol es http, ya que el servicio web usa este protocolo. La parte user:password@ permite autenticarse en el servidor web mediante la URL, aunque no se recomienda por razones de seguridad, ya que los navegadores pueden guardar accesos recientes. Host es el nombre del dominio del servidor y port es el puerto de acceso. Path y resource completan la ruta al recurso compartido y el nombre del recurso.

Un ejemplo de URL real sería:

<http://www.marca.com/futbol/seleccion/131.html>

Aplicaciones del servicio web

Las aplicaciones del servicio web abarcan una amplia gama de funcionalidades y usos en diversos contextos. A continuación, se describen algunas de las principales aplicaciones del servicio web:

**▸ Navegación web:**

- Páginas web: permite la visualización y el acceso a contenido en línea a través de navegadores web. Esto incluye sitios de noticias, blogs, foros y otros tipos de contenido informativo y de entretenimiento.

**▸**

- Aplicaciones web: proporciona funcionalidades interactivas directamente en el navegador, como herramientas de edición de texto, hojas de cálculo y aplicaciones de gestión de proyectos.

**▸ Comunicación y redes sociales:**

- Plataformas sociales: servicios como Facebook, Twitter e Instagram utilizan aplicaciones web para la interacción social, el intercambio de información y la creación de comunidades en línea.

- Mensajería y correo electrónico: servicios como Gmail, Outlook y WhatsApp ofrecen comunicación instantánea y gestión de correos electrónicos a través de interfaces web.

**▸ Comercio electrónico:**

- Tiendas en línea: permite a las empresas vender productos y servicios a través de sitios web de comercio electrónico, como Amazon, eBay y Shopify.

- Pasarelas de pago: facilita las transacciones financieras en línea mediante servicios como PayPal y Stripe.

**▸ Servicios en la nube:**

- Almacenamiento en la nube: ofrece servicios de almacenamiento y gestión de archivos en línea, como Google Drive, Dropbox y OneDrive.

- Aplicaciones de productividad: proporciona herramientas en línea para la creación y edición de documentos, hojas de cálculo y presentaciones, como Google Docs y Microsoft Office Online.

**▸ Servicios de información y entretenimiento:**

- Streaming de vídeo y música: permite el acceso a contenido multimedia en tiempo real, como Netflix, YouTube y Spotify.

- Noticias y publicaciones: acceso a fuentes de noticias y publicaciones especializadas en diferentes áreas de interés.

**▸ Servicios financieros y bancarios:**

- Banca en línea: ofrece servicios de gestión de cuentas, transferencias y pagos a través de plataformas web proporcionadas por bancos y entidades financieras.

- Trading y finanzas: proporciona acceso a plataformas de trading y análisis financiero en línea.

**▸ Integración de sistemas:**

- API y servicios web: facilita la integración y comunicación entre diferentes aplicaciones y servicios mediante el uso de API (Interfaces de Programación de Aplicaciones) para intercambiar datos y funcionalidades.

**▸ Educación y capacitación:**

- Plataformas de aprendizaje virtual: ofrecen cursos y materiales educativos en línea a través de plataformas como Coursera, Udemy y Khan Academy.

- Herramientas de colaboración: facilitan el trabajo en equipo y la colaboración en proyectos educativos mediante herramientas como Google Classroom y Microsoft Teams.

**▸ Servicios de atención al cliente:**

- Soporte en línea: incluye chat en vivo, sistemas de tickets y bases de datos de conocimiento que proporcionan asistencia y soporte a los usuarios a través de interfaces web.

Estas aplicaciones demuestran cómo los servicios web se han convertido en una parte integral de la vida diaria y empresarial, proporcionando una amplia gama de herramientas y funcionalidades accesibles a través de la web.

Historia y funcionalidad

El servicio web se basa principalmente en el protocolo HTTP (HyperText Transfer Protocol), que se desarrolla desde 1990 por el W3C (World Wide Web Consortium) y el IETF (Internet Engineering Task Force). La versión activa actual es la 1.2, especificada en el RFC 2774.

Al igual que otros protocolos, como DHCP o DNS, HTTP **opera** en la capa de aplicación del **modelo OSI** (Open Systems Interconnection). Utiliza **TCP** (Transmission Control Protocol) como **protocolo de transporte** y, por defecto, tanto los servidores web como los clientes usan el **puerto 80,** aunque, a menudo, se utilizan puertos diferentes en redes locales o intranets por razones de seguridad.

HTTP sigue una **arquitectura cliente/servidor,** donde los clientes envían solicitudes de recursos a los servidores web, que almacenan las páginas web y responden con el recurso solicitado o con un código de error si el recurso no está disponible (por ejemplo, el error 404).

![Figura 2. Arquitectura cliente-servidor. Fuente: Edgar, 2014.](images/image-4.png)

*Figura 2. Arquitectura cliente-servidor. Fuente: Edgar, 2014.*

Es crucial señalar la existencia de **páginas web dinámicas,** que **interactúan** con el usuario y cambian en función de las acciones del usuario, como subir una foto o completar un formulario. Para implementar estas páginas dinámicas, se añaden **aplicaciones** tanto en el lado del cliente como en el del servidor. En el lado del cliente, se pueden encontrar aplicaciones como applets Java o aplicaciones Flash. En el lado del servidor, se utilizan aplicaciones web como PHP o Python.

HTTP es un **protocolo sin estado,** lo que significa que no recuerda las visitas previas. Para gestionar la información de sesiones, se utilizan ***cookies,*** pequeños archivos que los servidores web colocan en los equipos clientes para recordar la actividad pasada. El uso de *cookies* está regulado por ley debido a las implicaciones de privacidad, ya que pueden almacenar información sensible como contraseñas y hábitos de navegación.

Finalmente, es importante tener en cuenta que, por defecto, la información transmitida por HTTP se envía en texto plano, sin cifrado. Esto compromete la seguridad, ya que cualquier usuario con acceso a la red puede interceptar y leer la información transmitida. Para mejorar la seguridad, se utiliza **HTTPS (HTTP Secure),** un protocolo que cifra la comunicación entre el cliente y el servidor web.

## 4.3. Cliente y servidor web

Cliente web

El cliente web es un *software* específico que permite a un dispositivo **realizar** **solicitudes de páginas web** a los servidores web y mostrar las respuestas en pantalla para su visualización. Es decir, este *software* solicita recursos a los servidores web y luego presenta gráficamente las respuestas (ya sea el recurso solicitado o un código de error) para que el usuario las pueda ver.

Comúnmente, estos programas son conocidos como **navegadores web** o web *browsers.* En el mercado actual, y especialmente con la popularidad de los teléfonos inteligentes, existe una **amplia gama** de navegadores web, que incluye Internet Explorer, Firefox, Opera, Google Chrome, Epiphany, Maxthon, Safari y Links (un navegador en modo texto). La mayoría de estos navegadores tienen una apariencia y un modo de uso muy similares.

En algunos contextos, el término **cliente web** también puede referirse al dispositivo que alberga este *software,* es decir, el **equipo físico** desde el cual se realizan las solicitudes de recursos a los servidores web.

![image-5](images/image-5.png)

Figura 3. *Ranking* de los navegadores más utilizados. Fuente: Fenollosa, 2023.

Servidor DNS

Un servidor web es un *software* específico que permite a un dispositivo **atender las** **solicitudes** de los navegadores para proporcionar los recursos solicitados o, en su defecto, un código de error si surge algún problema al procesar la solicitud.

Físicamente, el término servidor web, también, se refiere al equipo que contiene este *software* específico y en el que se alojan diversas páginas web y los recursos o información que estas páginas ofrecen.

En el mercado de servidores web existen diversas aplicaciones o *software* para implementar un servidor web en un dispositivo, dependiendo del sistema operativo instalado.

Por ejemplo, en sistemas operativos de la familia Microsoft, es común usar Windows Server 2008 o Windows Server 2012 para implementar este tipo de servicio. Microsoft ofrece una aplicación nativa llamada **I I S** (Internet Information Services), cuya última versión es la 8.5, que se puede integrar y configurar directamente en el sistema operativo para que funcione como servidor web.

![Figura 4. Servidor Web IIS. Fuente: Velasco, 2017.](images/image-6.png)

*Figura 4. Servidor Web IIS. Fuente: Velasco, 2017.*

En servidores basados en distribuciones Linux como Ubuntu Server o CentOS, la aplicación más popular para implementar servidores web es **Apache,** cuya última versión estable es la 2.4. Es importante notar que Apache, también, puede ser utilizado en sistemas operativos de la familia Microsoft.

![Figura 5. Servidor Web Apache. Fuente: Norfi Carrodeguas, 2022.](images/image-7.png)

*Figura 5. Servidor Web Apache. Fuente: Norfi Carrodeguas, 2022.*

## 4.4. Conceptos del servidor

En esta parte del tema de servicios web, se presentan varios términos esenciales vinculados con los servidores web, que serán relevantes durante la configuración, implementación y verificación del correcto funcionamiento de estos servidores.

Sitio web

Un sitio web es una **colección organizada de directorios** que contienen todos los archivos necesarios para los recursos ofrecidos por un servidor web. En esencia, es una estructura jerárquica donde se almacenan páginas web interrelacionadas, así como todos los recursos e información que se publican y comparten en ellas.

Por lo general, los sitios web tienen una **estructura en forma de árbol,** con un directorio raíz que incluye todos los subdirectorios y la mayoría de los archivos del sitio web. Comprender esta jerarquía y el contenido de cada directorio es fundamental para mantener una seguridad adecuada, como restricciones de acceso y permisos.

Módulos

Los servidores web tienen **diferentes características y funcionalidades,** dependiendo de su implementación y el sistema operativo en el que se ejecutan. Algunos servidores son compatibles con aplicaciones específicas, otros proporcionan niveles avanzados de seguridad y otros permiten la ejecución de aplicaciones particulares. Los servidores web son **altamente personalizables** y se pueden mejorar mediante la adición de módulos, que son complementos que amplían sus capacidades.

Los módulos son componentes que se integran en el servidor web para añadir nuevas funcionalidades.

Según las necesidades del servidor, se pueden añadir módulos de diferentes tipos, tales como:

**▸ Módulos de seguridad:** incrementan la protección del servidor contra amenazas.

**▸ Módulos de monitorización:** facilitan el seguimiento del rendimiento y el estado del servidor.

**▸ Módulos de autenticación:** gestionan la autenticación y el control de acceso de los usuarios.

**▸ Otros módulos:** ofrecen una gama de funcionalidades adicionales, según las necesidades específicas. Estos módulos permiten adaptar y optimizar los servidores web para satisfacer mejor los requisitos específicos de cada caso.

## 4.5. Sitios web virtuales

#### Sitio virtual

**El concepto de sitio virtual surge para optimizar el uso de los servidores web,** **evitando que cada sitio web requiera un servidor físico individual. Si cada sitio web** **tuviera su propio servidor, se desperdiciaría gran parte de los recursos del servidor** **(memoria, CPU, etc.) resultando en una pérdida económica considerable.**

**Con la técnica de sitio virtual, un solo servidor web puede gestionar, alojar y atender** **las peticiones de varios sitios web independientes, conocidos como sitios virtuales.** **Esto permite aprovechar al máximo el potencial de los servidores web, almacenando** **tantos sitios virtuales como sea posible sin afectar el rendimiento.**

**Este término, también, se conoce como** *virtual host* **y es ampliamente utilizado por**

#### los proveedores de servicios de alojamiento web (hosting), que permiten a los

**usuarios de Internet alojar contenidos accesibles a través de la web, como páginas** **web y aplicaciones web.**

#### Cuando un servidor web aloja varios sitios virtuales, el conjunto de directorios, subdirectorios y archivos de todos estos sitios se denomina

**sitio web virtual.**

![Figura 6. Virtual Host en Apache. Fuente: Qué es virtual host en apache, 2017.](images/image-8.png)

*Figura 6. Virtual Host en Apache. Fuente: Qué es virtual host en apache, 2017.*

#### Tipos de sitios web virtuales (identificación)

#### Cuando un servidor web alberga varios

#### sitios virtuales, surge la necesidad de

**identificar cuál de estos sitios debe ser accedido en cada solicitud. Existen varias** **técnicas para la identificación de sitios virtuales, y a menudo se combinan para lograr** **una identificación precisa.**

#### Sitios virtuales basados en nombre

#### Esta técnica asocia diferentes FQDN (Fully Qualified Domain Name) o nombres al

**servidor web. Cada FQDN soporta un sitio virtual diferente. Por ejemplo, un acceso** **web con el FQDN X dirigirá a un sitio virtual específico, mientras que un acceso con** **el FQDN Y dirigirá a otro sitio virtual, aunque ambos estén en el mismo servidor web.** **Es la técnica más popular y requiere una correcta configuración de los servidores** **DNS que gestionan los nombres del servidor web.**

#### Sitios virtuales basados en puerto

**En este caso, la identificación se realiza mediante el puerto de acceso al servidor** **web. El protocolo HTTP define el puerto 80 como el predeterminado, pero se** **pueden utilizar otros puertos para diferentes sitios virtuales. Por ejemplo, un acceso**

Servicios en Red e Internet 21 Tema 4. Material de estudio **web al puerto 8080 dirigirá a un sitio virtual específico, mientras que el puerto 9090** **dirigirá a otro.**

**Esta técnica se combina frecuentemente con la identificación basada en nombres y** **requiere una correcta gestión de cortafuegos** *(firewalls)* **para evitar problemas de** **acceso.**

#### Sitios virtuales basados en dirección IP

**La identificación se realiza mediante la dirección IP utilizada en la solicitud web. Los** **servidores web que emplean esta técnica necesitan múltiples tarjetas de red o utilizar** **aliasing IP para asociar varias direcciones IP a una sola interfaz de red. Por ejemplo,** **una solicitud con la IP «xxx.xxx.xxx.xxx» dirigirá a un sitio virtual específico, mientras** **que con la IP «yyy.yyy.yyy.yyy» dirigirá a otro.**

**Aunque es la menos popular de las tres técnicas, es común en grandes servidores** **web que tienen múltiples interfaces de red para gestionar el tráfico.**

**El uso de sitios virtuales permite maximizar la eficiencia de los servidores web al**

#### permitir que un solo servidor gestione múltiples sitios. Esto se logra mediante técnicas de identificación basadas en nombres, puertos o direcciones IP y cada técnica tiene sus propias ventajas y aplicaciones en diferentes contextos. Los

**proveedores de** *hosting* **utilizan estas técnicas para ofrecer servicios de alojamiento** **web eficientes y económicos, permitiendo a los usuarios acceder a contenidos web** **de manera sencilla y efectiva.**

## 4.6. Acceso al servidor web

Cuando un usuario intenta acceder a un servidor web, puede pasar por **tres fases** diferentes: autenticación, autorización y control de acceso. No todos los servidores web requieren que los usuarios pasen por estas fases, dependiendo de las necesidades de seguridad del servidor. A continuación, se describen estas fases en detalle.

Autenticación

La autenticación es el proceso mediante el cual se **verifica la identidad del usuario** que intenta acceder al servidor web. Este proceso asegura que el usuario es quien dice ser, similar a cómo se verifica la identidad de una persona mediante un documento de identificación o huellas dactilares.

Métodos de autenticación comunes incluyen:

**▸ Anónima (predeterminada):** no se requiere nombre de usuario ni contraseña. Es común en accesos a zonas públicas de servidores web.

**▸ Básica:** utiliza un nombre de usuario y una contraseña sin cifrar. Es sencillo, pero inseguro, ya que las credenciales se transmiten en texto plano.

**▸ Digest:** similar a la autenticación básica, pero las credenciales están cifradas usando el algoritmo criptográfico MD5, ofreciendo mayor seguridad.

**▸ Otros métodos:** incluyen sistemas más avanzados que a menudo requieren un servidor de autenticación, como RADIUS, LDAP, etc.

Autorización

La autorización está estrechamente relacionada con la autenticación. Una vez que la identidad del usuario ha sido autenticada, se verifica si el usuario tiene **permiso para** **acceder al recurso** solicitado. Es similar a verificar si una persona tiene entrada a un evento después de comprobar su identidad.

Control de acceso

El control de acceso **gestiona** qué **dispositivos** pueden acceder al servidor web, independientemente de quién sea el usuario. Esta fase es crucial para bloquear dispositivos (como bots) que intentan acceder de manera malintencionada al servidor web.

Aunque es independiente de la autenticación y la autorización, combinar las tres fases proporciona una protección óptima al servidor web.

## 4.7. Referencias bibliográficas

Carrodeguas, N. (2024, septiembre 3). Como instalar y configurar el servidor web Apache en Windows. *Norfipc.* <https://norfipc.com/internet/instalar-servidorapache.html> Edgar. (2014, febrero 25). Arquitectura Cliente-Servidor (Dos capas). *Blog* *programación web.* [https://edgarbc.wordpress.com/dos-capas/](https://edgarbc.wordpress.com/dos-capas/) Fenollosa, A. (2023, noviembre 9). ¿Cuál es el mejor navegador web? 2024. *Programadores web Valencia.* <https://programadorwebvalencia.com/cual-es-el-mejornavegador-web-2024/> Qué es virtual host en apache. (2017). *Hostings one.* <https://hostings.one/que-esvirtual-host-en-apache>

Velasco, R. (2017, marzo 28). Encuentran una vulnerabilidad grave en el servidor web IIS de Windows. *Redes Zone.* [https://www.redeszone.net/2017/03/28/vulnerabilidad-servidor-web-iis-6/](https://www.redeszone.net/2017/03/28/vulnerabilidad-servidor-web-iis-6/)

# [https://www.hostinger.es/tutoriales/que-es-un-hosting](https://www.hostinger.es/tutoriales/que-es-un-hosting)

## ¿Qué es un hosting y cómo funciona?

Gustavo B. (2024 julio 24). ¿Qué es un hosting y cómo funciona? *Hostinger.* ¿Tienes nueve minutos? Es lo que vas a tardar en leer este completísimo artículo que te va a explicar todo lo relacionado con los *hostings.* ¿Sabes lo que es un *hosting?* ¿Sabes lo que cuesta? ¿y cómo funciona? No te quedes con dudas.

# ¿Qué es un servidor web? (2023, septiembre 14). IONOS Digital Guide.

# historia-y-programas/

## ¿Qué es un servidor web?

<https://www.ionos.es/digitalguide/servidores/know-how/servidor-web-definicion->

Aquí tendrás una explicación diferente de lo que es un servidor web y las soluciones de *software* libre que existen para servidores web y cuál sería el más adecuado para cada caso.

# (2024). Top 10. [https://www.top10.com/hosting/sp-comparison](https://www.top10.com/hosting/sp-comparison)

## Mejores servicios de alojamiento web de 2024

¿Qué son los servicios de alojamiento de sitios web y cuál es el indicado para ti? Si tienes intención de contratar un servidor web, este sitio te hace una comparativa de los mejores alojamientos valorando servicio, precio, ancho de banda, seguridad y disponibilidad. Incluso, te muestra sitios gratuitos para alojar tu sitio web.

# [https://www.hostinger.es/tutoriales/que-es-un-servidor-web](https://www.hostinger.es/tutoriales/que-es-un-servidor-web)

## ¿Qué es un servidor web y cómo funciona?

Betania V. (2024, mayo 22). ¿Qué es un servidor web y cómo funciona? *Hostinger.* Si dispones de seis minutos, te recomiendo que leas este artículo donde se explica cómo funciona un servidor web y cuáles son los más populares para que puedas decidir cuál es el más apropiado para tu instalación.

# [https://www.arsys.es/blog/que-es-apache-y-para-que-sirve](https://www.arsys.es/blog/que-es-apache-y-para-que-sirve)

## ¿Qué es Apache y para qué sirve?

García de Zúñiga, F. (2024, abril 4). ¿Qué es Apache y para qué sirve? *Arsys.* Si quieres utilizar un servidor web de código abierto puedes trabajar con el servidor Apache pudiéndolo instalar tanto en Windows como en entorno Linux. Por ello es importante que leas este artículo donde se explica sus principales características y cómo configurarlo.

# Alquila un servidor online y céntrate en lo importante. (s. f.). IONOS.

# [https://www.ionos.es/servidores/servidores](https://www.ionos.es/servidores/servidores)

## Alquila un servidor online y céntrate en lo importante

¿Qué es mejor un servidor cloud o un servidor dedicado? ¿Cuáles son las ventajas de alquilar un servidor en línea? Utiliza la virtualización para desarrollar tu modelo de negocio.

# Y o u T u b e . <https://www.youtube.com/watch?>

# v=TX1rWg8y9Xw&list=PLQ1o0rYO0QWtJzasUzysBjfL5g3ebsUn6

## Curso de servidores web gratis | zoneclass.com

Zoneclass. (2017, junio 26). *Curso de servidores web gratis | zoneclass.com* [Vídeo]. Curso muy completo con 44 lecciones para que puedas entender cómo funcionan los servidores web en diferentes entornos.

![image-9](images/image-9.png)

Accede al vídeo:

[https://www.youtube.com/embed/PLQ1o0rYO0QWtJzasUzysBjfL5g3ebsUn6](https://www.youtube.com/embed/PLQ1o0rYO0QWtJzasUzysBjfL5g3ebsUn6)

## Entrenamiento 1. Instalación y configuración de

## servicio DHCP en Windows

**▸ Planteamiento del ejercicio**

Se desea utilizar un servidor Windows Server como servidor Web para que sea capaz de ofrecer acceso a páginas web de diferentes sitios web virtuales.

Para ello puedes valerte de máquinas virtuales en un entorno virtual como VirtualBox.

**▸ Desarrollo paso a paso**

- Instalar la función propia de Microsoft (IIS7) pare que el servidor Windows Server pueda trabajar como servidor web.

- Comprobar que la función está instalada correctamente.

- ¿Cómo se configura dicha función?

- ¿Conoces alguna otra aplicación que pueda ser instalada en el servidor Windows Server para que este pueda funcionar como servidor web?

**▸ Solución**

Para configurar un servidor Windows Server como servidor web utilizando Internet Information Services (IIS), puedes seguir estos pasos. Además, mencionaremos algunas otras aplicaciones que se pueden instalar en un servidor Windows Server para habilitarlo como servidor web.

#### Instalación de IIS en Windows Server

**▸** Acceder al servidor Windows Server:

- Asegúrate de tener acceso a tu servidor Windows Server, ya sea físicamente o mediante una conexión remota.

**▸** Abrir el administrador del servidor:

- En el servidor, abre «Administrador del servidor» desde el menú de inicio o desde la barra de tareas.

**▸** Agregar roles y características:

- En «Administrador del servidor», selecciona la opción «Agregar roles y características».

- Aparecerá el «Asistente para agregar roles y características». Haz clic en «Siguiente» hasta llegar a la página «Seleccionar roles de servidor».

**▸** Seleccionar el rol de IIS:

- En la lista de roles de servidor, marca la casilla «Servidor web (IIS)».

- Al seleccionar este rol, se te pedirá que agregues las características necesarias para IIS. Acepta y haz clic en «Agregar características».

**▸** Seleccionar características adicionales (opcional):

- Puedes seleccionar características adicionales según tus necesidades. Por defecto, IIS viene con las configuraciones necesarias para funcionar como servidor web básico.

**▸** Continuar con la instalación:

- Haz clic en «Siguiente» hasta llegar a la página «Confirmar selecciones de instalación».

- Revisa tus selecciones y haz clic en «Instalar» para comenzar la instalación de IIS.

**▸** Finalizar la instalación:

- Una vez que se complete la instalación, haz clic en «Cerrar».

#### Comprobación de la instalación de IIS

**▸** Abrir un navegador web:

- En el mismo servidor donde instalaste IIS, abre un navegador web (por ejemplo, Microsoft Edge).

**▸** Acceder a la página de prueba de IIS: **•** Escribe <http://localhost> en la barra de direcciones y presiona «Enter».

- Si IIS se instaló correctamente, deberías ver la página de bienvenida predeterminada de IIS (IIS7 Welcome Page).

#### Configuración de IIS para alojar sitios web

**▸** Acceder al Administrador de IIS:

- Abre «Administrador de IIS» desde el menú de inicio o mediante «Administrador del Servidor» → «Herramientas» → «Administrador de Internet Information Services (IIS)».

**▸** Crear un nuevo sitio web:

- En el panel de conexiones a la izquierda, haz clic derecho en «Sitios» y selecciona «Agregar sitio web».

- Rellena los campos necesarios:

- Nombre del sitio: el nombre que deseas para el sitio.

- Ruta física: la ruta en el sistema de archivos donde se encuentran los archivos del sitio web.

- Dirección IP y puerto: generalmente, puedes dejarlo en «Sin asignar» y puerto 80 (para HTTP) o 443 (para HTTPS).

- Nombre de host: el nombre de dominio que deseas asociar con este sitio.

**▸** Configurar múltiples sitios web (sitios virtuales):

- Para alojar múltiples sitios web, necesitas configurar «Encabezados de host» (Host *Headers)* o asignar diferentes puertos o direcciones IP.

- Al agregar un nuevo sitio, puedes especificar un nombre de host (como www.ejemplo.com) que IIS utilizará para identificar el sitio.

**▸** Verificar la configuración:

- Asegúrate de que los archivos del sitio web estén en la ruta correcta y que el sitio esté iniciado.

- Puedes probar accediendo desde un navegador web usando la IP del servidor o el nombre de *host* configurado.

#### Otras aplicaciones para servidores web en Windows Server

Si bien IIS es la opción nativa de Microsoft para servidores web en Windows Server, existen otras aplicaciones que puedes utilizar:

**▸ Apache HTTP Server:** Apache es uno de los servidores web más populares en el mundo. Es de código abierto y puede ser instalado en Windows. Se prefiere,

Servicios en Red e Internet 36 Tema 4. Entrenamientos generalmente, en entornos que utilizan aplicaciones web desarrolladas en PHP, Python, o Ruby.

**▸ Nginx:** es otro servidor web de alto rendimiento que se puede utilizar en Windows Server. Es conocido por su eficiencia en el manejo de conexiones concurrentes y, también, puede actuar como proxy inverso y equilibrador de carga.

**▸ Tomcat:** Apache Tomcat es un servidor web y contenedor de servlets que se utiliza para ejecutar aplicaciones web Java. Es ideal para entornos que requieren soporte para JSP y servlets.

**▸ Node.js:** si estás trabajando con aplicaciones basadas en JavaScript del lado del servidor, puedes configurar un servidor Node.js en tu Windows Server para servir aplicaciones web.

#### Conclusión

Instalar y configurar IIS en Windows Server es una forma sencilla y eficaz de configurar un servidor web para múltiples sitios. Sin embargo, según tus necesidades específicas, también, puedes considerar otras aplicaciones como Apache, Nginx, Tomcat o Node.js para aprovechar diferentes funcionalidades y características.

## Entrenamiento 2. Instalación y configuración de

## servicio web en Ubuntu

**▸ Planteamiento del ejercicio** Se desea utilizar el servidor Ubuntu como servidor Web para que sea capaz de ofrecer acceso a páginas web de diferentes sitios web virtuales. Para ello puedes valerte de máquinas virtuales en un entorno virtual como VirtualBox.

**▸ Desarrollo paso a paso**

- Instalar la aplicación Apache2 en el servidor Ubuntu.

- Comprobar que la aplicación está instalada correctamente e indicar el PID del proceso de dicha aplicación.

- ¿Cómo se configura dicha aplicación?

- ¿Conoces alguna otra aplicación que pueda ser instalada en el servidor Ubuntu para que este pueda funcionar como servidor web?

**▸ Solución**

#### Instalar Apache2 en el servidor Ubuntu

Primero, debes actualizar el índice de paquetes y luego instalar Apache2:

![image-10](images/image-10.png)

#### Comprobar que Apache2 está instalado correctamente

Para verificar que Apache2 se ha instalado correctamente y está en ejecución:

![image-11](images/image-11.png)

Si Apache2 está funcionando correctamente, verás un mensaje indicando que el servicio está activo *(active/running).*

#### Obtener el PID del proceso de Apache2

Para encontrar el PID del proceso de Apache2:

![image-12](images/image-12.png)

Este comando te mostrará el PID del proceso principal de Apache2. Si el servicio tiene varios procesos (algo común en Apache debido a su naturaleza multiproceso), se mostrará una lista de PID.

#### Configurar Apache2 para manejar sitios web virtuales

Apache2 utiliza archivos de configuración para gestionar sitios virtuales. La configuración básica de un sitio virtual se realiza de la siguiente manera:

Paso 1. Crear los directorios para los sitios web:

**▸** Crea un directorio para cada sitio web que deseas servir. Supongamos que

queremos servir example.com y example2.com .

![image-13](images/image-13.png)

**▸** Luego, cambia la propiedad de estos directorios para que el usuario www-data (el usuario predeterminado bajo el cual Apache2 se ejecuta) tenga los permisos adecuados:

![image-14](images/image-14.png)

Paso 2. Crear archivos de configuración para los sitios virtuales: Apache2 tiene un directorio llamado /etc/apache2/sites-available/ donde se almacenan los archivos de configuración de los sitios virtuales.

**▸** Crea un archivo de configuración para example.com :

![image-15](images/image-15.png)

![▸ Dentro de este archivo, escribe lo siguiente:](images/image-16.png)

Repite el proceso para example2.com , cambiando los valores apropiados.

Paso 3. Habilitar los sitios virtuales:

**▸** Activa los sitios web virtuales utilizando a2ensite :

![image-17](images/image-17.png)

**▸** Luego, recarga Apache para aplicar los cambios:

![image-18](images/image-18.png)

Paso 4. Modificar el archivo hosts (opcional): si estás trabajando en un entorno de pruebas y no tienes un DNS configurado, puedes modificar el archivo hosts de tu máquina para resolver los nombres de dominio localmente:

![image-19](images/image-19.png)

**▸** Añade lo siguiente al archivo:

![image-20](images/image-20.png)

Ahora, cuando navegues a <http://example.com> o <http://example2.com> en tu navegador web, deberías ver el contenido de los directorios

/var/www/example.com/public_html y /var/www/example2.com/public_html , respectivamente.

#### Alternativas a Apache2 para servidor web en Ubuntu

Existen varias alternativas a Apache2 que puedes instalar y configurar en un servidor Ubuntu para que funcione como un servidor web:

**▸ Nginx:** es un servidor web muy popular conocido por su alto rendimiento y bajo consumo de recursos. Es excelente para manejar muchas conexiones simultáneas y es comúnmente utilizado como un proxy inverso. Instalación:

![image-21](images/image-21.png)

**▸ Lighttpd:** es un servidor web ligero y adecuado para servidores con limitaciones de recursos. Es menos común que Apache2 y Nginx, pero es una opción viable para ciertos casos de uso. Instalación:

![image-22](images/image-22.png)

**▸ Caddy:** es un servidor web moderno que tiene SSL/TLS integrado y configuraciones automáticas. Es más fácil de configurar para quienes buscan simplicidad en el despliegue de sitios web seguros. Instalación (requiere descargar desde su sitio web oficial o usar snap):

![image-23](images/image-23.png)

![image-24](images/image-24.png)

Cada una de estas alternativas tiene sus ventajas y casos de uso específicos. La elección del servidor web adecuado depende de tus necesidades particulares, como el rendimiento, la facilidad de configuración y la seguridad.

## Entrenamiento 3. Configuración particular de un

## servidor web con Windows

**▸ Planteamiento del ejercicio**

Se desea utilizar un servidor Windows Server como servidor Web para que sea capaz de ofrecer acceso a páginas web de diferentes sitios web virtuales:

El servidor web albergará dos sitios web virtuales con las siguientes características:

**▸** Sitio 1:

- El sitio web deberá ser accedido por el protocolo http mediante el nombre <www.weba.com> y utilizando el puerto por defecto.

- El documento predeterminado de este sitio web deberá ofrecer una imagen en el navegador del cliente similar a la que se indica a continuación:

**▸** Sitio 2:

![image-25](images/image-25.png)

- El sitio web deberá ser accedido por el protocolo http mediante el nombre <www.webb.com> y utilizando el puerto por defecto.

- El documento predeterminado de este sitio web deberá ofrecer una imagen en el navegador del cliente similar a la que se indica a continuación:

![image-26](images/image-26.png)

Será necesario verificar el correcto funcionamiento del servidor. Para ello utilizan un navegador web en el cliente Ubuntu y realiza accesos a los sitios web configurados en el servidor. Modifica los dos sitios web anteriores para que ahora se conecten por los puertos:

**▸** Web A: puerto 9999.

**▸** Web B: puerto 3231. Utilizando un navegador web en el cliente Ubuntu realiza accesos a los sitios web configurados en el servidor y comprobar que funcionan correctamente. Ahora este servidor tendrá una única interfaz de red, pero mediante la técnica de IP Aliasing deberá tener asociadas dos direcciones IP (192.168.100.100 y 192.168.100.200). Cada uno de los sitios web anteriormente creados serán accesibles por una de estas IP.

**▸** Sitio A por la IP 192.168.10.10 **▸** Sitio B por la IP 192.168.10.20 Para concluir será necesario verificar el correcto funcionamiento del servidor. Para ello, utilizando un navegador web en el cliente Ubuntu, realiza accesos a los sitios web configurados en el servidor.

**▸ Desarrollo paso a paso**

- Instalación y configuración de IIS (Internet Information Services).

**•** Configuración del primer sitio web (www.weba.com).

**•** Configuración del segundo sitio web (www.webb.com).

- Verificación del funcionamiento inicial.

- Configuración de nuevos puertos.

- Configuración de IP Aliasing.

**▸ Solución**

#### Instalación y Configuración de IIS (Internet Information Services)

Instalar IIS: **▸** Accede al «Administrador del Servidor» en Windows Server. **▸** Haz clic en «Agregar roles y características». **▸** Selecciona «Instalación basada en características o en roles». **▸** Elige el servidor de destino. **▸** En la lista de roles, selecciona «Servidor web (IIS)». **▸** Sigue las instrucciones para completar la instalación. Configurar los sitios web virtuales: **▸** Abre el «Administrador de IIS». **▸** Expande el nombre de tu servidor en el panel izquierdo. **▸** Haz clic derecho en «Sitios» y selecciona «Agregar sitio web». **Configuración del primer sitio web (<www.weba.com>)** Crear el sitio web (Sitio 1): **▸** En el «Administrador de IIS», selecciona «Agregar sitio web».

**▸** Nombre del sitio: Sitio 1.

**▸** Ruta física: crea una carpeta en C:\inetpub\wwwroot\weba .

**▸** Dirección IP: no asignada.

**▸** Puerto: 80 (por defecto).

**▸** Nombre del *host:* <www.weba.com>.

**▸** Clic en «Aceptar».

Configurar el documento predeterminado:

**▸** Dentro del directorio C:\inetpub\wwwroot\weba , crea un archivo index.html .

**▸** El contenido HTML del archivo debería incluir una imagen:

![image-27](images/image-27.png)

**Configuración del segundo sitio web (<www.webb.com>)**

Crear el sitio web (Sitio 2):

**▸** Repite los pasos anteriores para crear un segundo sitio.

**▸** Nombre del sitio: Sitio 2.

**▸** Ruta física: crea una carpeta en C:\inetpub\wwwroot\webb .

**▸** Dirección IP: no asignada.

**▸** Puerto: 80 (por defecto).

**▸** Nombre del *host:* <www.webb.com>.

**▸** Clic en «Aceptar».

Configurar el documento predeterminado:

**▸** Dentro del directorio C:\inetpub\wwwroot\webb , crea un archivo index.html .

**▸** El contenido HTML del archivo debería incluir una imagen:

![Verificación del funcionamiento inicial](images/image-28.png)

Configurar el archivo de hosts en el cliente Ubuntu:

**▸** Edita el archivo /etc/hosts en la máquina cliente Ubuntu para apuntar los nombres de

![▸ Añade las siguientes líneas: ▸ Guarda y cierra el archivo.](images/image-29.png)

los sitios web a la dirección IP del servidor:

**▸** Acceder a los sitios web: abre un navegador en Ubuntu y accede a <http://www.weba.com> y <http://www.webb.com> para verificar que ambos sitios funcionan correctamente.

#### Configuración de nuevos puertos

Cambiar los puertos de los sitios web:

**▸** En el «Administrador de IIS», selecciona «Sitio 1».

**▸** Haz clic en «Configuración avanzada» y cambia el puerto a 9999.

**▸** Repite el proceso para Sitio 2, cambiando el puerto a 3231.

Verificación en Ubuntu: en el cliente Ubuntu, accede a los sitios web utilizando los nuevos puertos:

**▸** <http://www.weba.com:9999>

**▸** <http://www.webb.com:3231>

#### Configuración de IP Aliasing

Configurar IP Aliasing en Windows Server:

**▸** Abre la consola de comandos en Windows Server con privilegios de administrador.

**▸** Agrega las direcciones IP secundarias con los siguientes comandos:

![image-30](images/image-30.png)

Asignar IP a los sitios web:

**▸** En el «Administrador de IIS», edita la configuración de Sitio1:

- Cambia la IP a 192.168.100.100 y deja el puerto en 9999.

- Haz lo mismo para Sitio2, asignando la IP 192.168.100.200 y el puerto 3231.

Verificación Final en Ubuntu:

**▸** Modifica el archivo /etc/hosts en Ubuntu para reflejar las nuevas IP:

![image-31](images/image-31.png)

**▸** Accede a los sitios utilizando las nuevas IP y puertos:

**•** <http://192.168.100.100:9999>

**•** <http://192.168.100.200:3231>

#### Conclusión

Estos pasos permiten configurar un servidor Windows Server como un servidor web con IIS, que alberga dos sitios web virtuales accesibles a través de diferentes nombres de host, puertos, y direcciones IP. Al seguir las instrucciones, podrás verificar que los sitios funcionan correctamente desde un cliente Ubuntu.

## Entrenamiento 4. Autenticación, autorización y

## control de acceso de un servidor Web con Windows

**▸ Planteamiento del ejercicio**

Se desea utilizar un servidor Windows Server como servidor web utilizando IIS. Los usuarios de este servidor deberán pasar por un proceso de autorización después de presentar sus credenciales en un proceso de autenticación básica antes de acceder a dicho servidor.

Por otro lado, el servidor web albergará un único sitio web virtual con las siguientes características:

Sitio virtual:

**▸** El sitio web deberá ser accedido por el protocolo http, utilizando la dirección IP 192.168.200.11, el nombre <www.autorizacion.org> y utilizando el puerto por defecto.

**▸** El documento predeterminado de este sitio web deberá ofrecer una imagen en el navegador del cliente similar a la que se indica a continuación:

![image-32](images/image-32.png)

**▸** A continuación, se crearán en el sistema los tres usuarios estándar con las siguientes características:

- nombre de usuario: Alfonso. Password: User1.

- nombre de usuario: María. Password: User2.

- nombre de usuario: Manolo. Password: User3.

**▸** Configurar IIS para que pueda implementar un proceso de autenticación básica en el sitio web creado anteriormente.

**▸** Configurar el proceso de autorización para definir que únicamente los usuarios Alfonso y Manolo puedan acceder al servidor web. Para realizar la comprobación del correcto funcionamiento sitio virtual creado, realiza un acceso web mediante un navegador del cliente Ubuntu utilizando los usuarios creados en el sistema. Verifica quién puede acceder y quién no.

**▸** Configurar el servidor web para ejercer un control de acceso que únicamente deba permitir el acceso al servidor web a todos los usuarios que realicen un acceso desde dispositivos cuya tarjeta de red tenga la dirección IP 192.168.200.3 o 192.168.200.220.

**▸** Para realizar la comprobación del correcto funcionamiento sitio virtual creado, realizad un acceso web mediante un navegador del cliente Ubuntu verificando con qué direcciones IP se puede acceder.

**▸ Desarrollo paso a paso**

- Paso 1. Instalación de IIS en Windows Server.

- Paso 2. Configuración del sitio web virtual.

- Paso 3. Creación de usuarios estándar.

- Paso 4. Configuración de autenticación básica en IIS.

- Paso 5. Configuración del proceso de autorización.

- Paso 6. Configuración del control de acceso basado en IP.

- Paso 7. Verificación del funcionamiento.

**▸ Solución**

#### Paso 1. Instalación de IIS en Windows Server

**▸** Abrir el Administrador del servidor (Server Manager):

- Haz clic en «Inicio» y selecciona «Administrador del servidor».

**▸** Agregar roles y características:

- En el administrador del servidor, selecciona «Agregar roles y características».

- Sigue el asistente hasta llegar a la selección de roles.

- Marca «Servidor Web (IIS)» y sigue las instrucciones para completar la instalación.

#### Paso 2. Configuración del sitio web virtual

**▸** Abrir el Administrador de IIS:

- En el Administrador del servidor, selecciona «Herramientas» y luego «Administrador de Internet Information Services (IIS)».

**▸** Crear un nuevo sitio web. En el Administrador de IIS, haz clic derecho en «Sitios» y selecciona «Agregar sitio web». Configura el sitio con los siguientes detalles: **•** Nombre del sitio <www.autorizacion.org>.

- Ruta física: selecciona o crea una carpeta en el servidor donde se almacenarán los archivos del sitio.

- Dirección IP: 192.168.200.11

- Puerto: 80 (por defecto para HTTP).

**•** Nombre de host: <www.autorizacion.org>

**▸** Establecer el documento predeterminado:

- En el administrador de IIS, selecciona el sitio recién creado.

- En la sección «Documentos predeterminados», asegúrate de que el archivo de la imagen (por ejemplo, index.html o default.html ) esté listado.

- Crea un archivo HTML sencillo en la ruta física del sitio que muestre la imagen deseada.

#### Paso 3. Creación de usuarios estándar

**▸** Abrir el Administrador de usuarios y grupos locales:

- En el Administrador del servidor, selecciona «Herramientas» y luego «Usuarios y equipos de Active Directory» o «Usuarios y grupos locales», dependiendo de tu configuración.

**▸** Crear los usuarios:

- Crea los usuarios Alfonso, María y Manolo con las contraseñas User1, User2 y User3 respectivamente.

- Asegúrate de que las cuentas están habilitadas.

#### Paso 4. Configuración de autenticación básica en IIS

**▸** Habilitar autenticación básica: **•** En el Administrador de IIS, selecciona el sitio <www.autorizacion.org>.

- En la sección «Autenticación», deshabilita «Autenticación Anónima» y habilita «Autenticación Básica».

**▸** Configurar las credenciales:

- Asegúrate de que los usuarios creados anteriormente estén autorizados a autenticarse.

#### Paso 5. Configuración del proceso de autorización

**▸** Configurar las reglas de autorización:

- En el administrador de IIS, selecciona el sitio y luego «Autorización de solicitudes».

- Agrega una regla que permita el acceso solo a los usuarios Alfonso y Manolo.

- Añade otra regla que deniegue el acceso a todos los demás usuarios.

#### Paso 6. Configuración del control de acceso basado en IP

**▸** Agregar restricciones de IP:

- En el Administrador de IIS, selecciona el sitio y luego «Restricciones de dirección IP y dominios».

- Agrega las direcciones IP 192.168.200.3 y 192.168.200.220 como direcciones permitidas.

- Configura la regla predeterminada para denegar el acceso a todas las demás direcciones IP.

#### Paso 7. Verificación del funcionamiento

**▸** Acceder desde un navegador en Ubuntu:

- En el cliente Ubuntu, abre un navegador web.

**•** Accede al sitio utilizando la dirección <http://www.autorizacion.org>.

- Prueba el acceso con cada uno de los usuarios para verificar que Alfonso y Manolo pueden acceder, mientras que María no.

**▸** Verificación de acceso según IP:

- Modifica la configuración de red del cliente Ubuntu para que tenga las direcciones IP 192.168.200.3 y 192.168.200.220 y prueba el acceso al sitio.

- Verifica que solo puedas acceder al sitio desde esas IP.

Siguiendo estos pasos, deberías tener un servidor web IIS configurado en Windows Server que requiera autenticación básica, restrinja el acceso basado en usuarios específicos y que solo permita el acceso desde ciertas direcciones IP.

## Entrenamiento 5. Autenticación, autorización y control de acceso de un servidor Web con Ubuntu

**▸ Planteamiento del ejercicio**

Se desea utilizar un servidor Ubuntu como servidor web utilizando Apache. Los usuarios de este servidor deberán pasar por un proceso de autorización después de presentar sus credenciales en un proceso de autenticación básica antes de acceder a dicho servidor.

Por otro lado, el servidor web albergará un único sitio web virtual con las siguientes características:

**▸** Sitio virtual 1:

- El sitio web deberá ser accedido por el protocolo http, utilizando la dirección IP 192.168.3.33, el nombre <www.autorizacion.es> y utilizando el puerto por defecto.

- El documento predeterminado de este sitio web deberá ofrecer una imagen en el navegador del cliente similar a la que se indica a continuación:

![image-33](images/image-33.png)

**▸** Sitio virtual 2:

- El sitio web deberá ser accedido por el protocolo http, utilizando la dirección IP 192.168.5.55, el nombre <www.equipos.ai> y utilizando el puerto por defecto.

- El documento predeterminado de este sitio web deberá ofrecer una imagen en el navegador del cliente similar a la que se indica a continuación:

![image-34](images/image-34.png)

Configurar DNS para que desde el equipo cliente se pueda acceder a dichos sitios como <www.autorizacion.es> y <www.equipos.ai>.

**▸** Comprobar el funcionamiento de los dos sitios virtuales. Crear en el servidor Ubuntu 3 usuarios estándar con las siguientes características:

**▸** nombre de usuario: Ubuntu1 password: Usuario1 **▸** nombre de usuario: Ubuntu2 password: Usuario1 **▸** nombre de usuario: Ubuntu3 password: Usuario1 Configurar apache para que pueda implementar un proceso de autenticación básica en el sitio web <www.autorizacion.es>. Configurar el proceso de autorización para definir que únicamente los usuarios Usuario 2 y Usuario 3 puedan acceder al servidor web. Configurar el servidor web para ejercer un control de acceso que únicamente deba permitir el acceso al servidor web a todos los usuarios que realicen un acceso desde dispositivos cuya tarjeta de red tenga la dirección IP 192.168.1.11 o 192.168.1.22 en el sitio <www.equipos.ai>.

**▸** Realizar comprobaciones cambiando la IP del equipo cliente para asegurarse que el control por IP es correcto. Configurar el servidor web para que pueda almacenar información sobre las solicitudes recibidas por el mismo y para almacenar información sobre las solicitudes que han acabado en error. ¿Dónde se almacenan por defecto estos registros de eventos?

**▸** Comprobamos que se hayan creado los registros de eventos en el lugar configurado.

**▸ Desarrollo paso a paso**

- Instalar Apache en el servidor Ubuntu.

- Configuración de los sitios virtuales en Apache.

- Configuración del DNS.

- Crear usuarios en Ubuntu.

**•** Configurar la autenticación básica en Apache para <www.autorizacion.es>.

**•** Configurar control de acceso por IP en <www.equipos.ai>.

**▸ Solución**

#### Instalar Apache en el Servidor Ubuntu

Antes de comenzar, asegúrate de que tu servidor Ubuntu esté actualizado y que

Apache esté instalado.

![image-35](images/image-35.png)

#### Configuración de los sitios virtuales en Apache

Sitio virtual 1: <www.autorizacion.es>

**▸** Crear el directorio para el sitio web:

![image-36](images/image-36.png)

**▸** Asignar permisos apropiados:

![image-37](images/image-37.png)

**▸** Crear un archivo HTML simple con una imagen:

![image-38](images/image-38.png)

![image-39](images/image-39.png)

**▸** Crear la configuración del sitio virtual en Apache:

![image-40](images/image-40.png)

![▸ Contenido del archivo: ▸ Habilitar el sitio web: Sitio Virtual 2: <www.equipos.ai> ▸ Crear el directorio para el sitio web:](images/image-41.png)

![image-42](images/image-42.png)

**▸** Asignar permisos apropiados:

![image-43](images/image-43.png)

**▸** Crear un archivo HTML simple con una imagen:

![image-44](images/image-44.png)

![image-45](images/image-45.png)

**▸** Crear la configuración del sitio virtual en Apache:

![Contenido del archivo: ▸ Habilitar el sitio web: Configuración del DNS](images/image-46.png)

Para que las direcciones <www.autorizacion.es> y <www.equipos.ai> sean accesibles, debes configurarlas en el archivo /etc/hosts del servidor y de los equipos clientes o configurar un servidor DNS.

**▸** En el servidor y en los clientes, agrega lo siguiente al archivo /etc/hosts:

![image-47](images/image-47.png)

![Crear usuarios en Ubuntu Crear los tres usuarios en el servidor Ubuntu:](images/image-48.png)

**Configurar la autenticación básica en Apache para <www.autorizacion.es>**

**▸** Instalar la utilidad htpasswd :

![image-49](images/image-49.png)

**▸** Crear un archivo .htpasswd para la autenticación:

![image-50](images/image-50.png)

**▸** Modificar la configuración del sitio <www.autorizacion.es>:

![image-51](images/image-51.png)

**▸** Agrega lo siguiente dentro del bloque <VirtualHost> :

![▸ Recargar Apache para aplicar los cambios:](images/image-52.png)

![image-53](images/image-53.png)

**Configurar control de acceso por IP en <www.equipos.ai>** **▸** Modificar la configuración del sitio `www.equipos.ai`:

![image-54](images/image-54.png)

**▸** Agrega lo siguiente dentro del bloque <VirtualHost> :

![▸ Recargar Apache para aplicar los cambios:](images/image-55.png)

![image-56](images/image-56.png)

#### Configurar el registro de eventos en Apache

Apache por defecto almacena los registros en los siguientes archivos:

**▸** Registros de acceso: </var/log/apache2/access.log> **▸** Registros de errores: </var/log/apache2/error.log> Si quieres que los registros se almacenen en ubicaciones diferentes, puedes modificar las rutas en las configuraciones de los sitios virtuales:

![image-57](images/image-57.png)

Finalmente, comprobar que los registros se están creando:

![image-58](images/image-58.png)

Donde:

**▸** tail -f :

- tail : muestra las últimas líneas de un archivo. Por defecto, muestra las últimas diez líneas.

- -f : activa el modo follow (seguimiento), que permite ver en tiempo real las nuevas líneas que se añaden al archivo mientras sigue ejecutándose. Es útil para monitorizar registros en vivo.

**▸** /var/log/apache2/access.log : es el archivo de registro de acceso de Apache. Este archivo almacena información sobre cada solicitud realizada al servidor web, como la dirección IP del cliente, la fecha y hora de la solicitud, el recurso solicitado, y el código de estado HTTP.

**▸** /var/log/apache2/error.log : el archivo de registro de errores de Apache. Este archivo contiene mensajes de error generados por Apache, incluyendo problemas de configuración, fallos en la ejecución de *scripts,* o cualquier otro tipo de error relacionado con el servidor web.

#### Comprobaciones

**▸** Acceder a <www.autorizacion.es>: desde un navegador, intenta acceder a <http://www.autorizacion.es> y verifica que se solicite autenticación.

**▸** Acceder a <www.equipos.ai>: desde un navegador, intenta acceder a <http://www.equipos.ai> desde las IP permitidas y otras IP para comprobar el control de acceso.

**▸** Verificar registros de eventos: asegúrate de que los accesos y errores se registren correctamente.

Con esto, habrás configurado el servidor Ubuntu con Apache según los requisitos indicados.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–25)*
- A fondo  *(pp.26–32)*
- Entrenamientos  *(pp.33–64)*
- Servicios en Red e Internet 7 Tema 4. Material de estudio · Servicios en Red e Internet 8 Tema 4. Material de estudio · Servicios en Red e Internet 9 Tema 4. Material de estudio · Servicios en Red e Internet 10 Tema 4. Material de estudio · Servicios en Red e Internet 11 Tema 4. Material de estudio · Servicios en Red e Internet 12 Tema 4. Material de estudio · Servicios en Red e Internet 13 Tema 4. Material de estudio · Servicios en Red e Internet 14 Tema 4. Material de estudio · Servicios en Red e Internet 15 Tema 4. Material de estudio · Servicios en Red e Internet 16 Tema 4. Material de estudio · Servicios en Red e Internet 17 Tema 4. Material de estudio · Servicios en Red e Internet 18 Tema 4. Material de estudio · Servicios en Red e Internet 19 Tema 4. Material de estudio · Servicios en Red e Internet 20 Tema 4. Material de estudio · Servicios en Red e Internet 22 Tema 4. Material de estudio · Servicios en Red e Internet 23 Tema 4. Material de estudio · Servicios en Red e Internet 24 Tema 4. Material de estudio · Servicios en Red e Internet 25 Tema 4. Material de estudio  *(pp.7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 22, 23, 24, 25)*
- Servicios en Red e Internet 26 Tema 4. A fondo · Servicios en Red e Internet 27 Tema 4. A fondo · Servicios en Red e Internet 28 Tema 4. A fondo · Servicios en Red e Internet 29 Tema 4. A fondo · Servicios en Red e Internet 30 Tema 4. A fondo · Servicios en Red e Internet 31 Tema 4. A fondo · Servicios en Red e Internet 32 Tema 4. A fondo  *(pp.26–32)*
- Servicios en Red e Internet 33 Tema 4. Entrenamientos · Servicios en Red e Internet 34 Tema 4. Entrenamientos · Servicios en Red e Internet 35 Tema 4. Entrenamientos · Servicios en Red e Internet 37 Tema 4. Entrenamientos · Servicios en Red e Internet 38 Tema 4. Entrenamientos · Servicios en Red e Internet 39 Tema 4. Entrenamientos · Servicios en Red e Internet 40 Tema 4. Entrenamientos · Servicios en Red e Internet 41 Tema 4. Entrenamientos · Servicios en Red e Internet 42 Tema 4. Entrenamientos · Servicios en Red e Internet 43 Tema 4. Entrenamientos · Servicios en Red e Internet 44 Tema 4. Entrenamientos · Servicios en Red e Internet 45 Tema 4. Entrenamientos · Servicios en Red e Internet 46 Tema 4. Entrenamientos · Servicios en Red e Internet 47 Tema 4. Entrenamientos · Servicios en Red e Internet 48 Tema 4. Entrenamientos · Servicios en Red e Internet 49 Tema 4. Entrenamientos · Servicios en Red e Internet 50 Tema 4. Entrenamientos · Servicios en Red e Internet 51 Tema 4. Entrenamientos · Servicios en Red e Internet 52 Tema 4. Entrenamientos · Servicios en Red e Internet 53 Tema 4. Entrenamientos · Servicios en Red e Internet 54 Tema 4. Entrenamientos · Servicios en Red e Internet 55 Tema 4. Entrenamientos · Servicios en Red e Internet 56 Tema 4. Entrenamientos · Servicios en Red e Internet 57 Tema 4. Entrenamientos · Servicios en Red e Internet 58 Tema 4. Entrenamientos · Servicios en Red e Internet 59 Tema 4. Entrenamientos · Servicios en Red e Internet 60 Tema 4. Entrenamientos · Servicios en Red e Internet 61 Tema 4. Entrenamientos · Servicios en Red e Internet 62 Tema 4. Entrenamientos · Servicios en Red e Internet 63 Tema 4. Entrenamientos · Servicios en Red e Internet 64 Tema 4. Entrenamientos  *(pp.33, 34, 35, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64)*