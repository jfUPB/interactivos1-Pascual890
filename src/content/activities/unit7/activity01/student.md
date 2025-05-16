## Actividad 1

### ¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?
Obtuve esta URL https://5f10b98h-3000.use2.devtunnels.ms/mobile/
no se puede con local host debido a que el dispossitivo externo no es local, se podria con la ip local
unicamente si ambos dispositivos se encuentran en la misma red. El Dev Tunnel permite o da la libertad
de usarse en cualquier disposito donde sea

### Describe brevemente qué hace npm install y npm start.
la instruccion npm install se usa para descargar las librerias que se van a utilizar, descarga e instala
por otro lado npm start ejecuta el proyecto siempre y cuando este configurado el package.json

### ¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?
sfinteractivesocketiodesktopmobile@1.0.0 start
node server.js
Server is listening on http://localhost:3000
New client connected
New client connected
lo cual indica que ambos clientes lograron conectarse exitosamente 
### Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?
Si, la interaccion funciono como se esperaba. El servidor recibio el touch desde el dispositivo 
En cuanto al delay no se encontro bajo las condiciones que la prueba fue ejecutada
