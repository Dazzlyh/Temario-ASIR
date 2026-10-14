---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-10-07
tema: Laboratorio 2 · DHCP real sobre una red falsa (cable virtual veth)
fuente: guía PDF del profesor (8 páginas) + script preparar_red.sh + transcripción de la clase en directo
---
# SER · Laboratorio 2 (07/10) · DHCP con cable virtual

> Anterior: [Clase 4: DHCP](2026-10-06_clase4-dhcp.md) · Profesor: Damián Sualdea Soy

**Esta actividad no se entrega ni se puntúa** — es solo para ver un DHCP funcionando de verdad. El profesor avisa explícitamente: no es así como se monta un DHCP en producción, es una trampa para poder verlo sin tener dos máquinas reales.

> Nota de transcripción: el audio de esta clase se transcribió con bastante ruido en los nombres de comandos (p. ej. "Betlee"/"Beathclip" por `veth`, nombres de interfaz poco claros). Los conceptos y el procedimiento de abajo son fieles a lo explicado en clase, pero antes de teclear en el examen o en una entrega real, verificar la sintaxis exacta contra la guía PDF de 8 páginas que subió el profesor (`SER_Lab02_*`), no contra este resumen.

## Por qué hay que hacer trampa
AWS **capa mucho** la VPC: no deja montar un servidor DHCP propio dentro de la red privada de Amazon (esa red ya tiene su propio DHCP, el de Amazon, y no se puede sustituir). Como no se puede levantar una segunda instancia EC2 para hacer de cliente real, la solución es simular cliente y servidor **dentro de la misma instancia** (`srv2`, Ubuntu 24.04), creando un **cable de red virtual** (interfaz tipo `veth`, par de interfaces virtuales conectadas entre sí) con un script ya preparado (`preparar_red.sh`). Un extremo del cable hace de servidor, el otro de cliente sin IP.

## Antes de nada: permisos del script
El script llega sin permiso de ejecución (`rw- rw- r--`). Para ejecutarlo:
```bash
chmod +x preparar_red.sh      # o chmod u+x preparar_red.sh (notación simbólica)
ls -l                          # el script pasa a verse en VERDE: tiene permiso de ejecución
sudo ./preparar_red.sh
```
Truco repetido en clase para ver permisos: con `ls -l` lo que aparece en **verde** es lo que tiene bit de ejecución activo.

El script monta el cable virtual y dice qué lado es cuál: un extremo (`vez-srv` aprox.) con IP **10.10.0.1** (el servidor), el otro extremo sin ninguna IP todavía (el cliente).

## Instalar el servidor DHCP
```bash
sudo apt update
sudo apt install -y isc-dhcp-server
```
El paquete en Ubuntu/Debian se llama literalmente `isc-dhcp-server` (de ahí el nombre del binario/servicio).

## Regla de oro antes de tocar cualquier configuración: copia de seguridad
```bash
cd /etc/dhcp
sudo mv dhcpd.conf dhcpd.conf.original    # mv aquí NO mueve, renombra -> hace de copia de seguridad
sudo nano dhcpd.conf                       # el nuevo queda vacío, se escribe desde 0
```
Lo mismo con `/etc/default/isc-dhcp-server`: ahí se pone el nombre de la interfaz donde tiene que escuchar el servidor (`INTERFACESv4="<interfaz-del-cable-virtual>"`).

Repaso de `grep` (vale para cualquier fichero de configuración del curso): buscar un patrón dentro de un fichero y que lo saque resaltado si existe.
```bash
grep "INTERFACESv4" /etc/default/isc-dhcp-server
```

En `dhcpd.conf` se define la subred falsa con su rango de IPs (ámbito), igual que en la teoría de la Clase 4: `subnet ... netmask ... { range 10.10.0.50 10.10.0.100; ... }` — el profesor entra en directo dejando la configuración similar a la de la diapositiva 18 ya mencionada en la Clase 4.

## Arrancar y comprobar el servicio
```bash
sudo systemctl restart isc-dhcp-server
sudo systemctl status isc-dhcp-server
sudo ss -tulnp | grep 67       # confirma que el servicio escucha en el puerto 67/UDP
```

