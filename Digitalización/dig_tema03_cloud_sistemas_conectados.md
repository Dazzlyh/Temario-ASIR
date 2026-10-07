# Tema 3. Cloud y sistemas conectados

*Digitalización aplicada a los Sectores Productivos (GS)*

## Índice

- Esquema
- Material de estudio
  - 3.1. Introducción y objetivos
  - 3.2. Cloud: definición, niveles y posibilidad de trabajo en la nube
  - 3.3. Edge, fog y mist computing
  - 3.4. Ventajas y rentabilidad para la empresa por el uso de los recursos de la cloud
  - 3.5. Referencias bibliográficas
- A fondo
  - Tipos de cloud computing
  - Beneficios de la cloud computing
- Entrenamientos (1 a 5)

---

## Esquema

*(Esquema original en imagen; transcrito.)*

**Cloud y sistemas conectados**

- **Cloud (nube):** definición y características; tipos de cloud.
- **Edge / Fog / Mist:** diferencias y límites entre las tres y cloud.
- **Ventajas y rentabilidad:** sostenibilidad; oportunidad de negocio; seguridad y TIC; operativas; innovación y aprendizaje continuo; económicas.

---

## 3.1. Introducción y objetivos

El *cloud computing* o informática en la nube ha adquirido un papel protagonista en el panorama actual de las nuevas tecnologías y el mundo empresarial. No se puede perder de vista que es una pieza clave en la transformación digital de las empresas, porque permite almacenar, procesar y acceder a datos y servicios desde cualquier lugar, sin una infraestructura compleja. Esto aporta agilidad, ahorro de costes, escalabilidad y gran capacidad de adaptación a los cambios del mercado.

> Gracias a la nube, pequeñas y medianas empresas pueden acceder a tecnologías avanzadas que antes solo estaban en manos de grandes organizaciones.

Su potencial futuro va mucho más allá: el cloud será esencial para el despliegue generalizado de tecnologías habilitadoras como gemelos digitales, procesamiento masivo de datos, cobots o sistemas inmersivos. En definitiva, no es solo una herramienta de almacenamiento remoto, es el motor invisible que conecta procesos, personas y tecnologías.

Al finalizar este tema serás capaz de:

- Comprender qué es el *cloud computing*.
- Identificar ventajas y riesgos del uso de la nube.
- Reconocer ejemplos concretos de aplicación del cloud y sistemas conectados.
- Valorar la importancia de la conectividad, la seguridad y la disponibilidad en entornos digitales en la nube.
- Relacionar el uso del cloud con otras tecnologías habilitadoras.

---

## 3.2. Cloud: definición, niveles y posibilidad de trabajo en la nube

De forma adaptada y traducida, una de las definiciones más ampliamente usadas del *cloud computing* es la que aporta el NIST SP 800-145:

> «Cloud computing es un modelo para permitir el acceso ubicuo, conveniente y bajo demanda a través de la red a un conjunto compartido de recursos informáticos configurables (por ejemplo, redes, servidores, almacenamiento, aplicaciones y servicios), que pueden ser rápidamente aprovisionados y liberados con un mínimo esfuerzo de gestión o interacción con el proveedor del servicio» (Mell y Grance, 2011).

De la mano del National Institute of Standards and Technology (NIST), se puede detallar que las principales características del *cloud computing* son cinco:

- **Autoservicio bajo demanda** (*on-demand self service*): los usuarios pueden acceder automáticamente sin intervención del proveedor.
- **Acceso amplio a la red** (*broad network access*): los recursos cloud están disponibles a través de redes estándar y pueden ser utilizados desde diferentes dispositivos.
- **Agrupamiento de recursos** (*resource pooling*): los recursos se comparten entre múltiples clientes, cada uno accede a lo que necesita.
- **Elasticidad rápida** (*rapid elasticity*): la capacidad de recursos se puede escalar automáticamente o bajo demanda.
- **Servicio medido** (*measured service*): el uso de los recursos se monitorea, controla y registra de forma transparente.

**Figura 1. Características *cloud computing*.** Fuente: elaboración propia. *(Infografía "Computación en la nube. Cinco características esenciales"; transcrita.)*

