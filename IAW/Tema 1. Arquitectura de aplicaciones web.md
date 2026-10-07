## Tema 1

# Implantación de Aplicaciones Web

# Tema 1. Arquitectura de

# aplicaciones web

# Índice

Esquema Material de estudio

## 1.1. Introducción y objetivos

## 1.2. Aplicaciones web vs. de escritorio

## 1.3. Arquitectura de dos niveles

## 1.4. Arquitectura de tres niveles

1.5 Protocolos de aplicación más usados A fondo IoT: protocolos de comunicación, ataques y recomendaciones Arquitectura de la aplicación Dspace Latencia de red Entrenamientos

Entrenamiento 1

Entrenamiento 2

Entrenamiento 3

Entrenamiento 4

Entrenamiento 5

# Esquema

![image-1](images/image-1.png)

Implantación de Aplicaciones Web 3 Tema 1. Esquema

# 1.1. Introducción y objetivos

En este tema nos vamos a familiarizar con las aplicaciones web. Veremos la diferencia entre las aplicaciones web y las de escritorio. Veremos sus ventajas e inconvenientes y conoceremos los diferentes tipos de arquitecturas y protocolos más utilizados. Los objetivos son:

**▸** Conocer los diferentes conceptos relacionados con la web.

**▸** Conocer los diferentes tipos de arquitectura.

**▸** Entender la diferencia entre la arquitectura de dos niveles y la de tres.

**▸** Conocer los protocolos de aplicación más usados.

# 1.2. Aplicaciones web vs. de escritorio

Una aplicación es un *software* que permite al usuario realizar una determinada tarea o servicio. Las aplicaciones de escritorio se

crean en lenguajes que ponen a

disposición del programador todas las capacidades de la computadora, mientras que una aplicación web, simplemente, es una aplicación creada para ser ejecutada por un navegador. El *hardware* queda oculto al usuario, que solo ve la capa de trabajo que le cede el navegador.

Hoy en día, las aplicaciones web son las aplicaciones más populares, ya que todos los usuarios actuales utilizan navegadores como Google Chrome, Edge, Firefox y Opera, entre otros, para navegar por Internet y están muy acostumbrados a trabajar con ellos.

Una aplicación web, en principio, es menos potente que una aplicación de escritorio, al no poder optimizar su código para la máquina en la que se está ejecutando. Las aplicaciones de escritorio pueden acceder a todo el *hardware* de la computadora y, por ello, optimizar su rapidez y prestaciones.

Las aplicaciones web dependen de la capacidad del navegador para manejar el *hardware* de la máquina en la que reside. Estas aplicaciones se crean en HTML y sus tecnologías asociadas (CSS, JavaScript).

![Figura 1. Ventajas de las aplicaciones web. Fuente: elaboración propia.](images/image-2.png)

*Figura 1. Ventajas de las aplicaciones web. Fuente: elaboración propia.*

Si las aplicaciones web han triunfado sobre las tradicionales aplicaciones de escritorio es por sus **ventajas,** las cuales se enumeran a continuación:

**▸ Gran compatibilidad.** Funcionan en todo tipo de sistemas, tanto de escritorio como sistemas móviles. Lo único que requieren es la presencia de un navegador, requisito fácil de cumplir ya que los navegadores se incluyen en cualquier dispositivo, sea del tipo que sea. En las aplicaciones de escritorio existe el problema de que, por ejemplo, una aplicación creada para Windows normalmente no funcionará en un entorno Linux. Aunque hay soluciones de virtualización de aplicaciones para solucionar este problema, lo cierto es que siempre es más fácil utilizar aplicaciones web.

**▸ Requisitos mínimos en el cliente.** El único requisito de las aplicaciones web es el navegador, las aplicaciones de escritorio exigen un sistema operativo concreto, una determinada cantidad de memoria RAM, instalación de ciertas plataformas, paquetes o servicios. Es verdad que a veces las aplicaciones web exigen determinados navegadores o bien ciertos *plugins* en ellos, pero disponiendo de un navegador de

