## Tema 7

# Servicios en Red e Internet

# Tema 7. Seguridad en los

# servicios

# Índice

Esquema Material de estudio

## 7.1. Introducción y objetivos

## 7.2. Seguridad en DHCP

## 7.3. Seguridad en DNS

## 7.4 Seguridad en un servidor web

## 7.5. Seguridad en el correo electrónico

A fondo Crear un sitio web seguro con HTTPS y UBUNTU Server 20.04 Seguridad del servidor de correo FTP, FTPS y SFTP: diferencias, ventajas e inconvenientes DHCP SNOOPING: ¿qué es? ¿cómo funciona? De qué se trata un ataque transferencia de zona a los DNS

He blindado mi conexión a Internet con estos nuevos DNS europeos Entrenamientos Entrenamiento 1. Configuración de filtrado de direcciones MAC en un entorno virtualizado de Windows Server en VirtualBox Entrenamiento 2. Configuración de filtrado de direcciones MAC en un entorno Ubuntu en VirtualBox Entrenamiento 3. Implementación de SMTP AUTH en un servidor de correo en Ubuntu

Entrenamiento 4. Configuración de un servidor Web seguro en Windows Server usando IIS7 Entrenamiento 5. Configuración de un Servidor Web Seguro en Ubuntu con Apache2 Test

# Esquema

![image-2](images/image-2.png)

Servicios en Red e Internet 4 Tema 7. Esquema

# 7.1. Introducción y objetivos

En un mundo cada vez más interconectado, la seguridad de las infraestructuras de red se ha convertido en una prioridad para proteger los datos sensibles y garantizar la disponibilidad de los servicios. Las amenazas cibernéticas continúan evolucionando, lo que obliga a las organizaciones a implementar medidas de seguridad adecuadas en sus redes.

Entre los elementos críticos en cualquier infraestructura de red se encuentran el Protocolo de Configuración Dinámica de Host (DHCP), el Sistema de Nombres de Dominio (DNS), los servidores web y los servidores de correo electrónico. Estos servicios son fundamentales para el funcionamiento de cualquier red moderna y su seguridad es crucial para proteger tanto los sistemas internos como los datos de los usuarios.

El **DHCP** es un protocolo utilizado para asignar direcciones IP de manera automática a dispositivos dentro de una red. Su principal ventaja es la simplificación de la gestión de direcciones IP, lo que lo convierte en una herramienta imprescindible en redes grandes. Sin embargo, como cualquier servicio que asigna recursos, el DHCP también representa un punto de vulnerabilidad.

Un ataque común relacionado con el DHCP es el ataque de **servidor DHCP falso.** En este tipo de ataque, un atacante configura un servidor DHCP malicioso en la red con el objetivo de interceptar las direcciones IP que deberían asignarse a dispositivos legítimos. Esto puede permitir al atacante redirigir el tráfico de la víctima a un servidor controlado por él, lo que facilita el **robo de datos** o la ejecución de un **ataque** *Man in the Middle* (MitM). Para prevenir este tipo de ataques, es fundamental utilizar técnicas como autenticación de servidores DHCP, filtrado de direcciones MAC y listas de control de acceso (ACL) en los *switches.*

E l **DNS** es otro componente esencial de la infraestructura de red que traduce los nombres de dominio legibles por los humanos en direcciones IP, permitiendo que los dispositivos se comuniquen entre sí a través de Internet. Dado su papel fundamental, el DNS es un objetivo frecuente para los atacantes, quienes pueden explotar vulnerabilidades para redirigir a los usuarios a sitios web maliciosos, interceptar tráfico o realizar ataques de denegación de servicio.

Uno de los ataques más conocidos al DNS es el **envenenamiento de caché DNS.** En este ataque, el atacante inserta información falsa en la caché de un servidor DNS, lo que redirige a los usuarios a sitios web fraudulentos sin su conocimiento. Para mitigar este tipo de ataques, se recomienda el uso de DNSSEC (DNS Security Extensions), que proporciona autenticación de los datos de DNS mediante el uso de firmas digitales. Además, es esencial mantener los servidores DNS actualizados y configurados correctamente para evitar vulnerabilidades conocidas.

Los **servidores web** son la columna vertebral de muchas aplicaciones en línea, ya que permiten a los usuarios acceder a servicios y contenidos a través de la web. Sin embargo, estos servidores son objetivos frecuentes de ataques cibernéticos, debido a su accesibilidad pública. Los ataques más comunes incluyen inyección SQL, *cross‑site scripting* (XSS), *cross-site request forgery* (CSRF) y ataques de denegación de servicio (DoS).

Para proteger un servidor web, se deben aplicar varias **capas de seguridad.** Una de las primeras medidas es mantener el servidor y sus aplicaciones actualizados, ya que las vulnerabilidades conocidas suelen ser explotadas en ataques. Además, es recomendable implementar **cortafuegos de aplicaciones web** (WAF), que protegen contra una amplia gama de ataques comunes dirigidos a servidores web. La autenticación de dos factores (2FA) y la encriptación TLS/SSL son esenciales para proteger las credenciales de los usuarios y garantizar la confidencialidad de los datos transmitidos.

E l **correo electrónico** sigue siendo uno de los métodos de comunicación más utilizados en el ámbito corporativo y personal. Sin embargo, debido a su popularidad, los servidores de correo electrónico se han convertido en un objetivo atractivo para los atacantes. Los ataques más comunes incluyen el *phishing,* el spam, el *malware* adjunto y el *spoofing* de direcciones de correo.

La autenticación en los correos electrónicos, como SPF (Sender Policy Framework), DKIM (DomainKeys Identified Mail)

y DMARC (Domain-based Message

Authentication, Reporting, and Conformance), ayuda a prevenir que los atacantes suplanten la identidad de dominios legítimos para enviar correos electrónicos maliciosos. Además, la implementación de antivirus y filtros de *spam* es crucial para evitar que el *malware* llegue a los buzones de los usuarios.

Otra medida importante es la encriptación de correos electrónicos, utilizando estándares como S/MIME o PGP, para asegurar que los correos electrónicos no sean interceptados o leídos por personas no autorizadas.

La seguridad en los servicios de DHCP, DNS, servidores web y servidores de correo es esencial para proteger la infraestructura de red de una organización y los datos sensibles de los usuarios. Implementar medidas de seguridad como la autenticación, el uso de encriptación, la actualización constante de los sistemas y el uso de herramientas especializadas como cortafuegos y filtros de contenido es fundamental para reducir el riesgo de ciberataques.

A medida que las amenazas evolucionan, las organizaciones deben mantenerse alerta y adaptarse constantemente a nuevas vulnerabilidades para proteger sus redes y servicios críticos.

Los **objetivos** que se pretende alcanzar en este tema son:

**▸** Comprender los riesgos asociados al uso de DHCP.

**▸** Implementar medidas de seguridad en el servidor DHCP.

**▸** Proteger el servidor DNS contra ataques de envenenamiento de caché.

**▸** Optimizar la configuración de servidores DNS para mejorar la seguridad.

**▸** Implementar medidas de seguridad en servidores web.

**▸** Identificar y prevenir ataques comunes a servidores web.

**▸** Garantizar la seguridad del correo electrónico.

**▸** Aplicar tecnologías de autenticación de correo electrónico.

**▸** Establecer políticas de filtrado de contenido y protección contra *malware* en correos

electrónicos. **▸** Desarrollar planes de respuesta ante incidentes de seguridad relacionados con DHCP, DNS, servidores web y de correo.

# 7.2. Seguridad en DHCP

La seguridad en DHCP es fundamental en redes para evitar ataques y garantizar que solo los dispositivos autorizados reciban configuraciones de red válidas. Aquí te explico algunas de las principales prácticas y técnicas para asegurar un servicio DHCP.

Filtrado de MAC (MAC Filtering)

El filtrado de MAC es una medida de seguridad en la cual se configura el servidor DHCP para que solo asigne direcciones IP a dispositivos cuyas direcciones MAC están en una lista de permisos *(whitelist).* Este enfoque es útil en redes pequeñas o medianas donde el administrador conoce los dispositivos autorizados. Sin embargo, su limitación es que las direcciones MAC pueden falsificarse. En redes grandes, la administración de estas listas puede ser compleja, pero sigue siendo efectiva contra accesos casuales o no autorizados.

![image-3](images/image-3.png)

Tabla 1. Características del filtrado de MAC. Fuente: elaboración propia.

Ejemplo de red sin filtrado de MAC

Supón que tienes una red corporativa con un servidor DHCP que asigna automáticamente direcciones IP a todos los dispositivos que se conectan.

Un atacante se conecta físicamente a la red (o de forma inalámbrica si es wifi abierta o mal configurada) y automáticamente recibe una dirección IP

Servicios en Red e Internet 9 Tema 7. Material de estudio del servidor DHCP, dándole acceso a los recursos de la red. Con este acceso, el atacante podría:

- Capturar tráfico de la red para intentar descubrir credenciales,

información confidencial o patrones de uso.

- Lanzar ataques de escaneo para identificar otros dispositivos en la red y

sus vulnerabilidades.

- Realizar suplantación (spoofing) de la IP o de la MAC para hacerse pasar

por otro dispositivo en la red, en un intento de obtener información confidencial o acceder a sistemas críticos.

- Configurar un servidor DHCP falso para enviar configuraciones IP

maliciosas, redirigiendo el tráfico de los dispositivos legítimos hacia el propio dispositivo del atacante.

Solución: filtrado de MAC

Si configuramos el servidor DHCP para que solo asigne direcciones IP a las MAC específicas de los dispositivos de confianza (empleando una lista de permitidos), evitamos que un dispositivo desconocido o no autorizado obtenga acceso a la red simplemente al conectarse.

En este caso, el servidor DHCP rechazaría las solicitudes de cualquier dispositivo con una dirección MAC que no esté en la lista de dispositivos permitidos. Así, incluso si el atacante se conecta físicamente a la red, no podría recibir una configuración IP válida, dificultando su acceso y reduciendo el riesgo de ataques.

El filtrado de MAC actúa como una primera línea de defensa en redes que no tienen autenticación avanzada, ayudando a limitar el acceso a dispositivos conocidos y de confianza y minimizando el riesgo de intrusión y ataques.

DHCP snooping

DHCP *snooping* es una funcionalidad de seguridad en *switches* gestionados que actúa como un «guardia» de tráfico DHCP, permitiendo solo ciertos puertos (de confianza) para que pasen tráfico DHCP de

servidores válidos. Esto previene

ataques como el **rogue DHCP,** donde un dispositivo malicioso se hace pasar por servidor DHCP y envía configuraciones IP falsas, redirigiendo tráfico o causando problemas de conectividad.

![image-4](images/image-4.png)

Tabla 2. Características del DHCP *snooping.* Fuente: elaboración propia.

DHCP *snooping* es fundamental para proteger la red contra ataques de suplantación de servidores DHCP. Aquí tienes un ejemplo que muestra por qué es importante:

Ejemplo de red sin DHCP *snooping*

Imagina una red corporativa en la que

no está habilitado el DHCP

*snooping.* Un atacante puede conectarse a un puerto de red y configurar un servidor DHCP falso en su dispositivo. Este servidor DHCP malicioso puede enviar configuraciones de red incorrectas a otros dispositivos que

Servicios en Red e Internet 11 Tema 7. Material de estudio solicitan una dirección IP, logrando varios efectos maliciosos:

- Redirigir el tráfico: el atacante configura el servidor DHCP falso para

asignar direcciones IP con una puerta de enlace que conduce el tráfico al propio dispositivo del atacante, permitiéndole interceptar y capturar información confidencial.

- Interrumpir la conectividad: los dispositivos pueden recibir

configuraciones de red incorrectas, como una puerta de enlace que no es válida o un servidor DNS inexistente. Esto provoca que los usuarios pierdan la conexión a Internet o a otros recursos importantes de la red, interrumpiendo el funcionamiento normal de la empresa.

