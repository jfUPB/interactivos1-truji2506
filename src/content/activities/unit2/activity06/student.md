#### Solución actividad 6 

En esta actividad elaboré un codigo donde muestra 3 tipos de imagenes con sus respectivos textos, 

Presionando A en el microbit podemos evidenciar una cara feliz en el feedback de los leds, despues de terminar esta animación podremos evidenciar la salida del texto donde dice hola 

Presionando B en el microbit podemos evidenciar un corazon en el feedback de los leds, despues de terminar estar animación podremos evidenciar la salida del texto donde dice Micro:bit 

Presionando el logo del microbit podemos evidenciar un fantasma en el feedback de los leds, despues de terminar esta animación podremos evidenciar la salida del texto donde dice Python 


```c
from microbit import *

while True:
    if button_a.is_pressed():  # Si se presiona el botón A
        display.show(Image.HAPPY)
        sleep(1000)
        display.scroll("¡Hola Mundo!")

    if button_b.is_pressed():  # Si se presiona el botón B
        display.show(Image.HEART)
        sleep(1000)
        display.scroll("Micro:bit")

    if pin_logo.is_touched():  # Si se toca el logo táctil
        display.show(Image.GHOST)  
        sleep(1000)
        display.scroll("Python")
```
En este codigo creamos un while true: ademas de varios if para con sus respectivas declaraciones de botones para el A,B y el logo 
