## Tema 2

# Implantación de Aplicaciones Web

# Tema 2. Instalación de servidores de aplicaciones

# web

# índice

Esquema Material de estudio

## 2.1. Introducción y objetivos

## 2.2. Análisis de requerimientos

2.3. Sistema operativo anfitrión: instalación y configuración

## 2.4. Servidor web: instalación y configuración

2.5 Sistema gestor de bases de datos: instalación y configuración

## 2.6. Procesamiento de código

2.7. Módulos y componentes necesarios

## 2.8. Utilidades de prueba e instalación integrada

## 2.9. Verificación del funcionamiento integrado

## 2.10. Documentación de la instalación

## 2.11. Referencias biliográficas

A fondo

Recomendaciones de seguridad Apache HTTP Server

Project

Documentación MySQL Workbench

Entrenamientos

Entrenamiento 1

Entrenamiento 2

Entrenamiento 3

Entrenamiento 4

Entrenamiento 5

# Esquema

![image-1](images/image-1.png)

Implantación de Aplicaciones Web 4 Tema 2. Esquema

# 2.1. Introducción y objetivos

Un servidor de aplicaciones web es un *software* que se ejecuta en un servidor y proporciona un entorno para que las aplicaciones web puedan ejecutarse. Estas aplicaciones pueden ser desde simples sitios empresariales. Los servidores de aplicaciones

web hasta complejos sistemas se encargan de gestionar las

solicitudes de los usuarios, procesarlas y generar las respuestas correspondientes, todo de manera eficiente y segura, según la rendimiento del hardware donde estén alojados.

configuración del entorno y el

Los objetivos principales que queremos conseguir con el estudio de este tema son:

**▸** Explicar de manera clara y concisa qué es un servidor de aplicaciones web, cómo funciona y cuál es su papel en el desarrollo de aplicaciones web.

**▸** Presentar los diferentes tipos de servidores de aplicaciones web existentes (Java EE, NET, Node.js, etc.) y sus características.

**▸** Detallar la arquitectura típica de un servidor de aplicaciones web, incluyendo los componentes clave y sus interacciones.

**▸** Resolver problemas comunes relacionados con servidores de aplicaciones web.

# 2.2. Análisis de requerimientos

El análisis de requerimientos es un paso crucial en cualquier proyecto de instalación de servidores de aplicaciones web. Establece las bases para garantizar que el sistema final cumpla con las necesidades específicas del negocio y los usuarios. Este análisis es un proceso detallado para identificar, documentar y comprender todos los aspectos que influyen en la instalación del servidor, que son los siguientes:

**▸ Funcionalidades:** ¿qué tareas va a realizar el servidor? ¿Qué aplicaciones se ejecutarán? ¿Qué interacción tendrán los usuarios?

**▸ Rendimiento:** ¿qué volumen de tráfico se espera?

**▸ Disponibilidad:** ¿cuál es el porcentaje de tiempo que la aplicación debe estar disponible? ¿Qué medidas se tomarán para garantizar la continuidad del servicio en caso de fallos?

**▸ Escalabilidad:** ¿qué previsiones futuras de demanda puede haber?

**▸ Seguridad:** ¿qué niveles de protección se necesitan para los datos y las aplicaciones? ¿Qué configuraciones base serán necesarias?

**▸ Integración:** ¿cómo se integrará el servidor con otros sistemas existentes? ¿Qué protocolos de comunicación se utilizarán?

**▸ Mantenimiento:** ¿qué herramientas y procedimientos se necesitarán para administrar y mantener el servidor a largo plazo?

**▸ Hardware:** ¿usaremos un servidor físico, virtual o en la nube? ¿Qué potencia de proceso necesitaremos, memoria RAM y de almacenamiento?

**▸ Software:** ¿qué sistema operativo usaremos? ¿Qué servidor web instalaremos (Apache, Nginx, IIS)? ¿Qué lenguaje se utilizará para desarrollar la aplicación (PHP, Python, Java, etc.)? ¿Qué base de datos se utilizará (MySQL, PostgreSQL, MongoDB)?

Si queremos realizar un análisis de requerimientos efectivo, debemos tener en cuenta los siguientes aspectos:

**▸** Involucra a todas las partes interesadas, desde los usuarios finales hasta los administradores del sistema.

**▸** Recopilar la mayor información posible utilizando técnicas como entrevistas, encuestas, talleres y análisis de documentos para obtener una comprensión profunda de las necesidades.

**▸** Crear una lista detallada y organizada de todos los requisitos utilizando un formato claro y conciso.

**▸** Clasificar los requisitos según su importancia y urgencia para ayudar a tomar decisiones sobre la implementación.

**▸** Verificar que los requisitos sean los necesarios, comprensibles y consistentes.

Herramientas que nos ayudan en la gestión de requerimientos

**▸** Diagramas de flujo para la visualización de los procesos y las interacciones entre los diferentes componentes del sistema.

**▸** Matrices de rastreabilidad/trazabilidad para vincular los requisitos con los objetivos y las pruebas.

![image-2](images/image-2.png)

Tabla 1. Matriz de trazabilidad. Fuente: elaboración propia.

Un análisis de requisitos bien estructurado es la base para un proyecto exitoso. Al identificar y documentar todas las necesidades de manera clara y concisa se evita la aparición de problemas inesperados durante el desarrollo y se garantiza que el servidor de aplicaciones web cumpla con las expectativas planteadas.

Ejemplo de **requerimientos** para una **aplicación de gestión de contenidos** (CMS):

**▸** Funcionalidades:

- Creación y edición de contenido (páginas, blog posts, etc.).

- Gestión de usuarios y permisos.

- Diseño de plantillas y personalización de la apariencia.

- Integración con plugins y módulos.

**▸** No funcionales:

- Facilidad de uso para usuarios no técnicos.

- Seguridad para proteger el contenido del sitio web.

- Optimización para motores de búsqueda (SEO).

- Escalabilidad para gestionar sitios web de gran tamaño.

**▸** Específicos:

- Multiidioma para llegar a una audiencia global.

- Integración con herramientas de análisis web.

# 2.3. Sistema operativo anfitrión: instalación y configuración

El **sistema operativo anfitrión** (también conocido como sistema operativo base) es la base sobre la que se construye todo un servidor de aplicaciones web. Es el *software* que gestiona los recursos de *hardware* (CPU, memoria, disco duro, red) y proporciona un entorno en el que pueden ejecutarse otras aplicaciones, como el servidor web, la base de datos y la propia aplicación web.