| Característica | Descripción en la figura |
|---|---|
| Autoservicio bajo demanda | Los recursos se aprovisionan automáticamente sin intervención humana. |
| Acceso amplio a la red | Acceso a los recursos desde cualquier lugar a través de la red. |
| Agrupamiento de recursos | Los recursos informáticos se comparten entre múltiples usuarios. |
| Elasticidad rápida | Los recursos se pueden escalar rápidamente, hacia arriba y hacia abajo. |
| Servicio medido | El uso de los recursos se monitoriza y se controla. |

Para seguir ampliando el aprendizaje en *cloud*, se distinguen los distintos tipos de *cloud computing* existentes en el mercado:

- **Nube pública** (*public cloud*): los recursos son proporcionados por un proveedor externo y compartidos entre múltiples clientes.
  - Ventajas: bajo coste inicial, alta escalabilidad, fácil acceso.
  - Desventajas: menor control sobre datos e infraestructura.
- **Nube privada** (*private cloud*): la infraestructura *cloud* es de uso exclusivo de una única organización. Puede estar alojada en sus propias instalaciones o ser gestionada por un tercero.
  - Ventajas: mayor control, seguridad personalizada, cumplimiento normativo.
  - Desventajas: mayor coste y mantenimiento complejo.
  - Uso típico: hospitales y bancos.
- **Nube híbrida** (*hybrid cloud*): combina nube pública y privada, lo que permite mover datos y aplicaciones entre ambas según convenga.
  - Ventajas: equilibrio entre seguridad y flexibilidad, optimización de costes.
  - Desventajas: complejidad de integración y gestión.
  - Uso típico: empresas que precisan de privacidad en procesos críticos y a la vez aprovechar servicios públicos en otras funciones.
- **Nube de comunidad** (*community cloud*): modelo compartido por varias organizaciones que tienen intereses, necesidades o normativas comunes.
  - Ventajas: coste compartido, mayor control que la nube pública, facilita la colaboración y la personalización sectorial.
  - Desventajas: coste superior a la pública, escalabilidad limitada, dependencia entre organizaciones.
  - Uso típico: sanidad pública (varios hospitales que comparten servicio), universidades o centros de educación, incluso organismos regionales que comparten servicios digitales ciudadanos.

> En la sección A fondo hay un vídeo que ilustra los principales tipos de *cloud computing*.

> Nota: la página 5 del PDF original está en blanco.

---

## 3.3. Edge, fog y mist computing

A medida que las organizaciones generan más datos, no siempre es práctico enviar todo a la nube central. Por ello, han surgido modelos como *edge*, *fog* y *mist computing*, que permiten procesar los datos cerca del lugar donde se originan con mayor rapidez y menor saturación de red:

- **Edge computing:** procesa los datos directamente en el dispositivo o sistema cercano al origen. De esta forma reduce la latencia (ofrece respuesta más rápida), evita la saturación de la red con información innecesaria y mejora la seguridad manteniendo parte de los datos localmente.
- **Fog computing:** es un intermediario entre la nube y los dispositivos, se utiliza cuando el procesamiento requiere más capacidad de la que tiene un sensor, pero se quiere evitar depender de la nube. De esta forma sirve para procesar y filtrar datos cerca de donde se generan, conectar varios dispositivos a una red local inteligente y ofrecer agilidad, pero con mayor potencia que un dispositivo *edge*.
- **Mist computing:** es un modelo computacional que extiende el *edge* hasta el nivel más bajo de la red, permitiendo que sensores o microdispositivos realicen procesamiento mínimo, control autónomo y decisiones locales, incluso cuando no hay conexión con la red superior.

### Ejemplo

Imagina una casa con sensores, luces automáticas, cámaras y una central domótica:

- **Mist computing:** el sensor reacciona. Es como si el detector de humo en la cocina activara la alarma él solo, sin esperar a que nadie le diga nada. Solo hace tareas simples pero muy rápidas.
- **Edge computing:** el aparato decide. Es como si la cámara de seguridad revisara las imágenes y solo avisara si ve algo raro. Procesa más que el sensor, pero sigue en el lugar donde ocurre.
- **Fog computing:** ordenador que coordina. Es como si un miniordenador en el salón recogiera los datos de los sensores y los resumiera para que el sistema central lo entienda mejor.
- **Cloud computing:** la central inteligente que guarda y conecta. Es como si toda la información de la casa se mandara a una nube en Internet donde puedes verla desde tu móvil, guardar todo o conectar con otros servicios como Alexa o Google Home.

