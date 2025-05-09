#### Solución actividad 8

#### Codigo d5 p5.js 
```c
let bombaEncendida = false;
let chispaTamaño = 10;
let chispaCreciendo = true;
let puertoSerial;
let datosRecibidos = ""; // Almacenará el dato recibido del micro:bit

function setup() {
    createCanvas(600, 600);
    background(200);
    
    // Configuración del puerto serial
    puertoSerial = new p5.SerialPort();
    puertoSerial.list();
    puertoSerial.open('/dev/ttyUSB0'); // Cambiar según el puerto usado
    puertoSerial.on('data', recibirDatos);
}

function draw() {
    background(200);
    dibujarBomba();
}

function dibujarBomba() {
    fill(0);
    ellipse(width / 2, height / 2, 150, 150);

    stroke(0);
    strokeWeight(4);
    line(width / 2, height / 2 - 75, width / 2, height / 2 - 120);

    if (bombaEncendida) {
        fill(255, 100, 0);
        noStroke();
        ellipse(width / 2, height / 2 - 130, chispaTamaño, chispaTamaño);

        if (chispaCreciendo) {
            chispaTamaño += 0.2;
            if (chispaTamaño > 15) chispaCreciendo = false;
        } else {
            chispaTamaño -= 0.2;
            if (chispaTamaño < 10) chispaCreciendo = true;
        }
    }
}

// Función para recibir datos del micro:bit
function recibirDatos() {
    let entrada = puertoSerial.readStringUntil('\n');
    if (entrada) {
        datosRecibidos = entrada.trim();
        if (datosRecibidos === "ON") {
            bombaEncendida = true;
        } else if (datosRecibidos === "OFF") {
            bombaEncendida = false;
        }
    }
}
```

#### Codigo del microbit

```c
from microbit import *
import utime

while True:
    if button_a.is_pressed():
        uart.write("ON\n")
        utime.sleep(0.2)  # Pequeño retraso para evitar múltiples envíos
    elif button_b.is_pressed():
        uart.write("OFF\n")
        utime.sleep(0.2)
```
