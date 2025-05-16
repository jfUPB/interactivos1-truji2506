#### Solución actividad 11

#### Cómo es Posible Mapear los Botones al Movimiento del Círculo
Micro:bit

El Micro:bit detecta cuando se presionan los botones A o B
Al presionar el botón A, envía el mensaje "left", lo que indica que el círculo debe moverse a la izquierda.
Al presionar el botón B, envía el mensaje "right", lo que indica que el círculo debe moverse a la derecha.

#### p5.js:
El programa en p5.js establece una conexión serial con el Micro:bit.
Lee los mensajes enviados por el Micro:bit.
Si recibe el mensaje "left", mueve el círculo hacia la izquierda (disminuyendo su coordenada X).
Si recibe el mensaje "right", mueve el círculo hacia la derecha (aumentando su coordenada X).
El círculo se redibuja en la nueva posición cada vez que se recibe un mensaje.
Flujo de Comunicación
El Micro:bit detecta el botón presionado y envía el mensaje correspondiente ("left" o "right").
El mensaje es recibido por p5.js a través de la comunicación serial.
p5.js procesa el mensaje y mueve el círculo según la dirección indicada.
El círculo se redibuja en la nueva posición.
Este proceso permite mapear la acción de presionar los botones en el Micro:bit para controlar el movimiento del círculo en p5.js.







