---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-10-27
tema: Correcciones y dudas del Laboratorio 3 (DNS) + arranque del Tema 4 (servidor web, HTTP, `curl`/`telnet`)
fuente: "transcripción de la clase en directo (≈90 min; la primera mitad, dudas del lab 3) + SER_Clase07_diapositivas.pdf (25 diapositivas) + SER_Clase07_Instrucciones.pdf (5 páginas). Los dos PDF llegaron el 4/11, después de la primera versión de esta nota; lo que cambia por su causa está marcado «(PDF)»."
---
# SER · 27/10 · Correcciones del Lab 3 y primer día de servidor web

> Anterior: [Laboratorio 3: DNS con BIND9 (21/10)](2026-10-21_laboratorio3-dns-bind9.md) · Profesor: Damián Sualdea Soy · Siguiente: [Clase 8 (3/11): Apache y virtual hosts](2026-11-03_clase8-dns-actividad1-apache-virtual-hosts.md)

Dos mitades. **Minutos 0–44:** dudas y errores del laboratorio 3 (DNS). **Minutos 44–90:** teoría del Tema 4 (servidor web) con una demostración de HTTP a mano. Los cambios que afectan al laboratorio ya están volcados en la [nota del 21/10](2026-10-21_laboratorio3-dns-bind9.md); aquí van **organizados por tarea** y con lo que es nuevo.

Marcas: **(clase)** lo dijo el profesor; **(mío)** inferencia o dato que añado yo; **sin confirmar** lo que el audio o la clase no dejan cerrado.

## Lo imprescindible

1. **El error del 21/10 era del profesor, y está confirmado:** en `named.conf.local` la zona directa se llama **como el dominio puro** (`desplegando123.com`), **sin `ns.`** (clase). La zona inversa, `x.y.in-addr.arpa`. El resto del laboratorio estaba bien.
2. **Hay guía y fichero de comandos actualizados**: el profesor dijo que los corrigió la noche del 21 y los subió el día siguiente (clase). Úsalos, no los de antes.
3. **Namecheap: borra los registros por defecto** del panel antes de probar, o el dominio puede seguir resolviendo a una IP que no es la tuya. **Sin confirmar por el profesor**: él es de IONOS y no puede probarlo (ver más abajo).
4. **Hay que repetir el laboratorio en casa** (clase): "es importante para la actividad". Parte de la **evaluación** exige DNS funcionando, y luego los *virtual hosts* se montan encima.
5. **Próxima clase: servidor web (Apache) + virtual hosts**, y **vídeos en el foro** que conviene ver antes.

> [!important] Evaluación (clase)
> "Si no sale esta parte de la actividad, hay parte que no puedo evaluar: uno de los puntos de evaluación es que tengáis un DNS; el siguiente son los virtual hosts." Si haces los laboratorios, "tienes la actividad hecha" (cada laboratorio está pensado para rellenar la actividad).

## Tarea 1 · Corregir el laboratorio 3 (DNS)

### El error de `named.conf.local`

| | Estaba (guía/clase del 21/10) | Es lo correcto |
|---|---|---|
| Zona directa | `zone "ns.<dominio>"` (solo en ese fichero) | `zone "<dominio>"` |
| Zona inversa | `zone "31.172.in-addr.arpa"` | igual |

- Regla del profesor: **arriba (la declaración de zona) va el dominio puro; abajo, dentro del fichero de zona, van los `ns`** (clase). Sol lo resumió y él lo confirmó: "en la configuración general va el dominio puro, y después va el `ns` en el resto".
- Si ya lo hiciste con `ns.` en el nombre de la zona, **cámbialo y reinicia `named`**. Prueba: `dig axfr <dominio> @<ELASTIC-IP>` debe mostrar el apex como `<dominio>.` a secas (ver nota del 21/10).
- **Por qué solo un dominio** (clase, a una pregunta de María): en producción un servidor lleva muchos dominios y hay servidores autoritativos y no autoritativos; para el laboratorio se **simplifica**: un solo servidor, un solo dominio, "si lo pones desde ahí recoges el dominio entero y de ahí para abajo haces lo que quieras". Declarar `ns.<dominio>` como zona no es "más completo": rompe la zona.

### Qué es cada nombre: dominio, `ns` y SOA (preguntas de Sol y María)

Dos preguntas se repitieron: *¿por qué a veces se pone el dominio y a veces el `ns`?* y *¿tiene que ser `ns`?*

