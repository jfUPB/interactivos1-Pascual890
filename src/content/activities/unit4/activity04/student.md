## Actividad 4

### ¿Para qué se usan estas imágenes? ¿Qué representan?
Estas imágenes se usan para cambiar el tipo de trazo del dibujo, como si fueran diferentes puntas de pincel. Cada imagen representa una forma distinta que se puede usar para pintar en el canvas.

### ¿Qué pasaría ahora si das click al botón?
Si el puerto está cerrado, se abre. Si ya está abierto, entonces se cierra. Es un botón de encendido/apagado para la conexión serial.

### ¿Por qué? ¿Podrías leer datos si el puerto está cerrado? ¿Qué pasaría si el puerto está cerrado y el micro:bit envía datos?
No, no se pueden leer datos si el puerto está cerrado porque no hay comunicación entre el microbit y el sketch.

Si el micro:bit envía datos mientras el puerto está cerrado, esos datos simplemente se pierden, porque nadie los está recibiendo.

Si port.opened() es false, el Sketch no puede recibir los datos que el microbit manda.

### Qué pasaría si el micro:bit no envía el “\n”?
Si no se envía el salto de línea (\n), el comando readUntil("\n") no puede saber cuándo termina un mensaje, entonces sigue leyendo sin parar, eso causaría que los datos no se separen correctamente

En resumen, se daña el programa, ya que este funciona con datos en grupos de 4 datos por linea

### ¿Por qué se suma windowWidth/2 y windowHeight/2 a los valores de x e y?
Porque el micro:bit está enviando coordenadas con respecto al centro del canvas (donde (0,0) es el centro), pero en p5.js el (0,0) está en la esquina superior izquierda. 
Al sumar la mitad del ancho y la mitad del alto, estamos trasladando el punto para que quede bien ubicado en el sistema de p5.js.

### ¿Cómo puedes verificar que los eventos de keypressed y keyreleased se están generando?
Puedo agregar print() dentro de las funciones keyPressed y keyReleased para que salga un mensaje en la consola cada vez que se presiona o se suelta una tecla. 
También puedo darme cuenta si funcionan al ver que cambian cosas en el dibujo cuando uso las teclas.

### Ahora te pediré que analices el algoritmo updateButtonStates. ¿Qué hace? ¿Por qué es necesario almacenar el estado anterior de los botones? ¿Qué pasaría si no se almacenara el estado anterior?
El programa revisa si hubo un cambio en los botones A y B del micro:bit. Si el botón A pasó de no estar presionado a estarlo, se cambia el tamaño del pincel. Si el botón B pasó de presionado a no presionado, se cambia el color.

Guardar el estado anterior es importante para detectar ese cambio. Si no se guarda, el programa no sabría si el botón fue presionado o soltado, y por lo tanto no reaccionaría como se quiere que reaccione.

### Observa el código original y el nuevo código. ¿Qué diferencias encuentras?
La diferencia principal es que ahora el microbit se está usando como entrada, en vez del teclado o el mouse. Se usa el puerto serial para recibir los datos.

### ¿Qué pasó con algunos eventos del mouse?
Muchos de los eventos del mouse ya no se usan. Ahora el dibujo se controla con los datos que vienen del microbit como su posición y los botones A y B.

### ¿Qué paso con la función relacionada con la barra de espacio del teclado?
Esta función ya no está disponible, creería que lo que la reemplazó fue le botón B que es el que cambia el color ahora.

### “No se están recibiendo 4 datos del micro:bit”
### ¿Qué significa esto? Analiza si este mensaje ocurre en varios frames o solo en uno.
Significa que el programa está esperando recibir exactamente 4 datos desde el microbit (por ejemplo, dos coordenadas y dos estados de botones), pero en ese momento no han llegado los cuatro.
Puede que solo hayan llegado 1, 2 o 3, o incluso ninguno. Entonces, como no están completos, no se puede usar ese paquete de datos para dibujar o procesar nada.

Este mensaje normalmente aparece solo en un frame o en los primeros pocos frames justo cuando se abre la conexión serial.
No es un mensaje que aparezca constantemente durante la ejecución, sino más bien algo que sucede al arrancar el sketch.

### ¿Por qué?
Porque en el primer momento en que se ejecuta el código, el microbit aún no ha alcanzado a enviar el primer paquete completo de 4 datos.

### ¿Qué puedes hacer para solucionar este problema?
Una opción sería simplemente ignorar esos paquetes incompletos y seguir esperando hasta que llegue uno correcto.

Otra solución posible es inicializar los valores esperados con algo por defecto, como (0, 0, false, false), para que el programa tenga datos válidos desde el principio.

También se podría mostrar un mensaje visual o en consola que diga “Esperando datos del microbi” o algo asi para que el usuario entienda que es normal al inicio.


