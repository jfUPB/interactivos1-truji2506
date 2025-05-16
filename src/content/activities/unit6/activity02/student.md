#### Solución actividad 2
#### Pausa activa 1: Tu conexión a Internet
#### ¿Qué pasaría si se corta tu rampa de acceso (Wi-Fi o cable de red)?
Si se corta mi conexión a Internet, ya sea por Wi-Fi o por cable, mi navegador no podrá comunicarse con ningún servidor. Es como si mi “vehículo” quedara atrapado en el garaje sin poder salir a las carreteras digitales. No podría acceder a sitios web, enviar correos, ver videos o usar servicios en línea. Todo lo que dependa de Internet dejaría de funcionar hasta que se restablezca la conexión.

#### Pausa activa 2: Ejemplos de Cliente-Servidor en la vida diaria
#### ¿Qué ejemplos encuentras fuera del mundo digital?
Un ejemplo claro es un restaurante. El cliente soy yo, cuando me siento a pedir algo del menú. El camarero es el servidor, quien recibe mi pedido, lo transmite a la cocina y luego me trae la comida. Yo hago una “petición” y el servidor me da una “respuesta” en forma de comida. Otro ejemplo podría ser cuando pido un paquete en línea: yo soy el cliente, la tienda es el servidor.

#### Pausa activa 3: Desglosar una URL
#### Toma una URL y analízala. ¿Qué pasa si solo escribes el dominio?

URL: https://www.youtube.com/watch?v=abc123

Protocolo: https://

Dominio: www.youtube.com

Ruta: /watch?v=abc123

Si solo escribo www.youtube.com sin la ruta, el servidor me dirige a una página de inicio o portada por defecto, que en este caso es la página principal de YouTube. Esa página por defecto suele ser algo como index.html, aunque no siempre se ve en la URL.

#### Pausa activa 4: Comparación de HTTP con protocolos seriales
#### ¿Similitudes, diferencias, por qué HTTP es más complejo?

Similitudes: Ambos definen reglas claras para que dos dispositivos puedan intercambiar datos de forma entendible. También requieren que emisor y receptor estén de acuerdo en el formato de los mensajes.

Diferencias: HTTP es más complejo porque trabaja a través de Internet, donde puede haber miles de kilómetros de distancia, múltiples sistemas intermedios, y requiere información adicional como encabezados, estado, tipo de contenido, etc. Los protocolos seriales son más simples porque suelen ser comunicación entre dos dispositivos cercanos.

Razón de la complejidad de HTTP: Necesita manejar muchos tipos de datos, usuarios simultáneos, seguridad (como HTTPS), errores, formatos distintos (HTML, JSON, imágenes), y más.

#### Pausa activa 5: Formulario de login y los roles de HTML, CSS y JS
#### ¿Qué parte es HTML, CSS y JS?

En un formulario de login:

HTML: Define los campos de texto, etiquetas, botón de “Iniciar sesión”.

CSS: Define que el fondo del botón sea azul, que los bordes sean redondeados, o que la fuente sea Arial.

JavaScript: Verifica si se llenaron los campos, muestra el mensaje de “Contraseña incorrecta” sin recargar la página, o evita enviar el formulario si falta algo.

#### Pausa activa 6: draw() vs modelo basado en eventos
#### ¿Ventajas del modelo basado en eventos? ¿Es eficiente redibujar toda la página constantemente?

El modelo basado en eventos es ideal para interfaces web porque solo se ejecuta código cuando ocurre algo (como un clic, escribir texto, etc.). Esto ahorra recursos del sistema y mejora el rendimiento. Redibujar toda la página 60 veces por segundo como en draw() sería innecesario y consumiría mucho procesamiento, incluso cuando no hay cambios. El modelo basado en eventos es más eficiente para la web.

#### Pausa activa 7: ¿Por qué usar JavaScript en cliente y servidor?
#### ¿Qué ventajas tiene esto para los desarrolladores?

Una gran ventaja de usar JavaScript tanto en el cliente como en el servidor (con Node.js) es que los desarrolladores pueden trabajar con un solo lenguaje en ambos lados, lo que facilita el desarrollo, mantenimiento y colaboración del proyecto. También permite compartir lógica entre cliente y servidor, lo que ahorra tiempo y reduce errores.

#### Pausa activa 8: HTTP vs WebSockets / Socket.IO
#### ¿Cuál es la diferencia y en qué aplicaciones se usa WebSockets?

Diferencia clave: HTTP es como enviar una carta: haces una petición y esperas una respuesta. WebSockets es como una llamada telefónica abierta: una vez establecida, ambas partes pueden hablar en cualquier momento sin repetir el saludo.

Aplicaciones en tiempo real: Se usa en chats en vivo, videojuegos online, colaboración en documentos (como Google Docs), actualizaciones en tiempo real de datos (como precios de criptomonedas o resultados deportivos), o incluso ver el cursor de otro usuario en la pantalla.
