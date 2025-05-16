## Actividad 5

## Explica los cambios clave que realizaste en mobile/sketch.js: ¿Qué datos envías ahora y cómo/cuándo los envías? Pega fragmentos de código relevantes.
Envío de Color y Stroke:
Se añadió el envío del color y si usar borde (stroke) junto con la posición del toque.

Ejemplo:
``` js
let touchData = {
    type: 'touch',
    x: mouseX,
    y: mouseY,
    color: currentColor,   // Color de la partícula
    stroke: true            // Usar borde
};
``` 
Envío de Datos al Mover el Toque:
Los datos del toque se envían solo si el toque se mueve más de un umbral.

Ejemplo:
``` js
if (dx > threshold || dy > threshold || lastTouchX === null) {
    socket.emit('message', JSON.stringify(touchData));
}
Cambio de Color Automático:
El color de la partícula cambia automáticamente cada 5 segundos.
``` 
Ejemplo:
``` 
setInterval(() => {
    currentColor = colors[colorIndex];
    console.log('Color changed to:', currentColor);
}, 5000);
``` 
## Explica los cambios clave que realizaste en desktop/sketch.js: ¿Cómo recibes e interpretas los datos? ¿Qué modificaste en setup() o draw() para lograr el nuevo efecto? Pega fragmentos de código relevantes.
Recepción de datos:

Se reciben las coordenadas (x, y), el color y el estado del borde (useStroke) desde el servidor.

Código relevante
``` js
socket.on('message', (data) => {
    let parsedData = JSON.parse(data);
    if (parsedData && parsedData.type === 'touch') {
        circleX = parsedData.x;
        circleY = parsedData.y;
        circleColor = parsedData.color || '#ff0000';
        useStroke = parsedData.useStroke || false;
        receivedData = true;
    }
});
``` 
Cambio automático de color:

El color cambia cada 5 segundos entre un conjunto de colores predefinidos.

Código relevante
``` js
setInterval(() => {
    colorIndex = (colorIndex + 1) % colors.length;
    currentColor = colors[colorIndex];
}, 5000);
``` 
Dibujo del círculo:

Se dibuja el círculo con el color recibido o el color automático, y con o sin borde dependiendo de useStroke.

Código relevante
``` js
function draw() {
    if (receivedData) {
        if (useStroke) {
            stroke(0);
            strokeWeight(2);
        } else {
            noStroke();
        }
        fill(currentColor);
        ellipse(circleX, circleY, 50, 50);
    }
}
```
## Si modificaste server.js, explica por qué fue necesario y qué cambiaste.
No se modifico
