´´´mpy
from microbit import *

uart.init(baudrate=115200)
while True:
    if button_a.is_pressed():
        uart.write('A')
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        sleep(500)
´´´
Este fue el codigo usado para microbit

Este es el codigo de p5js:

'''js
let port;
let squareColor; 

function setup() {
    createCanvas(400, 400);
    port = createSerial();
    let connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
}

function draw() {
    
    if (port.availableBytes() > 0) {
        let dataRx = port.read(1); // Leer un byte de datos

        
        if (dataRx == 'A') {
            squareColor = color(random(255), random(255), random(255));
        } else if (dataRx == 'B') {
            squareColor = color(random(255), random(255), random(255));
        }
        
        background(220);
        fill(squareColor);
        rect(width / 2 - 50, height / 2 - 50, 100, 100); 
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}
´´´
