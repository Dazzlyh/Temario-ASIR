---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-10-13
tema: Tema 3 · DNS — jerarquía de dominios, zonas, resolución de nombres
fuente: transcripción de la clase en directo
---
# SER · Tema 3: arranque de DNS — jerarquía, TLDs, zonas y resolución de nombres (13/10)

> Anterior: [07/10 · Laboratorio 2: DHCP con cable virtual](2026-10-07_laboratorio2-dhcp-veth.md) · Profesor: Damián Sualdea Soy

Primera clase de Tema 3 (DNS). El profesor enlaza con DHCP (clase anterior): DHCP resuelve "quién tiene qué IP"; DNS resuelve el problema humano de no tener que recordar esas IPs, traduciéndolas a nombres de dominio. Ha compartido aparte un **vídeo propio sobre instalación de BIND9** (adelantado ~2 semanas, como hace siempre) que no se trabaja hoy en directo — hoy es la teoría de DNS; BIND9 y el montaje real del servidor se hacen la semana siguiente (20-21/10).

## De DHCP a DNS: por qué existe el DNS
- Con DHCP ya se resuelve la asignación de IP a una máquina (rango, reservas, concesión con tiempo limitado — repaso del protocolo DORA visto el día anterior).
- El problema siguiente es que **nadie memoriza IPs**: el DNS traduce "el idioma humano" (nombres de dominio) a direcciones IP.
- Analogía del profesor: así como hay un 8.8.8.8 (DNS de Google), un 9.9.9.9 o un 1.1.1.1, lo que se monta en la asignatura es **un DNS propio y personalizado** que gestiona el dominio completo de cada alumno.

## Resolución local antes de salir a Internet
- **localhost**: forma "cutre" de nombrar una máquina, solo vale en local.
- **Fichero hosts** (nativo del SO): en Linux/Unix/Mac es `/etc/hosts`; en Windows está en `C:\Windows\System32\drivers\etc\hosts`. Es una lista manual de `nombre → IP` que se consulta *antes* de salir a Internet.
- Demo en directo: el profesor edita `/etc/hosts` con `sudo` y añade una entrada falsa (`casajuan.paco` → una IP inventada). Al hacer `ping`/`host` a ese nombre, resuelve la IP local en vez de salir a Internet — "hacer trampas": sirve para forzar una resolución local, pero **no se trabaja así en el mundo real**; es uno de los puntos que el profesor insiste en evitar durante el módulo.
- **Orden de consulta**: el profesor lo explica dos veces en la clase con *orden distinto* (caché → hosts → DNS en un momento; hosts → caché → DNS en otro). No lo corrigió explícitamente en directo — **queda como algo a verificar**, pero la idea de fondo que repite varias veces es clara: primero se mira algo local (caché y/o fichero hosts) y solo si no hay nada ahí se pregunta al DNS configurado (ej. 8.8.8.8).

## Dominio, nombre de dominio y FQDN
Ejemplo trabajado en clase: `www.unir.net`
| Parte | Valor en el ejemplo |
|---|---|
| Dominio (TLD incluido) | `unir.net` |
| TLD | `.net` |
| Nombre de dominio | `unir` |
| FQDN (nombre completo) | `www.unir.net` |

- El árbol de dominios admite hasta **127 niveles** en teoría, aunque en la práctica casi nadie pasa de `www.algo.com`.
- Comprar un dominio es alquilar el nombre de **segundo nivel** (el que se paga); con él se pueden crear tantos subdominios como se quiera, gratis, sin límite — el profesor insiste: "es mi dominio, hago lo que me dé la gana con él".

