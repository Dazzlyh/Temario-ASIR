---
asignatura: Sistemas Gestores de Bases de Datos (SGBD)
fecha: 2026-10-26
tema: Tema 4 · Optimización y monitorización del rendimiento en SGBD (índices, planes de ejecución, alertas) + entrega 1 del TFC
fuente: transcripción de la clase en directo + presentación «Tema 4 – Optimización y Monitorización del Rendimiento en SGBD» (TEMA4.pdf, 11 págs., solo imágenes) + resumen «Tema 4 – Optimización e índices» (PDF)
---
# SGBD · Tema 4: optimización, monitorización e índices (26/10)

> Anterior: [Tema 3: scripts, eventos y triggers (19/10)](2026-10-19_tema3-scripts-eventos-triggers.md) · Profesor: César Carrión

> [!warning] Corrección al índice del repo
> El README decía que el Tema 4 era "transacciones". **No lo es**: el Tema 4 es *optimización y monitorización del rendimiento* (así lo dicen las dos presentaciones y el profesor). Las transacciones (`commit`/`rollback`) se mencionaron como contexto. Según el profesor, el **Tema 5 trata de copias de seguridad**.

## Lo imprescindible

> [!important] Cómo se evalúa este tema (dicho por el profesor)
> - Es el tema "empalagoso": **no pedirá sintaxis de memoria** (`EXPLAIN`, crear un índice o un clúster de índices) ni scripts.
> - La **única pregunta posible** del Tema 4: te describe un escenario en el que "el sistema va lento" y tú explicas **los pasos que seguirías para encontrar el problema, físicos y lógicos** (lógicos = lo que se hace en la base de datos). Es pensamiento crítico.
> - Lo que sí quiere del trimestre para el examen de **mayo**: scripts, **procedimientos almacenados** (qué son, qué significan, cómo se crean) y **commit/rollback** en transacciones. "Superimportante".
> - Esta fue **la última clase de SGBD "de base de datos"** antes de lo que llamó "la semana previa" (no queda claro a qué se refiere; **sin confirmar**). El viernes la clase es de TFC.

## 1. Ciclo de vida del rendimiento (5 pasos, diapositiva 2)

| Paso | Qué es | Lo que dijo el profesor |
|---|---|---|
| 1. **Comprender** | Evaluar el estado actual con métricas base (tiempo de respuesta, uso de recursos) | **El más importante.** Entender qué significa "va lento" para el usuario, cuál era el rendimiento inicial, qué se considera aceptable |
| 2. **Identificar** | Localizar cuellos de botella (consultas lentas, bloqueos, ineficiencia de memoria) | No asumir que es el servidor: puede ser red, switch, disco… |
| 3. **Establecer** | Metas de rendimiento claras y medibles | ¿1 minuto, 10 s? Define qué es "bueno" |
| 4. **Aplicar** | Estrategias técnicas: ajuste de índices, reescritura de consultas, redistribución | Normalmente índices |
| 5. **Evaluar** | Medir el impacto y ajustar iterativamente (*tuning* constante) | Vuelve a medir: es un ciclo |

- **Rendimiento no es un número fijo**: depende de la velocidad que necesita el usuario (ejemplo: venta de entradas de un concierto, donde 5 min de espera colapsan el sistema).
- Pregunta clave al usuario: ¿"no entra" significa que no conecta o que se queda colgado validando usuario/contraseña?
- **Medir en vacío**: probar con nadie más conectado (el profesor ha ido un sábado a una empresa) para ver el rendimiento mínimo de referencia.
- Si ya iba lento al ponerlo en marcha, el sistema **solo empeorará** al llenarse.
- **Medir → cambiar → volver a medir** (resumen).

## 2. Diagnóstico paso 2: dónde buscar el cuello de botella

Elementos susceptibles de diagnóstico (diapositiva 4):

| Área | Qué mirar |
|---|---|
| **Consultas y lógica** | Tiempos de ejecución, uso del plan de ejecución, **table scans** |
| **Concurrencia** | Bloqueos entre transacciones, nivel de contención, procesos en segundo plano |
| **Estructuras físicas** | Eficacia de los índices, fragmentación de tablas, crecimiento de archivos temporales |
| **Recursos del sistema** | CPU, caché de datos en memoria, E/S en disco |

### Checklist de "pasos físicos" (lo que explicó con ejemplos; útil para la pregunta de examen)

