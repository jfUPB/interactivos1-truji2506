#### Solución actividad 7 

En esta actividad interactue con varios codigos en Micro:bit Python Editor, con la ayuda de chatgpt me ayudo a comprender los codigos de musica que se pueden implementar, en los ejercicios anteriores pude aleborar y entender el uso de os codigos para el boton A y B, y en este codigo use para que poder elaborar la actividad y asi hacerlo de forma ordenada

```c
from microbit import *
import music
BUZZER = pin0
while True:
    if button_a.is_pressed():
        music.play(music.JUMP_UP, pin=BUZZER)
    elif button_b.is_pressed():
        music.play(music.POWER_DOWN, pin=BUZZER)
```
En el codigo podemos evidenciar que realizamos la importacion de musica para la elaboración, se realizo la declaracion del buzzer para que pueda realizar la salida de sonidos, en el while true evidenciamos que si presionamos A escuchamos un sonido de salto, y si presionamos B escuchamos un sonido donde el poder baja 
