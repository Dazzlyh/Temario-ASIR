# Tema 2. Seguridad física y ambiental
*Ciberseguridad*

## Índice
Esquema · 2.1 Introducción y objetivos · 2.2 Protección física de equipos y servidores · 2.3 Implementación de sistemas de alimentación ininterrumpida · 2.4 Referencias bibliográficas · A fondo · Entrenamientos

## Esquema
**Seguridad física y ambiental**
- **Seguridad**
  - *Medidas de protección:* ubicación estratégica de los equipos, dotados de vigilancia y autentificaciones, además de sistemas antiincendios.
  - *Sistemas de Alimentación Ininterrumpida (SAI):* protección ante cortes eléctricos; tipos Off-Line, Line-Interactive, On-Line; aplicaciones en centros de datos y sistemas críticos.
  - *Factores clave para la seguridad física:* buen mantenimiento de la infraestructura, combinada con protección contra fluctuaciones eléctricas y una gestión adecuada en la instalación eléctrica de cables y ventilación.
- **Amenazas:** 1. Acceso no autorizado · 2. Robo o sabotaje · 3. Desastres naturales.

---

## 2.1. Introducción y objetivos
En ciberseguridad se pone a menudo el foco en lo lógico (firewalls, antivirus, cifrado), pero un aspecto crítico es la **seguridad física y ambiental**, que protege dispositivos e infraestructura frente a accesos no autorizados, daños accidentales y condiciones ambientales adversas.

Abarca desde la ubicación estratégica de los equipos hasta los controles de acceso y sistemas de monitoreo. Sin protección adecuada, un atacante con acceso físico a un dispositivo podría comprometer la integridad y confidencialidad de la información. Los **SAI** son cruciales para la continuidad operativa.

Objetivos:
- Comprender la importancia de la seguridad física y ambiental en la protección de infraestructuras y la continuidad operativa.
- Identificar los principales riesgos: accesos no autorizados, manipulación indebida de dispositivos y desastres naturales.
- Analizar mejores prácticas en ubicación y protección de equipos y servidores.
- Explorar el papel de los SAI en la prevención de cortes de energía.
- Evaluar la efectividad de los controles de acceso físicos (biometría, vigilancia, medidas perimetrales).
- Comprender el impacto de los factores ambientales y cómo mitigarlos (temperatura, humedad, incendios).
- Desarrollar un enfoque integral que combine medidas físicas, lógicas y operativas.

---

## 2.2. Protección física de equipos y servidores
La seguridad física protege los dispositivos a dos niveles:
- **Protección del hardware:** mantener la integridad de dispositivos, periféricos (discos duros, USB…) y componentes físicos.
- **Protección de los datos:** el objetivo de los ciberdelincuentes suele ser obtener información, no destruir el dispositivo; hay que proteger la transmisión y el almacenamiento.

### ¿Qué incidentes están relacionados con la seguridad física?
Desde un portátil desbloqueado fuera de nuestra vista hasta un USB perdido.

- **Acceso físico:** si un tercero tiene acceso físico, las probabilidades de éxito se multiplican. Ej.: dejar el portátil sin bloquear en un tren; riesgos: leer correos, modificar información, robar datos o infectar con malware mediante un USB.
- **Integridad física:** proteger los dispositivos de golpes, caídas o desperfectos por mala manipulación o mantenimiento incorrecto. Ej.: un disco duro de copias de seguridad que se cae de una estantería.
- **Exposición de la información:** fugas o pérdidas por falta de buenas prácticas: cuaderno con contraseñas, agenda con datos, publicar información en redes sociales. Ej.: un post-it en el portátil con usuario y contraseña del correo.

La seguridad física abarca también desastres naturales y robo de dispositivos.

### Ubicación estratégica
- **Criterios de selección del sitio:** centros de datos lejos de zonas propensas a inundaciones, terremotos o huracanes; en lugares discretos.
- **Diseño del espacio:** ventilación, iluminación y gestión de cables; áreas de trabajo ergonómicas y organizadas.