| Dónde | Qué va | Por qué (clase) |
|---|---|---|
| Registrador, "servidor de nombres" | `ns.<dominio>` (+ la Elastic IP) | Ese nombre dice **quién gestiona** el dominio: "si pregunto quién es el nameserver de `desplegando123.com`, responde `ns.desplegando123.com`" |
| `named.conf.local` | `<dominio>` | Es el nombre de la **zona** |
| SOA, campo 1 | `ns.<dominio>.` | Servidor primario. **"Esto hay que ponerlo siempre"** |
| SOA, campo 2 (`admin`) | lo que quieras | "Este me lo estoy inventando yo" |
| `@ IN NS` y `ns IN A` | `ns.<dominio>.` → Elastic IP | El que declaras arriba lo declaras otra vez abajo y apunta a tu IP |

- **`ns` es solo una convención**: "es una forma que tengo yo de decir *main server*" (clase). Se puede trabajar **sin `ns`**, pero entonces hay que decirle al registrador que el servidor de nombres es el propio dominio **y quitarlo también en el fichero de zona**: tienen que coincidir los dos sitios. Es normal ponerlo "porque es una forma identificativa a nivel de sistemas".
- **El segundo NS (`ns1`/`ns2`)**: "eso no existe para mí", lo pide el registrador pero para el laboratorio no se usa. Lo normal en producción es tener dos servidores, pero el profesor no monta un secundario "para que se entienda" (clase). María tuvo un *Not found* con IONOS al exigirle dos; probaron a abrir otra zona y el profesor lo descartó porque complica la propagación.
- **Idea de fondo** (clase): al delegar con IONOS/Namecheap "nos cargamos" los registros que el registrador tenía por defecto, y **pasamos a ser nosotros el servidor**: cuando alguien pregunta por tu dominio, el mundo pregunta a tu `ns`, no al registrador.

### Punto final: la explicación

El profesor y María acordaron que el punto final es "para encadenar con el siguiente" y que es "un error muy típico". **La explicación correcta es la de la guía** (mío): un nombre **sin** punto es *relativo* y BIND le pega detrás el nombre de la zona; con punto es *absoluto* y no se toca. No es que se "encadene" nada: es lo contrario, el punto **corta** la concatenación. Para el examen quédate con relativo/absoluto.

### Ping a la máquina

Desde fuera no responde a `ping` porque **el Security Group de AWS no abre ICMP por defecto** (clase). El laboratorio solo abre SSH y DNS (UDP/TCP 53). Si quieres hacer ping, añade una regla **ICMP** (todo el ICMP). "Como no estoy trabajando con `ping` todavía... con los servidores web tiene más sentido" (clase). No hace falta para la actividad.

### Namecheap: registros por defecto

Lo contó **Sergio** (compañero) y el profesor lo recogió como aviso importante:

- En Namecheap el panel trae **registros preconfigurados** (en las capturas, un A/CNAME del dominio que apunta a una IP que no es la del servidor propio). Sergio dice que, mientras estén, el dominio resuelve a **esa** IP y "te vuelves loco" intentando que salga tu Elastic IP.
- **Solución propuesta (clase): borrarlos** desde Advanced DNS ("acción, borrar", el icono de la papelera).
- IONOS **borra todo al delegar**, por eso el profesor (de IONOS) no se encontró con esto.
- A la pregunta de María ("¿hay que reconfigurar los ficheros o basta con borrar?"), el profesor respondió que **con borrar** debería responder tu servidor, pero **"esto no lo sé yo hasta que no haga la prueba"**: lo que se confirma es lo que comprobéis vosotros.
- **Sin confirmar**: la IP concreta que ponen por defecto (el audio no la recoge con claridad), y si hace falta algo más que borrar. El profesor pidió a **Sergio y Fernando** (Namecheap) que le mandaran por correo la configuración de su panel, la iba a analizar "con la IA" y **puede cambiar el manual**. Fernando le mandó una captura con `NS`, `SPF`, un *Redirect record* y un CNAME; el profesor **no supo decir** por qué aparecía el redirect. Pendiente: mira el foro por si publica una versión nueva.

> [!warning] Cómo detectar el problema (diagnóstico de clase)
> Sol hizo `host -t ns <dominio>` y salió bien, pero `host ns.<dominio>` **no** devolvía su Elastic IP. El profesor: "te está diciendo que tu DNS sigue siendo el de Namecheap". Es decir: el NS está delegado, pero el registro A del `ns` lo está contestando otro. Si te pasa, mira los registros por defecto.

