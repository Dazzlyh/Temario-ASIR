## Tema 7

# Seguridad y Alta Disponibilidad

# Tema 7. Seguridad en redes

# corporativas

# Índice

Esquema Material de estudio

## 7.1. Introducción y objetivos

## 7.2. Direccionamiento IP en LAN

## 7.3. Mecanismos de seguridad en LAN

## 7.4. Referencias bibliográficas

A fondo ¿Qué es una red LAN? ¿Qué son las VLAN y cuáles son sus beneficios? Diferencias entre VLAN y subredes VLAN: qué son, qué tipos hay y para qué sirven Entrenamientos

Entrenamiento 1: cuestiones

Entrenamiento 2: cálculo de subnetting

Entrenamiento 3: creación de VLAN en Packet Tracert

Entrenamiento 4: ACL extendidas

Entrenamiento 5: autenticación en el servidor RADIUS

# Esquema

![image-2](images/image-2.png)

Seguridad y Alta Disponibilidad 3 Tema 7. Esquema

# 7.1. Introducción y objetivos

Introducción

La seguridad en una red local es un aspecto fundamental en la gestión y protección de la información en entornos empresariales y domésticos. Para garantizar la integridad, la confidencialidad y la disponibilidad de los datos, es esencial implementar medidas que permitan segmentar la red y controlar el flujo de información entre distintas áreas. En este texto exploraremos diferentes **técnicas de** **configuración de redes locales,** como el *subnetting, variable length subnet mask* (VLSM) y la creación de redes *virtual local area networks* (VLAN), para entender cómo pueden contribuir a mejorar la seguridad y la eficiencia de una infraestructura de red. Además, se presentarán ejemplos prácticos que ilustran la aplicación de estos conceptos en entornos reales, con lo que se ofrece una guía para su implementación efectiva.

Al final del documento veremos las **redes WLAN.** Las redes inalámbricas han ganado popularidad debido a sus múltiples ventajas. Ofrecen conectividad en cualquier lugar y momento, su instalación es simple y económica y son fácilmente escalables sin las limitaciones del cableado. Sin embargo, presentan riesgos significativos, especialmente en cuanto a seguridad y fiabilidad. Una de las principales preocupaciones es la seguridad. Las redes inalámbricas utilizan el espectro de radiofrecuencia, que es público y puede ser interceptado, lo que aumenta la vulnerabilidad a ataques. Para mitigar estos riesgos, se han desarrollado varios sistemas de cifrado y autenticación.

Objetivos

**▸** Comprender los conceptos fundamentales de seguridad en redes locales y su importancia en la protección de la información.

**▸** Explorar diferentes técnicas de configuración de redes, como *subnetting,* VLSM y VLAN, para segmentar y organizar el tráfico de datos.

**▸** Identificar los beneficios de la segmentación de redes, como el control del tráfico, la optimización del rendimiento y la protección contra amenazas internas y externas.

**▸** Aprender a calcular máscaras de red y a asignar direcciones IP de manera eficiente para satisfacer las necesidades de una red, considerando el número de equipos y subredes requeridos.

**▸** Familiarizarse con ejemplos prácticos que ilustren la aplicación de las técnicas de segmentación de redes en entornos empresariales y domésticos.

**▸** Obtener conocimientos prácticos sobre la configuración de VLAN en *switches* administrables, lo cual incluye la asignación de puertos, configuración de troncales y enrutamiento inter-VLAN.

**▸** Adquirir habilidades para diseñar e implementar una estructura de red segura y eficiente, adecuada para las necesidades específicas de una organización o entorno doméstico.

**▸** Simplificar y Economizar la Instalación de Redes, ofreciendo una solución más sencilla y menos costosa para la instalación y ampliación de redes, permitiendo una rápida escalabilidad sin necesidad de cableado físico.

**▸** Garantizar la Seguridad de las Comunicaciones Inalámbricas, desarrollando y utilizando sistemas de cifrado y autenticación robustos para proteger las transmisiones inalámbricas contra accesos no autorizados e interceptaciones.

**▸** Proteger Contra Ataques y Vulnerabilidades, implementando medidas de seguridad avanzadas, como el cifrado AES y la autenticación robusta, para proteger las redes inalámbricas de ataques como la interceptación de datos y los ataques de diccionario.

# 7.2. Direccionamiento IP en LAN

Diferentes áreas de seguridad en la red

Dentro de una red Local, su configuración nos permite configurar los dispositivos para tener diferentes áreas en la red. Cada una de ellas se puede comunicar o no con las otras para salvaguardar la intimidad de privilegiados o no.

alguna y establecer nodos

Dentro de las **opciones básicas de configuración** que nos ofrecen los dispositivos de una red nos podríamos plantear:

**▸** *Subnetting* en la red.

**▸** VLSM, máscaras de red de tamaño variable.

**▸** Crear redes VLAN.

A esto hay que agregarle que desde el *router* de la red de la red se pueden establecer **políticas de control de paso de datos** en uno u otro sentido: lista de control de acceso (ACL).

Subnetting

Si se basa en una red de arquitectura TCP/IP y se personaliza la máscara de red, se puede crear en la red local diferentes áreas lógicas entre los equipos para aislar unos de otros.

La división en subredes, también conocida como *subnetting,* es una práctica esencial en la administración de redes de computadoras que permite segmentar **una red** **grande** en varias subredes más pequeñas. A principales motivos para realizar esta división.

continuación, se detallan los

#### Motivos para la división en subredes

**▸** Controlar el tráfico mediante la contención del tráfico de *broadcast* dentro de la subred:

- Broadcast control: en una red grande los mensajes de broadcast, que son enviados a todos los dispositivos de la red, pueden generar una cantidad significativa de tráfico que consume el ancho de banda y los recursos de los dispositivos. Al dividir la red en subredes, se limita el alcance de estos mensajes a una subred específica, lo que reduce la cantidad de tráfico *broadcast* y evita que afecte a toda la red.

**▸** Reducir el tráfico general de la red y mejorar el rendimiento de esta:

- Mejora el rendimiento: con menos dispositivos en cada subred, hay menos colisiones y retransmisiones, lo que mejora la eficiencia y el rendimiento general de la red. La reducción del tráfico de *broadcast* también contribuye a este incremento en el rendimiento.

- Tráfico localizado: al segmentar la red, el tráfico generado por los dispositivos dentro de una subred permanece dentro de esa subred, en lugar de propagarse por toda la red. Esto resulta en una utilización más eficiente del ancho de banda y una menor congestión en la red principal.

#### Beneficios adicionales de la división en subredes

**▸ Mejora de la seguridad:** las subredes permiten implementar políticas de seguridad específicas para diferentes segmentos de la red. Por ejemplo, se pueden aplicar reglas de *firewall* que restrinjan el acceso entre subredes, lo que protege segmentos sensibles de la red.

**▸ Gestión simplificada:** la administración de una red grande puede ser compleja. Al dividirla en subredes, la gestión se vuelve más manejable. Es más fácil identificar y resolver problemas cuando están contenidos dentro de una subred.

**▸ Escalabilidad:** la división en subredes facilita la expansión de la red. Se pueden añadir nuevas subredes sin necesidad de reestructurar toda la red existente.

**▸ Optimización del uso de direcciones IP:** el *subnetting* permite un uso más eficiente del espacio de las direcciones IP, especialmente en entornos donde las direcciones IP son limitadas. Al ajustar el tamaño de las subredes, se pueden asignar direcciones de manera más precisa según las necesidades específicas.

#### Comunicación entre subredes

Al crear subredes, es fundamental entender que, en muchas situaciones, será necesario permitir la comunicación entre estas subredes. Para facilitar esta comunicación, se deben considerar los siguientes aspectos clave:

**▸ Uso de un** ***router:***

- Necesidad de un router: un router es esencial para permitir la comunicación entre dispositivos en diferentes redes y subredes. Los *switches* y *hubs* no pueden realizar esta función porque operan principalmente en la capa de enlace de datos (capa 2 del modelo OSI), mientras que los *routers* operan en la capa de red (capa 3 del modelo OSI).

