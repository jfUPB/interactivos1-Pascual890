Código de microbit:

El código en MicroPython para el micro:bit configura la comunicación serial y muestra en la pantalla LED cualquier carácter recibido por el puerto serial.

Flujo del código:

Inicialización de UART: Se configura la comunicación serial con una velocidad de baudios de 115200.
Lectura de datos: El micro:bit verifica si hay datos disponibles en el buffer serial.
Procesamiento y visualización: Si recibe un carácter, lo decodifica en formato UTF-8 y lo muestra en la matriz LED.

```py
from microbit import *

uart.init(baudrate=115200)

while True:
    if uart.any(): 
        data = uart.read(1)
        if data:
            display.show(data.decode('utf-8'))
```
Código de p5.js:

El código en p5.js permite enviar caracteres al micro:bit mediante una interfaz web.

Flujo del código:

Inicialización de la conexión serial: Se crea una instancia para la conexión con el micro:bit.
Interfaz de usuario: Se generan un botón para conectar/desconectar y un campo de entrada con un botón para enviar caracteres.
Manejo de conexión: Un botón permite abrir o cerrar la conexión serial.
Envío de caracteres: Cuando el usuario ingresa un carácter y presiona el botón, este se envía al micro:bit por el puerto serial.

```js
let port;
let connectBtn;
let inputField;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    
    inputField = createInput('');
    inputField.position(80, 250);
    
    let sendBtn = createButton('Send Character');
    sendBtn.position(220, 250);
    sendBtn.mousePressed(sendBtnClick);
}

function draw() {
    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } else {
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

function sendBtnClick() {
    let charToSend = inputField.value().charAt(0);
    if (charToSend) {
        port.write(charToSend);
    }
}
```
