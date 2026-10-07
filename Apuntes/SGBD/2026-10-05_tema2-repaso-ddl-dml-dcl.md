---
asignatura: Sistemas Gestores de Bases de Datos (SGBD)
fecha: 2026-10-05
tema: Tema 2 · repaso de 1º · DDL, DML y DCL
fuente: apuntes de clase de Dani (lista de sentencias)
---
# SGBD · Tema 2 (05/10) · Repaso de SQL de 1º

Lo anotado en clase (**solo lista; falta desarrollar con ejemplos**):
- **DDL**: `CREATE TABLE`, `CREATE DATABASE`, `USE`, `IF NOT EXISTS`, `ALTER TABLE` (`ADD COLUMN`, `DROP COLUMN`), `TRUNCATE`, `CREATE VIEW`, `ALTER VIEW`, `DROP VIEW`.
- **DML**: `SELECT`, `INSERT` (`INSERT INTO tabla VALUES ...`), `UPDATE` (`UPDATE tabla SET valor ...`), `DELETE` — sintaxis completa.
- **DCL**: `CREATE USER xxx IDENTIFIED BY xxx`, `GRANT xxx ON tabla TO usuario`, `FLUSH PRIVILEGES`, `SHOW GRANTS FOR usuario`, `REVOKE xxx ON tabla FROM usuario`, creación de **roles** para asignarlos a usuarios.
