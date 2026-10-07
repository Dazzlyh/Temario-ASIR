## Tema

## Servicios en Red e Internet

# Tema 6. Correo electrónico

# Índice

Esquema Material de estudio

## 6.1. Introducción y objetivos

## 6.2. Características

## 6.3. Protocolos

## 6.4. Cliente y servidor correo electrónico

## 6.5. Buzón de correo electrónico

## 6.6. Cuentas de correo electrónico, alias y listas de

distribución

## 6.7. Referencias bibliográficas

A fondo Elementos del servicio de correo electrónico Servidor de correo electrónico con contenedores Docker Servidor de correo electrónico, ¿cómo funciona? Tu dirección de correo electrónico temporal IMAP y POP3: ¿En qué se diferencian y cuándo usar cada uno?

¿Qué es SMTP? ¿Cómo funciona y para qué sirve?

Correo electrónico. Parte 1

Correo electrónico. Parte 2

Administración de sistemas

Administración de sistemas - Protocolo IMAP

Administración de sistemas - Protocolo SMTP

Administración de sistemas - Protocolo POP - Fernando Terroso Entrenamientos Entrenamiento 1. Clientes de correo electrónico Entrenamiento 2. Servidor de correo electrónico en Windows Entrenamiento 3. Servidor de correo electrónico en Ubuntu Entrenamiento 4. Cuentas de correo electrónico con Windows Entrenamiento 5. Autenticación, autorización y control de acceso de un servidor Web con Ubuntu

# Esquema

![image-2](images/image-2.png)

Servicios en Red e Internet 4 Tema . Esquema

## 6.1. Introducción y objetivos

El correo electrónico ha transformado profundamente la forma en que nos comunicamos tanto en el ámbito personal como en el profesional. Desde su invención en la década de **1970,** el correo electrónico ha evolucionado hasta convertirse en una **herramienta indispensable** en la vida cotidiana de millones de personas en todo el mundo. En un entorno cada vez más digitalizado, entender el funcionamiento del correo electrónico y su impacto es crucial para navegar con éxito en la era de la información.

A lo largo de los años, el correo electrónico ha pasado de ser una novedad tecnológica a un componente esencial de la **infraestructura de comunicación** **global.** Su accesibilidad y versatilidad lo han convertido en el medio preferido para la **comunicación escrita** en muchos contextos, desde la correspondencia empresarial hasta el contacto personal. Pero más allá de su uso cotidiano, el correo electrónico encierra una serie de conceptos técnicos y protocolos que, al ser comprendidos, permiten un manejo más efectivo y seguro de esta herramienta.

Uno de los aspectos más importantes del correo electrónico es la **infraestructura** **tecnológica** que lo sustenta. Los **protocolos** de correo electrónico, como SMTP, IMAP y POP3, juegan un papel fundamental en la entrega y recepción de mensajes. Estos protocolos facilitan el proceso de envío y recepción de correos, asegurando que los mensajes lleguen a sus destinatarios de manera eficiente. Comprender estos protocolos es esencial no solo para aquellos que desean profundizar en la tecnología detrás del correo electrónico, sino también para usuarios que buscan optimizar el uso de sus cuentas de correo.

Además, la evolución del correo electrónico ha ido de la mano con el desarrollo de nuevas tecnologías y dispositivos. Con la llegada de los teléfonos inteligentes y la proliferación de dispositivos móviles, el acceso al correo electrónico se ha vuelto más

Servicios en Red e Internet 5 Tema . Material de estudio instantáneo y ubicuo. Esta evolución ha redefinido

cómo, cuándo y dónde las

personas interactúan con sus correos electrónicos, impulsando una mayor conectividad y flexibilidad en la comunicación.

No obstante, a medida que el correo electrónico ha crecido en importancia, también lo han hecho las **amenazas** asociadas con su uso. El *phishing,* el *spam* y otros tipos de ciberataques son peligros reales que los usuarios de correo electrónico deben enfrentar. Protegerse contra estas amenazas requiere una comprensión no solo de los riesgos, sino también de las herramientas y prácticas disponibles para mitigarlos. Desde el uso de *software antispam* hasta la adopción de buenas prácticas en la gestión del correo, existen múltiples estrategias que pueden ayudar a los usuarios a mantener su seguridad y privacidad en línea.

El correo electrónico también tiene **aplicaciones** que van más allá de la simple comunicación. En el ámbito empresarial, por ejemplo, es una herramienta clave para e l *marketing* digital, permitiendo a las empresas llegar a sus clientes de manera directa y personalizada. Los alias y las listas de distribución, por su parte, facilitan la organización y el manejo de grandes volúmenes de correo, optimizando así la eficiencia en la comunicación.

Finalmente, es importante destacar que el correo electrónico, pese a su antigüedad en el mundo digital, sigue siendo una herramienta adaptable y relevante en múltiples contextos. Su **capacidad para adaptarse** a nuevas tecnologías y necesidades lo mantiene como un recurso vital en la comunicación moderna. Al entender sus fundamentos, los usuarios pueden no solo mejorar su manejo del correo electrónico, sino también aprovechar al máximo su potencial en diversas áreas de su vida.

Esta guía está diseñada para proporcionar una comprensión profunda y práctica del correo electrónico, abordando desde sus aspectos técnicos hasta su uso seguro y eficiente. A través de este contenido, los lectores podrán adquirir las herramientas y conocimientos necesarios para gestionar su correo electrónico de manera efectiva y

Servicios en Red e Internet 6 Tema . Material de estudio protegerse contra las amenazas que enfrentan en el entorno digital actual.

Los **objetivos** que se pretende alcanzar en este tema son: **▸** Comprender los fundamentos del correo electrónico. **▸** Diferenciar entre protocolos de correo electrónico. **▸** Explicar la historia y evolución del correo electrónico. **▸** Reconocer el impacto de la tecnología en el correo electrónico. **▸** Describir el funcionamiento de los clientes de correo electrónico. **▸** Describir el funcionamiento de los servidores de correo electrónico. **▸** Identificar los componentes de una dirección de correo electrónico. **▸** Entender la funcionalidad de alias y listas de distribución. **▸** Protegerse contra amenazas de correo electrónico. **▸** Promover buenas prácticas en la gestión del correo electrónico. **▸** Destacar la importancia del formato de archivos. **▸** Fomentar el uso seguro de herramientas de correo electrónico. **▸** Mejorar la comprensión de los conceptos de envío y recepción de correos. **▸** Capacitar en el uso de funcionalidades del correo electrónico. **▸** Ilustrar el rol del correo electrónico en el *marketing* digital. **▸** Resaltar la adaptabilidad del correo electrónico en diferentes contextos.

## 6.2. Características

¿Qué es este servicio?

El servicio de correo electrónico presenta muchas similitudes con el tradicional servicio de correo postal, por lo que, en esencia, se podría aplicar una definición similar a ambos, con la consideración de las diferencias tecnológicas significativas que los separan. Así, el correo electrónico podría definirse como un servicio de comunicación que facilita el envío y la recepción de **mensajes** (correos electrónicos) **y archivos adjuntos** a través de una red de **manera diferida.** Esto significa que varios usuarios, utilizando dispositivos conectados a una red, especialmente a Internet, pueden intercambiar información en forma de correos electrónicos, que pueden incluir tanto mensajes de texto simples como archivos adjuntos, sin necesidad de que ambos estén conectados al mismo tiempo.

La **similitud con el correo postal tradicional** es clara: el remitente puede enviar un mensaje, que puede incluir diversos contenidos en el «sobre» virtual (como un simple texto, fotos, documentos, etc.) y cuando dicho mensaje llega a su destino, el destinatario puede no estar disponible en ese momento para recibirlo, pero lo recogerá y revisará cuando lo considere oportuno. Aunque existen **diferencias** **obvias** entre el correo electrónico y el correo postal tradicional, como la velocidad de entrega, el medio de transporte y la posibilidad de añadir multimedia, el objetivo básico que subyace a ambos servicios es, esencialmente, el mismo: permitir la comunicación e intercambio de información entre personas, independientemente de la distancia o el tiempo.

El correo electrónico ha sido uno de los servicios más populares y dominantes en Internet durante muchos años, especialmente antes de la explosión del servicio web, que ahora también juega un papel crucial en la vida digital. Sin embargo, en los últimos años, la actividad relacionada con el correo electrónico ha experimentado un

Servicios en Red e Internet 8 Tema . Material de estudio **resurgimiento,** impulsado en gran medida por el desarrollo de los teléfonos móviles y la llegada de los *smartphones.* Estos dispositivos han hecho que acceder al correo electrónico sea mucho más conveniente, permitiendo a los usuarios revisar y enviar correos desde prácticamente cualquier lugar y en cualquier momento, lo que ha revitalizado su uso y relevancia.

Además, la expansión y el uso del correo electrónico, junto con el crecimiento exponencial del servicio web, han sido factores clave en la evolución de Internet. Estos servicios han actuado como motores del crecimiento de la red, configurando la forma en que interactuamos, trabajamos y nos comunicamos en el mundo digital. Es difícil imaginar cómo sería el Internet actual sin la presencia del correo electrónico y las páginas web, ya que ambos servicios han establecido las bases para muchas de las actividades que hoy damos por sentadas en línea.

La importancia del correo electrónico no solo radica en su capacidad para facilitar la comunicación personal y profesional, sino también en su papel fundamental en la estructuración del entorno digital que define la era moderna.

¿Para qué sirve?

El correo electrónico es una herramienta de comunicación digital extremadamente versátil, que se utiliza en una amplia variedad de contextos tanto personales como profesionales.

A continuación, te presento un listado de algunos de los **usos más** comunes del correo electrónico:

**▸ Comunicación personal:** el correo electrónico permite a las personas mantenerse en contacto con amigos, familiares y conocidos sin importar las distancias geográficas. Es una herramienta utilizada para compartir noticias, fotos, vídeos y

Servicios en Red e Internet 9 Tema . Material de estudio cualquier otro tipo de contenido personal. A diferencia de las llamadas telefónicas o mensajes instantáneos, los correos electrónicos ofrecen la posibilidad de redactar mensajes más detallados y reflexivos, que pueden ser leídos y respondidos en el momento que el destinatario considere más conveniente.

**▸ Comunicación profesional:** en el entorno laboral, el correo electrónico es indispensable para la coordinación de actividades, la asignación de tareas y la comunicación entre colegas, jefes, y clientes. Es comúnmente utilizado para enviar informes, solicitar reuniones, discutir proyectos y mantener un registro de las comunicaciones empresariales. Además, permite adjuntar documentos relevantes, como contratos, presentaciones y planificaciones, facilitando la colaboración en equipo, incluso a distancia.

**▸ Envío de documentos:** el correo electrónico es una de las formas más rápidas y seguras de enviar documentos importantes, como contratos, acuerdos legales, facturas y propuestas. Esto permite a las personas y organizaciones enviar y recibir documentos cruciales sin necesidad de utilizar servicios de mensajería física, reduciendo tiempos y costos.

**▸ Suscripción a boletines:** muchas empresas y organizaciones utilizan el correo electrónico para enviar boletines informativos o *newsletters* a sus suscriptores. Estos boletines suelen incluir actualizaciones sobre productos, noticias de la industria, promociones exclusivas y contenido relevante para el lector. Esta es una estrategia clave en el *marketing* digital, que permite a las empresas mantener el interés y la lealtad de sus clientes.

