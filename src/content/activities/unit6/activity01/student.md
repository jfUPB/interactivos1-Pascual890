## Reporte Actividad 1

### ¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?

Aparece una lista de paquetes siendo instalados. Se crea una carpeta node_modules.

Propósito: instalar las dependencias definidas en package.json para que el proyecto pueda funcionar correctamente.

Algunos paquetes necesitaban fix. Se usó npm audit fix

### ¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?

Sale el siguiente mensaje:
Server is listening on http://localhost:3000

Esto indica que el servidor ya está funcionando y listo para recibir conexiones, escuchando peticiones en el puerto 3000.

### Describe lo que ves inicialmente en page1 y page2 en tu navegador.

Se ve inicialmente en cada page una bola roja con un palo conectado. Al momento de abrir las dos juntas se sincronizan y se conectan con el palo negro. Si se mueve alguna ventana el programa se va sincronizando.

### ¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?

A user connected
A user connected

Ese mensaje sale cada vez que se abre una page. Si se cierra sale que se desconecto el usuario. si se actualiza se desconecta y se conecta nuevamente.

### Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?

Visualmente se ve como en tiempo real se sincronizan las posiciones y se mueve el palo para amntener ambas bolas conectadas. 

En la consola del browser sale algo como: {x: 115, y: 312, width: 492, height: 323}

Cada que se mueve la otra ventana se van actualizando estos datos.
