---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-10-14
tema: "Tema 1 · Los tres puntos de vista de un incidente y el análisis forense"
fuente: "Transcripción de clase + SAD_Clase05_Practica.pdf + SAD_Clase05_Presentacion.pdf"
---
# SAD · Clase 5 (14/10) · Tres puntos de vista de un incidente y primer concepto de forense

> Anterior: [Actividad 1: MITRE y análisis forense (07/10)](2026-10-07_actividad1-mitre-forense.md) · Siguiente: [Laboratorio: primera foto del servidor (19/10)](2026-10-19_laboratorio-primera-foto-servidor.md) · Profesor: Damián Sualdea Soy

Clase que cierra el Tema 1. El profesor confirma que la clase en directo sigue el guion de los dos PDFs oficiales (práctica + presentación) sin discrepancias de contenido: los tres puntos de vista, Colonial Pipeline, las 4 fases del análisis forense, la cadena de custodia, a quién avisar, el ENS, el caso SEPE, la tabla comparativa, "no siempre caen los tres", el plan en capas con el MTTR y el repaso final de la rúbrica de la Actividad 1 aparecen todos y en ese orden. Hay, eso sí, una diferencia respecto al PDF de práctica: **la demo de `sha256sum`/`scp` no se ejecutó en directo** — el profesor la explicó paso a paso en pantalla pero pidió explícitamente no repetirla en el momento ("no lo hagáis ahora, Juan, que no me va a dar tiempo") porque se quedaba sin tiempo para el resto de la clase; queda como ejercicio para hacer por cuenta propia con la documentación ya subida.

## 1 · Los tres puntos de vista de un incidente

Hilo conductor de la clase, ligado dos veces a la actividad: es la teoría del apartado 1.7 **y** el apartado 5 (15 %) de la Actividad 1.

| Punto de vista | En qué piensa |
|---|---|
| **Organización / dirección** | El negocio: cuánto cuesta el incidente, qué servicios se paran, el impacto legal (incumplir contratos, el RGPD) y quién es el responsable de que haya pasado |
| **Usuario** | Poder seguir trabajando y que sus datos estén a salvo; es el "eslabón más débil" no por tonto, sino porque no está pensando en seguridad sino en hacer su trabajo (y a veces está cabreado o tiene prisa) |
| **Atacante** | Por dónde entrar, qué puede sacar, cómo no ser pillado — al final siempre va "por dinero o por datos, porque datos es dinero" |

> «Como G-CISO o jefe de seguridad, o como equipo azul, tenéis que pensar en los 3, no solo en la parte mala — tenéis que tener una visión global.»

> «Quien no entienda todavía que más datos es más dinero está en el siglo equivocado.»

El profesor insiste en que el administrador no piensa solo para la organización: también tiene que proteger al usuario, y debe asumir que el atacante va a venir siempre — enlaza con la idea de que **no existe el riesgo cero ni nada invulnerable** («partimos de esas dos premisas»).

Matiz nuevo sobre el "problema con el empleado": si falla la formación, el problema casi nunca es solo "el empleado despistado" — puede ser que no haya cultura de ciberseguridad real en la empresa. Las campañas de concienciación eficaces no son "un curso y ya está": son anuales, con carteles, píldoras de 3-5 min, entrevistas, y luego una campaña de phishing simulado para medir si la gente vuelve a caer o si al menos avisa rápido y bien.

## 2 · Caso Colonial Pipeline (2021), hilo conductor

- Oleoducto de ~9.000 km, transporta diésel, gasolina y queroseno de Texas a Nueva York — infraestructura crítica.
- Mayo de 2021: ransomware (grupo **DarkSide**). Entrada por una **contraseña de VPN antigua, filtrada, sin doble factor**.
- Pararon el oleoducto entero **por precaución** — no fue el ataque técnico el que lo tumbó, fue una decisión preventiva ante la incertidumbre.
- Pagaron ~4,4 millones $ de rescate en bitcoin; el FBI recuperó parte siguiendo el rastro de las transacciones.
- Consecuencia real: colas con compra de pánico en gasolineras y subida de precios en la costa Este — «una pequeña cosa a nivel de tecnología provocó algo mucho más gordo en el mundo real».
- Cifrado del ransomware: comentado en clase que a nivel genérico puede combinar simétrico (rápido, para cifrar el volumen de datos) y asimétrico (para la clave) — enlaza con lo visto en criptografía en otra asignatura.

> «El daño no fue técnico, fue físico y social: a nivel técnico no hizo falta nada sofisticado, solo una contraseña vieja sin doble factor. Con un doble factor en esa VPN ya habría sido suficiente.»

> «Colonial Pipeline no era una chapuza: es una empresa enorme, con medios, que lo hace bien. Entrar igual no es que fallara por incompetencia — es que nadie es invulnerable.»

