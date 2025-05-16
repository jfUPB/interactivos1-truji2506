#### Solucion actividad 12 

#### Declaración de variables globales
Aquí declaramos tres variables:

##### port:
Para manejar la conexión serial con la micro:bit.
##### connectBtn: 
Botón para conectar/desconectar la micro:bit.
##### buttons: 
Un array donde guardaremos los botones dinámicamente.

#### setup() - Configuración inicial
*Crea un lienzo donde se mostrará información visual.
*Inicializa port para manejar la comunicación con la micro:bit.
*Crea un botón para conectar y desconectar la micro:bit.
*Define un array buttonData con la información de cada botón.
*Usa forEach() para crear cada botón de manera automática.
*Cada botón al ser presionado enviará un comando diferente a la micro:bit.
*Si presionas el botón "Heart", se enviará la letra "h" a la micro:bit
*Lee Datos de la micro:bit y cambia los colores dependiendo el valor recibido.
*Dibuja un circulo en la pantalla para representar el estado del sistema
*Muestra el carácter recibido en el centro de la pantalla
*Cambia el texto del botón dependiendo de si la conexión está activa o no.
* Si la micro:bit envía "A", el color de la elipse será rojo
* Si envia "B", el color de la elipse será amarillo
* Si enviar "C", el color será verde
* Si el puerto no está abierto, lo abre para comunicarse con la micro:bit
* Si el puerto ya está abierto, lo cierra
```c
let port;
let connectBtn;
let buttons = [];

function setup() {
    createCanvas(600, 600);
    background(200);

    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);

    let buttonData = [
        { label: 'FABULOUS', command: 'p', x: 80, y: 180 },
        { label: 'HEART', command: 'h', x: 80, y: 100 },
        { label: 'HAPPY', command: 'i', x: 80, y: 120 },
        { label: 'ALL_ARROWS', command: 'q', x: 80, y: 140 },
        { label: 'ANGRY', command: 'a', x: 80, y: 160 }
    ];

    buttonData.forEach(data => {
        let btn = createButton(data.label);
        btn.position(data.x, data.y);
        btn.mousePressed(() => sendCommand(data.command));
        buttons.push(btn);
    });

    fill('white');
    ellipse(width / 2, height / 2, 100, 100);
}

function draw() {
    if (port.availableBytes() > 0) {
        let dataRx = port.read();
        if (dataRx === 'A') {
            fill('red');
        } else if (dataRx === 'B') {
            fill('yellow');
        } else {
            fill('green');
        }
        background(220);
        ellipse(width / 5, height / 2, 50, 100);
        fill('black');
        textSize(20);
        text(dataRx, width / 2 - 5, height / 2);
    }

    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function sendCommand(command){
  if (port.opened()) {
    port.write(command);
  }
  else{
    print("Debes conectar el micro:bit")
  }
}

```



```c
from microbit import *

uart.init(baudrate=115200)
display.show(Image.FABULOUS)

while True:
    if button_a.is_pressed():
        uart.write('A')
        sleep(200)  
    if button_b.is_pressed():
        uart.write('B')
        sleep(200)
    if accelerometer.was_gesture('shake'):
        uart.write('C')
        sleep(200)

    if uart.any():
        data = uart.read(1)
        if data:
            char = data.decode('utf-8')
            if char == 'h':
                display.show(Image.HEART)
                sleep(200)  
            elif char == 'i':
                display.show(Image.HAPPY)
                sleep(200)  
            elif char == 'q':
                display.show(Image.ALL_ARROWS)
                sleep(200)  
            elif char == 'a':
                display.show(Image.ANGRY)
                sleep(200)  


function sendCommand(command) {
    if (port.opened()) {
        port.write(command);
    }
}
```