-Acceder a sistemas críticos: al controlar la configuración de red de los dispositivos, el atacante podría dirigir el tráfico hacia servidores o servicios críticos para intentar explotar vulnerabilidades.

Solución: DHCP *snooping*

Activar DHCP *snooping* en los *switches* permite marcar puertos de confianza y no confianza. Solo los puertos de confianza (donde están conectados los servidores DHCP legítimos) pueden enviar respuestas DHCP. Los puertos no de confianza, como los accesos a estaciones de trabajo o invitados, no pueden enviar respuestas DHCP, bloqueando servidores DHCP no autorizados.

DHCP *snooping* actúa como un filtro que asegura que solo los servidores DHCP legítimos puedan asignar direcciones IP, protegiendo a la red contra ataques de suplantación y manteniendo la integridad de las configuraciones de red en un entorno corporativo.

IP Source Guard

IP *Source Guard* es una extensión de DHCP *snooping* que evita que los dispositivos falsifiquen direcciones IP. Este mecanismo vincula cada dirección IP asignada con una dirección MAC específica en el puerto del *switch,* permitiendo solo el tráfico desde esa combinación de IP y MAC. Este enfoque **limita los ataques de** **suplantación de IP** en redes locales, protegiendo la integridad del direccionamiento.

![image-5](images/image-5.png)

Tabla 3. Características del IP *Source Guard.* Fuente: elaboración propia.

Imagina una red empresarial que no tiene habilitado IP Source Guard. En este escenario, un atacante puede conectarse a un puerto de red donde no está configurada una política de seguridad, como el acceso a la red corporativa desde una estación de trabajo. Si el atacante tiene acceso físico a la red podría:

- Realizar suplantación de IP: el atacante puede cambiar la configuración

de su dispositivo para que utilice una dirección IP que ya ha sido asignada a otro dispositivo legítimo de la red, permitiéndole interceptar o manipular el tráfico destinado a esa IP.

-Acceso no autorizado: con la suplantación de IP, el atacante podría intentar acceder a servicios o recursos a los que no tiene permiso, ya que la red lo reconoce como un dispositivo legítimo.

-Interrupción de tráfico: si el atacante utiliza una IP ya asignada a un

Servicios en Red e Internet 13 Tema 7. Material de estudio dispositivo válido, puede causar interrupciones en el tráfico de la red, bloqueando el acceso de otros comunicaciones críticas.

Solución: IP *Source Guard*

usuarios o interfiriendo con

Cuando IP *Source Guard* está habilitado en la red, se monitorea el tráfico DHCP y se crea una tabla de enlace que asocia las direcciones IP a las direcciones MAC de los dispositivos

que las están utilizando. Si un

dispositivo intenta usar una dirección IP que no corresponde a su dirección MAC registrada, el tráfico es bloqueado. Esto previene que un atacante pueda realizar una suplantación de IP y acceder a la red de manera no autorizada.

IP Source Guard es una herramienta esencial para proteger las redes corporativas contra ataques como la suplantación de IP, asegurando que solo los dispositivos legítimos con direcciones IP autorizadas puedan acceder a los recursos de la red.

Control de tiempos de arrendamiento (Lease Time)

El tiempo de arrendamiento en DHCP define el **período** durante el cual un dispositivo puede mantener una **dirección IP** antes de solicitar su renovación. Configurar tiempos de arrendamiento más cortos puede reducir la cantidad de direcciones IP retenidas por dispositivos inactivos y mejorar la disponibilidad en redes dinámicas.

![image-6](images/image-6.png)

Tabla 4. Características del *Lease Time.* Fuente: elaboración propia.

Autenticación 802.1X

802.1X es un estándar de autenticación que regula el acceso a la red en el nivel de puerto de un *switch.* Cada dispositivo debe autenticarse, generalmente a través de un servidor RADIUS, antes de recibir una dirección IP o acceder a recursos de la red. Esto se utiliza en redes empresariales para evitar que dispositivos no autorizados accedan al DHCP.

![image-7](images/image-7.png)

Tabla 5. Características de la autenticación 802.1x. Fuente: elaboración propia.

Supervisión y registro (Logging)

Registrar las solicitudes DHCP permite al administrador monitorear todas las asignaciones IP en tiempo real y ver qué dispositivos están activos y cuándo. Esto puede ayudar a identificar patrones inusuales o intentos de ataque, como solicitudes masivas de IP o intentos fallidos de asignación.

![image-8](images/image-8.png)

Tabla 6. Características de la supervisión y registro. Fuente: elaboración propia.

Reducción de rango de IP y configuración de subnetting

Al limitar el rango de direcciones IP disponible y aplicar técnicas de segmentación mediante *subnetting,* se puede reducir la exposición de la red y dificultar el acceso no autorizado a determinadas áreas.

![image-9](images/image-9.png)

Tabla 7. Características de la supervisión y registro. Fuente: elaboración propia.

# 7.3. Seguridad en DNS

La seguridad en DNS (sistema de nombres de dominio) es crucial para proteger las comunicaciones en Internet y garantizar la integridad, confidencialidad y disponibilidad de los servicios que dependen de él. Aquí te dejo algunos aspectos clave sobre la seguridad en DNS.

DNSSEC (DNS Security Extensions)

DNSSEC es una extensión de seguridad para DNS que agrega una capa de autenticación mediante la firma digital de las respuestas de los servidores DNS. Este mecanismo asegura que la información que los usuarios reciben no ha sido alterada ni modificada durante su transmisión.

![image-10](images/image-10.png)

Tabla 8. Características de DNSSec. Fuente: elaboración propia.

DNS Tunneling

El DNS *Tunneling* es una técnica utilizada para **esconder datos o comandos** dentro de consultas DNS legítimas. Los atacantes utilizan este método para exfiltrar datos, evadir *firewalls* y saltarse políticas de seguridad de la red, ya que las consultas DNS a menudo no son bloqueadas.

Los datos se encapsulan en el campo de las consultas DNS. Por ejemplo, un atacante podría enviar datos codificados dentro de un nombre de dominio, lo cual sería interpretado por el servidor DNS de comunicación encubierta entre un dispositivo comando y control (C&C).

Prevención:

destino. Esto puede permitir la comprometido y un servidor de

**▸ Monitoreo de tráfico DNS:** detectar patrones de tráfico DNS inusuales (por ejemplo, grandes volúmenes de consultas hacia dominios desconocidos) puede ayudar a identificar el uso de túneles.

**▸ Filtrado de consultas DNS no estándar:** configurar los servidores DNS para rechazar consultas que no se alineen con el formato típico de un nombre de dominio.

DDoS (Distributed Denial of Service) contra servidores DNS

Un ataque DDoS a servidores DNS busca **sobrecargar el servidor** con una cantidad masiva de **tráfico,** causando que no pueda procesar solicitudes legítimas, lo que resulta en la interrupción del servicio DNS. Esto puede afectar la disponibilidad de muchos sitios web y servicios.

¿Cómo prevenirlo?

**▸ Anycast:** utilizar servidores DNS distribuidos geográficamente con la tecnología Anycast permite que las consultas DNS sean redirigidas automáticamente al servidor más cercano y disponible, distribuyendo así la carga de las consultas.

**▸ Soluciones antiDDoS:** utilizar servicios especializados de protección contra DDoS, como Cloudflare, que filtran el tráfico no deseado antes de que llegue al servidor DNS.

**▸ Limitar el tráfico:** configurar límites para las consultas DNS por segundo para prevenir que un único origen haga demasiadas solicitudes.

Actualización y parches

**▸ Riesgos de no mantener actualizado el servidor DNS:**

- Los servidores DNS, como cualquier otro software, tienen vulnerabilidades que los atacantes pueden explotar. Si no se actualizan, pueden quedar expuestos a fallos de seguridad conocidos que podrían ser utilizados para realizar ataques.

**▸ Prácticas recomendadas:**

- Automatización de actualizaciones: utilizar herramientas que mantengan automáticamente los servidores DNS actualizados con los últimos parches de seguridad.

- Monitoreo constante: estar al tanto de las actualizaciones de seguridad emitidas por los proveedores de *software* DNS como BIND, Unbound o PowerDNS.

Bloqueo de resolución recursiva

La resolución recursiva es un proceso mediante el cual un servidor DNS realiza todas las **consultas necesarias** para resolver un **nombre de dominio,** incluso si no tiene la respuesta en su base de datos.

**▸ Riesgosde permitir resolución recursiva pública:**

- Si la resolución recursiva está habilitada de manera pública, un atacante puede abusar del servidor DNS para lanzar ataques de amplificación DDoS (mediante peticiones DNS recursivas).

**▸ Soluciones:**

- Deshabilitar la resolución recursiva en servidores que no necesiten proporcionar este servicio a todo el mundo.

- Restringir la resolución recursiva a direcciones IP o rangos de red específicos (por ejemplo, solo para clientes internos).

Control de acceso

El control de acceso se refiere a **restringir** q u é **dispositivos o redes** pueden consultar los servidores DNS. Sin control, cualquier usuario podría realizar consultas que podrían ser maliciosas. ¿Cómo implementar el control de acceso?

**▸ Listas de control de acceso (ACL):** configurar listas de acceso en los servidores DNS para permitir solo consultas desde direcciones IP o redes confiables.

**▸** ***Firewalls:*** configurar *firewalls* para permitir solo tráfico DNS desde fuentes autorizadas y bloquear todo lo demás.

DNS over HTTPS (DoH) y DNS over TLS (DoT)

DNS over HTTPS (DoH) y DNS over TLS (DoT) son protocolos que cifran las consultas y respuestas DNS para evitar que sean interceptadas por atacantes en la red, lo que mejora la privacidad y seguridad de las consultas DNS.

**▸ Ventajas:**

- Protección contra espionaje: impide que atacantes puedan ver o modificar las consultas DNS.

- Prevención de ataques Man in the Middle: al usar cifrado, las consultas DNS no pueden ser interceptadas o manipuladas.

**▸ Desventajas:**

- Mayor latencia: debido al cifrado y a la necesidad de una conexión segura, el rendimiento podría verse afectado en algunos casos.

- Complejidad en la implementación: requiere configuración adicional tanto del lado del cliente como del servidor.

# 7.4 Seguridad en un servidor web

La seguridad en un servidor web es crucial para proteger tanto los datos de los usuarios como los sistemas de la organización frente a amenazas y ataques. Aquí hay algunas prácticas clave para asegurar un servidor web.

Actualización y parches

La actualización constante es uno de los pilares fundamentales de la seguridad de un servidor web. Sin las actualizaciones regulares, las vulnerabilidades ya conocidas en el *software* pueden ser explotadas por los atacantes.

**▸ Sistema operativo:** mantén el sistema operativo del servidor actualizado con los últimos parches de seguridad. Esto incluye cualquier actualización de *software* relacionado con la red, el *firewall* o el sistema de almacenamiento.

**▸ Software de servidor web:** Apache, Nginx, IIS y otros servidores web tienen actualizaciones periódicas que abordan vulnerabilidades específicas. Configura alertas para saber cuándo se lanzan nuevas versiones o parches.

**▸ Librerías y dependencias:** no solo el *software* de servidor web necesita ser actualizado. Muchas veces, las aplicaciones web dependen de otras librerías y tecnologías, como PHP, Python, Node.js y bases de datos como MySQL. Estas también deben ser gestionadas correctamente.

Configuración adecuada de los permisos

La configuración de permisos es crucial para asegurar que los archivos y directorios del servidor web estén protegidos de accesos no deseados.

**▸ Permisos de archivo:** asegúrate de que los archivos y directorios tengan permisos restrictivos. El principio de menor privilegio debe aplicarse: asigna solo los permisos necesarios a cada usuario o proceso. Por ejemplo, los archivos de configuración del servidor no deberían ser modificables por usuarios que no sean administradores.

**▸ Propietarios y grupos:** utiliza el control de acceso basado en usuarios y grupos en el sistema operativo para asegurarte de que solo los usuarios correctos tienen acceso a los archivos sensibles.

