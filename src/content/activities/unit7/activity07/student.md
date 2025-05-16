## Actividad 7

Configurar y usar VS Code Dev Tunnels: 4

Implementar arquitectura cliente-servidor (móvil->servidor): 3

Usar Socket.IO para retransmitir datos (servidor->escritorio): 4

Capturar y procesar eventos en el móvil (p5.js): 4

Modificar sistema interactivo para crear la experiencia: 3

Analizar y explicar flujo de datos completo (móvil->servidor->escritorio): 3

### ¿Qué concepto o actividad de esta unidad te resultó más fácil de entender o realizar? ¿Por qué crees que fue así?
El setup del devtunnel, port y todo lo que se debe hcer en terminal para iniciar el proyecto y ponerlo a funcionar. Creo que fue lo m[as f[acil por lo similar a la unidad anterior y porque lo hice en clase paso a paso con profesor.

### ¿Qué concepto o actividad te presentó mayor dificultad? ¿Qué pasos seguiste para intentar superarla? ¿Qué recursos o estrategias te fueron más útiles?
La actividad 5. similar a la unidad anterior la parte más dificil fue al momento de tener que modificar el caso para hacer otra cosa. Al igual que la unidad anterior, el truco fue tener paciencia y hacer un ejemplo no tan complejo, suficiente para entender bien el funcionamiento.
Hcaer el diagrama tambien me sigue costando.

### Describe con tus propias palabras, como si se lo explicaras a alguien que no tomó el curso, cuál es el flujo principal de información en la aplicación que construimos (desde la interacción del usuario en el móvil hasta la imagen en el escritorio). ¿Qué rol juega cada tecnología (Node.js, Socket.IO, Dev Tunnels, p5.js)?
La aplicación funciona así: 
El usuario interactúa con una página web en su celular hecha con p5.js, que capta movimientos o toques y los envía en tiempo real a un servidor local hecho con node.js y socket.io.
Dev tunnels permite que ese servidor sea accesible desde el celular. Luego, el servidor reenvía los datos a otra página en la computadora, donde se genera una imagen o animación según la información recibida.
Cada tecnología tiene un rol: p5.js maneja lo visual e interactivo, socket.io transmite los datos, node.js los gestiona en el servidor, y dev tunnels conecta el servidor local con el celular.

### ¿Cómo crees que podrías aplicar lo aprendido en esta unidad (usar un móvil como controlador, comunicación en tiempo real, túneles) en otros proyectos o contextos?
Podría usar lo aprendido para controlar videojuegos, instalaciones interactivas o robots usando el celular como control remoto. También serviría para hacer aplicaciones colaborativas en tiempo real o para conectar sensores físicos a visualizaciones en pantalla, incluso a distancia, gracias a los túneles.
Las posibilidades son casi ilimitadas, más con todas las nuevas tecnologías potentes que salen dia a dia. Solo es cuestión de usar las herramientas a disposición y con paciencia se pueden lograr muchisimos proyectos basados en lo aprendido esta unidad.
