---
asignatura: Implantación de Aplicaciones Web (IAW)
fecha: 2026-09-28
tema: Tema 1 (cierre) · modelo vista-controlador, puertos, F12 en detalle + Actividad 1
fuente: transcripción de la clase en directo
---
# IAW · Clase 3 (28/09) · Modelo vista-controlador y Actividad 1

> Anterior: [Clase 2 (21/09): arquitecturas web y cliente-servidor](2026-09-21_clase2-arquitecturas-cliente-servidor.md) · Siguiente: [Clase 4 (05/10): instalación de XAMPP y PHP básico](2026-10-05_clase4-xampp-php-basico.md)

Clase dedicada a cerrar el Tema 1 (repaso de arquitectura de 2/3 niveles y modelo vista-controlador) y a explicar la **Actividad 1**.

## Repaso: arquitectura de 2 y 3 niveles
- 2 niveles = cliente-servidor; el servidor recibe HTTP/HTTPS, aplica la lógica y responde con contenido "listo para presentar" (HTML, JSON...).
- 3 niveles = se separa la lógica del negocio (acceso a datos) de la lógica de presentación (lo que habla con el cliente). Ejemplo trabajado con la app del banco: el cliente nunca consulta la base de datos directamente, siempre hay un servidor de aplicaciones intermedio.

## Modelo vista-controlador (MVC), explicado con 2 ejemplos
El profesor usó dos diagramas distintos para explicar el mismo flujo, porque "a veces se enreda, se enreda en las clases":
1. El **controlador** recibe la petición del navegador (p. ej. un login).
2. El controlador pide al **modelo** que consulte/valide contra la base de datos.
3. El modelo devuelve el resultado al controlador.
4. El controlador decide qué **vista** generar (pantalla de bienvenida si todo OK, o mensaje de error).

> *"El controlador recibe la petición HTTP y pide la validación, el modelo consulta y es el encargado de consultar la base de datos y validar al usuario; en el momento en que ya le tenemos validado, la vista genera la pantalla de bienvenida."*

## Protocolos y puertos (teoría del tema, posible pregunta de test)
El profesor remarcó que **casi con seguridad habrá una pregunta de test sobre puertos** de este tema (como pasó el año pasado). Puertos a conocer por ahora (se irán ampliando tema a tema, no de golpe):
- HTTP / HTTPS
- FTP / FTPS
- Puerto 53 (DNS, mencionado de pasada con el ejemplo del eMule)

## Actividad 1: detalles de entrega
- **Fecha de entrega: 12 de octubre, 23:59** — aviso importante: el 12 de octubre es festivo, y el profesor pidió explícitamente no dejarlo para el último minuto, porque con tantos alumnos entregando a la vez en la UNIR el servidor puede saturarse ("se monta el cristo, no funciona, se cae Canvas y no lo puedo entregar").
- Entrega **fuera de plazo = un 0**, sin excepciones ("un minuto tarde es fuera de tiempo; a mí me sale en rojo fuera de tiempo, ni le leo el trabajo").
- Formato de entrega: **solo PDF** (el profesor dijo explícitamente que no tiene instalado Word ni LibreOffice en su ordenador de trabajo, solo Adobe Reader gratuito — un DOCX se corrige con un 0).
- Actividad **individual**.
- Vale **3 de los 15 puntos** totales de evaluación continua de la asignatura.
- Contenido de la actividad (muy sencilla, pensada para que "sea un regalo" de nota):
  1. Comparativa de arquitectura (matriz: aplicación de escritorio vs aplicación web, dónde se ejecuta cada cosa) + justificación.
  2. Caso práctico de un departamento de diseño gráfico — síntesis obligatoria en 50 palabras máximo (límite puesto deliberadamente para evitar respuestas generadas sin criterio con IA: *"si me lo hacéis con IA en 50 palabras os pasáis; por favor, síntesis, porque las IAs no hacen esa síntesis"*).
  3. Mapeo de la arquitectura MVC sobre un caso de registro/login de usuario: qué tecnología y qué función hace cada capa (presentación, lógica, negocio) tanto en el registro como en el login. Confirmado en clase que se puede mencionar un framework concreto si se conoce, sin que sea obligatorio.
  4. Flujo de ejecución del patrón MVC sobre el mismo caso.

## Puertos y herramientas en la práctica (consola)
- Windows: `netstat` (el profesor lo mencionó de forma indirecta, confirmando que la pregunta de un alumno sobre Linux era correcta).
- Linux: comando para ver puertos abiertos, forma general usada en clase:
```
ss -tuln
```
- Mención de una web para comprobar puertos públicos (no mostrada en pantalla por motivos de privacidad — exponía la IP pública del profesor); el profesor remarcó que hacerlo desde consola es más seguro que desde una web de terceros.

## Ejercicio práctico: F12 / Network con una web de pedir pizza
Se hizo en directo con una web de ejemplo de pedir una pizza, para ver cómo se monta una petición `POST`:
- Pestaña **Network** del navegador, con la caché desactivada para ver todas las peticiones.
- Identificación del **payload** de la petición POST (los datos del formulario: tamaño de pizza, ingredientes, hora).
- Códigos de estado HTTP (mención rápida, no entra en el examen según el profesor, pero importante entenderlos):
  - 100-199: informativos
  - 200-299: éxito
  - 300-399: redirección
  - 400-499: errores de cliente
  - 500-599: errores de servidor
- Visualización de cabeceras y del HTML generado por el servidor tras la petición.
- Comparación con una web más compleja (la propia web de la UNIR, la de grados): muchas más peticiones, carga progresiva de contenido (imágenes, scripts) a medida que se hace scroll, en vez de cargar todo de golpe — explicado como buena práctica de rendimiento web (un periódico "no puede cargar toda la web de golpe, porque la haría lentísima").
- **Ver código fuente** de una web antigua (ejemplo: la primera web de la historia, mantenida igual desde su creación) frente a una web moderna ofuscada/minificada (ejemplo: la propia web de la UNIR), explicando el concepto de **ofuscación** de código para que no se pueda copiar fácilmente con "botón derecho → copiar".

## Cierre del Tema 1
El profesor dio el Tema 1 por cerrado tras esta clase. Próxima sesión: instalación práctica del entorno (XAMPP/WAMP) y primeras pruebas con PHP.
