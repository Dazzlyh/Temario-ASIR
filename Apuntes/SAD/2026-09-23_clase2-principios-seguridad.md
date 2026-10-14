---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-09-23
tema: Tema 1 (1.1-1.2) · Principios de seguridad · riesgo · MITRE ATT&CK
fuente: transcripción de la clase en directo
---
# SAD · Clase 2 (23/09) · Principios de seguridad

> Anterior: [Laboratorio 0](2026-09-21_lab0-dia0-servidor.md) · Siguiente: [MITRE y defensa del servidor](2026-09-30_mitre-defensa-servidor.md)

## Seguridad informática vs. seguridad de la información
No son lo mismo y no son independientes, van siempre de la mano:
- **Seguridad informática** = bastionar sistemas, redes, equipos, servicios, infraestructura. Es la parte técnica que se trabaja en este curso.
- **Seguridad de la información** (SGSI, norma **ISO 27001**) = qué información es confidencial, quién debe gestionarla, cómo se protege independientemente de la tecnología. Por mucho que bastiones, si no hay directrices desde arriba, no vale para nada. Es una salida profesional importante que **no requiere perfil técnico** (hay gente dedicada solo a la parte documental/legal).

> El profesor usa el término **"elementos"** (no "pilares", para no confundirlo con la tríada CID que se verá en la siguiente clase) para lo que hay que proteger: **software** (SO + servicios + aplicaciones), **hardware** (CPD, discos, red) y **datos**.

## Caso real: ransomware en el Hospital Clínic de Barcelona (marzo 2023)
Un ransomware cifró los sistemas del hospital. Se canceló un gran número de operaciones y consultas. Documentado por **INCIBE**. El profesor lo compara con lo ocurrido en el **Hospital de Torrejón de Ardoz** durante la pandemia, donde volvieron a escribir los historiales en papel.
- Análisis CID del incidente: **confidencialidad** rota (datos secuestrados), **integridad** probablemente comprometida (manipulación durante el cifrado), **disponibilidad** rota (no se podía acceder al historial clínico). Un dato médico robado "no se recompra ni se recupera".
- **ENISA** = agencia europea de ciberseguridad; publica un informe anual de amenazas y actores (de qué países operan los grupos, a qué sectores atacan). Fuente recomendada para seguir el panorama real de amenazas.

## Demo en vivo sobre un servidor propio del profesor
```bash
history                                  # ver instrucciones ejecutadas
wc -l access.log                         # nº de líneas (peticiones)
awk '{print $7}' access.log | sort | uniq -c | sort -rn | head -15   # URLs más pedidas
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head       # IPs más activas
```
Comprobó el origen de las IPs sospechosas en **abuseipdb.com** (muestra reportes de abuso, nº de denuncias, tipo de actividad: scan, fuerza bruta, honeypot...).

Demo interactiva: compartió su IP pública en directo, cada alumno accedió desde el navegador añadiendo su nombre como parámetro de la URL, y se vio en tiempo real cómo aparecían las peticiones en el log del servidor (algunas con código **408**, timeout del cliente).

```bash
sudo tail -f /var/log/auth.log           # intentos de conexión SSH en directo
```
Un alumno hizo un `ssh` de prueba y apareció al instante en el log — así se identifica, separando por franjas de tiempo e IP, quién intenta qué.

## Factor humano: la "capa 8"
Las personas son la primera línea de defensa **y** el eslabón más frágil (insider, empleado descontento, alguien que da su contraseña por teléfono). La única solución real es formación y cultura de ciberseguridad: campañas de phishing controladas (se verán con GoPhish en Ciberseguridad/SER), charlas, normas no punitivas.

> Anécdota contada por el profesor, **no verificada**: auditoría (cree recordar que de Deloitte) a una empresa israelí en la que un hallazgo decía que los empleados no bloqueaban el PC al levantarse del puesto; la empresa respondió "no aplica" porque es su cultura de confianza interna. De ahí el nombre jocoso **"ataque de David Hasselhoff"**: broma informática (de origen británico) que consiste en cambiar el fondo de pantalla de quien deja la sesión sin bloquear.

