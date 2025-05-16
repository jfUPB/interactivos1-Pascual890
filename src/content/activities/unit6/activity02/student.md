# Actividad 2

### Pausa activa 1
#### ¿Qué pasaría si esa rampa se corta?

Si la conexión a Internet (ya sea Wi-Fi o por cable) se corta, no podré acceder a ningún sitio web ni enviar o recibir datos en línea.
Sería como si mi vehículo se quedara atrapado en el garaje, sin poder salir a las carreteras de Internet.
Algunas aplicaciones podrían seguir funcionando localmente, pero cualquier servicio que dependa de la red se detendría.

### Pausa activa 2
#### ¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?

En el ejemplo del restaurante, el cliente es la persona que ordena la comida, y el mesero o cocinero es el servidor. El cliente hace una petición (pide un plato del menú) y el servidor responde entregando el plato solicitado. 
Otro ejemplo sería pedir ayuda en una biblioteca: el usuario solicita un libro (cliente), y el bibliotecario lo busca y lo entrega (servidor).

### Pausa activa 3
#### Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?

Ejemplo:

URL: https://www.wikipedia.org/wiki/JavaScript

- Protocolo: https://

- Nombre de dominio: www.wikipedia.org

- Ruta: /wiki/JavaScript

Si escribo solo www.wikipedia.org, el navegador solicita la ruta por defecto. 
El servidor responde con la página principal del sitio, que es la página que se muestra si no se especifica una ruta.

### Pausa activa 4
#### Compara HTTP con los protocolos seriales que usaste. ¿Qué similitudes encuentras? ¿Qué diferencias clave ves? ¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?

Similitudes:

Ambos son protocolos de comunicación: definen cómo dos dispositivos intercambian información.

En ambos hay un emisor (cliente) y un receptor (servidor).

Diferencias:

HTTP es más complejo y estructurado; incluye encabezados, tipos de contenido, códigos de estado, etc.

Los protocolos seriales con el micro:bit suelen ser más simples: envían bytes con estructura mínima.

¿Por qué HTTP es más complejo?
Porque debe transmitir datos variados (HTML, imágenes, scripts) entre dispositivos muy distintos, a través de redes globales. Requiere más información para garantizar seguridad, compatibilidad y correcto funcionamiento.

### Pausa activa 5
#### ¿Qué parte crees que es HTML (ej. los campos de texto, el botón)? ¿Qué parte es CSS (ej. el color del botón, el tipo de letra)? ¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?

HTML: estructura básica del formulario, como los campos para usuario y contraseña, y el botón de enviar.

CSS: define el color del botón, el tipo de letra, el espaciado, y otros estilos visuales.

JavaScript: Js jala el programa, verifica que los campos no estén vacíos, muestra un mensaje de error si la contraseña es incorrecta sin recargar la página, o envía los datos al servidor mediante una petición.

### Pausa activa
#### Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”. ¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web? ¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?

Ventajas del modelo basado en eventos:

- Es más eficiente porque solo reacciona cuando algo realmente sucede.

- Evita usar recursos innecesarios si no hay cambios.

- Permite que el navegador gestione múltiples tareas sin bloquearse.

No sería eficiente un draw() a 60 fps en una página web. Redibujar toda la página 60 veces por segundo sería un desperdicio de recursos si nada ha cambiado. Además, haría que el navegador consuma mucha CPU y batería.

### Pausa activa
#### ¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?

Porque los desarrolladores pueden usar el mismo lenguaje en ambos lados, lo que facilita el aprendizaje y la escritura de código más coherente. 

También permite reutilizar funciones y lógica, y mejora la colaboración en equipos, ya que todos trabajan en el mismo stack.

### Pausa activa final
#### Resume con tus propias palabras la diferencia fundamental entre una comunicación HTTP tradicional y una comunicación usando WebSockets/Socket.IO. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?

HTTP: es una comunicación de ida y vuelta: el cliente hace una solicitud y el servidor responde. Se repite cada vez que se necesita algo nuevo.

WebSockets: permite una conexión continua, donde cliente y servidor pueden enviarse mensajes en cualquier momento, sin volver a abrir la conexión.

¿Dónde se usa esto?

En chats en tiempo real, juegos en línea, colaboración en vivo (como Google Docs), apps de seguimiento en tiempo real (como mapas o sensores conectados)




