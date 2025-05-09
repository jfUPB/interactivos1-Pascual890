## Actividad  10

### Explicación concurrencia

El programa crea concurrencia utilizando una máquina de estados finita (FSM) y temporizadores no bloqueantes.
Esto permite que el microbit cambie entre imágenes automáticamente con base en el tiempo y responda a eventos de usuario (presionar el botón A) en cualquier momento.

No se usan sleep() ni pausas que bloqueen el flujo del programa, lo que significa que el sistema está siempre “escuchando” tanto el paso del tiempo como los botones.

Esto permite:

- Ejecutar varios comportamientos aparentemente en paralelo.

- Mantener la lógica organizada y controlada.

Ventajas de usar una máquina de estados

- Escalabilidad: fácil agregar más estados o condiciones.

- Facilita las pruebas y el mantenimiento del código.

- Control total sobre el comportamiento en cada estado.

### Vectores de prueba

#### Vector 1: Cambio de estado automático por tiempo

Condición inicial:

- El programa está en el estado HAPPY.

Evento:

- No se presiona ningún botón. Se espera que pasen 1500 ms.

Resultado esperado:

- El programa cambia al estado SMILE, muestra la cara sonriente y reinicia el temporizador con un nuevo intervalo.

Resultado obtenido:

- El cambio ocurre como se espera

#### Vector 2: Interrupción por botón A en estado HAPPY

Condición inicial:

- El programa está en el estado HAPPY.

Evento:

- El usuario presiona el botón A antes de que pasen los 1500 ms.

Resultado esperado:

- El programa interrumpe el ciclo, cambia al estado SAD, muestra la cara triste y ajusta el temporizador al nuevo intervalo.

Resultado obtenido:

- El cambio ocurre correctamente.

#### Vector 3: Interrupción por botón A en estado SAD

Condición inicial:

- El programa está mostrando la cara SAD.

Evento:

- El usuario presiona el botón A antes de que pasen los 2000 ms.

Resultado esperado:

- El programa cambia al estado SMILE, muestra la cara sonriente y ajusta el temporizador.

Resultado obtenido:

- Funciona como se espera.
