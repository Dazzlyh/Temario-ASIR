---
asignatura: Servicios en Red e Internet (SER)
fecha: 2026-09-15
tema: Presentación del módulo, logística y roadmap de los 3 trimestres
fuente: transcripción de la clase en directo
---
# SER · Presentación del módulo (15/09)

> Siguiente: [22/09 · Conceptos básicos de red: puertos, datagramas, NAT, protocolos](2026-09-22_conceptos-red-puertos-nat.md)

Primera clase, sin contenido técnico todavía: presentación del profesor (Damián Sualdea), logística del curso y roadmap de los 3 trimestres. Mismo profesor da SER, SAD y la optativa de Ciberseguridad.

## Logística
- Horario (**no verificado** — el profesor se corrigió varias veces en la propia clase): clase en directo semanal, queda grabada; tutorías quincenales.
- **Fechas de entrega de las 3 actividades**: 1ª el **16 de noviembre**, 2ª el **15 de febrero**, 3ª el **8 de abril**. Todas se entregan el lunes, hasta las **23:59**.
- **Evaluación**: examen presencial obligatorio + hasta 15 puntos extra repartidos en las 3 actividades (3 + 3 + 4 → se suman sobre un máximo de 10 en la nota de evaluación continua) más los tests de cada unidad (hasta 5 puntos cada test).
- **Pista de examen**: el profesor comenta que el año pasado entró una pregunta sobre cómo se monta un *virtual host* paso a paso — los comandos de las actividades "valen mucho para el examen".
- Primera actividad (entrega 16/11): montar una web completa — DNS propio + Apache + HTTPS + WordPress/CMS. Se trabaja íntegramente en AWS.

## Roadmap de la asignatura (3 trimestres)
- **1er trimestre**: conceptos básicos de red e Internet → DHCP (único apartado que se monta con máquinas virtuales en red aislada) → DNS con BIND9 → Apache (virtual hosts, HTTPS con Let's Encrypt, WordPress/Moodle).
- **2º trimestre**: FTP (`vsftpd`) → seguridad de los servicios → correo electrónico (Postfix + Dovecot + Roundcube) — "el tocho", pero nunca para uso personal (listas negras).
- **3er trimestre**: streaming de audio/vídeo (Plex/Jellyfin + streaming puro), mensajería/colaboración (Nextcloud), telefonía IP en la nube.
- Todo se monta sobre **Ubuntu Server por consola, sin entorno gráfico**, conectando por SSH, desde el minuto 1 en AWS (EC2/F2).

## Entorno de trabajo
- AWS Academy: de alta gratis para los alumnos (50 $ de crédito para prácticas, laboratorios con 180 días de validez, se renueva). Cursos disponibles: Cloud Foundations, Architecting, Security, Developer/Operations (CI/CD).
- Alternativas de servidor gratis mencionadas (no verificado en detalle): Oracle Cloud Free Tier "de por vida" (2 vCPU / 12 GB RAM / 100 GB disco) — más barato que AWS según un compañero con experiencia en varios proveedores (Azure, Google, Oracle, OVH).
- **GitHub Student Developer Pack**: dominio gratis 1 año (.me, .live, .software, .app, .tech), créditos Azure (100 $), Namecheap, DigitalOcean, etc. — se valida con el correo `@unir...` (no garantizado, depende del proveedor).
- Dominios recomendados para el curso: comprar uno barato (desde 1€, ej. OVH) — hace falta mínimo 1 dominio para el proyecto intermodular.

## Vocabulario / definiciones del profesor
- **Servidor = camarero**: el cliente pide, el servidor va a la "cocina" (el recurso/backend), lo trae y responde. Metáfora que reaparece en la siguiente clase.
- **"La nube es el ordenador de otro"**: software de gestión de muchos servidores, se cobra por uso (horas encendida), no por "estar contratada".
- IA en clase: usarla para entender errores, no para que trabaje por ti — "se contrata a una persona para que supervise lo que hace la IA, no al revés".

## Enlaces
Buscador RFC: rfc-editor.org · AWS Academy · GitHub Student Developer Pack
