---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-09-29
tema: Tema 1 · Modelo OSI vs TCP/IP (4 capas reales) · IPv4/IPv6 · comandos por capa
fuente: transcripción de la clase en directo
---
# SER · Modelo TCP/IP en directo (29/09)

> Anterior: [23/09 · Primer laboratorio: SRV1 en AWS, Linux básico, Apache](2026-09-23_laboratorio-srv1-linux-basico.md) · Siguiente: [Clase 4](2026-10-06_clase4-dhcp.md)

Clase de arranque de Tema 1: de la teoría del modelo OSI (7 capas) se pasa al modelo real con el que se trabaja en la asignatura, **TCP/IP de 4 capas**, demostrado con comandos reales en `srv1` (Ubuntu 24.04 en AWS). El profesor avisa: la semana siguiente toca DHCP y, según él, "no tiene mucha historia"; lo interesante empieza más adelante.

## OSI (teoría) vs TCP/IP (lo que se implementa de verdad)
| OSI (7 capas) | TCP/IP (4 capas, la realidad) |
|---|---|
| Aplicación + Presentación + Sesión | **Aplicación** |
| Transporte | **Transporte** |
| Red | **Internet** |
| Enlace de datos + Física | **Acceso a la red** |

- El modelo OSI es la teoría de examen de test; en la práctica **todo Internet funciona con las 4 capas de TCP/IP**. La capa de sesión "no tiene equivalente" claro en TCP/IP; según el profesor solo entra en preguntas tipo test.
- Metáfora del encapsulamiento: cada capa superior mete sus datos dentro de la de abajo, haciendo el datagrama "más tocho" (TLS, HTTP, lo que sea va dentro); **solo las capas adyacentes y el extremo remoto se hablan entre sí**, nunca se "salta" una capa.

## Vocabulario de capa 2 (acceso a la red)
- **MAC**: identifica el fabricante + un número de serie; dos tarjetas no deberían repetirla nunca. Con tarjetas virtuales (máquinas virtuales, instancias cloud) los buscadores de MAC por fabricante suelen devolver "no record found" porque no es hardware físico real.
- **Conflicto de MAC**: poner la misma MAC dos veces en la misma red local genera un conflicto (el sistema avisa de que ya existe esa dirección); con máquinas virtuales en **modo puente** es fácil que pase y "se vuelve loco" el sistema.
- Estándares de capa física/enlace: **IEEE 802.3** (Ethernet, cable de cobre/fibra), **IEEE 802.11** (WiFi; las generaciones "WiFi 5/6" que se venden en las cajas son en realidad 802.11ac/802.11ax), **Token Ring** (IBM, legado, "se pasa el testigo").

## Comandos por capa (en `srv1`, interfaz `ens5`)
```bash
ip -brief link                 # capa 2: lo (loopback) + ens5 (nombre real); muestra la MAC
ip -brief address               # capa 3: IP privada (172.31.x.x en AWS; "no te miente", es la privada)
ss -tulnp                       # capa 4: puertos a la escucha (22 abierto siempre; 80 si hay Apache instalado)
curl ifconfig.me                # capa 7: pregunta a un servicio externo cuál es tu IP pública
curl ifconfig.io
```
- Nombres de tarjeta según plataforma: `ens5` (AWS), `enp0s3`/`ens33` (VirtualBox/VMware), `eth0` (clásico/Kali).
- La IP privada "nunca miente": es la que ve el propio equipo. La IP pública hay que **preguntarla fuera** (no la sabe el propio equipo, la asigna el NAT/proveedor).

## curl, telnet y por qué un telnet manual falla
```bash
curl -v https://unir.net          # -v: ver la conversación HTTP completa (petición y respuesta)
curl -Is http://unir.net          # ver solo cabeceras; aquí se ve el 301 que mueve de HTTP a HTTPS
telnet unir.net 80                # abre una conexión TCP cruda al puerto 80
GET / HTTP/1.1                    # tecleado a mano dentro del telnet: "bad request" si falta Host/cabeceras
```
- **telnet** abre la conexión pero el "idioma" (protocolo de aplicación) hay que hablarlo tú a mano; con HTTP mal formado da error. **curl** hace la petición GET bien formada automáticamente — "es como un navegador pequeñito que sabe hablar correctamente".
- Un `curl` a `http://` sobre un sitio HTTPS devuelve un **301** (muévete a HTTPS); repetir el curl ya con `https://` y dominio con `www.` puede devolver **403 Forbidden**: `curl` no completa el intercambio de certificado/clave propio de TLS (eso sí lo hace un navegador real), así que el servidor no deja pasar la petición.

## host / dig — preguntar al DNS por capas de registro
```bash
host unir.net          # registro A (IPv4) por defecto
host -t AAAA unir.net  # registro AAAA (IPv6): unir.net no tiene -> "not found"
host -t MX unir.net    # registro de correo: unir.net usa Exchange/Outlook (Microsoft)
host -t A renfe.com    # renfe.com: sin MX propio (no gestiona correo ahí)
host -t A renfe.es     # renfe.es: sí tiene MX
host -t AAAA zara.com  # zara.com: SÍ tiene IPv6 (raro de encontrar en dominios españoles)
host despegando2t.com  # un dominio puede resolver a VARIAS IPs -> balanceo de carga (se verá en AWS más adelante)
```
- `host` y `dig` preguntan al DNS; `dig` da más detalle. En Windows el equivalente es `nslookup`.
- Comprobar sistemáticamente un dominio con A / AAAA / MX antes de asumir qué tiene montado: **no tener AAAA es lo normal todavía en dominios .es**; tener varias IPs en el A es indicio de balanceador.