## TLD: tipos
- **gTLD (genéricos)**: `.com` (el más conocido, comercial), `.org`, `.info`, `.tech` (caro de mantener, según el profesor), y "nuevos" gTLD más recientes. Demo en directo sobre la lista de TLDs de Namecheap/registrador (búsqueda con Ctrl+F de "genérico", "info", etc.).
- **ccTLD (country code)**: dos letras por país — `.es` (España), `.eu`, `.ad` (Andorra Telecom), y muchos otros. El profesor comprueba varios en directo sobre la lista de TLDs.
- **sTLD (patrocinados/restringidos)**: no se le dan a cualquiera — `.gov` (gubernamental), `.mil` (militar), `.edu`. Gestionados por una entidad concreta que filtra quién puede registrarlos.
- **Reservados / no resolubles** (nunca se registran, no salen a Internet): `.test`, `.example`, `.local` — por eso en prácticas y documentación de ejemplo aparecen estos sufijos sin miedo a "pisar" un dominio real.
- **Novedad 2024 (ICANN)**: reserva de **`.internal`** para redes privadas (uso interno, no enrutable en Internet) — el profesor lo señala como algo que descubrió hace poco y le llamó la atención.
- **Casos "raros" / regionales**: `.cat` (catalán, gestionado por la Fundación puntCAT — **no es un ccTLD**, es un TLD patrocinado por la comunidad lingüística), `.eus` (euskera, Gobierno Vasco / fundación), `.gal` (gallego), `.madrid` (gestionado y pagado por la Comunidad de Madrid; el profesor comenta que no cualquiera puede registrarlo libremente porque no es de libre explotación comercial — queda como matiz, no profundizó del todo). También existen TLDs ya comprados por terceros (*domain parking*): si alguien ya tiene el nombre, hay que negociar comprárselo a él, es un negocio en sí mismo.

## Quién gestiona qué: ICANN vs. registradores
- **ICANN**: coordina el sistema de nombres de dominio a nivel mundial (quién puede emitir qué TLD, políticas, etc.).
- **Registradores**: las empresas a las que realmente se les paga por el dominio — ejemplos citados: Namecheap, Dinahosting, Nominalia (España). **No se compra el dominio "para siempre"**: se alquila el derecho a gestionarlo, normalmente con pago anual.
- Recordatorio de logística: pedir ya el **GitHub Student Pack** (necesita carné de estudiante para validarse rápido) — incluye un dominio gratuito durante el curso (ej. `.me` vía Namecheap) y créditos (se menciona ~100$ de Azure/Microsoft). El dominio gratuito del Pack es válido para toda la asignatura.

## Proceso de resolución de un nombre (paso a paso)
Ejemplo narrado con `www.unir.net`:
1. El cliente (Windows/Mac/Linux) mira su fichero hosts / caché local → nada.
2. Pregunta al DNS configurado (p. ej. 8.8.8.8).
3. El DNS pregunta al servidor **raíz** → "no lo sé, pregunta al `.net`".
4. El servidor **`.net`** → "no lo sé, pregunta a quien gestiona `unir.net`".
5. El servidor **autoritativo de `unir.net`** responde con la IP de `www`.

→ en total, **5 pasos** hasta resolver el nombre. El profesor lo demuestra en directo con:
```bash
dig +trace www.unir.net     # muestra el recorrido completo: raíz -> .net -> unir.net -> respuesta final
host unir.net                 # equivalente más simple, sin el recorrido completo
host -t MX unir.net           # consulta de un tipo de registro concreto (aquí, correo)
host -t NS unir.net           # quién gestiona el DNS de ese dominio
```
(en Windows el equivalente de `host`/`dig` es **`nslookup`**)

- La IP resuelta se guarda en caché local; mientras la caché no se limpie, las siguientes resoluciones de ese nombre son instantáneas (no se repite el proceso de 5 pasos).
- Ejemplo real visto con `host -t NS www.unir.net`: aparece una cadena de **alias (CNAME)** — `unir.net` resuelve primero a un alias de tipo `*.edgekey.net` (infraestructura de CDN tipo Akamai) y ese alias resuelve finalmente a la IP. Sirve para ver que detrás de un dominio "normal" puede haber una CDN.
- Con `host -t NS <dominio>` también se puede ver qué registrador/DNS gestiona cualquier dominio ajeno (ejemplo con un dominio de prueba del profesor, apareciendo nameservers tipo `ns1...`). El profesor relaciona esto con **footprinting** (reconocimiento pasivo), que se verá más adelante en Pentesting: a partir del DNS y un `whois`/búsqueda de la IP se puede averiguar en qué proveedor (ej. Linode) está alojado un dominio.

## Protocolo de transporte: UDP (y matiz de las transferencias de zona)
- **DNS trabaja por UDP, puerto 53**, por rapidez: "me da igual si llega o no llega, lo importante es que vaya rápido" (misma lógica UDP que ya se vio en la clase de capas de transporte).
- **Confirmación de un matiz que quedó pendiente de la clase del 29/09**: las **transferencias de zona** (la réplica completa de una zona entre servidores DNS, ej. de maestro a esclavo) van por **TCP**, no por UDP, aunque las consultas normales sí van por UDP. El profesor lo repite aquí con seguridad ("transferencias de zona... a la bestia" por TCP), así que este punto que había quedado "a revisar" se puede dar por confirmado.

