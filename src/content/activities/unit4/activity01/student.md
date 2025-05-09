#### Solucion actividad 1

#### Enlace del ejemplo 
https://openprocessing.org/sketch/2588143

Me llamo la atención  por su creatividad visual, su fluidez en la animación o la manera en que usa interactividad con el usuario. También me fue el uso eficiente de código para generar un efecto llamativo.

#### Análisis del Sketch en p5.js
El sketch usa varias funciones clave de p5.js para crear y animar círculos que interactúan con el mouse, generando un efecto de conexión suave entre ellos.

#### Funciones principales de p5.js utilizadas:
createCanvas(): Define el tamaño del lienzo.

fill(), noStroke(): Configuran el color y los bordes de los objetos.

circle(): Dibuja los círculos en la cuadrícula.

mouseX, mouseY: Capturan la posición del mouse para mover un círculo.

beginShape(), endShape(), bezierVertex(): Dibujan las conexiones suaves entre los círculos.

#### Técnicas de programación aplicadas:
Uso de arreglos: Se almacenan los círculos en un array para gestionarlos fácilmente.

Estructura de datos con objetos: Cada círculo es un objeto con posición, radio y color.

Interactividad: Un círculo sigue la posición del mouse.

Funciones matemáticas: dist(), atan2(), acos() calculan distancias y ángulos para conectar los círculos de forma fluida.

#### Explicación de los cambios
#### Colores dinámicos

En draw(), los colores de los círculos cambian con el tiempo usando sin(frameCount * 0.02), lo que da un efecto de pulsación.

#### Círculo del mouse con tamaño variable

Se calcula la velocidad del mouse y se usa constrain() para ajustar el tamaño del círculo en draw().

#### Conexiones más suaves

maxDistance aumentó de 100 a 120, permitiendo más conexiones.

lerpColor() mezcla los colores de las conexiones para una mejor integración visual.

#### Los cambios hicieron el código más dinámico y atractivo:

Colores dinámicos: Agrega variedad visual con cambios suaves.

Tamaño del círculo del mouse variable: Hace la interacción más natural.

Conexiones más suaves: Mejora la estética y fluidez del diseño.

#### URL de p5.js 
https://editor.p5js.org/josetrujillo631/sketches/0C86cZylQ

