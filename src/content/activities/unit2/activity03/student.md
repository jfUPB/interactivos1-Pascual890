### Entradas del microbit

Botón A: Un botón físico ubicado en la parte frontal izquierda de la placa. Al ser presionado, genera una señal que puede ser detectada por el microcontrolador. Se utiliza comúnmente para iniciar acciones, cambiar estados o seleccionar opciones.

Botón B: Similar al Botón A, este botón físico se encuentra en la parte frontal derecha de la placa. Su funcionamiento es análogo al Botón A y se utiliza para propósitos similares.

Acelerómetro: Un sensor de movimiento integrado que mide la aceleración lineal en los tres ejes (X, Y, Z). Permite detectar la orientación de la placa, movimientos bruscos (sacudidas), caídas e incluso la fuerza de la gravedad.

Brújula: Un sensor que detecta los campos magnéticos, incluyendo el campo magnético terrestre. Permite al micro:bit determinar su rumbo o dirección, actuando como una brújula digital.

### Salidas del microbit

Matriz LED: Una cuadrícula de 25 LEDs individuales ubicados en la parte frontal de la placa. Cada LED puede ser controlado individualmente para mostrar patrones, texto, números e incluso animaciones sencillas.

Pines de E/S (GPIO - Propósito General de Entrada/Salida): Un conjunto de pines ubicados en el borde inferior de la placa (y en la versión V2, pines dedicados). Estos pines pueden configurarse como entradas o salidas digitales y, en algunos casos, como salidas analógicas (PWM). Permiten conectar componentes externos como LEDs, motores, sensores, etc.

Altavoz Integrado: La versión 2 del micro:bit incorpora un pequeño altavoz que permite generar sonidos y melodías simples.

Salida de Audio (Conector para Auriculares: También en la versión 2, un conector permite conectar auriculares o un amplificador externo para una salida de audio más potente o discreta.

### Funciones Básicas de MicroPython para entradas

1. button_a.is_pressed() y button_b.is_pressed(): Estas funciones booleanas retornan True si el botón correspondiente está siendo presionado y False en caso contrario.
```py
from microbit import *

while True:
    if button_a.is_pressed():
        display.show("A")
    elif button_b.is_pressed():
        display.show("B")
    else:
        display.clear()
    sleep(100)
```

2. accelerometer.get_values(): Esta función retorna una tupla de tres enteros que representan la aceleración en los ejes X, Y y Z.
```py
from microbit import *

while True:
    x, y, z = accelerometer.get_values()
    print((x, y, z))
    sleep(500)
```

3. compass.heading(): Esta función retorna un entero que representa la dirección en grados (0-359) en la que apunta el norte magnético.
```py
from microbit import *

compass.calibrate() # Calibrar la brújula al inicio

while True:
    direccion = compass.heading()
    print("Dirección:", direccion)
    sleep(1000)
```

### Funciones Básicas de MicroPython para salidas

1. display.show(image): Esta función muestra una imagen en la matriz de LEDs. image puede ser una imagen predefinida (como Image.HEART)
```py
from microbit import *

display.show(Image.HAPPY)
sleep(2000)
display.scroll("Hola Mundo!")
```

2. pin*.write_digital(value): Esta función permite establecer el estado de un pin de E/S digital como alto (1) o bajo (0). Reemplaza * con el nombre del pin (por ejemplo, pin0, pin1, pin2).
```py
from microbit import *

pin0.write_digital(1) # Enciende el dispositivo conectado al pin 0
sleep(1000)
pin0.write_digital(0) # Apaga el dispositivo conectado al pin 0
```

3. music.play(music_list) (micro:bit V2 con altavoz): Esta función permite reproducir una secuencia de notas musicales definidas en una lista. También se pueden usar melodías predefinidas.
```py
from microbit import *
import music

music.play(music.DADADADUM)
sleep(2000)
music.play(['C4:4', 'D4:4', 'E4:4', 'F4:4'])
```








   
