## Tema

## Seguridad y Alta Disponibilidad

# Tema 5. Criptografía

# Índice

Esquema Material de estudio

## 5.1. Introducción y objetivos

## 5.2. Principios de la criptografía

## 5.3. Cifrado simétrico y asimétrico

## 5.4. Funciones hash y firma digital

## 5.5. Referencias bibliográficas

A fondo

¿Qué es la criptografía?

Distintos tipos de cifrado

Encriptación asimétrica: clave pública y privada

explicación Cifrado simétrico y asimétrico: cinco diferencias Public key cryptography: Diffie-Hellman key exchange Certificación digital DNI electrónico ¿Qué es el hash? ¿Cómo se genera el hash? Cifrado. Software Cifrado de extremo a extremo ¿qué significa y cómo funciona? Entrenamientos Entrenamiento 1: cifrado simétrico

Entrenamiento 2: cifrado de ficheros con algoritmos asimétricos usando GPG en Ubuntu

Entrenamiento 3: firma de ficheros

Entrenamiento 4: encriptación simétrica en Ubuntu

Entrenamiento 5: SSH con clave pública

# Esquema

![image-2](images/image-2.png)

Seguridad y Alta Disponibilidad 4 Tema . Esquema

## 5.1. Introducción y objetivos

En un mundo cada vez más interconectado

y digitalizado, la seguridad de la

información se ha convertido en una preocupación fundamental. En respuesta a esta creciente necesidad, la criptografía emerge

como un **pilar indispensable** en la

protección de datos sensibles y en la garantía de la privacidad y la confidencialidad en línea. Este arte y ciencia del cifrado y descifrado de información no solo se remonta a las raíces de las matemáticas y

la informática, sino que también

evoluciona constantemente para hacer frente a los desafíos de un entorno digital en constante cambio.

Desde los antiguos jeroglíficos egipcios hasta los modernos estándares de cifrado como AES y RSA, la criptografía ha desempeñado un papel crucial en la historia, en cuanto a asegurar la comunicación militar

hasta proteger las transacciones

financieras en línea. En este contexto, el presente documento se propone explorar exhaustivamente los fundamentos de la criptografía, desde los conceptos básicos como el texto en claro y el cifrado, hasta los algoritmos de cifrado simétrico y asimétrico más utilizados en la actualidad.

Además de abordar el proceso de encriptación y desencriptación, se analizarán en detalle las funciones *hash* y las firmas digitales, componentes esenciales en la protección de la integridad y la autenticidad de la información en un mundo digital. Asimismo, se examinarán las fortalezas y debilidades de diferentes algoritmos, así como los desafíos inherentes a la distribución segura de claves y la autenticación de los mensajes electrónicos.

En resumen, este documento aspira a proporcionar una visión completa de la criptografía y su relevancia en la protección de la información sensible en un entorno digital en constante evolución, al destacar

su papel crucial en la seguridad

informática y la preservación de la privacidad en línea.

Los objetivos que se pretenden alcanzar en este tema son:

**▸** Desarrollar y usar algoritmos de cifrado.

**▸** Cifrar y descifrar mensajes.

**▸** Entender la historia y evolución de la criptografía.

**▸** Comprender los fundamentos de la criptografía.

**▸** Distinguir entre criptografía simétrica y asimétrica.

**▸** Explorar los principales algoritmos criptográficos.

**▸** Analizar los problemas y desafíos en la seguridad de la información.

**▸** Definir y explicar el concepto de *hash.*

**▸** Describir las características de los algoritmos *hash* comunes.

**▸** Introducir el concepto de firma digital.

**▸** Resaltar la importancia de las firmas digitales.

**▸** Asimilar conceptos como criptoanálisis y esteganografía.

## 5.2. Principios de la criptografía

Concepto de criptografía

La criptografía representa tanto un arte como una ciencia que se dedica a codificar y descodificar datos mediante técnicas especializadas. Su utilidad principal radica en facilitar el **intercambio de mensajes confidenciales** entre partes específicas, las cuales disponen de los medios para descifrarlos.

Además de su función en la comunicación segura, la criptografía se emplea con frecuencia para **cifrar información almacenada** en diferentes dispositivos, para garantizar así su privacidad y confidencialidad.

Esta disciplina se enmarca en las matemáticas y, en la actualidad, en la informática y telemática, ya que se vale de métodos y técnicas matemáticas para encriptar mensajes o archivos mediante algoritmos que requieren una o más claves.

La criptografía, aunque a menudo se asocia con el mundo de los espías y agencias como la Agencia de Seguridad Nacional (NSA), desempeña un papel fundamental en nuestra vida diaria. Por ejemplo, cuando utilizamos servicios como Gmail, establecemos una comunicación segura y cifrada entre nuestro dispositivo y los servidores de Google. Del mismo modo, al realizar una llamada desde nuestro teléfono móvil, los datos que transmitimos están encriptados, lo que evita que terceros no autorizados puedan interceptar nuestras conversaciones.

La principal función de la criptografía es proteger los mensajes mediante la codificación, lo que asegura que su contenido no es accesible para personas no autorizadas. Para lograr esto, se utilizan códigos y algoritmos de cifrado que confunden la información y la protegen de cualquier intento de acceso no autorizado.

Terminología

En el ámbito de la criptografía, se encuentran los siguientes elementos clave:

**▸ Texto en claro o texto plano:** es la información original que se desea proteger.

**▸ Cifrado:** proceso de transformar el texto en claro en un texto ilegible, conocido como texto cifrado o criptograma. Este procedimiento se basa en un algoritmo de cifrado que utiliza una clave para adaptarse a cada uso específico.

**▸ Algoritmos de cifrado:** se dividen en dos categorías principales.

- Cifrado en bloque: divide el texto en claro en bloques de bits de un tamaño fijo y los cuales son cifrados de forma independiente.

- Cifrado de flujo: cifra los datos bit a bit, byte a byte o carácter a carácter.

**▸ Técnicas básicas de cifrado en criptografía clásica:**

- Sustitución: cambia el significado de los elementos básicos del mensaje, como letras, dígitos o símbolos.

- Transposición: reordena los elementos básicos sin modificar su contenido.

**▸ Descifrado:** proceso inverso que recupera el texto en claro a partir del criptograma y la clave.

**▸ Criptología:** campo más amplio que incluye al criptoanálisis, el cual se centra en romper codificaciones realizadas por terceros sin conocer la clave.

**▸ Esteganografía:** práctica de ocultar mensajes dentro de canales inseguros para que pasen desapercibidos. El estegoanálisis, por otro lado, busca detectar mensajes ocultos mediante esteganografía.

Historia

La historia de la criptografía se remonta a más de 4 000 años atrás, mucho antes de que aparecieran figuras como Alan Turing, Claude Shannon o la NSA (figuras relevantes relacionadas con la criptografía).

La palabra *criptografía* proviene del

griego *krypto,* que significa 'oculto', y *graphos,* que significa 'escribir', lo que se traduce como 'escritura oculta'.

El cifrado de mensajes asegura que solo el emisor y el receptor puedan entender la información transmitida, con lo cual se **mantiene el contenido oculto** para cualquier **persona externa.** Esto se logra haciendo que el mensaje aparezca descompuesto y sin sentido para los que no están autorizados.

Así, los **jeroglíficos del antiguo Egipto** se consideran uno de los primeros ejemplos de «escritura oculta» en la historia. La piedra de Rosetta fue crucial para descifrar estos jeroglíficos.

![Figura 1. Jeroglífico egipcio. Fuente: Orientación Andújar, 2012.](images/image-3.png)

*Figura 1. Jeroglífico egipcio. Fuente: Orientación Andújar, 2012.*

En el libro de Jeremías de la **Biblia** se hace mención del Atbash, que era un sistema de **sustitución de letras** utilizado para cifrar mensajes (año 600 a. C.). En la misma época, en los reinos Mahajanapadas de la India, también se encontraron ejemplos de cifrado por sustitución de letras.

En la ***Ilíada*** de Homero, se menciona el uso de cifrado de mensajes cuando Belerofonte entrega una carta cifrada por el rey Preto de Tirinto al rey Ióbates de Licia. El contenido de la carta es secreto y cifrado, ocultando el mensaje de que se debe dar muerte a Belerofonte, el portador.

L o s **espartanos** empleaban la criptografía para proteger sus comunicaciones, utilizando una técnica conocida como **cifrado por transposición.** En este método el mensaje se escribía en un pergamino que se enrollaba alrededor de una estaca llamada excítala, lo cual ordenaba las letras de manera específica. Para descifrar el mensaje, el receptor necesitaba una excítala del mismo diámetro que la del emisor (criptografía simétrica que veremos más adelante), con lo cual se aseguraba que el mensaje se visualizara correctamente. Tanto el emisor como el receptor utilizaban un método similar para ocultar y mostrar el mensaje.

![Figura 2. Excítala griega. Fuente: Luringen, 2007.](images/image-4.png)

*Figura 2. Excítala griega. Fuente: Luringen, 2007.*

El **cifrado César,** cuyo nombre alude directamente a Julio César, tiene su origen en la antigua Roma. Este método criptográfico se fundamenta en desplazar cada letra del texto original un número fijo de posiciones en el alfabeto.

![Figura 3. Cifrado por transposición. Fuente: Doncherry, 2013.](images/image-5.png)

*Figura 3. Cifrado por transposición. Fuente: Doncherry, 2013.*

En la Edad Media, la criptografía experimentó una notable evolución en el mundo árabe. En el siglo IX, **Al-Kindi** sentó una de las bases fundamentales para el análisis de mensajes cifrados mediante el estudio del Corán. Introdujo técnicas como el **análisis de frecuencias,** utilizadas más adelante durante la Segunda Guerra Mundial, para identificar patrones en mensajes cifrados y correlacionar la frecuencia de las letras con la probabilidad de aparición en un texto en particular.

En el **Renacimiento,** los Estados Pontificios se destacaron por su **uso intensivo de** **la criptografía,** con lo cual desarrollaron sistemas como el cifrado de Alberti, que empleaba discos mecánicos para codificar y descodificar información.

La **Primera** y la **Segunda Guerra Mundial** fueron períodos cruciales en la evolución de la criptografía, desde métodos relativamente simples hasta sistemas avanzados y máquinas de cifrado que definieron el campo en las décadas siguientes. Estos conflictos también marcaron un punto de inflexión en el desarrollo de técnicas de criptoanálisis que se aplicarían posteriormente en la Guerra Fría y más allá.

Antes de la Primera Guerra Mundial, la criptografía se basaba principalmente en métodos clásicos como el cifrado por sustitución y transposición. Estos métodos eran relativamente simples y a menudo podían ser descifrados con suficiente tiempo y recursos. Con el estallido de la guerra en 1914, la **importancia de la comunicación** **segura** se hizo evidente. Los países participantes comenzaron a invertir más en el desarrollo de sistemas de cifrado más avanzados. Hubo un aumento significativo en el número de criptoanalistas, personas especializadas en romper códigos enemigos. Entre los más destacados estaba Room 40 en el Reino Unido, que jugó un papel crucial en la interceptación y descifrado de mensajes alemanes.

La Segunda Guerra Mundial vio un avance significativo en la criptografía con la **máquina Enigma** de los alemanes, que fue un desafío enorme para los aliados en términos de criptoanálisis. Los británicos, liderados por Alan Turing en Bletchley Park, jugaron un papel crucial en descifrar las comunicaciones Enigma, lo que tuvo un impacto decisivo en el curso de la guerra. Además de Enigma, se desarrollaron o t r o s **sistemas avanzados de cifrado y criptoanálisis,** incluidos métodos estadounidenses como las máquinas de cifrado SIGABA y las contribuciones de otros países aliados para mejorar las técnicas de descifrado. El uso de la criptografía fue fundamental para mantener la ventaja estratégica y la confidencialidad de las operaciones militares, diplomáticas y de inteligencia en ambos bandos.

