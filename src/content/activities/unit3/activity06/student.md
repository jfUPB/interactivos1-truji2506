#### Solución acitividad 6

#### Conexión y Desconexión del microbit
1.  Si el micro:bit está desconectado y presiono el botón Conectar a microbit, el sistema debe conectar el dispositivo y mostrar Desconectar.
Fallo: A veces no conecta y muestra el error: Error al conectar con el Microbit.
Correccion: Verificar que el navegador tenga permisos para acceder a dispositivos seriales.
2.  Si el microbit esta conectado y presiono el botón Desconectar, el sistema debe cerrar la conexion y cambiar el boton a Conectar a microbit.
Fallo: El boton no cambia a conectar al desconectar.
Corrección: Asegurarse de que el objeto port se cierre correctamente usando await port.close();.

#### Envío de Comandos
3.  Si el microbit esta conectado y presiono el boton Reducir Tiempo (B), el sistema debe enviar el comando B y mostrar Enviado B en la consola.
Fallo: El comando no se imprime en la consola.
Correccion: Añadir un bloque catch para capturar errores de escritura.

4.  Si el microbit está conectado y presiono el botón Agitar (SHAKE), el sistema debe enviar el comando SHAKE y mostrar Enviado: SHAKE en la consola.
Fallo: No se detecta el comando en el microbit.
Corrección: Asegurarse de que el micro:bit interprete correctamente el comando SHAKE.


