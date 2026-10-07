## Tema 9

# Seguridad y Alta Disponibilidad

# Tema 9. Configuraciones de

# alta disponibilidad

# Índice

Esquema Material de estudio

## 9.1. Introducción y objetivos

## 9.2. Redundant array of independent disks (RAID)

## 9.3. Storage area network (SAN)

## 9.4. Network attached storage (NAS)

## 9.5. Virtualización

## 9.6. Clúster

## 9.7. Referencias bibliográficas

A fondo Servidor en clúster Tipos de RAID para servidores NAS: conócelos todos y sus características ¿Existen riesgos al usar una nube privada? Sí, estos son los peores Por qué no deberías guardar todos tus datos en un servidor NAS Tipos de RAID. En qué se diferencian y cuáles son los mejores Servidores NAS: todo lo que necesitas saber NAS vs. SAN explicación Entrenamientos Entrenamiento 1: configuración de RAID 0 en Windows 10 con VirtualBox

Entrenamiento 2: configuración de RAID 1 en Windows 10 con VirtualBox Entrenamiento 3: configuración de RAID 5 en Windows 10 con VirtualBox Entrenamiento 4: implantación de configuración RAID 1, 3 y 5 en Ubuntu Entrenamiento 5: configuración de un clúster de servidores Test

# Esquema

![image-1](images/image-1.png)

Seguridad y Alta Disponibilidad 4 Tema 9. Esquema

# 9.1. Introducción y objetivos

La alta disponibilidad en los sistemas informáticos es esencial para asegurar que los datos y los servicios estén **siempre accesibles,** incluso ante fallos o mantenimientos.

La alta disponibilidad es crítica en entornos en los que el tiempo de inactividad puede resultar en pérdidas económicas significativas, daño a la reputación y otros impactos adversos. Esto implica la implementación de medidas y tecnologías que minimicen el tiempo de inactividad y aseguren que los recursos críticos estén siempre disponibles. Algunas estrategias comunes para lograr alta disponibilidad en seguridad informática incluyen la **redundancia de** ***hardware*** **y** ***software*** (utilizar múltiples servidores, dispositivos de red y componentes de seguridad para asegurar que, si uno falla, otro pueda tomar su lugar sin interrumpir el servicio) y el **balanceo de carga** (distribuir el tráfico de red entre múltiples servidores para evitar la congestión y asegurar un rendimiento óptimo).

Esta unidad explora diversas tecnologías que garantizan dicha disponibilidad, las cuales incluyen *redundant array of independent disks* (RAID), *storage area network* (SAN), *network attached storage* (NAS) y virtualización.

**▸ RAID:** mejora el rendimiento y la redundancia al distribuir los datos en varios discos duros.

**▸ SAN:** conecta los servidores con el almacenamiento mediante una red de alta velocidad, lo que optimiza el rendimiento y la centralización de datos.

**▸ NAS:** permite el almacenamiento y la recuperación de datos a través de una red, lo que facilita el acceso remoto y la centralización.

**▸ Virtualización:** crea versiones virtuales de los recursos informáticos, lo cual mejora la eficiencia, la flexibilidad y la gestión de recursos. **▸ Clúster:** conjunto de computadoras interconectadas que trabajan juntas, lo que mejora el rendimiento, la disponibilidad y la capacidad de manejo de cargas de trabajo.

Estas tecnologías, con sus respectivas ventajas y desventajas, son fundamentales para mantener la operatividad continua y fiable de los sistemas informáticos.

Los objetivos que se pretenden alcanzar en este tema son:

**▸** Garantizar la alta disponibilidad.

**▸** Mejorar el rendimiento.

**▸** Aumentar la redundancia y la seguridad de los datos.

**▸** Centralizar y gestionar eficazmente los recursos de almacenamiento.

**▸** Facilitar la recuperación ante desastres y el respaldo de datos.

**▸** Optimizar la utilización de recursos mediante la virtualización.

**▸** Simplificar la gestión y administración de sistemas.

**▸** Garantizar la disponibilidad y la integridad de los datos.

**▸** Comprender la tecnología RAID.

**▸** Identificar los diferentes niveles de RAID.

**▸** Saber lo que es un clúster.

# 9.2. Redundant array of independent disks (RAID)

RAID, que significa conjunto redundante de discos independientes, es un método para **almacenar datos de manera distribuida** en varios discos duros, a los cuales el sistema ve como una sola unidad lógica de almacenamiento. Puede adoptar múltiples configuraciones, conocidas como «niveles RAID», para proporcionar seguridad y redundancia en el almacenamiento de datos.

En un arreglo RAID, los datos se distribuyen y almacenan en tiempo real en varias unidades de disco, con lo que se forma lo que se conoce como un *«array»* o «clúster». El **proceso de distribución** de datos se realiza mediante una técnica llamada *«striping»,* en la cual la información se divide en bloques y se organiza de manera organizada en los diferentes discos del *array.* Estos clústeres pueden ser diseñados para ser tolerantes a fallos, lo que aumenta la fiabilidad y la seguridad de los datos almacenados, además de mejorar la capacidad de lectura y escritura.

Su objetivo es mejorar la redundancia (prevención contra la pérdida de datos) y el rendimiento (velocidad de lectura/escritura) del almacenamiento de datos.

![Figura 1. RAID. Fuente: Informática Sevilla, 2019.](images/image-2.png)

*Figura 1. RAID. Fuente: Informática Sevilla, 2019.*

Aquí tienes algunas ventajas y desventajas generales de la tecnología RAID:

#### Ventajas

**▸ Mejor rendimiento:** al distribuir la carga de trabajo entre varios discos, muchas configuraciones RAID pueden mejorar significativamente el rendimiento de la lectura y la escritura en comparación con una sola unidad de disco.

**▸ Redundancia:** las configuraciones RAID que incluyen espejado (como RAID 1) o paridad (como RAID 5 y RAID 6) pueden proteger los datos contra la pérdida debido a fallas de disco. Esto permite que los sistemas continúen funcionando incluso si una o más unidades fallan.

**▸ Disponibilidad:** al usar RAID, los sistemas pueden mantenerse operativos incluso durante el reemplazo de una unidad defectuosa. Esto minimiza el tiempo de inactividad y reduce el impacto en las operaciones comerciales.

**▸ Escalabilidad:** algunas configuraciones RAID, como RAID 0+1 o RAID 5, permiten agregar o reemplazar unidades fácilmente para aumentar la capacidad de almacenamiento o mejorar el rendimiento.

**▸ Protección de datos:** la redundancia incorporada en algunas configuraciones RAID puede ayudar a proteger contra la corrupción de datos o errores de disco.

#### Desventajas

**▸ Costo:** implementar RAID puede ser costoso, especialmente para configuraciones que requieren múltiples unidades de disco o controladoras RAID dedicadas.

**▸ Complejidad:** la configuración y la gestión de sistemas RAID pueden ser más complejas que la gestión de discos individuales. Esto puede requerir conocimientos técnicos adicionales y tiempo para administrarlos correctamente.

**▸ No es inmune a todas las fallas:** aunque RAID proporciona cierta protección contra fallas de disco, no es una solución infalible. Por ejemplo, un fallo simultáneo de múltiples discos en ciertas configuraciones RAID puede resultar en la pérdida total de datos.

**▸ Rendimiento asimétrico:** algunas configuraciones RAID pueden experimentar un rendimiento asimétrico, especialmente durante las operaciones de escritura intensivas en configuraciones como RAID 5 o RAID 6. Esto se debe al cálculo de la paridad que requiere tiempo de CPU adicional.

**▸ Reconstrucción lenta:** después de una falla de disco, la reconstrucción de los datos puede llevar tiempo, durante el cual el rendimiento del sistema puede verse afectado. Además, la intensidad de la actividad en el disco durante la reconstrucción puede aumentar el riesgo de falla adicional.

En resumen, aunque RAID ofrece muchas ventajas en términos de rendimiento y confiabilidad, también tiene sus desafíos y consideraciones importantes para tener en cuenta al implementarlo.

Implementación de un RAID

Un sistema RAID puede ser implementado de forma **interna o externa** y puede utilizar una implementación **p o r** ***hardware*** **o por** ***software.*** En el caso de la implementación por *hardware,* se utiliza un controlador independiente que se encarga de la gestión del almacenamiento y proporciona interfaces (como SCSI o SATA) para la conexión de los discos en el *array.* Por otro lado, en la implementación por *software,* es el sistema operativo el responsable de controlar el RAID.

El **RAID por** ***hardware*** tiende a ser más rápido y eficiente, ya que el controlador se encarga de las operaciones de RAID sin cargar al procesador principal del sistema. Sin embargo, puede ser más costoso debido al *hardware* adicional requerido. Por otro lado, el **RAID por** ***software*** es más flexible y generalmente más económico, ya que utiliza recursos existentes del sistema, aunque puede ser menos eficiente en términos de rendimiento, especialmente en las cargas de trabajo intensivas.

![Figura 2. RAID por hardware. Fuente: de la Peña Amor, 2015a.](images/image-3.png)

*Figura 2. RAID por hardware. Fuente: de la Peña Amor, 2015a.*

Ambos enfoques tienen sus propias ventajas y consideraciones:

![image-4](images/image-4.png)

![image-5](images/image-5.png)

Tabla 1. Comparativa entre los diferentes tipos de RAID. Fuente: elaboración propia.

Niveles comunes de RAID

Los discos en un clúster RAID se organizan según diferentes configuraciones, conocidas como «niveles RAID». Aquí hay un resumen de los niveles más comunes:

#### RAID 0 (striping)

Divide los datos en bloques y los distribuye entre dos o más discos. Aumenta significativamente el rendimiento, pero no ofrece redundancia. Si un disco falla, todos los datos que están en el *array* se pierden.

![Figura 3. RAID 0. Fuente: de la Peña Amor, 2015b.](images/image-6.png)

