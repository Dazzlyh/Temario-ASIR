---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-10-28
tema: "Tema 2 · Seguridad pasiva (2ª parte): CPD y seguridad física, disponibilidad y «nueves», RTO/RPO, redundancia y Tiers, plan de recuperación ante desastres + examen y calendario"
fuente: "Transcripción de la clase en directo (≈83 min). Sin PDF nuevo: el profesor proyectó el temario y un ejercicio propio."
---
# SAD · Tema 2, 2ª parte: seguridad pasiva con enfoque de disponibilidad (28/10)

> Anterior: [Corrección de la Actividad 1 + inicio del Tema 2 (21/10)](2026-10-21_tema2-seguridad-pasiva.md) · Profesor: Damián Sualdea Soy

Esta clase cierra el Tema 2. El profesor dijo que la mitad de la parte física **es idéntica a Ciberseguridad** (sin cambios en el temario) y que en SAD la reorientó hacia la **disponibilidad**, que es "el nombre del módulo". Está organizada por temas, no por orden de clase. Marcas: **(clase)** lo dijo el profesor; **(mío)** cálculo o inferencia mía; **sin confirmar** lo que el audio no deja claro.

## Lo imprescindible

1. **Disponibilidad = porcentaje de tiempo que el servicio está funcionando.** Se mide en **«nueves»** (99 %, 99,9 %, 99,99 %...). Cada nueve más es "una auténtica locura" de coste y de dificultad. **El 100 % no existe** (clase).
2. Solo hay **dos palancas**: que **falle menos** (MTBF) y que **se arregle antes** (MTTR) (clase).
3. **RTO** = cuánto tardo en volver a estar en marcha. **RPO** = cuánta información puedo perder (antigüedad de la última copia útil). Son "preguntas típicas mías" en el examen.
4. **Redundancia:** N, N+1 y duplicado completo. Los centros de datos se clasifican en **Tier I–IV** según redundancia y disponibilidad.
5. **Plan de recuperación ante desastres (DRP):** documento paso a paso, **no se improvisa nada**, se aprueba y se ensaya con simulacros.
6. **Copiar es fácil; restaurar es el problema.** Si no has restaurado nunca una copia, "para mí no hay copia de seguridad" (criterio de auditoría, clase).

> [!important] Frase para el examen (clase)
> **La seguridad activa evita el golpe; la seguridad pasiva decide si, cuando el golpe llega, vuelves en una hora o no vuelves.**

## 1 · Seguridad física del CPD (repaso, solo se comentó por encima)

Es el contenido del Tema 2 que ya se vio en Ciberseguridad (mira tus apuntes de Ciberseguridad sobre CPD). El profesor lo recorrió como lista de comprobación:

| Área | Qué se dijo |
|---|---|
| **Ubicación** | Lejos de sótanos e inundaciones. "Algo tan sencillo como no dejar el servidor debajo de una tubería" |
| **Suelo técnico** | El suelo se levanta unos 30–40 cm y por debajo van los cables |
| **Ventanas / discreción** | Que nadie sepa que ahí hay un servidor: no señalizar la sala |
| **Acceso físico** | Tarjeta, biometría, **NFC** (su preferencia, ver debate abajo), cámaras, **esclusa**, puerta con contactos |
| **Clima** | Temperatura controlada (el audio dice "entre 18 o 17 grados", **sin confirmar** el rango; mira Ciber), humedad controlada, **pasillo frío/caliente** |
| **Incendios** | Detección de humo lo más sensible posible (avisa antes de que haya llama). Extinción **sin agua** en la sala |
| **Energía** | **SAI**, **toma de tierra** (deriva la corriente al suelo y evita que reviente el equipo), **protección contra sobretensiones**, **circuitos separados** (el CPD tiene su propio circuito) |
| **Sensores 24 h** | Temperatura y humedad en varios puntos del rack, **sensores de líquido** en el suelo técnico, control de acceso |

