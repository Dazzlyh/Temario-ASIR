---
asignatura: Sistemas Gestores de Bases de Datos (SGBD)
fecha: 2026-09-25
tema: "Tutoría (viernes) · instalación práctica de SQL Server Express, MariaDB (XAMPP) y Oracle, y su conexión unificada en DBeaver"
fuente: transcripción de la clase en directo (tutoría)
---
# SGBD · Tutoría (25/09) · Instalación de los 3 motores y DBeaver

> Anterior: [Tema 1: relacional, ANSI/SPARC y el rol del DBA](2026-09-21_tema1-conceptos-relacional-ansi-sparc.md) · Siguiente: [Cierre Tema 1 + inicio Tema 2 (28/09)](2026-09-28_cierre-tema1-cajon-inicio-tema2.md)

Tutoría de viernes (no se da contenido nuevo de examen en tutorías, son refuerzo práctico). César desinstaló y reinstaló todo su equipo en directo para documentar paso a paso la instalación de **SQL Server Express, MariaDB (vía XAMPP) y Oracle**, y su conexión unificada desde **DBeaver**. Subió además un PDF con capturas de pantalla de todo el proceso. Explícito: esto **no entra en el examen**, es una actividad complementaria recomendada para tener los 3 motores operativos antes de las prácticas.

## Postura del profesor sobre la herramienta
Insistencia repetida: **no importa con qué herramienta cliente se haga cada cosa** (SSMS, phpMyAdmin, DBeaver, modo comando) — lo que importa es entender el concepto y la instrucción DDL/DML/DCL que corresponde. El examen no pide "instalar algo", sino explicar con las propias palabras un concepto (qué es un script, un trigger, cómo se crea una base de datos).

## Puertos por defecto de cada motor (dato concreto, útil de memorizar)
| Motor | Puerto por defecto |
|---|---|
| SQL Server Express | 1433 |
| Oracle (listener) | 1521 |
| MariaDB/MySQL (XAMPP) | 3306 |
| Apache (HTTP / HTTPS) | 80 / 443 |

Explicación del concepto de puerto dada en clase (analogía): un ordenador es como un estadio de fútbol con miles de puertas (puertos); cada servicio (FTP=21, SSH, correo entrante POP=110, HTTPS=443, etc.) tiene su propia puerta. Un puerto abierto es el punto de entrada más sencillo para un ataque.

## SQL Server Express: pasos reales de instalación
- Tipo de instalación: **básica** (sin complicarse).
- Tras instalar, pide instalar también **SQL Server Management Studio (SSMS)** desde el propio instalador.
- Clave: el **SQL Server Configuration Manager** — ahí se habilita el protocolo **TCP/IP** (viene deshabilitado por defecto) para permitir conexiones externas (p. ej. desde DBeaver). Doble clic → habilitar → en la ventana de propiedades se puede fijar el puerto manualmente (por defecto 1433, se puede cambiar, p. ej. a 8312, sin problema — lo importante es ser consistente con el puerto que luego se use en DBeaver).
- Desde el mismo Configuration Manager se **para/arranca** el servicio (botón derecho → reiniciar/detener). **Importante**: si se intenta hacer una copia de seguridad con el servidor en marcha, la copia puede salir corrupta porque el sistema puede estar insertando/leyendo/borrando datos en ese momento — herramientas de backup externas (tipo Veeam) necesitan parar el servicio, hacer la copia y volver a arrancarlo.
- **Autenticación**: por defecto, "Windows Authentication" (valida con el login del propio sistema). Para poder conectar con usuario/contraseña propios de SQL (más realista en producción), hay que **habilitar el usuario `sa`** (superadministrador, viene deshabilitado) y asignarle contraseña:
  ```sql
  ALTER LOGIN sa ENABLE;
  ALTER LOGIN sa WITH PASSWORD = 'contraseña';
  ```
  Después, en DBeaver, el tipo de conexión cambia de "Windows Authentication" a "SQL Server Authentication", usando `sa` + la contraseña creada.
- Cada vez que se añade un nuevo cliente de conexión (p. ej. instalar SSMS después de DBeaver), hay que volver al Configuration Manager y **reiniciar el servicio** para que reconozca al nuevo cliente.

## MariaDB vía XAMPP (Sam)
- XAMPP trae Apache (servidor web) + MariaDB/MySQL + **phpMyAdmin** como cliente de administración por defecto.
- Puerto 3306. Hay que tener el servicio de MySQL arrancado en el panel de XAMPP para poder conectar (si no está en marcha, ni phpMyAdmin ni DBeaver pueden acceder).
- Conexión desde DBeaver: elegir MariaDB, indicar servidor y puerto 3306; DBeaver descarga su propio driver de conexión si no lo tiene.

## Oracle (versión gratuita Database Free, "23ai")
- Descarga desde `oracle.com/database/free`.
- Al instalar, pide definir contraseña para las cuentas **`system`** y **`sys`** (apuntarla, es fácil perderla).
- Por defecto arranca un servicio **Listener** escuchando en el puerto **1521**; base de datos por defecto: **`FREEPDB1`**.
- Comprobación desde `cmd` con `lsnrctl status` (verifica que el listener está activo y en qué puerto).
- **Problema real que ocurrió en directo**: el fichero `listener.ora` (dentro de la ruta de instalación) puede quedar apuntando a una IP de red tipo `10.x.x.x` en vez de `localhost`/`127.0.0.1`, lo que impide conectar desde DBeaver. Solución: editar `listener.ora` con el bloc de notas, cambiar esa IP por `127.0.0.1` o `localhost`, y relanzar el servicio con:
  ```
  lsnrctl stop
  lsnrctl start
  ```
- Conexión en DBeaver: conector Oracle, `localhost`, puerto 1521, base de datos `FREEPDB1`, usuario/contraseña creados en la instalación.

## DBeaver: detalles prácticos
- Necesita descargar un **driver** distinto para cada motor (SQL Server, MariaDB, Oracle) la primera vez que se conecta a cada uno — acepta la descarga cuando lo pide.
- Se pueden **renombrar las conexiones** (botón derecho → redenominar) para identificarlas visualmente mejor (p. ej. llamar "Caracol" a la conexión de Oracle) — es solo cosmético, no afecta al funcionamiento.
- Con las 3 conexiones activas, DBeaver muestra Oracle, MariaDB y SQL Server **en el mismo árbol lateral**, confirmando la idea central del curso: un único cliente para administrar todos los sistemas de gestión.

## Deberes / cierre
No entregable. Practicar la instalación de los 3 motores durante el fin de semana con el PDF subido. El lunes se lanzaría un cajón de repaso del Tema 1 antes de arrancar el Tema 2.
