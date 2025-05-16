## Actividad 2

### Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?
Esto se necesita para poder ejecturar el programa desde cualquier parte y desde cualquier dispositivo sin limitaciones como el donde se ejecuta y configuraciones de las redes locales

### ¿Por qué usamos JSON.stringify() en el emisor (móvil) y JSON.parse() en el receptor (escritorio)? ¿Qué problema resuelve JSON aquí?
Esto lo usamos ya que necesitamos convertir objetos en texto para enviarlos por red y luego reconstruirlos en el receptor

### Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.
touchMoved() detecta el movimiento que se generea en la pantalla tactic y threshold es para optimizar la red

### ¿Qué otros eventos táctiles existen en p5.js y para qué tipo de interacciones podrían ser útiles (ej. un botón virtual, detectar un tap)?
touchStarted() y touchEnded() permiten detectar toques iniciales y finales

### Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?
La ip es mas rapida y no depende de servicios externos, pero esta solo funciona de manera local (o wifi si no hay firewalls impidiendo)
Dev Tunnels puede ser algo mas lenta pero tiene la facilidad de poderse ejecutar desde fuera del entorno local. En cuanto a seguridad 
la opcion de ip local es mas segura ya que esdesde la misma red que se ejecuta, dev usa la isp por lo
que puede ser algo mas vulnerable.
