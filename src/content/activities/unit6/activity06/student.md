#### Solucion actividad 6
#### ¿Cuál es la función del servidor Node.js en la arquitectura que exploramos? ¿Por qué los clientes p5.js no se comunican directamente entre sí?

El servidor Node.js actúa como intermediario entre todos los clientes p5.js. Su función principal es recibir mensajes de un cliente y reenviarlos a los demás, gestionando así la comunicación en tiempo real de forma centralizada. Los clientes p5.js no se comunican directamente entre sí porque eso requeriría conexiones peer-to-peer, que son más complejas de establecer, mantener y escalar. Node.js, en cambio, simplifica este proceso al mantener un punto central de control, seguridad y sincronización.

#### Explica la diferencia fundamental entre socket.emit() y socket.broadcast.emit() en el contexto de Socket.IO en el servidor. ¿Cuándo usarías cada uno?

socket.emit() envía un mensaje solo al cliente que originó la conexión (es decir, al mismo que envió el evento).

socket.broadcast.emit() envía un mensaje a todos los demás clientes, excepto al que originó el evento.

Usaría socket.emit() cuando quiero responder directamente a un cliente con información específica (como confirmar que su mensaje fue recibido). En cambio, usaría socket.broadcast.emit() cuando un cliente hace algo (como mover un objeto o enviar un dibujo) y quiero que todos los demás vean ese cambio.

#### Compara la comunicación mediante Node.js/Socket.IO con la comunicación serial (ASCII y binaria con framing) que viste en unidades anteriores. Menciona al menos una ventaja y una desventaja de cada enfoque según el contexto de aplicación.

Node.js/Socket.IO

Ventaja: Permite comunicación en tiempo real entre múltiples navegadores conectados en red, ideal para aplicaciones colaborativas como juegos o visualizaciones compartidas.

Desventaja: Requiere conexión a internet o red local, además de un servidor corriendo, lo cual no siempre es posible en contextos desconectados o con hardware limitado.

Comunicación serial (ASCII/binaria)

Ventaja: Es ideal para conectar hardware como el micro:bit a una computadora, ya que es más directa, simple y funciona incluso sin conexión a internet.

Desventaja: Es comunicación punto a punto (entre dos dispositivos), no permite fácilmente múltiples clientes, y la sincronización de datos requiere un protocolo de framing bien definido.

####  ¿Qué rol juega el protocolo HTTP y qué rol juega Socket.IO (que usa WebSockets por debajo) en la aplicación del caso de estudio?

El protocolo HTTP se usa inicialmente para cargar la página web y los scripts (HTML, CSS, JS). Una vez que la página está cargada, Socket.IO, utilizando WebSockets, establece una conexión persistente y bidireccional entre el navegador y el servidor. Esto permite enviar y recibir datos en tiempo real sin necesidad de recargar la página ni hacer múltiples solicitudes HTTP.

####  ¿Qué fue lo más sorprendente o interesante que aprendiste sobre la comunicación en red en esta unidad?

Lo más interesante fue descubrir cómo con unas pocas líneas de código usando Socket.IO se puede construir una aplicación interactiva en red donde varios navegadores se sincronizan en tiempo real. Ver en vivo cómo lo que hace un usuario se refleja al instante en otras pantallas fue muy impactante, especialmente comparado con la comunicación más limitada de la conexión serial con micro:bit.

