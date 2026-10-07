## Tema

## Seguridad y Alta Disponibilidad

# Tema 8. Seguridad

# perimetral

# Índice

Esquema Material de estudio

## 8.1. Introducción y objetivos

## 8.2. Principios de seguridad perimetral

## 8.3. Referencias bibliográficas

A fondo Snort Qué son los sistemas IDS e IPS y sus diferencias Firewall o cortafuegos: qué es y tipos de firewalls Servidor proxy: qué es y cuatro funciones que te interesan Qué es una VPN. Para qué sirve la VPN: cinco usos muy interesantes ¿Qué es una DMZ? Zona desmilitarizada en redes informáticas Todo sobre DMZ: para qué sirve y cómo configurarla en un router ¿Cuándo deberías usar una VPN? Entrenamientos

Entrenamiento 1: proxy Squid

Entrenamiento 2: firewall de Windows

Entrenamiento 3: firewall en Ubuntu

Entrenamiento 4: configuración de una VPN site-to-site

en Cisco Packet Tracer Entrenamiento 5: implementación de DMZ con Packet Tracer

# Esquema

![image-2](images/image-2.png)

Seguridad y Alta Disponibilidad 4 Tema . Esquema

## 8.1. Introducción y objetivos

La interconexión de redes corporativas con redes públicas aumenta los riesgos de ataques a los sistemas internos. Para protegerse, se implementan medidas de seguridad perimetral, que incluyen el uso de *firewalls,* zonas desmilitarizadas (DMZ), *virtual private network* (VPN), sistemas de detección de intrusos (IDS) y servidores *proxy.*

Los ***firewalls*** controlan el acceso mediante reglas predefinidas. Los **DMZ** proporcionan una capa adicional de seguridad, al ubicar ciertos servidores en una zona intermedia. Los **IDS** monitorean actividades sospechosas, por lo cual alertan sobre posibles intrusiones. Las **VPN** crean túneles seguros para la transmisión de datos. Los **servidores proxy** filtran el contenido y controlan el tráfico, con lo cual mejoran la seguridad y la privacidad.

Estas tecnologías combinadas forman una defensa integral contra las amenazas externas y los accesos no autorizados, con lo cual protegen los recursos internos de la red.

Los objetivos que se pretenden alcanzar en este tema son: **▸** Proteger la red interna de accesos no autorizados. **▸** Monitorear y detectar actividades sospechosas. **▸** Asegurar la transmisión segura de datos. **▸** Controlar y filtrar el tráfico de red. **▸** Mantener la privacidad y el anonimato de los usuarios. **▸** Actualizar y adaptar las medidas de seguridad. **▸** Balancear la seguridad con la accesibilidad.

## 8.2. Principios de seguridad perimetral

En el contexto de la seguridad de redes, cuando una red corporativa se interconecta con una red pública, como Internet, se incrementan significativamente los riesgos de ataques cibernéticos. Para mitigar estos riesgos se implementan diversas medidas de seguridad perimetral, las cuales actúan como la primera línea de defensa. A continuación, se describen algunas de estas medidas clave.

Firewall

Los cortafuegos *(firewalls)* son componentes fundamentales en la seguridad de las redes, ya que están diseñados para proteger la integridad y la confidencialidad de los datos al **controlar el tráfico de red** entrante y saliente. Funcionan como barreras entre redes de diferentes niveles de confianza, por ejemplo, entre una red privada y una red pública como Internet. Aquí se desarrollan en detalle sus tipos, funciones y mejores prácticas.

#### Tipos de firewalls

**▸** ***Firewalls*** **de filtrado de paquetes(packet** *filtering):* inspeccionan cada paquete de datos que atraviesa el *firewall* y toman decisiones basadas en las direcciones IP de origen y destino, puertos y protocolos.

- Uso típico: es ideal para configuraciones simples en las que la seguridad de base es suficiente.

- Implementación: es rápida y sencilla, generalmente se configura en routers.

**▸** ***Firewalls*** **de inspección con estado(stateful** *inspection):* monitorean el estado de las conexiones activas y toman decisiones en función del estado y el contexto de la conexión (por ejemplo, si una conexión es una respuesta a una solicitud previa).

- Uso típico: es adecuado para redes que requieren un nivel de seguridad intermedio, ya que protege contra ataques basados en el estado de la conexión.

- Implementación: es más complejo que el filtrado de paquetes, por lo que generalmente es implementado en dispositivos dedicados.

**▸** ***Firewalls*** **a nivel de aplicación** *(application-level gateways* o *proxy firewalls):* inspeccionan y filtran el tráfico a nivel de aplicación, lo que permite una profunda inspección del contenido de los paquetes.

- Uso típico: es ideal para redes en las que se necesita un control exhaustivo del tráfico de las aplicaciones, como en empresas con requisitos estrictos de seguridad.

- Implementación: requiere una configuración detallada y es más intensivo en recursos.

**▸** ***Firewalls*** **de nueva generación** *(next-generation firewalls,* NGFW): integran múltiples capacidades de seguridad, lo cual incluye la inspección profunda de paquetes (DPI), la prevención de intrusiones (IPS), el control de aplicaciones y más.

- Uso típico: es adecuado para organizaciones que necesitan una seguridad avanzada y multifuncional.

- Implementación: puede ser compleja y costosa, idealmente es manejado por personal especializado en seguridad.

![image-3](images/image-3.png)

Tabla 1. Comparación de los tipos de *firewall.* Fuente: elaboración propia.

#### Ejemplos de cada tipo de FW

Filtrado de paquetes *(packet filtering):* **Cisco ASA 5500 Series.**

**Descripción:** los dispositivos Cisco ASA 5500 Series son *appliances* de seguridad que ofrecen funciones de *firewall,* VPN y otros servicios de seguridad. Utilizan el filtrado de paquetes para controlar el tráfico basándose en reglas de IP, puertos y protocolos.

**Características adicionales:** además del filtrado de paquetes, incluyen capacidades de *firewall* de inspección con estado, VPN y otras funciones de seguridad avanzadas.

Inspección con estado *(stateful inspection):* **pfSense.**

**Descripción:** pfSense es una plataforma de *firewall* de código abierto que proporciona una inspección con estado de las conexiones de red, lo que permite una gestión detallada del tráfico en función del estado de la conexión.

**Características adicionales:** pfSense ofrece una amplia gama de funciones, lo cual incluye balanceo de carga, VPN y características de seguridad adicionales como detección y prevención de intrusiones.

Nivel de aplicación *(application-level gateways* o *proxy firewalls):* **Squid.**

**Descripción:** Squid es un servidor *proxy* y caché web de código abierto que permite el control detallado del tráfico HTTP, HTTPS y FTP. Funciona a nivel de aplicación, mediante el filtrado del contenido según reglas específicas.

**Características adicionales:** Squid puede mejorar el rendimiento del acceso web mediante el almacenamiento en caché de contenido frecuentemente solicitado y ofrece controles detallados de acceso a nivel de aplicación.

*Next-generation firewalls* (NGFW): **Palo Alto Networks PA Series.**

**Descripción:** los dispositivos de la serie PA de Palo Alto Networks son *firewalls* de próxima generación que integran múltiples funciones de seguridad, las cuales incluyen inspección profunda de paquetes (DPI), prevención de intrusiones (IPS), control de aplicaciones y protección contra amenazas avanzadas.

**Características adicionales:** estos *firewalls* ofrecen capacidades avanzadas como la segmentación de red basada en usuarios, el análisis del comportamiento de amenazas y la administración centralizada para entornos empresariales complejos.

Estos ejemplos ilustran cómo se implementan los diferentes tipos de *firewalls* en productos específicos, con lo que se proporcionan **opciones variadas según las** **necesidades** de seguridad de una red

Configurar un *firewall* implica **definir políticas de seguridad** que determinen qué tráfico se permite y cuál se bloquea.

Esto puede incluir reglas basadas en

direcciones IP, puertos, protocolos y contenido de los paquetes de datos. La gestión d e *firewalls* implica un monitoreo regular y actualizaciones para adaptarse a las nuevas amenazas y cambios en la red.

#### Funciones de los firewalls

**▸ Filtrado de tráfico:** bloquea o permite el tráfico según reglas predefinidas.

**▸ Control de acceso:** definición de quién o qué puede acceder a determinados recursos de la red.

**▸ Monitoreo de tráfico:** registro de eventos y generación de informes sobre el tráfico de red.

**▸ Protección contra amenazas:** detección y bloqueo de intentos de intrusión y ataques cibernéticos.

**▸ Políticas de seguridad:** implementación y aplicación de políticas de seguridad a nivel de red y de aplicación.

#### Mejores prácticas en el uso de firewalls

Las mejores prácticas en el uso de *firewalls*

