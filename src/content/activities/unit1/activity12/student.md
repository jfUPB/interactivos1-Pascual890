Codigo del microbit
py
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
   '''
