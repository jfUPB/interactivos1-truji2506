#### Solución actividad 9
```c
from microbit import *
import utime

class Semaforo:
    def __init__(self, rojo, amarillo, verde, initState):
        self.state = initState
        self.startTime = utime.ticks_ms()
        self.rojo = rojo
        self.amarillo = amarillo
        self.verde = verde

    def update(self):
        currentTime = utime.ticks_ms()

        if self.state == "Init":
            self.state = "WaitTimeoutRojo"
            self.startTime = currentTime
            display.set_pixel(self.rojo["x"], self.rojo["y"], 9)

        elif self.state == "WaitTimeoutRojo":
            if utime.ticks_diff(currentTime, self.startTime) > self.rojo["interval"]:
                display.set_pixel(self.rojo["x"], self.rojo["y"], 0)
                self.startTime = currentTime
                self.state = "WaitTimeoutAmarillo"
                display.set_pixel(self.amarillo["x"], self.amarillo["y"], 9)

        elif self.state == "WaitTimeoutAmarillo":
            if utime.ticks_diff(currentTime, self.startTime) > self.amarillo["interval"]:
                display.set_pixel(self.amarillo["x"], self.amarillo["y"], 0)
                self.startTime = currentTime
                self.state = "WaitTimeoutVerde"
                display.set_pixel(self.verde["x"], self.verde["y"], 9)

        elif self.state == "WaitTimeoutVerde":
            if utime.ticks_diff(currentTime, self.startTime) > self.verde["interval"]:
                display.set_pixel(self.verde["x"], self.verde["y"], 0)
                self.startTime = currentTime
                self.state = "WaitTimeoutRojo"
                display.set_pixel(self.rojo["x"], self.rojo["y"], 9)

semaforo = Semaforo(
    {"x": 0, "y": 0, "interval": 1000},
    {"x": 1, "y": 0, "interval": 1000},
    {"x": 2, "y": 0, "interval": 1000},
    "Init"
)

while True:
    semaforo.update()
    utime.sleep_ms(100)
````
#### Estados del semaforo 
1. Init: Estado inicial del semaforo
2. WaitTimeoutRojo: Espera el tiempo asignado al rojo
3. WaitTimeoutAmarillo: Espera el tiempo asignado al amarillo
4. WaitTimeoutVerde: Espera  el tiempo asignado al verde


#### Eventos que se evaluan en cada estado
1. Evento principal: Se evalua si ha pasado el tiempo necesario y se encuentra en el Interval desde que se activo el estado actual
2. Explicación:
   CurrentTime: Es el tiempo actual en milisegundos
   self.starTime: El  tiempo de espera asignado al color actual
   Si la diferencia de tiempo (ticks_diff) es mayor que el intervalo, se dispara el evento de cambio de estado
