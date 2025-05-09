## Actividad 12

### ¿Qué tanto aprendí en esta unidad?

Considero que fue una unidad bastante efectiva. Los conceptos estaban medianamente complicados y nuevos para mi pero al momento de verlos aplicados me quedaron mas claros.
Tener claros estos conceptos ayuda a isualizar como funcionan muchos proyectos de mayor escala y como hacer proyectos de manera más eficiente.
Con esta unidad aprendí bastante sobre la importancia de conocer métodos eficientes para crear algo, puesto a que en el código hay muchas formas y no todas son igual de adecuadas para todos los proyectos.


### Conceptos aprendidos

El concepto de que es una maquina de estados no me quedaba muy claro. Con esta actividad de la bomba ya entendí a que se refiere el concepto.

Ejemplo:

``` py
from microbit import *

class Semaforo:
    def __init__(self, columna, t_rojo, t_amarillo, t_verde):
        self.columna = columna
        self.tiempos = {
            "rojo": t_rojo,
            "amarillo": t_amarillo,
            "verde": t_verde
        }
        self.estado = "rojo"
        self.tiempo_estado = running_time()

    def update(self):
        tiempo_actual = running_time()
        transcurrido = (tiempo_actual - self.tiempo_estado) / 1000

        if transcurrido >= self.tiempos[self.estado]:
            self.cambiar_estado()
            self.tiempo_estado = tiempo_actual

    def cambiar_estado(self):
        if self.estado == "rojo":
            self.estado = "verde"
        elif self.estado == "verde":
            self.estado = "amarillo"
        elif self.estado == "amarillo":
            self.estado = "rojo"

    def dibujar(self):
        # Apagamos la columna
        for y in range(5):
            display.set_pixel(self.columna, y, 0)

        # Encendemos el LED según el estado (posición fija)
        if self.estado == "rojo":
            display.set_pixel(self.columna, 0, 9)
        elif self.estado == "amarillo":
            display.set_pixel(self.columna, 2, 5)
        elif self.estado == "verde":
            display.set_pixel(self.columna, 4, 2)

semaforo1 = Semaforo(0, 5, 2, 3)
semaforo2 = Semaforo(2, 3, 1, 2)
semaforo3 = Semaforo(4, 4, 3, 2)

while True:
    semaforo1.update()
    semaforo2.update()
    semaforo3.update()

    semaforo1.dibujar()
    semaforo2.dibujar()
    semaforo3.dibujar()

    sleep(100)
```

### Conceptos no aprendidos

Modelar el sistema en los mapas

Vectores de prueba

En la unidad no realicé los ejerciciso de estos conceptos. No entendí y me tocó continuar por cuestiones de tiempo.

### Define estrategias para mejorar en los conceptos que aún te cuestan trabajo. ¿Qué harás para mejorar en esos conceptos? ¿Qué recursos usarás? ¿Qué tiempo le dedicarás? ¿Cuándo comenzarás?

Actualmente hay muchas herramientas en la web para entender conceptos de programación. Puedo utilizar herramientas de IA para explicarme los conceptos aplicados a lo que ya tengo en código, para asi poder entender mejor qe solo buscando la definición del concepto.
Puedo comenzar cuando tenga algún tiempo libre que no tenga que dedicar a otras materias de la carrera, no se un tiempo exacto o una duración exacta.