*Figura 3. RAID 0. Fuente: de la Peña Amor, 2015b.*

#### RAID 1 (mirroring)

Crea una copia exacta de los datos en dos o más discos. Ofrece una excelente redundancia, ya que los datos están seguros incluso si un disco falla. El rendimiento de la lectura mejora, pero el de la escritura puede ser ligeramente más lento debido al proceso de duplicación.

![Figura 4. RAID 1. Fuente: Bytelearning, 2018a.](images/image-7.png)

*Figura 4. RAID 1. Fuente: Bytelearning, 2018a.*

#### RAID 5 (striping con paridad)

Distribuye los datos y un bloque de paridad entre tres o más discos. Ofrece una buena combinación de rendimiento y redundancia. Si un disco falla, los datos se pueden reconstruir utilizando los bloques de paridad de los discos restantes.

![Figura 5. RAID 5. Fuente: Bytelearning, 2018b.](images/image-8.png)

*Figura 5. RAID 5. Fuente: Bytelearning, 2018b.*

#### RAID 6 (striping con doble paridad)

Es similar a RAID 5, pero con una capa adicional de paridad, lo que le permite sobrevivir al fallo de dos discos. Ofrece una mayor protección de datos a expensas de una menor capacidad de almacenamiento y un rendimiento ligeramente reducido.

![Figura 6. RAID 6. Fuente: Cburnett, 2006.](images/image-9.png)

*Figura 6. RAID 6. Fuente: Cburnett, 2006.*

#### RAID 10 (combinación de RAID 1 y RAID 0)

Combina el *striping* de RAID 0 con el *mirroring* de RAID 1. Ofrece una excelente redundancia y alto rendimiento, pero requiere al menos cuatro discos y solo utiliza el 50 % del almacenamiento total para los datos.

![Figura 7. RAID 6. Fuente: Vinicius, 2014.](images/image-10.png)

*Figura 7. RAID 6. Fuente: Vinicius, 2014.*

#### Implementación y gestión de RAID

**▸** ***Hardware*** **vs.** ***software*** **RAID:** RAID puede implementarse a través de *hardware* (controladoras RAID dedicadas) o *software* (gestión a través del sistema operativo). El RAID de *hardware* generalmente ofrece mejor rendimiento y más características, pero a un costo más elevado.

**▸ Selección del nivel adecuado:** la elección del nivel de RAID depende de los requisitos específicos de rendimiento, redundancia y presupuesto. Por ejemplo, el RAID 5 es común para servidores que requieren un buen equilibrio entre rendimiento y redundancia, mientras que el RAID 10 es preferido para aplicaciones de alta velocidad y seguridad.

**▸ Monitoreo y mantenimiento:** es crucial monitorear regularmente el estado de los discos en un *array* RAID y reemplazar los discos fallidos lo antes posible. La mayoría

Seguridad y Alta Disponibilidad 15 Tema 9. Material de estudio de las soluciones RAID permiten la reconstrucción «en caliente» de los datos en un nuevo disco sin interrumpir las operaciones.

#### Consideraciones adicionales

**▸ Capacidad y costo:** la elección del nivel de RAID impacta en la capacidad total disponible y el costo. Por ejemplo, RAID 1 y RAID 10 requieren más discos para la misma cantidad de almacenamiento utilizable en comparación con RAID 5 o RAID 6.

**▸ Recuperación de datos:** en RAID 1, 5 y 6 los datos se pueden recuperar en caso de un fallo de discos. Sin embargo, la recuperación puede ser compleja y requiere una gestión cuidadosa.

**▸ Uso en conjunto con otras tecnologías:** RAID a menudo se utiliza junto con otras tecnologías de almacenamiento y servidores, como SAN y NAS, para mejorar aún más la disponibilidad y la integridad de los datos.

# 9.3. Storage area network (SAN)

![Figura 8. SAN. Fuente: Gola, 2023.](images/image-11.png)

*Figura 8. SAN. Fuente: Gola, 2023.*

Una SAN es una red de alta velocidad dedicada que conecta los servidores con los recursos de almacenamiento, lo que permite el **acceso a los datos** de manera **centralizada y compartida.** En lugar de conectar los dispositivos de almacenamiento directamente a los servidores, como se haría en un entorno de almacenamiento de área de servidor directo (DAS), un SAN utiliza una arquitectura de red para conectar los dispositivos de almacenamiento a través de una infraestructura de red especializada.

Arquitectura y componentes

Típicamente, una SAN se compone de servidores, *switches* de fibra óptica, matrices de almacenamiento, unidades de cinta, unidades de estado sólido (SSD) y dispositivos de conexión. Estos componentes están interconectados mediante el uso de tecnologías como la fibra óptica (o a veces a través de redes Ethernet de alta

Seguridad y Alta Disponibilidad 17 Tema 9. Material de estudio velocidad) utilizando protocolos como *fibre channel* o *Internet small computer system* *interface* (iSCSI). Esta **separación física** entre los dispositivos de almacenamiento y los servidores permite una **mayor flexibilidad, escalabilidad y gestión** **centralizada** del almacenamiento lo que garantiza un alto rendimiento y una baja latencia.

Ventajas de implementar una SAN

**▸ Alta velocidad y rendimiento:** los SAN utilizan tecnologías de conectividad de alta velocidad, como *fibre channel* o iSCSI, lo que permite tener un acceso rápido a los datos y un rendimiento optimizado para las aplicaciones empresariales exigentes.

**▸ Escalabilidad:** los SAN pueden expandirse fácilmente para satisfacer las crecientes necesidades de almacenamiento de una organización al agregar más dispositivos de almacenamiento o ampliar la infraestructura de red.

**▸ Centralización de recursos:** los SAN permiten la consolidación de los recursos de almacenamiento en un solo lugar, lo que facilita la gestión y el control centralizados de los datos y la capacidad de almacenamiento.

**▸ Alta disponibilidad y tolerancia a fallos:** los SAN suelen incluir características como la redundancia de componentes y los mecanismos de conmutación por error para garantizar la disponibilidad continua de los datos y minimizar el riesgo de pérdida de datos debido a fallos del sistema.

**▸ Flexibilidad:** los SAN admiten una amplia gama de dispositivos de almacenamiento y arquitecturas, lo que le permite a las organizaciones utilizar una combinación de tecnologías de almacenamiento para satisfacer sus necesidades específicas.

**▸ Mejora del Rendimiento:** al separar el tráfico de almacenamiento del tráfico de la red regular, las SAN mejoran el rendimiento tanto de las redes como de los servidores.

**▸ Recuperación de desastres y respaldo de datos:** las SAN son ideales para implementar soluciones de recuperación de desastres y respaldo de datos debido a su capacidad para replicar datos y mover grandes volúmenes de información rápidamente.

Desventajas de implementar una SAN

**▸ Costo:** la implementación de un SAN puede ser costosa debido al *hardware* especializado, la infraestructura de red y el *software* de gestión requeridos. Además, los costos de mantenimiento y de administración también pueden ser significativos.

**▸ Complejidad:** la configuración y la gestión de un SAN pueden ser complejas y requieren conocimientos especializados. Esto puede aumentar la carga de trabajo para los administradores de sistemas, también puede requerir una curva de aprendizaje considerable.

**▸ Dependencia de la red:** dado que los SAN dependen de la red para la conectividad entre los servidores y los dispositivos de almacenamiento, cualquier problema en la red puede afectar el acceso a los datos y la disponibilidad del sistema.

**▸ Posible punto único de fallo:** a pesar de las características de la tolerancia a fallos, un SAN mal diseñado o mal configurado puede convertirse en un punto único de fallo, lo que potencialmente puede causar interrupciones en el servicio y la pérdida de datos.

**▸ Requerimientos de mantenimiento:** los SAN requieren una gestión y mantenimiento continuos para garantizar un rendimiento óptimo y la integridad de los datos. Esto incluye tareas como la supervisión del rendimiento, la aplicación de parches de seguridad y la realización de copias de seguridad regulares.

Integración con otras tecnologías

La integración de un SAN con otras tecnologías es fundamental para maximizar su eficacia y adaptabilidad en los entornos empresariales. Aquí hay algunas formas comunes en las que un SAN se integra con otras tecnologías:

**▸ Complementariedad con NAS:** mientras que la SAN proporciona un almacenamiento a nivel de bloque, lo que es ideal para bases de datos y aplicaciones críticas, un NAS ofrece almacenamiento a nivel de archivo, lo que es más adecuado para compartir archivos.

**▸ Uso con sistemas de virtualización:** las SAN son especialmente útiles en entornos virtualizados, en los que la capacidad de almacenamiento puede asignarse y reasignarse dinámicamente a diferentes servidores virtuales. La integración con plataformas de virtualización como VMware vSphere, Microsoft Hyper-V o KVM permite una gestión más eficiente del almacenamiento y una mayor flexibilidad en la asignación de recursos.

**▸ Copia de seguridad y recuperación ante desastres:** los SAN pueden integrarse con *software* de copia de seguridad y soluciones de recuperación ante desastres para proteger los datos críticos de la empresa. La replicación de los datos a través de la red SAN a ubicaciones remotas proporciona una capa adicional de protección contra la pérdida de datos.

**▸ Conectividad de red:** los SAN pueden integrarse con la infraestructura de red existente, ya sea a través de redes de fibra óptica dedicadas o mediante protocolos de almacenamiento sobre redes IP (iSCSI). Esto permite una conectividad sin problemas con otros sistemas de la red y facilita la implementación de soluciones de almacenamiento distribuido.

**▸ Almacenamiento en la nube:** la integración de SAN con los servicios de almacenamiento en la nube les permite a las organizaciones ampliar su capacidad de almacenamiento más allá de los límites físicos de sus centros de datos. Esto puede lograrse mediante la implementación de soluciones de almacenamiento híbridas, las cuales combinan almacenamiento local con almacenamiento en la nube, o a través de la migración de datos a la nube para fines de archivado o recuperación ante desastres.

