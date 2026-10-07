## Tema 8

# Servicios en Red e Internet

# Tema 8. Servicios de

# streaming (audio y vídeo)

# Índice

Esquema Material de estudio

## 8.1. Introducción y objetivos

## 8.2. Características

## 8.3. Protocolos

## 8.4. Integración en la web

## 8.5. Uso de redes CDN y direccionamiento multicast

## 8.6. Clientes multimedia

## 8.7. Edición de audio y vídeo

## 8.8. Servir audio y vídeo usando streaming: Open

Broadcaster Studio (OBS)

## 8.9. Referencias bibliográficas

A fondo Cómo insertar vídeo en directo en su sitio web 5 plugins WordPress para añadir streaming a tu sitio web OBS Studio: cómo crear los manuales del futuro Entrenamientos Entrenamiento 1. Trabajar con VLC Media Player Entrenamiento 2. Explorando el Comando FFmpeg Entrenamiento 3. Crear una transmisión en vivo usando OBS

Entrenamiento 4. Creación de una infraestructura de streaming multimedia. Entrenamiento 5. Gestionar una biblioteca multimedia con Ampache e implementar un reproductor HLS en una plataforma web

# Esquema

![image-2](images/image-2.png)

Servicios en Red e Internet 4 Tema 8. Esquema

# 8.1. Introducción y objetivos

E l *streaming* es un método de **transmisión de datos** en **tiempo real** que permite acceder a contenidos multimedia de manera casi instantánea, sin necesidad de descargar archivos completos. En lugar de almacenar los datos en el dispositivo del usuario, los contenidos se reproducen mientras son recibidos y luego se descartan, lo que exige una **conexión a Internet estable.** Esto contrasta con la descarga directa, donde se transfiere el archivo completo al dispositivo y se puede acceder al contenido sin conexión una vez finalizada la descarga.

E l *streaming* ha revolucionado el **consumo de música, radio y televisión.** En música, plataformas como Spotify o Apple Music han transformado la forma en que las personas acceden a millones de canciones, con opciones de descubrimiento de nueva música a través de algoritmos. En cuanto a la radio, servicios como TuneIn e iHeartRadio han expandido la experiencia tradicional, permitiendo emisoras globales y personalizadas. Finalmente, el *streaming* de televisión, liderado por plataformas como Netflix y Disney+, ha cambiado la dinámica del entretenimiento televisivo, ofreciendo contenido bajo demanda y transmisiones en vivo, accesibles en múltiples dispositivos.

Actualmente, los servicios de *streaming* son fundamentales en la **industria del** **entretenimiento,** con un enfoque creciente en la creación de contenido original y producciones internacionales para atraer audiencias globales. Además, la tecnología sigue avanzando y se espera que innovaciones como la realidad virtual y la inteligencia artificial jueguen un papel importante en el futuro del *streaming.*

La integración de **tecnologías** de *streaming* y **comunicación** en la web ha avanzado considerablemente gracias a la adopción de **estándares modernos** como HTML5, WebRTC y HLS.

**HTML5** ha revolucionado la forma en que se maneja el contenido multimedia, permitiendo la reproducción nativa de vídeo y audio sin necesidad de *plugins* externos. **WebRTC,** por su parte, facilita la comunicación en tiempo real entre navegadores, siendo ideal para videoconferencias y chats en vivo. **HLS,** desarrollado por Apple, es un protocolo adaptativo que ajusta la calidad del *streaming* en función de la red del usuario, siendo utilizado en plataformas como YouTube y Netflix.

Además, tecnologías como las **redes CDN** y el **direccionamiento multicast** optimizan la distribución de contenido multimedia, mejorando la eficiencia y calidad de la transmisión. Por otro lado, herramientas como VLC Media Player y FFmpeg permiten la reproducción, edición y gestión avanzada de archivos multimedia, mientras que Open Broadcaster Studio (OBS) se destaca en el ámbito del *streaming* en vivo, proporcionando una plataforma potente y versátil para la transmisión de audio y vídeo en tiempo real.

En resumen, el *streaming* ha democratizado el acceso a los contenidos multimedia, brindando una experiencia más flexible y personalizada en comparación con la descarga directa y ha cambiado de manera profunda cómo consumimos música, radio y televisión.

Los **objetivos** que se pretende alcanzar en este tema son:

**▸** Comprender las diferencias entre *streaming* y descarga directa.

**▸** Conocer las plataformas de *streaming* más populares.

**▸** Identificar los usos y beneficios del *streaming.*

**▸** Analizar las ventajas y desventajas del *streaming* frente a la descarga directa.

**▸** Explorar la historia y evolución del *streaming.*

**▸** Entender los protocolos de transmisión de datos.

**▸** Reconocer el impacto global del *streaming* en la industria del entretenimiento.

**▸** Visualizar las tendencias futuras del *streaming.*

**▸** Manejar tecnologías de comunicación en tiempo real.

**▸** Aplicar protocolos de *streaming* adaptativo.

**▸** Optimizar la distribución de contenido multimedia.

**▸** Desarrollar habilidades de reproducción multimedia.

**▸** Dominar la edición de archivos multimedia.

**▸** Implementar *streaming* en vivo.

# 8.2. Características

¿Qué es el streaming? Comparativa con la descarga directa

El streaming es un **método de transmisión** de datos en **tiempo real.** En lugar de descargar un archivo completo, el contenido se envía en pequeños paquetes desde el servidor al dispositivo del usuario, que se reproduce casi instantáneamente. El usuario no almacena una copia completa del archivo en su dispositivo; en cambio, **el** **contenido se reproduce** a medida que se recibe y luego **se descarta.** Para ello se necesita una conexión estable para una

experiencia de *streaming* fluida. Si la

conexión es interrumpida, la reproducción se detendrá.

Algunos ejemplos son ver un vídeo en YouTube, escuchar música en Spotify o ver una película en Netflix.

A diferencia del *streaming,* la **descarga directa** implica la transferencia completa de un archivo desde un servidor a un dispositivo local (como una computadora, tableta o teléfono inteligente). Una vez que se completa la descarga, el archivo queda almacenado en el dispositivo y puede ser accedido y reproducido tantas veces como se desee, incluso sin conexión a Internet.

![image-3](images/image-3.png)

Tabla 1. Comparativa entre descarga directa (archivo) y *streaming* (continuo). Fuente: elaboración propia.

¿Para qué sirve?

El *streaming* ha transformado la forma en que se distribuyen y consumen contenidos en diversas áreas, como la música, la radio y la televisión. A continuación, te presento un resumen de los usos del *streaming* en cada uno de estos ámbitos:

#### Streaming de música

El *streaming* de música permite a los usuarios escuchar canciones, álbumes y listas de reproducción sin necesidad de descargarlos. Este método ha revolucionado la industria musical, facilitando el acceso instantáneo a vastos catálogos de música.

**▸** Plataformas de *streaming* de música:

- Spotify: ofrece acceso a millones de canciones y permite la creación de listas de reproducción personalizadas. Los usuarios pueden optar por una versión gratuita con

Servicios en Red e Internet 9 Tema 8. Material de estudio anuncios o suscribirse a una versión prémium sin anuncios.

- Apple Music: combina una vasta biblioteca de música con la posibilidad de descargar canciones para escucharlas sin conexión.

- Tidal: se enfoca en la transmisión de música en alta calidad y vídeo, además de ofrecer contenido exclusivo de artistas.

- YouTube Music: permite escuchar música con acceso a vídeos musicales y contenido relacionado.

**▸** Usos:

- Acceso a música bajo demanda: los usuarios pueden escuchar cualquier canción disponible en la plataforma en cualquier momento.

- Descubrimiento de música: las plataformas utilizan algoritmos para recomendar música según las preferencias del usuario, lo que facilita el descubrimiento de nuevos artistas y géneros.

- Listas de reproducción personalizadas: los usuarios pueden crear y compartir listas de reproducción o escuchar listas curadas por la plataforma o por otros usuarios.

#### Streaming de radio

El *streaming* ha expandido la experiencia tradicional de la radio, permitiendo que las emisoras alcancen audiencias globales y ofreciendo opciones de radio a la carta y personalizadas.

**▸** Plataformas de *streaming* de radio:

- TuneIn: ofrece acceso a emisoras de radio en vivo de todo el mundo, además de pódcasts y programas especiales.

- iHeartRadio: permite a los usuarios escuchar estaciones de radio en vivo, crear estaciones personalizadas basadas en artistas o géneros y acceder a pódcasts.

- Pandora: ofrece una experiencia de radio personalizada en la que los usuarios pueden crear estaciones basadas en sus gustos musicales.

- SiriusXM: combina radio por satélite con servicios de streaming, ofreciendo una amplia gama de canales de música, deportes, noticias y entretenimiento.

**▸** Usos:

- Emisión global: las estaciones de radio pueden transmitir en línea, llegando a una audiencia más amplia fuera de su área geográfica tradicional.

- Radio personalizada: los usuarios pueden crear «estaciones» personalizadas basadas en artistas, géneros o canciones específicas.

- Acceso a contenido a la carta: muchos servicios de radio streaming ofrecen la posibilidad de escuchar programas y pódcasts cuando el usuario lo desee, no solo en vivo.

#### Streaming de juego

El *streaming* de videojuegos ha ganado una enorme popularidad en los últimos años, permitiendo que jugadores compartan en tiempo real su experiencia de juego con una audiencia. Este fenómeno ha dado lugar a comunidades vibrantes y a la creación de plataformas dedicadas al contenido en vivo, con diversos usos y características.

**▸** Principales plataformas de *streaming* de juegos:

- Twitch: la plataforma más grande para el streaming de videojuegos. Ofrece transmisiones en vivo, suscripciones a canales, donaciones y un chat interactivo.

- YouTube Gaming: compite directamente con Twitch, integrándose en el ecosistema de YouTube. *Streaming* en vivo y vídeos bajo demanda, con integración al sistema de comentarios de YouTube.

- Facebook Gaming: parte de la expansión de Facebook hacia los videojuegos. Fácil integración con cuentas de Facebook, con un enfoque en la comunidad de amigos y seguidores.

- Trovo: plataforma más reciente y en crecimiento, con un enfoque en la interacción social. Sistema de recompensas y puntos para la audiencia.

- Kick: nueva plataforma que busca competir directamente con Twitch ofreciendo una mejor repartición de ingresos para los *streamers. Streaming* en vivo con enfoque en la comunidad.

**▸** Usos:

- Entretenimiento: los streamers transmiten sus sesiones de juego para entretener a sus seguidores, con interacciones en tiempo real.

- Educación: tutoriales y guías de juegos, donde los streamers explican mecánicas, estrategias y trucos.

- Eventos y competiciones: los torneos de deportes electrónicos y competiciones profesionales son muy populares en plataformas de *streaming.*

- Just Chatting: espacio para que los creadores conversen con su audiencia sobre diversos temas más allá del juego.

- Monetización: los streamers pueden ganar dinero a través de donaciones, suscripciones, patrocinios y publicidad.

Estas plataformas no solo son lugares de entretenimiento, sino también *hubs* sociales donde los jugadores y fans interactúan en tiempo real, haciendo del *streaming* una parte clave de la cultura de los videojuegos.

#### Streaming de TV

El *streaming* de televisión ha cambiado radicalmente cómo se consume el contenido televisivo, pasando de la programación lineal tradicional a opciones bajo demanda y en vivo a través de Internet.

**▸** Plataformas de *streaming* de TV:

- Netflix: ofrece series, películas, documentales y programas originales que pueden ser vistos en cualquier momento.

- Hulu: combina series de TV actuales con contenido clásico y original, además de ofrecer transmisión en vivo de algunos canales.

- Disney+: ofrece contenido de Disney, Pixar, Marvel, Star Wars y National Geographic

- HBO Max: ofrece contenido de HBO junto con películas y series de Warner Media.

- YouTube TV: proporciona acceso en vivo a canales de televisión tradicionales a través de Internet, junto con la posibilidad de grabar programas en la nube.

**▸** Usos:

- Vídeo bajo demanda (VOD): permite a los usuarios ver programas de televisión y películas cuando lo deseen, sin estar limitados por horarios de transmisión.

- Transmisión en vivo: algunos servicios permiten ver canales de televisión en vivo, como deportes, noticias y eventos especiales.

