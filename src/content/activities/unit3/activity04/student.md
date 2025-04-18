## Controlador bomba
```js
let port;
let connectBtn;

function setup() {
  createCanvas(400, 200);
  background(220);
  port = createSerial();
  connectBtn = createButton('Conectar al micro:bit');
  connectBtn.position(20, 20);
  connectBtn.mousePressed(toggleConnection);
  connectBtn.html(port.opened() ? 'Desconectar' : 'Conectar al micro:bit');

  let btnA = createButton('Enviar A');
  btnA.position(20, 70);
  btnA.mousePressed(() => enviarEvento('A'));

  let btnB = createButton('Enviar B');
  btnB.position(120, 70);
  btnB.mousePressed(() => enviarEvento('B'));

  let btnS = createButton('Enviar S (Shake)');
  btnS.position(220, 70);
  btnS.mousePressed(() => enviarEvento('S'));
}

function draw() {
  background(220);
  textSize(16);
  textAlign(CENTER, CENTER);
  text(
    port.opened() ? 'Conectado al micro:bit' : 'No conectado',
    width / 2,
    150
  );

}

function toggleConnection() {
  if (!port.opened()) {
    port.open('MicroPython', 9600);
  } else {
    port.close();
  }
}

function enviarEvento(valor) {
  if (port.opened()) {
    port.write(valor + '\n');
    console.log('Enviado:', valor);
  } else {
    console.warn('Puerto no conectado.');
  }
}
```