![Figura 4. Máquina Enigma. Fuente: Ayuntamiento de Valladolid, 2016.](images/image-6.png)

*Figura 4. Máquina Enigma. Fuente: Ayuntamiento de Valladolid, 2016.*

## 5.3. Cifrado simétrico y asimétrico

¿Qué significa encriptar (cifrar) y desencriptar (descifrar)?

Encriptar significa transformar un texto en otro no entendible a simple vista. Para transformar el texto en otro se usan mecanismos criptográficos, el objetivo es que el texto resultante **no pueda ser interpretado** a no ser que se disponga de una «clave» para desencriptarlo y así volverlo al texto original.

Para poder encriptar y desencriptar un texto es necesario un algoritmo que permita encriptar y luego, basándose en dicho algoritmo y la «clave» con la que se encriptó, se podrá llevar a cabo la desencriptación.

Algoritmo criptográfico

Un algoritmo criptográfico es un **método matemático** utilizado para ocultar y revelar mensajes. Normalmente funciona usando una o más claves (como una combinación de números y/o cadenas de texto) como parte del proceso, de manera que estas claves son necesarias para poder ver el mensaje original a partir de su versión oculta.

El mensaje antes de ser ocultado se llama texto claro y una vez ocultado se conoce como texto cifrado.

Sistema criptográfico

Un sistema criptográfico, por su parte, es un conjunto organizado de estos algoritmos criptográficos, claves y, posiblemente, varios mensajes en texto claro junto con sus correspondientes versiones cifradas.

Hoy en día, los sistemas criptográficos se basan en **tres tipos principales de** **algoritmos:**

**▸ Simétricos (o de clave simétrica o privada):** transforman un mensaje en un texto cifrado que tiene el mismo tamaño que el mensaje original. Estos algoritmos utilizan una única clave tanto para cifrar como para descifrar el mensaje. Son ideales para asegurar la transferencia segura de grandes cantidades de información.

**▸ Asimétricos (o de clave asimétrica o pública):** encriptan un mensaje generando un texto cifrado del mismo tamaño que el original. Utilizan dos claves diferentes, una clave privada para cifrar el mensaje y una clave pública para descifrarlo. Tienen un costo computacional más alto y generalmente se usan para distribuir claves seguras para ser utilizadas por los algoritmos simétricos.

**▸ Resumen de mensajes (funciones de dispersión o** ***hash):*** estos transforman mensajes de longitud variable en textos cifrados de longitud fija. En su proceso no se utilizan claves. Son útiles para convertir mensajes extensos en una «equivalencia de ese mensaje» más manejable y son ampliamente utilizados en la verificación de integridad y el almacenamiento seguro de contraseñas, entre otros usos.

Algoritmos de cifrado simétrico

#### Principios de la criptografía simétrica

La criptografía simétrica implica el **uso de una única clave** tanto para cifrar como para descifrar mensajes. Ambas partes comunicantes deben acordar esta clave de antemano. Una vez que ambas tienen acceso a la clave, el remitente cifra un mensaje con ella, lo envía al destinatario y este último lo descifra utilizando la misma clave.

En este método, **toda la seguridad reside en la clave,** no en el algoritmo de cifrado. Por lo tanto, es crucial que la clave sea altamente difícil de adivinar. Esto significa que el espacio de claves posibles debe ser amplio y debe estar determinado por la longitud y la variedad de caracteres utilizados.

Hoy en día, los ordenadores son capaces de descifrar claves con gran rapidez, lo que destaca la importancia del tamaño de la clave en los criptosistemas modernos.

![Figura 5. Encriptación simétrica. Fuente: Prado, 2022a.](images/image-7.png)

*Figura 5. Encriptación simétrica. Fuente: Prado, 2022a.*

#### Principales problemas de la criptografía simétrica

**▸ Intercambio seguro de claves:** el intercambio seguro de claves es crítico en la criptografía simétrica. Si un tercero intercepta las claves durante el intercambio, la seguridad del sistema se ve comprometida. Los métodos comunes para resolver este problema incluyen el uso de canales seguros o el cifrado de las claves durante la transmisión.

**▸ Número de claves necesarias:** a medida que el número de participantes en la comunicación aumenta, la cantidad de claves necesarias crece exponencialmente. Esto se debe a que cada par de participantes necesita su propia clave única. Este problema se vuelve especialmente difícil de manejar en grandes redes, en las que el número de claves necesarias se vuelve poco práctico.

Estos desafíos han llevado al desarrollo de otras técnicas criptográficas. La criptografía simétrica sigue siendo valiosa en muchas aplicaciones, pero es importante comprender y abordar sus limitaciones.

#### Algoritmos simétricos existentes

**▸** El algoritmo de cifrado **Data Encryption Standard (DES)** utiliza una clave de 56 bits, lo que implica un total de 256 (72 057 594 037 927 936) posibles claves. Aunque es un número considerablemente grande, los computadores genéricos pueden probar todas estas combinaciones en cuestión de días.

**▸** Algoritmos como **3DES, Blowfish** e **IDEA** emplean claves de 128 bits, lo que significa que hay 2128 combinaciones posibles de claves. 3DES es comúnmente utilizado en tarjetas de crédito y otros sistemas de pago electrónico.

**▸** Otros algoritmos de cifrado ampliamente utilizados incluyen **RC5** y ***Advanced*** ***encryption standard*** (AES), desarrollado como estándar por el Gobierno de los Estados Unidos bajo el nombre Rijndael.

#### Información complementaria sobre algoritmos de cifrado simétricos

**▸ Estándar de encriptación de datos** (DES) y **algoritmo de encriptación de datos** (DEA): es uno de los algoritmos de cifrado simétrico más reconocidos y ampliamente utilizados. Se basa en cifrar bloques de 64 bits utilizando una clave de 56 bits. Aunque originalmente fue considerado seguro, con el tiempo se descubrió que es vulnerable a ataques de fuerza bruta debido al tamaño de su clave. Como solución, surgió el triple DES.

**▸ Triple-DES:**

- DES-EEE3: tres cifrados DES con claves diferentes.

- DES-EDE3: secuencia de cifrado-descifrado-cifrado con tres claves distintas.

- DES-EEE2 y DES-EDE2: similar al anterior, pero reutiliza una clave.

El DES-EEE3 se considera el más seguro de estos métodos.

**▸ Estándar criptográfico avanzado** (AES): algoritmo propuesto para reemplazar a DES. Aunque aún se encuentran en proceso de selección, existen quince propuestas en consideración.

**▸ RC2:** fue diseñado por Ron Rivest, se trata de un algoritmo de cifrado por bloques con una clave de tamaño ajustable. Es más rápido que el DES y su seguridad puede ajustarse mediante el tamaño de la clave.

**▸ RC4:** algoritmo de cifrado de flujo también creado por Rivest. Es conocido por su rapidez y se usa en protocolos como SSL (TLS).

**▸ RC5:** este algoritmo, de Ron Rivest, es notable por su flexibilidad, por lo que permite ajustar el tamaño del bloque, la clave y el número de rotaciones. Es resistente a diversos métodos de ataque criptográfico.

**▸** ***International data encryption algorithm*** **(IDEA):** algoritmo de cifrado por bloques con una clave de 128 bits. Es robusto frente a muchos ataques criptográficos y es eficiente tanto en *hardware* como en *software.*

**▸ SAFER:** un algoritmo de cifrado por bloques que se centra en la velocidad y seguridad. Aunque se creía resistente a ciertos ataques, se descubrió una debilidad que llevó a su modificación.

**▸ Blowfish:** desarrollado por Scheiner, este algoritmo de cifrado por bloques de 64 bits es conocido por su velocidad en máquinas de 32 bits. Aunque se considera seguro, se han identificado ciertas vulnerabilidades en versiones específicas del algoritmo.

#### ¿Dónde se utilizan los algoritmos simétricos?

Los algoritmos simétricos se utilizan en una variedad de aplicaciones para proteger la confidencialidad y la integridad de los datos. Algunos de los **principales usos** de los algoritmos simétricos son:

**▸ Comunicaciones seguras:** los algoritmos simétricos se utilizan para cifrar datos transmitidos a través de redes, como correos electrónicos, mensajería instantánea, transacciones en línea y transferencias de archivos, lo que garantiza que solo los destinatarios autorizados puedan acceder a la información.

**▸ Almacenamiento de datos:** se utilizan para cifrar datos almacenados en dispositivos de almacenamiento como discos duros, unidades USB y sistemas de archivos, lo cual protege la información confidencial en caso de pérdida o robo del dispositivo.

**▸ Autenticación y firma digital:** los algoritmos simétricos también pueden utilizarse en sistemas de autenticación y firma digital, en los cuales se generan y verifican códigos de autenticación o firmas para garantizar la identidad y la integridad de los datos transmitidos.

**▸ Protección de contraseñas:** los algoritmos simétricos se utilizan en aplicaciones y sistemas que requieren almacenar contraseñas de forma segura, como bases de datos de contraseñas y sistemas de autenticación de usuarios.

**▸ Encriptación de archivos:** se utilizan para cifrar archivos individuales o conjuntos de archivos, lo que proporciona una capa adicional de seguridad para los datos sensibles almacenados en dispositivos de almacenamiento o transmitidos a través de redes.

**▸ Seguridad en dispositivos móviles:** los algoritmos simétricos se utilizan en los dispositivos móviles para cifrar datos almacenados en el dispositivo, como contactos, mensajes y archivos multimedia, lo cual protege la privacidad del usuario en caso de pérdida o robo del dispositivo.

Estos son solo algunos ejemplos de los numerosos usos de los algoritmos simétricos en la protección de la información en diversas aplicaciones y entornos.

Algoritmos de cifrado asimétrico

En los algoritmos de cifrado asimétrico **cada usuario** del sistema criptográfico **debe** **poseer un par de claves:**

**▸ Clave privada:** esta clave debe ser resguardada por su propietario y no debe ser revelada a ninguna otra persona.

**▸ Clave pública:** esta clave puede ser conocida por todos los usuarios del sistema.

Estas dos claves están **relacionadas de manera complementaria:** lo que se cifra con una de ellas solo puede ser descifrado con la otra y viceversa. Las claves se generan mediante algoritmos y funciones matemáticas complejas, de modo que es imposible calcular una clave a partir de la otra debido al tiempo computacional necesario. Si una persona cifra un mensaje con la llave privada, ese mensaje solo podrá ser descifrado con la llave pública asociada. Y si se cifra con la pública, se podrá descifrar con la privada.

Los sistemas de cifrado de clave pública utilizan **funciones de** ***hash*** **unidireccionales** que aprovechan propiedades específicas, como las de los números primos. Una función unidireccional es aquella que se puede calcular fácilmente en una dirección, pero revertir este proceso es extremadamente difícil.

Las claves públicas y privadas se generan simultáneamente y están ligadas la una a la otra. Esta relación debe ser muy compleja para que resulte muy difícil que obtengamos una a partir de la otra.

![Figura 6. Encriptación asimétrica. Fuente: Prado, 2022b.](images/image-8.png)

*Figura 6. Encriptación asimétrica. Fuente: Prado, 2022b.*

#### Proceso de cifrado

El proceso de cifrado asimétrico implica **varios pasos clave:**

**▸ Generación de claves:** cada entidad (como un usuario o un servidor) genera un par de claves, una pública y una privada. Estas claves están matemáticamente relacionadas entre sí.

**▸ Distribución de claves públicas:** las claves públicas se distribuyen libremente entre los usuarios. Por ejemplo, si Alice quiere enviarle un mensaje a Bob de forma segura, utiliza la clave pública de Bob para cifrar el mensaje.

