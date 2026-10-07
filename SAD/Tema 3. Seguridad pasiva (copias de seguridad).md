## Tema 3

# Seguridad y Alta Disponibilidad

# Tema 3. Seguridad pasiva (copias de seguridad)

# Índice

Esquema Material de estudio

## 3.1. Introducción y objetivos

## 3.2. Copias de seguridad

## 3.3. Frecuencia de las copias de backup

## 3.4. Política de copias de seguridad

## 3.5. Referencias bibliográficas

A fondo Tipos de copias de seguridad Los 8 mejores programas de copia de seguridad gratis para Windows

Cómo hacer copias de seguridad en la nube

Copias de seguridad (Incibe, 2024)

Recuperación de archivos

Entrenamientos Entrenamiento 1: estrategia de copia de seguridad Entrenamiento 2: implementación y gestión de copias de seguridad con Bacula Entrenamiento 3: copia de seguridad basada en las torres de Hanoi Entrenamiento 4: copia de backup en Windows Entrenamiento 5: copia de backup en Ubuntu con herramientas de sistema

# Esquema

![image-2](images/image-2.png)

Seguridad y Alta Disponibilidad 3 Tema 3. Esquema

# 3.1. Introducción y objetivos

La seguridad de los datos es una preocupación central en el mundo digital actual. Ante la posibilidad de pérdida, daño o corrupción de la información almacenada en nuestros dispositivos, las copias de seguridad se erigen como una salvaguarda esencial. Este documento explora en detalle qué son las copias de seguridad, cómo se estructuran, qué tipos existen y cuáles son las mejores prácticas para su implementación.

Desde la selección de datos críticos hasta la elección del método de almacenamiento y los tipos de copias más adecuados para cada situación, esta guía ofrece un completo panorama para garantizar la integridad y la disponibilidad de la información ante cualquier eventualidad. Además, se analizan las diferencias entre copias diferenciales e incrementales, así como recomendaciones específicas según el volumen de datos y la frecuencia de actualización. Por último, se examinan las opciones de almacenamiento y se destacan los servicios de copias de seguridad en línea como una alternativa moderna y conveniente. En resumen, esta introducción brinda una visión integral sobre la **importancia** y la **implementación efectiva** de las **copias de seguridad** en el entorno digital actual.

Los objetivos que se pretende alcanzar en este tema son:

**▸** Comprender la importancia de las copias de seguridad.

**▸** Tomar conocimiento de los tipos y métodos de copia de seguridad.

**▸** Identificar las mejores prácticas.

**▸** Comprender las diferencias entre copias diferenciales e incrementales.

**▸** Implementar políticas de respaldo diario.

**▸** Evaluar las ventajas y desventajas de diferentes programaciones. **▸** Seleccionar la estrategia de respaldo adecuada. **▸** Optimizar la restauración de datos. **▸** Reconocer la importancia de las consideraciones legales. **▸** Apreciar la naturaleza continua de la seguridad informática.

# 3.2. Copias de seguridad

Definición de copia de seguridad

La información en nuestro equipo puede dañarse o incluso perderse. Las copias de seguridad (o también llamadas copias de *backups),* son réplicas de datos o información relevante que nos permiten **recuperar la información original** cuando esta se ha perdido o estropeado.

«Uno de los principios de seguridad: "Ordenar de mayor a menor prioridad qué archivos, datos y configuraciones son difíciles de volver a realizar o recuperar, y mantener de forma segura copias de seguridad de los mismos, distribuidas en espacio y tiempo"» (Santos, 2014).

Es fundamental que cada usuario identifique y seleccione los datos que, por su importancia, deben incluirse en las copias de seguridad. Esto asegura que la **información crucial esté protegida** en caso de fallos del sistema, ataques cibernéticos o cualquier otra eventualidad que pueda comprometer la integridad de los datos. Las copias de seguridad pueden almacenarse en varios medios, dependiendo de las necesidades y recursos disponibles, como:

**▸ Soportes extraíbles:** CD, DVD, pendrives, cintas de *backup,* etc.

**▸ Ubicaciones locales:** otros directorios o particiones en la misma máquina.

**▸ Ubicaciones de red:** unidades compartidas en otros equipos o discos de red.

**▸ Servidores remotos:** almacenamiento en la nube u otros servidores accesibles a través de Internet (lo veremos en un apartado posterior).

Para garantizar la seguridad y la facilidad de gestión de las copias de seguridad, es recomendable que estos archivos se encuentren **cifrados y comprimidos** en un único archivo. Esto no solo asegura la confidencialidad de los datos almacenados, sino que también facilita su mantenimiento y distribución. A continuación, se describen algunos de los pasos y consideraciones clave para realizar copias de seguridad efectivas:

**▸ Identificación de los datos críticos:** determinar qué archivos y datos son esenciales para las operaciones y la continuidad del negocio o las actividades del usuario.

**▸ Elección del medio de almacenamiento:** seleccionar el soporte más adecuado en función de la cantidad de datos, la frecuencia de las copias de seguridad y el presupuesto disponible.

**▸ Frecuencia de las copias de seguridad:** establecer un horario regular para la realización de copias de seguridad, ya sea diaria, semanal, o según la necesidad específica.

**▸ Cifrado de datos:** utilizar herramientas y métodos de cifrado para proteger la información sensible y asegurarse de que solo las personas autorizadas puedan acceder a los datos respaldados.

**▸ Compresión de archivos:** comprimir los datos en un solo archivo para ahorrar espacio y facilitar la transferencia y almacenamiento.

**▸ Pruebas de restauración:** realizar pruebas periódicas de restauración para asegurarse de que los datos respaldados pueden recuperarse de manera efectiva en caso de necesidad.

**▸ Mantenimiento y rotación de medios:** mantener los medios de almacenamiento en buen estado y rotarlos periódicamente para evitar la degradación y pérdida de datos.

Siguiendo estas recomendaciones, se puede asegurar que las copias de seguridad son efectivas, confiables y están disponibles cuando se necesiten.

Medios de almacenamiento externo

Las políticas de almacenamiento y los medios de almacenamiento externo son componentes cruciales en la gestión de datos dentro de una organización. Aquí te proporciono un resumen sobre los diferentes tipos de medios de almacenamiento externo y las estrategias de copias de seguridad e imágenes de respaldo.

**▸** ***Direct attached storage*** **(DAS):** el almacenamiento conectado directamente se refiere a los dispositivos de almacenamiento que están conectados directamente a una computadora o servidor individual a través de interfaces como USB, SCSI, SATA, o SAS.

**▸** ***Network attached storage*** **(NAS):** el almacenamiento conectado a la red es un dispositivo de almacenamiento dedicado que se conecta a una red y proporciona acceso de almacenamiento a varios dispositivos en la red.

**▸** ***Storage Area Network*** **(SAN):** la red del área de almacenamiento es una red especializada de alta velocidad que proporciona acceso al almacenamiento consolidado y permite que varios servidores accedan a dispositivos de almacenamiento.

![image-3](images/image-3.png)

Tabla 1. Comparativa entre los diferentes medios de almacenamiento externo. Fuente: elaboración propia.

Tipos de copias de seguridad

Al elegir el tipo de copia de seguridad por realizar, es crucial comprender las **características y beneficios** de cada tipo para adecuarse a las necesidades específicas de la organización o del usuario. A continuación, se detallan los tipos de copias de seguridad mencionados:

**▸ Copia de seguridad completa, total o íntegra:** esta copia de seguridad incluye todos los archivos y directorios seleccionados, independientemente de si han cambiado desde la última copia de seguridad o no.

**▸ Copia de seguridad incremental:** en esta modalidad, solo se copian los archivos que han cambiado desde la última copia de seguridad, sea del tipo que sea (completa o incremental).

**▸ Copia de seguridad diferencial:** esta copia de seguridad incluye todos los archivos que han cambiado desde la última copia de seguridad completa.

Diferencias entre la diferencial y la incremental

La **diferencial** guarda **todos los datos** desde la última copia total: todo se guarda en la última copia diferencial, por eso necesitamos solo la última copia diferencial y la copia total.

La **incremental** guarda lo modificado de la última copia (ya sea total u otra copia), es decir, solo guarda **lo que ha cambiado** desde la última copia (si se hizo anteriormente una copia incremental, la siguiente solo guarda la diferencia con respecto a esta última y no con respecto a la copia total), por eso se necesita disponer de la copia total y todas las incrementales intermedias.