Implantación de Aplicaciones Web 6 Tema 1. Material de estudio última generación (teniendo en cuenta que todos son gratuitos y que los *smartphones* ya los incorporan) una aplicación web bien hecha no debería requerir nada más.

**▸ Fácil manejo para los usuarios.** El entorno de trabajo (es decir, el navegador) es conocido por los usuarios, por lo que les es más fácil manejar una aplicación web, ya que cualquier usuario actual está acostumbrado a recorrer páginas web con su navegador.

**▸ Facilidad de mantenimiento.** Quizás es el aspecto más importante. Cuando una aplicación de escritorio se renueva, el usuario necesita actualizarla en su equipo. Todos los usuarios de Windows estamos acostumbrados a las periódicas actualizaciones del sistema que resultan enormemente pesadas por el tiempo de espera que suponen. Las aplicaciones web también se actualizan, pero solo en el servidor en el que se alojan. En cuanto se actualiza allí, todos los usuarios verán la última versión la próxima vez que accedan a ella, sin tener que instalar nada en su máquina. Por otro lado, tendremos la seguridad de saber qué versión de la aplicación poseen los usuarios. En las aplicaciones de escritorio dependemos de si el usuario instala o no la última versión. En las aplicaciones de escritorio, si hay fallos, por ejemplo, de seguridad que se detectan en una versión, el correspondiente parche a aplicar depende de que los usuarios lo instalen; fácilmente habría versiones inseguras de la aplicación, ya que no todos los usuarios habrían instalado ese parche. En una aplicación web, el parche se instalaría e instantáneamente todos los usuarios accederían a la versión segura de la aplicación.

**▸ Datos centralizados.** Los datos que maneja una aplicación web se encuentran en un único almacén o base de datos. Lo que facilita su mantenimiento y administración. El usuario, además, se despreocupa de estas tareas.

**▸ No requieren instalación.** El proceso de instalar algunas aplicaciones de escritorio es, a veces, largo, tedioso y difícil. Una aplicación web no requiere instalación, es simplemente un servicio accesible desde Internet a través del navegador.

**▸ Costes reducidos en implantación.** No hay material de instalación, ni impreso ni cajas de producto. Todo lo relacionado con la aplicación es digital. Hoy en día, las propias aplicaciones de escritorio utilizan, en gran medida, esta idea al poderse comprar y descargar desde Internet.

**▸ Accesibles desde diferentes dispositivos y ubicaciones.** De cara al usuario es la gran ventaja. Las aplicaciones de escritorio cuentan con una gran tarea, el hecho de que si cambio de dispositivo tengo que instalar en la aplicación, lo que implica, además, tener permisos de usuario o administrador para realizar esta labor, además de que las licencias de uso suelen estar restringidas a un número concreto de dispositivos. Cada vez es más habitual que los usuarios utilicen distintos dispositivos para trabajar: puesto de trabajo, portátil personal, tableta, smartphone.

Las aplicaciones web son accesibles desde cualquier dispositivo y desde cualquier parte del mundo siempre que tengamos conexión a Internet. La idea es muy diferente: si es una aplicación de pago, se paga por el uso (pagará cada usuario) y no por el número de dispositivos desde los que se accede a ellas.

Pero las aplicaciones web también tienen sus **inconvenientes.** A continuación, se describen los cinco principales:

![Figura 2. Desventajas de las aplicaciones web. Fuente: elaboración propia.](images/image-3.png)

*Figura 2. Desventajas de las aplicaciones web. Fuente: elaboración propia.*

**▸ Menos potentes.** No todas las tareas se pueden realizar desde una aplicación web, o al menos no con la misma eficiencia y velocidad. Por ejemplo, este manual está creado con la aplicación Adobe InDesign, que es un *software* de maquetación de documentos. De este *software* se requiere que manipule, coloque y edite con rapidez textos, imágenes, formas. Para ello exprime la potencia del ordenador en el que se instala: es más, una aplicación de este tipo no se puede instalar en cualquier ordenador, tiene requisitos muy altos. Lo mismo ocurre con un juego de última generación, que requerirá renderizar escenarios y música de gran calidad a tiempo real. Esto no está al alcance (al menos por ahora) de los navegadores. Sin ir tan lejos, es fácil percibir que es más grata la experiencia de escribir un documento en un procesador de textos instalado en el ordenador (como Microsoft Word, por ejemplo) que hacer la misma tarea en un procesador de textos *online* (como Office 365, por ejemplo).

