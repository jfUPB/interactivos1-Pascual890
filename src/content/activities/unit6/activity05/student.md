## Actividad 5

### Concepto: Ventilador direccional

Page1: Tiene una pelota u objeto flotando en el centro de la ventana.

Page2: Representa el ventilador. Su posición en la pantalla define la dirección del viento.

La dirección del viento se calcula como el vector que va desde Page2 hacia Page1.

Ese vector se usa en Page1 para aplicar una fuerza que mueve la pelota, como si el ventilador empujara.

### Plan técnico

Comunicación

Page2: Envía su posición de ventana al servidor (win2update).

Servidor: Reenvía a Page1 con un getwind o puedes seguir usando getdata.

Page1: Recibe la posición de Page2 y calcula la dirección del viento.

Movimiento

- En Page1, tienes una pelota con x, y, vx, vy.

- Cada frame, calculas un vector desde Page2 hacia Page1 (ventanaPage2 → ventanaPage1) y lo usas para aumentar vx, vy.

- También puedes agregar algo de fricción para que no se mueva infinitamente.

### Código

Server.js

Este código se dejó igual a como se habia trabajado en actividad anterior. no hubo necesidad de cambios.
``` js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const path = require('path');
const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

let page1 = { x: 0, y: 0, width: 100, height: 100 };
let page2 = { x: 0, y: 0, width: 100, height: 100 };

app.use(express.static(path.join(__dirname, 'views')));

app.get('/page1', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page1.html'));
});

app.get('/page2', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page2.html'));
});

io.on('connection', (socket) => {
    console.log('A user connected - ID:', socket.id);
    socket.on('disconnect', () => {
        console.log('User disconnected - ID:', socket.id);
    });

    socket.on('win1update', (window1, sendid) => {
        console.log('Received win1update from ID:', socket.id, 'Data:', window1); // Log para ver qué llega
        page1 = window1; // Actualiza la información del estado de page1 en el servidor

        // Envía la información actualizada de page1 a TODOS los demás clientes conectados
        socket.broadcast.emit('getdata', page1);
    })

    socket.on('win2update', (window2, sendid) => {
        console.log('Received win2update from ID:', socket.id, 'Data:', window2); // Log para ver qué llega
        page2 = window2; // Actualiza la información del estado de page2 en el servidor

        // Envía la información actualizada de page2 a TODOS los demás clientes conectados
        socket.broadcast.emit('getdata', page2);
    })
});

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
```

page 1

``` js
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
}

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point1 = [currentPageData.width / 2, currentPageData.height / 2]

let socket = io('http://localhost:3000');

let pelota;
let velocidad;

socket.on('connect', () => {
    socket.emit('win1update', currentPageData, socket.id);
});

socket.on('getdata', (dataWindow) => {
    remotePageData = dataWindow;
});

let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};

function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
    pelota = createVector(width / 2, height / 2);
    velocidad = createVector(0, 0);
}

function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y ||
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {

        point1 = [currentPageData.width / 2, currentPageData.height / 2];
        socket.emit('win1update', currentPageData, socket.id);
        previousPageData = currentPageData;
    }
}

function draw() {
    background(220);
    checkWindowPosition();

    // Cálculo del viento: vector desde page2 hacia esta ventana
    let pos1 = createVector(currentPageData.x, currentPageData.y);
    let pos2 = createVector(remotePageData.x, remotePageData.y);
    let viento = p5.Vector.sub(pos1, pos2); // viento viene desde page2
    viento.normalize().mult(0.2); // reduce la fuerza del viento

    // Aplica el viento a la pelota
    velocidad.add(viento);
    pelota.add(velocidad);
    velocidad.mult(0.95); // fricción para que no se acelere infinitamente

    // Rebote en bordes
    if (pelota.x < 0 || pelota.x > width) {
        velocidad.x *= -1;
        pelota.x = constrain(pelota.x, 0, width);
    }
    if (pelota.y < 0 || pelota.y > height) {
        velocidad.y *= -1;
        pelota.y = constrain(pelota.y, 0, height);
    }

    // Dibuja pelota
    fill(0, 100, 255);
    ellipse(pelota.x, pelota.y, 50, 50);
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}
```

