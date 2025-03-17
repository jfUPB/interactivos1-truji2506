#### Solucion actividad 7 
```c
let bombaEncendida = true;
let chispaTamaño = 10;
let chispaCreciendo = true;

function setup() {
    createCanvas(600, 600);
    background(200);
}

function draw() {
    background(200);
    dibujarBomba();
}

function dibujarBomba() {
    // Dibuja el cuerpo de la bomba
    fill(0);
    ellipse(width / 2, height / 2, 150, 150);

    // Dibuja la mecha
    stroke(0);
    strokeWeight(4);
    line(width / 2, height / 2 - 75, width / 2, height / 2 - 120);

    // Dibuja la chispa (animada)
    if (bombaEncendida) {
        fill(255, 100, 0);
        noStroke();
        ellipse(width / 2, height / 2 - 130, chispaTamaño, chispaTamaño);

        // Animación de la chispa
        if (chispaCreciendo) {
            chispaTamaño += 0.2;
            if (chispaTamaño > 15) chispaCreciendo = false;
        } else {
            chispaTamaño -= 0.2;
            if (chispaTamaño < 10) chispaCreciendo = true;
        }
    }
}
```
