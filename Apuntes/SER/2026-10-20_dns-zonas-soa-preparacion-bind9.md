---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-10-20
tema: Tema 3 · DNS — archivo de zona, registro SOA, delegación de NS personalizados y preparación de AWS para BIND9
fuente: transcripción de la clase en directo
---
# SER · DNS: archivo de zona, SOA y preparación de AWS para BIND9 (20/10)

> Anterior: [Tema 3: arranque de DNS (13/10)](2026-10-13_tema3-dns-jerarquia-zonas.md) · Profesor: Damián Sualdea Soy

Clase puente entre la teoría de DNS (13/10) y el laboratorio de BIND9 del día siguiente (21/10). El profesor lo dice explícitamente: **hoy no se toca BIND9 todavía** — es la clase para entender de antemano el archivo de zona, los comandos (`host`, `dig`), el registro SOA con detalle, y dejar preparado el servidor de AWS (Elastic IP + Security Group) para que el laboratorio de mañana no se pierda tiempo con eso. También resuelve dudas de logística sobre dominios (GitHub Student Pack / Namecheap / IONOS) de varios alumnos que todavía no lo tenían.

## Objetivo de la clase (dicho explícitamente por el profesor)
1. Entender los **7 registros de un archivo de zona** (lo que más tiempo ocupa de la clase).
2. La **replicación**: servidor principal y servidor de réplica (aunque en la asignatura se trabaja con uno solo).
3. El **DNS dinámico** (mención breve, ver más abajo).

## Archivo de zona: formato de 5 columnas
El profesor insiste en que el fichero de zona **no es una base de datos, es un fichero de texto plano** que se edita a mano (nunca por SQL): si lo editas mal, el dominio deja de funcionar. Todos los registros siguen la misma estructura de columnas:

| Columna | Qué es | Ejemplo visto en clase |
|---|---|---|
| Nombre | El registro al que se refiere la línea | `@`, `www`, `ns1` |
| TTL | Segundos en caché (ej. `3600`) | `3600` |
| Clase | Siempre `IN` (de Internet) | `IN` |
| Tipo | `NS`, `A`, `CNAME`, `MX`, `TXT`... | `NS` |
| Valor/datos | A dónde apunta (otro nombre o una IP) | `ns.alumno7.despegando23.com.` |

- El **`@` (arroba)** es el registro raíz/apex del dominio; cuando se pone `@` + `NS`, se está diciendo "esto es una transferencia completa de la zona" (quién es el DNS autoritativo de todo el dominio).
- Ejemplo trabajado en clase: `NS alumno7.despegando23.com.` → significa que ese NS gestiona `despegando23.com`.

## El registro SOA en detalle (novedad respecto al 13/10)
El 13/10 solo se mencionó que el SOA existe; hoy se explican sus campos uno a uno con el ejemplo propio del profesor (`ns.alumno7.despegando23.com.`):

| Campo del SOA | Qué significa | Ejemplo / valor usado en clase |
|---|---|---|
| Servidor primario (NS del SOA) | Quién es el DNS autoritativo/principal de la zona | `ns.alumno7.despegando23.com.` |
| Admin (hostmaster) | Contacto administrativo de la zona (un segundo campo tipo email, con `.` en vez de `@`) | el que el profesor tiene puesto en IONOS |
| **Serial** | Versión de la zona; si la subes, "avisas" de que hay un cambio — pero **cambiar el serial no hace que el cambio salga de tu máquina por sí solo**, solo es la referencia de versión | formato año-mes-día + nº de cambio del día, ej. `2026102001` (21 de octubre de 2026, primer cambio del día) — el profesor dice que él nunca lo toca a mano |
| **Refresh** | Cada cuánto tiempo el secundario pregunta/comprueba al primario | ejemplo en clase: 2 h (el profesor sugiere bajarlo en pruebas) |
| **Retry** | Cada cuánto se reintenta si una comprobación falla | ejemplo en clase: 1 h |
| **Expire** | Cuándo el secundario "se rinde" si no puede contactar al primario y descarta la copia | ejemplo en clase: 2 semanas |
| **TTL mínimo** | El TTL mínimo de la zona completa, el que se usa por defecto para el despliegue si no se especifica otro | — |

