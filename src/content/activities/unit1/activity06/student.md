### Actividad 6

Describe qué pasa en el punto 15 y cómo crees que esto se logre.
Describe qué pasa en el punto 16 y cómo crees que esto se logre.
Describe qué pasa en el punto 17 y cómo crees que esto se logre.

1. Al presionar los botones A o B, sale en pantalla un color respectivo asignado a cada botón (A es rojo, B amarillo). Esto funciona debido al codigo que se le cargó al microbit, el cual dice que lea si el microbit le esta entrando un input ya sea a los botones o al sensor de movimiento. Al preisonar el botón A, el microbit manda la señal A, que despues el codigo de p5.js interpreta y hace que el color en pantalla se vuelva rojo. Lo mismo pasa en el caso del botón B pero con color amarillo.
2. Al sacudir el micro bit el color en pantalla se vuelve verde. Al igual que en el caso de los botones, el micro ya tiene un codigo cargado que dice que hacer con los inputs recibidos. Para el movimiento el microbit manda la señal C que luego el programa de p5.js interpreta para poner en pantalla el color verde.
3. Al presionar send love las luces del microbit forman un corazón por un tiempo breve. En este caso el sistema funciona de manera inversa a las otras funciones de botones y movimiento. Para este caso, el sistema recibe la orden de mandar un output al microbit luego de presionar el botón send love del pc. Al ser presionada la función send love, el microbit recibe la orden de reproducir la imagen HEART.
