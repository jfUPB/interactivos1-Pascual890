## Bomba 2
```py
from microbit import *
import utime
import music

estado = 0  
contador = 20
secuencia = []

secuencia_correcta = ['A', 'B', 'A', 'shake']

while True:
    if estado == 0:
        display.show(str(contador))
        if button_a.is_pressed():
            contador = min(60, contador + 1)
            utime.sleep_ms(300)
        if button_b.is_pressed():
            contador = max(10, contador - 1)
            utime.sleep_ms(300)
        if accelerometer.was_gesture("shake"):
            estado = 1
            secuencia = []

    elif estado == 1:
        while contador > 0:
            display.scroll(str(contador), wait=False, loop=False, delay=80)
            utime.sleep(1)
            contador -= 1

            # Detectar la secuencia
            if button_a.was_pressed():
                secuencia.append('A')
            elif button_b.was_pressed():
                secuencia.append('B')
            elif accelerometer.was_gesture("shake"):
                secuencia.append('shake')

            if len(secuencia) > 4:
                secuencia.pop(0)

            if secuencia == secuencia_correcta:
                estado = 0
                contador = 20
                display.show(Image.HAPPY)
                utime.sleep(1)
                display.clear()
                break

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
```
Solución:

Lista secuencia:
Se crea una lista para guardar los pasos que el usuario realiza durante la cuenta regresiva.

Detección de entrada:
En cada ciclo, si se presiona A, B o se sacude el microbit, se registra el evento en la lista.

Control de tamaño:
Solo se guardan los últimos 4 eventos (longitud de la secuencia esperada).

Verificación:
Si la lista coincide con la secuencia correcta (A, B, A, shake), se considera exitosa y la bomba vuelve al modo configuración.

Fallos:
Si el usuario se equivoca, la secuencia sigue acumulando eventos hasta acertar o que explote.