## Ver los logs en vivo (journalctl)
```bash
sudo journalctl -u isc-dhcp-server -f
```
Comparación que hace el profesor: es como un `tail -f` de un fichero que no para de crecer, o como leer un periódico con las últimas noticias del servicio — cada entrada nueva del log aparece aquí en tiempo real. Lo deja abierto en una ventana durante toda la práctica.

## El cliente pide IP (el DORA, visto en vivo)
Desde la otra "ventana" (misma máquina, otro terminal apuntando al lado cliente del cable virtual), se simula un cliente DHCP pidiendo dirección. Antes de pedir: sin IP en absoluto. Al lanzar la petición, en la ventana del `journalctl` del servidor aparece en vivo la secuencia completa **DHCPDISCOVER → DHCPOFFER → DHCPREQUEST → DHCPACK**, confirmando en la práctica lo que ya se había visto en teoría en la Clase 4. El cliente recibe una IP del rango (en la demo, la **.50**, la primera del rango).

### Capturando el DORA por cable con tcpdump (en vez de journalctl)
```bash
sudo tcpdump -i <interfaz-cable-virtual> -n port 67 or port 68
```
Con esto se ve el tráfico **tal y como viaja por el cable**, no el log interno del servicio — permite ver que cualquiera que tenga acceso a ese segmento de red y levante un sniffer (`tcpdump`, Wireshark) puede ver toda la negociación DHCP en claro (no hay cifrado ni autenticación en el protocolo, coherente con lo visto en la Clase 4 sobre DHCP "falso"/MITM).

## Observación sobre los tiempos (confirmación práctica de la teoría)
El profesor puso en la configuración de prueba un `default-lease-time`/`max-lease-time` corto (**120 segundos**) a propósito, para poder ver en minutos lo que en producción tardaría horas. Resultado observado en el log:
- El cliente vuelve a pedir/renovar aproximadamente a los **60 s** (el 50% de 120 s: renovación).
- Si no ha podido renovar con su servidor, amplía la pregunta a toda la red a los **~105 s** (el 87,5% de 120 s: reenlace/rebinding).
Esto coincide exactamente con los porcentajes de RFC 2131 (renovación al 50%, reenlace al 87,5%) ya documentados en la Clase 4, ahora visto con cronómetro real en lugar de leído en la ficha.

## Reserva de IP por MAC (en directo)
1. En el lado cliente, comprobar la MAC de su adaptador (equivalente a `ip link show` → dirección `ether`). El profesor la llama coloquialmente "el DNI de la tarjeta de red".
2. En `dhcpd.conf`, añadir un bloque de reserva con esa MAC y una IP fija dentro (o fuera) del rango:
   ```
   host cliente-reservado {
       hardware ethernet <MAC-del-cliente>;
       fixed-address 10.10.0.80;
   }
   ```
3. Reiniciar el servicio (`sudo systemctl restart isc-dhcp-server`).
4. En el cliente: liberar la IP actual y volver a pedir. Resultado: en vez de recibir una IP cualquiera del rango (la .50 de antes), recibe **siempre la .80** — la reserva por MAC tiene prioridad sobre la asignación dinámica normal.

**Por qué importa en el mundo real**: así es como se reservan direcciones estables (vía DHCP, sin tener que configurar IP estática a mano) para servidores de correo, web, NAS o cualquier equipo cuya IP no puede cambiar — se coge la MAC de su tarjeta y se mete como reserva en el `dhcpd.conf` del servidor DHCP real.

## Limpiar y repetir desde cero
Al terminar (o para que cada alumno pueda repetir la práctica las veces que quiera):
```bash
sudo systemctl stop isc-dhcp-server
sudo apt purge -y isc-dhcp-server
sudo apt autoremove -y
```
Y eliminar/deshacer el cable virtual de pruebas (lo monta el mismo script de preparación, así que relanzarlo vuelve a dejar todo listo para empezar de 0).

## Logística / próxima clase
- Próxima clase: **DNS**. El profesor va a colgar en el foro un vídeo propio explicando la parte técnica antes de la clase en directo — avisa de que es su primer vídeo grabado y bromea sobre su aspecto (anécdota sin valor técnico).
- Plan declarado para el resto del curso: siempre que toque laboratorio, primero se explica el concepto en teoría y luego se va directo a la práctica con el guión preparado — mismo formato que esta sesión.