**▸ No aprovechan al 100 % el** ***hardware.*** Tiene clara relación con la desventaja anterior. El hecho de tener un mejor o peor ordenador no influye apenas en el rendimiento de una aplicación web. Evidentemente, esto es una ventaja para los usuarios de ordenadores menos potentes, pero significa que no se está aprovechando debidamente el rendimiento que pueden proporcionar los ordenadores más veloces y se infrautiliza la inversión que el usuario hizo en la compra de su máquina.

**▸ Requieren conectividad.** Es decir, debemos estar conectados a Internet de forma ininterrumpida para utilizar la aplicación web. Hoy en día no parece un requisito excesivo, pero lo cierto es que no siempre funciona una conexión a Internet y este hecho podría paralizar la realización de una tarea importante. Esta es la razón por la que la conectividad de las empresas a Internet se ha convertido en una cuestión tan crítica, porque se requiere de enlaces red undantes dentro de su red interna, así como de la posibilidad de utilizar diversas (y también redundantes) conexiones a Internet.

**▸ Mas complejas a la hora de desarrollarlas.** No es difícil crear una simple página web con HTML y CSS; pero una aplicación de escritorio en general es más fácil de crear que una aplicación web, por el hecho de que en una aplicación web hay muchos más elementos dinámicos. La depuración es compleja en el caso de las aplicaciones web, ya que debemos esperar respuestas a peticiones del servidor, las cuales se consiguen tras realizar numerosos procesos en diversos lenguajes. Se agrava esta circunstancia por el hecho de que crecen las exigencias de los usuarios hacia las aplicaciones web, lo que fuerza al desarrollador de la aplicación a incorporar cada vez más elementos, esto dificulta el mantenimiento. No obstante, también aparecen continuamente nuevas herramientas que facilitan este trabajo, porque hoy en día disponen de una miríada de herramientas para producir, mantener, codificar, testar, simular, etc.

**▸ Delegación del control de nuestra información.** Probablemente sea la cuestión más ignorada por los usuarios de las aplicaciones web y, sin embargo, la que tiene implicaciones más importantes. Cuando una persona maneja una aplicación de escritorio para escribir un documento, este, por lo general, se almacena en nuestra máquina. Las cuestiones sobre dónde lo almacenamos, hacer sus copias de seguridad, quién tiene acceso, etc., recaen sobre nosotros mismos, es nuestra responsabilidad. En una aplicación web, normalmente, los datos se almacenan en Internet y los gestiona la empresa creadora de la aplicación. Eso supone que no necesitamos preocuparnos por las cuestiones anteriores sobre nuestros datos; pero, a la vez, significa que dependemos de las buenas prácticas que la empresa propietaria de la aplicación realice sobre nuestros datos. El hecho de que, además, estos estén centralizados hace que una persona que obtenga acceso a ellos de forma indebida tenga la posibilidad de manejar información confidencial de miles o millones de usuarios. A lo largo de la historia de Internet es una situación que, desgraciadamente, ha ocurrido varias veces y que hay que tener muy en cuenta. Realmente no solo las aplicaciones web provocan delegar el uso de nuestra información a terceros, es muy habitual usar aplicaciones de escritorio y que los datos se almacenen en lo que llamamos la nube, que no es más que un servicio en Internet que centraliza el almacenamiento de los datos y, por lo tanto, adolecerá de estas mismas ventajas e inconvenientes.

# 1.3. Arquitectura de dos niveles

La arquitectura web a dos niveles, también conocida como arquitectura clienteservidor, es un modelo de diseño utilizado en aplicaciones web donde las tareas se distribuyen entre estos dos componentes. Vamos a describir los dos niveles:

![Figura 3. Arquitectura de dos niveles: cliente-servidor. Fuente: elaboración propia.](images/image-4.png)

