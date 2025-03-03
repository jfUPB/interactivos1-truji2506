#### Solución actividad 14

##### Descripción de las pruebas realizadas en el codigo de la bomba, pruebas, errores encontrados y las correcciones

##### Casos de prueba 
Se inicio con la configuraion del tiempo en el estado confi, teniendo en cuenta el tiempo en 20 segundos, ademas se tomo la acción de presionar varias veces la tecla A para que aumentara los segundos hasta el tope, en ese momento funciono bien 
Se revisaron los limites de los segundos en el estado de config siendo 60 segundos, teniendo en cuenta que no se podria pasar de los 60 segundo y fue correcto 
Se realizo la activación del temporizador, teniendo en cuenta que si el temporizador llegaba a 10 segundos al momento de sacudirlo empieza el conteo regresivo de los 10 segundos 
al momento de entrar en la cuenta regresiva se establecio que en el 1 uno sacara una imagen con su respectivo sonido de warning y cuando terminaba el conteo y llegara a 0 tambien se evidenciara una calavera junto con su rrespectivo sonido 

##### Errores encontrados 
El sonido de alerta final no siempre se reproduce 
Al momento de preparar el microbit lo que hace es dar sonidos no programados

#### Correcciones elaboradas por chatGPT
```c
from microbit import *
import utime
import music

BUZZER = pin0
SOUND_ARMED = music.JUMP_UP
SOUND_WARNING = music.POWER_UP
SOUND_EXPLOSION = music.POWER_DOWN

STATE_INIT = 0
STATE_CONFIG = 1
STATE_ARMED = 2
STATE_EXPLOSION = 3
STATE_RESET = 4

tiempo = 20
start_time = 0
interval = 1000  # 1 segundo

current_state = STATE_INIT
pin0.set_pull(Pull.DOWN)  # Estabilizar la lectura del pin

while True:
    if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        tiempo = 20
        start_time = utime.ticks_ms()
        current_state = STATE_CONFIG

    elif current_state == STATE_CONFIG:
        if button_a.was_pressed() and tiempo < 60:
            tiempo += 1
            display.scroll(str(tiempo))
        
        if button_b.was_pressed() and tiempo > 10:
            tiempo -= 1
            display.scroll(str(tiempo))
        
        if accelerometer.was_gesture("shake"):
            display.show(Image.SKULL)
            music.play(SOUND_ARMED, pin=BUZZER)
            start_time = utime.ticks_ms()
            current_state = STATE_ARMED

    elif current_state == STATE_ARMED:
        if utime.ticks_diff(utime.ticks_ms(), start_time) >= interval:
            if tiempo > 0:
                tiempo -= 1
                display.scroll(str(tiempo))
            start_time = utime.ticks_ms()

        if tiempo == 1:
            music.play(SOUND_WARNING, pin=BUZZER)

        if tiempo <= 0:
            display.show(Image.SKULL)
            current_state = STATE_EXPLOSION

    elif current_state == STATE_EXPLOSION:
        display.show(Image.SKULL)
        music.play(SOUND_EXPLOSION, pin=BUZZER)
        utime.sleep(1)
        current_state = STATE_RESET

    elif current_state == STATE_RESET:
        display.show(Image.HAPPY)
        if pin0.read_digital():
            tiempo = 20
            display.clear()
            current_state = STATE_INIT
```
