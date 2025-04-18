Codigo bomba en p5js

``` js
let tiempo = 20;
let estado = "inactiva";
let inicio;

function setup() {
  createCanvas(400, 300);
  textAlign(CENTER, CENTER);
  textSize(48);

  let btnIniciar = createButton("Activar bomba");
  btnIniciar.position(150, 250);
  btnIniciar.mousePressed(activarBomba);

  let btnSumar = createButton("+ tiempo");
  btnSumar.position(50, 250);
  btnSumar.mousePressed(() => {
    if (estado === "inactiva") {
      tiempo = min(tiempo + 1, 60);
    }
  });

  let btnRestar = createButton("- tiempo");
  btnRestar.position(280, 250);
  btnRestar.mousePressed(() => {
    if (estado === "inactiva") {
      tiempo = max(tiempo - 1, 10);
    }
  });
}

function draw() {
  background(30);
  dibujarBomba();

  if (estado === "activa") {
    let tiempoPasado = int((millis() - inicio) / 1000);
    let restante = max(0, tiempo - tiempoPasado);
    mostrarTiempo(restante);

    if (restante === 0 && estado !== "explotó") {
      estado = "explotó";
      setTimeout(reiniciarBomba, 3000);
    }
  } else if (estado === "inactiva") {
    mostrarTiempo(tiempo);
    mostrarTexto("Listo");
  } else if (estado === "explotó") {
    mostrarTexto("¡BOOM!");
  }
}

function activarBomba() {
  if (estado === "inactiva") {
    inicio = millis();
    estado = "activa";
  }
}

function reiniciarBomba() {
  estado = "inactiva";
  tiempo = 20;
}

function dibujarBomba() {
  fill(100);
  ellipse(width / 2, height / 2 - 20, 120, 120);
  stroke(255);
  line(width / 2, height / 2 - 80, width / 2, height / 2 - 50);
  noStroke();
  fill(255, 100, 0);
  ellipse(width / 2, height / 2 - 90, 20, 20);
}

function mostrarTiempo(t) {
  fill(255);
  textSize(40);
  text(t, width / 2, height / 2 + 50);
}

function mostrarTexto(msg) {
  fill(255);
  textSize(24);
  text(msg, width / 2, height / 2 + 90);
}
```