> [!important] Regla del profesor: empezar por lo sencillo y aislar variables
> Probar con el servidor y **un solo cliente** conectados directamente, sin nada más en la red; cambiar **una variable cada vez** (cable, switch, tarjeta…). Si cambias varias cosas a la vez, no sabes cuál era el problema.

- **Servidor sobredimensionado no arregla nada** si el cuello está en otro sitio (ejemplo: comprar un servidor de 6 000 € y seguir igual de lento).
- **Red**: un servidor con una tarjeta de red de 10 Gb que atiende 10 transferencias de ficheros reparte el ancho (1 Gb cada una). Un servidor que **además es servidor de ficheros** satura la red con transferencias grandes aunque las consultas SQL sean pequeñas.
- **Switch**: un switch de 100 Mb limita a 100 Mb aunque la tarjeta sea de 1 Gb; con 10 clientes simultáneos son ~10 Mb cada uno. Un solo enlace entre el switch de usuarios y el de servidores (1 Gb) también limita.
- **Dominio de broadcast demasiado grande** (David Cantos): una red plana con todas las IP juntas. Segmentar en subredes (servidores, administración, oficina técnica, almacén…).
- **Conflicto de IP**: un equipo con IP manual que choca con otro. DHCP evita colisiones. TCP es orientado a conexión y se "vuelve loco" preguntando dónde está el otro; satura la red.
- **Bucle de red (looping)**: dos switches unidos con dos cables, o ambos extremos de un cable en dos puertos del router. Recomendación: **switches gestionables/programables**, que identifican equipos por IP/MAC, aíslan y muestran el tráfico.
- **Conexión a Internet** (consultas remotas): el ancho contratado no es el garantizado. El profesor citó un **caudal garantizado (CIR) típico del ~10 %** de lo contratado; es dato suyo de experiencia, **sin verificar**.
- **Disco/almacenamiento**: disco IDE/SATA antiguo frente a SSD/NVMe; un **mirror (RAID 1)** escribe dos veces, así que **ralentiza** las escrituras.
- **Equipos/aplicaciones antiguas**: cliente en Visual Basic 6 contra una BD de 1996; el miedo al cambio de los usuarios es real.
- Tarjetas de red que se calientan y fallan; el problema puede ser incluso capa 1.

### Pasos lógicos (en la base de datos)

- **Evitar `SELECT *`**: pide los 25 campos cuando solo quieres el teléfono. Pide solo las columnas necesarias, o crea una **vista**.
- **Access como servidor**: te manda toda la tabla y filtra en local; peso enorme. Mejor trabajar contra SQL.
- **Ordenar**: si los usuarios siempre piden un orden, construir la **vista ya ordenada** evita que el `ORDER BY` ralentice cada consulta (pregunta de Víctor, el profesor la valoró como buen escenario).
- **Consultas lógicas mal formuladas** o con partes que sobran.
- **Concurrencia/transacciones**: lotes de varios `INSERT`/`SELECT` que deben ejecutarse juntos (commit/rollback) también retrasan al servidor.
- **Caché y servidores secundarios**: si el usuario no necesita datos en tiempo real, sincronizar cada 6/12/24 h y que consulte una réplica, para no cargar al principal.
- **Limpieza de datos antiguos**: facturas de hace 5 años → mover a una tabla histórica (con trigger/evento), como en el Tema 3.
- **Scripts de medición**: un script que mide el tiempo de acceso de cada consulta durante un periodo y decide con esos datos (la idea de Francisco, que el profesor confirmó).

## 3. Herramientas de monitorización (diapositiva 5)

| Herramienta | Motor / ámbito | Para qué |
|---|---|---|
| **Oracle Enterprise Manager (OEM)** | Oracle | Interfaz gráfica de métricas en tiempo real |
| **`pg_stat_statements`** | PostgreSQL (extensión) | Estadísticas de consultas |
| **Prometheus / Grafana** | Multi-plataforma, código abierto | Monitorización global y visualización. El profesor recomendó Grafana por sencilla |
| **Extended Events (XEvent Profiler)** | SQL Server (SSMS) | Captura ligera de eventos; **reemplaza a SQL Profiler** |
| **Activity Monitor (Monitor de actividad)** | SQL Server (SSMS) | Vista en tiempo real de CPU, E/S y consultas activas |
| **Query Store** | SQL Server (SSMS) | Histórico de estadísticas y planes de ejecución |
| **Performance Monitor** | Windows | Métricas físicas de CPU, memoria y disco |
| **Database Mirroring Monitor** | SQL Server (SSMS) | Caso práctico: latencia de sincronización |