- Interfaz del router: cada interfaz del router debe tener una dirección de host IPv4 que pertenezca a la red o subred a la cual se conecta. Esto significa que, si el *router* conecta múltiples subredes, cada una de sus interfaces debe estar configurada con una dirección IP correspondiente a cada subred específica.

**▸** ***Gateway*** **predeterminado:**

- Configuración de gateway: los dispositivos en una red o subred utilizan la interfaz del *router* conectada a su *local area network* (LAN) como su *gateway* predeterminado. Esto significa que cualquier tráfico destinado a una red diferente se enviará a esta interfaz del *router,* que luego reenviará el tráfico al destino correcto.

#### Factores que se deben tener en cuenta al planificar las subredes

Al planificar la división en subredes, es crucial

considerar varios factores para

asegurarse de que la red satisfaga las necesidades actuales y futuras:

**▸ Cantidad de subredes requeridas:**

- Evaluación de necesidades: determinar cuántas subredes se necesitan en función de la estructura organizativa, los departamentos, las ubicaciones físicas y los requisitos de seguridad. Cada subred puede ser utilizada para diferentes propósitos o áreas de una organización.

**▸ Cantidad de direcciones de** ***host*** **requeridas:**

- Estimación de hosts: calcular cuántos dispositivos necesitarán direcciones IP en cada subred. Esto incluye no solo los dispositivos actuales, sino también la proyección de crecimiento futuro para evitar la necesidad de rediseñar la red a medida que aumenta el número de dispositivos.

**▸** Fórmula para determinar la **cantidad de** ***hosts*** **utilizables:**

Esta es la fórmula básica para determinar la cantidad de *hosts* utilizables en una red IPv4, en la que «n» representa el número de bits de *host* en la dirección IP. Sin embargo, cabe señalar que se resta 2 de la fórmula para excluir la dirección de red (que tiene todos los bits de *host* establecidos en 0) y la dirección de *broadcast* (que tiene todos los bits de *host* establecidos en 1), ya que estas direcciones no se asignan a dispositivos individuales en la red.

#### Ejemplo 1

Si tienes una dirección IP con una máscara de subred de /24 (que significa que hay 24 bits dedicados a la red y 8 bits dedicados a los *hosts),* entonces tendrías:

#### Ejemplo 2

Subneteo de una red clase C (/24) en subredes más pequeñas (/26):

Supongamos que tienes la red 192.168.1.0/24 y deseas dividirla en subredes más pequeñas para diferentes departamentos de una empresa. Tenemos cuatro departamentos y queremos crear una red para cada Dpto.

**▸** Dirección IP de red original: 192.168.1.0.

**▸** Máscara de subred original: 255.255.255.0 (/24).

Queremos crear subredes para cada Dpto. por lo que se tendrá que dividir la red en cuatro subredes. Si inicialmente tenemos 256 direcciones, ahora tendremos, para cada subred, 64 direcciones disponibles. Para ello, necesitamos una máscara de subred que tenga al menos 6 bits para hosts.

La máscara de red original es /24, lo que significa que los primeros 24 bits están dedicados a la red y los últimos 8 bits están dedicados a los hosts. Ahora, con 2 bits adicionales para las subredes, la nueva máscara de subred será /26 (24 + 2).

![▸ Nueva máscara de subred: 255.255.255.192 (/26). Ahora, podemos crear subredes de esta manera:](images/image-3.png)

Tabla 1. Resultados del ejemplo 2. Fuente: elaboración propia.

#### Ejemplo 3

Subneteo de una red clase B (/16) en subredes más pequeñas (/24): Supongamos que tienes la red 172.16.0.0/16 y deseas dividirla en subredes más pequeñas para diferentes sucursales de una empresa.

**▸** Dirección IP de red original: 172.16.0.0.

**▸** Máscara de subred original: 255.255.0.0 (/16). Queremos crear subredes con suficientes direcciones para 50 *hosts* en cada una. Para ello, necesitamos una máscara de subred que tenga al menos 6 bits para *hosts:*

**▸** Nueva máscara de subred: 255.255.255.192 (/26).

![Podemos crear subredes de esta manera:](images/image-4.png)

Tabla 2. Resultados del ejemplo 3. Fuente: elaboración propia.

VLSM

Es una técnica utilizada en la configuración de redes IP que permite dividir un espacio de red en subredes de diferentes tamaños, con lo cual se optimiza el uso de las direcciones IP. A continuación, te explico los puntos clave de VLSM:

**▸** La máscara de subred varía según la cantidad de bits que se toman prestados para una subred específica. Esto permite crear subredes de diferentes tamaños dentro de la misma red principal.

**▸** La red primero se divide en subredes y, a continuación, las subredes se vuelven a dividir en subredes. Este proceso se repite tantas veces como sea necesario.

**▸** El proceso de subdivisión se repite hasta que se obtienen subredes del tamaño adecuado para las necesidades específicas de la red. Esto maximiza la eficiencia del uso de direcciones IP.

**▸** En el proceso de crear subredes con VLSM se recomienda iniciar con las subredes más grandes y terminar con las más pequeñas. Esto se debe a que las subredes más grandes tienen más direcciones IP disponibles y es más fácil dividirlas en subredes más pequeñas después. Comenzar con las subredes más grandes garantiza que las necesidades de las subredes más grandes se satisfacen primero y reduce el riesgo de quedarte sin espacio para las subredes más pequeñas.

#### Ejemplo de VLSM

Dada la red 192.168.1.0/24, desarrolla un esquema de direccionamiento que cumpla con los siguientes requerimientos. Optimice el espacio de direccionamiento tanto como sea posible (por lo tanto, utiliza VLSM).

**▸** Una subred de 20 hosts para ser asignada a la VLAN de diseñadores.

**▸** Una subred de 80 hosts para ser asignada a la VLAN de programadores.

**▸** Una subred de 20 hosts para ser asignada a la VLAN de invitados.

**▸** Tres subredes de 2 hosts para ser asignada a los enlaces entre enrutadores.

Recomendación:

1.º - Ordenar las redes de mayor a menor por n.º de *host.*

2.º - Calcular la máscara, subred, etc., para cada área en función de los

*hosts.*

**80** ***hosts*** **– programadores:**

Necesito 7 bits (27=128, menos red y *broadcast* 126 *hosts* máx.).

Prefijo /25.

Subred cero 192.168.1.0/25.

IP mínima 192.168.1.1.

IP máxima 192.168.1.126.

*Broadcast* 192.168.1.127.

**20** ***hosts*** **– diseñadores:**

Necesito 5 bits (25=32, es decir 30 *hosts* máx.).

Prefijo /27.

Subred: 192.168.1.128.

IP mínima 192.168.1.129.

IP máxima 192.168.1.158.

*Broadcast* 192.168.1.159.

**20** ***hosts*** **– invitados:**

La siguiente subred es del mismo tamaño 5 bits y el prefijo es el mismo

/27.

Subred: 192.168.1.160/27.

IP mínima 192.168.1.161.

IP máxima 192.168.1.190.

*Broadcast* 192.168.1.191.

**3 enlaces entre enrutadores:**

2 *host* necesito 4 bits (22=4, es decir 2 *hosts* máx.) por lo tanto el prefijo

debe ser /30:

**Enlace 1:** Subred: 192.168.1.192 /30.

Ip 1: 192.168.1.193.

Ip 2: 192.168.1.194.

*Broadcast:* 192.168.1.195.

**Enlace 2:** Subred: 192.168.1.196 /30.

Ip 1: 192.168.1.197.

Ip 2: 192.168.1.198.

*Broadcast:* 192.168.1.199.

**Enlace 3:** Subred: 192.168.1.200 /30.

Ip 1: 192.168.1.201.

Ip 2: 192.168.1.202.

*Broadcast:* 192.168.1.203.

![image-5](images/image-5.png)

Tabla 3. Resumen Ejemplo VLMS. Fuente: elaboración propia.

VLAN

Crear redes VLAN es una forma de segmentar una red física en múltiples redes virtuales, lo que permite aislar el tráfico y mejorar la seguridad y el rendimiento.