**▸ Accesos de ejecución:** limita la ejecución de *scripts* o archivos solo a aquellos directorios o ubicaciones donde se necesiten. Evita ejecutar *scripts* en directorios que no estén bajo control directo.

Desactivar servicios innecesarios

Cada servicio que ejecuta un servidor web es un posible vector de ataque. Si un servicio no es necesario, debería ser desactivado.

**▸ Servicios del sistema:** revisa los servicios que están en ejecución en tu servidor. Si un servicio como FTP o Telnet no es necesario, desactívalo. Si se utiliza SSH, asegúrate de que solo los administradores puedan acceder a través de él.

**▸ Minimizar el** ***software*** **en el servidor:** cuanto más *software* tengas en ejecución, mayor es el riesgo de que una vulnerabilidad en alguno de ellos sea explotada. Solo instala lo que sea estrictamente necesario para el funcionamiento del servidor web.

Uso de firewalls

U n *firewall* actúa como una barrera entre tu servidor web y el mundo exterior, bloqueando el tráfico no deseado.

**▸** ***Firewall*** **a nivel de red:** configura reglas estrictas para limitar el acceso a tu servidor. Solo permite el tráfico en los puertos necesarios, como el puerto 80 para HTTP y 443 para HTTPS.

**▸** ***Firewall*** **de aplicaciones web (WAF):** un WAF puede proteger tu servidor web de ataques específicos a nivel de la aplicación, como inyecciones SQL, *cross-site* *scripting* (XSS) y otros ataques comunes. Los WAF pueden filtrar y bloquear el tráfico malicioso antes de que llegue a la aplicación.

**▸ IP** ***whitelisting*** **y** ***geofencing:*** si es posible, limita las direcciones IP que pueden acceder al servidor. También, puedes bloquear regiones geográficas que no necesitan acceder a tu servidor.

Autenticación y control de acceso

La autenticación fuerte y el control de acceso son esenciales para evitar accesos no autorizados.

**▸ Autenticación multifactor (2FA):** además de las contraseñas, implementa autenticación multifactor (2FA) para añadir una capa extra de seguridad en los accesos al servidor y a las aplicaciones web.

**▸ HTTPS y cifrado de conexiones:** utiliza SSL/TLS para cifrar todas las comunicaciones entre el cliente y el servidor, garantizando que los datos no puedan ser interceptados por atacantes. Asegúrate de que todos los certificados SSL sean válidos y configurados correctamente.

**▸ Accesos controlados:** define roles de usuario y controla qué pueden hacer. Un administrador debería tener acceso completo, mientras que un usuario normal solo debería poder ver los recursos necesarios. Implementa controles de acceso basados en roles (RBAC).

Cifrado de datos

El cifrado es crucial para la protección de los datos tanto en tránsito como en reposo.

**▸ SSL/TLS:** implementa HTTPS en lugar de HTTP para que toda la información transmitida entre el cliente y el servidor esté cifrada. Esto previene que los atacantes puedan interceptar las comunicaciones o realizar un ataque de intermediario (MITM).

**▸ Cifrado de bases de datos:** asegúrate de que las bases de datos que contienen información sensible estén cifradas, tanto a nivel de archivo como a nivel de aplicación.

**▸ Cifrado en reposo:** protege los archivos almacenados en el servidor mediante cifrado. Esto es especialmente importante para archivos de configuración o bases de datos que contienen información sensible de los usuarios.

Prevención de inyecciones

Las inyecciones de código son uno de los tipos de ataques más comunes. Estos pueden ocurrir cuando los usuarios malintencionados logran **insertar código SQL,** **HTML o JavaScript** en las entradas de la aplicación web.

**▸ Validación de entradas:** filtra y valida todas las entradas del usuario para asegurarte de que no contengan caracteres peligrosos (como comillas, apóstrofes o *scripts).* Utiliza una lista blanca de entradas permitidas en lugar de una lista negra.

**▸ Consultas preparadas:** en el caso de las bases de datos, utiliza consultas preparadas para prevenir inyecciones SQL, ya que estas consultas separan el código SQL de los datos proporcionados por el usuario.

**▸ Escapar caracteres:** si es necesario usar datos proporcionados por el usuario en consultas SQL o en el código de la página web, asegúrate de escapar correctamente todos los caracteres que puedan ser interpretados como código.

Monitoreo y registro

Es fundamental monitorear las actividades del servidor y registrar eventos críticos para detectar cualquier actividad sospechosa.

**▸ Registros de acceso:** mantén registros detallados de todos los accesos a tu servidor web. Incluye la IP de origen, el tipo de acceso (GET, POST), el código de estado HTTP y cualquier mensaje de error.

**▸ Monitoreo en tiempo real:** utiliza herramientas de monitoreo como Nagios, Zabbix o Prometheus para supervisar el tráfico y el estado de salud del servidor en tiempo real.

**▸ Detección de anomalías:** implementa un sistema de detección de intrusiones (IDS/IPS) que te notifique si detecta comportamientos anómalos o ataques potenciales.

Seguridad en las aplicaciones

La seguridad en las aplicaciones web es crítica, ya que muchas veces los ataques se dirigen a vulnerabilidades en el código de la aplicación.

**▸ Desarrollo seguro:** utiliza prácticas de desarrollo seguro como las pautas OWASP (Open Web Application Security Project) para asegurar que las aplicaciones sean seguras desde el diseño.

**▸ Revisión y auditoría de código:** realiza auditorías regulares de seguridad del código y pruebas de penetración para identificar posibles vulnerabilidades en el código.

**▸** ***Frameworks*** **seguros:** utiliza *frameworks* y bibliotecas que proporcionen mecanismos de seguridad incorporados para protegerte de los ataques más comunes (por ejemplo, inyecciones SQL, XSS).

Protección contra ataques DDoS

Los ataques de denegación de servicio distribuido (DDoS) son diseñados para hacer que tu servidor web sea inaccesible al sobrecargarlo con tráfico malicioso.

**▸ Protección en la red:** utiliza servicios de mitigación de DDoS como Cloudflare, AWS Shield o Akamai para proteger tu servidor frente a estos ataques.

**▸ Monitoreo de tráfico:** implementa sistemas que puedan identificar picos anómalos en el tráfico y responder rápidamente a posibles ataques.

Copia de seguridad y recuperación ante desastres

Aunque la prevención es fundamental, siempre existe la posibilidad de que un atacante pueda comprometer el servidor.

**▸ Copia de seguridad regular:** haz copias de seguridad de los datos y configuraciones del servidor de manera periódica y guárdalas en un lugar seguro, preferentemente en una ubicación externa (por ejemplo, en la nube).

**▸ Plan de recuperación:** ten un plan de recuperación ante desastres que detalle cómo restaurar el servidor a su estado operativo tras un incidente de seguridad grave.

Pruebas de penetración y auditorías de seguridad

Las pruebas de penetración (o *pentesting)* y las auditorías de seguridad ayudan a identificar vulnerabilidades en el servidor.

**▸** ***Pentesting*** **regular:** realiza pruebas de penetración periódicas para simular ataques y detectar posibles debilidades en la infraestructura.

**▸ Auditorías externas:** contrata expertos en seguridad para realizar auditorías externas y validar que el servidor y la aplicación estén correctamente protegidos.

Estas prácticas conforman un **enfoque integral** para la seguridad de un servidor web, que reducen las probabilidades de ataques exitosos y garantizan una rápida recuperación en caso de incidentes.

# 7.5. Seguridad en el correo electrónico

La seguridad en un servidor de correo electrónico es fundamental para proteger la integridad de los datos, la privacidad de los usuarios y evitar el acceso no autorizado o la propagación de *malware.* Aquí te detallo algunos **aspectos clave** para asegurar un servidor de correo electrónico:

Autenticación y autorización

La autenticación y autorización son la **primera línea de defensa** contra el acceso no autorizado.

**▸ Autenticación de usuarios (SMTP AUTH):** SMTP AUTH permite que los usuarios se autentiquen antes de enviar correos electrónicos, evitando el uso no autorizado del servidor. Usualmente, se utiliza junto con TLS para asegurar la comunicación de las credenciales. El servidor requiere un nombre de usuario y una contraseña antes de enviar el correo.

**▸ Autenticación multifactor (MFA):** la autenticación multifactor agrega una capa extra de seguridad, lo que significa que además del nombre de usuario y la contraseña, el usuario debe proporcionar un segundo factor, como un código enviado por SMS, una aplicación de autenticación o una huella digital. Esto reduce significativamente el riesgo de acceso no autorizado, incluso si las credenciales de usuario se ven comprometidas.

**▸ Control de acceso:** en un servidor de correo, es esencial aplicar políticas de acceso mínimas, como el principio de «necesidad de saber». Solo los usuarios que realmente necesiten utilizar el servidor de correo deben tener acceso a él. Esto, también, incluye restricciones sobre qué direcciones de correo electrónico pueden enviar o recibir mensajes.

Cifrado

El cifrado protege tanto los datos en tránsito como los datos en reposo, impidiendo que los atacantes intercepten o lean los correos electrónicos.

**▸ Cifrado en tránsito (TLS/SSL):** el cifrado TLS (Transport Layer Security) se utiliza para asegurar las conexiones entre los servidores de correo y entre los clientes y el servidor. Es fundamental para proteger la confidencialidad e integridad de los correos electrónicos mientras están en tránsito a través de la red. El uso de SSL (Secure Sockets Layer) también sigue siendo común en algunos entornos, aunque TLS es su sucesor más seguro. Funciona cuando un correo electrónico se envía desde un cliente de correo a un servidor, el servidor recibe el correo cifrado mediante TLS, asegurando que nadie más pueda interceptar ni modificar los datos durante el proceso.

**▸ Cifrado de extremo a extremo (E2EE):** el cifrado de extremo a extremo significa que solo el remitente y el destinatario pueden leer el contenido del correo electrónico. Ningún intermediario, como el proveedor de servicios de correo electrónico, podrá acceder al contenido del mensaje. Para ello, se pueden utilizar tecnologías como PGP o S/MIME, que cifran el mensaje y la clave de encriptación solo es accesible por el destinatario. Funciona cuando el remitente cifra el correo electrónico con la clave pública del destinatario. Solo el destinatario, que tiene la clave privada correspondiente, puede descifrarlo y leerlo.

Protección contra spam y malware

Los correos electrónicos pueden ser vectores de ataque si no se toman las medidas adecuadas de protección.

**▸ Filtros de** ***spam:*** los filtros de *spam* son herramientas que analizan los correos entrantes y los clasifican como legítimos o no deseados. Los filtros pueden basarse en diversos factores, como el contenido del mensaje, la reputación de la dirección IP del servidor que envió el mensaje o la presencia de enlaces sospechosos. Algunas herramientas populares son SpamAssassin, Barracuda, MailScanner o SpamTitan.

Estos filtros utilizan listas negras (por ejemplo, IP de servidores conocidos por enviar *spam),* patrones de contenido malicioso y reglas predefinidas para identificar y bloquear mensajes no deseados antes de que lleguen a la bandeja de entrada del usuario.

**▸ Antivirus y** ***antimalware:*** el antivirus es esencial para evitar que se transmitan correos con archivos adjuntos maliciosos (como virus, troyanos o *ransomware).* Las soluciones de *antimalware* escanean los correos electrónicos en busca de archivos adjuntos peligrosos y los bloquean o eliminan antes de que lleguen a la bandeja de entrada. Herramientas como ClamAV, Sophos o McAfee son opciones comunes para esto.

**▸ Escaneo de enlaces y archivos adjuntos:** los enlaces y archivos adjuntos en los correos electrónicos también pueden ser vectores de ataque. Se recomienda utilizar una herramienta de seguridad que analice los enlaces para verificar si están relacionados con sitios web maliciosos *(phishing,* robo de información, etc.). Los archivos adjuntos también deben ser escaneados en busca de código malicioso.

Políticas de seguridad de correo electrónico