> **Del sensor a la nube:** *mist* actúa, *edge* analiza, *fog* coordina y *cloud* conecta y almacena.

---

## 3.4. Ventajas y rentabilidad para la empresa por el uso de los recursos de la cloud

*Cloud computing* es, sin duda, un instrumento acelerador para una empresa, para que esta logre evolucionar. Su uso permite utilizar software, almacenamiento y servicio sin necesidad de tener costosos servidores.

Partiendo de este lugar, se describen, dentro de una clasificación que facilita la comprensión de todas ellas, las ventajas principales que el uso de la nube ofrece en las organizaciones:

### Innovación y aprendizaje continuo

¿Qué aporta la cloud en términos de cultura digital y mejora continua?

- Acceso a tecnologías emergentes (IA, BBDD o plataformas *e-learning*).
- Fomenta la digitalización progresiva: permite ir transformando los procesos de la empresa paso a paso, sin asumir grandes riesgos iniciales.
- Promueve una cultura de mejora continua: los entornos cloud suelen incluir funcionalidades para medir rendimiento, probar soluciones o mejorar procesos.
- Facilita la formación y actualización del personal: muchas soluciones cloud tienen entornos de formación integrados, tutoriales y soporte en línea.

### Sostenibilidad

¿Cómo ayuda al medio ambiente y a una empresa responsable?

- Reduce consumo energético: los grandes centros de datos son más eficientes que tener muchos servidores pequeños dispersos.
- Minimiza residuos electrónicos: se usan menos equipos físicos y duran más tiempo.
- Facilita el teletrabajo y la formación en línea: se reduce la huella de carbono al reducir desplazamientos.
- Fomenta el uso compartido y responsable de recursos: muchas empresas usan recursos bajo demanda, evitando el desperdicio.

### Oportunidad de negocio

¿Qué nuevas posibilidades abre el uso de la nube?

- Lanzar nuevos servicios digitales rápidamente: una tienda puede abrir un *e-commerce* en días o un centro educativo puede crear su campus virtual.
- Conexión con otras soluciones digitales: los sistemas cloud se integran fácilmente con ERP, CRM, etc.
- Mayor agilidad comercial y organizativa: una empresa puede adaptarse más rápido a los cambios del mercado, sin depender de largos procesos de instalación.
- Analítica de datos integrada: muchas soluciones cloud ofrecen *dashboards* para analizar ventas, rendimiento, interacciones, etc.

### Seguridad y TIC (tecnologías de la información y la comunicación)

¿Qué garantías ofrece el cloud?

- Copias de seguridad automáticas y programadas: los datos no se pierden en caso de fallo del equipo o robo del dispositivo.
- Protección avanzada frente a ciberataques: los grandes proveedores (Google, AWS, Microsoft) tienen sistemas mucho más robustos que la mayoría de las pequeñas empresas.
- Recuperación ante desastres (*disaster recovery*): si ocurre una pérdida la información puede recuperarse desde la nube en cuestión de minutos u horas.
- Control de accesos: se pueden definir usuarios con distintos permisos, registrar actividad y evitar filtraciones accidentales.

### Operativas

¿Cómo mejora el día a día de trabajo?

- Accesibilidad total: se puede acceder a documentos, plataformas o datos desde cualquier lugar, en cualquier momento y con múltiples dispositivos.
- Trabajo colaborativo y sincrónico: varias personas pueden trabajar a la vez el mismo archivo o proyecto, lo que mejora la eficiencia de los equipos distribuidos.
- Escalabilidad inmediata: si una empresa crece o lanza una nueva línea de negocio puede contratar más capacidad de almacenamiento o servicios sin cambiar su infraestructura.
- Mantenimiento invisible: el proveedor se encarga de actualizaciones, parches de seguridad y funcionamiento, lo que evita interrupciones.

### Económicas

¿Por qué es rentable para la empresa?

