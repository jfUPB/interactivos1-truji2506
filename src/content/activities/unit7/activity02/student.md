#### Solucion actividad 2
#### ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?

Dev Tunnels es necesario porque el servidor Node.js corre en localhost, lo que significa que solo es accesible desde mi propio computador. Si intento acceder desde el celular, este buscará un servidor en su propio localhost, no en el de mi PC.

Dev Tunnels crea una URL pública accesible desde internet, y actúa como un túnel que redirecciona las conexiones externas hacia mi servidor local en el puerto 3000. Es como tener una línea directa temporal para que mi celular pueda hablar con mi computador sin que estén en la misma red.

#### ¿Por qué usamos JSON.stringify() en el emisor (móvil) y JSON.parse() en el receptor (escritorio)? ¿Qué problema resuelve JSON aquí?

JSON.stringify() convierte un objeto JavaScript (por ejemplo, { x: 100, y: 200 }) en una cadena de texto para poder enviarlo por la red. Socket.IO no puede enviar directamente objetos, pero sí cadenas de texto.

Luego, en el cliente receptor, usamos JSON.parse() para convertir esa cadena de texto de nuevo en un objeto utilizable. Esto nos permite acceder a las coordenadas como data.x y data.y.

Sin esto, tendríamos que enviar los datos como texto plano (como "100,200"), lo cual es menos flexible y más difícil de manejar si queremos enviar más información en el futuro.

#### Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.

touchMoved() es una función de p5.js que se ejecuta automáticamente cada vez que el usuario arrastra el dedo sobre la pantalla.

Se usa threshold para evitar enviar demasiados mensajes cuando el movimiento es muy pequeño o casi imperceptible. Si enviáramos datos con cada mínimo temblor del dedo, la red se llenaría de mensajes innecesarios, lo que podría generar más latencia o congestión.

Con threshold, el sistema solo envía datos cuando el dedo se ha movido una cierta distancia desde la última vez, lo que mejora el rendimiento.

#### ¿Qué otros eventos táctiles existen en p5.js y para qué tipo de interacciones podrían ser útiles?

touchStarted(): Se ejecuta cuando el usuario toca la pantalla por primera vez. Útil para detectar un tap o iniciar una acción (como presionar un botón virtual).

touchEnded(): Se ejecuta cuando el usuario levanta el dedo. Sirve para terminar una acción o liberar un botón.

touchMoved(): (ya lo usamos) para seguir el dedo mientras se mueve.

Estos eventos permiten crear interacciones complejas como botones, sliders o gestos en pantalla.

Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?

#### Método	Ventajas	Desventajas
IP local	Rápido y no necesita conexión externa	Solo funciona si ambos dispositivos están en la misma red y no hay firewalls
Dev Tunnels	Funciona desde cualquier red (incluso datos móviles) y es segura	Puede ser más lento y necesita conexión a internet y VS Code

En mi caso, Dev Tunnels fue esencial porque no siempre tenía ambos dispositivos en la misma red o el firewall bloqueaba la IP local.