Establecer y aplicar políticas es fundamental para mantener la seguridad a largo plazo.

**▸ Política de contraseñas:** las contraseñas deben ser complejas (mínimo doce caracteres, incluyendo mayúsculas, minúsculas, números y caracteres especiales) y deben cambiarse regularmente. Además, es recomendable implementar un sistema de gestión de contraseñas o una herramienta que permita verificar su fortaleza.

**▸ SPF, DKIM, DMARC:** estos tres protocolos ayudan a verificar la autenticidad de los correos electrónicos y protegen contra el *phishing* y la suplantación de identidad.

- SPF (Sender Policy Framework): el servidor receptor comprueba si el servidor de envío está autorizado para enviar correos desde esa dirección. Si no está autorizado, el correo es rechazado.

- DKIM (DomainKeys Identified Mail): este sistema utiliza una firma digital en los correos electrónicos, que permite al servidor receptor verificar que el correo no ha sido alterado en tránsito y que proviene de una fuente legítima.

- DMARC (Domain-based Message Authentication, Reporting & Conformance): permite que el propietario de un dominio publique políticas sobre cómo los servidores de correo deben manejar los correos que no pasen la autenticación SPF o DKIM.

Monitoreo y auditoría

El monitoreo continuo ayuda a identificar y responder rápidamente a incidentes de seguridad.

**▸ Registros de acceso y actividad:** es fundamental que los servidores de correo registren todas las interacciones, como intentos de inicio de sesión, envíos de correos y errores. Estos registros deben ser revisados regularmente para detectar patrones inusuales o ataques de fuerza bruta.

**▸ Alertas en tiempo real:** configurar alertas automáticas para actividades sospechosas, como múltiples intentos de acceso fallidos, acceso desde direcciones IP inusuales o la detección de tráfico anómalo, puede ayudar a prevenir incidentes de seguridad.

Actualizaciones y parches de seguridad

Las vulnerabilidades en el *software* de correo electrónico pueden ser una puerta de entrada para los atacantes.

**▸** Mantener el *software* actualizado: asegúrate de que el servidor de correo y todos sus componentes (como la base de datos, las bibliotecas de *software* y el sistema operativo) estén actualizados con los últimos parches de seguridad.

**▸** Seguridad en el sistema operativo: configurar adecuadamente el sistema operativo subyacente es igualmente importante. Esto incluye desactivar servicios innecesarios, aplicar parches de seguridad y asegurar la configuración de las políticas de acceso.

Protección de datos

Los datos confidenciales, como los correos electrónicos, deben estar protegidos tanto en tránsito como en reposo.

**▸** ***Backup*** **de correos electrónicos:** realizar copias de seguridad regulares de todos los correos electrónicos y configuraciones del servidor es esencial para recuperar datos en caso de un incidente. Las copias de seguridad deben ser cifradas para garantizar su seguridad.

**▸ Protección contra pérdida de datos (DLP):** implementar tecnologías DLP para evitar que los usuarios envíen información confidencial (como datos personales, contraseñas o información financiera) fuera de la organización sin autorización.

Seguridad en el acceso físico

El acceso físico a los servidores debe estar restringido para prevenir manipulaciones y ataques físicos.

**▸** Acceso restringido al servidor: solo el personal autorizado debe tener acceso físico a los servidores. Esto puede incluir el uso de cámaras de seguridad, sistemas de control de acceso y auditoría de acceso físico para garantizar que no se produzcan accesos no autorizados.

Implementar estas medidas de seguridad fortalecerá tu servidor de correo electrónico y reducirá el riesgo de compromisos y ataques.

# Crear un sitio web seguro con HTTPS y UBUNTU

# Server 20.04