## Jerarquía de servidores DNS y zonas
- **Zona** = la porción del árbol de dominios de la que un servidor concreto es responsable (no se gestionan IPs completas; para una zona directa normalmente basta con los 3 primeros octetos de la red).
- Tipos de servidor DNS mencionados (nomenclatura de examen, aunque el profesor avisa que "en el mundo real" se simplifica mucho):
  - **Autoritativo**: tiene la copia original de la zona.
  - **No autoritativo / caché**: responde desde caché, no es la fuente original.
  - **Principal (master)** y **secundario (slave)**: el slave es una copia que se sincroniza desde el master mediante transferencia de zona.
  - **Reenvío (forwarder)** y **de recursión**: intermediarios que van preguntando hacia arriba hasta un servidor raíz.
  - En la asignatura, por simplicidad, se trabajará con **un único servidor** que hace de todo (no se monta arquitectura master/slave separada).
- **Zona directa vs. zona inversa**: toda zona directa (nombre → IP) tiene su correspondiente zona inversa (IP → nombre), que usa la notación `in-addr.arpa` con los octetos invertidos. El profesor avisa que **no se va a entender bien sin la práctica con BIND9** (queda para el vídeo/laboratorio); hoy solo se presenta el concepto.

## Los 13 servidores raíz (root servers)
- En la cima del árbol DNS hay **13 servidores raíz**, nombrados con una letra (el profesor dice "de la A a la N", aunque la nomenclatura estándar habitual es de la A a la M).
- Nomenclatura de examen que el profesor reutiliza de clases presenciales anteriores: cuando pide "el nombre completo de un servidor raíz", la respuesta correcta tiene la forma `<letra>.root-servers.net` (ej. `a.root-servers.net`), con direcciones tanto IPv4 como IPv6.
- Es un proyecto de origen militar estadounidense: entre las organizaciones que gestionan instancias raíz se citan Verisign, la Universidad de California/USC y el Departamento de Defensa / Ejército de EE. UU. — el profesor hace notar que no hay presencia europea en el origen del sistema, aunque sí hay instancias físicas repartidas por el mundo hoy.
- Demo en directo sobre **root-servers.org**: mapa de instancias físicas por país. España tiene varias instancias con comunicación directa (ejemplo visto: Barcelona con acceso a D, E, F, K); otros países como Francia o Alemania (Frankfurt) tienen muchas más instancias. La idea pedagógica: la consulta normalmente **no cruza el Atlántico**, se resuelve contra una instancia física cercana (más rápido).
- **Aviso sobre el temario**: el material del curso parece tener una cifra de número de instancias raíz anticuada (dice algo así como "pasan de ~1900 a 2000 instancias"); el profesor avisa que **si aparece una pregunta de examen sobre ese número concreto, la eliminará** porque el propio temario puede estar desactualizado.

## Demo en vivo: crear y propagar registros DNS (panel de IONOS)
El profesor entra en el panel de gestión de DNS de su propio dominio (IONOS) para mostrar en vivo cómo se crea una zona sin usar aún BIND9:
- El **"arroba" (`@`)** es el registro raíz del dominio (apex): a qué IP apunta el dominio desnudo (`midominio.com` sin subdominio). Solo puede haber uno.
- Crea un **subdominio nuevo** (`paquito.<dominio>`) con un registro **A** apuntando a una IP inventada — funciona igual aunque la IP no exista, "porque es mi dominio, hago lo que me dé la gana".
- Esto genera una línea de tipo zona: `paquito.dominio.com. 3600 IN A <ip>` — el TTL (aquí 3600 s / 1 hora) define cuánto tarda en refrescarse la caché de los clientes. Un compañero sugiere bajar el TTL a 1 minuto durante las pruebas para no esperar tanto a cada cambio; el profesor lo hace en directo.
- Comprobación de la propagación mundial con **watchmydns.net**: tras crear el registro, el cambio no es instantáneo — tarda varios minutos en verse desde distintos puntos (se prueba en vivo con alumnos en Málaga y Huelva, viendo cómo el registro va apareciendo poco a poco en el mapa de servidores de comprobación).
- Los servidores DNS del registrador propagan el cambio **por UDP** a nivel mundial.

