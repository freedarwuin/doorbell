
# 📄 Timbre Inteligente con Raspberry Pi

## 📌 Descripción
Este script permite a una Raspberry Pi reproducir aleatoriamente un sonido `.mp3` cuando detecta que se ha presionado un botón conectado a uno de sus pines GPIO.  
El sistema está pensado para funcionar como un **timbre inteligente** que puede personalizarse con diferentes audios.

---

## 🛠 Requisitos de hardware
- **Raspberry Pi** (probado en Raspberry Pi 3).
- Botón físico conectado al **pin 12** (numeración física **BOARD**).
- Resistencia de *pull-up* (puede ser interna de la Pi).
- Altavoz o sistema de audio conectado a la Raspberry Pi.
- Archivos de audio en formato `.mp3` dentro de la carpeta configurada.

---

## 📦 Dependencias de software
Instalar paquetes necesarios en la Raspberry Pi:

```bash
sudo apt update
sudo apt install mpg321 python3-rpi.gpio
```

---

## 📂 Estructura de archivos
```
/home/freedarwuin/doorbell/audio/   # Carpeta con los sonidos .mp3
app.py                              # Script principal
```

---

## ⚙ Configuración
En el script puedes modificar:
```python
AUDIO_DIRECTORY = '/home/freedarwuin/doorbell/audio'  # Ruta a los audios
PIN_NUMBER = 12                                        # Pin físico usado para el botón
```

---

## ▶ Ejecución
Para iniciar el timbre:
```bash
python3 timbre.py
```
El script quedará en ejecución, esperando que se presione el botón.

---

## 🔍 Funcionamiento
1. **Lectura de audios**:  
   El script busca todos los archivos `.mp3` en la carpeta definida en `AUDIO_DIRECTORY`.

2. **Detección del botón**:  
   Usa la librería `RPi.GPIO` para detectar cambios de estado en el **pin 12**.

3. **Reproducción aleatoria**:  
   Cada vez que el pin detecta un cambio, el script elige aleatoriamente un audio y lo reproduce usando `mpg321`.

4. **Ejecución continua**:  
   El script funciona en un bucle infinito hasta que se detiene manualmente con `CTRL+C`.

---

## 📝 Notas
- Si no se encuentran archivos `.mp3` en la carpeta especificada, el script finaliza con un mensaje de error.
- El script usa **numeración física** (`GPIO.BOARD`), no la numeración BCM.
- Funciona únicamente en Raspberry Pi con sistema Linux.
- El retardo `time.sleep(0.5)` evita que un toque prolongado genere múltiples reproducciones.