Aquí tienes los pasos básicos para crear VLAN en un *switch* administrable:

**▸ Accede al** ***switch:*** utiliza un *software* de gestión de red o una interfaz de línea de comandos (CLI) para acceder al *switch.*

**▸ Configura las VLAN:** utiliza comandos específicos del *switch* para crear las VLAN deseadas. Por ejemplo, en muchos *switches* Cisco, usarías comandos como «vlan <ID>» para crear una VLAN con un ID específico.

**▸ Asigna puertos a las VLAN:** una vez que las VLAN estén creadas, asigna los puertos del *switch* a cada VLAN. Esto se puede hacer mediante comandos específicos del *switch* o mediante una interfaz gráfica de usuario (GUI) si el *switch* la ofrece. Por ejemplo, puedes usar comandos como «switchport access vlan <ID>» para asignarle un puerto a una VLAN en un *switch* Cisco.

**▸ Configura troncales** ***(trunks):*** si estás conectando varios *switches* entre sí y quieres que las VLAN se comuniquen a través de ellos, necesitarás configurar troncales *(trunks)* entre los *switches.* Esto permite que todas las VLAN pasen a través de los enlaces entre *switches.*

**▸ Configura el enrutamiento inter-VLAN (opcional):** si necesitas que las VLAN se comuniquen entre sí, deberás configurar el enrutamiento inter-VLAN. Esto se puede hacer mediante un *router* que sea capaz de manejar múltiples subredes o mediante una capa tres de *switch* que admita enrutamiento inter-VLAN.

**▸ Verifica la configuración:** después de configurar las VLAN, verifica que todo esté funcionando correctamente. Puedes hacerlo mediante comandos de verificación en el *switch* o mediante herramientas de monitoreo de red.

Es esencial entender la topología de red y las necesidades específicas antes de configurar las VLAN. Además, asegúrate de seguir las mejores prácticas de seguridad, como segmentar las VLAN según la sensibilidad de los datos y limitar el tráfico entre ellas según sea necesario.

![Figura 1. Estructura de red con VLAN. Fuente: Martínez, 2013.](images/image-6.png)

*Figura 1. Estructura de red con VLAN. Fuente: Martínez, 2013.*

#### Ejemplo de VLAN en entorno de red empresarial

Supongamos que tienes un *switch* administrable (p. ej. Cisco Catalyst) con varios puertos y quieres crear VLAN para separar el tráfico de diferentes departamentos de tu empresa: ventas (VLAN 10), ingeniería (VLAN 20) y administración (VLAN 30).

1. Acceso al switch: accedes al switch a través de una interfaz de línea de

comandos (CLI) o una interfaz gráfica de usuario (GUI).

## 2. Configuración de VLAN:

- ▸ Creas las VLAN utilizando comandos específicos del switch:

![Figura 2. Creación de VLAN. Fuente: elaboración propia.](images/image-7.png)

*Figura 2. Creación de VLAN. Fuente: elaboración propia.*

    - Seguridad y Alta Disponibilidad 19

        - Tema 7. Material de estudio

## 3. Asignación de puertos a las VLAN:

![Figura 3. Asignación de puertos a las VLAN. Fuente: elaboración propia. Asignar los puertos del switch a cada VLAN: ▸ Puertos 1-10 están en VLAN 10 (ventas). ▸ Puertos 11-20 están en VLAN 20 (ingeniería). ▸ Puertos 21-30 están en VLAN 30 (administración).](images/image-8.png)

*Figura 3. Asignación de puertos a las VLAN. Fuente: elaboración propia.*

## 4. Configuración de troncales (opcional):

**▸** Si necesitamos que otro *switch* o un *router* se conecte y entienda todas las VLAN, configuramos un puerto como *trunk.* Supongamos que usamos el puerto 0/48 para esto.

![Figura 4. Configuración de troncales en las VLAN. Fuente: elaboración propia.](images/image-9.png)

*Figura 4. Configuración de troncales en las VLAN. Fuente: elaboración propia.*

## 5. Verificación de la configuración:

**▸** Verificar que la configuración se haya aplicado correctamente utilizando comandos de verificación en el *switch* o herramientas de monitoreo de red.

![Figura 5. Verificación de la configuración en las VLAN. Fuente: elaboración propia.](images/image-10.png)

*Figura 5. Verificación de la configuración en las VLAN. Fuente: elaboración propia.*

Estos comandos mostrarán las VLAN creadas y los puertos asignados a cada una, así como los puertos configurados como *trunk.*

![Figura 6. Comando VLAN brief. Fuente: elaboración propia.](images/image-11.png)

*Figura 6. Comando VLAN brief. Fuente: elaboración propia.*

![Figura 7. Comando interface trunk. Fuente: elaboración propia.](images/image-12.png)

*Figura 7. Comando interface trunk. Fuente: elaboración propia.*

Este es solo un ejemplo básico. La configuración exacta puede variar según el tipo de *switch* y los requisitos específicos de la red, pero estos pasos deberían darte una idea de cómo se realiza la configuración de VLAN en un entorno empresarial.

# 7.3. Mecanismos de seguridad en LAN

Las VLAN permiten la segmentación lógica de una red física en múltiples redes virtuales, lo que facilita una administración más flexible y eficiente. A continuación, vamos a ver varios tipos de VLAN basadas en diferentes criterios, como puertos, direcciones MAC y protocolos, también destacaremos sus ventajas, como la mayor flexibilidad, seguridad y eficiencia en la transmisión de tráfico.

Las ACL son herramientas utilizadas para seleccionar y controlar el tráfico en una red mediante reglas que determinan qué tráfico se permite o se bloquea. Vamos a explicar los tipos de ACL, incluyendo las ACL estándar, que filtran el tráfico basado en direcciones IP de origen, y las ACL extendidas, que permiten un control más detallado que incluye las direcciones IP de destino y protocolos específicos.

Finalmente, abordaremos la seguridad en las redes inalámbricas, para lo cual destacaremos los riesgos asociados y las soluciones de cifrado y autenticación que están disponibles, como *wired equivalent privacy* (WEP), *wifi protected access* (WPA), WPA2 y WPA3, que mejoran la protección de las comunicaciones inalámbricas.

En conjunto, estos temas proporcionan un marco integral para entender cómo mejorar la gestión y la seguridad de las redes modernas.

VLAN

Como hemos visto antes, una red de área local virtual (VLAN) es una red de área local que organiza un grupo de dispositivos de forma lógica en lugar de física.

Normalmente, la comunicación entre los dispositivos en una red de área local está determinada por la estructura física de la red. Sin embargo, con las VLAN, es posible superar las restricciones de la arquitectura física (como limitaciones geográficas o de direccionamiento), ya que se establece una **segmentación lógica** que agrupa los

Seguridad y Alta Disponibilidad 23 Tema 7. Material de estudio dispositivos según ciertos criterios (como direcciones MAC, números de puertos, protocolos, etc.). Esto permite alcanzar un mayor nivel de seguridad para controlar el acceso a los dispositivos.

#### Tipos de VLAN

Existen diferentes tipos de VLAN, los cuales son clasificados según los **criterios de** **conmutación y el nivel** en el que se implementan:

**▸ VLAN de nivel 1** (VLAN basada en puerto): este tipo de VLAN define una red virtual según los puertos de conexión del conmutador. Es el tipo más simple, en el que cada puerto del conmutador se asigna a una VLAN específica.

**▸ VLAN de nivel 2** (VLAN basada en la dirección MAC): este tipo de VLAN define una red virtual según las direcciones MAC de los dispositivos. Es más flexible que la VLAN basada en puerto, ya que permite que la red sea independiente de la ubicación física de los dispositivos.

**▸ VLAN de nivel 3:**

- VLAN basada en la dirección de red: conecta subredes según la dirección IP de origen de los datagramas. Esta solución ofrece una gran flexibilidad, ya que los conmutadores se configuran automáticamente cuando se mueve un dispositivo. Sin embargo, puede haber una ligera disminución del rendimiento debido al análisis detallado de la información contenida en los paquetes.

