---
asignatura: Ciberseguridad
fecha: 2026-10-06
tema: Tema 1 · Clase 4 · seguridad física, CPDs y el SAI
fuente: transcripción de la clase en directo (sin diapositivas adjuntas en este envío)
---
# Ciber · Clase 4 (06/10) · Seguridad física y el SAI

> Anterior: [Clase 3](2026-09-29_clase3-donde-falla-un-sistema.md) · Siguiente: [Lab 2 · Metasploitable](2026-10-09_lab2-metasploitable.md)

> «No sirve de nada cifrar el disco si alguien se lo puede llevar bajo el brazo.»
> «Si no tenemos seguridad física, la seguridad lógica no vale absolutamente para nada.»

Clase de teoría (la más «no práctica» del curso, según el propio profesor), pero que entra en el examen igual. Dos bloques: proteger el **sitio** y proteger la **energía**.

## Por qué la física va primero
Puedes cifrar el disco, tener el mejor firewall y ningún CVE sin parchear: si alguien se lleva el disco físico (un portátil robado, un comercial que viaja en taxi con la torre, un portátil olvidado en un concierto), da igual todo lo anterior — la confidencialidad ya se ha roto. Por eso en cualquier auditoría **lo físico se revisa lo primero**.

- Riesgo clásico de empresa: el comercial que se lleva solo el disco duro, no la torre entera, y lo pierde o se lo roban.
- Medidas mínimas razonables: cifrado de disco + MFA — pero ninguna de las dos sirve si el soporte físico ya no está en tu poder.
- Truco que el profesor hace con cualquier ordenador sin protección en la BIOS: arrancar con un **live USB** de Linux cualquiera, montar el disco duro interno como si fuera un segundo disco y tener acceso completo a los archivos sin contraseña del sistema. Única defensa real: bloquear en la BIOS el arranque por USB (y, aun así, desmontando el disco y metiéndolo en una carcasa/dock externo se puede seguir leyendo si no está cifrado).
- MDM (Mobile Device Management — mencionado por un alumno, Manuel): software corporativo (ej. Jamf para Mac, equivalentes para Windows/móvil/tablet) que permite borrado remoto (*wipe*) de un dispositivo perdido, robado o de un empleado despedido que no devuelve el equipo, y que además detecta comportamiento anómalo de un usuario (aviso temprano de insider / empleado descontento).

## Amenazas físicas y cómo entra alguien
No solo robo por fuerza: la vía más efectiva es la **ingeniería social** —
- Hacerse pasar por técnico de un ISP (chaleco amarillo, "vengo de Vodafone/Telefónica") para que te dejen pasar.
- Escuchar una conversación ajena (en un tren, por ejemplo) sobre una visita prevista a cierta hora y presentarse poco después alegando "tengo una reunión" — anécdota real contada en clase sobre cómo entraron a robar portátiles en un CPD así, y cómo acabaron identificando al ladrón por las cámaras.
- Mono azul + furgoneta + "venimos a repararlo" — anécdota de un compañero (Francisco) sobre un robo de máquinas de escribir en una oficina años atrás, que hizo que desde entonces no se dejara pasar a nadie sin control.
- Un juzgado que solo abría cada dos semanas y a cuya gente de mantenimiento no se le había informado de una visita prevista, mostrando lo fácil que es que el control de acceso falle por simple descoordinación.