- Recomienda apuntarse al programa de **cibercooperantes de INCIBE** (voluntariado, charlas de concienciación en colegios/asociaciones, gratuito, apunta currículum).
- Demo con **haveibeenpwned.com**: comprobó un correo Hotmail antiguo del propio profesor → 9 brechas encontradas (LinkedIn, Daily Motion y otras), con datos filtrados como dirección, teléfono o email+contraseña según el caso.

## Gestión del riesgo
**El riesgo cero no existe**, solo se gestiona. Quien diga lo contrario "está vendiendo humo".
- **Amenaza**: algo que puede causar daño (un ataque, un incendio).
- **Vulnerabilidad**: el fallo que permite que la amenaza se cumpla.
- **Impacto**: el daño sobre el activo (con un "precio" asociado).
- **Riesgo**: probabilidad de que la amenaza explote la vulnerabilidad y afecte al activo.
- Tres estrategias frente al riesgo: **reducirlo** (medidas de seguridad), **delegarlo/transferirlo** (contratar un seguro), **aceptarlo** (asumir la franquicia). Herramienta de análisis de riesgos mencionada: **PILAR**.
- Salidas profesionales mencionadas en este campo (más documentales que técnicas): Risk Manager, consultor GRC, consultor de normativa ENS, consultor ISO 27001.

## Inventario antes que nada
> "Sin inventario no hay seguridad": si no sabes qué tienes (hardware, software, datos), no puedes protegerlo.

```bash
lscpu              # nº de CPUs (t3.micro → 2 vCPU)
free -h            # memoria disponible
dpkg -l | wc -l    # nº de paquetes instalados (demo en sad1: 696)
```

## MITRE ATT&CK, con ejemplos reales usados en clase
Framework público que documenta tácticas (el objetivo del atacante) y técnicas (cómo lo consigue), con grupos conocidos que las usan y mitigaciones/detección para cada una.
- **T1110 — Fuerza bruta** (táctica *Credential Access*): probar credenciales de forma sistemática contra un servicio o contra hashes robados. Herramientas citadas: Hydra, Hydra/"patator".
- **T1566 — Phishing** (táctica *Initial Access*): múltiples sub-técnicas (enlaces, adjuntos...).

### Cómo se rompe una contraseña (hash, no cifrado)
- Un hash es **irreversible**: no es lo mismo que codificar/cifrar, no se puede "descifrar" el hash para recuperar la contraseña.
- Para romperlo: se generan candidatas, se calcula su hash y se compara con el robado (fuerza bruta o diccionario) hasta encontrar coincidencia.
- La longitud de la contraseña es determinante en el tiempo de crackeo (demo con una calculadora online de tiempos de fuerza bruta): con 8 caracteres se rompe casi al instante; añadir caracteres dispara el tiempo exponencialmente. Se verá en detalle (y se practicará con `John the Ripper`) en Ciberseguridad.

## Actividad 1 (recordatorio, entrega 19/10)
Elegir un incidente real (ej. WannaCry, el caso de Cracovia mencionado en clase, u otro que proponga el alumno), documentarlo usando la terminología de MITRE ATT&CK:
1. Resumen del incidente.
2. Activos afectados.
3. Cadena de ataque (tácticas/técnicas MITRE).
4. Evidencias.
5. Principios de seguridad comprometidos (CID).
6. Medidas que se podrían haber tomado.
7. Reflexión final.

> Consejo del profesor: "si lo hacéis más o menos normal, vais a tener un notable sin complicarse la vida; si lo subís cutre, me vais a obligar a leerlo a fondo para buscar los puntos — mejor para vosotros que quede claro y bien explicado."

## Tarea para la semana
- Elegir el incidente de la Actividad 1.
- Opcional: cuestionario "Analiza tus riesgos" de INCIBE (no se entrega, es para uso propio).

Próxima clase: **miércoles 30 de septiembre**.
