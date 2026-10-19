---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-10-07
tema: Tema 1 · amenazas, ingeniería social, CVE/CVSS/NVD, MITRE ATT&CK · Actividad 1
fuente: SAD_Clase04_Presentacion.pdf (24 páginas) + SAD_Clase04_Actividad1_Guia.pdf (2 páginas) + transcripción de la clase en directo
---
# SAD · Clase 4 (07/10) · Actividad 1: análisis forense con MITRE ATT&CK

> Anterior: [Laboratorio 2](2026-10-05_lab2-security-group.md) · Profesor: Damián Sualdea

> ⚠️ **Corrección importante (19/10):** la estructura de la Actividad 1 descrita más abajo se ha corregido con la guía oficial del profesor (`SAD_Clase04_Actividad1_Guia.pdf`), que **no coincide del todo** con lo que se entendía de la transcripción: son **5 apartados, no 6** (no hay un apartado 6 de "reflexión personal" independiente — el punto 5 oficial es "puntos de vista": organización / usuario / atacante), y los **pesos son distintos**: Cadena de ataque = 25 % (no 30 %) y Medidas de protección = 30 % (es el apartado que más puntúa, no la cadena de ataque). **Hoy es el día de entrega (lunes 19, 23:59)** — revisa tu informe contra la tabla de abajo si ya lo tenías montado con la estructura antigua.

**Entrega: lunes 19 de octubre a las 23:59.** Es la primera actividad de evaluación continua — **3 de los 10 puntos** — sobre el Tema 1 entero, y es **100% investigación, no hay que montar ni instalar nada**. Elegir el incidente en el foro cuanto antes (para no repetir; repetir con otro compañero no penaliza, pero se prefiere variedad) y buscar **dos fuentes públicas** que lo describan (son las que se citan en el informe).

> Idea clave del día: **no puedes defender lo que no conoces** — primero quién/qué nos ataca y por qué, luego cómo nos defendemos.

## 1 · Estructura exacta de la Actividad 1 (rúbrica oficial)
Informe en **PDF**, con las fuentes citadas, con estos 5 apartados:

| Apartado | Qué tiene que llevar | Peso |
|---|---|---|
| 1 · Contextualización | Qué pasó, a quién y con qué consecuencias. Tabla de activos afectados, clasificados por **criticidad** (hardware, software, datos; alto/medio/bajo). | 15 % |
| 2 · Cadena de ataque | Al menos **cuatro técnicas** de MITRE ATT&CK, cada una con su **código** (Txxxx), su **fase** y el **CVE** que explota si lo hay. | 25 % |
| 3 · Principios rotos | Qué compromete cada técnica: confidencialidad, integridad o disponibilidad, y por qué. | 15 % |
| 4 · Medidas de protección | **Una medida por técnica**, justificada y clasificada en preventiva, detectora o correctora. **Es el apartado que más puntúa.** | 30 % |
| 5 · Puntos de vista | El mismo incidente contado desde la organización, desde el usuario y desde el atacante. | 15 % |

**Ejemplo resuelto de la guía** (con WannaCry, 2017 — no hay que usarlo, es solo para ver cómo encaja una fila):

| Fase | Técnica ATT&CK | CVE | Principio que rompe | Medida (tipo) |
|---|---|---|---|---|
| Escalada/movimiento | T1210 · explotación de servicios remotos | CVE-2017-0144 (SMBv1, CVSS 8.1) | Integridad y disponibilidad | Parchear a tiempo (preventiva) |
| Impacto | T1486 · cifrado de datos | — | Disponibilidad (y confidencialidad) | Copias probadas para restaurar (correctora) |

**Herramientas / dónde buscar:**
| Para qué | Dónde |
|---|---|
| Ficha del fallo y su gravedad (CVSS) | nvd.nist.gov |
| Técnicas de los atacantes, detección y mitigación | attack.mitre.org |
| Informes de incidentes en español | incibe.es · ccn-cert.cni.es |
| Comprobar si un dato/correo está en una filtración | haveibeenpwned.com |