### Propagación y comprobaciones

- **Demo en directo**: el profesor añadió un subdominio `maria` (A y su PTR), lo consultó con `host` y **no salía todavía**. Lo atribuyó a que acababa de arrancar la máquina y a la propagación ("hay que esperar un poco"); lo comprobó con **whatsmydns.net**; unos minutos después ya salía. **Sin confirmar** la causa exacta.
- Dijo que **no hacía falta reiniciar `named`**. Mi lectura (mío): su servidor acababa de arrancar, así que cargó las zonas editadas al arrancar. En un `named` que ya está corriendo, un cambio en la zona **sí requiere reiniciar o recargar**, como en el 21/10.
- `host -t ns <dominio>` y `host ns.<dominio>`: los dos comandos de diagnóstico que usó. El primero dice quién es el NS; el segundo, a qué IP resuelve.
- Recomendó repetirlo **en casa** y mirar la propagación mañana si hoy no sale.

### Qué se dijo de `named.conf.options` y de `dig axfr`

- El profesor sí mencionó hoy `allow-query { any; }` y **`recursion no`**: "para que no funcione como propagador de DNS". Es la mención en clase que faltaba el 21/10; sigue sin haberse hecho en directo.
- Recomendó `dig axfr` porque "se ve muy bien la transferencia de zona" y, si no entiendes una salida, **pasársela a una IA**, "que te va a decir si ve algo raro".

## Tarea 2 · Arranque del Tema 4: servidor web

Hoy fue una **introducción conceptual** (apartados **4.1 y 4.2** del Tema 4) con la consola al lado. **Montar Apache es el Laboratorio 4, el miércoles 4 de noviembre.**

> [!note] (PDF) Material oficial de esta clase
> Hay **diapositivas** y un documento de **instrucciones** con los comandos explicados (resumen más abajo, en «Material oficial»). Mi primera versión de esta nota decía que no había PDF: era porque no me habían llegado, no porque no existiera. En clase el profesor parece que se apoyó sobre todo en un **Prezi** propio (el enlace va en las instrucciones; yo no lo puedo abrir) y en la consola, así que **lo dicho en voz alta y lo escrito no coinciden siempre** y lo marco donde pasa.

### Cadena completa

```
navegador ──▶ DNS (tu BIND9: "¿IP de desplegando123.com?") ──▶ IP del servidor web ──▶ Apache (puerto 80/443)
                                                                         │
                                         estático: devuelve el fichero tal cual
                                         dinámico: PHP + base de datos ──▶ HTML/CSS/JS
```

- **Analogía del profesor**: el DNS es la **centralita** y el servidor web es quien **descuelga el teléfono**. Hasta hoy teníamos "la puerta" (el DNS lleva al servidor); ahora ponemos algo detrás que abra.
- Lo ideal en producción: **servidores separados** (uno DNS, otro/s web). En el laboratorio se hará **todo en la misma máquina** AWS. Con *virtual hosts* se juntan varios sitios web en **un** servidor.
- **Reutiliza la Elastic IP**: sigue siendo la de `srv_dns`. Por eso no se libera.

### Qué es cada cosa

| Concepto | Qué dijo |
|---|---|
| **HTTP** | Protocolo de transferencia de hipertexto. Capa de **aplicación**. Es "el idioma que entienden servidor y navegador". Cliente pide, servidor da (o da error) |
| **HTML** | Lenguaje de marcas. El **hipertexto** es el que enlaza páginas |
| **URL** | Definir un recurso en un sitio concreto: `protocolo://host/ruta/recurso`. El `www` es un **CNAME** (alias). El puerto va tras `:` (80 HTTP, 443 HTTPS, 8080 alternativo). (PDF) Sintaxis completa en «Material oficial» |
| **Navegador** | Programa cliente: interpreta el texto HTML. Lo que viaja es **texto** |
| **Servidor web** | Programa que atiende peticiones HTTP y devuelve ficheros. El nombre "servidor web" se usa para el programa y para la máquina |
| **Estático / dinámico** | Estático: fichero tal cual. Dinámico: código del lado del servidor (**PHP**) que consulta la **base de datos** y devuelve HTML. WordPress, PrestaShop, Moodle... son PHP libre |
| **HTTP es *stateless*** | "No guarda nada": cada petición son órdenes sueltas. Lo que guarda estado son las **cookies**: pequeño texto que el navegador guarda en tu equipo (idioma, si aceptaste cookies...) |