## Qué es un CPD y por qué el edificio ya resuelve media seguridad física
Un CPD no es solo una sala con servidores: es, en palabras del profesor, **un edificio industrial** —"lo que vive ahí dentro son todo menos informáticos: son industriales"— pensado específicamente para neutralizar las amenazas físicas:
- **Acceso y robo**: trazabilidad total de quién entra y sale (tarjeta + biometría + cámaras); en los racks ya no se dan llaves físicas, se abren electrónicamente diciendo de antemano qué rack vas a usar, con un pequeño retraso programado mientras te grababan.
- **Fuego**: detección temprana y extinción por gas (no agua, porque el agua estropea el hardware igual que el fuego); cada recarga del sistema de extintores cuesta del orden de **6.000 €** y hay que probarlo periódicamente.
- **Calor/humedad**: climatización con sensores de temperatura; dentro de un mismo CPD hay zonas muy frías (donde están los servidores) y zonas de calor fuerte (donde está la parte eléctrica) — el cambio de temperatura entre pasillos es "bestial".
- **Corte de luz**: nunca hay una única acometida eléctrica; hay varias, de proveedores distintos.
- **Agua para apagar incendios**: no se usa agua directamente sobre el hardware; hay aljibes (depósitos) para emergencias que sí necesiten agua en otra parte de la instalación.
- Anécdota sobre el pasado: antiguamente se fumaba dentro de los CPD sin mayor problema (hoy impensable, todo grabado); y una curiosidad histórica sobre el uso de **argón** en sistemas de extinción (desplaza el oxígeno para apagar el fuego) y los problemas que causó antes de ajustar las concentraciones para que fueran respirables.

### CPDs por Tier (nivel de disponibilidad)
| Tier | Redundancia | Disponibilidad | Caída máx. al año (aprox.) |
|---|---|---|---|
| Tier 1 | Ninguna | 99,67% | ~29 horas |
| Tier 2 | Parcial | más alta que Tier 1 | ~1,6 horas... (salto grande hasta Tier 3) |
| Tier 3 | Doble acometida eléctrica, tolera mantenimiento sin parar | 99,9... % | ~1,6 horas |
| Tier 4 | Tolerante a fallos (redundancia total) | 99,995% | ~26 minutos |
La mayoría de los grandes proveedores (AWS, OVH, etc.) montan **Tier 3-4**. El profesor no confirmó con seguridad en qué Tier exacto está cada uno, solo que suelen ser de los niveles altos.

### CPDs modulares (lo que más le gusta de esta clase)
Concepto relativamente nuevo: en vez de construir el edificio entero in situ, llegan **módulos prefabricados tipo contenedor de barco** (como los que se ven en un tren de mercancías) ya montados de fábrica con todo integrado — electricidad, climatización, extinción de incendios — y se instalan donde interese (preferentemente en sitios fríos, para ahorrar en refrigeración). Ejemplo que proyectó en clase: los módulos de **Colt**.
- Ejemplos curiosos de ubicaciones de CPD que mencionó: el más grande del mundo, en **China** (del tamaño de decenas de campos de fútbol); uno de **Meta/Facebook en Suecia**, cerca del círculo polar, refrigerado con aire frío cercano a Groenlandia; y el proyecto más conocido de CPD **submarino** de Microsoft (el famoso "Project Natick", al que llama "como la Sirenita"), que usa el agua fría del mar para refrigerarse gratis.
- Un alumno (Manuel) añadió que ya se está hablando de **CPDs espaciales**: Elon Musk y Google estarían probando los primeros nodos de computación en el espacio, comunicados vía Starlink, para medir la latencia — comentario del propio profesor: no lo tenía apuntado, lo anota para documentarse, así que queda como dato a verificar, no confirmado en clase.
- Nota ambiental que el profesor subraya: los CPD a gran escala son una de las industrias más contaminantes de los últimos años (consumo eléctrico de refrigeración comparable al de una ciudad pequeña, más el uso intensivo de agua).

## El SAI (UPS en inglés)
Batería/sistema que protege frente a cortes y picos de tensión. Tipos, de más básico a más robusto:
| Tipo | Qué hace | Para qué sirve |
|---|---|---|
| Offline / Stand-by | Salta a batería solo al cortarse la luz (pequeño salto perceptible) | Un PC de casa, uso doméstico |
| Línea interactiva | Además regula subidas y bajadas de tensión | Un servidor pequeño; evita que una subida de tensión queme electrodomésticos/equipos |
| Online / doble conversión | Corriente constante, sin salto perceptible al cortarse la luz | Un CPD pequeño; necesitaría doble acometida eléctrica, por eso no tiene sentido en casa |

