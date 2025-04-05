#### Solución actividad 10

#### Estados posibles de la bomba
Bomba apagada: 	No se muestra la chispa
Bomba encendida: Se muestra la chispa animada

#### Eventos y fuentes
Botón A presionado:	Microbit	activa la chispa envía ON
Botón B presionado:	Microbit	apaga la chispa envía OFF
Dato incorrecto recibido:	Microbit	ignorar si el dato no es ON o OFF
Pérdida de conexión:	Microbit / p5js	Si se pierde la conexión, la chispa debe apagarse
Reinicio del microbit:	Microbit	debe mantener el estado de la bomba al reiniciarse
Desconexión de USB:	Microbit / p5js	la bomba debe apagarse y no mostrar la chispa.
Ruido en la señal:	Microbit	si llegan datos corruptos, no debe afectar el comportamiento
