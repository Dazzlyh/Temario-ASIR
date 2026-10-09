---
asignatura: Implantación de Aplicaciones Web (IAW)
fecha: 2026-09-21
tema: Tema 1 · aplicaciones de escritorio vs web, cliente-servidor, seguridad y roles de desarrollo
fuente: transcripción de la clase en directo
---
# IAW · Clase 2 (21/09) · Arquitecturas web y cliente-servidor

> Anterior: [Clase 1 (14/09): presentación del módulo](2026-09-14_clase1-presentacion.md) · Siguiente: [Clase 3 (28/09): modelo vista-controlador y actividad 1](2026-09-28_clase3-mvc-actividad1.md)

Primera clase de contenido real del Tema 1 (arquitectura de aplicaciones web). El profesor avisó de que la tutoría de los miércoles se movía este trimestre a **3 a 4 de la tarde** (antes 9:30-10:30), a modo de prueba — si no funciona bien, se puede volver al horario anterior el segundo trimestre. Las tutorías colectivas se grabarán.

## Aplicaciones de escritorio vs aplicaciones web
- **Escritorio**: acceso directo al hardware (CPU) de la máquina; instalación local; rendimiento depende del propio ordenador.
- **Web**: el hardware real queda oculto detrás del navegador — depende de dónde esté alojada la aplicación y de sus recursos (ejemplo puesto en clase: un "Windows" montado dentro del navegador el año anterior, cuyo rendimiento dependía del servidor donde estaba alojado, no del PC del usuario).
- Estándar de la web: HTML, CSS y JavaScript (con frameworks por encima del JS "puro").

### Ventajas/inconvenientes de la web frente al escritorio
- **A favor**: compatibilidad teóricamente universal (con matices: hay diferencias de un navegador/motor a otro, p. ej. casos históricos con Internet Explorer y trámites que solo funcionaban en ese navegador), mantenimiento unificado (se actualiza una vez en el servidor y afecta a todos los usuarios sin tener que tocar equipo por equipo).
- **En contra**: dependencia de Internet (anécdota del profesor sobre caídas de internet y de servicios de IA durante los simulacros del curso anterior — "la gente llorando porque no podía hacer el examen porque no funcionaba la IA"), coste de infraestructura (hay que pensar en quién va a usar la aplicación y con qué presupuesto: "no me da lo mismo morir de éxito que morir por descalabro"), y privacidad delegada (cuando los datos de una empresa viven en un proveedor extranjero, la legalidad aplicable es la de ese país; aviso sobre fugas de información por vibe coding sin saber qué se está exponiendo — ejemplo mencionado: gente que ha subido ficheros `.env` con contraseñas a repositorios por pedirle todo a la IA sin entender qué hace).

## Arquitectura cliente-servidor (2 niveles)
- **Cliente**: navegador (distinto de un buscador), interfaz de usuario. Envía peticiones HTTP/HTTPS.
- **Servidor**: recibe la petición, aplica la lógica de negocio y devuelve una respuesta (HTML, JSON...).
- Ejemplo trabajado en clase: login en la app del banco — el cliente envía las credenciales (huella, usuario/contraseña), el servidor valida contra la base de datos y devuelve una interfaz distinta para cada usuario (su saldo, sus cuentas).

## Capas de red / inconvenientes de separar cliente y servidor
Ventajas de separar responsabilidades: aislamiento de fallos, cambios independientes en cliente y servidor sin tocar producción entera, escalabilidad (se puede levantar otro contenedor/servidor). Mención de **Podman** como alternativa a Docker que está ganando adeptos por no depender de un demonio central (y por la desconfianza tras que Docker pasara a ser de pago en ciertos usos). Inconvenientes: latencia de red, dependencia de la conexión entre ambas máquinas, gestión de sesiones (cookies).

## Arquitectura de 3 niveles
Se separa el servidor en dos capas:
- **Capa de lógica / controlador**: habla con el cliente, nunca con la base de datos directamente.
- **Capa de negocio / modelo**: accede a los datos de forma segura.

Regla remarcada como fundamental por el profesor: *"el cliente nunca debe tratar directamente con la base de datos. Nunca. Eso grabadlo a fuego."* El usuario no puede estar lanzando consultas SQL directamente contra la base de datos; siempre tiene que pasar por la capa de lógica.

## Roles de desarrollo: frontend vs backend
- **Frontend**: diseño gráfico, interfaces de usuario (HTML, CSS, JS).
- **Backend**: lógica de negocio, bases de datos, seguridad, rendimiento.
- El profesor comentó que, históricamente, estos roles estaban muy separados, pero con la IA cada vez se pide más que una sola persona cubra ambas partes. Debate en clase sobre si siguen existiendo ofertas de trabajo solo de frontend (un alumno, que trabaja en el sector, confirmó que sí existen en su empresa, sobre todo en sectores como la salud donde el frontend tiene mucho peso por la experiencia de usuario).

## Seguridad y sesiones (mención, no examinable en detalle)
- Comunicaciones deben ir **cifradas** (corrección del profesor sobre el término: "cifrado", no "encriptado").
- Gestión de sesión: cookies, tokens. Mención de **JWT**, usado el año pasado por prácticamente todos los grupos en sus TFC — el profesor valora que se busquen alternativas más originales para innovar, y advirtió de una limitación real de JWT (comentada por un alumno): si se manda en texto plano se puede inspeccionar y robar fácilmente desde las herramientas de red del navegador.
- Doble factor de autenticación (2FA) mencionado como buena práctica cada vez más extendida.

## Herramienta clave para todo el curso: F12 (herramientas de desarrollador)
El profesor insistió en que todo el alumnado debe saber al menos **abrir y leer** las herramientas de desarrollador del navegador (F12), especialmente la pestaña **Network**, para ver las peticiones que hace una página web. Lo plantea como ejercicio de esta semana: entrar con F12 en cualquier periódico (ABC, Marca, El Mundo...) y comprobar cómo se puede modificar una noticia en el DOM sin que eso cambie nada en el servidor real.

## Cierre
Próxima clase: se cerrará el Tema 1 con el **modelo vista-controlador (MVC)** y se trabajará de forma más práctica, con ejercicios. Se recomendó leer el tema del MVC antes de la siguiente sesión.
