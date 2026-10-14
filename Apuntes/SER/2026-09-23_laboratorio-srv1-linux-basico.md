---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-09-23
tema: Primer laboratorio — SRV1 desde cero en AWS, comandos básicos de Linux, primer Apache
fuente: transcripción de la clase en directo
---
# SER · Laboratorio: SRV1 desde cero (23/09)

> Anterior: [22/09 · Conceptos básicos de red: puertos, datagramas, NAT, protocolos](2026-09-22_conceptos-red-puertos-nat.md) · Siguiente: [29/09 · Modelo TCP/IP en directo](2026-09-29_modelo-tcpip-en-directo.md)

Primer laboratorio, 100% práctico, **sin copiar-pegar los comandos clave** ("vamos al barro"): crear una instancia EC2 desde cero, conectarse por SSH, y recorrer los comandos básicos de Linux que se van a usar durante todo el curso.

## Crear la instancia (SRV1) en AWS
1. EC2 → Lanzar instancia → nombre **SRV1** (o SRV01, da igual la numeración; cada alumno nombra el suyo).
2. Imagen: **Ubuntu Server 24.04**.
3. Tipo de instancia: no tocar (la que viene por defecto / free tier).
4. **Par de claves**: crear uno nuevo, tipo **RSA** (el profesor lo prefiere a ED25519 "por costumbre"; un alumno apunta que ED25519 es un cifrado más moderno — ambos válidos). Nombre de ejemplo: `ser001` (clave para "servicios en red", alumno 001). Se descarga el `.pem`: la clave pública queda en AWS, la privada (el `.pem`) hay que guardarla bien — es la llave de acceso.
5. Grupo de seguridad: de momento solo con **SSH** habilitado (el resto del firewall de AWS se va abriendo en laboratorios posteriores, puerto a puerto, según el servicio).
6. Lanzar instancia → en el listado de EC2, seleccionar la instancia → **Conectar** → pestaña **Clientes SSH**: ahí AWS ya te da el comando de conexión completo, listo para copiar.

```bash
# permisos obligatorios de la clave privada antes de poder usarla
chmod 400 ser001.pem

# conexión (el comando exacto con IP/DNS lo da el propio panel de AWS en "Conectar")
ssh -i "ser001.pem" ubuntu@<dns-publico-o-ip-de-la-instancia>
# primera vez pregunta por el fingerprint -> responder "yes"
```

## Primeros comandos de reconocimiento
```bash
whoami          # quién soy (útil para saber si entraste "en malas maneras" / confirmar usuario)
hostname        # nombre de la máquina (aquí: el que le pusiste a la instancia)
pwd             # Print Working Directory: dónde estoy (home por defecto: /home/ubuntu)
```
- El prompt `usuario@host:~$` — el **`~`** (virgulilla) significa "estoy en mi carpeta home".
- **`$` = usuario normal**, **`#` = superusuario (root)** — diferencia importante de ver en el prompt.

## Convertirse en superusuario
```bash
sudo su          # te conviertes en root (evita escribir "sudo" delante de cada orden)
whoami            # -> root
hostname          # no cambia
pwd               # si vienes de /home/ubuntu y haces sudo su, pwd pasa a decir otra ruta:
cd                # sin argumentos -> te lleva a TU home (root va a /root, no a /home/ubuntu)
exit              # sale de root y vuelve al usuario normal (ubuntu)
```
- Detalle de permisos real visto en clase: `cat /etc/sudoers` muestra que, por defecto, **solo el usuario `ubuntu` puede hacer `sudo`** (sin pedir contraseña) en una instancia AWS recién creada; si se crea un usuario nuevo y se quiere que sea sudoer hay que añadirlo ahí (se verá más adelante).

