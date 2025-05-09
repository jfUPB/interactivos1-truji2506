#### Solución actividad 6

#### ¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?
Un protocolo de comunicación es un conjunto de reglas que permiten que dos dispositivos se entiendan y transmitan datos 
de forma organizada y segura 

#### ¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?
Las comas funcionan como delimitadores, es decir, permiten separar los distintos datos dentro un mismo mensaje 

#### ¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?
Porque ayuda a saber cuando termina un mensaje completo, en el que caso anterior el que se uso fue /n

#### ¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?
La maquina de estados ayuda a comtrolar el flujo del programa dependiendo del contexto 

#### ¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?
Se convierten en texto plano con valores separados por comas y se termina con salto de linea

#### ¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?
Significa que los numeros, letras y simbolos son enviados como caracteres legibles, no como binarios puros

#### ¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?
Para evitar errores, si no hay datos y se intentar leer, pueden volverse null o datos incorrectos

#### ¿Cómo se elimina el retorno de carro o salto de línea de un string en p5.js?
Usando trim()

#### Si una cadena tiene información separada por espacios y quieres dividir dicha información en varias cadenas individuales, ¿qué función de p5.js usarías?

Usaría split() con " " como delimitador

#### ¿Por qué es necesario en la aplicación del caso de estudio convertir las cadenas a números enteros antes de usarlas en el sketch de p5.js?
Porque al recibir los datos del micro:bit, llegan como texto. Para poder hacer cálculos o graficarlos, deben ser números.

#### Si el micro:bit tiene los siguientes datos: xValue: 123, yValue: 756, aState: False, bState: True ¿Qué bytes se enviarían por el puerto serial?
Se enviaría este string (en ASCII)

#### ¿Qué aprendiste nuevo del micro:bit que no sabías antes?
Aprendí que el micro:bit puede enviar datos por el puerto serial en tiempo real y se puede conectar con p5.js para crear aplicaciones interactivas.

#### ¿Qué aprendiste nuevo de p5.js que no sabías antes?
Aprendí a usar p5.serialport para leer datos de hardware externo y cómo visualizarlos gráficamente usando draw() y split().
