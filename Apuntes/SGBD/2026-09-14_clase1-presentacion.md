---
asignatura: Sistemas Gestores de Bases de Datos (SGBD)
fecha: 2026-09-14
tema: Clase 1 · presentación del módulo, organización y evaluación
fuente: transcripción de la clase en directo
---
# SGBD · Clase 1 (14/09) · Presentación del módulo

> Siguiente: [Tema 1: relacional, ANSI/SPARC y el rol del DBA](2026-09-21_tema1-conceptos-relacional-ansi-sparc.md)

Clase introductoria (contaba oficialmente como "semana 1"; la primera clase con contenido fue el lunes 21/09), sin contenido técnico de examen. Organización del curso.

## El profesor
**César Carrión**. Es también el tutor del grupo este curso. El año pasado daba SAD e IAW; este año esas dos las dan otros compañeros (Damián y Jairo respectivamente) — él se centra en SGBD y en el seguimiento de los TFC.

## Cómo funciona la asignatura
- **Clases los lunes.** Por eso el calendario de este módulo en concreto sufre mucho los festivos (muchos festivos "se mueven" al lunes cuando caen en domingo).
- Para todo el primer trimestre hay solo **5 días de clase** (semanas con clase real: 21/09, 28/09, 5/10, 19/10, 26/10 — las semanas del 2/11 y 9/11 no hay clase por estar cerca del simulacro de examen del 23/11).
- En todo el curso: **16 días de clase** en total (15 si se cuenta solo lo lectivo del tercer trimestre nuevo). Dato que dio el propio profesor: este año, al haber 3 trimestres en vez de 2 como el curso anterior, hay un ~33% más de clases que las que tuvo la promoción anterior en esta misma asignatura.
- Material: programación didáctica (PCA/PGA) y guía del estudiante, disponibles en la sección "Archivos" de la plataforma (se suben los primeros días). Dudas de clase al foro; el profesor responde en menos de 24h.
- Sube todas las presentaciones que use a la plataforma, igual que el resto de profesores de este módulo.
- Las tutorías colectivas (los viernes, cada 2 semanas aprox. de 15:00 a 16:00) se pueden aprovechar para repasar contenido o incluso hacer un repaso de SQL básico de 1º (tablas, consultas, vistas) si hace falta; las tutorías individuales normalmente no se graban salvo acuerdo mutuo.

## Qué es esta asignatura (y qué no es)
El nombre importa: **no es "Gestión de Bases de Datos", es "Administración de Sistemas de Gestión de Bases de Datos"**. La distinción que marca el profesor:
- Un SGBD (motor de base de datos: MySQL, Oracle, SQL Server, MariaDB, etc.) no solo almacena datos: también gestiona **permisos, usuarios, eventos, triggers, transacciones, copias de seguridad**.
- Como alumnos de **ASIR** (no DAM ni DA), el objetivo **no es desarrollar** bases de datos — para eso están los perfiles de desarrollo — sino **administrarlas**: asegurar que existen copias de seguridad, triggers para volcados históricos, gestión de transacciones (poder revertir una operación cuando falla algo a mitad de una secuencia de órdenes), usuarios y permisos.
- Por eso el enfoque no es "aprender un lenguaje de programación de memoria": aunque el Tema 3 trata triggers y automatización con scripts, no habrá que programarlos literalmente de memoria en el examen — sí entender el concepto, la estructura, el tipo de bucle que usan y cuándo se disparan (ej. un trigger que hace un volcado a una tabla histórica cada vez que hay un `INSERT`).
- Herramienta que se usará para conectar con cualquier motor: **DBeaver** (cliente universal; funciona igual conectando a MySQL, Oracle, SQL Server...). La idea es aprender las herramientas de administración que rodean a cualquier SGBD, no aprender un motor concreto de memoria.

## Estructura del temario: 10 temas en 3 trimestres
| Trimestre | Temas | Contenido |
|---|---|---|
| 1º | 1, 2, 3, 4 | Bases de datos **relacionales**: repaso de lo visto en 1º (tablas, vistas, consultas), instalación/configuración, triggers y automatización con scripts |
| 2º | 5, 6, 7 | Continúa con relacional (el Tema 7 empieza ya el giro hacia lo distribuido) |
| 3º | 8, 9, 10 | Bases de datos **distribuidas / NoSQL**: MongoDB, Cassandra, Redis |

