---
asignatura: Seguridad y Alta Disponibilidad (SAD)
fecha: 2026-09-16
tema: Clase 1 · Presentación del módulo
fuente: transcripción de la clase en directo
---
# SAD · Clase 1 (16/09) · Presentación del módulo

> Siguiente: [Laboratorio 0](2026-09-21_lab0-dia0-servidor.md)

Profesor: **Damián Sualdea** (también da Ciberseguridad y Servicios en Red, SER). Los 3 temarios se solapan al principio y luego se diversifican.

## Logística del curso
- Clases los **miércoles a partir de las 19:00** (hora y media). Tutorías colectivas **quincenales los lunes de 18:00 a 19:00** = laboratorio práctico (vuelve este año tras desaparecer el curso pasado).
- Todo se trabaja en **Linux**; no se administra Windows Server (eso lo da otro módulo).
- Mismo entorno **AWS Academy** que en Ciberseguridad y SER.
- 10 temas; 2 de ellos coinciden literalmente con Ciberseguridad → esas preguntas caen en ambos exámenes.

## Evaluación
- Se aprueba igual que las demás: **nota mínima 5 en el examen** + hacer las actividades (imprescindible).
- **3 actividades**, todas se entregan en **lunes**:
  - Actividad 1 — **19 de octubre**: informe de un incidente real analizado con el framework **MITRE ATT&CK** (p. ej. WannaCry). 3 puntos.
  - Actividad 2 — **18 de enero**: seguridad física, copias de seguridad y control de acceso.
  - Actividad 3 — **15 de marzo**: cifrado, anti-malware, PCI DSS y proxy.
- ⚠️ **Pistas de examen** dadas en clase:
  - Habrá una pregunta sobre el **RGPD** (reglamento general de protección de datos).
  - Habrá una pregunta sobre **PCI DSS**.
  - Habrá una pregunta sobre qué metodología de copia de seguridad usarías en una pyme o en una empresa desplegada en la nube.
  - Regla de copias de seguridad que se repetirá: **3-2-1** (y su variante ampliada 3-2-1-1-0).

## Demo en directo: primer servidor EC2
Crea una instancia Ubuntu Server, `t3.micro`, par de claves por defecto (Vockey → se descarga como `labuser.pem`), Security Group con SSH(22) y HTTP(80) abiertos.

```bash
sudo apt update
sudo apt install apache2 -y
cd /var/www/html
sudo rm index.html
sudo nano index.html        # escribe un <h1>Bienvenidos...</h1> y guarda
```
```bash
chmod 400 labuser.pem
ssh -i labuser.pem ubuntu@<IP-pública>
sudo su
exit
```

> Error de novato que comete el propio profesor en directo: ejecutar `apt install` sin haber hecho `apt update` antes → falla. "Siempre que entras a un servidor hay que actualizarlo primero."

- La **IP pública es dinámica**: cambia cada vez que paras/arrancas la instancia. Una **IP elástica** (fija) cuesta dinero mientras la tienes reservada y no asignada (estimado en clase: del orden de 50 céntimos/día si la máquina está encendida 24h). Se verá más adelante.

## WannaCry ("Guanacray"), mencionado como ejemplo
Malware/ransomware que se propagó explotando el protocolo **SMB (Samba)**, puerto **445** (el profesor dudó primero entre 449 y 445, confirmó 445), aprovechando SMBv1 activo por defecto en Windows. Afectó a Telefónica España; en el relato del profesor, Chema Alonso recibió críticas públicas injustas porque en ese momento no estaba en el área de seguridad. **No verificado**: el año exacto que menciona en el audio es confuso ("no fue en 2014"); el incidente de WannaCry en Telefónica es de **mayo de 2017** — contrastar con fuentes oficiales antes de usarlo en la Actividad 1.

## Tarea para el fin de semana
- Comprar un **dominio gratuito**.
- Tener cuenta de **GitHub**.
- Instalar un hipervisor (VirtualBox, UTM si Mac, etc.) por si hace falta.
- Leer el Tema 1 si se quiere ir viendo algo, sin obligación todavía.

Próxima clase: miércoles, primera "clase oficial" (laboratorio 0, levantar el servidor **sad1**).