- VLAN basada en protocolo: permite crear una red virtual según el tipo de protocolo (por ejemplo, TCP/IP, IPX, AppleTalk, etc.). Esto permite agrupar todos los dispositivos que utilizan el mismo protocolo en la misma red.

#### Ventajas de la VLAN

La VLAN permite definir una nueva red por encima de la red física y, por lo tanto, ofrece las siguientes ventajas:

**▸ Mayor flexibilidad** en la administración y cambios de la red: la arquitectura puede cambiarse utilizando parámetros de los conmutadores sin necesidad de reconfigurar el cableado físico.

**▸ Aumento de la seguridad:** la información se encapsula en un nivel adicional y posiblemente se analiza, lo que proporciona un nivel extra de protección contra accesos no autorizados.

**▸ Disminución en la transmisión de tráfico en la red:** segmenta el tráfico de red, lo que reduce las colisiones y mejora la eficiencia del uso del ancho de banda.

En resumen, las VLAN permiten una gestión más eficiente y flexible de las redes, con lo que ofrecen soluciones personalizadas según las necesidades específicas de una organización, ya sea en términos de ubicación física, direcciones MAC, direcciones

IP o protocolos utilizados.

Listas de control de acceso

Una ACL es una **lista de reglas que controlan el tráfico** de red hacia y desde una

red específica. Estas reglas se utilizan para permitir o denegar el tráfico en función de diversos criterios, como la dirección IP de origen, la dirección IP de destino, el puerto de origen, el puerto de destino y el protocolo utilizado.

Una vez que la selección se establece, se puede usar para **múltiples finalidades:**

**▸** Como mecanismo básico de seguridad, es decir, el tráfico seleccionado se puede bloquear o permitir según las necesidades de la organización.

**▸** Para definir conjuntos de direcciones o flujos de tráfico seleccionados entre muchos otros.

Las ACL se pueden configurar en *routers* y *switches* para controlar el tráfico de entrada y salida en interfaces específicas, y en *firewalls* para definir políticas de seguridad y controlar el acceso a diferentes partes de la red.

#### Tipos de ACL

Para un enrutador, las listas de control de acceso (ACL) son herramientas cruciales:

**▸ ACL estándar:** se basa únicamente en la dirección IP de origen. Se utiliza principalmente para permitir o denegar el tráfico según la dirección IP de origen. Es útil para controlar el acceso de ciertos *hosts* o subredes a recursos de red específicos.

Ejemplo

Queremos que el enrutador permita únicamente el tráfico proveniente de la subred 192.168.1.0/24 hacia tu red interna y deniegue todo lo demás.

![Figura 8. Configuración ACL estándar. Fuente: elaboración propia.](images/image-13.png)

*Figura 8. Configuración ACL estándar. Fuente: elaboración propia.*

Explicación

ip access-list standard ACL-ESTANDAR : esto le indica al enrutador que vas a crear una lista de control de acceso estándar llamada «ACL-ESTANDAR». permit 192.168.1.0 0.0.0.255 : esta línea especifica que se permitirá el tráfico desde la subred 192.168.1.0/24 hacia cualquier destino.

deny any : esta línea deniega cualquier otro tráfico que no esté permitido explícitamente.

interface FastEthernet0/0 : esta línea selecciona la interfaz FastEthernet0/0 para aplicar la lista de control de acceso.

ip access-group ACL-ESTANDAR in : esta línea aplica la lista de control de acceso «ACL-ESTANDAR» a la interfaz FastEthernet0/0 en la dirección de entrada («in»).

**▸ ACL extendida:** además de la dirección IP de origen, también puede filtrar por dirección IP de destino, protocolo, puerto y otros criterios. Proporciona una mayor granularidad en el control del tráfico. Puede utilizarse para aplicar políticas de seguridad más específicas, como permitir o denegar el tráfico de aplicaciones específicas o servicios.

Ejemplo Imagina que deseas permitir el tráfico SSH (puerto 22) desde una dirección IP específica (por ejemplo, 203.0.113.5) hacia tu red interna.

![Figura 9. Configuración ACL extendida. Fuente: elaboración propia.](images/image-14.png)

*Figura 9. Configuración ACL extendida. Fuente: elaboración propia.*

Explicación access-list 101 : crea una lista de control de acceso numerada. En este caso, utilizamos el número 101, pero podría ser cualquier número disponible. permit : indica que se permitirá el tráfico que coincida con los criterios de la ACL. tcp : especifica que el tráfico que se va a permitir es de tipo TCP. host 203.0.113.5 : especifica la dirección IP desde la que se permitirá el tráfico SSH. any : indica que el tráfico puede tener cualquier dirección de destino. eq 22 : indica que el tráfico permitido debe tener como puerto de destino el puerto 22, que es el puerto estándar para SSH. interface GigabitEthernet0/0 : esta línea selecciona la interfaz GigabitEthernet0/0 para aplicar la lista de control de acceso. ip access-group 101 in : esta línea aplica la lista de control de acceso «101» a la interfaz GigabitEthernet0/0 en la dirección de entrada («in»).

Seguridad en redes inalámbricas

En los últimos años ha irrumpido con fuerza, en el sector de las redes locales, las comunicaciones inalámbricas, también denominadas *wireless.* La tecnología inalámbrica ofrece muchas ventajas en comparación con las tradicionales redes conectadas por cable.

#### Ventajas

**▸ Mayor disponibilidad y acceso a redes:** la capacidad de ofrecer conectividad en cualquier momento y lugar es una de las mayores ventajas de las redes inalámbricas. Esto permite una mayor flexibilidad y movilidad para los usuarios, ya que no están limitados por cables físicos.

**▸ Instalación simple y económica:** la instalación de tecnología inalámbrica es generalmente más simple y económica que la instalación de redes cableadas. No se requiere tendido de cables, lo que reduce los costos y el tiempo de implementación.

**▸ Escalabilidad:** las redes inalámbricas permiten una expansión fácil sin las limitaciones físicas del cableado. Esto significa que las empresas pueden ampliar su red de manera rápida y sencilla para adaptarse a las necesidades cambiantes sin tener que realizar grandes inversiones en infraestructura cableada.

Sin embargo, junto con estas ventajas, también existen riesgos y limitaciones asociados con las comunicaciones inalámbricas.

#### Riesgos y limitaciones

**▸ Interferencia de señal:** las redes inalámbricas operan en el espectro de la radiofrecuencia, que es compartido por una variedad de dispositivos y tecnologías. Esto puede llevar a la interferencia de señal, especialmente en entornos densos en los que múltiples dispositivos inalámbricos compiten por el mismo espectro.

**▸ Seguridad:** la seguridad es una preocupación importante en las redes inalámbricas debido a la naturaleza de las transmisiones de datos a través del aire. Sin las debidas precauciones, las comunicaciones inalámbricas pueden ser interceptadas por cualquier dispositivo que esté dentro del alcance de la señal, lo que puede conducir a la exposición de datos sensibles y vulnerabilidades de seguridad.

Abordar estos riesgos y limitaciones es crucial para garantizar la integridad, la confidencialidad y la disponibilidad de las redes inalámbricas. Esto puede implicar la implementación de medidas de seguridad robustas, como la encriptación de datos, la autenticación de usuarios y la gestión adecuada del espectro de radiofrecuencia para minimizar la interferencia.

#### Sistemas de seguridad de WLAN

Los sistemas de cifrados empleados para la autenticación con encriptación en redes inalámbricas son:

**▸ Sistema abierto:** este es el nivel más básico de seguridad, el cual no incluye autenticación ni cifrado. Esencialmente, cualquier dispositivo puede conectarse a la red sin restricciones.

**▸** ***Wired equivalent privacy*** **(WEP):** fue el primer estándar de cifrado utilizado en redes inalámbricas. Sin embargo, WEP es conocido por sus graves vulnerabilidades de seguridad y se considera obsoleto. A pesar de su fácil configuración, es muy fácil de romper y no se recomienda su uso.

**▸** ***Wifi protected access*** **(WPA):** fue introducido como una mejora sobre WEP, ya que WPA aborda algunas de las debilidades de su predecesor. Utiliza el protocolo TKIP para la encriptación, que proporciona una mayor seguridad que WEP. También mejora la autenticación mediante el protocolo EAP.

