#### Solucion actividad 4
####  Explicación del código
#### setup(): Establece conexión con el servidor usando io() y define qué hacer cuando llega un mensaje:

socket.on('message', (data) => { ... });
socket.on('message', ...):

Recibe el mensaje JSON como texto (data).

Lo intenta convertir en un objeto con JSON.parse(data).

Verifica si es un mensaje de tipo 'touch'.

Si es válido, actualiza las coordenadas circleX y circleY.

draw():

Se ejecuta continuamente y dibuja el fondo y un círculo rojo en la posición actualizada.

#### Reflexión (Escritorio)
#### ¿Por qué usar JSON.parse() dentro de try...catch?
Porque si el mensaje no es un JSON válido, JSON.parse() lanzaría un error que detendría la ejecución del script. El bloque try...catch previene que el programa se bloquee y permite detectar errores de forma segura.

#### ¿Qué pasa si los canvas tienen tamaños diferentes?
Para ajustar proporcionalmente, se puede usar la función map():

circleX = map(parsedData.x, 0, 300, 0, width);
circleY = map(parsedData.y, 0, 300, 0, height);
Esto convierte las coordenadas de un canvas móvil de 300x300 a uno de escritorio, por ejemplo, de 600x600.

#### ¿Qué cambiar si el servidor emite updateDesktop en lugar de message?
#### Se debe cambiar el listener:

socket.on('updateDesktop', (data) => { ... });
El resto del código dentro del callback podría mantenerse igual si el formato de data no cambia.
