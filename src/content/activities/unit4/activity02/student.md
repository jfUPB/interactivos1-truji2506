#### Solución acitividad 2

#### Explicación del Sketch
Este código genera una trayectoria que sigue un "agente inteligente" en un lienzo de p5.js. La dirección del agente cambia al azar dentro de ciertos límites, creando un patrón generativo basado en su movimiento.

#### Configuración Inicial (setup())

Se define un lienzo de 600x600 píxeles con un fondo blanco.

Se establece el modo de color en HSB para manejar colores más intuitivamente.

El agente comienza en una posición aleatoria en el eje X y en la parte superior del lienzo (posición Y = 5).

#### Dibujo del Movimiento (draw())

Se ajusta la velocidad del agente según la posición del mouse en el eje X.

El agente dibuja puntos en su trayectoria.

Se mueve en la dirección definida por un ángulo calculado aleatoriamente.

Se verifica si el agente alcanza los bordes del lienzo o si cruza su propia trayectoria.

#### Cambio de Dirección (getRandomAngle())

Calcula un nuevo ángulo basado en la dirección actual.

Si choca con los bordes o con una línea previa, cambia de dirección.

Si la distancia entre la posición actual y la anterior es suficiente, dibuja una línea entre esos puntos.

#### Interacción con Teclado (keyReleased())

Tecla s: Guarda la imagen generada.

Tecla DEL o BACKSPACE: Limpia el lienzo y reinicia el dibujo.

#### Modificaciones y Dibujos Generados
#### Cambio de color dinámico

Modifiqué el color del trazo para que cambie en función de la posición del mouse.

Resultado: Un efecto visual más dinámico con colores que varían en tiempo real.

#### Ajuste de velocidad

Aumenté el valor máximo de velocidad cuando el mouse está en la parte derecha del lienzo.

Resultado: Patrones más complejos y densos en la parte derecha de la pantalla.

#### Modificación en la dirección

Hice que el ángulo de cambio sea más amplio, permitiendo giros más bruscos.

#### Resultado: Se generan patrones más irregulares y abstractos.