**Recurso nuevo mencionado en clase (no está en el PDF oficial): No More Ransom** — proyecto en el que participan Europol, Banco Santander y otras entidades; si sufres un ransomware, subes un archivo cifrado y la web comprueba si ya existe una herramienta de descifrado para esa variante conocida. Útil como recurso real, no solo teoría.

## 3 · Análisis forense: las 4 fases y la cadena de custodia

Por ley, **no se pueden tocar las evidencias** informáticas directamente — se trabaja siempre sobre copias. En peritaje informático se suelen manejar varias copias con su hash certificado: el original (lo custodia el notario/el perito), una copia para el juez, otra para el cliente.

**Las 4 fases, siempre en este orden:**

| Fase | Qué se hace |
|---|---|
| 1. Identificar | Qué ha pasado, qué equipos, qué pruebas hay — sin tocar nada, "desde fuera" |
| 2. Adquirir | Copiar la prueba con su huella (hash); orden de lo más volátil a lo menos volátil (RAM antes que disco) |
| 3. Analizar | Siempre sobre la copia, nunca sobre el original; reconstruir la cronología |
| 4. Documentar | Informe para el juez/abogados, cadena de custodia, repetible |

Detalle ampliado sobre la adquisición: los ordenadores **no se apagan** para no perder la RAM (es volátil y no se puede copiar de forma fiable una vez se apaga el equipo), aunque si el disco ya está parado se puede hacer copia "en frío"; la copia "en caliente" es la que interesa cuando el disco está cifrado. El orden de volatilidad no es un criterio inventado por el profesor: lo fija un estándar (lo citó como ISO/IETF) sobre el orden en que se debe recoger la evidencia.

Para discos grandes, en el mundo profesional se usan **duplicadores forenses dedicados** (dispositivos con hardware especializado: se mete el disco original, se mete el disco destino, se le da a reproducir y hace la copia exacta) en vez de depender solo de MD5/software porque el proceso de copiar discos grandes a mano es lento.

Herramientas que se nombran como preview de lo que se verá en el módulo de forense (ciberseguridad), sin entrar en detalle hoy:
- **Volatility** — scripts en Python para extraer y analizar la memoria RAM.
- **`dd`** — para hacer la copia bit a bit del disco.
- **Autopsy** — herramienta de análisis forense sobre la copia.

Pregunta de un alumno (Víctor): ¿se puede falsear un disco? El profesor confirma que sí es posible manipular un disco en el momento de la copia, y que esto se verá en la parte práctica con `dd` más adelante en el módulo de ciberseguridad.

Regla sobre cómo se redacta el informe forense: **nunca se nombra a la persona**, solo el equipo — "en este equipo pasó esto", no "esta persona hizo esto"; la atribución a una persona concreta es un paso posterior que hacen otros (RR.HH., dirección, un juez), no el informe forense en sí.

## 4 · Qué hacer tú primero ante un incidente

No eres el perito forense, pero no debes cargarte las pruebas antes de que llegue el equipo especializado:

- **Aislar, no apagar.** Aislar = desconectar la máquina de la red (sin acceso a nada más), para no perder la RAM ni dejar que siga la intrusión.
- **No destruir pruebas.** No restaurar, no limpiar nada, no borrar logs — se queda tal cual está, aunque parezca "sucio".
- **Avisar y apuntar la hora exacta.** La cronología del incidente se reconstruye hacia atrás desde esa hora, así que apuntar qué viste, qué hiciste y cuándo es crítico para la alarma correcta.

> «El administrador da la voz de alarma, aísla y entrega las pruebas al equipo especializado — tú no haces el forense puro, pero sí la primera toma de contacto.»

## 5 · A quién avisar

- **A la organización, ya** — a la dirección o al responsable de seguridad. Un incidente nunca se tapa: «es como quien tiene una enfermedad: por mucho que no vayas al médico, la enfermedad sigue ahí».
- **A la AEPD en menos de 72 h** si hay datos de carácter personal afectados — obligación del RGPD (y, en España, la Ley Orgánica de Protección de Datos y Garantía de los Derechos Digitales, que se apoya en el RGPD: ambos dicen lo mismo, el RGPD manda por encima). Se verá entero en el Tema 10.
- **A quien te pueda echar una mano**, según el caso: INCIBE-CERT (si no eres sector público) o CCN-CERT (si trabajas para la administración pública o prestas servicios a ella).

Mención breve del **ENS** (Esquema Nacional de Seguridad, Real Decreto): obligatorio para la administración pública y sus proveedores, categoriza los sistemas en básica/media/alta, lo gobierna el **CCN** con sus guías CCN-STIC. Jerarquía mencionada en clase: la UE arriba con **ENISA** (la agencia europea de ciberseguridad), España con el **CNI** y dentro el **CCN**. Se verá entero en el Tema 10.