### Control de acceso físico
- **Barreras perimetrales:** vallas, puertas reforzadas, cerraduras electrónicas.
- **Sistemas de vigilancia:** cámaras y sensores de movimiento para detectar actividades sospechosas en tiempo real.
- **Autenticación biométrica:** huellas, reconocimiento facial o iris.

### Prevención de factores ambientales
- **Temperatura y humedad:** rango seguro, generalmente **18 °C a 24 °C** con humedad relativa del **40 a 60 %**, mediante sistemas HVAC.
- **Protección contra incendios:** detección y extinción automática (rociadores o gas limpio, p. ej. **FM-200**).
- **Aislamiento eléctrico:** puesta a tierra y protectores contra sobretensiones.

---

## 2.3. Implementación de sistemas de alimentación ininterrumpida
Un **SAI** (UPS, *Uninterruptible Power Supply*) proporciona energía de respaldo ante interrupciones o fluctuaciones del suministro. Esencial para continuidad operativa y protección de dispositivos críticos.

### Importancia de los SAI
- **Protección de equipos sensibles** (servidores, telecomunicaciones, equipos médicos).
- **Continuidad del negocio:** los cortes causan pérdidas económicas y daños reputacionales.
- **Prevención de pérdida de datos** ante apagones repentinos.

### Componentes principales

| Componente | Descripción |
|---|---|
| **Baterías** | Almacenan energía para cortes. Dos tipos: **plomo-ácido reguladas por válvula (VRLA)** (uso común en SAI pequeños y medianos) y **iones de litio** (más livianas, mayor vida útil, más costosas). |
| **Convertidores (inversores)** | Transforman la energía almacenada (DC) en corriente alterna (AC). |
| **Rectificadores** | Convierten la AC de la red en DC para cargar las baterías. |
| **Unidad de control** | Supervisa y gestiona las operaciones del SAI, incluyendo el estado de las baterías y la carga. |
| **Filtros de supresión de picos** | Protegen contra sobretensiones y picos de tensión. |

### Tipos de SAI
- **Off-Line o Standby:** operan en modo pasivo hasta que ocurre un corte; para equipos básicos (PC). Tiempo de transferencia: **5 a 20 ms**.
- **Line-Interactive:** protegen contra fluctuaciones menores de tensión con reguladores automáticos de voltaje (**AVR**); pequeñas oficinas. Tiempo de transferencia: **inferior a 10 ms**.
- **On-Line o de doble conversión:** alimentación constante; convierte AC→DC→AC; ideales para centros de datos y hospitales. Tiempo de transferencia: **0 ms**.

### Principales aplicaciones
- **Centros de datos:** mantienen servidores durante cortes breves y facilitan el apagado ordenado en interrupciones prolongadas.
- **Sistemas médicos:** respiradores y monitores críticos.
- **Telecomunicaciones:** torres celulares y sistemas de comunicaciones.
- **Industria manufacturera:** evitan interrupciones en procesos automatizados.

### Dimensionamiento
- **Potencia** (W o VA): al menos **25 % superior** a la carga conectada.
- **Autonomía:** tiempo que puede dar energía antes de agotar las baterías.
- **Factores ambientales:** temperatura, humedad y ventilación.

### Mantenimiento y pruebas
- **Pruebas de carga** bajo condiciones simuladas de interrupción.
- **Reemplazo de baterías:** generalmente cada **3-5 años**.
- **Limpieza y verificación** de conexiones, filtros y ventiladores.

---

## 2.4. Referencias bibliográficas
- Agencia Española de Protección de Datos. (2023). *Guía sobre el uso de videovigilancia en entornos de alta seguridad.* AEPD, Madrid.
- Comisión Europea. (2022). *Directrices para la implementación del RGPD en centros de datos.* Oficina de Publicaciones de la UE.
- INCIBE. (2024). "Análisis comparativo de sistemas antiincendios en CPD". León.
- Centro Criptológico Nacional. (2024). "Informe de cumplimiento del ENS en la administración pública". CCN, Madrid.
- INCIBE. (2024). "La formación como pilar de la seguridad en infraestructuras críticas". León.
- ENISA. (2024). *Informe de 2024 sobre el estado de la ciberseguridad en la Unión.* https://www.enisa.europa.eu/publications/report-files/ncaf-translations/national-capabilities-assessment-framework-es.pdf
- DORLET. (2024). *Informe anual sobre tendencias en seguridad física.* Madrid.
- Gómez-Barrero, M., et al. (2023). Avances en sistemas biométricos multimodales para control de acceso. *Revista de la Universidad Politécnica de Madrid, 45*(3), 78-92.
- Jurado del Águila, M. (2020). *La Ciberseguridad en el Marco Europeo. El caso de España.* Universidad de Almería.
- Red Española de Supercomputación. (2023). *Estudio sobre la resiliencia de CPD frente a desastres naturales.* Barcelona.

