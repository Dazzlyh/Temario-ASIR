---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-10-07
tema: Laboratorio 2 · tu propio servidor DHCP sobre una red de pruebas (veth + netns)
fuente: SER_Lab02_Guia.pdf (8 páginas) + transcripción de la clase en directo
---
# SER · Laboratorio 2 (07/10) · Tu propio servidor DHCP

> Anterior: [Clase 4: DHCP](2026-10-06_clase4-dhcp.md) · Profesor: Damián Sualdea Soy

**Esta actividad no se entrega ni se puntúa** — es solo para verlo funcionar. El giro respecto a la Clase 4: allí `srv1` era el que **pedía** (cliente del DHCP de Amazon); hoy `srv1` pasa a ser el que **reparte**, con su propio rango, tiempos y fichero de concesiones, frente a un cliente simulado.

## El montaje: una sola máquina, dos papeles
En la VPC de Amazon el DHCP es de Amazon y no se puede sustituir ni apagar. La solución: fabricar una **red de pruebas dentro de la propia `srv1`**, sin segunda máquina, usando dos mecanismos de Linux:
- **`veth`**: un cable de red virtual con dos extremos (`veth-srv` y `veth-cli`), como un cable ethernet entre dos tarjetas.
- **network namespace** (`ip netns`): una pila de red completa y aislada dentro de la misma máquina — para el sistema, es "otro equipo". El extremo `veth-cli` se mete dentro de ese espacio de nombres llamado `cliente`.

| En esta red | `srv1` es | Quién reparte las direcciones |
|---|---|---|
| `ens5` · 172.31.0.0/20 (VPC Amazon) | Cliente | El DHCP de Amazon (172.31.0.1) |
| `veth-srv` · 10.10.0.0/24 (red de pruebas) | Servidor | Tú, con el `dhcpd.conf` de hoy |

Nada de este tráfico sale de la máquina ni toca la red de Amazon — es justo lo que **no** se puede hacer en casa, donde el router ya reparte direcciones y un segundo DHCP dejaría sin Internet a quien esté conectado.

## Parte 0 · Fabricar la red de pruebas
```bash
sudo apt update
cat > preparar-red.sh <<'FIN'
#!/bin/bash
set -e
if [ "$1" = "borrar" ]; then
  ip netns del cliente 2>/dev/null || true
  ip link del veth-srv 2>/dev/null || true
  echo "Red de pruebas eliminada."; exit 0
fi
ip netns del cliente 2>/dev/null || true
ip netns add cliente
ip link del veth-srv 2>/dev/null || true
ip link add veth-srv type veth peer name veth-cli
ip link set veth-cli netns cliente
ip addr add 10.10.0.1/24 dev veth-srv
ip link set veth-srv up
ip netns exec cliente ip link set lo up
ip netns exec cliente ip link set veth-cli up
echo; echo "Red de pruebas lista."
echo "  Servidor -> veth-srv  10.10.0.1/24"
echo "  Cliente  -> veth-cli  sin direccion"
echo; echo "MAC del cliente (la necesitas en la parte 4):"
ip netns exec cliente ip -brief link show veth-cli | awk '{print "  " $3}'
FIN
chmod +x preparar-red.sh
sudo ./preparar-red.sh
```
Las comillas `'FIN'` del heredoc son importantes: evitan que la shell interprete nada del contenido del script al pegarlo. Apuntar la **MAC del cliente** que imprime el script al final — hace falta en la parte 4.

Comprobar los dos extremos:
```bash
ip -brief address show veth-srv                 # servidor: 10.10.0.1/24
sudo ip netns exec cliente ip -brief address     # cliente: sin dirección
```
**Regla constante en todo el laboratorio**: cualquier comando que deba ejecutarse "dentro" del cliente lleva siempre delante `sudo ip netns exec cliente`. Si se olvida, el comando se ejecuta en `srv1` y no en el cliente simulado.

## Parte 1 · Instalar el servidor y decirle dónde escuchar
```bash
sudo apt update && sudo apt install -y isc-dhcp-server
sudo nano /etc/default/isc-dhcp-server
```
Se instala y arranca mal a propósito: todavía no sabe por qué interfaz escuchar. Buscar la línea `INTERFACESv4=""` (casi al final, vacía) y dejarla:
```
INTERFACESv4="veth-srv"
```
Guardar con `Ctrl+O`, `Enter`, `Ctrl+X`, y comprobar:
```bash
grep INTERFACESv4 /etc/default/isc-dhcp-server
```
Con eso el servidor escucha por la red de pruebas y no por `ens5` (ahí manda Amazon).

Si el servicio falla al arrancar en este punto es normal — todavía falta el `dhcpd.conf` de la parte 2. Diagnóstico siempre igual: `sudo journalctl -u isc-dhcp-server -n 20 --no-pager`. Si alguna vez sale «There's already a DHCP server running»: `sudo systemctl stop isc-dhcp-server` + `sudo rm -f /run/dhcpd.pid` antes de reintentar.

