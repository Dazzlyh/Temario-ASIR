---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-09-22
tema: Conceptos básicos de red e Internet — puertos, IANA/RFC, datagramas, NAT, protocolos, clasificación de redes
fuente: transcripción de la clase en directo
---
# SER · Conceptos básicos de red (22/09)

> Anterior: [15/09 · Presentación del módulo](2026-09-15_presentacion-modulo.md) · Siguiente: [23/09 · Primer laboratorio: SRV1 en AWS, Linux básico, Apache](2026-09-23_laboratorio-srv1-linux-basico.md)

Primera clase de contenido real. Metáfora que se repite: **un servidor es un camarero** (el cliente pide, el servidor va a buscarlo — p. ej. a la "cocina" — y responde).

## Puertos
- **Puerto físico** (dónde se conecta el cable: Ethernet, USB, serie) vs **puerto lógico** (0–65535 por cada equipo/servidor).
- Rangos (asignados por **IANA**, iana.org):
  - **0–1023**: *well-known ports*, reservados (HTTP 80, HTTPS 443, SSH 22, FTP 21, SMTP 25, POP3 110, IMAP 143, DNS 53, MySQL 3306, PostgreSQL 5432...).
  - **1024–49151**: registrados, no estándar pero conocidos por convención (p. ej. 8080 para Tomcat).
  - **49152–65535**: **efímeros** — los que usa el cliente de salida en cada conexión (por eso puedes abrir muchas pestañas a la vez, cada una sale por un puerto distinto).
- IANA no obliga a nada técnicamente: "puedo montar mi servidor web en el 8080, el 81, el que quiera"; lo estándar es una convención para que cliente y servidor se entiendan sin configurar nada.
- Herramienta para ver IANA: `iana.org` → buscador de puertos (ctrl+F el número) y buscador de RFC (rfc-editor.org) — el **IETF** (Internet Engineering Task Force) es quien redacta los RFC.
- Comando en el servidor para ver qué puertos están escuchando: `ss -tlnp` (los que están en `LISTEN` son los que aceptan conexión entrante).

### Puertos que se van a trabajar en el módulo (por tema)
| Tema | Servicio | Puerto |
|---|---|---|
| 2 (6 oct) | DHCP | 67/68 |
| 3 (octubre) | DNS (BIND9) | 53 (UDP + algo de TCP) |
| 4 | Apache | 80 / 443 |
| 5 | FTP (`vsftpd`) | 20/21 (activo/pasivo) |
| 2º trim | SMTP / POP3 / IMAP | 25 / 110 / 143 |
| desde el minuto 1 | SSH | 22 |

## Datagramas
- Un **datagrama = paquete**: "una caja con su etiqueta", los datos que viajan de origen a destino. El mismo concepto por UDP o TCP, pero con estructura distinta (IPv4/IPv6 + cabecera + payload).
- Demo con `ping -c 3 unir.net` desde el servidor AWS: cada eco es un datagrama ICMP; se ve la IP privada local resolviendo vía DNS a la IP pública de destino.
- Detalle real de clase: el ping **desde el portátil local a unir.net no respondía** (100% paquetes perdidos, timeout) pero **desde el servidor sí respondía** — probablemente un firewall bloqueando ICMP echo request en la red local del profesor (detectado en directo por un alumno). Pista: cuando el eco no vuelve pero sí resuelve DNS, sospechar de un firewall que bloquea ICMP, no de que el host esté caído.
- IP pública de salida: comando `curl ifconfig.me` (o visitar una página que la devuelva) — distinto de la IP privada que ves con `ip a`.

## NAT
- El NAT traduce direcciones de red entre la red interna (privada) y la externa (pública).
- **NAT estático**: la IP privada y la pública son la misma (ejemplo real: un VPS en OVH con IP fija).
- **NAT dinámico**: una IP privada se mapea a una de un pool de públicas, puede ir rotando (caso de AWS EC2: `ip a` muestra una IP privada tipo 172.x, pero la pública real —vista con `curl ifconfig.me`— es otra, p. ej. 54.x).
- **PAT / NAT sobrecargado** (overloading): muchas IPs privadas comparten una sola IP pública — es lo que pasa en casa con el router; también explica por qué un ISP (Movistar, Vodafone...) puede tener muchos clientes saliendo por la misma IP pública rotativa (por eso no tenemos IP pública fija en casa salvo que se contrate).