**▸ Notificaciones y alertas:** el correo electrónico es ampliamente utilizado por los servicios en línea para enviar notificaciones y alertas a sus usuarios. Esto incluye desde alertas de actividad sospechosa en cuentas bancarias hasta notificaciones de nuevas publicaciones en redes sociales o recordatorios de citas. Estas notificaciones ayudan a los usuarios a mantenerse informados y protegidos, además de facilitar la gestión de sus actividades en línea.

**▸**

**▸ Gestión de cuentas y servicios en línea:** el correo electrónico es fundamental para la gestión de cuentas en diversas plataformas y servicios en línea. Es común que los usuarios reciban correos electrónicos para confirmar su identidad, recuperar contraseñas y actualizar información de perfil. Además, muchos servicios envían recordatorios de facturación, renovaciones de suscripción y otros avisos importantes directamente a la bandeja de entrada del usuario.

**▸** ***Marketing*** **y publicidad:** el correo electrónico es una herramienta poderosa en el *marketing* digital, que permite a las empresas llegar directamente a los clientes con campañas promocionales, ofertas especiales y anuncios personalizados. A través de técnicas como el *email marketing,* las empresas pueden segmentar su audiencia y enviar mensajes dirigidos que incrementan la probabilidad de conversión y fidelización de clientes.

**▸ Coordinación de eventos:** organizar y coordinar eventos, como reuniones, conferencias, talleres y celebraciones, es mucho más fácil con el uso del correo electrónico. Los organizadores pueden enviar invitaciones, confirmar asistencias, compartir agendas y coordinar detalles logísticos, todo desde la comodidad de sus dispositivos. Además, los participantes pueden responder a las invitaciones, hacer preguntas y sugerencias y recibir actualizaciones en tiempo real.

**▸ Educación:** en el ámbito educativo, el correo electrónico es una herramienta clave para la comunicación entre estudiantes, profesores y administradores. Permite el envío y recepción de materiales de estudio, la entrega de tareas y la coordinación de actividades académicas. Además, facilita la retroalimentación y el seguimiento personalizado del progreso de los estudiantes, creando un canal de comunicación directo entre el docente y el estudiante.

**▸ Asistencia técnica:** muchas empresas ofrecen soporte técnico y atención al cliente a través del correo electrónico. Los usuarios pueden enviar consultas, reportar problemas y solicitar ayuda, recibiendo respuestas detalladas y soluciones a sus problemas. Este método permite a las empresas brindar un servicio más personalizado y eficiente, registrando y haciendo un seguimiento de cada caso.

**▸ Confirmación de pedidos y compras:** tras realizar una compra en línea, es habitual recibir una confirmación del pedido a través del correo electrónico. Estos mensajes suelen incluir detalles como el número de pedido, el resumen de los productos adquiridos, la fecha estimada de entrega y enlaces para rastrear el envío. Esta práctica proporciona a los clientes seguridad y transparencia en sus transacciones.

**▸** ***Networking*** **profesional:** el correo electrónico es esencial para construir y mantener redes profesionales. Permite a los usuarios conectarse con colegas, posibles socios de negocios y otros profesionales dentro de su industria. A través del correo electrónico, se pueden concertar reuniones, compartir ideas y colaborar en proyectos, ayudando a expandir las oportunidades profesionales.

**▸ Recepción de notas de prensa:** los periodistas y medios de comunicación a menudo reciben notas de prensa y comunicados oficiales a través del correo electrónico. Estas notas suelen contener información sobre eventos, lanzamientos de productos, cambios corporativos y otros asuntos de interés público. Este medio permite a las organizaciones distribuir información relevante de manera eficiente y directa a los medios.

**▸ Registro de actividades:** el correo electrónico también sirve como un archivo de comunicaciones y actividades, donde se pueden almacenar y organizar correos importantes, que luego pueden ser referenciados o recuperados en caso necesario. Esta capacidad de almacenar y gestionar mensajes hace que el correo electrónico sea una herramienta útil para mantener un registro de correspondencia y eventos a lo largo del tiempo.

**▸ Compartir enlaces y contenidos en línea:** los usuarios suelen utilizar el correo electrónico para compartir enlaces a artículos, vídeos, sitios web, y otros contenidos en línea con amigos, familiares y colegas. Este método es una forma sencilla y directa de difundir información relevante o interesante, facilitando el intercambio de conocimientos y recursos entre personas.

Estos usos destacan la importancia del correo electrónico en la vida diaria, demostrando que es mucho más que un simple medio de comunicación. Su versatilidad y capacidad para adaptarse a diferentes necesidades lo convierten en una herramienta indispensable tanto en el ámbito personal como profesional.

Historia y funcionalidad

El servicio de correo electrónico tiene sus **orígenes** en la **década de 1960,** lo que lo convierte en una tecnología mucho más antigua que el propio Internet. Aunque su concepción surgió en los años 60, la primera transmisión de un correo electrónico tal como lo entendemos hoy en día no se realizó hasta principios de los años 70. El objetivo fundamental de este servicio siempre ha sido facilitar la transmisión de mensajes, conocidos como correos electrónicos, entre dispositivos conectados a una red.

En sus inicios, el servicio de correo electrónico tenía una **capacidad bastante** **limitada** en comparación con lo que conocemos hoy. Originalmente, solo permitía el envío de mensajes de texto en **formato ASCII,** es decir, mensajes compuestos exclusivamente por caracteres alfanuméricos simples. No había posibilidad de incluir imágenes, documentos, ni ningún otro tipo de archivo adjunto. Esta limitación se mantuvo hasta la década de 1990, cuando surgieron las **extensiones MIME** (Multipurpose Internet Mail Extensions) en 1991.

Estas extensiones marcaron un cambio significativo en la funcionalidad del correo electrónico, ya que establecieron una serie de especificaciones que ampliaron las capacidades de los protocolos utilizados para la transferencia de correos

Servicios en Red e Internet 13 Tema . Material de estudio electrónicos. Gracias a MIME, se hizo posible **adjuntar una variedad de archivos,** como documentos, imágenes y aplicaciones, permitiendo así que el correo electrónico evolucionara hacia la herramienta versátil que utilizamos en la actualidad.

En cuanto a su funcionamiento, el servicio de correo electrónico, a diferencia de otros servicios de red, involucra una variedad de protocolos que se activan según la tarea específica que se esté llevando a cabo, ya sea el envío, la distribución o la entrega del correo electrónico al destinatario final. Los **principales protocolos** involucrados en este proceso, que se estudiarán en detalle, son los siguientes:

**▸ SMTP (Simple Mail Transfer Protocol):** es el protocolo principal para el envío de correos electrónicos desde el cliente al servidor de correo y entre servidores. SMTP se encarga de la transmisión del mensaje a través de la red, asegurando que llegue al servidor correspondiente para su posterior distribución.

**▸ IMAP (Internet Message Access Protocol):** este protocolo permite a los usuarios acceder a sus correos electrónicos almacenados en un servidor. A diferencia de otros protocolos, IMAP permite ver y gestionar los correos directamente en el servidor, lo que es útil para acceder a los mensajes desde múltiples dispositivos.

**▸ POP (Post Office Protocol):** similar al IMAP, este protocolo, también, permite la descarga de correos electrónicos desde el servidor al dispositivo del usuario. Sin embargo, a diferencia de IMAP, POP generalmente descarga los mensajes y los elimina del servidor, almacenándolos localmente en el dispositivo del usuario.

El servicio de correo electrónico, al igual que otros servicios de red como la configuración automática de parámetros o la resolución de nombres de dominio, sigue un modelo cliente/servidor.

En este modelo, el **cliente de correo electrónico** (el programa que el usuario utiliza para enviar y recibir correos) es responsable de hacer solicitudes al servidor de correo. Estas solicitudes, generalmente, se limitan a dos funciones básicas:

**▸** Enviar correo electrónico.

**▸** Acceder al correo electrónico almacenado.

Haciendo un paralelo con el correo postal tradicional, los clientes de correo electrónico actúan como los usuarios que envían cartas en una oficina de correos o que abren sus buzones para recoger la correspondencia.

Por su parte, los **servidores de correo electrónico** desempeñan un papel crucial en la gestión de estas solicitudes. Su función principal es procesar y gestionar los correos electrónicos enviados por los clientes, distribuirlos a través de la red y almacenarlos en el servidor de destino para que el destinatario pueda acceder a ellos.

A diferencia de otros servicios de red, en el correo electrónico es común que intervengan **varios servidores** durante la transmisión de un mensaje. Esto se debe a que, en su viaje desde el remitente hasta el destinatario, los correos electrónicos «saltan» de un servidor a otro, actuando estos servidores como encaminadores que facilitan la entrega del mensaje final. Este proceso puede compararse con la infraestructura del correo postal tradicional, donde las cartas pasan por varios puntos de procesamiento—como oficinas de correos y centros de distribución—antes de llegar al buzón del destinatario.

![Figura 1. Servidores participantes al enviar un correo electrónico. Fuente: elaboración propia.](images/image-3.png)

*Figura 1. Servidores participantes al enviar un correo electrónico. Fuente: elaboración propia.*

En resumen, aunque el servicio de correo electrónico tiene raíces profundas que se remontan a las primeras décadas de la informática, su evolución ha sido constante y significativa. Desde sus humildes comienzos, cuando solo permitía la transmisión de texto simple, hasta convertirse en una herramienta robusta capaz de manejar una amplia gama de tipos de archivos y soportar una comunicación global eficiente, el correo electrónico ha sido y sigue siendo un pilar fundamental en la estructura de las comunicaciones digitales.

## 6.3. Protocolos

El servicio de correo electrónico se sustenta en varios protocolos, cada uno diseñado para cumplir una **función específica** en el proceso de enviar, distribuir y recibir correos electrónicos. Estos protocolos, esenciales para el funcionamiento de cualquier red que gestione correos electrónicos, son el SMTP (Simple Mail Transfer Protocol), el POP (Post Office Protocol) y el IMAP (Internet Message Access Protocol). A continuación, se describen las características y funciones de cada uno de ellos.

Protocolo SMTP

El SMTP, o Protocolo Simple de Transferencia de Correo, fue desarrollado en 1982 por Suzanne Sluizer y Jon Postel para facilitar el intercambio de mensajes en ARPANET, la red de comunicaciones interna del gobierno estadounidense que **precedió a Internet.** Hoy en día, el SMTP está estandarizado en el **RFC 5321** y es utilizado extensivamente en Internet para enviar correos electrónicos.

El SMTP se encarga de la **transmisión y distribución de correos electrónicos** a través de una red. Cuando un usuario envía un correo, el proceso se ejecuta a través de este protocolo. Además, el SMTP se utiliza cuando un correo electrónico es transferido de un servidor a otro hasta llegar a su destino final. Por lo tanto, el SMTP es esencial tanto para los **servidores de correo emisores** (aquellos desde los cuales se envían los correos) como para los **servidores encaminadores** (aquellos que distribuyen los correos a lo largo de la red).

En analogía con el sistema postal tradicional, el SMTP es el equivalente al proceso de dejar una carta en el buzón o en la oficina de correos y al trabajo del cartero que entrega la carta a su destino. Para cumplir su función, el protocolo SMTP utiliza **TCP** (Protocolo de Control de Transmisión) en la capa de transporte, empleando típicamente los **puertos 25 o 587.**

Protocolo POP

El POP, o Protocolo de Oficina de Correos, fue creado en 1984 para **simplificar el** **acceso** a los correos electrónicos almacenados en un servidor. En sus primeros días, acceder a los correos electrónicos no era una tarea sencilla, ya que, generalmente, requería el uso de SSH (Secure Shell) para realizar una conexión remota. Con el creciente número de dispositivos conectados a Internet y la necesidad de un **acceso más intuitivo** al correo electrónico, se desarrolló POP como una solución más amigable para el usuario. Actualmente, se utiliza la tercera versión de este protocolo, conocida como POP3, definida en el RFC 1939.