- Qué vigilar (resumen): **consultas lentas, índices que no se usan, espacio y uso de memoria**.
- Para el TFC: incorporar Grafana/Prometheus y "trastear" cuenta como referencia a la asignatura, aunque no se profundice.

## 4. Intervención física (diapositiva 6)

| Área | Acciones |
|---|---|
| **Almacenamiento** | Mantenimiento de la **fragmentación**; controlar el tamaño y uso de **tempdb** (archivos temporales); eliminar y reorganizar archivos obsoletos |
| **Procesos** | Ajustar la **concurrencia**; programar **backups y mantenimiento en horas valle** |
| **Memoria** | Ajustar la **caché de datos** (que las consultas frecuentes no lean disco); controlar la **memoria compartida** para no asfixiar al SO |

## 5. Intervención lógica: plan de ejecución, `EXPLAIN`, `ANALYZE`

El **plan de ejecución** es el mapa de cómo el optimizador resolverá la consulta (representación gráfica o XML).

- **Árbol de ejecución**: nodos = operaciones; flechas = flujo de datos; **el grosor de la flecha indica el volumen de filas**.
- **Operadores**: lógicos (operación conceptual) y físicos (cómo la implementa el motor).
- **Coste**: tiempo estimado por el optimizador para resolver el operador.
- Muchos **table scans** ⇒ probablemente **falta un índice**.

| Sentencia | Qué hace | Ejemplo (PDF) |
|---|---|---|
| `EXPLAIN` | Describe cómo el optimizador planea ejecutar la consulta (orden de uniones, uso de índices). **No ejecuta** la consulta | `EXPLAIN SELECT * FROM empleados WHERE departamento = 'Ventas';` |
| `ANALYZE` | Recopila estadísticas reales sobre el contenido y distribución de las tablas en el catálogo, para que el optimizador decida mejor | `ANALYZE empleados;` |

> [!warning] Cuidado con la sintaxis y con lo que dijo el profesor
> - El profesor dijo en clase que `EXPLAIN` "funciona con SQL Server". **Es dudoso**: `EXPLAIN`/`ANALYZE` con esa sintaxis son típicos de MySQL/MariaDB y PostgreSQL; en SQL Server los planes se ven con el plan de ejecución gráfico de SSMS o `SET SHOWPLAN_...` (conocimiento mío, **no visto en clase**). Como no pide sintaxis en el examen, el matiz no es evaluable, pero conviene no escribirlo como "T-SQL".
> - Habló de un "porcentaje de optimización" (un 67 % lejos del 100 % óptimo) que da el análisis. **No aparece en las diapositivas y no lo puedo confirmar**; probablemente se refería al coste relativo del plan de SSMS. No lo uses como dato.
> - Usó ejemplo de tabla con 3-4 índices (id, matrícula, nombre+DNI…) de los que el análisis muestra que solo se usa uno: se pueden eliminar, **pero antes haciendo copia de seguridad** (si no lo has diseñado tú, puede romper otra parte).

## 6. Índices (el mecanismo de aceleración)

- **Un índice no es una copia de los datos: es una estructura de punteros** (como el índice analítico de un libro). Permite localizar el registro sin recorrer toda la tabla (*table scan*).
- Efecto: reduce mucho la E/S de lectura **a costa de un ligero sobrecoste en las escrituras** (`INSERT`/`UPDATE`/`DELETE`). **Demasiados índices ralentizan las escrituras.**
- ¿En qué columnas? Las que aparecen en **`WHERE`, `JOIN` y `ORDER BY`**.
- **Un índice mal diseñado**: con mucho texto o compuesto. Se prefieren **índices numéricos** (autoincrementales, un ID) frente a texto, y **sin duplicados**. Ejemplos de mala idea (profesor): matrícula, DNI o nombre+apellidos como índice; mejor un ID.
- El índice permite ir al puntero directo en vez de ordenar toda la tabla con `ORDER BY`.

### Agrupado vs no agrupado

| Característica | **Clustered** (agrupado) | **Non-clustered** (no agrupado) |
|---|---|---|
| Estructura física | **Reordena físicamente** las filas en disco según el índice | No altera el orden físico; estructura separada con **punteros** a las filas |
| Límite por tabla | **Solo 1** (dicta el almacenamiento) | **Varios** |
| Uso ideal | Columnas con muchos valores únicos (p. ej. **clave primaria**) | Columnas usadas en `WHERE`/`JOIN` que no alteran el orden global |
| Coste de crearlo | Alto en tablas con datos | Menor |

- Además, el resumen menciona **Unique**: garantiza que no se repita el valor.

