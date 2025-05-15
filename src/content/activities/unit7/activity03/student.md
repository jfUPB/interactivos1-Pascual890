### Actividad 3

## ¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?
app.get('/ruta', ...) Se usa para acceder desde un directorio especificado <br/>
express.static('public') Se usa para que uno escriba la direccion HTTP y retorne lo que uno necesite <br/>

## Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?
Primero, el telefono envia un llamado messages <br/>
Segundo, el servidor recibe el message con el socket <br/>
Tercero, El servidor emite una respuesta usando el socket broadcast a todos menos el móvil <br/>
Cuarto, Los clientes reciben el mensaje de su socket message <br/>
Ultimo, Se usa el socket para enviar a todo los clientes incluyendo el movil que inicio el envío <br/>

## Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?
Ambos computadores recibiran la señal ya que el brodcast se hace de manera masiva a todos quienes escuchen

## ¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?
Los console.log muestran mensajes en la consola de cuando se desconecta o conecta junto con el ID, del socket.id
ademas, cada vez que el movil actuializa la información se envia al log la nueva posición. 