El protocolo POP está diseñado principalmente para la recepción de correos electrónicos. Permite a los usuarios **acceder a los mensajes almacenados** en un servidor **y descargarlos** en su dispositivo local. Aunque los correos se descargan al equipo del usuario, normalmente se mantiene una copia en el servidor, lo que permite recuperarlos en caso de que se eliminen accidentalmente del dispositivo local.

El diseño de POP se basó en la simplicidad, ofreciendo funciones básicas como la descarga y eliminación de correos electrónicos. Sin embargo, debido a su simplicidad, es un protocolo que **carece de estado,** lo que significa que no guarda información sobre correos leídos o eliminados. Además, POP no requiere una conexión permanente a la red; basta con estar en línea para descargar los correos y una vez descargados, pueden leerse sin conexión. No obstante, esto puede ser una desventaja en dispositivos con espacio de almacenamiento limitado, ya que los correos descargados ocupan espacio en el disco local. Si el usuario cambia de dispositivo, necesitará volver a descargar los correos para acceder a ellos.

En términos de su función, en el sistema postal tradicional POP3 sería el equivalente a abrir el buzón en casa para recoger la correspondencia dejada por el cartero. El protocolo POP3 también utiliza **TCP** como protocolo de capa de transporte, utilizando el **puerto 110** para entregar los correos electrónicos a los clientes de correo.

![Figura 2. Funcionamiento del servicio de correo. Fuente: El correo electrónico, s. f.](images/image-4.png)

*Figura 2. Funcionamiento del servicio de correo. Fuente: El correo electrónico, s. f.*

Protocolo IMAP

El IMAP, o Protocolo de Acceso a Mensajes de Internet, fue desarrollado en 1986 por Mark Crispin en la Universidad de Stanford. Actualmente, se utiliza la cuarta versión de este protocolo, conocida como IMAP4, definida en el RFC 3501.

Al igual que POP3, IMAP es un protocolo orientado a la recepción de correos electrónicos, permitiendo a los usuarios acceder a los mensajes almacenados en un servidor. Sin embargo, a diferencia de POP3, IMAP permite **gestionar los correos** directamente en el servidor sin necesidad de descargarlos en el dispositivo local.

Esto significa que los correos permanecen en el servidor y pueden ser accedidos desde cualquier dispositivo conectado a la red, siempre que el usuario esté en línea.

IMAP ofrece una mayor funcionalidad en comparación con POP3, permitiendo a los usuarios **organizar** sus correos electrónicos **en carpetas** en el servidor, lo que facilita la gestión de grandes volúmenes de correos provenientes de diferentes fuentes. Además, IMAP **guarda información** sobre el estado de los correos, como los mensajes leídos o eliminados, lo que mejora la eficiencia en la gestión de correos.

Al igual que POP3, IMAP se utiliza cuando el usuario accede a los correos electrónicos recibidos a través de un cliente de correo. Sin embargo, es importante destacar que **ambos protocolos son mutuamente excluyentes,** por lo que un usuario puede optar por utilizar IMAP o POP3, pero no ambos simultáneamente.

La elección entre estos protocolos dependerá de las preferencias del usuario y las características de su dispositivo local. Por ejemplo, para usuarios de teléfonos inteligentes, IMAP es una opción conveniente, ya que no descarga los correos al dispositivo, preservando así el espacio de almacenamiento.

Finalmente, al igual que los otros protocolos mencionados, IMAP4 utiliza TCP como protocolo de capa de transporte y los servidores de correo que utilizan IMAP emplean el puerto 143 para entregar los correos electrónicos a los clientes.

![Figura 3. Componentes y protocolos de un servicio de correo electrónico. Fuente: UCAM Universidad](images/image-5.png)

*Figura 3. Componentes y protocolos de un servicio de correo electrónico. Fuente: UCAM Universidad*

Católica de Murcia, 2018.

## 6.4. Cliente y servidor correo electrónico

Cliente de correo electrónico

A lo largo de este tema ya se ha mencionado el término cliente de correo electrónico, que se refiere a un *software* o aplicación diseñada específicamente para permitir a los usuarios gestionar sus correos electrónicos. Esta herramienta facilita al usuario la tarea de **enviar, descargar, acceder y organizar sus correos.**

El *software* en cuestión está **asociado con un buzón de correo electrónico,** que no es más que un espacio de almacenamiento en un servidor de correo electrónico vinculado al usuario. Gracias a esta asociación, el usuario puede acceder a sus correos almacenados en el servidor, leerlos, archivarlos o eliminarlos, según lo desee. Además, estos clientes permiten que los usuarios envíen correos electrónicos, ya que establecen la conexión necesaria con los servidores emisores para cursar la solicitud de envío de correos.

Estos programas, también conocidos como MUA (Mail User Agent), son las herramientas primordiales para iniciar la comunicación por correo electrónico y acceder a los mensajes recibidos y son, por tanto, fundamentales en los extremos de la comunicación digital.

En el mercado actual, existe una amplia variedad de clientes de correo electrónico, adaptados a las preferencias y necesidades de los usuarios. Aunque cada uno tiene sus características particulares, todos comparten el mismo objetivo: facilitar la gestión integral del correo electrónico.

En cuanto a los **tipos de clientes** de correo electrónico, se pueden destacar dos grandes categorías:

**▸** ***Software*** **instalado en el equipo del usuario:** este tipo de cliente de correo se instala directamente en el dispositivo del usuario, funcionando como cualquier otro programa. Dentro de esta categoría, podemos diferenciar entre los clientes de correo en modo gráfico y los de modo texto. Los clientes de correo en modo gráfico, como Claws, Outlook y Evolution, son populares por su interfaz visual, que hace que su uso sea intuitivo y atractivo. Estos clientes permiten a los usuarios interactuar con el correo de una manera cómoda y eficiente, facilitando tareas como la lectura y el envío de mensajes, así como la gestión de contactos y calendarios. Por otro lado, los clientes de correo en modo texto, como Mutt y Alpine, se manejan a través del intérprete de comandos del sistema operativo. Aunque su uso no es tan cómodo ni visualmente atractivo, son herramientas poderosas para usuarios avanzados y administradores de sistemas, especialmente útiles para realizar pruebas y verificar el correcto funcionamiento de servidores de correo recién configurados.

**▸ Webmail:** este tipo de cliente de correo electrónico se encuentra integrado en páginas web y es accesible desde cualquier navegador de Internet. Estos clientes son, quizás, los más utilizados, ya que permiten a los usuarios enviar, recibir y gestionar sus correos electrónicos desde cualquier lugar con acceso a Internet. La principal ventaja del Webmail es su accesibilidad, ya que no requiere la instalación de *software* adicional en el dispositivo del usuario. Además, estos clientes de correo suelen operar mediante el protocolo IMAP, lo que facilita la sincronización de correos en diferentes dispositivos. Ejemplos populares de clientes Webmail incluyen a Gmail, Hotmail y Horde.

Finalmente, algunos de los clientes de correo electrónico más populares hoy en día son aquellos que combinan **funcionalidad con accesibilidad.** Entre ellos se encuentran las **aplicaciones Webmail multinavegador** como Horde, Gmail y Hotmail, que permiten una gestión del correo electrónico desde cualquier dispositivo

Servicios en Red e Internet 23 Tema . Material de estudio con acceso a Internet. También destacan aplicaciones dedicadas como Microsoft Outlook y FoxMail para sistemas Windows y KMail o Thunderbird, que están disponibles tanto para Linux como para Windows. Estas aplicaciones ofrecen una gama de funcionalidades avanzadas, adaptándose a las diversas necesidades de los usuarios, desde la simple gestión de correos hasta la integración con calendarios y tareas.

Servidor de correo electrónico

Como se ha mencionado anteriormente, el servicio de correo electrónico se basa en una arquitectura cliente/servidor, lo que implica la necesidad de comprender en profundidad el concepto de servidor de correo electrónico para completar este modelo.

Aunque a lo largo del tema se ha hecho referencia al término servidor de correo electrónico en varias ocasiones, aún no se ha ofrecido una definición clara.

En este contexto, un servidor de correo electrónico es un *software* o aplicación especializada que permite a un dispositivo realizar funciones clave como enviar, recibir, almacenar o distribuir correos electrónicos a través de una red.

Es importante destacar que no es necesario que un único servidor de correo electrónico asuma todas estas funciones. En una red, y especialmente en Internet, podemos encontrar **diferentes tipos** de servidores de correo electrónico que cumplen roles específicos.

Por ejemplo, existen los **servidores emisores,** que son responsables de enviar los correos electrónicos a solicitud de los clientes de correo electrónico. Estos servidores toman los mensajes redactados por los usuarios y los envían al destino correspondiente.

Por otro lado, están los **servidores encaminadores,** cuya función es distribuir los correos electrónicos a lo largo de la red hasta que estos lleguen a su destino final. Estos servidores actúan como intermediarios, asegurando que los correos electrónicos se dirijan a la ruta correcta dentro de la vasta infraestructura de Internet. Son cruciales en el proceso de transmisión, especialmente cuando el correo debe atravesar múltiples redes o servidores antes de llegar al destinatario final.

Finalmente, tenemos los **servidores receptores,** que reciben y almacenan los correos electrónicos dirigidos a los destinatarios en los buzones correspondientes. Estos servidores garantizan que los mensajes lleguen a la bandeja de entrada del destinatario, donde se almacenan hasta que el usuario decida leerlos, eliminarlos o archivarlos.

En muchas ocasiones, los servidores emisores y encaminadores de correo electrónico se denominan **servidores SMTP** (Simple Mail Transfer Protocol) o **MTA** (Mail Transfer Agents). Estos servidores son esenciales en la fase inicial y media del proceso de envío de correos electrónicos, ya que gestionan la transmisión efectiva de los mensajes a través de la red. Su labor es crucial para garantizar que los correos electrónicos lleguen a su destino de manera eficiente y segura.

Por otro lado, los servidores que se encargan de recibir y almacenar los correos electrónicos de los destinatarios, conocidos como **servidores receptores,** a menudo se denominan **servidores POP** (Post Office Protocol), **IMAP** (Internet Message Access Protocol) o **MDA** (Mail Delivery Agents). Estos servidores juegan un papel fundamental en la última etapa del proceso de entrega de correos electrónicos, asegurando que los mensajes se guarden en los buzones correctos y estén disponibles para su acceso en cualquier momento.

En el mercado actual, existen diversas aplicaciones que permiten a un dispositivo operar como un servidor de correo electrónico. Algunas de las opciones más populares incluyen hMailServer para sistemas Microsoft y el paquete Microsoft

Exchange para Windows Server 2008. Para los usuarios de sistemas basados en Linux, aplicaciones como Postfix y Sendmail en Ubuntu son ampliamente utilizadas. Estos programas ofrecen una amplia gama de funciones y configuraciones que permiten a las organizaciones gestionar sus comunicaciones de correo electrónico de manera eficiente y segura.

En resumen, un servidor de correo electrónico es una pieza clave en la infraestructura de comunicaciones digitales. Dependiendo de su función específica, puede actuar como emisor, encaminador o receptor de correos electrónicos, garantizando que los mensajes se transmitan de manera efectiva desde el remitente hasta el destinatario final. La elección del *software* adecuado para esta tarea dependerá de las necesidades específicas de cada red y del entorno operativo en el que se desee implementar.