- El profesor avisa de que, en la práctica de la asignatura, **nunca se trabaja con esclavo real** (un único servidor hace de todo), así que estos campos de replicación son sobre todo "para saber qué significan" de cara al examen, no algo que se vaya a tocar activamente.
- Confirma otra vez (como el 13/10) que el **puerto 53** se usa para las consultas normales por UDP, pero las **transferencias de zona van por TCP** — por eso en el Security Group de AWS hay que abrir el 53 tanto en UDP como en TCP (ver más abajo).

## Repaso de tipos de registro con matices nuevos
Tabla ya vista el 13/10, pero con detalles nuevos añadidos hoy:

| Registro | Novedad/matiz de hoy |
|---|---|
| **A** | Confirma que debajo de cada NS tiene que existir obligatoriamente un registro A con su IP — "si pones el NS de arriba, abajo tiene que estar clavado el A correspondiente". |
| **AAAA** | Es **opcional**; el propio profesor no lo usa porque no ha comprobado si su instancia de AWS tiene IPv6 asignada ("no me he fijado, no sé si lo tengo"). |
| **CNAME** | Ejemplo concreto: si alguien pone `www.despegando23.com`, el CNAME hace que automáticamente se vaya a `despegando23.com` (quitando la `www`) — "un acceso directo" para no repetir toda la zona. |
| **MX** | Ejemplo trabajado con dominio real: `info@dominio` → mira el registro MX → el MX apunta a otro dominio que tiene que tener su propio registro A (si no, no funciona). Caso real del profesor: su dominio tiene el correo gestionado por **Outlook/Microsoft 365** (vía una suscripción con OneDrive), mientras que la web puede estar en otro servidor distinto — "dependiendo de lo que quieras hacer, apuntas cada cosa a un sitio". Varias prioridades posibles (ejemplo citado: 10 y 20); si no contesta la de prioridad más baja, se usa la siguiente. |
| **TXT / SPF** | Para verificación de propiedad (Instagram, Facebook, Google Analytics/Search Console piden un código en TXT) y para reputación de correo (SPF) — formato de ejemplo mencionado: `v=spf1 mx all` (se profundizará al dar el servicio de correo). |
| **NS** | Siempre se exige un mínimo de **2 NS** al configurar DNS personalizados en el registrador (ver sección siguiente); el profesor rellena el segundo con una copia del mismo valor "porque me obligan", aclarando que no es necesario real un segundo servidor distinto. |
| **PTR** | Confirma que el PTR vive en un **fichero de zona inversa aparte** (no en el de la zona directa); se trabajará en el laboratorio de BIND9. |

## Delegar el dominio a un DNS propio (NS personalizados)
Paso conceptual clave de la clase, nuevo respecto al 13/10: cómo pasar de "mi registrador gestiona mi DNS" a "yo gestiono mi propio DNS con BIND9".

1. En el panel del registrador (Namecheap/IONOS) hay una opción de **"DNS personalizados" / "Custom DNS" / "Personal DNS Server"** (según el registrador).
2. Ahí, en vez de dejar los NS que trae el registrador por defecto, se ponen **nombres de servidor propios**, con el patrón `ns1.<tudominio>` y `ns2.<tudominio>` (el registrador obliga a declarar al menos 2 NS).
3. A cada uno de esos NS hay que asignarle una **dirección IPv4** — en el ejemplo del profesor, su propia IP elástica de AWS. Como el formulario exige 2 NS distintos y solo tiene un servidor real, mete la misma IP en ambos (o, si se quiere ser más riguroso, se podría plantear uno como "principal" y el otro como un valor inventado, pero sin usarlo realmente).
4. Al guardar, el cambio puede tardar **hasta 48 h en teoría, pero normalmente se ve de un día para otro** (el profesor lo confirma con el aviso típico del panel).
5. A partir de aquí, cualquier petición a ese dominio que llegue a un servidor raíz termina reenviada al propio servidor del alumno — "porque soy yo el propietario del dominio".