**▸ Automatización y orquestación:** la integración de SAN con herramientas de automatización y orquestación permite simplificar y acelerar las operaciones de gestión del almacenamiento. Esto incluye la automatización de tareas como aprovisionamiento de almacenamiento, migración de datos, ajuste de recursos y generación de informes de uso.

En resumen, la integración de un SAN con otras tecnologías es clave para aprovechar al máximo su potencial y satisfacer las necesidades cambiantes de almacenamiento en entornos empresariales modernos.

# 9.4. Network attached storage (NAS)

![Figura 9. NAS. Fuente: Delport, 2015.](images/image-12.png)

*Figura 9. NAS. Fuente: Delport, 2015.*

Un NAS es un dispositivo de almacenamiento que está conectado a una red y que permite almacenar y recuperar datos a través de una conexión de red. Actúa como un **servidor de archivos dedicado** y es accesible por múltiples clientes dentro de la red.

El NAS se utiliza comúnmente para compartir archivos en una red, realizar copias de seguridad de datos, almacenar y transmitir multimedia, también como solución de almacenamiento para virtualización.

Ventajas del NAS

**▸ Acceso remoto:** puedes acceder a tus archivos desde cualquier lugar del mundo siempre y cuando tengas conexión a Internet, lo que es útil para compartir archivos o acceder a ellos mientras estás fuera de casa u oficina.

**▸ Centralización:** permite centralizar el almacenamiento de datos en un único dispositivo, lo que facilita la gestión y el acceso a los archivos desde múltiples dispositivos.

**▸ Seguridad:** muchos NAS ofrecen opciones avanzadas de seguridad, como cifrado de datos, control de acceso y protección contra *malware,* lo que ayuda a mantener seguros tus archivos.

**▸ Redundancia:** algunos modelos de NAS ofrecen opciones de redundancia de datos, como RAID, para proteger contra la pérdida de datos debido a fallos de disco duro.

**▸ Escalabilidad:** puedes expandir fácilmente la capacidad de almacenamiento al añadir más discos duros o al utilizar unidades de mayor capacidad.

**▸ Respaldo automático:** muchos NAS ofrecen opciones de respaldo automático, lo que garantiza que tus datos estén siempre protegidos contra pérdidas.

**▸ Facilidad de acceso y gestión:** a diferencia de las soluciones de almacenamiento más complejas como SAN, los NAS son fáciles de configurar y gestionar, lo que los hace ideales para pequeñas y medianas empresas, así como para usuarios domésticos.

#### ▸ Compatibilidad con múltiples dispositivos y sistemas operativos: los NAS

suelen ser compatibles con una amplia variedad de dispositivos y sistemas operativos, lo que les permite a los usuarios de Windows, Mac, Linux y otros sistemas acceder y compartir archivos de manera efectiva.

**▸ Funciones adicionales:** además del almacenamiento de archivos, muchos NAS ofrecen una variedad de funciones adicionales, como copias de seguridad automáticas, transmisión de medios, servidores de correo electrónico, servidores web, y más. Estas funciones adicionales pueden hacer que un NAS sea una solución versátil para las necesidades de almacenamiento y servicio en una red.

Desventajas del NAS

**▸ Velocidad limitada:** la velocidad de transferencia de datos de un NAS puede ser más lenta en comparación con el almacenamiento local, especialmente en redes domésticas con conexiones más lentas.

**▸ Configuración compleja:** configurar y administrar un NAS puede requerir cierto nivel de conocimientos técnicos, lo que puede ser desafiante para usuarios menos experimentados.

**▸ Dependencia de la red:** la disponibilidad de los archivos en un NAS depende de la disponibilidad y la estabilidad de la red, lo que puede ser un inconveniente si experimentas problemas de conectividad.

**▸ Riesgo de fallo del** ***hardware:*** como cualquier dispositivo electrónico, los NAS están sujetos a los fallos del *hardware,* lo que puede resultar en la pérdida de datos si no se toman medidas adecuadas de respaldo y redundancia.

En general, aunque los sistemas NAS ofrecen muchas ventajas en términos de accesibilidad, seguridad y escalabilidad, es importante considerar también las posibles limitaciones y desafíos asociados con su implementación y uso.

# 9.5. Virtualización

![Figura 10. Virtualización. Fuente: Guest, 2015.](images/image-13.png)

*Figura 10. Virtualización. Fuente: Guest, 2015.*

La virtualización se refiere a la **creación de una versión virtual** de los recursos informáticos, como servidores, dispositivos de almacenamiento, redes y aplicaciones. Permite que múltiples sistemas operativos y aplicaciones se ejecuten en un solo servidor físico.

Incluye la virtualización de los servidores, del almacenamiento, de las redes y de los escritorios. Cada tipo se centra en virtualizar diferentes aspectos de los sistemas informáticos.

Virtualización de servidores

Permite que múltiples máquinas virtuales (VM) operen en un solo servidor físico. Cada VM actúa como un servidor independiente, lo que mejora la utilización de recursos, simplifica la gestión y reduce costos. Entornos más comunes: VMware, Microsoft Hyper-V y soluciones de código abierto como KVM y Xen.

Virtualización del almacenamiento

Consiste en agrupar el almacenamiento físico de múltiples dispositivos de red y presentarlo como un solo recurso de almacenamiento. Mejora la eficiencia, la escalabilidad y la accesibilidad de los datos. La virtualización del almacenamiento se utiliza a menudo en conjunción con SAN y NAS, lo que optimiza la gestión del almacenamiento y la recuperación de datos.

Virtualización de redes

Incluye la virtualización de los componentes

de red como *switches, routers* y

conexiones de red. Permite la creación de redes virtuales independientes en una misma infraestructura física. Una aplicación de la virtualización de las redes es **redes** **definidas por** ***software*** (SDN), que centraliza el control de la red y facilita la gestión y automatización.

Virtualización de escritorios

Permite que los usuarios accedan a sus

escritorios personales, que están

almacenados en un servidor central, desde cualquier dispositivo y ubicación. Mejora la movilidad, la seguridad y la gestión de los escritorios. Es útil en entornos en los que se requiere flexibilidad de acceso y control centralizado. Por ejemplo, ThinClient.

Ventajas y desventajas de la virtualización

La virtualización ofrece una serie de ventajas y desventajas:

#### Ventajas

**▸ Mayor eficiencia de recursos:** la virtualización permite consolidar múltiples sistemas en un solo servidor físico, lo que reduce el desperdicio de recursos y mejora la utilización de la capacidad de procesamiento, almacenamiento y red.

**▸ Flexibilidad y escalabilidad:** al virtualizar, es más fácil escalar los recursos según las necesidades del negocio. Se pueden asignar o desasignar recursos a las

Seguridad y Alta Disponibilidad 26 Tema 9. Material de estudio máquinas virtuales según sea necesario, sin necesidad de modificar la infraestructura física.

**▸ Aislamiento de aplicaciones:** cada máquina virtual opera de manera independiente de las demás, lo que proporciona un alto grado de aislamiento entre las aplicaciones y los sistemas operativos que se ejecutan en ellas. Esto reduce el riesgo de que un problema en una aplicación afecte a otras.

**▸ Facilidad de copia y respaldo:** las máquinas virtuales pueden ser copiadas y respaldadas fácilmente, lo que simplifica la recuperación ante desastres y la creación de entornos de desarrollo y pruebas.

**▸ Mejora en la gestión y la administración:** la virtualización proporciona herramientas e interfaces de gestión centralizadas que facilitan la administración de múltiples sistemas y recursos desde una sola ubicación.

#### Desventajas

**▸ Costo inicial:** implementar una infraestructura de virtualización puede requerir una inversión inicial significativa en *hardware, software* y capacitación.

**▸** ***Overhead*** **de rendimiento:** aunque la virtualización ofrece beneficios en cuanto a la eficiencia de recursos, también introduce un pequeño *overhead* de rendimiento debido a la capa de *software* adicional necesaria para gestionar las máquinas virtuales.

**▸ Complejidad de la gestión:** administrar entornos virtualizados puede ser complejo, especialmente a medida que crece el número de máquinas virtuales y de la infraestructura asociada. Se requiere personal capacitado para gestionar eficazmente estos entornos.

**▸ Dependencia de la infraestructura física:** aunque las máquinas virtuales son independientes entre sí, siguen dependiendo de la infraestructura física subyacente. Un fallo en el *hardware* físico puede afectar a múltiples máquinas virtuales.

**▸ Riesgo de consolidación excesiva:** si no se planifica adecuadamente, la consolidación excesiva de sistemas en un solo servidor físico puede aumentar la carga de trabajo y comprometer el rendimiento general del sistema.

# 9.6. Clúster

Un clúster es un grupo de computadoras (o nodos) que están conectadas entre sí y que trabajan de manera conjunta **como si fueran una sola entidad.** Los nodos en un clúster pueden ser servidores, estaciones de especializados.

trabajo o incluso dispositivos

Los clústeres se utilizan principalmente para mejorar el rendimiento, la disponibilidad y la capacidad de manejo de las cargas de

trabajo. Al agrupar recursos

computacionales, se pueden resolver tareas más complejas o manejar mayores volúmenes de datos de manera más eficiente.

Tipos de clústeres

**▸ Clúster de alta disponibilidad:** está diseñado para proporcionar una alta disponibilidad y continuidad del servicio. Si un nodo falla, las tareas se redistribuyen automáticamente a otros nodos para evitar interrupciones en el servicio.

**▸ Clúster de balanceo de carga:** es utilizado para distribuir equitativamente las cargas de trabajo entre los nodos del clúster, con lo que se mejora el rendimiento y la capacidad de respuesta del sistema.