son esenciales para mantener una

infraestructura de red segura y eficiente. En primer lugar, es fundamental establecer una definición clara de **políticas de seguridad.** Esto implica la creación de reglas específicas sobre el tráfico permitido y el que se debe bloquear, así como la revisión y actualización periódica de estas políticas para adaptarse a las nuevas amenazas.

Otra práctica importante es la **segmentación de red.** Esto consiste en implementar *firewalls* entre diferentes segmentos de la red para contener ataques potenciales y utilizar DMZ para aislar los servicios públicos, como los servidores web, de la red interna. De esta forma, se minimizan los riesgos de que un ataque a un servicio público afecte al resto de la red.

El **monitoreo y registro continuo** es otra medida crucial. Configurar el *firewall* para registrar todos los eventos relevantes y analizar regularmente estos registros permite identificar y responder a incidentes de seguridad de manera oportuna. Este análisis regular es esencial para detectar patrones inusuales o actividades sospechosas que puedan indicar una brecha de seguridad.

Mantener el *firmware* y *software* del *firewall* actualizaciones y parches protegen contra

**actualizados** es también vital. Las las vulnerabilidades conocidas.

Implementar un proceso riguroso de gestión de parches asegura que estas actualizaciones se apliquen de manera eficiente y sin demoras.

Además, realizar **pruebas y auditorías regulares** contribuye a evaluar la efectividad del *firewall.* Las pruebas de penetración y auditorías de seguridad periódicas ayudan a identificar debilidades en la configuración y en las reglas del *firewall.* Basándose en los resultados de estas pruebas, es posible ajustar y mejorar las configuraciones para mantener una postura de seguridad robusta.

Por último, la **educación y capacitación del personal** en la administración y configuración de *firewalls* es crucial. Capacitar a los empleados en las mejores prácticas de seguridad y fomentar la conciencia sobre la importancia de la seguridad informática ayuda a crear una cultura organizacional que prioriza la protección de la red y de los datos.

DMZ

La DMZ es una subred que funciona como una zona intermedia entre la red interna segura de una organización y redes externas no confiables. Su propósito es proporcionar una **capa adicional de seguridad,** para evitar el acceso directo de Internet a la red interna.

La idea detrás de la DMZ es que cualquier servidor expuesto a Internet es más vulnerable a los ataques. Por ello, es crucial **aislar estos servidores** para reducir el riesgo de que un ataque exitoso se propague a la red interna.

![Figura 1. Firewall. Fuente: Maldonado, 2021.](images/image-4.png)

*Figura 1. Firewall. Fuente: Maldonado, 2021.*

![Figura 2. Zona DMZ diferente de la red local. Fuente: Instituto Nacional de Ciberseguridad (INCIBE),](images/image-5.png)

*Figura 2. Zona DMZ diferente de la red local. Fuente: Instituto Nacional de Ciberseguridad (INCIBE),*

2019a.

Los servidores que se colocan en la DMZ son accesibles desde Internet (servidores públicos), pero tienen **restricciones de acceso a la red interna.** Esto incluye servidores web, servidores de correo y FTP. La configuración de la DMZ requiere un cuidadoso equilibrio entre accesibilidad y seguridad, para asegurar que solo los servicios necesarios están expuestos y adecuadamente protegidos.

![Figura 3. Zona DMZ aislada de la red local. Fuente: Instituto Nacional de Ciberseguridad (INCIBE), 2019a.](images/image-6.png)

*Figura 3. Zona DMZ aislada de la red local. Fuente: Instituto Nacional de Ciberseguridad (INCIBE), 2019a.*

Así todo, si queremos aumentar aún más la seguridad, es común utilizar un doble Firewall como se muestra en la Figura 4:

![Figura 4. Doble Firewall con una DMZ. Fuente: Instituto Nacional de Ciberseguridad (INCIBE), 2019b.](images/image-7.png)

*Figura 4. Doble Firewall con una DMZ. Fuente: Instituto Nacional de Ciberseguridad (INCIBE), 2019b.*

La DMZ ayuda a **mitigar el riesgo de ataques directos** contra los activos críticos de la red interna. Sin embargo, cualquier sistema en la DMZ sigue siendo más

Seguridad y Alta Disponibilidad 15 Tema . Material de estudio vulnerable que aquellos dentro de la red interna, por lo que requiere medidas de seguridad robustas y monitoreo constante.

#### Configuración básica de un firewall en una DMZ

Para configurar una DMZ en la red de una organización, se requiere un cortafuegos *(firewall).* Este dispositivo segmenta la red y controla las conexiones permitidas o denegadas. A continuación, se presenta una tabla básica que ilustra las conexiones recomendadas que el *firewall* permitiría o denegaría según su origen y destino:

![image-8](images/image-8.png)

Tabla 1. Reglas básicas de configuración de un *firewall* con DMZ. Fuente: elaboración propia.

#### Detalles de configuración

**▸ Segmentación de red:** utilizar el *firewall* para crear subredes separadas para la DMZ y la red interna. Esto ayuda a aislar los servidores expuestos al público de los recursos internos.

**▸ Reglas del** ***firewall:***

- Reglas de entrada: configurar reglas que permitan conexiones desde Internet solo a los servidores específicos en la DMZ.

- Reglas de salida: permitir que los servidores en la DMZ respondan a las solicitudes de Internet, pero bloquear cualquier intento de acceder a la red interna.

- Reglas internas: permitir que los usuarios de la red interna accedan a los servicios en la DMZ, como aplicaciones web o servidores de correo.

**▸ Monitoreo y registro:** configurar el *firewall* para registrar todas las conexiones permitidas y denegadas. Esto es crucial para detectar y responder a posibles intentos de intrusión.

Implementar una DMZ correctamente ayuda a minimizar los riesgos y proteger los activos internos de la organización, lo que asegura que las amenazas externas tienen menos probabilidades de afectar la red interna.

Sistemas de detección de intrusos (IDS)

U n *intrusion detection system* (IDS), o sistema de detección de intrusiones, es una herramienta esencial en la seguridad informática, ya que está diseñada para **detectar accesos no autorizados** a un ordenador o a una red. Su funcionamiento se basa en la monitorización constante del tráfico entrante y la comparación de este con una base de datos actualizada de firmas de ataque conocidas.

Los IDS pueden ser de dos tipos: **basados en red** (NIDS), los cuales monitorean el tráfico de toda la red, y **basados en** ***host*** (HIDS), que monitorean actividades específicas en un servidor o estación de trabajo.

Los IDS utilizan diversas técnicas como el análisis de patrones, la detección de anomalías y firmas para identificar actividades sospechosas o maliciosas. Es fundamental mantener actualizadas las bases de datos de firmas y adaptar los sistemas de detección a las nuevas amenazas.

Los IDS a menudo se integran con *firewalls* y otros sistemas de seguridad para proporcionar una visión más completa de la seguridad de la red y responder más eficazmente a los incidentes de seguridad.

![Figura 5. IDS. Fuente: Instituto Nacional de Ciberseguridad (INCIBE), 2020.](images/image-9.png)

*Figura 5. IDS. Fuente: Instituto Nacional de Ciberseguridad (INCIBE), 2020.*

#### Funciones principales del IDS

**▸ Monitorización del tráfico:** el IDS analiza todo el tráfico entrante y saliente en la red, así como las actividades que se realizan en los sistemas monitoreados.

**▸ Comparación con firmas de ataque:** utiliza una base de datos de firmas de ataque conocidas para identificar patrones de comportamiento sospechosos. Estas firmas son secuencias de datos o actividades que han sido previamente identificadas como maliciosas.

**▸ Generación de alertas:** cuando el IDS detecta una actividad que coincide con una firma de ataque conocida genera una alerta. Estas alertas son enviadas a los administradores del sistema para que puedan tomar las medidas adecuadas.

**▸ Detección de actividades sospechosas:** puede identificar tanto ataques esporádicos realizados por usuarios malintencionados como ataques repetidos que utilizan herramientas automáticas.

#### Limitaciones del IDS

**▸ Detecta, no previene:** los IDS son sistemas reactivos, lo que significa que su función principal es la detección de posibles intrusiones y no la mitigación de estas. No impiden los accesos no autorizados, sino que alertan a los administradores para que estos actúen en consecuencia.

**▸ Dependencia de la base de datos de firmas:** su eficacia depende en gran medida de la actualización y precisión de la base de datos de firmas de ataque. Si una firma de ataque no está registrada en la base de datos, el IDS puede no detectar el ataque.

**▸ Generación de falsos positivos:** los IDS pueden generar alertas ante actividades legítimas que se parecen a los patrones de ataque conocidos, lo que puede llevar a la generación de falsos positivos y potencialmente a la fatiga de alertas.

