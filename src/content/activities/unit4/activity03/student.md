## Hallazos actividad 3

### ¿Qué información se está enviando? ¿Cómo se está enviando? Qué significa esta parte del código: "{},{},{},{}\n".format(xValue, yValue, aState,bState)

Se están enviando cuatro datos del microbit:

- xValue: el valor del eje X del acelerómetro.

- yValue: el valor del eje Y del acelerómetro.

- aState: el estado del botón A (True si está presionado, False si no).

- bState: el estado del botón B (True si está presionado, False si no).\

Se envía a través del puerto serial (UART) con una velocidad de 115200. El resultado será un string como: "-125,420,True,False\n". cada línea representa un "paquete" de datos que se puede leer fácilmente en otro dispositivo o programa como p5.js

### Observa en la aplicación SerialTerminal cómo se ven los datos que se están enviando. ¿Qué puedes inferir de la estructura de los datos?
En el SerialTerminal salen datos como:

-143,276,False,False  
-147,280,False,True  
-150,290,True,True

- Cada línea representa un conjunto completo de datos.

- Los valores están en orden, separados por comas.

- El formato es fácil de leer por otros programas como p5.js.

### ¿Por qué se separan los datos con comas y se termina con un salto de línea?

Las comas permiten separar cada dato para identificarlo fácilmente. El salto de línea (\n) indica el fin de un paquete de datos, ideal para leer línea por línea desde otro programa. Esto se hace para facilitar la lectura y la organización de los datos al momento de enviar a otro programa o de leer en el serial.

### ¿Qué crees que pasaría si no se separan los datos con comas y no terminan con un salto de línea?

Sin comas, los datos quedarían pegados (ej. -1023123FalseTrue) y sería difícil saber qué representa cada parte.

Sin salto de línea, no podrías saber dónde termina un paquete y comienza el siguiente. Sería una cadena continua sin estructura. Esto dificultaría mucho el procesamiento de datos desde el otro extremo.

### Para qué crees que se usa la función sleep(100)? ¿Qué pasaría si no se usara?

sleep(100) hace que el programa espere 100 milisegundos entre cada envío. Sin el sleep(100) el micro bit enviaría datos lo más rápido posible, se podria saturar el puerto serial y el programa receptor podría no seguir el ritmo y perder datos.

### Observa cómo cambian los valores de xValue y yValue a medida que el micro:bit se inclina hacia la izquierda, derecha, adelante y atrás. ¿Qué valores toman xValue y yValue en cada caso?

Plano (horizontal): x se aproxima a  0, y se aproxima a 0

Izquierda: x → valores negativos 

Derecha: x → valores positivos

Adelante (pantalla hacia abajo): y -> valores positivos

Atrás (pantalla hacia mi): y -> valores negativos

Los valores pueden ir de aproximadamente -1024 a +1024 dependiendo del ángulo.

### ¿Qué valores toman aState y bState cuando presionas los botones A y B?

Si se presiona A, aState = True, bState = False

Si se presiona B, aState = False, bState = True

Si se presionan ambos ambos serán True

Si no se presiona ninguno ambos serán False

### Observa qué ocurre si en vez de is_pressed() usas was_pressed(). ¿Qué diferencias encuentras?

is_pressed() devuelve True mientras el botón está siendo presionado.

was_pressed() devuelve True solo una vez, justo después de haber sido presionado, luego se reinicia a False.

Ejemplo:

Si mantienes el botón A presionado:

is_pressed() = True constantemente

was_pressed() = True una sola vez, luego False

was_pressed() es útil para detectar eventos únicos, como un clic. En este caso es mejor is_pressed() ya que se necesita verificar si se mantiene presionado.

### si el micro:bit tiene los siguientes datos xValue: 969, yValue: 652, aState: True, bState: False ¿Qué bytes se enviarían por el puerto serial? 

Cuando el micro:bit tiene estos valores se crea este texto:
969,652,True,False\n

Eso es lo que el micro:bit envía por el cable (puerto serial).
Cada letra o número se convierte en un número especial para que la computadora entienda los caracteres.

Lista de bytes que se envían:

39 36 39 2C 36 35 32 2C 54 72 75 65 2C 46 61 6C 73 65 0A

Cada grupo representa un carácter del texto. Por ejemplo:

39 = "9"

2C = ","

54 = "T"

0A = salto de línea (\n)







