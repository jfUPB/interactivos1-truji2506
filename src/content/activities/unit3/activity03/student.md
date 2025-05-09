#### Solucion actividad 3

#### Explicación 
El código fue separado en dos funciones principales:
tareaEventos(): Se encarga de detectar todos los eventos de entrada, ya sea desde los botones, el logo, 
el acelerómetro o el puerto serial. Cuando detecta un evento válido, lo almacena en la variable current_event
y marca event_detected como True.
tareaBomba(): Controla el funcionamiento de la bomba con base en los eventos detectados, sin interactuar 
directamente con los sensores. Solo consume los eventos almacenados por tareaEventos().

```c
from microbit import *
import utime
import music

BUZZER = pin_logo  
SOUND_ARMED = music.JUMP_UP
SOUND_WARNING = music.POWER_UP
SOUND_EXPLOSION = music.POWER_DOWN

STATE_INIT = 0
STATE_CONFIG = 1
STATE_ARMED = 2
STATE_EXPLOSION = 3
STATE_RESET = 4

DISARM_SEQUENCE = ["A", "B", "A", "SHAKE"]
input_sequence = []

tiempo = 20
start_time = 0
interval = 1000  # 1 segundo

event_detected = False
current_event = ""
current_state = STATE_INIT

def tareaEventos():
    global event_detected, current_event
    if button_a.was_pressed():
        current_event = "A"
        event_detected = True
    elif button_b.was_pressed():
        current_event = "B"
        event_detected = True
    elif accelerometer.was_gesture("shake"):
        current_event = "SHAKE"
        event_detected = True
    elif pin_logo.is_touched():
        current_event = "T"
        event_detected = True
    
    # Detectar eventos por puerto serial
    if uart.any():
        message = uart.read().decode('utf-8').strip()
        if message in ["A", "B", "SHAKE", "T"]:  # Validar que sea un evento válido
            current_event = message
            event_detected = True


def tareaBomba():
    global current_state, tiempo, start_time, input_sequence, event_detected, current_event

    if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        tiempo = 20
        input_sequence = [] 
        start_time = utime.ticks_ms()
        current_state = STATE_CONFIG

    elif current_state == STATE_CONFIG:
        if event_detected and current_event == "A" and tiempo < 60:
            tiempo += 1
            display.show(str(tiempo)) if tiempo < 10 else display.scroll(str(tiempo))

        elif event_detected and current_event == "B" and tiempo > 10:
            tiempo -= 1
            display.show(str(tiempo)) if tiempo < 10 else display.scroll(str(tiempo))

        elif event_detected and current_event == "SHAKE":
            display.show(Image.SKULL)
            music.play(SOUND_ARMED, pin=BUZZER)
            start_time = utime.ticks_ms()
            current_state = STATE_ARMED

        event_detected = False 

    elif current_state == STATE_ARMED:
        if utime.ticks_diff(utime.ticks_ms(), start_time) >= interval:
            tiempo -= 1
            display.show(str(tiempo)) if tiempo > 0 else display.scroll("0")
            start_time = utime.ticks_ms()

        if event_detected:
            if current_event in ["A", "B", "SHAKE"]:
                input_sequence.append(current_event)
                event_detected = False

        if input_sequence == DISARM_SEQUENCE:
            display.show(Image.HAPPY)
            music.play(SOUND_ARMED, pin=BUZZER)
            input_sequence = []  
            current_state = STATE_CONFIG

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
        if current_event == "T": 
            tiempo = 20
            display.clear()
            current_state = STATE_INIT
        event_detected = False  


while True:
    tareaEventos() 
    tareaBomba()
``` 
