---
asignatura: Ciberseguridad
fecha: 2026-09-22
tema: Práctica 1 · reproducir las tres demostraciones de la Clase 2
fuente: CIBER_Practica1.md
---
# Ciber · Práctica 1 · los pilares desde el atacante

> Relacionado: [Clase 2](2026-09-22_clase2-pilares.md)

**No se entrega y no puntúa.** Cada captura es una evidencia válida para la Actividad 1. La integridad se hace en cualquier SO; confidencialidad y disponibilidad necesitan Linux (Kali) — si no está montado, se hacen en el [Lab 1](2026-09-24_lab1-paseo-por-kali.md).

## Preparación: servidor de prueba
`servidor_demo.py` (adjunto en el foro), de **una sola cola a propósito**.
```bash
mkdir -p ~/lab01 && cd ~/lab01     # copiar ahí servidor_demo.py (y algún fichero para que la página no salga vacía)
python3 servidor_demo.py           # debe salir: «Servidor de demostración escuchando en http://localhost:8000»
```
Si no existe `python3`, probar `python`. Parar con Ctrl+C.

## 1 · Confidencialidad
```bash
sudo tcpdump -i lo -A port 8000                                  # terminal 1
curl 'localhost:8000/login?user=admin&pass=Verano2026'           # terminal 2
```
En la terminal 1 aparece la petición con la contraseña legible → captura = prueba.

## 2 · Integridad (cualquier sistema)
```bash
echo 'Transferir 1.000 euros a la cuenta ES12' > orden.txt
sha256sum orden.txt | tee orden.sha256
sed -i 's/1.000/9.000/' orden.txt
ls -l orden.txt            # mismo peso
sha256sum -c orden.sha256  # orden.txt: FAILED
```
macOS: `shasum -a 256`; Windows: `Get-FileHash` (PowerShell).

## 3 · Disponibilidad
Con `servidor_demo.py` corriendo:
```bash
nc localhost 8000                    # déjalo quieto, sin escribir
curl --max-time 5 localhost:8000     # sin -s, o no se ve el error -> curl: (28) Operation timed out
```
Una sola conexión sin terminar tumba el servicio de una cola = denegación de servicio. Recuperar: Ctrl+C en el `nc`.

## Para pensar (salió en clase; se cierra en la Clase 5)
Si el atacante cambia también el fichero de huellas (`orden.sha256`), ¿se puede demostrar? ¿Dónde debería haberse guardado la huella para que no la pudiera tocar?
*(Pista del material: Clase 5 = criptografía asimétrica/firmas. Es una inferencia mía; la respuesta oficial se da en esa clase.)*

## Recordatorio legal
Solo tu máquina o las del laboratorio. Escanear, capturar tráfico o atacar otra cosa puede ser delito (**arts. 197 y 264 del Código Penal**).
