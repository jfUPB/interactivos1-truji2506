#### Solución actividad 6

##### Punto 15: Presiona los botones A y B del micro:bit. ¿Qué pasa?
Al presionar el botón A, el programa en el micro:bit envía el carácter A a través del puerto serial. El programa en p5.js detecta este carácter y cambia el color del círculo en la pantalla a rojo. Similarmente, al presionar el botón B, se envía el carácter B, y el círculo cambia de color a amarillo.

##### ¿Cómo se logra?
Según mi investigación:
La función button_a.is_pressed() detecta si el botón A está siendo presionado.
Si es presionado, el carácter 'A' se envía mediante la función uart.write('A').
El mismo proceso ocurre para el botón B con el carácter 'B'.

En p5.js:
La función port.availableBytes() verifica si hay datos disponibles en el puerto serial.
Si hay datos, la función port.read(1) lee un byte (carácter) enviado por el micro:bit.
Según el carácter recibido ('A' o 'B'), se cambia el color del círculo en el lienzo.

##### Punto 16: Sacude el micro:bit. ¿Qué pasa?
Al sacudir el micro:bit, el sensor de aceleración detecta el gesto shake. Esto hace que el micro:bit envíe el carácter C al puerto serial. En p5.js, este carácter hace que el círculo cambie su color a verde.

##### ¿Cómo se logra?
Según mi investigación:

En el micro:bit :
El método accelerometer.was_gesture(shake) detecta el gesto de sacudida.
Si ocurre el gesto, se envía el carácter C mediante uart.write (C).

En p5.js:
Similar al punto anterior, el programa detecta el carácter C enviado por el micro:bit.
El color del círculo cambia a verde al recibir este carácter.

##### Punto 17: Presiona el botón "Send Love". ¿Qué pasa?
Al presionar el botón Send Love en la interfaz de p5.js, se envía el carácter h al micro:bit. En el micro:bit, al recibir este carácter, se muestra un corazón en la pantalla LED, seguido de una cara feliz.

##### ¿Cómo se logra?

En p5.js:
La función sendBtnClick() es llamada al presionar el botón "Send Love".
Esta función utiliza port.write('h') para enviar el carácter 'h' al micro:bit.

En el micro:bit :
La función uart.any() verifica si hay datos recibidos en el puerto serial.
Si hay datos, se leen mediante uart.read(1) y se comprueba si corresponden al carácter 'h' (ord('h')).
Si coincide, el micro:bit muestra una imagen de corazón (Image.HEART) seguida de una imagen de cara feliz (Image.HAPPY).





