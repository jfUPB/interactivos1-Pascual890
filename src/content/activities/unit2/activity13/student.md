## Reflexión actividad bomba

Al reflexionar sobre el diseño de la máquina de estados para la bomba temporizada, considero que la estructura de tres estados (CONFIGURACION, CUENTA_REGRESIVA, EXPLOSION) fue una decisión acertada y la más natural para modelar el ciclo de vida del dispositivo. 
Esta división facilitó la organización del código y la separación clara de responsabilidades: configuración inicial, operación activa y estado final. 
Sin embargo, una dificultad inherente al diseño implementado se trata la naturaleza de utime.sleep(1) dentro del estado CUENTA_REGRESIVA, ya que puede bloquear ciertas funciones. 
Aunque garantiza un conteo por segundos simple de implementar, impide que el sistema reaccione a otros eventos (como presionar botones) durante esa pausa de un segundo. 
Como principal mejora, se podría rediseñar la gestión del tiempo usando utime.ticks_ms() para crear un temporizador no bloqueante. 
Esto permitiría verificar otros sensores o entradas de forma concurrente, haciendo el sistema más reactivo y abriendo la puerta a funcionalidades más complejas, como la posibilidad de pausar o modificar el tiempo durante la cuenta atrás.
Además, podría buscar una manera en que la configuración inicial de tiempo sea mas rápida y responsiva a la hora de sumar o restar el tiempo de la bomba
Adicionalmente, se podría refinar el feedback al usuario, quizás con patrones de luz o sonido distintos para los estados de aborto y reinicio post-explosión, mejorando la claridad de la interacción.
