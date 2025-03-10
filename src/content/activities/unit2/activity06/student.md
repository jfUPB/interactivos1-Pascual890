``` py
from microbit import *

uart.init(baudrate=115200)

while True:
    if button_a.is_pressed():
        display.show(Image.HEART)
        sleep(500)

    if button_b.is_pressed():
        display.show(Image.HAPPY)
        sleep(500)

    if accelerometer.was_gesture('shake'):
        display.show(Image.SAD)
        sleep(500)

    if button_a.is_pressed() and button_b.is_pressed():
        display.show(Image.BUTTERFLY)
        sleep(500)
```
Este codigo de microbit permite seleccionr 4 imagenes diferentes en microbit dependiendo del input que se le de. Cada boton tiene una imagen asignada y presionarlos a la vez daria una tercera imagen, por ultimo, agitar el microbit pone la cuarta imagen en el LED.
