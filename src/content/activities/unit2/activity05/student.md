#### Solución actividad 5

Realizando la respectiva investigación me doy cuenta que la comuniación serial, son bidimencionales a través de la UART integrada en el microcontrolador, esto es un circuito integrado encargado de enviar datos al micro controlador y estos realizan una salida de datos respectivos, realizando pruebas en el micro:bit realice un envio de imagen de cara enojada del modulo de Python Editor adjunto codigo 

```c
from microbit import *

uart.init(baudrate=115200)
display.show(Image.ANGRY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        sleep(500)
    if accelerometer.was_gesture('shake'):
        uart.write('C')
        sleep(500)
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('h'):
                display.show(Image.HEART)
                sleep(500)
                display.show(Image.HAPPY)
```
