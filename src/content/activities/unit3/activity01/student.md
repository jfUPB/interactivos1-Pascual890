Programa:
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
Por medio de este nuevo programa se pueden ver 3 diferentes semáforos funcionando a la vez con diferentes tiempos. Como todos los leds del dispositivo son rojos, se usa la posición como diferenciación de cada color. Cada semáforo funciona en una columna de leds diferente. 

Usar una clase para representar cada semáforo permite organizar mejor el código, hacerlo más limpio y reutilizable. Cada instancia maneja su propio estado y tiempos sin interferir con las demás, lo que facilita la creación de múltiples semáforos concurrentes. Además, al usar una máquina de estados finita (FSM), se controla de forma precisa y ordenada el cambio entre luces (rojo, amarillo, verde), lo que simplifica el diseño y lo hace ideal para sistemas como el micro bit, donde se necesita eficiencia y claridad en la lógica.