*Figura 3. Arquitectura de dos niveles: cliente-servidor. Fuente: elaboración propia.*

Cliente

El cliente es el nivel que interactúa directamente con el usuario final. Su función principal es proporcionar una interfaz a través de la cual el usuario puede interactuar con el sistema. Las características y funciones del cliente incluyen:

**▸ Interfaz de usuario (UI):** el cliente proporciona la interfaz gráfica que permite al usuario interactuar con la aplicación. Esto puede incluir navegadores web, aplicaciones móviles o aplicaciones de escritorio.

**▸ Solicitudes al servidor:** el cliente envía solicitudes al servidor para obtener datos, procesar información o realizar acciones. Estas solicitudes, generalmente, se realizan a través de HTTPS en aplicaciones web.

**▸ Presentación:** una vez que el cliente recibe la respuesta del servidor, procesa y presenta los datos al usuario de manera comprensible y visualmente atractiva. Ejemplos comunes: navegadores web (como Chrome, Firefox, Safari), aplicaciones móviles que se conectan a servicios web, aplicaciones de escritorio conectadas a servidores.

Servidor

El servidor es el nivel que maneja la lógica de negocio, el almacenamiento y la manipulación de datos, y la respuesta a las solicitudes del cliente. Las características y funciones del servidor incluyen:

**▸ Procesamiento de solicitudes:** el servidor recibe y procesa las solicitudes enviadas por los clientes. Esto puede incluir la ejecución de lógica de negocio, cálculos, validaciones, etc.

**▸ Gestión de datos:** el servidor accede, manipula y almacena datos en una base de datos o cualquier otro sistema de almacenamiento. Este nivel es responsable de mantener la integridad y consistencia de los datos.

**▸ Generación de respuestas:** después de procesar una solicitud, el servidor genera una respuesta que es enviada de vuelta al cliente. Esta respuesta puede contener datos en varios formatos (HTML, JSON, XML, etc.) que el cliente presentará al usuario.

**▸ Seguridad y autenticación:** el servidor gestiona la seguridad del sistema incluyendo la autenticación de usuarios y la autorización de acceso a los recursos necesarios para que la aplicación cumpla el objetivo para el que se desarrolló. Ejemplos comunes: servidores web (como Apache, Nginx), servidores de aplicaciones, bases de datos, servidores de API.

Flujo de trabajo en la arquitectura cliente-servidor

**▸ Inicio de solicitud:** el usuario interactúa con la interfaz de usuario en el cliente, lo que inicia una solicitud (por ejemplo, al hacer clic en un botón). **▸ Envío de la solicitud:** el cliente envía una solicitud al servidor a través de la red. **▸ Procesamiento de la solicitud:** el servidor recibe la solicitud, procesa la lógica de negocio necesaria y accede a la base de datos si es necesario. **▸ Generación de respuesta:** el servidor genera una respuesta con los datos o el resultado del procesamiento. **▸ Envío de la respuesta:** el servidor envía la respuesta de vuelta al cliente. **▸ Presentación al usuario:** el cliente recibe la respuesta, la procesa y presenta la información al usuario.

Beneficios y desafíos

#### Beneficios

**▸** Separación de responsabilidades: claramente divide la interfaz de usuario de la lógica del negocio y la gestión de datos. **▸** Escalabilidad: permite escalar el servidor independientemente del cliente. **▸** Flexibilidad: facilita la actualización y mantenimiento del cliente y servidor de manera independiente.

#### Desafíos

**▸ Latencia de red:** la comunicación entre cliente y servidor puede introducir retrasos. **▸ Seguridad:** la transferencia de datos a través de la red debe ser segura y el acceso a los recursos.

**▸ Manejo de sesiones:** mantener el estado del usuario puede ser complejo, especialmente en aplicaciones web.

**▸ Sobrecarga:** si hay una gran cantidad de peticiones de muchos clientes se podría producir una congestión de red al intentar descargar o acceder los clientes a los datos del servidor. Este problema se conoce como cliente pesado. La arquitectura de tres niveles intenta evitar esta sobrecarga equilibrando las tareas.

