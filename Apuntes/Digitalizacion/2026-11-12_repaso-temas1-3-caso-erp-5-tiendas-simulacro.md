---
asignatura: Digitalización aplicada a los sectores productivos
fecha: 2026-11-12
tema: "Repaso de los Temas 1-3: cierre del caso 'ERP de las 5 tiendas' (local vs nube), preguntas tipo test de práctica y confirmación del formato de examen"
fuente: "Transcripción de la clase en directo (sin diapositivas) + temario oficial (Digitalización/dig_tema01-03) + cálculos y aportaciones propias marcadas (mío)"
---
# Digitalización · Repaso Temas 1-3 y caso ERP de las 5 tiendas (12/11)

> Anterior: [Cierre Tema 2 e inicio Tema 3: cloud (29/10)](2026-10-29_tema2-cierre-ia-sostenibilidad-tema3-cloud.md) · Profesor: David Cantos

> [!info] Cómo leer estos apuntes
> Nota pensada para estudiar **sin ver la grabación**. El profesor proyectó diapositivas propias (caso, preguntas, ideas clave) que **no están en la transcripción**: solo se oye lo que dice. **(clase)** = dicho en voz alta; **(temario)** = PDFs `Digitalización/dig_tema01-03`; **(mío)** = cálculo o aportación mía. No se vio contenido nuevo del temario: es una sesión de cierre del primer trimestre.

## Lo imprescindible

1. **Formato del examen CONFIRMADO (clase): solo tipo test**, sin desarrollo, "para que no tengáis que memorizar conceptos". Estructura anunciada: **una pregunta y 4 respuestas, una sola correcta**. Antes (17/09 y 15/10) estaba "sin confirmar"; ahora lo afirma él. **Sigue sin confirmar** que no lo cambie la coordinación (en la sesión del 15/10 dijo que no dependía solo de él).
2. **Solo cae lo que está en el temario oficial** (el de la plataforma / los PDF `dig_tema0X`). Lo que se comenta en clase "es material de apoyo". Aun así dijo que **puede caer alguna pregunta sobre modelos de servicio (IaaS/PaaS/SaaS) y la definición de cloud**, porque, según él, el temario lo menciona. (Ver discrepancia abajo.)
3. **Próxima sesión: simulacro de examen tipo test** sobre los **3 temas vistos**, con las preguntas comentadas en directo. Recomienda conectarse en directo y haber leído antes los 3 temas. Fecha: sesiones quincenales -> lo más probable es el **jueves 26/11** (inferencia mía, sin confirmar; mirar la plataforma). Cierra el primer trimestre de la asignatura.
4. **Subirá las diapositivas** a la plataforma (resumen de ideas clave por tema, preguntas de práctica y soluciones). Sin fecha.
5. **Regla de oro de las preguntas de criterio**: "la mejor opción no es la más cara ni la más moderna, sino la que garantiza las necesidades de esa empresa con coste y riesgos asumibles"; la decisión se basa en un **análisis completo, no solo en el precio**.

> [!warning] Discrepancia: ¿IaaS/PaaS/SaaS están en el temario?
> El profesor dice que el temario "lo menciona". Lo he comprobado: en `dig_tema01-03` **solo aparece la palabra "SaaS" una vez** (Entrenamiento 2 del Tema 3, para decir que en la nube se pueden ejecutar aplicaciones completas). **IaaS y PaaS no aparecen** ni hay definición de los tres modelos. Con el PDF como fuente, **la definición de los modelos de servicio no es temario evaluable seguro**, pero el profesor sí los usará en las preguntas del simulacro. Estudia el resumen de la nota del 29/10 (sección 2.3).

## Parte 1 · El caso real: "ERP de las 5 tiendas"

**Datos del caso (clase).** Cliente con **1 almacén y 4 tiendas**, un **servidor de 10 años o más** que empieza a dar problemas. Quiere **mantener su ERP**. Las alternativas:

