## Tema 4

## Seguridad y Alta Disponibilidad

# Tema 4. Seguridad lógica

# Índice

Esquema Material de estudio

## 4.1. Introducción y objetivos

## 4.2. Principios de seguridad lógica

## 4.3. Control de acceso lógico

## 4.4. Control de acceso en la BIOS y gestor de arranque

## 4.5. Control de acceso en el sistema operativo

## 4.6. Referencias bibliográficas

A fondo

¿Son suficientes las contraseñas?

Gestión de contraseñas seguras

Autenticación de dos factores (2FA)

Comprueba tu contraseña

Los mejores gestores de contraseñas

Entrenamientos Entrenamiento 1: simulación de ataque de fuerza bruta (SSH-Hydra) Entrenamiento 2: simulación de ataque de fuerza bruta (FTP-Medusa) Entrenamiento 3: gestión de contraseñas seguras y directivas de seguridad en Windows Entrenamiento 4: gestión de contraseñas seguras y directivas de seguridad en Ubuntu Entrenamiento 5: configuración de contraseña en la BIOS

# Esquema

![image-2](images/image-2.png)

Seguridad y Alta Disponibilidad 4 Tema 4. Esquema

## 4.1. Introducción y objetivos

En la actualidad, la protección de la información digital es esencial para las organizaciones y la seguridad lógica juega un papel crucial en esta tarea. Este documento explora los principios y los métodos de la seguridad lógica, al abordar cómo se pueden implementar las barreras y los procedimientos para asegurar que solo las personas autorizadas tengan acceso a los datos sensibles. Se discuten diversas técnicas, como la gestión efectiva de permisos y el control de acceso, basadas en la identificación, autenticación y autorización de usuarios. También se destacan las políticas de contraseñas, la configuración segura de la *basic input/output system* (BIOS) y los métodos avanzados de acceso a sistemas operativos. En conjunto, estos enfoques buscan **proteger los activos digitales** contra accesos no autorizados y amenazas comunes, para asegurar la integridad y confidencialidad de la información. Los objetivos que se pretenden alcanzar en este tema son:

**▸** Proteger la información de la organización.

**▸** Gestionar efectivamente los permisos y el control de acceso.

**▸** Prevenir el acceso y las modificaciones no autorizadas.

**▸** Utilizar métodos fundamentales de seguridad lógica.

**▸** Implementar políticas de contraseñas efectivas.

**▸** Proteger los sistemas contra ataques de fuerza bruta y diccionario.

**▸** Asegurar la BIOS y el gestor de arranque.

**▸** Evaluar y mejorar la seguridad del sistema operativo.

## 4.2. Principios de seguridad lógica

¿Qué es la seguridad lógica?

La información es el activo más crítico para las organizaciones, por lo tanto, es vital asegurarlo más allá de las medidas físicas mediante técnicas de seguridad lógica.

La seguridad lógica se centra en **establecer barreras y procedimientos** que protejan el acceso a los datos, las cuales permiten únicamente que personas autorizadas puedan acceder a ellos. En los próximos temas exploraremos la seguridad en el acceso a sistemas, el uso de *software* antimalware y la criptografía, que son métodos esenciales para esta protección. Los administradores de los sistemas deben estar preparados para enfrentar amenazas como accesos no autorizados y modificaciones indebidas de los datos y las aplicaciones.

Esta forma de seguridad se apoya en una gestión efectiva de los permisos y del control del acceso a los recursos informáticos, la cual está basada en la identificación, autenticación y autorización de usuarios.

En la configuración de sistemas, un principio fundamental de seguridad lógica es que todo lo que no esté expresamente permitido debe estar prohibido.

## 4.3. Control de acceso lógico

¿Cómo se controla el acceso lógico?

El control de acceso lógico es fundamental para proteger la información de los sistemas informáticos, para evitar el acceso no autorizado. Este control se basa en dos procesos esenciales: la identificación y la autenticación.

**▸ Identificación:** es el proceso mediante el cual el usuario se presenta al sistema. Es la fase en la que el usuario declara su identidad, usualmente proporcionando un nombre de usuario.

**▸ Autenticación:** es el proceso que sigue a la identificación, en el cual el sistema verifica la autenticidad de la identidad presentada. Esto se hace mediante diferentes métodos, como contraseñas, tokens, biometría, entre otros.

Single sign-on

Para maximizar la eficiencia, es ideal que los usuarios solo tengan que **identificarse** **y autenticarse una vez** para acceder a todas las aplicaciones y datos autorizados, tanto de forma local como remotamente. Este concepto se conoce como *single sign-* *on* (SSO) o sincronización de *passwords.*

Una técnica efectiva para implementar SSO

es el uso de un **servidor de**

**autenticación centralizada.** Este servidor centraliza el proceso de autenticación, lo que les permite a los usuarios identificarse una sola vez. Posteriormente, el servidor autentica a los usuarios en los demás sistemas que necesitan acceder.

Este servidor no necesariamente debe ser un equipo independiente. Sus funciones pueden estar distribuidas tanto geográfica como lógicamente para gestionar la carga de trabajo de manera eficiente. Dos ejemplos de implementación son:

**▸** *Lightweight Directory Access Protocol* (LDAP) en sistemas GNU/Linux.

**▸** *Active Directory* en Windows Server.

El **LDAP** es un protocolo estándar para acceder y mantener servicios de directorio distribuidos a través de una red. Los servidores LDAP se utilizan para autenticar usuarios y almacenar información sobre ellos, como credenciales y permisos.

El ***Active Directory*** es un servicio de directorio desarrollado por Microsoft para redes Windows. Gestiona identidades y relaciones, lo que permite la autenticación y autorización de usuarios y recursos dentro de un dominio.

![image-3](images/image-3.png)

Tabla 1. Pros y contras del uso de SSO. Fuente: elaboración propia.

Problemas de contraseñas

Los sistemas de control de acceso protegidos con contraseña son **vulnerables a** **varios tipos de ataques,** los más comunes son el ataque de fuerza bruta y el ataque de diccionario. A continuación, se detalla cada uno de estos métodos de ataque y una forma sencilla de mitigarlos.

#### Tipos de ataques a contraseñas

**▸ Ataque de fuerza bruta:** este tipo de ataque intenta recuperar una clave probando todas las combinaciones posibles hasta encontrar la correcta.

- Cuanto más corta sea la contraseña, más rápido será encontrarla.

- Es un método exhaustivo y puede ser muy lento si la contraseña es larga y compleja.

**▸ Ataque de diccionario:** este ataque intenta descubrir una clave probando todas las palabras de un diccionario o conjunto de palabras comunes.

- Es más eficiente que un ataque de fuerza bruta porque muchas personas usan palabras comunes como contraseñas.

- Se basa en la suposición de que los usuarios eligen contraseñas fáciles de recordar.

#### Mitigación de ataques

Una forma efectiva y sencilla de proteger un sistema contra estos ataques es establecer un **límite** en el número de **intentos de inicio de sesión permitidos.** Este enfoque se puede ilustrar con el mecanismo de las tarjetas SIM, que se bloquean automáticamente tras tres intentos fallidos de ingreso del código PIN o, por ejemplo, se puede configurar para bloquear la cuenta de usuario de un sistema informático después de tres a cinco intentos fallidos, ya sea temporalmente (por ejemplo, quince minutos) o hasta que un administrador la desbloquee.

![Aquí hay una tabla que resume esta estrategia:](images/image-4.png)

Tabla 2. Mitigación de ataques. Fuente: elaboración propia.

Políticas de contraseñas

#### ¿Cómo se controla el acceso lógico?

Las contraseñas son claves utilizadas para acceder a información personal o profesional almacenada en dispositivos y aplicaciones, incluyendo entornos web como el correo electrónico, la banca online y las redes sociales.

Para garantizar la seguridad de una contraseña, se recomienda lo siguiente:

**▸ Longitud mínima:** cada carácter en una contraseña aumenta exponencialmente su nivel de protección. Se aconseja que las contraseñas tengan un mínimo de ocho caracteres, idealmente, lo aconsejable es doce caracteres o más.

**▸ Combinación de caracteres:** para hacer la contraseña más segura, se debe incluir una combinación de letras minúsculas, letras mayúsculas, números y símbolos especiales. Cuanto más variados sean estos caracteres, más difícil será que sea adivinada.

Vamos a detallar el cálculo del número de combinaciones posibles para una contraseña de seis caracteres y ver cómo se incrementa la seguridad al añadir mayúsculas a las minúsculas.

**Solo letras minúsculas:**

El alfabeto español tiene veintisiete letras minúsculas. Para una contraseña de seis caracteres:

$$276= 387 420 489$$

**Letras minúsculas y mayúsculas:**

Al añadir mayúsculas, tenemos veintisiete letras minúsculas y veintisiete letras mayúsculas, lo que suma un total de 54 caracteres. Para una contraseña de seis caracteres:

$$546= 21 073 741 824$$

Incluir tanto letras minúsculas como mayúsculas incrementa drásticamente el número de combinaciones posibles, lo que hace que la contraseña sea **significativamente** **más segura** frente a ataques de fuerza bruta.

Esta comparación muestra cómo el aumento en la complejidad de la contraseña al incluir más tipos de caracteres incrementa exponencialmente el número de combinaciones que un atacante tendría que probar, lo cual mejora la seguridad del sistema.

![Figura 1. Contraseñas más habituales en el 2023. Fuente: Melo, 2024.](images/image-5.png)

*Figura 1. Contraseñas más habituales en el 2023. Fuente: Melo, 2024.*

#### Recomendaciones para contraseñas

Las contraseñas son una de las formas más comunes de autenticar usuarios. Para que una contraseña sea segura, se recomienda lo siguiente:

![Figura 2. Consejos y recomendaciones. Fuente: adaptado de Instituto Nacional de Ciberseguridad, (s. f.).](images/image-6.png)

*Figura 2. Consejos y recomendaciones. Fuente: adaptado de Instituto Nacional de Ciberseguridad, (s. f.).*

![Figura 3. Consejos y recomendaciones. Fuente: adaptado de Instituto Nacional de Ciberseguridad, (s. f.).](images/image-7.png)

*Figura 3. Consejos y recomendaciones. Fuente: adaptado de Instituto Nacional de Ciberseguridad, (s. f.).*

![Figura 4. Consejos y recomendaciones. Fuente: adaptado de Instituto Nacional de Ciberseguridad, (s. f.).](images/image-8.png)

*Figura 4. Consejos y recomendaciones. Fuente: adaptado de Instituto Nacional de Ciberseguridad, (s. f.).*

Implementación de medidas de protección

La implementación de medidas de protección contra ataques de fuerza bruta y de diccionario es crucial para asegurar la integridad y la seguridad de los sistemas de control de acceso basados en contraseñas. A continuación, se describen algunas medidas prácticas y cómo implementarlas.

**▸ Límite de intentos de inicio de sesión:** limitar el número de intentos de inicio de sesión permitidos antes de bloquear la cuenta de usuario.

- Configurar políticas de seguridad en el sistema operativo o en la aplicación para limitar los intentos de inicio de sesión.

Por ejemplo, en Windows se puede usar la política de seguridad local (secpol.msc) para configurar el «Umbral de bloqueo de cuenta».

En sistemas Linux, se puede utilizar *pluggable authentication modules* (PAM) para limitar los intentos fallidos añadiendo reglas en el archivo «/etc/pam.d/common-auth».

**▸ Contraseñas fuertes y complejas:** se requieren contraseñas que cumplan con criterios de complejidad.

- Configurar políticas de contraseñas en el sistema operativo o en la aplicación para requerir contraseñas que incluyan una combinación de letras mayúsculas, minúsculas, números y caracteres especiales.

Por ejemplo, en *Active Directory:*

*Abrir «Group Policy Management» y navegar por «Default Domain Policy -* *> Computer Configuration -> Policies -> Windows Settings -> Security* *Settings -> Account Policies -> Password Policy».*

Configurar las políticas como «Minimum password length», «Password must meet complexity requirements», etc.

**▸ Bloqueo y desbloqueo de cuentas:** bloquear cuentas tras múltiples intentos fallidos y proporcionar un mecanismo seguro para el desbloqueo.

- Configurar el sistema para bloquear la cuenta tras un número específico de intentos fallidos y definir el procedimiento de desbloqueo.

Ejemplo en Windows: Usar la política de seguridad local para configurar «Account lockout duration» y «Reset account lockout counter after». Proveer un mecanismo de desbloqueo:

- Desbloqueo manual por un administrador.

- Uso de una autenticación secundaria (correo, SMS) para permitirle al

usuario desbloquear su cuenta de manera segura.

**▸ Monitoreo y alerta:** implementar sistemas de monitoreo y alerta para detectar intentos de acceso no autorizados.

- Utilizar herramientas de monitoreo como Security Information and Event Management (SIEM) para supervisar los intentos de acceso fallidos y generar alertas en tiempo real.

- Configurar alertas de seguridad para que los administradores sean notificados sobre los intentos de acceso sospechosos.

Ejemplo de herramienta: Splunk, OSSEC, o ELK stack.

**▸ Autenticación multifactor (MFA):** añadir una capa adicional de seguridad mediante el uso de múltiples factores de autenticación.

- Configurar MFA en el sistema o aplicación, para requerir no solo una contraseña sino también un segundo factor, como un código enviado a un dispositivo móvil o una huella digital.

Ejemplo de implementación con Google Authenticator:

- Instalar y configurar «libpam-google-authenticator» en sistemas Linux

para añadir MFA a los accesos SSH.

Implementar estas medidas de protección requiere una combinación de configuraciones de sistema, políticas de seguridad y el uso de herramientas adicionales para asegurar que los sistemas están protegidos contra ataques de fuerza bruta y de diccionario. Estas prácticas no solo mejoran la seguridad, sino que también ofrecen una experiencia más segura para los usuarios.

## 4.4. Control de acceso en la BIOS y gestor de arranque

El control de acceso en la BIOS y en el gestor de arranque es fundamental para asegurar la integridad y la seguridad de un sistema informático. Aquí te detallo cómo se implementan estos controles:

Control de acceso en la BIOS

**▸ Seguridad del sistema(system** *security):*

- Contraseña de arranque(power-on password): se configura una contraseña que se debe ingresar cada vez que se enciende el ordenador. Si la contraseña no es correcta, el sistema no arrancará. Esta medida impide que personas no autorizadas puedan acceder al sistema operativo y a los datos almacenados.

- Contraseña de supervisión(supervisor password): se establece una contraseña que permite acceder y modificar la configuración de la BIOS. Sin esta contraseña, el acceso a la BIOS estará limitado o denegado. Esto asegura que solo los usuarios autorizados puedan cambiar la configuración crítica del sistema.

**▸ Seguridad de la configuración de la BIOS(setup** *security):*

- Roles y permisos: se pueden definir roles con diferentes niveles de acceso. Uno de ellos puede ser usuario *(user),* que, generalmente, tienen permisos de solo lectura. Pueden visualizar las configuraciones de la BIOS, pero no modificarlas. Otro rol es el de administrador (Admin), los cuales tienen permisos completos para leer y modificar la configuración de la BIOS. Este rol permite realizar cambios críticos, como el orden de arranque, ajustes de voltaje, entre otros.

- Doble contraseña: algunas BIOS permiten configurar dos contraseñas, una para el administrador y otra para el usuario. De esta forma, se puede limitar el acceso según el nivel de permisos configurado.

Control de acceso en el gestor de arranque

El gestor de arranque *(bootloader)* es el *software* que carga el sistema operativo después de que la BIOS ha realizado su trabajo. Controlar el acceso a este componente es crucial para mantener la seguridad del sistema operativo.

**▸ Contraseña de arranque:**

- Es similar a la contraseña de arranque de la BIOS, una contraseña de arranque en dicho gestor impide que personas no autorizadas carguen el sistema operativo o cambien los parámetros del gestor de arranque. Por ejemplo, en Grand Unified Bootloader (GRUB), se puede configurar una contraseña para proteger el menú de arranque y las opciones avanzadas.

**▸ Firma digital de cargas de arranque:**

- Secure boot: es una característica de las BIOS modernas (unified extensible *firmware interface,* UEFI) que garantiza que solo se cargue el *software* de arranque que está firmado digitalmente por una autoridad de confianza. Esto previene la ejecución de *software* malicioso en el arranque, lo que proporciona una capa adicional de seguridad.

**▸ Configuración del gestor de arranque:**

- Acceso restringido: el archivo de configuración del gestor de arranque puede ser protegido para evitar modificaciones no autorizadas. Por ejemplo, en GRUB, el archivo «grub.cfg» puede estar protegido para que solo el usuario *root* tenga permisos de escritura.

- Modo de usuario y administrador: es similar a la BIOS, algunos gestores de arranque permiten definir roles de usuario y administrador, lo cual limita las opciones que pueden ser modificadas por los usuarios no autorizados.

Implementación de seguridad adicional

**▸ Actualización regular:** mantener la BIOS y el gestor de arranque actualizados con los últimos parches de seguridad es crucial para proteger contra las vulnerabilidades conocidas.

**▸ Protección física:** asegurarse de que el acceso físico al ordenador está restringido.

Sin protección física, un atacante con acceso directo al *hardware* podría resetear la BIOS o el gestor de arranque.

Al implementar estas medidas de seguridad, se puede asegurar que tanto la BIOS como el gestor de arranque están protegidos contra accesos no autorizados y manipulaciones que puedan comprometer la seguridad del sistema.

## 4.5. Control de acceso en el sistema operativo

