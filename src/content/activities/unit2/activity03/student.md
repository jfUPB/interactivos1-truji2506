#### Solución actividad 3 

#### Investigación sobre micro:bit y MicroPython

##### Entradas y salidas del micro:bit

###### Entradas
1. Boton A: Boton fisico en la parte frontal del micro:bit que puede ser presionado para interactuar con lo programado
2. Boton B: Segundo boton fisico en la parte frontal del micro:bit que puede ser presionado para interactuar con el programa
3. Sensor de luz: Detecta la intensidad de la luz del ambiente usando la matriz de Leds
4. Acelerometro: Permite detectar movimientos y orientación del dispositivo

###### Salidas
1. Matriz de Leds: Permite mostrar imagenes, texto o patrones de luz
2. Zumbador: Puede generar sonidos en diferentes frecuencias
3. Puertos GPIO: Se pueden usar para conectar otros dispositivos como motores o sensores externos
4. Comunicación por Radio: Permite enviar y recibir datos de otros micro:bits cercanos.

##### Funciones de MicroPython para el micro:bit

###### Funciones de entrada:

1. button_a.is_pressed(): Devuelve True si el botón A está presionado.
```c
from microbit import *
if button_a.is_pressed():
    display.show("A")
````
2. accelerometer.get_x(): Devuelve el valor de inclinación en el eje X
```c
from microbit import *
while True:
    x = accelerometer.get_x()
    print(x)
    sleep(100)
````
3. pin0.read_analog(): Lee un valor analógico del pin 0
```c
from microbit import *
value = pin0.read_analog()
print(value)
````
###### Funciones de salida:
1. display.show(): Muestra caracteres o imágenes en la matriz de LEDs
```c
from microbit import *
display.show(Image.HEART)
````
2. pin1.write_digital(1): Envía una señal digital (1 o 0) a un pin de salida.
```c
from microbit import *
pin1.write_digital(1)  # Enciende un LED conectado al pin 1
````
3. music.play(music.BA_DING) – Reproduce una melodía predefinida en el zumbador.
```c
from microbit import *
import music
music.play(music.BA_DING)
````





