#### Solución actividad 12

Se importaron 3 librerias, microbit para interactuar con el mismo, utime para manejar el tiempo con precion, ademas tambien añadi music para reproducir 3 sonidos de armada, peligro y explision 

Se realizo la definicion de los pines y sonidos son sus respectivos sonidos 

Se establecio los estados del codigo 
init 
config 
armed 
explosion
reset

Se configuro el tiempo del temporizador que iniciara en 20 se podria ajustar entre 10 y 60 segundos

Se establecio el bucle principal 

En el estado inicial se establecio una imgen de cara feliz para que este presente al inicio del codigo aqui se establece el reinciio del temporizador 20 segundos y pasa al estado de configuración 

En el estado de configuración cuando presionas A aumenta el tiempo en 1 hasta los 60 segundos, dismuye el tiempo en 1
hasta que llegue a 10 segundos, se le puso un acelerometro activa el estado armado, mostrando una calabera y reproduciendo el sonido de armado

En el estado armado reduce el tiempo cada segundo y lo muestra en la pantalla, si el tiempo llega a 1 segundo, se reproduce el sonido de advertencia, y si el tiempo llega a 0, se muestra una calavera y cambia al estado explosion 

En el estado Exposion muestra una calavera y reproduce el sonido de explosion, espera 1 segundo antes de pasar el estado de reset

En el estado Reset muestra de nuevo la cara feliz y si se presiona en el boton del logo se limpia a pantalla y se regresa al estado inicial 

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

while True:
    if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        tiempo = 20
        start_time = utime.ticks_ms()
        current_state = STATE_CONFIG
        
    elif current_state == STATE_CONFIG:
        if button_a.was_pressed() and tiempo < 60:
            tiempo += 1
            if tiempo < 10:
                display.show(str(tiempo))
            else:
                display.scroll(str(tiempo))
        
        if button_b.was_pressed() and tiempo > 10:
            tiempo -= 1
            if tiempo < 10:
                display.show(str(tiempo))
            else:
                display.scroll(str(tiempo))
        
        if accelerometer.was_gesture("shake"):
            display.show(Image.SKULL)
            music.play(SOUND_ARMED, pin=BUZZER) 
            start_time = utime.ticks_ms()
            current_state = STATE_ARMED

    elif current_state == STATE_ARMED:
        if utime.ticks_diff(utime.ticks_ms(), start_time) >= interval:
            tiempo -= 1
            if tiempo > 0:
                if tiempo < 10:
                    display.show(str(tiempo))
                else:
                    display.scroll(str(tiempo))
            else:
                display.show("0")
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
````
