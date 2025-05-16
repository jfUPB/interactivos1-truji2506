#### Solucion actividad 3

#### 1. ¿Cuál es la función principal de express.static('public') en este servidor? ¿Cómo se compara con el uso de app.get('/ruta', …) del servidor de la Unidad 6?

La función express.static('public') le indica al servidor que sirva automáticamente cualquier archivo que esté dentro de la carpeta public, sin necesidad de crear rutas individuales para cada archivo HTML, JS o CSS.

En comparación, en la Unidad 6 usábamos app.get('/ruta', (req, res) => { res.sendFile(...) }) para definir manualmente cada ruta y archivo que el servidor debía entregar. Esto es más detallado pero también más tedioso.

Usar express.static es más simple y flexible cuando tenemos varios archivos organizados en carpetas (como mobile/ o desktop/), porque el servidor busca automáticamente index.html dentro de esas rutas.

#### 2. Explica detalladamente el flujo de un mensaje táctil:

¿Qué evento lo envía desde el móvil?
El evento touchMoved() en p5.js del cliente móvil se ejecuta cuando el usuario mueve el dedo. En esa función, se crea un objeto con las coordenadas (x, y), que luego se convierte a JSON con JSON.stringify() y se envía usando socket.emit('message', data).

¿Qué evento lo recibe el servidor?
En el servidor, se escucha ese evento con socket.on('message', (message) => { ... }). Aquí se recibe la cadena JSON enviada por el móvil.

¿Qué hace el servidor con él?
El servidor usa socket.broadcast.emit('message', message) para reenviar el mensaje a todos los demás clientes, excepto al que lo envió (el móvil).

¿Qué evento lo envía el servidor al escritorio?
El servidor emite el mismo evento message, y el cliente de escritorio tiene un socket.on('message', callback) que lo recibe y convierte la cadena de nuevo en objeto con JSON.parse() para usarlo.

¿Por qué se usa socket.broadcast.emit() en lugar de io.emit() o socket.emit()?
Se usa socket.broadcast.emit() porque queremos reenviar el mensaje a todos los demás clientes, pero no al cliente que lo envió.

socket.emit() enviaría el mensaje solo al mismo cliente.

io.emit() lo enviaría a todos, incluido el emisor.

socket.broadcast.emit() es ideal para este caso, ya que excluye automáticamente al emisor.

#### 3. Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?

Los dos computadores de escritorio recibirían el mensaje, pero no el móvil. Esto es porque el servidor está usando socket.broadcast.emit(), que excluye al cliente que envió el mensaje (el móvil) y lo manda a los demás.

Esto permite que los dispositivos receptores (como los escritorios) respondan a los eventos táctiles del móvil sin que el móvil reciba su propio mensaje.

#### 4. ¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?

Los console.log en el servidor sirven para:

Ver cuándo un nuevo cliente se conecta, junto con su socket.id.

Ver exactamente qué mensaje se recibe y desde qué cliente.

Saber cuándo un cliente se desconecta.

Esto es útil para verificar que el servidor está funcionando, depurar errores, y entender quién está enviando qué en tiempo real. También permite monitorear si hay clientes que se caen o se reconectan.