> [!note] Datos históricos (clase)
> Tim Berners-Lee creó **HTTP, HTML y la URL** (propuesta de 1989; primer navegador y servidor en 1991) y los regaló sin patente. **No inventó Internet**, inventó la **Web**. El W3C se fundó en 1994. **DNS: 1987**.
> **(PDF) Corrijo dos suposiciones mías de la primera versión.** La línea del tiempo de las diapositivas es: **DNS 1987** (RFC 1034/1035), **la web / HTTP 1989**, **DHCP 1993** (RFC 2131). Así que el **«1993»** del audio era el **DHCP**, no una versión de HTTP; y la frase sobre UDP era **«DNS y DHCP van por UDP, HTTP por TCP»**, no HTTP/3 como supuse. Detalle curioso del material: **la web (1989) es más vieja que el DHCP (1993)**.
> RFC de HTTP (PDF): **HTTP/1.0 = RFC 1945 (1996)**; **HTTP/1.1 = RFC 2616 (1999), hoy RFC 9110–9112 (2022)**; **HTTP/2 = RFC 7540 (2015)**; **HTTP/3 = RFC 9114 (2022)**. DNS también usa TCP para transferencias (mío).

### Servidores web comunes

- **Apache** (el que se usará): elegido por **docencia**, porque tiene estructuras de gestión muy claras y se ve cómo funciona. El profesor corrigió que **Apache no es el más usado, lo es Nginx** (afirmación suya, no comprobada por mí). Él en su servidor tiene Nginx.
  - **(PDF) Contradicción:** las diapositivas y las instrucciones dicen **«Apache: el más usado»** y **«Nginx: muy eficiente con muchas conexiones; hace de proxy inverso y balanceador»**; el profesor dijo en voz alta lo contrario. Para el examen, vale lo escrito (el temario nombra estos tres: Apache, Nginx e IIS). Mi impresión, sin comprobar hoy, es que Nginx suele ir por delante en las encuestas recientes.
- **Nginx**, **Lighttpd**: alternativas ligeras.
- **IIS** (Microsoft): opinión del profesor: **no lo aconseja** ("ni se os ocurra"): pesado, historial de vulnerabilidades, código cerrado. Es una opinión personal; para este módulo no se usa.
- "Desde el laboratorio 4... 2 o 3 semanas solo con Apache para entenderlo bien."

### Códigos de estado y métodos (demostración)

> [!important] Códigos HTTP citados en clase
> (PDF) Los del material: **200 OK** (todo bien, aquí está el recurso) · **301/302** (se mudó: búscalo en esta otra dirección) · **403 Forbidden** (existe, pero no tienes permiso) · **404 Not Found** (ese recurso no está en el servidor) · **500** (el servidor se ha roto por dentro). Familias: **2 bien, 3 redirección, 4 culpa del cliente, 5 culpa del servidor**.
>
> Los dichos en clase: **200** OK · **301** movido (redirección, p. ej. de HTTP a HTTPS) · **400** petición mal hecha · **404** no encontrado · **405** método no permitido · **408** *request timeout* (tardas demasiado) · **500** error del servidor · **502** *bad gateway* · **503** servicio no disponible. Regla: **todos los 5xx son fallo del servidor**, los 4xx del cliente.

- **Métodos**: `GET` (pide un recurso), `HEAD` (solo las cabeceras, "no te manda el cuerpo entero"), `POST` (envía un formulario). También nombró `PUT` y `DELETE`.
- **Todo esto está definido en las RFC** (clase).

### `curl` y `telnet`: HTTP a mano

```bash
curl marca.com            # GET a la página principal; devolverá un 301 hacia https
curl -v marca.com         # ver la conversación (cabeceras de petición y respuesta)
curl -I marca.com         # solo cabeceras (HEAD) y código de respuesta
```

- El profesor dudó en clase con la opción de cabeceras ("¿-I o -L?"). **(PDF) Confirmado:** `curl -v` es un **GET** (lo que hace el navegador), `curl -I` es un **HEAD** (solo cabeceras) y `-L` **sigue las redirecciones** (de ahí `curl -IL`).
- **Sin `curl`, a mano con `telnet`** (clase):