- Contenido original: las plataformas de streaming producen y distribuyen contenido original exclusivo, lo que ha cambiado la dinámica de producción en la industria televisiva.

- Acceso multidispositivo: los usuarios pueden ver contenido en una variedad de dispositivos, como televisión y teléfonos inteligentes, tabletas y computadoras, con la

Servicios en Red e Internet 13 Tema 8. Material de estudio capacidad de pausar y reanudar en diferentes dispositivos.

En resumen, el *streaming* ha democratizado el acceso al contenido, permitiendo a los usuarios disfrutar de música, radio y televisión de una manera más flexible, personalizada y global.

Historia y funcionalidad

El mundo de los servicios de *streaming* ha experimentado un crecimiento explosivo en las últimas dos décadas, transformando por completo cómo consumimos entretenimiento. Aquí te doy un recorrido por su historia.

Los primeros servicios de *streaming* de vídeo datan de finales de la década de **1990.** RealNetworks, fundada en 1994, fue una de las pioneras al lanzar **RealPlayer,** un *software* que permitía a los usuarios transmitir contenido multimedia en Internet. Sin embargo, la tecnología y las conexiones a Internet en ese momento eran limitadas, lo que hacía que la calidad fuera baja y la experiencia del usuario, insatisfactoria.

El verdadero cambio llegó con la fundación de **YouTube** e n **2005.** Esta plataforma permitió a cualquier persona con una cámara y acceso a Internet subir y compartir vídeos con una audiencia global. Su modelo basado en la publicidad y su enfoque en contenido generado por los usuarios fueron revolucionarios. YouTube popularizó el concepto de vídeo bajo demanda, donde los usuarios podían ver lo que quisieran, cuando quisieran.

**Netflix,** que comenzó en 1997 como un servicio de alquiler de DVD por correo, marcó un punto de inflexión en la historia del *streaming.* En **2007,** lanzó su servicio de transmisión en línea, permitiendo a los suscriptores ver series y películas directamente a través de Internet. Esto fue una innovación clave, que capitalizó el aumento de las velocidades de Internet y la proliferación de dispositivos como portátiles y teléfonos inteligentes.

Netflix no solo distribuyó contenido, sino que también comenzó a producirlo, con la serie *House of Cards* en 2013, lo que la convirtió en una plataforma de **creación de** **contenido original.** Esto marcó el comienzo de la era del *binge-watching,* donde los usuarios podían ver temporadas completas de series sin interrupciones.

El éxito de Netflix atrajo a otros grandes jugadores

al mercado del *streaming.*

Amazon lanzó Prime Video en 2011, mientras que Hulu, que comenzó en 2007, consolidó su posición como un fuerte competidor, particularmente en la oferta de contenido televisivo reciente. Estos servicios, junto con otros como HBO Now (lanzado en 2015), Apple TV+ (2019) y Disney+ **competencia y** diversificaron la **oferta** de contenido.

(2019), intensificaron la

Cada plataforma comenzó a buscar su propio nicho, con Netflix enfocándose en la creación de una amplia variedad de contenido original, Amazon en combinar sus ofertas de *streaming* con su servicio Prime y Disney+ en capitalizar su enorme catálogo de franquicias populares.

E l *streaming* se ha convertido en un **fenómeno global,** con servicios como Netflix disponibles en más de 190 países. Esto ha cambiado no solo cómo se distribuye el contenido, sino también qué tipo de contenido se crea. Las plataformas están invirtiendo en producciones locales para atraer audiencias internacionales y el contenido no anglófono ha ganado visibilidad global.

Actualmente, el mercado de *streaming* está en constante evolución. La guerra del *streaming* se ha intensificado con la entrada de nuevos jugadores y el lanzamiento de servicios como Peacock (de NBCUniversal) y Paramount+ (de ViacomCBS). Además, la pandemia de COVID-19 aceleró la adopción del *streaming,* ya que las personas buscaban entretenimiento en casa durante los confinamientos.

Se espera que el *streaming* continúe creciendo, con tecnologías emergentes como la realidad virtual (VR) y la inteligencia artificial (IA) posiblemente jugando un papel importante en el futuro. Además, la forma en que las personas pagan por contenido

Servicios en Red e Internet 15 Tema 8. Material de estudio también podría cambiar, con más opciones de modelos de suscripción, publicidad, y pago por visión.

![Figura 1. Plataformas de streaming más vistas en España en 2023. Fuente: Morillo, 2023.](images/image-4.png)

*Figura 1. Plataformas de streaming más vistas en España en 2023. Fuente: Morillo, 2023.*

En resumen, el *streaming* ha pasado de ser una novedad técnica para convertirse en la forma dominante de consumo de contenido en todo el mundo, redefiniendo la industria del entretenimiento de manera profunda y permanente.

# 8.3. Protocolos

En la arquitectura de sistemas de *streaming,* los protocolos juegan un papel crucial en la transmisión y el control de datos multimedia. Aquí te presento una visión detallada de los protocolos más importantes en esta área, incluyendo sus características y usos.

RTMP (Real-Time Messaging Protocol)

**▸** Descripción:

- Desarrollador: Macromedia (ahora Adobe).

- Tipo: propietario.

- Uso principal: streaming de vídeo y audio en tiempo real.

**▸** Características:

- Protocolos subyacentes: TCP.

- Transmisión: permite transmisión continua en vivo y bajo demanda.

- Capacidades: soporta vídeo, audio y datos. Es ideal para aplicaciones interactivas, como transmisiones en vivo y chat en vídeo.

- Compresión: utiliza códecs como H.264 para vídeo y AAC para audio.

**▸** Ventajas:

- Latencia baja: ideal para transmisiones en tiempo real debido a su baja latencia.

- Interactividad: soporta características interactivas como chat en vivo y encuestas.

**▸** Desventajas:

- Obsolescencia: ha perdido popularidad con la disminución del soporte para flash y la migración a protocolos más modernos.

- Compatibilidad: menor compatibilidad con dispositivos móviles y navegadores modernos sin soporte *flash.*

RTP (Real-Time Transport Protocol) y RTCP (Real-Time Control Protocol)

**▸** Descripción:

- RTP (RFC 3550): protocolo para la transmisión de datos en tiempo real, como audio y vídeo.

- RTCP (RFC 3550): protocolo complementario para el control de RTP, proporcionando retroalimentación sobre la calidad del servicio.

**▸** Características:

- Transmisión: utiliza UDP para la transmisión de datos, permitiendo la entrega continua en tiempo real.

- Control: RTCP proporciona estadísticas y control sobre la calidad del flujo RTP, como la pérdida de paquetes y el retraso.

- Capacidades: diseñado para aplicaciones en tiempo real como videoconferencias y transmisión de audio.

**▸** Ventajas:

- Adaptación en tiempo real: permite la adaptación dinámica a las condiciones de red cambiantes.

- Información de calidad: RTCP proporciona información sobre la calidad del servicio y ayuda en la gestión de la red.

**▸** Desventajas:

- No adaptativo: RTP por sí solo no realiza adaptaciones de calidad basadas en la red; esto depende de aplicaciones de nivel superior.

RTSP (Real-Time Streaming Protocol)

**▸** Descripción:

- RFC: 2326.

- Tipo: protocolo de control para el streaming en tiempo real.

- Uso principal: control y gestión de streaming multimedia en tiempo real.

**▸** Características:

- Transmisión: utiliza UDP para datos y TCP para el control.

- Control: permite operaciones como play, pause y stop en flujos multimedia.

- Interactividad: facilita el control remoto de la transmisión de medios.

**▸** Ventajas:

- Control fino: ofrece un control preciso sobre la reproducción y gestión de streams.

- Flexibilidad: puede trabajar con diferentes protocolos de transporte, adaptándose a las necesidades específicas de la aplicación.

**▸** Desventajas:

- Latencia: puede tener una mayor latencia debido al uso de TCP para el control.

- Complejidad: la implementación puede ser más compleja en comparación con otros protocolos de *streaming.*

DASH (Dynamic Adaptive Streaming over HTTP)

**▸** Descripción:

- Tipo: protocolo de streaming adaptativo basado en HTTP.

- Uso principal: streaming adaptativo de vídeo y audio a través de HTTP.

**▸** Características:

- Transmisión: utiliza HTTP para la entrega de contenido, permitiendo la adaptación dinámica a las condiciones de red.

- Adaptabilidad: ajusta la calidad del vídeo en función del ancho de banda disponible y las capacidades del dispositivo.

- Contenedores: soporta varios formatos de contenedores y códecs.

**▸** Ventajas:

- Adaptación dinámica: mejora la experiencia del usuario ajustando la calidad del vídeo en tiempo real.

- Compatibilidad: funciona con la mayoría de los navegadores y dispositivos que soportan HTTP.

**▸** Desventajas:

- Buffering inicial: puede haber un pequeño buffering inicial mientras el cliente se adapta a la calidad de la red.

HLS (HTTP Live Streaming)

**▸** Descripción:

- RFC: 8216.

- Tipo: protocolo de streaming basado en HTTP desarrollado por Apple.

- Uso principal: streaming de vídeo y audio en vivo y bajo demanda.

**▸** Características:

- Transmisión: utiliza HTTP para entregar segmentos de vídeo en formatos como TS (Transport Stream) y M3U8 (lista de reproducción).

- Adaptabilidad: permite la adaptación dinámica a diferentes calidades de red.

- Segmentación: divide el contenido en segmentos pequeños para una reproducción eficiente.

**▸** Ventajas:

- Compatibilidad amplia: compatible con una amplia gama de dispositivos y plataformas, incluidos iOS y macOS.

- Adaptación a la red: permite una experiencia de visualización suave adaptando la calidad según las condiciones de la red.

**▸** Desventajas:

- Latencia: puede tener una mayor latencia en comparación con otros protocolos debido a la segmentación y el *buffering.*

Estos protocolos son fundamentales para la transmisión eficiente y la gestión del contenido multimedia en una variedad de aplicaciones, desde transmisiones en vivo hasta servicios de vídeo bajo demanda.

# 8.4. Integración en la web

La integración de tecnologías de *streaming* y comunicación en la web se ha facilitado significativamente con los avances en estándares y protocolos modernos. A continuación, te presento cómo se integran

enfocándonos en HTML5, WebRTC y HLS.

HTML5

#### Descripción

HTML5 es la última versión del lenguaje de

estas tecnologías en la web,

marcado HTML, diseñado para

estructurar y presentar contenido en la web. Introdujo nuevas funcionalidades que han revolucionado la forma en que se manejan multimedia y *streaming.*

**Características clave:**

**▸** Elementos de multimedia integrados:

- <vídeo>: permite la integración de contenido de vídeo directamente en la página web sin necesidad de *plugins* externos. Soporta varios formatos de vídeo, incluyendo MP4, WebM y Ogg.

- <audio>: similar al <vídeo>, permite la integración de contenido de audio en la página web, soportando formatos como MP3, WAV y Ogg.

**▸** API de JavaScript:

- Canvas API: permite la manipulación de imágenes y vídeo en tiempo real, lo que es útil para aplicaciones que requieren edición o visualización personalizada.

- Media Source Extensions (MSE): permite a los desarrolladores construir transmisiones de vídeo personalizadas y adaptativas en la web mediante JavaScript.

**▸** Compatibilidad:

- HTML5 es compatible con la mayoría de los navegadores modernos, lo que facilita la reproducción de contenido multimedia en diversas plataformas sin la necesidad de *plugins* adicionales.

**▸** Ventajas:

- Simplicidad: integración directa de multimedia en la web sin necesidad de plugins.

- Compatibilidad amplia: soporte nativo en la mayoría de los navegadores.

- Flexibilidad: amplias opciones para manipular y controlar contenido multimedia.

**▸** Desventajas:

- Soporte de formatos: algunos navegadores tienen soporte limitado para ciertos formatos de vídeo y audio.

WebRTC (Web Real-Time Communication)

#### Descripción

WebRTC es una tecnología que permite la comunicación en tiempo real directamente entre navegadores web sin la necesidad de plugins adicionales. Está diseñada para aplicaciones de videoconferencia, chat en vivo y otras formas de comunicación en tiempo real. **Características clave:**

**▸** Protocolos:

- RTP/RTCP: utilizado para la transmisión de datos en tiempo real y control de calidad.

