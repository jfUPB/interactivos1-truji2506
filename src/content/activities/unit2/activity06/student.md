#### Solución actividad 6 

En esta actividad elaboré un codigo donde se mostraba 3 imagenes en el micro bit, donde se evidenciaba un corazon, una cara feliz y ademas una cara enojada

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