## Parte 2 · El ámbito y el rango (se escribe a mano, no se copia)
El paquete trae un `dhcpd.conf` de ejemplo con 50 líneas de `example.org` que no sirven aquí. En vez de borrarlas una a una, se aparta el original (copia de seguridad con `mv`, mismo patrón que en SAD) y se empieza en blanco:
```bash
sudo mv /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.original
sudo nano /etc/dhcp/dhcpd.conf
```
Contenido completo (9 líneas, el fichero que **sí hay que escribir a mano**):
```
default-lease-time 120;    # 2 minutos, para verlo rápido
max-lease-time 120;        # el tope de arriba
authoritative;

subnet 10.10.0.0 netmask 255.255.255.0 {
  range 10.10.0.50 10.10.0.60;
  option routers 10.10.0.1;
  option domain-name-servers 8.8.8.8, 1.1.1.1;
  option domain-name "laboratorio.local";
}
```
Arrancar y comprobar:
```bash
sudo systemctl restart isc-dhcp-server
sudo systemctl status isc-dhcp-server --no-pager
sudo ss -ulpn | grep 67       # activo y escuchando en 67/UDP, proceso dhcpd
```
Error típico si falta la subred: «No subnet declaration for veth-srv (10.10.0.1)» + «Not configured to listen on any interfaces!» — significa que el `dhcpd.conf` no tiene ninguna `subnet` que encaje con la red de `veth-srv` (fichero no guardado, o se dejó el de ejemplo, o la red declarada no coincide con la de la interfaz).

## Parte 3 · Pedir dirección y ver el DORA
Hacen falta **dos sesiones SSH simultáneas** a la misma `srv1` (no son dos máquinas, son dos ventanas de terminal contra la misma): **VENTANA SERVIDOR** (mira lo que recibe/contesta el servidor) y **VENTANA CLIENTE** (pide dirección). El cliente DHCP en Ubuntu 24.04 es **`dhcpcd`** — `dhclient` ya no existe, ISC lo abandonó en 2022 (mismo dato ya visto en la Clase 4 de DHCP).

### 3a · El servidor lo cuenta (journalctl)
```bash
### VENTANA SERVIDOR ###
sudo journalctl -u isc-dhcp-server -f
```
```bash
### VENTANA CLIENTE ###
sudo ip netns exec cliente dhcpcd -k veth-cli      # suelta lo que tuviera (DHCPRELEASE)
sudo ip netns exec cliente dhcpcd -d -1 veth-cli   # pide una nueva (-d: detalla, -1: sale al tener IP)
```
En la ventana servidor aparecen los 4 mensajes del DORA con su nombre oficial, identificando siempre por MAC (el cliente aún no tiene IP):
```
DHCPDISCOVER from ea:b8:4f:77:b0:14 via veth-srv
DHCPOFFER    on 10.10.0.50 to ea:b8:4f:77:b0:14 via veth-srv
DHCPREQUEST  for 10.10.0.50 (10.10.0.1) from ea:b8:4f:77:b0:14
DHCPACK      on 10.10.0.50 to ea:b8:4f:77:b0:14 via veth-srv
```
En la ventana cliente, la otra mitad: `sending DISCOVER` → `offered 10.10.0.50 from 10.10.0.1` → `sending REQUEST` → `acknowledged 10.10.0.50`.

**Tres líneas del cliente que valen por media clase de teoría:**
- `leased 10.10.0.50 for 120 seconds` y debajo `renew in 60 seconds, rebind in 105 seconds`. 60 s es el 50 % exacto de 120 (renovación) y 105 s es el 87,5 % (reenlace) — el cliente los calcula solo, con los porcentajes de RFC 2131 ya vistos en la Clase 4; aquí se confirma con cronómetro real.
- `ARP probing 10.10.0.50 (1 of 3)`: antes de quedarse la IP, el cliente pregunta por ARP si alguien ya la está usando; si respondiera alguien, la rechazaría con un **DHCPDECLINE**.
- `discarding expired lease`: si ya se había pedido antes, la concesión anterior había caducado y se descarta.

Mensaje inofensivo que puede salir: «Failed to set DNS configuration: Link 5 not known» — dentro del espacio aislado no hay servicio de DNS al que escribirle los servidores, pero la dirección y la ruta sí se aplican.

Comprobar la IP asignada **sin esperar** (al salir con `-1` nadie renueva, y a los 120 s la concesión caduca sola y la IP desaparece — no es un fallo, es ver caducar una concesión):
```bash
sudo ip netns exec cliente ip -brief address
```