![Figura 1. Tipos de Backup. Fuente: de la Cuesta, 2016.](images/image-4.png)

*Figura 1. Tipos de Backup. Fuente: de la Cuesta, 2016.*

![image-5](images/image-5.png)

Tabla 2. Comparativa entre los diferentes tipos de copia. Fuente: elaboración propia.

Recomendaciones

Realizar copias de seguridad es esencial para asegurar la protección de los datos. A continuación, se presentan recomendaciones sobre el tipo de copia para efectuar según el volumen de datos y la frecuencia de modificaciones:

**▸ Volumen de datos bajo** (menos de 4 GB):

- Copia total: dado que el volumen de datos no es elevado, lo más práctico es realizar copias totales. Esto facilita la recuperación en caso de desastre, ya que solo se necesita la última copia total para restaurar todos los datos.

**▸ Volumen de datos elevado** (mayor de 50 GB) **con pocos cambios** (alrededor de 4 GB): la primera es copia total, luego copias diferenciales.

- Copia total inicial: realizar una copia total al comienzo.

- Copias diferenciales subsecuentes: estas copias almacenan solo los datos que han cambiado desde la última copia total. En caso de desastre, se debe recuperar la copia total inicial y la última copia diferencial.

- Copia total periódica: realizar copias totales periódicamente para reducir la dependencia de múltiples copias diferenciales y evitar que las diferenciales crezcan demasiado.

**▸ Volumen de datos elevado** (mayor de 50 GB) **con cambios frecuentes:** la primera es copia total, luego copias incrementales.

- Copia total inicial: realizar una copia total al inicio.

- Copias incrementales subsecuentes: estas copias almacenan solo los datos que han cambiado desde la última copia (total o incremental). Son más eficientes en términos de espacio, pero en caso de desastre, se necesita recuperar la última copia total y todas las copias incrementales realizadas desde entonces.

- Copia total más frecuente: para evitar mantener un número excesivo de copias incrementales, es recomendable realizar copias totales más frecuentemente. Esto facilita la recuperación y reduce el riesgo de fallo en la restauración debido a una larga cadena de copias incrementales.

![image-6](images/image-6.png)

Tabla 3. Métodos de copia. Fuente: elaboración propia.

La estrategia para realizar copias de seguridad viene condicionada por una serie de factores para tener en cuenta:

**▸** La frecuencia de realización.

**▸** El volumen de datos para copiar.

**▸** La disponibilidad de la copia.

**▸** El tiempo de recuperación del sistema.

Una debida planificación de copias de seguridad nos permite mantener una organización de las copias. La política de copias de seguridad debe garantizar la reconstrucción de los ficheros en caso de fallo del sistema.

Copias de seguridad online

Las copias de seguridad *online,* también conocidas como copias de seguridad en la nube, son una forma de proteger tus datos al **almacenarlos en servidores remotos** accesibles a través de Internet. Este método ofrece varias ventajas sobre las copias de seguridad tradicionales locales, como la accesibilidad, la seguridad y la redundancia.

Existe una multitud de empresas que ofrecen servicios de copias de seguridad online.

![image-7](images/image-7.png)

Tabla 4. Comparativa de los proveedores de *backup* en la nube más habituales. Los datos son del 2024. Fuente: elaboración propia.

# 3.3. Frecuencia de las copias de backup

Frecuencia de backup

Ya hemos habado de los diferentes tipos de copias de seguridad (total, incremental, diferencial, etc.), pero de lo que no hemos hablado es de que existen diferentes niveles de profundidad de copia que se pueden aplicar a estos. A continuación, se detallan los niveles de profundidad más utilizados:

**▸ Nivel 0 o total:** copia total del sistema, idéntica a la modalidad de copia de seguridad total. Se suele usar de base para las copias de nivel superior.

**▸ Nivel 1:** copia incremental que respalda todos los datos modificados o creados desde la última copia de nivel 0. Permite un respaldo más frecuente sin duplicar la información que ya se ha respaldado.

**▸ Niveles 2-9:** cada nivel realiza una copia de los datos modificados o creados desde la última copia de menor nivel más cercana. Por ejemplo, en una secuencia 0, 3, 2, la copia de nivel 2 respalda los datos cambiados desde la copia de nivel 0.

Proporciona flexibilidad en la programación de respaldos, lo que permite ajustes según la criticidad de los datos y los recursos disponibles.

Es fundamental **realizar copias diariamente** para minimizar la pérdida de datos. Para ello debemos determinar las horas de menor actividad para ejecutar las copias y minimizar el impacto en el rendimiento

del sistema. Deberíamos definir una

secuencia de niveles que optimice el uso del espacio y facilite la recuperación. Por ejemplo, podría establecerse una copia de nivel 0 semanalmente, con copias de nivel 1 diariamente y de niveles 2-9 según la necesidad específica.

Ejemplos de tipos de programaciones

Existen diversas modalidades de copias de profundidad que se pueden aplicar, lo cual

seguridad y distintos niveles de permite una amplia variedad de

combinaciones para programar las copias. A continuación, se describen algunas de las más comunes y eficaces, aunque es importante recordar que la elección de la modalidad adecuada dependerá de las necesidades específicas de cada situación.

![Figura 2. Tipo1. Copias totales. Fuente: elaboración propia. Tipo 1. Programación de copias totales](images/image-8.png)

*Figura 2. Tipo1. Copias totales. Fuente: elaboración propia.*

En este caso, la programación utilizada es de **un solo nivel,** ya que se realizan copias completas, o de nivel 0, todos los días de la semana en volúmenes distintos. Este método proporciona una seguridad total, pero a un costo elevado, ya que el volumen de datos copiados aumenta diariamente y se requieren siete volúmenes diferentes para almacenar cada copia diaria. Cada día de la semana se realizará una copia que borrará la copia que existe de ese mismo día la semana anterior. Esta programación solo se recomienda para sistemas de tamaño medio a grande.

![image-9](images/image-9.png)

Tabla 5. Programación semanal con copias totales. Fuente: elaboración propia.

#### Tipo 2. Copia total semanal con copias diferenciales de nivel 1

![Figura 3. Tipo 2. Copia total y diferenciales. Fuente: elaboración propia.](images/image-10.png)

*Figura 3. Tipo 2. Copia total y diferenciales. Fuente: elaboración propia.*

Con este tipo de copias, a principios de semana se realiza una copia completa, de nivel 0, y los días restantes se llevan a cabo copias de seguridad diferenciales de nivel 1. Así, solo se necesitan **dos volúmenes para la restauración:** uno para la copia total semanal y otro para la última copia diferencial válida, ya que las copias de nivel 1 almacenan todos los datos modificados o creados desde la última copia completa.

Este método es ideal si no se utilizan aplicaciones que gestionen los volúmenes, ya que solo se requieren dos. Ofrece **dos ventajas principales:** primero, facilita la restauración completa de datos al usar únicamente dos volúmenes y, segundo, proporciona múltiples copias de los archivos modificados a lo largo de la semana, lo que simplifica la recuperación de datos parciales.

![image-11](images/image-11.png)

Tabla 6. Programación semanal con copias diferenciales de nivel 1. Fuente: elaboración propia.

#### Tipo 3. Copia total semanal con copias incrementales

![Figura 4. Tipo 3. Copia total e incrementales. Fuente: elaboración propia.](images/image-12.png)

*Figura 4. Tipo 3. Copia total e incrementales. Fuente: elaboración propia.*

En este método se realiza una copia total el primer día de la semana, seguida de copias incrementales durante los seis días siguientes. Cada copia incremental guarda los datos modificados o creados desde la última copia incremental o, si no existe, desde la última copia total.

La principal ventaja de este enfoque es que las copias incrementales diarias suelen ser rápidas de realizar. No obstante, hay un **riesgo asociado:** si alguna de las copias incrementales se corrompe, se pueden perder varios días de datos, ya que las copias están encadenadas. Además, el proceso de restauración en caso de un desastre es más lento porque se debe comenzar con la última copia total y luego restaurar cada copia incremental en orden. Por el contrario, las restauraciones parciales de datos son rápidas.

![image-13](images/image-13.png)

Tabla 7. Programación semanal con copias incrementales diarias. Fuente: elaboración propia.

![Figura 5. Tipo 4. Copia total, diferencial e incrementales. Fuente: elaboración propia. Tipo 4. Copia total, diferencial e incrementales](images/image-14.png)