```bash
# Comandos usados en clase para comprobar quién gestiona cada parte de un dominio
host -t soa <dominio>      # servidor DNS primario (SOA) y datos de administración de la zona
host -t ns <dominio>       # (también aceptado como "nameserver") qué NS gestionan el dominio
host -t mx <dominio>       # a qué servidor de correo apunta el dominio
host <dominio>             # resolución directa (registro A)

# Alternativa con dig (da más información, el profesor prefiere host por ser más rápido)
dig <dominio> soa
dig axfr <dominio>         # vuelca la transferencia de zona completa (comando mencionado para entender cómo viaja una transferencia de zona por TCP)

# nslookup es el equivalente universal en Windows (y también funciona en Linux/Mac)
```

Demo en vivo repetida (continuación del ejercicio del 13/10): crear un subdominio nuevo (p. ej. `sol.despegando23.com`, `google.despegando23.com`) con un registro A y comprobar la propagación mundial con **watchmydns.net**, confirmando otra vez que el cambio no es instantáneo.

## Dominio = fichero de texto (idea de cierre de la clase)
Frase resumen del profesor: **"el dominio es un fichero de texto"** y mañana cada alumno va a escribir ese fichero de texto completo con BIND9. Todo lo hecho hoy (delegar el DNS al propio servidor, dejar la IP elástica y el Security Group preparados) es la fase de "quitarle la gestión del DNS al registrador y delegarla en mi propio servidor", para que el día del laboratorio solo quede la parte técnica de instalar y configurar BIND9.

## Preparar AWS antes del laboratorio de BIND9
Pasos realizados en directo por el profesor, a replicar por cada alumno antes del 21/10:

1. **Lanzar una instancia EC2** nueva:
   - Nombre: `SRV-DNS`.
   - Ubuntu 24 (no la 25).
   - Tipo `t3.micro` (instancia pequeña, suficiente).
   - Par de claves: reutilizar el que ya se tenga de prácticas anteriores.
   - Crear un **grupo de seguridad nuevo** para esta instancia (de momento solo con el 22/SSH por defecto).
2. **Crear y asociar una IP elástica**:
   - En "Direcciones IP elásticas" → Asignar dirección IP elástica (la da AWS automáticamente, del pool de Amazon, no se elige).
   - Asociarla a la instancia `SRV-DNS`.
   - Razón: la IP pública dinámica de una instancia **desaparece al detenerla** y cambia al volver a arrancarla; la IP elástica, en cambio, se queda fija aunque se pare y se vuelva a arrancar la máquina — imprescindible para que el DNS no "se pierda" cada vez que se apaga el servidor.
3. **Abrir el puerto 53 en el Security Group**, por **dos protocolos**:
   - `UDP` puerto 53 (origen "Anywhere"/`0.0.0.0/0`) → consultas DNS normales.
   - `TCP` puerto 53 (origen "Anywhere") → por si se monta un esclavo más adelante, ya que las transferencias de zona van por TCP (dejar esto abierto "por si acaso", aunque no se use en la asignatura).
4. Comprobar que el dominio del alumno ya resuelve ese NS personalizado apuntando a la IP elástica recién creada (con `host -t ns <dominio>` y `host -t soa <dominio>`).

```text
Security Group — reglas de entrada añadidas en clase
Tipo: UDP personalizado   Puerto: 53   Origen: Anywhere (0.0.0.0/0)
Tipo: TCP personalizado   Puerto: 53   Origen: Anywhere (0.0.0.0/0)
```

## DNS dinámico (mención breve)
El profesor lo saca como "tercera cosa importante" de la clase, pero avisa de que **no lo recomienda actualmente**:
- Es la idea de usar el propio router de casa como si fuera un servidor DNS ("el DNS de router de andar por casa").
- Servicios tipo **No-IP** permiten que, aunque tu IP doméstica cambie, el dominio se vaya actualizando automáticamente para seguir apuntando a ella.
- El profesor avisa explícitamente de que con los routers actuales de operadoras como Movistar (equipos ZTE) esto da problemas, así que **no lo aconseja para la asignatura** — se usará Elastic IP de AWS en su lugar.