- **Quién trabaja en un CPD** (clase): sobre todo **personal industrial** (frío, calor, electricidad), no informáticos. Aconsejó, si te interesa la electrónica, meterte en ese sector porque "siempre hay trabajo".
- **Consejo personal del profesor** (no es temario): ante un apagón, bajar los fusibles y subirlos cuando la red se estabilice, porque al volver la luz llegan picos que revientan equipos.
- **Debate: tarjeta o biometría** (clase, no evaluable). El profesor prefiere **tarjeta con doble factor**: lo que importa es la **revocabilidad**, "si pierdo una clave o una tarjeta, hago otra; si me roban el ojo, ¿qué hago?". Compañeros defendieron la biometría porque es más difícil de robar que una tarjeta (Manuel) y plantearon el problema ético de usar el cuerpo como contraseña (Francisco). Ejemplo citado: gente que vendió el escaneo de su retina por unos 20–300 € (el profesor lo asoció a *Worldcoin*; sin confirmar las cifras). **Para el examen, la idea útil es la unicidad frente a la revocabilidad.**

## 2 · Disponibilidad y «nueves»

**Definición (clase):** porcentaje de tiempo que un sistema está disponible y funcionando.

La relación con MTBF y MTTR la nombró pero no escribió la fórmula. La habitual es (mío):

```
Disponibilidad = MTBF / (MTBF + MTTR)
```

Con eso se ve por qué hay dos palancas: subir el MTBF (fallar menos) o bajar el MTTR (arreglar antes).

| Disponibilidad | Nombre | Parada al año (aprox., **mío**) | Lo que dijo en clase |
|---|---|---|---|
| 99 % | dos nueves | ≈ 3,65 días | "puede haber una caída al año" |
| 99,9 % | tres nueves | ≈ 8,8 h | el audio da "8 h" |
| 99,99 % | cuatro nueves | ≈ 52 min | "unos 52 min" (clase) |
| 99,999 % | cinco nueves | ≈ 5 min | "estamos hablando de 5 min" |

- Cálculo mío: 365 días × 24 h × (1 − disponibilidad). El profesor dio solo parte de esas cifras (el audio de 99 % y 99,9 % es confuso, por eso las he calculado yo).
- Ante la pregunta "¿99,9 % es buena disponibilidad?": **"normal, no es buena, buena; hay mejores"** (clase).
- **Mensual frente a anual:** un 99,99 % **mensual** son unos 4 min de caída al mes (≈ 52 min al año). El profesor lo usó para leer los SLA.
- **SLA y proveedores** (clase): AWS promete 99,99 % mensual en EC2 y, si lo incumple, **devuelve parte de lo pagado**. Mostró una comparativa de OVH que ponía **dedicado puro: 99,95 %** y **nube pública: 99,99 %**; **sin confirmar**, lo leyó en pantalla sin detenerse.
- **Servidor dedicado (*bare metal*) frente a nube** (clase): en un servidor dedicado tienes **"un ordenador para ti"**, sin réplica; en la nube está todo replicado. Su anécdota: un Kimsufi barato que le duró 7–8 años "hasta que reventó". Ejemplo de que la disponibilidad real de un servidor dedicado depende de la suerte.

> [!warning] Fallo en un test (clase)
> Dos compañeros avisaron de un **error en una pregunta de test sobre MTTR** (el audio dice "MDTR"). El profesor dijo que **la pregunta no valdrá para nada y se dará por buena cualquier respuesta**. **Sin confirmar** de qué test se trata (parece el del Tema 1); revisa tu nota cuando se publique.

## 3 · RTO y RPO

| | Qué mide | Cómo se baja | Ejemplo (clase) |
|---|---|---|---|
| **RTO** (*Recovery Time Objective*) | **Cuánto tardo** en volver a estar en marcha | Tener **repuestos**, sitio alternativo, un plan | Discos de más en la oficina; ante un ransomware, tirar de discos nuevos y restaurar en un sitio alternativo |
| **RPO** (*Recovery Point Objective*) | **Hasta qué punto puedo perder información**. Se mide como la **antigüedad de la última copia útil** | **Hacer muchas copias**, más a menudo | Si pierdo más de X, "la he liado": puede ser de horas a días o meses según la empresa |