*Figura 5. Tipo 4. Copia total, diferencial e incrementales. Fuente: elaboración propia.*

La programación de copias de seguridad en este caso emplea los **tres modelos más** **comunes:** total, incremental y diferencial.

El primer día de la semana se realiza una copia total del sistema, seguido de tres días de copias incrementales. El jueves se realiza una copia diferencial que guarda todos los datos modificados o creados desde la última copia total, es decir, desde el domingo.

Finalmente, se llevan a cabo copias incrementales el viernes y el sábado, con lo que se respaldan los datos modificados o creados el jueves y el viernes, respectivamente. Esta secuencia se repite todas las semanas siguientes.

Esta programación permite **distribuir el volumen de datos** para restaurar en caso de desastre. En la siguiente tabla se pueden ver los archivos de respaldo necesarios según el día de la semana en el que se realiza la restauración.

![image-15](images/image-15.png)

Tabla 8. Copias necesarias cada día. Fuente: elaboración propia.

![image-16](images/image-16.png)

Tabla 9. Programación semanal con copia total, diferencial e incremental diarias. Fuente: elaboración

propia.

#### Tipo 5. Copias multinivel. Método torre de Hanoi

Si pretendes gestionar **múltiples volúmenes y niveles** de manera eficiente, una de las programaciones más interesantes y que consume menos tiempo y recursos es la utilización de copias de seguridad multinivel, especialmente siguiendo el método conocido como torre de Hanoi.

La programación relacionada con la torre de Hanoi **se basa en un juego de lógica** creado en 1883 por el matemático francés Édouard Lucas (1842-1891). El juego consta de tres postes verticales. En uno de ellos se apilan varios discos de madera de diferentes tamaños para formar una torre escalonada en forma de pirámide, con el

Seguridad y Alta Disponibilidad 20 Tema 3. Material de estudio disco más grande en la base y el más pequeño en la parte superior. El objetivo del juego es trasladar la torre de discos de un poste a otro, cumpliendo con ciertas reglas:

**▸** Solo se puede mover un disco a la vez.

**▸** Un disco no puede colocarse sobre otro de menor tamaño.

**▸** Solo se puede mover el disco que está en la parte superior de cada poste.

![Figura 6. Juego torres de Hanoi. Fuente: Croce Busquets, 2011.](images/image-17.png)

*Figura 6. Juego torres de Hanoi. Fuente: Croce Busquets, 2011.*

![Figura 7. Juego torres de Hanoi. Fuente: Espada, 2011.](images/image-18.png)

*Figura 7. Juego torres de Hanoi. Fuente: Espada, 2011.*

**Solución.** Da igual el número de anillos del que partamos, siempre seguiremos la siguiente secuencia: moveremos el anillo superior (el más pequeño) cada dos movimientos (1, 3, 5, 7, 9…), el siguiente anillo cada cuatro movimientos (2, 6, 10, 14…), el tercer anillo cada ocho movimientos (4, 12, 20, 28…), el cuarto anillo cada 16 movimientos (8, 24, 32, 40…) y así sucesivamente. De esta manera conseguiremos resolver el problema en el menor número de pasos.

La programación de copias de seguridad siguiendo la resolución de las torres de Hanoi **utiliza el mismo patrón,** pero en vez de movimientos de anillos tendremos sesiones y en lugar de anillos, tendremos niveles de copias.

Con una torre de Hanoi de cuatro niveles de copia (cuatro anillos siguiendo con el símil), se puede establecer una programación que cubra ocho sesiones de copias.

Esta estrategia, debido a su complejidad, requiere el uso de ***software*** **especializado** **en copias de seguridad** (como puede ser Acronis Backup, que contempla la posibilidad de implementar el método de torres de Hanoi) para gestionarlas adecuadamente.

Es especialmente útil para pequeñas empresas en las que se quiera optimizar el coste (ya que es más económica en términos de uso de recursos) y que, sin embargo, necesitan realizar restauraciones completas de sus sistemas de datos cuando sea necesario (ganamos en coste a base de sacrificar la disponibilidad diaria de la restauración de la copia).

Queremos una copia diaria (que empiece en el día 1), que existan cuatro niveles y que el tipo sea completa/diferencial/incremental. La secuencia de copias será la siguiente:

![image-19](images/image-19.png)

Tabla 10. Secuencia torres de Hanoi-1. 4 niveles. Fuente: elaboración propia.

Las copias de seguridad de último nivel (4) son completas, las de los niveles intermedios (2 y 3) son diferenciales y las de primer nivel (1) son incrementales. La secuencia continuaría en el tiempo.

Por defecto, una copia de seguridad no se eliminará mientras tenga otras copias que dependan de ella. Por ejemplo, si quisiera eliminar una copia de seguridad completa, pero hay copias incrementales o diferenciales que dependen de ella, la eliminación se retrasará hasta que todas las copias dependientes puedan ser eliminadas.

Así, por ejemplo, si hoy fuera el día 8 (antes de realizar una nueva copia completa) se mantendrán las siguientes copias (en blanco se muestra las copias borradas).

![image-20](images/image-20.png)

Tabla 11. Secuencia torres de Hanoi-2. 4 niveles. Fuente: elaboración propia.

Se ve que se almacenan más copias de seguridad cuanto más cerca estemos de la fecha actual. En este punto disponemos de 4 copias (días 1, 5, 7 y 8) con lo que podremos recuperar los datos de hoy, de ayer, de hace media semana y de hace una semana.

En este punto podemos hablar del **período de recuperación,** que es el número de días garantizado que podemos recuperar una copia de seguridad. En la situación anterior teníamos cuatro días.

En función del número de niveles que elijamos al realizar la copia (a más niveles, más complejidad), tendremos diferentes valores para el período de recuperación:

![image-21](images/image-21.png)

Tabla 12. Secuencia torres de Hanoi. Período de recuperación. Fuente: elaboración propia.

Para entender la columna referente a «en días diferentes, puedo volver atrás», supongamos que nos encontramos en el día 12 del ejemplo anterior.

![image-22](images/image-22.png)

Tabla 13. Secuencia torres de Hanoi-3. 4 niveles. Fuente: elaboración propia.

En este punto, aún no se ha creado una copia diferencial de nivel 3, por lo que la copia diferencial del día 5 sigue almacenada y, como esta depende de la copia total del día 1, esta última también aparece disponible. Por lo tanto, podemos retroceder 11 días y recuperar la copia de ese día. Esta sería la situación más favorable para un número de niveles de 4.

Si nos situamos en el día siguiente, como en ese momento se realiza una copia diferencial nivel 3, se elimina la copia diferencial de nivel 3 del día 5 (y en consecuencia la copia total del día 1).

![image-23](images/image-23.png)

Tabla 14. Secuencia torres de Hanoi-4. 4 niveles. Fuente: elaboración propia.

En este escenario tenemos un intervalo de recuperación de 4 días, por lo cual, esta es la situación más desfavorable.

Este esquema mantiene la estructura jerárquica de las copias de seguridad y facilita la eliminación de copias innecesarias al seguir la lógica de dependencias del método de las torres de Hanoi.

# 3.4. Política de copias de seguridad

Implementar una buena política de copias de seguridad es fundamental para asegurar la protección y la recuperación de datos críticos en caso de pérdida, corrupción o fallo del sistema. A continuación, se presenta una guía resumen para la implementación de una política de copias de seguridad:

Evaluación inicial

**▸ Identificación de datos críticos:**

- Determinar qué datos son críticos para la operación del negocio.

- Clasificar los datos en niveles de importancia.

**▸ Requerimientos de retención:**

- Definir por cuánto tiempo deben mantenerse las copias de seguridad.

- Considerar los requisitos legales y normativos.

**▸ Evaluación de riesgos:**

- Identificar las posibles amenazas y vulnerabilidades.

- Evaluar el impacto potencial de la pérdida de datos.

Definición de la política de copias de seguridad

**▸ Objetivos de la política:**

- Establecer los objetivos principales de la política de copias de seguridad.

- Asegurar la integridad, la disponibilidad y la confidencialidad de los datos.

**▸ Frecuencia de las copias de seguridad:**

- Definir la periodicidad de las copias (diarias, semanales, mensuales).

- Ajustar la frecuencia según la criticidad de los datos.

**▸ Tipos de copias de seguridad:**

