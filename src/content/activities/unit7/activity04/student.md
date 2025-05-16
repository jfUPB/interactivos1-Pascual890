## Actividad 4


### Describe el propósito principal de mobile/sketch.js y desktop/sketch.js.
mobile/sketch.js: Captura movimientos táctiles en el móvil y los envía al servidor en JSON si superan un umbral. <br/>
desktop/sketch.js: Recibe esos datos y dibuja un círculo rojo en la posición indicada.<br/>

### Explica la función touchMoved en el móvil, incluyendo el uso del threshold y JSON.stringify.
<p align = "center">Detecta movimiento táctil<p/>
threshold evita enviar datos por cambios mínimos<br/>
JSON.stringify convierte el objeto con coordenadas a string para enviarlo por el socket<br/>

### Explica cómo el cliente de escritorio recibe (socket.on) y procesa (JSON.parse, chequeo de type) los datos para actualizar la posición del círculo.
<p align = "center">socket.on recibe los datos<p/>
JSON.parse convierte la cadena en objeto<br/>
Si el type es 'touch', actualiza la posición del círculo con las coordenadas recibidas<br/>

### Responde a las preguntas de reflexión de las secciones del móvil y del escritorio

#### Reflexión (Móvil)


#### ¿Por qué usar JSON ({type: 'touch', x, y}) y no solo "x,y"?
JSON permite enviar datos estructurados y escalables, facilita agregar más información y es más legible 

#### ¿Qué pasa si quitas el threshold?
Se enviarían demasiados datos por cada pequeño movimiento, sobrecargando la red y afectando el rendimiento y la fluidez, posibles recalentameientos por cantidad de envios y recibos

#### ¿Cómo adaptar el código para clic del ratón?
Usar mouseMoved() o mouseDragged() y replicar la lógica de touchMoved() para enviar la posición del mouse


#### Reflexión (Escritorio)


#### ¿Por qué usar JSON.parse() con try...catch?
Previene errores si los datos llegan corruptos o malformados, evitando que el programa se detenga

#### ¿Qué hacer si los canvas tienen distintos tamaños?
Usar map() para escalar las coordenadas del móvil al tamaño del canvas del escritorio:
circleX = map(obj.x, 0, 300, 0, 600);
circleY = map(obj.y, 0, 300, 0, 600);

#### ¿Qué cambiar si el servidor usa 'updateDesktop' en lugar de 'message'?
Cambiar el nombre del evento en el socket.on:
socket.on('updateDesktop', (data) => { ... });

