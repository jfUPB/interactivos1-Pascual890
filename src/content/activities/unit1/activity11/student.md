Codigo de microbit:
```py
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A')
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        sleep(500)
```

Código de p5.js:
```js
let port;
let circleX = 200;

function setup() {
    createCanvas(400, 400);
    port = createSerial();
    let connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
}

function draw() {
    background(220);
    
   
    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        
       
        if(dataRx == 'A'){
            circleX -= 10; 
        }
        else if(dataRx == 'B'){
            circleX += 10; 
        }
    }

   
    fill('blue');
    ellipse(circleX, height / 2, 50, 50);
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}
```

Similar a ejercicios anteriores, se usa el codigo de microbit para detectar cuando se presiona un botón y hacer posible el mapeo de los botones con p5.js El codigo p5.js solo toma la señal y, en vez de cambiar de color la figura como en el ejercicio anterior, solo suma o resta 10 a la posicion x, haciendolo moverse en este eje.