**▸ Cifrado:** cuando Alice quiere enviarle un mensaje a Bob, primero cifra el mensaje utilizando la clave pública de Bob. Solo la clave privada correspondiente de Bob puede descifrar este mensaje cifrado.

**▸ Descifrado:** Bob recibe el mensaje cifrado y utiliza su clave privada (que mantiene en secreto) para descifrarlo y recuperar el mensaje original.

#### Ventajas y desventajas

La **ventaja** del cifrado asimétrico es que la clave pública puede ser conocida por todo el mundo (no así la privada), sin embargo en el cifrado simétrico se trabaja con la misma clave para todos los usuarios (y esa clave debe hacerse llegar a cada uno de los distintos usuarios por un canal seguro).

Las **desventajas** en comparación con el cifrado simétrico serían:

**▸** Para una misma longitud de clave y mensaje se necesita mayor tiempo de proceso.

**▸** Las claves deben ser de mayor tamaño que las simétricas.

**▸** El mensaje cifrado ocupa más espacio que el original.

#### Algoritmos asimétricos existentes

En el ámbito de la seguridad informática y las comunicaciones seguras se utilizan diversas herramientas y protocolos que combinan técnicas de cifrado asimétrico y simétrico para asegurar la confidencialidad, la integridad y la autenticación de la información. Aquí tienes una explicación más detallada:

**▸ Técnicas de clave asimétrica:**

- Diffie-Hellman (DH): permite que dos partes establezcan una clave compartida de manera segura sobre un canal no seguro.

- RSA: es utilizado para el cifrado de datos y la generación de firmas digitales. Es eficaz para el intercambio seguro de claves simétricas.

- Digital signature algorithm(DSA): específicamente diseñado para generar y verificar firmas digitales.

- ElGamal: proporciona tanto cifrado como firma digital basados en la teoría de números.

- Criptografía de curva elíptica: utiliza operaciones matemáticas en curvas elípticas para proporcionar niveles de seguridad similares a los algoritmos tradicionales con claves más cortas.

**▸ Protocolos y software que utilizan estos algoritmos:**

- Digital signature standard (DSS) con DSA: estándar para la generación y verificación de firmas digitales en documentos y comunicaciones.

- Pretty good privacy (PGP) y GNU privacy guard (GPG): utilizan tanto el cifrado simétrico como el asimétrico para asegurar la confidencialidad de los mensajes y la autenticación de las partes. GPG es una implementación de OpenPGP.

- Secure shell (SSH): proporciona una conexión segura a través de redes inseguras utilizando tanto el cifrado asimétrico (para el intercambio inicial de claves) como el simétrico (para la sesión de comunicación).

- Secure sockets layer (SSL) y transport layer security (TLS): proporcionan seguridad en la comunicación a través de Internet, al utilizar criptografía asimétrica para establecer las claves de sesión y criptografía simétrica para la transferencia de datos.

Estos protocolos y herramientas son fundamentales en entornos en los que la seguridad de la información es crucial, como en transacciones bancarias en línea, comunicaciones corporativas seguras y protección de la privacidad en general. Utilizan una combinación inteligente de técnicas criptográficas asimétricas y simétricas para garantizar la protección completa de los datos durante su transmisión y almacenamiento.

#### Información complementaria sobre algoritmos de clave asimétrica

**▸ Diffie-Hellman:** es un protocolo que está enfocado en la creación de claves secretas compartidas entre dos partes que se comunican a través de un canal inseguro. Su principal aplicación es en la generación de claves que luego se usarán con algoritmos de cifrado simétrico. La fortaleza de Diffie-Hellman reside en la complejidad del cálculo de logaritmos discretos en campos numéricos grandes. Sin embargo, tiene la debilidad de no ofrecer autenticación, es decir, no valida la identidad de los participantes. Si un atacante interviene la comunicación (ataque de intermediario), podría obtener acceso a las claves.

**▸ RSA:** este es uno de los algoritmos asimétricos más populares. Funciona con un par de claves, una pública y una privada. La seguridad de RSA se basa en la dificultad de factorizar grandes números primos.

- Ventajas: soluciona problemas asociados con la distribución de claves en el cifrado simétrico. Además, puede utilizarse para firmas digitales, lo cual garantiza la autenticidad e integridad de los mensajes.

- Desventajas: su seguridad puede verse comprometida a medida que aumenta la capacidad de cálculo de los ordenadores. Por otro lado, RSA es más lento en comparación con los algoritmos simétricos, además de que es necesario proteger la clave privada, usualmente cifrándola con un algoritmo simétrico.

#### RSA. Algoritmo seguro

Para que un algoritmo sea considerado seguro debe cumplir:

**▸ Confidencialidad del texto cifrado y la clave privada:** debe ser extremadamente difícil o prácticamente imposible obtener tanto el texto en claro como la clave privada a partir del texto cifrado. Esto se basa en la premisa de que la seguridad del sistema no debe depender de mantener el texto cifrado en secreto, sino únicamente de mantener segura la clave privada.

**▸ Dificultad en la obtención de la clave privada:** si se conoce el texto en claro y su correspondiente texto cifrado, el proceso para obtener la clave privada (o descifrar otros textos cifrados) debe ser considerablemente más costoso y difícil que simplemente descifrar el texto en claro mediante métodos criptoanalíticos.

**▸ Unicidad de las claves y relación entre clave pública y privada:** para el cifrado asimétrico, cada entidad (usuario, servidor) debe tener un par único de claves, una pública y una privada. Solo la clave privada correspondiente puede descifrar los mensajes cifrados con la clave pública asociada, y viceversa. Esto asegura que la comunicación segura entre dos partes se pueda lograr sin necesidad de compartir secretamente una clave simétrica.

Estos criterios garantizan que un algoritmo de cifrado asimétrico como RSA, por ejemplo, sea seguro y adecuado para su uso en aplicaciones en las que la seguridad y la privacidad son críticas, como en transacciones financieras, comunicaciones gubernamentales y la protección de datos personales en Internet.

Comparativa entre el cifrado simétrico y el asimétrico

Aquí tienes una tabla comparativa con las ventajas y desventajas tanto del cifrado asimétrico y como del simétrico:

![image-9](images/image-9.png)

![image-10](images/image-10.png)

Tabla 1. Comparativa entre el cifrado simétrico y el asimétrico. Fuente: elaboración propia.

Esta tabla proporciona una visión clara de las ventajas y desventajas de ambos tipos

Seguridad y Alta Disponibilidad 27 Tema . Material de estudio de cifrado, por lo cual ayuda a entender en qué situaciones podría ser más adecuado utilizar uno sobre el otro.

## 5.4. Funciones hash y firma digital

Concepto de *hash*

L o s *hash* o funciones de resumen son algoritmos diseñados para **convertir una** **entrada** (como un texto, una contraseña o un archivo) en una **salida alfanumérica** **de longitud fija.** Esta salida, conocida como *hash,* representa un resumen único y determinístico de los datos de entrada. La característica fundamental de los *hashes* es que, dado un conjunto de datos de entrada, siempre se generará el mismo *hash.*

A diferencia de la criptografía simétrica y asimétrica, cuyo propósito principal es asegurar la confidencialidad de la información y la autenticación entre partes, los *hashes* tienen **varios cometidos esenciales:**

**▸ Integridad de los datos:** permiten verificar si los datos han sido modificados durante su transmisión o almacenamiento. Al comparar el *hash* del archivo original con el *hash* calculado del archivo recibido, se puede detectar cualquier alteración, por mínima que sea.

**▸ Seguridad de las contraseñas:** en lugar de almacenar las contraseñas de manera directa, los sistemas de autenticación almacenan el *hash* de la contraseña. Cuando un usuario intenta iniciar sesión, se calcula el *hash* de la contraseña ingresada y se compara con el *hash* almacenado en la base de datos. Esto evita que las contraseñas sean expuestas en caso de una violación de seguridad.

**▸ Firma digital:** los *hashes* se utilizan en la firma digital para garantizar la integridad de los documentos o mensajes. El *hash* del documento se firma digitalmente, lo que les permite a las partes verificar que el documento no ha sido alterado desde que se firmó.

**▸ Indexación rápida:** en bases de datos y sistemas de almacenamiento, los *hashes* se utilizan para indexar y buscar datos de manera eficiente. Los *hashes* de las claves de búsqueda permiten el acceso rápido y eficiente a los registros correspondientes.

En resumen, los *hashes* son herramientas fundamentales para garantizar la integridad de los datos, proteger contraseñas, firmar digitalmente documentos y facilitar búsquedas eficientes en grandes conjuntos de datos. Su uso se extiende ampliamente en sistemas de seguridad informática y gestión de datos.

![Figura 7. Función hash aplicada sobre un texto. Fuente: Stolfi, 2008.](images/image-11.png)

*Figura 7. Función hash aplicada sobre un texto. Fuente: Stolfi, 2008.*

Características del hash

Las características que deben tener los algoritmos de *hash* para ser considerados criptográficamente seguros son las siguientes:

**▸ Función irreversible de una sola dirección:** esto significa que no se debe poder obtener el mensaje original solo a partir de su resumen *(hash).* La función de *hash* debe ser una función de una sola dirección, según la cual es fácil calcular el *hash* a partir del mensaje, pero extremadamente difícil o imposible calcular el mensaje a partir del *hash.*

**▸ Dificultad en la búsqueda inversa:** dado un resumen *(hash),* debe ser computacionalmente inviable encontrar un mensaje que genere ese mismo *hash.*

Esto implica que la función de *hash* debe distribuir los posibles *hashes* de manera uniforme e impredecible a lo largo de todos los posibles mensajes.

**▸ Imposibilidad de colisiones computacionales:** debe ser computacionalmente imposible encontrar dos mensajes diferentes que generen el mismo resumen (colisión de *hash).* Esto asegura que cada mensaje tenga un *hash* único y que no existan dos mensajes diferentes con el mismo resumen.

Estas propiedades aseguran que los algoritmos de *hash* sean adecuados para su uso en aplicaciones criptográficas, como la integridad de datos, la autenticación y la verificación de contraseñas, entre otras.

Firma digital

Una de las principales ventajas de la criptografía de clave pública es que posibilita la creación de firmas digitales.

Las firmas digitales le permiten al receptor de un mensaje confirmar la autenticidad del origen de la información y asegurar que esta no ha sido alterada desde su emisión. De esta manera, las firmas digitales

garantizan la autenticación y la

Seguridad y Alta Disponibilidad 31 Tema . Material de estudio integridad de los datos, así como el no repudio del origen, ya que quien envía un mensaje firmado digitalmente no puede negar que lo hizo. Una firma digital tiene el mismo propósito que una firma manuscrita. Sin embargo, mientras que una firma manuscrita puede ser falsificada con relativa facilidad, una firma digital es inviolable siempre que la clave privada del firmante permanezca segura.

Imaginemos que Juan quiere mandarle un mensaje a Pepe y se quiere comprobar que el mensaje ha llegado correctamente, sin que haya sido modificado.

Antes de enviar el mensaje Juan necesita generar la firma digital. Para esto él crea un resumen del mensaje utilizando la función *hash.* Este resumen lo cifra utilizando su clave privada. La firma digital estará compuesta de la clave pública de Juan junto con el *hash* generado y cifrado. El mensaje luego se envía junto con la firma digital.

![Figura 8. Firma digital. Fuente: TIC Escuelas Pías Carabanchel, 2017ª.](images/image-12.png)

*Figura 8. Firma digital. Fuente: TIC Escuelas Pías Carabanchel, 2017ª.*

Pepe, al recibir el mensaje, separa por un lado el mensaje recibido y por otro la firma digital (que contiene la clave pública de Juan y el resumen del mensaje cifrado). A continuación, a partir del mensaje recibido, crea su

