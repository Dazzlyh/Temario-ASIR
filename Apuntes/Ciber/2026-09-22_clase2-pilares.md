---
asignatura: Ciberseguridad
fecha: 2026-09-22
tema: Tema 1 (1.1 y 1.2) · Clase 2 · los cuatro pilares desde el atacante
fuente: CIBER_Clase02_diapositivas.pdf
---
# Ciber · Clase 2 (22/09) · Pautas de seguridad

> Anterior: — · Siguiente: [Lab 1](2026-09-24_lab1-paseo-por-kali.md) · Práctica asociada: [Práctica 1](2026-09-22_practica1-tres-demostraciones.md)

## Qué se vio
1. Qué se protege: los **cuatro pilares** del material.
2. Cómo lo mira un atacante: qué pilar rompe cada ataque y cómo se demuestra.
3. Tres demostraciones en directo (confidencialidad, integridad, disponibilidad).

La Actividad 1 pide, por cada apartado, **evidencia**: hoy se aprende qué cuenta como evidencia.

> «El defensor tiene que acertar siempre. Al atacante le basta con acertar una vez.»

## Los cuatro pilares (según el material de la asignatura)
| Pilar | Significado |
|---|---|
| **Fiable** | Que funcione sin fallos el tiempo que tiene que durar |
| **Confidencial** | Que solo lo vea quien debe verlo, en reposo y en tránsito |
| **Íntegro** | Que nadie lo cambie sin que se note, ni siquiera por error |
| **Disponible** | Que esté ahí cuando hace falta, aunque te ataquen |

- OJO con la palabra: en otros libros «pilares» = hardware, software y datos. Aquí son estas cuatro propiedades.
- **La fiabilidad NO es lo mismo que la disponibilidad: es la «pregunta trampa» del examen** (lo dice la diapositiva).

## Cómo se rompe cada pilar y cómo se demuestra
| Pilar | Cómo lo rompe un atacante | Cómo se demuestra |
|---|---|---|
| Fiabilidad | Un proceso que se come la memoria y lo tumba a ratos | Registros del sistema y alertas de recursos |
| Confidencialidad | Escuchar tráfico sin cifrar o llevarse una copia | El dato aparece donde no debía: una captura |
| Integridad | Cambiar un fichero sin cambiar su tamaño | El hash ya no coincide |
| Disponibilidad | Saturar el servicio o cifrarle los datos | No responde, y queda en el registro |

Un auditor no dice «esto es inseguro»; dice **«esto se rompe así, y aquí está la prueba»**. Esa frase es la Actividad 1 entera.

## Las dos que se olvidan (no están en los cuatro pilares)
- **Autenticidad**: que quien dice ser el origen lo sea de verdad. Es lo que ataca la suplantación.
- **No repudio**: que quien hizo algo no pueda negarlo después. Convierte un registro en prueba (el Tema 4 gira en torno a la cadena de custodia).
- Ambas se consiguen con **criptografía asimétrica**: firmas con tu clave privada, cualquiera verifica con la pública. Se ve en la Clase 5.

## Las tres demostraciones (comandos)
**Confidencialidad: el dato viaja en claro**
```bash
sudo tcpdump -i lo -A port 8000                                  # terminal 1: escucha
curl 'localhost:8000/login?user=admin&pass=Verano2026'           # terminal 2
# aparece GET /login?user=admin&pass=Verano2026 -> contraseña legible. La prueba es la captura.
```
**Integridad: un byte cambiado, mismo tamaño, otro hash**
```bash
echo 'Transferir 1.000 euros a la cuenta ES12...' > orden.txt
sha256sum orden.txt | tee orden.sha256
sed -i 's/1.000/9.000/' orden.txt
ls -l orden.txt            # pesa exactamente lo mismo
sha256sum -c orden.sha256  # orden.txt: FAILED (la suma no coincide) -> la prueba es el hash
```
**Disponibilidad: una conexión sin terminar tumba el servicio**
```bash
curl -s localhost:8000            # responde al instante
nc localhost 8000                 # otra terminal: abre conexión y NO escribe nada
curl --max-time 5 localhost:8000  # SIN -s para ver el error: curl: (28) Operation timed out
```
Es un DoS: una sola conexión que no suelta (servidor de una sola cola a propósito).

## Tres miradas sobre la misma máquina
| Rol | Pregunta |
|---|---|
| Administrador | ¿Está protegido y sigue funcionando? (desde dentro, para mantenerlo) |
| Atacante | ¿Por dónde se rompe? Busca el pilar **más débil**, no el más importante |
| Auditor | ¿Cómo lo demuestro? Es el atacante **con permiso por escrito y con informe**; es lo que seremos en el módulo |

Primer principio del apartado 1.2: conocer el panorama de ciberamenazas, a partir de ataques reales, para construir defensas que funcionen.

## Qué pilar rompe cada ataque
| Ataque | Pilar(es) | Cómo se nota |
|---|---|---|
| Phishing que roba credenciales | Confidencialidad y autenticidad | Accesos desde sitios u horas raras |
| Ransomware | Disponibilidad (y confidencialidad si antes se lleva los datos) | Ficheros ilegibles y nota de rescate |
| Alterar una web o una factura | Integridad | El hash o la firma ya no coinciden |
| Denegación de servicio | Disponibilidad | No responde y el tráfico se dispara |

Clásico que rompe los cuatro a la vez sin hacer ruido: la **contraseña por defecto**.

## Práctica de la semana (no se entrega ni puntúa)
- «¿Cuál han tocado?»: cinco ficheros, su fichero de sumas y un comando que altera uno al azar; encontrarlo y demostrarlo.
- Dos incidentes: **WannaCry** y el **incendio de OVH (2021)**: qué pilares rompe cada uno y con qué evidencia.

## Para la Clase 3 (deberes)
- Leer apartados 1.1 y 1.2 del campus.
- Instalar Kali (Práctica 0 del foro; solo Kali en el portátil) → se presenta en el Lab 1.
- **Test 1**: medio punto, diez preguntas, se abre la semana del 28. Los diez test suman **5 de los 15 puntos de la continua**.
- Clase 3: apartados 1.3, 1.4 y 1.5.