| Opción | Dato dicho en clase | Notas |
|---|---|---|
| **Renovar infraestructura local** (servidor, y posiblemente red, *switch* y puntos de acceso en el almacén) | Estimación del profesor: **12.000 €**, que redondea a **20.000 €** por la subida del precio de memoria RAM y discos | **No es un presupuesto real**: aún no tiene presupuestos. Inversión inicial alta |
| **ERP en la nube (SaaS)** que ofrece **el propio proveedor del ERP** | **450 €/mes** para todos los usuarios de tienda y almacén (redondeado a 500 €/mes) | Cuota mensual, varía según usuarios y servicios incluidos |

**Cálculo de amortización (mío).** Un alumno dijo "a 4 años se amortiza" y el profesor lo aceptó. Comprobado: 20.000 / 5.400 (450 x 12) = **3,7 años**; con 500 €/mes (6.000 €/año) = **3,3 años**. Es decir, "unos 4 años" es aproximado, y **solo compara la inversión inicial con la cuota**: el local suma además electricidad, mantenimiento, licencias, soporte, copias y renovación futura. A 5 años, el SaaS a 450 €/mes suma 27.000 € (mío) frente a 20.000 € más los costes recurrentes del local.

**Datos del negocio que cambian la decisión (clase).** El cliente quiere **potenciar la venta online** (invertir en la web, conectar ERP y web) y **centralizar en un almacén grande**; incluso estudia **cerrar alguna tienda poco rentable**. Por tanto la **escalabilidad** que más importa podría ser **hacia abajo**, no hacia arriba. Ventaja clásica de la nube = crecer cuando se abren tiendas.

**Criterios de comparación que el profesor puso en la tabla** (los valores de su tabla no se oyen; los criterios sí):

| Criterio | Qué hay que preguntarse |
|---|---|
| Inversión inicial | Local: alta. Nube: baja |
| Coste recurrente | Nube: cuota mensual siempre (según usuarios y servicios). Local: mantenimiento, electricidad, licencias, soporte, copias |
| Quién gestiona | ¿Tienen informático contratado? Actualizaciones, copias de seguridad: ¿quién las hace? ¿habría que contratar a alguien? |
| Tiempo de respuesta ante avería | Local: normalmente mayor. Nube: soporte del proveedor |
| Dependencia de Internet | Si cae la conexión, ¿se para el almacén? |
| Escalabilidad | Plan de crecimiento o reducción del negocio |
| Disponibilidad | Qué garantiza el proveedor (porcentaje) y qué supone en horas |
| Seguridad y copias | Qué hace el proveedor y qué debe seguir haciendo la empresa |
| Continuidad de negocio y tiempos de recuperación | Qué pasa tras un fallo o un ciberataque |
| Contrato | Qué incluye exactamente, cómo se sale |
| Subvenciones | Un alumno la citó; el profesor lo aprobó como criterio |

**Opción híbrida (clase).** Si el negocio es muy crítico y no puede parar por una caída de Internet, se puede mantener **una copia local o la base de datos sincronizada** para que el almacén siga trabajando y luego se sincronice con la nube. **Cuesta más**, hay que volver a mirar costes.

**Cómo asesorar (clase).**
- Los clientes miran primero "en cuántos años lo amortizo"; hay que **ser claro y realista** y explicar el resto de criterios.
- **La última palabra la tiene el cliente**, influido por lo que se le aconseje.
- Su criterio principal en este cliente, elija lo que elija: **seguridad y continuidad del negocio**. Citó empresas que han perdido mucha información por no proteger sus infraestructuras (sin detalles).
- Si tienes dudas, "hacer el traje a medida" (frase de un alumno que el profesor aceptó).
- **Estado**: el cliente **no ha decidido**; el profesor aún no tiene presupuestos reales.

> [!important] Disponibilidad: cuánto es el 99 % (mío; corrige un detalle de clase)
> El profesor puso de ejemplo que un 99 % de disponibilidad mensual podía equivaler a "una hora de caída al mes" y añadió que "99 lo he puesto muy alto". Cálculo: un mes de 30 días = 720 h; **99 % = 7,2 h de caída al mes** (unos 3,65 días al año); **99,9 % = 43,2 min al mes**. La idea de fondo de su ejemplo es correcta: **hay que traducir el porcentaje a horas y valorar si el negocio lo soporta**.

