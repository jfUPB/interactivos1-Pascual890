## Actividad 3 

### ¿Por qué crees que es útil usar módulos o librerías en lugar de escribir todo desde cero? ¿Qué ventajas aporta? Anota tus ideas en la bitácora.

Usar módulos o librerías en lugar de escribir todo desde cero es útil por varias razones:

- Ahorro de tiempo: Los módulos ya están probados y listos para usar, lo que permite enfocarse en la lógica de la aplicación en lugar de reinventar funciones.

- Menos errores: Las librerías populares han sido desarrolladas y revisadas por muchas personas, por lo que son más confiables que escribir código desde cero.

- Código más limpio y organizado: Usar módulos permite dividir responsabilidades y mantener el código más claro.

- Compatibilidad: Estas herramientas ya manejan muchos detalles técnicos y ayudan a seguir buenas prácticas sin tener que conocer todos los detalles de bajo nivel.

- Comunidad y documentación: Las librerías populares tienen buena documentación y soporte de la comunidad, lo que facilita aprender y solucionar problemas rápidamente.

Basicamente, el uso de librerias o módulos ayuda a que los desarrolladores a nivel global puedan usar recursos ue se han pulido efectivamente por otros desarrolladores,
permitiendo que todos esten en la misma página y que el desarrollo de un programa se facilite

### ¿Qué ocurre? ¿Por qué? ¿Qué mensaje ves en el navegador o en su consola de desarrollador (F12)?

Cuando cambié la línea y luego inicié el servidor y traté de abrir http://localhost:3000/page1.html, el navegador mostró un error. Específicamente, recibí un mensaje como:

Cannot GET /page1.html

También, en la consola del navegador (F12 → Consola), no se pudo cargar el archivo solicitado, y en la terminal del servidor no se imprimió nada nuevo.

Esto ocurre porque la carpeta 'archivos_cliente' no existe, y por lo tanto el servidor no encuentra ningún archivo. 
Express busca los archivos estáticos en la carpeta que se le indique, y si no hay nada allí, no puede responder a la petición del browser.

### Intenta acceder a http://localhost:3000/page1. ¿Funciona? Ahora intenta acceder a http://localhost:3000/pagina_uno. ¿Funciona? ¿Qué te dice esto sobre cómo el servidor asocia URLs con respuestas? Restaura el código.

Acceso a /page1 después de cambiar la ruta a /pagina_uno:
Cuando intenté acceder a http://localhost:3000/page1, no funcionó. El navegador mostró un error "Cannot GET /page1"

Acceso a /pagina_uno:
Sí funcionó correctamente. El servidor respondió con el archivo page1.html como se esperaba.

Esto demuestra que el servidor solo responde a las URLs que se le han definido explícitamente mediante app.get(). 
Si no existe una ruta exacta, el servidor no sabe qué enviar y responde con un error, por eso es importante tener definidas correctamente las rutas para cada recurso que quieras servir.

### Abre http://localhost:3000/page1 en una pestaña. Observa la terminal del servidor. ¿Qué mensaje ves? Anota el ID. Abre http://localhost:3000/page2 en OTRA pestaña. Observa la terminal. ¿Qué mensaje ves? ¿El ID es diferente? Cierra la pestaña de page1. Observa la terminal. ¿Qué mensaje ves? ¿Coincide el ID con el que anotaste? Cierra la pestaña de page2. Observa la terminal.

A user connected - ID: J28LKnSrXhHPc0A9AAAB
A user connected - ID: sCQwO_J8a0eSKN9hAAAD
User disconnected - ID: sCQwO_J8a0eSKN9hAAAD
User disconnected - ID: J28LKnSrXhHPc0A9AAAB

Se puede observar que cada conexion que se hace genera un ID al conectarse a cada page, es decir, 2 IDs diferentes en este caso, como se ve en el ejemplo. 
Al desconectarse, se ve el mismo id que cuando se conectó, permitiendo saber cual page se cerró.

### Mueve la ventana de page1. Observa la terminal del servidor. ¿Qué evento se registra (win1update o win2update)? ¿Qué datos (Data:) ves? Mueve la ventana de page2. Observa la terminal. ¿Qué evento se registra ahora? ¿Qué datos ves?
### Experimento clave: cambia socket.broadcast.emit(‘getdata’, page1); por socket.emit(‘getdata’, page1); (quitando broadcast). Reinicia el servidor, abre ambas páginas. Mueve page1. ¿Se actualiza la visualización en page2? ¿Por qué sí o por qué no? (Pista: ¿A quién le envía el mensaje socket.emit?). Restaura el código a broadcast.emit.

Received win1update from ID: zPFp29Zh8osQPic3AAAB Data: { x: 0, y: 0, width: 1699, height: 941 }

Received win2update from ID: AaXfsowDMLhUbxPoAAAD Data: { x: 0, y: 0, width: 1699, height: 941 }

Algo asi se ven los datos que salen. Al momento de hacer cualquier cambio a una ventena, se va actualizando el mensaje con la posición y tamaño actuales de la page. 
Dependiendo de que ventana sea sale win1update o win2 update.

Si cambio esto:

socket.broadcast.emit('getdata', page1);

por esto:

socket.emit('getdata', page1);

Y luego muevo page1, page2 no veo el cambio porque sólo se le está devolviendo la información al mismo cliente.

### Inicia el servidor. ¿Qué mensaje ves en la consola? ¿En qué puerto dice que está escuchando? Intenta abrir http://localhost:3000/page1. ¿Funciona? Intenta abrir http://localhost:3001/page1. ¿Funciona? ¿Qué aprendiste sobre la variable port y la función listen? Restaura el puerto a 3000.

Server is listening on http://localhost:3001

http://localhost:3000/page1 - NO funciona
Muestra error de no poder acceder al sitio porque el servidor ya no está escuchando en ese puerto.

http://localhost:3001/page1 - SÍ funciona
Aquí es donde el servidor está activo ahora, así que carga correctamente la página.

- El número de puerto define dónde se debe hacer la conexión.

- Si el servidor está escuchando en un puerto distinto (3001, 4000, etc.), los clientes deben conectarse a ese puerto exacto.

- La función server.listen(port, ...) lanza el servidor, y el console.log() confirma que todo salió bien.