Esta arquitectura sigue siendo una base fundamental en el desarrollo de aplicaciones y servicios en la web, adaptándose y evolucionando con nuevas tecnologías y necesidades.

# 1.4. Arquitectura de tres niveles

Las aplicaciones web actuales utilizan lo que se conoce como arquitectura de tres niveles (en inglés, *three-tier architecture),* a veces incluso se habla de más capas. Estas capas son:

![Figura 4. Arquitectura a tres niveles. Fuente: elaboración propia.](images/image-5.png)

*Figura 4. Arquitectura a tres niveles. Fuente: elaboración propia.*

**▸ Capa de presentación.** Maneja la parte de la aplicación web que ve el usuario. Es decir, se encarga de la forma de presentar la información al usuario. Consta del código del lado del cliente (HTML, JavaScript, CSS, etc.) que le llega al navegador, aunque ese código haya sido generado originalmente por una tecnología del lado del servidor.

**▸ Capa lógica.** Es la encargada de gestionar el funcionamiento de la aplicación. En ella se encuentran los documentos escritos en un lenguaje que se debe interpretar en el lado del servidor (por ello, esta capa está relacionada con el servidor de aplicaciones) y cuyo resultado se enviará al servidor web para que este, a su vez, lo envíe al cliente que hizo la petición. Habitualmente, la programación en esta capa divide el código en tres partes: el modelo, el controlador y la vista utilizando el exitoso **modelo MVC.** Cada parte se encarga de una acción concreta de la aplicación y así se facilita el mantenimiento de esta.

**▸ Capa de negocio.** Es la que contiene la información empresarial. Esta información siempre tiene como requerimiento que quede oculta a cualquier persona sin autorización. En esta capa, fundamentalmente, se encuentra el sistema gestor de bases de datos (SGBD) de la empresa u organización, además de otros servidores que proporcionan otros recursos empresariales (como servidores de vídeo, audio, certificados, etc.).

El servidor de aplicaciones hace peticiones a estos servidores para obtener los recursos de la empresa u organización que requieren para cumplir la petición HTTP

|  |  | original. De modo que el proceso de acceso a estos recursos | queda oculto |
| --- | --- | --- | --- |
| totalmente | al navegador, | lo que añade una mayor seguridad al | proceso. Los |
| servidores | de esta capa | entregarán los recursos solicitados y el servidor de |  |

aplicaciones será el encargado de situarle de forma adecuada en el resultado que viajará hasta el navegador del usuario.

Todo este mecanismo de trabajo es el que involucra la creación de aplicaciones web. En general, los servidores web actuales actúan de servidores de aplicaciones, una vez que se les instala el *software* pertinente. Por ello, cuando se habla de servidores web, en realidad también hablamos de servidores de aplicaciones web.

Existe, también, una división entre las tareas de las personas encargadas del desarrollo de aplicaciones web en base a lo cerca o lejos que su tarea está respecto al usuario. En este punto vamos a introducir los conceptos de *front-end* y *back-end,* que en esta arquitectura los podríamos ubicar de la siguiente forma:

**▸** ***Front-end:*** se refiere a la parte del desarrollo encargado de producir la apariencia final de la aplicación que verá el usuario. En cierto modo, es la interfaz de usuario.

Las personas que se encargan del *front-end* de la aplicación son las que diseñan las maquetas o *mockups* de la aplicación. También forman parte del *front-end* las personas encargadas del HTML y CSS de la página, así como del JavaScript. Es decir, del funcionamiento de la capa de presentación. Lo que el *front-end* intenta conseguir es una buena experiencia de usuario.

**▸** ***Back-end:*** se ubica en el servidor. Esto incluye la lógica de negocio, la gestión de datos y las operaciones de almacenamiento y recuperación de datos en una base de datos. El servidor procesa las solicitudes enviadas por el cliente, realiza las operaciones necesarias y devuelve la respuesta correspondiente al cliente.

Paradigma modelo-vista-controlador

