#### Solución actividad 4
En esta actividad tuve algunas dificultades al momento de realizar el codigo me dice que tengo algunos errores aunque en la 
Consola muestra que esta corriendo el codigo, tambien estuve con problema con la conexion aveces me mostraba errores y aveces 
no donde, buscando que enviara mensajes al puerto serial 
```c
let port;
let writer;
let connectBtn;
let buttons = [];

function setup() {
    createCanvas(600, 600);
    background(200);

    connectBtn = createButton('Conectar a micro:bit');
    connectBtn.position(50, 300);
    connectBtn.mousePressed(connectBtnClick);

    let buttonData = [
        { label: 'Aumentar Tiempo (A)', command: 'A', x: 80, y: 100 },
        { label: 'Reducir Tiempo (B)', command: 'B', x: 80, y: 140 },
        { label: 'Agitar (SHAKE)', command: 'SHAKE', x: 80, y: 180 },
        { label: 'Reiniciar (T)', command: 'T', x: 80, y: 220 }
    ];

    buttonData.forEach(data => {
        let btn = createButton(data.label);
        btn.position(data.x, data.y);
        btn.mousePressed(() => sendCommand(data.command));
        buttons.push(btn);
    });

    fill('black');
    ellipse(width / 2, height / 2,200,200);
}

function draw() {
    if (!port) return;
}

async function connectBtnClick() {
    try {
        if (port) {
            await port.close();
            port = null;
            writer = null;
            connectBtn.html('Conectar a micro:bit');
            return;
        }

        port = await navigator.serial.requestPort();
        await port.open({ baudRate: 115200 });
        writer = port.writable.getWriter();
        connectBtn.html('Desconectar');
        console.log('Micro:bit conectado exitosamente.');
    } catch (err) {
        console.error('Error al conectar con el Micro:bit: ', err);
    }
}

async function sendCommand(command) {
    if (writer) {
        const data = new TextEncoder().encode(command + '\n');
        await writer.write(data);
        console.log('Enviado: ' + command);
    } else {
        console.log('Debes conectar el micro:bit primero');
    }
}
```