- El profesor lo describe como "el punto en el que no hay vuelta atrás: si paso de aquí, se va mi negocio al garete". Esa es su explicación del RPO.
- Más adelante se verá **RPO diario** y las políticas de copia.
- Son **valores que fija la organización**, normalmente el área de consultoría y análisis de riesgos ("el mundo corbatero": Deloitte, informes de riesgo, documentación), no el técnico. Aparecen mucho en ofertas de empleo de seguridad.

## 4 · Redundancia y niveles de CPD (Tiers)

**Redundancia** (clase): repetir algo para que no se pierda ("la copia de la copia de la copia").

| Esquema | Qué es | Ejemplo (clase) |
|---|---|---|
| **N** | Justo lo necesario, **sin repuesto**. Si se cae, se cae | Un solo equipo de aire para la sala |
| **N+1** | **Un repuesto** | Dos equipos de aire y uno de sobra |
| **Duplicado completo** (el audio dice "golsene"; es probable que sea **2N**, mío) | **Dos salas completamente distintas**, con acometidas distintas. Si cae una entera, sigue la otra | "Nunca para"; es lo más caro: "pagar más para que el servicio no se caiga" |

**Tiers** (clase; el profesor dice "tía/tío"): el nivel de un CPD se mide por su redundancia y su disponibilidad.

| Tier | Redundancia | Disponibilidad citada | Parada anual (clase) |
|---|---|---|---|
| **I** | N, sin redundancia | 99,67 % | (no dicha) |
| **II** | Redundancia **parcial** | 99,74 % | ≈ 22 h |
| **III** | N+1 y **mantenible en caliente** | 99,982 % | ≈ 1,6 h |
| **IV** | **Duplicado completo, tolerante a fallos** | 99,995 % | (no dicha) |

El salto grande es del **Tier II al III** (clase). Las cifras coinciden con las que suelen citarse para esta clasificación (el profesor las leyó de memoria o de la diapositiva; el audio de los porcentajes es poco claro, por eso no las doy como verificadas al detalle).

> [!note] Consejo del profesor
> **Si quiero medir un CPD, lo mido con los Tier.** Para calcular el anual a partir de un dato mensual, multiplica por 12.

## 5 · Rack: el armario de 42 U (ejercicio del profesor)

Visto en Ciber, no en SAD, así que lo dejó como ejercicio **opcional** ("no hay que hacerlo para nada").

- **Rack** = armario metálico de **19 pulgadas** con medidas estándar. La altura típica es **42 unidades (42 U)**. Se anuncian armarios de 5 U hasta 42 U.
- **1 U ≈ 4,4 cm** (el profesor dijo "44 cm" por un fallo de lectura; es **4,4 cm**, 1,75 pulgadas).
- Un servidor fino ocupa **1 o 2 U**; un switch, **1 U**. No se llena el armario: **se deja hueco para ventilación**. Además del espacio manda el **peso** y la **capacidad eléctrica**.
- **Parte delantera:** conexión y gestión del equipo. **Parte trasera:** todo el cableado de red y eléctrico.
- Accesorios que aportó Francisco: **patch panel**, **pasacables** y **regleta de alimentación** (PDU). También hay que contarlos, no solo los equipos.
- **Ejercicio:** 10 servidores de 2 U + 5 switches de 1 U en un armario de 42 U. ¿Cuántas U ocupan? ¿Cabe? ¿Qué margen conviene dejar? Cálculo mío: 10 × 2 + 5 × 1 = **25 U**, quedan **17 U** libres. Qué margen dejar, **lo preguntaba el profesor y no dio la respuesta**.

## 6 · Plan de recuperación ante desastres (DRP) y casos reales