- ICE (Interactive Connectivity Establishment): ayuda en la negociación de conexiones directas entre clientes.

- STUN/TURN: protocolos para superar problemas de NAT (Network Address Translation) y *firewall.*

**▸** API:

- getUserMedia(): permite a las aplicaciones web acceder a la cámara y micrófono del usuario.

- RTCPeerConnection: maneja la conexión de datos en tiempo real, incluyendo la codificación y transmisión de audio y vídeo.

- RTCDataChannel: permite el intercambio de datos en tiempo real entre navegadores.

**▸** Ventajas:

- Baja latencia: ideal para aplicaciones que requieren comunicación en tiempo real.

- Interoperabilidad: compatible con la mayoría de los navegadores modernos.

- Sin plugins: funciona directamente en el navegador sin necesidad de plugins adicionales.

**▸** Desventajas:

- Complejidad: la configuración y el manejo de conexiones en tiempo real pueden ser complejos.

- Problemas de red: puede haber problemas relacionados con NAT y firewall que pueden complicar la conexión directa.

**▸** Uso común:

- Videoconferencias, chat en vivo, aplicaciones de colaboración en tiempo real.

HLS (HTTP Live Streaming)

#### Descripción

HLS es un protocolo de *streaming* adaptativo basado en HTTP desarrollado por Apple. Permite la transmisión de contenido multimedia en vivo y bajo demanda a través de la web.

#### Características clave

**▸** Segmentación:

- Segmentos de vídeo: divide el vídeo en pequeños segmentos (usualmente de diez a treinta segundos) que se descargan secuencialmente.

- Listas de reproducción: utiliza archivos M3U8 para listar los segmentos y las diferentes calidades del vídeo.

**▸** Adaptación:

- Adaptación dinámica: ajusta la calidad del vídeo según las condiciones de la red y las capacidades del dispositivo del usuario.

**▸** Compatibilidad:

- Navegadores y dispositivos: ampliamente compatible con dispositivos iOS y otros navegadores modernos.

**▸** Ventajas:

- Compatibilidad amplia: funciona en una amplia gama de dispositivos y navegadores.

- Adaptación a la red: ajusta la calidad del streaming en función del ancho de banda disponible.

- Simplicidad: basado en HTTP, lo que simplifica la integración con redes de entrega de contenido (CDNs).

**▸** Desventajas:

- Latencia: puede tener mayor latencia en comparación con otros protocolos de *streaming* debido a la segmentación y el *buffering.*

- Fragmentación: puede requerir múltiples versiones del contenido para diferentes calidades.

**▸** Uso común:

- Streaming de vídeo en vivo y bajo demanda en plataformas como YouTube, Netflix y otras aplicaciones de *streaming.*

# 8.5. Uso de redes CDN y direccionamiento multicast

Las redes de entrega de contenidos (CDN) y el direccionamiento multicast son

#### tecnologías clave en la transmisión eficiente

abordan distintos aspectos de la distribución

de contenido en redes. Ambas de contenido, optimizando la

experiencia del usuario final y la gestión de recursos de red. A continuación, se detalla cómo cada tecnología se utiliza en el contexto del *streaming* y su impacto en la eficiencia y la calidad del servicio.

Redes CDN (Content Delivery Network)

Una CDN es una red distribuida de servidores que **almacena copias** del contenido en múltiples ubicaciones geográficas. Su objetivo es entregar el contenido a los usuarios de manera más rápida y eficiente, reduciendo la latencia y el tiempo de carga.

Direccionamiento Multicast

El multicast es una técnica de transmisión de datos en redes que permite a **un solo** **flujo de datos** ser enviado a múltiples destinatarios simultáneamente, en lugar de enviar copias separadas a cada receptor.

![Comparativa CDN vs. Multicast](images/image-5.png)

Tabla 2. Comparativa CDN vs. Multicast. Fuente: elaboración propia

Los CDN son ideales para la **entrega eficiente** de contenido multimedia a **nivel** **global,** mejorando la velocidad y calidad de la almacenamiento en caché y la optimización de rutas.

transmisión mediante el

El Multicast es efectivo para la **transmisión simultánea** a **múltiples usuarios,** reduciendo el uso de ancho de banda en redes

internas o en aplicaciones

específicas como la televisión digital y los eventos en vivo.

Ambas tecnologías tienen sus ventajas y desventajas y se eligen en función de los requisitos específicos de transmisión y distribución de contenido.

# 8.6. Clientes multimedia

VLC Media Player: clientes multimedia

VLC Media Player es uno de los reproductores multimedia más populares y versátiles disponibles para una amplia gama de sistemas operativos. Es conocido por su capacidad de reproducir casi cualquier formato de audio y video y por su flexibilidad en la gestión de contenido multimedia.

#### Componentes de VLC Media Player

**▸** Interfaz de usuario (UI):

- Controles de reproducción: botones para reproducir, pausar, detener, avanzar o retroceder el contenido multimedia.

- Lista de reproducción: permite a los usuarios agregar, organizar y gestionar archivos multimedia para la reproducción continua.

- Visualización de contenido: área donde se muestra el vídeo o se reproduce el audio.

**▸** Motor de reproducción:

- Decodificación: procesa los datos de los archivos multimedia, utilizando códecs para decodificar vídeo y audio.

- Renderizado: muestra el contenido de vídeo en la pantalla y reproduce el audio a través del sistema de altavoces.

**▸** Biblioteca de medios:

- Gestión de medios: permite a los usuarios organizar y buscar archivos multimedia en su sistema.

- Metadatos: muestra información sobre los archivos, como el título, el artista y el álbum para contenido musical.

**▸** Ajustes y configuración:

- Preferencias de vídeo y audio: permite ajustar la calidad de reproducción, la sincronización de audio y vídeo y otros parámetros.

- Subtítulos y captions: configuración para cargar, ajustar y sincronizar subtítulos y *captions.*

**▸** Funcionalidades avanzadas:

- Transcodificación: convierte archivos multimedia de un formato a otro.

- Streaming: permite la transmisión de contenido en vivo o bajo demanda a través de redes.

- Grabación: graba contenido multimedia en vivo o desde archivos existentes.

#### Códecs soportados

VLC Media Player es conocido por su amplia compatibilidad con diferentes códecs de audio y vídeo. A continuación, se detallan algunos de los códecs más comunes que VLC puede manejar:

**▸** Códecs de vídeo:

- H.264/AVC: formato de compresión de vídeo comúnmente utilizado en streaming y almacenamiento.

- H.265/HEVC: códec de vídeo de alta eficiencia que ofrece mejor compresión que H.264.

- VP8 y VP9: códecs de vídeo desarrollados por Google, utilizados en streaming en línea y aplicaciones web.

- MPEG-2: códec de vídeo utilizado en DVD y algunas transmisiones de televisión.

- Theora: códec de vídeo libre y abierto, utilizado en algunos formatos de vídeo en línea.

**▸** Códecs de audio:

- MP3: códec de audio popular para compresión de música.

- AAC: códec de audio avanzado utilizado en transmisiones en vivo y servicios de *streaming.*

- FLAC: códec de audio sin pérdida que ofrece alta calidad de sonido.

- Vorbis: códec de audio libre y abierto utilizado en algunos formatos de streaming y archivos multimedia.

- Opus: códec de audio de alta calidad y baja latencia, utilizado en comunicación en tiempo real y *streaming.*

#### Uso de VLC Media Player

**▸** Reproducción de medios:

- Versatilidad: capaz de reproducir casi cualquier tipo de archivo multimedia, incluyendo vídeo, audio y formatos menos comunes.

- Calidad: ofrece opciones avanzadas para ajustar la calidad de reproducción y la sincronización de audio y vídeo.

**▸** *Streaming* y grabación:

- Streaming: soporta la transmisión de contenido multimedia en vivo a través de protocolos como HTTP, RTSP y RTP.

- Grabación: permite grabar contenido en vivo desde fuentes como cámaras o transmisiones en línea.

**▸** Conversión de formatos:

- Transcodificación: convierte archivos multimedia a diferentes formatos, lo que es útil para la compatibilidad con otros dispositivos y plataformas.

**▸** Uso en redes:

- Streaming en red: puede servir como servidor de streaming para distribuir contenido multimedia a través de una red local o Internet.

- Acceso a Contenidos en Línea: Soporta la reproducción de contenido desde URLs y transmisiones en vivo.

**▸** Personalización y ajustes:

- Configuración personalizada: permite ajustar diversos parámetros de reproducción, como la velocidad de reproducción, la sincronización de subtítulos y los efectos visuales.

- Subtítulos: capacidad para cargar y sincronizar subtítulos externos o incrustados en los archivos multimedia.

# 8.7. Edición de audio y vídeo

FFmpeg: edición de audio y vídeo

FFmpeg es una colección de bibliotecas y herramientas de *software* de código abierto que permite la conversión, grabación, edición y transmisión de archivos multimedia. Es ampliamente utilizado en la industria para procesos de codificación, decodificación, transcodificación, *muxing, demuxing, streaming,* filtrado y reproducción de audio y vídeo.

#### Componentes clave de FFmpeg

**▸** ffmpeg:

- Función principal: comando principal que ejecuta operaciones de conversión y edición de archivos multimedia.

- Usos comunes: conversión de formatos, transcodificación, mezcla de audio y vídeo y extracción de información de archivos.

**▸** ffplay:

- Función principal: reproductor multimedia basado en la biblioteca FFmpeg.

- Usos comunes: visualización rápida de archivos multimedia y pruebas de streaming.

**▸** ffprobe:

- Función principal: herramienta para analizar y mostrar información sobre archivos multimedia.

- Usos comunes: inspección de metadatos, información de códecs, y estadísticas de archivos multimedia.

**▸** libavcodec, libavformat, libavfilter, libavdevice, libswscale, libswresample:

- Función principal: bibliotecas de bajo nivel que FFmpeg utiliza para codificación, decodificación, filtrado, redimensionamiento y otros procesos relacionados con audio y vídeo.

- Usos comunes: proporcionan funcionalidades específicas que FFmpeg utiliza internamente para llevar a cabo tareas de procesamiento de medios.

#### Capacidades de edición automatizada con FFmpeg

FFmpeg es especialmente útil para la edición de audio y video en modo automatizado gracias a sus capacidades programables y de línea de comandos. Aquí algunos ejemplos de cómo se puede utilizar FFmpeg para tareas comunes de edición:

**▸** Conversión de formatos:

- Comando: ffmpeg -i input.mp4 output.avi

- Descripción: convierte un archivo de video de formato MP4 a AVI.

**▸** Extracción de audio de un vídeo:

- Comando: ffmpeg -i input.mp4 -q:a 0 -map a output.mp3

- Descripción: extrae el audio de un archivo de vídeo y lo guarda como MP3.

**▸** Recorte de vídeo:

- Comando: ffmpeg -i input.mp4 -ss 00:00:30 -to 00:01:00 -c copy output.mp4

- Descripción: recorta un segmento de un archivo de vídeo, desde el segundo treinta hasta el minuto uno.

**▸** Redimensionamiento de vídeo:

$$• Comando: ffmpeg -i input.mp4 -vf scale=1280:720 output.mp4$$

- Descripción: redimensiona un archivo de vídeo a una resolución de 1280 x 720 píxeles.

**▸** Añadir subtítulos a un vídeo:

- Comando: ffmpeg -i input.mp4 -vf subtitles=subtitles.srt output.mp4

- Descripción: añade un archivo de subtítulos SRT a un vídeo.

**▸** Filtrado de vídeo (por ejemplo, aplicar un filtro de desenfoque):

- Comando: ffmpeg -i input.mp4 -vf "blur=5" output.mp4

- Descripción: aplica un filtro de desenfoque al vídeo.

**▸** Transcodificación de vídeo a diferente códec:

- Comando: ffmpeg -i input.mp4 -c:v libx265 -c:a aac output.mp4

- Descripción: convierte un vídeo al códec H.265 para vídeo y AAC para audio.

**▸** Unir archivos de vídeo:

- Comando: ffmpeg -f concat -safe 0 -i filelist.txt -c copy output.mp4

- Descripción: une varios archivos de vídeo en un solo archivo (se requiere un archivo de texto con la lista de archivos por unir).

**▸** Generación de Thumbnails de vídeo:

- Comando: ffmpeg -i input.mp4 -ss 00:00:10 -vframes 1 thumbnail.png

- Descripción: genera una imagen en miniatura (thumbnail) del vídeo en el segundo diez.

#### Ventajas de Usar FFmpeg

- ▸ Flexibilidad y potencia: ofrece una amplia gama de funcionalidades para trabajar con

    - audio y vídeo, desde la conversión básica hasta la edición avanzada.

- ▸ Automatización: ideal para scripts y procesos automatizados, lo que facilita la

    - integración en flujos de trabajo más grandes.

- ▸ Código abierto: gratuito y de código abierto, lo que permite personalización y

    - adaptación a necesidades específicas.

- ▸ Soporte de formatos: compatible con una amplia variedad de formatos de archivo y

    - códecs.

#### Desventajas

- ▸ Interfaz de línea de comandos: requiere conocimientos de la línea de comandos y

    - puede tener una curva de aprendizaje para nuevos usuarios.

- ▸ Configuración compleja: algunas operaciones avanzadas pueden requerir

    - configuraciones y parámetros detallados.

        - Servicios en Red e Internet 36 Tema 8. Material de estudio

# 8.8. Servir audio y vídeo usando streaming: Open

# Broadcaster Studio (OBS)

Open Broadcaster Studio (OBS) es una herramienta de *software* de código abierto que se utiliza ampliamente para la transmisión en vivo y la grabación de vídeo. Es conocida por su flexibilidad, potencia y capacidades multiplataforma, permitiendo a los usuarios capturar, codificar y transmitir audio y vídeo en tiempo real.

A continuación, se detalla cómo OBS se utiliza para servir contenido multimedia a través de *streaming* y sus principales características.

Características principales de Open Broadcaster Studio (OBS)

#### Captura de fuentes de vídeo y audio en tiempo real

OBS permite capturar diversas fuentes de vídeo y audio en tiempo real. Esto incluye:

**▸** Dispositivos de captura de vídeo: cámaras web, cámaras de vídeo externas y capturadoras de *hardware.*

**▸** Fuentes de vídeo de pantalla: captura de pantalla completa, ventanas individuales o regiones específicas del escritorio.

**▸** Audio: captura de audio desde micrófonos, mezcladores de audio y otras fuentes de entrada.

#### Composición de escenas y añadido de filtros

OBS permite a los usuarios crear y gestionar múltiples escenas, cada una con diferentes fuentes y filtros. Las funciones incluyen:

**▸** Composición de escenas: crear múltiples escenas que pueden incluir combinaciones de vídeo, audio, imágenes, textos y más. Puedes alternar entre estas escenas durante la transmisión.

**▸** Filtros: aplicar filtros a las fuentes de vídeo y audio, como corrección de color, eliminación de fondo y mejoras de audio (ecualización, compresión, etc.).

#### Codificación y transmisión (streaming)

OBS utiliza el códec x264 para la codificación de video y ofrece soporte para varios protocolos de streaming, como RTMP.

**▸** Codificación de vídeo: OBS utiliza x264 para codificar el vídeo en formatos adecuados para *streaming,* ajustando la calidad y el bitrate según las configuraciones del usuario.

**▸** *Streaming:* se conecta a plataformas de *streaming* mediante protocolos como RTMP, permitiendo la transmisión en vivo de vídeo a servicios como YouTube, Vimeo, Twitch, entre otros.

#### Grabación local

Además de la transmisión en vivo, OBS permite la grabación local de vídeo y audio. Puedes guardar tus transmisiones o grabaciones en el disco duro en formatos como MP4, MKV o FLV.

# 8.9. Referencias bibliográficas

Morillo, V. (2023, Julio 7). Estas son las plataformas de *streaming* más vistas en España en 2023, por ahora. *El español.* <https://www.elespanol.com/series/20230707/plataformas-streaming-vistas-espanaahora/777172357_0.html>

# streaming-en-su-sitio-web/

# Cómo insertar vídeo en directo en su sitio web

Duhamel, H. (2024, septiembre 17). Cómo insertar vídeo en directo en su sitio web [2023 Update]. *Dacast.* <https://www.dacast.com/es/blog-es/como-incrustar-videos-en-> Si tienes o gestionas un sitio web y quieres incluir vídeo en directo este es tu sitio. No te conformes con la emisión que te proporciona YouTube, sube un nivel y muestra un contenido de manera más profesional.

Servicios en Red e Internet 40 Tema 8. A fondo

# anadir-streaming-a-tu-sitio-web/

# 5 plugins WordPress para añadir streaming a tu

# sitio web

Martín, B. (2015). 5 plugins WordPress para añadir streaming a tu sitio web. *Video* *C o n t e n t .* <https://videocontent.es/blog/video-streaming/5-plugins-wordpress-para-> Para realizar una webinar, para integrar YouTube en vivo en tu sitio web, para utilizar *streaming* utilizando dispositivos de audio y vídeo propios, para almacenar contenido en tu nube de Amazon y disponer de ello para emitir en tu web o si quieres montar una tienda con servicios de *streaming* para la venta, este es tu sitio.

Servicios en Red e Internet 41 Tema 8. A fondo

# Nacional de Tecnologías Educativas y de Formación del Profesorado.

# OBS Studio: cómo crear los manuales del futuro