![Figura 4. Funcionamiento servidor de correo. Fuente: boss667, 2012.](images/image-6.png)

*Figura 4. Funcionamiento servidor de correo. Fuente: boss667, 2012.*

## 6.5. Buzón de correo electrónico

El concepto de buzón de correo electrónico resulta familiar si lo comparamos con el sistema tradicional de correo postal. Se puede definir como el **espacio de** **almacenamiento,** que puede ser un único directorio o un conjunto de ellos, dentro de un servidor de correo electrónico, en el que se almacenan los mensajes asociados a una o varias cuentas de correo. Este espacio es donde se guarda toda la correspondencia electrónica destinada a un usuario y su funcionamiento guarda una notable similitud con el buzón físico que tenemos en nuestros hogares.

En términos sencillos, un buzón de correo electrónico cumple una función muy similar a la del buzón de casa. En nuestro buzón físico, recibimos no solo nuestra correspondencia personal, sino también la de otras personas que viven en la misma dirección. De igual manera, un buzón de correo electrónico almacena todos los mensajes enviados a una **dirección de correo específica,** pudiendo ser compartido por varios usuarios en ciertas configuraciones. Además, al igual que en el buzón físico recibimos frecuentemente publicidad no deseada, en el buzón de correo electrónico también es habitual recibir **mensajes no solicitados o** ***spam,*** que pueden ser tanto molestos como perjudiciales.

Es importante tener en cuenta que el **espacio disponible** en un buzón de correo electrónico, al igual que en un buzón físico, es limitado. Si no gestionamos adecuadamente el espacio y dejamos que se acumule demasiada correspondencia, podríamos quedarnos sin capacidad para recibir nuevos mensajes. En un buzón de correo electrónico, esto se traduce en la necesidad de revisar y limpiar regularmente los correos almacenados, eliminando aquellos archivándolos en otro lugar para liberar espacio. que ya no sean necesarios o

El diseño de un buzón de correo electrónico puede variar, existiendo dos estrategias principales para su implementación en un servidor de correo. Estas **estrategias** se conocen como **mbox y maildir** y cada una tiene sus propias características y ventajas.

Mbox

Este es el **método tradicional** para el almacenamiento de correos electrónicos en un servidor. Con este formato, todos los correos electrónicos de un buzón se almacenan en un único archivo dentro de un solo directorio. A medida que se van recibiendo nuevos mensajes, estos se concatenan al final de ese archivo, formando una cadena de correos electrónicos almacenados en el mismo lugar.

Sin embargo, este enfoque requiere un **sistema de bloqueo** para evitar que dos procesos accedan al archivo simultáneamente, ya que esto podría corromper los datos o hacer que el archivo se vuelva ilegible.

Maildir

Este es un formato más **moderno y avanzado** que el Mbox. En lugar de almacenar todos los correos en un único archivo, Maildir organiza cada mensaje en **archivos** **individuales,** utilizando una estructura de varios subdirectorios para gestionar los correos.

En este sistema, los correos se distribuyen en tres **directorios principales:**

**▸ tmp:** aquí se almacenan temporalmente los correos que están en proceso de ser guardados de manera permanente.

**▸ new:** este directorio guarda los correos electrónicos que han sido recibidos, pero que aún no han sido leídos o accedidos por el usuario.

**▸ cur:** una vez que un correo ha sido leído por el usuario, se mueve a este directorio.

El formato maildir tiene la ventaja de evitar los problemas de concurrencia que afectan al formato mbox, ya que cada mensaje se maneja de manera independiente. Esto **reduce el riesgo** de corrupción de datos y **mejora la eficiencia** del sistema, especialmente en servidores con un gran volumen de correos.

Si en algún momento es necesario cambiar de un formato de buzón a otro, es importante destacar que los formatos mbox y maildir **no son compatibles entre sí.** Por lo tanto, para realizar una migración de un sistema a otro, se necesitará utilizar una herramienta específica que pueda convertir los correos de un formato a otro.

En resumen, el buzón de correo electrónico es una parte esencial de la infraestructura del correo electrónico, actuando como el punto de almacenamiento y acceso a los mensajes recibidos. Su correcta gestión es fundamental para asegurar que el correo electrónico funcione de manera eficiente y sin interrupciones, independientemente del formato utilizado para almacenar los correos.

## 6.6. Cuentas de correo electrónico, alias y listas de

## distribución

Para utilizar el servicio de correo electrónico, ya sea para enviar o recibir mensajes, es imprescindible contar con una cuenta de correo electrónico. Este concepto se asemeja a la dirección postal tradicional, ya que necesitamos una dirección de contacto para enviar correspondencia y recibir cartas y paquetes.

Una cuenta de correo electrónico actúa como un identificador alfanumérico que asocia a un usuario con un buzón específico en un servidor de correo.

Esta cuenta define el espacio de almacenamiento en el servidor al que se envían todos los correos electrónicos del usuario.

Aunque la terminología puede variar, se utiliza comúnmente el término dirección de correo electrónico para referirse a este **identificador.** Hoy en día, además de la opción de instalar y configurar nuestro propio servidor de correo y crear cuentas en él, existen numerosos proveedores de servicios de correo electrónico, como Outlook, Gmail y Yahoo! que ofrecen cuentas gratuitas. En sus inicios, estas cuentas solían ser de pago.

Cada cuenta de correo electrónico está estructurada en tres **partes clave:**

**▸ Nombre de usuario:** esta es la primera parte de la cuenta y se refiere a la identificación del usuario asociado al buzón en el servidor. Elegir un nombre de usuario adecuado es importante, ya que será la forma en que el usuario será identificado al recibir correos. Es recomendable utilizar un nombre de usuario que sea claro y profesional.

**▸ El símbolo @:** este símbolo, introducido por Ray Tomlinson en 1971, sirve para separar el nombre de usuario del dominio del servidor de correo. Su función es designar que el nombre de usuario está asociado con un servidor específico.

**▸ Identificador del servidor:** la última parte de la cuenta indica el servidor de correo donde se encuentra el buzón del usuario. Este identificador generalmente se presenta como un nombre de dominio DNS, aunque también puede expresarse como una dirección IP.

Como las cuentas de correo electrónico son públicas, es crucial protegerlas con una contraseña segura, similar a cómo usamos una llave para asegurar nuestro buzón de correo físico. Es vital elegir contraseñas robustas para evitar el acceso no autorizado y el uso indebido, como el envío de *spam.*

Una vez que tenemos una cuenta de correo electrónico y una contraseña, se necesita un cliente de correo electrónico, ya sea un *software* específico o una aplicación web, para acceder al buzón, enviar, recibir, leer y gestionar correos electrónicos.

Alias de correo electrónico

Los alias de correo electrónico permiten **gestionar múltiples cuentas de correo** sin tener que manejar varias bandejas de entrada. Por ejemplo, en un entorno corporativo, podríamos necesitar manejar tanto una cuenta general como info@miempresa.com como una cuenta personal como empleado@miempresa.com. En lugar de crear y gestionar dos cuentas separadas, se puede configurar un alias.

Un alias de correo electrónico es una técnica que permite que varias direcciones de correo electrónico se asocien a un solo buzón.

Esto significa que todos los correos electrónicos enviados a diferentes alias llegarán al mismo buzón. Por ejemplo, la cuenta principal podría ser empleado@miempresa.com, e info@miempresa.com sería un alias.

Existen dos tipos principales de alias:

**▸ Alias por nombre de usuario:** este tipo de alias es el más común. Aquí, el alias se crea sobre el nombre de usuario, manteniendo el mismo identificador de servidor.

Por ejemplo, servred@decroly.com podría ser un alias de pgarralda@decroly.com.

**▸ Alias por nombre DNS:** este tipo es menos común. Aquí, el alias se basa en el nombre del servidor, manteniendo el mismo nombre de usuario. Por ejemplo, pgarralda@gmail.com podría ser un alias de pgarralda@decroly.com.

Usar alias ofrece varias **ventajas:**

**▸** Simplifica la gestión al permitir que todos los correos lleguen a un único buzón.

**▸** Proporciona una apariencia más profesional para las direcciones de correo, como info@miempresa.com en lugar de joseluis@miempresa.com.

**▸** Facilita la migración entre servidores de correo, ya que los alias pueden redirigir correos antiguos a nuevas cuentas sin pérdida de mensajes.

**▸** El uso de alias reduce el número total de buzones necesarios, ahorrando espacio y recursos.

Listas de distribución

Las listas de distribución son una herramienta que permite **enviar correos** **electrónicos a múltiples destinatarios simultáneamente.** Funcionan como un alias masivo que no está asociado a un buzón específico, sino que agrupa múltiples direcciones de correo electrónico. Cuando se envía un mensaje a una lista de distribución, se redirige a todos los buzones asociados con esa lista.

Esta funcionalidad es especialmente útil para el **envío masivo de correos** **electrónicos,** como en campañas de *marketing* o notificaciones a grupos grandes. Sin embargo, también puede ser utilizada para enviar *spam* si no se gestiona adecuadamente. Las listas de distribución simplifican la comunicación con varios destinatarios y son una herramienta eficiente para mantener a múltiples personas informadas con un solo envío de correo.

En resumen, el concepto de cuenta de correo electrónico, junto con la utilización de alias y listas de distribución, optimiza la gestión del correo electrónico, proporcionando eficiencia y organización tanto en el ámbito personal como profesional.

## 6.7. Referencias bibliográficas