Las aplicaciones web, a medida que se van actualizando, son más difíciles de mantener y, si a esto unimos cuestiones sobre los distintos niveles, hace que sea necesario separar el código para mejorar la organización de este.

A este respecto, el paradigma MVC de creación de aplicaciones (y sus diversas variantes) ha tenido muy buena aceptación en el campo del desarrollo de *software,* ya que la capa de trabajo de la aplicación web es la capa lógica, y es aquí donde reside la generación del código final, porque en esta capa es donde se aplica el paradigma MVC.

Lo que hace este patrón de diseño es separar la programación de la capa lógica en otras tres capas: el modelo, la vista y el controlador.

**▸ Modelo:** contiene el código que se encarga de asociar la información que procede la capa de negocio a su formato entendible por el lenguaje y tecnología utilizado para programar la aplicación web.

**▸ Vista:** genera la presentación de cara al usuario. Es la encargada de definir la interfaz de usuario.

**▸ Controlador:** es la capa encargada de manejar las peticiones del usuario y de comunicarse con las capas anteriores para que obtengan lo necesario de dicha petición. Resumiendo, lo que hace es determinar la petición, requerir al modelo los datos necesarios y enviarle a la vista para que genere el resultado final que llega al usuario. La petición de usuario se lanza por una acción que realiza el usuario (un clic de ratón, desplazarse por la página, etc.) En definitiva, el controlador es un mediador entre modelo y vista.

![Figura 5. Funcionamiento del paradigma MVC. Fuente: elaboración propia.](images/image-6.png)

*Figura 5. Funcionamiento del paradigma MVC. Fuente: elaboración propia.*

En la figura se observa el funcionamiento básico del patrón de diseño MVC. Se puede observar cómo el cliente, a través del navegador en el caso de una aplicación web, genera una petición, y esta llega a la capa **controlador,** que se encarga de contactar con el **modelo,** a fin de acceder y modificar, si la petición lo requiere, los datos. El **controlador** recibe los datos y con ellos pide a la capa **vista** que modifique la presentación que ve el usuario.

Como todos los patrones de diseño, tiene sus ventajas y sus inconvenientes:

**▸** Ventajas:

- La aplicación se desarrolla de forma modular, lo que facilita el trabajo en equipo.

- Las vistas muestran siempre información actualizada.

- Las modificaciones a las vistas no afectan a otros módulos.

**▸** Desventajas:

- Mayor tiempo de desarrollo.

- Orientado a objetos.

# 1.5 Protocolos de aplicación más usados

En el desarrollo de aplicaciones web se utilizan varios protocolos para la comunicación, la transferencia de datos y la seguridad. A continuación, se describen los protocolos más comunes:

HTTP/HTTPS (Hypertext Transfer Protocol/Secure)

**▸ HTTP:** es el protocolo base para la comunicación en la web. Define cómo se formatean y transmiten los mensajes y cómo los navegadores y servidores web deben responder a diversas órdenes. Usa el puerto 80 por defecto.

**▸ HTTPS:** es la versión segura de HTTP. Utiliza SSL/TLS para cifrar la comunicación entre el cliente y el servidor, lo que asegura que los datos transmitidos no puedan ser interceptados o alterados. Usa el puerto 443 por defecto.

FTP/SFTP (File Transfer Protocol/Secure File Transfer Protocol)

**▸ FTP:** es un protocolo para la transferencia de archivos entre sistemas en una red. Usa el puerto 21 para la conexión de control (comandos y respuestas) y el puerto 20 para transferencia de datos en modo activo.

**▸ SFTP:** es la versión segura de FTP, que utiliza SSH para cifrar la transferencia de archivos. Utiliza el puerto 22 para la transferencia segura de archivos, ya que SFTP es parte del protocolo SSH (Secure Shell), que también utiliza este puerto.

SMTP (Simple Mail Transfer Protocol)

Es un protocolo de red utilizado para el intercambio de mensajes de correo electrónico entre dispositivos. Utiliza los siguientes puertos:

**▸ Puerto 25:** este es el puerto estándar original para el envío de correos electrónicos a través de SMTP.