La elección del sistema operativo anfitrión es una decisión crucial que influirá en:

**▸ Estabilidad:** garantiza un funcionamiento continuo y minimiza los tiempos de inactividad.

**▸ Seguridad:** protege el servidor de ataques externos y garantiza la integridad de los datos.

**▸ Rendimiento:** mejora el rendimiento de las aplicaciones y reduce los tiempos de respuesta.

**▸ Compatibilidad:** el SO debe ser compatible con el *software* que se va a instalar (servidor web, base de datos, lenguajes de programación, etc.).

**▸ Fácil administración:** reduce los costes de mantenimiento.

Factores para considerar cuando elegimos un sistema operativo

Debemos tener en cuenta que algunas aplicaciones pueden tener **requisitos** **específicos** para su ejecución, como puede ser el sistema operativo. Además, hay aplicaciones grandes y complejas, que es recomendable alojar en un **SO estable y** **escalable.** Los **costos de las licencias y el soporte técnico,** pueden variar significativamente entre los diferentes sistemas operativos, así como el **trabajo de** **administración,** que puede necesitar en algunos casos de mayor experiencia y esfuerzo del administrador del sistema.

Los sistemas operativos más comunes para servidores de aplicaciones web son:

**▸ Linux.**

- Ventajas: alta estabilidad, seguridad, rendimiento, gran comunidad de usuarios, *software* libre y de código abierto. Tiene distribuciones muy populares, como Ubuntu, CentOS, Debian, Fedora.

- Inconvenientes: posible falta de soporte en algunas distribuciones menos populares.

#### ▸ Windows

- Ventajas: fácil integración con otras tecnologías de Microsoft, interfaz gráfica intuitiva.

- Inconvenientes: costo de las licencias, menor rendimiento en comparación con Linux para mucha carga de trabajo.

#### ▸ macOS

- Ventajas: estabilidad, seguridad, integración con otros productos de Apple.

- Inconvenientes: menor cuota de mercado, costo elevado.

Proceso de instalación resumido de Linux, Windows y macOS

#### Linux

Ofrece una amplia variedad de distribuciones (distros), cada una con su propio enfoque y apariencia.

**▸** **▸** **▸** **▸** **▸** **Descarga de la ISO:** elige una distribución que se adapte a tus necesidades.

**Crea un medio de instalación:** generalmente se utiliza una unidad USB. Podemos usar la herramienta Rufus para crear el medio desde la ISO descargada.

**Inicio desde el USB:** reinicia tu computadora y configura la BIOS para arrancar desde el USB o medio elegido.

**Instalador:** sigue las instrucciones del instalador seleccionando el idioma, la distribución del teclado, la partición donde se instalará y otros ajustes.

**Reinicio:** una vez finalizada la instalación, reinicia tu computadora para iniciar Linux.

#### Windows

La popular interfaz gráfica es muy reconocible y amigable para los usuarios más novatos.

**▸** **▸** **▸** **Medio de instalación:** generalmente se utiliza un DVD o una unidad USB con la imagen de instalación de Windows. Lo podemos crear con la herramienta de Microsoft, Media Creation Tool desde un equipo que ya tenga el SO.

**Inicio desde el medio:** reinicia tu computadora y configura la BIOS para arrancar desde USB u otro medio (DVD, red, etc.).

**Instalador:** sigue las instrucciones del instalador seleccionando el idioma, la hora y formato, la distribución del teclado y la partición donde se instalará Windows.

**▸ Activación:** una vez finalizada la instalación, necesitarás una clave de producto para activar Windows.

**▸ Actualizaciones:** Windows se actualiza automáticamente para corregir errores y agregar nuevas funciones.

#### MacOS

Es el sistema operativo exclusivo diseñado para los equipos de *hardware* Apple (Mac).

**▸ Instalación desde el Mac App Store:** la forma más común de instalar macOS en un equipo Apple:

**▸ Reinstalación desde una copia de seguridad:** si tenemos una copia de seguridad de tu Mac, puedes restaurar el sistema operativo.

**▸ Instalación limpia:** para realizar una instalación limpia, necesitarás un instalador de macOS en una unidad USB.

**▸ Asistente de instalación:** sigue las instrucciones del asistente de instalación seleccionando el idioma, la región y la partición donde se instalará macOS.

Instalación dual o múltiple

Si queremos tener varios sistemas operativos en tu computadora, puedes realizar una instalación dual o múltiple. Esto implica crear particiones en tu disco duro y asignar una partición a cada sistema operativo.

Los sistemas operativos que instalemos para alojar nuestro servidor web no tienen que ser la versión *server* obligatoriamente, simplemente deben tener conectividad de red. El servidor web dará todas las funcionalidades necesarias para el funcionamiento de las aplicaciones web alojadas.

#### Configuración del sistema operativo

La configuración del sistema operativo es un paso crucial antes de instalar un servidor de aplicaciones web. Esta configuración garantiza que el entorno sea óptimo para el funcionamiento de las aplicaciones y los servicios asociados.

Una vez instalado el sistema operativo anfitrión debemos realizar una serie de tareas de configuración, y así tener un entorno adecuado para la explotación de aplicaciones web. Las tareas principales por realizar son:

**▸ Actualización del sistema** mediante la instalación de las últimas actualizaciones de seguridad y *software.*

**▸ Configuración de la red:** lo más importante es la interfaz de red (IP fija para acceder desde la red al puerto 80-HTTP), el DNS *(domain name system)* y el *firewall* (aplicando las reglas adecuadas a nuestros propósitos de control de acceso).

**▸ Creación de usuarios** con los permisos y roles adecuados para la administración de nuestro servidor.

**▸ Optimización del sistema:** desactivaremos los servicios innecesarios y ajustaremos los parámetros del kernel a las necesidades reales de nuestro proyecto. Estos ajustes son de gran importancia y requieren conocimientos avanzados, solo se deben hacer si estamos completamente seguros de lo que implica y tenemos una copia de seguridad del sistema.

**▸ Instalación del** ***software*** **esencial,** como pueden ser el servidor web, el servidor de base de datos, los intérpretes de los lenguajes de programación que vayamos a utilizar y las herramientas de administración que sean necesarias para nuestro proyecto.

Ejemplo de configuración Ubuntu/Debian (Bash)

# Actualizar listas de paquetes sudo apt update