**DRP** (clase, "DR P"/*Disaster Recovery Plan*; en el temario puede aparecer como plan de continuidad): documento que dice **paso a paso cómo se vuelve a la normalidad tras un desastre**: **quién** hace qué, **en qué orden**, **con qué recursos**. Y una regla: **no se improvisa absolutamente nada.**

- Lo redactan los perfiles de consultoría, que **fijan el RTO y el RPO** y **dónde están las copias**. Se **aprueba** y se **ensaya con simulacros**, como un simulacro de incendio.
- Anécdota del profesor: un conocido responsable de seguridad física de una farmacia tenía **todos los casos escritos** (incendio, explosión...) y sabía qué comunicar a terceros en cada uno.
- **Auditoría de copias:** uno de los puntos de verificación es si se comprueban las copias. Pregunta típica: "¿has restaurado alguna en el último mes?". Si no, "para mí no hay copia".

**Casos que citó** (para que veas que 100 % no existe):

| Caso | Qué pasó (clase) | Lección (clase) |
|---|---|---|
| **AWS, 20/10/2025** | Se cayó medio Internet desde la región **us-east-1 (Virginia)** por un **error de DNS** que dejó sin respuesta a **DynamoDB**, base de datos interna de la que dependen más de 100 servicios de AWS. Duración: "x horas". Afectó a Alexa, Fortnite, Snapchat, ChatGPT... y a las prácticas del propio profesor ese día | Lo que se compensa es el **dinero**, no lo perdido (créditos de SLA). Funcionó quien tenía **HA activada** (p. ej. base de datos multi-AZ), un *failover* en otra región o **otro proveedor** |
| **Azure** | "Y a los dos meses fue Azure": el audio es confuso. **Sin confirmar** la fecha ("a los 2 meses" no me cuadra con lo que recuerdo, que fue pocos días después; mío, no comprobado) | Lo mismo: nadie tiene el 100 % |
| **OVH, marzo de 2021** | **Incendio** en su CPD de Estrasburgo que tumbó unos **3,6 millones de sitios web** (el profesor dijo "3,6 millones de golpes"; audio de la fecha: "1 021"). Según él, **falló el sistema de extinción y el incendio lo provocó un SAI**: "tu medida de seguridad fue una de las que provocaron todo" (afirmación suya; **sin comprobar**) | Sobrevivió quien tenía **un DRP y una copia fuera** y un entorno alternativo. **La diferencia no fue tener o no tener un fallo, sino tener un plan de recuperación aprobado.** "Eso es la alta disponibilidad" |

Fuentes consultadas por mí solo para el caso de AWS (la clase no las cita): el incidente del **20/10/2025** en us-east-1 con DNS y DynamoDB está documentado, por ejemplo, en [The Register](https://www.theregister.com/2025/10/20/amazon_aws_outage/) y en el [análisis de ThousandEyes](https://www.thousandeyes.com/blog/aws-outage-analysis-october-20-2025).

## 7 · Alta disponibilidad en la práctica (adelanto, tema posterior)

El profesor dio un **adelanto** y avisó de que es contenido nuevo del manual. No se hizo en clase por falta de tiempo.

- **Ejemplos de alta disponibilidad:** **RAID** (discos redundantes, N+1); **clúster con balanceo** (varios servidores haciendo el mismo trabajo); **IP flotante** (la Elastic IP puede saltar de un servidor a otro).
- **Failover** = si cae un servidor, se levanta o se activa otro.

**Failover manual en AWS (~20 min, la actividad la subirá, optativa en casa):**

1. Se clona el servidor (SAD1): **snapshot/imagen** y se lanza una instancia a partir de ella.
2. La **Elastic IP** está asociada al servidor original.
3. Se **para** el original y se comprueba que el servicio cae.
4. En la configuración de la Elastic IP se **reasigna al clon**. El servicio vuelve.
5. El clon tendrá el **estado del momento del snapshot**: lo posterior al snapshot se pierde. Es decir, **eso es tu RPO** (mío, enlace con el punto 3). Lo importante se deja fuera de la máquina (p. ej. caché o base de datos aparte). Víctor lo preguntó en clase y el profesor lo confirmó.

**Versión automática** (se verá en el tema 9, según el profesor): **Elastic Load Balancer**, **Auto Scaling**, **RDS Multi-AZ** (la casilla "multi-AZ" levanta otro servidor si cae el primero), **Route 53**, **ElastiCache**. Con balanceador y autoescalado "el usuario no nota nada". Aquí lo dejó "por encima".

## 8 · Examen, evaluación y calendario (clase)

> [!important] Qué dijo del examen
> - **Todo el contenido es evaluable.** Aprovecha la última semana para tocar todo ("no me dejo nada en el tintero").
> - Tipo de preguntas: **test**, **un par de preguntas de desarrollo** y, si hay algo de código o de sistemas, **ejercicio concreto**.
> - Propuesta suya: usar las clases de la **semana de repaso/simulacros** (el 30/11 empieza el siguiente trimestre) para **90 min de simulacro por trimestre**: "solo cae esto de este trimestre". **Aún no está decidido**: tiene que hablarlo con su coordinadora. Manuel propuso usar también las últimas tutorías.
> - **Preocupación suya:** que el examen dure **solo una hora**, en cuyo caso entra poco de cada trimestre ("cojo esto del 1.º, esto del 2.º, y el 3.º, más técnico, le pongo instrucciones").
> - **Calendario:** hoy es el **Tema 2**; la semana siguiente, **laboratorio de copias de seguridad** y fin del bloque.

- **Corrección de la Actividad 1:** dijo que ha leído todos los trabajos, que los ha encontrado "supercompletos", que ha puesto notas "altas, acordes al trabajo" y que **hasta no leerlos todos no pone ninguna nota**. En los exámenes corrige **pregunta por pregunta a todos** ("para que sea más justo"). **Sin confirmar** si las notas ya están subidas.
- **Laboratorio de la semana próxima** (clase): **copias de seguridad**: completa, incremental y diferencial, **frecuencia** y política, guardar el estado inicial del servidor (clon). **El lunes 2 de noviembre es festivo** (lo recordó a mitad de clase), así que el laboratorio **se mete en la clase**; la fecha exacta **sin confirmar**.

> [!warning] Contradicción con mis apuntes de calendario
> El README decía que la **Actividad 2** era de **seguridad lógica**. Hoy el profesor la describió como **seguridad pasiva**: "cómo configuramos la sala de servidores, las copias, el acceso, cuáles son tus RTO y RPO", y que la trocea para que, al llegar, solo haya que montarla. Además dijo que viene "en el siguiente trimestre". **No sé cuál es correcta**; si es la de seguridad pasiva, la fecha de entrega (18 de enero en el README) tampoco la he podido contrastar hoy.

> [!note] La Actividad 2: lo que se vio hoy
> Una **lista de comprobación** (el profesor la pidió como "documento de Excel, como si fueras un auditor", marcando *conforme / a medias / parcial / no conforme*): acceso (¿quién puede entrar? ¿hay registro y cámaras? ¿esclusa?), energía bien dimensionada (toma de tierra, sobretensiones, acometida redundante), clima (temperatura controlada, redundancia N+1), incendios y agua, y un poco de cableado. "Ojo que esto viene de la actividad."

## Dudas y cosas sin confirmar

- **Rango de temperatura** del CPD (el audio: "17 o 18 grados"). Mira Ciber.
- **Cifras de disponibilidad** (99 % y 99,9 %) y de los Tier: el audio es confuso; las anuales de los nueves las calculé yo.
- **SLA de OVH** y **datos del incendio de OVH** (extinción, SAI): tal como los dijo, sin verificar.
- **Fecha de la caída de Azure**.
- **De qué test es la pregunta errónea de MTTR**.
- **Actividad 2:** tema (seguridad pasiva o lógica) y fecha de entrega.
- **Cuándo es el laboratorio de copias** (festivo 2/11) y si habrá simulacros de examen (depende de su coordinadora).
- **Si las notas de la Actividad 1 están subidas.**

## Logística y para llevar a casa

- **Para la próxima clase** (clase): mirar los **RTO/RPO**, hacer el **ejercicio del rack** (opcional), y pensar "**qué importancia tiene tu SAD1**" (qué RTO y RPO le pondrías). **Dejar preparado el servidor SAD1** (levantarlo y pararlo, "levantando, cerrando"), porque se harán operaciones sobre él.
- **Optativo:** el failover manual con Elastic IP (apartado 7), con un clon del SAD1.
- Sigue abierto desde el 21/10: la [corrección de la Actividad 1](2026-10-21_tema2-seguridad-pasiva.md).