La seguridad del control de acceso en los sistemas operativos es un tema crítico, ya que es la primera línea de defensa contra accesos no autorizados. Los métodos de autenticación, como la biometría y las contraseñas, presentan ventajas y desventajas que deben ser consideradas en la implementación de políticas de seguridad.

![image-9](images/image-9.png)

Biometría

Tabla 3. Ventajas y desventajas de la biometría. Fuente: elaboración propia.

![Usuario/contraseña](images/image-10.png)

Tabla 4. Ventajas-desventajas del usuario-contraseña. Fuente: elaboración propia.

Métodos para acceder a los sistemas operativos sin control de contraseña

Existen varias herramientas y métodos que pueden ser utilizados para acceder a un sistema operativo sin conocer la contraseña del usuario. Algunas de estas incluyen:

**▸ Distribuciones Live de Linux:** herramientas como Kali Linux o Ubuntu en modo Live pueden ser utilizadas para acceder a los archivos de un sistema operativo sin necesidad de autenticación. Esto permite modificar, eliminar o recuperar contraseñas.

**▸ Herramientas de recuperación de contraseñas:** programas como Ophcrack utilizan tablas de arco iris para intentar descifrar las contraseñas. Otros, como John the Ripper, realizan ataques de fuerza bruta o de diccionario.

**▸ Modificación de archivos de sistema:** en los sistemas Windows es posible utilizar una distribución Live de Linux para modificar archivos como el «Sethc.exe» y activar un *shell* de comandos con privilegios de administrador desde la pantalla de inicio de sesión.

**▸ Modo de recuperación:** en sistemas operativos como macOS o Linux, se puede acceder al modo de recuperación o a un terminal con privilegios de *root* para resetear contraseñas de usuarios.

Recomendaciones para mejorar la seguridad

**▸ Fortaleza de las contraseñas:** implementar políticas de contraseñas seguras que incluyan la longitud mínima, el uso de caracteres especiales, números y letras mayúsculas y minúsculas.

**▸ Autenticación multifactor (MFA):** utilizar, además de la contraseña, un segundo factor de autenticación, como un código enviado al teléfono móvil, una aplicación de autenticación o una clave de *hardware.*

**▸ Auditorías de seguridad:** regularmente auditar los sistemas y las políticas de acceso para detectar y corregir posibles vulnerabilidades.

**▸ Encriptación de datos:** asegurar que los datos sensibles están encriptados, tanto en reposo como en tránsito.

**▸ Capacitación de usuarios:** educar a los usuarios sobre la importancia de la seguridad de sus credenciales y cómo protegerse contra las técnicas de ingeniería social y *phishing.*

Conocer y valorar estas herramientas y métodos no solo nos ayuda a proteger mejor nuestros sistemas, sino que también nos permite entender las posibles vulnerabilidades y cómo mitigarlas efectivamente.

## 4.6. Referencias bibliográficas