## Parte 2 · Preguntas de práctica (las que dio)

Aviso: en el simulacro serán **4 opciones con una correcta**; las de verdadero/falso de la diapositiva eran solo de práctica.

| Pregunta (resumida) | Respuesta del profesor | Por qué |
|---|---|---|
| Una empresa contrata **máquinas virtuales, almacenamiento y redes** a un proveedor cloud y **instala y administra ella el sistema operativo y el ERP**. ¿Qué modelo? | **IaaS** (infraestructura como servicio) | El proveedor da la infraestructura; el cliente gestiona del SO hacia arriba |
| "Una aplicación industrial puede procesar **datos críticos en un dispositivo edge** y enviar después **información agregada a la nube** para análisis histórico". ¿V o F? | **Verdadero** | Edge = respuesta rápida y control local; cloud = grandes volúmenes y análisis |
| Caso del cliente, 4 afirmaciones: "con estos números el local se amortiza..." / "los 12.000 € cubren el coste del servidor local durante los 5 años" / "la comparación debe incluir costes recurrentes, riesgos y continuidad" / "hay que revisar garantías de recuperación, copias y disponibilidad del proveedor (leer el contrato)" | Dijo que la primera (la de los números) era correcta; **la de los 12.000 € es incorrecta**; la de incluir costes recurrentes, riesgos y continuidad **es correcta**; la de revisar garantías y contrato **también es correcta** | Los 12.000 € son solo la inversión inicial; faltan mantenimiento y copias. **Confuso**: no queda claro qué letra es la única correcta, porque se oyen varias correctas; pendiente de ver la diapositiva |
| Si una empresa migra el ERP a la nube, ¿**el proveedor asume automáticamente** copias de seguridad, permisos de usuario y protección de datos? | Puso "Falso" en la diapositiva, pero admite que **"depende"** (una tercera opción) | **Copias**: depende del contrato. **Roles/permisos de usuario y protección de datos**: **siguen siendo responsabilidad de la empresa cliente** (quién accede a qué información), independientemente del contrato |
| ¿Una empresa que usa herramientas digitales y pasó del papel a tablets "ya ha completado su transformación digital"? | **Falso** | Digitalizar tareas no es transformar procesos (Tema 1) |
| ¿La IA o la tecnología más nueva es **siempre** lo más adecuado para automatizar un proceso? | **Falso** | A menudo basta conocer las reglas del negocio y una automatización convencional o una aplicación sencilla |
| Trabajadores que acceden por **VPN** a un servidor de la empresa: ¿es cloud computing? | **No** (su opinión, ver aviso del 29/10) | Es acceso remoto a infraestructura propia, no consumo de servicios de un tercero |
| Procesar datos cerca de donde se generan reduce **latencia** y **dependencia de Internet**. | **Verdadero** | Edge/fog/mist (temario 3.3). Latencia = tiempo de respuesta |
| "Migrar el ERP a la nube **siempre** es más conveniente que renovar el servidor local." | **Ni V ni F: depende** | Depende del análisis de costes totales, disponibilidad, mantenimiento, seguridad, conectividad y contrato |

> [!warning] El VPN y el "no es cloud": para el test, usa el temario
> Se repite que el profesor responde "no" porque cloud = servicio de un tercero con sus centros de datos, por el que se paga. Recuerda lo avisado el 29/10: el PDF define cloud con las **5 características NIST**. Para una pregunta de test, el resultado "no es cloud" coincide; si dudas entre opciones, elige la que se apoye en las características del temario.