**▸ Puerto 587:** este puerto se usa para el envío de correos electrónicos con autenticación, conocido como SMTP Submission.

**▸ Puerto 465:** originalmente asignado para SMTP sobre SSL (Secure Sockets Layer), ahora se utiliza comúnmente para SMTP con seguridad mediante TLS (Transport Layer Security).

![image-7](images/image-7.png)

Tabla 1. Resumen de puertos de protocolos aplicación. Fuente: elaboración propia.

# comunicacion-ataques-y-recomendaciones

# IoT: protocolos de comunicación, ataques y recomendaciones

Porro Sáez, I. (2019, febrero 7). *IoT: protocolos de comunicación, ataques y* *recomendaciones.* Incibe. <https://www.incibe.es/incibe-cert/blog/iot-protocolos->

La implantación de aplicaciones web también nos permite realizar portales web para la gestión y el control de dispositivos IoT, muy utilizados, sobre todo, en la industria. Es importante tener en cuenta las consideraciones de seguridad que se indican y los protocolos de comunicación más habituales.

Implantación de Aplicaciones Web 23 Tema 1. A fondo

# Donohue, T. (2015, marzo 17). Architecture. Confluence.

# [https://wiki.lyrasis.org/display/DSDOC6x/Architecture](https://wiki.lyrasis.org/display/DSDOC6x/Architecture)

# Arquitectura de la aplicación Dspace

Ver el esquema gráfico de una arquitectura a tres niveles de esta aplicación de código abierto que normalmente se utiliza como repositorio bibliográfico institucional.

Implantación de Aplicaciones Web 24 Tema 1. A fondo

# is/latency/

# Latencia de red

¿Qué es la latencia de red? (s. f.). AWS Amazon. <https://aws.amazon.com/es/what->

Leer toda la información sobre lo que afecta la latencia en las aplicaciones web y las que requieren una latencia más baja y por qué.

Implantación de Aplicaciones Web 25 Tema 1. A fondo

# Entrenamiento 1

**▸ Planteamiento del ejercicio:** configuración de un servidor FTP. Para ello debes utilizar FileZilla Server.

**▸ Desarrollo paso a paso:** descarga FileZilla Server y realiza la instalación para Windows en tu equipo. Una vez instalado revisa las opciones de configuración y verifica en que direcciones IP y puertos se está escuchando.

**▸ Solución:** vamos a «Server», «Configure», «Server listeners».

![Figura 6. Settings for server 127.0.0.1:14148. Fuente: elaboración propia.](images/image-8.png)

*Figura 6. Settings for server 127.0.0.1:14148. Fuente: elaboración propia.*

# Entrenamiento 2

**▸ Planteamiento del ejercicio:** cuando trabajamos con servidores, como un servidor de FTP, es muy importante tener información de lo que está pasando dentro de él y poder analizar esa informacion. Para eso se utilizan los ficheros de log.

**▸ Desarrollo paso a paso:** identifica dónde acceder al fichero de log en la configuración y dónde está ubicado físicamente.

**▸ Solución:** vamos a «Server», «Configure», «Logging». La ruta física por defecto sería: «C:\Program Files\FileZilla Server\Logs»

![Figura 7. Settings for server 127.0.0.1:14148. Fuente: elaboración propia.](images/image-9.png)

*Figura 7. Settings for server 127.0.0.1:14148. Fuente: elaboración propia.*

# Entrenamiento 3

**▸ Planteamiento del ejercicio:** configuración de usuarios y acceso.

**▸ Desarrollo paso a paso:** ahora vamos a configurar para que los usuarios de Windows puedan conectarse a nuestro servidor y acceder a sus directorios de trabajo.

**▸ Solución:** para esto vamos a «Configure», «Server», «Rights management», «Users». Aquí habilitamos la opción «User is enabled». De esta forma habilitamos el acceso a los usuarios.

![Figura 8. Settings for server 127.0.0.1:14148. Fuente: elaboración propia.](images/image-10.png)

*Figura 8. Settings for server 127.0.0.1:14148. Fuente: elaboración propia.*

# Entrenamiento 4