Cano, J. G. (2021, febrero 17). *Crear un sitio Web seguro con HTTPS y UBUNTU* *Server 20.04* [Vídeo]. YouTube. [https://www.youtube.com/watch?v=YwQypFwOEm4](https://www.youtube.com/watch?v=YwQypFwOEm4)

Este vídeo te muestra los pasos detallados para configurar un servidor web apache seguro en un entorno Ubuntu.

![image-11](images/image-11.png)

Accede al vídeo: [https://www.youtube.com/embed/YwQypFwOEm4](https://www.youtube.com/embed/YwQypFwOEm4)

# servidor-correo/

# Seguridad del servidor de correo

Gitlan, D. (2024, febrero 15). Seguridad del servidor de correo: cómo proteger sus correos electrónicos. *SSL Dragon.* <https://www.ssldragon.com/es/blog/seguridad-> Este documento te muestra diez puntos clave para mantener seguro de servidor de correo electrónico. Si eres capaz de implementar todas las medidas, tendrás asegurado tu servidor.

# FTP, FTPS y SFTP: diferencias, ventajas e inconvenientes

Hierro, A. (2018). FTP, FTPS y SFTP: diferencias, ventajas e inconvenientes. *Blog* *ahierro* [https://blog.ahierro.es/ftp-ftps-y-sftp-diferencias-ventajas-inconvenientes/](https://blog.ahierro.es/ftp-ftps-y-sftp-diferencias-ventajas-inconvenientes/)

Aunque no hayamos hablado en este tema del servicio FTP, también, tenemos que tener presente que se enfrenta a numerosos problemas de seguridad. Este artículo identifica las posibilidades seguras para utilizar este servicio.

# CONFIGURACIÓN - Packet Tracer 8.0 [Vídeo]. YouTube.

# [https://www.youtube.com/watch?v=ETbBB65X1HM](https://www.youtube.com/watch?v=ETbBB65X1HM)

# DHCP SNOOPING: ¿qué es? ¿cómo funciona?

Network Warriors. (2023, Julio 14). *DHCP SNOOPING ¿Qué es? ¿Cómo Funciona?* En este vídeo, y en el resto de los vídeos de la serie, el autor te enseñará todo lo que tiene que ver con el DHCP *snooping* y, a través de la herramienta Cisco Tracert Packet, cómo configurarlo en un entorno simulado.

![image-12](images/image-12.png)

Accede al vídeo: [https://www.youtube.com/embed/ETbBB65X1HM](https://www.youtube.com/embed/ETbBB65X1HM)

# transferencia-zona-dns/

# De qué se trata un ataque transferencia de zona a

# los DNS

Pérez, I. (2015, junio 17). De qué se trata un ataque transferencia de zona a los DNS. *Welive Security.* <https://www.welivesecurity.com/la-es/2015/06/17/trata-ataque-> Para poder defender tus servidores deberás conocer cuáles son los ataques más comunes. Esta web te mantiene informado de uno de los ataques más habituales al que te puedes enfrentar.

# europeos-seguros-dns0/

# He blindado mi conexión a Internet con estos nuevos DNS europeos

Soriano, D. (2023, febrero 10). He blindado mi conexión a Internet con estos nuevos DNS europeos. *Adsl zone.* <https://www.adslzone.net/noticias/redes/nuevos-dns-> Aquí te muestro los mejores o por lo menos más seguros servidores DNS. Puedes utilizarlos sustituyendo los que tienes actualmente.

# Entrenamiento 1. Configuración de filtrado de direcciones MAC en un entorno virtualizado de

# Windows Server en VirtualBox

#### ▸ Planteamiento del ejercicio

Esta actividad implica la creación de una red interna en VirtualBox, donde configurarás Windows Server como servidor DHCP y aplicarás reglas de filtrado de direcciones MAC para administrar el acceso de los dispositivos cliente a la red.

Realizarás un conjunto de pasos que te ayudarán a familiarizarte con el rol DHCP de

Windows Server y sus configuraciones de seguridad básicas.

Competencias que desarrollar:

**▸** Implementar y configurar el rol DHCP en un servidor Windows Server.

**▸** Crear un ámbito de DHCP y definir un rango de IP para la red.

**▸** Aplicar políticas de filtrado de MAC en entornos de red virtualizados.

**▸** Evaluar y analizar la efectividad del filtrado de MAC para la seguridad de la red. Requisitos previos:

**▸** VirtualBox instalado con:

- Una máquina virtual con Windows Server configurada y activada.

- Una máquina virtual de cliente (puede ser cualquier sistema operativo compatible con VirtualBox).

**▸** Conocimientos básicos de redes, DHCP y direcciones MAC.

#### ▸ Desarrollo paso a paso

**▸** Configurar el entorno en VirtualBox:

- Asegúrate de que ambas máquinas virtuales (Windows Server y el cliente) estén en la misma red interna en VirtualBox, configurando la opción adaptador de red interna para ambas máquinas y asignándoles el mismo nombre de red (por ejemplo, RedInterna).

**▸** Configurar Windows Server como servidor DHCP:

- Inicia la máquina Windows Server y abre «Administrador del servidor».

- Instala el rol de servidor DHCP si no está instalado y configura un ámbito DHCP con un rango de IP (por ejemplo, 192.168.1.10 a 192.168.1.50).

**▸** Habilitar el filtrado de MAC en el ámbito DHCP:

- En administrador de DHCP, abre IPv4 y selecciona el ámbito creado.

- Activa el filtrado de direcciones MAC y elige entre las listas de permitidos o denegados para filtrar dispositivos según sus direcciones MAC.

**▸** Añadir direcciones MAC a las listas de filtrado:

- Configura la lista de filtrado añadiendo la dirección MAC del cliente en la lista de permitidos o denegados, dependiendo del comportamiento que desees observar.

- Para obtener la dirección MAC del cliente, inicia la máquina cliente y utiliza el comando ipconfig /all en el símbolo del sistema.

**▸** Verificar la configuración:

- Inicia el cliente y verifica si este puede obtener una dirección IP.

- En función de las configuraciones de filtrado de MAC, el cliente deberá recibir una IP

Servicios en Red e Internet 41 Tema 7. Entrenamientos o no, según esté en la lista de permitidos o denegados. **▸** Análisis de resultados:

- Observa el comportamiento del cliente al intentar conectarse a la red y documenta los resultados.

- Discute la efectividad del filtrado de MAC como medida de seguridad, destacando ventajas y posibles limitaciones.

Preguntas de reflexión: **▸** ¿Cómo mejora la seguridad de la red el uso de filtrado de direcciones MAC? **▸** ¿Qué limitaciones presenta el filtrado de MAC en un entorno real frente a posibles ataques? **▸** ¿Qué ventajas ofrece la simulación en VirtualBox para probar configuraciones de red y de seguridad? Evaluación: **▸** Capturas de pantalla que demuestren cada paso de la configuración. **▸** Explicación de los resultados obtenidos tras implementar el filtrado de MAC. **▸** Respuestas a las preguntas de reflexión, demostrando comprensión de los conceptos de filtrado y seguridad de la red.

#### ▸ Solución

#### Paso 1. Crear y configurar las máquinas virtuales en VirtualBox

**▸** Abrir VirtualBox e instalar las siguientes máquinas:

- Windows Server (por ejemplo, Windows Server 2019 o 2022).

- Cliente (por ejemplo, Windows 10 o cualquier otro sistema operativo cliente).

**▸** Configurar el adaptador de red:

- Abre la configuración de red para Windows Server y para el cliente en VirtualBox.

- En la pestaña Red, elige «Adaptador de red interna» en ambas máquinas virtuales. Así estarán en la misma red aislada.

- Asigna un nombre a esta red interna (por ejemplo, RedInterna).

#### Paso 2. Configurar DHCP en Windows Server

**▸** Inicia la máquina virtual de Windows Server. **▸** Instalar el rol de servidor DHCP (si no está instalado):

- Abre «Administrador del servidor» y selecciona «Agregar roles y características».

- Elige «Servidor DHCP» y sigue los pasos del asistente para la instalación.

**▸** Configurar un ámbito DHCP:

- Abre el administrador de DHCP en el servidor.

- Haz clic derecho en «IPv4» y selecciona «Nuevo ámbito».

- Sigue las instrucciones del asistente para crear un ámbito.

- Define el rango de IP: por ejemplo, 192.168.1.10 a 192.168.1.50.

- Define la máscara de subred: por ejemplo, 255.255.255.0.

- Define la duración del arrendamiento: puedes mantener el valor predeterminado o ajustarlo según necesidades.

#### Paso 3. Configurar el filtrado de direcciones MAC

**▸** En «Administrador de DHCP», abre «IPv4» y selecciona el ámbito que acabas de crear.

**▸** Haz clic derecho en el ámbito y selecciona «Propiedades».

**▸** En la ventana de propiedades, ve a la pestaña «Filtrado de Direcciones MAC».

**▸** Habilitar el filtrado:

- Marca la casilla para habilitar el filtrado de direcciones MAC.

- Puedes optar por configurar una lista de permitidos o denegados.

- Lista de permitir: solo los dispositivos en esta lista podrán obtener una dirección IP.

- Lista de denegar: los dispositivos en esta lista no podrán obtener una dirección IP.

**▸** Añadir una dirección MAC:

- Si seleccionaste la lista de permitidos o denegados, haz clic en «Editar» o «Añadir en la lista correspondiente».

- Introduce la dirección MAC del dispositivo cliente. Para obtener la dirección MAC en el cliente, puedes usar el comando ipconfig /all en Windows.

#### Paso 4. Probar la configuración de filtrado de MAC

**▸** Inicia la máquina cliente:

- Asegúrate de que el cliente tiene el adaptador de red configurado en modo red interna y en la misma red (RedInterna).

**▸** Verifica si el cliente obtiene una IP:

- En el cliente abre la terminal o símbolo del sistema y usa el comando ipconfig .

- Si la dirección MAC del cliente está en la lista de permitidos, debería recibir una IP del servidor DHCP.

- Si está en la lista de denegados, el cliente no obtendrá ninguna IP.

#### Paso 5. Ajustes finales y verificación

**▸** Revisión de *logs:*

- En administrador de DHCP, puedes verificar los registros de eventos para confirmar que el filtrado de MAC está funcionando según lo esperado.

**▸** Comprobación final:

- Prueba con distintas direcciones MAC para verificar la efectividad del filtrado de MAC, agregando más dispositivos a la lista de permitidos o denegados según el comportamiento que desees observar.

#### Conclusión

Este proceso completa la configuración del filtrado de MAC en Windows Server en un entorno VirtualBox. Esta configuración permite limitar el acceso a la red a dispositivos específicos, proporcionando una capa básica de seguridad en la red interna que se ha configurado en VirtualBox.

#### Preguntas planteadas

**¿Cómo mejora la seguridad de la red el uso de filtrado de direcciones MAC?**

El filtrado de direcciones MAC mejora la seguridad de la red al controlar qué dispositivos pueden conectarse a la red basándose en sus identificadores únicos (direcciones MAC). Al permitir únicamente las direcciones MAC autorizadas, se restringe el acceso a dispositivos no reconocidos, lo que protege la red contra accesos no autorizados. Este método actúa como una capa adicional de seguridad, especialmente, en redes pequeñas o en situaciones donde no se cuentan con medidas avanzadas de autenticación, como en entornos domésticos o de pequeñas oficinas.

Beneficios específicos:

**▸** Restricción de acceso no autorizado: solo los dispositivos con direcciones MAC en la lista de permitidos pueden acceder a la red.

**▸** Prevención de intrusos: los dispositivos no autorizados no pueden obtener una dirección IP y, por lo tanto, no pueden participar en la red.

**▸** Facilidad de administración: la lista de direcciones MAC es fácil de gestionar en redes pequeñas y permite un control más directo sobre los dispositivos conectados.

**¿Qué limitaciones presenta el filtrado de MAC en un entorno real frente a**

#### posibles ataques?

A pesar de ser una herramienta útil para la seguridad de redes pequeñas, el filtrado de direcciones MAC tiene varias limitaciones importantes en entornos reales:

**▸** Vulnerabilidad al MAC *spoofing:* los atacantes pueden suplantar una dirección MAC (MAC *spoofing)* para hacer que un dispositivo no autorizado parezca legítimo. Esto es posible porque las direcciones MAC no están diseñadas para ser un medio de autenticación seguro.

**▸** Escalabilidad limitada: en redes grandes, gestionar y mantener una lista de direcciones MAC puede volverse un desafío. A medida que más dispositivos se conectan, las listas se vuelven más difíciles de administrar y menos efectivas.

**▸** No proporciona autenticación real: el filtrado de MAC solo verifica la dirección de *hardware,* no garantiza que un dispositivo sea de confianza o que esté autorizado de alguna otra manera. Esto lo hace menos confiable frente a métodos de autenticación más robustos.

**▸** Redundancia de dispositivos: en redes dinámicas, donde los dispositivos pueden unirse y salir frecuentemente, el filtrado de MAC puede no ser tan práctico, ya que requiere actualizar constantemente las listas de dispositivos autorizados.

#### ¿Qué ventajas ofrece la simulación en VirtualBox para probar configuraciones

#### de red y de seguridad?

La simulación en VirtualBox ofrece varias ventajas cuando se trata de probar configuraciones de red y de seguridad sin poner en riesgo una infraestructura real:

**▸** Entorno controlado: VirtualBox proporciona un entorno aislado donde puedes realizar pruebas sin afectar a una red en producción. Puedes experimentar con diversas configuraciones y ver cómo afectan el comportamiento de la red y los dispositivos sin riesgo de interrupciones.

**▸** Facilidad de prueba de configuraciones: puedes probar configuraciones como el filtrado de MAC, la segmentación de red o, incluso, protocolos de seguridad sin tener que realizar cambios en la infraestructura física. Esto permite realizar pruebas de forma rápida y económica.

**▸** Repetibilidad y flexibilidad: VirtualBox permite crear y borrar máquinas virtuales con facilidad. Puedes probar diferentes configuraciones, restaurar el sistema a un estado anterior y repetir los procesos de prueba tantas veces como sea necesario.

**▸** Prueba de múltiples escenarios: Puedes crear diversas redes y máquinas virtuales con diferentes roles (servidores, clientes, etc.), lo que te permite simular un entorno más realista para probar políticas de seguridad, como filtrado de MAC, autenticación, DHCP, etc.

**▸** Eficiencia de costos: no necesitas invertir en *hardware* adicional ni en configuraciones físicas para realizar pruebas de red. VirtualBox te permite emular redes complejas utilizando solo un equipo físico.

**▸** Facilita el aprendizaje: al proporcionar un entorno de prueba accesible, VirtualBox es una excelente herramienta educativa para aprender sobre redes y seguridad sin la necesidad de tener experiencia previa en redes físicas.

# Entrenamiento 2. Configuración de filtrado de

# direcciones MAC en un entorno Ubuntu en VirtualBox

#### ▸ Planteamiento del ejercicio

En esta actividad se te guiará a través de la configuración de un servidor Ubuntu que actuará como servidor DHCP, encargado de asignar direcciones IP a los dispositivos en la red. Configurarás el filtrado de direcciones MAC para controlar el acceso de los dispositivos, permitiendo solo a los dispositivos autorizados obtener una dirección IP en la red. La actividad se realiza dentro de un entorno virtualizado en VirtualBox, lo que te permitirá simular y analizar la configuración de redes de manera segura. Competencias que desarrollar:

**▸** Implementar y configurar un servidor DHCP en Ubuntu.

**▸** Configurar el filtrado de direcciones MAC para restringir el acceso a la red.

**▸** Evaluar y analizar la efectividad del filtrado de MAC para aumentar la seguridad de la red. Requisitos previos:

**▸** VirtualBox instalado en tu máquina.

**▸** Máquinas virtuales:

- Ubuntu Server configurado como servidor DHCP.

- Máquina cliente (puede ser otro sistema Ubuntu o Windows) configurada para obtener IP automáticamente.

**▸** Conocimientos básicos sobre redes y DHCP.

#### ▸ Desarrollo paso a paso

#### Paso 1. Configurar el entorno en VirtualBox

**▸** Crear una red interna.

**▸** Configurar las máquinas virtuales.

#### Paso 2. Instalar y configurar el servidor DHCP en Ubuntu

**▸** Instalar el servidor DHCP.

**▸** Configurar el servidor DHCP.

**▸** Configurar la interfaz de red del servidor DHCP.

**▸** Reiniciar el servidor DHCP.

#### Paso 3. Implementar filtrado de direcciones MAC

**▸** Configurar el filtrado de MAC.

**▸** Reiniciar el servidor DHCP.

#### Paso 4. Verificación de la configuración

**▸** Obtener la dirección MAC del cliente.

**▸** Verificar si el filtrado de MAC está funcionando:

- Si la dirección MAC está permitida en el archivo de configuración del servidor, el cliente debería recibir una IP.

- Si la dirección MAC está bloqueada, el cliente no recibirá una IP.

#### Paso 5. Análisis de resultados

**▸** Pruebas de conexión:

- Conecta o desconecta dispositivos y observa si el filtrado de MAC está funcionando correctamente. El servidor debe permitir solo a las direcciones MAC configuradas.

**▸** Documentación:

- Documenta el proceso de configuración, incluyendo los archivos editados y las capturas de pantalla de las pruebas realizadas.

#### Preguntas de reflexión

**▸** ¿Cómo mejora la seguridad de la red el uso de filtrado de direcciones MAC en Ubuntu? **▸** ¿Qué limitaciones presenta el filtrado de MAC en un entorno real frente a posibles ataques? **▸** ¿Qué ventajas ofrece la simulación en VirtualBox para probar configuraciones de red y de seguridad en Ubuntu?

#### Entregables

El informe de la actividad, que debe incluir:

**▸** Las capturas de pantalla del proceso de configuración.

**▸** Las respuestas a las preguntas de reflexión.

**▸** Una explicación de cómo el filtrado de MAC mejora la seguridad en la red.

#### ▸ Solución

Paso 1. Configurar el entorno en VirtualBox **▸** Crear una red interna:

- Abre VirtualBox y crea una red interna para ambas máquinas virtuales: la de Ubuntu Server y la de cliente.

- Asegúrate de que ambas máquinas estén conectadas a esta red interna.

**▸** Configurar las máquinas virtuales:

- La máquina virtual con Ubuntu Server debe tener suficiente RAM y CPU para actuar como un servidor DHCP.

- La máquina cliente debe estar configurada para obtener IP automáticamente desde el servidor DHCP de Ubuntu.

#### Paso 2. Instalar y configurar el servidor DHCP en Ubuntu

Instalar el servidor DHCP: **▸** Inicia Ubuntu Server y abre una terminal. **▸** Instala el paquete ISC DHCP Server:

![image-13](images/image-13.png)

Configurar el servidor DHCP: **▸** Abre el archivo de configuración del servidor DHCP:

![image-14](images/image-14.png)

![▸ Configura un rango de IP para el servidor DHCP: Configurar la interfaz de red del servidor DHCP:](images/image-15.png)

**▸** Edita el archivo /etc/default/isc-dhcp-server para especificar la interfaz de red:

![image-16](images/image-16.png)

**▸** Asegúrate de que la línea INTERFACESv4 contenga el nombre de la interfaz de red correspondiente (por ejemplo, eth0 o ens33 ).

Reiniciar el servidor DHCP: **▸** Reinicia el servicio DHCP:

![image-17](images/image-17.png)

#### Paso 3. Implementar filtrado de direcciones MAC

Configurar el Filtrado de MAC: **▸** En el archivo dhcpd.conf , agrega configuraciones para permitir o denegar direcciones MAC específicas:

![▸ Para permitir una dirección MAC específica:](images/image-18.png)

**▸** Para denegar direcciones MAC no autorizadas, añade:

![image-19](images/image-19.png)

Reiniciar el servidor DHCP: **▸** Después de editar el archivo dhcpd.conf , reinicia el servidor DHCP:

![image-20](images/image-20.png)

#### Paso 4. Verificación de la configuración

Obtener la dirección MAC del cliente: **▸** Inicia la máquina cliente y ejecuta el comando ifconfig o ip a para obtener la dirección MAC. **▸** Verificar si el filtrado de MAC está funcionando:

- Si la dirección MAC está permitida en el archivo de configuración del servidor, el cliente debería recibir una IP.

- Si la dirección MAC está bloqueada, el cliente no recibirá una IP.

#### Paso 5. Análisis de resultados

Pruebas de conexión: **▸** Conecta o desconecta dispositivos y observa si el filtrado de MAC está funcionando correctamente. El servidor debe permitir solo a las direcciones MAC configuradas. Documentación: **▸** Documenta el proceso de configuración, incluyendo los archivos editados y las capturas de pantalla de las pruebas realizadas.

#### Preguntas de reflexión

**¿Cómo mejora la seguridad de la red el uso de filtrado de direcciones MAC en**

#### Ubuntu?

El filtrado de direcciones MAC mejora la seguridad de la red al restringir el acceso a dispositivos autorizados basados en sus direcciones únicas. Al configurar el servidor DHCP para que solo asigne direcciones IP a dispositivos con direcciones MAC específicas, se previene que dispositivos no autorizados o maliciosos se conecten a la red. Esto ayuda a evitar el acceso no autorizado a los recursos de la red y puede reducir riesgos de ataques como el *spoofing* de MAC. Este enfoque proporciona un control adicional sobre qué dispositivos pueden conectarse a la red, mejorando la seguridad general, especialmente en redes internas o sensibles.

**¿Qué limitaciones presenta el filtrado de MAC en un entorno real frente a**

#### posibles ataques?

A pesar de ser una capa adicional de seguridad, el filtrado de MAC tiene varias limitaciones en un entorno real:

**▸** Vulnerabilidad al MAC *spoofing:* los atacantes pueden falsificar *(spoof)* la dirección MAC de un dispositivo autorizado y hacerse pasar por él. Esto se puede hacer con herramientas especializadas, permitiendo a los atacantes eludir el filtrado de MAC.

**▸** Escalabilidad: en redes grandes con muchos dispositivos, gestionar las direcciones MAC de todos los dispositivos puede ser complicado y propenso a errores. Los administradores deben actualizar las configuraciones constantemente cuando se agregan o eliminan dispositivos.

**▸** No es una solución completa: el filtrado de MAC por sí solo no es suficiente para asegurar una red, ya que no impide otros tipos de ataques, como DDoS, *phishing* o *malware.* Es solo una capa más en una estrategia de seguridad más amplia.

#### ¿Qué ventajas ofrece la simulación en VirtualBox para probar configuraciones

#### de red y de seguridad en Ubuntu?

La simulación en VirtualBox para probar configuraciones de red y de seguridad en Ubuntu tiene varias ventajas:

**▸** Entorno controlado y seguro: VirtualBox permite crear redes virtuales aisladas, lo que te permite probar configuraciones sin poner en riesgo tu red real. Esto es útil para hacer pruebas de seguridad, como el filtrado de MAC, sin interferir con otros sistemas.

**▸** Facilidad de prueba y ajuste: puedes probar diferentes configuraciones rápidamente, hacer ajustes y verificar su funcionamiento sin interrumpir los dispositivos o servicios reales. Es posible agregar y eliminar máquinas virtuales fácilmente, lo que facilita probar cómo interactúan diferentes dispositivos con la red.

**▸** Simulación de diversos escenarios: VirtualBox permite simular diferentes escenarios de red, como configuraciones de seguridad, ataques potenciales y fallos en los sistemas, todo dentro de un entorno controlado. Esto te ayuda a entender el impacto de las configuraciones y anticipar posibles problemas antes de implementarlas en una red real.

**▸** Ahorro de costos: puedes realizar pruebas sin necesidad de *hardware* adicional, lo que reduce los costos y el tiempo necesario para configurar entornos físicos.

En resumen, VirtualBox proporciona una plataforma flexible y segura para probar configuraciones de red y seguridad, permitiendo a los administradores realizar experimentos sin los riesgos asociados a la implementación directa en una red real.

Este enunciado proporciona una guía completa para llevar a cabo la actividad de filtrado de direcciones MAC en un entorno de Ubuntu Server en VirtualBox, permitiéndote practicar y comprender cómo aumentar la seguridad de las redes a través de este mecanismo.

# Entrenamiento 3. Implementación de SMTP AUTH

# en un servidor de correo en Ubuntu

#### ▸ Planteamiento del ejercicio

En esta actividad, simularás un servidor de correo en un entorno virtualizado, utilizando VirtualBox para crear una máquina virtual con Ubuntu. Configurarás un servidor de correo con Postfix y SASL para implementar la autenticación SMTP. También, asegurarás que el servidor utilice TLS para garantizar la seguridad en la transmisión de correos electrónicos. Requisitos previos:

**▸** VirtualBox instalado en tu máquina física *(host).*

**▸** Ubuntu Server como sistema operativo para la máquina virtual.

**▸** Conocimientos básicos sobre administración de servidores Linux y de herramientas de virtualización. Material requerido:

**▸** VirtualBox instalado y configurado en tu equipo.

**▸** Imagen ISO de Ubuntu Server (última versión disponible).

**▸** Acceso a Internet en la máquina virtual para instalar paquetes.

**▸** Acceso a privilegios de *root* o sudo en Ubuntu.

#### ▸ Desarrollo paso a paso

- Creación de la máquina virtual en VirtualBox

- Instalar los paquetes necesarios

- Configurar Postfix para usar autenticación SMTP (SMTP AUTH)

- Configurar SASL para la autenticación.

- Reiniciar los servicios.

- Configurar TLS para cifrar las conexiones de correo.

- Verificar la configuración.

- Prueba de la configuración con un cliente de correo.

Evaluación: **▸** Correcta configuración de Postfix y SASL para habilitar la autenticación SMTP. **▸** Implementación de seguridad con TLS para cifrar las comunicaciones. **▸** Verificación de que solo los usuarios autenticados pueden enviar correos electrónicos. **▸** Pruebas con un cliente de correo para verificar la autenticación y el envío de correos.

#### ▸ Solución

#### Creación de la máquina virtual en VirtualBox

**▸** Abre VirtualBox y crea una nueva máquina virtual con las siguientes especificaciones:

- Nombre: servidor de correo SMTP

- Tipo: Linux

- Versión: Ubuntu (64-bit)

- Memoria: 1024 MB (puedes aumentar si tienes más recursos)

- Disco duro: crear un disco duro virtual de 10 GB o más.

**▸** Inicia la máquina virtual y monta la imagen ISO de Ubuntu Server para la instalación.

**▸** Completa el proceso de instalación de Ubuntu Server.

#### Instalar los paquetes necesarios

Una vez instalado Ubuntu Server, debes acceder a la máquina virtual e instalar los paquetes necesarios para configurar el servidor de correo y la autenticación SMTP.

**▸** Instalar Postfix, SASL y paquetes requeridos:

![image-21](images/image-21.png)

**▸** Postfix: servidor de correo.

**▸** SASL: mecanismo de autenticación.

**▸** libsasl2-2 y libsasl2-modules: librerías necesarias para soportar la autenticación

SMTP.

#### Configurar Postfix para usar autenticación SMTP (SMTP AUTH)

Edite el archivo de configuración principal de Postfix para habilitar la autenticación SMTP.

![image-22](images/image-22.png)

![Agrega o descomenta las siguientes líneas: Configurar SASL para la autenticación](images/image-23.png)

**▸** Configura el servicio saslauthd para autenticar a los usuarios del sistema.

**▸** Edita el archivo de configuración de `saslauthd`:

![image-24](images/image-24.png)

**▸** Asegúrate de que las siguientes líneas estén configuradas:

![image-25](images/image-25.png)

**▸** Esto configura saslauthd para usar PAM (Pluggable Authentication Modules) como mecanismo de autenticación.

#### Reiniciar los servicios

Reinicia los servicios necesarios para aplicar la configuración:

![image-26](images/image-26.png)

#### Configurar TLS para cifrar las conexiones de correo

Para habilitar TLS y asegurar las comunicaciones entre el servidor de correo y los clientes, edita el archivo de configuración de Postfix.

![image-27](images/image-27.png)

Agrega o asegúrate de que las siguientes líneas estén configuradas correctamente:

![image-28](images/image-28.png)

Estos certificados son los predeterminados en Ubuntu. Para un entorno real, deberías usar certificados SSL/TLS válidos.

#### Verificar la configuración

Verifica que la autenticación SMTP está habilitada y funcionando correctamente. Usa telnet para probar la autenticación SMTP en el puerto 25.

![image-29](images/image-29.png)

En la sesión de telnet, ejecuta los siguientes comandos:

![image-30](images/image-30.png)

Te pedirá un nombre de usuario y una contraseña, que se deben proporcionar en formato base64.

#### Prueba de la configuración con un cliente de correo

Configura un cliente de correo (por ejemplo, Thunderbird) para conectarse a tu servidor SMTP utilizando autenticación y TLS:

**▸** Servidor SMTP: dirección IP de tu máquina virtual o nombre de dominio.

**▸** Puerto SMTP: 587 (para TLS).

**▸** Método de autenticación: PLAIN o LOGIN.

**▸** Nombre de usuario: usuario local en Ubuntu.

**▸** Contraseña: la contraseña del usuario local. Envía un correo desde el cliente de correo asegurándote de que la autenticación SMTP está funcionando correctamente.

Evaluación: **▸** Correcta configuración de Postfix y SASL para habilitar la autenticación SMTP. **▸** Implementación de seguridad con TLS para cifrar las comunicaciones. **▸** Verificación de que solo los usuarios autenticados pueden enviar correos electrónicos. **▸** Pruebas con un cliente de correo para verificar la autenticación y el envío de correos.

# Entrenamiento 4. Configuración de un servidor

# Web seguro en Windows Server usando IIS7

#### ▸ Planteamiento del ejercicio

Se desea configurar un servidor Windows Server para que funcione como servidor web utilizando IIS7 (Internet Information Services). Este servidor deberá asegurar la comunicación con los clientes utilizando certificados autofirmados y el protocolo HTTPS. A continuación, se presentan los requisitos y las instrucciones para la configuración:

Requisitos del sitio web virtual

**▸** Protocolo de acceso:

- El sitio web deberá ser accesible únicamente mediante el protocolo HTTPS.

- Debe utilizar la dirección IP 192.168.20.17.

**•** El nombre del sitio debe ser <www.seguro.com>.

- El acceso debe realizarse a través del puerto predeterminado para HTTPS, el puerto 443.

**▸** Documento predeterminado:

- La página inicial del sitio web debe mostrar una imagen en el navegador del cliente con el texto «SERVIDOR SEGURO» o incluir una imagen que diga «SERVIDOR SEGURO».

**▸** Certificados autofirmados:

- Para asegurar la comunicación HTTPS, crea un certificado autofirmado utilizando la herramienta de IIS7 en Windows Server.

#### ▸ Desarrollo paso a paso

Instrucciones para la configuración:

**▸** Instalación y configuración de IIS:

- Instala el rol de servidor web (IIS) en Windows Server.

- Configura el sitio web en IIS7 con la IP, nombre de host y puerto indicados en los requisitos.

**▸** Generación del certificado autofirmado:

- Crea un certificado autofirmado en IIS7 y asígnalo al sitio web para permitir el acceso mediante HTTPS.

**▸** Configuración del documento predeterminado:

- Establece el documento predeterminado del sitio web con el contenido de SERVIDOR SEGURO o una imagen similar que se visualizará en el navegador del cliente.

#### Comprobación del funcionamiento desde un Cliente Ubuntu

Para verificar el correcto funcionamiento del sitio web:

**▸** Accede al sitio web desde un cliente con Ubuntu a través de un navegador utilizando la URL <https://192.168.20.17> o <https://www.seguro.com>.

**▸** Observa el comportamiento del navegador:

- Dado que se está utilizando un certificado autofirmado, es posible que el navegador muestre una advertencia de seguridad indicando que el sitio no es de confianza. Esta advertencia es normal, ya que los navegadores solo confían en certificados

Servicios en Red e Internet 67 Tema 7. Entrenamientos emitidos por autoridades certificadoras oficiales.

- Si ocurre esta advertencia, acepta el riesgo para continuar y acceder al sitio.

Al finalizar, asegúrate de que el sitio web se cargue correctamente con el contenido esperado y que la conexión esté asegurada mediante HTTPS.

#### ▸ Solución

#### Paso 1. Preparación del entorno virtual en VirtualBox

Crear las máquinas virtuales (MV):

**▸** Abre VirtualBox y selecciona «Nueva» para crear dos máquinas virtuales:

- MV 1: Windows Server (versión compatible con IIS7, como Windows Server 2008).

- MV 2: Ubuntu (para realizar pruebas como cliente).

**▸** Asigna los recursos (memoria, almacenamiento) necesarios para cada MV y completa el proceso de configuración de cada una. Configuración de red en VirtualBox:

**▸** Para que ambas máquinas se comuniquen en la misma red:

- Ve a la configuración de red de cada MV.

- Selecciona Adaptador de red > Conectado a: Red Interna.

- Asegúrate de asignar el mismo nombre de red interna a ambas máquinas para que puedan comunicarse.

#### Paso 2. Configuración de Windows Server con IIS7

Configuración de la red en Windows Server:

**▸** Inicia la MV de Windows Server. **▸** Asigna una IP estática:

- Ve a Centro de redes y recursos compartidos > Cambiar configuración del adaptador.

- Haz clic derecho en el adaptador de red y selecciona Propiedades > Protocolo de Internet versión 4 (TCP/IPv4).

- Ingresa la IP 192.168.20.17, una máscara de subred de 255.255.255.0 y, si es necesario, una puerta de enlace (opcional en este caso).

Instalar IIS7: **▸** Abre Server Manager. **▸** Selecciona «Add Roles and Features» y añade el rol de Web Server (IIS). **▸** Sigue las indicaciones y completa la instalación. Crear el sitio web en IIS7: **▸** Abre IIS Manager en Windows Server. **▸** En el panel izquierdo, selecciona el servidor y expande «Sites». **▸** Haz clic derecho en «Sites» y selecciona «Add Web Site». Configura el sitio: **•** Site name: <www.seguro.com>.

- Physical path: elige una carpeta en el servidor donde se almacenarán los archivos del sitio.

- Binding.

- Type: HTTPS.

- IP address: 192.168.20.17.

- Port: 443.

**•** Host name: <www.seguro.com>. **▸** Haz clic en «OK» para crear el sitio. Generar un certificado autofirmado: **▸** En IIS Manager, selecciona el servidor y haz clic en «Server Certificates». **▸** Selecciona «Create Self-Signed Certificate» y nómbralo Certificado_Seguro. **▸** Vuelve a la configuración de Bindings del sitio web y asigna este certificado autofirmado para HTTPS. Configurar el documento predeterminado: **▸** En IIS Manager, selecciona tu sitio web (<www.seguro.com>) y ve a «Default Document». **▸** Agrega o edita el documento predeterminado para incluir el texto o una imagen que diga «SERVIDOR SEGURO».

#### Paso 3. Configuración del cliente Ubuntu

Configuración de la red en Ubuntu: **▸** Inicia la MV de Ubuntu. **▸** Abre la configuración de red y asigna una IP estática en el mismo rango que el servidor, como 192.168.20.18, con una máscara de subred 255.255.255.0. Configurar el archivo *hosts:*

Para resolver el nombre del servidor en Ubuntu:

**▸** Abre una terminal y edita el archivo hosts:

![image-31](images/image-31.png)

**▸** Agrega la línea:

![image-32](images/image-32.png)

**▸** Guarda y cierra el archivo.

#### Paso 4. Comprobación del funcionamiento desde Ubuntu

**▸** Abre un navegador web en la máquina virtual de Ubuntu.

**▸** Ingresa la URL <https://www.seguro.com>.

**▸** Debería aparecer una advertencia de seguridad, ya que se trata de un certificado

autofirmado. **▸** Acepta el riesgo para continuar y verifica que el sitio cargue y que el contenido predeterminado, SERVIDOR SEGURO, se muestre.

#### Solución de problemas

**▸** Problemas de red: si no puedes acceder al sitio, verifica que ambas MV estén en la misma red interna y que las IP estén configuradas correctamente. **▸** Certificado no confiable: los navegadores muestran advertencias de seguridad para certificados autofirmados. Esto es normal; simplemente agrega una excepción.

Al completar estos pasos, habrás configurado un servidor seguro en Windows Server utilizando IIS7 y un certificado autofirmado.

# Entrenamiento 5. Configuración de un Servidor

# Web Seguro en Ubuntu con Apache2

#### ▸ Planteamiento del ejercicio

Se desea configurar un servidor web seguro en un sistema operativo Ubuntu utilizando Apache2. Este servidor debe asegurar la comunicación con los clientes mediante el protocolo HTTPS y certificados autofirmados generados con OpenSSL.

#### ▸ Desarrollo paso a paso

**▸** Instalación de *software:* asegúrate de que el servidor Ubuntu tiene instalados Apache2 y OpenSSL. Si no están instalados, deberás instalarlos.

**▸** Creación de un certificado autofirmado: usa OpenSSL para crear un certificado autofirmado que permitirá a Apache2 gestionar conexiones seguras mediante HTTPS.

**▸** Configuración de un único sitio web virtual en Apache con las siguientes características:

- El sitio web debe estar disponible solo mediante el protocolo HTTPS, utilizando la dirección IP 192.168.21.15, el nombre de dominio <www.secure.es> y el puerto por defecto (443).

- El directorio raíz del sitio web debe ser /var/www/secure .

- Asegúrate de que el sitio web utilice el certificado autofirmado para encriptar las conexiones.

- Configura Apache para que el sitio virtual utilice SSL y esté configurado en el archivo de sitios disponibles.

**▸** Documento predeterminado del sitio web:

- Crea un archivo index.html en el directorio raíz

/var/www/secure con el contenido de

texto «SERVIDOR SEGURO» para verificar la visualización en el navegador del cliente.

**▸** Prueba de funcionamiento del sitio web:

**▸** Configura el archivo /etc/hosts en un cliente Ubuntu para que la dirección <www.secure.es> apunte a la IP del servidor (192.168.21.15).

**•** En el cliente, abre un navegador y accede a la URL <https://www.secure.es> para verificar que el sitio web es accesible y muestra el texto «SERVIDOR SEGURO».

**▸** Observación sobre la conexión segura:

- Durante la prueba, observa que el navegador podría mostrar una advertencia de seguridad debido a que el certificado es autofirmado y no ha sido emitido por una autoridad de certificación reconocida. Anota lo que ocurre y permite la excepción de seguridad en el navegador para confirmar el correcto funcionamiento del sitio.

Objetivo: esta actividad tiene como objetivo aprender a configurar un servidor Apache2 en Ubuntu para que gestione conexiones seguras mediante HTTPS utilizando un certificado autofirmado, además de familiarizarse con la configuración de sitios virtuales y certificados SSL en un entorno de servidor Linux.

#### ▸ Solución

Para realizar esta actividad en VirtualBox, sigue estos pasos detallados para configurar un servidor web seguro con Ubuntu y Apache2 usando HTTPS con un

Servicios en Red e Internet 73 Tema 7. Entrenamientos certificado autofirmado. Asegúrate de tener VirtualBox instalado y configurado en tu máquina anfitriona.

#### Paso 1. Crear y configurar la máquina virtual de Ubuntu

**▸** Crear una nueva máquina virtual:

- Abre VirtualBox y selecciona «Nueva».

- Asigna un nombre a la máquina virtual (por ejemplo, ServidorWebSeguro).

- Selecciona el tipo como Linux y la versión Ubuntu (64-bit).

- Ajusta la memoria RAM (recomendada: 1024 MB o más).

**▸** Configurar el almacenamiento:

- Añade un disco de instalación de Ubuntu (archivo .iso).

- Completa la configuración de almacenamiento y crea la máquina virtual.

**▸** Configurar la red:

- En «Configuración» de la VM, ve a «Red».

- Selecciona el «Adaptador de red฀» y elige «Adaptador de red interna» para permitir la comunicación entre la máquina anfitriona y la VM usando direcciones IP locales.

**▸** Instalar Ubuntu:

- Inicia la VM, sigue los pasos de instalación de Ubuntu y completa la configuración básica (idioma, zona horaria, nombre de usuario, contraseña, etc.).

#### Paso 2. Instalar Apache2 y OpenSSL en Ubuntu

Actualizar paquetes e instalar Apache2 y OpenSSL: **▸** Abre la terminal en la VM de Ubuntu.

**▸** Ejecuta los siguientes comandos:

![Paso 3. Configurar el sitio web virtual](images/image-33.png)

Crear el directorio para el sitio web:

![image-34](images/image-34.png)

Configurar el archivo de sitio virtual:

**▸** Crea un archivo de configuración en / etc/apache2/sites-available/secure.conf :

![image-35](images/image-35.png)

![▸ Añade la siguiente configuración: Activar el sitio virtual y el módulo SSL:](images/image-36.png)

![image-37](images/image-37.png)

#### Paso 4. Crear el certificado autofirmado con OpenSSL

Generar el certificado y la clave privada:

**▸** Ejecuta el siguiente comando para crear el certificado y la clave:

![image-38](images/image-38.png)

![image-39](images/image-39.png)

**▸** Completa los datos solicitados, indicando «www.secure.es» como «Common Name» cuando se solicite.

#### Paso 5. Crear el documento predeterminado

Crear un archivo HTML básico para el sitio:

![image-40](images/image-40.png)

![Añadir el contenido: Ajustar permisos para el directorio:](images/image-41.png)

![image-42](images/image-42.png)

**Paso 6. Configuración en la máquina cliente (otra VM o en la máquina**

#### anfitriona)

Si estás usando otra VM para simular el cliente, repite los pasos de creación de la VM y asegúrate de que esté en la misma red interna.

Modificar el archivo /etc/hosts en la máquina cliente para enlazar el nombre del sitio con la IP del servidor:

![image-43](images/image-43.png)

Añadir la línea:

![image-44](images/image-44.png)

#### Paso 7. Verificación de la conexión HTTPS

**▸** Acceder al sitio web:

- Abre el navegador en la máquina cliente.

**•** Ingresa la URL <https://www.secure.es>.

**▸** Excepción de seguridad:

- Debido a que el certificado es autofirmado, el navegador mostrará una advertencia de seguridad. Acepta la excepción para ver el sitio web.

- Deberías ver el mensaje «SERVIDOR SEGURO» en el navegador, indicando que la configuración es correcta.

#### Nota final

Esta actividad te ha guiado en el proceso de configuración de un servidor Apache2 en un entorno de red interna usando HTTPS y certificados autofirmados en VirtualBox. Recuerda que, en un entorno de producción, es recomendable usar certificados emitidos por una autoridad de advertencias de seguridad en los navegadores.

certificación reconocida para evitar

1. ¿Cuál de las siguientes opciones es una medida de seguridad para evitar que un

dispositivo no autorizado obtenga una dirección IP en una red DHCP?

    - A) DHCP snooping.

    - B) Filtrado de MAC.

    - C) IP Source Guard.

    - D) Encriptación de tráfico.

2. ¿Qué función tiene el IP Source Guard en una red?

    - A) Prevenir ataques de suplantación de IP.

    - B) Filtrar el tráfico de DHCP.

    - C) Encriptar las direcciones IP.

    - D) Configurar la dirección MAC de un dispositivo.

