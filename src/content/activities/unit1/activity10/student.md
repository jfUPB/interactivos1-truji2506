#### Solución acitividad 10

```c
let squareColor = [255, 0, 0]; // Color inicial
let serial; // Objeto para la conexión serial
let port;

function setup() {
  createCanvas(400, 400);
  noLoop(); // Solo dibujar cuando sea necesario

  // Crear botón para conectar el Micro:bit
  let connectButton = createButton('Conectar Micro:bit');
  connectButton.position(10, 10);
  connectButton.mousePressed(connectMicrobit);
}

function draw() {
  background(220);
  fill(squareColor);
  rect(150, 150, 100, 100); // Dibuja el cuadrado
}

async function connectMicrobit() {
  try {
    port = await navigator.serial.requestPort(); // Solicitar puerto serial
    await port.open({ baudRate: 9600 }); // Abrir puerto a 9600 baudios

    serial = port.readable.getReader(); // Crear lector
    listenToSerial(); // Iniciar escucha de datos
  } catch (err) {
    console.error('Error al conectar:', err);
  }
}

async function listenToSerial() {
  while (true) {
    const { value, done } = await serial.read();
    if (done) break;

    // Decodificar datos recibidos y mostrarlos en la consola
    const data = new TextDecoder().decode(value).trim();
    console.log(`Dato recibido: ${data}`); // Depuración

    if (data === 'changeColor') {
      squareColor = [random(255), random(255), random(255)];
      redraw(); // Actualizar dibujo
    }
  }
}
```

#### Proceso de Conexión y Comunicación
Micro:bit:
Envía el mensaje "changeColor" al puerto USB cuando se presiona el botón A, usando serial.writeLine().
p5.js:

##### Establece la conexión al Micro:
bit mediante la Web Serial API.
##### Escucha los datos enviados por el Micro:
bit. Si recibe "changeColor", cambia el color del cuadrado en pantalla.
##### Resumen del Flujo:
Botón A → Micro:bit envía mensaje → p5.js procesa mensaje → Cambia color del cuadrado.
