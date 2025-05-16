Codigo bomba en p5js

``` js
let estado = "inactiva";
let tiempo = 20;
let tiempoRestante = 0;
let tiempoInicio = 0;

let secuencia = [];
let secuenciaCorrecta = ['A', 'B', 'A', 'S'];

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(32);

  let sumarBtn = createButton("+1s (A)");
  sumarBtn.position(50, 360);
  sumarBtn.mousePressed(() => manejarEvento('A'));

  let restarBtn = createButton("-1s (B)");
  restarBtn.position(150, 360);
  restarBtn.mousePressed(() => manejarEvento('B'));

  let activarBtn = createButton("Activar (S)");
  activarBtn.position(250, 360);
  activarBtn.mousePressed(() => manejarEvento('S'));
}

function draw() {
  background(30);
  dibujarBomba();

  if (estado === "activa") {
    tiempoRestante = tiempo - int((millis() - tiempoInicio) / 1000);
    if (tiempoRestante <= 0) {
      estado = "exploto";
      setTimeout(reiniciarBomba, 3000);
    }
  }
}

function manejarEvento(e) {
  if (estado === "inactiva") {
    if (e === "A") tiempo = min(tiempo + 1, 60);
    if (e === "B") tiempo = max(tiempo - 1, 10);
    if (e === "S") activarBomba();
  }

  // Detectar secuencia para desactivar la bomba
  secuencia.push(e);
  if (secuencia.length > secuenciaCorrecta.length) {
    secuencia.shift();
  }

  if (JSON.stringify(secuencia) === JSON.stringify(secuenciaCorrecta)) {
    reiniciarBomba();
    secuencia = [];
    console.log("Bomba desactivada por clave secreta!");
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