3. ¿Qué acción puede realizar un atacante si no se implementa DHCP snooping en

una red?

    - A) El atacante puede obtener la contraseña del rúter.

    - B) El atacante puede interceptar las direcciones IP de los dispositivos.

    - C) El atacante puede configurar un servidor DHCP malicioso.

    - D) El atacante puede cifrar las direcciones IP.

4. ¿En qué tipo de redes es más recomendable utilizar Subnetting?

    - A) Redes domésticas pequeñas.

    - B) Redes corporativas o empresariales.

    - C) Redes de área local (LAN) sin conexión a Internet.

    - D) Redes de servidores de bases de datos.

5. ¿Cuál de las siguientes afirmaciones sobre VLAN es correcta?

    - A) Las VLAN segmentan el tráfico de la red basándose únicamente en las

direcciones IP. B) Las VLAN permiten la segmentación del tráfico de red y mejoran la seguridad.

    - C) Las VLAN solo se utilizan para redes de área local (LAN).

    - D) Las VLAN desactivan el tráfico entre dispositivos de la misma red.

6. ¿Cuál es la principal ventaja de utilizar DHCP snooping en una red de switches?

    - A) Mejorar el rendimiento de la red.

    - B) Prevenir que un servidor DHCP malicioso responda a las solicitudes de los