# Instalar Apache, MySQL y PHP sudo apt install apache2 mysql-server php libapache2-mod-php # Configurar Apache sudo nano /etc/apache2/apache2.conf

# Configurar MySQL sudo mysql_secure_installation;

# 2.4. Servidor web: instalación y configuración

Un servidor web es un programa que se ejecuta en un equipo de proceso u ordenador **(servidor)** y permite que otros ordenadores **(clientes)** accedan a archivos alojados en él desde una red, como Internet. El servidor ofrece réplicas exactas a cada petición de los clientes. Estas réplicas pueden ser de archivos como documentos web, imágenes, vídeos, aplicaciones y otros formatos.

Existen numerosos servidores web, cada uno con sus propias características y ventajas. Algunos de los más populares son:

Apache

Es el servidor web más utilizado en el mundo, de código abierto y altamente configurable. Ofrece una gran estabilidad y compatibilidad con diversos sistemas operativos, como Windows y Linux. Este servidor web está integrado en la arquitectura de desarrollo web **LAMP,** que es un acrónimo que recoge un conjunto de tecnologías de *software* de código abierto, ampliamente utilizado para construir servidores web dinámicos y aplicaciones web. LAMP corresponde con:

**▸ Linux:** sistema operativo de código abierto, conocido por su estabilidad, seguridad y flexibilidad.

**▸ Apache:** un servidor web de alto rendimiento, que se encarga de recibir las solicitudes de los clientes (navegadores) y enviarles las páginas web correspondientes.

**▸ MySQL:** un sistema de gestión de bases de datos relacionales, utilizado para almacenar y gestionar la información de la aplicación web.

**▸ PHP:** un lenguaje de programación del lado del servidor, empleado para crear el contenido dinámico de las páginas web.

#### ¿Cuál es el funcionamiento de la arquitectura LAMP?

**▸ El cliente (navegador) envía una solicitud:** cuando un usuario escribe una dirección web en su navegador y presiona Enter, se envía una solicitud al servidor.

**▸ Apache recibe la solicitud:** el servidor web recibe esta solicitud y la procesa.

**▸ PHP genera el contenido dinámico:** si la página solicitada requiere contenido dinámico (por ejemplo, datos de una base de datos), Apache pasa la solicitud a PHP, que se conecta con MySQL, obtiene los datos necesarios y genera el código HTML de la página.

**▸ Apache envía la respuesta al cliente:** una vez que PHP ha generado el HTML, Apache lo envía al navegador del usuario, quien lo interpreta y muestra la página web.

Nginx

Conocido por su alto rendimiento y eficiencia en el manejo de un gran número de conexiones simultáneas. Es ideal para sitios web con mucho tráfico y aplicaciones que requieren baja latencia. En la arquitectura, **LEMP** sustituye a Apache como servidor web Nginx (según la pronunciación, *engine x).* El resto de las tecnologías de esta arquitectura son las mismas que en LAMP.

Microsoft IIS

Desarrollado por Microsoft, es el servidor web más utilizado en entornos Windows.

Ofrece una estrecha integración con otras tecnologías de Microsoft.

LiteSpeed

Un servidor web comercial que destaca por su velocidad y capacidad para manejar

cargas de trabajo pesadas.

Lighttpd

Un servidor web ligero y rápido diseñado para entornos con recursos limitados.

Hay otra arquitectura de servidor web, además de **LAMP, LEMP** y otras menos populares, como **WAMP** y **MAMP,** que se ha popularizado debido al crecimiento en uso del lenguaje Javascript y los innumerables *frameworks* para web, que se han desarrollado teniendo este lenguaje de programación como base, tanto en el servidor como el cliente. Esta arquitectura basada enteramente en Javascrip, es conocida como **MEAN,** que es el acrónimo de las siguientes herramientas:

**▸ MongoDB:** una base de datos NoSQL, altamente flexible y escalable, que almacena datos en formato JSON en sistema binario (BSON).

**▸ Express.js:** un *framework* de aplicaciones web para Node.js, ligero y rápido, que proporciona un conjunto de características para crear aplicaciones web y API *(application programming interface).*

**▸ Angular:** un *framework* de *front-end* en JavaScript, potente y versátil, utilizado para crear aplicaciones web de una sola página (SPA, *single page application),* ricas en características.

**▸ Node.js:** un entorno de ejecución que permite ejecutar código JavaScript fuera de un navegador web, proporcionando un servidor web ligero y eficiente.

Instalación de un servidor web con XAMPP

La instalación aislada de Apache es bastante compleja y se requieren conocimientos técnicos avanzados. Normalmente, la instalación de este servidor web se realiza mediante la instalación conjunta de herramientas denominadas XAMPP (Apache Friends), mucho más amigable y eficiente.

![Figura 1. Búsqueda de XAMPP en Google. Fuente: elaboración propia.](images/image-3.png)

*Figura 1. Búsqueda de XAMPP en Google. Fuente: elaboración propia.*

Pulsamos en el menú, la opción «Descargar».

![Figura 2. Cómo descargar XAMPP. Fuente: Apache Friends, s. f.](images/image-4.png)

*Figura 2. Cómo descargar XAMPP. Fuente: Apache Friends, s. f.*

En este caso vamos a descargar la versión para Windows 8.0.30/PHP 8.0.30 y pulsamos el botón «Descargar (64 bit)» de esta versión. La descarga comenzará luego de pulsar el botón, pero, si surge algún problema, pulsaremos en «Haz clic aquí» para acceder al servidor de descargas de SOURCEFORGE, donde encontraremos todos los instaladores de todas las versiones de XAMPP.

Una vez descargado el archivo de instalación, haremos doble clic sobre él y comenzará la instalación. El primer mensaje que nos dará XAMPP es un aviso de seguridad para que estemos alerta sobre la configuración de permisos y acceso a usuarios (UAC).

![Figura 3. Aviso de seguridad de XAMPP. Fuente: elaboración propia.](images/image-5.png)

*Figura 3. Aviso de seguridad de XAMPP. Fuente: elaboración propia.*

Si aceptamos, comenzará la instalación de XAMPP y pulsaremos «Siguiente» en el Setup XAMPP. Pasando a la siguiente pantalla, donde se muestra que vamos a instalar (más adelante hablaremos de todos los componentes y módulos de XAMPP).

![Figura 4. Setup XAMPP. Fuente: elaboración propia.](images/image-6.png)