Muro, A. Z. (2020). OBS Studio: cómo crear los manuales del futuro. *Instituto* [https://intef.es/observatorio_tecno/obs-studio-como-crear-los-manuales-del-futuro/](https://intef.es/observatorio_tecno/obs-studio-como-crear-los-manuales-del-futuro/)

Aquí vas a descubrir unos primeros pasos para aprender a usar la herramienta de código libre OBS Studio donde podrás combinar, al mismo tiempo, audio, vídeo, imágenes, música, pizarra, etc.

Servicios en Red e Internet 42 Tema 8. A fondo

# Entrenamiento 1. Trabajar con VLC Media Player

#### ▸ Planteamiento del ejercicio

#### Parte1: instalación VLC y prueba de funcionamiento

Deberás instalar el *software* VLC Media Player y comprueba que puedes abrir (en local y en remoto): **▸** En disco: un vídeo, un audio. **▸** En remoto:

- Ver listas m3u8: canal de noticias (24/7): <http://iptv.3nq2.com:8000/live/stream.m3u8>, canal de deportes: <https://media.streamlive.to/stream/live.m3u8>, canal de entretenimiento: <https://cdn2.wowza.com/streaming/mysample.mp4/playlist.m3u8>.

- Ver vídeos de YouTube con VLC.

#### Parte2: preguntas

**▸** ¿Cuáles son los componentes principales de la interfaz de usuario de VLC Media Player? **▸** ¿Qué tipos de códecs de audio y vídeo son soportados por VLC Media Player? **▸** ¿Cómo puede VLC Media Player ser utilizado para reproducir archivos multimedia en una red local? **▸** ¿Cómo se pueden personalizar los atajos de teclado en VLC Media Player? **▸** ¿Qué opciones de transcodificación ofrece VLC Media Player y cómo se pueden utilizar?

**▸** Establece distintos usos que se pueden dar al software VLC Media Player.

#### ▸ Desarrollo paso a paso

Sigue los pasos planteados en cada apartado y resuelve las cuestiones planteadas.

#### ▸ Solución

#### Parte 1

#### Instalación de VLC

**▸** Descargar VLC:

- Windows/Mac: Ve al sitio web oficial de VLC en <videolan.org> (<https://www.videolan.org/vlc/>). Descarga el instalador adecuado para tu sistema operativo.

- Linux: puedes instalar VLC a través del gestor de paquetes de tu distribución. Por ejemplo, en Ubuntu, usa el comando sudo apt install vlc .

**▸** Instalar VLC:

- Windows: ejecuta el archivo descargado y sigue las instrucciones del asistente de instalación.

- Mac: abre el archivo .dmg descargado y arrastra VLC a la carpeta de aplicaciones.

- Linux: la instalación se completará automáticamente al ejecutar el comando en el terminal.

#### Abrir archivos locales en VLC

**▸** Abrir un vídeo:

- Windows/Mac/Linux: abre VLC, ve a «Medios» > «Abrir archivo» (o usa el atajo «Ctrl+O» en Windows/Linux, «Cmd+O» en Mac), navega hasta el archivo de vídeo en tu disco y selecciona «Abrir».

**▸** Abrir un audio:

- Windows/Mac/Linux: similar al vídeo, ve a «Medios» > «Abrir archivo», selecciona tu archivo de audio y haz clic en «Abrir».

#### Ver contenidos remotos en VLC

Listas M3U8: **▸** Abre VLC. **▸** Ve a «Medios» > «Abrir red฀» (o usa «Ctrl+N» en Windows/Linux, «Cmd+N» en Mac). **▸** Ingresa la URL de la lista M3U8 que deseas ver y haz clic en «Reproducir». Por ejemplo, puedes usar una URL pública como <https://example.com/playlist.m3u8> (reemplaza con una lista válida). Puedes utilizar los enlaces proporcionados en el enunciado: **▸** Canal de Noticias (24/7): <http://iptv.3nq2.com:8000/live/stream.m3u8>. **▸** Canal de Deportes: <https://media.streamlive.to/stream/live.m3u8>. **▸** Canal de entretenimiento:

<https://cdn2.wowza.com/streaming/mysample.mp4/playlist.m3u8>.

Consejos adicionales **▸** Listas M3U8: asegúrate de que la URL sea válida y accesible desde tu red. Algunas listas M3U8 requieren autenticación o pueden no estar disponibles. **▸** YouTube: la reproducción directa de vídeos de YouTube puede no funcionar siempre debido a cambios en el formato o a las políticas de YouTube. En algunos casos, es posible que necesites complementos adicionales o usar métodos alternativos.

#### Parte 2

#### ¿Cuáles son los componentes principales de la interfaz de usuario de VLC

#### Media Player?

Los componentes principales de la interfaz de usuario de VLC Media Player incluyen: **▸** Barra de menú: ofrece opciones como medios, vista, herramientas y ayuda. **▸** Controles de reproducción: botones para reproducir, pausar, detener, avanzar, retroceder, etc. **▸** Barra de progreso: muestra el progreso de reproducción del archivo de medios. **▸** Lista de reproducción: muestra los archivos que están en cola para reproducirse. **▸** Pantalla de vídeo: área principal donde se muestra el contenido multimedia. **¿Qué tipos de códecs de audio y vídeo son soportados por VLC Media Player?** VLC Media Player es conocido por su amplia compatibilidad con códecs. Algunos de los códecs soportados incluyen: **▸** Códecs de vídeo: H.264, H.265 (HEVC), MPEG-4, MPEG-2, VP8, VP9, AV1. **▸** Códecs de audio: MP3, AAC, FLAC, OGG, WAV, ALAC, Opus.

**▸** Códecs de subtítulos: SRT, SUB, ASS, SSA.

#### ¿Cómo puede VLC Media Player ser utilizado para reproducir archivos

#### multimedia en una red local?

Para reproducir archivos multimedia en una red local con VLC:

**▸** Abrir VLC y seleccionar «Medios» → «Abrir red».

**▸** Ingresar la URL del archivo o flujo en la red local (por ejemplo, una dirección IP o

nombre de archivo compartido en la red).

**▸** Hacer clic en «Reproducir» para comenzar la reproducción del contenido en la red.

#### ¿Cómo se pueden personalizar los atajos de teclado en VLC Media Player?

Para personalizar los atajos de teclado en VLC:

**▸** Abrir VLC y seleccionar «Herramientas» → «Preferencias».

**▸** Ir a la pestaña «Atajos de teclado».

**▸** Modificar o asignar nuevos atajos para las funciones deseadas.

**▸** Guardar los cambios haciendo clic en «Guardar».

#### ¿Qué opciones de transcodificación ofrece VLC Media Player y cómo se

#### pueden utilizar?

VLC ofrece varias opciones de transcodificación para convertir archivos multimedia a diferentes formatos:

**▸** Abrir VLC y seleccionar «Medios» → «Convertir / Guardar».

**▸** Agregar el archivo que deseas transcodificar.

**▸** Hacer clic en «Convertir / Guardar».

**▸** Elegir el perfil de conversión deseado (como MP4, MKV, AVI).

**▸** Configurar las opciones adicionales si es necesario y seleccionar la ubicación de destino.

**▸** Hacer clic en «Iniciar» para comenzar el proceso de transcodificación.

#### Diferentes usos del VLC Media Player

VLC Media Player es una herramienta extremadamente versátil que se puede usar para una variedad de propósitos. Aquí te detallo algunos de los usos más comunes y útiles de VLC:

**▸** Reproducción de archivos multimedia:

- Audio y vídeo local: reproduce casi cualquier formato de archivo de audio o vídeo almacenado en tu disco duro, como MP4, MKV, MP3, AVI, etc.

- Dispositivos externos: reproduce archivos multimedia desde dispositivos externos como USB, discos duros externos o unidades de red.

**▸** *Streaming* de contenidos en red:

- Flujos en vivo: permite ver transmisiones en vivo y canales de TV mediante URL de listas M3U8, RTSP o HTTP.

- Reproducción de contenidos de red local: reproduce archivos multimedia ubicados en otros dispositivos en tu red local (por ejemplo, usando una dirección de red UNC o IP).

**▸** Transcodificación de archivos:

- Conversión de formatos: convierte archivos multimedia de un formato a otro, por ejemplo, de AVI a MP4 o de FLAC a MP3.

- Ajustes de calidad: permite ajustar la calidad de los archivos convertidos, como la

Servicios en Red e Internet 48 Tema 8. Entrenamientos resolución, el bitrate y los códecs de audio/vídeo.

**▸** Captura y grabación de vídeo

- Grabar desde Webcam: graba vídeo desde una cámara web o dispositivo de captura.

- Grabar el escritorio: graba lo que ocurre en tu escritorio para crear tutoriales, presentaciones o capturas de pantalla en movimiento.

- Grabar streams: graba transmisiones en vivo o vídeos en streaming mientras se reproducen en VLC.

**▸** Visualización y edición de subtítulos:

- Carga de subtítulos: agrega archivos de subtítulos externos a tus videos (SRT, SUB, ASS, etc.).

- Sincronización: ajusta la sincronización de los subtítulos con el vídeo en caso de desincronización.

- Edición: modifica el tamaño, color y posición de los subtítulos durante la reproducción.

**▸** Edición básica de vídeos:

- Recorte y fusión: recorta secciones de vídeo y fusiona múltiples clips en uno solo (a través de la opción de «Convertir / Guardar»).

- Aplicación de filtros: aplica filtros básicos como corrección de color, efectos de vídeo y rotación de imagen.

**▸** Reproducción de contenidos de CD y DVD:

- CD de audio: reproduce CD de audio directamente desde VLC.

- DVD: reproduce DVD y Blu-ray, incluyendo menús y características adicionales, siempre que el soporte de decodificación esté disponible.

**▸** Configuración de listas de reproducción:

- Listas de reproducción personalizadas: crea y gestiona listas de reproducción para organizar y reproducir múltiples archivos de audio o vídeo en secuencia.

- Guardar listas de reproducción: guarda listas de reproducción para usarlas en el futuro o compartirlas con otros.

**▸** Reproducción de contenidos en diferentes protocolos:

- Protocolos de streaming: soporta diversos protocolos de streaming como HTTP, FTP, MMS y RTSP.

- Reproducción de contenidos web: permite reproducir vídeos desde páginas web y plataformas que proporcionan URL directas a los archivos de vídeo.

**▸** Interfaz y personalización

- Temas y skins: personaliza la apariencia de VLC con diferentes temas y skins.

- Atajos de teclado: configura atajos de teclado personalizados para controlar la reproducción de manera más eficiente.

VLC Media Player es una herramienta muy completa que puede adaptarse a una amplia gama de necesidades relacionadas con la reproducción, conversión y grabación de medios. Si necesitas ayuda con alguna de estas funciones o tienes alguna pregunta específica, no dudes en preguntar.

# Entrenamiento 2. Explorando el Comando FFmpeg

#### ▸ Planteamiento del ejercicio

Se desea familiarizarse con las funcionalidades básicas de FFmpeg para la manipulación de archivos multimedia.

Materiales: **▸** Computadora con FFmpeg instalado. **▸** Archivos multimedia (vídeo y audio) para manipular (se pueden descargar ejemplos desde Internet o usar archivos locales).

#### ▸ Desarrollo paso a paso

**▸** Instala el *software* FFmpeg en tu computadora.

- Indica los pasos para instalarlo en Windows.

- Indica los pasos para instalarlo en Ubuntu.

**▸** Introducción al comando FFmpeg.

- Revisa la descripción general del comando ffmpeg y sus principales usos.

- Abre una terminal o consola en tu computadora.

**▸** Obtener información de un vídeo.

**▸** Convertir el formato de un vídeo.

**▸** Modificar la calidad del vídeo.

**▸** Redimensionar o rotar el vídeo.

**▸** Extraer audio del vídeo.

**▸** Recortar vídeo o audio.

**▸** Extraer fotogramas del vídeo.

Reflexión: ¿qué funcionalidades de FFmpeg encontraste más útiles o interesantes?

Discusión opcional: ¿en qué proyectos futuros podrías utilizar FFmpeg?

#### ▸ Solución

**▸** Instala el *software* FFmpeg en tu computadora.

- Indica los pasos para instalarlo en Windows

**▸** Descargar FFmpeg:

**•** Ve a la página oficial de FFmpeg: <https://ffmpeg.org/download.html>.

- En la sección «Get packages & executable files», selecciona el enlace a Windows builds from gyan.dev.

- Descarga el archivo comprimido (zip) desde la sección «Release builds».

**▸** Extraer los archivos:

- Una vez descargado, descomprime el archivo en una ubicación de fácil acceso, como C:\FFmpeg .

**▸** Agregar FFmpeg al PATH del sistema:

- Haz clic derecho en «Este PC» o «Mi PC» y selecciona «Propiedades».

- Haz clic en «Configuración avanzada del sistema» y luego en «Variables de entorno».

- En «Variables del sistema», selecciona la variable «Path» y haz clic en «Editar».

- Haz clic en «Nuevo» y añade la ruta donde extrajiste FFmpeg, por ejemplo: C:\FFmpeg\bin .

- Haz clic en «Aceptar» en todas las ventanas.

**▸** Verificar instalación:

- Abre una consola de comandos (Windows + R, escribe «cmd», y presiona «Enter»).

- Escribe «ffmpeg» y presiona «Enter». Si ves información sobre FFmpeg, la instalación ha sido exitosa.

Indica los pasos para instalarlo en Ubuntu

#### Actualizar los repositorios

Abre una terminal y actualiza los repositorios del sistema.

![image-6](images/image-6.png)

#### Instalar FFmpeg

Para instalar FFmpeg, simplemente ejecuta el siguiente comando:

![image-7](images/image-7.png)

#### Verificar instalación

Una vez completada la instalación, escribe «ffmpeg» en la terminal para verificar que

todo esté funcionando correctamente.

#### Introducción al comando FFmpeg

**▸** Revisa la descripción general del comando ffmpeg y sus principales usos. FFmpeg es una herramienta de línea de comandos que permite convertir, procesar, editar y manipular archivos multimedia (vídeo y audio). Es compatible con una gran cantidad de formatos y códecs, lo que lo hace extremadamente versátil.

**▸** Abre una terminal o consola en tu computadora. Una vez que tengas la terminal abierta, puedes comenzar a ejecutar los comandos de FFmpeg.

#### Obtener información de un vídeo

Usa el siguiente comando para obtener detalles sobre el vídeo de ejemplo que hayas elegido:

![image-8](images/image-8.png)

Preguntas de reflexión:

**▸** ¿Qué información se muestra?

- Formato del archivo: el tipo de archivo (por ejemplo, MP4, AVI, MOV).

- Códecs de vídeo y audio: qué tecnologías se usan para codificar el vídeo y el audio.

- Resolución: la cantidad de píxeles del vídeo (por ejemplo, 1920 x 1080).

- FPS: cuántos fotogramas por segundo tiene el vídeo (por ejemplo, 30 fps).

- Duración del vídeo: tiempo total que dura el archivo (por ejemplo, 00:05:32).

- Tasa de bits: la tasa a la que se transfieren los datos de vídeo y audio, que puede afectar la calidad.

**▸** ¿Cuáles son los códecs de vídeo y audio?

**•**

**•** Códec de vídeo: aparecerá algo como «Vídeo: h264» o «Vídeo: vp8», indicando el formato de compresión de vídeo.

- Códec de audio: mostrará algo como «Audio: aac», «Audio: mp3» o cualquier otro formato de audio que esté usando tu archivo.

**▸** ¿Cuál es la duración del archivo?

- La duración del vídeo se mostrará en un formato como Duration: 00:05:32.15, lo que significa que el vídeo dura cinco minutos y 32 segundos (con 15 milisegundos).

Convertir el formato de un vídeo: Convierte el vídeo a otro formato (por ejemplo, de AVI a MP4 o viceversa):

![image-9](images/image-9.png)

Ejercicio opcional: prueba convertir el archivo a otro formato como MKV

#### Modificar la calidad del vídeo

Ajusta la calidad del vídeo usando uno de los siguientes comandos:

![image-10](images/image-10.png)

O utilizando el control CRF:

![image-11](images/image-11.png)

Tarea: compara el tamaño de los archivos antes y después de cambiar la calidad.

#### Redimensionar o rotar el vídeo

Redimensiona el vídeo a una resolución específica:

![image-12](images/image-12.png)

O rota el vídeo a noventa grados:

![image-13](images/image-13.png)

Desafío: experimenta con diferentes resoluciones o ángulos de rotación.

#### Extraer audio del vídeo

Extrae el audio del vídeo y guárdalo como un archivo MP3:

![image-14](images/image-14.png)

Tarea: reproduce el archivo de audio generado y verifica la calidad.

#### Recortar vídeo o audio

Recorta un segmento específico del vídeo, por ejemplo, del segundo treinta al minuto

uno:

![image-15](images/image-15.png)

O recorta un segmento de audio:

![image-16](images/image-16.png)

Ejercicio: crea clips cortos a partir del archivo original y compara los tiempos.

#### Extraer fotogramas del vídeo

Extrae un fotograma específico del vídeo en el segundo diez:

![image-17](images/image-17.png)

O extrae imágenes en intervalos regulares (por ejemplo, una imagen por segundo):

#### Cierre

![image-18](images/image-18.png)

Reflexión: ¿qué funcionalidades de ffmpe encontraste más útiles o interesantes?

Las funcionalidades que destacan en ffmpeg son su capacidad para convertir formatos y extraer audio, ya que estas son tareas comunes cuando se trabaja con contenido multimedia. Otra funcionalidad muy útil es la posibilidad de recortar segmentos de un vídeo o audio sin pérdida de calidad, lo que es valioso para la edición rápida. La opción de redimensionar y rotar vídeos también es interesante, sobre todo si se necesita adaptar archivos para diferentes plataformas o pantallas.

Además, la capacidad de extraer fotogramas es fascinante, ya que permite crear imágenes estáticas a partir de vídeos, útil para análisis visual o creación de miniaturas. También, es destacable la posibilidad de unir archivos de vídeo fácilmente o añadir subtítulos, lo cual es esencial para proyectos que involucren múltiples archivos de vídeo o cuando se trabaja con contenido accesible.

Discusión opcional: ¿en qué proyectos futuros podrías utilizar ffmpeg?

ffmpeg podría ser útil en varios tipos de proyectos. Aquí, algunas ideas:

**▸** Edición y producción de vídeos: podrías usar ffmpeg para crear clips, cambiar formatos o reducir la resolución de vídeos para compartirlos en diferentes plataformas.

**▸** Creación de contenidos para redes sociales: convertir videos largos en clips más cortos, añadir subtítulos o extractar fotogramas para crear imágenes de vista previa o miniaturas.

**▸** Desarrollo de aplicaciones multimedia: si desarrollas una aplicación que necesita procesar vídeo/audio, ffmpeg sería la herramienta ideal para integrar funcionalidades de conversión y edición en segundo plano.

**▸** Automatización de procesamiento de archivos: podrías automatizar procesos en lotes para convertir múltiples archivos a la vez, lo que sería útil en proyectos que requieren grandes volúmenes de datos multimedia.

**▸** Análisis de vídeo: si trabajas con vídeo para análisis o investigación, podrías usar ffmpeg para extraer segmentos de vídeo o fotogramas para análisis más detallado.

# Entrenamiento 3. Crear una transmisión en vivo

# usando OBS

#### ▸ Planteamiento del ejercicio

Aprenderás a configurar una transmisión en vivo utilizando OBS, capturando vídeo y audio, creando escenas y aplicando filtros, así como grabando el contenido localmente. Materiales requeridos:

**▸** Computadora con acceso a Internet.

**▸** Micrófono y cámara web (o dispositivo de captura de vídeo).

**▸** *Software* OBS instalado.

#### ▸ Desarrollo paso a paso

- Parte 1. Instalación y configuración inicial.

- Parte 2. Crear escenas y añadir filtros.

- Parte 3. Configurar el streaming.

- Parte 4. Iniciar la transmisión y grabación.

- Parte 5. Evaluación final.

#### ▸ Solución

#### Parte 1. Instalación y configuración inicial

**▸** Descarga e instalación de OBS:

**•** Descarguen e instalen OBS desde el sitio oficial <https://obsproject.com/>.

**▸** Configuración de vídeo y audio:

- Abre OBS y agrega tu cámara web como una fuente de vídeo: Fuentes → Agregar → Dispositivo de captura de vídeo → Selecciona tu cámara.

- Añade una fuente de audio: Fuentes → Agregar → Entrada de audio → Selecciona tu micrófono.

#### Parte 2. Crear escenas y añadir filtros

**▸** Crear una nueva escena:

- Ve a la sección «Escenas» y haz clic en «Agregar». Nombra la escena como «Introducción».

**▸** Añadir filtros a una fuente de vídeo:

- Selecciona la fuente de tu cámara web en la escena creada.

- Haz clic derecho en la fuente y selecciona «Filtros». Añade el filtro de Chroma Key si tienes un fondo verde o, simplemente, ajusta la corrección de color.

#### Parte 3. Configurar el streaming

**▸** Conectar OBS a un servicio de *streaming* (Twitch, YouTube):

- En OBS, haz clic en «Configuración» (ubicado en la parte inferior derecha de la interfaz).

- Ve a la sección «Transmisión».

- En Servicio, selecciona la plataforma de streaming que vas a usar (por ejemplo, YouTube o Twitch).

- Inicia sesión en tu cuenta de la plataforma de streaming desde tu navegador.

- Localiza la clave de transmisión en tu cuenta de streaming: en YouTube, ve a YouTube Studio → Crear directo → Configuración → Clave de transmisión. En Twitch, ve a Configuración del Canal → Transmisión → Clave de transmisión principal.

- Copia la clave de transmisión desde la plataforma de streaming.

- Pégala en OBS en el campo «Clave de transmisión».

- Haz clic en «Aceptar» para guardar los cambios.

**▸** Ajustar la codificación de vídeo:

- Ve a Configuración → Salida.

- En la sección «Codificación», ajusta el bitrate de vídeo: para calidad media, selecciona entre 2500-3500 kbps, para alta calidad (recomendado para Full HD), selecciona entre 4000-6000 kbps.

- En «Resolución de salida», selecciona la resolución de vídeo que deseas transmitir: 1920 x 1080 (Full HD) para alta calidad, 1280 x 720 (HD) si prefieres usar menos ancho de banda.

- En «Tasa de fotogramas» (FPS), selecciona entre 30 FPS o 60 FPS: 30 FPS para una transmisión estándar, 60 FPS si deseas un vídeo más fluido, especialmente para videojuegos o contenido con movimiento rápido.

- Haz clic en «Aceptar» para guardar los ajustes.

#### Parte 4. Iniciar la transmisión y grabación

**▸** Iniciar el *streaming:*

- Una vez que hayas configurado las escenas y conectado a tu servicio de streaming, haz clic en Iniciar transmisión.

**▸** Grabar el *streaming* localmente:

- También puedes grabar la transmisión en tu computadora. En Configuración → Salida selecciona el formato de grabación (MP4 recomendado) y haz clic en «Iniciar grabación».

#### Parte 5. Evaluación final

Discusión:

Reflexionar sobre la experiencia de transmisión y analizar cómo las diferentes fuentes de vídeo y audio impactan la calidad del *streaming.*

Preguntas para guiar la discusión:

**▸** ¿Qué tipos de fuentes de vídeo y audio usaron durante la transmisión? ¿Cómo eligieron cada fuente?

**▸** ¿Cómo creen que la calidad de la cámara *(webcam* vs. cámara profesional) influye en la percepción del público?

**▸** ¿Qué efecto tiene el uso de micrófonos de calidad en la claridad del sonido transmitido? ¿Notaron alguna diferencia significativa?

**▸** ¿Cómo afecta la configuración del bitrate en la calidad del vídeo y la estabilidad de la transmisión?

**▸** Si usaron filtros (como Chroma Key), ¿cómo cambiaron la presentación del contenido? ¿Facilitó esto la creatividad en la transmisión?

**▸** ¿Hubo algún problema técnico durante la transmisión relacionado con las fuentes de audio o video? ¿Cómo lo solucionaron?

**¿Qué tipos de fuentes de vídeo y audio usaron durante la transmisión? ¿Cómo**

#### eligieron cada fuente?

Respuesta: utilicé una cámara web para la captura de vídeo, ya que es fácil de configurar y proporciona una calidad aceptable para transmisiones en vivo. Para el audio, usé un micrófono USB, que ofrece un sonido más claro y definido que el micrófono integrado de la computadora. Elegí estas fuentes por su accesibilidad y calidad, ideales para un entorno de transmisión.

#### ¿Cómo creen que la calidad de la cámara (webcam vs. cámara profesional)

#### influye en la percepción del público?

Respuesta: la calidad de la cámara tiene un gran impacto en la percepción del público. Una cámara profesional puede ofrecer una resolución más alta, mejor manejo de la luz y un enfoque más nítido, lo que mejora la experiencia visual. En contraste, una webcam puede verse borrosa o pixelada, lo que puede distraer y hacer que el contenido parezca menos profesional.

**¿Qué efecto tiene el uso de micrófonos de calidad en la claridad del sonido**

#### transmitido? ¿Notaron alguna diferencia significativa?

Respuesta: el uso de micrófonos de calidad mejora drásticamente la claridad del sonido. Noté que, al usar un micrófono externo, el audio era más claro y tenía menos ruido de fondo en comparación con el micrófono integrado. Esto permite una mejor comunicación con la audiencia y mejora la experiencia general.

**¿Cómo afecta la configuración del bitrate en la calidad del vídeo y la**

#### estabilidad de la transmisión?

Respuesta: la configuración del bitrate es crucial. Un bitrate más alto, generalmente, proporciona mejor calidad de vídeo, pero también requiere más ancho de banda. Si el bitrate es demasiado bajo, el vídeo puede aparecer pixelado o entrecortado. Durante la prueba, noté que un bitrate de 4500 kbps ofreció un buen equilibrio entre calidad y estabilidad, aunque en conexiones más lentas puede ser necesario bajarlo.

#### Si usaron filtros (como Chroma Key), ¿cómo cambiaron la presentación del

#### contenido? ¿Facilitó esto la creatividad en la transmisión?

Respuesta: usar el filtro Chroma Key fue muy útil para cambiar el fondo y hacer que la presentación fuera más dinámica. Esto permitió que el contenido se viera más profesional y atractivo. La creatividad se vio facilitada al poder incorporar diferentes escenarios y elementos visuales, lo que ayudó a captar mejor la atención de la audiencia.

#### ¿Hubo algún problema técnico durante la transmisión relacionado con las

#### fuentes de audio o vídeo? ¿Cómo lo solucionaron?

Respuesta: al principio, experimenté algunos problemas de sincronización entre el audio y el vídeo. Para solucionarlo, ajusté la latencia en la configuración de audio de OBS y también reinicié el programa. Además, verifiqué las conexiones de mis dispositivos de captura para asegurarme de que estaban bien configurados.

#### Conclusión de la discusión

**▸** Reflexionar sobre la importancia de seleccionar las fuentes adecuadas para obtener una experiencia de *streaming* óptima.

**▸** Resaltar que tanto la calidad del *hardware* (cámaras y micrófonos) como la configuración del *software* (OBS) son cruciales para el éxito de una transmisión.

Entrenamiento 4. Creación de una infraestructura de streaming multimedia.

#### ▸ Planteamiento del ejercicio

Con este entrenamiento vamos a aprender a utilizar FFmpeg para crear flujos de video y audio. Requisitos:

**▸** Un servidor RTMP (puedes usar Nginx con el módulo RTMP).

**▸** FFmpeg instalado en tu sistema (Windows o Ubuntu).

**▸** Un vídeo de ejemplo para transmitir (puede ser cualquier archivo .mp4 que tengas disponible).

#### ▸ Desarrollo paso a paso

- Parte 1. Configuración de FFmpeg para streaming.

- Parte 2. Configuración de Ampache.

- Parte 3. Implementación de un reproductor HLS en la Web.

#### ▸ Solución

#### Parte 1. Configuración de FFmpeg para streaming

#### Preparación de entorno

**▸** Instalación de FFmpeg:

- Instruir a los participantes para que instalen FFmpeg en sus sistemas. Proporcionar enlaces a las guías de instalación para diferentes sistemas operativos (Windows, macOS, Linux).

#### Instalación de FFmpeg en Windows

Descargar FFmpeg: **▸** Ve al sitio web oficial de FFmpeg: <https://ffmpeg.org/download.html>. **▸** Haz clic en «Get packages & executable files» para acceder a las versiones precompiladas de FFmpeg. **▸** Selecciona el enlace para la plataforma Windows y descarga la versión estática desde <https://www.gyan.dev/ffmpeg/builds/>. Extraer el archivo: **▸** Después de descargar el archivo ZIP, extrae su contenido en una carpeta. Puedes extraerla, por ejemplo, en C:\ffmpeg . Configurar la variable de entorno: **▸** Abre el explorador de archivos y haz clic derecho en «Este equipo» o «Mi PC». **▸** Selecciona «Propiedades» y luego haz clic en «Configuración avanzada del sistema». **▸** En la pestaña «Avanzado», haz clic en el botón «Variables de entorno». **▸** En la sección «Variables del sistema», busca la variable Path y haz clic en «Editar». **▸** Haz clic en «Nuevo» e introduce la ruta donde extrajiste FFmpeg, por ejemplo:

C:\ffmpeg\bin.

**▸** Guarda los cambios y cierra las ventanas.

Verificar la instalación: **▸** Abre el símbolo del sistema (puedes buscar cmd en el menú de inicio). **▸** Escribe el siguiente comando para verificar si FFmpeg está correctamente instalado: **▸** Si la instalación fue exitosa, deberías ver información sobre la versión de FFmpeg.

![image-19](images/image-19.png)

#### Instalación de FFmpeg en Ubuntu

Actualizar los paquetes: **▸** Abre una terminal y asegúrate de que tu sistema esté actualizado:

![image-20](images/image-20.png)

Instalar FFmpeg: **▸** Usa el siguiente comando para instalar FFmpeg desde los repositorios oficiales de Ubuntu:

![image-21](images/image-21.png)

Verificar la instalación: **▸** Una vez que la instalación esté completa, verifica que FFmpeg se haya instalado correctamente ejecutando:

![image-22](images/image-22.png)

**▸** Si ves la información de la versión de FFmpeg, la instalación ha sido exitosa.

Actualizar FFmpeg (opcional): **▸** Si deseas instalar la versión más reciente de FFmpeg, puedes agregar el repositorio PPA:

![Transmisión en vivo con FFmpeg y RTMP](images/image-23.png)

#### Parte 1. Configurar un Servidor RTMP usando Nginx con el Módulo RTMP

Instalación de Nginx con Módulo RTMP en Ubuntu: **▸** Instalar las dependencias necesarias:

![image-24](images/image-24.png)

**▸** Configurar Nginx para usar RTMP: abre el archivo de configuración de Nginx con un editor de texto:

![image-25](images/image-25.png)

**▸** Añadir la configuración RTMP: agrega lo siguiente al final del archivo nginx.conf .

![image-26](images/image-26.png)

**▸** Guardar y salir (presiona «CTRL+O» para guardar y «CTRL+X» para salir). **▸** Reiniciar Nginx:

![image-27](images/image-27.png)

**▸** Verificar que el puerto 1935 esté escuchando (puerto RTMP):

![image-28](images/image-28.png)

Si todo está configurado correctamente, el puerto 1935 estará en uso por Nginx.

Instalación de Nginx con RTMP en Windows:

Para Windows, puedes usar [Nginx con RTMP precompilado] <https://www.nginx.com/resources/wiki/modules/rtmp/>. **▸** Descarga la versión con el módulo RTMP preinstalado desde el [sitio de Nginx RTMP Windows] <https://nginx.org/en/download.html>. **▸** Configura el archivo nginx.conf como se muestra arriba y reinicia Nginx en Windows.

**Parte 2. Usar FFmpeg para transmitir un vídeo en vivo a través de RTMP** Proporcionar un vídeo de ejemplo: Para este ejercicio, puedes usar cualquier archivo de video en formato .mp4. Si no tienes uno, puedes descargar un vídeo de muestra de Internet, como desde

<https://sample-videos.com/>.

Transmitir el vídeo usando FFmpeg:

Una vez que el servidor RTMP esté configurado y corriendo, puedes usar FFmpeg

para transmitir el vídeo al servidor RTMP.

**▸** Comando de FFmpeg para transmitir el video, donde:

- input.mp4 : es el archivo de vídeo que deseas transmitir.

- libx264 : es el códec de video H.264.

- aac : Ees el códec de audio AAC.

- flv : formato de archivo de transmisión.

- rtmp://localhost/live/stream-key : es la URL del servidor RTMP. Si el servidor está en una máquina remota, reemplaza localhost con la IP o nombre de dominio del servidor y elige un *stream-key* adecuado.

![image-29](images/image-29.png)

**▸** Verificar la transmisión:

- Usa un cliente de reproducción RTMP como VLC o OBS para verificar la transmisión en vivo.

- En VLC, ve a «Medios» → «Abrir red» e ingresa la URL:

![image-30](images/image-30.png)

#### Parte 3. Opciones avanzadas de FFmpeg para la transmisión

Puedes ajustar varios parámetros según la calidad de transmisión deseada:

Cambiar la tasa de bits de vídeo:

![image-31](images/image-31.png)

![image-32](images/image-32.png)

-b:v 1M: establece la tasa de bits del video a 1 Mbps.

-b:a 128k: establece la tasa de bits del audio a 128 kbps.

Transmisión en múltiples calidades *(streaming* adaptativo):

Si deseas transmitir en varias calidades (por ejemplo, 720p y 1080p), puedes usar un

archivo .ffm que permita múltiples transmisiones adaptativas, pero este es un paso más avanzado.

#### Conclusión

Este ejercicio te permite comprender cómo configurar un servidor RTMP con Nginx y utilizar FFmpeg para transmitir vídeo en vivo. A través de la configuración adecuada y las opciones avanzadas de FFmpeg, puedes ajustar la calidad de la transmisión y usar múltiples clientes (como VLC) para ver el resultado.

# Entrenamiento 5. Gestionar una biblioteca multimedia con Ampache e implementar un reproductor HLS en una plataforma web

#### ▸ Planteamiento del ejercicio

Infraestructura para Streaming: usando bibliotecas y plataformas Web.

En la infraestructura de *streaming,* diferentes herramientas y tecnologías se integran para gestionar, transmitir y reproducir contenido multimedia. En el entrenamiento anterior implantamos el uso de FFmpeg con protocolos de *streaming.* A continuación, se exploran varios aspectos clave de esta infraestructura, incluyendo la gestión de bibliotecas multimedia en Internet y el uso de plataformas web y reproductores para *streaming.*

#### ▸ Desarrollo paso a paso

- Parte 1. Configuración de Ampache en Windows y Ubuntu.

- Parte 2. Implementación de un Reproductor HLS en la Web.

#### ▸ Solución

#### Parte 1. Configuración de Ampache

Tu biblioteca de audio y vídeo en Internet: Ampache

Ampache es un servidor de medios web que permite la gestión y transmisión de audio y vídeo a través de Internet. Es una plataforma de código abierto que puede usarse para crear tu propia biblioteca de medios en línea.

Características:

**▸** Gestión de medios: organiza y administra bibliotecas de música y vídeo.

**▸** Transmisión en *streaming:* permite la transmisión de medios a través de HTTP o HTTPS.

**▸** Acceso remoto: accede a tus medios desde cualquier dispositivo con un navegador web.

**▸** Interfaz de usuario: ofrece una interfaz web para explorar, reproducir y gestionar tu biblioteca multimedia. Configuración básica para la instalación de Ampache:

#### Instalación de Ampache en Ubuntu

Como requisitos previo, antes de instalar Ampache, debes asegurarte de tener configurado un servidor web con Apache, PHP y MySQL/MariaDB. Actualizar el sistema:

![image-33](images/image-33.png)

Instalar Apache, PHP y MariaDB:

**▸** Instalar Apache:

![image-34](images/image-34.png)

**▸** Instalar PHP y módulos necesarios: Ampache requiere algunos módulos de PHP para funcionar correctamente. Puedes instalarlos con el siguiente comando:

![▸ Instalar MariaDB (o MySQL):](images/image-35.png)

![image-36](images/image-36.png)

**▸** Configurar la base de datos: inicia el servicio de MariaDB y configura la contraseña root:

![image-37](images/image-37.png)

Durante el proceso, selecciona una contraseña para el usuario root y configura las opciones según tus necesidades.

Descargar e instalar Ampache:

**▸** Descargar Ampache: ve a la carpeta /var/www/html donde se encuentran los archivos web de Apache:

![image-38](images/image-38.png)

**▸** Descarga la última versión de Ampache desde su sitio oficial:

![image-39](images/image-39.png)

![image-40](images/image-40.png)

**▸** Extraer el archivo: descomprime el archivo que descargaste:

![image-41](images/image-41.png)

Cambiar los permisos de la carpeta Ampache:

![image-42](images/image-42.png)

**▸** Configurar Apache para Ampache: crea un archivo de configuración para Ampache:

![image-43](images/image-43.png)

![Agrega lo siguiente:](images/image-44.png)

**▸** Guarda el archivo («Ctrl + O» para guardar y «Ctrl + X» para salir).

**▸** Habilitar el sitio y reiniciar Apache:

![image-45](images/image-45.png)

Configuración de la base de datos:

**▸** Crear una base de datos para Ampache: entra en la consola de MariaDB:

![▸ Crea la base de datos: ▸ Finalizar la instalación desde el navegador:](images/image-46.png)

**•** Abre un navegador web y dirígete a <http://your-server-ip/ampache>.

- Sigue las instrucciones del asistente de instalación de Ampache. Durante la instalación, tendrás que introducir los datos de la base de datos que creaste anteriormente (nombre de base de datos, usuario y contraseña).

#### Instalación de Ampache en Windows

Ampache está diseñado, principalmente, para entornos basados en Linux, pero se puede ejecutar en Windows utilizando XAMPP, que incluye Apache, MySQL (MariaDB), y PHP.

Instalar XAMPP:

**▸** Descargar XAMPP: ve al sitio oficial de XAMPP:

<https://www.apachefriends.org/index.html> y descarga la versión para Windows.

**▸** Instalar XAMPP: durante la instalación, asegúrate de seleccionar Apache, MySQL, y PHP. Una vez que la instalación haya terminado, abre el panel de control de XAMPP y arranca los módulos de Apache y MySQL.

Configurar la base de datos en XAMPP: **▸** Acceder a phpMyAdmin: abre tu navegador y dirígete a <http://localhost/phpmyadmin>. **▸** Crear una base de datos para Ampache: en la página de phpMyAdmin, haz clic en «Base de datos» y crea una nueva base de datos llamada ampache. Después, crea un usuario y otórgale todos los privilegios sobre la base de datos ampache.

Descargar e instalar Ampache: **▸** Descargar Ampache: descarga Ampache desde <https://ampache.org/download>. **▸** Descomprimir Ampache: extrae el archivo descargado y cópialo en el directorio de tu servidor web de XAMPP (usualmente C:\xampp\htdocs\ampache ). **▸** Cambiar los permisos: asegúrate de que Apache tenga acceso completo al directorio de Ampache. Cambia los permisos del archivo si es necesario. Configurar Apache para Ampache: **▸** Configurar el archivo de Apache: abre el archivo de configuración de Apache (

httpd.conf ) ubicado en C:\xampp\apache\conf\httpd.conf . Asegúrate de que el módulo

mod_rewrite esté habilitado. Busca esta línea y descoméntala si está comentada:

![image-47](images/image-47.png)

**▸** Reiniciar Apache: reinicia Apache desde el Panel de Control de XAMPP.

Completar la instalación:

**▸** Abre tu navegador y dirígete a <http://localhost/ampache>.

**▸** Sigue las instrucciones del asistente de instalación de Ampache e introduce los datos de la base de datos que creaste anteriormente.

Configuración de medios:

Deberemos cargar, organizar y gestionar archivos de audio y vídeo en Ampache utilizando la interfaz web. Aquí están los pasos detallados:

#### Parte 1. Carga de archivos de audio y vídeo en Ampache

**▸** Acceder a la Interfaz Web de Ampache:

- Abrir el navegador web y navegar a la dirección de tu instalación de Ampache. La URL dependerá de tu configuración: si Ampache está instalado en tu máquina local, ve a <http://localhost/ampache>, si Ampache está en un servidor remoto, usa la IP o nombre de dominio del servidor: <http://your-server-ip/ampache>.

- Iniciar sesión con el nombre de usuario y contraseña que creaste durante la instalación.

**▸** Cargar archivos multimedia:

- Ir a la sección de administración: una vez dentro de la interfaz de Ampache, ve a la pestaña de administración (normalmente en la parte superior derecha del panel de control).

- Añadir archivos a la biblioteca: ve a «Catálogo» → «Añadir catálogo». Aquí podrás elegir la ubicación donde se almacenan los archivos multimedia. Ampache escaneará la carpeta seleccionada en busca de archivos de audio y vídeo para añadir a la biblioteca.

Nota: para que Ampache pueda acceder a los archivos, asegúrate de que estos estén en una carpeta que Ampache pueda leer. Los archivos deben estar en el servidor, ya que Ampache no admite la carga directa desde la interfaz web.

Escanear para añadir medios:

**▸** Después de seleccionar la carpeta donde están los archivos multimedia, haz clic en «Añadir catálogo». Ampache escaneará la carpeta y añadirá los archivos a la biblioteca.

#### Parte 2. Organización de la biblioteca

Exploración y organización de los medios:

**▸** Explorar la biblioteca:

- En el panel izquierdo, encontrarás opciones para explorar los archivos por artistas, álbumes, vídeos, géneros, etc.

- Usa estas opciones para navegar por la biblioteca multimedia que acabas de cargar.

**▸** Crear listas de reproducción:

- Desde la interfaz de Ampache, puedes organizar tu biblioteca creando listas de reproducción personalizadas.

- Ve a Playlists y selecciona Create Playlist para crear una nueva lista de reproducción.

- Asigna un nombre a la lista y luego agrega archivos seleccionados de tu biblioteca.

**▸** Editar Metadata (etiquetas):

- Haz clic en un archivo individual en la biblioteca y selecciona «Editar metadatos». Aquí puedes modificar información como el título, artista, álbum, género y otros detalles.

- Esto te permitirá tener una biblioteca organizada y limpia.

Filtros y búsquedas:

**▸** Filtrar archivos:

- Puedes utilizar la barra de búsqueda para filtrar archivos por nombre, género, artista, álbum, etc.

- Esto es útil cuando tienes una gran cantidad de archivos y necesitas encontrar algo específico.

**▸** Etiquetas personalizadas:

- Ampache permite agregar etiquetas personalizadas a archivos multimedia, lo que te permite organizar y clasificar tus archivos de una manera más específica.

#### Parte 3. Gestión de medios en grupo

**▸** Asignación de permisos a usuarios:

- Si Ampache tiene varios usuarios, el administrador puede crear usuarios adicionales y asignarles diferentes permisos (como acceso a ciertos archivos o capacidad para editar la biblioteca).

**▸** Acceso remoto:

- Si tienes varios participantes o usuarios, Ampache permite que se conecten de manera remota a través de su interfaz web desde diferentes dispositivos y ubicaciones, siempre y cuando tengan los permisos adecuados.

#### Transmisión de medios

Vamos a ver como reproducir medios directamente desde la interfaz de Ampache, así como a utilizar aplicaciones externas como VLC para streaming local y remoto.

#### Parte 1. Reproducir medios directamente desde la interfaz de Ampache

Reproducción de medios desde la interfaz Web:

**▸** Acceder a Ampache:

- Abre tu navegador y dirígete a la URL de tu instalación de Ampache: <http://localhost/ampache> (si está en tu máquina local) o <http://your-serverip/ampache> (si está en un servidor remoto).

- Inicia sesión con tus credenciales.

**▸** Navegar en la biblioteca:

- Usa las opciones del panel lateral para buscar música o vídeos por artistas, álbumes, canciones, vídeos o géneros.

**▸** Seleccionar y reproducir archivos:

- Haz clic en cualquier archivo multimedia que quieras reproducir. Verás que se abre un reproductor en la parte inferior de la página.

- El reproductor integrado de Ampache permite la reproducción de los archivos seleccionados directamente desde el navegador.

- Puedes hacer clic en «Play», «Pausa» y avanzar como lo harías en cualquier reproductor.

**▸** Crear una lista de reproducción:

- Puedes agregar varios archivos a una lista de reproducción.

- Marca las canciones o vídeos que deseas incluir, selecciona «Add to Playlist» y elige una lista existente o crea una nueva.

Reproducir en aplicaciones externas como VLC:

**▸** Obtener la URL del archivo:

- Para reproducir un archivo en un reproductor externo como VLC, Ampache te permite obtener el enlace directo de *streaming.*

- Haz clic derecho sobre el archivo que quieres reproducir y selecciona Transmitir URL o Download. Copia la URL proporcionada.

**▸** Abrir en VLC:

- Abre VLC Media Player.

- Ve a «Medios» → «Abrir red» y pega la URL del archivo.

- Haz clic en «Reproducir» y VLC comenzará a transmitir el archivo desde el servidor de Ampache.

#### Parte 2. Streaming remoto

Ampache, también, permite transmitir música y vídeo a otros dispositivos que tengan acceso a su servidor. Aquí los usuarios podrán ver cómo reproducir medios remotamente desde cualquier dispositivo con acceso a Internet.

Acceder remotamente a Ampache:

**▸** Acceder desde otro dispositivo:

- Si tienes un servidor Ampache accesible externamente (con una IP pública o dominio), puedes conectarte desde cualquier dispositivo, como un teléfono, tableta o laptop.

**•** Abre el navegador en el dispositivo externo y dirígete a <http://your-serverip/ampache> o el nombre de dominio configurado.

**▸** Iniciar sesión:

- Usa las mismas credenciales que en tu servidor local para iniciar sesión.

**▸** Reproducir medios:

- Ahora podrás acceder a toda la biblioteca multimedia cargada en el servidor desde cualquier lugar. Al igual que en la interfaz web local, selecciona un archivo y reprodúcelo directamente desde el navegador en el dispositivo externo.

Usar aplicaciones externas para *streaming* remoto:

**▸** *Streaming* en aplicaciones externas (VLC, Kodi, etc.):

- Además del reproductor integrado, Ampache permite el uso de aplicaciones externas para el *streaming* remoto.

- Al igual que con VLC en la Parte 1 , puedes copiar la URL de un archivo y pegarla en cualquier aplicación de reproducción multimedia compatible con URL remotas.

**▸** Ampache compatible con clientes externos:

- Ampache, también, es compatible con aplicaciones como Subsonic, Kodi, y otras plataformas de *streaming* multimedia. Esto te permite acceder y reproducir la biblioteca desde diferentes dispositivos conectados a tu red local o a Internet.

Compartir listas de reproducción:

**▸** Compartir medios:

- Los usuarios pueden compartir listas de reproducción con otros usuarios de Ampache, siempre que tengan los permisos adecuados.

- Esto permite que múltiples usuarios disfruten de la misma biblioteca multimedia sin necesidad de duplicar los archivos.

#### Implementación de un reproductor HLS en la Web

Uso de HLS (HTTP *Live Streaming):* Para implementar *streaming* con HLS en una plataforma web, debes generar listas de reproducción M3U8 y segmentos de medios.

Generación de listas M3U8:

Comando FFmpeg.

![image-48](images/image-48.png)

![image-49](images/image-49.png)

Descripción: este comando crea una lista de reproducción playlist.m3u8 y segmentos

de video segment_%03d.ts , que son utilizados para el streaming HLS. Reproducción de HLS:

**▸** Con VLC Media Player:

- Abrir «VLC» → «Medios» → «Abrir red» → Introduce la URL de la lista M3U8 (por ejemplo, <http://your-server/playlist.m3u8>).

**▸** Con reproductor HLS en la web:

- Puedes integrar un reproductor HLS en tu sitio web utilizando JavaScript. Un reproductor popular para esto es hls.js , una biblioteca que permite reproducir flujos HLS en navegadores que soportan HTML5.

Ejemplo de integración con hls.js :

![image-50](images/image-50.png)

Descripción: este código HTML incluye el reproductor HLS en una página web. hls.js se encarga de manejar la reproducción del flujo HLS en el navegador. **▸** Cambiar la URL del Flujo HLS:

**•** Reemplaza la línea hls.loadSource('<http://your-server/playlist.m3u8>') ; por la URL de tu

propio flujo HLS, que debería haberse creado previamente con FFmpeg.

**•** Ejemplo: hls.loadSource ('<http://localhost/stream/playlist.m3u8>')

Verificar el funcionamiento del reproductor:

**▸** Guardar el archivo HTML:

- Asegúrate de guardar el archivo HTML con las modificaciones.

**▸** Abrir la página en un navegador:

- Abre el archivo hls_player.html en tu navegador (puedes hacerlo arrastrando el archivo al navegador o usando «Archivo» → «Abrir archivo»).

**▸** Reproducción del vídeo:

- Si la URL del flujo HLS es correcta y hls.js está funcionando, deberías ver un vídeo cargado en la página web.

- El reproductor debe comenzar a reproducir automáticamente si la conexión al flujo HLS es exitosa.

**▸** Verificación: si el flujo HLS no comienza a reproducirse automáticamente, asegúrate de que:

- El servidor HLS esté en funcionamiento.

- La URL del flujo playlist.m3u8 sea accesible desde el navegador.

- No haya bloqueos de seguridad o restricciones de red.

Consideraciones para navegadores:

**▸** Compatibilidad del navegador:

- El reproductor HLS funciona mejor en navegadores como Google Chrome y Firefox que no tienen soporte nativo para HLS. Estos navegadores utilizan la biblioteca hls.js para manejar la reproducción.

- En navegadores como Safari (macOS/iOS), que soportan HLS de manera nativa, el código utiliza la fuente directamente sin hls.js .

**▸** Pruebas en diferentes navegadores:

- Recomendamos que los participantes prueben la página en varios navegadores para ver cómo se comporta la reproducción HLS.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–39)*
- A fondo  *(pp.40–42)*
- Entrenamientos  *(pp.43–87)*
- Servicios en Red e Internet 5 Tema 8. Material de estudio · Servicios en Red e Internet 6 Tema 8. Material de estudio · Servicios en Red e Internet 7 Tema 8. Material de estudio · Servicios en Red e Internet 8 Tema 8. Material de estudio · Servicios en Red e Internet 10 Tema 8. Material de estudio · Servicios en Red e Internet 11 Tema 8. Material de estudio · Servicios en Red e Internet 12 Tema 8. Material de estudio · Servicios en Red e Internet 14 Tema 8. Material de estudio · Servicios en Red e Internet 16 Tema 8. Material de estudio · Servicios en Red e Internet 17 Tema 8. Material de estudio · Servicios en Red e Internet 18 Tema 8. Material de estudio · Servicios en Red e Internet 19 Tema 8. Material de estudio · Servicios en Red e Internet 20 Tema 8. Material de estudio · Servicios en Red e Internet 21 Tema 8. Material de estudio · Servicios en Red e Internet 22 Tema 8. Material de estudio · Servicios en Red e Internet 23 Tema 8. Material de estudio · Servicios en Red e Internet 24 Tema 8. Material de estudio · Servicios en Red e Internet 25 Tema 8. Material de estudio · Servicios en Red e Internet 26 Tema 8. Material de estudio · Servicios en Red e Internet 27 Tema 8. Material de estudio · Servicios en Red e Internet 28 Tema 8. Material de estudio · Servicios en Red e Internet 29 Tema 8. Material de estudio · Servicios en Red e Internet 30 Tema 8. Material de estudio · Servicios en Red e Internet 31 Tema 8. Material de estudio · Servicios en Red e Internet 32 Tema 8. Material de estudio · Servicios en Red e Internet 33 Tema 8. Material de estudio · Servicios en Red e Internet 34 Tema 8. Material de estudio · Servicios en Red e Internet 35 Tema 8. Material de estudio · Servicios en Red e Internet 37 Tema 8. Material de estudio · Servicios en Red e Internet 38 Tema 8. Material de estudio · Servicios en Red e Internet 39 Tema 8. Material de estudio  *(pp.5, 6, 7, 8, 10, 11, 12, 14, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 37, 38, 39)*
- Servicios en Red e Internet 43 Tema 8. Entrenamientos · Servicios en Red e Internet 44 Tema 8. Entrenamientos · Servicios en Red e Internet 45 Tema 8. Entrenamientos · Servicios en Red e Internet 46 Tema 8. Entrenamientos · Servicios en Red e Internet 47 Tema 8. Entrenamientos · Servicios en Red e Internet 49 Tema 8. Entrenamientos · Servicios en Red e Internet 50 Tema 8. Entrenamientos · Servicios en Red e Internet 51 Tema 8. Entrenamientos · Servicios en Red e Internet 52 Tema 8. Entrenamientos · Servicios en Red e Internet 53 Tema 8. Entrenamientos · Servicios en Red e Internet 54 Tema 8. Entrenamientos · Servicios en Red e Internet 55 Tema 8. Entrenamientos · Servicios en Red e Internet 56 Tema 8. Entrenamientos · Servicios en Red e Internet 57 Tema 8. Entrenamientos · Servicios en Red e Internet 58 Tema 8. Entrenamientos · Servicios en Red e Internet 59 Tema 8. Entrenamientos · Servicios en Red e Internet 60 Tema 8. Entrenamientos · Servicios en Red e Internet 61 Tema 8. Entrenamientos · Servicios en Red e Internet 62 Tema 8. Entrenamientos · Servicios en Red e Internet 63 Tema 8. Entrenamientos · Servicios en Red e Internet 64 Tema 8. Entrenamientos · Servicios en Red e Internet 65 Tema 8. Entrenamientos · Servicios en Red e Internet 66 Tema 8. Entrenamientos · Servicios en Red e Internet 67 Tema 8. Entrenamientos · Servicios en Red e Internet 68 Tema 8. Entrenamientos · Servicios en Red e Internet 69 Tema 8. Entrenamientos · Servicios en Red e Internet 70 Tema 8. Entrenamientos · Servicios en Red e Internet 71 Tema 8. Entrenamientos · Servicios en Red e Internet 72 Tema 8. Entrenamientos · Servicios en Red e Internet 73 Tema 8. Entrenamientos · Servicios en Red e Internet 74 Tema 8. Entrenamientos · Servicios en Red e Internet 75 Tema 8. Entrenamientos · Servicios en Red e Internet 76 Tema 8. Entrenamientos · Servicios en Red e Internet 77 Tema 8. Entrenamientos · Servicios en Red e Internet 78 Tema 8. Entrenamientos · Servicios en Red e Internet 79 Tema 8. Entrenamientos · Servicios en Red e Internet 80 Tema 8. Entrenamientos · Servicios en Red e Internet 81 Tema 8. Entrenamientos · Servicios en Red e Internet 82 Tema 8. Entrenamientos · Servicios en Red e Internet 83 Tema 8. Entrenamientos · Servicios en Red e Internet 84 Tema 8. Entrenamientos · Servicios en Red e Internet 85 Tema 8. Entrenamientos · Servicios en Red e Internet 86 Tema 8. Entrenamientos · Servicios en Red e Internet 87 Tema 8. Entrenamientos  *(pp.43, 44, 45, 46, 47, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87)*