- ▸ Planteamiento del ejercicio: descarga FileZilla Client para conectarnos a nuestro

    - servidor de FTP.

- ▸ Desarrollo paso a paso: vamos a conectarnos a un nuevo sitio y en los parámetros

    - especificaremos lo siguiente:

- IP: 127.0.0.1

- USUARIO: nuestro usuario de Windows.

- PASSWORD: nuestra contraseña de acceso a Windows.

Después de hacer esto le damos a «Conectar».

**▸ Solución:** veremos que FileZilla Client se conecta a nuestro servidor.

![Figura 9. Settings for server 127.0.0.1:14148. Fuente: elaboración propia.](images/image-11.png)

*Figura 9. Settings for server 127.0.0.1:14148. Fuente: elaboración propia.*

En el servidor tendremos que ver que la conexión ha sido exitosa y que hay un usuario conectado.

![Figura 10. Revisión de conexión exitosa. Fuente: elaboración propia.](images/image-12.png)

*Figura 10. Revisión de conexión exitosa. Fuente: elaboración propia.*

# Entrenamiento 5

**▸ Planteamiento del ejercicio:** en Filezilla Server configura para que el acceso sea de solo lectura y este limitado a cinco ficheros. Una vez hecho esto, accede al fichero filezilla-server.log y revisa lo que ha pasado.

**▸ Desarrollo paso a paso:** nos vamos a configuración de servidor, habilitamos el acceso «Read only» y en la opción de «Limits» habilitamos los ficheros a cinco.

**▸ Solución:** a continuación, se muestran capturas gráficas de la solución.

![Figura 11. Settings for server 127.0.0.1:14148. Fuente: elaboración propia.](images/image-13.png)

*Figura 11. Settings for server 127.0.0.1:14148. Fuente: elaboración propia.*

![Figura 12. Settings for server 127.0.0.1:14148. Fuente: elaboración propia.](images/image-14.png)

*Figura 12. Settings for server 127.0.0.1:14148. Fuente: elaboración propia.*

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.4–22)*
- A fondo  *(pp.23–25)*
- Entrenamientos  *(pp.26–32)*
- Implantación de Aplicaciones Web 4 Tema 1. Material de estudio · Implantación de Aplicaciones Web 5 Tema 1. Material de estudio · Implantación de Aplicaciones Web 7 Tema 1. Material de estudio · Implantación de Aplicaciones Web 8 Tema 1. Material de estudio · Implantación de Aplicaciones Web 9 Tema 1. Material de estudio · Implantación de Aplicaciones Web 10 Tema 1. Material de estudio · Implantación de Aplicaciones Web 11 Tema 1. Material de estudio · Implantación de Aplicaciones Web 12 Tema 1. Material de estudio · Implantación de Aplicaciones Web 13 Tema 1. Material de estudio · Implantación de Aplicaciones Web 14 Tema 1. Material de estudio · Implantación de Aplicaciones Web 15 Tema 1. Material de estudio · Implantación de Aplicaciones Web 16 Tema 1. Material de estudio · Implantación de Aplicaciones Web 17 Tema 1. Material de estudio · Implantación de Aplicaciones Web 18 Tema 1. Material de estudio · Implantación de Aplicaciones Web 19 Tema 1. Material de estudio · Implantación de Aplicaciones Web 20 Tema 1. Material de estudio · Implantación de Aplicaciones Web 21 Tema 1. Material de estudio · Implantación de Aplicaciones Web 22 Tema 1. Material de estudio  *(pp.4, 5, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22)*
- Implantación de Aplicaciones Web 26 Tema 1. Entrenamientos · Implantación de Aplicaciones Web 27 Tema 1. Entrenamientos · Implantación de Aplicaciones Web 28 Tema 1. Entrenamientos · Implantación de Aplicaciones Web 29 Tema 1. Entrenamientos · Implantación de Aplicaciones Web 30 Tema 1. Entrenamientos · Implantación de Aplicaciones Web 31 Tema 1. Entrenamientos · Implantación de Aplicaciones Web 32 Tema 1. Entrenamientos  *(pp.26–32)*