boss667. (2012, julio 7). Introducción al servidor de correo Postfix. *Syconet.* [https://syconet.wordpress.com/2012/07/07/introduccion-al-servidor-de-correo-postfix/](https://syconet.wordpress.com/2012/07/07/introduccion-al-servidor-de-correo-postfix/)

El correo electrónico. (s. f.). *Apuntes Informática FP.* [https://www.apuntesinformaticafp.com/cursos/servicio_correo.html](https://www.apuntesinformaticafp.com/cursos/servicio_correo.html)

UCAM Universidad Católica de Murcia. (2018, mayo 23). *Administración de sistemas* *- Protocolo SMTP - Fernando Terroso* [Fotograma]. YouTube. [https://www.youtube.com/watch?v=mwFjf6-IrU4](https://www.youtube.com/watch?v=mwFjf6-IrU4)

# SlidePlayer. [https://slideplayer.es/slide/5435094/](https://slideplayer.es/slide/5435094/)

## Elementos del servicio de correo electrónico

Navarrete Castro, C. (2015). Elementos del servicio de correo electrónico. Aquí tienes una presentación donde se trata, de forma esquemática, todo lo relacionado con el mundo del correo electrónico, desde agentes, servidores, clientes, estructura de los correos, relación con servidores DNS, hasta los diferentes protocolos de correo que existen.

# contenedores-docker/

## Servidor de correo electrónico con contenedores

## Docker

Dondoker. (2016, junio 4. Servidor de correo electrónico con contenedores Docker. *Blog Dondoker.* <https://dondocker.com/servidor-de-correo-electronico-con->

¿Quieres tener un servidor de correo en un servidor Docker? Aquí se explica cómo conseguirlo. Aprovecha las ventajas que te ofrece la estructura Docker para instalar tu servidor de correo.

# correo-electronico-como-funciona

## Servidor de correo electrónico, ¿cómo funciona?

Lara Galicia, F. P. (2023, octubre 31). Servidor de correo electrónico, ¿cómo funciona? *GoDaddy.* <https://www.godaddy.com/resources/latam/stories/servidor-de-> ¿Te ha quedado claro que es un servidor de correo electrónico y para qué se utiliza?, ¿qué ventajas y desventajas tiene usar un servidor de correo gratuito?, ¿qué relación tiene un servidor DNS con un servidor de correo electrónico? Todo esto se te explica en este documento.

## Tu dirección de correo electrónico temporal

TempMail. (s. f.). *¿Qué es el E-mail temporal desechable?* [https://temp-mail.org/es/](https://temp-mail.org/es/)

¿Quieres acceder a formularios, foros y grupos de discusión, pero no te apetece indicar tu cuenta de correo electrónico por temor a recibir spam? Tu identidad nunca será revelada ni vendida a nadie, evitando de esa manera el correo basura.

IMAP y POP3: ¿En qué se diferencian y cuándo usar cada uno?

IMAP y POP3: ¿En qué se diferencian y cuándo usar cada uno? (s. f.). *Vadavo.* [https://www.vadavo.com/blog/correo-imap-pop3-que-son-y-cuando-usarlos/](https://www.vadavo.com/blog/correo-imap-pop3-que-son-y-cuando-usarlos/)

Seguro que te quedan dudas de cuál es el protocolo más adecuado para configurar tu servidor de correo electrónico. Aquí encontrarás cuales son las ventajas y desventajas de cada uno y cuando se recomienda usar uno u otro.

# sirve? (+ herramientas). Email Vendor Selection.

# [https://www.emailvendorselection.com/es/que-es-smtp/](https://www.emailvendorselection.com/es/que-es-smtp/)

## ¿Qué es SMTP? ¿Cómo funciona y para qué sirve?

Kasianenko, S. (2023, septiembre 21). ¿Qué es SMTP? ¿Cómo funciona y para qué Esta página web, además de explicarte el protocolo, te enseña los diferentes comandos con los que interactuar con el servidor y te muestra cuales son los errores más comunes y porque suceden.

## Correo electrónico. Parte 1

Universitat Politècnica de València. (2016, octubre 5). *Correo electrónico - 1 | 18/38 |* *UPV* [Vídeo]. YouTube. [https://www.youtube.com/watch?v=PmL-RCzxkcY](https://www.youtube.com/watch?v=PmL-RCzxkcY)

Primera parte de dos vídeos muy interesantes que te explican todo lo relacionado con el correo electrónico, desde los diferentes protocolos hasta el tratamiento del spam y como evitarlo.

![image-7](images/image-7.png)

Accede al vídeo: [https://www.youtube.com/embed/PmL-RCzxkcY](https://www.youtube.com/embed/PmL-RCzxkcY)

## Correo electrónico. Parte 2

Universidad politècnica de València. (2016, octubre 5). *Correo electrónico - 2 | 19/38* *| UPV* [Vídeo]. YouTube. [https://www.youtube.com/watch?v=cDlRRrD9KI0](https://www.youtube.com/watch?v=cDlRRrD9KI0)

Segunda parte de dos vídeos muy interesantes que te explican todo lo relacionado con el correo electrónico, desde los diferentes protocolos hasta el tratamiento del *spam* y como evitarlo.

# - Tema 7: Correo electrónico - Fernando Terroso [Vídeo]. YouTube.

# [https://www.youtube.com/watch?v=xR1TN77J21Q&t=198s](https://www.youtube.com/watch?v=xR1TN77J21Q%2526t=198s)

## Administración de sistemas

UCAM Universidad Católica de Murcia. (2018, mayo 23). *Administración de sistemas* Afianza tus conocimientos mediante la visualización de este vídeo., donde aparte de explicarte el funcionamiento del servicio de correo electrónico, te describe como están configuradas las partes de un correo electrónico.

![image-8](images/image-8.png)

Accede al vídeo: [https://www.youtube.com/embed/PmL-RCzxkcY](https://www.youtube.com/embed/PmL-RCzxkcY)

# - Protocolo IMAP - Fernando Terroso [Vídeo]. YouTube.

# [https://www.youtube.com/watch?v=23BNEeM_K2w](https://www.youtube.com/watch?v=23BNEeM_K2w)

## Administración de sistemas - Protocolo IMAP

UCAM Universidad Católica de Murcia. (2018, mayo 23). *Administración de sistemas* Todo lo que querías saber del protocolo IMAP, explicado muy claramente en este vídeo. También, tienes una comparativa IMAP/POP3 para que puedas decidir cuál es el mejor protocolo que utilizar.

![image-9](images/image-9.png)

Accede al vídeo: [https://www.youtube.com/embed/23BNEeM_K2w](https://www.youtube.com/embed/23BNEeM_K2w)

# - Protocolo SMTP - Fernando Terroso [Vídeo]. YouTube.

# [https://www.youtube.com/watch?v=mwFjf6-IrU4](https://www.youtube.com/watch?v=mwFjf6-IrU4)

## Administración de sistemas - Protocolo SMTP

UCAM Universidad Católica de Murcia. (2018, mayo 23). *Administración de sistemas* Aquí vas a descubrir todos los comandos que están involucrados en todas las fases posibles que pueden suceder en una comunicación SMTP. Entender estos comandos y sus respuestas te ayudarán a entender el funcionamiento de este protocolo.

![image-10](images/image-10.png)

Accede al vídeo: [https://www.youtube.com/embed/23BNEeM_K2w](https://www.youtube.com/embed/23BNEeM_K2w)

# - Protocolo POP - Fernando Terroso [Vídeo]. YouTube.

# [https://www.youtube.com/watch?v=lhMOh2RSo30](https://www.youtube.com/watch?v=lhMOh2RSo30)

## Administración de sistemas - Protocolo POP - Fernando Terroso

UCAM Universidad Católica de Murcia. (2018, mayo 23). *Administración de sistemas* Aquí tienes la explicación completa del funcionamiento del último protocolo del correo electrónico, el protocolo POP. Este recurso, también, te muestra las diferentes fases por las que sucede este protocolo.

![image-11](images/image-11.png)

Accede al vídeo: [https://www.youtube.com/embed/lhMOh2RSo30](https://www.youtube.com/embed/lhMOh2RSo30)

## Entrenamiento 1. Clientes de correo electrónico

**▸ Planteamiento del ejercicio**

#### Apartado 1

Se desea obtener una cuenta de correo electrónico gratuita. Una buena opción es el servicio gratuito Gmail que proporciona Google:

**▸** Crear una cuenta de correo electrónico Gmail. La cuenta tendrá una estructura como la siguiente si es posible: nombre.apellido.unir@gmail.com, donde el nombre y el apellido serán tu nombre y tu primer apellido.

**▸** Una vez que hayas creado la cuenta, accede a ella por Webmail a través de la página oficial de Google y verifica que funciona correctamente enviándote un correo electrónico a ti mismo.

#### Apartado 2

Se desea utilizar la aplicación Sylpheed instalada en cliente Ubuntu como cliente de correo electrónico:

**▸** Agrega la cuenta de correo electrónico creada en el Apartado 1 para ser utilizada con el protocolo IMAP. Verifica el correcto funcionamiento enviándote un correo a ti mismo. ¿Qué ocurre si borras un correo con Sylpheed? ¿Se borra también en el servidor de correo electrónico?

**▸** Elimina la cuenta agregada antes y vuelve a agregarla otra vez, pero en este caso, configúrala para ser utiliza con el protocolo POP3. Verifica el correcto funcionamiento enviándote un correo a ti mismo. ¿Dónde almacena Sylpheed los correos electrónicos que se descarga al equipo local?

#### Apartado 3

Se desea utilizar la aplicación Thunderbird como cliente de correo electrónico en cliente Ubuntu:

**▸** Instala la aplicación Thunderbird en el cliente Ubuntu y configúrala para que se pueda utilizar en castellano.

**▸** Agrega la cuenta de correo electrónico creada en el apartado a) para ser utilizada con el protocolo IMAP. Verifica el correcto funcionamiento enviándote un correo a ti mismo. ¿Qué ocurre si borras un correo con Thunderbird? ¿Se borra también en el servidor de correo electrónico?

**▸** Elimina la cuenta agregada antes y vuelve a agregarla otra vez, pero en este caso, configúrala para ser utiliza con el protocolo POP3. Verifica el correcto funcionamiento enviándote un correo a ti mismo. ¿Dónde almacena Thunderbird los correos electrónicos que se descarga al equipo local?

Para ello puedes valerte de máquinas virtuales en un entorno virtual como VirtualBox.

**▸ Desarrollo paso a paso**

Sigue los pasos planteados en cada apartado y resuelve las cuestiones analizando los resultados.

**▸ Solución**

#### Apartado 1

Para crear una cuenta de correo electrónico gratuita en Gmail, sigue estos pasos:

#### Paso 1. Crear una cuenta de correo electrónico en Gmail

**▸** Accede a la página de registro de Gmail:

**•** Abre tu navegador web y ve a [https://accounts.google.com/signup](https://accounts.google.com/signup)

**▸** Completa el formulario de registro:

- Nombre: ingresa tu nombre y apellido.

- Nombre de usuario: intenta crear una dirección de correo que siga la estructura nombre.apellido.unir@gmail.com. Si esa dirección ya está tomada, Gmail te sugerirá otras alternativas. Es posible que tengas que probar con variaciones (por ejemplo, agregar un número o intercambiar el orden de las palabras) hasta que encuentres una dirección disponible que te guste.

- Contraseña: elige una contraseña segura y luego confírmala.

**▸** Completa los datos adicionales:

- Ingresa tu número de teléfono y una dirección de correo electrónico de recuperación. Esto es opcional, pero recomendable para mayor seguridad.

- Ingresa tu fecha de nacimiento y tu género.

**▸** Aceptar los términos y condiciones:

- Revisa los términos y condiciones de Google y acéptalos.

**▸** Verificación:

**•**

**•** Google podría pedirte que verifiques tu cuenta mediante un código enviado a tu teléfono móvil. Si es así, ingresa el código que recibas.

#### Paso 2. Accede a tu cuenta de Gmail

**▸** Inicia sesión: **•** Ve a [https://mail.google.com](https://mail.google.com/) e ingresa con tu nueva dirección de correo electrónico y contraseña. **▸** Envía un correo de prueba:

- Una vez que hayas iniciado sesión en tu cuenta de Gmail, haz clic en «Redactar» para crear un nuevo correo electrónico.

- En el campo «Para», ingresa tu propia dirección de correo electrónico.

- Escribe un asunto y un mensaje corto.

- Haz clic en «Enviar».

**▸** Verifica que el correo ha sido recibido:

- Ve a la bandeja de entrada y verifica que has recibido el correo que acabas de enviarte.

Consejos adicionales:

**▸** Guarda tu contraseña: asegúrate de recordar tu contraseña o guardarla en un lugar seguro.

**▸** Configura la autenticación en dos pasos: para mayor seguridad, puedes habilitar la autenticación en dos pasos en la configuración de tu cuenta.

Una vez completados estos pasos, habrás creado con éxito tu cuenta de Gmail y verificado que funciona correctamente.

#### Apartado 2

Aquí tienes las instrucciones detalladas para configurar y utilizar Sylpheed con la cuenta de Gmail que creaste tanto con el protocolo IMAP como con el protocolo POP3 en un cliente Ubuntu. También, responderé a las preguntas relacionadas con el borrado de correos y el almacenamiento local.

#### Paso 1. Configurar la cuenta de correo en Sylpheed con IMAP

**▸** Abrir Sylpheed:

- Abre la aplicación Sylpheed en tu sistema Ubuntu.

**▸** Agregar la cuenta de correo:

- Ve a «Configuración» y selecciona «Crear nueva cuenta de correo».

- En «Nombre de la cuenta», pon un nombre descriptivo, como Gmail IMAP.

- Ingresa tu nombre y dirección de correo electrónico (la cuenta de Gmail que creaste).

- En «Servidor de correo entrante (IMAP)», ingresa «imap.gmail.com».

- En «Servidor de correo saliente (SMTP)», ingresa «smtp.gmail.com».

- Activa las casillas que indican que los servidores requieren autenticación y utiliza tu dirección de correo y contraseña para autenticarte.

**▸** Configuración avanzada:

- IMAP: asegúrate de que el puerto para IMAP sea 993 y que la opción «Usar conexión segura (SSL)» esté habilitada.

- SMTP: asegúrate de que el puerto para SMTP sea 465 o 587 y que también esté habilitada la opción «Usar conexión segura (SSL)».

- Termina el asistente de configuración y guarda los cambios.

**▸** Verificación:

- Para asegurarte de que todo funciona correctamente, envíate un correo electrónico a ti mismo y verifica que lo recibes.

¿Qué ocurre si borras un correo con Sylpheed utilizando IMAP? Si configuras tu cuenta con IMAP y borras un correo en Sylpheed, el correo también se borrará en el servidor de Gmail. IMAP sincroniza las acciones entre el cliente y el servidor, por lo que cualquier cambio que hagas en Sylpheed (como borrar un correo) se reflejará en la cuenta de Gmail accesible desde la web.

#### Paso 2. Configurar la cuenta de correo en Sylpheed con POP3

**▸** Eliminar la cuenta IMAP:

- Ve a «Configuración» > «Configuración de cuenta» y selecciona la cuenta IMAP que configuraste antes. Luego, haz clic en «Eliminar».

**▸** Agregar la cuenta de correo con POP3. Repite el proceso de agregar una cuenta nueva, pero esta vez:

- En «Servidor de correo entrante (POP3)», ingresa «pop.gmail.com».

- Configura el puerto a 995 y habilita la opción «Usar conexión segura (SSL)».

- Configura el SMTP como antes (smtp.gmail.com).

**▸** Configuración adicional para POP3:

- En la configuración de la cuenta, puedes decidir si deseas que los correos se borren del servidor después de descargarlos o si quieres mantener una copia en el servidor. Si deseas que se mantengan en el servidor, busca y marca la opción «Mantener mensajes en el servidor» en la configuración avanzada.

**▸** Verificación:

- Envíate un correo electrónico para verificar que la cuenta funciona correctamente.

¿Dónde almacena Sylpheed los correos electrónicos descargados al equipo local con POP3? Cuando usas POP3, los correos electrónicos se descargan al almacenamiento local del equipo y se guardan en la carpeta de correo de Sylpheed. En un sistema Ubuntu, por defecto, estos correos se almacenan en una carpeta en tu directorio de inicio. Generalmente, los archivos se encuentran en: ~/.sylpheed-2.0/

Esta ruta puede variar dependiendo de la versión de Sylpheed y las configuraciones específicas que hayas hecho.

Resumen:

**▸** IMAP: los correos borrados en Sylpheed también se borran en el servidor.

**▸** POP3: los correos se almacenan localmente y, dependiendo de la configuración, podrían borrarse del servidor tras la descarga. Sylpheed almacena los correos en

~/.sylpheed-2.0/ en Ubuntu.

#### Apartado 3

Aquí tienes una guía detallada para instalar y configurar Thunderbird en Ubuntu (en español) y para agregar tu cuenta de correo tanto con el protocolo IMAP como POP3.

#### Paso 1. Instalar Thunderbird en Ubuntu y configurarlo en español

Instalar Thunderbird:

**▸** Abre una terminal en tu sistema Ubuntu y ejecuta el siguiente comando para instalar Thunderbird:

![image-12](images/image-12.png)

**▸** Esto instalará Thunderbird en tu sistema.

Configurar Thunderbird en español:

**▸** Abre Thunderbird.

**▸** Ve al menú (tres líneas horizontales en la esquina superior derecha) y selecciona

«Preferences» (preferencias) o «Options» (opciones). **▸** Busca la sección «General» y luego «Language» (idioma). **▸** Si el idioma español no está disponible, puedes instalarlo desde el gestor de complementos:

- Ve a «Herramientas» > «Complementos» > «Extensiones».

- Busca «Language Pack Spanish» (paquete de idioma español) y añádelo.

- Reinicia Thunderbird para que los cambios tengan efecto.

#### Paso 2. Agregar la cuenta de correo con IMAP en Thunderbird

**▸** Agregar cuenta IMAP:

- Abre Thunderbird y en la pantalla de bienvenida selecciona «Correo electrónico».

- Ingresa tu nombre, dirección de correo electrónico (la cuenta Gmail que creaste) y tu contraseña.

- Thunderbird debería detectar automáticamente la configuración para IMAP.

- Verifica el servidor de correo entrante: IMAP, imap.gmail.com, puerto 993, SSL/TLS.

- Verifica el servidor de correo saliente: SMTP, smtp.gmail.com, puerto 465 o 587,

SSL/TLS.

- Haz clic en «Hecho» para completar la configuración.

**▸** Verificación:

- Envía un correo a tu propia dirección para verificar que la cuenta está funcionando correctamente.

- Asegúrate de recibir el correo en la bandeja de entrada.

¿Qué ocurre si borras un correo con Thunderbird utilizando IMAP? Al borrar un correo en Thunderbird configurado con IMAP, el correo se borra también en el servidor de Gmail. IMAP sincroniza los cambios entre el cliente (Thunderbird) y el servidor (Gmail), por lo que cualquier correo que elimines en Thunderbird será eliminado en el servidor de correo.

#### Paso 3. Configurar la cuenta de correo con POP3 en Thunderbird

**▸** Eliminar la cuenta IMAP:

- Ve al menú (tres líneas horizontales) > «Opciones de cuenta» > selecciona la cuenta que configuraste y haz clic en «Eliminar cuenta».

**▸** Agregar cuenta POP3:

- Repite el proceso de agregar una cuenta nueva, pero esta vez selecciona manualmente la configuración de POP3.

- Servidor de correo entrante: POP3, pop.gmail.com, puerto 995, SSL/TLS.

- Servidor de correo saliente: SMTP, smtp.gmail.com, puerto 465 o 587, SSL/TLS.

- Completa la configuración.

**▸** Configuración adicional para POP3:

- En las opciones de la cuenta, puedes decidir si deseas mantener una copia de los correos en el servidor después de descargarlos. Para ello, ve a «Configuración de cuenta» > «Configuración del servidor» y marca la opción «Dejar los mensajes en el servidor» si no deseas que se borren de Gmail después de descargarlos.

**▸** Verificación:

- Envía un correo a tu propia dirección y verifica que lo recibes en Thunderbird.

¿Dónde almacena Thunderbird los correos electrónicos descargados al equipo local con POP3? Cuando configuras Thunderbird con POP3, los correos se descargan y se almacenan localmente en tu equipo. Por defecto, Thunderbird guarda los correos en un directorio dentro de tu carpeta de perfil. Este perfil generalmente se encuentra en Ubuntu: ~/.thunderbird/xxxxxx.default/ (donde xxxxxx.default es un nombre de carpeta único generado automáticamente).

Dentro de esta carpeta, los correos se almacenan en archivos de formato MBOX sin extensión, como Inbox, Sent, etc., dependiendo de las carpetas de correo.

## Entrenamiento 2. Servidor de correo electrónico

## en Windows

**▸ Planteamiento del ejercicio**

Se desea utilizar el servidor Windows Server 2008 Enterprise como servidor de correo electrónico SMTP y como servidor de correo electrónico IMAP/POP3, para que sea capaz tanto de enviar correos electrónicos, como de recibirlos y entregárselos a los clientes de correo electrónico. Averigua si esta aplicación sirve para implementar un servidor de correo electrónico SMTP o para implementar un servidor de correo IMAP/POP.

Para ello puedes valerte de máquinas virtuales en un entorno virtual como VirtualBox.

**▸ Desarrollo paso a paso**

- Instalación de hMailServer en Windows Server 2008 Enterprise.

- Comprobar que la aplicación está instalada correctamente.

- Configuración de hMailServer.

- ¿Sirve hMailServer para implementar un servidor de correo electrónico SMTP o para implementar un servidor de correo IMAP/POP?

**▸ Solución**

Para configurar un servidor de correo electrónico en Windows Server 2008 Enterprise utilizando hMailServer, puedes seguir estos pasos:

#### Paso 1. Instalación de hMailServer en Windows Server 2008 Enterprise

Pasos de instalación: **▸** Descargar hMailServer:

- Ve al sitio web oficial de hMailServer y descarga la última versión disponible del instalador.

**▸** Ejecutar el instalador:

- Ejecuta el archivo descargado para iniciar el proceso de instalación.

**▸** Seleccionar componentes:

- Durante la instalación, selecciona los componentes que deseas instalar. Asegúrate de incluir el servidor y la consola administrativa.

**▸** Configurar la base de datos:

- hMailServer requiere una base de datos para almacenar información. Puedes elegir usar el motor de base de datos incorporado (Microsoft SQL Compact) o conectarlo a un servidor SQL (como MySQL o SQL Server).

**▸** Configurar la contraseña del administrador:

- Configura una contraseña para el usuario administrador de hMailServer. Esto es esencial para acceder a la consola de administración.

**▸** Finalizar la instalación:

- Completa el proceso de instalación siguiendo las instrucciones en pantalla.

#### Paso 2. Comprobar que la aplicación está instalada correctamente

Pasos de verificación:

**▸** Iniciar hMailServer Administrator:

- Después de la instalación, abre hMailServer Administrator desde el menú de inicio.

**▸** Conectarse al servidor:

- Se te pedirá que ingreses la contraseña del administrador que configuraste durante la instalación.

**▸** Verificar el estado del servidor:

- Una vez dentro de la consola de administración, puedes verificar que el servidor esté corriendo sin errores. Ve a la sección «Status» para revisar el estado general del servidor y sus componentes.

#### Paso 3. Configuración de hMailServer

Pasos de configuración: **▸** Configurar un dominio:

- En la consola de administración, ve a la sección «Domains» y agrega un nuevo dominio. Introduce el nombre del dominio (por ejemplo, tudominio.com).

**▸** Crear cuentas de correo electrónico:

- Dentro del dominio, agrega cuentas de correo electrónico. Por ejemplo, admin@tudominio.com.

**▸** Configurar los protocolos SMTP, IMAP y POP3:

- Ve a la sección «Settings» y configura los servicios para SMTP, IMAP y POP3. Asegúrate de que los puertos predeterminados estén correctamente configurados (SMTP: 25, IMAP: 143, POP3: 110).

**▸** Configurar reglas y listas negras/blancas:

- Puedes establecer reglas para filtrar correos y configurar listas negras o blancas para controlar qué correos se reciben o se bloquean.

**▸** Configurar rutas y dominios externos (opcional):

- Si necesitas reenviar correos a otros servidores o gestionar dominios externos, puedes configurar rutas en la sección «Routes».

**▸** Configurar las opciones de seguridad:

- Configura opciones de seguridad como TLS/SSL para cifrar las comunicaciones de correo y evita que el servidor se convierta en un servidor de *open relay* (que permite enviar correos sin autenticación).

#### Paso 4. ¿Sirve hMailServer para implementar un servidor de correo electrónico

#### SMTP o para implementar un servidor de correo IMAP/POP?

hMailServer sirve para implementar tanto un servidor de correo electrónico SMTP como un servidor de correo IMAP/POP3.

**▸** SMTP (Simple Mail Transfer Protocol): este protocolo se utiliza principalmente para enviar correos electrónicos desde un cliente o desde un servidor a otro servidor de correo. hMailServer puede actuar como un servidor SMTP, manejando el envío y recepción de correos electrónicos.

**▸** IMAP (Internet Message Access Protocol) y POP3 (Post Office Protocol 3): estos protocolos se utilizan para recibir correos electrónicos. hMailServer puede actuar como un servidor IMAP/POP3, permitiendo que los clientes de correo electrónico (como Outlook, Thunderbird, etc.) accedan a los correos almacenados en el servidor.

Por lo tanto, hMailServer es una solución completa para gestionar tanto el envío como la recepción de correos electrónicos en tu red.

## Entrenamiento 3. Servidor de correo electrónico

## en Ubuntu

**▸ Planteamiento del ejercicio**

Se desea utilizar el servidor Ubuntu Server como servidor de correo electrónico SMTP y como servidor de correo electrónico IMAP/POP3, para que sea capaz tanto de enviar correos electrónicos como de recibirlos y entregárselos a los clientes de correo electrónico.

**▸ Desarrollo paso a paso**

- Instalar las aplicaciones Postfix y Dovecot en el servidor Ubuntu Server.

- Comprobar que las aplicaciones están instaladas correctamente e indicar su PID.

- ¿Cómo se configura cada una de las aplicaciones?

- ¿Para qué sirve cada aplicación?

**▸ Solución**

#### Instalación de las aplicaciones Postfix y Dovecot

Para instalar Postfix y Dovecot en un servidor Ubuntu, puedes usar los siguientes comandos:

![image-13](images/image-13.png)

#### Comprobación de la instalación e identificación del PID

Después de la instalación, puedes comprobar que los servicios están instalados y ejecutándose con los siguientes comandos:

**▸** Para Postfix:

![image-14](images/image-14.png)

**▸** Para Dovecot:

![image-15](images/image-15.png)

Para obtener el PID de cada servicio, puedes usar:

**▸** Postfix:

![image-16](images/image-16.png)

**▸** Dovecot:

![image-17](images/image-17.png)

#### Configuración de las aplicaciones

#### Configuración de Postfix

Archivo de configuración principal:

**▸** El archivo principal de configuración de Postfix es /etc/postfix/main.cf. Algunos de los

parámetros básicos que podrías configurar incluyen:

- myhostname : el nombre del host del servidor.

- mydomain : el dominio principal del servidor.

- myorigin : el dominio que aparecerá en los correos salientes.

- mydestination : especifica los dominios para los que el servidor acepta correo.

- relayhost: configura un servidor SMTP externo si deseas que Postfix reenvíe todos los correos a otro servidor.

- inet_interfaces : configura en qué interfaces de red escuchará el servidor.

![Ejemplo de configuración básica: Ajustar el archivo de configuración:](images/image-18.png)

**▸** Una vez realizada la configuración, reinicia el servicio para aplicar los cambios.

#### Configuración de Dovecot

Archivos de configuración principales: **▸** Los archivos de configuración de Dovecot se encuentran en /etc/dovecot/dovecot.conf y en los directorios conf.d . Configuraciones básicas: **▸** Mail Location: define dónde se almacenarán los correos electrónicos:

![image-19](images/image-19.png)

**▸** Autenticación: configura el método de autenticación (por ejemplo, PAM, LDAP, etc.).

El archivo de configuración relevante es /etc/dovecot/conf.d/10-auth.conf.

![image-20](images/image-20.png)

**▸** Habilitar servicios IMAP/POP3: asegúrate de que los protocolos IMAP y POP3 estén

habilitados en /etc/dovecot/conf.d/20-imap.conf y /etc/dovecot/conf.d/20-pop3.conf .

**▸** IMAP:

![image-21](images/image-21.png)

**▸** POP3:

![image-22](images/image-22.png)

#### ¿Para qué sirve cada aplicación?

#### Postfix

**▸** Función: Postfix es un agente de transferencia de correo (MTA) que se encarga de

enviar y recibir correos electrónicos. Gestiona el enrutamiento y la entrega de correos electrónicos desde y hacia otros servidores SMTP.

**▸** Uso: Postfix es utilizado, principalmente, para enviar correos electrónicos desde tu servidor a otros servidores de correo y para aceptar correos electrónicos entrantes que deben ser entregados localmente o reenviados.

#### Dovecot

**▸** Función: Dovecot es un servidor de correo IMAP y POP3 que se encarga de gestionar el acceso a los buzones de correo. Permite a los clientes de correo (como Thunderbird, Outlook, etc.) conectarse al servidor y descargar o sincronizar sus correos electrónicos.

**▸** Uso: Dovecot es utilizado para ofrecer acceso a los correos electrónicos almacenados en el servidor, permitiendo a los usuarios leer, enviar y gestionar sus correos desde aplicaciones cliente.

Estas aplicaciones combinadas permiten configurar un servidor de correo completo que puede enviar y recibir correos electrónicos y permitir a los usuarios acceder a sus bandejas de entrada a través de clientes de correo.

## Entrenamiento 4. Cuentas de correo electrónico

## con Windows

**▸ Planteamiento del ejercicio**

Se desea utilizar el servidor Windows Server 2008 Enterprise como servidor de correo electrónico (servidor de correo electrónico SMTP y servidor de correo electrónico IMAP/POP3 al mismo tiempo) utilizando la aplicación hMailServer. El servidor deberá tener las siguientes especificaciones:

**▸** El servidor de correo electrónico (tanto el SMTP como el IMAP/POP3) utilizará la dirección IP 192.168.100.100 para llevar a cabo el servicio.

**▸** Tanto el servidor de correo electrónico SMTP como el servidor de correo electrónico IMAP/POP3 deberán estar configurados para requerir autenticación a los usuarios que vayan a utilizarlos para enviar y para acceder a correos electrónicos. El método de autenticación que se va a utilizar será la autenticación en texto plano.

**▸** El servidor de correo electrónico deberá ser capaz de distribuir y entregar correos del dominio miempresa.com.

**▸** Deberá contener las cuentas de correo electrónico maria@miempresa.com, pepe@miempresa.com y ernesto@miempresa.com (contraseña a elección del administrador).

Para finalizar este apartado será necesario agregar al cliente de correo electrónico Thunderbird del cliente Ubuntu las cuentas de correo electrónico creadas anteriormente en el servidor y verificar que funcionan correctamente enviando y recibiendo algún correo electrónico. Configura las cuentas en el cliente Thunderbird utilizando en los dos protocolos de acceso a correos electrónicos, es decir, IMAP y POP3.

**▸ Desarrollo paso a paso**

- Instalación y configuración de hMailServer.

- Configuración de cuentas en Thunderbird (Ubuntu).

- Resolución de problemas.

**▸ Solución**

Para configurar un servidor de correo electrónico en Windows Server 2008 utilizando hMailServer y luego configurarlo en un cliente Thunderbird en ubuntu, sigue estos pasos.

#### Paso 1. Instalación y configuración de hMailServer

Descarga e instalación de hMailServer:

**▸** Descarga hMailServer desde su sitio web oficial.

**▸** Ejecuta el instalador y sigue los pasos hasta completar la instalación.

**▸** Durante la instalación, se te pedirá que configures una contraseña para el

administrador de hMailServer.

Configuración básica del servidor: **▸** Abre la consola de administración de hMailServer. **▸** Conéctate al servidor usando la contraseña de administrador que configuraste durante la instalación. Crear el dominio:

**▸** En el árbol de la izquierda, haz clic derecho en «Domains» y selecciona «Add».

**▸** En «Domain name», ingresa «miempresa.com».

**▸** Haz clic en «Save».

Crear las cuentas de correo electrónico:

**▸** Dentro del dominio `miempresa.com`, selecciona «Accounts» y haz clic en «Add».

**▸** Crea las siguientes cuentas:

- maria@miempresa.com

- pepe@miempresa.com

- ernesto@miempresa.com.

**▸** Define las contraseñas para cada una de las cuentas.

**▸** Haz clic en «Save» después de crear cada cuenta.

Configurar los protocolos SMTP, IMAP y POP3:

**▸** Ve a la sección «Settings» en el árbol de la izquierda.

**▸** SMTP:

- Expande «Protocols» y selecciona «SMTP».

- En la pestaña «Delivery of e-mail», asegúrate de que la IP de escucha sea 192.168.100.100.

- Habilita la opción «Requires authentication for deliveries».

- Haz clic en «Save».

**▸** IMAP:

- Selecciona «IMAP» en la lista de «Protocols».

- Configura la IP de escucha como 192.168.100.100.

- Habilita la autenticación en texto plano (si es necesario).

- Haz clic en «Save».

**▸** POP3:

- Selecciona «POP3» en la lista de "«Protocols».

- Configura la IP de escucha como 192.168.100.100.

- Habilita la autenticación en texto plano.

- Haz clic en «Save».

Configuración de puertos: **▸** Asegúrate de que los puertos necesarios estén abiertos en el *firewall* de Windows:

- SMTP: puerto 25.

- IMAP: puerto 143.

- POP3: puerto 110.

Prueba básica del servidor de correo: **▸** Usa la herramienta de diagnóstico de hMailServer para verificar que el servidor está configurado correctamente. **▸** En la ventana de «Diagnostics», selecciona el dominio que deseas probar en el campo «Domain». En este caso, selecciona «miempresa.com». **▸** La herramienta de diagnóstico comprobará la configuración de DNS, conectividad y funcionamiento general del servidor de correo para el dominio seleccionado.

**▸** Haz clic en «Start» para comenzar la prueba. **▸** La herramienta realizará varias comprobaciones, incluyendo:

- DNS Records: verifica que los registros MX y A estén configurados correctamente para el dominio.

- Connect (SMTP): comprueba si el servidor SMTP está accesible desde el exterior.

- Test local connect: verifica si hMailServer puede enviar correos electrónicos localmente utilizando la configuración SMTP.

- Test inbound port (IMAP/POP3): verifica si los puertos para IMAP y POP3 están abiertos y funcionando.

#### Paso 2. Configuración de cuentas en Thunderbird (Ubuntu)

Instalar Thunderbird en Ubuntu:

**▸** Abre un terminal y ejecuta: sudo apt-get install thunderbird

**▸** Inicia Thunderbird una vez que se complete la instalación.

Configurar cuentas de correo (IMAP y POP3): **▸** IMAP:

- Inicia Thunderbird.

- Haz clic en «Crear una nueva cuenta» y selecciona «Cuenta de correo electrónico».

- Introduce el nombre, dirección de correo (maria@miempresa.com, pepe@miempresa.com, ernesto@miempresa.com) y la contraseña correspondiente.

- Selecciona «Configuración manual» y elige IMAP como protocolo de entrada.

- Configurar los siguientes parámetros.

- Servidor de entrada: 192.168.100.100, puerto: 143, SSL: ninguno, autenticación: contraseña normal.

- Servidor de salida: 192.168.100.100, puerto: 25, SSL: ninguno, autenticación: contraseña normal.

- Haz clic en «Hecho».

**▸** POP3:

- Repite el proceso anterior, pero selecciona POP3 en lugar de IMAP.

- Configurar los siguientes parámetros.

- Servidor de entrada: 192.168.100.100, puerto: 110, SSL: ninguno, autenticación: contraseña normal.

- Servidor de salida: 192.168.100.100, puerto: 25, SSL: ninguno, autenticación: contraseña normal.

- Haz clic en «Hecho».

Verificación del funcionamiento:

**▸** Envía un correo desde una cuenta configurada a otra dentro de Thunderbird.

**▸** Verifica que el correo se envía y se recibe correctamente tanto para IMAP como para POP3.

#### Paso 3. Resolución de problemas

**▸** Si encuentras problemas de conexión, verifica que los puertos mencionados estén abiertos y que no haya bloqueos en el *firewall.*

**▸** Asegúrate de que la autenticación en texto plano está habilitada tanto en el servidor como en Thunderbird.

Con estos pasos, habrás configurado un servidor de correo electrónico funcional en Windows Server 2008 y configurado el acceso en Thunderbird desde Ubuntu usando tanto IMAP como POP3.

## Entrenamiento 5. Autenticación, autorización y control de acceso de un servidor Web con Ubuntu

**▸ Planteamiento del ejercicio**

Se desea utilizar el servidor Ubuntu Server como servidor de correo electrónico (servidor de correo electrónico SMTP y servidor de correo electrónico IMAP/POP3 al mismo tiempo) utilizando las aplicaciónes Postfix y Dovecot. El servidor deberá tener las siguientes especificaciones:

**▸** El servidor de correo electrónico (tanto el SMTP como el IMAP/POP3) utilizará la dirección IP 192.168.200.110 para llevar a cabo el servicio.

**▸** Tanto el servidor de correo electrónico SMTP como el servidor de correo electrónico IMAP/POP3 deberán estar configurados para requerir autenticación a los usuarios que vayan a utilizarlos para enviar y para acceder a correos electrónicos. El método de autenticación que se va a utilizar será la autenticación en texto plano.

**▸** El servidor de correo electrónico deberá ser capaz de distribuir y entregar correos del dominio company.com.

**▸** Deberá contener las cuentas de correo electrónico alonso@company.com, alejandra@company.com y paula@company.com (contraseña a elección del administrador).

Para finalizar este apartado será necesario agregar al cliente de correo electrónico Thunderbird del cliente Ubuntu las cuentas de correo electrónico creadas anteriormente en el servidor y verificar que funcionan correctamente enviando y recibiendo algún correo electrónico. Configura las cuentas en el cliente Thunderbird utilizando en los dos protocolos de acceso a correos electrónicos, es decir, IMAP y POP3.

**▸ Desarrollo paso a paso**

- Instalar Apache en el servidor Ubuntu.

- Configuración de los sitios virtuales en Apache.

- Configuración del DNS.

- Crear usuarios en Ubuntu.

**•** Configurar la autenticación básica en Apache para <www.autorizacion.es>.

**•** Configurar control de acceso por IP en <www.equipos.ai>.

**▸ Solución** Aquí dejo una guía paso a paso para configurar tu servidor de correo electrónico en Ubuntu Server utilizando Postfix y Dovecot, cumpliendo con las especificaciones que has solicitado.

#### Configuración del servidor de correo electrónico

Instalación de Postfix y Dovecot:

**▸** Primero, asegúrate de que el sistema esté actualizado e instala Postfix y Dovecot:

![image-23](images/image-23.png)

#### Configuración de Postfix

Configuración básica en /etc/postfix/main.cf : **▸** Edita el archivo de configuración principal de Postfix para que coincida con las siguientes configuraciones:

![▸ Ajusta los siguientes parámetros: Habilitar autenticación SMTP:](images/image-24.png)

Configura Postfix para requerir autenticación al enviar correos electrónicos.

**▸** Abre el archivo /etc/postfix/main.cf :

![image-25](images/image-25.png)

**▸** Añade las siguientes líneas para configurar la autenticación SMTP:

![▸ Guarda y cierra el archivo.](images/image-26.png)

Configuración de Dovecot como servidor SASL para Postfix: **▸** Dovecot será utilizado para manejar la autenticación. Edita el archivo de configuración de Dovecot:

![image-27](images/image-27.png)

![▸ Busca y ajusta las siguientes líneas:](images/image-28.png)

Esto permitirá que Postfix utilice el servicio de autenticación de Dovecot.

#### Configuración de Dovecot

Configuración básica:

**▸** Edita los archivos de configuración de Dovecot:

![image-29](images/image-29.png)

**▸** Asegúrate de que los siguientes módulos estén habilitados:

![image-30](images/image-30.png)

**▸** Luego, edita el archivo de configuración de autenticación:

![image-31](images/image-31.png)

**▸** Descomenta y ajusta las siguientes líneas para habilitar la autenticación en texto plano:

![image-32](images/image-32.png)

Configuración de las ubicaciones de correo:

**▸** Configura la ubicación de los buzones de correo:

![image-33](images/image-33.png)

**▸** Ajusta la línea de mail_location:

![image-34](images/image-34.png)

#### Creación de las cuentas de correo electrónico

Configuración de usuarios virtuales: Dovecot y Postfix pueden manejar cuentas de correo electrónico mediante usuarios virtuales. Para este propósito, vamos a crear usuarios virtuales almacenados en un archivo de texto plano. Crea los directorios y archivos para usuarios virtuales:

![image-35](images/image-35.png)

Crea el archivo de usuarios virtuales:

![image-36](images/image-36.png)

**▸** Añade las siguientes líneas para las cuentas de correo:

![image-37](images/image-37.png)

**▸** Guarda y cierra el archivo, luego genera el mapa de usuarios:

![image-38](images/image-38.png)

Configura las contraseñas para los usuarios:

**▸** Dovecot soporta contraseñas encriptadas. Vamos a utilizar doveadm para generar

contraseñas.

![image-39](images/image-39.png)

**▸** Introduce la contraseña para cada usuario y copia las contraseñas generadas en un archivo passwd :

![image-40](images/image-40.png)

**▸** El formato será:

![Configura Dovecot para utilizar estas cuentas:](images/image-41.png)

Edita el archivo de configuración:

![image-42](images/image-42.png)

![Cambia la sección passdb y userdb : Verificación y configuración en Thunderbird](images/image-43.png)

Una vez que los servicios estén configurados, reinicia los servicios de Postfix y

Dovecot:

![image-44](images/image-44.png)

Ahora, en tu cliente Thunderbird:

**▸** Nombre: `Alonso` **▸** Correo: alonso@company.com.

**▸** Contraseña: la que configuraste.

**▸** Servidor IMAP: mail.company.com, puerto 143, autenticación en texto plano.

**▸** Servidor POP3: mail.company.com, puerto 110, autenticación en texto plano.

**▸** Servidor SMTP: mail.company.com, puerto 25, autenticación en texto plano. Prueba enviando y recibiendo correos electrónicos para verificar la correcta configuración. Con estos pasos, tendrás un servidor de correo completo configurado y funcionando, capaz de enviar y recibir correos electrónicos y gestionado mediante el cliente Thunderbird en LUbuntu.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–34)*
- A fondo  *(pp.35–46)*
- Entrenamientos  *(pp.47–81)*
- Servicios en Red e Internet 7 Tema . Material de estudio · Servicios en Red e Internet 10 Tema . Material de estudio · Servicios en Red e Internet 11 Tema . Material de estudio · Servicios en Red e Internet 12 Tema . Material de estudio · Servicios en Red e Internet 14 Tema . Material de estudio · Servicios en Red e Internet 15 Tema . Material de estudio · Servicios en Red e Internet 16 Tema . Material de estudio · Servicios en Red e Internet 17 Tema . Material de estudio · Servicios en Red e Internet 18 Tema . Material de estudio · Servicios en Red e Internet 19 Tema . Material de estudio · Servicios en Red e Internet 20 Tema . Material de estudio · Servicios en Red e Internet 21 Tema . Material de estudio · Servicios en Red e Internet 22 Tema . Material de estudio · Servicios en Red e Internet 24 Tema . Material de estudio · Servicios en Red e Internet 25 Tema . Material de estudio · Servicios en Red e Internet 26 Tema . Material de estudio · Servicios en Red e Internet 27 Tema . Material de estudio · Servicios en Red e Internet 28 Tema . Material de estudio · Servicios en Red e Internet 29 Tema . Material de estudio · Servicios en Red e Internet 30 Tema . Material de estudio · Servicios en Red e Internet 31 Tema . Material de estudio · Servicios en Red e Internet 32 Tema . Material de estudio · Servicios en Red e Internet 33 Tema . Material de estudio · Servicios en Red e Internet 34 Tema . Material de estudio  *(pp.7, 10, 11, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34)*
- Servicios en Red e Internet 35 Tema . A fondo · Servicios en Red e Internet 36 Tema . A fondo · Servicios en Red e Internet 37 Tema . A fondo · Servicios en Red e Internet 38 Tema . A fondo · Servicios en Red e Internet 39 Tema . A fondo · Servicios en Red e Internet 40 Tema . A fondo · Servicios en Red e Internet 41 Tema . A fondo · Servicios en Red e Internet 42 Tema . A fondo · Servicios en Red e Internet 43 Tema . A fondo · Servicios en Red e Internet 44 Tema . A fondo · Servicios en Red e Internet 45 Tema . A fondo · Servicios en Red e Internet 46 Tema . A fondo  *(pp.35–46)*
- Servicios en Red e Internet 47 Tema . Entrenamientos · Servicios en Red e Internet 48 Tema . Entrenamientos · Servicios en Red e Internet 49 Tema . Entrenamientos · Servicios en Red e Internet 50 Tema . Entrenamientos · Servicios en Red e Internet 51 Tema . Entrenamientos · Servicios en Red e Internet 52 Tema . Entrenamientos · Servicios en Red e Internet 53 Tema . Entrenamientos · Servicios en Red e Internet 54 Tema . Entrenamientos · Servicios en Red e Internet 55 Tema . Entrenamientos · Servicios en Red e Internet 56 Tema . Entrenamientos · Servicios en Red e Internet 57 Tema . Entrenamientos · Servicios en Red e Internet 58 Tema . Entrenamientos · Servicios en Red e Internet 59 Tema . Entrenamientos · Servicios en Red e Internet 60 Tema . Entrenamientos · Servicios en Red e Internet 61 Tema . Entrenamientos · Servicios en Red e Internet 62 Tema . Entrenamientos · Servicios en Red e Internet 63 Tema . Entrenamientos · Servicios en Red e Internet 64 Tema . Entrenamientos · Servicios en Red e Internet 65 Tema . Entrenamientos · Servicios en Red e Internet 66 Tema . Entrenamientos · Servicios en Red e Internet 67 Tema . Entrenamientos · Servicios en Red e Internet 68 Tema . Entrenamientos · Servicios en Red e Internet 69 Tema . Entrenamientos · Servicios en Red e Internet 70 Tema . Entrenamientos · Servicios en Red e Internet 71 Tema . Entrenamientos · Servicios en Red e Internet 72 Tema . Entrenamientos · Servicios en Red e Internet 73 Tema . Entrenamientos · Servicios en Red e Internet 74 Tema . Entrenamientos · Servicios en Red e Internet 75 Tema . Entrenamientos · Servicios en Red e Internet 76 Tema . Entrenamientos · Servicios en Red e Internet 77 Tema . Entrenamientos · Servicios en Red e Internet 78 Tema . Entrenamientos · Servicios en Red e Internet 79 Tema . Entrenamientos · Servicios en Red e Internet 80 Tema . Entrenamientos · Servicios en Red e Internet 81 Tema . Entrenamientos  *(pp.47–81)*