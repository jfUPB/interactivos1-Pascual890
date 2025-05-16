### Codigo de microbit
```py
from microbit import *
import music


tune1 = ['C#3:2', 'D#3:2', 'E3:2', 'F#3:8']  
tune2 = ['C#5:3', 'D#5:2', 'E5:5', 'D#5:5', 'B4:5', 'C#5:5']

while True:
    if button_a.is_pressed():
        music.play(tune1)
    
    if button_b.is_pressed():
        music.play(tune2)
    
    sleep(100)
```
### Documentación del código
#### Librerías utilizadas:
microbit: Permite la interacción con el hardware del micro:bit.
music: Facilita la reproducción de sonidos y melodías.

#### Explicación del código
tune1: Contiene una secuencia de notas (C#3, D#3, E3, F#3) con duraciones específicas.
tune2: Contiene otra secuencia diferente de notas (C#5, D#5, E5, etc.).
Cada nota tiene un formato Nota:Duración, donde la duración determina el tiempo que se mantiene la nota.
Bucle principal (while True)

El programa entra en un ciclo infinito donde constantemente verifica el estado de los botones A y B.
Si el botón A es presionado, se reproduce la tune1 con music.play(tune1).
Si el botón B es presionado, se reproduce la tune2 con music.play(tune2).
Se agrega un pequeño retraso (sleep(100)) para evitar que la detección del botón sea demasiado rápida y genere repeticiones involuntarias.