*Figura 4. Setup XAMPP. Fuente: elaboración propia.*

Como queremos instalar todos los componentes, pulsaremos «Next» y nos informará de aspectos de la configuración de instalación (en el directorio de instalación es aconsejable dejar la ubicación por defecto C:\xampp y el lenguaje del instalador, solo disponible en inglés y alemán).

![Figura 5. Instalación de XAMPP. Fuente: elaboración propia.](images/image-7.png)

*Figura 5. Instalación de XAMPP. Fuente: elaboración propia.*

Una vez realizadas las correspondientes elecciones, empezará la instalación luego de confirmar que queremos comenzar.

![Figura 6. Instalación de XAMPP. Fuente: elaboración propia.](images/image-8.png)

*Figura 6. Instalación de XAMPP. Fuente: elaboración propia.*

Cuando la barra de progreso llegue a la derecha, tendremos todos los componentes de XAMPP en nuestro equipo, y confirmaremos con «Finish».

![Figura 7. Instalación de XAMPP completada. Fuente: elaboración propia.](images/image-9.png)

*Figura 7. Instalación de XAMPP completada. Fuente: elaboración propia.*

Una vez confirmada la finalización de la instalación, aparecerá ante nosotros el famoso panel de control de XAMPP, con todas las opciones de inicio de servicios, configuración y control de errores.

![Figura 8. Panel de control de XAMPP. Fuente: elaboración propia.](images/image-10.png)

*Figura 8. Panel de control de XAMPP. Fuente: elaboración propia.*

Desde el panel de control podemos arrancar los módulos disponibles como, por ejemplo, el servidor Apache. Procedemos a pulsar «Start» y observamos cómo se inicia el servidor y se queda con el estatus *running* ('corriendo'). Vemos, también, que los puertos en los que está activo son el 80 HTTP, o servicio web, y el 443 HTTPS dedicado al envío y recepción de paquetes cifrados.

![Figura 9. Panel de control de XAMPP. Fuente: elaboración propia.](images/image-11.png)

*Figura 9. Panel de control de XAMPP. Fuente: elaboración propia.*

Si pulsamos sobre el botón «Admin» del módulo Apache activo veremos que automáticamente se abre el navegador por defecto del equipo y nos muestra, en su barra de navegación, la URL («localhost/dashboard»). Esta dirección corresponde con el contenido alojado en carpeta «C:\xampp\htdocs» (directorio correspondiente al servidor web).

![image-12](images/image-12.png)

![Figura 10. Navegador por defecto de XAMPP. Fuente: Apache Friends, s. f.](images/image-13.png)

*Figura 10. Navegador por defecto de XAMPP. Fuente: Apache Friends, s. f.*

Todas las carpetas y archivos alojados en el directorio htdocs pueden ser llamadas desde una URL en el navegador. Si solamente indicamos una carpeta, automáticamente se lanzará el archivo con nombre index.html o index.php , que esté alojado en su interior.

Localhost corresponde a la IP 127.0.0.1, que se puede poner en la barra de navegación directamente y tendrá el mismo efecto que si utilizamos localhost.

![Figura 11. Navegador por defecto de XAMPP. Fuente: elaboración propia.](images/image-14.png)

*Figura 11. Navegador por defecto de XAMPP. Fuente: elaboración propia.*

# 2.5 Sistema gestor de bases de datos: instalación y

# configuración

En la instalación de XAMPP van incluidos diferentes módulos útiles y necesarios donde se incluye el sistema gestor de bases de datos MariaDB (versión de código abierto creada desde un *fork* del proyecto MySQL, para garantizar la existencia libre del sistema, cuando Oracle adquirió MySQL en 2009). El SGBD ya está incluido y no es necesario realizar ninguna instalación adicional a la de XAMPP.

Si activamos MySQL en el panel de control, veremos que el servicio de base de datos está activo en el puerto 3306, aunque podemos cambiarlo sin ningún problema, simplemente haciendo clic en el botón «Config» correspondiente y editando el fichero my.ini (para la configuración de SGBD) que aparece.

![Figura 12. MySQL activado en el panel de control de XAMPP. Fuente: elaboración propia.](images/image-15.png)

*Figura 12. MySQL activado en el panel de control de XAMPP. Fuente: elaboración propia.*

Si cambiamos el port=3306 , en los dos lugares que vemos en el texto resaltado, por el puerto que necesitemos, por ejemplo, port=3350 , veremos que ese puerto es el que tomará MySQL para estar activo.

![Figura 13. Cambio de port=3306. Fuente: elaboración propia.](images/image-16.png)

*Figura 13. Cambio de port=3306. Fuente: elaboración propia.*

Si queremos instalar otro sistema gestor de bases de datos, por ejemplo PostgreSQL, simplemente seguiremos el siguiente proceso y podremos utilizarlo en el desarrollo de nuestras aplicaciones web (estará disponible en el puerto 5432 del localhost, para poder acceder a él con el lenguaje de servidor que estemos usando, por ejemplo PHP).

Descarga del instalador:

