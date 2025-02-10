#### Solución actividad 4 

##### Experimento 1: Detección del botón A

###### ¿Que quiero comprobar?
Quiero comprobar si el micro:bit detecta correctamente cuando se presiona el boton A y si puedo mostrar un mensaje en la matriz de Leds en respuesta.

###### ¿Cual fue mi hipotesis?
Si presiono el boton A, la pantalla debería mostrar la letra A y al soltarlo, los leds deberian apargarse

###### Codigo del experimiento 
```c
from microbit import *

while True:
    if button_a.is_pressed():
        display.show("A")
    else:
        display.clear()
````
###### Descripcion del resultado
Cuando presione el boton A la pantalla mostro la letra A Al soltarlo, la pantalla se apago.

###### Análisis de los resultados:
El dispositivo detecta correctamente cuando el boton A es presionado gracias a la funcion button_a.is_pressed() y como el codigo se encuentra en un bucle while True, verifica continuamente el estado del boton, actualizando los leds en tiempo real.

###### Conclusión
El micro:bit responde en tiempo real a la presión del botón A, lo que permite crear interacciones dinámicas en juegos o aplicaciones interactivas.

##### Experimento 2: Detección del botón B

###### ¿Que quiero comprobar?
Quiero comprobar si el micro:bit detecta correctamente cuando se presiona el boton B y si puedo mostrar un mensaje en la matriz de Leds en respuesta.

###### ¿Cual fue mi hipotesis?
Si presiono el boton B, la pantalla debería mostrar la letra A y al soltarlo, los leds deberian apargarse

###### Codigo del experimiento
```c
from microbit import *

while True:
    if button_b.is_pressed():
        display.show("B")
    else:
        display.clear()
````
###### Descripcion del resultado
Cuando presione el boton B la pantalla mostro la letra A Al soltarlo, la pantalla se apago.

###### Análisis de los resultados:
El dispositivo detecta correctamente cuando el boton B es presionado gracias a la funcion button_a.is_pressed() y como el codigo se encuentra en un bucle while True, verifica continuamente el estado del boton, actualizando los leds en tiempo real.

###### Conclusión
El micro:bit responde en tiempo real al presionar el boton B, lo que permite crear interacciones dinamicas en juegos o aplicaciones interactivas.

##### Experimento 3: Detección del botón virtual del logo

###### ¿Que quiero comprobar?
Quiero verificar si el micro:bit detecta cuando se toca el logo y si puedo mostrar la letra L en la pantalla.

###### ¿Cual fue mi hipotesis?
Si toco el logo del micro:bit, la pantalla mostrará la letra L.

###### Codigo del experimiento
```c
from microbit import *

while True:
    if pin_logo.is_touched():
        display.show("L")
    else:
        display.clear()
````
###### Descripcion del resultado
Cuando toque el logo del micro:bit, la pantalla mostro la letra L y al soltarlo, la pantalla se apago.

###### Análisis de los resultados:
El logo actua como un sensor tactil lo que significa que detecta la proximidad de mi dedo. La funcion pin_logo.is_touched() detecta esta interaccion y permite responder a ella en tiempo real. Ademas funciona similar al button_a.is_pressed()

###### Conclusión
El boton virtual del logo amplia las opciones de entrada en el micro:bit, permitiendo interacciones tactiles sin botones fisicos.