## Logística de dominios (dudas resueltas en clase)
- Varios alumnos (Jaime, María, Roberto...) seguían sin tener dominio comprado el día de la clase; el profesor aclara que **basta con tenerlo comprado para esta clase, aunque no esté listo para el laboratorio de mañana**, porque el dominio gratuito del GitHub Student Pack vale para todo el curso.
- Recordatorio del **GitHub Student Pack** (vía GitHub Education / "GitHub Developer"): incluye, entre otras cosas, un dominio **.me gratis durante un año** vía Namecheap, y (según lo que se ve en pantalla) otro proveedor de dominios ofrece **25 dominios gratuitos** del tipo `.life`, `.studio`, `.software`, `.app`, `.dev`, válidos mientras dure la promoción del Pack.
- Aviso de precio: pasado el año gratuito, renovar un `.me` cuesta del orden de **12–15 €/año**; un `.tech` es bastante más caro (se cita un ejemplo de ~90 $ al comprobarlo en directo) — el profesor avisa de tener cuidado con los TLD caros antes de comprarlos.
- Cada alumno puede usar **cualquier dominio que ya tenga**, de cualquier registrador (Namecheap, IONOS, Dinahosting...): "es tu dominio, haces lo que te dé la gana con él".
- El profesor trabaja en la demo con varios dominios propios distintos (Namecheap, IONOS, Dinahosting) para que se vea que el procedimiento es el mismo independientemente del registrador.

## Logística y fechas
- **Laboratorio de BIND9**: mañana **miércoles 21/10**, de **20:30 a 21:30** (confirmado en clase tras una confusión inicial sobre si era la clase de SAD o el laboratorio de SER — es el laboratorio de SER).
- Antes del laboratorio: ver el **vídeo de instalación de BIND9** ya compartido en Foros → Material complementario de clases (dura ~22 minutos; la parte técnica empieza pasados los primeros minutos, el resto es contexto/historia). El profesor insiste en que si se ve el vídeo, el laboratorio será "mucho copiar y pegar, salvo modificaciones concretas".
- Recomendación práctica: **dejar la instancia de AWS encendida un rato antes** de empezar el laboratorio (de 1 a 1,5 h) para dar tiempo a que la propagación de los NS personalizados ya esté hecha y no haya que esperar durante la clase.
- Repite el resumen de la sesión: hoy se ha dejado todo "delegado" (NS personalizados apuntando al propio servidor, Elastic IP creada y asociada, Security Group con el 53 abierto en UDP y TCP); **todavía no se ha tocado BIND9 en sí** — eso es íntegramente para el 21/10.

## Matices y cosas a revisar
- El número de letras de los root servers se repite otra vez de forma distinta a la clase anterior ("de la A a la G", cuando el 13/10 se dijo "de la A a la N"); sigue sin corregirse en directo — se mantiene como matiz pendiente de las clases anteriores, el profesor parece no tenerlo claro de memoria.
- El formato exacto del campo "admin/hostmaster" del SOA no se explicó con el mismo detalle que el resto de campos — quedó como algo que "se copia y se pega" sin entrar en por qué tiene ese formato.
- No se aclaró del todo si el segundo NS obligatorio del registrador necesita o no ser realmente un servidor distinto fuera del contexto de la asignatura (en clase se rellena con un valor duplicado/inventado solo para poder guardar el formulario).

## Para llevar a casa
- Ver el vídeo de instalación de BIND9 (en Foros → Material complementario) antes del laboratorio del 21/10 si no se ha visto ya.
- Tener el dominio comprado y, si aún no se ha hecho, configurar ya los **NS personalizados** apuntando a una IP (de momento puede ser la IP elástica de AWS que se cree siguiendo esta clase) — recordar que la propagación puede tardar hasta un día.
- Dejar preparada en AWS la instancia `SRV-DNS` (Ubuntu 24) con su **IP elástica asociada** y el **Security Group con el puerto 53 abierto en UDP y TCP** antes del laboratorio.
- Repasar bien los campos del **SOA** (serial, refresh, retry, expire, TTL mínimo) y las 5 columnas del archivo de zona (nombre, TTL, clase, tipo, valor) — es la base necesaria para no perderse en el fichero de BIND9 de mañana.
- Practicar `host -t soa`, `host -t ns` y `host -t mx` sobre el propio dominio y sobre dominios conocidos (ej. un dominio con correo en Gmail/Outlook) para ver cómo encajan SOA, NS y MX entre sí antes de la práctica técnica.