![Figura 6. Snort. Fuente: Davidochobits, 2020.](images/image-10.png)

*Figura 6. Snort. Fuente: Davidochobits, 2020.*

VPN

Las VPN crean un **túnel seguro entre dispositivos y redes,** lo que permite la transmisión segura de datos a través de redes públicas. Son esenciales para el trabajo remoto, el acceso seguro a los recursos de la red interna y la conexión entre sedes de una organización.

![Figura 7. VPN. Fuente: Bibhuranjan, 2020.](images/image-11.png)

*Figura 7. VPN. Fuente: Bibhuranjan, 2020.*

Las VPN pueden ser de sitio a sitio (al conectar redes enteras) o de acceso remoto (al conectar usuarios individuales a una red). La seguridad en una VPN se logra mediante el uso de **protocolos robustos de cifrado y autenticación,** lo que asegura que los datos transmitidos permanezcan privados y a salvo de interceptaciones.

Al implementar una VPN, es crucial considerar aspectos como el tipo de cifrado, la gestión de claves, la autenticación de usuarios y la configuración de la red. Además, debe haber políticas claras para el uso de las VPN, especialmente en lo que respecta al acceso remoto por parte de empleados y terceros.

#### Cómo funcionan las VPN

Las VPN funcionan creando una **conexión segura y cifrada** entre tu dispositivo y un servidor VPN a través de Internet. Este proceso involucra varias tecnologías y pasos que garantizan la seguridad y la privacidad de tu información. Aquí tienes una explicación detallada de cómo funcionan:

**▸ Encriptación:** cuando te conectas a una VPN, todo el tráfico de Internet entre tu dispositivo y el servidor VPN se cifra utilizando algoritmos de encriptación fuertes. Esto asegura que cualquier dato interceptado sea ilegible para terceros.

- Beneficio: protege tus datos sensibles, como contraseñas y números de tarjetas de crédito, de ser leídos por *hackers* y otros actores malintencionados.

**▸** ***Tunneling(túnel*** **virtual):** la VPN encapsula tu tráfico de datos en un túnel virtual. Este túnel es una conexión privada entre tu dispositivo y el servidor VPN, por lo que aísla tu tráfico de otros usuarios en la red.

- Beneficio: aumenta la seguridad al asegurar que tus datos viajan por una ruta protegida y no pueden ser fácilmente accedidos por terceros.

**▸ Cambio de dirección IP:** al conectarte a un servidor VPN, tu dirección IP original (asignada por tu proveedor de servicios de Internet) es reemplazada por una dirección IP del servidor VPN.

- Beneficio: esto oculta tu ubicación real y hace que parezca que estás navegando desde la ubicación del servidor VPN, lo que mejora tu privacidad y permite acceder a contenido restringido geográficamente.

**▸ Autenticación:** antes de establecer la conexión, la VPN utiliza protocolos de autenticación para verificar tu identidad y asegurarse de que solo los usuarios autorizados pueden conectarse.

- Beneficio: garantiza que solo tú (y otros usuarios autorizados) puedas acceder a la VPN, con lo cual mantiene la red segura.

#### Protocolos VPN más comunes

Aquí tienes una tabla comparativa de los protocolos VPN comunes, con sus características clave:

![image-12](images/image-12.png)

Tabla 2. Protocolos VPN más utilizados. Fuente: elaboración propia.

Proxys

Un *proxy* **actúa como intermediario** entre los usuarios y los recursos de Internet a los que acceden. Puede servir para diversos propósitos, como filtrar contenido, proporcionar anonimato, balancear carga y para caché de datos. En el contexto de seguridad perimetral, los *proxys* desempeñan un papel crucial en el **control** y la **monitorización del tráfico** entrante y saliente de la red.

#### Tipos de proxy

Existen varios tipos de *proxys,* cada uno con diferentes características y usos. Aquí tienes una descripción de los tipos más comunes:

**▸** ***Proxy*** **HTTP:** este tipo de *proxy* maneja específicamente el tráfico HTTP.

- Uso común: se utiliza para navegar por la web de manera anónima o para eludir restricciones de contenido.

**▸** ***Proxy*** **HTTPS:** es similar al *proxy* HTTP, pero maneja tráfico HTTPS, el cual está encriptado.

- Uso común: proporciona una capa adicional de seguridad para la navegación web.

**▸** ***Proxy*** **SOCKS:** un *proxy* de nivel inferior que puede manejar cualquier tipo de tráfico de Internet (HTTP, FTP, SMTP, etc.).

- Uso común: es usado para aplicaciones como torrents, juegos en línea y programas de correo.

**▸** ***Proxy*** **transparente:** un *proxy* que no requiere ninguna configuración por parte del usuario y no modifica las solicitudes ni las respuestas.

- Uso común: se utiliza para el monitoreo y el filtrado de contenido sin que los usuarios lo noten.

**▸** ***Proxy*** **anónimo:** oculta la dirección IP del usuario, pero puede revelar que se está utilizando un *proxy.*

- Uso común: navegación anónima en la web.

**▸** ***Proxy*** **de alta anonimidad** ***(elite proxy):*** oculta completamente el uso de un *proxy* y la dirección IP del usuario.

- Uso común: navegación web altamente segura y anónima.

**▸** ***Proxy*** **inverso:** un *proxy* que se coloca frente a uno o varios servidores web y maneja las solicitudes en nombre de estos servidores.

- Uso común: mejora la seguridad, el balanceo de carga y la aceleración de contenido.

**▸** ***Proxy*** **residencial:** utiliza direcciones IP asignadas por los proveedores de servicios de Internet (ISP) a los hogares.

- Uso común: emulación del comportamiento de un usuario real para evitar bloqueos y restricciones.

**▸** ***Proxy*** **público:** un *proxy* que está disponible públicamente para cualquier usuario.

- Uso común: navegación anónima, pero puede ser menos seguro y más lento debido a la alta demanda.

**▸** ***Proxy*** **privado:** un *proxy* exclusivo para un solo usuario o para un pequeño grupo de usuarios.

- Uso común: navegación segura y rápida con menos riesgo de sobrecarga.

Cada tipo de *proxy* tiene sus ventajas y desventajas, la elección del *proxy* adecuado depende de las necesidades específicas del usuario.

![Figura 8. Proxy. Fuente: Nishant, 2019.](images/image-13.png)

*Figura 8. Proxy. Fuente: Nishant, 2019.*

En un entorno de ASIR, los *proxys* se configuran para filtrar solicitudes de contenido no deseado o peligroso, controlar el uso de Internet y prevenir el acceso a sitios web maliciosos. Además, pueden utilizarse para implementar políticas de seguridad, como la autenticación de usuarios y la encriptación de datos.

L o s *proxys* también pueden ser utilizados para aumentar la privacidad de los usuarios al ocultar sus direcciones IP reales. Esto es particularmente útil en entornos en los que la privacidad y el anonimato son preocupaciones importantes.

Los *proxys* permiten un **registro detallado del tráfico** de red, lo que es fundamental para el análisis forense y la detección de patrones sospechosos de tráfico. Esta capacidad de monitorización ayuda en la identificación temprana de posibles amenazas y en la toma de decisiones informadas sobre la seguridad.

Aunque los *proxys* ofrecen beneficios significativos en términos de seguridad y control, también pueden ser puntos de cuello de botella y presentar **desafíos** en términos de **latencia y gestión del rendimiento.** La configuración y el mantenimiento de los *proxys* requieren un equilibrio cuidadoso entre seguridad, rendimiento y usabilidad.

## 8.3. Referencias bibliográficas