**Errores que bajan la nota (de la guía, literal):**
- Medidas genéricas tipo "más seguridad" o "formar a la gente" sin decir contra qué técnica — cada medida va emparejada con su técnica.
- Citar técnicas sin su código o sin su fase — siempre: nombre, Txxxx y fase.
- No citar las fuentes, o citar solo Wikipedia.
- Dejarlo para el fin de semana: se entrega el LUNES 19, no el viernes 23 — el plazo cierra al empezar esa semana.

## 2 · De dónde viene el golpe (diapositiva 1.5) y las tres barreras (1.6)
Toda amenaza cae en uno de estos tres cajones (diapositiva oficial):

| Humanas | Lógicas | Físicas |
|---|---|---|
| Un atacante de fuera | Malware y ransomware | Incendio e inundación |
| Un empleado descontento | Exploits de un fallo | Robo de equipos |
| Un error sin mala intención | Software mal configurado | Corte de luz, fallo de disco |
| **Las más frecuentes** | El arma, no la mano | Se ve entero en el Tema 2 |

> «Casi todo empieza en la columna humana: alguien que entra, que se equivoca o que es engañado. La tecnología suele ser solo el camino.»

Dos ejes a distinguir dentro de las amenazas humanas: **dentro o fuera** (el de dentro —con acceso legítimo— puede hacer tanto o más daño que el de fuera, porque ya tiene la puerta pasada) y **queriendo o sin querer** (un error de un administrador, sin mala intención, es una amenaza igual de real que un ataque deliberado). De ahí la importancia del **mínimo privilegio**: no es desconfiar de la gente, es que un error o una cuenta robada hagan el menor daño posible.

**Quién ataca de verdad** (actores de amenaza según ENISA, la agencia de ciberseguridad de la UE — Threat Landscape 2025):
| Actor | Perfil |
|---|---|
| Hacktivistas | 8 de cada 10 incidentes; sobre todo DDoS (tirar una web para protestar) — mucho ruido, poco daño real, pero molesto |
| Ciberdelincuentes | Menos casos, pero el daño gordo: ransomware y ataques a la cadena de suministro — van por dinero |
| Estados | Los más sigilosos: ciberespionaje y desinformación, casi siempre contra la administración pública |

**A quién le toca** (sectores más atacados en la UE, ENISA 2025): administración pública **38 %**, transporte 7,5 %, infraestructura y servicios digitales 4,8 %, finanzas 4,5 %. Más de la mitad de los incidentes (54 %) fueron a entidades esenciales de la directiva **NIS2** (se verá en el Tema 10). Vía de entrada: **60 % por un correo falso** (phishing) y **21 % explotando un fallo sin parchear**.

**Toda medida de protección hace una de tres cosas** (diapositiva 1.6 — base del apartado 4 de la actividad):
| Preventiva | Detectora | Correctora |
|---|---|---|
| Evita que pase | Avisa de que está pasando | Recupera tras el daño |
| Contraseñas, cifrado | Registros (logs) | Copias de seguridad |
| Cortafuegos, parches | Antivirus, IDS | Plan de contingencia |
| Formación | Alertas y monitorización | Alta disponibilidad |

Ninguna sola basta: se ponen en capas (**defensa en profundidad**) — si una falla, la siguiente aún cubre.

**Ejemplo de técnica → medida → tipo** (tal como lo da la diapositiva, de cara al apartado 4):
| Técnica | Medida que la para | Tipo |
|---|---|---|
| Fuerza bruta (T1110) | Doble factor y bloqueo tras varios fallos | Preventiva |
| Phishing (T1566) | Formación y filtro de correo | Preventiva |
| Explotar un CVE (T1210) | Parchear y revisar los registros | Preventiva + detectora |
| Ransomware (T1486) | Copias probadas para restaurar | Correctora |

**Las cuatro fases de un ataque** (así está ordenado MITRE ATT&CK — es la cadena del apartado 2):
| Fase | Qué hace el atacante | Ejemplo de técnica |
|---|---|---|
| Reconocimiento | Mira qué hay y qué versión tiene | T1595 · sondeo (visto ya en el Laboratorio 2, `sad1`) |
| Intrusión | Entra por el fallo o por engaño | T1566 phishing · T1110 fuerza bruta |
| Escalada y movimiento | Gana más permisos y salta de máquina | T1210 explotar un servicio |
| Impacto | Hace el daño: roba, cifra o tira | T1486 cifrar datos (ransomware) |