## Shodan — reconocimiento de servicios expuestos
- Demo con **shodan.io**: buscador de "cosas" conectadas a Internet (cámaras, NAS, servidores...).
- Sintaxis vista: `port:22 country:ES` (SSH abiertos en España), `port:3389` (escritorio remoto Windows), filtros por ciudad (`city:Madrid`), categoría `Explore` → `Research`/`Industrial Control Systems`/`Webcams`.
- **Aviso legal explícito en clase**: "mirar es legal, pero entrar en una máquina ajena no". Un compañero (con experiencia en seguridad) matiza: acceder sin usuario/contraseña puede defenderse como no intencionado, pero **nunca se debe hacer**.
- Moraleja para cuando levantéis vuestro propio servidor: una IP pública con un puerto visible **se encuentra sola**, en minutos, por bots de escaneo (el profesor menciona un bot llamado "Solder"/similar que rastrea todo lo publicado — no verificado el nombre exacto).

## Protocolo
- **Protocolo = idioma**: define sintaxis (cómo se estructura el datagrama: un datagrama ICMP no es igual que uno TCP) y semántica (qué significa cada código, p. ej. **404 = recurso no encontrado**, porque así lo decidió el RFC correspondiente).
- Cada protocolo de aplicación necesita elegir entre **fiable** (TCP: reordena, retransmite lo perdido — ideal para HTTP, donde una página rota no sirve) o **rápido** (UDP: no espera confirmación, tolera pérdida — ideal para streaming/videollamada).
- **Demo en directo con BIND**: el profesor añade un registro DNS tipo A a un dominio propio (`roja.<dominio>.com` → una IP inventada), y muestra con `dig` y la web **whatsmydns.net** cómo se propaga a nivel mundial en segundos — ejemplo práctico de por qué el DNS va por UDP (rapidez) en la resolución estándar.
- Comandos usados: `dig unir.net`, `host roja.<dominio>.com`.

## Clasificación de redes (repaso rápido, "esto es de primero")
- Por alcance: **PAN** (bluetooth móvil-reloj) < **LAN** (un edificio) < **MAN** (una ciudad) < **WAN** (un país) < lo que el profesor llama en broma "GAN" (todo el planeta).
- Por conexión: cableada / inalámbrica. Por relación funcional: cliente-servidor o P2P.
- Comparado con una VPC de AWS: combina red privada (VPC) + salida pública — "un poco de todo lo anterior".

## Infraestructura física de Internet (apartado curioso/anecdótico)
- Internet viaja mayoritariamente **por cables submarinos** intercontinentales (mapa mostrado: submarinecablemap.com).
- España recibe cables en **Bilbao/Sopelana** (cable "Marea", desde Virginia EEUU, co-construido por Microsoft/Facebook; y "Grace Hopper", desde Nueva York).
- El **Estrecho de Gibraltar** es un punto crítico de paso de cables entre el Atlántico y el Mediterráneo — un alumno con experiencia real en telecos cuenta (**no verificado**, anécdota personal) que se colocaron bloques de hormigón en el fondo para impedir que la pesca de arrastre dañara los cables.
- Starlink: constelación de satélites de Elon Musk, visible a simple vista en cielos sin contaminación lumínica, alternativa a los cables submarinos para dar cobertura.
- **Los 13 servidores raíz DNS mundiales** dependen, en origen, de instituciones estadounidenses (universidades, NASA, Departamento de Defensa, Armada de EEUU) — herencia directa de **ARPANET**, proyecto militar de EEUU del que nace Internet.

## Para la próxima clase (23/09)
Laboratorio: crear el primer servidor en AWS desde cero (instancia Ubuntu 24.04, par de claves, conexión SSH) y trabajar con comandos básicos de Linux.

## Enlaces
RFC / buscador: rfc-editor.org · IANA: iana.org (registro de puertos) · Shodan: shodan.io · Propagación DNS: whatsmydns.net · Mapa de cables submarinos: submarinecablemap.com