**▸** ***Wifi protected access*** **2 (WPA2):** fue considerado el estándar de seguridad más robusto para redes inalámbricas antes de la introducción de WPA3, dado que WPA2 utiliza el protocolo AES para la encriptación, que es aún más seguro que TKIP. Ofrece dos modos de operación: WPA2-Personal y WPA2-Enterprise.

**▸** ***Wifi protected access*** **3 (WPA3):** es la última versión de seguridad wifi y fue diseñada para abordar las deficiencias de WPA2. Introduce características como el cifrado individualizado de datos, la protección mejorada contra ataques de diccionario y un proceso de autenticación más sólido.

Además de estos sistemas de cifrado, hay otras medidas de seguridad que se pueden implementar en las redes inalámbricas, como el filtrado de direcciones MAC, la ocultación de SSID, la autenticación por servidor RADIUS y la autenticación de dos factores. Sin embargo, es importante recordar que ninguna medida de seguridad es infalible, por lo que es fundamental mantenerse al tanto de las últimas amenazas y adoptar prácticas de seguridad sólidas.

**▸ Autenticación de servidor** ***remote authentication dial-in user service*** **(RADIUS):** en entornos empresariales más grandes, es común utilizar un servidor de autenticación RADIUS. Con este método, los usuarios deben ingresar sus credenciales (generalmente un nombre de usuario y contraseña), que son verificadas por el servidor RADIUS, antes de que se les conceda acceso a la red. Este método proporciona un mayor nivel de seguridad y control sobre quién tiene acceso a la red, ya que las credenciales de usuario se almacenan y administran centralmente en el servidor RADIUS.

# 7.4. Referencias bibliográficas