```bash
telnet marca.com 80
GET / HTTP/1.1
Host: marca.com
                      # línea en blanco: fin de la petición
```

  Eso es lo que `curl` envía por debajo. Hizo la demo con `marca.com` y le salió un **503** y conexiones que se quedaban colgadas; él mismo dijo que "aquí hay algo raro" y que lo investigaría. **No saques conclusiones** de esa demo.
- **Dejar la sesión abierta con muchas peticiones** a un servidor sería una **denegación de servicio**. El nombre de la herramienta no lo recordó (mío: probablemente *Slowloris*; sin confirmar).
- `telnet` **en Windows no viene instalado**; Sol preguntó si era solo de Linux y el profesor dijo que no. En el servidor Ubuntu se instala con `apt` y se podrá usar ahí.
- **Una petición mal hecha** (p. ej. un método que no existe) da un **400**.

### Plan de las próximas clases

> [!important] (PDF) Calendario del tema, con fechas
> - **Clase 8 · martes 3 de noviembre:** cliente y servidor, sitios virtuales, acceso, y la **explicación de la Actividad 1** (apartados 4.3 a 4.6).
> - **Laboratorio 4 · miércoles 4 de noviembre:** **Apache con tres sitios virtuales, PHP, MariaDB y WordPress** sobre tu dominio.
> - **Clase 9 · martes 10 de noviembre:** **HTTPS con Certbot** y un **segundo CMS**.
> - **Actividad 1: se entrega el lunes 16 de noviembre.** Tu dominio del Lab 3 es la base.
> - Todo corre en **la misma máquina y con el mismo nombre del Lab 3**: «No toques tu `srv_dns`: déjala en **Stop** y **no liberes la Elastic IP**».

- **Certificados:** las diapositivas dicen que el Tema 4 oficial **no entra en certificados** y que se montan con **Let's Encrypt** (Certbot) **«para la Actividad 1»** en la clase 9. Es decir, **la Actividad 1 incluye HTTPS** según este material (en clase no lo dijo así).
- **Instalaciones:** en clase habló de WordPress (unos 10 min) y de una tienda virtual; el material solo dice «un segundo CMS». **Sin confirmar cuál.**
- **Vídeos en el foro** «entre hoy y mañana» (clase): instalación de Apache, virtual hosts y un tercero (WordPress). Insistió en verlos **antes** del laboratorio. Los PDF no los mencionan.
- **10 minutos diarios** de dudas «de sistemas» y, si alguien lo necesita, un vídeo de cómo se hace algo (clase).

> [!warning] (PDF) Errata del temario: HTTP 1.2, y qué vale en el examen
> El temario dice **«versión activa: HTTP 1.2»** y **«especificada en el RFC 2774»**. La realidad: **no existe HTTP 1.2**; ese RFC es otra cosa (un marco de extensión experimental); en uso hoy están **HTTP/1.1, HTTP/2 y HTTP/3**. La diapositiva lo dice así: **«Para el examen vale lo del PDF, pero que sepáis la verdad»**. Es decir: **en el examen, responde lo que pone el temario**.
> Detalle mío: el material dice a la vez que HTTP lo desarrollaron «W3C e IETF desde 1990» y que el W3C es «de 1994»; es una imprecisión, no te la juegues con esa frase.

## Material oficial: diapositivas e instrucciones (PDF, recibido el 4/11)

Lo que traen y la clase no recogió, o recogió distinto. Todo es **lectura**: «hoy no se monta ningún servidor» (instrucciones). Se hace en **`srv1`**, el servidor de los primeros laboratorios (no en `srv_dns`).

> [!important] Marcado como pregunta de examen (diapositiva 9)
> **Internet NO es la WWW.** Internet es la **red**: millones de dispositivos conectados entre sí (el cable, los routers, las direcciones IP). La WWW es el **contenido**: el conjunto de **páginas web alojadas en servidores web**. «Viaja por Internet, pero no es Internet.» **No todo dispositivo de Internet es un servidor web**; por eso muchas webs empiezan por `www`. El material la llama «pregunta de examen fácil».

### La URL, «el DNI del recurso»

```
protocol://[user:password@]host[:port]/path/resource
http://www.marca.com/futbol/seleccion/131.html
 │         │               │               │
protocolo  host            path            recurso
```