**Contenido nuevo no cubierto en el resumen previo — SOC y CERT/CSIRT regionales:** el profesor dedica varios minutos a explicar qué es un **SOC** (Security Operations Center) — el equipo que gestiona alertas tempranas, muchas veces subcontratado en vez de tenerlo en plantilla propia; mostró fotos del SOC de **NEMO** (centro de monitorización que visitó con alumnos de ciberseguridad) para ilustrar el puesto de trabajo (pantallas, "ventanas" opacables para que no se vea desde fuera lo que se está gestionando). Comenta que hay un **CERT/CSIRT por comunidad autónoma** en España (el profesor sigue especialmente el de la Comunidad Valenciana) y que para 2030 se espera que casi todas las comunidades autónomas, no solo Madrid, tengan su propio SOC/ciber-SOC. **Aviso de logística nuevo:** anuncia que en una próxima clase vendrá un compañero suyo de **Deloitte** a dar una charla sobre el SOC.

## 6 · Demo de adquisición de evidencia (explicada, no ejecutada en directo)

Explicada paso a paso en pantalla a partir del PDF de práctica, sin ejecutarla en vivo por falta de tiempo:

```bash
# En el servidor (sad1)
sudo cp /var/log/auth.log evidencia_auth.log
sha256sum evidencia_auth.log
# (guardar el valor del hash)

# Desde el equipo local
scp -i labsuser.pem ubuntu@<IP>:~/evidencia_auth.log .
sha256sum evidencia_auth.log
# Si el hash coincide con el del servidor, la copia no se ha modificado
```

Aclaraciones orales sobre el comando:
- **SCP es el protocolo que usa SSH para subir y bajar archivos** — por eso se necesita la clave (`-i labsuser.pem`) igual que para conectarse por SSH.
- La comprobación de integridad es literalmente esto: mismo hash en origen y en destino = no se ha modificado nada.
- Primero se aísla la máquina, luego se hace esto — nunca al revés.

## 7 · Caso SEPE (9 de marzo de 2021) y comparación con Colonial

- Ransomware **Ryuk**. Sector público español, en plena pandemia.
- ~700 oficinas caídas y la sede electrónica fuera de servicio.
- Afectó a citas, trámites de **paro** y **ERTE** — contexto crítico porque era pandemia y la gente no podía salir de casa.
- Matiz oral que no estaba en el resumen previo: **la gente sí cobró**, pese a la caída del sistema — se tiró de procedimientos en papel/manuales mientras se recuperaba el servicio.
- No se pagó el rescate, según las fuentes oficiales — el profesor añade como **opinión personal suya, sin confirmar**: «a mí que no pagaran no me lo creo, pero es una opinión mía».
- Recuperación progresiva, de orden de semanas. Al ser administración pública pura, aplica el **ENS** con nivel alto de prioridad.

**Tabla comparativa Colonial vs SEPE:**

| | Colonial Pipeline | SEPE |
|---|---|---|
| Dónde | EE. UU., privado, energía | España, público, empleo |
| Qué rompió | Disponibilidad | Disponibilidad |
| Cuánto tardó | ~6 días | Semanas |
| ¿Pagó rescate? | Sí (~4,4 M$) | No, según las fuentes oficiales |
| Ransomware | Sí (DarkSide) | Sí (Ryuk) |

Conclusión del profesor: mismo patrón de ransomware tumbando un servicio crítico — cambia el país y el dueño, no el patrón.

## 8 · "No siempre caen los tres" (CID)

| Caso | Qué cayó |
|---|---|
| Renfe (2025) | Confidencialidad — robaron datos de viajeros, los trenes siguieron funcionando |
| SEPE / Colonial (2021) | Disponibilidad — pararon el servicio, los datos no se tocaron |
| SolarWinds (2020) | Integridad — metieron código en una actualización legítima |
| Un ransomware típico | Las tres a la vez — cifra, inutiliza y bloquea de golpe |

Mensaje del profesor: saber cuál de los tres pilares ha caído es lo que decide cómo respondes al incidente.

## 9 · El plan en capas y el MTTR

La seguridad es un **plan en capas**, no un parche puntual ni un curso de un día:

| Capa | Qué incluye |
|---|---|
| 01 · Antes · prevenir | Seguridad perimetral, contraseñas, doble factor, formación — "es casi todo el curso" |
| 02 · Durante · detectar | Registros, alertas, antivirus, SOC — darse cuenta rápido de que algo está pasando |
| 03 · Después · responder y recuperar | Plan de respuesta, copias y análisis forense — volver a funcionar y aprender para que no se repita |

**MTTR** — introducido aquí por primera vez, y lo trae a colación una pregunta de un alumno en el chat antes de que el profesor llegara a esa diapositiva: es el tiempo que se tarda en volver tras una caída. Colonial ~6 días; SEPE, semanas. Bajar el MTTR es de lo que va la segunda mitad del módulo (copias, redundancia y alta disponibilidad, desde el Tema 2).