Idea de fondo del bloque distribuido (Tema 7 en adelante): servicios como Netflix, Spotify, Disney+, TikTok, YouTube o Instagram **ya no usan bases de datos relacionales clásicas** porque el volumen de datos lo ha dejado obsoleto para ese caso de uso; usan bases distribuidas, donde la información no vive en un único sitio sino repartida según la ubicación del usuario (ejemplo que dio: por qué al viajar al extranjero cambian los anuncios que ves en redes sociales — te conecta a una réplica de datos más cercana a tu ubicación real).
- Mongo, Cassandra y Redis siguen siendo "tablas" en el fondo, pero con una forma de guardarse distinta a la relacional.
- Algunos de estos motores (ej. Redis) no están pensados para Linux/Windows normal, así que se instalarán con **Docker**.
- El profesor subirá vídeos de instalación de DBeaver, SQL Server y Oracle.

## Evaluación
- **Actividad 1**: 3 puntos. Se desbloquea el **12 de octubre**, con 3 semanas para entregarla (fecha límite: semana del 26 de octubre).
- **Actividad 2** (2º trimestre): 3 puntos. **Actividad 3** (3er trimestre): 4 puntos.
- **10 test** (uno por unidad, 0,5 puntos cada uno): 5 puntos en total.
- Suma máxima teórica: 3+3+4+5 = 15 puntos, pero **solo hacen falta 10** — a partir de 10 no suma más (tener 11, 14 o 15 da exactamente el mismo resultado que tener 10).
- Fórmula final: **nota de evaluación continua (sobre 10) × 50% + nota del examen (sobre 10) × 50%**. Ejemplo que dio: con 10 puntos de continua y un 5 en el examen → 2,5 + 2,5 = 5, pero con ponderaciones típicas el boletín puede marcar más alto (ej. ejemplo del profesor: 10 de continua + 5 de examen = 8 en el boletín, según su fórmula concreta de curso).
- Consecuencia práctica que remarca: **no es obligatorio entregar todas las actividades ni hacer todos los test**. Si ya se llega a 10-11 puntos de continua con, por ejemplo, los test + una o dos actividades, no hace falta agobiarse con la actividad 3 si el tiempo escasea y hay otras asignaturas peor llevadas. Recomendación personal del profesor: hacer siempre los 10 test (son los más baratos en tiempo y aseguran los primeros puntos).
- **Simulacro de examen**: semana del 23 de noviembre. No puntúa, no está confirmado quién lo corrige (el curso anterior lo corregían algunos profesores, este año sin confirmar); sirve solo para autoevaluarse antes de mayo.
- Sobre hacer las actividades con IA: el profesor recomienda **intentarlo primero por cuenta propia** y después usar una IA para mejorarlo o para ver en qué se falló — no delegar el ejercicio entero desde el principio, porque el objetivo es aprender, no solo conseguir el título.
- Aviso sobre los test cronometrados/no puntuados: pide no entregarlos a los pocos minutos de abrirlos aunque no puntúen, porque queda registrado en la plataforma y da mala impresión.

## Recursos adicionales mencionados (Certiprof / cursos UNIR)
La universidad ha habilitado este curso acceso a una serie de cursos cortos de Certiprof sobre IA y automatización (uso de Claude Code, LangChain, Ollama, LM Studio, Docker, fundamentos de IA, n8n, etc.), visibles en la plataforma bajo "tareas no evaluables". El profesor los recomienda aprovechar, sin que sean parte evaluable de esta asignatura.

## TFC (proyecto fin de ciclo): orientación recomendada
Aunque no es contenido de esta asignatura, en esta misma clase se habló de cómo orientar el TFC de forma que case con el perfil ASIR (y no se quede en "solo desarrollo"):
- La aplicación/proyecto que se desarrolle es "la excusa"; lo que de verdad evalúan es la parte de **sistemas**: cómo se administra, se protege, se hacen copias de seguridad, cómo se gestionan usuarios y permisos sobre los datos, cómo se bastiona, cómo reacciona el sistema ante incidentes provocados a propósito.
- Ideas sugeridas como ejemplo válido de enfoque: dockerizar servicios, aislar redes, meter un proxy inverso o un firewall (pfSense), montar un IDS, desplegar en la nube con medidas de seguridad, hacer pruebas de intrusión sobre la propia aplicación (tokens, inyección SQL, expiración de sesión).
- Sobre datos sensibles (ej. un proyecto de gestión escolar con datos de alumnos, mencionado por un compañero): se valoró positivamente la idea de **anonimizar** — no guardar nombre/DNI identificable junto a la nota, sino relacionar los datos sensibles con un identificador (ID), de forma que un robo de datos no permita relacionarlos directamente con una persona (medida relacionada con RGPD/LOPDGDD).
- El profesor insiste en que no todos los proyectos tienen que ser espectaculares: se evalúa también el punto de partida de cada alumno, no solo el resultado final.

## Siguiente
Lunes 21/09, primera clase con contenido real: Tema 1 (repaso de bases de datos relacionales, arquitectura, instalación y configuración).
