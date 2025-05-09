## Análisis Código
Funcionamiento del Código

Se define la clase Pixel, que controla el encendido y apagado de un LED en la matriz del micro:bit con un intervalo de tiempo determinado.
Se crean dos píxeles (pixel1 y pixel2) con diferentes posiciones y tiempos de parpadeo (1s y 0.5s).
En un bucle infinito, cada píxel alterna su estado de brillo (9 - 0) cuando el tiempo transcurrido supera su intervalo.
### Estados Identificados
"Init" → Se establece el tiempo de inicio y se enciende el LED.

"WaitTimeout" → Se espera hasta que pase el tiempo definido para cambiar el estado del LED.

### Eventos Identificados
Creación del píxel (state == "Init").

Verificación de si ha pasado el tiempo (utime.ticks_diff() > interval).

### Acciones Identificadas
Encender el LED en "Init".

Alternar entre encendido y apagado en "WaitTimeout".

El código implementa un modelo de máquina de estados en el que cada Pixel tiene estados bien definidos y reacciona a eventos de tiempo. Este enfoque modular permite manejar múltiples píxeles con diferentes intervalos de parpadeo, lo que hace el programa flexible y escalable.
