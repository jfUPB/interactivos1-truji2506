#### Solución actividad 3

#### ¿Qué información se está enviando? ¿Cómo se está enviando? Qué significa esta parte del código:
```c
"{},{},{},{}\n".format(xValue, yValue, aState, bState)
```
Esto es una cadena formateada que utiliza el metodo .format() para insertar valores en una cadena de texto 

{},{},{},{} estos son los espacios reservados donde se insertan los valores

\n Esto significa un salto de linea lo que significa que cada conjunto de valores estará en una nueva linea cuando se escriba en un archivo o se envie por UART 
 y de esta forma lee los datos que se encuentran el .format que serian estos xValue, yValue, aState, bState y asi creando la cadena resultante. 

#### Observa en la aplicación SerialTerminal cómo se ven los datos que se están enviando. ¿Qué puedes inferir de la estructura de los datos?

Observano en la aplicacion SerialTerminal, la estrutura de datos es la correcta por que es la estructura que se le dio desde el codigo del microbit y es de esta forma  xValue, yValue, aState, bState

#### ¿Por qué se separan los datos con comas y se termina con un salto de línea?

Se sepanran los dats con comas por el codigo que se explico anteriormente {},{},{},{} esto lo que hace es separar por comas y almacenar en cada llave los datos correspondientes y termina en un salto de linea \n por este codigo que lo que hace es a momento de terminar la cadena de texto termina con un salto de linea

#### ¿Qué crees que pasaría si no se separan los datos con comas y no terminan con un salto de línea?

Se verian de una forma muy desordenada ya que toda la información estaria junta y no se podria establecer donde empieza y termina cada cadena de texto 

#### Para qué crees que se usa la función sleep(100)? ¿Qué pasaría si no se usara?

lo que hace la funcion de sleep(100) es que cada 1000 milisegundo se reinicia el ciclo de esta forma controlar el envio de datos, si no se usara lo que hace es enviar datos en exceso y esto puede saturar la conexion y la informacion puede que no se envie de una forma correcta 

#### Observa cómo cambian los valores de xValue y yValue a medida que el micro:bit se inclina hacia la izquierda, derecha, adelante y atrás. ¿Qué valores toman xValue y yValue en cada caso?

Estos datos cambian mediante la rotacion del microbit, si lo movemos con rotacion a la izq la informacion de x cambia a negativa, y si lo movemos a la derecha cambia a positiva,para de esa misma forma con una rotacion en Y 

#### ¿Qué valores toman aState y bState cuando presionas los botones A y B?

Lo que hace aState y bState es establecer si la tecla A o B estan presionados o no, por ejemplo. Al momento de no oprimir nada aparece como False y si lo apromes aparece como True.

#### Observa qué ocurre si en vez de is_pressed() usas was_pressed(). ¿Qué diferencias encuentras?

Cambiar estos datos no veo la diferencia al momento de realizar la interaccion.

#### Finalmente, analiza este asunto: si el micro:bit tiene los siguientes datos xValue: 969, yValue: 652, aState: True, bState: False ¿Qué bytes se enviarían por el puerto serial? Piensa, primero piensa por favor, y luego verifica con la aplicación SerialTerminal. Ten presente que en Mostrar datos como puedes ver los bytes que se están enviando mediante Todo en HEX.

Esto lo que hace es convertir los valores HEX a ASCII y obtendre exactamente los datos que envia, esta seria una representacion hexadecimal del texto enviar por UART