Seguridad y Alta Disponibilidad 32 Tema . Material de estudio resumen (utilizando la función *hash)* y descifra el resumen que recibió dentro de la firma. En este punto, Pepe compara ambos resúmenes y, si coinciden, significa que el mensaje que le ha llegado es originario de Juan.

![Figura 9. Firma digital. Fuente: TIC Escuelas Pías Carabanchel, 2017b.](images/image-13.png)

*Figura 9. Firma digital. Fuente: TIC Escuelas Pías Carabanchel, 2017b.*

La firma digital es el resultado de cifrar con clave privada el resumen de los datos por firmar, haciendo uso de funciones resumen o *hash.*

Con este sistema logramos:

**▸ Autenticación:** la firma digital actúa de manera equivalente a una firma física en un documento, al verificar la identidad del remitente.

**▸ Integridad:** garantiza que el mensaje no pueda ser alterado tras su creación y firma. **▸ No repudio en origen:** el emisor no puede negar haber enviado el mensaje, lo que asegura su responsabilidad.

Se suele emplear la firma digital principalmente para trámites legales con la utilización de unas claves generadas por alguna entidad el Gobierno, como puede ser Ceres (Real Casa de la Moneda, [s. f.]). La firma digital tiene el mismo valor que el DNI para identificar a una persona.

## 5.5. Referencias bibliográficas

Ayuntamiento de Valladolid. (2016). *La máquina Enigma que exhibe la Academia de* *C a b a l l e r í a* [ i m a g e n ] . <https://www.info.valladolid.es/blog/maquina-enigma-devalladolid/>

Doncherry. (2013). *How to create a Caesar's encryption disk using LaTeX* [gráfico]. <https://tex.stackexchange.com/questions/103364/how-to-create-a-caesarsencryption-disk-using-latex>