### 3b · Los paquetes en crudo (tcpdump)
```bash
### VENTANA SERVIDOR ### (Ctrl+C para parar el journalctl antes)
sudo tcpdump -i veth-srv -n port 67 or port 68
```
```bash
### VENTANA CLIENTE ###
sudo ip netns exec cliente dhcpcd -k veth-cli
sudo ip netns exec cliente dhcpcd -d -1 veth-cli
```
`tcpdump` llama «Request» a todo lo del cliente y «Reply» a todo lo del servidor (nomenclatura BOOTP) — lo que importa son las direcciones, no esas etiquetas:
```
0.0.0.0.68      > 255.255.255.255.67   el cliente no tiene dirección: grita
10.10.0.1.67    > 10.10.0.50.68        le contesta el servidor
```
El registro del servidor (`journalctl`) dice **qué** mensaje es; la captura (`tcpdump`) dice **cómo** viaja por el cable. Juntas son el DORA completo.

**La contabilidad del servidor** — lo que diferencia un servidor DHCP de un reparto a ciegas:
```bash
sudo cat /var/lib/dhcp/dhcpd.leases
```
Cada entrada `lease` trae la dirección, hora de inicio/fin de la concesión y la MAC — por eso el servidor nunca repite una dirección ya concedida. La resta fin−inicio tiene que dar los 120 s configurados.

## Parte 4 · Reserva por MAC
```bash
### VENTANA CLIENTE ###
sudo ip netns exec cliente ip -brief link show veth-cli    # para confirmar la MAC
```
Añadir al final de `/etc/dhcp/dhcpd.conf` (con la MAC real del cliente, no la del ejemplo):
```
host cliente-lab {
  hardware ethernet AA:BB:CC:DD:EE:FF;
  fixed-address 10.10.0.80;
}
```
```bash
sudo systemctl restart isc-dhcp-server
### VENTANA CLIENTE ###
sudo ip netns exec cliente dhcpcd -k veth-cli      # DHCPRELEASE
sudo ip netns exec cliente dhcpcd -d -1 veth-cli
sudo ip netns exec cliente ip -brief address       # ahora: 10.10.0.80, no una del rango
```
Es la asignación estática con reserva del tema: el servidor reconoce la MAC y da siempre la misma IP. Así se reservan en producción direcciones estables para servidores de correo, web o NAS sin tener que configurar IP estática a mano en cada equipo.

## Parte 5 · Romperlo a propósito (agotar el rango)
Reducir el rango a solo dos direcciones y hacer que pidan tres clientes. Si se complica montar un tercer cliente de verdad, la guía da un atajo: comentar la reserva, dejar el rango con una sola dirección, y pedir **dos veces seguidas** desde el mismo cliente (`dhcpcd -k` + `dhcpcd -d -1`) — la segunda vez no hay nada que dar.

**Qué se ve**: el cliente sin dirección acaba **autoasignándose una 169.254.x.x (APIPA)** — el síntoma de "pedí y nadie me dio" (servidor caído, rango agotado, o tráfico que no llega). Es exactamente el mecanismo detrás del **ataque de agotamiento de rango** visto en la Clase 4 de DHCP.

## Antes de irse (dejar la instancia limpia)
```bash
sudo systemctl stop isc-dhcp-server
sudo ./preparar-red.sh borrar
sudo pkill tcpdump
exit
```
Y en EC2: **Instance state → Stop instance. Nunca Terminate.**

### Para repetirlo de cero
```bash
sudo systemctl stop isc-dhcp-server
sudo apt purge -y isc-dhcp-server
sudo apt autoremove -y
sudo rm -rf /etc/dhcp /var/lib/dhcp /run/dhcpd.pid
sudo ./preparar-red.sh borrar      # primero deshacer la red...
rm -f preparar-red.sh              # ...y después borrar el script
sudo rm -f /var/lib/dhcpcd/veth-cli.lease
```
**Nunca** `apt purge dhcp*` con comodín: se llevaría por delante `dhcpcd` (el cliente que trae Ubuntu, necesario en la parte 3) junto con el servidor. El `purge` de `isc-dhcp-server` no toca `dhcpcd`, porque el cliente guarda su estado en `/var/lib/dhcpcd`, no en `/etc/dhcp`.

## Checklist de autoevaluación (las 6 del laboratorio)
1. He creado la red de pruebas y sé qué extremo es servidor y cuál cliente.
2. `isc-dhcp-server` arranca y escucha en el puerto 67.
3. Sé qué es el ámbito, el rango y qué significa cada opción del fichero.
4. He visto los cuatro paquetes del DORA en `tcpdump`.
5. He hecho una reserva por MAC y el cliente recibe esa dirección.
6. Sé leer el fichero de concesiones del servidor (`dhcpd.leases`).

## Logística
Dudas → foro, el mismo día, con captura del error. **13 de octubre empieza DNS**, montado sobre estas mismas máquinas (`srv1`/`srv2`).
