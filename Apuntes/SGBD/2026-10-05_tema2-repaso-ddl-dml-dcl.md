---
asignatura: Sistemas Gestores de Bases de Datos (SGBD)
fecha: 2026-10-05
tema: Tema 2 · repaso de 1º · DDL, DML y DCL
fuente: apuntes de clase de Dani (lista de sentencias) + transcripción de la clase en directo
---
# SGBD · Tema 2 (05/10) · Repaso de SQL de 1º

> Anterior: [Cierre Tema 1 + inicio Tema 2 (28/09)](2026-09-28_cierre-tema1-cajon-inicio-tema2.md)

Lo anotado en clase (**solo lista; falta desarrollar con ejemplos**):
- **DDL**: `CREATE TABLE`, `CREATE DATABASE`, `USE`, `IF NOT EXISTS`, `ALTER TABLE` (`ADD COLUMN`, `DROP COLUMN`), `TRUNCATE`, `CREATE VIEW`, `ALTER VIEW`, `DROP VIEW`.
- **DML**: `SELECT`, `INSERT` (`INSERT INTO tabla VALUES ...`), `UPDATE` (`UPDATE tabla SET valor ...`), `DELETE` — sintaxis completa.
- **DCL**: `CREATE USER xxx IDENTIFIED BY xxx`, `GRANT xxx ON tabla TO usuario`, `FLUSH PRIVILEGES`, `SHOW GRANTS FOR usuario`, `REVOKE xxx ON tabla FROM usuario`, creación de **roles** para asignarlos a usuarios.

## Notas en directo (matices del profesor, no están en la lista escrita)

### Lo que realmente pide el examen sobre estos comandos
César fue explícito: **en mayo no se pide escribir de memoria la sentencia exacta** (crear una base de datos, asignar permisos, etc.) — al revés: la pregunta sería del tipo "¿cuáles son los principales comandos de DDL y qué hace cada uno?", respondida con las propias palabras. Razón que dio: hoy en día cualquiera puede pedirle la sentencia exacta a una IA (Claude, GPT, Copilot...) — lo que hay que saber es **qué existe y para qué sirve**, para poder detectar cuándo la IA "alucina" y se le olvida un comando.

### DDL: create/alter/drop/truncate — sobre **contenedores**
Remarcado como la idea clave del lenguaje DDL: actúa sobre **contenedores** (espacios donde se guarda información), no sobre los datos en sí. Contenedores = bases de datos, tablas **y también vistas** (una vista no almacena datos propios, es un contenedor de columnas de otras tablas — por eso `CREATE VIEW`/`ALTER VIEW`/`DROP VIEW` son DDL).
- `CREATE` — crear un contenedor nuevo.
- `ALTER` — modificar un contenedor que ya existe (añadir/renombrar columna, cambiar tipo de dato).
- `DROP` — eliminar el contenedor.
- `TRUNCATE` — vaciar completamente el contenido de una tabla **y reiniciar el contador del autoincremental** a 1. Diferencia importante frente a `DELETE`: un `DELETE` borra las filas pero el contador de autoincremental sigue por donde iba (si se borran los primeros 500 registros de prueba, el siguiente insertado sería el 501, no el 1). `TRUNCATE` es la herramienta correcta para limpiar datos de desarrollo/pruebas antes de pasar a producción, o para reiniciar una tabla de ventas/facturas al cambiar de año (tras mover los datos del año anterior a una tabla histórica).

### `IF NOT EXISTS`: por qué es crítico en scripts y triggers
Punto remarcado especialmente porque conecta con el Tema 3 (triggers): un script o trigger que se lanza automáticamente sin supervisión (p. ej. a medianoche) **no puede abortar** si una condición previa no se cumple — por eso hay que añadir control de errores:
```sql
CREATE DATABASE IF NOT EXISTS manolo;   -- no da error aunque la BD ya exista
CREATE DATABASE manolo;                 -- SIN el IF NOT EXISTS: error si ya existe
```
Demostrado en directo en DBeaver: sin `IF NOT EXISTS` el sistema lanza un error ("ya existe") y el script se detendría; con `IF NOT EXISTS` simplemente no hace nada si ya existe, y el proceso continúa sin interrumpirse — imprescindible para que un trigger o procedimiento automático siga adelante.

### Export/import de una base de datos como fichero `.sql`
Demostración práctica: desde el cliente (phpMyAdmin/DBeaver) se puede **exportar** una base de datos completa a un fichero `.sql`, que resulta ser literalmente un listado secuencial de sentencias `CREATE` (estructura de tablas) seguido de `INSERT` (volcado de todos los datos fila a fila) y `ALTER` (claves primarias, índices). Importar ese mismo fichero en otro sistema relanza todas esas sentencias y reconstruye la base de datos entera — es, en la práctica, la forma más simple de hacer una copia de seguridad/migración completa de una base de datos.

