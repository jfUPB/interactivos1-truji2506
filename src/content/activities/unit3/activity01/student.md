#### Solución actividad 1

#### Reflexion
El comportamiento del semáforo en una clase, el código se vuelve más organizado y modular. Esto facilita su reutilización y mantenimiento.
La clase Semaforo permite ocultar los detalles internos del funcionamiento de cada semáforo. Así, podemos crear múltiples instancias sin preocuparnos por el manejo individual de cada uno.
Al usar una clase, podemos crear tantos semáforos como sea necesario sin duplicar código, simplemente creando nuevas instancias. Cada objeto semáforo maneja su propio estado y tiempos, lo que permite que cada uno funcione de manera independiente.

```c
from microbit import *
import utime

class Semaforo:
    def __init__(self, rojo, amarillo, verde, initState):
        self.state = "Init"
        self.startTime = 0
        self.rojo = rojo
        self.amarillo = amarillo
        self.verde = verde
        self.semaforostate = initState

    def update(self):

        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "WaitTimeoutRojo"
            display.set_pixel(self.rojo["x"], self.rojo["y"], 9)

        elif self.state == "WaitTimeoutRojo":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.rojo["interval"]:
                self.startTime = utime.ticks_ms()
                display.set_pixel(self.rojo["x"], self.rojo["y"], 0)
                display.set_pixel(self.amarillo["x"], self.amarillo["y"], 5)  # Amarillo con intensidad 5
                self.state = "WaitTimeoutAmarillo"

        elif self.state == "WaitTimeoutAmarillo":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.amarillo["interval"]:
                self.startTime = utime.ticks_ms()
                display.set_pixel(self.amarillo["x"], self.amarillo["y"], 0)
                display.set_pixel(self.verde["x"], self.verde["y"], 2)  # Verde con intensidad 2
                self.state = "WaitTimeoutVerde"

        elif self.state == "WaitTimeoutVerde":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.verde["interval"]:
                self.startTime = utime.ticks_ms()
                display.set_pixel(self.verde["x"], self.verde["y"], 0)
                display.set_pixel(self.rojo["x"], self.rojo["y"], 9)
                self.state = "WaitTimeoutRojo"


semaforo1 = Semaforo({"x":0,"y":0,"interval":5000}, {"x":0,"y":1,"interval":2000}, {"x":0,"y":2,"interval":3000}, "Init")
semaforo2 = Semaforo({"x":1,"y":0,"interval":3000}, {"x":1,"y":1,"interval":1000}, {"x":1,"y":2,"interval":2000}, "Init")
semaforo3 = Semaforo({"x":2,"y":0,"interval":4000}, {"x":2,"y":1,"interval":3000}, {"x":2,"y":2,"interval":2000}, "Init")

while True:
    semaforo1.update()
    semaforo2.update()
    semaforo3.update()
    utime.sleep_ms(100)
```
