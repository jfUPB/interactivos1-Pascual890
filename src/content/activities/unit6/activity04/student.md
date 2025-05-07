## Actividad 4 

### Detén el servidor Node.js (Ctrl+C). Refresca la página page2.html. Observa la consola del navegador. ¿Ves algún error relacionado con la conexión? ¿Qué indica? Vuelve a iniciar el servidor y refresca la página. ¿Desaparecen los errores?

Con el servidor corriendo, abri page2.html - No aparece ningún error en la consola del navegador.

La conexión con Socket.IO se establece correctamente.

Detuve el servidor y refresqué la página:

En la consola aparece un error

Esto indica que el cliente no puede conectarse al servidor porque está apagado.

Reinicié el servidor y di refresh

Los errores desaparecen y la conexión vuelve a funcionar normalmente.

Conclusión: El cliente depende completamente del servidor para establecer comunicación. Si el servidor no está disponible, el navegador mostrará errores de conexión en la consola.

### ¿Qué pasó en page1 antes de que movieras page2? ¿Tenía la información correcta sobre page2 desde el principio? ¿Por qué es útil enviar el estado inicial al conectarse? Descomenta la línea.

Comenté la línea socket.emit('win2update', currentPageData, socket.id);

El cliente ya no envía el estado inicial al conectarse.

Reinicié el servidor y abri page1.html y page2.html.

Antes de mover la ventana de page2, en page1 no se mostraba ninguna información sobre page2. Esto ocurre porque el servidor nunca recibió datos iniciales de page2 al conectarse.
Después de mover la ventana de page2, entonces sí se actualizó y apareció en page1.

Conclusión:
Enviar el estado inicial justo al conectarse es importante para que el servidor tenga información actual desde el primer momento, y para que los otros clientes (como page1) puedan visualizar correctamente sin tener que esperar una acción (como mover la ventana).

### Asegúrate de tener este console.log en page2.js. Abre ambas páginas. Mueve la ventana de page1. Observa la consola del navegador de page2. ¿Se dispara el log “Page 2 received…”? ¿Qué datos muestra? Mueve la ventana de page2. Observa la consola de page2. ¿Se dispara este log? ¿Por qué sí o por qué no? (Pista: ¿Quién envía el evento getdata?)

Al mover la ventana de page1, en la consola de page2 sí aparece el log:

Page 2 received data about the other window: Object height: 432width: 492x: -38y: 122[[Prototype]]: Object

Al mover la ventana de page2, NO se dispara este log en page2 porque socket.broadcast.emit('getdata', ...) no se reenvía a sí mismo. 
Solo los otros clientes (como page1) recibirán ese evento.

### Mueve la ventana de page2 muy lentamente. Observa la consola de page2. ¿Cuándo aparece el mensaje “Page 2 detected change…”? Deja la ventana de page2 quieta. ¿Aparece el mensaje? ¿Por qué es eficiente esta estrategia de comparar con el estado anterior antes de enviar datos por la red? Anota tu reflexión.

Al mover la ventana de page2 lentamente, el mensaje aparece solo cuando cambia la posición o el tamaño, incluso si el cambio es mínimo. Eso indica que el sistema está detectando correctamente los cambios reales.

Cuando se deja la ventana quieta, ya no aparece el mensaje. Esto confirma que no se están enviando datos innecesarios mientras no haya movimiento.

Comparar el estado actual con el anterior evita enviar información repetida, lo cual reduce el tráfico de red y mejora la eficiencia. 
Solo se envía una actualización cuando realmente hay un cambio relevante, lo cual es esencial para mantener el sistema ligero y reactivo en aplicaciones en tiempo real como esta.

### COdigo modificado

``` js
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
    drawCircle(point2[0], point2[1]);

    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let resultingVector = p5.Vector.sub(vector2, vector1);

    let distancia = resultingVector.mag();
    let maxDistancia = 1000; 

    let colorCerca = color(0, 255, 0); // verde
    let colorLejos = color(255, 0, 0); // rojo
    let mezcla = constrain(distancia / maxDistancia, 0, 1);
    stroke(lerpColor(colorCerca, colorLejos, mezcla));
    strokeWeight(10);

    let remoteCenterX = resultingVector.x + remotePageData.width / 2;
    let remoteCenterY = resultingVector.y + remotePageData.height / 2;

    drawCircle(remoteCenterX, remoteCenterY);
    line(point2[0], point2[1], remoteCenterX, remoteCenterY);
}

function drawCircle(x, y) {
    fill(255, 0, 0);
    ellipse(x, y, 150, 150);
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}
```