- Reducción de inversiones iniciales: no hace falta comprar servidores, equipos caros ni instalaciones físicas. Solo se paga por el servicio contratado.
- Modelos de pago flexible: las empresas pueden adaptar su presupuesto a las necesidades o recursos que necesita en cada momento.
- Ahorro en mantenimiento y soporte técnico: muchas tareas que antes hacían informáticos internos ahora las gestiona el proveedor cloud.
- Evita obsolescencia tecnológica: no hay que reemplazar equipos cada pocos años porque el servicio se mantiene actualizado.

### Datos que respaldan la rentabilidad

En definitiva, y apoyando en datos la teoría incorporada, la adopción de soluciones en la nube está demostrando ser una decisión estratégicamente rentable para empresas de todos los tamaños y sectores:

- Según el *Informe del Mercado Cloud en España 2023* (Nogales et al., 2023), el 49,2 % de las compañías españolas prevé aumentar su inversión en la nube en más de un 20 %, motivadas por la necesidad de optimizar costes, mejorar su escalabilidad y responder con mayor agilidad a las exigencias del mercado.
- Un estudio de IBM, citado por el medio especializado ITSitio (2024), revela que el 85 % de las empresas que migraron a la nube lograron reducir sus costes operativos en un 56 %, además de aumentar su agilidad interna en un 57 %, gracias a la automatización, el acceso remoto y la simplificación de infraestructuras.
- Un informe de FTI Communications (2023) sobre el impacto económico de la nube pública en América Latina destaca que esta tecnología puede generar reducciones de costes totales de hasta el 90 %, al tiempo que multiplica por nueve el número de usuarios que una empresa puede atender. Esto evidencia un claro retorno de la inversión y una mejora sustancial de la escalabilidad y productividad.

> Nota: las cifras proceden de informes citados por el propio tema; el informe de FTI está publicado con el logotipo de AWS (según la URL de la referencia) y se centra en América Latina. No se han verificado de forma independiente.

> En la sección A fondo hay un vídeo que, de forma visual, presenta los beneficios de la *cloud computing*.

---

## 3.5. Referencias bibliográficas

Mell, P. y Grance, T. (2011). *NIST SP 800-145. The NIST Definition of Cloud Computing.* National Institute of Standards and Technology (NIST). https://doi.org/10.6028/NIST.SP.800-145

Nogales, J., Martín, E., Gómez, D. y Zamora, M. (2023). *Informe del Mercado Cloud en España 2023.* Eraneos. https://www.eraneos.com/es/wp-content/uploads/sites/5/2023/07/ERANEOS_informe-cloud_2023-OK.pdf

ITSitio. (2024, noviembre 02). *Cómo las empresas redujeron un 56% de costos con almacenamiento en la nube.* https://www.itsitio.com/mx/cloud/costos-con-almacenamiento-en-la-nube/

FTI Communications. (2023). *Impacto económico de la adopción de la nube pública en América Latina.* FTI Communications. https://fticommunications.com/wp-content/uploads/2023/10/Economic-Impact-Espanol_aws-logo.pdf

---

## A fondo

### Tipos de cloud computing

Nominalia. (2021, noviembre 17). *Nube pública, privada e híbrida* [Vídeo]. YouTube. https://www.youtube.com/watch?v=7oHPAxpLkRk

De forma concisa y directa puedes ver las principales tipologías de *cloud computing* en este vídeo.

### Beneficios de la cloud computing

Edutin Academy. (2024, septiembre 05). *Beneficios de Cloud Computing - Curso de Computing* [Vídeo]. YouTube. https://www.youtube.com/watch?v=lYJnf2mAts4

Aprovecha el vídeo para afianzar lo estudiado en el tema sobre las ventajas y beneficios que ofrece la *cloud computing* dentro de las organizaciones.

---

## Entrenamientos

### Entrenamiento 1

**Planteamiento del ejercicio**

Elige tu nube ideal (reto de decisión en grupo).

**Desarrollo paso a paso**

Se presentan diferentes perfiles de empresas. Por grupos, se deben debatir y elegir qué tipo de nube es más adecuada para cada caso y justificarlo ante la clase.

De los siguientes perfiles, tienes que ofrecer la nube que según tu criterio es la ideal:

- Clínica veterinaria rural.
- Centro de formación online con 500 estudiantes.
- Startup de videojuegos en crecimiento.
- Ayuntamiento con bibliotecas, centros y oficinas.
- Asesoría fiscal con clientes empresariales.
- Empresa de transporte logístico internacional.
- Escuela infantil concertada.
- Comercio minorista con tiendas físicas y web.

**Solución** *(tabla en imagen; transcrita)*

| Entidad o empresa | Situación o necesidad | Tipo de nube recomendada | Justificación resumida |
|---|---|---|---|
| Clínica veterinaria rural | Necesita acceso remoto, con protección de datos clínicos sensibles. | Nube privada o híbrida | Por la confidencialidad de los datos sanitarios, pero también por necesidad de movilidad. |
| Centro de formación en línea con 500 estudiantes | Utiliza plataformas LMS, contenido multimedia y requiere colaboración continua. | Nube híbrida | Necesita combinar seguridad (datos personales) y escalabilidad para contenidos en línea. |
| Startup de videojuegos en crecimiento | Escalar servidores globalmente, distribuir juegos por *streaming*. | Nube pública | Alta demanda de escalabilidad y costes bajos en fase inicial. |
| Ayuntamiento con bibliotecas, centros y oficinas | Compartir recursos digitales entre distintas sedes públicas. | Nube de comunidad | Uso conjunto entre entidades con objetivos comunes y necesidad de interoperabilidad. |
| Asesoría fiscal con clientes empresariales | Maneja datos sensibles y documentación tributaria digital. | Nube privada | Necesita máxima confidencialidad y control sobre la información. |
| Empresa de transporte logístico internacional | Requiere acceso a ERP, trazabilidad de rutas y stock en tiempo real desde distintas zonas. | Nube híbrida | Mezcla de movilidad, disponibilidad continua y tratamiento de datos estratégicos. |
| Escuela infantil concertada | Quiere compartir recursos educativos y comunicarse con familias en línea. | Nube de comunidad o híbrida | Necesita seguridad de datos personales y colaboración con otras escuelas o servicios. |
| Comercio minorista con tiendas físicas y web | Quiere sincronizar ventas, inventario y CRM online desde varios puntos de venta. | Nube pública o híbrida | Precisa sincronización y crecimiento flexible sin infraestructura propia. |

### Entrenamiento 2

**Planteamiento del ejercicio**

Identifica conceptos correctos con verdadero o falso y justificar.

**Desarrollo paso a paso**

Identifica y justifica si las siguientes afirmaciones son verdaderas o falsas:

- La nube pública es menos segura por defecto.
- La nube solo es útil en grandes empresas.
- La nube permite trabajar desde cualquier sitio.
- En la nube no se necesita copia de seguridad.
- La nube requiere obligatoriamente conexión a Internet.
- En la nube no se puede almacenar software, solo archivos.
- La nube permite escalar recursos según la demanda de la empresa.
- Migrar a la nube elimina totalmente los riesgos de ciberseguridad.

**Solución**

- La nube pública es menos segura por defecto: **falso**, puede ser muy segura si está bien configurada.
- La nube solo es útil en grandes empresas: **falso**, también pymes la usan para ahorrar costes.
- La nube permite trabajar desde cualquier sitio: **verdadero**.
- En la nube no se necesita copia de seguridad: **falso**, siempre debe haber *backup*, aunque esté automatizado.
- La nube requiere obligatoriamente conexión a Internet: **verdadero**.
- En la nube no se puede almacenar software, solo archivos: **falso**, se pueden ejecutar aplicaciones completas (SaaS) además de almacenar datos.
- La nube permite escalar recursos según la demanda de la empresa: **verdadero**.
- Migrar a la nube elimina totalmente los riesgos de ciberseguridad: **falso**, reduce algunos riesgos, pero no los elimina; sigue siendo necesario proteger accesos, cifrado y *backups*.

### Entrenamiento 3

**Planteamiento del ejercicio**

Reflexiona y representa el concepto de cloud de forma creativa.

**Desarrollo paso a paso**

Cada estudiante debe redactar una frase que sintetice el papel del cloud en el entorno actual. Puede acompañarla de una imagen simbólica o metáfora.

**Solución**