- Completa: copia de todos los datos.

- Incremental: copia de los datos que han cambiado desde la última copia.

- Diferencial: copia de los datos que han cambiado desde la última copia completa.

**▸ Medios de almacenamiento:**

- Dispositivos locales (discos duros, NAS).

- Almacenamiento en la nube.

- Soportes externos (cintas, discos externos).

**▸ Retención y rotación:**

- Establecer períodos de retención para cada tipo de copia.

- Implementar esquemas de rotación (por ejemplo, el esquema de abuelo-padre-hijo).

Implementación de la técnica

**▸ Herramientas y software:**

- Seleccionar el software de copias de seguridad adecuado.

- Asegurar la compatibilidad con los sistemas y aplicaciones existentes.

**▸ Configuración y automatización:**

- Configurar el software para realizar copias de seguridad según la política definida.

- Programar tareas de copias de seguridad automáticas.

**▸ Seguridad de las copias:**

- Encriptar las copias de seguridad para proteger la información confidencial.

- Implementar controles de acceso para garantizar que solo el personal autorizado pueda acceder a las copias.

Pruebas y verificación

**▸ Pruebas regulares:**

- Realizar pruebas periódicas de restauración para asegurarse de que las copias de seguridad son funcionales.

- Documentar los resultados de las pruebas.

**▸ Monitoreo y auditoría:**

- Monitorear las copias de seguridad para identificar fallos y errores.

- Realizar auditorías periódicas para asegurar el cumplimiento de la política.

Mantenimiento y actualización

**▸ Revisión periódica:**

- Revisar y actualizar la política de copias de seguridad regularmente.

- Adaptar la política a los cambios en la infraestructura, las tecnologías y las necesidades del negocio.

**▸ Capacitación:**

- Capacitar al personal en la política de copias de seguridad.

- Asegurar que todos entienden su rol en el proceso de copias de seguridad.

#### Ejemplo de política de copias de seguridad

**Objetivo:** garantizar la disponibilidad y recuperación de los datos críticos de la organización.

**Alcance:** esta política aplica a todos los sistemas y datos críticos identificados por la organización.

**Frecuencia:**

**▸** Copias de seguridad diarias de los datos transaccionales.

**▸** Copias de seguridad semanales de los datos operativos.

**▸** Copias de seguridad mensuales de todos los datos (copia completa).

**Retención:**

**▸** Copias diarias: una semana.

**▸** Copias semanales: un mes.

**▸** Copias mensuales: un año.

**Medios de almacenamiento:**

**▸** Copias diarias y semanales: almacenamiento en la nube.

**▸** Copias mensuales: soporte externo (almacenado fuera del sitio).

**Seguridad:**

**▸** Encriptación AES-256 para todas las copias de seguridad.

**▸** Control de acceso basado en roles para el acceso a las copias.

**Procedimientos de pruebas:**

**▸** Pruebas de restauración trimestrales.

**▸** Monitoreo continuo y auditorías anuales.

Implementar una política de copias de seguridad robusta y efectiva requiere una planificación cuidadosa y un compromiso continuo con la revisión y mejora del proceso. Asegurarse de que todos los empleados comprendan y sigan esta política es crucial para proteger los datos críticos de la organización.

# 3.5. Referencias bibliográficas