page2
```js
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight

}

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point2 = [currentPageData.width / 2, currentPageData.height / 2];
let socket = io('http://localhost:3000')

socket.on('connect', () => {
    console.log(socket.id);
    socket.emit('win2update', currentPageData, socket.id);
});

socket.on('getdata', (dataWindow) => {
    // Actualiza los datos de la ventana remota con la información recibida
    remotePageData = dataWindow;
    console.log('Page 2 received data about the other window:', remotePageData);
});


let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};


function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
}


function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y ||
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {

        console.log("Page 2 detected change, sending update:", currentPageData); // Log para saber cuándo enviamos
        point2 = [currentPageData.width / 2, currentPageData.height / 2];
        // Si hubo cambios, envía el nuevo estado al servidor
        socket.emit('win2update', currentPageData, socket.id);
        previousPageData = currentPageData; // Actualiza el estado anterior para la próxima comparación
    }
}


function draw() {
    background(220);
    checkWindowPosition();

    // Calcular la posición relativa de la otra ventana
    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let resultingVector = p5.Vector.sub(vector2, vector1);
    let distancia = resultingVector.mag();
    let maxDistancia = 1000;

    let remoteCenterX = resultingVector.x + remotePageData.width / 2;
    let remoteCenterY = resultingVector.y + remotePageData.height / 2;

    // Dibuja ventilador en el centro
    drawVentilador(point2[0], point2[1]);
    angle += 0.05;
}

let angle = 0;

function draw() {
    background(220);
    checkWindowPosition();

    // Calcular la posición relativa de la otra ventana
    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let resultingVector = p5.Vector.sub(vector2, vector1);
    let distancia = resultingVector.mag();
    let maxDistancia = 1000;

    let remoteCenterX = resultingVector.x + remotePageData.width / 2;
    let remoteCenterY = resultingVector.y + remotePageData.height / 2;

    // Dibuja ventilador en el centro de la pantalla
    drawVentilador(point2[0], point2[1]);
    angle += 0.05;
}

function drawVentilador(x, y) {
    push();
    translate(x, y);

    // Base del ventilador
    fill(80);
    noStroke();
    ellipse(0, 0, 100, 100);

    // Aspas giratorias
    stroke(0);
    strokeWeight(2);
    fill(150, 150, 255);
    for (let i = 0; i < 4; i++) {
        let a = angle + i * HALF_PI;
        let bladeLength = 60;
        triangle(
            0, 0,
            cos(a) * bladeLength, sin(a) * bladeLength,
            cos(a + 0.3) * bladeLength * 0.6, sin(a + 0.3) * bladeLength * 0.6
        );
    }

    pop();
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}

```
### Enlace video proyecto funcionando

https://youtu.be/dcyWUBw86I4

### Breve reflexión sobre el proceso de modificación: ¿Qué fue fácil? ¿Qué fue difícil? ¿Qué aprendiste al aplicar los conceptos?

Teniendo en cuenta como me cuesta el código, se puede decir que no hubo nada fácil. De pronto la pare mas facil fue entender la explicación del caso base y que hace cada parte.
Pero luego al momento de implementar lo visto fue más complicado.

Dificil fue saber que pasos debía seguir luego de pensar en un ejemplo para realizar, puesto que como dije antes se me hace duro cambiar un código y lo dañé varias veces. De hecho, me tocó hacer un ejemplo más sencillo entre todas las posibles ideas qe tuve.

Aprendí la importancia de saber usar todos los programas y terminales para lograr depurar y desarrollar un proyecto. Si bien este debe tener cosas por corregir, siento que sirvió para aprender los conceptos de la unidad.