- «Es como tener una oficina invisible y global: trabaja, guarda, comparte y crece desde cualquier lugar, sin tener servidores en la sala».
- «Es una mochila infinita, siempre la llevo, cabe todo y nunca pesa».
- «La nube no es un lugar, es el espacio que te da libertad digital».

### Entrenamiento 4

**Planteamiento del ejercicio**

La nube bajo amenaza.

**Desarrollo paso a paso**

Cada estudiante debe identificar situaciones de riesgo o amenaza posible en entornos cloud. De esta forma, se plantean diferentes situaciones y de manera individual (en foro o clase en directo) tendrán que responder si existe riesgo y, de ser así, qué solución plantearían:

- Un trabajador accede a archivos de la empresa desde un WiFi público sin VPN.
- Una pyme hace copias automáticas diarias de seguridad en la nube.
- La empresa usa siempre la misma contraseña en todos los servicios cloud.
- Se contrata un proveedor de nube sin comprobar su política de datos.
- Se almacena información confidencial sin cifrar en una nube pública.
- El acceso a los archivos cloud está protegido por contraseña de un solo paso.
- Se comparte un documento sensible con enlace público sin caducidad.
- El sistema cloud se configura por defecto sin personalizar niveles de acceso.

**Solución**

- Un trabajador accede a archivos de la empresa desde un WiFi público sin VPN: **sí existe riesgo.** Solución: usar conexión segura y autenticación de doble factor.
- Una pyme hace copias automáticas diarias de seguridad en la nube: **no existe riesgo.**
- La empresa usa siempre la misma contraseña en todos los servicios cloud: **sí existe riesgo.** Solución: uso de gestores de contraseñas y claves únicas.
- Se contrata un proveedor de nube sin comprobar su política de datos: **sí existe riesgo.** Solución: revisar cumplimiento de la normativa RGPD.
- Se almacena información confidencial sin cifrar en una nube pública: **sí existe riesgo.** Solución: implementar cifrado de datos en tránsito y en reposo.
- El acceso a los archivos cloud está protegido por contraseña de un solo paso: **sí existe riesgo.** Solución: activar autenticación en dos pasos.
- Se comparte un documento sensible con enlace público sin caducidad: **sí existe riesgo.** Solución: limitar acceso por usuario, caducidad de enlace y control de permisos.
- El sistema cloud se configura por defecto sin personalizar niveles de acceso: **sí existe riesgo.** Solución: configurar roles y permisos por perfiles con el principio de mínimo privilegio.

### Entrenamiento 5

**Planteamiento del ejercicio**

Antes y después.

**Desarrollo paso a paso**

Cada estudiante debe analizar los siguientes elementos antes (sin nube) y después de incorporar la nube a la empresa:

- Gestión documental.
- Trabajo en equipo.
- Coste de mantenimiento.
- Accesibilidad.
- Escalabilidad.
- Seguridad.
- Sostenibilidad.

**Solución** *(tabla en imagen; transcrita)*

| Elemento | Antes del *cloud* | Después del *cloud* |
|---|---|---|
| Gestión documental | Archivos físicos, almacenamiento local, duplicación de versiones. | Archivos centralizados, acceso simultáneo, versiones controladas y almacenadas en la nube. |
| Trabajo en equipo | Envío de documentos por e-mail, trabajo secuencial, riesgo de errores por versiones. | Trabajo colaborativo en tiempo real (Docs, Drive, Teams, etc.), comentarios simultáneos, flujo unificado. |
| Coste de mantenimiento | Servidores propios, licencias de software, actualizaciones manuales. | Pago por uso, sin inversión en hardware, actualizaciones automáticas. |
| Accesibilidad | Solo disponible en oficina o mediante conexión a red interna. | Acceso remoto 24/7 desde cualquier dispositivo con conexión a Internet. |
| Escalabilidad | Costosa y lenta: más equipos, licencias, espacio físico. | Escalado automático de recursos según demanda: rápido, flexible y sin interrupciones. |
| Seguridad | Dependencia de protocolos internos y copias físicas. | Seguridad avanzada (cifrado, doble factor, *backups* automáticos, control de accesos). |
| Sostenibilidad | Alto consumo energético, infraestructuras locales activas permanentemente. | Reducción del consumo energético, menor huella de carbono y externalización eficiente de recursos. |