> «Ningún ataque se evita al 100 %. La diferencia entre un susto y una catástrofe es cuánto tardas en volver.»

> «Nadie es invulnerable. Colonial no era una chapuza — si prometes que no te va a pasar nunca, estás mintiendo. El objetivo real no es que no pase: es estar listo para cuando pase.»

## 10 · Repaso final de la rúbrica de la Actividad 1

Confirma en directo la misma tabla ya documentada en la nota del 07/10 (5 apartados: contextualización 15 %, cadena de ataque 25 %, principios rotos 15 %, medidas 30 %, puntos de vista 15 %) — no hay cambios respecto a esa rúbrica, solo repaso oral de última hora.

**Checklist antes de entregar**, insistido con humor varias veces en clase:
- Entregar en **PDF**, cinco apartados, con las fuentes citadas — "no me hagáis leer algo copiado tal cual, con vuestras palabras".
- Las técnicas, con código y fase ("no vale decir 'usó phishing', hay que poner T1566 y la fase").
- Cada medida, clasificada en preventiva/detectora/correctora, emparejada con su técnica — es el apartado que más puntúa (30 %).
- Los tres puntos de vista (organización/usuario/atacante) — "esto es lo que acabamos de ver hoy".

## 11 · Logística

- **Entrega: lunes 19 de octubre, 23:59**, en la tarea de Canvas — nunca por correo electrónico («fuera de fecha, no corrijo; no me lo pueden enviar por correo porque es no evaluable»). El profesor pide explícitamente no dejarlo para el último momento porque necesita que todos entreguen antes de empezar a corregir, y la corrección le come una semana entera.
- **Sesión de dudas de última hora: lunes 19, de 18:00 a 19:00** — "para dudas de última hora, no para empezarla: traed lo que lleváis y lo repasamos". Antes de esa sesión subirá primero el laboratorio del lunes para que no haya problemas de acceso a tiempo.
- **Miércoles 21:** se corrige la Actividad 1 en clase (el profesor comentará ejemplos de cómo podría haberse hecho mejor, sin entrar en el detalle de cada entrega) y arranca el **Tema 2: seguridad pasiva, física y ambiental**. El Tema 1 queda cerrado.
- Propuesta de un alumno (Manuel), bien recibida por el profesor: montar un sitio compartido donde cada uno pueda ver los incidentes elegidos por los compañeros — pendiente de que el grupo lo organice.

> «Ya sabéis mirar un incidente por los cuatro costados. Ahora contadlo bien: eso es la Actividad 1.»

## Notas en directo

- **Mulero digital (dinero) — anécdota sin confirmar.** El profesor cuenta un caso real, que le relató personalmente un agente de la Guardia Civil dedicado a ciberseguridad (el mismo que descubrió la red de bots "Mariposa", una de las más grandes conocidas): grupos capitalizan jóvenes en parques cerca de oficinas de envío de dinero (tipo Western Union) ofreciéndoles sacar una cantidad (p. ej. 3.000 €) de una cuenta a cambio de quedarse con una parte (p. ej. 500 €) y entregar el resto. El aviso del profesor: para sacar el dinero hace falta el DNI, con lo que la persona queda identificada y puede acabar implicada en un delito de blanqueo de capitales sin saberlo del todo — recomienda encarecidamente no participar nunca en este tipo de "favores" de mover dinero entre cuentas a cambio de una comisión. Marcado explícitamente como relato de segunda mano, no verificado de forma independiente.
- **Digresión sobre políticas de dispositivo personal / BYOD.** Un alumno (Manuel) pregunta por qué muchas empresas no dejan sincronizar el calendario corporativo de Outlook en el móvil personal. El profesor no da una respuesta técnica cerrada («al final son políticas: hay políticas, y el blanco y el negro se ven bien, pero el gris no»), pero conecta la pregunta con dos conceptos de seguridad que no estaban previstos en la diapositiva de hoy: la **política de desconexión** (el derecho a no estar disponible fuera de horario) y el **mínimo privilegio** / reducción de la **superficie de ataque** — la idea de que cuantos más dispositivos y aplicaciones tengan acceso a datos corporativos, más puertas de entrada hay, aunque el propio profesor admite que en su caso personal usa el móvil para centralizarlo todo y no sigue esa política de forma estricta.
- El profesor pidió a los alumnos avisarle siempre que detecten un enlace o fichero con el nombre equivocado en el campus (hoy mismo tuvo un fallo subiendo el material de la Clase 5, confundido con el de "SAD" vs otra asignatura) — no es contenido de la asignatura, pero explica por qué conviene revisar que el material de cada clase coincide con lo anunciado antes de empezar a trabajar sobre él.
