#### Solución Acitivdad 8  

El codigo usa una clase Pixel que controla el estado de un pixel en la pantalla del micro:bit
Cada pixel cambia el estado de encendido y apagado segun el tiempo que se especifica en el codigo

##### La clase pixel tiene unos atributos donde tiene:

State: Que es el estado actual del pixel
StartTime: Que es el momento donde se inicio
Interval: Es el tiempo que debe de pasar para cambiar su estado encendido a apagado
Pixelx y Pixely: Coordenadas del pixel en la pantalla del microbit
pixelstate: el estado del pixel si esta encendido 9 y si esta apagado 0

##### Metodos que se implementaron en el codigo 

Init(): Este inicializa un pixel con su posicion, estado inicial y el intervalo del cambio 
Update(): Este cambia el estado del pixel segun el tiempo transcurrido 

#### Estados del pixel 
Init: Este inicia el pixel, enciende en el estado inicial y se cambia a WaitTimeuot
WaitTimeout: se espera hasta que pase el tiempo definido en el interval para cambiar el estado del pixel 

#### Eventos y Acciones
Evento: Este verifica si ha pasado tiempo interval desde el StartTime
Accion: Si el tiempo ha pasado, se cambia el estado del pixel pixelState entre 0 y 9

#### Loop principal While True
Se crea dos objetos pixel
pixel1 en 0,0 con intervalo de 1s (1000ms)
pixel2 en 4,4 con intervalo de 0.5s (500ms)

Se llama a Update() en cada iteracion, lo que permite que cada pixel parpadee de forma intermitente






