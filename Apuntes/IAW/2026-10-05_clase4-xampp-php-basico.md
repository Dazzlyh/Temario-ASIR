---
asignatura: Implantación de Aplicaciones Web (IAW)
fecha: 2026-10-05
tema: Tema 2 · instalación de XAMPP, Apache, PHP incrustado en HTML y variables de servidor
fuente: transcripción de la clase en directo
---
# IAW · Clase 4 (05/10) · Instalación de XAMPP y PHP básico

> Anterior: [Clase 3 (28/09): modelo vista-controlador y Actividad 1](2026-09-28_clase3-mvc-actividad1.md)

Clase práctica de instalación del entorno de desarrollo (XAMPP) y primer contacto con PHP incrustado en HTML.

## Logística y avisos de curso
- Confirmado por una alumna (María Eugenia, encargada de coordinar fechas con otros módulos para evitar solapes): la actividad del tercer trimestre de IAW se moverá al **1 de marzo**, para no coincidir con otra actividad del mismo periodo. El profesor lo aceptó directamente.
- Las **FCT (prácticas de empresa) pasan de 300 a 500 horas** este curso respecto a años anteriores.
- Dudas aclaradas sobre la Actividad 1 (ver nota de la clase anterior): se resuelve directamente sobre el enunciado (en los corchetes o quitándolos), **no es necesario redactarla como informe técnico**.
- Recordatorio: el profesor es tutor de prácticas de al menos una alumna (Esther) presente en clase.
- **Próximo lunes no hay clase de IAW** (festivo).
- Aprovechar los cursos de **AWS Academy** dados en otro módulo (impartido por Damián) para profundizar en despliegue real en la nube — el profesor advirtió que si alguien monta su proyecto de WordPress directamente con Docker en AWS en el TFC, "genial"; pero que no montarlo así no penaliza, él solo exige la base de XAMPP/Apache+PHP+BBDD.

## Repaso rápido del Tema 1 antes de empezar
MVC: controlador ↔ modelo (acceso a base de datos) ↔ vista. Puertos clave: 80 (HTTP) y 443 (HTTPS). Esta clase introduce las tecnologías concretas: Apache, PHP, MariaDB/MySQL.

## Qué hace un servidor web: Apache
- Apache **solo sirve contenido estático por sí solo**: recibe peticiones y devuelve HTML. No genera contenido dinámico él solo (eso lo da JavaScript en el cliente, o PHP en el servidor combinándose con la base de datos).
- Mención de **Nginx** como alternativa cada vez más usada en el mundo empresarial por ser más potente para gestionar muchas conexiones, aunque el módulo trabajará con Apache por ser el más extendido en entornos educativos.
- Fichero de configuración principal de Apache: `httpd.conf` (dentro del menú "Config" del panel de XAMPP) — determina módulos cargados, puertos e IPs que escucha. El profesor mostró que todo lo que empieza por `#` está comentado/desactivado; lo que no, está activo.
- Aviso práctico sobre hosting compartido: el tamaño máximo de fichero subido por HTTP suele venir limitado (el profesor mencionó un valor por defecto de referencia en torno a los 40 MB, pero un hosting típico de pago lo reduce a 2-3 MB), lo que da problemas al subir plantillas pesadas de WordPress — hay que pedir al proveedor que cambie ese límite si es necesario.
- `php.ini` es el fichero que normalmente hay que tocar en un hosting real (más que `httpd.conf`), según el profesor.

## Instalación de XAMPP (en directo, con incidentes)
- El profesor tuvo que reinstalar XAMPP en directo porque se le rompió la máquina virtual preparada previamente — ejemplo real de por qué **conviene tener clonada una copia limpia** de la máquina virtual antes de empezar a trastear (mismo consejo dado en ASO).
- Aviso de instalación en Windows: puede dar un error relacionado con el **Control de Cuentas de Usuario (UAC)**; hay que desactivarlo si da problemas.
- Carpeta clave: **`htdocs`** — todos los proyectos y webs del XAMPP se guardan ahí. El profesor insistió en prestar atención a dónde se instala XAMPP en el disco para no perder la referencia a esta carpeta.
- Al entrar a `localhost` o `127.0.0.1` sin servidor arrancado, el navegador no devuelve nada; una vez arrancado Apache en el panel de XAMPP, carga automáticamente el `index` de `htdocs` (que redirige al dashboard de XAMPP).
- Nota histórica (anécdota del profesor, sin relevancia para el examen): antiguamente Skype ocupaba el puerto 80, lo que generaba conflicto al levantar Apache; había que cerrar Skype para poder arrancar el servidor web.

## PHP incrustado en HTML
Primer ejemplo mostrado en clase, usando variables de servidor:
```php
<?php
echo $_SERVER['SERVER_NAME'];
echo $_SERVER['DOCUMENT_ROOT'];
echo $_SERVER['SERVER_SOFTWARE'];
?>
```
Puntos clave remarcados por el profesor:
- Las etiquetas `<?php ... ?>` delimitan el código PHP incrustado dentro de un documento que, por lo demás, sigue siendo HTML normal.
- **Lo que el servidor Apache manda finalmente al navegador es HTML puro** — nunca se envía el código PHP en sí; Apache lo transforma/ejecuta en el servidor y "escupe" el resultado ya convertido en HTML plano.
- Esto se puede comprobar con F12 → ver código fuente: nunca aparecerá código PHP, solo el HTML resultante.
- **Aviso importante de examen/práctica**: si el fichero se guarda con extensión `.html` en lugar de `.php`, el código PHP **no se ejecuta** y se muestra literalmente como texto — hay que guardar el fichero con extensión `.php` para que Apache lo procese.
- Framework de PHP mencionado: **Laravel** (el más usado hoy); Symfony mencionado como alternativa menos extendida actualmente.

## Tarea para las próximas 2 semanas (sin clase la semana que viene)
1. **Obligatorio**: instalar XAMPP (o equivalente), levantar Apache y PHP sin conflictos de puerto, crear un fichero PHP con las variables de servidor (`$_SERVER[...]`) de ejemplo visto en clase, comprobar que funciona en `localhost`/`127.0.0.1`, y verificar con F12 que lo que llega al navegador es HTML limpio sin rastro de PHP.
2. **Optativo** (adelanto de la futura Actividad 2, de nivel más avanzado): crear una base de datos sencilla en phpMyAdmin (MariaDB/MySQL) con una tabla de ejemplo (alumnos, profesores...) e intentar recuperar un dato desde PHP y mostrarlo sin estilos, a pelo (ejemplo dado: mostrar "nombre: Sol, apellido: Micaela" extraído de la base de datos).

## Cierre
Confirmado que esto será la base de la futura **Actividad 2** (más avanzada que la 1, centrada en MVC real con PHP + base de datos). El profesor subirá la presentación de esta clase a la plataforma.