| Parte | Qué es | Ejemplo |
|---|---|---|
| `protocol` | Cómo se pide (casi siempre `http`/`https`) | `http` |
| `host` | El nombre del servidor; **lo resuelve tu DNS** | `www.marca.com` |
| `port` | Puerto; si no se escribe, **80** (443 en https) | `:8080` |
| `path` | La ruta dentro del servidor | `/futbol/seleccion` |
| `resource` | El recurso concreto | `131.html` |

- `user:password@` **existe pero no se usa**: el navegador guarda esos accesos y es inseguro.
- El puerto casi nunca se escribe porque el navegador asume el 80 en http.

### Una petición por dentro

```bash
curl -v http://www.marca.com/
> GET / HTTP/1.1                 # las líneas con > las manda tu equipo
> Host: www.marca.com
> User-Agent: curl/8.5.0
<
< HTTP/1.1 200 OK                # las líneas con < las devuelve el servidor
< Server: nginx                  # quién responde
< Content-Type: text/html; charset=utf-8
```

«Eso es una conversación HTTP completa, y está en texto.» **Tecléalo, no lo copies**: leer la respuesta en crudo es lo que se aprende (instrucciones).

### Métodos

| Método | Qué pide | Con curl |
|---|---|---|
| **GET** | Dame el recurso entero. Lo que hace el navegador al abrir una página | `curl -v` (por defecto) |
| **HEAD** | Solo las cabeceras, sin cuerpo: ¿existe?, ¿qué tipo?, ¿cuánto pesa? | `curl -I` |
| **POST** | Envía datos (un formulario). Lo verás con WordPress y las API | — |
| **PUT / DELETE** | Crea y borra un recurso. Propios de las API | — |

> [!important] Idea clave del material
> **GET y HEAD solo piden: no cambian nada en el servidor.** POST, PUT y DELETE sí. **Por eso un enlace siempre es un GET.**

### Otras ideas del PDF

- **HTTP «no recuerda nada»** (sin estado): cada petición es la primera para el servidor. Para reconocerte se usan las **cookies**, que pueden guardar hábitos y hasta contraseñas, «de ahí el aviso legal de todas las webs».
- **Estática**: un `.html` que el servidor entrega tal cual, igual para todos (el `index` del Lab 4). **Dinámica**: se genera en el momento (tu perfil, tu carrito); en el servidor con **PHP o Python**, en el cliente con **JavaScript**; **WordPress es dinámica**. El temario cita **applets de Java y Flash** en el cliente: «hoy están muertos, es todo JavaScript».
- **HTTP vive en la capa de aplicación**, igual que DNS y DHCP, sobre **TCP**, puerto 80 (443 en HTTPS). (Mío: HTTP/3 va sobre QUIC/UDP; el material no lo dice.)
- **Para qué se usa**: navegación; redes y comunicación (Gmail, WhatsApp web...); comercio electrónico (Amazon, Shopify, PayPal, Stripe); nube (Drive, Dropbox, OneDrive); **integración por API**: «hoy media web no la mira un humano, la llama otro programa».
- **Una red existe para compartir** (P2P, mensajería y redes, la página web): «casi todo lo anterior acabó funcionando dentro de una página web» (palabras del temario).
- **Servidores** que nombra el temario: **Apache**, **Nginx**, **IIS**. «¿Cuál elegir? Depende del contenido, del tráfico y de la seguridad que necesites.»

### HTTP y HTTPS

HTTP va en **texto plano**: quien esté en medio de la red ve usuarios y contraseñas. **HTTPS es lo mismo, pero cifrado con un certificado**, por el **puerto 443**; es el candado del navegador.

```bash
curl -v https://www.marca.com/ 2>&1 | grep -iE "SSL|TLS|subject|HTTP/"
```

Con eso verás el *handshake* TLS y el certificado (`subject`).

### Tu dominio del Lab 3, todavía sin web

```bash
host desplegando123.com
desplegando123.com has address 184.197.19.142

curl -v http://desplegando123.com/
*   Trying 184.197.19.142:80...
* connect to 184.197.19.142 port 80 failed: Connection refused
```

«El nombre lleva a tu máquina (eso es el Lab 3), pero **no hay ningún servidor web escuchando en el 80**.» Ese `Connection refused` es **«el hueco que llena el Tema 4»**: en el Lab 4 montas Apache y el dominio empieza a cargar. (La IP del ejemplo es la del material, no la tuya.)

### Ejercicios del PDF («a vosotros»)

