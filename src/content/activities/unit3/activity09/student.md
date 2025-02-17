#### Solución actividad 9

```c
from microbit import *
import utime

class Semaforo:
    def __init__(self,rojo,amarillo,verde, initState):
        self.state = "Init"
        self.startTime = 0
        self.rojo = rojo
        self.amarillo= amarillo
        self.verde= verde
        self.semaforostate= initState

    def update(self):

        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "WaitTimeoutRojo"
            display.set_pixel(self.rojo["x"],self.rojo["y"],9)
            
        elif self.state == "WaitTimeoutRojo":
            if utime.ticks_diff( utime.ticks_ms() , self.startTime) > self.rojo["interval"]: 
                self.startTime = utime.ticks_ms()
                display.set_pixel(self.rojo["x"],self.rojo["y"],0)
                display.set_pixel(self.amarillo["x"],self.amarillo["y"],9)
                self.state = "WaitTimeoutAmarillo"

        elif self.state == "WaitTimeoutAmarillo":
            if utime.ticks_diff( utime.ticks_ms() , self.startTime) > self.amarillo["interval"]: 
                self.startTime = utime.ticks_ms()
                display.set_pixel(self.amarillo["x"],self.amarillo["y"],0)
                display.set_pixel(self.verde["x"],self.verde["y"],9)
                self.state = "WaitTimeoutVerde"
                
        elif self.state == "WaitTimeoutVerde":
            if utime.ticks_diff(utime.ticks_ms(), self.startTime) > self.verde["interval"]:
                self.startTime = utime.ticks_ms()
                display.set_pixel(self.verde["x"], self.verde["y"],0)
                display.set_pixel(self.rojo["x"], self.rojo["y"],9)
                self.state = "WaitTimeoutRojo"


semaforo = Semaforo({"x":0,"y":0,"interval":1000},{"x":0,"y":1,"interval":1000},{"x":0,"y":2,"interval":1000},"Init")

while True:
    semaforo.update()
    utime.sleep_ms(100)

```