## Navegación y estructura de directorios
```bash
cd /          # raíz del sistema de ficheros
cd ..         # sube un nivel
cd            # va a tu home
cd /var/log   # con el TAB puedes autocompletar -> una pulsación completa si no hay ambigüedad;
              # dos pulsaciones muestran las opciones si hay varias coincidencias (lib / local / lock / log...)
```
Rutas clave explicadas en clase:
- `/etc` — ficheros de configuración.
- `/var/log` — registros del sistema (logs).
- `/home/<usuario>` — carpeta personal de cada usuario.
- `/root` — home del superusuario (no confundir con `/home/ubuntu`).

## Gestión de ficheros (el set mínimo que usa el profesor)
```bash
mkdir -p pruebas/dia1        # -p crea toda la estructura de carpetas de golpe
apt install tree             # (tras apt update) herramienta para ver el árbol de carpetas
tree                         # ver estructura
cd pruebas/dia1
touch nota.txt               # crea fichero vacío
nano nota.txt                # editor de texto: Ctrl+O (guardar) + Enter, Ctrl+X (salir)
cat nota.txt                 # ver contenido por pantalla
cp nota.txt copia.txt        # copiar
mv copia.txt segunda.txt     # mover / renombrar (si no cambias de carpeta, renombra)
ls -lah                      # listado completo, incluidos ocultos, tamaños legibles
rm segunda.txt                # eliminar (¡cuidado con rm -rf!)
find /etc -name "*.com"      # buscar ficheros; * es patrón comodín de nombres
```
Nota del profesor: "con esto trabajáis mucho; no hagáis un `rm -rf` que la liamos" — advertencia explícita sobre el borrado recursivo forzado.

## Gestión de paquetes (APT)
```bash
apt update                   # SIEMPRE antes que nada: actualiza la lista de paquetes del repositorio
                              # (busca en /etc/apt/sources.list[.d]/ el repo configurado, p.ej. security.ubuntu.com)
apt upgrade -y                # actualiza los paquetes instalados (-y evita la pregunta de confirmación)
apt search <nombre>            # buscar en el repositorio si existe un paquete (ej: "bind9", "vsftpd")
apt install apache2            # instalar un servicio
apt purge apache2              # desinstalar completamente un paquete y su configuración
apt update                     # (otra vez) para verificar que todo quedó consistente tras purgar
```
- **`apt update` ≠ `apt upgrade`**: `update` refresca el índice de paquetes disponibles; `upgrade` instala las nuevas versiones. El profesor advierte: **en servidores no se hace `upgrade` a la ligera**, salvo entorno muy controlado, porque puede romper versiones concretas de PHP/Angular/etc. de las que dependen las aplicaciones instaladas.

## systemctl — gestionar servicios
```bash
systemctl status ssh         # ver estado de un servicio (q para salir del paginador)
systemctl status apache2
systemctl stop apache2       # parar (queda "inactive" pero seguiría arrancando al reiniciar la máquina)
systemctl start apache2      # arrancar
systemctl restart apache2    # reiniciar
```

## Primer servicio real: Apache
```bash
apt install apache2 -y
ss -tlnp                     # confirmar que aparece un nuevo puerto en LISTEN (80) tras instalar
systemctl status apache2     # "active (running)"
```
- Verificación: ir a `http://<ip-publica>` desde el navegador — en este punto **da error/no conecta** porque el **grupo de seguridad de AWS todavía no tiene abierto el puerto 80** (solo se abrió SSH al crear la instancia). Queda pendiente para el siguiente laboratorio abrir el firewall por servicio.
- Para quitarlo todo: `systemctl stop apache2` → `apt purge apache2` → `apt update` (verificación final).

## Comandos de red básicos usados
```bash
ip a                          # ver IPs locales (equivalente más corto a "ip addr show")
ss -tulpn                     # ver todos los puertos en escucha (TCP+UDP), con el proceso
```

## Cierre del laboratorio
**Muy importante** (insistido varias veces por el profesor): al terminar la práctica, **parar la instancia** en el panel EC2 (nunca "terminar/eliminar" salvo que se indique) — para no consumir crédito/horas de la cuenta.

## Para la próxima clase
Traer **Kali** instalado/descargado — se presentará la herramienta con la que se trabajará en la parte de seguridad del curso.
