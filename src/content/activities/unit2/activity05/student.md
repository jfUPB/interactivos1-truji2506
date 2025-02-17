#### Solución actividad 5

##### Explicación del codigo
Inicializamos la comunicación serial con uart.init(baudrate=115200)
verificamos si hay datos disponibles con uart.any()
Se pone la variable para almacenar el ultimo dato recibido con ultimo_caracter = "?"
Nos aseguramos que solo lea 1 bit data = uart.read(1)  
Y ademas pasamos el ultimo_Caracter a un String 
Me aseguro que presionando la tecla A del caracter nos muestre el feedback del microbit 


´´´c
from microbit import *
uart.init(baudrate=115200)
ultimo_caracter = "?"
while True:
    if uart.any():
        data = uart.read(1)  
        if data:
            ultimo_caracter = data.decode('utf-8') 
    if button_a.is_pressed():
        display.show(ultimo_caracter.upper()) 
    else:
        display.clear()  # Borra la pantalla cuando se suelta el botón
    ```


