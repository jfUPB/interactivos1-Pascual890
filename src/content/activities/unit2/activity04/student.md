## Actividad 4 Unidad 2

### Experimento 1

#### ¿Qué querías comprobar?
Quería verificar si un solo programa en el micro:bit puede detectar de forma independiente las pulsaciones de los botones A y B, mostrando "A" en la pantalla cuando se presiona A y "B" cuando se presiona B. 
También quería observar qué sucede si no se presiona ninguno o si se presionan ambos al mismo tiempo.

#### ¿Cuál fue tu hipótesis?
Mi hipótesis es que dentro del bucle principal (while True), puedo usar una estructura condicional (if/elif/else) para comprobar el estado de ambos botones. 
Primero comprobaré si se presiona A, luego si se presiona B, y si ninguno se presiona se limpiará la pantalla. 
Creo que el programa podrá distinguir entre las pulsaciones y reaccionar mostrando la letra correcta. 
Para el caso de presionar ambos simultáneamente, anticipo que podría mostrar solo "A" (si esa condición se comprueba primero) o quizás necesite una lógica adicional si quiero un comportamiento específico para esa combinación. 
Actualización de hipótesis tras reflexión: Una estructura if/elif/else más completa debería comprobar primero si ambos están presionados, luego si solo A lo está, luego si solo B lo está, y finalmente el caso en que ninguno lo está.

#### Código:

```py
from microbit import *

while True:
    a_presionado = button_a.is_pressed()
    b_presionado = button_b.is_pressed()

    if a_presionado and b_presionado:
        display.show("AB")
   
    elif a_presionado:
        display.show("A")
   
    elif b_presionado:
        display.show("B")
    
    else:
        display.clear()

    sleep(100)
```
#### Descripción de los resultados:

Al iniciar el programa, la pantalla LED estaba apagada.
Al presionar solo el botón A, la pantalla mostró la letra "A". Al soltarlo, la pantalla se apagó.
Al presionar solo el botón B, la pantalla mostró la letra "B". Al soltarlo, la pantalla se apagó.
Al presionar ambos botones (A y B) simultáneamente, la pantalla mostró las letras "AB". Al soltar ambos (o uno de ellos), la pantalla cambió para mostrar la letra del botón que quedaba presionado o se apagó si se soltaron ambos.
Mientras no se presionaba ningún botón, la pantalla permanecía apagada.

#### Análisis de esos resultados:

Los resultados coinciden con la hipótesis actualizada y el comportamiento esperado del código.
La clave está en la estructura if/elif/else. El programa evalúa las condiciones en orden:
Primero verifica a_esta_presionado and b_esta_presionado. Si ambos son True, muestra "AB" y salta el resto de elif y else en esa iteración del bucle.
Si la primera condición es False, verifica elif a_esta_presionado. Si es True (y por la lógica anterior, b_esta_presionado debe ser False), muestra "A" y salta el resto.
Si las dos primeras condiciones son False, verifica elif b_esta_presionado. Si es True (y a_esta_presionado es False), muestra "B" y salta el else.
Si ninguna de las condiciones anteriores es True, significa que ambos botones están sin presionar, por lo que se ejecuta el bloque else, limpiando la pantalla.
Leer el estado de los botones (is_pressed()) al inicio de cada ciclo y guardarlos en variables (a_esta_presionado, b_esta_presionado) asegura que se use una lectura consistente dentro de la misma iteración del bucle.
El orden de las comprobaciones es importante, especialmente al verificar la condición combinada (and) primero para manejar correctamente el caso de pulsación simultánea.

#### Conclusiones:

El experimento demuestra que es perfectamente posible monitorizar múltiples entradas digitales (botones A y B) dentro de un único programa y reaccionar de manera diferente según qué entrada esté activa o qué combinación de entradas lo esté.
La estructura if/elif/else es una herramienta fundamental en programación para tomar decisiones basadas en múltiples condiciones excluyentes o priorizadas.
Se ha gestionado con éxito el caso de la pulsación simultánea dándole una salida específica ("AB"), mostrando la flexibilidad del sistema.


### Experimento 2

#### ¿Qué querías comprobar?
Quería comprobar si el micro:bit V2 puede detectar cuándo se toca el logo dorado en la parte frontal y cómo se representa esta acción.

#### ¿Cuál fue tu hipótesis?
Dado que el logo no es un botón mecánico como A y B, sino una entrada capacitiva, sospecho que la función para leerlo será diferente. 
Basándome en la documentación o exploración, mi hipótesis es que el logo está asociado a un pin específico (el pin del logo) y que habrá una función como is_touched() o similar asociada a ese pin. 
Al tocar el logo, esta función debería devolver True, permitiéndome mostrar algo (quizás una cara sonriente o la letra 'L') en la pantalla.

#### Código

```py
from microbit import *

while True:

    if pin_logo.is_touched():
        display.show(Image.HAPPY)
    else:
        display.clear()

    sleep(100)
```
#### Descripción de los resultados:

Al ejecutar el código en un micro:bit V2, la pantalla LED estaba inicialmente apagada.
Cuando toqué el logo dorado con el dedo, apareció una cara sonriente (Image.HAPPY) en la pantalla LED.
Tan pronto como retiré el dedo del logo, la cara sonriente desapareció y la pantalla se apagó.
Tocar los botones A o B no tuvo ningún efecto relacionado con este código.

#### Análisis de esos resultados:

Los resultados validan la hipótesis. El logo táctil actúa como una entrada digital y su estado se puede leer.
La forma de leerlo es a través del objeto pin_logo y su método is_touched(). Esto es diferente de los botones A y B, que tienen objetos button_a y button_b dedicados.
El principio de funcionamiento es similar: pin_logo.is_touched() devuelve True cuando se detecta el contacto (un cambio en la capacitancia del pin) y False en caso contrario.
El bucle while True y la estructura if/else funcionan de la misma manera que en los experimentos anteriores para reaccionar continuamente al estado de la entrada.

#### Conclusiones:

El experimento demuestra que el logo táctil del micro:bit V2 funciona como una entrada digital adicional.
Se accede a su estado mediante el objeto pin_logo y el método is_touched().
Aunque el mecanismo físico (táctil vs. mecánico) es diferente al de los botones A y B, desde el punto de vista de la programación, se trata de manera similar: comprobar un estado booleano (True/False) dentro de un bucle para tomar decisiones.





