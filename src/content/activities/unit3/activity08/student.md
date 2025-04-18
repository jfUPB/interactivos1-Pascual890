Código bomba en p5.js

``` js
let estado = "inactiva";
let tiempo = 20;
let tiempoRestante = 0;
let tiempoInicio = 0;

let secuencia = [];
let secuenciaCorrecta = ['A', 'B', 'A', 'S'];

let port;
let connectBtn;

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(32);

  port = createSerial();
  connectBtn = createButton("Conectar micro:bit");
  connectBtn.position(20, 360);
  connectBtn.mousePressed(toggleConnection);

  let sumarBtn = createButton("+1s (A)");
  sumarBtn.position(20, 320);
  sumarBtn.mousePressed(() => manejarEvento('A'));

  let restarBtn = createButton("-1s (B)");
  restarBtn.position(120, 320);
  restarBtn.mousePressed(() => manejarEvento('B'));

  let activarBtn = createButton("Activar (S)");
  activarBtn.position(220, 320);
  activarBtn.mousePressed(() => manejarEvento('S'));
}

function draw() {
  background(30);
  dibujarBomba();

  if (port.availableBytes() > 0) {
    let data = port.read(1);
    if (data) {
      manejarEvento(data);
    }
  }

  if (!port.opened()) {
    connectBtn.html("Conectar micro:bit");
  } else {
    connectBtn.html("Desconectar");
  }

  if (estado === "activa") {
    tiempoRestante = tiempo - int((millis() - tiempoInicio) / 1000);
    if (tiempoRestante <= 0) {
      estado = "exploto";
      setTimeout(reiniciarBomba, 3000);
    }
  }
}

function toggleConnection() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
  } else {
    port.close();
  }
}

function manejarEvento(e) {
  if (estado === "inactiva") {
    if (e === "A") tiempo = min(tiempo + 1, 60);
    if (e === "B") tiempo = max(tiempo - 1, 10);
    if (e === "S") activarBomba();
  }

  secuencia.push(e);
  if (secuencia.length > secuenciaCorrecta.length) {
    secuencia.shift();
  }

  if (JSON.stringify(secuencia) === JSON.stringify(secuenciaCorrecta)) {
    reiniciarBomba();
    secuencia = [];
    console.log("Bomba desactivada con clave secreta");
  }
}

function activarBomba() {
  estado = "activa";
  tiempoInicio = millis();
}

function reiniciarBomba() {
  estado = "inactiva";
  tiempo = 20;
  secuencia = [];
}

function dibujarBomba() {
  fill(255);
  if (estado === "inactiva") {
    text("⏱ " + tiempo + "s", width / 2, height / 2);
  } else if (estado === "activa") {
    text("💣 " + tiempoRestante + "s", width / 2, height / 2);
  } else if (estado === "exploto") {
    text("💥 BOOM 💥", width / 2, height / 2);
  }
}
```
Código control microbit
``` py
from microbit import *
import utime

while True:
    if button_a.is_pressed():
        uart.write("A")
        utime.sleep_ms(300)
    elif button_b.is_pressed():
        uart.write("B")
        utime.sleep_ms(300)
    elif accelerometer.was_gesture("shake"):
        uart.write("S")
        utime.sleep_ms(300)
```