Martínez, V. E. (2013). *Configuración de VLAN (Virtual Local Area Network)* [gráfico]. [https://theosnews.com/2013/03/configuracion-de-vlan-virtual-local-area-network/](https://theosnews.com/2013/03/configuracion-de-vlan-virtual-local-area-network/)

# VLAN y cuáles son sus beneficios? [vídeo]. YouTube.

# [https://www.youtube.com/watch?v=VD5k_0q_fus](https://www.youtube.com/watch?v=VD5k_0q_fus)

¿Qué es una red LAN? ¿Qué son las VLAN y cuáles son sus beneficios?

AlbertoLopez TECH TIPS. (2023, julio 17). *¿Qué es una red LAN? ¿Qué son las* Si no te ha quedado claro qué es una red LAN y qué es una VLAN, deberías ver este vídeo. Entenderás la importancia que tiene el implementar un sistema de VLAN dentro de tu corporación.

![image-15](images/image-15.png)

Accede al vídeo: [https://www.youtube.com/embed/VD5k_0q_fus](https://www.youtube.com/embed/VD5k_0q_fus)

Seguridad y Alta Disponibilidad 33 Tema 7. A fondo

# [https://www.youtube.com/watch?v=FfaA__4T2zc](https://www.youtube.com/watch?v=FfaA__4T2zc)

# Diferencias entre VLAN y subredes

AlbertoLopez TECH TIPS. (2023, septiembre 3). *Diferencias entre VLAN y subredes* *[Curso de redes] Explicación sencilla y básica | Alberto López* [vídeo]. YouTube. No siempre queda claro cuáles son las diferencias entre las subredes y las VLAN. En este vídeo te muestran cuándo utilizar un método u otro, en función de tus necesidades.

![image-16](images/image-16.png)

Accede al vídeo: [https://www.youtube.com/embed/FfaA__4T2zc](https://www.youtube.com/embed/FfaA__4T2zc)

Seguridad y Alta Disponibilidad 34 Tema 7. A fondo

# VLAN: qué son, qué tipos hay y para qué sirven

De Luz, S. (2024, mayo 29). VLAN: qué son, tipos y para qué sirven. *Redes Zone.* [https://www.redeszone.net/tutoriales/redes-cable/vlan-tipos-configuracion/](https://www.redeszone.net/tutoriales/redes-cable/vlan-tipos-configuracion/)

Profundiza mucho más en la tecnología VLAN. Encuentra las virtudes de este método. Se trata de un concepto que tendría que estar más arraigado en los conocimientos de un técnico informático.

Seguridad y Alta Disponibilidad 35 Tema 7. A fondo

# Entrenamiento 1: cuestiones

#### ▸ Planteamiento del ejercicio

Responde argumentando las siguientes cuestiones:

**▸**

- 1. Se quiere tener una red de veinticinco equipos, ¿cuál es la máscara de red más adecuada?

- 2. Una IP 172.56.2.8/17 ¿cuántos equipos puede llegar a tener como máximo?

- 3. ¿Cuántas subredes tiene una máscara de red /25? ¿Cuántos equipos puede tener cada una de las subredes?

- 4. Tengo una red con quinientos equipos, ¿qué máscara de red necesito?

- 5. Tengo una red con ocho equipos, ¿qué máscara de red necesito?

- 6. Tengo una red con diez mil equipos, ¿qué máscara de red necesito?

#### ▸ Desarrollo paso a paso

Si te basas en lo dado en teoría, no te resultará difícil llegar a los resultados.

#### ▸ Solución

- 1. Para una red de veinticinco equipos necesitamos calcular cuántos bits de host se necesitan. Sabemos que , lo que significa que necesitamos al menos 5 bits para representar 25 direcciones IP. La máscara de red más adecuada sería /27, ya que esto proporciona 32 direcciones IP en total, de las cuales 30 pueden ser utilizables por los equipos.

- 2. Para la dirección IP 172.56.2.8/17 tenemos 17 bits para la parte de red y 15 bits para la parte de *host.* Para calcular el número máximo de equipos, restamos 2 (una para la dirección de red y otra para la dirección de *broadcast)* del total de direcciones posibles para la parte de host:

.

- 3. Con una máscara de red /25, tenemos 25 bits para la parte de red y 7 bits para la parte de *host.* Para calcular el número de subredes utilizamos y para el número máximo de equipos por subred utilizamos

.

- 4. Para quinientos equipos necesitamos calcular cuántos bits de host se necesitan. Sabemos que , lo que significa que necesitamos al menos 9 bits para representar 500 direcciones IP. La máscara de red necesaria sería /23, ya que proporciona 510 direcciones IP en total.

- 5. Para ocho equipos necesitamos calcular cuántos bits de host se necesitan. Sabemos que , lo que significa que necesitamos al menos 4 bits para representar 8 direcciones IP. La máscara de red necesaria sería /29, ya que proporciona 6 direcciones IP utilizables en total.

- 6. Para diez mil equipos necesitamos calcular cuántos bits de host se necesitan. Sabemos que , lo que significa que necesitamos al menos 14 bits para representar 10 000 direcciones IP. La máscara de red necesaria sería /20, ya que proporciona direcciones IP utilizables en total, lo que es suficiente para 10 000 equipos.

# Entrenamiento 2: cálculo de subnetting

#### ▸ Planteamiento del ejercicio

Disponemos de una clase C (192.168.1.0/24) y queremos dividirla en ocho subredes que sean iguales en tamaño.

#### ▸ Desarrollo paso a paso

- Comenzaremos por determinar cuántos bits necesitaremos para representar las ocho subredes.

- Continuaremos calculando la nueva máscara de subred.

- A continuación, calcularemos el tamaño de cada subred.

- Por último, definiremos cuál es cada subred, la dirección de red y la de broadcast y representaremos todos los datos en una tabla.

#### ▸ Solución

Bits necesarios para representar las ocho subredes

Como , necesitaremos 3 bits adicionales para crear las 8 subredes.

La máscara de subred original es /24, lo que significa que los primeros 24 bits están dedicados a la red y los últimos 8 bits están dedicados a los *hosts.* Ahora, con 3 bits adicionales para las subredes, la nueva máscara de subred será /27 (24 + 3).

A continuación, calculamos el tamaño de cada subred. Como ahora tenemos 3 bits adicionales para las subredes, cada subred puede tener direcciones IP disponibles (debido a que se reserva una dirección para la dirección de red y otra para la dirección de *broadcast).*

![Aquí está la tabla de las ocho subredes:](images/image-17.png)

Tabla 4. Tabla de las ocho subredes. Fuente: elaboración propia.

# Entrenamiento 3: creación de VLAN en Packet

# Tracert

#### ▸ Planteamiento del ejercicio

Una empresa necesita segmentar su red para mejorar el rendimiento y la seguridad. Se te ha asignado la tarea de configurar las VLAN en su red existente utilizando Packet Tracer. Debes seguir las siguientes pautas:

**▸**

- Existe un switch y un router. Se deben crear tres VLAN (administración, ventas y desarrollo), que deben estar comunicadas.

- Debes verificar que las VLAN estén configuradas correctamente utilizando comandos de verificación en el *switch* y el *router.*

#### ▸ Desarrollo paso a paso

1. Topología de red: crea una topología que incluya al menos un switch, un router y

varios dispositivos finales como computadoras o servidores.

2. Creación de VLAN: configura el switch para crear al menos tres VLAN (VLAN de

administración, VLAN de ventas y VLAN de desarrollo). Asigna rangos de direcciones IP adecuados a cada VLAN.

3. Asignación de puertos: asigna los puertos del switch a las VLAN

correspondientes según el departamento al que pertenezcan los dispositivos finales conectados.

4. Comunicación entre VLAN: configura el router para permitir la comunicación

entre las VLAN. Utiliza subinterfaces en el *router* para conectar las VLAN a la red local.

5. Verificación y pruebas: verifica que las VLAN estén configuradas correctamente

utilizando comandos de verificación en el *switch* y el *router.* Realiza pruebas de conectividad entre dispositivos en diferentes VLAN

configuración funcione como se espera.

#### ▸ Solución

Debemos tener instalado el *software* Packet Tracer.

**Paso 1:** crear la topología de red.

**▸**

para asegurarte de que la

- Agregar dispositivos: añade un switch, un router y varios dispositivos finales (PC o servidores) al área de trabajo de Packet Tracer.

- Conectar dispositivos: usa cables de cobre (copper straight-through) para conectar los dispositivos al *switch* y al *router.*

**Paso 2:** configurar las VLAN en el *switch.*

**▸**

- Acceder al switch: haz clic en el switch y accede a la línea de comandos (CLI).

- 2. Entrar en modo de configuración global:

![Figura 10. Modo de configuración global. Fuente: elaboración propia.](images/image-18.png)

*Figura 10. Modo de configuración global. Fuente: elaboración propia.*

**▸**

- Crear las VLAN:

![Figura 11. Crear las VLAN. Fuente: elaboración propia.](images/image-19.png)

*Figura 11. Crear las VLAN. Fuente: elaboración propia.*

Con estos comandos crearemos las tres VLAN y les asignaremos un nombre. Así tendremos la VLAN con el ID 10 de nombre administración, la VLAN con el ID 20 de nombre ventas y la VLAN con el ID 30 de nombre desarrollo.

**Paso 3:** asignar los puertos del *switch* a las VLAN.

**▸**

- Asigna los puertos del switch a las VLAN creadas. Por ejemplo:

![Figura 12. Asignar los puertos del switch a las VLAN creadas. Fuente: elaboración propia.](images/image-20.png)

*Figura 12. Asignar los puertos del switch a las VLAN creadas. Fuente: elaboración propia.*

Se seleccionan los puertos del 0/1 al 0/3 del *switch* y se asignan a la VLAN 10. Por otro lado los puertos del 0/4 al 0/6 del *switch* se asignan a la VLAN 20 y, por último, se seleccionan los puertos del 0/7 al 0/9 del *switch* y se asignan a la VLAN 30.

**Paso 4:** configurar el *router* para la comunicación entre las VLAN.

**▸**

- Acceder al router: haz clic en el router y accede a la línea de comandos (CLI).

- Entrar en modo de configuración global:

![Figura 13. Modo de configuración global. Fuente: elaboración propia.](images/image-21.png)

*Figura 13. Modo de configuración global. Fuente: elaboración propia.*

![Figura 14. Crear subinterfaces para cada VLAN. Fuente: elaboración propia. ▸ • Crear subinterfaces para cada VLAN:](images/image-22.png)

*Figura 14. Crear subinterfaces para cada VLAN. Fuente: elaboración propia.*

Donde:

**▸**

- interface gigabitethernet 0/0.10 : crea una subinterfaz para la VLAN 10 en la interfaz gigabitethernet 0/0.

- encapsulation dot1Q 10 : configura la encapsulación 802.1Q para la VLAN 10.

- ip address 192.168.10.1 255.255.255.0 : asigna la dirección IP 192.168.10.1 con una máscara de subred de 255.255.255.0 a esta subinterfaz.

Y así con el resto de las VLAN.

**Paso 5:** verificación y pruebas.

**▸**

![Figura 15. Verificar la configuración en el switch. Fuente: elaboración propia. • Verificar la configuración en el switch:](images/image-23.png)

*Figura 15. Verificar la configuración en el switch. Fuente: elaboración propia.*

Donde:

show vlan brief : muestra un resumen de las VLAN configuradas y los puertos asignados a cada una. show interfaces trunk : muestra información sobre las interfaces configuradas como troncales, incluyendo las VLAN permitidas y activas en cada troncal.

![Figura 16. Resultado. Fuente: elaboración propia. El resultado esperado sería el siguiente:](images/image-24.png)

*Figura 16. Resultado. Fuente: elaboración propia.*

![Figura 17. Resultado. Fuente: elaboración propia.](images/image-25.png)

*Figura 17. Resultado. Fuente: elaboración propia.*

**▸**

- Verificar la configuración en el router:

![Figura 18. Verificar la configuración en el router. Fuente: elaboración propia.](images/image-26.png)

*Figura 18. Verificar la configuración en el router. Fuente: elaboración propia.*

![Figura 19. Resultado. Fuente: elaboración propia. Obtendremos como resultado:](images/image-27.png)

*Figura 19. Resultado. Fuente: elaboración propia.*

**▸**

- Pruebas de conectividad:

Configura las direcciones IP en los dispositivos finales de acuerdo con las VLAN a las que pertenecen.

![image-28](images/image-28.png)

Tabla 5. Configurar las direcciones IP. Fuente: elaboración propia.

Usa el comando «ping» desde un dispositivo en una VLAN para verificar la conectividad con dispositivos en otra VLAN.

Con esta configuración deberías tener una red segmentada con VLAN para administración, ventas y desarrollo, además de tener una comunicación entre las VLAN a través del *router* configurado. Realiza las pruebas de *ping* para asegurarte de que la configuración es correcta y que los dispositivos en los diferentes VLAN pueden comunicarse entre sí.

# Entrenamiento 4: ACL extendidas

#### ▸ Planteamiento del ejercicio

Mostrar ejemplos de cómo configurar ACL extendidas en *routers* Cisco por protocolo, por puerto, una ACL dinámica, y explica cada comando que incluyas

#### ▸ Desarrollo paso a paso

- ACL extendida por protocolo: una ACL extendida por protocolo en redes informáticas es una lista de control de acceso que les permite a los administradores de red definir reglas detalladas para permitir o denegar el tráfico de red según una variedad de criterios. Estas listas se utilizan para mejorar la seguridad y controlar el tráfico en las redes.

Pongamos, por ejemplo, una ACL que deniega el tráfico ICMP (protocolo 1) desde cualquier origen hacia la red 192.168.10.0/24 y permite todo el resto del tráfico IP.

**Paso 1:** acceder al modo de configuración global.

**Paso 2:** crear una ACL extendida.

**Paso 3:** permitir todo el resto del tráfico IP.

**Paso 4:** aplicar la ACL a una interfaz.

**▸**

- ACL extendida por puerto: cuando hablamos de una «ACL extendida por puerto», nos estamos refiriendo a la capacidad de la ACL extendida para filtrar el tráfico basándose en los números de puerto específicos. Esto es particularmente útil para controlar el acceso a ciertos servicios y aplicaciones que operan en puertos específicos.

Pongamos, por ejemplo, que queremos denegar el tráfico HTTP (puerto 80) desde la red 10.1.1.0/24 hacia cualquier destino y permitiremos todo el resto del tráfico IP.

**Paso 1:** acceder al modo de configuración global.

**Paso 2:** crear una ACL extendida.

**Paso 3:** permitir todo el resto del tráfico IP.

**Paso 4:** aplicar la ACL a una interfaz.

**▸**

- ACL dinámica: una «ACL dinámica» se refiere a una lista de control de acceso (ACL) que se crea, modifica o elimina automáticamente en respuesta a ciertos eventos o condiciones en una red.

Una ACL dinámica podría ser configurada para ajustarse automáticamente a los cambios en la red, como la aparición o desaparición de dispositivos, cambios en la topología de la red, o el estado de seguridad de la red. Por ejemplo, una ACL dinámica podría permitir el acceso a un recurso de red solo durante ciertas horas del día, o podría bloquear automáticamente ciertos tipos de tráfico en respuesta a un ataque de seguridad detectado. Ejemplo: imagina que deseas permitir temporalmente el tráfico SSH desde cualquier origen hacia tu red interna durante ciertas horas del día.

**Paso 1:** acceder al modo de configuración global.

**Paso 2:** crear una lista de tiempo *(time-range).*

**Paso 3:** permitir todo el resto del tráfico IP.

**Paso 4:** aplicar la ACL a una interfaz.

#### ▸ Solución

- ACL extendida por protocolo: una ACL que deniega el tráfico ICMP (protocolo 1) desde cualquier origen hacia la red 192.168.10.0/24 y permite todo el resto del tráfico IP.

**Paso 1:** acceder al modo de configuración global. Primero, necesitas entrar en el modo de configuración global de tu *router.*

![Figura 20. Modo de configuración global. Fuente: elaboración propia.](images/image-29.png)

*Figura 20. Modo de configuración global. Fuente: elaboración propia.*

**Paso 2:** crear una ACL extendida. A continuación, crearás una ACL extendida especificando el protocolo que quieres filtrar.

![Figura 21. Crear una ACL extendida. Fuente: elaboración propia.](images/image-30.png)

*Figura 21. Crear una ACL extendida. Fuente: elaboración propia.*

Explicación: access-list 100 : inicia la creación de una ACL extendida con el número 100. deny icmp : especifica que quieres denegar el protocolo ICMP. any : indica que el tráfico puede provenir de cualquier origen. 192.168.10.0 0.0.0.255 : especifica la red de destino y la máscara *wildcard.*

**Paso 3:** permitir todo el resto del tráfico IP. Después de denegar el tráfico específico, debes permitir el resto del tráfico IP para asegurar que no bloqueas accidentalmente otro tráfico.

![Figura 22. Permitir el resto del tráfico IP. Fuente: elaboración propia.](images/image-31.png)

*Figura 22. Permitir el resto del tráfico IP. Fuente: elaboración propia.*

Explicación: permit ip : especifica que quieres permitir cualquier tráfico IP. any any : indica que el tráfico puede provenir de cualquier origen y destino.

**Paso 4:** aplicar la ACL a una interfaz.

Finalmente, aplica la ACL a una interfaz específica para que sea efectiva.

![Figura 23. Aplicar la ACL a una interfaz específica. Fuente: elaboración propia.](images/image-32.png)

*Figura 23. Aplicar la ACL a una interfaz específica. Fuente: elaboración propia.*

Explicación:

interface GigabitEthernet0/0 : entra en la configuración de la interfaz GigabitEthernet0/0. ip access-group 100 in : aplica la ACL 100 a la entrada de la interfaz, lo que significa que la ACL revisará el tráfico entrante en esa interfaz.

**▸**

- ACL extendida por puerto: queremos denegar el tráfico HTTP (puerto 80) desde la red 10.1.1.0/24 hacia cualquier destino y permitiremos todo el resto del tráfico IP.

**Paso 1:** acceder al modo de configuración global.

![Figura 24. Modo de configuración global. Fuente: elaboración propia.](images/image-33.png)

*Figura 24. Modo de configuración global. Fuente: elaboración propia.*

**Paso 2:** crear una ACL extendida.

A continuación, crearás una ACL extendida especificando el puerto que quieres

filtrar.

![Figura 25. Crear una ACL extendida. Fuente: elaboración propia.](images/image-34.png)

*Figura 25. Crear una ACL extendida. Fuente: elaboración propia.*

Explicación: access-list 101 : inicia la creación de una ACL extendida con el número 101. deny tcp : especifica que quieres denegar el protocolo TCP. 10.1.1.0 0.0.0.255 : especifica la red de origen y la máscara *wildcard.* any : indica que el tráfico puede ir a cualquier destino. eq 80 : indica que el puerto de destino es 80 (HTTP).

**Paso 3:** permitir todo el resto del tráfico IP. Después de denegar el tráfico específico, debes permitir el resto del tráfico IP para asegurar que no bloqueas accidentalmente otro tráfico.

![Figura 26. Permitir el resto del tráfico IP. Fuente: elaboración propia.](images/image-35.png)

*Figura 26. Permitir el resto del tráfico IP. Fuente: elaboración propia.*

**Paso 4:** aplicar la ACL a una interfaz. Finalmente, aplica la ACL a una interfaz específica para que sea efectiva.

**▸**

![Figura 27. Aplicar la ACL a una interfaz específica. Fuente: elaboración propia.](images/image-36.png)

*Figura 27. Aplicar la ACL a una interfaz específica. Fuente: elaboración propia.*

- ACL dinámica: imagina que deseas permitir temporalmente el tráfico SSH desde cualquier origen hacia tu red interna durante ciertas horas del día.

**Paso 1:** acceder al modo de configuración global. Primero, necesitas entrar en el modo de configuración global de tu *router.*

![Figura 28. Modo de configuración global. Fuente: elaboración propia.](images/image-37.png)

*Figura 28. Modo de configuración global. Fuente: elaboración propia.*

**Paso 2:** crea una lista de tiempo *(time-range).*

Antes de configurar la ACL dinámica, necesitas definir un período de tiempo durante el cual deseas permitir el tráfico SSH. Puedes hacerlo usando el comando «timerange».

![Figura 29. Crear una lista de tiempo. Fuente: elaboración propia.](images/image-38.png)

*Figura 29. Crear una lista de tiempo. Fuente: elaboración propia.*

En este ejemplo, se crea un período de tiempo llamado «SSH-TIME» que se repite diariamente desde las 8:00 a. m. hasta las 5:00 p. m.

**Paso 3:** crea la entrada de la ACL dinámica.

Ahora, puedes configurar la ACL dinámica para permitir el tráfico SSH durante el período de tiempo definido anteriormente. Utilizaremos el comando «access-list dynamic» para crear la entrada de la ACL dinámica.

![Figura 30. Crear la entrada de la ACL dinámica. Fuente: elaboración propia.](images/image-39.png)

*Figura 30. Crear la entrada de la ACL dinámica. Fuente: elaboración propia.*

Donde:

101 : es el número de la lista de acceso (ACL) que estamos configurando. Puedes elegir un número de ACL disponible que se ajuste a tus necesidades.

permit tcp any any eq 22 : permite el tráfico TCP (puerto SSH, puerto 22) desde cualquier origen hacia cualquier destino.

time-range SSH-TIME : especifica que esta regla de ACL dinámica solo será efectiva durante el período de tiempo definido por el «time-range SSH-TIME».

**Paso 4:** verifica y aplica la configuración.

Una vez que hayas configurado la ACL dinámica, verifica la configuración para asegurarte de que no haya errores de sintaxis. Puedes hacerlo usando el comando

«show access-lists».

![Figura 31. Verificar la configuración. Fuente: elaboración propia.](images/image-40.png)

*Figura 31. Verificar la configuración. Fuente: elaboración propia.*

Donde:

Extended IP access list 101 : indica que estamos viendo la lista de acceso extendida

número 101.

permit tcp any any eq 22 time-range SSH-TIME (dynamic) : muestra la entrada dinámica de la

ACL. Esto indica que permite el tráfico TCP (puerto SSH, puerto 22) desde cualquier origen hacia cualquier destino durante el tiempo especificado por el período de tiempo «SSH-TIME». La etiqueta «(dynamic)» indica que esta entrada es dinámica.

**Paso 5:** aplica la ACL dinámica.

Finalmente, aplica la ACL dinámica a la interfaz relevante de tu dispositivo. Por ejemplo, si deseas aplicar esta ACL en la interfaz que conecta tu red interna, puedes usar el comando «ip access-group 101 in» en la configuración de esa interfaz.

![Figura 32. Aplicar la ACL dinámica. Fuente: elaboración propia.](images/image-41.png)

*Figura 32. Aplicar la ACL dinámica. Fuente: elaboración propia.*

Después de ejecutar estos comandos, la ACL dinámica estará aplicada en la interfaz especificada y el tráfico SSH será permitido según lo configurado en la ACL durante el tiempo especificado por el período de tiempo SSH-TIME.

# Entrenamiento 5: autenticación en el servidor

# RADIUS

#### ▸ Planteamiento del ejercicio

Configura un servidor RADIUS en Packet Tracer para permitir la autenticación de un punto de acceso inalámbrico, a través de un servicio centralizado de autenticación. Para ello deberás agregar al menos dos usuarios en el servidor RADIUS con credenciales de autenticación (nombre de usuario y contraseña). Existirá un dispositivo cliente (punto de acceso inalámbrico) para autenticar a través del servidor RADIUS.

#### ▸ Desarrollo paso a paso

Deberemos tener instalado el simulador de redes Packet Tracert.

1. Configurar un servidor RADIUS en Packet Tracer con la siguiente información:

**▸**

    - Dirección IP: 192.168.0.2.

    - Máscara de subred: 255.255.255.0.

    - Clave compartida (shared secret): «secreto123».

2. Agregar al menos dos usuarios en el servidor RADIUS con credenciales de

autenticación (nombre de usuario y contraseña).

3. Configurar un dispositivo cliente (punto de acceso inalámbrico) para autenticar a

través del servidor RADIUS con la siguiente información:

**▸**

    - Dirección IP: 192.168.0.1.

    - Máscara de subred: 255.255.255.0.

4. Establecer una política de autenticación en el servidor RADIUS que permita la

autenticación de los dispositivos cliente utilizando el protocolo RADIUS.

5. Comprobar que los dispositivos cliente puedan comunicarse con el servidor

RADIUS a través de la red simulada en Packet Tracer.

#### ▸ Solución

Entramos en el Packet Tracert y añadimos los diferentes equipos necesarios para simular la instalación y los conectamos:

**▸**

- Dos equipos portátiles con la tarjeta wifi-habilitada (IP automática, por DHCP).

- Un router inalámbrico modelo WRT300N (IP: 192.168.0.1/24).

- Un switch 2960.

- Un servidor (IP: 192.168.0.2/24).

![Figura 33. Añadir los equipos necesarios. Fuente: elaboración propia.](images/image-42.png)

*Figura 33. Añadir los equipos necesarios. Fuente: elaboración propia.*

Configuramos cada uno de ellos:

**▸**

- Servidor RADIUS: para que el servidor actúe como servidor RADIUS entramos en su configuración y vamos a la pestaña *services* y accedemos a la opción AAA (autenticación, autorización y contabilidad). Aquí añadimos la IP del cliente (nuestro *router* inalámbrico) y una clave secreta (en nuestro caso «secreto123»).

![Figura 34. Configurar el servidor RADIUS. Fuente: elaboración propia.](images/image-43.png)

*Figura 34. Configurar el servidor RADIUS. Fuente: elaboración propia.*

Un poco más abajo añadiremos tantos usuarios/contraseñas como necesitemos (tantos como usuarios queremos que se conecten). En nuestro caso, como solo tenemos dos portátiles añadiremos dos usuarios.

**▸**

![Figura 35. Añadir usuarios/contraseñas. Fuente: elaboración propia.](images/image-44.png)

*Figura 35. Añadir usuarios/contraseñas. Fuente: elaboración propia.*

- Router inalámbrico: si accedemos a su configuración, en la pestaña GUI podemos configurar su dirección IP y el *pool* de direcciones que debe asignar el servidor DHCP habilitado.

![Figura 36. Configurar su dirección IP y el pool de direcciones. Fuente: elaboración propia.](images/image-45.png)

*Figura 36. Configurar su dirección IP y el pool de direcciones. Fuente: elaboración propia.*

Ahora, si accedemos a la opción *wireless* y dentro de ella, a *wireless security,* deberemos configurar el modo de seguridad como «WPA2 Enterprise» (el propio del RADIUS) y apuntar al servidor RADIUS, colocando la clave secreta configurada en este («secreto123»).

**▸**

![Figura 37. Configurar el modo de seguridad y apuntar al servidor RADIUS. Fuente: elaboración propia.](images/image-46.png)

*Figura 37. Configurar el modo de seguridad y apuntar al servidor RADIUS. Fuente: elaboración propia.*

- Equipos portátiles: ahora solo hace falta acceder a la configuración de cada equipo portátil en la pestaña «Desktop» y pinchar sobre la opción «IP Configuration» y habilitar el DHCP, también sobre la opción «PC Wireless» para conectar con el *router.* En este punto accederemos la pestaña «Connect» y refrescaremos hasta que nos aparezca la red *wireless* que tenemos configurada en el *router.*

![Figura 38. Red Wireless. Fuente: elaboración propia.](images/image-47.png)

*Figura 38. Red Wireless. Fuente: elaboración propia.*

Después pincharemos en la pestaña «Profiles» y crearemos un perfil.

![Figura 39. Crear un perfil. Fuente: elaboración propia.](images/image-48.png)

*Figura 39. Crear un perfil. Fuente: elaboración propia.*

![Figura 40. Crear un perfil. Fuente: elaboración propia.](images/image-49.png)

*Figura 40. Crear un perfil. Fuente: elaboración propia.*

![Figura 41. Crear un perfil. Fuente: elaboración propia.](images/image-50.png)

*Figura 41. Crear un perfil. Fuente: elaboración propia.*

En este punto indicaremos las credenciales del usuario (contraseña/password) que fueron añadidas en el servidor RADIUS para cada usuario.

![Figura 42. Indicar las credenciales del usuario. Fuente: elaboración propia.](images/image-51.png)

*Figura 42. Indicar las credenciales del usuario. Fuente: elaboración propia.*

![Figura 43. Indicar las credenciales del usuario. Fuente: elaboración propia.](images/image-52.png)

*Figura 43. Indicar las credenciales del usuario. Fuente: elaboración propia.*

![Figura 43. Resultado. Fuente: elaboración propia. Si ahora le damos a conectar nos aparece…](images/image-53.png)

*Figura 43. Resultado. Fuente: elaboración propia.*

Lo mismo haremos con el segundo equipo y ya tendremos creada la red con la seguridad RADIUS.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.4–32)*
- A fondo  *(pp.33–35)*
- Entrenamientos  *(pp.36–66)*
- Seguridad y Alta Disponibilidad 4 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 5 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 6 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 7 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 8 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 9 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 10 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 11 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 12 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 13 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 14 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 15 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 16 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 17 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 18 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 20 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 21 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 22 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 24 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 25 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 26 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 27 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 28 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 29 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 30 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 31 Tema 7. Material de estudio · Seguridad y Alta Disponibilidad 32 Tema 7. Material de estudio  *(pp.4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 20, 21, 22, 24, 25, 26, 27, 28, 29, 30, 31, 32)*
- Seguridad y Alta Disponibilidad 36 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 37 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 38 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 39 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 40 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 41 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 42 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 43 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 44 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 45 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 46 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 47 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 48 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 49 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 50 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 51 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 52 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 53 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 54 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 55 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 56 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 57 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 58 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 59 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 60 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 61 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 62 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 63 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 64 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 65 Tema 7. Entrenamientos · Seguridad y Alta Disponibilidad 66 Tema 7. Entrenamientos  *(pp.36–66)*