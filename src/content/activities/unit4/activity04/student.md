#### Solucion actividad 4

#### Compara el código original del caso de estudio con el anterior. ¿Qué notas de diferente?

El primer código usa p5.min.js y la librería p5.webserial, ideal para comunicar p5.js con dispositivos como Micro:bit o Arduino por puerto serial.

El segundo código usa p5.js junto con p5.sound, útil para trabajar con audio, como reproducir o analizar sonidos.

#### ¿Para qué se usan estas imágenes? ¿Qué representan?

Las imágenes SVG que se cargan en el arreglo lineModule son probablemente componentes visuales reutilizables que forman parte de una composición modular o generativa. Aunque no se muestran en este fragmento, se usan más adelante en el sketch para crear una pieza visual más compleja.

#### ¿Cómo puedes solucionar este tipo de problema?
Puedo solucionar este problema con una maquina de estados, donde puedo organizar adecuadamente la aplicacion segun el estado en que se encuentre

#### ¿Qué era el pseudoestado INIT?
En estado init, solo se inicializaban cosas: 
Se mostraba la interfaz, se configuraban variables y luego se pasaba al sgte estado automaticamente, es decir que solo era preparacion 

#### ¿Y por qué ahora no está el estado INIT?
Por que la funcion setup() cumple el mismo rol, todo lo que se ponia el Init, se esta poniendo directamente en setup() 

#### ¿Entonces, sí está el pseudoestado INIT?
Si, pero llamado como setup() pero ya no se llama Init ni se controla con un case dentro del draw(), por que p5 ya me esta dando una estructura que separa lo que se ejecuta una vez 

#### ¿Qué pasaría ahora si das click al botón?
Al dar click en el boton Connect to microbit se ejecuta la funcion connectBtnClick(), esta funcion verifica si el puerto serial ya esta abierto 

#### ¿Para qué abres el puerto serial?
Se abre el puerto serial para poder recibir los datos que el microbit esta enviando por UART
Esto quiere decir que el microbit esta enviando una linea con cuatro valores separados por comas que representa los valores de sus sensores y botones 

#### ¿Qué debes verificar al ejecutar la aplicación?
En la esquina superior izq, aparece el boton Connect to microbit

Al hacer click, la consola debe de mostrar informacion indicando si el puerto se conecto o no

Si el microbit esta conectado y enviando datos, mas adelante en el desarrollo podria ver los datos impresos en la consola o usado dentro del draw()

#### ¿Qué comportamiento interesante se observa con el botón?
Muestra "Disconnect from micro:bit" si ya estás conectado.
Muestra "Connect to micro:bit" si estás desconectado.

#### ¿Por qué solo se leen datos si el puerto está abierto?
por que la lectura de datos del microbit solo es posible cuando el puerto serial esta abierto, si el puerto esta cerrado, simplemente no hay comunicacion entre el microbit y la aplicacion de p5 

#### ¿Se podrían leer datos si el puerto está cerrado?
Creeria que no, si el puerto esta cerrado, la funcion port.availableBytes() siempre devolvera 0, y el otro puerto no podria leer nada, por que no hay datos entrado.

#### ¿Qué pasaría si el puerto está cerrado y el micro:bit envía datos?
El microbit seguira enviando datos, pero esos datos se perderan

#### ¿Qué hace port.availableBytes() > 0?
Esto verifica si hay al menos un byte disponible para ser leido en el buffer de entrada del puerto serial.
Sirve para evitar errores en el programa y cuando lea no haya nada 

#### ¿Por qué usamos readUntil("\n")?
Se utiliza para recibir una linea completa de datos, y esta linea termina con el caracter especial /n que se usa para marcar el fin de un paquete de datos 

#### ¿Qué pasa si el micro:bit no envía el \n?
Si el microbit no envia /n la funcion usada se quedara esperando indefinidamente a que llegue ese caracter. El programa no podra procesar la información por que no sabra cuando termina la linea de datos

#### ¿Por qué usamos .trim() después de leer los datos?
Por que el /n al final de la linea no hace parte de los datos utiles, solo sirve como marcador de final 

#### ¿Por qué se usa split(",")?
Se usa split con coma por que esto facilita el acceso individual de cada dato 

#### ¿Por qué verificamos que values.length == 4?
Porque esperamos exactamente 4 valores xValue, yValue, aState, bState. Si no hay 4 valores, los datos estan incompletos o corruptos y no deben usarse

#### ¿Por qué hay que convertir los valores de cadena a número o booleano?
Por que al llegar por el puerto serial, todos los datos vienen como cadenas de texto incluso si originalmente eran numeros booleanos 
convertir x e y a numeros enteros
convertir los estos de los botones A y B a Booleanos con .tolowerCase() == True

#### ¿Por qué se suma windowWidth/2 y windowHeight/2 a los valores de x e y?
probablemente enviar valores de aceleracion que van desde negativos hasta positivos
Al sumar windowWidth/2 lo que se esta haciendo es centrar el punto (x,y) en el centro de la pantalla, para que cuando xValue = 0 y yValue = 0, el punto este justo en el centro del canvas

#### ¿Cómo puedes verificar que los eventos keyPressed y keyReleased se están generando?
una forma de verificarlo seria usando print() en la consola. Modifique el codigo de updateButtonStates() para imprimir un mensaje cuando se detecta que se presiono o solte el boton.

#### ¿Qué hace updateButtonStates()?
Este algoritmo compara el estado actual de los boton A y B con su estado anterior. Si detecta un cambio y actualiza el estado anterior

#### ¿Por qué es necesario almacenar el estado anterior de los botones?
Por que solo se debe generar un evento cuando el estado cambia. Si no guardamos el estado anterior del evento keypressed() se estaria ejecutando en cada frame mientras el boton este presionado.

#### ¿Qué pasaría si no se almacenara el estado anterior?
Si no se almacenara, entonces cada vez que se leyera un true, se ejecutaria KeyPresset() una y otra vez, aunque el boton no se haya soltado ni vuelto a presionar. 