---

## A fondo
> **Nota:** en el material original esta sección contiene recursos *placeholder* que no corresponden al tema: «Pobreza y migraciones» (Castro, A. (2010), *Revista Derecho del Estado*, (24), 65-80, https://www.redalyc.org/articulo.oa?id=337630234004) y el vídeo «Jaques Derrida: la huella» (Canal22, 2017, https://www.youtube.com/watch?v=udKVbuvZGbQ), ambos con el texto de plantilla «Justifica la elección del recurso…».

---

## Entrenamientos

### Entrenamiento 1: implementación de un control de acceso físico seguro
**Planteamiento:** sistema de control de acceso físico para restringir la entrada a zonas críticas.
1. Evaluar requisitos de seguridad del área, normativa y riesgos.
2. Seleccionar un sistema de autenticación: RFID, biometría o PIN.
3. Configurar un registro de accesos con trazabilidad mediante software de gestión.
4. Implementar alertas para accesos no autorizados (intentos fallidos o fuera de horario).
5. Pruebas y simulaciones para ajustar parámetros.

**Solución:** solo entra personal autorizado, se registra cada acceso y se generan alertas ante intentos no autorizados.

### Entrenamiento 2: configuración de un SAI
**Planteamiento:** garantizar la continuidad operativa de servidores y dispositivos críticos.
1. Determinar la carga total para elegir la capacidad adecuada.
2. Elegir el tipo (Off-line, Line-Interactive u On-line).
3. Configurar la conexión del SAI a la red eléctrica y los equipos.
4. Habilitar notificaciones automáticas de fallos eléctricos y estado de batería.
5. Pruebas de desconexión eléctrica para comprobar autonomía y apagado seguro.

**Solución esperada:** respaldo energético suficiente para garantizar la continuidad del servicio.

### Entrenamiento 3: protección contra desastres naturales en un centro de datos
1. Análisis de riesgos ambientales (inundaciones, terremotos, incendios).
2. Ubicación segura de los servidores; elevar los equipos si es necesario.
3. Sensores de humedad, temperatura y humo con alerta temprana.
4. Planes de contingencia: respaldos externos y procedimientos de evacuación de equipos.
5. Capacitar al personal en respuesta a emergencias.

**Solución:** sistemas críticos protegidos y plan de recuperación ante desastres.

### Entrenamiento 4: sistema de videovigilancia para seguridad física
1. Seleccionar puntos estratégicos (accesos, pasillos, zonas críticas).
2. Cámaras con visión nocturna y detección de movimiento.
3. Almacenamiento seguro de grabaciones con cifrado y acceso restringido.
4. Alertas automáticas al personal de seguridad.
5. Pruebas operativas (calidad de imagen, alertas, funcionamiento).

**Solución:** cobertura efectiva de áreas críticas, grabaciones accesibles solo por personal autorizado y alertas en tiempo real.

### Entrenamiento 5: seguridad perimetral para un edificio empresarial
1. Evaluar puntos vulnerables en el perímetro (accesos no controlados, zonas con visibilidad reducida).
2. Instalar barreras físicas: vallas, puertas reforzadas, cerraduras electrónicas.
3. Sensores de movimiento y alarmas.
4. Iluminación perimetral automatizada.
5. Capacitar al personal de seguridad en protocolos de respuesta rápida.

**Solución:** perímetro que disuada accesos no autorizados y permita respuesta rápida.