**▸ Clúster de cómputo de alto rendimiento (HPC):** es empleado para ejecutar aplicaciones que requieren un gran poder de cómputo, como simulaciones científicas, modelado climático, análisis genómico, etc.

**▸ Clúster de almacenamiento:** está orientado a proporcionar un almacenamiento centralizado y escalable para las aplicaciones que manejan grandes volúmenes de datos.

# 9.7. Referencias bibliográficas

| Bytelearning. | (2018a). RAID | 1 | [gráfico]. |
| --- | --- | --- | --- |
|  | https://bytelearning.blogspot.com/2018/02/raid-software-mdadm-linux.html |  |  |
| Bytelearning. | (2018b). RAID | 5 | [gráfico]. |
|  | https://bytelearning.blogspot.com/2018/02/raid-software-mdadm-linux.html |  |  |
| Cburnett. | (2006). RAID | 6 | [gráfico]. |

[https://commons.wikimedia.org/wiki/File:RAID_6.svg](https://commons.wikimedia.org/wiki/File:RAID_6.svg)

Delport, R. (2015). *A NAS is a device managing multiple hard drives as one* [imagen]. [https://behind-the-scenes.net/things-to-consider-before-buying-a-nas-system/](https://behind-the-scenes.net/things-to-consider-before-buying-a-nas-system/)

Gola, G. (2023). How to Recover Data from SAN Storage? [gráfico]. [https://www.stellarinfo.co.in/kb/recover-data-from-san-storage.php](https://www.stellarinfo.co.in/kb/recover-data-from-san-storage.php)

Guest. (2015). *Reasons why Switching to Virtualization is Easy and Effective* [gráfico]. <https://technofaq.org/posts/2015/06/reasons-why-switching-to-virtualizationis-easy-and-effective/>

Informática Sevilla. (2019). *Recuperación de datos sistemas RAID* [imagen]. [https://informaticasevilla.com/recuperacion-de-datos-sistemas-raid/](https://informaticasevilla.com/recuperacion-de-datos-sistemas-raid/)

De la Peña Amor, Á. (2015a). *Configuraciones RAID: rendimiento y seguridad* [imagen]. [https://bytelix.com/guias/configuraciones-raid-rendimiento-y-seguridad/](https://bytelix.com/guias/configuraciones-raid-rendimiento-y-seguridad/)

De la Peña Amor, Á. (2015b). *RAID 0* [gráfico].

[https://bytelix.com/guias/configuraciones-raid-rendimiento-y-seguridad/](https://bytelix.com/guias/configuraciones-raid-rendimiento-y-seguridad/)

Vinicius. (2014). *Esquema de RAID 10 (no caso do RAID 01, invertem-se as* *posições do RAID 0 e RAID 1)* [gráfico]. <https://www.monolitonimbus.com.br/discosem-raid/>

# Borges, E. (2019, abril 30). Servidor en cluster. Infranetworking.

# [https://blog.infranetworking.com/servidor-en-cluster/](https://blog.infranetworking.com/servidor-en-cluster/)

# Servidor en clúster

¿Qué es un servidor en clúster? ¿Qué ventajas ofrece? Te conviene leer este artículo si pretendes ofrecer un servicio de alta disponibilidad a un entorno empresarial.

# raid-servidor-nas/

# Tipos de RAID para servidores NAS: conócelos

# todos y sus características

De Luz, S. (2024, abril 19). Tipos de RAID para servidores NAS: conoce todos y sus características. *Redes Zone.* <https://www.redeszone.net/tutoriales/servidores/tipos-> Un servidor NAS es un dispositivo que está presente en la mayoría de las empresas. Si quieres mejorar su alta disponibilidad, sería conveniente implementar un sistema de RAID que garantice su usabilidad. Elije el RAID adecuado para tu NAS.

# riesgos-usar-nube-privada/

# ¿Existen riesgos al usar una nube privada? Sí, estos

# son los peores

De Luz, S. (2024, enero 26). ¿Existen riesgos al usar una nube privada? Sí, estos son los peores. *Redes Zone.* <https://www.redeszone.net/noticias/seguridad/peores-> Todo el mundo guarda su información en la nube, pero ¿estamos completamente seguros? Deberíamos tomar precauciones al usar la nube para guardar nuestros datos…

# guardar-todo-servidor-nas/

# Por qué no deberías guardar todos tus datos en un

# servidor NAS

De Luz, S. (2022, abril 5). Por qué no deberías guardar todos tus datos en un servidor NAS. *Redes Zone.* <https://www.redeszone.net/noticias/redes/por-que-no-> ¿Tienes curiosidad por conocer el contenido de este *post?* ¿Alguna vez te has planteado qué tan seguro es guardar tu información en un servidor NAS?

# Tipos de RAID. En qué se diferencian y cuáles son

# los mejores

NASeros. (2020, febrero 7). *Tipos de RAID. En qué se diferencian y cuáles son los* *mejores* [vídeo]. YouTube. [https://www.youtube.com/watch?v=x8MXkvgeD0w](https://www.youtube.com/watch?v=x8MXkvgeD0w)

Ya hemos visto la diferencia entre los diferentes tipos de RAID en la teoría, pero no siempre la situación de partida es la misma: ¿cuál utilizarías en diferentes situaciones?

![image-14](images/image-14.png)

Accede al vídeo: [https://www.youtube.com/embed/x8MXkvgeD0w](https://www.youtube.com/embed/x8MXkvgeD0w)

# YouTube. [https://www.youtube.com/watch?v=YPlCdjCmX0I](https://www.youtube.com/watch?v=YPlCdjCmX0I)

# Servidores NAS: todo lo que necesitas saber

Xataka. (2021, octubre 25). *Servidores NAS: todo lo que necesitas saber* [vídeo]. Amplia tus conocimientos sobre los servidores NAS. Todos sabemos qué es un servidor NAS, pero con tu perfil técnico te deberías plantear saber más sobre cómo se usan, sus utilidades…

![image-15](images/image-15.png)

Accede al vídeo: [https://www.youtube.com/embed/YPlCdjCmX0I](https://www.youtube.com/embed/YPlCdjCmX0I)

# [https://www.youtube.com/watch?v=tWo825XSnVA](https://www.youtube.com/watch?v=tWo825XSnVA)

# NAS vs. SAN explicación

Daksinho. (2019, octubre 20). *NAS vs. SAN explicación* [vídeo]. YouTube. ¿Sabes lo que es un NAS? ¿Sabes lo que es un SAN? ¿Te ha quedado claro en qué cosas se asemejan y en cuáles se diferencian un NAS y un SAN? Aquí te lo explican más a fondo.

![image-16](images/image-16.png)

Accede al vídeo: [https://www.youtube.com/embed/tWo825XSnVA](https://www.youtube.com/embed/tWo825XSnVA)

# Entrenamiento 1: configuración de RAID 0 en Windows 10 con VirtualBox

#### ▸ Planteamiento del ejercicio

- Objetivo: configurar un RAID 0 utilizando dos discos virtuales en VirtualBox para mejorar el rendimiento y la velocidad de acceso a los datos en una máquina virtual con Windows 10.

Requisitos:

## 1. VirtualBox instalado en tu sistema.

## 2. Dos discos virtuales creados en VirtualBox.

3. Conocimientos básicos de administración de sistemas operativos Windows.

#### ▸ Desarrollo paso a paso

Paso 1. Preparación: tener listo Windows 10 y dos discos virtuales adicionales.

Paso 2. Iniciar la máquina virtual.

Paso 3. Entrar en la administración de discos de Windows 10.

Paso 4. Identificar los dos discos virtuales añadidos.

Paso 5. Crear el conjunto RAID 0.

Paso 6. Formatear y asignar una letra de unidad.

Paso 7. Verificación.

**Paso 1.** Preparación: creación de discos virtuales en VirtualBox.

## 1. Abre VirtualBox en tu sistema.

2. Selecciona tu máquina virtual de Windows 10 y haz clic en «Configuración».

## 3. En el menú de la izquierda, selecciona «Almacenamiento».

4. En la sección «Controlador SATA» o similar, haz clic en el icono de añadir un

nuevo disco duro.

**▸**

    - Selecciona «Crear un nuevo disco duro ahora» y haz clic en «Crear».

    - Elige el tipo de archivo de disco duro. Por lo general, VirtualBox Disk Image (VDI) es una buena opción si no tienes necesidades específicas.

    - Selecciona el tipo de almacenamiento. «Dinámicamente asignado» es generalmente el adecuado para las máquinas virtuales de prueba y desarrollo.

    - Define el tamaño del disco. Puedes ajustarlo según tus necesidades, pero asegúrate de tener suficiente espacio para tus datos.

5. Una vez creado el primer disco virtual, repite los pasos para crear un segundo

disco virtual. Asegúrate de que ambos discos virtuales estén listos y añadidos a la configuración de la máquina virtual de Windows 10. **Paso 2.** Iniciar la máquina virtual.

## 1. Inicia VirtualBox si no lo has hecho ya.

2. Selecciona tu máquina virtual de Windows 10 y haz clic en «Iniciar».

**Paso 3.** Administración de discos en Windows 10. Una vez que Windows 10 esté cargado en la máquina virtual:

**▸**

- Presiona «Win + X» en tu teclado y selecciona «Administración de discos» en el menú desplegable que aparece.

**Paso 4.** Identificar discos virtuales. En la ventana de administración de discos:

**▸**

- Verifica que los dos discos virtuales que has creado en VirtualBox aparezcan en la lista de discos. Deberían mostrarse como «No asignado».

**Paso 5.** Crear el conjunto RAID 0. Haz clic derecho en uno de los discos y selecciona «Nuevo conjunto RAID-0...».

**▸**

- Se abrirá el asistente para configurar el RAID. Haz clic en «Siguiente» para comenzar.

- Selecciona los dos discos virtuales que deseas incluir en el conjunto RAID 0 y haz clic en «Siguiente».

- Define el tamaño del volumen RAID 0. Por lo general, puedes seleccionar el tamaño máximo disponible si planeas usar todo el espacio de los discos.

- Selecciona las opciones de formato y nombre del volumen según tus preferencias.

**Paso 6.** Formatear y asignar una letra de unidad. Una vez creado el conjunto RAID 0:

**▸**

- Haz clic derecho en el nuevo volumen RAID 0 que se ha creado y selecciona «Nuevo volumen simple...».

- Sigue el asistente para formatear el nuevo volumen RAID 0 con el sistema de archivos deseado (como NTFS) y asígnale una letra de unidad.

**Paso 7.** Verificación del funcionamiento. Para asegurarte de que el RAID 0 está funcionando correctamente:

**▸**

- Copia algunos archivos al nuevo volumen RAID 0 y verifica que se escriban en ambos discos virtuales.

- Puedes comparar la velocidad de acceso a datos antes y después de configurar el RAID 0 para evaluar cualquier mejora en el rendimiento.

# Entrenamiento 2: configuración de RAID 1 en Windows 10 con VirtualBox

#### ▸ Planteamiento del ejercicio

- Objetivo: configurar un RAID 1 utilizando dos discos virtuales en VirtualBox para proporcionar redundancia de los datos en una máquina virtual con Windows 10.

Requisitos:

## 1. VirtualBox instalado en tu sistema.

## 2. Dos discos virtuales creados en VirtualBox.

3. Conocimientos básicos de administración de sistemas operativos Windows.

#### ▸ Desarrollo paso a paso

Paso 1. Preparación: tener listo Windows 10 y dos discos virtuales adicionales.

Paso 2. Iniciar la máquina virtual.

Paso 3. Entrar en administración de discos de Windows 10.

Paso 4. Identificar los dos discos virtuales añadidos.

Paso 5. Crear el conjunto RAID 1.

Paso 6. Formatear y asignar una letra de unidad.

Paso 7. Verificación.

**Paso 1.** Preparación inicial.

## 1. Verificación de VirtualBox:

**▸**

- Asegúrate de tener VirtualBox instalado en tu sistema.

- Confirma que tienes una máquina virtual de Windows 10 creada y que está funcionando correctamente en VirtualBox.

## 2. Creación de discos virtuales:

**▸**

- En VirtualBox, asegúrate de tener dos discos duros virtuales adicionales creados y adjuntados a tu máquina virtual de Windows 10.

- Estos discos deben estar en estado «no asignado» para poder configurarlos como parte de un RAID.

**Paso 2.** Iniciar la máquina virtual.

## 1. Arranca tu máquina virtual:

**▸**

- Inicia VirtualBox.

- Selecciona tu máquina virtual de Windows 10 y haz clic en iniciar.

**Paso 3.** Administración de discos en Windows 10. Acceso a la administración de discos:

**▸**

- Una vez que Windows 10 esté completamente cargado en la máquina virtual, presiona «Win + X» en tu teclado.

- En el menú que aparece, selecciona «Administración de discos».

**Paso 4.** Identificar los discos virtuales. Verificación de discos:

**▸**

- En la ventana de administración de discos, deberías ver los discos duros de tu máquina virtual, así como los dos discos virtuales adicionales que has creado.

- Los discos virtuales deben aparecer como «No asignado», lo que significa que aún no tienen particiones ni están formateados.

**Paso 5.** Configurar el RAID 1.

## 1. Crear el volumen espejo RAID 1:

**▸**

- Haz clic derecho en uno de los discos virtuales que deseas incluir en el RAID.

- En el menú contextual, selecciona «Nuevo volumen reflejado...». Se abrirá el asistente para crear un volumen reflejado.

## 2. Seleccionar los discos:

**▸**

- En el asistente, selecciona los dos discos virtuales que quieres usar para el RAID 1.

- Haz clic en «Siguiente» para continuar.

**Paso 6.** Asignar letras de unidad y formatear.

**▸**

- Sigue las instrucciones del asistente para asignarle una letra de unidad al nuevo volumen RAID 1.

- Elige el sistema de archivos que deseas utilizar (generalmente NTFS para Windows).

- Completa el proceso siguiendo las indicaciones del asistente.

**Paso 7.** Verificación de la configuración.

## 1. Prueba de redundancia:

**▸**

- Copia algunos archivos a la unidad RAID 1 desde Windows.

- Verifica que los archivos se escriban simultáneamente en ambos discos virtuales.

- Desconecta uno de los discos virtuales desde VirtualBox para simular una falla.

- Verifica que los archivos aún sean accesibles desde el disco restante.

## 2. Restauración del RAID:

**▸**

- Reconecta el disco virtual que desconectaste anteriormente.

- Verifica que el RAID se restaure automáticamente y que los datos estén sincronizados nuevamente entre ambos discos.

# Entrenamiento 3: configuración de RAID 5 en Windows 10 con VirtualBox

#### ▸ Planteamiento del ejercicio

Configurar un RAID 5 utilizando tres discos virtuales en VirtualBox para proporcionar redundancia de datos y tolerancia a fallos en una máquina virtual con Windows 10.

Requisitos:

## 1. VirtualBox instalado en tu sistema.

## 2. Tres discos virtuales creados en VirtualBox.

3. Conocimientos básicos de administración de sistemas operativos Windows.

#### ▸ Desarrollo paso a paso

Paso 1. Preparación: tener listo Windows 10 y tres discos virtuales adicionales.

Paso 2. Iniciar la máquina virtual.

Paso 3. Entrar en administración de discos de Windows 10.

Paso 4. Identificar los dos discos virtuales añadidos.

Paso 5. Crear el conjunto RAID 5.

Paso 6. Formatear y asignar una letra de unidad.

Paso 7. Verificación.

**Paso1.** Preparación.

1. Abrir VirtualBox: inicia VirtualBox desde tu sistema operativo.

2. Verificar la máquina virtual: asegúrate de que tienes una máquina virtual con

Windows 10 creada y lista para ser iniciada.

## 3. Configurar los discos virtuales:

**▸**

- Ve a la configuración de la máquina virtual de Windows 10.

- En la sección de almacenamiento, añade tres discos duros virtuales adicionales (pueden ser discos VDI, VHD, o VMDK según tu preferencia).

**Paso 2.** Iniciar la máquina virtual. Iniciar Windows 10:

**▸**

- Selecciona tu máquina virtual de Windows 10 y haz clic en «Iniciar» en VirtualBox para iniciar Windows 10.

**Paso 3.** Administración de discos. Acceder a la administración de discos:

**▸**

- Una vez que Windows 10 esté completamente cargado, presiona «Win + X» en el teclado para abrir el menú de opciones avanzadas.

- Selecciona «Administración de discos» en el menú.

**Paso 4.** Identificar discos virtuales.

Ver los discos no asignados:

**▸**

- En la ventana de administración de discos, deberías ver los tres discos virtuales que has añadido. Estos discos aparecerán como «no asignado».

**Paso 5.** Crear el conjunto RAID 5.

## 1. Iniciar el asistente para nuevo conjunto RAID:

**▸**

- Haz clic derecho en uno de los discos virtuales no asignados y selecciona «Nuevo conjunto RAID-5...» en el menú contextual.

## 2. Configurar el RAID:

**▸**

- En el asistente que aparece, selecciona los tres discos virtuales que deseas utilizar para el RAID 5.

- Sigue las instrucciones del asistente para definir el tamaño del conjunto RAID y el tamaño de los sectores (generalmente, los valores predeterminados son adecuados para la mayoría de los casos).

- Elige el sistema de archivos deseado para el RAID 5 (como NTFS) y asigna una letra de unidad. Asegúrate de seleccionar la opción para formatear el volumen con el sistema de archivos elegido.

## 3. Finalizar la configuración:

**▸**

- Completa el asistente para crear el conjunto RAID 5. Esto puede llevar algún tiempo dependiendo del tamaño de los discos y la velocidad del sistema.

**Paso 6.** Formatear y asignar una letra de unidad.

Formatear el volumen RAID:

**▸**

- Una vez que se haya creado el conjunto RAID 5, Windows te pedirá que formatees el volumen.

- Elige el sistema de archivos deseado (por ejemplo, NTFS) y proporciona un nombre para el volumen.

- Haz clic en «Aceptar» para iniciar el formateo y espera a que se complete.

**Paso7.** Verificación.

## 1. Probar la funcionalidad del RAID 5:

**▸**

- Copia algunos archivos al volumen RAID 5 desde Windows para asegurarte de que los datos se escriban correctamente en todos los discos.

## 2. Simular un fallo de disco:

**▸**

- Desde la configuración de VirtualBox, desconecta uno de los discos virtuales que forman parte del RAID 5.

- Verifica que los archivos sean aún accesibles desde el volumen RAID 5 y que la redundancia esté funcionando.

## 3. Restaurar el disco:

**▸**

- Reconecta el disco virtual que desconectaste anteriormente desde VirtualBox.

- Verifica que el sistema RAID 5 se restaure automáticamente y que los datos estén nuevamente protegidos y accesibles.

Consideraciones adicionales:

**▸**

- Backup de datos: antes de realizar cualquier acción que implique generar cambios en la configuración del disco, asegúrate de hacer una copia de seguridad de todos los datos importantes.

- Monitoreo y mantenimiento: después de configurar el RAID 5, considera implementar algún método de monitoreo para verificar regularmente el estado del RAID y la integridad de los datos.

Al seguir estos pasos detallados, deberías poder configurar un RAID 5 funcional en Windows 10 utilizando discos virtuales en VirtualBox, lo que proporciona una redundancia de datos y tolerancia a fallos para tu máquina virtual.

# Entrenamiento 4: implantación de configuración

# RAID 1, 3 y 5 en Ubuntu

#### ▸ Planteamiento del ejercicio

El objetivo de esta actividad es que aprendas a configurar diferentes tipos de RAID (1, 3 y 5) en un sistema Ubuntu, comprendas las ventajas y desventajas de cada tipo de RAID y seas capaz de verificar su funcionamiento y rendimiento.

#### ▸ Desarrollo paso a paso

- Partiremos de una instalación de Ubuntu en una máquina virtual, como VirtualBox, y tendremos tres discos adicionales para la configuración de RAID (pueden ser archivos de imagen de disco si se trabaja en una máquina virtual).

- Instalaremos la herramienta mdadm, que es una herramienta esencial para la gestión efectiva de RAID en sistemas Linux como Ubuntu, lo que proporcionará las herramientas necesarias para configurar, administrar y monitorizar arreglos RAID de manera eficiente y confiable.

- Crearemos la configuración RAID1.

- Crearemos la configuración RAID3.

- Crearemos la configuración RAID5.

- Se harán pruebas de rendimiento con las herramientas dd o fio.

- Verificaremos la redundancia desconectando un disco de cada configuración RAID y observaremos su comportamiento.

- Reemplazaremos el disco fallido y reconstruiremos el RAID correspondiente.

## 1. Instalación de Ubuntu en VirtualBox:

**▸**

- Descarga la imagen ISO de Ubuntu desde el sitio web oficial.

- Crea una nueva máquina virtual en VirtualBox y configúrala para usar la imagen ISO descargada.

- Sigue el asistente de instalación para instalar Ubuntu en la máquina virtual.

## 2. Creación de discos adicionales:

**▸**

- Abre la configuración de la máquina virtual en VirtualBox.

- Añade tres discos duros virtuales adicionales en la sección de almacenamiento de la máquina virtual.

## 3. Instalación de las herramientas necesarias:

![Figura 11. Instalar las herramientas necesarias. Fuente: elaboración propia.](images/image-17.png)

*Figura 11. Instalar las herramientas necesarias. Fuente: elaboración propia.*

- Seguridad y Alta Disponibilidad 54

    - Tema 9. Entrenamientos

## 4. Verificación de los discos disponibles:

**▸**

- Listar los discos disponibles para asegurarse de que hay suficientes discos adicionales.

![Figura 12. Listar los discos disponibles. Fuente: elaboración propia.](images/image-18.png)

*Figura 12. Listar los discos disponibles. Fuente: elaboración propia.*

**▸**

- La respuesta que se debe obtener debería ser parecida a lo siguiente:

![Figura 13. Resultado. Fuente: elaboración propia.](images/image-19.png)

*Figura 13. Resultado. Fuente: elaboración propia.*

En este caso, /dev/sdb, /dev/sdc y /dev/sdd representan los tres discos virtuales adicionales que se han creado en VirtualBox para utilizar en la configuración de RAID en Ubuntu.

## 5. Configuración de RAID 1:

**▸**

- Seleccionar dos discos para la configuración RAID 1.

**▸**

![Figura 14. Seleccionar dos discos. Fuente: elaboración propia.](images/image-20.png)

*Figura 14. Seleccionar dos discos. Fuente: elaboración propia.*

- Se utiliza la herramienta «mdadm» para crear un arreglo RAID 1 utilizando dos dispositivos. Aquí está el significado de cada parte del comando:

sudo : ejecuta el comando con privilegios de superusuario. mdadm : es el comando utilizado para administrar los dispositivos RAID en sistemas Linux. --create : indica que se desea crear un nuevo arreglo RAID. --verbose : especifica que se desea una salida detallada del proceso de creación. /dev/md0 : especifica el nombre del dispositivo RAID que se va a crear. En este caso, se le asigna el nombre «/dev/md0». --level=1 : indica que se está creando un arreglo RAID nivel 1, que es un espejo. Esto significa que los datos se replicarán en ambos discos.

--raid-devices=2 : especifica el número de dispositivos que formarán parte del arreglo RAID. En este caso, se utilizarán dos dispositivos.

/dev/sdb /dev/sdc : son los dispositivos físicos que se utilizarán para el arreglo RAID. En este caso, se utilizan «/dev/sdb» y «/dev/sdc».

**▸**

![Figura 15. Crear un sistema de archivos y montarlo. Fuente: elaboración propia. • Crear un sistema de archivos y montarlo:](images/image-21.png)

*Figura 15. Crear un sistema de archivos y montarlo. Fuente: elaboración propia.*

sudo mkfs.ext4 /dev/md0 : este comando formatea el dispositivo RAID /dev/md0 con el sistema de archivos ext4.

sudo mkdir -p /mnt/raid1 : este comando crea un directorio /mnt/raid1 en el sistema de archivos.

sudo mount /dev/md0 /mnt/raid1 : este comando monta el dispositivo RAID /dev/md0 en el directorio /mnt/raid1.

**▸**

![Figura 16. Verificar la configuración RAID 1. Fuente: elaboración propia. • Verificar la configuración RAID 1:](images/image-22.png)

*Figura 16. Verificar la configuración RAID 1. Fuente: elaboración propia.*

cat /proc/mdstat : este comando muestra el estado actual de todos los dispositivos RAID en el sistema.

sudo mdadm --detail /dev/md0 : este comando muestra información detallada sobre el arreglo RAID específico /dev/md0 .

![Figura 17. Resultado. Fuente: elaboración propia. Su resultado debería ser similar a lo siguiente:](images/image-23.png)

*Figura 17. Resultado. Fuente: elaboración propia.*

## 6. Configuración de RAID 3:

**▸**

- Seleccionar tres discos para la configuración RAID 3.

**▸** **▸**

![Figura 18. Seleccionar tres discos. Fuente: elaboración propia. Fuente: elaboración propia.](images/image-24.png)

*Figura 18. Seleccionar tres discos. Fuente: elaboración propia. Fuente: elaboración propia.*

![Figura 19. Crear un sistema de archivos y montarlo. Fuente: elaboración propia. • Crear un sistema de archivos y montarlo:](images/image-25.png)

*Figura 19. Crear un sistema de archivos y montarlo. Fuente: elaboración propia.*

![Figura 20. Verificar la configuración. Fuente: elaboración propia. • Verificar la configuración RAID 3:](images/image-26.png)

*Figura 20. Verificar la configuración. Fuente: elaboración propia.*

## 7. Configuración de RAID 5:

**▸**

- Seleccionar tres discos para la configuración de RAID 5.

**▸** **▸**

![Figura 21. Seleccionar tres discos. Fuente: elaboración propia.](images/image-27.png)

*Figura 21. Seleccionar tres discos. Fuente: elaboración propia.*

![Figura 22. Crear un sistema de archivos y montarlo. Fuente: elaboración propia. • Crear un sistema de archivos y montarlo:](images/image-28.png)

*Figura 22. Crear un sistema de archivos y montarlo. Fuente: elaboración propia.*

- Verificar la configuración RAID 5:

![Figura 23. Verificar la configuración. Fuente: elaboración propia.](images/image-29.png)

*Figura 23. Verificar la configuración. Fuente: elaboración propia.*

## 8. Evaluación y comparación.

## 9. Pruebas de rendimiento:

**▸**

- Utiliza herramientas como `dd` o `fio` para evaluar el rendimiento de lectura y escritura en cada configuración RAID.

![Figura 24. Pruebas de rendimiento. Fuente: elaboración propia.](images/image-30.png)

*Figura 24. Pruebas de rendimiento. Fuente: elaboración propia.*

Se utilizan « d d » para crear archivos de prueba llenos de ceros en diferentes dispositivos RAID montados en los directorios « /mnt/raid1» , « /mnt/raid3» y « /mnt/raid5 », respectivamente. En resumen, cada comando crea un archivo llamado «testfile» lleno de ceros en el directorio correspondiente a cada configuración RAID.

## 10. Verificación de la redundancia:

**▸**

- Desconectamos un disco de cada configuración RAID y observamos el comportamiento del sistema.

![Figura 25. Verificación de la redundancia. Fuente: elaboración propia.](images/image-31.png)

*Figura 25. Verificación de la redundancia. Fuente: elaboración propia.*

Estos comandos están destinados a simular un fallo de disco en cada uno de los arreglos RAID y luego eliminar el disco fallido del arreglo.

## 11. Restauración de la redundancia:

**▸**

- Reemplazar el disco fallido y reconstruir el RAID.

**▸**

![Figura 26. Restauración de la redundancia. Fuente: elaboración propia.](images/image-32.png)

*Figura 26. Restauración de la redundancia. Fuente: elaboración propia.*

- Después de ejecutar estos comandos, se agregarán los discos especificados de vuelta a los arreglos RAID correspondientes.

# Entrenamiento 5: configuración de un clúster de

# servidores

#### ▸ Planteamiento del ejercicio

En esta actividad, configurarás un clúster de servidores para asegurar la alta disponibilidad de un servicio web (Apache) y aplicarás medidas de seguridad para proteger el entorno. Los servidores estarán configurados de tal manera que, si uno de ellos falla, el otro pueda tomar el control y mantener el servicio en funcionamiento. Material necesario:

**▸**

- Dos o más máquinas virtuales o servidores físicos con Ubuntu (192.168.1.101 y 192.168.1.102).

- Acceso a Internet para la instalación de paquetes necesarios.

- Acceso SSH a los servidores.

#### ▸ Desarrollo paso a paso

**Paso 1.** Configuración inicial de los servidores: actualizar los paquetes en cada servidor, instalar el servidor SSH si no está instalado y asegurar el acceso SSH configurando la autenticación con clave pública.

**Paso 2.** Configuración del clúster de alta disponibilidad: instalar el *software* de clúster (Pacemaker y Corosync), configurar el acceso a Pacemaker/Corosync Command Line Interface (PCS), autenticar los nodos del clúster, crear y configurar el clúster, y verificar el estado del clúster.

**Paso 3.** Configuración de recursos y *failover:* agregar un recurso de IP virtual para el clúster, agregar un recurso de servicio (ejemplo: Apache), configurar el orden y la colocación de los recursos, verificar el estado de los recursos.

**Paso 4.** Implementación de medidas de seguridad: configurar *firewall* para permitir solo el tráfico necesario y configurar Application Armor (AppArmor).

#### ▸ Solución

**Paso 1.** Configuración inicial de los servidores:

## 1. Actualizar los paquetes en cada servidor:

![Figura 27. Actualizar los paquetes. Fuente: elaboración propia.](images/image-33.png)

*Figura 27. Actualizar los paquetes. Fuente: elaboración propia.*

## 2. Instalar el servidor SSH si no está instalado:

![Figura 28. Instalar el servidor SSH. Fuente: elaboración propia.](images/image-34.png)

*Figura 28. Instalar el servidor SSH. Fuente: elaboración propia.*

    - Seguridad y Alta Disponibilidad 65

        - Tema 9. Entrenamientos

3. Asegurar el acceso SSH configurando la autenticación con clave pública:

**▸**

- Generar una clave SSH en tu máquina local (si no tienes una):

![Figura 29. Generar una clave SSH. Fuente: elaboración propia.](images/image-35.png)

*Figura 29. Generar una clave SSH. Fuente: elaboración propia.*

**▸**

- Copiar la clave pública a cada servidor:

![Figura 30. Copiar la clave pública. Fuente: elaboración propia.](images/image-36.png)

*Figura 30. Copiar la clave pública. Fuente: elaboración propia.*

Este comando se utiliza para copiar la clave pública SSH de tu máquina local al servidor remoto especificado. Esto facilita el acceso al servidor sin tener que introducir la contraseña cada vez que te conectas vía SSH. La parte de «usuario» es el nombre de usuario en el servidor remoto y «servidor_ip» es la dirección IP del servidor.

**Paso 2.** Configuración del clúster de alta disponibilidad:

1. Instalar el software de clúster (Pacemaker y Corosync) en las dos máquinas

(nodos) que formarán parte del clúster:

Se instalarán tres paquetes:

**▸**

- Pacemaker: es un gestor de recursos de clúster de alta disponibilidad. Se encarga de iniciar y detener servicios en los nodos del clúster y de monitorizar su estado. Si detecta que un nodo ha fallado, reasigna los recursos a otro nodo activo.

- Corosync: es un sistema de mensajería de clúster que proporciona servicios de comunicación entre los nodos del clúster, así como de *quorum* y de configuración de clústeres. Trabaja estrechamente con Pacemaker para coordinar el estado del clúster y sus recursos.

- Pacemaker/Corosync Configuration System (PCS): es una herramienta de línea de comandos que facilita la configuración y la administración de los clústeres que utilizan Pacemaker y Corosync. Permite crear, configurar y gestionar clústeres de manera más sencilla.

## 2. Configurar el acceso a PCS en cada nodo:

**▸**

- Configurar una contraseña para el usuario «hacluster» (es típicamente un usuario del sistema utilizado por las herramientas de gestión de clústeres como Pacemaker y Corosync para la autenticación y la administración del clúster):

![Figura 31. Configurar una contraseña para el usuario «hacluster». Fuente: elaboración propia.](images/image-37.png)

*Figura 31. Configurar una contraseña para el usuario «hacluster». Fuente: elaboración propia.*

Donde se te pedirá que introduzcas una nueva contraseña.

**▸**

    - Habilitar e iniciar el servicio «pcs»:

![Figura 32. Habilitar e iniciar el servicio «pcs». Fuente: elaboración propia.](images/image-38.png)

*Figura 32. Habilitar e iniciar el servicio «pcs». Fuente: elaboración propia.*

3. Desde uno de los nodos, autenticar todos los nodos del clúster:

![Figura 33. Autenticar los nodos. Fuente: elaboración propia.](images/image-39.png)

*Figura 33. Autenticar los nodos. Fuente: elaboración propia.*

Esto se utiliza para autenticar y establecer una confianza mutua entre los nodos de un clúster de alta disponibilidad.

Las direcciones IP 192.168.1.101 y 192.168.1.102 son de los dos nodos, y la contraseña del usuario hacluster es mi_contraseña_segura .

![Figura 34. Crear y configurar el clúster. Fuente: elaboración propia. 4. Crear y configurar el clúster:](images/image-40.png)

*Figura 34. Crear y configurar el clúster. Fuente: elaboración propia.*

Para configurar el clúster, ejecuta este comando en uno de los nodos (por ejemplo, en 192.168.1.101):

![Figura 35. Configurar el clúster. Fuente: elaboración propia.](images/image-41.png)

*Figura 35. Configurar el clúster. Fuente: elaboración propia.*

Desde uno de los nodos, autentica ambos nodos utilizando PCS:

![image-42](images/image-42.png)

Figurar 36. Autenticar ambos nodos. Fuente: elaboración propia.

Finalmente, habilita el clúster para que se inicie automáticamente en todos los nodos:

![Figura 37. Habilitar el clúster. Fuente: elaboración propia.](images/image-43.png)

*Figura 37. Habilitar el clúster. Fuente: elaboración propia.*

## 5. Verificar el estado del clúster:

![Figura 38. Verificar el estado del clúster. Fuente: elaboración propia.](images/image-44.png)

*Figura 38. Verificar el estado del clúster. Fuente: elaboración propia.*

Este comando te proporcionará información sobre el estado del clúster, los nodos y cualquier recurso configurado.

**Paso 3.** Configuración de recursos y *failover*

## 1. Agregar un recurso de IP virtual para el clúster:

![Figura 39. Agregar un recurso de IP virtual. Fuente: elaboración propia.](images/image-45.png)

*Figura 39. Agregar un recurso de IP virtual. Fuente: elaboración propia.*

Esto se utiliza para crear un recurso en un clúster de alta disponibilidad gestionado por Pacemaker. Este recurso se utilizará

para asegurar que una dirección IP

específica esté siempre disponible en uno de los nodos del clúster, con lo que se proporcionará una alta disponibilidad para

los servicios que dependen de esa

dirección IP. A continuación, se desglosa cada parte del comando para explicar su funcionalidad:

pcs resource create mi_ip :

**▸**

- Comando de PCS para crear un nuevo recurso en el clúster.

- mi_ip : es el nombre que se le asignará al recurso. Puedes elegir cualquier nombre descriptivo para identificar el recurso dentro del clúster.

ocf:heartbeat:IPaddr2 :

**▸**

- Especifica el tipo de recurso que estás creando. En este caso, «IPaddr2» es un agente de recursos de Pacemaker que gestiona una dirección IP virtual. El prefijo «ocf:heartbeat» indica el estándar *open cluster framework* (OCF) y el proveedor del agente *(heartbeat).*

$$ip=192.168.1.100 :$$

**▸**

- Parámetro del recurso que define la dirección IP virtual que se le asignará al recurso. En este ejemplo, «192.168.1.100» es la dirección IP que el recurso intentará configurar y mantener activa en uno de los nodos del clúster.

cidr_netmask=24 :

**▸**

- Especifica la máscara de red CIDR para la dirección IP. Indica la cantidad de bits que se utilizan para definir la red en la que reside la dirección IP. En este caso, «24» corresponde a una máscara de red que cubre los primeros 24 bits de la dirección IP (255.255.255.0).

op monitor interval=30s :

**▸**

- Define las operaciones de monitoreo para el recurso.

- monitor : especifica que el agente debe monitorear el estado del recurso para asegurarse de que esté activo y funcional.

- interval=30s : especifica cada cuántos segundos se debe realizar la operación de monitoreo. En este caso, cada 30 segundos.

## 2. Agregar un recurso de servicio (ejemplo: Apache):

**▸**

- Instalar Apache en todos los nodos:

![Figura 40. Instalar Apache. Fuente: elaboración propia.](images/image-46.png)

*Figura 40. Instalar Apache. Fuente: elaboración propia.*

**▸**

- Crear el recurso de Apache:

![Figura 41. Crear el recurso de Apache. Fuente: elaboración propia.](images/image-47.png)

*Figura 41. Crear el recurso de Apache. Fuente: elaboración propia.*

## 3. Configurar el orden y la colocación de los recursos:

![Figura 42. Configurar el orden y la colocación de los recursos. Fuente: elaboración propia.](images/image-48.png)

*Figura 42. Configurar el orden y la colocación de los recursos. Fuente: elaboración propia.*

## 4. Verificar el estado de los recursos:

![Figura 43. Verificar el estado de los recursos. Fuente: elaboración propia.](images/image-49.png)

*Figura 43. Verificar el estado de los recursos. Fuente: elaboración propia.*

- Seguridad y Alta Disponibilidad 72

    - Tema 9. Entrenamientos

**Paso 4.** Implementación de medidas de seguridad:

1. Configurar el firewall para permitir solo el tráfico necesario:

**▸**

- Habilitar y configurar UFW:

![Figura 44. Habilitar y configurar UFW. Fuente: elaboración propia.](images/image-50.png)

*Figura 44. Habilitar y configurar UFW. Fuente: elaboración propia.*

**▸**

- Permitiremos el tráfico SSH a través del firewall. Es fundamental ejecutarlo en todos los nodos del clúster que necesiten acceso SSH desde fuera de la red local. Es común que los administradores de sistemas necesiten acceder a los nodos del clúster mediante SSH para la administración y el mantenimiento.

- Permitiremos el tráfico TCP en el puerto 80, que es el puerto estándar utilizado para HTTP. Debes ejecutar este comando en todos los nodos del clúster donde desees permitir el acceso a los servicios web que escuchen en el puerto 80.

## 2. Configurar AppArmor:

**▸**

![Figura 45. Habilitar AppArmor. Fuente: elaboración propia. • Habilitar AppArmor:](images/image-51.png)

*Figura 45. Habilitar AppArmor. Fuente: elaboración propia.*

AppArmor es un sistema de seguridad de acceso obligatorio *(mandatory access* *control,* MAC) para Linux. Su objetivo principal es reforzar la seguridad al limitar las acciones que programas específicos pueden realizar en el sistema, según los perfiles de seguridad predefinidos. AppArmor se configura utilizando perfiles que especifican a qué recursos (archivos, directorios, puertos de red, etc.) puede acceder una aplicación y en qué modos (lectura, escritura, ejecución, etc.).

**Evaluación:**

1. Pruebas de failover: son procedimientos diseñados para verificar la capacidad de

un sistema o servicio para gestionar una conmutación automática *(failover)* de recursos críticos a un nodo de respaldo en caso de que el nodo principal falle o experimente problemas. Estas pruebas son una parte crucial de la estrategia de alta disponibilidad en sistemas informáticos y de red.

**▸**

- Apagar uno de los nodos y verificar que el otro nodo toma el control del servicio.

- Verificar el funcionamiento del servicio web al acceder a la IP virtual.

## 2. Revisión de seguridad:

**▸**

- Verificar que solo los puertos necesarios están abiertos.

- Asegurarse de que AppArmor está activo y no genera errores de acceso.

**Conclusión:**

Al finalizar esta actividad, los participantes habrán configurado un clúster básico de alta disponibilidad con medidas de seguridad, con lo que comprenderán los conceptos de *failover* y la importancia de proteger los servicios críticos en un entorno de producción.

1. ¿Cuál es el objetivo principal de la alta disponibilidad en los sistemas

informáticos?

    - A. Aumentar la capacidad de almacenamiento.

    - B. Minimizar el tiempo de inactividad.

    - C. Reducir el consumo de energía.

    - D. Mejorar la interfaz de usuario.

2. ¿Qué tecnología combina el striping de RAID 0 con el mirroring de RAID 1?

    - A. RAID 3.

    - B. RAID 5.

    - C. RAID 6.

    - D. RAID 10.

3. ¿Qué es una SAN?

    - A. Un dispositivo de almacenamiento directo.

    - B. Una red de alta velocidad que está dedicada a conectar los servidores con

el almacenamiento.

    - C. Un software de copia de seguridad.

    - D. Una tecnología de virtualización.

4. ¿Cuál es una de las principales desventajas de la tecnología RAID?

    - A. Incrementa la capacidad de almacenamiento.

    - B. No requiere conocimientos técnicos.

    - C. Puede ser costosa y compleja de gestionar.

    - D. Siempre ofrece la misma velocidad de rendimiento.

5. ¿Qué tipo de almacenamiento es más adecuado para compartir archivos en una

red?

    - A. DAS.

    - B. SAN.

    - C. NAS.

    - D. RAID.

6. ¿Qué tecnología permite que múltiples máquinas virtuales operen en un solo

servidor físico?

    - A. Virtualización de almacenamiento.

    - B. Virtualización de redes.

    - C. Virtualización de escritorios.

    - D. Virtualización de servidores.

7. ¿Qué nivel de RAID distribuye datos y un bloque de paridad entre tres o más

discos?

    - A. RAID 0.

    - B. RAID 1.

    - C. RAID 5.

    - D. RAID 6.

8. ¿Cuál de las siguientes opciones es una ventaja de usar una SAN?

    - A. Baja velocidad de transferencia.

    - B. Escalabilidad.

    - C. Dependencia de la red.

    - D. Configuración compleja.

9. ¿Cuál es la principal función de la virtualización de escritorios?

    - A. Mejorar la conectividad de red.

    - B. Permitir el acceso a escritorios personales desde cualquier dispositivo.

    - C. Aumentar la capacidad de almacenamiento.

    - D. Facilitar la administración de discos duros.

10. ¿Qué tipo de RAID es más adecuado para aplicaciones que requieren alta

velocidad y seguridad?

    - A. RAID 0.

    - B. RAID 1.

    - C. RAID 5.

    - D. RAID 10.

11. ¿Qué característica define a una NAS?

    - A. Alta velocidad de transferencia mediante fibra óptica.

    - B. Conecta directamente el almacenamiento a los servidores.

    - C. Almacenamiento y recuperación de datos a través de una red.

    - D. Utilizar una tecnología de virtualización avanzada.

12. ¿Cuál es una ventaja de la virtualización?

    - A. Requiere hardware adicional especializado.

    - B. Introduce un alto overhead de rendimiento.

    - C. Mejora la eficiencia de los recursos.

    - D. Aumenta la complejidad de la gestión.

13. ¿Qué nivel de RAID permite la reconstrucción de datos incluso si fallan dos

discos?

    - A. RAID 0.

    - B. RAID 1.

    - C. RAID 5.

    - D. RAID 6.

14. ¿Cuál es una desventaja de la implementación de SAN?

    - A. Alto costo.

    - B. Fácil configuración.

    - C. Baja velocidad de transferencia.

    - D. Poca flexibilidad.

15. ¿Qué nivel de RAID no ofrece redundancia?

    - A. RAID 0.

    - B. RAID 1.

    - C. RAID 5.

    - D. RAID 6.

16. ¿Cuál es un componente clave en una arquitectura SAN?

    - A. Controladores RAID.

    - B. Switches de fibra óptica.

    - C. Discos duros internos.

    - D. Tarjetas gráficas.

17. ¿Qué ventaja ofrece un NAS sobre otros sistemas de almacenamiento?

    - A. Dependencia mínima de la red.

    - B. Acceso remoto.

    - C. Requiere hardware especializado.

    - D. Baja capacidad de almacenamiento.

18. ¿Cuál es una desventaja de la virtualización?

    - A. Reducción de los costos iniciales.

    - B. Overhead de rendimiento.

    - C. Mejora en la gestión.

    - D. Aislamiento de aplicaciones.

19. ¿Qué tipo de almacenamiento se utiliza comúnmente para bases de datos y

aplicaciones críticas?

    - A. NAS.

    - B. SAN.

    - C. DAS.

    - D. RAID 0.

20. ¿Cuál es una ventaja de implementar RAID 5?

    - A. No requiere discos adicionales.

    - B. Ofrece redundancia con paridad.

    - C. Máximo rendimiento sin redundancia.

    - D. Alta capacidad de almacenamiento sin pérdida de rendimiento.

21. ¿Qué nivel de RAID requiere al menos cuatro discos y utiliza el 50 % del

almacenamiento total?

    - A. RAID 0.

    - B. RAID 1.

    - C. RAID 5.

    - D. RAID 10.

22. ¿Qué protocolo se utiliza comúnmente en una SAN?

    - A. FTP.

    - B. Fibre channel.

    - C. HTTP.

    - D. SMTP.

23. ¿Cuál es una desventaja de los sistemas NAS?

    - A. Alta velocidad de transferencia.

    - B. Configuración compleja.

    - C. Fácil acceso remoto.

    - D. Costo bajo.

24. ¿Qué es lo que permite consolidar múltiples sistemas en un solo servidor físico?

    - A. RAID 5.

    - B. NAS.

    - C. Virtualización.

    - D. SAN.

25. ¿Cuál es un beneficio de la virtualización de almacenamiento?

    - A. Incrementa la necesidad de hardware adicional.

    - B. Mejora la eficiencia y la escalabilidad de los datos.

    - C. Reduce la necesidad de gestión centralizada.

    - D. Limita la capacidad de almacenamiento.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.5–31)*
- A fondo  *(pp.32–38)*
- Entrenamientos  *(pp.39–75)*
- Test  *(pp.76–82)*
- Seguridad y Alta Disponibilidad 5 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 6 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 7 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 8 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 9 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 10 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 11 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 12 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 13 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 14 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 16 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 18 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 19 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 20 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 21 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 22 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 23 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 24 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 25 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 27 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 28 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 29 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 30 Tema 9. Material de estudio · Seguridad y Alta Disponibilidad 31 Tema 9. Material de estudio  *(pp.5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 16, 18, 19, 20, 21, 22, 23, 24, 25, 27, 28, 29, 30, 31)*
- Seguridad y Alta Disponibilidad 32 Tema 9. A fondo · Seguridad y Alta Disponibilidad 33 Tema 9. A fondo · Seguridad y Alta Disponibilidad 34 Tema 9. A fondo · Seguridad y Alta Disponibilidad 35 Tema 9. A fondo · Seguridad y Alta Disponibilidad 36 Tema 9. A fondo · Seguridad y Alta Disponibilidad 37 Tema 9. A fondo · Seguridad y Alta Disponibilidad 38 Tema 9. A fondo  *(pp.32–38)*
- Seguridad y Alta Disponibilidad 39 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 40 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 41 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 42 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 43 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 44 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 45 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 46 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 47 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 48 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 49 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 50 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 51 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 52 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 53 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 55 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 56 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 57 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 58 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 59 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 60 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 61 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 62 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 63 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 64 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 66 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 67 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 68 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 69 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 70 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 71 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 73 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 74 Tema 9. Entrenamientos · Seguridad y Alta Disponibilidad 75 Tema 9. Entrenamientos  *(pp.39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 66, 67, 68, 69, 70, 71, 73, 74, 75)*
- ▸ Solución  *(pp.40, 44, 49, 54)*
- Seguridad y Alta Disponibilidad 76 Tema 9. Test · Seguridad y Alta Disponibilidad 77 Tema 9. Test · Seguridad y Alta Disponibilidad 78 Tema 9. Test · Seguridad y Alta Disponibilidad 79 Tema 9. Test · Seguridad y Alta Disponibilidad 80 Tema 9. Test · Seguridad y Alta Disponibilidad 81 Tema 9. Test · Seguridad y Alta Disponibilidad 82 Tema 9. Test  *(pp.76–82)*