## Traceroute / MTR — ver los saltos
```bash
# en Linux puede faltar el paquete:
sudo apt install traceroute      # o net-tools, según distro
traceroute despegando.com
mtr despegando.com               # "my traceroute": interactivo, va refrescando los saltos (como Windows tracert pero en vivo)
```
- En Windows es `tracert`; en Linux el nombre del binario varía según distro (a veces falta y hay que instalarlo). El profesor improvisa con `mtr` cuando no recuerda el comando — queda como ejemplo real de que **cada entorno Linux puede no traer las mismas herramientas de serie**.
- Un salto que no responde se queda "esperando respuesta" (waiting for reply); no implica fallo, solo que ese nodo no contesta a ICMP.

## IPv4 / IPv6 — historia y confusión típica de examen
| | IPv4 | IPv6 |
|---|---|---|
| Bits | 32 | 128 |
| Direcciones | ~4 300 000 000 (4,3·10⁹) | ~340 sextillones |
| Pensado en | 1981 (RFC 791) | 1998 (RFC 2460; reescrito luego en RFC 8200) |
| Formato | decimal con puntos | hexadecimal |

- **Error muy común de examen**: IPv4 e IPv6 **no están relacionadas entre sí** — no hay "traducción" de una IP v4 a su v6 equivalente; son dos direccionamientos independientes que convive el mismo host.
- Adopción real de IPv6 (dato de Google, medido por el profesor en septiembre de 2026): **en torno al 50 %** de tráfico global por IPv6. Un alumno apunta un matiz importante: ese 50% de "uso" incluye muchas IPv6 asignadas pero sin tráfico real — gran parte del tráfico sigue pasando en la práctica por NAT/IPv4 con cada salto.
- **IPv4 ≠ IPv6 "a la vez" sin coste**: si una red local usa ambas simultáneamente hay traducción extra (más lenta) y más superficie de ataque. Consejo del profesor para redes locales pequeñas: si no se necesita, **desactivar IPv6** (en Windows: propiedades del adaptador de red → desmarcar IPv6).
- Comprobación casera de pública vs privada: comparar la IP pública del móvil por WiFi de casa frente a la misma por datos (4G/5G) — deberían ser distintas porque salen por NAT/operadoras distintas. Si salen **iguales** estando en redes distintas, sospechar de una VPN o del **relay de privacidad de iCloud** en Safari (oculta la IP real; no pasa lo mismo abriendo la misma web en Chrome en el mismo móvil).

## Capa de transporte: TCP vs UDP
| | TCP | UDP |
|---|---|---|
| Modelo | orientado a conexión (handshake) | sin conexión, "a lo bestia" |
| Fiabilidad | retransmite, controla flujo, segmenta | no garantiza nada, no hay cliente-servidor real |
| Analogía del profesor | "bebértelo tranquilo" | "tirar piedras": cada datagrama es una piedra, lo importante es que lleguen rápido, no en orden |
| Ejemplos | HTTP/HTTPS, FTP, SSH, SMTP | DNS (consultas), DHCP, streaming (RTP/RTSP), VoIP, juegos online |

- Puerta de entrada para preguntas de entrevista de trabajo: *"dime protocolos que vayan por UDP"* → DHCP, DNS, streaming son las respuestas típicas.
- Matiz que se le escapó al profesor en directo y corrigió después: la **transferencia de zona DNS va por TCP** (no UDP), aunque las consultas normales de DNS sí van por UDP; lo deja marcado como "a revisar", **no verificado del todo en el momento**.
- Tabla de puertos de capa de aplicación comentada: HTTP/HTTPS → TCP 80/443 (Apache o Nginx; en la asignatura se trabajará sobre todo con Apache); FTP → TCP 20 (datos, modo activo, "antiguo") / 21 (control; en modo pasivo los datos van por otro puerto negociado); SSH → TCP 22 (OpenSSH); DNS → UDP 53; DHCP → UDP 67 (servidor) / 68 (cliente).

## Historia de ARPANET / TCP-IP (contexto de examen tipo test)
- **ARPANET**: proyecto militar de EE.UU.; la idea de **partir la información en trozos y enrutarlos** por caminos distintos nace de que, si el enemigo pincha un cable, solo intercepta un trozo del mensaje, no el mensaje entero — además la red debía seguir funcionando aunque cayeran nodos intermedios.
- **1973**: se diseña el modelo TCP/IP, separando TCP (control) de IP (encaminamiento).
- **1983**: ARPANET adopta TCP/IP como su estándar oficial — "nace" en la práctica Internet tal como se conoce.
- RFCs mencionados en la demo del buscador de rfc-editor.org: **RFC 768** (UDP, 1980, muy corto, con diagramas ASCII del datagrama), **RFC 8200** (IPv6, versión moderna; la original era RFC 2460 de 1998).
- Los RFC son **incrementales**: cuanto más bajo el número, más antiguo. Ejemplo que da el profesor: TCP se reescribió entero en 2022 recogiendo décadas de parches, resultando en el RFC 9293 (sustituye a la RFC 793 original).
- El IETF (Internet Engineering Task Force) es quien redacta y mantiene los RFC; el profesor lo traduce en broma como "grupo de asalto a Internet".

## Para llevar a casa
- Repetir con vuestro propio equipo/servidor los comandos de cada capa (MAC, IP privada, puertos abiertos, IP pública) y comparar resultado en WiFi vs datos móviles.
- Entender por qué **IPv4 y IPv6 no están relacionadas** entre sí es un punto de examen explícito.
- El próximo día (Clase 4) se monta DHCP de verdad en AWS; el profesor avisa de que es "el servicio que menos le gusta" pero que siempre entra en examen y prácticas.

## Enlaces
RFC 768 (UDP) · RFC 791 (IPv4) · RFC 2460 / RFC 8200 (IPv6) · RFC 9293 (TCP, reescritura 2022) · buscador rfc-editor.org
