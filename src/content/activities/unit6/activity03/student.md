#### Solución actividad 3 
#### 1. Reflexiona sobre el uso de módulos o librerías
#### ¿Por qué es útil usar módulos en lugar de escribir todo desde cero?

Ahorra tiempo: las librerías ya están optimizadas y probadas.

Fiabilidad: usan código que ha sido testeado por la comunidad.

Organización: permiten separar responsabilidades (servidor, rutas, sockets).

Comunidad: hay documentación, foros, y soporte disponibles.

#### Cambiar la carpeta estática
#### ¿Qué pasa si cambias 'views' por 'archivos_cliente' (una carpeta que no existe)?

El servidor inicia, pero al abrir http://localhost:3000/page1.html aparece un error 404 (Archivo no encontrado).

En la consola del navegador: error de carga (Failed to load resource) y GET http://localhost:3000/page1.html 404 (Not Found).

El navegador no encuentra el archivo porque esa carpeta no existe o no contiene los archivos esperados.

Express sirve estáticos sólo desde la carpeta especificada y no busca fuera de ella.

#### Cambiar ruta /page1 a /pagina_uno
Si visitas http://localhost:3000/page1, no funciona (404).

http://localhost:3000/pagina_uno sí funciona.

Las rutas son literalmente las definidas en el código. El servidor no "adivina" lo que quieres, responde exactamente a lo que programas con app.get.

#### Conexiones de Socket.IO
Al abrir page1, en la terminal aparece:
A user connected - ID: <un_id_unico>

Al abrir page2, aparece otro ID distinto.

Al cerrar una pestaña, aparece:
User disconnected - ID: <id_correspondiente>

Cada cliente tiene su propio socket.id. Puedes rastrear y manejar clientes individualmente.

#### Escuchar eventos de clientes
Mover page1 → en terminal se muestra:
Received win1update from ID: ... Data: {x:..., y:..., width:..., height:...}

Mover page2 → aparece evento win2update con datos correspondientes.

¿Qué pasa si cambias socket.broadcast.emit por socket.emit?

Solo el emisor recibe el mensaje getdata, los demás no.

El otro cliente (por ejemplo page2) no se actualiza.

socket.emit → mensaje solo para ese cliente.

socket.broadcast.emit → mensaje para todos menos el que lo envió.
Esto es clave para comunicación colaborativa.

#### Cambiar el puerto
Cambiar a const port = 3001; → al iniciar:
Server is listening on http://localhost:3001

http://localhost:3000/page1 → no funciona (servidor no está ahí).

http://localhost:3001/page1 → sí funciona.

Lección: La variable port define dónde escucha el servidor. El navegador debe hacer las peticiones al mismo puerto donde corre el servidor.
