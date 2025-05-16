#### Solución actividad 4 
#### 1. Conexión inicial
Prueba:

Abriste page2.html, luego detuviste el servidor y refrescaste.

Observaciones esperadas:

En la consola aparece un error de conexión WebSocket. Algo como:
"WebSocket connection to 'ws://localhost:3000/socket.io/…' failed"

¿Qué indica esto?:

Que el cliente intentó conectarse al servidor en localhost:3000, pero no lo encontró activo.

Cuando reinicias el servidor y refrescas:

El error desaparece y se imprime:
"Connected to server - My ID: …"

#### Conexión establecida y envío de estado inicial
Prueba:

Comentaste la línea socket.emit('win2update', currentPageData, socket.id);.

Observación:

Al iniciar page2, no se envía su estado inicial.

En page1, no aparece nada sobre page2 hasta que mueves page2.

Reflexión:

Enviar el estado inicial al conectarse es útil porque permite que los otros clientes (o el servidor) ya tengan una idea de su posición y dimensiones sin esperar a que haya cambios. Mejora la sincronización desde el comienzo.

#### Recepción de datos
Prueba:

Mueves page1, observas consola en page2.

Observación esperada:

Se imprime:
"Page 2 received data about the other window: …"

Si mueves page2:

No aparece ese mensaje, porque page2 solo recibe, el mensaje getdata viene del servidor cuando page1 envía un cambio.

Reflexión:

Este diseño evita redundancia: cada cliente escucha los cambios de los demás, no los propios.

#### Detección de cambios
Observación:

Solo aparece "Page 2 detected change…” cuando realmente hay cambios de posición o tamaño.

Reflexión:

Esta estrategia es eficiente porque reduce el tráfico de red: no envía datos si la ventana está quieta.

Útil cuando tienes muchos clientes conectados: evita saturar el servidor con datos innecesarios.

#### Visualización
Modificaciones propuestas:

Color del fondo basado en distancia:
```c
let distancia = resultingVector.mag();
background(map(distancia, 0, 1000, 255, 0));
```
Resultado: Cuanto más lejos esté la otra ventana, más oscuro se ve el fondo. Da una sensación de "lejanía".

Tamaño del círculo local depende del ancho de la ventana remota:

```c
let tamaño = map(remotePageData.width, 0, 1500, 50, 300);
drawCircle(point2[0], point2[1], tamaño);
```
Resultado: Permite ver gráficamente si la ventana remota está muy ancha o estrecha.

Color de línea cambia si está a la izquierda o derecha:
```c
if (resultingVector.x < 0) {
    stroke('blue');
} else {
    stroke('red');
}
```
Resultado: Da una indicación visual clara de la posición relativa.

Reflexión final:

Este tipo de visualizaciones permiten crear experiencias colaborativas interactivas, donde varias ventanas o dispositivos pueden verse entre sí en tiempo real. Puede usarse en arte interactivo, juegos cooperativos o instalaciones educativas.