### DML en profundidad: INSERT, UPDATE (con sus riesgos reales) y DELETE
- **INSERT**: además de un insert de una fila, puede ser un **insert masivo** de varias filas en una sola sentencia (tal y como aparecen generados los `.sql` de volcado): una lista de valores separados por comas, una tupla por fila.
- **UPDATE — herramienta "delicada"**: ejemplo extenso usado en clase, subida de precios de un 5% a toda la tabla de productos (`UPDATE productos SET precio = precio * 1.05`). Riesgos reales señalados:
  - Si el jefe luego dice que el porcentaje era otro, hay que poder revertir — por eso antes de un `UPDATE` masivo es buena práctica volcar los datos a una **tabla temporal** o llevar un **historial de precios**, de forma que el cambio sea reversible.
  - Riesgo de diseño más grave: si las facturas antiguas **no guardan el precio del producto en el momento de la venta**, sino que solo enlazan al ID de producto y consultan el precio actual, un `UPDATE` de precio **cambia retroactivamente el importe de todas las facturas ya emitidas** — error de diseño real que el profesor remarcó como "problemón".
- **DELETE — el comando "menos inocuo"**: recomendación explícita de no borrar directamente en muchos casos, sino usar un campo tipo `activo`/`inactivo` para desactivar en lugar de eliminar (evita el "efecto dominó" de borrar un cliente y arrastrar en cascada sus facturas relacionadas). Cuando sí se borra, es buena práctica tener un trigger que copie el registro eliminado a una tabla histórica antes del borrado.

### DCL en profundidad: usuarios, GRANT/REVOKE y roles
- Habilitar el superadministrador en SQL Server (ya visto en la tutoría del 25/09): `ALTER LOGIN sa ENABLE; ALTER LOGIN sa WITH PASSWORD = '...';`
- Crear usuario nuevo con permisos limitados (no dar el usuario `sa`/root a nadie salvo necesidad real):
  ```sql
  CREATE USER usuario IDENTIFIED BY 'contraseña';
  GRANT SELECT ON basededatos.tabla TO usuario;        -- solo lectura
  GRANT SELECT, INSERT, UPDATE ON basededatos.* TO usuario;
  REVOKE ALL PRIVILEGES ON basededatos.* FROM usuario;  -- quitar todo
  SHOW GRANTS FOR usuario;                               -- ver permisos actuales
  FLUSH PRIVILEGES;                                      -- aplicar los cambios
  ```
- Ejemplos de permisos según el tipo de aplicación: una app que solo muestra información necesita solo `SELECT`; una que permite "añadir al carrito" necesita `INSERT`; una que gestiona stock necesita `UPDATE`; una que elimina necesita `DELETE`. Recomendación: dar siempre el mínimo permiso necesario.
- **Roles vs. asignación directa**: la forma correcta de trabajar no es dar permisos usuario por usuario, sino crear un **rol** (p. ej. `administradores`) con los permisos definidos, y luego asignar usuarios a ese rol: `ALTER USER ana SET ROLE administradores;` — así se gestionan permisos de forma centralizada.
- Aclaración sobre la nomenclatura `usuario@localhost` en MariaDB: `localhost` es el **nombre del servidor** donde vive la base de datos, no un valor fijo — en producción sería la IP o el nombre real del host, no siempre "localhost". La tabla `mysql.user` es la tabla donde el propio motor MariaDB centraliza la gestión de todos los usuarios de todas sus bases de datos.
- Diferencia entre `AUTO_INCREMENT` (MariaDB/MySQL) e `IDENTITY(1,1)` (SQL Server Express) para claves autoincrementales — SQL Server no reconoce el comando `AUTO_INCREMENT`.

### Cierre del Tema 2: protección de datos (LOPD/RGPD y LSSI)
El tema 2 termina con una introducción a la legislación de protección de datos — contenido que se repetirá más adelante en un tema específico, así que aquí quedó solo como primera toma de contacto:
- **RGPD / LOPDGDD** (la ley española deriva del reglamento europeo): obliga a cuidar cómo se almacenan los datos sensibles — p. ej. cualquier comunicación por email debe incluir opción de darse de baja de la newsletter.
- **LSSI** (Ley de Servicios de la Sociedad de la Información): complementa a la LOPD — regula la información mínima que una web/servicio debe ofrecer al usuario (avisos de cookies, condiciones de uso, etc.).
- El profesor remarcó que, como administradores de sistemas, **seréis vosotros quienes respondáis ante una auditoría de calidad** sobre cómo se hacen las copias de seguridad, dónde se guardan los datos y quién tiene acceso — y aconsejó, con humor, responder a los auditores "lo justo y necesario", porque cuanta más información se da, más preguntas y tareas adicionales genera la auditoría.
- Anécdota personal del profesor (sin verificar, mencionada como ejemplo de actualidad, no como hecho confirmado en clase): dijo haber recibido un intento de phishing con datos reales de una reserva de hotel, que atribuyó a una filtración de datos de Booking ocurrida esos días — usada para ilustrar que los datos robados se usan para suplantación y fraude, y que al estar Reino Unido fuera de la UE no aplicaría directamente el RGPD. **Queda como anécdota del profesor, no como hecho verificado por esta nota.**

### Deberes / cierre
Viernes 09/10 (tutoría): reinstalación en directo de los motores y prácticas de creación/modificación de bases de datos, inserts, etc. El mínimo válido para seguir la práctica sin instalar nada adicional es XAMPP + phpMyAdmin.