clientes.

    - C) Encriptar las solicitudes DHCP.

    - D) Optimizar las direcciones IP asignadas.

7. ¿Qué es DNSSEC?

    - A) Un sistema de cifrado de consultas DNS.

    - B) Una extensión de seguridad para proteger las respuestas DNS mediante

firmas digitales.

    - C) Un método para bloquear servidores DNS no autorizados.

    - D) Un protocolo de autenticación para usuarios DNS.

8. ¿Cuál es el propósito principal de DNS spoofing?

    - A) Enviar respuestas DNS con la información correcta.

    - B) Modificar la respuesta de una consulta DNS para redirigir a los usuarios a

un sitio malicioso.

- C) Asegurar la integridad de las respuestas DNS.

- D) Mejorar la velocidad de resolución de consultas DNS.

9. ¿Qué técnica se utiliza para prevenir el DNS spoofing?

    - A) Criptografía simétrica.

    - B) DNSSEC.

    - C) Encriptación de correos electrónicos.

    - D) Firewall de aplicaciones web.

10. ¿Cuál de los siguientes es un riesgo del uso de resolución recursiva pública en

un servidor DNS?

    - A) Aumento de la velocidad de resolución de consultas.

    - B) Exposición a ataques de amplificación DDoS.

    - C) Mejora de la seguridad al bloquear peticiones no deseadas.

    - D) Reducción de los costos operativos.