Luringen. (2007). *Skytale* [imagen]. [https://es.wikipedia.org/wiki/Esc%C3%ADtala](https://es.wikipedia.org/wiki/Esc%25C3%25ADtala)

Orientación Andújar. (2012). *Abecedario de jeroglíficos Egipto* [gráfico]. <https://www.orientacionandujar.es/2012/11/14/atencion-en-primaria-e-infantil-lostraductores-de-papiros-nivel-inicial-i/abecedario-de-jeroglificos-egipto/>

Prado, S. (2022a). *Symmetric*

*Encryption* [gráfico].

<https://sergioprado.blog/introduction-to-encryption-for-embedded-linux-developers/?>

$$ref=0xor0ne.xyz$$

Prado, S. (2022b). *Asymmetric*

*Encryption* [gráfico].

<https://sergioprado.blog/introduction-to-encryption-for-embedded-linux-developers/?>

$$ref=0xor0ne.xyz$$

Real Casa de la Moneda, Fábrica Nacional de Moneda y Timbre. (s. f.). *Ceres* [consultado el 8 de agosto de 2024]. [https://www.cert.fnmt.es/](https://www.cert.fnmt.es/)

Stolfi, J. (2008). *Cryptographic Hash Function* [gráfico]. [https://en.wikipedia.org/wiki/Cryptographic_hash_function](https://en.wikipedia.org/wiki/Cryptographic_hash_function)

TIC Escuelas Pías Carabanchel. (2017a). *La firma digital* [gráfico]. <https://ticescolapiaslaclave.blogspot.com/2017/10/el-certificado-digital-como-se-usala.html>

TIC Escuelas Pías Carabanchel. (2017b). *Firma digital* [gráfico]. <https://ticescolapiaslaclave.blogspot.com/2017/10/el-certificado-digital-como-se-usala.html>

## ¿Qué es la criptografía?

Androide Sabiondo. (2020, junio 1). *¿Qué es la criptografía? Simétrica, asimétrica,* *clave pública, HTTPS, RSA, SSL…* [vídeo]. YouTube.

![image-14](images/image-14.png)

Accede al vídeo: [https://www.youtube.com/embed/IFZS36m8Miw](https://www.youtube.com/embed/IFZS36m8Miw)

Avanza un poco más en criptografía. ¿Cómo se utiliza la criptografía en un entorno web? ¿Qué función cumple la criptografía simétrica en TLS/SSL? Todo eso y más en una explicación entretenida y fácil de entender.

# para-proteger-la-privacidad

## Distintos tipos de cifrado

Instituto Nacional de Ciberseguridad (INCIBE). (2019). *¿Sabías que existen distintos* *tipos de cifrado para proteger la privacidad de nuestra información en Internet?* <https://www.incibe.es/ciudadania/blog/sabias-que-existen-distintos-tipos-de-cifrado->

INCIBE te facilita una descripción detallada de los diferentes tipos de cifrado más habituales que nos podemos encontrar en el mercado. Por si no te quedó claro el tema, te aconsejo que accedas a este contenido.

## Encriptación asimétrica: clave pública y privada

## explicación

AlbertoLopez TECH TIPS. (2020, noviembre 26). *Encriptación asimétrica ►clave* *pública y privada | Software para cifrado asimétrico* [vídeo]. YouTube.

![image-15](images/image-15.png)

Accede al vídeo: [https://www.youtube.com/embed/apn1BN6XMVo](https://www.youtube.com/embed/apn1BN6XMVo)

¿Te han quedado dudas respecto a la encriptación asimétrica? ¿Ya sabes diferenciar la clave pública de la privada? ¿Quieres reafirmar tus conocimientos? Aquí tienes otro enfoque para que lo entiendas mejor…

# diferencias | Seguridad de la información [vídeo]. YouTube.

# [https://www.youtube.com/watch?v=5BYhdr5n3es](https://www.youtube.com/watch?v=5BYhdr5n3es)

## Cifrado simétrico y asimétrico: cinco diferencias

AlbertoLopez TECH TIPS. (2020, diciembre 2). *Cifrado simétrico y asimétrico ► 5* Cifrado simétrico o asimétrico, ¿cuál utilizo? ¿En qué situaciones es más ventajoso utilizar uno u otro? Descubre las cinco diferencias más importantes entre los dos métodos de cifrado más habituales.

## Public key cryptography: Diffie-Hellman key exchange

Art of the Problem. (2012, febrero 24). *Public key cryptography: Diffie-Hellman key* *exchange (short version)* [vídeo]. YouTube.

![image-16](images/image-16.png)

Accede al vídeo: [https://www.youtube.com/embed/3QnD2c4Xovk](https://www.youtube.com/embed/3QnD2c4Xovk)

Diffie-Hellman es un tipo diferente de algoritmo criptográfico de clave pública diseñado específicamente para ayudar a las partes a acordar una clave simétrica en ausencia de un canal seguro.

## Certificación digital

Real Casa de la Moneda, Fábrica Nacional de Moneda y Timbre. (s. f.). *Certificación* *digital* [consultado el 8 de agosto de 2024]. [https://www.fnmt.es/ceres](https://www.fnmt.es/ceres)

¿Tienes certificado electrónico? ¿Sabes la cantidad de usos que tiene? Aquí tienes la web de la Fábrica Nacional de Moneda y Timbre, una autoridad de certificación y expedición de certificados digitales.

# 2024]. [https://www.dnielectronico.es/PortalDNIe/](https://www.dnielectronico.es/PortalDNIe/)

## DNI electrónico

Cuerpo Nacional de Policía. (s. f.). *DNI electrónico* [consultado el 8 de agosto de ¿Sabes cómo funciona tu DNI electrónico? Y si no lo tienes, ¿cómo conseguir el tuyo? Este es un sitio oficial en el que podrás resolver todas tus dudas en cuanto al funcionamiento y las aplicaciones del DNI electrónico.

## ¿Qué es el hash? ¿Cómo se genera el hash?

AlbertoLopez TECH TIPS. (2020, noviembre 22). *[Hash] ¿Qué es el hash? ¿Cómo se* *genera el hash? ► Los 6 usos más destacados del hash* [vídeo]. YouTube.

![image-17](images/image-17.png)

Accede al vídeo: [https://www.youtube.com/embed/lP_pbygY3PA](https://www.youtube.com/embed/lP_pbygY3PA)

Ya sabes lo que es un *hash,* pero ¿sabes cómo se genera un *hash?,* y lo más importante, ¿en qué situaciones se hace uso de las funciones *hash?* Completa tu formación visualizando este vídeo.

# Cifrado [consultado el 8 de agosto de 2024].

# <https://www.incibe.es/ciudadania/filtro/herramientas?>

# tid=303602&tid_1=All&tid_2=All&tid_3=All

## Cifrado. Software

Instituto Nacional de Ciberseguridad (INCIBE). (s. f.). *Herramientas de seguridad.* Seguro que almacenas información que no quieres que vea nadie excepto aquellas personas que tu autorizas. Para evitar que alguien acceda a ella sin tu permiso y pueda ver su contenido, cífrala con una contraseña.

Cifrado de extremo a extremo ¿qué significa y cómo funciona?

AlbertoLopez TECH TIPS. (2020, diciembre 6). *Cifrado de extremo a extremo ¿qué* *significa y cómo funciona? ► Ejemplo con el cifrado de WhatsApp* [vídeo]. YouTube.

![image-18](images/image-18.png)

Accede al vídeo: [https://www.youtube.com/embed/eeG9HV6gApU](https://www.youtube.com/embed/eeG9HV6gApU)

¿Te has preguntado alguna vez qué tan segura está la información que transmites a través de WhatsApp? ¿Sabes lo que es el cifrado extremo a extremo? Visualiza este vídeo que te resolverá tus dudas.

## Entrenamiento 1: cifrado simétrico

**▸ Planteamiento del ejercicio** Se desea cifrar ficheros con algoritmos simétricos mediante la herramienta IZArc. Para ello suponte que quieres mandar un documento a un compañero y lo quieres cifrar para que únicamente él pueda verlo. Al utilizar un cifrado simétrico, deberás proporcionarle, además del documento, la clave con la que se ha cifrado.

**▸ Desarrollo paso a paso**

1.Descargar e instalar IZArc.

2.Crear un archivo de texto y cifrarlo.

3.Transportar el archivo al segundo equipo.

4.Recuperar el archivo en el segundo equipo.

**▸ Solución** Deberemos tener instaladas dos máquinas Windows10 en Virtualbox.

## 1. Descarga e instalación de IZArc:

**▸** En el primer ordenador con Windows 10, abre tu navegador y ve a la web oficial de IZArc: ([http://www.izarc.org](http://www.izarc.org/)).

**▸** Descarga la versión más reciente del *software.*

**▸** Una vez descargado, ejecuta el instalador y sigue las instrucciones en pantalla para completar la instalación.

## 2. Crear un archivo de texto y cifrarlo:

**▸** Abre un editor de texto (por ejemplo, el Bloc de notas). **▸** Escribe algo en el archivo y guárdalo con el nombre «criptografía simétrica.txt». **▸** Abre IZArc. **▸** Añade el archivo «criptografía simétrica.txt» a un nuevo archivo comprimido. Puedes hacer esto seleccionando «Add» o arrastrando el archivo a la interfaz de IZArc. **▸** En la ventana de «Add» selecciona «Encrypt» y elige el algoritmo de encriptación AES de 128 bits. **▸** Introduce una contraseña segura y confirma. **▸** Guarda el archivo cifrado (por ejemplo, «criptografía_simétrica.zip»).

## 3. Transportar el archivo al segundo equipo:

**▸** Usa un medio de transporte (por ejemplo, una memoria USB, un correo electrónico, o una red compartida) para mover el archivo cifrado «criptografía_simétrica.zip» al segundo ordenador con Windows 10.

## 4. Recuperar el archivo en el segundo equipo:

**▸** Asegúrate de que IZArc está instalado en el segundo ordenador.

**▸** Abre IZArc y navega hasta el archivo «criptografía_simétrica.zip».

**▸** Selecciona el archivo y haz clic en «Extract».

**▸** Se te pedirá que ingreses la contraseña. Introduce la misma contraseña que usaste

para cifrar el archivo. **▸** Una vez ingresada la contraseña correcta, el archivo «criptografía simétrica.txt» se extraerá y estará disponible para su lectura.

## 5. Función de cada opción del menú de IZArc:

**▸** ***Extract to…:*** esta opción te permite extraer los archivos comprimidos en una ubicación específica. Puedes seleccionar la carpeta de destino donde deseas que se extraigan los archivos.

**▸** ***Test:*** esta opción verifica la integridad del archivo comprimido. IZArc revisa si el archivo está corrupto o si los archivos comprimidos dentro de este están completos y sin errores.

**▸** ***Convert archive:*** permite convertir el archivo comprimido a otro formato de archivo de compresión compatible con IZArc. Por ejemplo, puedes convertir un archivo ZIP a formato 7z, TAR, etc.

**▸** ***Create self-extracting*** **[.EXE]** ***file:*** esta opción crea un archivo autoextraíble (.exe) a partir del archivo comprimido. Este archivo puede ejecutarse en cualquier ordenador con Windows, incluso si no tiene IZArc instalado, ya que el archivo contiene un pequeño ejecutable que puede descomprimir el contenido.

Al seguir estos pasos, podrás cifrar y descifrar archivos usando IZArc en dos ordenadores con Windows 10 y entender las funciones del menú contextual que ofrece la herramienta.

## Entrenamiento 2: cifrado de ficheros con

## algoritmos asimétricos usando GPG en Ubuntu

**▸ Planteamiento del ejercicio** Aprenderás a cifrar y descifrar ficheros utilizando algoritmos de cifrado asimétrico mediante la herramienta GPG en un entorno Ubuntu, para asegurar la integridad y la autenticidad de las claves públicas y privadas. Mediante el uso de una máquina con SO Ubuntu 20.04 o posterior, el usuario profesor mandará un fichero cifrado con un algoritmo asimétrico (GPG) al alumno1, que también se registrará en ese mismo ordenador.

**▸ Desarrollo paso a paso** Requisitos:

**▸** Un ordenador con Ubuntu instalado.

**▸** Acceso a la terminal.

**▸** Conocimiento básico de comandos Linux.

**Paso 1:** crear la cuenta «profesor» e iniciar sesión con ella.

**Paso 2:** instalación de GPG.

**Paso 3:** generación del par de claves.

**Paso 4:** lista de claves en el llavero.

**Paso 5:** verificar el directorio en el que se almacenan las claves.

**Paso 6:** compartir la clave pública.

**Paso 7:** creación del usuario «alumno1» y envío de un mensaje cifrado con la clave pública de «profesor» al profesor. **Paso 7:** con el usuario «profesor» descifrar el archivo cifrado. **Paso 8:** manipulación del archivo cifrado para comprobar que no se puede descifrar si ha sido manipulado.

**▸ Solución**

**Paso 1:** creamos el usuario «profesor».

## 1. Utilizamos el comando adduser.

![Figura 10. Comando adduser. Fuente: elaboración propia.](images/image-19.png)

*Figura 10. Comando adduser. Fuente: elaboración propia.*

Si deseas que el usuario «profesor» tenga privilegios administrativos en el sistema

(para poder ejecutar comandos como superusuario), puedes agregarlo al grupo sudo

.

![Figura 11. Grupo sudo. Fuente: elaboración propia.](images/image-20.png)

*Figura 11. Grupo sudo. Fuente: elaboración propia.*

Iniciamos sesión con «profesor».

![Figura 12. Iniciar sesión con «profesor». Fuente: elaboración propia.](images/image-21.png)

*Figura 12. Iniciar sesión con «profesor». Fuente: elaboración propia.*

**Paso 2:** instalación de GPG.

1. Abrimos una terminal y actualizamos la lista de paquetes:

![Figura 13. Actualizar la lista de paquetes. Fuente: elaboración propia.](images/image-22.png)

*Figura 13. Actualizar la lista de paquetes. Fuente: elaboración propia.*

## 2. Instalamos la herramienta GPG:

![Figura 14. Instalar la herramienta GPG. Fuente: elaboración propia.](images/image-23.png)

*Figura 14. Instalar la herramienta GPG. Fuente: elaboración propia.*

**Paso 3:** generación del par de claves.

## 1. Generamos un par de claves (pública y privada):

![Figura 15. Generar un par de claves. Fuente: elaboración propia.](images/image-24.png)

*Figura 15. Generar un par de claves. Fuente: elaboración propia.*

Siga las instrucciones en pantalla para configurar su clave. Especifique el tipo de

clave (por ejemplo, RSA), su tamaño y su duración.

**Paso 4:** lista de claves en el llavero.

## 1. Listamos las claves del llavero:

![Figura 16. Lista de claves en el llavero. Fuente: elaboración propia.](images/image-25.png)

*Figura 16. Lista de claves en el llavero. Fuente: elaboración propia.*

![Figura 17. Resultado. Fuente: elaboración propia. Este podría ser el resultado obtenido:](images/image-26.png)

*Figura 17. Resultado. Fuente: elaboración propia.*

En el cual la primera línea muestra la ruta del archivo «pubring.kbx» donde se almacenan las claves públicas. En este caso, «/home/usuario/.gnupg/pubring.kbx».

**▸** pub : indica que es una clave pública.

**▸** rsa4096 : tipo y tamaño de la clave (RSA de 4096 bits).

**▸** 2024-06-13 : fecha de creación de la clave.

**▸** [SC] : la clave puede ser utilizada para firmar (S) y certificar (C).

**▸** [expires: 2026-06-12] : fecha de expiración de la clave.

**▸** ID de la clave: un identificador único para la clave (por ejemplo,

«9C4D639A3B5F96A3D6A8D1B9A8D1B0A1A1B1A1B2»).

**▸** uid : muestra la identidad asociada con la clave (nombre y correo electrónico).

**▸** sub : indica que es una subclave.

**▸** rsa4096 : tipo y tamaño de la subclave (RSA de 4096 bits).

**▸** 2024-06-13 : fecha de creación de la subclave.

**▸** [E] : la subclave puede ser utilizada para cifrar (E).

**▸** [expires: 2026-06-12] : fecha de expiración de la subclave.

**Paso 5:** directorio .gnupg.

1. Verificamos el directorio en el que se almacenan las claves:

![Figura 18. Directorio en el que se almacenan las claves. Fuente: elaboración propia.](images/image-27.png)

*Figura 18. Directorio en el que se almacenan las claves. Fuente: elaboración propia.*

En este directorio encontrará los archivos «pubring.gpg» (con las claves públicas) y «secring.gpg» (con las claves privadas).

**Paso 6:** compartir la clave pública.

1. Primero necesitas saber la lista de claves para saber el ID de la clave pública que

deseas exportar:

![Figura 19. Lista de claves. Fuente: elaboración propia.](images/image-28.png)

*Figura 19. Lista de claves. Fuente: elaboración propia.*

![Figura 20. Resultado. Fuente: elaboración propia. Y obtenemos:](images/image-29.png)

*Figura 20. Resultado. Fuente: elaboración propia.*

Ahora exportamos la clave pública del profesor:

![Figura 21. Exportar la clave pública del profesor. Fuente: elaboración propia.](images/image-30.png)

*Figura 21. Exportar la clave pública del profesor. Fuente: elaboración propia.*

2. Enviamos el archivo «mi_clave_publica.asc» a quien esté interesado en

mandarnos un mensaje cifrado (en este caso en «nombre de usuario» pondremos alumno1, un usuario que crearemos en el siguiente paso).

**Paso 6:** creación de un nuevo usuario y envío de mensaje cifrado.

![Figura 22. Crear un nuevo usuario. Fuente: elaboración propia. 1. Creamos un nuevo usuario:](images/image-31.png)

*Figura 22. Crear un nuevo usuario. Fuente: elaboración propia.*

Utilizamos «alumno1» en el lugar de "tu_nombre", tanto para el *user* como para la *paswd.*

2. Copiamos el archivo asc con la clave pública al directorio de alumno1:

![Figura 23. Copiar el archivo asc con la clave pública al directorio de alumno1. Fuente: elaboración propia.](images/image-32.png)

*Figura 23. Copiar el archivo asc con la clave pública al directorio de alumno1. Fuente: elaboración propia.*

3. Iniciamos sesión como el nuevo usuario y creamos un mensaje cifrado:

![Figura 24. Iniciamos sesión como el nuevo usuario y creamos un mensaje cifrado. Fuente: elaboración](images/image-33.png)

*Figura 24. Iniciamos sesión como el nuevo usuario y creamos un mensaje cifrado. Fuente: elaboración*

propia.

Importamos la clave pública:

![Figura 25. Importar la clave pública. Fuente: elaboración propia.](images/image-34.png)

*Figura 25. Importar la clave pública. Fuente: elaboración propia.*

Como comprobación, se puede verificar si se ha importado correctamente la clave pública con el comando:

![Figura 26. Comando. Fuente: elaboración propia.](images/image-35.png)

*Figura 26. Comando. Fuente: elaboración propia.*

![Figura 27. Resultado. Fuente: elaboración propia. Y tendríamos algo así:](images/image-36.png)

*Figura 27. Resultado. Fuente: elaboración propia.*

Creamos un archivo de texto con el mensaje que se quiere cifrar. Por ejemplo:

![Figura 28. Crear el archivo del mensaje para cifrar. Fuente: elaboración propia.](images/image-37.png)

*Figura 28. Crear el archivo del mensaje para cifrar. Fuente: elaboración propia.*

Usa la clave pública de «profesor» para cifrar el archivo «mensaje.txt»:

![Figura 29. Cifrar el archivo con la clave pública del profesor. Fuente: elaboración propia.](images/image-38.png)

*Figura 29. Cifrar el archivo con la clave pública del profesor. Fuente: elaboración propia.*

Esto generará un archivo cifrado llamado mensaje.txt.gpg .

**Paso 7:** descifrar el archivo cifrado.

1. Deberemos compartir el archivo cifrado con «profesor». Puedes mover el archivo

cifrado al directorio de «profesor» o usar cualquier otro método para compartir archivos. Aquí hay un ejemplo de cómo mover el archivo al directorio de «profesor»:

![Figura 30. Mover el archivo al directorio del profesor. Fuente: elaboración propia.](images/image-39.png)

*Figura 30. Mover el archivo al directorio del profesor. Fuente: elaboración propia.*

## 2. Debemos registrarnos como «profesor».

![Figura 31. Registrarse como «profesor». Fuente: elaboración propia.](images/image-40.png)

*Figura 31. Registrarse como «profesor». Fuente: elaboración propia.*

Usa el siguiente comando para descifrar el archivo.

![Figura 32. Resultado. Fuente: elaboración propia.](images/image-41.png)

*Figura 32. Resultado. Fuente: elaboración propia.*

Esto generará un archivo llamado mensaje.txt donde se guardará el mensaje original que «alumno1» escribió. Deberías ver el mensaje original que «alumno1» escribió, por ejemplo:

![image-42](images/image-42.png)

![Figura 33. Ejemplo. Fuente: elaboración propia.](images/image-43.png)

*Figura 33. Ejemplo. Fuente: elaboración propia.*

**Paso 8:** manipulación del archivo cifrado.

## 1. Si metemos algún contenido extra en el fichero cifrado:

![Figura 34. Manipulación del archivo cifrado. Fuente: elaboración propia.](images/image-44.png)

*Figura 34. Manipulación del archivo cifrado. Fuente: elaboración propia.*

## 2. Intentamos descifrar el archivo modificado:

![Figura 35. Descifrar el archivo modificado. Fuente: elaboración propia.](images/image-45.png)

*Figura 35. Descifrar el archivo modificado. Fuente: elaboración propia.*

- Seguridad y Alta Disponibilidad 59

    - Tema . Entrenamientos

La salida será algo similar a lo siguiente:

![Figura 36. Salida. Fuente: elaboración propia.](images/image-46.png)

*Figura 36. Salida. Fuente: elaboración propia.*

Observamos que el descifrado fallará, lo cual indica que el archivo ha sido alterado.

## Entrenamiento 3: firma de ficheros

**▸ Planteamiento del ejercicio** Se desea firmar ficheros con algoritmos asimétricos mediante la herramienta GPG. Para ello, desde una cuenta principal en Ubuntu, firma documentos con tu clave privada y, al recibirlos, un usuario llamado «alumno» deberá comprobar que han sido firmados por el remitente. Se deberá probar con todas las opciones posibles que tenemos para firmar.

**▸ Desarrollo paso a paso**

Para ello necesitamos un ordenador Ubuntu.

**Parte 1.** Instala la aplicación GPG en Ubuntu.

**Parte 2.** Genera un par de claves: la clave pública y la privada.

**Parte 3.** Busca la lista de claves de la máquina (el llavero) e impórtala al usuario

alumno. **Parte 4.** Crea un archivo con el nombre «mensaje1» y fírmalo usando la clave privada y el parámetro «detachsign». **Parte 5.** Crea un archivo con el nombre «mensaje2» y fírmalo usando la clave privada y el parámetro «clearsign». **Parte 6.** Crea un archivo con el nombre «mensaje3» y fírmalo usando la clave privada y el parámetro «sign». **Parte 7.** Crea un archivo con el nombre «mensaje4», fírmalo y encríptalo usando la clave privada y el parámetro «sign».

**Parte 8.** ¿Qué pasa si borramos la clave púbica y la clave privada del usuario alumno?

**▸ Solución**

![Figura 37. Instalar la aplicación GPG. Fuente: elaboración propia. Parte 1. Instala la aplicación GPG en Ubuntu.](images/image-47.png)

*Figura 37. Instalar la aplicación GPG. Fuente: elaboración propia.*

**Parte 2.** Genera un par de claves: la clave pública y la clave privada.

![Figura 38. Generar un par de claves. Fuente: elaboración propia.](images/image-48.png)

*Figura 38. Generar un par de claves. Fuente: elaboración propia.*

**Parte 3.** Busca la lista de claves de la máquina (el llavero) y exporta la clave pública al usuario alumno.

![Figura 39. Lista de claves. Fuente: elaboración propia.](images/image-49.png)

*Figura 39. Lista de claves. Fuente: elaboración propia.*

![Figura 40. Resultado. Fuente: elaboración propia, Donde obtendremos:](images/image-50.png)

*Figura 40. Resultado. Fuente: elaboración propia,*

En este ejemplo, ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789ABCDEF es el ID de la

clave pública que hemos utilizado para firmar documentos.

Vamos a exportar la clave pública asociada para que el usuario «alumno» pueda importarla y verificar las firmas:

![Figura 41. Exportar la clave pública. Fuente: elaboración propia.](images/image-51.png)

*Figura 41. Exportar la clave pública. Fuente: elaboración propia.*

Donde ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789ABCDEF es el ID de la clave

pública que queremos exportar. Este comando exporta la clave en formato ASCII armado ( -a ).

Para transferir la clave pública desde la cuenta principal al usuario «alumno» a través de la carpeta temporal ( /tmp ), puedes seguir los siguientes pasos.

Primero, copia o mueve el archivo clave_publica.asc a la carpeta temporal ( /tmp ).

![Figura 42. Copiar o mover el archivo clave_publica.asc a la carpeta temporal. Fuente: elaboración propia.](images/image-52.png)

*Figura 42. Copiar o mover el archivo clave_publica.asc a la carpeta temporal. Fuente: elaboración propia.*

Desde la cuenta del usuario «alumno», accede a la carpeta temporal y copia la clave pública a una ubicación adecuada en la cuenta del usuario «alumno». Por ejemplo, puedes copiarla al directorio de inicio ( ~ ) del usuario «alumno»:

![Figura 43. Ejemplo. Fuente: elaboración propia.](images/image-53.png)

*Figura 43. Ejemplo. Fuente: elaboración propia.*

Esto copiará el archivo clave_publica.asc desde la carpeta temporal ( /tmp ) al directorio de inicio del usuario «alumno».

Ahora, importa la clave pública desde el directorio en el que la copiaste en la cuenta del usuario «alumno»:

![Figura 44. Importar la clave pública. Fuente: elaboración propia.](images/image-54.png)

*Figura 44. Importar la clave pública. Fuente: elaboración propia.*

Esto importará la clave pública al llavero GnuPG del usuario «alumno», lo que le permitirá verificar las firmas digitales de los documentos firmados por la cuenta principal.

**Parte 4.** Crea un archivo con nombre «mensaje1» y fírmalo usando la clave privada y el parámetro «detachsign».

Los pasos son los siguientes:

![Figura 45. Crear el archivo con el mensaje. Fuente: elaboración propia.](images/image-55.png)

*Figura 45. Crear el archivo con el mensaje. Fuente: elaboración propia.*

Esto creará un archivo llamado mensaje1 con el texto especificado.

![Figura 46. Firmar el mensaje usando la clave privada y el parámetro «detachsign». Fuente: elaboración](images/image-56.png)

*Figura 46. Firmar el mensaje usando la clave privada y el parámetro «detachsign». Fuente: elaboración*

propia.

--detach-sign : es una opción de GnuPG que indica que se desea realizar una firma digital separada *(detached signature).* Esto significa que la firma digital no se incorpora en el contenido del archivo original, sino que se almacena en un archivo separado.

Este comando creará un archivo llamado mensaje1.sig que contiene la firma digital del archivo mensaje1 .

Una vez que tengas los archivos mensaje1 y mensaje1.sig en la cuenta del usuario «alumno», puedes verificar la firma digital utilizando el siguiente comando:

![Figura 47. Comando. Fuente: elaboración propia.](images/image-57.png)

*Figura 47. Comando. Fuente: elaboración propia.*

Este comando realizará la verificación de la firma digital utilizando la clave pública correspondiente a la clave privada con la que se firmó el archivo mensaje1 . Si la verificación es exitosa, verás un mensaje que indica que la firma es válida y que el archivo mensaje1 no ha sido alterado desde que se creó la firma.

![Figura 48. Verificación exitosa. Fuente: elaboración propia.](images/image-58.png)

*Figura 48. Verificación exitosa. Fuente: elaboración propia.*

**Parte 5.** Crea un archivo con nombre «mensaje2» y fírmalo usando la clave privada y el parámetro «clearsign».

Los pasos son similares a los de la parte 4, pero cambia el atributo a la hora de firmar.

![Figura 49. Firmar el archivo con la clave privada y el parámetro «clearsign». Fuente: elaboración propia.](images/image-59.png)

*Figura 49. Firmar el archivo con la clave privada y el parámetro «clearsign». Fuente: elaboración propia.*

Este comando creará un archivo llamado mensaje2.asc que contiene el contenido original del archivo mensaje2 , seguido de la firma digital en texto claro.

Cuando usas --clearsign con GnuPG, lo que sucede es:

**▸** El contenido original del archivo ( mensaje2 en este caso) permanece intacto y sin modificaciones.

**▸** GnuPG añade una firma digital en texto claro al final del archivo, separada por una línea en blanco. Esta firma incluye la información necesaria para verificar la integridad del contenido original y asegurar que proviene de la entidad que posee la clave privada correspondiente a la clave pública utilizada para verificarla.

El propósito de utilizar --clearsign en lugar de --detach-sign es que el contenido original del archivo ( mensaje2 ) sea legible sin necesidad de GnuPG. Esto es útil en situaciones en las que quieres enviar un mensaje firmado y que el receptor pueda leer fácilmente el contenido sin necesidad de herramientas adicionales para descifrarlo.

En resumen, gpg --clearsign mensaje2 es una instrucción que crea una firma digital en texto claro del archivo mensaje2 , lo que asegura la integridad y autenticidad del contenido original utilizando la clave privada del usuario actual en GnuPG.

El alumno puede verificar la firma de la siguiente manera:

![Figura 50. Verificar la firma. Fuente: elaboración propia.](images/image-60.png)

*Figura 50. Verificar la firma. Fuente: elaboración propia.*

**Parte 6** y **Parte 7.** Crea un archivo con nombre mensaje4, fírmalo y encríptalo usando la clave privada y el parámetro «sign».

Procederemos igual que en las partes anteriores, cambiando el parámetro «sign».

![Figura 51. Firmar el mensaje con la clave privada y el parámetro «sign». Fuente: elaboración propia.](images/image-61.png)

*Figura 51. Firmar el mensaje con la clave privada y el parámetro «sign». Fuente: elaboración propia.*

Este comando creará un archivo firmado llamado mensaje3.gpg . GnuPG automáticamente utiliza la mejor práctica de firmar el archivo y también cifrarlo. El usuario alumno podrá comprobar la firma de la siguiente manera:

![Figura 52. Comprobar la firma. Fuente: elaboración propia.](images/image-62.png)

*Figura 52. Comprobar la firma. Fuente: elaboración propia.*

En cualquier caso, en la cuenta del alumno, GnuPG utilizará la clave pública importada para verificar la firma y mostrará un mensaje que indica si la firma es válida.

Consideraciones adicionales:

**▸** Seguridad: asegúrate de que la transferencia del archivo clave_publica.asc se realice de manera segura para evitar manipulaciones no deseadas.

**▸** Eliminación segura: después de importar la clave pública, considera eliminar el archivo clave_publica.asc de la carpeta temporal ( /tmp ) para mantener la seguridad y la limpieza del sistema.

Siguiendo estos pasos, puedes transferir de manera efectiva la clave pública desde la cuenta principal a través de la carpeta temporal y asegurarte de que esté disponible para el usuario «alumno» en su cuenta en Ubuntu.

**Parte 8.** ¿Qué pasa si borramos la clave púbica del usuario alumno?

Si borramos la clave pública del usuario «alumno» que se utilizó para verificar la firma digital en el archivo «mensaje3.gpg», GnuPG no podrá realizar la verificación correctamente. Aquí están las implicaciones de borrar la clave pública:

**▸** Imposibilidad de verificar firmas: sin la clave pública correspondiente en el llavero de GnuPG del usuario «alumno», cualquier intento de verificar la firma digital en «mensaje3.gpg» resultará en un mensaje de error que indica que la clave pública necesaria para la verificación no está disponible.

**▸** Error al verificar la firma: cuando intentas verificar la firma digital en un archivo firmado como «mensaje3.gpg», GnuPG consulta su llavero de claves públicas para encontrar la clave pública correspondiente a la clave privada que se utilizó para firmar el archivo. Si no encuentra esta clave pública, mostrará un mensaje de error similar al del siguiente ejemplo.

![Figura 53. Error al verificar la firma. Fuente: elaboración propia.](images/image-63.png)

*Figura 53. Error al verificar la firma. Fuente: elaboración propia.*

## Entrenamiento 4: encriptación simétrica en Ubuntu

**▸ Planteamiento del ejercicio**

En esta práctica se aplicarán conceptos y herramientas básicos relacionados con la criptografía simétrica. Se utilizará la herramienta OpenSSL para generar claves y cifrar los archivos. Los objetivos por alcanzar son:

**▸** Instalar *software* de encriptación simétrica en Ubuntu.

**▸** Realizar la encriptación simétrica de un archivo, con el conocimiento de las vulnerabilidades de este.

**▸** Realizar la encriptación simétrica de un archivo realizando un intercambio seguro de claves en un canal inseguro utilizando el algoritmo Diffie-Hellman.

**▸ Desarrollo paso a paso**

**Parte 1:** realiza el cifrado de cuatro archivos de diferentes pesos (1 MB, 20 MB, 100 MB y 200 MB) con la herramienta OpenSSL empleando los algoritmos DES, 3DES y AES. Puedes descargar ficheros de prueba (test files) de diferentes pesos en muchas webs online. Compara los tiempos de cifrado de cada algoritmo empleando la utilidad «time». Realiza cinco medidas de cada tiempo y obtén el tiempo medio de cifrado de cada algoritmo para cada fichero. Realiza una gráfica que muestre los resultados obtenidos.

**Parte 2:** genera un archivo de texto que tenga tu nombre y apellidos. Este archivo es el que cifraremos a partir de ahora.

**Parte 3:** cifra ese archivo con el algoritmo AES. Mándale el archivo encriptado a un compañero y recibe su archivo encriptado. Desencríptalo y muestra su contenido. ¿Qué información te ha hecho falta para poder desencriptarlo? ¿Cuál es el principal fallo de seguridad de este sistema?

**Parte 4.** Ahora repetiremos el proceso mejorando la seguridad del intercambio de claves empleando el algoritmo Diffie-Hellman. Los pasos por seguir son:

**▸** Un integrante de la pareja genera los parámetros Diffie-Hellman y los comparte con el otro.

**▸** Empleando dichos parámetros, cada integrante genera un número secreto y su número público correspondiente (openssl genpkey/openssl pkey).

**▸** Los integrantes se intercambian sus números públicos.

**▸** Cada integrante emplea su número secreto y el número público del otro para generar una clave compartida (openssl pkeyutl).

**▸** Se verifica que la clave compartida que tiene cada uno de los estudiantes es la misma mediante una función *hash.*

**▸** Cada estudiante emplea dicha clave compartida para cifrar un archivo. Los estudiantes intercambian sus archivos cifrados y comprueban que pueden descifrar el archivo recibido empleando la misma clave.

**▸** ¿Qué diferencias hay con el ejercicio anterior? ¿En qué aspectos mejora la seguridad este algoritmo?

**▸ Solución**

**Parte 1:**

![Figura 54. Instalación de OpenSSL. Fuente: elaboración propia. Instalación de OpenSSL:](images/image-64.png)

*Figura 54. Instalación de OpenSSL. Fuente: elaboración propia.*

Cifrado de archivos:

Se asume que tienes archivos de prueba de diferentes tamaños (1MB, 20MB,

100MB, 200MB) y que ya los tienes descargados o generados.

Donde:

openssl : es el comando para invocar OpenSSL, una herramienta de línea de comandos que proporciona funciones de cifrado, entre otras. e n c : es el subcomando de OpenSSL utilizado para operaciones de cifrado y descifrado.

![Figura 55. Cifrado con DES. Fuente: elaboración propia. ▸ Cifrado con DES:](images/image-65.png)

*Figura 55. Cifrado con DES. Fuente: elaboración propia.*

-des : especifica el algoritmo de cifrado para utilizar. En este caso, Data Encryption Standard (DES), que es un algoritmo de cifrado simétrico de bloque con una clave de 56 bits.

- e : indica que se va a realizar una operación de cifrado ( - d se utilizaría para

descifrado).

-in archivo.txt : especifica el archivo de entrada que se va a cifrar. En este caso, archivo.txt contiene el texto que será cifrado.

-out archivo.des : especifica el nombre del archivo de salida que contendrá el texto cifrado. Aquí, archivo.des será el nombre del archivo cifrado con extensión .des .

![Figura 56. Cifrado con 3DES. Fuente: elaboración propia. ▸ Cifrado con 3DES:](images/image-66.png)

*Figura 56. Cifrado con 3DES. Fuente: elaboración propia.*

Es igual, pero cambia el cifrado.

![Figura 57. Cifrado con AES. Fuente: elaboración propia. ▸ Cifrado con AES:](images/image-67.png)

*Figura 57. Cifrado con AES. Fuente: elaboración propia.*

**Medición de tiempos:** para medir el tiempo de cifrado, puedes usar el comando «time» de Unix junto con el comando de cifrado de OpenSSL. A continuación, se muestra un ejemplo.

![Figura 58. Medir el tiempo de cifrado. Fuente: elaboración propia.](images/image-68.png)

*Figura 58. Medir el tiempo de cifrado. Fuente: elaboración propia.*

Repite este proceso cinco veces para cada tamaño de archivo y algoritmo, luego calcula el tiempo promedio de cifrado.

**Gráfica de resultados:** usa una herramienta como Excel, Google Sheets o matplotlib en Python para graficar los tiempos promedio de cifrado de cada algoritmo para los diferentes tamaños de archivo.

Conclusión:

**▸ Para archivos pequeños** (como 1 MB): la diferencia de tiempo entre AES, 3DES y DES puede no ser muy significativa en términos absolutos, pero AES seguirá siendo generalmente más rápido debido a su diseño eficiente.

**▸ Para archivos grandes** (como 100 MB y 200 MB): la diferencia de tiempo será más notable. AES será probablemente el más rápido, seguido por 3DES y luego DES.

En resumen, si estás realizando mediciones de tiempos de cifrado con OpenSSL para diferentes tamaños de archivos usando DES, 3DES y AES, es muy probable que encuentres que AES es el más rápido en todos los casos, seguido por 3DES y luego DES.

**Parte 2:** genera un archivo de texto que tenga tu nombre y apellidos. Este archivo es el que cifraremos a partir de ahora.

![Figura 59. Generar un archivo de texto. Fuente: elaboración propia.](images/image-69.png)

*Figura 59. Generar un archivo de texto. Fuente: elaboración propia.*

Aquí escribiremos nuestro nombre y apellido.

**Parte 3:** cifra ese archivo con el algoritmo AES.

Utiliza OpenSSL para cifrar el archivo nombre_apellidos.txt utilizando AES-256 en

modo *Cipher Block Chaining* (CBC), que es una opción común y segura para cifrar archivos:

![Figura 60. Cifrar el archivo. Fuente: elaboración propia.](images/image-70.png)

*Figura 60. Cifrar el archivo. Fuente: elaboración propia.*

Al ejecutar este comando, OpenSSL solicitará que ingreses una contraseña (clave). Esta clave es crucial para el proceso de desencriptación, así que asegúrate de recordarla o de compartirla de manera segura con tu compañero.

**▸** Envío del archivo cifrado: Envía el archivo cifrado nombre_apellidos.aes a tu compañero de forma segura, utilizando métodos seguros de transferencia de archivos, como el cifrado de extremo a extremo en aplicaciones de mensajería seguras o mediante un servicio en la nube con cifrado adecuado.

**▸** Recepción del archivo cifrado: Recibe el archivo cifrado nombre_apellidos.aes de tu compañero de manera segura.

**▸** Desencriptado del archivo:

Para desencriptar el archivo recibido, utiliza OpenSSL de la siguiente manera:

![image-71](images/image-71.png)

![Figura 61. Desencriptar el archivo. Fuente: elaboración propia.](images/image-72.png)

*Figura 61. Desencriptar el archivo. Fuente: elaboración propia.*

OpenSSL solicitará la misma contraseña (clave) que se utilizó para cifrar el archivo. Ingresa la clave de forma correcta para que OpenSSL pueda desencriptar el archivo correctamente.

Información necesaria y fallos de seguridad

**▸** Información necesaria para desencriptar: la contraseña (clave) utilizada para cifrar el archivo es necesaria para desencriptarlo correctamente. Sin esta clave, no se puede acceder al contenido del archivo cifrado.

**▸** Principal fallo de seguridad: el principal fallo de seguridad en este sistema es la gestión y la transmisión segura de la contraseña utilizada para cifrar y descifrar el archivo. Si la contraseña no se transmite de manera segura (por ejemplo, si se envía por el mismo canal inseguro que el archivo cifrado), podría ser interceptada por un atacante, quien podría usarla para descifrar el archivo y acceder a su contenido.

Para mejorar la seguridad, es esencial utilizar métodos seguros para la transmisión y gestión de claves, como el uso de canales de comunicación cifrados (como HTTPS o aplicaciones de mensajería segura), o utilizar métodos de intercambio de claves más avanzados como Diffie-Hellman, que garantizan un intercambio seguro de claves sin necesidad de transmitir la clave directamente.

**Parte 4:**

En esta parte de la práctica, utilizaremos el algoritmo de intercambio de claves Diffie- Hellman para mejorar la seguridad del intercambio de claves y, por lo tanto, del cifrado de archivos. Aquí están los pasos detallados:

## 1. Generación de parámetros Diffie-Hellman:

El primer paso es que uno de los participantes genere los parámetros Diffie-Hellman y los comparta con el otro. Los parámetros Diffie-Hellman incluyen un número primo (p) y un generador (g).

![Figura 62. Generación de parámetros Diffie-Hellman. Fuente: elaboración propia.](images/image-73.png)

*Figura 62. Generación de parámetros Diffie-Hellman. Fuente: elaboración propia.*

## 2. Generación de claves públicas y privadas:

Cada integrante de la pareja generará su propia clave privada y su correspondiente clave pública utilizando los parámetros Diffie-Hellman compartidos.

![Figura 63. Generación de claves públicas y privadas. Fuente: elaboración propia. Para la persona A:](images/image-74.png)

*Figura 63. Generación de claves públicas y privadas. Fuente: elaboración propia.*

![Figura 64. Generación de claves públicas y privadas. Fuente: elaboración propia. Para la persona B:](images/image-75.png)

*Figura 64. Generación de claves públicas y privadas. Fuente: elaboración propia.*

## 3. Intercambio de claves públicas:

Cada integrante le envía su clave pública al otro participante de manera segura (por ejemplo, mediante correo electrónico cifrado o cualquier otro canal seguro).

## 4. Generación de la clave compartida:

Cada integrante utiliza su clave privada y la clave pública del otro para generar la clave compartida utilizando OpenSSL.

Para la persona A:

![Figura 65. Generación de la clave compartida. Fuente: elaboración propia.](images/image-76.png)

*Figura 65. Generación de la clave compartida. Fuente: elaboración propia.*

Para la persona B:

![Figura 66. Generación de la clave compartida. Fuente: elaboración propia.](images/image-77.png)

*Figura 66. Generación de la clave compartida. Fuente: elaboración propia.*

## 5. Verificación de la clave compartida:

Ambos participantes deben verificar que la clave compartida que han generado es la misma, utilizando una función *hash.*

![Figura 67. Verificación de la clave compartida. Fuente: elaboración propia.](images/image-78.png)

*Figura 67. Verificación de la clave compartida. Fuente: elaboración propia.*

Si las huellas digitales SHA-256 son idénticas, significa que ambas partes han generado la misma clave compartida de manera exitosa.

## 6. Cifrado y descifrado de archivos:

Cada integrante utiliza la clave compartida para cifrar un archivo y luego intercambian los archivos cifrados para correctamente.

Para cifrar con la clave compartida:

**▸** Persona A cifra con la clave compartida:

openssl enc -aes-256-cbc -e

verificar que puedan descifrarlos

-in nombre_apellidos.txt -out

nombre_apellidos_cifradoA.aes -K $(cat shared_secretA.bin | xxd -p) -iv 0

**▸** Persona B cifra con la clave compartida:

openssl enc -aes-256-cbc -e -in nombre_apellidos.txt -out

nombre_apellidos_cifradoB.aes -K $(cat shared_secretB.bin | xxd -p) -iv 0

Para descifrar con la clave compartida:

**▸** Persona A descifra el archivo recibido de B: openssl enc -aes-256-cbc -d -in nombre_apellidos_cifradoB.aes -out nombre_apellidos_recuperadoA.txt -K $(cat shared_secretA.bin | xxd -p) -iv 0 **▸** Persona B descifra el archivo recibido de A: openssl enc -aes-256-cbc -d -in nombre_apellidos_cifradoA.aes -out nombre_apellidos_recuperadoB.txt -K $(cat shared_secretB.bin | xxd -p) -iv 0

Diferencias con el ejercicio anterior:

**▸ Intercambio seguro de claves:** en lugar de enviar la clave directamente o usar una contraseña compartida, Diffie-Hellman permite un intercambio seguro de claves públicas, lo que no revela las claves privadas y garantiza que solo las partes involucradas puedan generar la clave compartida.

**▸ No hay transmisión directa de la clave:** en el ejercicio anterior, la seguridad dependía de la transmisión segura de la contraseña utilizada para AES, con lo cual es vulnerable si la transmisión no es segura. Con Diffie-Hellman, no se transmite directamente la clave, sino que se genera de manera segura por ambas partes.

Mejoras en la seguridad:

**▸** ***Perfect forward secrecy*** **(PFS):** Diffie-Hellman proporciona PFS, lo que significa que, incluso si una clave privada se ve comprometida en el futuro, los mensajes anteriores cifrados con esa clave no pueden ser descifrados, ya que cada sesión genera una nueva clave compartida.

**▸ Resistencia a ataques de escucha pasiva:** Diffie-Hellman protege contra estos ataques (como la interceptación de la contraseña de AES) al no transmitir directamente la clave y al asegurar que solo las partes involucradas puedan derivar la clave compartida.

En resumen, Diffie-Hellman mejora significativamente la seguridad del intercambio de claves en comparación con el método de contraseña compartida utilizado en el ejercicio anterior, lo que proporciona un método más seguro y robusto para el cifrado de archivos.

## Entrenamiento 5: SSH con clave pública

**▸ Planteamiento del ejercicio** Se desea realizar conexión mediante SSH utilizando el par de claves (pública y privada) de un usuario.

**▸ Desarrollo paso a paso** Requisitos:

**▸** Dos computadoras con Ubuntu instalado y acceso a Internet.

**▸** Conocimientos básicos de línea de comandos en Linux. **Parte 1:** crear el par de claves en la máquina cliente en Ubuntu. **Parte 2:** ubicar la clave pública en el servidor SSH. **Parte 3:** iniciar sesión SSH en el servidor sin la contraseña de la cuenta remota. **Parte 4:** una vez que has conseguido conectar con la clave pública/privada, inhabilita la autenticación con contraseña en su servidor. ¿Por qué ganamos en seguridad al hacer este paso? **Parte 5:** explica por qué es interesante este método de conexión frente al método tradicional de usuario/contraseña.

**▸ Solución** **Parte 1:** crear el par de claves en la máquina cliente en Ubuntu. En la primera máquina (la que actuará como cliente), abrimos una terminal y ejecutamos el siguiente comando para generar el par de claves RSA:

![Figura 68. Generar el par de claves RSA. Fuente: elaboración propia.](images/image-79.png)

*Figura 68. Generar el par de claves RSA. Fuente: elaboración propia.*

Presionamos «Enter» para guardar la clave

en el directorio por defecto

(«/home/usuario/.ssh/id_rsa»). Opcionalmente, podemos ingresar una contraseña para proteger la clave privada (recomendado para mayor seguridad).

**Parte 2:** ubicar la clave pública en el servidor SSH.

Utilizamos el comando «ssh-copy-id» para copiar la clave pública al servidor remoto. Asumiremos que la IP del servidor es «192.168.1.100» y el usuario es «usuario_remoto»:

![Figura 69. Copiar la clave pública del servidor remoto. Fuente: elaboración propia.](images/image-80.png)

*Figura 69. Copiar la clave pública del servidor remoto. Fuente: elaboración propia.*

Nos pedirá la contraseña del usuario remoto para autenticar y copiar la clave pública al archivo «~/.ssh/authorized_keys» en el servidor.

**Parte 3:** iniciar sesión SSH en el servidor sin la contraseña de la cuenta remota.

Intentamos conectarnos al servidor remoto sin ingresar una contraseña:

![Figura 70. Conectarse al servidor remoto sin ingresar una contraseña. Fuente: elaboración propia.](images/image-81.png)

*Figura 70. Conectarse al servidor remoto sin ingresar una contraseña. Fuente: elaboración propia.*

Deberíamos poder acceder al servidor remoto sin ingresar una contraseña, usando la clave privada que generamos en el paso 1.

**Parte 4:** una vez que has conseguido conectar con la clave pública/privada, inhabilita la autenticación con contraseña en su servidor. ¿Por qué ganamos en seguridad al hacer este paso?

Para mejorar la seguridad, podemos desactivar la autenticación con contraseña y permitir solo la autenticación con clave pública en el servidor:

**▸** Editamos el archivo de configuración SSH del servidor:

![Figura 71. Editar el archivo de configuración SSH del servidor. Fuente: elaboración propia.](images/image-82.png)

*Figura 71. Editar el archivo de configuración SSH del servidor. Fuente: elaboración propia.*

**▸** Buscamos la línea que dice «PasswordAuthentication» y aseguramos que esté configurada como `no`:

![Figura 72. Desactivar la autenticación con contraseña. Fuente: elaboración propia.](images/image-83.png)

*Figura 72. Desactivar la autenticación con contraseña. Fuente: elaboración propia.*

**▸** Guardamos y cerramos el archivo.

**▸** Reiniciamos el servicio SSH para que los cambios surtan efecto:

![Figura 73. Reiniciar el servicio SSH. Fuente: elaboración propia.](images/image-84.png)

*Figura 73. Reiniciar el servicio SSH. Fuente: elaboración propia.*

Inhabilitar la autenticación con contraseña en el servidor SSH una vez que has configurado la autenticación mediante claves públicas y privadas proporciona varios beneficios significativos en términos de seguridad:

**▸ Elimina riesgos de fuerza bruta:** cuando la autenticación con contraseña está habilitada, los atacantes pueden intentar realizar ataques de fuerza bruta para adivinar la contraseña de un usuario. Estos ataques son más difíciles de detectar y pueden tener éxito si la contraseña no es lo suficientemente fuerte o si hay otros errores de seguridad en la configuración.

**▸ Protección contra ataques de diccionario:** incluso con contraseñas complejas, los ataques de diccionario pueden ser efectivos si los atacantes tienen suficiente tiempo y recursos para probar múltiples combinaciones de contraseñas.

**▸ Reducción del riesgo de interceptación de contraseñas:** con la autenticación con contraseña existe el riesgo de que esta sea interceptada si la conexión no está cifrada adecuadamente o si hay algún tipo de ataque de intermediario *(man-in-the-* *middle).*

**▸ Mayor control y cumplimiento:** al desactivar la autenticación con contraseña y usar exclusivamente claves públicas y privadas, se establece un método de autenticación más controlado y auditable. Las claves SSH se pueden gestionar centralmente, se pueden revocar rápidamente si es necesario y están asociadas con niveles de acceso específicos basados en la configuración de autorización.

**▸ Facilita el cumplimiento de las políticas de seguridad:** muchas políticas de seguridad y regulaciones requieren el uso de la autenticación multifactor (como claves SSH más contraseñas) o preferentemente el uso de métodos de autenticación más seguros, como las claves SSH. El inhabilitar las contraseñas cuando se utilizan claves SSH asegura que se cumplan estas políticas de seguridad.

En resumen, al inhabilitar la autenticación con contraseña y optar por la autenticación basada en claves SSH, se mejora significativamente la seguridad del sistema al reducir las vulnerabilidades asociadas con el uso de contraseñas, lo que aumenta la resistencia contra ataques y proporciona un método de autenticación más seguro y eficiente para las conexiones SSH.

**Parte 5:** verificar la configuración:

Intentamos conectarnos nuevamente desde la máquina cliente al servidor remoto para asegurarnos de que la autenticación con clave pública funciona y la autenticación con contraseña está deshabilitada.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–36)*
- A fondo  *(pp.37–46)*
- Entrenamientos  *(pp.47–87)*
- Seguridad y Alta Disponibilidad 5 Tema . Material de estudio · Seguridad y Alta Disponibilidad 6 Tema . Material de estudio · Seguridad y Alta Disponibilidad 7 Tema . Material de estudio · Seguridad y Alta Disponibilidad 8 Tema . Material de estudio · Seguridad y Alta Disponibilidad 9 Tema . Material de estudio · Seguridad y Alta Disponibilidad 10 Tema . Material de estudio · Seguridad y Alta Disponibilidad 11 Tema . Material de estudio · Seguridad y Alta Disponibilidad 12 Tema . Material de estudio · Seguridad y Alta Disponibilidad 13 Tema . Material de estudio · Seguridad y Alta Disponibilidad 14 Tema . Material de estudio · Seguridad y Alta Disponibilidad 15 Tema . Material de estudio · Seguridad y Alta Disponibilidad 16 Tema . Material de estudio · Seguridad y Alta Disponibilidad 17 Tema . Material de estudio · Seguridad y Alta Disponibilidad 18 Tema . Material de estudio · Seguridad y Alta Disponibilidad 19 Tema . Material de estudio · Seguridad y Alta Disponibilidad 20 Tema . Material de estudio · Seguridad y Alta Disponibilidad 21 Tema . Material de estudio · Seguridad y Alta Disponibilidad 22 Tema . Material de estudio · Seguridad y Alta Disponibilidad 23 Tema . Material de estudio · Seguridad y Alta Disponibilidad 24 Tema . Material de estudio · Seguridad y Alta Disponibilidad 25 Tema . Material de estudio · Seguridad y Alta Disponibilidad 26 Tema . Material de estudio · Seguridad y Alta Disponibilidad 28 Tema . Material de estudio · Seguridad y Alta Disponibilidad 29 Tema . Material de estudio · Seguridad y Alta Disponibilidad 30 Tema . Material de estudio · Seguridad y Alta Disponibilidad 33 Tema . Material de estudio · Seguridad y Alta Disponibilidad 34 Tema . Material de estudio · Seguridad y Alta Disponibilidad 35 Tema . Material de estudio · Seguridad y Alta Disponibilidad 36 Tema . Material de estudio  *(pp.5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 28, 29, 30, 33, 34, 35, 36)*
- Seguridad y Alta Disponibilidad 37 Tema . A fondo · Seguridad y Alta Disponibilidad 38 Tema . A fondo · Seguridad y Alta Disponibilidad 39 Tema . A fondo · Seguridad y Alta Disponibilidad 40 Tema . A fondo · Seguridad y Alta Disponibilidad 41 Tema . A fondo · Seguridad y Alta Disponibilidad 42 Tema . A fondo · Seguridad y Alta Disponibilidad 43 Tema . A fondo · Seguridad y Alta Disponibilidad 44 Tema . A fondo · Seguridad y Alta Disponibilidad 45 Tema . A fondo · Seguridad y Alta Disponibilidad 46 Tema . A fondo  *(pp.37–46)*
- Seguridad y Alta Disponibilidad 47 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 48 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 49 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 50 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 51 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 52 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 53 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 54 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 55 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 56 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 57 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 58 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 60 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 61 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 62 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 63 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 64 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 65 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 66 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 67 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 68 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 69 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 70 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 71 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 72 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 73 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 74 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 75 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 76 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 77 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 78 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 79 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 80 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 81 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 82 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 83 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 84 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 85 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 86 Tema . Entrenamientos · Seguridad y Alta Disponibilidad 87 Tema . Entrenamientos  *(pp.47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87)*