En `srv1`, contra webs públicas. **Apunta el código de respuesta de cada una; es lo que se pregunta.**

1. **GET:** `curl -v https://www.unir.net/` y lee la primera línea de la respuesta (`< HTTP/1.1 ...`). ¿Qué código es? ¿Qué pone en la cabecera `Server`?
2. **HEAD:** `curl -I https://www.unir.net/` sobre la misma web. ¿Qué ves ahora y qué ha desaparecido respecto al GET? (el cuerpo)
3. **Un 404:** `curl -I https://www.unir.net/pagina-que-no-existe-123`. ¿Qué código devuelve?
4. **Una redirección:** `curl -I http://google.com/` y luego `curl -IL http://google.com/`. ¿Qué código da el primero y a dónde manda? ¿Qué cambia al añadir `-L`?
5. **http frente a https:** compara `curl -I http://...` con `curl -I https://...` de una misma web. ¿Cuál va cifrado? (el 443)

**Para entregar (si lo pide el profesor):** captura de pantalla con los cinco comandos y, al lado, **una línea por cada uno con el método usado y el código obtenido**. No he ejecutado estos comandos: los resultados son los que te salgan a ti.

> Ampliación del profesor: un **Prezi** con más detalle (enlace en las instrucciones, página 1: `https://prezi.com/view/oLe1ObYCEjpJ8juUiGVJ/?referral_token=o0JA0fInB3FN`). Referencia de los RFC: `rfc-editor.org/rfc/rfcXXXX`; manual de Apache: `httpd.apache.org/docs`.

## Si algo no funciona (DNS, repaso del día)

| Lo que ves | Qué pasa |
|---|---|
| `host -t ns <dominio>` sale bien, pero `host ns.<dominio>` no da tu IP | Registros por defecto del registrador (Namecheap) respondiendo en lugar de tu servidor → borrarlos |
| Aún no sale nada | Falta propagar. Esperar y comprobar con whatsmydns.net |
| Todo sale con el nombre repetido (`www.<dominio>.<dominio>`) | Falta un punto final en el fichero de zona |
| `Not found` en IONOS al poner solo un NS | IONOS pide dos; se pone el segundo con cualquier IP, no se usa |

## Dudas y cosas sin confirmar

- **Namecheap**: la IP por defecto y si hace falta algo más que borrar; el profesor no lo ha probado.
- **Causa del retraso de `maria`** en la demo (¿propagación, máquina recién arrancada o recarga de `named`?).
- **(Resuelto por los PDF)** El «HTTP en 1993» era el DHCP; la frase de UDP era DNS/DHCP; el temario dice «HTTP 1.2, RFC 2774».
- **Qué «tienda virtual» o «segundo CMS»** se instala: en clase PrestaShop (tras corregirse de Magento), en el material solo «segundo CMS».
- **Apache o Nginx, ¿el más usado?** Clase y material se contradicen.
- **Prezi**: no lo he visto; puede contener cosas que la clase mencionó y yo no recojo.
- **Demo con `marca.com`**: el 503 y las conexiones colgadas no se explicaron.
- **Herramienta de DoS**: nombre no recogido con claridad en el audio. (El «programa de certificados» ya es **Certbot / Let's Encrypt**, según el PDF.)
- Audio con **cortes** al principio (el profesor compartía pantalla y los alumnos no le veían).

## Logística y para llevar a casa

- **Laboratorio 4: miércoles 4/11.** Arranca `srv_dns` (está en Stop; la Elastic IP sigue siendo tuya) antes de empezar.
- **Ver los vídeos** del foro (Apache, virtual hosts, WordPress) antes del laboratorio.
- **Hacer los 5 ejercicios `curl`** en `srv1` y guardar la captura con método y código.
- **Rehacer el laboratorio 3** con la guía y los comandos **actualizados**, sobre todo si usas Namecheap, y **comprobar la propagación** (`host`, `dig +trace`, whatsmydns).
- **Si tu dominio es de Namecheap**: borrar los registros por defecto y, si funciona o no, **contárselo al profesor** (lo pidió expresamente por correo).
- **No liberes la Elastic IP**: se reutiliza en el servidor web.
- Actividad 1: entrega **lunes 16/11** (ver README). Los puntos de evaluación incluyen el DNS y los virtual hosts, y según el PDF también **HTTPS con Let's Encrypt** (clase 9, 10/11).
