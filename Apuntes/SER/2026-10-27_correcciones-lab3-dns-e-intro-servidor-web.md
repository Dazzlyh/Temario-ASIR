---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-10-27
tema: Correcciones y dudas del Laboratorio 3 (DNS) + arranque del Tema 4 (servidor web, HTTP, `curl`/`telnet`)
fuente: "transcripción de la clase en directo (≈90 min; la primera mitad, dudas del lab 3) + notas de clase de Dani. Sin PDF nuevo."
---
# SER · 27/10 · Correcciones del Lab 3 y primer día de servidor web

> Anterior: [Laboratorio 3: DNS con BIND9 (21/10)](2026-10-21_laboratorio3-dns-bind9.md) · Profesor: Damián Sualdea Soy

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

Sin presentación nueva en el PDF; el profesor tenía las diapositivas pero las usó poco. Hoy fue una **introducción conceptual**. El laboratorio viene la **semana que viene**.

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
| **URL** | Definir un recurso en un sitio concreto: `protocolo://host/ruta/recurso`. El `www` es un **CNAME** (alias). El puerto va tras `:` (80 HTTP, 443 HTTPS, 8080 alternativo) |
| **Navegador** | Programa cliente: interpreta el texto HTML. Lo que viaja es **texto** |
| **Servidor web** | Programa que atiende peticiones HTTP y devuelve ficheros. El nombre "servidor web" se usa para el programa y para la máquina |
| **Estático / dinámico** | Estático: fichero tal cual. Dinámico: código del lado del servidor (**PHP**) que consulta la **base de datos** y devuelve HTML. WordPress, PrestaShop, Moodle... son PHP libre |
| **HTTP es *stateless*** | "No guarda nada": cada petición son órdenes sueltas. Lo que guarda estado son las **cookies**: pequeño texto que el navegador guarda en tu equipo (idioma, si aceptaste cookies...) |

> [!note] Datos históricos (clase)
> Tim Berners-Lee creó **HTTP, HTML y la URL** (propuesta de 1989; primer navegador y servidor en 1991) y los regaló sin patente. **No inventó Internet**, inventó la **Web**. El W3C se fundó en 1994. **DNS: 1987**. Con "HTTP en 1993" el audio es confuso: **sin confirmar** a qué versión se refería. Puertos y transporte: DNS va por UDP (y TCP para transferencias), HTTP por TCP. El profesor añadió una frase sobre HTTP y UDP que el audio no deja clara (es probable que se refiriera a HTTP/3; es mío, sin confirmar).

### Servidores web comunes

- **Apache** (el que se usará): elegido por **docencia**, porque tiene estructuras de gestión muy claras y se ve cómo funciona. El profesor corrigió que **Apache no es el más usado, lo es Nginx** (afirmación suya, no comprobada por mí). Él en su servidor tiene Nginx.
- **Nginx**, **Lighttpd**: alternativas ligeras.
- **IIS** (Microsoft): opinión del profesor: **no lo aconseja** ("ni se os ocurra"): pesado, historial de vulnerabilidades, código cerrado. Es una opinión personal; para este módulo no se usa.
- "Desde el laboratorio 4... 2 o 3 semanas solo con Apache para entenderlo bien."

### Códigos de estado y métodos (demostración)

> [!important] Códigos HTTP citados en clase
> **200** OK · **301** movido (redirección, p. ej. de HTTP a HTTPS) · **400** petición mal hecha · **404** no encontrado · **405** método no permitido · **408** *request timeout* (tardas demasiado) · **500** error del servidor · **502** *bad gateway* · **503** servicio no disponible. Regla: **todos los 5xx son fallo del servidor**, los 4xx del cliente.

- **Métodos**: `GET` (pide un recurso), `HEAD` (solo las cabeceras, "no te manda el cuerpo entero"), `POST` (envía un formulario). También nombró `PUT` y `DELETE`.
- **Todo esto está definido en las RFC** (clase).

### `curl` y `telnet`: HTTP a mano

```bash
curl marca.com            # GET a la página principal; devolverá un 301 hacia https
curl -v marca.com         # ver la conversación (cabeceras de petición y respuesta)
curl -I marca.com         # solo cabeceras (HEAD) y código de respuesta
```

- El profesor dudó en clase con la opción de cabeceras ("¿-I o -L?"). Es `-I` para solo cabeceras (**HEAD**); `-L` es para **seguir redirecciones** (mío, dato técnico conocido; no lo comprobó él).
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

### Plan de las próximas clases (clase)

- **Semana que viene (lab 4)**: instalar **Apache** y ver `GET`/`HEAD` con tu propio servidor: obtener un **404** y un **200**. Se habla de la **Actividad 1** en el laboratorio. **Virtual hosts**, **PHP**.
- **Instalaciones**: **WordPress** (unos 10 min) y una **tienda virtual** (la transcripción dice PrestaShop tras corregirse de Magento; sin confirmar cuál).
- **HTTPS**: con un programa que instala un **certificado** (la transcripción dice "Zervot"; es probable que sea **Certbot**, mío). Va con la semana siguiente.
- **Vídeos en el foro** "entre hoy y mañana": instalación de Apache, virtual hosts y un tercero (WordPress). Insistió en verlos **antes** de la próxima clase.
- **Errata en el temario** sobre la versión de HTTP: dijo que lo que pone "no es verdad" y que la correcta es **HTTP/1.1**. El audio es confuso; **sin confirmar** qué número pone el temario. Dato mío: **HTTP/1.2 no existe como versión estándar** (existen 0.9, 1.0, 1.1, 2 y 3).
- **10 minutos diarios** de dudas "de sistemas" y, si alguien lo necesita, un vídeo de cómo se hace algo.

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
- **Qué número de versión HTTP** corrige en el temario.
- **"HTTP en 1993"** y la frase sobre HTTP/UDP.
- **Demo con `marca.com`**: el 503 y las conexiones colgadas no se explicaron.
- **Herramienta de DoS** y **programa de certificados**: nombres no recogidos con claridad en el audio.
- Audio con **cortes** al principio (el profesor compartía pantalla y los alumnos no le veían).

## Logística y para llevar a casa

- **Ver los vídeos** del foro (Apache, virtual hosts, WordPress) antes de la próxima clase.
- **Rehacer el laboratorio 3** con la guía y los comandos **actualizados**, sobre todo si usas Namecheap, y **comprobar la propagación** (`host`, `dig +trace`, whatsmydns).
- **Si tu dominio es de Namecheap**: borrar los registros por defecto y, si funciona o no, **contárselo al profesor** (lo pidió expresamente por correo).
- **No liberes la Elastic IP**: se reutiliza en el servidor web.
- Actividad 1: entrega **16/11** (ver README). Los puntos de evaluación incluyen el DNS y los virtual hosts.
