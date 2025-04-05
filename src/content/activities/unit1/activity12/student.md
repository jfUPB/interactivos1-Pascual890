Codigo del microbit
```py
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

Codigo p5.js
```js
let port;
let connectBtn;

function setup() {
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
}

function draw() {

    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    }
    else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}
```