### Gestión de índices (DDL)

```sql
-- Crear (no agrupado por defecto)
CREATE INDEX idx_apellido ON dbo.Clientes (Apellido);

-- Crear agrupado (operación costosa en tablas pobladas)
CREATE CLUSTERED INDEX idx_pedidos_id ON dbo.Pedidos (ID);

-- Eliminar (recupera espacio / quita cuellos de botella en escrituras)
DROP INDEX idx_apellido ON dbo.Clientes;
```

El resumen añade: `CREATE INDEX idx_Cliente ON Ventas(ID_Cliente);` y `CREATE CLUSTERED INDEX idx_Ventas_Fecha ON Ventas(Fecha_Venta);` ("elegir la columna por la que más se consulta"). Mantenimiento: **revisar** los índices (fragmentación, uso) y reconstruirlos si hace falta.

> [!important] Qué hacer si no sabes cuánto se usa un índice
> Primero medir (plan de ejecución/estadísticas), luego decidir. **No borres índices "porque no los veo"** sin backup: el profesor insistió en el riesgo.

## 7. Prevención: alertas de rendimiento

- Monitorización **proactiva**: fijar **umbrales**; cuando una métrica los supera, el SGBD/Grafana genera una **alerta**.
- Una alerta puede **disparar un evento, un trigger o un procedimiento almacenado** que haga una limpieza genérica. Enlaza con el Tema 3 (eventos y triggers) y con los procedimientos almacenados.
- **Caso práctico (PDF)**: *Database Mirroring* en alta disponibilidad (instancia principal + reflejo). La latencia es el enemigo. Herramienta: **Database Mirroring Monitor** (SSMS). **Umbral crítico: latencia de sincronización > 5 segundos.** Acción: la alerta avisa al DBA antes de que la retención de transacciones colapse la base principal.

## TFC: primera entrega (9 de noviembre)

Aviso del profesor al inicio de la clase (no es de SGBD en sí):

- **Fecha: 9 de noviembre.** Extensión orientativa: **6-8 páginas**. **No es técnica**; no hay que profundizar en el desarrollo.
- Contenido, tres partes:
  1. **Motivación personal/de equipo** (½-1 página): por qué hacéis este proyecto y cómo vais más allá de lo visto en clase.
  2. **Conexión con las asignaturas del ciclo**: cómo cada módulo encaja con vuestra idea (BD: permisos de usuarios, copias de seguridad; SAD: ciberseguridad; IAW: WordPress informativo, etc.).
  3. **Qué existe ya en el mercado** y **en qué os diferenciáis** (si no aportáis nada nuevo, decirlo y justificarlo).
- Segunda entrega (**diciembre**, fecha sin precisar): ahí sí hay que concretar BD, campos y elementos.
- Consejo del feedback: **centrarse en ASIR**, no en el desarrollo de la aplicación web.
- El profesor dijo que subiría el **feedback de los borradores la noche del 26/10**; la clase del **viernes** (30/10) se dedica a dudas sobre ese feedback.

## Dudas y cosas sin confirmar

- **No se vio en clase ninguna práctica** de índices ni de `EXPLAIN`: el profesor dijo que tenía ejemplos preparados pero de scripts, y no los enseñó. Los ejemplos de SQL son los de las diapositivas.
- El profesor **no recorrió todas las diapositivas**; "ni siquiera hemos pasado de transparencia" en la primera mitad. Aun así las 11 páginas están en el PDF y se recogen arriba.
- `EXPLAIN` en SQL Server y el "67 %": ver aviso en la sección 5.
- "La semana previa": no queda claro a qué se refiere (¿semana de evaluación o prácticas?). **Sin confirmar**.
- Ejemplo del profesor: el CIR del 10 % y datos de empresas reales son anécdotas, no contenido evaluable.

## Logística y para llevar a casa

- [ ] **TFC**: entregar la primera memoria el **9/11** (6-8 págs.: motivación, conexión con asignaturas, mercado/diferenciación). Mirar el feedback (debería estar ya subido) y llevar dudas al viernes 30/10.
- [ ] Preparar para el examen: ser capaz de **explicar el ciclo de 5 pasos** y de **describir pasos físicos y lógicos** ante "el sistema va lento".
- [ ] Repasar para mayo: **procedimientos almacenados**, **scripts** y **commit/rollback**.
- [ ] Recordar: **clustered = 1 por tabla, reordena la tabla; non-clustered = varios, con punteros**.
- [ ] Opcional (TFC): montar Grafana/Prometheus o Query Store como referencia al módulo.