11. ¿Qué es el DNS Tunneling?

    - A) Un método para cifrar las consultas DNS.

    - B) Un ataque que usa consultas DNS para esconder datos y realizar

comunicaciones maliciosas.

    - C) Un protocolo de enrutamiento para mejorar la eficiencia de DNS.

    - D) Una extensión para mejorar la fiabilidad de DNS.

12. ¿Qué protocolo se usa para proteger las consultas DNS mediante cifrado?

    - A) SSL/TLS.

    - B) DNSSEC.

    - C) DNS over HTTPS (DoH) o DNS over TLS (DoT).

    - D) VPN.

13. ¿Cuál es la principal razón por la que es crucial mantener actualizado el

servidor web?

    - A) Mejorar el rendimiento del servidor.

    - B) Garantizar que no se produzcan errores en la aplicación.

    - C) Corregir vulnerabilidades de seguridad conocidas.

    - D) Facilitar el uso de nuevas funciones.

14. ¿Qué medida se recomienda para asegurar la comunicación entre el servidor

web y los usuarios?

    - A) Usar contraseñas complejas.

    - B) Implementar SSL/TLS para cifrado.

    - C) Limitar el acceso por IP.

    - D) Configurar autenticación de dos factores.

15. ¿Qué medida de seguridad se debe tomar para evitar ataques de inyección

SQL?

    - A) Validar y escapar todas las entradas de usuario.

    - B) Desactivar todos los servicios en el servidor.

    - C) Usar contraseñas más largas.

    - D) Aplicar firewalls de aplicaciones.

16. ¿Qué servicio debería ser desactivado si no es necesario para la operación del

servidor web?

- A) FTP.

- B) SSH.

- C) HTTPS.

- D) DNS.

17. ¿Qué es un firewall de aplicaciones web (WAF) y por qué es importante?

    - A) Un firewall que filtra tráfico HTTP malicioso dirigido a las aplicaciones web.

    - B) Un firewall que protege el servidor de ataques DDoS.

    - C) Un firewall que actúa como un servidor proxy.

    - D) Un firewall que solo filtra tráfico HTTPS.

18. ¿Cuál es la función de la autenticación multifactor (2FA) en un servidor web?

    - A) Asegurar que solo los administradores tengan acceso.

    - B) Reemplazar contraseñas en el servidor.

    - C) Añadir una capa extra de seguridad mediante un segundo factor de

autenticación.

D) Limitar el acceso a direcciones IP específicas.

19. ¿Cuál de las siguientes opciones se utiliza para cifrar la comunicación entre el

cliente de correo y el servidor de correo en tránsito?

    - A) PGP (Pretty Good Privacy).

    - B) SSL (Secure Sockets Layer).

    - C) DKIM (DomainKeys Identified Mail).

    - D) SPF (Sender Policy Framework).

20. ¿Qué protocolo se utiliza para verificar que un correo electrónico proviene de un

servidor autorizado?

- A) DMARC.

- B) SPF.

- C) TLS.

- D) PGP.

21. ¿Cuál de las siguientes técnicas es un método de autenticación multifactor

(MFA) para acceder a un servidor de correo?

    - A) Contraseña de doce caracteres.

    - B) Token de seguridad enviado por SMS.

    - C) SPF.

    - D) DKIM.

22. ¿Qué protocolo permite que los correos electrónicos sean verificados y firmados

digitalmente para asegurar su autenticidad?

    - A) TLS.

    - B) SPF.

    - C) DKIM.

    - D) SSL.

23. ¿Cuál de las siguientes opciones ayuda a prevenir el envío de correos

electrónicos no deseados o *spam?*

    - A) DMARC.

    - B) Antivirus.

    - C) Filtro de spam.

    - D) Cifrado de extremo a extremo.

24. ¿Qué tipo de cifrado garantiza que solo el remitente y el destinatario puedan

leer el contenido del correo electrónico?

- A) Cifrado TLS.

- B) Cifrado de extremo a extremo.

- C) SPF.

- D) Filtro de antivirus.

25. ¿Cuál es el propósito de la autenticación SMTP en un servidor de correo

electrónico?

- A) Cifrar los correos electrónicos.

- B) Verificar la identidad de los usuarios antes de enviar correos.

- C) Filtrar correos electrónicos no deseados.

- D) Comprimir los archivos adjuntos.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–33)*
- A fondo  *(pp.34–39)*
- Entrenamientos  *(pp.40–78)*
- Test  *(pp.79–85)*
- Servicios en Red e Internet 5 Tema 7. Material de estudio · Servicios en Red e Internet 6 Tema 7. Material de estudio · Servicios en Red e Internet 7 Tema 7. Material de estudio · Servicios en Red e Internet 8 Tema 7. Material de estudio · Servicios en Red e Internet 10 Tema 7. Material de estudio · Servicios en Red e Internet 12 Tema 7. Material de estudio · Servicios en Red e Internet 14 Tema 7. Material de estudio · Servicios en Red e Internet 15 Tema 7. Material de estudio · Servicios en Red e Internet 16 Tema 7. Material de estudio · Servicios en Red e Internet 17 Tema 7. Material de estudio · Servicios en Red e Internet 18 Tema 7. Material de estudio · Servicios en Red e Internet 19 Tema 7. Material de estudio · Servicios en Red e Internet 20 Tema 7. Material de estudio · Servicios en Red e Internet 21 Tema 7. Material de estudio · Servicios en Red e Internet 22 Tema 7. Material de estudio · Servicios en Red e Internet 23 Tema 7. Material de estudio · Servicios en Red e Internet 24 Tema 7. Material de estudio · Servicios en Red e Internet 25 Tema 7. Material de estudio · Servicios en Red e Internet 26 Tema 7. Material de estudio · Servicios en Red e Internet 27 Tema 7. Material de estudio · Servicios en Red e Internet 28 Tema 7. Material de estudio · Servicios en Red e Internet 29 Tema 7. Material de estudio · Servicios en Red e Internet 30 Tema 7. Material de estudio · Servicios en Red e Internet 31 Tema 7. Material de estudio · Servicios en Red e Internet 32 Tema 7. Material de estudio · Servicios en Red e Internet 33 Tema 7. Material de estudio  *(pp.5, 6, 7, 8, 10, 12, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33)*
- Servicios en Red e Internet 34 Tema 7. A fondo · Servicios en Red e Internet 35 Tema 7. A fondo · Servicios en Red e Internet 36 Tema 7. A fondo · Servicios en Red e Internet 37 Tema 7. A fondo · Servicios en Red e Internet 38 Tema 7. A fondo · Servicios en Red e Internet 39 Tema 7. A fondo  *(pp.34–39)*
- Servicios en Red e Internet 40 Tema 7. Entrenamientos · Servicios en Red e Internet 42 Tema 7. Entrenamientos · Servicios en Red e Internet 43 Tema 7. Entrenamientos · Servicios en Red e Internet 44 Tema 7. Entrenamientos · Servicios en Red e Internet 45 Tema 7. Entrenamientos · Servicios en Red e Internet 46 Tema 7. Entrenamientos · Servicios en Red e Internet 47 Tema 7. Entrenamientos · Servicios en Red e Internet 48 Tema 7. Entrenamientos · Servicios en Red e Internet 49 Tema 7. Entrenamientos · Servicios en Red e Internet 50 Tema 7. Entrenamientos · Servicios en Red e Internet 51 Tema 7. Entrenamientos · Servicios en Red e Internet 52 Tema 7. Entrenamientos · Servicios en Red e Internet 53 Tema 7. Entrenamientos · Servicios en Red e Internet 54 Tema 7. Entrenamientos · Servicios en Red e Internet 55 Tema 7. Entrenamientos · Servicios en Red e Internet 56 Tema 7. Entrenamientos · Servicios en Red e Internet 57 Tema 7. Entrenamientos · Servicios en Red e Internet 58 Tema 7. Entrenamientos · Servicios en Red e Internet 59 Tema 7. Entrenamientos · Servicios en Red e Internet 60 Tema 7. Entrenamientos · Servicios en Red e Internet 61 Tema 7. Entrenamientos · Servicios en Red e Internet 62 Tema 7. Entrenamientos · Servicios en Red e Internet 63 Tema 7. Entrenamientos · Servicios en Red e Internet 64 Tema 7. Entrenamientos · Servicios en Red e Internet 65 Tema 7. Entrenamientos · Servicios en Red e Internet 66 Tema 7. Entrenamientos · Servicios en Red e Internet 68 Tema 7. Entrenamientos · Servicios en Red e Internet 69 Tema 7. Entrenamientos · Servicios en Red e Internet 70 Tema 7. Entrenamientos · Servicios en Red e Internet 71 Tema 7. Entrenamientos · Servicios en Red e Internet 72 Tema 7. Entrenamientos · Servicios en Red e Internet 74 Tema 7. Entrenamientos · Servicios en Red e Internet 75 Tema 7. Entrenamientos · Servicios en Red e Internet 76 Tema 7. Entrenamientos · Servicios en Red e Internet 77 Tema 7. Entrenamientos · Servicios en Red e Internet 78 Tema 7. Entrenamientos  *(pp.40, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 68, 69, 70, 71, 72, 74, 75, 76, 77, 78)*
- Servicios en Red e Internet 79 Tema 7. Test · Servicios en Red e Internet 80 Tema 7. Test · Servicios en Red e Internet 81 Tema 7. Test · Servicios en Red e Internet 82 Tema 7. Test · Servicios en Red e Internet 83 Tema 7. Test · Servicios en Red e Internet 84 Tema 7. Test · Servicios en Red e Internet 85 Tema 7. Test  *(pp.79–85)*