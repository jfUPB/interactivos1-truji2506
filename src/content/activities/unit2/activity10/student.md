#### Solución actividad 10

```c
from microbit import *
import utime

STATE_INIT = 0
STATE_HAPPY = 1
STATE_SMILE = 2
STATE_SAD = 3
STATE_ANGRY= 4
STATE_DIAMOND = 5
STATE_RABBIT= 6 

HAPPY_INTERVAL = 1500
SMILE_INTERVAL = 1000
SAD_INTERVAL = 2000
ANGRY_INTERVAL = 2500
DIAMOND_INTERVAL = 3000
RABBIT_INTERVAL = 3500

current_state = STATE_INIT
start_time = 0
interval = 0

while True:
    # pseudoestado STATE_INIT
    if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        start_time = utime.ticks_ms()
        interval = HAPPY_INTERVAL
        current_state = STATE_HAPPY
    elif current_state == STATE_HAPPY:
        if button_a.was_pressed():
            # Acciones para el evento
            display.show(Image.SAD)
            # Acciones de entrada para el siguiente estado
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
            current_state = STATE_SAD
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            # Acciones para el evento
            display.show(Image.SMILE)
            # Acciones de entrada para el siguiente estado
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE
    elif current_state == STATE_SMILE:
        if button_a.was_pressed():
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.SAD)
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
            current_state = STATE_SAD
    elif current_state == STATE_SAD:
        if button_a.was_pressed():
            display.show(Image.SMILE)
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.ANGRY)
            start_time = utime.ticks_ms()
            interval = ANGRY_INTERVAL
            current_state = STATE_ANGRY
    elif current_state == STATE_ANGRY:
        if button_a.was_pressed():
            display.show(Image.SAD)
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
            current_state = STATE_SAD
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.DIAMOND)
            start_time = utime.ticks_ms()
            interval = DIAMOND_INTERVAL
            current_state = STATE_DIAMOND
    elif current_state == STATE_DIAMOND:
        if button_a.was_pressed():
            display.show(Image.ANGRY)
            start_time = utime.ticks_ms()
            interval = ANGRY_INTERVAL
            current_state = STATE_ANGRY
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.RABBIT)
            start_time = utime.ticks_ms()
            interval = RABBIT_INTERVAL
            current_state = STATE_RABBIT
    elif current_state == STATE_RABBIT:
        if button_a.was_pressed():
            display.show(Image.SMILE)
            start_time = utime.ticks_ms()
````
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY
