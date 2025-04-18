## Bomba 3
```py
from microbit import *
import utime
import music

evento_ocurrio = False
evento = ''

estado = 0
contador = 20
secuencia = []
secuencia_correcta = ['A', 'B', 'A', 'S']

uart.init(baudrate=9600)

def tareaEventos():
    global evento_ocurrio, evento

    if not evento_ocurrio:

        if button_a.was_pressed():
            evento = 'A'
            evento_ocurrio = True

        elif button_b.was_pressed():
            evento = 'B'
            evento_ocurrio = True

        elif accelerometer.was_gesture("shake"):
            evento = 'S'
            evento_ocurrio = True

        if uart.any():
            datos = uart.read()
            if datos:
                recibido = datos.decode('utf-8').strip().upper()
                if recibido in ['A', 'B', 'S', 'T']:
                    evento = recibido
                    evento_ocurrio = True
def tareaBomba():
    global estado, contador, secuencia, evento_ocurrio, evento

    if estado == 0:
        display.show(str(contador))

        if evento_ocurrio:
            if evento == 'A':
                contador = min(60, contador + 1)
            elif evento == 'B':
                contador = max(10, contador - 1)
            elif evento == 'S':
                estado = 1
                secuencia = []

            
            evento_ocurrio = False

            utime.sleep_ms(300)

    elif estado == 1:
        display.scroll(str(contador), wait=False, loop=False, delay=80)
        utime.sleep(1)
        contador -= 1

        if evento_ocurrio:
            if evento in ['A', 'B', 'S']:
                secuencia.append(evento)

                if len(secuencia) > 4:
                    secuencia.pop(0)

                if secuencia == secuencia_correcta:
                    estado = 0
                    contador = 20
                    display.show(Image.HAPPY)
                    utime.sleep(1)
                    display.clear()

            evento_ocurrio = False

        if contador == 0:
            estado = 2

    elif estado == 2:
        display.show(Image.SKULL)

        music.pitch(1500, 150, wait=True)
        music.pitch(800, 200, wait=True)
        music.pitch(300, 350, wait=True)

        utime.sleep(3)
        estado = 0
        contador = 20
        display.clear()
        music.stop()

while True:
    tareaBomba()
    tareaEventos()
```

### ¿Cómo se hizo la solución?

Se dividió el programa en dos tareas:

tareaEventos(): detecta eventos (botones, shake, mensajes por serial) y los guarda.

tareaBomba(): maneja los estados de la bomba usando esos eventos, sin saber de dónde vienen.

#### Se usan dos variables:

evento_ocurrio: indica si hay un nuevo evento.

evento: contiene el valor del evento (por ejemplo 'A', 'B', 'S').

Así, ya no importa si el evento viene del micro:bit o del puerto serial.

#### Puerto serial
Se agregó soporte para recibir mensajes (A, B, S, T) por serial.
Se verifica que uart.read() devuelva datos antes de decodificar, para evitar errores.

#### Resultado

La bomba puede controlarse desde los botones o por el puerto serial.

La lógica es más clara y escalable.

Es fácil añadir nuevas fuentes de eventos en el futuro.