**Ideas clave del cierre (clase)**, por si caen:
- Trabajar en la nube **no es solo acceder a un servidor remoto**: es usar recursos y servicios informáticos de **un tercero** (proveedor) con **flexibilidad, escalabilidad y pago** por ello.
- ERP del propio proveedor en la nube = **SaaS**. Plataforma donde despliegas tu aplicación = **PaaS**. Máquinas virtuales que administras = **IaaS**.
- No todo tiene que estar en la nube: **soluciones híbridas** y **procesamiento cerca del origen** (edge/mist).
- Valorar **costes a largo plazo, copias, datos, mantenimiento y continuidad**.

## Parte 3 · Resumen de incidencias de una digitalización (consultoría)

Diapositiva con "incidencias típicas" tras implantar tecnología (se oyen los ejemplos, no la lista exacta). Se pretendía que el alumno actúe como **consultor tecnológico**. Si no da tiempo, se verá en el simulacro.

**Ejemplos citados (clase):** tienda online que permite comprar productos que **no están en el almacén**; si **falla Internet**, los operarios quedan parados y no pueden registrar entradas y salidas; **sensores IoT** en máquinas (p. ej. inyectoras de plástico) que dan datos que **nadie sabe aprovechar**; **roles de usuario** mal definidos (cada uno debe entrar al ERP con sus credenciales y ver solo lo suyo); proveedor cloud que garantiza un porcentaje de disponibilidad que la empresa no ha traducido a horas; **la dirección quiere meter IA** para resolverlo todo.

**Cómo abordarlo (clase):**
1. **Priorizar**: ver las **3 incidencias más graves** y **por qué** ocurren.
2. Decidir **qué tecnología o solución** corresponde a cada una.
3. Identificar **procesos críticos** que deban seguir funcionando aunque falle algo (p. ej. Internet) = **plan B**.
4. **Leer los contratos** y aclarar qué responsabilidad es del proveedor cloud.
5. Valorar si conviene **introducir ahora una tecnología nueva** (p. ej. IA) o si hay **prioridades más importantes** antes.
6. (Alumno, aceptado) Comparar con el coste y los errores de los **procedimientos manuales** anteriores: las incidencias de la digitalización se asumen porque se busca una mejora.
7. (Alumno, aceptado) Los datos digitalizados deben **servir y aportar valor al negocio**.

## Avisos de logística

- **Grabación**: disponible en diferido.
- **Examen**: solo tipo test (4 opciones, 1 correcta); solo temario oficial. Ver arriba.
- **Simulacro**: próxima sesión (probable 26/11, sin confirmar); conviene **leer antes los 3 temas**; la plataforma publicará la sesión.
- **Tests de la plataforma**: no se dijo nada; **consultar en el aula** si están abiertos los tests de los Temas 1-3 y su fecha límite.
- **Diapositivas**: subirá las de esta sesión (ideas clave por tema, preguntas y soluciones).
- **Contenido omitido**: una conversación con un alumno sobre su proyecto personal, que no es de la asignatura.

## Para llevar a casa

1. **Leer los Temas 1, 2 y 3** (`Digitalización/dig_tema01…03`) antes del simulacro; lo evaluable del Tema 3 casi no se vio en clase (ver nota del 29/10).
2. Dominar: modelos de servicio (nota 29/10, sección 2.3), 5 características NIST, 4 tipos de nube, mist/edge/fog/cloud, y las ideas del Tema 1 (digitalizar ≠ usar herramientas digitales; IT vs OT).
3. Practicar a traducir **porcentaje de disponibilidad -> horas** y **amortización -> años**.
4. Comprobar en el aula los tests de los Temas 1-3 (fechas límite).
5. Pasarme las diapositivas cuando el profesor las suba, para completar la tabla de criterios y la pregunta de las 4 afirmaciones.

> [!warning] Dudas del audio
> - La pregunta de las 4 afirmaciones del caso: no se oyen todas las opciones; se interpreta por lo que dijo (ver tabla). **Sin confirmar** cuál es la única correcta.
> - Las cifras del caso (12.000, 20.000, 450 y 500 €/mes) son **orientativas** y el profesor lo dijo expresamente.
> - Transcripción: "club computing" = cloud computing; "Rp" = ERP; "I A S" = IaaS; "S A, G" = SaaS; "P A, S" = PaaS.