**Fórmula de dimensionado que da en clase** (no obliga a calcularla, es orientativa):
```
1. Suma los vatios de todo lo que quieres proteger (ordenador, monitor, impresora, Raspberry...)
2. Pasa esa potencia a VA (voltiamperios): VA = vatios / 0,6   (0,6 es el factor de potencia típico)
3. Añade un margen del 20-30% sobre ese resultado
```
Precios orientativos que dio: línea básica desde ~50-90 €; línea interactiva para servidor pequeño ~130-150 €; online/doble conversión (tipo "mini CPD") entre ~1.000 y 1.800 €; para proteger algo del orden de 10 kW ya se habla de varios millones de euros (CPD real).

### Jerarquía completa de respaldo energético (de menor a mayor aguante)
1. **Regleta** normal → si se va la luz, no hay nada que hacer.
2. **SAI** → cubre huecos de segundos/minutos (ejemplo real de una pyme: 20 minutos de aviso antes de apagar ordenadamente).
3. **Grupo electrógeno** (generador diésel) → aguanta horas o días mientras haya combustible; lo tienen preparado sitios donde no se puede permitir perder la cadena de frío o el servicio: supermercados (ejemplo dado: Mercadona, por las neveras), hospitales, CPDs.
4. **Motores de barco / locomotoras** como generador de reserva en CPDs grandes (ejemplo: el de Colt, con el generador en la azotea).

### Software de monitorización de SAI mencionado
**NUT (Network UPS Tools)** — herramienta open source que el profesor encontró y mostró en directo (sin tenerlo conectado a un SAI real para probarlo): informa del estado de un SAI conectado (porcentaje de batería, carga, etc.). Antiguo (origen a mediados de los 90, aunque el profesor dio la fecha de 2012 para una versión concreta), escrito en parte en Java, todavía mantenido. Útil como idea para un TFC si se quiere montar monitorización de energía.

## Cómo encaja esto en los pilares (CID)
La seguridad física protege sobre todo la **disponibilidad** (que el servicio siga funcionando) — es el pilar que más se toca cuando falla algo físico. Pero si alguien roba un disco físicamente, se pierden **también** confidencialidad e integridad de golpe: ni el cifrado ni las copias de seguridad salvan nada si el atacante ya tiene el soporte original en la mano.

## Casos reales de fallo físico (mencionados en clase)
- **Incendio de OVH en Estrasburgo** (ya visto en clases anteriores): empezó en un SAI y acabó calcinando el CPD entero.
- **British Airways**: un fallo de alimentación en un CPD dejó **75.000 pasajeros afectados** y le costó a la aerolínea del orden de **80 millones de libras**.
- Caídas conocidas de **AWS** y **Azure** en los últimos dos años: ninguna fue un ciberataque, en ambos casos el origen fue un fallo físico/de cable.
- Anécdota (sin fuente cerrada, contada de memoria por el profesor) sobre una persona cavando con una pala que cortó accidentalmente un cable de fibra que dejaba sin internet a todo un país durante más de una semana — queda como anécdota, no como dato verificado.
- Anécdota de un alumno (Manuel) desde su propia experiencia profesional: al tender un cable nuevo en el CPD de Gibraltar (ubicado en la planta baja del World Trade Center, de la operadora Gibtelecom, entonces única operadora de internet de la isla) conectaron por error el cable en el sitio equivocado y tumbaron **5 horas de internet de todo Gibraltar**, afectando a los casinos online que operaban allí (coste estimado en varios millones de euros); tras el incidente se cambió la normativa local sobre CPDs.

## Deberes / práctica de la semana (no obligatoria, no puntúa)
- Dimensionar un SAI propio con la fórmula de arriba (opcional; si ya se hizo con otro profesor, no hace falta repetirlo).
- Hacer un inventario físico de lo que se querría proteger con un SAI.
- **Test 1** sigue abierto (medio punto, 10 preguntas, se puede hacer en cualquier momento del curso — no hay límite de intentos confirmado por el profesor, un alumno preguntó y quedó sin resolver en el momento).
- Siguiente clase (Lab, jueves): primer laboratorio «de verdad» con una máquina Ubuntu propia creada para la ocasión (con Security Groups y servicios deliberadamente vulnerables) para atacarla con Kali — cada alumno la levanta, prueba y apaga él mismo (no se deja encendida, por seguridad).
- Clase 5: criptografía simétrica y asimétrica, control de accesos.
