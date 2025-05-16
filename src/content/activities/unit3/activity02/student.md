#### Solucion actividad 2 
```c
DISARM_SEQUENCE = ["A", "B", "A", "SHAKE"]
input_sequence = []
```
Aquí defines la secuencia correcta que debe ingresarse para desactivar la bomba. También se inicializa input_sequence como una lista vacía que almacenará los eventos de entrada del usuario.
Detección de eventos en el estado ARMADO (STATE_ARMED): En el bloque elif current_state == STATE_ARMED:, se agregaron estos fragmentos de código para registrar las entradas:

```c
if button_a.was_pressed():
    input_sequence.append("A")
if button_b.was_pressed():
    input_sequence.append("B")
if accelerometer.was_gesture("shake"):
    input_sequence.append("SHAKE")
```
Este código detecta cuándo se presionan los botones A o B o cuándo se sacude el dispositivo, y almacena cada evento en la lista input_sequence.
Validación de la secuencia:

```c
if input_sequence == DISARM_SEQUENCE:
    display.show(Image.HAPPY)
    music.play(SOUND_ARMED, pin=BUZZER)
    input_sequence = []  # Reiniciar la secuencia
    current_state = STATE_CONFIG
```
Si la lista input_sequence coincide con DISARM_SEQUENCE, la bomba se desactiva y se muestra la imagen HAPPY mientras suena un tono indicando éxito.
Reinicio de la secuencia: Cada vez que se inicia un nuevo ciclo (STATE_INIT) o se desactiva la bomba correctamente, se vacía la lista input_sequence con:
```c
input_sequence = []
```




```c
from microbit import *
import utime
import music

BUZZER = pin_logo  # Cambiado para usar el botón del logo
SOUND_ARMED = music.JUMP_UP
SOUND_WARNING = music.POWER_UP
SOUND_EXPLOSION = music.POWER_DOWN

STATE_INIT = 0
STATE_CONFIG = 1
STATE_ARMED = 2
STATE_EXPLOSION = 3
STATE_RESET = 4

# Nueva variable para almacenar la secuencia de desactivación
DISARM_SEQUENCE = ["A", "B", "A", "SHAKE"]
input_sequence = []


tiempo = 20
start_time = 0
interval = 1000  # 1 segundo

current_state = STATE_INIT

while True:
    if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        tiempo = 20
        input_sequence = []  # Reiniciar la secuencia al iniciar
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

        # Comprobar si se presiona A o B
        if button_a.was_pressed():
            input_sequence.append("A")
        if button_b.was_pressed():
            input_sequence.append("B")
        if accelerometer.was_gesture("shake"):
            input_sequence.append("SHAKE")

        # Verificar si la secuencia es correcta
        if input_sequence == DISARM_SEQUENCE:
            display.show(Image.HAPPY)
            music.play(SOUND_ARMED, pin=BUZZER)
            input_sequence = []  # Reiniciar la secuencia
            current_state = STATE_CONFIG

        # Reproducir sonido de advertencia si queda 1 segundo
        if tiempo == 1:
            music.play(SOUND_WARNING, pin=BUZZER)

        # Si el tiempo llega a cero, mostrar la explosión
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
        if pin_logo.is_touched():  # Cambiado para usar el botón del logo
            tiempo = 20
            display.clear()
            current_state = STATE_INIT
```