### Tipos de registro vistos (tabla resumen de la clase)
| Registro | Para qué sirve | Ejemplo/nota de la clase |
|---|---|---|
| **A** | Nombre → IPv4 | El más usado; el que se ha estado creando en la demo |
| **AAAA** | Nombre → IPv6 | Igual que A pero para IPv6, si el dominio lo soporta |
| **CNAME** | Alias: un nombre apunta a *otro nombre* (no a una IP directa) | "Como un acceso directo"; ejemplo: que `algo.dominio` apunte a `unir.net` |
| **MX** | Servidor(es) de correo del dominio (Mail Exchange) | Normalmente se crean 2 (con prioridad); se verá SPF/DKIM/DMARC más adelante al hablar de reputación de correo |
| **NS** | Qué servidor(es) de nombres gestionan el dominio (delegación) | Permite tener una copia "esclava" en otro servidor |
| **TXT** | Verificación de propiedad del dominio / texto libre | Caso de uso citado: Instagram, X/Twitter, Facebook o Google Search Console piden poner un código en un TXT para verificar que el dominio es tuyo |
| **PTR** | Zona inversa (IP → nombre) | Se verá a nivel práctico con BIND9, zona inversa (nomenclatura `in-addr.arpa`) |

## Logística y fechas
- **Actividad 1 (DNS + BIND9)**: marcada como **opcional**, vale un **15 %**. Consiste en montar un servidor BIND9 con: dominio principal, un subdominio "blog" y un tercer dominio para otro CMS; configurar registros, consultas, TXT y NS; hay una rúbrica publicada en la plataforma. Usa un dominio real (no localhost).
- **Vídeo de instalación de BIND9**: ya compartido (adelanto habitual de ~2 semanas); el profesor pide verlo antes de la próxima clase para entender el "por qué" de cada paso, aunque en código activo son solo "10-15 minutos" de órdenes.
- **Calendario para la semana siguiente**:
  - **Martes 20/10** (clase): preparar en AWS el servidor publicado (con **Elastic IP** fija, Security Group) y comprobar que el dominio apunta ya a ese servidor DNS propio (`srv-dns`).
  - **Miércoles 21/10** (laboratorio): montar el servidor BIND9 en sí, abrir el **puerto 53 UDP** en el Security Group de AWS, y apuntar el dominio (vía DNS personalizados en el registrador, p. ej. Namecheap) al propio servidor.
- **Elastic IP** necesaria porque la IP pública de una instancia cambia si se apaga/enciende; sin IP fija el DNS "se perdería". Coste estimado bajo (del orden de $0,005/hora mientras está activa) dentro del presupuesto de crédito AWS de la asignatura.
- No se ha dado todavía el RFC de DNS en esta clase (al ser el primer servicio del tema, el profesor ha preferido presentar primero el "ecosistema" antes del RFC formal); quedó pendiente de repasar aparte.

## Matices y cosas a revisar
- **Orden de resolución local (caché vs. fichero hosts)**: el profesor lo dijo de dos formas distintas en la misma clase sin corregirlo explícitamente — anotar como pendiente de confirmar con la documentación oficial o con la práctica.
- Número exacto de letras de los root servers ("A a la N" dicho en clase vs. la A-M estándar de 13 raíces) — probablemente un lapsus en directo, no se corrigió.
- Estatus de `.madrid` como TLD de registro restringido no quedó totalmente explicado ("no podéis porque no van a hacer negocio con eso"); tratar como matiz pendiente.
- La cifra de instancias de root servers que aparece en el temario oficial del centro está, según el propio profesor, probablemente desactualizada — si sale una pregunta de examen sobre ese dato concreto, dice que la retirará.

## Para llevar a casa
- Comprar o conseguir (vía GitHub Student Pack) un **dominio real** antes del 20/10; no vale trabajar con `localhost` ni con el fichero hosts para esta asignatura.
- Ver el vídeo de instalación de BIND9 compartido aparte antes de la clase del 21/10.
- Repasar bien la diferencia entre dominio / TLD / nombre de dominio / FQDN, los tipos de TLD (gTLD, ccTLD, sTLD, reservados) y los tipos de registro DNS (A, AAAA, CNAME, MX, NS, TXT, PTR) — son material claro de examen.
- Practicar en el propio equipo `host`/`dig` (o `nslookup` en Windows) sobre varios dominios: tipo A, AAAA, MX, NS, y sobre todo `dig +trace` para ver el recorrido completo de 5 pasos hasta la respuesta final.