Instituto Nacional de Ciberseguridad (INCIBE). (s. f.). *Privacidad y seguridad en* *Internet* [diapositiva]. [https://www.incibe.es/sites/default/files/docs/contrasenas01.pdf](https://www.incibe.es/sites/default/files/docs/contrasenas01.pdf)

Melo, M. F. (2024). *Las contraseñas más comunes* [gráfico]. [https://es.statista.com/grafico/23636/contrasenas-mas-usadas-en-el-mundo/](https://es.statista.com/grafico/23636/contrasenas-mas-usadas-en-el-mundo/)

# Internet. ¿Son suficientes las contraseñas? [diapositiva].

## ¿Son suficientes las contraseñas?

Instituto Nacional de Ciberseguridad (INCIBE). (s. f.). *Privacidad y seguridad en* [https://www.incibe.es/sites/default/files/docs/contrasenas02.pdf](https://www.incibe.es/sites/default/files/docs/contrasenas02.pdf)

Infografía muy fácil de comprender para entender la necesidad del uso de otros mecanismos diferentes al clásico usuario/contraseña para proteger la cuenta de usuario.

## Gestión de contraseñas seguras

Instituto Nacional de Ciberseguridad (INCIBE). (s. f.). *Gestión de contraseñas* *seguras.* [https://www.incibe.es/ciudadania/tematicas/contrasenas-seguras](https://www.incibe.es/ciudadania/tematicas/contrasenas-seguras)

Aquí tienes curiosidades sobre el mundo de las contraseñas seguras: principales ataques, reglas nemotécnicas para crear contraseñas seguras, recursos divertidos…

# seguras/autenticacion-de-dos-factores

## Autenticación de dos factores (2FA)

Instituto Nacional de Ciberseguridad (INCIBE). (s. f.). *Autenticación de dos factores*

*( 2 F A ) .* <https://www.incibe.es/ciudadania/tematicas/contrasenas-> Si deseas aumentar la seguridad de tus cuentas de usuario para garantizar que solo tú puedas acceder a ellas, esta herramienta es la solución ideal. Además de la contraseña, requerirás un código único que recibirás exclusivamente en tu teléfono móvil.

## Comprueba tu contraseña

Página web de Kaspersky ([https://password.kaspersky.com/es/](https://password.kaspersky.com/es/)).

¿Estás utilizando contraseñas seguras? Compruébalo.

# GoDaddy. (2023, julio 31). Los mejores gestores de contraseñas.

# contrasenas

## Los mejores gestores de contraseñas

<https://www.godaddy.com/resources/es/seguridad/los-mejores-gestores-de->

Guarda tus contraseñas en el repositorio más adecuado.

## Entrenamiento 1: simulación de ataque de fuerza

## bruta (SSH-Hydra)

**▸ Planteamiento del ejercicio** El objetivo de esta actividad es comprender los riesgos asociados con los ataques de fuerza bruta, familiarizarse con las herramientas y técnicas utilizadas en el campo de la seguridad informática y aprender a implementar contramedidas para mitigar estos ataques. Utiliza una herramienta como Hydra para llevar a cabo un ataque simulado contra servicios vulnerables en máquinas virtuales (SSH). Una vez realizado el ataque, plantea contramedidas para mejorar la seguridad.

**▸ Desarrollo paso a paso** **Paso 1:** configuración del entorno.

**▸** Abre tu *software* de virtualización (por ejemplo, VirtualBox) y crea una nueva máquina virtual.

**▸** Selecciona el tipo y la versión del sistema operativo por instalar. Por ejemplo, elige una distribución de Linux desactualizada como Ubuntu 20.04.

**▸** Asigna recursos de *hardware* según sea necesario (CPU, RAM, espacio en disco).

**▸** Inicia la máquina virtual y sigue las instrucciones para instalar el sistema operativo. **Paso 2:** instalación de servicios vulnerables.

**▸** Una vez que el sistema operativo está instalado, configura los servicios susceptibles de ataques de fuerza bruta. En este caso debes instalar un servidor SSH.

**▸** Asegúrate de que este servicio esté configurado con credenciales débiles o predecibles para simular un entorno vulnerable.

**Paso 3:** configuración de la herramienta de ataque.

**▸** En tu máquina anfitriona instala la herramienta de ataque de fuerza bruta Hydra. Puedes utilizar el gestor de paquetes de tu sistema operativo (apt-get en Ubuntu, por ejemplo) o descargar la herramienta desde su sitio web oficial.

**▸** Configura la herramienta para apuntar al servicio objetivo en tu máquina virtual. Especifica la dirección IP de la máquina virtual, el puerto del servicio objetivo y la lista de usuarios o contraseñas si es aplicable.

**Paso 4:** ejecución del ataque

**▸** Ejecuta la herramienta de ataque de fuerza bruta desde tu máquina anfitriona. Por ejemplo, si estás utilizando Hydra para atacar un servicio SSH, el comando podría ser algo como: hydra -l <usuario> -P <lista_de_contraseñas> ssh://<dirección_IP>.

**▸** Observa cómo la herramienta intenta diferentes combinaciones de nombres de usuario y contraseñas para obtener acceso al servicio.

**Paso 5:** análisis de resultados.

**▸** Registra el tiempo necesario para que la herramienta de ataque encuentre credenciales válidas.

**▸** Analiza la eficacia del ataque y considera cómo podría impactar en la seguridad del sistema objetivo. Reflexiona sobre la importancia de tener credenciales seguras y prácticas de autenticación robustas.

**Paso 6:** implementación de contramedidas.

**▸** Discute y propón posibles contramedidas para mitigar los ataques de fuerza bruta. Algunas medidas podrían incluir la implementación de políticas de bloqueo de cuentas después de varios intentos fallidos, el uso de autenticación de dos factores o el uso de contraseñas más seguras.

**▸** Implementa al menos una contramedida en la máquina virtual para proteger el servicio objetivo contra futuros ataques de fuerza bruta. Por ejemplo, configura el servicio SSH para bloquear direcciones IP después de un número específico de intentos fallidos.

**Paso 7:** reflexión final.

**▸** Reflexiona sobre los resultados de la actividad y discute cómo los ataques de fuerza bruta pueden representar una amenaza para la seguridad de los sistemas informáticos.

**▸** Considera cómo los administradores de sistemas pueden detectar y responder a los ataques de fuerza bruta de manera efectiva y cómo pueden implementar medidas preventivas para proteger sus sistemas.

**▸ Solución**

- Instalación del servicio SSH (OpenSSH):

El servicio SSH te permite acceder de forma remota a tu máquina a través de una conexión cifrada.

![Figura 5. Instalación del servicio SSH. Fuente: elaboración propia.](images/image-11.png)

*Figura 5. Instalación del servicio SSH. Fuente: elaboración propia.*

Una vez que la instalación haya finalizado, el servicio SSH debería iniciarse automáticamente. Puedes verificar el estado del servicio ejecutando:

Si el servicio está activo y en ejecución, verás un mensaje que indica que el servicio está «active (running)».

**▸** Configuración de usuarios y contraseñas en SSH:

El servidor SSH en Ubuntu utiliza los usuarios del sistema para la autenticación. Por lo tanto, puedes crear y administrar usuarios del sistema para permitirles iniciar sesión a través de SSH.

Para agregar un nuevo usuario al sistema, puedes utilizar el comando adduser . Por ejemplo, para agregar un usuario llamado «usuario_ssh», ejecuta el siguiente comando y sigue las instrucciones en pantalla para establecer una contraseña para el nuevo usuario:

![Figura 6. Verificar el estado del servicio. Fuente: elaboración propia.](images/image-12.png)

*Figura 6. Verificar el estado del servicio. Fuente: elaboración propia.*

![Figura 7. Comando. Fuente: elaboración propia.](images/image-13.png)

*Figura 7. Comando. Fuente: elaboración propia.*

Si deseas que un usuario específico tenga acceso SSH, asegúrate de que esté en el grupo ssh (que puede no existir por defecto). Puedes crear este grupo y agregar al usuario a este con los siguientes comandos:

![Figura 8. Comandos. Fuente: elaboración propia.](images/image-14.png)

*Figura 8. Comandos. Fuente: elaboración propia.*

Asegúrate de que el servicio SSH esté configurado para permitir la autenticación de contraseñas. Abre el archivo de configuración /etc/ssh/sshd_config en un editor de texto con privilegios de superusuario:

![Figura 9. Archivo de configuración /etc/ssh/sshd_config. Fuente: elaboración propia.](images/image-15.png)

*Figura 9. Archivo de configuración /etc/ssh/sshd_config. Fuente: elaboración propia.*

Busca la línea PasswordAuthentication y asegúrate de que esté configurada como yes :

![Figura 10. Línea PasswordAuthentication. Fuente: elaboración propia.](images/image-16.png)

*Figura 10. Línea PasswordAuthentication. Fuente: elaboración propia.*

Reinicia el servicio SSH para aplicar los cambios:

![Figura 11. Reinicia el servicio SSH. Fuente: elaboración propia.](images/image-17.png)

*Figura 11. Reinicia el servicio SSH. Fuente: elaboración propia.*

Ahora, el usuario «usuario_ssh» podrá iniciar sesión a través de SSH utilizando la contraseña que estableciste (una fácil para implementar el ataque).

Para configurar la herramienta de ataque de fuerza bruta en tu máquina anfitriona y apuntar al servicio objetivo en tu máquina virtual, sigue estos pasos utilizando Hydra.

**▸** Instalación de Hydra:

En Ubuntu, puedes instalar Hydra fácilmente utilizando el gestor de paquetes apt :

![Figura 12. Instalación de Hydra. Fuente: elaboración propia.](images/image-18.png)

*Figura 12. Instalación de Hydra. Fuente: elaboración propia.*

**▸** Configuración de Hydra:

Una vez que Hydra esté instalado, puedes configurarlo para apuntar al servicio objetivo en tu máquina virtual. Por ejemplo, si deseas atacar el servicio SSH en la dirección IP 192.168.1.100 y el puerto SSH predeterminado 22 , el comando sería algo como esto:

![Figura 13. Comando para configuración de Hydra. Fuente: elaboración propia.](images/image-19.png)

*Figura 13. Comando para configuración de Hydra. Fuente: elaboración propia.*

-l <usuario> : especifica el nombre de usuario que se utilizará en el ataque.

-P <lista_de_contraseñas> : especifica el archivo que contiene la lista de contraseñas que se probarán en el ataque.

Seguridad y Alta Disponibilidad 37 Tema 4. Entrenamientos ssh://192.168.1.100:22 : especifica el protocolo (SSH), la dirección IP y el puerto del servicio SSH que se está atacando.

Con estos pasos, habrás configurado Hydra para apuntar al servicio objetivo en tu máquina virtual y estarás listo para ejecutar el ataque de fuerza bruta.

**▸** Contramedidas:

Para configurar los servicios de SSH en Ubuntu para bloquear temporalmente las cuentas después de un número específico de intentos fallidos, puedes seguir estos pasos:

Configuración de SSH:

Abre el archivo de configuración de SSH sshd_config en un editor de texto. Puedes hacerlo con el siguiente comando en la terminal:

![Figura 14. Abrir el archivo de configuración de SSH sshd_config. Fuente: elaboración propia.](images/image-20.png)

*Figura 14. Abrir el archivo de configuración de SSH sshd_config. Fuente: elaboración propia.*

Busca la línea que dice #MaxAuthTries y elimina el símbolo # al principio de la línea si está presente. Si la línea no existe, agrégala al final del archivo. Establece el número máximo de intentos de autenticación permitidos antes de que se bloquee temporalmente la cuenta. Por ejemplo:

![Figura 15. Establecer el número máximo de intentos de autenticación. Fuente: elaboración propia.](images/image-21.png)

*Figura 15. Establecer el número máximo de intentos de autenticación. Fuente: elaboración propia.*

Esto limitará a tres el número de intentos de autenticación permitidos antes de bloquear la cuenta.

Guarda los cambios y cierra el editor de texto. Reinicia el servicio SSH para que los cambios surtan efecto:

![Figura 16. Reiniciar el servicio SSH. Fuente: elaboración propia.](images/image-22.png)

*Figura 16. Reiniciar el servicio SSH. Fuente: elaboración propia.*

## Entrenamiento 2: simulación de ataque de fuerza

## bruta (FTP-Medusa)

**▸ Planteamiento del ejercicio** El objetivo de esta actividad es comprender los riesgos asociados con los ataques de fuerza bruta, familiarizarse con las herramientas y técnicas utilizadas en el campo de la seguridad informática y aprender a implementar contramedidas para mitigar estos ataques. Utiliza la herramienta Medusa para llevar a cabo un ataque simulado contra servicios vulnerables en máquinas virtuales (FTP). Una vez realizado el ataque, plantea contramedidas para mejorar la seguridad.

**▸ Desarrollo paso a paso** **Paso 1:** configuración del entorno.

**▸** Abre tu *software* de virtualización (por ejemplo, VirtualBox) y crea una nueva máquina virtual.

**▸** Selecciona el tipo y la versión del sistema operativo por instalar. Por ejemplo, elige una distribución de Linux desactualizada como Ubuntu 20.04.

**▸** Asigna recursos de *hardware* según sea necesario (CPU, RAM, espacio en disco).

**▸** Inicia la máquina virtual y sigue las instrucciones para instalar el sistema operativo. **Paso 2:** instalación de servicios vulnerables.

**▸** Una vez que el sistema operativo esté instalado, configura los servicios susceptibles de ataques de fuerza bruta. En este caso, debes instalar un servidor FTP.

**▸** Asegúrate de que este servicio esté configurado con credenciales débiles o predecibles para simular un entorno vulnerable.

**Paso 3:** configuración de la herramienta de ataque.

**▸** En tu máquina anfitriona, instala una herramienta de ataque de fuerza bruta como Medusa. Puedes utilizar el gestor de paquetes de tu sistema operativo (apt-get en Ubuntu, por ejemplo) o descargar la herramienta desde su sitio web oficial.

**▸** Configura la herramienta para apuntar al servicio objetivo en tu máquina virtual. Especifica la dirección IP de la máquina virtual, el puerto del servicio objetivo y la lista de usuarios o contraseñas si es aplicable.

**Paso 4:** ejecución del ataque.

**▸** Ejecuta la herramienta de ataque de fuerza bruta desde tu máquina anfitriona.

**▸** Observa cómo la herramienta intenta diferentes combinaciones de nombres de usuario y contraseñas para obtener acceso al servicio.

**Paso 5:** análisis de resultados.

**▸** Registra el tiempo necesario para que la herramienta de ataque encuentre credenciales válidas.

**▸** Analiza la eficacia del ataque y considera cómo podría impactar en la seguridad del sistema objetivo. Reflexiona sobre la importancia de tener credenciales seguras y prácticas de autenticación robustas.

**Paso 6:** implementación de contramedidas.

**▸** Discute y propón posibles contramedidas para mitigar los ataques de fuerza bruta. Algunas medidas podrían incluir la implementación de políticas de bloqueo de cuentas después de varios intentos fallidos, el uso de autenticación de dos factores o el uso de contraseñas más seguras.

**▸** Implementa al menos una contramedida en la máquina virtual para proteger el servicio objetivo contra futuros ataques de fuerza bruta. Por ejemplo, una de las más efectivas es el uso de fail2ban. Esta herramienta monitorea los archivos de registro en busca de patrones de intentos de inicio de sesión fallidos y bloquea automáticamente las direcciones IP que exceden un número permitido de intentos fallidos.

**▸** Reflexiona sobre los resultados de la actividad y discute cómo es que los ataques de fuerza bruta pueden representar una amenaza para la seguridad de los sistemas informáticos.

**▸** Considera cómo los administradores de sistemas pueden detectar y responder a los ataques de fuerza bruta de manera efectiva y qué medidas preventivas pueden implementar para proteger sus sistemas.

**▸ Solución**

Instalación del servicio FTP (vsftpd)

El servicio FTP te permite transferir archivos de forma remota a través del protocolo FTP. En la misma terminal, instala el servidor FTP vsftpd ejecutando el siguiente comando:

![Figura 17. Comando. Fuente: elaboración propia.](images/image-23.png)

*Figura 17. Comando. Fuente: elaboración propia.*

Una vez que la instalación haya finalizado, el servicio vsftpd debería iniciarse automáticamente. Puedes verificar el estado del servicio ejecutando:

![Figura 18. Verificar el estado del servicio. Fuente: elaboración propia.](images/image-24.png)

*Figura 18. Verificar el estado del servicio. Fuente: elaboración propia.*

Si el servicio está activo y en ejecución, verás un mensaje que indica que el servicio está «active (running)».

Por defecto, vsftpd les permite a los usuarios locales iniciar sesión en el servidor FTP. Si deseas permitir que los usuarios anónimos se conecten al servidor FTP, debes editar el archivo de configuración /etc/vsftpd.conf y cambiar la configuración anonymous_enable a YES . Puedes abrir el archivo de configuración en un editor de texto con privilegios de superusuario.

Configuración de usuarios y contraseñas en FTP (vsftpd)

El servidor FTP vsftpd en Ubuntu también utiliza los usuarios del sistema para la autenticación. Si aún no lo has hecho, crea un usuario utilizando el comando adduser .

Para agregar un nuevo usuario al sistema en Ubuntu y configurar su contraseña, puedes seguir estos pasos utilizando el comando adduser . Este ejemplo creará un usuario llamado «usuario_ftp»:

Abre una terminal en tu sistema Ubuntu. Ejecuta el siguiente comando para agregar un nuevo usuario llamado «usuario_ftp»:

![Figura 19. Agregar un nuevo usuario. Fuente: elaboración propia.](images/image-25.png)

*Figura 19. Agregar un nuevo usuario. Fuente: elaboración propia.*

Sigue las instrucciones en pantalla. El sistema te pedirá que establezcas una contraseña para el nuevo usuario (coloca una contraseña fácil para que sea fácil hacer el ataque):

![Figura 20. Establecer contraseña. Fuente: elaboración propia.](images/image-26.png)

*Figura 20. Establecer contraseña. Fuente: elaboración propia.*

Después de establecer la contraseña, puedes proporcionar información adicional sobre el usuario (como nombre completo, número de teléfono, etc.) o simplemente presionar «Enter» para dejar los valores por defecto.

Confirma que la información es correcta presionando «Y» y luego «Enter». Ahora, el usuario «usuario_ftp» ha sido creado con la contraseña que estableciste.

Asegúrate de que el servicio vsftpd esté configurado para permitir la autenticación de usuarios locales. Abre el archivo de configuración /etc/vsftpd.conf en un editor de texto con privilegios de superusuario:

![Figura 21. Abrir el archivo de configuración /etc/vsftpd.conf. Fuente: elaboración propia.](images/image-27.png)

*Figura 21. Abrir el archivo de configuración /etc/vsftpd.conf. Fuente: elaboración propia.*

Asegúrate de que la configuración local_enable esté configurada como YES:

![Figura 22. Configuración local_enable. Fuente: elaboración propia.](images/image-28.png)

*Figura 22. Configuración local_enable. Fuente: elaboración propia.*

Reinicia el servicio vsftpd para aplicar los cambios:

![Figura 23. Reiniciar el servicio vsftpd. Fuente: elaboración propia.](images/image-29.png)

*Figura 23. Reiniciar el servicio vsftpd. Fuente: elaboración propia.*

Ahora, el usuario «usuario_ftp» (o cualquier otro usuario del sistema) podrá iniciar sesión en el servidor FTP utilizando la misma contraseña que estableciste para él.

Con estos pasos, has configurado usuarios y contraseñas para el servicio FTP en tu sistema Ubuntu. Los usuarios podrán iniciar sesión utilizando las credenciales que estableciste.

Para configurar la herramienta de ataque de fuerza bruta Medusa en tu máquina anfitriona y apuntar al servicio objetivo en tu máquina virtual, sigue estos pasos:

Instalación de Medusa: puedes instalar Medusa en Ubuntu utilizando el gestor de paquetes apt.

![Figura 24. Instalación de Medusa. Fuente: elaboración propia.](images/image-30.png)

*Figura 24. Instalación de Medusa. Fuente: elaboración propia.*

Configuración de Medusa:

Una vez que Medusa está instalado, puedes configurarlo para apuntar al servicio objetivo en tu máquina virtual. Por ejemplo, si deseas atacar el servicio SSH en la dirección IP 192.168.1.100 y el puerto SSH predeterminado 22 , el comando sería algo como esto:

![Figura 25. Configurar Medusa para apuntar al servicio objetivo. Fuente: elaboración propia.](images/image-31.png)

*Figura 25. Configurar Medusa para apuntar al servicio objetivo. Fuente: elaboración propia.*

-u <usuario> : especifica el nombre de usuario que se utilizará en el ataque.

-P <lista_de_contraseñas> : especifica el archivo que contiene la lista de contraseñas que se probarán en el ataque.

-h 192.168.1.100 : especifica la dirección IP del objetivo.

-M ftp : especifica el módulo para FTP.

Recuerda reemplazar <usuario> por el nombre de usuario que deseas probar y <lista_de_contraseñas> por el archivo que contiene las contraseñas que quieres probar. Además, asegúrate de ajustar la dirección IP y el puerto según la configuración de tu máquina virtual.

Con estos pasos, habrás configurado Medusa para apuntar al servicio objetivo en tu máquina virtual y estarás listo para ejecutar el ataque de fuerza bruta.

Contramedidas

Para proteger el servicio FTP en tu máquina virtual contra futuros ataques de fuerza bruta puedes implementar varias contramedidas. Una de las más efectivas es el uso d e fail2ban . Esta herramienta monitorea los archivos de registro en busca de patrones de intentos de inicio de sesión fallidos y bloquea automáticamente las direcciones IP que exceden un número permitido de intentos fallidos.

A continuación, se muestra cómo instalar y configurar fail2ban para proteger el servicio FTP (vsftpd):

Abre una terminal en tu máquina virtual. Actualiza el índice de paquetes:

![Figura 26. Actualizar el índice de paquetes. Fuente: elaboración propia.](images/image-32.png)

*Figura 26. Actualizar el índice de paquetes. Fuente: elaboración propia.*

Instala fail2ban:

![Figura 27. Instalar fail2ban. Fuente: elaboración propia.](images/image-33.png)

*Figura 27. Instalar fail2ban. Fuente: elaboración propia.*

Configuración de fail2ban para vsftpd

Crea una copia del archivo de configuración predeterminado de fail2ban para protegerlo de futuras actualizaciones.

![Figura 28. Configuración de fail2ban para vsftpd. Fuente: elaboración propia.](images/image-34.png)

*Figura 28. Configuración de fail2ban para vsftpd. Fuente: elaboración propia.*

Abre el archivo de configuración jail.local en un editor de texto con privilegios de superusuario:

![Figura 29. Archivo de configuración jail.local. Fuente: elaboración propia.](images/image-35.png)

*Figura 29. Archivo de configuración jail.local. Fuente: elaboración propia.*

Agrega la configuración para proteger el servicio vsftpd. Busca la sección [vsftpd] y, si no existe, agrégala al final del archivo:

Seguridad y Alta Disponibilidad 48 Tema 4. Entrenamientos enabled : activa la protección para vsftpd. port : especifica los puertos utilizados por el servicio FTP. filter : utiliza el filtro vsftpd para analizar los archivos de registro.

![Figura 30. Sección vsftpd. Fuente: elaboración propia.](images/image-36.png)

*Figura 30. Sección [vsftpd]. Fuente: elaboración propia.*

logpath : especifica la ubicación del archivo de registro de vsftpd . maxretry : establece el número máximo de intentos fallidos permitidos antes de que se bloquee la IP.

Guarda los cambios y cierra el editor de texto.

Configuración del filtro para vsftpd

Crea o edita el archivo del filtro vsftpd.conf :

![Figura 31. Crear o editar el archivo del filtro vsftpd.conf. Fuente: elaboración propia.](images/image-37.png)

*Figura 31. Crear o editar el archivo del filtro vsftpd.conf. Fuente: elaboración propia.*

Agrega el siguiente contenido al archivo para definir el patrón de detección de

![Figura 32. Contenido para definir el patrón de detección de intentos fallidos. Fuente: elaboración propia.](images/image-38.png)

*Figura 32. Contenido para definir el patrón de detección de intentos fallidos. Fuente: elaboración propia.*

intentos fallidos en los registros de vsftpd:

Esto le indica a fail2ban que busque líneas en los registros de vsftpd que coincidan con el patrón de intento de inicio de sesión fallido. Guarda los cambios y cierra el editor de texto.

Para que los cambios surtan efecto, reinicia el servicio fail2ban :

![Figura 33. Reiniciar el servicio fail2ban. Fuente: elaboración propia.](images/image-39.png)

*Figura 33. Reiniciar el servicio fail2ban. Fuente: elaboración propia.*

Verificar el funcionamiento

Para asegurarte de que fail2ban está protegiendo tu servicio vsftpd, puedes verificar

![Figura 34. Verificar el funcionamiento. Fuente: elaboración propia.](images/image-40.png)

*Figura 34. Verificar el funcionamiento. Fuente: elaboración propia.*

el estado de fail2ban y revisar las IPs bloqueadas:

Con fail2ban configurado, tu servicio FTP estará protegido contra los ataques de fuerza bruta, ya que las direcciones IP que realicen demasiados intentos fallidos serán bloqueadas temporalmente. Puedes ajustar la configuración (como el tiempo de bloqueo y el número máximo de intentos) según tus necesidades de seguridad.

## Entrenamiento 3: gestión de contraseñas seguras

## y directivas de seguridad en Windows

**▸ Planteamiento del ejercicio** Configura directivas de seguridad para contraseñas en Windows. Genera contraseñas seguras que cumplan requisitos específicos y evalúa su fortaleza. Utiliza el editor de políticas de grupo para establecer directivas de contraseña y bloqueo de cuenta. Documenta los pasos con capturas de pantalla y reflexiona sobre la importancia de la seguridad de contraseñas. Entrega un informe detallado.

**▸ Desarrollo paso a paso** Generación de contraseñas seguras Utiliza un generador de contraseñas en línea (por ejemplo, LastPass Password Generator) o una herramienta de línea de comandos. Genera al menos tres contraseñas que cumplan los siguientes requisitos:

**▸** Longitud mínima de doce caracteres.

**▸** Incluir letras mayúsculas y minúsculas.

**▸** Incluir números.

**▸** Incluir caracteres especiales. Evaluación de Contraseñas **▸** Utiliza Have I Been Pwned para verificar si alguna de las contraseñas ha sido comprometida anteriormente.

**▸** Evalúa la fortaleza de las contraseñas utilizando la web How Secure Is My Password ([https://howsecureismypassword.net/](https://howsecureismypassword.net/)). Directivas de seguridad en Windows: Para la configuración de directivas de contraseña en Windows, configura las siguientes:

**▸** Longitud mínima de la contraseña: doce caracteres.

**▸** Cumplimiento de requisitos de complejidad de contraseñas: habilitado.

**▸** Período de vigencia de la contraseña: sesenta días.

**▸** Historial de contraseñas: recordar cinco contraseñas anteriores. Sobre la configuración de directivas de bloqueo de cuenta en Windows, configura las siguientes directivas:

**▸** Umbral de bloqueo de cuenta: cinco intentos fallidos.

**▸** Duración del bloqueo de cuenta: treinta minutos.

**▸** Restablecer el contador de bloqueos de cuenta después de: treinta minutos. Comprobación y validación en Windows Intenta cambiar la contraseña de un usuario y verifica que se cumplen las nuevas directivas. Realiza intentos de inicio de sesión fallidos para verificar el bloqueo de la cuenta.

**▸ Solución** Generación de contraseñas seguras Utiliza un generador de contraseñas en línea (por ejemplo, LastPass Password Generator) o una herramienta de línea de comandos. Genera al menos tres contraseñas que cumplan los siguientes requisitos:

**▸** Longitud mínima de doce caracteres.

![Figura 35. Generación de contraseñas con LastPass Password Generator. Fuente: elaboración propia. ▸ Incluir letras mayúsculas y minúsculas. ▸ Incluir números. ▸ Incluir caracteres especiales.](images/image-41.png)

*Figura 35. Generación de contraseñas con LastPass Password Generator. Fuente: elaboración propia.*

Evaluación de contraseñas **▸** Utiliza Have I Been Pwned para verificar si alguna de las contraseñas ha sido comprometida anteriormente.

**▸** Evalúa la fortaleza de las contraseñas utilizando How Secure Is My Password.

![Figura 36. Verificar la contraseña con Have I Been Pwned. Fuente: elaboración propia.](images/image-42.png)

*Figura 36. Verificar la contraseña con Have I Been Pwned. Fuente: elaboración propia.*

Configuración de directivas de contraseña en Windows

Abre el editor de políticas de grupo: presiona Win + R , escribe gpedit.msc y presiona

Enter .

Navega a Configuración del Equipo -> Configuración de Windows -> Configuración de Seguridad ->

Directivas de Cuenta -> Directiva de Contraseña .

Configura las siguientes directivas:

**▸** Longitud mínima de la contraseña: doce caracteres.

**▸** Cumplimiento de requisitos de complejidad de contraseñas: habilitado.

**▸** Período de vigencia de la contraseña: sesenta días.

**▸** Historial de contraseñas: recordar cinco contraseñas anteriores.

Configuración de directivas de bloqueo de cuenta en Windows

Navega a Configuración del Equipo -> Configuración de Windows -> Configuración de Seguridad ->

Directivas de Cuenta -> Directiva de Bloqueo de Cuenta .

Configura las siguientes directivas:

**▸** Umbral de bloqueo de cuenta: cinco intentos fallidos.

**▸** Duración del bloqueo de cuenta: treinta minutos.

**▸** Restablecer el contador de bloqueos de cuenta después de: treinta minutos. Comprobación y validación en Windows Intenta cambiar la contraseña de un usuario y verifica que se cumplen las nuevas directivas. Realiza intentos de inicio de sesión fallidos para verificar el bloqueo de la cuenta.

## Entrenamiento 4: gestión de contraseñas seguras

## y directivas de seguridad en Ubuntu

**▸ Planteamiento del ejercicio** Configura directivas de seguridad para contraseñas en Ubuntu. Genera contraseñas seguras que cumplan requisitos específicos y evalúa su fortaleza. Configura «libpampwquality» y ajusta los archivos «common-password» y «common-auth». Documenta los pasos con capturas de pantalla y reflexiona sobre la importancia de la seguridad de las contraseñas. Entrega un informe detallado.

**▸ Desarrollo paso a paso** Generación de contraseñas seguras Utiliza un generador de contraseñas en línea (por ejemplo, LastPass Password Generator) o una herramienta de línea de comandos. Genera al menos tres contraseñas que cumplan los siguientes requisitos:

**▸** Longitud mínima de doce caracteres.

**▸** Incluir letras mayúsculas y minúsculas.

**▸** Incluir números.

**▸** Incluir caracteres especiales. Evaluación de Contraseñas **▸** Utiliza Have I Been Pwned para verificar si alguna de las contraseñas ha sido comprometida anteriormente.

**▸** Evalúa la fortaleza de las contraseñas utilizando la web How Secure Is My Password.

Configuración de directivas de seguridad en Ubuntu Instalaremos libpam-pwquality en Ubuntu para reforzar la seguridad de las contraseñas mediante la implementación de políticas de complejidad de contraseñas a través del módulo *pluggable authentication modules* (PAM). Este módulo permite configurar restricciones y requisitos específicos para las contraseñas, como la longitud mínima y la inclusión de caracteres especiales, mayúsculas, minúsculas y números. Configuración de políticas de contraseña:

**▸** Permitir tres intentos para ingresar una contraseña.

**▸** Longitud mínima de la contraseña.

**▸** Requerir al menos una letra mayúscula, una letra minúscula, un número y un carácter especial. Configuración de políticas de bloqueo de cuenta:

**▸** Bloquear la cuenta después de cinco intentos fallidos.

**▸** Desbloquear la cuenta después de treinta minutos. Comprobación y validación en Ubuntu:

**▸** Intenta cambiar la contraseña de un usuario y verifica que se cumplen las nuevas directivas.

**▸** Realiza intentos de inicio de sesión fallidos para verificar el bloqueo de la cuenta.

**▸** Solución Generación de contraseñas seguras Utiliza un generador de contraseñas en línea (por ejemplo, LastPass Password

Generator) o una herramienta de línea de comandos. Genera al menos tres contraseñas que cumplan los siguientes requisitos:

**▸** Longitud mínima de doce caracteres.

![Figura 37. Generación de contraseñas con LastPass Password Generator. Fuente: elaboración propia. ▸ Incluir letras mayúsculas y minúsculas. ▸ Incluir números. ▸ Incluir caracteres especiales.](images/image-43.png)

*Figura 37. Generación de contraseñas con LastPass Password Generator. Fuente: elaboración propia.*

Evaluación de contraseñas **▸** Utiliza Have I Been Pwned para verificar si alguna de las contraseñas ha sido comprometida anteriormente.

**▸** Evalúa la fortaleza de las contraseñas utilizando How Secure Is My Password.

![Figura 38. Verificar la contraseña con Have I Been Pwned. Fuente: elaboración propia.](images/image-44.png)

*Figura 38. Verificar la contraseña con Have I Been Pwned. Fuente: elaboración propia.*

Configuración de directivas de seguridad en Ubuntu:

**▸** Instalación de libpam-pwquality:

Abre una terminal. Ejecuta los siguientes comandos:

![Figura 39. Comandos. Fuente: elaboración propia.](images/image-45.png)

*Figura 39. Comandos. Fuente: elaboración propia.*

Configuración de políticas de contraseña **▸** Edita el archivo de configuración PAM:

![Figura 40. Configuración de políticas de contraseñas. Fuente: elaboración propia.](images/image-46.png)

*Figura 40. Configuración de políticas de contraseñas. Fuente: elaboración propia.*

**▸** Añade o modifica la línea que incluye pam_pwquality.so para establecer las siguientes directivas:

![Figura 41. Configuración de políticas de contraseñas. Fuente: elaboración propia.](images/image-47.png)

*Figura 41. Configuración de políticas de contraseñas. Fuente: elaboración propia.*

retry=3: permitir tres intentos para ingresar una contraseña. minlen=12 : longitud mínima de la contraseña. ucredit=-1 , lcredit=-1 , dcredit=-1 , ocredit=-1 : se requiere al menos una letra mayúscula, una letra minúscula, un número y un carácter especial. Configuración de políticas de bloqueo de cuenta:

**▸** Edita el archivo /etc/pam.d/common-auth:

![Figura 42. Configuración de políticas de bloqueo de cuenta. Fuente: elaboración propia.](images/image-48.png)

*Figura 42. Configuración de políticas de bloqueo de cuenta. Fuente: elaboración propia.*

**▸** Añade las siguientes líneas:

![Figura 43. Configuración de políticas de bloqueo de cuenta. Fuente: elaboración propia.](images/image-49.png)

*Figura 43. Configuración de políticas de bloqueo de cuenta. Fuente: elaboración propia.*

deny=5 : bloquear la cuenta después de cinco intentos fallidos. unlock_time=1800 : desbloquear la cuenta después de treinta minutos.

Comprobación y validación en Ubuntu: **▸** Intenta cambiar la contraseña de un usuario y verifica que se cumplen las nuevas directivas. **▸** Realiza intentos de inicio de sesión fallidos para verificar el bloqueo de la cuenta.

## Entrenamiento 5: configuración de contraseña en

## la BIOS

**▸ Planteamiento del ejercicio** Los estudiantes deberán establecer contraseñas de supervisor y usuario, habilitar *secure boot,* activar el TPM si está disponible, desactivar los puertos de arranque externos y realizar una actualización de *firmware.* Además, deberán investigar y elaborar un informe sobre las mejores prácticas para la configuración de seguridad en la BIOS/UEFI, en el cual destaquen la importancia de cada medida implementada. La actividad se evaluará según la correcta configuración de la BIOS/UEFI, la calidad del informe y la comprensión de las medidas de seguridad. **Notas:**

**▸ Precaución:** asegúrate de recordar la contraseña que configures. Olvidar la contraseña de la BIOS puede requerir procedimientos complicados para resetearla.

**▸ Diferencias de BIOS/UEFI:** ten en cuenta que las interfaces de BIOS/UEFI pueden variar considerablemente entre diferentes fabricantes y modelos de ordenadores. **Preguntas de reflexión:**

**▸** ¿Por qué es importante establecer una contraseña en la BIOS?

**▸** ¿Cuáles son las diferencias entre una *supervisor password* y una *user password?*

**▸** ¿Qué medidas adicionales podrías tomar para asegurar la BIOS/UEFI?

**▸** ¿Qué harías si olvidaras la contraseña de la BIOS? Investiga los métodos para resetearla.

**Tareas adicionales:**

**▸** Investiga cómo las configuraciones de seguridad en la BIOS pueden integrarse con otras medidas de seguridad, como el cifrado de disco completo.

**▸** Escribe un breve informe (una página) sobre las mejores prácticas para la configuración de seguridad en la BIOS/UEFI.

**▸ Desarrollo paso a paso**

1. Acceso a la BIOS/UEFI.

2. Busca la sección de seguridad o security.

3. Dentro de la sección de seguridad, busca las opciones para configurar contraseñas.

4. Ingresa la nueva contraseña.

5. Reinicia el ordenador e intenta acceder a la BIOS/UEFI nuevamente para asegurarte de que la contraseña se ha configurado correctamente.

**▸ Solución**

**▸** Acceso a la BIOS/UEFI: Reinicia tu ordenador. Durante el proceso de arranque, presta atención a las instrucciones en pantalla para determinar la tecla específica para acceder a la BIOS/UEFI. Esta tecla generalmente es Delete , F2 , F10 , Esc , o F12 . Presiona la tecla correspondiente repetidamente hasta que aparezca la pantalla de la BIOS/UEFI.

**▸** Navegación en la BIOS/UEFI: Una vez dentro de la BIOS/UEFI, utiliza las teclas de dirección (usualmente las

Seguridad y Alta Disponibilidad 63 Tema 4. Entrenamientos flechas) para navegar por los menús. Busca la sección de seguridad o *security.* Dependiendo de tu BIOS/UEFI, esta sección podría estar ubicada en diferentes lugares.

**▸** Configuración de contraseña:

Dentro de la sección de seguridad, busca las

opciones relacionadas con la

configuración de contraseñas. Estas opciones pueden variar según la BIOS/UEFI, pero comúnmente se denominan: *supervisor password* o *administrator password,* la cual controla el acceso completo a la BIOS, y *user password,* la cual controla el acceso al sistema operativo.

Selecciona la opción que desees configurar, por ejemplo, *supervisor password.*

**▸** Establecimiento de la contraseña:

Una vez dentro de la opción seleccionada (por ejemplo, *supervisor password),* elige la opción para crear una nueva contraseña. Ingresa la nueva contraseña cuando se te solicite. Asegúrate de que sea segura y difícil de adivinar.

Confirma la contraseña ingresándola nuevamente cuando se te indique. Guarda los cambios y sal de la BIOS/UEFI. En la mayoría

de los casos, esto se realiza

seleccionando una opción como «Save & Exit» o presionando F10 y confirmando con Yes .

**▸** Verificación:

Reinicia el ordenador. Intenta acceder a la BIOS/UEFI nuevamente para asegurarte de que la contraseña se ha configurado correctamente. También verifica si se solicita la contraseña al iniciar el sistema operativo.

**▸** Preguntas de reflexión:

¿Por qué es importante establecer una contraseña en la BIOS? Configurar una

Seguridad y Alta Disponibilidad 64 Tema 4. Entrenamientos contraseña en la BIOS es importante porque protege el acceso al *hardware* y a la configuración del sistema en un nivel fundamental. Sin esta contraseña, cualquier persona que tenga acceso físico al equipo podría cambiar la configuración de la BIOS, lo que podría resultar en cambios no deseados en el funcionamiento del sistema o incluso en la instalación de *software* malicioso. Además, al establecer una contraseña en la BIOS, se dificulta el acceso no autorizado al sistema operativo, ya que el acceso a la configuración de arranque también está protegido.

¿Cuáles son las diferencias entre una *supervisor password* y una *user password?*

L a *supervisor password* (contraseña de supervisor o administrador) proporciona acceso completo a la BIOS, lo que permite realizar cambios en la configuración del *hardware* y del sistema, así como en la configuración de arranque. La *user password* (contraseña de usuario) suele estar asociada con el sistema operativo. Requiere que sea ingresada antes de que el sistema operativo pueda cargarse. Esto evita que personas no autorizadas inicien sesión en el sistema y accedan a los datos del usuario.

¿Qué medidas adicionales podrías tomar para asegurar la BIOS/UEFI? Además de configurar contraseñas, otras medidas para asegurar la BIOS/UEFI incluyen:

**Actualización de la BIOS:** mantener la BIOS actualizada con las últimas versiones de *firmware* ayuda a corregir las posibles vulnerabilidades de seguridad.

**Habilitar** ***secure boot:*** esta característica ayuda a prevenir la ejecución de *software* no autorizado durante el proceso de arranque.

**Habilitar la protección de escritura:** algunas

BIOS/UEFI tienen la opción de

proteger la configuración contra escritura, lo que evita cambios no autorizados.

**Desactivar los puertos de arranque externos:** al desactivar los puertos USB y otros dispositivos de almacenamiento como opciones de arranque, se reduce el riesgo de que se instalen sistemas operativos no autorizados.

¿Qué harías si olvidaras la contraseña de la BIOS? Si olvidas la contraseña de la BIOS, puedes intentar resetearla utilizando métodos específicos según el fabricante de la placa base o del equipo. Algunas opciones comunes incluyen:

***Jumper Clear*** **CMOS:** algunas placas base tienen un *jumper* que se puede mover temporalmente para borrar la configuración de la BIOS, incluyendo la contraseña.

**Quitar la batería CMOS:** el retirar la batería de la placa base durante unos minutos puede borrar la configuración de la BIOS.

**Utilizar contraseñas maestras:** en algunos casos, el fabricante puede proporcionar contraseñas maestras que permiten el acceso a la BIOS, incluso si se ha olvidado la contraseña.

**▸ Tarea adicional:** integración de la configuración de seguridad en la BIOS con el cifrado de disco completo.

Integración de la seguridad en la BIOS/UEFI con el cifrado de disco completo:

El cifrado de disco completo (FDE, por sus siglas en inglés) es una técnica de seguridad que encripta todos los datos almacenados en un disco duro o unidad de almacenamiento, lo que hace que sea ilegible para cualquier persona que no tenga la clave de cifrado correspondiente. Integrar

esta medida de seguridad con la

configuración de la BIOS/UEFI puede fortalecer aún más la protección del sistema. Aquí hay una guía sobre cómo hacerlo:

**Habilitar secure** ***boot:*** en la BIOS/UEFI, asegúrate de tener la opción de *secure* *boot* habilitada. Esta opción ayuda a prevenir la ejecución de *software* no autorizado durante el proceso de arranque del sistema.

**Configurar la contraseña en la BIOS/UEFI:** establece una contraseña en la BIOS/UEFI para proteger la configuración del *hardware* y del sistema. Esto ayudará a

Seguridad y Alta Disponibilidad 66 Tema 4. Entrenamientos prevenir el acceso no autorizado a la BIOS/UEFI, lo que podría comprometer la seguridad del sistema.

**Habilitar** ***trusted platform module*** **(TPM):** si tu placa base tiene un módulo TPM, asegúrate de tenerlo habilitado en la BIOS/UEFI. El TPM proporciona funciones de seguridad adicionales, como el almacenamiento seguro de claves de cifrado.

**Configurar el cifrado de disco completo:** utiliza herramientas de cifrado de disco completo como BitLocker (para Windows) o LUKS (para Linux) para encriptar todo el disco duro o la partición del sistema. Durante este proceso, se te pedirá que elijas una contraseña de cifrado.

**Configurar la contraseña de inicio de sesión:** además de la contraseña de la BIOS/UEFI, configura una contraseña de inicio de sesión en el sistema operativo. Esto añade una capa adicional de seguridad y garantiza que, incluso si un atacante logra acceder a la BIOS/UEFI y arrancar el sistema, aún necesitará la contraseña de inicio de sesión para acceder a los datos.

**Realizar pruebas y mantenimiento:** una vez configuradas todas estas medidas de seguridad, realiza pruebas para asegurarte de que el sistema funcione correctamente. Además, asegúrate de mantener actualizadas tanto la BIOS/UEFI como las herramientas de cifrado de disco completo para garantizar la máxima seguridad.

Beneficios de la integración:

La integración de la configuración de seguridad en la BIOS/UEFI con el cifrado de disco completo proporciona una defensa en capas que protege el sistema desde el momento del arranque hasta el acceso a los datos almacenados. Al unir estas medidas de seguridad, se crea un entorno más resistente contra posibles amenazas, las cuales incluyen el acceso no autorizado y el robo de datos.

Esta tarea adicional demuestra la importancia de adoptar un enfoque holístico de la

Seguridad y Alta Disponibilidad 67 Tema 4. Entrenamientos seguridad, con la combinación de múltiples medidas para crear una defensa robusta contra posibles amenazas.

**▸** Informe sobre las mejores prácticas para la configuración de seguridad en la BIOS/UEFI

L a *basic input/output system* (BIOS) o su sucesora moderna, la *unified extensible* *firmware interface* (UEFI), son componentes fundamentales en cualquier sistema informático, ya que gestionan la interacción básica entre el *hardware* y el *software.* La configuración adecuada de la seguridad en la BIOS/UEFI es crucial para proteger al sistema contra accesos no autorizados y garantizar la integridad de los datos almacenados. En este informe se presentan las mejores prácticas para lograr una configuración de seguridad efectiva en la BIOS/UEFI.

**Establecimiento de contraseñas:** configurar contraseñas en la BIOS/UEFI es una medida fundamental de seguridad. Se recomienda establecer tanto una *supervisor* *password* como una *user password* para controlar el acceso a la configuración del sistema y al sistema operativo, respectivamente. Estas contraseñas deben ser fuertes y difíciles de adivinar, con la combinación de letras, números y caracteres especiales.

**Habilitar** ***secure boot:*** esta es una característica que garantiza que solo se ejecuten los controladores y los sistemas operativos firmados y confiables durante el proceso de arranque. Habilitar *secure boot* en la BIOS/UEFI ayuda a prevenir la carga de software malicioso durante el arranque del sistema.

**Utilizar TPM:** si el *hardware* es compatible, habilitar el TPM en la BIOS/UEFI proporciona una capa adicional de seguridad al almacenar de manera segura las claves de cifrado y las medidas de integridad del sistema. Esto ayuda a proteger contra ataques como la manipulación de claves de cifrado y el robo de datos.

**Desactivar puertos de arranque externos:** desactivar los puertos de arranque

Seguridad y Alta Disponibilidad 68 Tema 4. Entrenamientos externos como USB o CD/DVD-ROM en la BIOS/UEFI evita que un atacante inicie el sistema desde dispositivos externos y acceda a datos sensibles o realice cambios no autorizados en el sistema.

**Actualizar regularmente la BIOS/UEFI:** mantener actualizada la BIOS/UEFI con las últimas versiones de *firmware* proporciona parches de seguridad y correcciones de vulnerabilidades, lo que garantiza un entorno más seguro y estable.

**Realizar copias de seguridad de la configuración:** realizar copias de seguridad de la configuración de la BIOS/UEFI es crucial en caso de necesitar restaurarla después de un error o una configuración incorrecta. Muchas BIOS/UEFI ofrecen esta opción y se recomienda realizar copias de seguridad regularmente.

En conclusión, la configuración de seguridad en la BIOS/UEFI es un aspecto crítico de la seguridad de un sistema informático. Al seguir estas mejores prácticas, se puede fortalecer la protección del sistema contra accesos no autorizados, ataques de *firmware* y manipulación de datos. Es fundamental que los administradores de sistemas y los usuarios finales comprendan la importancia de estas medidas de seguridad y las implementen adecuadamente para mantener la integridad y la confidencialidad de los datos.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–26)*
- A fondo  *(pp.27–31)*
- Entrenamientos  *(pp.32–69)*
- Seguridad y Alta Disponibilidad 5 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 6 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 7 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 8 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 9 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 10 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 11 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 12 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 13 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 14 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 15 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 16 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 17 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 18 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 19 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 20 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 21 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 22 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 23 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 24 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 25 Tema 4. Material de estudio · Seguridad y Alta Disponibilidad 26 Tema 4. Material de estudio  *(pp.5–26)*
- Seguridad y Alta Disponibilidad 27 Tema 4. A fondo · Seguridad y Alta Disponibilidad 28 Tema 4. A fondo · Seguridad y Alta Disponibilidad 29 Tema 4. A fondo · Seguridad y Alta Disponibilidad 30 Tema 4. A fondo · Seguridad y Alta Disponibilidad 31 Tema 4. A fondo  *(pp.27–31)*
- Seguridad y Alta Disponibilidad 32 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 33 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 34 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 35 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 36 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 38 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 39 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 40 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 41 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 42 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 43 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 44 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 45 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 46 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 47 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 49 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 50 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 51 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 52 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 53 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 54 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 55 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 56 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 57 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 58 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 59 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 60 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 61 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 62 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 65 Tema 4. Entrenamientos · Seguridad y Alta Disponibilidad 69 Tema 4. Entrenamientos  *(pp.32, 33, 34, 35, 36, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 65, 69)*