No hace falta que un incidente de la actividad tenga las cuatro fases — basta con identificar al menos cuatro técnicas y colocarlas en su fase correspondiente.

Dentro de las amenazas humanas, tres tipos de más a menos peligroso según el profesor: **empleado descontento (insider)** — el más peligroso, tiene acceso legítimo y conoce el sistema por dentro; **error humano sin mala intención** — muy frecuente, evitable con formación; **atacante externo**. Concepto de la **gacela más débil**: los atacantes no van a por el objetivo más grande, van a por el eslabón más fácil de romper — casi siempre el factor humano ("capa 8").

**Ingeniería social** — para el profesor, más determinante que las vulnerabilidades técnicas puras (coincide con la técnica T1566 de la diapositiva oficial). Ejemplos clásicos de estafa en España: tocomocho, timo de la estampita, príncipe nigeriano, "te ha tocado la lotería", estafa del CEO (ahora potenciada con IA generativa: voz clonada e incluso videollamadas falsas), phishing bancario por SMS, vishing (llamada de falso soporte), un USB "perdido" en el aparcamiento, soporte técnico falso, "paga una fianza para empezar a trabajar" (nunca hay que pagar por conseguir un empleo). Factores por los que funciona: **prisa, miedo y autoridad** — "no hay parche para la confianza". Dato ENISA 2025: **6 de cada 10 ataques en la UE empiezan por un correo o mensaje falso**. Referencia de lectura recomendada: **Kevin Mitnick**, libros *El arte de la intrusión* / *El arte de la invisibilidad* (editorial Anaya).

Dato real compartido por un alumno: las empresas envían correos de phishing simulado a sus propios empleados como entrenamiento — quien pica recibe un curso de concienciación. Recurso del profesor para dar formación de concienciación: el **kit de concienciación de INCIBE** (carteles, temario y material de charlas sobre ransomware, phishing, etc.).

## 3 · De dónde sacar el incidente
- **ENISA Threat Landscape** (agencia de ciberseguridad europea, enisa.europa.eu) — informe anual con miles de incidentes reales categorizados por sector (administración pública ~38%, transporte, finanzas, infraestructuras digitales) y por tipo de amenaza (ransomware, brecha de datos, fraude, DDoS, desinformación/deepfakes, ciberespionaje de estado). El profesor mostró en directo el informe del año: ~8.300 incidentes catalogados — "sois 30 personas, elegid el que más os guste".
- Casos sugeridos por el profesor como ejemplo o inspiración:
  - **WannaCry (2017)** — SMBv1 de Windows, explota **CVE-2017-0144** (EternalBlue), técnica MITRE T1210 (explotación remota de servicios) + T1486 (cifrado de datos para impacto/ransomware). Grupos relacionados: APT28, Lazarus.
  - **NotPetya** — también usó EternalBlue, combinado con otro exploit.
  - **SolarWinds** (ya visto el 30/09) — ataque a la cadena de suministro.
  - **Hospital Clínic de Barcelona** y **Hospital de Torrejón** (ransomware, enero 2020, en plena pandemia) — ⚠️ el profesor dice conocerlo "de primera mano" (tenía un familiar trabajando allí); detalle anecdótico, no verificado documentalmente.
  - **Stuxnet** — gusano dirigido a una central nuclear iraní, entró por USB; saltó la seguridad física precisamente en el sitio "imposible". Se comentó también la película/caso "Mission: Impossible"-like real (atribuido a Israel según un compañero en clase, sin confirmar).
  - **ILOVEYOU** (gusano en Visual Basic, vía macros de correo) y el **gusano Morris** (1988, ARPANET, el primer gusano de la historia, creado como prueba y descontrolado) — ejemplos "clásicos" si se quiere un caso más antiguo (cuanto más antiguo, más información hay publicada).
  - Pegasus (spyware moderno) también es válido.
  - El profesor aceptó también un tema no puramente informático propuesto por un alumno (hackeo "físico" desde una cárcel en los años 70, línea de teléfono pirateada) — confirma que **vale cualquier incidente de seguridad**, no solo ataques a servidores.