Bibhuranjan. (2020). *Protect private data over public wifi* [gráfico]. [https://technofaq.org/posts/2020/01/the-top-7-benefits-of-using-a-vpn/](https://technofaq.org/posts/2020/01/the-top-7-benefits-of-using-a-vpn/)

Davidochobits. (2020). *Logo del producto Snort* [gráfico]. [https://www.ochobitshacenunbyte.com/2020/09/29/deteccion-de-intrusos-con-snort/](https://www.ochobitshacenunbyte.com/2020/09/29/deteccion-de-intrusos-con-snort/)

Instituto Nacional de Ciberseguridad (INCIBE). (2019a). *¿Qué es una zona* *desmilitarizada?* [gráfico]. <https://www.incibe.es/empresas/blog/dmz-y-te-puedeayudar-proteger-tu-empresa>

Instituto Nacional de Ciberseguridad (INCIBE). (2019b). *Doble firewall* [gráfico]. [https://www.incibe.es/empresas/blog/dmz-y-te-puede-ayudar-proteger-tu-empresa](https://www.incibe.es/empresas/blog/dmz-y-te-puede-ayudar-proteger-tu-empresa)

Instituto Nacional de Ciberseguridad (INCIBE). (2020). *¿Qué son y para qué sirven* *los SIEM, IDS e IPS?* [gráfico]. <https://www.incibe.es/empresas/blog/son-y-sirven-lossiem-ids-e-ips>

Maldonado, D. (2021). *¿Qué es un firewall?* [gráfico]. [https://danielmaldonado.com.ar/diccionario-de-hacking/que-es-un-firewall/](https://danielmaldonado.com.ar/diccionario-de-hacking/que-es-un-firewall/)

Nishant. (2019). *Architecture of a forward vs. reverse proxy setup from client to server* *over the Internet* [gráfico]. <https://stackoverflow.com/questions/224664/whats-thedifference-between-a-proxy-server-and-a-reverse-proxy-server>

# Página web de Snort ([https://www.snort.org/](https://www.snort.org/)).

## Snort

¿Sabes lo que es un IPS? Conoce el IPS más utilizado del mercado, cómo se instala, cómo se configura, cuáles son sus prestaciones y algún ejemplo real de cómo es su funcionamiento.

## Qué son los sistemas IDS e IPS y sus diferencias

AlbertoLopez TECH TIPS. (2021, febrero 14). *[IDS e IPS] Qué son los sistemas IDS* *e IPS y sus diferencias | Cómo detectar y prevenir intrusiones* [vídeo]. YouTube.

![image-14](images/image-14.png)

Accede al vídeo: [https://www.youtube.com/embed/6-asM2Bh2yE](https://www.youtube.com/embed/6-asM2Bh2yE)

En la teoría hemos visto los IDS, pero no hemos mencionado a los IPS. Investiga el significado y las diferencias entre ambos. Investiga de qué manera podrían funcionar para detectar y corregir intrusiones en tu corporación.

## Firewall o cortafuegos: qué es y tipos de firewalls

AlbertoLopez TECH TIPS. (2020, julio 25). *[Firewall o cortafuegos] ¿Qué es? y tipos* *de firewalls, conocimientos básicos esenciales* [vídeo]. YouTube.

![image-15](images/image-15.png)

Accede al vídeo: [https://www.youtube.com/embed/kH6oP6JUnHI](https://www.youtube.com/embed/kH6oP6JUnHI)

¿Te ha quedado claro para qué sirve un cortafuegos? ¿Conoces cuántos tipos de *firewalls* existen en el mercado? Afianza los conceptos con este vídeo que lo explica muy bien.

## Servidor proxy: qué es y cuatro funciones que te

## interesan

AlbertoLopez TECH TIPS. (2020, abril 19). *[Servidor proxy] Qué es, ¡4 funciones que* *te interesan!* [video]. YouTube.

![image-16](images/image-16.png)

Accede al vídeo: [https://www.youtube.com/embed/SwxGMPUGnkM](https://www.youtube.com/embed/SwxGMPUGnkM)

Todos hemos oído mencionar sobre los servidores *proxy,* pero ¿para qué se usa un servidor *proxy?* ¿Podrías mencionar más de cuatro utilidades? Afianza los conceptos con este vídeo que lo explica muy bien.

## Qué es una VPN. Para qué sirve la VPN: cinco usos

## muy interesantes

AlbertoLopez TECH TIPS. (2020, abril 12). *Qué es una VPN. Para qué sirve la VPN |* *5 usos muy interesantes* [vídeo]. YouTube.

![image-17](images/image-17.png)

Accede al vídeo: [https://www.youtube.com/embed/2Dao6N0jWEs](https://www.youtube.com/embed/2Dao6N0jWEs)

¿Para qué podemos usar una VPN? Aquí te ofrecen cinco usos significativos que van más allá de la mera conexión con una red privada.

## ¿Qué es una DMZ? Zona desmilitarizada en redes

## informáticas

AlbertoLopez TECH TIPS. (2021, marzo 21). *[DMZ] ¿Qué es una DMZ? Zona* *desmilitarizada en redes informáticas* [vídeo]. YouTube.

![image-18](images/image-18.png)

Accede al vídeo: [https://www.youtube.com/embed/YR8xaXvGcWc](https://www.youtube.com/embed/YR8xaXvGcWc)

Por experiencia, muchos alumnos no le dan la importancia que tiene una zona desmilitarizada en una red corporativa. Afianza los conceptos con este vídeo que los explica muy bien.

VPN o *proxy:* la gran diferencia

AlbertoLopez TECH TIPS. (2020, mayo 29). *VPN o proxy: la gran diferencia* [video].

# YouTube. [https://www.youtube.com/watch?v=qikXzlcjgww](https://www.youtube.com/watch?v=qikXzlcjgww)

La VPN y el *proxy* tienen similitudes, pero no son lo mismo. Si no te ha quedado claro, aquí te explican cuáles son las diferencias entre estos dos métodos de conexión.

# en un router. Redes Zone [consultado el 14 de agosto de 2024]

## Todo sobre DMZ: para qué sirve y cómo configurarla en un router

Espinosa, O. (2024, mayo 26). Todo sobre DMZ: Para qué sirve y cómo configurarla [https://www.redeszone.net/tutoriales/configuracion-puertos/configurar-dmz-router/](https://www.redeszone.net/tutoriales/configuracion-puertos/configurar-dmz-router/)

Ahora que ya sabes para qué se usa una DMZ, imagina que quieres ofrecer un servicio público desde tu casa: ¿Quieres aprender a configurar una DMZ doméstica? Aquí te enseñamos a hacerlo.

# [consultado el 14 de agosto de 2024].

# [https://www.redeszone.net/noticias/redes/cuando-usar-vpn/](https://www.redeszone.net/noticias/redes/cuando-usar-vpn/)

## ¿Cuándo deberías usar una VPN?

Jiménez, J. (2021, septiembre 2). Cuándo deberías usar una VPN. *Redes Zone* Todos conocemos que es una VPN, pero ¿en qué casos se recomienda usar una VPN y en cuáles no? No siempre es aconsejable utilizarlo. Averígualo.

Qué es un *proxy,* cómo funciona y cómo configurarlo

Jiménez, J. (2024, marzo 6). Qué es un Proxy, cómo funciona y cómo configurarlo. *Redes Zone* [actualizado el 17 de julio, 2024]. [https://www.redeszone.net/tutoriales/redes-cable/que-es-servidor-proxy-configurar/](https://www.redeszone.net/tutoriales/redes-cable/que-es-servidor-proxy-configurar/)

*Proxy,* el gran olvidado. Aprende más sobre los *proxys,* para qué sirven, qué utilidades presentan y cómo los podemos configurar. Una vez hayas leído este artículo te plantearás cuál es la utilidad de usar un *proxy* en tu corporación.

## Entrenamiento 1: proxy Squid

**▸ Planteamiento del ejercicio** Instalar y probar un proxy, documentar la instalación, la configuración y el uso de este. Se recomienda utilizar la aplicación Squid en Ubuntu 20.04 o 22.04.

**▸ Desarrollo paso a paso**

- Instalar el servidor y establecer un sistema de control de accesos (ACL con usuarios y contraseñas). El objetivo es que únicamente el usuario deseado pueda navegar por Internet.

- Configurar un navegador para que se conecte a través del proxy.

- Comprobar el correcto funcionamiento de la lista de accesos (autenticación del usuario).

- Comprobar el correcto enrutamiento a través del proxy (utilizar alguna página web como What Is My Proxy [[http://www.whatismyproxy.com/](http://www.whatismyproxy.com/)]).

- Añadir ACL para restringir el tráfico a dos páginas web (MARCA y SPORT). Intentar entrar a esas páginas y comentar el resultado.

- Verificar el funcionamiento del archivo de registro de accesos (log).

**▸ Solución** Para instalar y configurar Squid como *proxy* en Ubuntu 20.04 o 22.04 y realizar las pruebas solicitadas, sigue estos pasos detallados: **Paso 1:** instalación de Squid.

## 1. Actualizar el sistema:

![Figura 9. Actualizar el sistema. Fuente: elaboración propia.](images/image-19.png)

*Figura 9. Actualizar el sistema. Fuente: elaboración propia.*

## 2. Instalar Squid:

![Figura 10. Instalar Squid. Fuente: elaboración propia.](images/image-20.png)

*Figura 10. Instalar Squid. Fuente: elaboración propia.*

**Paso 2:** configuración del servidor Squid.

1. Configurar control de acceso (ACL) con autenticación básica.

Editar el archivo de configuración de Squid:

![Figura 11. Editar el archivo de configuración. Fuente: elaboración propia.](images/image-21.png)

*Figura 11. Editar el archivo de configuración. Fuente: elaboración propia.*

Agregar o modificar las siguientes líneas al final del archivo:

![Figura 12. Agregar o modificar estas líneas. Fuente: elaboración propia.](images/image-22.png)

*Figura 12. Agregar o modificar estas líneas. Fuente: elaboración propia.*

Donde:

**▸** acl allowed_user proxy_auth REQUIRED : esta línea define una ACL llamada «allowed_user». Esta ACL utiliza «proxy_auth REQUIRED», lo que significa que, para que un usuario tenga acceso permitido, debe autenticarse mediante una autenticación básica (usando un nombre de usuario y contraseña). Este usuario específico estará en el archivo de contraseñas especificado en la configuración de autenticación.

**▸** http_access allow allowed_user : esta línea le permite el acceso a través del *proxy* Squid solo a aquellos usuarios que cumplen con la condición establecida en la ACL «allowed_user». En otras palabras, solo los usuarios autenticados correctamente podrán utilizar el *proxy.*

**▸** auth_param basic program /usr/lib/squid/basic_ncsa_auth /etc/squid/passwd : esta línea

especifica el programa que Squid utilizará para realizar la autenticación básica. En este caso, se utiliza «basic_ncsa_auth», que es un módulo de autenticación básica de Squid, y el archivo «/etc/squid/passwd» contiene las credenciales de los usuarios.

**▸** auth_param basic children 5 : define cuántos procesos hijos *(children)* del módulo de autenticación se pueden iniciar simultáneamente para manejar las solicitudes de autenticación. Un número mayor puede aumentar la capacidad de manejar múltiples solicitudes de autenticación simultáneamente.

**▸** auth_param basic realm Proxy Authentication Required : define el mensaje que se le

mostrará al usuario cuando se le solicite la autenticación. En este caso, indica que se requiere una autenticación para acceder al *proxy.*

**▸** auth_param basic credentialsttl 2 hours : especifica por cuánto tiempo (en este caso, dos horas) deben mantenerse válidas las credenciales de autenticación antes de que el usuario deba volver a autenticarse. Esto es útil para mejorar la seguridad al limitar el tiempo durante el cual una credencial es válida.

**▸** acl users proxy_auth REQUIRED : define otra ACL llamada «users» que utiliza «proxy_auth REQUIRED». Esto significa que todos los usuarios que se autentiquen correctamente (los que están presentes en el archivo de contraseñas y proporcionan credenciales válidas) estarán en esta lista de usuarios autorizados.

**▸** http_access allow users : esta línea le permite el acceso a través del proxy Squid a todos los usuarios que estén presentes en la ACL «users», es decir, todos los usuarios que se autentiquen correctamente según las reglas definidas anteriormente.

Guarda y cierra el archivo («Ctrl + X», luego «Y» y «Enter»).

## 2. Crear un usuario y contraseña para el acceso:

Utiliza el comando «htpasswd» para crear un archivo de contraseñas y agregar un usuario.

![Figura 13. Crear un usuario y contraseña. Fuente: elaboración propia.](images/image-23.png)

*Figura 13. Crear un usuario y contraseña. Fuente: elaboración propia.*

Sustituye «username» con el nombre de usuario que desees y añade la contraseña que quieras.

## 3. Reiniciar Squid:

![Figura 14. Reiniciar Squid. Fuente: elaboración propia.](images/image-24.png)

*Figura 14. Reiniciar Squid. Fuente: elaboración propia.*

**Paso 3:** configuración del navegador.

## 1. Configurar el navegador para usar el proxy:

**▸** Abre las configuraciones del navegador.

**▸** Busca la sección de configuración de *proxy* o red.

**▸** Configura el *proxy* con la dirección IP del servidor Squid y el puerto por defecto (3128). **Paso 4:** pruebas de funcionamiento.

## 1. Comprobar acceso restringido a páginas web:

Modifica el archivo de configuración de Squid para añadir las ACL necesarias para

restringir el acceso a las páginas web específicas.

![Figura 15. Acceso restringido a páginas web. Fuente: elaboración propia.](images/image-25.png)

*Figura 15. Acceso restringido a páginas web. Fuente: elaboración propia.*

Guarda y cierra el archivo de configuración, luego reinicia Squid.

## 2. Verificar funcionamiento del log de acceso:

Squid registra los accesos en el archivo «/var/log/squid/access.log». Puedes revisar

este archivo para verificar que las restricciones y los accesos se están registrando correctamente.

**Paso 5:** verificación del funcionamiento del *proxy.*

## 1. Comprueba el funcionamiento del proxy:

**▸** Navega a una página como la de What Is My Proxy (<http://www.whatismyproxy.com/>) desde el navegador configurado para usar el *proxy.*

**▸** Deberías ver la IP y otros detalles del *proxy* en esa página.

Conclusiones

Al seguir estos pasos, habrás instalado Squid

como *proxy* en Ubuntu, habrás

configurado acceso restringido por usuario y por páginas web, además de haber verificado el funcionamiento del registro de accesos y realizado pruebas para asegurar que el *proxy* está funcionando correctamente. Asegúrate de ajustar las configuraciones según tus necesidades específicas y las políticas de seguridad.

## Entrenamiento 2: firewall de Windows

**▸ Planteamiento del ejercicio** La siguiente práctica consiste en configurar el *firewall* de Windows para conseguir los siguientes objetivos:

**▸** Bloquear todas las comunicaciones salientes de los protocolos HTTP y HTTPS.

**▸** Bloquear todas las comunicaciones de uno de los navegadores que tengas instalado. Crea las reglas que necesites y comprueba que se cumplen.

**▸ Desarrollo paso a paso** **Objetivo 1:** bloquear todas las comunicaciones salientes de los protocolos HTTP y HTTPS.

**▸** Abrir el *firewall* de Windows.

**▸** Crear una nueva regla de salida para HTTP y HTTPS. **Objetivo 2:** bloquear todas las comunicaciones de uno de los navegadores que tengas instalado.

**▸** Crear una regla para bloquear el navegador específico.

**▸ Solución**

**Objetivo 1:** bloquear todas las comunicaciones salientes de los protocolos HTTP y

HTTPS.

**Paso 1:** abrir el *firewall* de Windows.

## 1. Accede al firewall de Windows:

**▸** Ve al panel de control. Puedes hacer esto buscando «Panel de Control» en el menú de inicio de Windows.

**▸** En el panel de control, selecciona «Sistema y Seguridad» y luego «Firewall de Windows».

## 2. Accede a las reglas de salida:

**▸** En la ventana del firewall de Windows, haz clic en «Configuración avanzada» en el panel izquierdo.

**Paso 2:** crear una regla de salida para HTTP.

## 1. Crear la regla para HTTP:

**▸** En el panel izquierdo, haz clic en «Reglas de salida».

**▸** En el panel derecho, haz clic en «Nueva regla...».

## 2. Seleccionar tipo de regla:

**▸** En el asistente para la nueva regla de salida, selecciona «Programa» y luego haz

clic en «Siguiente».

## 3. Elegir el programa:

**▸** Selecciona el programa de tu navegador (por ejemplo, chrome.exe para Google Chrome) haciendo clic en «Examinar...». Normalmente se encuentra en la carpeta de instalación del navegador en «C:\Program Files\» o «C:\Program Files (x86)\».

## 4. Especificar la acción de bloqueo:

**▸** En la siguiente pantalla, elige «Bloquear la conexión» y haz clic en «Siguiente».

## 5. Configurar perfiles y nombre de la regla:

**▸** Deja seleccionados los perfiles predeterminados (dominio, privado, público) y da clic en «Siguiente». **▸** Asígnale un nombre descriptivo a la regla, por ejemplo, «Bloquear HTTP», y opcionalmente una descripción. **▸** Haz clic en «Finalizar» para completar la creación de la regla. **Paso 3:** crear una regla de salida para HTTPS.

## 1. Crear la regla para HTTPS:

**▸** Repite los pasos anteriores para crear una nueva regla de salida, pero esta vez selecciona HTTPS en lugar de HTTP.

Comprobación para el objetivo 1: **▸** Intenta acceder a un sitio web usando HTTP y HTTPS desde cualquier navegador configurado en estas reglas. Deberías recibir un mensaje de error que indique que la conexión está bloqueada por el *firewall.*

**Objetivo 2:** bloquear todas las comunicaciones de uno de los navegadores que tengas instalado.

**Paso 1:** crear una regla para bloquear un navegador específico.

## 1. Crear la regla para bloquear el navegador:

**▸** En el *firewall* de Windows, ve a «Reglas de salida». **▸** Haz clic en «Nueva regla...» y selecciona «Programa».

## 2. Seleccionar el programa del navegador:

**▸** Busca y selecciona el ejecutable del navegador que deseas bloquear (por ejemplo, chrome.exe para Google Chrome).

## 3. Configurar la acción de bloqueo:

**▸** En la siguiente pantalla, elige «Bloquear la conexión» y continúa con los pasos del asistente.

## 4. Finalizar la creación de la regla:

**▸** Asígnale un nombre descriptivo a la regla, como «Bloquear Chrome», y completa el asistente.

Comprobación para el objetivo 2:

**▸** Intenta usar el navegador bloqueado para acceder a cualquier sitio web. Deberías recibir un mensaje de error que indique que la conexión está bloqueada por el *firewall.*

Consideraciones adicionales:

**▸ Restauración y eliminación de reglas:** si necesitas deshacer alguna configuración, puedes eliminar las reglas creadas o desactivarlas temporalmente desde el panel de control del *firewall* de Windows.

**▸ Seguridad y permisos:** asegúrate de tener los permisos adecuados en tu cuenta de usuario para realizar cambios en el *firewall* de Windows, ya que las configuraciones incorrectas pueden afectar el funcionamiento de tus aplicaciones y servicios.

Al seguir estos pasos detallados, deberías poder configurar el *firewall* de Windows según tus requerimientos específicos para bloquear las comunicaciones salientes de HTTP y HTTPS, así como de un navegador particular.

## Entrenamiento 3: firewall en Ubuntu

**▸ Planteamiento del ejercicio** Vas a aprender a configurar y gestionar el *firewall* en un sistema operativo Ubuntu utilizando Uncomplicated Firewall (UFW). Para ello se debe permitir únicamente las conexiones entrantes SSH, HTTP y HTTPS. Investiga cómo serían las reglas (avanzadas) para permitir las conexiones desde una red de equipos, denegar la entrada a una IP específica, permitir las conexiones a un puerto específico de una IP específica, eliminar alguna regla… Como caso práctico deberás permitirle su tráfico a una aplicación que escucha por el puerto 8080. Material necesario:

**▸** Una computadora con Ubuntu instalado (versión 18.04 o superior recomendada).

**▸ Desarrollo paso a paso**

**Parte 1:** instalación y verificación de UFW.

**Parte 2:** configuración básica de UFW.

**Parte 3:** reglas avanzadas de UFW.

**Parte 4:** verificación y mantenimiento.

**Parte 5:** ejercicio práctico.

**▸ Solución** **Parte 1:** instalación y verificación de UFW.

1. Abrir la terminal: inicia una terminal en tu sistema Ubuntu.

## 2. Verificar si UFW está instalado:

![Figura 16. Verificar si UFW está instalado. Fuente: elaboración propia.](images/image-26.png)

*Figura 16. Verificar si UFW está instalado. Fuente: elaboración propia.*

**▸** Si UFW no está instalado, instálalo con el siguiente comando:

![Figura 17. Comando para instalar UFW. Fuente: elaboración propia.](images/image-27.png)

*Figura 17. Comando para instalar UFW. Fuente: elaboración propia.*

## 3. Habilitar UFW:

![Figura 18. Habilitar UFW. Fuente: elaboración propia.](images/image-28.png)

*Figura 18. Habilitar UFW. Fuente: elaboración propia.*

## 4. Verificar el estado de UFW:

![Figura 19. Verificar el estado de UFW. Fuente: elaboración propia.](images/image-29.png)

*Figura 19. Verificar el estado de UFW. Fuente: elaboración propia.*

Debería mostrar «Status: active». **Parte 2:** configuración básica de UFW.

## 1. Permitir conexiones SSH:

- ▸ Para asegurarte de no perder el acceso remoto:

![Figura 20. Permitir conexiones SSH. Fuente: elaboración propia.](images/image-30.png)

*Figura 20. Permitir conexiones SSH. Fuente: elaboración propia.*

- ▸ Alternativamente, puedes usar el puerto específico:

![Figura 21. Permitir conexiones SSH. Fuente: elaboración propia.](images/image-31.png)

*Figura 21. Permitir conexiones SSH. Fuente: elaboración propia.*

## 2. Permitir conexiones HTTP y HTTPS:

Para permitir tráfico web:

![Figura 22. Permitir el tráfico web. Fuente: elaboración propia.](images/image-32.png)

*Figura 22. Permitir el tráfico web. Fuente: elaboración propia.*

## 3. Denegar todas las conexiones entrantes por defecto:

- ▸ Esta regla es crucial para la seguridad:

    - Seguridad y Alta Disponibilidad 48

        - Tema . Entrenamientos

![Figura 23. Denegar las conexiones entrantes por defecto. Fuente: elaboración propia.](images/image-33.png)

*Figura 23. Denegar las conexiones entrantes por defecto. Fuente: elaboración propia.*

## 4. Permitir todas las conexiones salientes por defecto:

**▸** Esta regla asegura que todas las conexiones salientes sean permitidas:

![Figura 24. Permitir las conexiones salientes por defecto. Fuente: elaboración propia.](images/image-34.png)

*Figura 24. Permitir las conexiones salientes por defecto. Fuente: elaboración propia.*

## 5. Reiniciar UFW para aplicar los cambios:

![Figura 25. Reiniciar UFW. Fuente: elaboración propia.](images/image-35.png)

*Figura 25. Reiniciar UFW. Fuente: elaboración propia.*

**Parte 3:** reglas avanzadas de UFW.

## 1. Permitir conexiones de un rango de IP específico:

- ▸ Por ejemplo, para permitir conexiones desde la red 192.168.1.0/24:

![Figura 26. Permitir conexiones desde una IP específica. Fuente: elaboración propia.](images/image-36.png)

*Figura 26. Permitir conexiones desde una IP específica. Fuente: elaboración propia.*

    - Seguridad y Alta Disponibilidad 49

        - Tema . Entrenamientos

## 2. Denegar conexiones de una IP específica:

**▸** Por ejemplo, para bloquear la IP 203.0.113.5:

![Figura 27. Denegar conexiones desde una IP específica. Fuente: elaboración propia.](images/image-37.png)

*Figura 27. Denegar conexiones desde una IP específica. Fuente: elaboración propia.*

3. Permitir conexiones a un puerto específico desde una IP específica:

**▸** Por ejemplo, permitirle a la IP 192.168.1.10 acceder al puerto 3306:

![Figura 28. Permitir conexiones a un puerto específico. Fuente: elaboración propia.](images/image-38.png)

*Figura 28. Permitir conexiones a un puerto específico. Fuente: elaboración propia.*

## 4. Eliminar una regla:

- ▸ Primero, lista las reglas con números:

![Figura 29. Listar las reglas con números. Fuente: elaboración propia.](images/image-39.png)

*Figura 29. Listar las reglas con números. Fuente: elaboración propia.*

    - Seguridad y Alta Disponibilidad 50

        - Tema . Entrenamientos

![Figura 30. Ejemplo de resultado. Fuente: elaboración propia. Por ejemplo, este podría ser el resultado:](images/image-40.png)

*Figura 30. Ejemplo de resultado. Fuente: elaboración propia.*

**▸** Luego, elimina la regla específica:

![Figura 31. Eliminar la regla específica. Fuente: elaboración propia.](images/image-41.png)

*Figura 31. Eliminar la regla específica. Fuente: elaboración propia.*

**Parte 4:** verificación y mantenimiento.

## 1. Verificar el estado y las reglas actuales:

![Figura 32. Verificar el estado y las reglas actuales. Fuente: elaboración propia.](images/image-42.png)

*Figura 32. Verificar el estado y las reglas actuales. Fuente: elaboración propia.*

- Seguridad y Alta Disponibilidad 51

    - Tema . Entrenamientos

## 2. Deshabilitar UFW (si es necesario):

![Figura 33. Deshabilitar UFW. Fuente: elaboración propia.](images/image-43.png)

*Figura 33. Deshabilitar UFW. Fuente: elaboración propia.*

## 3. Habilitar UFW nuevamente:

![Figura 34. Habilitar UFW. Fuente: elaboración propia.](images/image-44.png)

*Figura 34. Habilitar UFW. Fuente: elaboración propia.*

**Parte 5:** ejercicio práctico.

## 1. Configurar UFW para una aplicación personalizada:

- ▸ Imagina que has instalado una aplicación que escucha en el puerto 8080.

- ▸ Permitir el tráfico hacia este puerto:

![Figura 35. Permitir el tráfico hacia el puerto 8080. Fuente: elaboración propia.](images/image-45.png)

*Figura 35. Permitir el tráfico hacia el puerto 8080. Fuente: elaboración propia.*

## 2. Verificar que la aplicación funciona:

- ▸ Inicia la aplicación y prueba el acceso desde otra máquina o navegador.

    - Seguridad y Alta Disponibilidad 52

        - Tema . Entrenamientos

## 3. Registrar un log de actividad:

- ▸ Habilitar el registro de eventos:

![Figura 36. Habilitar el registro de eventos. Fuente: elaboración propia.](images/image-46.png)

*Figura 36. Habilitar el registro de eventos. Fuente: elaboración propia.*

- ▸ Visualizar los logs:

![Figura 37. Visualizar los logs. Fuente: elaboración propia.](images/image-47.png)

*Figura 37. Visualizar los logs. Fuente: elaboración propia.*

    - Seguridad y Alta Disponibilidad 53

        - Tema . Entrenamientos

## Entrenamiento 4: configuración de una VPN site-

## to-site en Cisco Packet Tracer

**▸ Planteamiento del ejercicio** Configurar una VPN *site-to-site* entre dos sucursales utilizando *routers* en Cisco Packet Tracer para asegurar la comunicación privada a través de una red pública. Situación Una empresa tiene dos sucursales, Sucursal A y Sucursal B, que necesitan comunicarse de manera segura a través de una red pública. Tu tarea es configurar una VPN *site-to-site* entre los *routers* de ambas sucursales utilizando Cisco Packet

Tracer.

Topología de red

Sucursal A

- Router A:

**▸** Interfaz hacia la red pública: «200.1.1.1/24».

**▸** Interfaz LAN: «192.168.1.1/24». PC A: «192.168.1.2/24». Sucursal B

- Router B:

**▸** Interfaz hacia la red pública: «200.1.1.2/24».

**▸** Interfaz LAN: «192.168.2.1/24».

- PC B: «192.168.2.2/24».

**▸ Desarrollo paso a paso**

## 1. Configurar la topología en Cisco Packet Tracer.

## 2. Asignar direcciones IP.

## 3. Configurar el túnel VPN.

## 4. Probar la conexión VPN.

**▸ Solución**

## 1. Configurar la topología en Cisco Packet Tracer:

**▸** Añadir dos *routers,* dos *switches* y dos PC a la topología.

**▸** Conectar cada PC a su respectivo *switch* y los *switches* a sus respectivos *routers.*

**▸** Conectar las interfaces de los *routers* hacia la red pública.

## 2. Asignar direcciones IP

Configurar las direcciones IP en los *routers* y PC según la configuración proporcionada.

**▸** *Router* A:

![Figura 38. Router A. Fuente: elaboración propia.](images/image-48.png)

*Figura 38. Router A. Fuente: elaboración propia.*

![Figura 39. Router B. Fuente: elaboración propia. ▸ Router B:](images/image-49.png)

*Figura 39. Router B. Fuente: elaboración propia.*

**▸** PC A:

![Figura 40. PC A. Fuente: elaboración propia.](images/image-50.png)

*Figura 40. PC A. Fuente: elaboración propia.*

**▸** PC B:

![Figura 41. PC B. Fuente: elaboración propia.](images/image-51.png)

*Figura 41. PC B. Fuente: elaboración propia.*

## 3. Configurar el túnel VPN.

**▸** En los *router* A y B, configurar las políticas ISAKMP y los *transform sets* necesarios. **▸** Configurar el mapa de criptografía *(crypto map)* y aplicarlo a la interfaz hacia la red pública. **▸** Crear listas de acceso (ACL) para definir el tráfico que debe ser protegido por la VPN. *Router* A:

Seguridad y Alta Disponibilidad 57 Tema . Entrenamientos crypto isakmp policy 10 : define una nueva política ISAKMP con la prioridad 10. Las políticas con números más bajos tienen mayor prioridad. encryption aes : utiliza el algoritmo de cifrado *advanced encryption standard* (AES) para proteger los datos durante la negociación inicial del túnel VPN. hash sha : utiliza el algoritmo de *hashing secure hash algorithm* (SHA) para garantizar la integridad de los datos durante la negociación. authentication pre-share : indica que se usará una clave precompartida *(pre-shared key)*

Seguridad y Alta Disponibilidad 58 Tema . Entrenamientos para autenticar los dispositivos. group 2 : selecciona el grupo de Diffie-Hellman 2, que utiliza un tamaño de clave de 1024 bits. Este grupo define cómo se generarán y compartirán las claves durante la fase 1 de la negociación. lifetime 86400 : establece la duración de la política en 86400 segundos (24 horas). Después de este tiempo, la fase 1 de la negociación deberá renegociarse para mantener el túnel VPN seguro.

![Figura 42. Router A. Fuente: elaboración propia.](images/image-52.png)

*Figura 42. Router A. Fuente: elaboración propia.*

crypto isakmp key cisco123 address 200.1.1.2 :

**▸** crypto isakmp key : establece una clave ISAKMP.

**▸** cisco123 : es la clave precompartida que se usará para la autenticación.

**▸** address 200.1.1.2 : especifica la dirección IP del par remoto (en este caso, la dirección IP pública del *router* de la Sucursal B).

crypto ipsec transform-set MY_TRANSFORM_SET esp-aes esp-sha-hmac :

**▸** crypto ipsec transform-set : define un conjunto de transformación IPsec.

**▸** MY_TRANSFORM_SET : es el nombre asignado al conjunto de transformación.

**▸** esp-aes : especifica que se utilizará el protocolo *encapsulating security payload* (ESP) con cifrado AES.

**▸** esp-sha-hmac : indica que se utilizará *hash-based message authentication code* (HMAC) con SHA para la autenticación e integridad de los datos.

crypto map MY_CRYPTO_MAP 10 ipsec-isakmp :

**▸** crypto map MY_CRYPTO_MAP : define o selecciona un mapa de criptografía llamado «MY_CRYPTO_MAP».

**▸** 10 : asigna una secuencia de prioridad 10 a esta entrada en el mapa de criptografía.

**▸** ipsec-isakmp : especifica que este mapa de criptografía utilizará IPsec e ISAKMP para la negociación. set peer 200.1.1.2 : establece la dirección IP del par remoto como «200.1.1.2» (la dirección del *router* de la otra sucursal). set transform-set MY_TRANSFORM_SET : asigna el conjunto de transformación «MY_TRANSFORM_SET» (definido anteriormente) a esta entrada en el mapa de criptografía. Este conjunto especifica cómo se cifrarán y se autenticarán los datos. match address 100 : indica que se usará la ACL número «100» para identificar el tráfico que debe ser cifrado y protegido por IPsec. *Router* B:

![Figura 43. Router B. Fuente: elaboración propia.](images/image-53.png)

*Figura 43. Router B. Fuente: elaboración propia.*

En el *router* B se hace la misma configuración para garantizar la bidireccionalidad.

## 4. Probar la conexión VPN:

**▸** Desde la PC A, realizar un *ping* a PC B («192.168.2.2») para verificar la conectividad a través de la VPN. Evaluación:

**▸** La VPN se considera configurada correctamente si el *ping* desde la PC A a la PC B es exitoso.

**▸** Verifica que las configuraciones de criptografía y las políticas de seguridad estén correctamente aplicadas en ambos *routers.*

## Entrenamiento 5: implementación de DMZ con

## Packet Tracer

**▸ Planteamiento del ejercicio**

En esta actividad, implementaremos una DMZ utilizando Cisco Packet Tracer. La DMZ permitirá que ciertos servicios sean accesibles desde la red externa, mientras se mantiene la seguridad de la red interna.

Comenzaremos creando un escenario de red con un *router,* dos *switches,* tres PC y un servidor. Conectaremos los dispositivos de manera que el *router* esté vinculado a los *switches,* las PC se conecten a los *switches* según corresponda y que el servidor esté en la DMZ. Configuraremos las direcciones IP adecuadas para cada dispositivo y les asignaremos las interfaces del *router* a las redes correspondientes: interna, DMZ y externa.

Posteriormente, configuraremos el *router* para realizar NAT y estableceremos reglas de *firewall* que permitirán el acceso a los servicios en la DMZ desde la red externa, mientras restringen el acceso desde la red interna. Para finalizar, verificaremos la configuración mediante pruebas de conexión desde las distintas redes y revisaremos las traducciones NAT y las reglas de acceso en el *router.* Esta implementación equilibrará la accesibilidad y la seguridad, lo que protegerá la red interna al tiempo que permitirá el acceso controlado a los servicios desde el exterior.

**▸ Desarrollo paso a paso**

**Paso 1:** crear el escenario de red.

**Paso 2:** conectar los dispositivos.

**Paso 3:** configurar direcciones IP.

**Paso 4:** configurar el acceso a la DMZ

**Paso 5:** verificación y pruebas.

**▸ Solución**

**Paso 1:** crear el escenario de red.

## 1. Abrir Cisco Packet Tracer.

## 2. Agregar dispositivos:

**▸** Un *router* (por ejemplo, Cisco 1941).

**▸** Dos *switches* (por ejemplo, Cisco 2960).

**▸** 3 PC (PC1 para la red interna, PC2 para la DMZ y PC3 para la red externa).

**▸** Un servidor (para la DMZ).

**Paso 2:** conectar los dispositivos.

## 1. Conectar el router a los switches:

**▸** Conectar el puerto GigabitEthernet0/0 del *router* al *switch* 1 (red interna).

**▸** Conectar el puerto GigabitEthernet0/1 del *router* al *switch* 2 (DMZ).

## 2. Conectar los PC y el servidor a los switches:

**▸** Conectar la PC1 al *switch* 1.

**▸** Conectar la PC2 y el servidor al *switch* 2.

**▸** Conectar la PC3 directamente al *router* en un puerto adicional (simulando la red externa). Para hacer esta parte, necesitaremos ampliar el número de puertos de red del *router* pues han sido ocupados con los dos *switches.* Para ello, apagaremos el *router* y en la pestaña *physical* añadiremos un módulo expansión, como puede ser el HWIC-4ESW.

![Figura 44. Conectar los PC y el servidor a los switches. Fuente: elaboración propia.](images/image-54.png)

*Figura 44. Conectar los PC y el servidor a los switches. Fuente: elaboración propia.*

**Paso 3:** configurar direcciones IP.

## 1. Configurar el router:

- ▸ Entrar en el modo de configuración global.

- ▸ Asignar direcciones IP a las interfaces.

    - Seguridad y Alta Disponibilidad 65

        - Tema . Entrenamientos

![Figura 45. Configurar el router. Fuente: elaboración propia.](images/image-55.png)

*Figura 45. Configurar el router. Fuente: elaboración propia.*

## 2. Configurar la PC1 (red interna):

- ▸ Dirección IP: 192.168.1.2.

- ▸ Máscara de subred: 255.255.255.0.

- ▸ Puerta de enlace: 192.168.1.1.

## 3. Configurar la PC2 y el servidor (DMZ):

- ▸ Dirección IP de la PC2: 192.168.2.2.

- ▸ Dirección IP del servidor: 192.168.2.3.

- ▸ Máscara de subred: 255.255.255.0.

- ▸ Puerta de enlace: 192.168.2.1.

    - Seguridad y Alta Disponibilidad 66

        - Tema . Entrenamientos

## 4. Configurar la PC3 (red externa):

**▸** Dirección IP: 203.0.113.2.

**▸** Máscara de subred: 255.255.255.0.

**▸** Puerta de enlace: 203.0.113.1.

**Paso 4:** configurar el acceso a la DMZ.

## 1. Configurar NAT y las reglas de firewall en el router:

![Figura 46. Configurar NAT y las reglas de firewall. Fuente: elaboración propia.](images/image-56.png)

*Figura 46. Configurar NAT y las reglas de firewall. Fuente: elaboración propia.*

Donde:

**▸** access-list 100 permit ip 192.168.1.0 0.0.0.255 any : crea una lista de acceso (ACL)

numerada que permite el tráfico IP desde la red 192.168.1.0/24 hacia cualquier destino.

**▸** access-list 100 permit ip 192.168.2.0 0.0.0.255 any : crea una lista de acceso (ACL)

numerada que permite el tráfico IP desde la red 192.168.2.0/24 hacia cualquier destino.

**▸** ip nat outside : este comando configura la interfaz gigabitEthernet 0/2 como la interfaz «exterior» para NAT. En otras palabras, esta interfaz está conectada a la red externa (por ejemplo, Internet).

**▸** interface gigabitEthernet 0/0 seguido de ip nat inside : configura la interfaz gigabitEthernet

0/0 del *router* como una interfaz interna para NAT (lo mismo para la interfaz

gigabitEthernet 0/1 )

**▸** ip nat inside source list 100 interface gigabitEthernet 0/2 overload : permite que múltiples

dispositivos en la red interna compartan una sola dirección IP pública cuando se comunican con redes externas, como Internet.

## 2. Configurar el acceso a los servicios en la DMZ:

Para permitir el acceso a un servidor web en la DMZ:

![Figura 47. Configurar el acceso a los servicios en la DMZ. Fuente: elaboración propia.](images/image-57.png)

*Figura 47. Configurar el acceso a los servicios en la DMZ. Fuente: elaboración propia.*

Donde:

**▸** access-list 101 permit tcp any host 192.168.2.3 eq 80 : esta regla permite el tráfico TCP

desde cualquier origen hacia el host 192.168.2.3 cuando el tráfico está destinado al puerto 80 (HTTP).

**▸** interface gigabitEthernet 0/2 : esta línea indica que las configuraciones que sigan se aplicarán a la interfaz física GigabitEthernet 0/2.

**▸** ip access-group 101 in : este comando asegura que todo el tráfico entrante en la interfaz GigabitEthernet 0/2 será evaluado por las reglas en la ACL 101. Solo el tráfico que cumpla con las reglas de la ACL será permitido, mientras que el tráfico que no cumpla será denegado.

Este conjunto de comandos configura una lista de acceso (ACL) y aplica esta ACL a la interfaz gigabitEthernet 0/2 en un *router* Cisco. La función de estos comandos es permitir el tráfico TCP hacia el puerto 80 (HTTP) dirigido a la dirección IP específica

192.168.2.3 .

**Paso 5:** verificación y pruebas.

## 1. Probar conexiones:

**▸** Desde la PC3 (red externa), intenta acceder al servidor web en la DMZ (<http://192.168.2.3>).

**▸** Desde la PC1 (red interna), verifica que tienes acceso al servidor en la DMZ.

## 2. Comprobar NAT y firewall:

**▸** Usa el comando «show ip nat translations» en el *router* para verificar las traducciones NAT. Tendríamos algo similar a esto:

![Figura 48. Verificar NAT. Fuente: elaboración propia.](images/image-58.png)

*Figura 48. Verificar NAT. Fuente: elaboración propia.*

**▸** Usa el comando «show access-lists» para verificar que las reglas de acceso están aplicadas correctamente.

Siguiendo estos pasos, habrás implementado una configuración básica de una DMZ en Cisco Packet Tracer, con lo que protegerás tu red interna mientras permites el acceso a ciertos servicios desde la red externa.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–26)*
- A fondo  *(pp.27–35)*
- Entrenamientos  *(pp.36–70)*
- Seguridad y Alta Disponibilidad 5 Tema . Material de estudio · Seguridad y Alta Disponibilidad 6 Tema . Material de estudio · Seguridad y Alta Disponibilidad 7 Tema . Material de estudio · Seguridad y Alta Disponibilidad 8 Tema . Material de estudio · Seguridad y Alta Disponibilidad 9 Tema . Material de estudio · Seguridad y Alta Disponibilidad 10 Tema . Material de estudio · Seguridad y Alta Disponibilidad 11 Tema . Material de estudio · Seguridad y Alta Disponibilidad 12 Tema . Material de estudio · Seguridad y Alta Disponibilidad 13 Tema . Material de estudio · Seguridad y Alta Disponibilidad 14 Tema . Material de estudio · Seguridad y Alta Disponibilidad 16 Tema . Material de estudio · Seguridad y Alta Disponibilidad 17 Tema . Material de estudio · Seguridad y Alta Disponibilidad 18 Tema . Material de estudio · Seguridad y Alta Disponibilidad 19 Tema . Material de estudio · Seguridad y Alta Disponibilidad 20 Tema . Material de estudio · Seguridad y Alta Disponibilidad 21 Tema . Material de estudio · Seguridad y Alta Disponibilidad 22 Tema . Material de estudio · Seguridad y Alta Disponibilidad 23 Tema . Material de estudio · Seguridad y Alta Disponibilidad 24 Tema . Material de estudio · Seguridad y Alta Disponibilidad 25 Tema . Material de estudio · Seguridad y Alta Disponibilidad 26 Tema . Material de estudio  *(pp.5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26)*
- Seguridad y Alta Disponibilidad 27 Tema . A fondo · Seguridad y Alta Disponibilidad 28 Tema . A fondo · Seguridad y Alta Disponibilidad 29 Tema . A fondo · Seguridad y Alta Disponibilidad 30 Tema . A fondo · Seguridad y Alta Disponibilidad 31 Tema . A fondo · Seguridad y Alta Disponibilidad 32 Tema . A fondo · Seguridad y Alta Disponibilidad 33 Tema . A fondo · Seguridad y Alta Disponibilidad 34 Tema . A fondo · Seguridad y Alta Disponibilidad 35 Tema . A fondo  *(pp.27–35)*
- Seguridad y Alta Disponibilidad 36 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 37 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 38 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 39 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 40 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 41 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 42 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 43 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 44 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 45 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 46 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 47 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 54 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 55 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 56 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 59 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 60 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 61 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 62 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 63 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 64 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 67 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 68 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 69 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 70 Tema . Entrenamientos  *(pp.36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 54, 55, 56, 59, 60, 61, 62, 63, 64, 67, 68, 69, 70)*