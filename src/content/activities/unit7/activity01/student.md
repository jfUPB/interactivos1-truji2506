#### Solucion actividad 1
#### Pasos de configuración realizados:
Cloné el repositorio del caso de estudio y abrí la carpeta en VS Code.

En la terminal, ejecuté npm install para instalar las dependencias (express y socket.io).

#### Inicié el servidor con npm start. Apareció el mensaje:
Server is listening on http://localhost:3000

Usé la función "Forward a Port (Dev Tunnels)" en VS Code:

Puerto: 3000

#### Visibilidad: 
Public

URL generada:
https://tu-nombre.use2.devtunnels.ms (la mía fue diferente, pero similar).

#### Desde el navegador del PC accedí a:
http://localhost:3000/desktop/ → vi el círculo rojo.

#### Desde el celular, accedí a:
https://mi-url-de-devtunnels.use2.devtunnels.ms/mobile/ → apareció el mensaje "Touch to move the circle".

Al tocar y mover el dedo en el celular, el círculo en el computador se movía con algo de retraso (latencia leve).

#### ¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos esta URL en lugar de localhost o IP local?
Obtuve una URL similar a:
https://<mi-url>.use2.devtunnels.ms/

Necesitamos usar esta URL porque localhost solo funciona dentro del mismo dispositivo. El celular no puede acceder al localhost del computador. Dev Tunnels expone el servidor de Node.js a internet, generando una URL pública que sí puede ser accedida desde otros dispositivos, como el celular.

#### ¿Qué hace npm install y npm start?
npm install: descarga e instala todas las dependencias listadas en package.json, como express y socket.io.

npm start: ejecuta el archivo server.js si está configurado en el campo "start" del package.json.

#### ¿Qué mensajes observaste en la terminal del servidor?
Al conectar el cliente de escritorio y móvil, vi mensajes como:

Copiar
Editar
New client connected
Received message => {"x": 123, "y": 456}
Client disconnected
Cada cliente tenía un identificador diferente, pero ambos producían mensajes similares al conectarse o desconectarse. Cuando tocaba la pantalla del móvil, aparecían los valores x e y.

#### ¿Funcionó la interacción? ¿Hubo latencia?
Sí, la interacción funcionó: al mover el dedo en el celular, el círculo en la página del PC se movía.
Hubo un poco de retraso (latencia), especialmente cuando la conexión no era muy estable.

#### ¿Cerraste el puerto? ¿Por qué es importante hacerlo?
Sí, cerré el puerto al terminar.
Es importante cerrarlo para evitar que tu servidor siga siendo accesible públicamente, lo cual representa un riesgo de seguridad y consume recursos innecesarios.