## 4 · Bases de datos de vulnerabilidades (para el apartado de CVE)
- **NVD** (National Vulnerability Database, EE. UU.) — buscar por `CVE-YYYY-NNNNN`.
- **CVE Details** — buscador alternativo, útil para encontrar el listado de CVEs de un año/producto, aunque no explica el ataque en sí (para eso, NVD o el propio informe del incidente).
- **CVSS**: puntuación de 0 a 10 de gravedad de una vulnerabilidad (ya visto antes); 8-10 = crítico (rojo).
- Diferencia **vulnerabilidad / exploit / CVE**: vulnerabilidad = el fallo en sí (servicio sin parchear, contraseña por defecto, permiso mal puesto); exploit = el código que aprovecha esa vulnerabilidad; CVE = el identificador público de una vulnerabilidad ya conocida (si no está identificada, es un 0-day). Dato de ENISA: 1 de cada 5 intrusiones en la UE explotó un fallo que **ya tenía parche disponible**.
- Herramienta de ejemplo para detectar vulnerabilidades conocidas en un sistema: **Nexpose**.

## 5 · Cómo navegar MITRE ATT&CK para la actividad
En **attack.mitre.org**, cada técnica (p. ej. T1110 Fuerza bruta) tiene en su misma página:
- Descripción de la técnica.
- **Mitigación** (cómo protegerse) — usar esto para el apartado 4 de la actividad (medidas de protección), no inventar medidas.
- **Detección** — cómo se detectaría (qué tipo de software/alerta lo vería).
- Ejemplos de procedimiento / grupos conocidos que la usan (APTs).

Hay varias matrices además de la "Enterprise" por defecto: **Mobile** (ataques a móviles) e **ICS** (Industrial Control Systems — hospitales, centrales eléctricas, fábricas), útiles si el incidente elegido afecta a infraestructuras industriales.

## 6 · Ciclo de defensa (para el apartado de medidas, además de lo que diga MITRE)
**Prevenir → detectar → corregir**, de forma cíclica, no puntual:
- Prevenir: cultura de ciberseguridad, formación, cifrado, firewalls.
- Detectar: IDS (sistemas de detección de intrusiones — se trabajará con **Snort** o **Suricata** más adelante en el curso).
- Corregir: cada incidente debe producir un cambio real en cómo se protege la empresa, tanto a nivel preventivo como de detección.
- **Threat hunting**: buscar amenazas de forma proactiva, anticipándose a posibles vías de ataque antes de que se materialicen.
- **Defensa en profundidad**: redundancia (otra región de AWS, otro proveedor cloud) para que un único fallo no tumbe el servicio entero.

## 7 · Bastionado de SSH (demo breve, surgida de una pregunta)

Para impedir el login remoto directo como `root` por SSH (medida preventiva frente a fuerza bruta):
```bash
sudo nano /etc/ssh/sshd_config
# buscar/poner: PermitRootLogin no
sudo systemctl restart ssh
```
`root` como tal **no se puede bloquear** (no se banea ni se elimina), pero sí se le puede **prohibir el login remoto directo** por SSH con esa directiva — es distinto de bloquear al usuario. El control de qué usuarios pueden hacer `sudo` se gestiona aparte con `visudo`.

## 8 · Sobre el ritmo de las clases y el examen (para no agobiarse)
- Antes de cada examen trimestral hay una **semana de repaso** y un **simulacro**; el examen solo entra sobre lo que se repasa esas semanas, no sobre todo lo dicho al vuelo en cada clase en directo.
- Contenido que se repite entre asignaturas (p. ej. RAID visto ya en Sistemas Operativos) se trata con un repaso rápido, no se vuelve a explicar desde cero — si algo ya se ha visto, avisar al profesor para que lo agilice.
- El profesor sube la presentación del Tema 1 completa al final del tema (no solo el trozo del día), y en las semanas de repaso sube todo ya simplificado.
