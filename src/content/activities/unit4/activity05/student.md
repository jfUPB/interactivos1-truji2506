#### Solución actividad 5 


#### Muestra el código de p5.js para la versión modificada.
```c
let c;
let prevX = 0;
let prevY = 0;

let port;
let connectBtn;
let microBitConnected = false;

const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAITMICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};
let appState = STATES.WAIT_MICROBIT_CONNECTION;
let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(255);
  strokeWeight(2);
  c = color(0); // color inicial: negro

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(connectBtnClick);
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
  } else {
    port.close();
  }
}

function updateButtonStates(newAState, newBState) {
  if (newBState === false && prevmicroBitBState === true) {
    // Cambiar color aleatorio al soltar botón B
    c = color(random(255), random(255), random(255));
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}

function draw() {
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");
    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length == 4) {
          microBitX = int(values[0]) + windowWidth / 2;
          microBitY = int(values[1]) + windowHeight / 2;
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
          updateButtonStates(microBitAState, microBitBState);
        } else {
          print("No se están recibiendo 4 datos del micro:bit");
        }
      }
    }
  }

  switch (appState) {
    case STATES.WAIT_MICROBIT_CONNECTION:
      if (microBitConnected) {
        print("Microbit listo para dibujar");
        noCursor();
        appState = STATES.RUNNING;
        prevX = microBitX;
        prevY = microBitY;
      }
      break;

    case STATES.RUNNING:
      if (!microBitConnected) {
        print("Esperando microbit...");
        cursor();
        appState = STATES.WAIT_MICROBIT_CONNECTION;
      }

      if (microBitAState === true) {
        stroke(c);
        line(prevX, prevY, microBitX, microBitY);
      }

      prevX = microBitX;
      prevY = microBitY;
      break;
  }

}

function keyReleased() {
  if (key === "s" || key === "S") {
    saveCanvas("dibujo_" + Date.now(), "png");
  }
  if (keyCode === DELETE || keyCode === BACKSPACE) background(255);
}
```
#### Enlace a la aplicación modificada en el editor de p5.js.
https://editor.p5js.org/truji2506/sketches/jW8Gzn9ga


#### Muestra capturas de pantalla del canvas de tu aplicación modificada.

![image](https://github.com/user-attachments/assets/1bc6dd7d-3c18-4baa-88da-76b8b30334b4)