**▸** Visita la [página oficial de PostgreSQL](https://www.postgresql.org/download/windows/).

**▸** Selecciona la versión más reciente y adecuada para tu sistema.

**▸** Descarga el instalador.

Ejecución del instalador: **▸** Haz doble clic en el archivo descargado para iniciar el asistente de instalación. **▸** Sigue las instrucciones del asistente:

- Selecciona la carpeta de instalación.

- Elige los componentes que deseas instalar (servidor, pgAdmin, etc.).

- Establece una contraseña para el usuario postgres.

- Define el puerto de escucha (por defecto, 5432).

- Selecciona la localización (locale) para el clúster de la base de datos.

Configuración inicial: **▸** Una vez finalizada la instalación, puedes acceder a pgAdmin para administrar tus bases de datos desde el navegador. **▸** Crea una nueva base de datos y usuarios según tus necesidades. **▸** Configura los parámetros de conexión y seguridad.

# 2.6. Procesamiento de código

El procesamiento de código en un servidor Apache depende, en gran medida, del tipo de código que se esté ejecutando. Apache, por sí mismo, se encarga principalmente de servir contenido estático (HTML, CSS, imágenes, etc.) y manejar solicitudes HTTP. Sin embargo, con la ayuda de módulos y tecnologías adicionales puede procesar una variedad de lenguajes de programación y *scripts.*

Procesamiento de código en Apache

**▸ PHP:** uno de los lenguajes más populares para el desarrollo web del lado del servidor. Apache utiliza el módulo mod_php para interpretar y ejecutar *scripts* PHP. El código PHP se incrusta dentro de archivos HTML y se procesa en el servidor antes de enviar la salida al navegador del cliente.

**▸ Perl y Python:** otros lenguajes de *scripting* que se pueden ejecutar en Apache a través de módulos como mod_perl y mod_python . Estos módulos permiten una integración más estrecha del lenguaje con el servidor, lo que puede mejorar el rendimiento en comparación con la ejecución de *scripts* CGI.

**▸ CGI** ***(common gateway interface):*** un protocolo estándar que permite a Apache ejecutar cualquier programa externo como un *script.* Esto proporciona flexibilidad para usar cualquier lenguaje de programación, pero puede ser menos eficiente que los módulos específicos del lenguaje.

**▸ Java (a través de Tomcat o similar):** Apache puede actuar como un servidor web frontal para un contenedor de *servlets* Java, como Tomcat. Tomcat se encarga de procesar el código Java (servlets, JSP) y Apache maneja las solicitudes HTTP y el envío de contenido estático.

**▸ Node.js:** aunque Node.js tiene su propio servidor web incorporado, se puede configurar para ejecutarse detrás de Apache utilizando mod_proxy . Esto permite aprovechar las capacidades de Apache para servir contenido estático y balanceo de carga, mientras que Node.js maneja la lógica del lado del servidor.

Procesamiento código PHP

Volvemos a nuestro ejemplo inicial: donde teníamos un fichero llamado index.php alojado en la ubicación C:\xampp\htdocs\webprueba vamos a incluir un *script* de PHP, para que veamos su ejecución en el servidor web a través del navegador.

El código que vamos a incluir en el archivo es el siguiente:

![Figura 14. Código incluido en el archivo. Fuente: elaboración propia.](images/image-17.png)

*Figura 14. Código incluido en el archivo. Fuente: elaboración propia.*

Podemos ver el código PHP dentro del script <?php …. ?> y lo que hace es mostrar, mediante un comando echo **,** una línea de **HTML** con **CSS** centrando el contenido de la etiqueta H3 y poniendo la fuente en color rojo.

Para ver el resultado, llamaremos a la URL del servidor para que ejecute y muestre el fichero index.php . Escribiremos en el navegador «localhost/webprueba/» y al pulsar Enter obtendremos el siguiente resultado:

![Figura 15. Resultado de escribir localhost/webprueba. Fuente: elaboración propia.](images/image-18.png)

*Figura 15. Resultado de escribir localhost/webprueba. Fuente: elaboración propia.*

Si pulsamos «Stop» en Apache, en el panel de control de XAMPP, y quisiéramos ejecutar otra vez lo anterior, obtendremos el siguiente resultado.

![Figura 16. Resultado al pulsar «Stop» en Apache. Fuente: elaboración propia.](images/image-19.png)

*Figura 16. Resultado al pulsar «Stop» en Apache. Fuente: elaboración propia.*

# 2.7. Módulos y componentes necesarios

Un servidor web Apache requiere varios módulos y componentes para funcionar correctamente. Estos se pueden clasificar de la siguiente forma:

Componentes esenciales

**▸ HTTPD (núcleo de Apache):** es el corazón del servidor, responsable de manejar las solicitudes HTTP y entregar contenido.

Módulos de multiprocesamiento (MPM)

Controlan cómo Apache maneja las conexiones y solicitudes concurrentes. Algunos

MPM comunes son:

**▸ prefork:** crea un nuevo proceso para cada conexión.

**▸ worker:** utiliza un modelo híbrido de procesos y subprocesos.

**▸ event:** similar a *worker,* pero más eficiente en el manejo de conexiones persistentes.

Módulos básicos

Proporcionan funcionalidades esenciales como:

**▸ mod_so:** permite cargar módulos dinámicamente.

**▸ mod_mime:** asocia extensiones de archivo con tipos MIME.

**▸ mod_dir:** maneja la navegación de directorios.

**▸ mod_log_config:** configura el registro de acceso y errores.

Módulos adicionales recomendados

**▸ mod_rewrite:** permite reescribir URL, útil para SEO y mantenimiento de sitios. **▸ mod_ssl:** habilita el soporte para HTTPS, esencial para la seguridad. **▸ mod_headers:** permite manipular cabeceras HTTP. **▸ mod_deflate:** comprime el contenido antes de enviarlo, lo que mejora el rendimiento. **▸ mod_expires:** controla el almacenamiento en caché del contenido en los navegadores. **▸ mod_security:** agrega una capa de seguridad contra ataques comunes.

Otros componentes para elegir

**▸ PHP** (u otro lenguaje de *scripting):* si planeas ejecutar aplicaciones web dinámicas. **▸ MySQL** (u otro sistema gestor de bases de datos): para almacenar y recuperar datos. **▸ Firewall:** protege el servidor de accesos no autorizados. El fichero principal de configuración del servidor Apache y núcleo de este, como ya hemos citado anteriormente, es el fichero httpd.conf , para acceder a su edición debemos hacer clic en el botón «Config» de Apache y veremos que aparece en el primer lugar de la lista. Al pulsar sobre él, se editará un fichero con el siguiente contenido.

![Figura 17. Resultado al pulsar «Stop» en Apache. Fuente: elaboración propia.](images/image-20.png)

*Figura 17. Resultado al pulsar «Stop» en Apache. Fuente: elaboración propia.*

El fichero nos recuerda que es el fichero principal de configuración de Apache y consultemos la documentación disponible en las URL de documentación del sitio oficial, ya que debemos tener claro lo que queremos hacer y ver cómo hacerlo en la documentación oficial.

A través del siguiente enlace podrás acceder a la documentación de la versión 2.4 del servidor HTTP Apache (Apache, s. f. a):

[https://httpd.apache.org/docs/2.4/](https://httpd.apache.org/docs/2.4/)

A través del siguiente enlace podrás acceder al índice de directivas de la versión 2.4 del servidor HTTP Apache (Apache, s. f. b):

[https://httpd.apache.org/docs/2.4/mod/directives.html](https://httpd.apache.org/docs/2.4/mod/directives.html)

Todos los módulos se pueden habilitar y deshabilitar en este fichero, como vemos en la siguiente imagen, ya que al quitar la # de una línea se procederá a cargar o hacer la acción que indica la línea que estaba comentada.

![Figura 18. Resultado al pulsar «Stop» en Apache. Fuente: elaboración propia.](images/image-21.png)

*Figura 18. Resultado al pulsar «Stop» en Apache. Fuente: elaboración propia.*

# 2.8. Utilidades de prueba e instalación integrada

XAMPP, como paquete de servidor local, incluye una serie de utilidades que facilitan tanto la instalación como las pruebas de tus proyectos web. A continuación, vamos a ver las más importantes:

Utilidades de instalación

#### Instalador

El propio instalador de XAMPP simplifica el proceso de configuración en tu sistema. Te guía paso a paso permitiéndote elegir los componentes que deseas instalar (Apache, MySQL, PHP, etc.) y la ubicación en tu disco.

#### Panel de control

Una vez instalado, el panel de control de XAMPP te brinda una interfaz gráfica para iniciar, detener y reiniciar los distintos servicios (Apache, MySQL) de forma sencilla. También te permite acceder a configuraciones y registros importantes.

Utilidades de prueba

#### Servidor web Apache

Te permite alojar tus sitios web y aplicaciones localmente, esto ofrece un entorno de producción real, ya que puedes tener todas las funcionalidades que ofrecería un servidor web, accesible desde una IP asignada en la red. Puedes acceder a ellos a través de tu navegador web utilizando «<http://localhost»> o «<http://127.0.0.1»>.

#### Servidor de base de datos MySQL/MariaDB

Te proporciona un sistema de gestión de bases de datos para almacenar y recuperar la información de tus aplicaciones web. Puedes interactuar con él a través de herramientas como phpMyAdmin (incluida en XAMPP) o directamente desde tus *scripts* PHP.

#### Intérprete de PHP

Permite ejecutar tus *scripts* PHP en el servidor, lo que genera contenido dinámico para tus páginas web.

#### phpMyAdmin

Es una interfaz web intuitiva para administrar tus bases de datos MySQL/MariaDB. Te permite crear, modificar y eliminar bases de datos, tablas, registros, etc., sin necesidad de escribir consultas SQL complejas. Para esta gestión y administración del servidor de bases de datos, también hay otras herramientas mucho más potentes, como, por ejemplo, MySQL Workbench o pgAdmin para PostgreSQL.

#### FileZilla FTP Server

Es un servidor FTP para simular la transferencia de archivos a un servidor remoto, útil para probar funcionalidades de subida y descarga en tus archivos y proyectos.

#### Mercury Mail

Se trata de un servidor de correo local para probar el envío y recepción de correos electrónicos desde tus aplicaciones web.

#### Tomcat

Es un servidor de aplicaciones Java para desplegar y probar aplicaciones web desarrolladas en ese lenguaje de programación.

# 2.9. Verificación del funcionamiento integrado

Vamos a verificar el funcionamiento de los módulos de XAMPP con el siguiente procedimiento paso a paso para asegurarte de que todo está funcionando correctamente:

Iniciar XAMPP

**▸** Abre el panel de control de XAMPP.

**▸** Inicia los módulos necesarios:

- Apache: sirve páginas web.

- MySQL: gestiona bases de datos.

- FileZilla: si necesitas transferencia de archivos (opcional).

**▸** Asegúrate de que los módulos se inician sin errores, escuchan por el puerto

correspondiente y se muestran en verde.

Verificar Apache

**▸** Abre tu navegador web. **▸** Escribe «<http://localhost»> en la barra de direcciones. **▸** Deberías ver la página de bienvenida de XAMPP. Si es así, ¡Apache funciona! **▸** Puedes crear un archivo index.html o index.php simple en la carpeta htdocs de XAMPP para probarlo aún más.

Verificar MySQL

**▸** Abre phpMyAdmin. **▸** En el panel de control de XAMPP haz clic en el botón «Admin» junto a MySQL.

**▸** Deberías ver la interfaz de phpMyAdmin. **▸** Intenta crear una base de datos simple o una tabla para confirmar que MySQL funciona.

Verificar FileZilla (si está activo)

**▸** Abre FileZilla. **▸** Intenta conectarte a tu servidor local usando localhost como *host,* el usuario y contraseña que configuraste durante la instalación de XAMPP. **▸** Si puedes conectarte y navegar por los archivos, FileZilla funciona correctamente.

Probar la interacción entre módulos

**▸** Crea un *script* PHP simple (por ejemplo, test.php ) en la carpeta htdocs que se conecte a la base de datos MySQL y muestra algunos datos. En próximos temas realizaremos la conexión con bases de datos, para extraerles información. **▸** Accede a este *script* desde tu navegador: «<http://localhost/test.php»>. **▸** Si el *script* se ejecuta y muestra los datos de la base de datos, ¡la integración entre Apache, MySQL y PHP funciona!

Verificaciones adicionales

**▸** Verifica el registro de errores. **▸** Si encuentras algún problema, consulta los archivos de registro de Apache y MySQL en la carpeta logs de XAMPP (accesibles desde los botones «Logs» del panel de control) **▸** *Firewall* y antivirus. **▸** Asegúrate de que tu *firewall* o antivirus no estén bloqueando los puertos que XAMPP necesita. **▸** Actualizaciones. **▸** Mantén XAMPP y sus módulos actualizados para evitar problemas de compatibilidad y seguridad.

# 2.10. Documentación de la instalación

XAMPP es un paquete de *software* gratuito y de código abierto que te permite crear un servidor web local en tu computadora. Incluye Apache (servidor web), MariaDB (base de datos), PHP (lenguaje de programación) y Perl (otro lenguaje de programación). Es una herramienta muy popular entre desarrolladores web para probar sus sitios y aplicaciones antes de subirlos a un servidor en línea.

Descarga XAMPP

**▸** Visita el sitio web oficial de Apache Friends:

Accede a la web desde el siguiente enlace:

[https://www.apachefriends.org/es/index.html](https://www.apachefriends.org/es/index.html)

**▸** Haz clic en el botón de descarga correspondiente a tu sistema operativo (Windows, Linux o macOS).

Ejecuta el instalador

#### Windows

**▸** Haz doble clic en el archivo .exe descargado.

**▸** Es posible que aparezca una advertencia de seguridad de Windows. Haz clic en «Sí» o «Permitir» para continuar.

**▸** Sigue las instrucciones del asistente de instalación. Puedes aceptar la configuración predeterminada en la mayoría de los casos.

#### Linux

**▸** **▸** **▸** **▸** **▸**

Abre una terminal.

Navega hasta la carpeta donde descargaste el archivo .run (por ejemplo, cd

Descargas ).

Otorga permisos de ejecución al archivo: chmod +x xampp-linux-x64-....run

Ejecuta el instalador: sudo ./xampp-linux-x64-....run

Sigue las instrucciones en pantalla.

#### macOS

**▸** **▸** **▸** **▸**

Haz doble clic en el archivo .dmg descargado.

Arrastra el icono de XAMPP a la carpeta Aplicaciones .

Abre la carpeta Aplicaciones y haz doble clic en XAMPP para iniciar el gestor.

Inicia XAMPP.

#### Windows

**▸** **▸**

#### Linux

**▸** **▸**

Busca «XAMPP Control Panel» en el menú de inicio y ábrelo.

Haz clic en los botones «Start» junto a «Apache» y «MySQL» para iniciar los

servicios.

Abre una terminal. Ejecuta sudo/opt/lampp/lampp start para iniciar XAMPP.

#### macOS

- ▸ En el gestor de XAMPP, haz clic en «Manage Servers» y luego en «Start All» para

    - iniciar los servicios.

- ▸ Verifica la instalación:

- Abre tu navegador web favorito.

- Escribe «localhost» en la barra de direcciones y presiona Enter.

- Deberías ver la página de bienvenida de XAMPP. ¡Felicidades, XAMPP está instalado correctamente!

Notas para tener en cuenta

**▸** Durante la instalación es posible que se te pregunte si deseas agregar XAMPP a tu

PATH. Si no estás seguro, puedes dejar esta opción desmarcada.

**▸** Si tienes un *firewall* activo, es posible que necesites permitir el acceso a Apache y

MySQL a través de él.

**▸** La carpeta principal donde se almacenarán tus archivos web se llama htdocs y se encuentra dentro de la carpeta de instalación de XAMPP.

# 2.11. Referencias biliográficas

Apache (s. f. a.). *Apache HTTP Server Versión 2.4 Documentación.* [https://httpd.apache.org/docs/2.4/](https://httpd.apache.org/docs/2.4/)

Apache (s. f. b.). *Índice de Directivas.* [https://httpd.apache.org/docs/2.4/mod/directives.html](https://httpd.apache.org/docs/2.4/mod/directives.html) Página web de Apache Friends (<https://www.apachefriends.org/es/index.html>)

# Apache (s. f.). Security Tips.

# [https://httpd.apache.org/docs/2.4/es/misc/security_tips.html](https://httpd.apache.org/docs/2.4/es/misc/security_tips.html)

# A fondo

# Recomendaciones de seguridad Apache HTTP Server Project

En este recurso podemos ver de primera mano los consejos que nos ofrecen los desarrolladores del servidor web. No solo son consejos genéricos, sino que nos indican el código de configuración para diferentes aspectos, como ataques DoS, asignación de permisos en el servidor, etc. Siempre hay que tener a mano este recurso para poder consultarlo periódicamente.

Implantación de Aplicaciones Web 45 Tema 2. A fondo

# A fondo

# Documentación MySQL Workbench

MySQL (s. f.). MySQL Workbench. [https://dev.mysql.com/doc/workbench/en/](https://dev.mysql.com/doc/workbench/en/)

Esta aplicación gratuita es, posiblemente, la mejor herramienta de administración, desarrollo y gestión de bases de datos MySQL (MariaDB) que existe en la actualidad. Si tenemos la IP del servidor de BBDD y los datos de autenticación (usuario y contraseña) podemos conectarnos y gestionar cualquier aspecto en los servidores que tengamos conectados. La documentación que tiene asociada la aplicación es inmejorable para el uso de sentencias SQL, programar funciones, procedimientos y *triggers* o cualquier otra necesidad que pueda tener un administrador de base de datos.

Implantación de Aplicaciones Web 46 Tema 2. A fondo

# Entrenamiento 1

- ▸ Planteamiento del ejercicio: una vez instalado XAMPP, vamos a cargar su página

    - de bienvenida (sin pulsar el botón «Admin», en el panel de control) y vamos a buscar

    - la versión exacta de PHP que tenemos instalada en el servidor.

- ▸ Desarrollo paso a paso:

- Ejecutaremos el panel de control de XAMPP.

- Iniciaremos el servidor Apache pulsando el botón «Start».

- Abrimos nuestro navegador web y llamamos al localhost en la barra de direcciones (recuerda: podemos poner 127.0.0.1 con el mismo efecto).

- Si todo está bien, se cargará la página Welcome de XAMPP.

- En el menú de la página que se ha cargado, veremos que hay una opción que es PHPInfo, donde podemos ver multitud de información de configuración del servidor.

**▸ Solución:** hacemos clic en la opción de menú PHPInfo y se nos cargará una página como la siguiente, donde podemos ver la versión de PHP (junto con mucha más información del servidor).

![Figura 19. Versión 8.2.12 de PHP Fuente: elaboración propia.](images/image-22.png)

*Figura 19. Versión 8.2.12 de PHP Fuente: elaboración propia.*

# Entrenamiento 2

**▸ Planteamiento del ejercicio:** crearemos un base de datos con la herramienta phpMyAdmin en el servidor de base de datos MySQL/MariaDB.

**▸ Desarrollo paso a paso:**

- Arrancaremos el servidor MySQL en el panel de control de XAMPP.

- Pulsaremos el botón «Admin» una vez arrancado el servidor de bases de datos. También podemos pulsar sobre la opción de menú «phpMyAdmin» en la página de bienvenida de de XAMPP (accederemos a la misma ubicación, con ambas opciones).

- Estando en la página de administración de BBDD, podemos crear la sencilla base de datos CENTRO y una tabla muy simple, denominada ALUMNOS .

**▸ Solución:** crearemos la base de datos CENTRO y la tabla ALUMNOS con unos fáciles comandos SQL, como los siguientes:

![Figura 20. Comandos SQL. Fuente: elaboración propia.](images/image-23.png)

*Figura 20. Comandos SQL. Fuente: elaboración propia.*

Para ejecutar el código SQL, pulsaremos el botón «Continuar», que aparece abajo a la izquierda en la pestaña SQL.

![Figura 21. Comandos SQL. Fuente: elaboración propia.](images/image-24.png)

*Figura 21. Comandos SQL. Fuente: elaboración propia.*

Al ejecutar el SQL anterior, tendremos la tabla creada en la base de datos y sus campos correspondientes.

![Figura 22. Comandos SQL. Fuente: elaboración propia.](images/image-25.png)

*Figura 22. Comandos SQL. Fuente: elaboración propia.*

# Entrenamiento 3

- ▸ Planteamiento del ejercicio: vamos a crear una página web sencilla, para mostrarla

    - en nuestro navegador usando el servidor web Apache.

- ▸ Desarrollo paso a paso:

- En la carpeta «C:\xampp\htdocs» (carpeta del servidor Apache) crearemos otra con nombre ENTRENA3 .

- Dentro del directorio creado, haremos un fichero index.html con el siguiente código HTML.

![Figura 23. Fichero index.html. Fuente: elaboración propia.](images/image-26.png)

*Figura 23. Fichero index.html. Fuente: elaboración propia.*

Nos aseguraremos de que tenemos arrancado Apache en la consola del XAMPP.

**▸ Solución:** en la barra de direcciones de nuestro navegador indicaremos la dirección del servidor web donde está nuestra página y veremos que se carga de la siguiente forma:

![Figura 24. Carga de localhost/entrena3/. Fuente: elaboración propia.](images/image-27.png)

*Figura 24. Carga de localhost/entrena3/. Fuente: elaboración propia.*

# Entrenamiento 4

- ▸ Planteamiento del ejercicio: crearemos una página web sencilla, pero vamos a

    - incluir un script de PHP con varias sentencias en este lenguaje.

- ▸ Desarrollo paso a paso:

- Editaremos el fichero index.html , para incluir el script que necesitamos en el código HTML.

- Incluimos las modificaciones necesarias y guardamos el fichero para cambiarle la extensión a PHP (de lo contrario no funcionará, al no poder ejecutar el código PHP).

![Figura 25. Fichero con extensión PHP. Fuente: elaboración propia.](images/image-28.png)

*Figura 25. Fichero con extensión PHP. Fuente: elaboración propia.*

**▸ Solución:** si hemos realizado todos los pasos correctamente, al ejecutar el servidor la ubicación de nuestro archivo podremos ver el siguiente resultado.

![Figura 26. Resultado de la ejecución del servidor. Fuente: elaboración propia.](images/image-29.png)

*Figura 26. Resultado de la ejecución del servidor. Fuente: elaboración propia.*

# Entrenamiento 5

- ▸ Planteamiento del ejercicio: en la página que hemos creado en el entrenamiento

    - anterior vamos a incluir tres variables del entorno del servidor con PHP, para ver sus

    - valores en el navegador.

- ▸ Desarrollo paso a paso:

- Editaremos el fichero index.php , resultado del último entrenamiento, para incluir tres variables de entorno que queremos mostrar en nuestra página.

- Buscaremos las variables de entorno a mostrar en la información que nos ofrecía PHPInfo en el primer entrenamiento.

![Figura 27. Variables de entorno. Fuente: elaboración propia.](images/image-30.png)

*Figura 27. Variables de entorno. Fuente: elaboración propia.*

Incluiremos el código marcado en el *script* ya creado anteriormente.

![Figura 28. Código marcado en el script ya creado anteriormente. Fuente: elaboración propia.](images/image-31.png)

*Figura 28. Código marcado en el script ya creado anteriormente. Fuente: elaboración propia.*

**▸ Solución:** al guardar y ejecutar en el servidor, veremos el siguiente resultado:

![Figura 29. Ejecución del servidor. Fuente: elaboración propia.](images/image-32.png)

*Figura 29. Ejecución del servidor. Fuente: elaboración propia.*

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–44)*
- Tema 2. Material de estudio  *(pp.5–44)*
- Entrenamientos  *(pp.47–56)*
- Implantación de Aplicaciones Web 5 · Implantación de Aplicaciones Web 6 · Implantación de Aplicaciones Web 7 · Implantación de Aplicaciones Web 8 · Implantación de Aplicaciones Web 9 · Implantación de Aplicaciones Web 10 · Implantación de Aplicaciones Web 11 · Implantación de Aplicaciones Web 12 · Implantación de Aplicaciones Web 13 · Implantación de Aplicaciones Web 14 · Implantación de Aplicaciones Web 15 · Implantación de Aplicaciones Web 16 · Implantación de Aplicaciones Web 17 · Implantación de Aplicaciones Web 18 · Implantación de Aplicaciones Web 19 · Implantación de Aplicaciones Web 20 · Implantación de Aplicaciones Web 21 · Implantación de Aplicaciones Web 22 · Implantación de Aplicaciones Web 23 · Implantación de Aplicaciones Web 24 · Implantación de Aplicaciones Web 25 · Implantación de Aplicaciones Web 26 · Implantación de Aplicaciones Web 27 · Implantación de Aplicaciones Web 28 · Implantación de Aplicaciones Web 29 · Implantación de Aplicaciones Web 30 · Implantación de Aplicaciones Web 31 · Implantación de Aplicaciones Web 32 · Implantación de Aplicaciones Web 33 · Implantación de Aplicaciones Web 34 · Implantación de Aplicaciones Web 35 · Implantación de Aplicaciones Web 36 · Implantación de Aplicaciones Web 37 · Implantación de Aplicaciones Web 38 · Implantación de Aplicaciones Web 39 · Implantación de Aplicaciones Web 40 · Implantación de Aplicaciones Web 41 · Implantación de Aplicaciones Web 42 · Implantación de Aplicaciones Web 43 · Implantación de Aplicaciones Web 44  *(pp.5–44)*
- Implantación de Aplicaciones Web 47 Tema 2. Entrenamientos · Implantación de Aplicaciones Web 48 Tema 2. Entrenamientos · Implantación de Aplicaciones Web 49 Tema 2. Entrenamientos · Implantación de Aplicaciones Web 50 Tema 2. Entrenamientos · Implantación de Aplicaciones Web 51 Tema 2. Entrenamientos · Implantación de Aplicaciones Web 52 Tema 2. Entrenamientos · Implantación de Aplicaciones Web 53 Tema 2. Entrenamientos · Implantación de Aplicaciones Web 54 Tema 2. Entrenamientos · Implantación de Aplicaciones Web 55 Tema 2. Entrenamientos · Implantación de Aplicaciones Web 56 Tema 2. Entrenamientos  *(pp.47–56)*