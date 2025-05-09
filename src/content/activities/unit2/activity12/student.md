## Bomba temporizada}

``` py
from microbit import *
import utime
import music

estado = 0  # 0: Configuración, 1: Cuenta regresiva, 2: Explosión
contador = 20

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
    
    elif estado == 1: 
        while contador > 0:
            display.show(str(contador))
            utime.sleep(1)
            contador -= 1
            if pin_logo.is_touched():
                estado = 0
                contador = 20
                break
        if contador == 0:
            estado = 2
    
    elif estado == 2:
        display.show(Image.SKULL) 

        music.pitch(1500, 150, wait=True)
        music.pitch(800, 200, wait=True)
        music.pitch(300, 350, wait=True)

        while not pin_logo.is_touched():
            utime.sleep_ms(100)
        estado = 0 
        contador = 20
        display.clear()
        music.stop()
```

Enlace a video de bomba en funcionamiento:
https://youtu.be/U4y8RUrPm2k
(Creo que ese link sirve, si no me escribe para cambiarlo)


