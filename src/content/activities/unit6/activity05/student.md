#### Solución actividad 5

####  Punto 5 – Documentación del desarrollo
####  Idea
Mi proyecto es una modificación creativa del caso de estudio original. En lugar de enviar emociones entre clientes, implementé un semáforo interactivo, donde un usuario puede presionar un botón (cliente 1) para solicitar el paso como si fuera un peatón, y otro usuario (cliente 2) ve cómo cambia el semáforo en tiempo real, mostrando los estados rojo, verde y amarillo, junto a una cuenta regresiva.

Esta interacción simula una escena real de cruce peatonal y hace uso de la misma tecnología de comunicación del caso base: Socket.io con servidor Node.js y p5.js en los clientes.

#### Plan de implementación
Cliente 1 (page1.js):
Mostrará un botón "🚶 Pedir paso". Al presionarlo, se emite el evento pedirPaso al servidor.

Servidor (server.js):
Escucha pedirPaso y reemite un evento cambiarSemaforo a todos los clientes conectados.

Cliente 2 (page2.js):
Al recibir cambiarSemaforo, cambia el estado del semáforo de rojo a verde, luego a amarillo y finalmente regresa a rojo, todo esto con temporizadores. También muestra una cuenta regresiva para cruzar.

#### Control de versiones
Fui guardando versiones del código en tres etapas clave:

Estado original (emoción con emojis).

Cambio de nombres de eventos y mensajes (emotion → pedirPaso).

Implementación de lógica de semáforo con estados y temporizadores.

#### Desafíos encontrados y soluciones
Evitar que el botón sea presionado múltiples veces seguidas:
Solución: Usé una variable cambioEnProgreso en page2.js para ignorar nuevos eventos hasta que termine la secuencia del semáforo.

Sincronización visual del semáforo con la cuenta regresiva:
Solución: Guardé el tiempo futuro (cuentaRegresiva) con millis() y calculo el tiempo restante en cada draw().

Cambio fluido entre estados verde → amarillo → rojo:
Solución: Usé setTimeout() encadenados para manejar la secuencia de manera no bloqueante.