Croce Busquets, J. I. (2011). *Torres de Hanoi* [imagen]. [https://www.flickr.com/photos/jose_croce/5338808993/](https://www.flickr.com/photos/jose_croce/5338808993/) De la Cuesta, O. (2016). *Backup Total – incremental – diferencial* [gráfico]. Obtenido de <https://www.palentino.es/blog/backup-total-incremental-diferencial/> Espada, R. (2011). *Jogos matemáticos II - Torre de Hanoi* [imagen]. <https://becreesct.blogspot.com/2011/12/jogos-matematicos-ii-torre-de-hanoi.html> Santos, J. C. (2014). Mantenimiento de la Seguridad en sistemas informáticos. Ra- Ma.

# Tipos de copias de seguridad

JGAITPro. (2015, febrero 20). *Tipos de copias de seguridad - Completa, incremental* *y diferencial* [vídeo]. YouTube. [https://www.youtube.com/watch?v=Tt8v9CCdkYY](https://www.youtube.com/watch?v=Tt8v9CCdkYY)

Si te quedan dudas sobre cómo diferenciar los diferentes tipos de copias, te invito a que veas este vídeo.

![image-24](images/image-24.png)

Accede al vídeo: [https://www.youtube.com/embed/Tt8v9CCdkYY](https://www.youtube.com/embed/Tt8v9CCdkYY)

# para Windows [actualizado el 23 de julio de 2024]. Easeus.

# gratis.html

# Los 8 mejores programas de copia de seguridad

# gratis para Windows

Pedro. (2023, octubre 25). Los 8 mejores programas de copia de seguridad gratis <https://es.easeus.com/backup-recovery/mejores-programas-copia-de-seguridad->

Puedes elegir el programa de copia de seguridad que más te convenga… y gratis. En este sitio web encontrarás varios programas con una indicación para cada uno sobre sus pros y sus contras.

# seguridad/nube

# Cómo hacer copias de seguridad en la nube

Instituto Nacional de Ciberseguridad (INCIBE). (s. f.). *Cómo hacer copias de* *seguridad en la nube.* <https://www.incibe.es/ciudadania/tematicas/copias-> ¿Sabes cómo hacer una copia de seguridad en Onedrive?, ¿y en Dropbox?, ¿y en Google drive? Aquí tienes una explicación sobre cómo automatizar las copias de seguridad en diferentes plataformas de almacenamiento.

# tid=124&tid_1=All&tid_2=All&tid_3=All

# Copias de seguridad (Incibe, 2024)

Instituto Nacional de Ciberseguridad (INCIBE). (s. f.). *Herramientas. Copias de* *seguridad.* <https://www.incibe.es/ciudadania/filtro/herramientas?>

¿No quieres arriesgarte a perder la dispositivos? Entonces realiza copias

información crucial que guardas en tus de seguridad de manera regular. Si tu

dispositivo se daña o se pierde, podrás recuperar tus datos sin preocuparte por las consecuencias.

# tid=303606&tid_1=All&tid_2=All&tid_3=All

# Recuperación de archivos

Instituto Nacional de Ciberseguridad (INCIBE). (s. f.). *Herramientas. Recuperación de* *a r c h i v o s .* <https://www.incibe.es/ciudadania/filtro/herramientas?> Si has eliminado información que deseas recuperar, las herramientas de recuperación de datos pueden asistirte en esta tarea para que puedas volver a acceder a tus archivos perdidos y retomar el control sobre ellos.

# Entrenamiento 1: estrategia de copia de seguridad

#### ▸ Planteamiento del ejercicio

- Descripción de la empresa: la empresa XYZ es una pequeña empresa de desarrollo de *software* con diez empleados. Su infraestructura tecnológica incluye servidores locales para el almacenamiento de datos y sistemas de gestión de bases de datos. Recientemente, la empresa ha experimentado una pérdida de datos significativa debido a un fallo del disco duro en uno de sus servidores. Como resultado, la dirección ha decidido revisar su estrategia de copia de seguridad para evitar futuras pérdidas de datos.

- Infraestructura tecnológica: se compone de servidores locales para el almacenamiento de datos y sistemas de gestión de bases de datos. Utilizan una combinación de servidores Linux y Windows para ejecutar aplicaciones y almacenar datos relacionados con los proyectos de clientes, así como para gestionar sus propios recursos internos, como el correo electrónico y la colaboración en documentos.

- Estrategia de copia de seguridad actual: hasta ahora la empresa XYZ ha estado utilizando una estrategia de copia de seguridad básica, según la cual realizan copias de seguridad completas de sus datos una vez a la semana en un dispositivo de almacenamiento externo. Sin embargo, esta estrategia se ha demostrado ser insuficiente después de experimentar una pérdida de datos significativa debido a un fallo del disco duro en uno de sus servidores. La falta de copias de seguridad frecuentes y la ausencia de medidas de redundancia han expuesto a la empresa a un riesgo innecesario de pérdida de datos y tiempo de inactividad.

- Propuesta: desarrollar una estrategia de copia de seguridad robusta y efectiva que garantice la integridad, la disponibilidad y la seguridad de los datos de la empresa XYZ, con la cual se minimice el riesgo de pérdida de datos y el tiempo de inactividad.

#### ▸ Desarrollo paso a paso

- Evaluar la infraestructura existente: realizar una revisión exhaustiva de la infraestructura tecnológica actual de la empresa XYZ, incluyendo servidores, sistemas de almacenamiento y *software* de gestión de copias de seguridad.

- Mantener las copias completas semanales.

- Configurar copias de seguridad incrementales diarias: verificar el éxito de las copias incrementales diarias, asegurando que se realicen de manera consistente y sin errores.

- Establecer un servicio de almacenamiento en la nube para redundancia.

- Selección de proveedor de almacenamiento en la nube: investigar y seleccionar un proveedor de servicios de almacenamiento en la nube confiable y seguro que cumpla con los requisitos de la empresa XYZ en términos de capacidad, seguridad y coste.

- Para mejorar, se realizarán copias diferenciales semanales.

- Pruebas de restauración de datos diferenciales: realizar pruebas periódicas de restauración de datos utilizando las copias de seguridad diferenciales para verificar la integridad y la eficacia del proceso de recuperación.

- Se encriptarán todas las copias de seguridad.

- Implementación de cifrado en el software de copia de seguridad: configurar el *software* de copia de seguridad para que utilice algoritmos de cifrado robustos durante la transferencia y el almacenamiento de las copias de seguridad, para garantizar la seguridad de los datos.

**▸**

- Gestión de claves de cifrado: establecer procedimientos para la gestión segura de las claves de cifrado utilizadas para proteger las copias de seguridad, con lo cual se asegure que solo el personal autorizado tenga acceso a ellas.

- Se realizarán pruebas periódicas de restauración.

#### ▸ Solución

Componentes de la estrategia:

**▸**

- Implementación de copias de seguridad incrementales: en lugar de depender únicamente de copias de seguridad completas realizadas semanalmente, se implementarán copias de seguridad incrementales diarias. Esto permitirá capturar cambios incrementales en los datos desde la última copia de seguridad completa, lo que reduce significativamente el tiempo y los recursos necesarios para realizar las copias de seguridad.

- Uso de almacenamiento en la nube para redundancia: además de las copias de seguridad locales en dispositivos de almacenamiento externo, se establecerá un servicio de almacenamiento en la nube para almacenar copias de seguridad adicionales. Esto proporcionará una capa adicional de redundancia y facilitará la recuperación de datos en caso de un fallo del *hardware* o un desastre.

- Implementación de copias de seguridad diferenciales semanales: para complementar las copias de seguridad incrementales diarias, se realizarán copias de seguridad diferenciales semanales. Estas copias de seguridad capturarán todos los cambios realizados desde la última copia de seguridad completa, lo que garantizará una mayor velocidad de recuperación en comparación con las copias de seguridad completas.

- Encriptación de datos: todas las copias de seguridad, tanto las locales como las almacenadas en la nube, se encriptarán utilizando algoritmos de encriptación robustos. Esto garantizará la seguridad de los datos durante la transferencia y el almacenamiento, lo que los protegerá contra accesos no autorizados y asegurará el cumplimiento de las regulaciones de privacidad de datos.

- Pruebas periódicas de restauración de datos: se realizarán pruebas periódicas de restauración de datos para verificar la integridad y la eficacia de la estrategia de copia de seguridad. Esto permitirá detectar y corregir cualquier problema potencial antes de que se conviertan en crisis reales.

- Implementación y seguimiento: la implementación de la nueva estrategia de copia de seguridad será supervisada por un equipo dedicado de administradores de sistemas y técnicos de TI. Se establecerán procedimientos y protocolos claros para la gestión de las copias de seguridad, incluyendo la programación regular, la monitorización del estado de las copias de seguridad y la resolución rápida de cualquier problema que surja.

# Entrenamiento 2: implementación y gestión de

# copias de seguridad con Bacula

#### ▸ Planteamiento del ejercicio

En este ejercicio práctico, se te encargará implementar y gestionar un sistema de copias de seguridad utilizando Bacula en un entorno simulado de servidores Linux. A lo largo del ejercicio, configurarás tanto el servidor de copias de seguridad como el servidor de archivos que necesitan ser respaldados. El objetivo principal es aprender a planificar, implementar y gestionar un sistema de copias de seguridad eficiente y confiable para asegurar la integridad y la disponibilidad de los datos en una organización.

#### ▸ Desarrollo paso a paso

Configuración del entorno virtual:

**▸**

- Utiliza un software de virtualización como VirtualBox para crear dos máquinas virtuales: un servidor de copias de seguridad y un servidor de archivos.

Selección e instalación del *software* de copias de seguridad:

**▸**

- Investiga diferentes opciones de software de copias de seguridad y selecciona Bacula como la solución para implementar.

- Instala Bacula en el servidor de copias de seguridad y configura los parámetros básicos.

Configuración del cliente de copias de seguridad:

**▸**

- En el servidor de archivos, edita el archivo bacula-fd.conf para configurar la conexión con el servidor de copias de seguridad. Añade la dirección del servidor de copias de seguridad y la contraseña de autenticación.

Configuración del director de copias de seguridad:

**▸**

- En el servidor de copias de seguridad, edita el archivo bacula-dir.conf para definir los trabajos de copia de seguridad, los clientes y las políticas de retención. Configura al menos un trabajo de copia de seguridad programado y una política de retención de datos.

Pruebas y verificación:

**▸**

- Ejecuta manualmente una copia de seguridad desde el servidor de archivos al servidor de copias de seguridad.

- Verifica que las copias de seguridad se estén realizando correctamente y que puedan ser restauradas en caso de necesidad.

Documentación y presentación:

**▸**

- Documenta todo el proceso de implementación, incluyendo capturas de pantalla y descripciones detalladas.

- Prepara una presentación en la que resumas los pasos realizados, los resultados obtenidos y cualquier lección aprendida durante el proceso.

**Fase 1:** configuración del entorno virtual. Instalación del *software* de virtualización:

**▸** **•** Descarga e instala VirtualBox desde su sitio web oficial ([https://www.virtualbox.org/](https://www.virtualbox.org/)). Creación de máquinas virtuales

**▸**

- Crea dos máquinas virtuales en VirtualBox. Para el servidor de archivos, utiliza Ubuntu Server como sistema operativo. Asigna recursos según tus necesidades (CPU, RAM, almacenamiento). Para el servidor de copias de seguridad, utiliza el mismo sistema operativo o uno diferente. Asigna recursos similares a los del servidor de archivos.

Configuración de la red virtual:

**▸**

- Configura una red interna en VirtualBox para que las máquinas virtuales puedan comunicarse entre sí.

- En VirtualBox, ve a configuración > red > adaptador de red 1 > modo red interna.

**Fase 2:** selección e instalación del *software* de copias de seguridad Investigación del *software:*

**▸**

- Después de investigar, selecciona Bacula como el software de copias de seguridad debido a su flexibilidad y amplio soporte comunitario.

Instalación del *software* en el servidor de copias de seguridad:

**▸**

- En el servidor de copias de seguridad (Ubuntu Server), sigue estos pasos:

![Figura 8. Instalación del software en el servidor de copias de seguridad. Fuente: elaboración propia.](images/image-25.png)

*Figura 8. Instalación del software en el servidor de copias de seguridad. Fuente: elaboración propia.*

Configuración básica del *software*

**▸**

- Durante la instalación se te pedirá configurar algunos parámetros básicos, como la contraseña de administrador y el nombre del director. Sigue las instrucciones del instalador.

**Fase 3:** configuración de las tareas de las copias de seguridad. Instalación del cliente de copias de seguridad en el servidor de archivos:

**▸**

- En el servidor de archivos, instala el cliente de Bacula:

![Figura 9. Instalación del cliente de Bacula. Fuente: elaboración propia.](images/image-26.png)

*Figura 9. Instalación del cliente de Bacula. Fuente: elaboración propia.*

Configuración del cliente en el servidor de archivos:

**▸**

- Edita el archivo /etc/bacula/bacula-fd.conf en el servidor de archivos para configurar la conexión con el servidor de copias de seguridad. Agrega la dirección del servidor de copias de seguridad y la contraseña de autenticación.

Aquí tienes un ejemplo de cómo podrías configurar el archivo /etc/bacula/bacula-fd.conf en el servidor de archivos:

![Figura 10. Ejemplo de cómo configurar el archivo /etc/bacula/bacula-fd.conf en el servidor de archivos.](images/image-27.png)

*Figura 10. Ejemplo de cómo configurar el archivo /etc/bacula/bacula-fd.conf en el servidor de archivos.*

Fuente: elaboración propia.

En este ejemplo, reemplaza « tu_contraseña» con la contraseña de autenticación que hayas configurado en el servidor de las copias de seguridad. Asegúrate también de proporcionar la dirección IP o el nombre de dominio del servidor de las copias de seguridad, así como el puerto del FileDaemon y otros detalles de configuración relevantes para tu entorno específico.

Configuración del director en el servidor de copias de seguridad:

**▸**

- Edita el archivo /etc/bacula/bacula-dir.conf en el servidor de copias de seguridad para definir los trabajos de copia de seguridad, los clientes y las políticas de retención.

Aquí tienes un ejemplo básico de cómo podrías configurar el archivo /etc/bacula/baculadir.conf en el servidor de copias de seguridad:

![Figura 11. Ejemplo de cómo podrías configurar el archivo /etc/bacula/bacula-dir.conf en el servidor de](images/image-28.png)

*Figura 11. Ejemplo de cómo podrías configurar el archivo /etc/bacula/bacula-dir.conf en el servidor de*

copias de seguridad. Fuente: elaboración propia.

![Figura 12. Ejemplo de cómo podrías configurar el archivo /etc/bacula/bacula-dir.conf en el servidor de](images/image-29.png)

*Figura 12. Ejemplo de cómo podrías configurar el archivo /etc/bacula/bacula-dir.conf en el servidor de*

copias de seguridad. Fuente: elaboración propia.

En este ejemplo:

**▸**

- Se define el director Bacula con su nombre, puerto y otros detalles de configuración.

- Se establece una contraseña de autenticación para el director.

- Se define un trabajo de copia de seguridad predeterminado (DefaultJob) que realiza una copia incremental del cliente server-fd.

**▸**

- Se configura un conjunto de archivos (FileSet) que incluye los archivos por respaldar.

- Se establece un horario (Schedule) para ejecutar la copia de seguridad semanalmente.

- Se configura el cliente (Client) que se conectará al director, especificando su nombre, dirección, puerto y detalles de retención.

- Finalmente, se define el catálogo Bacula que almacena la información de las copias de seguridad.

Definición de tareas de copias de seguridad:

**▸**

- En el archivo bacula-dir.conf define un trabajo de copia de seguridad que incluya al servidor de archivos como cliente y especifique las políticas de retención y almacenamiento.

**Fase 4:** ejecución y verificación de copias de seguridad.

Ejecución de tareas de copias de seguridad:

**▸**

- Utiliza el comando bconsole para iniciar manualmente un trabajo de copia de seguridad y verifica que se complete sin errores.

Programación de tareas de copias de seguridad:

**▸**

- En el archivo bacula-dir.conf configura la programación automática de los trabajos de copia de seguridad utilizando la directiva Schedule.

Verificación de las copias de seguridad:

**▸**

- Revisa los logs del director y del cliente para verificar que las copias de seguridad se están realizando correctamente. También puedes verificar el almacenamiento de las copias en el directorio especificado.

Pruebas de restauración:

**▸**

- Utiliza el comando bconsole para iniciar una restauración de los archivos desde la copia de seguridad y verifica que los archivos se restauran correctamente en el servidor de archivos.

# Entrenamiento 3: copia de seguridad basada en las

# torres de Hanoi

#### ▸ Planteamiento del ejercicio

Una empresa quiere realizar una implementación de copias de seguridad basado en las torres de Hanoi. Para ello queremos realizar una copia diaria (empezando en el día 1), que existan cinco niveles de copias y que sea del tipo completa/diferencial/incremental. Aquí las copias de seguridad de último nivel (5) son completas, las de los niveles intermedios (2, 3 y 4) son diferenciales y las de primer nivel (1) son incrementales. La secuencia continuaría en el tiempo.

Realiza la secuencia de copias para un mes que tenga 31 días, indica cuál sería el período de recuperación y comprueba que coincida con lo indicado en la teoría.

#### ▸ Desarrollo paso a paso

Basándonos en lo enseñado en la teoría, tenemos que simular el movimiento de los discos de la torre de Hanoi para cinco discos o niveles, asociando cada nivel a un determinado tipo de copia de seguridad (total, incremental y diferencial) y cada movimiento a la copia diaria correspondiente.

El juego de las torres de Hanoi con cinco discos tiene 31 movimientos (días) en total para resolver. Usaremos esta estructura para planificar las copias de seguridad en un ciclo de 31 días.

Se asignarán tres tipos de copias de seguridad:

**▸**

- C: completa.

- D: diferencial.

- I: incremental.

Los movimientos en las torres de Hanoi se adaptarán para indicar cuándo se hace cada tipo de copia. En un ciclo de 31 días, se utilizarán las posiciones de los discos en las torres de Hanoi para determinar el tipo de copia de seguridad.

Por ejemplo:

**▸**

- Día 1: completa (C)

- Día 2: incremental (I)

- Día 3: diferencial (D)

- Día 4: incremental (I)

- Día 5: diferencial (D)

- Día 6: incremental (I)

- Día 7: diferencial (D)

Y así sucesivamente siguiendo el patrón de las torres de Hanoi.

Secuencia para 31 días: La secuencia más rápida de resolución para las Torres de Hanoi con cinco niveles implica mover 31 discos en total. Aquí está la secuencia paso a paso:

1. Mueve el disco 1 de la torre A a la torre C.

2. Mueve el disco 2 de la torre A a la torre B.

3. Mueve el disco 1 de la torre C a la torre B.

4. Mueve el disco 3 de la torre A a la torre C.

5. Mueve el disco 1 de la torre B a la torre A.

6. Mueve el disco 2 de la torre B a la torre C.

7. Mueve el disco 1 de la torre A a la torre C.

8. Mueve el disco 4 de la torre A a la torre B.

9. Mueve el disco 1 de la torre C a la torre B.

10. Mueve el disco 2 de la torre C a la torre A.

11. Mueve el disco 1 de la torre B a la torre A.

12. Mueve el disco 3 de la torre C a la torre B.

13. Mueve el disco 1 de la torre A a la torre C.

14. Mueve el disco 2 de la torre A a la torre B.

15. Mueve el disco 1 de la torre C a la torre B.

16. Mueve el disco 5 de la torre A a la torre C.

## 17. Mueve el disco 1 de la torre B a la torre A.

## 18. Mueve el disco 2 de la torre B a la torre C.

## 19. Mueve el disco 1 de la torre A a la torre C.

## 20. Mueve el disco 3 de la torre B a la torre A.

## 21. Mueve el disco 1 de la torre C a la torre B.

## 22. Mueve el disco 2 de la torre C a la torre A.

## 23. Mueve el disco 1 de la torre B a la torre A.

## 24. Mueve el disco 4 de la torre B a la torre C.

## 25. Mueve el disco 1 de la torre A a la torre C.

## 26. Mueve el disco 2 de la torre A a la torre B.

## 27. Mueve el disco 1 de la torre C a la torre B.

## 28. Mueve el disco 3 de la torre A a la torre C.

## 29. Mueve el disco 1 de la torre B a la torre A.

## 30. Mueve el disco 2 de la torre B a la torre C.

## 31. Mueve el disco 1 de la torre A a la torre C.

Esta secuencia lleva los cinco discos desde la torre A hasta la torre C siguiendo las reglas del juego.

Teniendo en cuenta lo siguiente:

**▸**

- Disco 1: copia incremental.

- Disco 2: copia diferencial.

- Disco 3: copia diferencial.

- Disco 4: copia diferencial.

- Disco 5: copia total.

Podemos asociar cada movimiento a cada tipo de copia. Aquí tienes una tabla que muestra la distribución de las copias de seguridad diarias durante un ciclo de 31 días, basadas en la estructura de las torres de Hanoi, utilizando copias completas, diferenciales e incrementales.

![image-30](images/image-30.png)

![Figura 13. Distribución de las copias de seguridad diarias durante un ciclo de 31 días. Fuente: elaboración](images/image-31.png)

*Figura 13. Distribución de las copias de seguridad diarias durante un ciclo de 31 días. Fuente: elaboración*

propia.

Las copias de seguridad de último nivel (5) son completas, las de los niveles intermedios (2, 3 y 4) son diferenciales y las de primer nivel (1) son incrementales.

![image-32](images/image-32.png)

![image-33](images/image-33.png)

Tabla 15. Patrón de tipo de copias de seguridad. Fuente: elaboración propia.

Este patrón asegura que las copias de seguridad sean eficientes en términos de almacenamiento y tiempo de ejecución, lo que proporciona una buena combinación de restauración rápida y almacenamiento optimizado.

Período de recuperación:

Para detallar el período de recuperación en función del día y del tipo de copia más reciente disponible, vamos a identificar el proceso de restauración requerido para cada día. Esto implica determinar cuál es la copia más reciente (completa o diferencial) disponible y luego añadir cualquier copia incremental necesaria.

![image-34](images/image-34.png)

![image-35](images/image-35.png)

Tabla 16. Proceso de restauración requerido para cada día. Fuente: elaboración propia.

Resumen de recuperación:

**▸**

- Días con copia completa: restaurar desde la copia completa más reciente.

- Días con copia incremental: restaurar desde la copia completa o diferencial más reciente y aplicar todas las copias incrementales subsecuentes.

- Días con copia diferencial: restaurar desde la copia completa más reciente y luego aplicar la copia diferencial correspondiente.

Notas adicionales:

**▸**

- La recuperación siempre comienza desde la copia más reciente de tipo completa o diferencial.

- El objetivo es minimizar el número de pasos de restauración, por lo que se optimiza el tiempo de recuperación al aplicar las copias incrementales necesarias.

Este sistema ofrece un balance entre la frecuencia de las copias de seguridad y la eficiencia en la recuperación de datos.

# Entrenamiento 4: copia de backup en Windows

#### ▸ Planteamiento del ejercicio

En la primera parte, utilizarás la herramienta de copia de seguridad de Windows para respaldar archivos seleccionados en la nube, utilizando tu cuenta de OneDrive de Educantabria como destino. En la segunda parte, explorarás la herramienta de copia de seguridad con historial de archivos para realizar copias de seguridad en un medio externo, como una partición de disco

o un *pendrive.* Por último, en la tercera

actividad, instalarás y configurarás el *software* EaseUS Todo Backup Free para crear copias de seguridad tanto cifradas como sin cifrar. Además, programarás una copia de seguridad para que se ejecute automáticamente en el momento especificado y verificarás que se realice correctamente.

#### ▸ Desarrollo paso a paso

**Primera parte:** configurar una copia

de seguridad en la nube utilizando la

herramienta de copia de seguridad de Windows y OneDrive.

**▸**

- Abrir la herramienta de copia de seguridad de Windows.

- Configurar la copia de seguridad.

- Establecer la programación (opcional).

- Iniciar la copia de seguridad.

**Segunda parte:** utilizar la herramienta de copia de seguridad con historial de archivos para respaldar en un medio externo.

**▸**

- Abrir la herramienta de copia de seguridad con historial de archivos.

- Configurar la copia de seguridad.

- Establecer la programación (opcional).

- Iniciar la copia de seguridad.

**Tercera parte:** instalar EaseUS Todo Backup seguridad.

**▸**

Free para configurar copias de

- En una máquina virtual Windows 10, descargar e instalar EaseUS Todo Backup Free.

- Configurar una copia de seguridad sin cifrar.

- Configurar una copia de seguridad cifrada.

- Comprobar la copia de seguridad programada.

Primera parte

## 1. Abrir la herramienta de copia de seguridad de Windows:

**▸**

- Haz clic en el menú de inicio y escribe «copia de seguridad» en la barra de búsqueda.

- Selecciona «Configurar copia de seguridad» en los resultados de la búsqueda.

## 2. Configurar la copia de seguridad:

**▸**

- Haz clic en «Agregar una unidad» y selecciona «OneDrive» como destino de la copia de seguridad.

- Inicia sesión en tu cuenta de OneDrive de Educantabria si se te solicita.

- Selecciona los archivos y carpetas que deseas respaldar. Puedes elegir específicamente qué quieres respaldar o dejar la configuración predeterminada.

## 3. Establecer la programación (opcional):

**▸**

- Si deseas programar copias de seguridad automáticas, haz clic en «Más opciones» y luego en «Cambiar configuración».

- Aquí puedes configurar la frecuencia y la hora de las copias de seguridad automáticas.

## 4. Iniciar la copia de seguridad:

**▸**

- Haz clic en «Guardar cambios» para iniciar la copia de seguridad en OneDrive.

Segunda parte

1. Abrir la herramienta de copia de seguridad con historial de archivos:

**▸**

- Haz clic en el menú de inicio y escribe «Historial de archivos».

- Selecciona la opción «Historial de archivos» en los resultados de la búsqueda.

## 2. Configurar la copia de seguridad:

**▸**

- Conecta el medio externo (por ejemplo, un pendrive o una partición de disco).

- En la ventana del historial de archivos, haz clic en «Seleccionar unidad» y elige el medio externo como destino de la copia de seguridad.

- Selecciona los archivos y las carpetas que deseas respaldar.

## 3. Establecer la programación (opcional):

**▸**

- Si deseas copias de seguridad automáticas, haz clic en «Configuración avanzada» y luego en «Elegir la frecuencia».

## 4. Iniciar la copia de seguridad:

**▸**

- Haz clic en «Activar» para iniciar la copia de seguridad en el medio externo.

Tercera parte

## 1. Descargar e instalar EaseUS Todo Backup Free:

**▸**

- Visita el sitio web de EaseUS y descarga el programa Todo Backup Free.

- Ejecuta el archivo de instalación descargado y sigue las instrucciones en pantalla para completar la instalación.

## 2. Configurar una copia de seguridad sin cifrar:

**▸**

- Abre EaseUS Todo Backup Free.

- Haz clic en «Copia de seguridad» y luego en «Archivo».

- Selecciona los archivos y las carpetas que deseas respaldar.

- Elige un destino para la copia de seguridad (por ejemplo, una unidad externa).

- Configura la programación si deseas copias de seguridad automáticas.

## 3. Configurar una copia de seguridad cifrada:

**▸**

- En la configuración de la copia de seguridad, activa la opción de cifrado.

- Sigue los mismos pasos que para la copia de seguridad sin cifrar para seleccionar archivos, carpetas y programar la copia de seguridad.

## 4. Comprobar la copia de seguridad programada:

**▸**

- Después de configurar la copia de seguridad programada, se verifica que se realice correctamente en el momento especificado.

# Entrenamiento 5: copia de backup en Ubuntu con

# herramientas de sistema

#### ▸ Planteamiento del ejercicio

En esta actividad, configurarás un sistema de copias de seguridad diarias en Ubuntu utilizando herramientas integradas del sistema, específicamente «rsync» y «cron». Esta configuración garantizará que los datos críticos de tu sistema sean respaldados automáticamente todos los días, lo cual reduce el riesgo de pérdida de información.

Rsync es una herramienta de copia y sincronización de archivos que se utiliza en sistemas Unix y Linux. Es muy potente y versátil, lo que permite copiar y sincronizar archivos y directorios de manera eficiente, tanto localmente como entre sistemas remotos.

Cron es una utilidad en sistemas Unix y Linux que permite la automatización de tareas programadas. Es un demonio que ejecuta comandos o *scripts* automáticamente a intervalos específicos definidos por el usuario. Esto es muy útil para tareas de mantenimiento, copias de seguridad, limpieza de archivos temporales, actualizaciones y muchas otras tareas administrativas.

#### ▸ Desarrollo paso a paso

- 1. Instalación de herramientas necesarias.

- 2. Crear un script de copia de seguridad.

- 3. Hacer el script ejecutable.

- 4. Programar la copia de seguridad diaria con cron.

**Paso 1:** instalación de las herramientas necesarias.

Primero, asegúrate de que «rsync» esté instalado en tu sistema Ubuntu. Abre una terminal y ejecuta el siguiente comando:

![Figura 14. Comando. Fuente: elaboración propia.](images/image-36.png)

*Figura 14. Comando. Fuente: elaboración propia.*

**Paso 2:** crear un *script* de copia de seguridad.

Usa un editor de texto para crear un *script* de *shell* que realizará la copia de seguridad. En este ejemplo, utilizaremos «nano» para crear el archivo «backup_script.sh».

![Figura 15. Crear un script de copia de seguridad. Fuente: elaboración propia.](images/image-37.png)

*Figura 15. Crear un script de copia de seguridad. Fuente: elaboración propia.*

![Figura 16. Contenido para el editor de texto. Fuente: elaboración propia. En el editor, escribe el siguiente contenido:](images/image-38.png)

*Figura 16. Contenido para el editor de texto. Fuente: elaboración propia.*

Donde:

**▸**

- «rsync»: es el programa utilizado para copiar y sincronizar archivos y directorios entre ubicaciones.

- «-a» (archive): esta opción activa el modo de archivo, que permite realizar una copia recursiva de los directorios y preserva los atributos de los archivos como permisos, tiempos de modificación y propietarios. Es equivalente a usar varias opciones individuales (-rlptgoD).

- «-r»: copia los directorios de manera recursiva.

- «-l»: copia enlaces simbólicos como enlaces simbólicos.

- «-p»: preserva los permisos.

- «-t»: preserva los tiempos de modificación.

- «-g»: preserva el grupo.

- «-o»: preserva el propietario.

- «-D»: preserva los dispositivos y enlaces especiales.

- «-v» (verbose): muestra información detallada sobre los archivos que se están copiando y sincronizando. Esto es útil para ver lo que está haciendo «rsync» en tiempo real.

- «--delete»: esta opción le indica a «rsync» que elimine los archivos en el directorio de destino que ya no existen en el directorio de origen. Esto mantiene el directorio de destino exactamente igual al directorio de origen, al eliminar a los archivos obsoletos.

- «$SOURCE_DIR»: esta variable representa al directorio de origen, es decir, el directorio que contiene los archivos y subdirectorios que deseas copiar o sincronizar.

- «$DEST_DIR»: esta variable representa al directorio de destino, es decir, el directorio donde deseas que se copien o sincronicen los archivos y subdirectorios.

En nuestro caso, deberemos reemplazar «/ruta/a/tu/directorio/a/copiar» y «/ruta/a/tu/directorio/de/copia/de/seguridad» con las rutas apropiadas en tu sistema.

Guarda el archivo y sal del editor (en «nano», usa «CTRL+O» para guardar y «CTRL+X» para salir).

**Paso 3:** hacer el *script* ejecutable.

Otórgale permisos de ejecución al *script:*

![Figura 17. Otórgale permisos de ejecución al script. Fuente: elaboración propia.](images/image-39.png)

*Figura 17. Otórgale permisos de ejecución al script. Fuente: elaboración propia.*

Donde:

**▸**

- «chmod»: es el comando utilizado para cambiar los permisos de los archivos y directorios en sistemas Unix y Linux. Es una abreviatura de «change mode» (cambiar modo).

- «+x»: esta opción específica de «chmod» añade permisos de ejecución al archivo para el usuario que lo posee. «x» significa «execute» (ejecutar). Al usar el símbolo más (+), estamos añadiendo este permiso sin alterar otros permisos existentes.

- «~/backup_script.sh»: esta es la ruta al archivo cuyo permiso queremos cambiar. El símbolo virgulilla (~) representa el directorio *home* del usuario actual. Por lo tanto, «~/backup_script.sh» se refiere a un archivo llamado «backup_script.sh» que se encuentra en el directorio home del usuario actual.

**Paso 4:** programar la copia de seguridad diaria con cron.

Abre el crontab para editar:

![Figura 18. Abrir el crontab. Fuente: elaboración propia.](images/image-40.png)

*Figura 18. Abrir el crontab. Fuente: elaboración propia.*

Donde:

**▸**

- «crontab»: es el comando utilizado para administrar las tareas programadas del cron, el demonio que ejecuta comandos o *scripts* en momentos específicos definidos por el usuario.

- «-e»: esta opción abre el archivo crontab del usuario actual en el editor de texto predeterminado, lo que permite la edición de las tareas programadas.

Agrega la siguiente línea al final del archivo para programar la copia de seguridad diaria a las 2 AM:

![Figura 19. Programar la copia de seguridad diaria. Fuente: elaboración propia.](images/image-41.png)

*Figura 19. Programar la copia de seguridad diaria. Fuente: elaboración propia.*

Donde:

**▸**

- «0»: minuto en el que se ejecutará la tarea (0 significa en el primer minuto de la hora).

- «2»: hora en la que se ejecutará la tarea (2 significa a las 2 AM).

- «*»: día del mes en el que se ejecutará la tarea (un asterisco significa «cualquier día del mes»).

- «*»: mes en el que se ejecutará la tarea (un asterisco significa «cualquier mes»).

**▸**

- «*»: día de la semana en el que se ejecutará la tarea (un asterisco significa «cualquier día de la semana»).

- «/ruta/completa/a/tu/script/backup_script.sh»: la ruta completa al script o comando que se ejecutará.

Asegúrate de usar la ruta completa al *script* «backup_script.sh». Guarda y cierra el archivo del crontab.

**Paso 5:** verificar y monitorear.

Verifica que el *script* se ejecute correctamente y que los archivos se respalden en el directorio de destino. Para monitorear la ejecución del cron job, puedes revisar el archivo de registro de «cron»:

![Figura 20. Revisar el archivo de registro de «cron». Fuente: elaboración propia.](images/image-42.png)

*Figura 20. Revisar el archivo de registro de «cron». Fuente: elaboración propia.*

Este comando mostrará las entradas del registro relacionadas con «cron», lo que te permitirá verificar que la tarea de copia de seguridad se haya ejecutado según lo programado.

![Figura 21. Entradas de log. Fuente: elaboración propia. Las entradas de log podrían verse así:](images/image-43.png)

*Figura 21. Entradas de log. Fuente: elaboración propia.*

Donde cada línea significa lo siguiente:

**▸**

- «Jun 12 02:00:01 hostname CRON[12345]: (usuario) CMD (/home/usuario/backup_script.sh)»: a las 2:00 AM del 12 de junio, el usuario «usuario» ejecutó el script «/home/usuario/backup_script.sh».

- «Jun 12 02:00:01 hostname CRON[12346]: (CRON) info (No MTA installed, discarding output)»: a las 2:00 AM del 12 de junio, cron intenta enviar un correo con la salida del *script,* pero como no hay un MTA instalado, la salida se descarta.

- «Jun 13 02:00:01 hostname CRON[12347]: (usuario) CMD (/home/usuario/backup_script.sh)»: a las 2:00 AM del 13 de junio, el usuario «usuario» ejecutó nuevamente el *script* «/home/usuario/backup_script.sh».

Siguiendo estos pasos, habrás configurado una actividad de copia de seguridad diaria en Ubuntu, al utilizar herramientas del sistema para asegurar que tus datos sean respaldados automáticamente todos los días.

---

## Repeated content (headers / footers / watermarks)

> The following appeared on most pages and was moved out of the body to keep reading order clean — kept here, not deleted.

- Material de estudio  *(pp.4–31)*
- A fondo  *(pp.32–36)*
- Entrenamientos  *(pp.37–74)*
- Seguridad y Alta Disponibilidad 4 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 5 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 6 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 7 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 8 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 9 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 10 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 11 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 12 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 13 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 14 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 15 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 16 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 17 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 18 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 19 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 21 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 22 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 23 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 24 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 25 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 26 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 27 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 28 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 29 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 30 Tema 3. Material de estudio · Seguridad y Alta Disponibilidad 31 Tema 3. Material de estudio  *(pp.4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31)*
- Seguridad y Alta Disponibilidad 32 Tema 3. A fondo · Seguridad y Alta Disponibilidad 33 Tema 3. A fondo · Seguridad y Alta Disponibilidad 34 Tema 3. A fondo · Seguridad y Alta Disponibilidad 35 Tema 3. A fondo · Seguridad y Alta Disponibilidad 36 Tema 3. A fondo  *(pp.32–36)*
- Seguridad y Alta Disponibilidad 37 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 38 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 39 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 40 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 41 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 42 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 43 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 44 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 45 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 46 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 47 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 48 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 49 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 50 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 51 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 52 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 53 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 54 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 55 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 56 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 57 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 58 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 59 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 60 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 61 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 62 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 63 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 64 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 65 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 66 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 67 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 68 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 69 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 70 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 71 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 72 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 73 Tema 3. Entrenamientos · Seguridad y Alta Disponibilidad 74 Tema 3. Entrenamientos  *(pp.37–74)*
- ▸ Solución  *(pp.43, 53, 63, 68)*