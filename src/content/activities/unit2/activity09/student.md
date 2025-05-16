``` py
from microbit import *
import utime

class TrafficLight:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.state = "rojo"
        self.start_time = utime.ticks_ms()

    def update(self):
        current_time = utime.ticks_ms()
        
        if self.state == "rojo":
            display.clear()
            display.set_pixel(self.x, self.y, 9)
            if utime.ticks_diff(current_time, self.start_time) > 4000:
                self.state = "rojo_amarillo"
                self.start_time = current_time
        
        elif self.state == "rojo_amarillo":
            display.clear()
            display.set_pixel(self.x, self.y, 9)
            display.set_pixel(self.x, self.y + 1, 9)
            if utime.ticks_diff(current_time, self.start_time) > 2000:
                self.state = "verde"
                self.start_time = current_time
        
        elif self.state == "verde":
            display.clear()
            display.set_pixel(self.x, self.y + 2, 9)
            if utime.ticks_diff(current_time, self.start_time) > 4000:
                self.state = "amarillo"
                self.start_time = current_time
        
        elif self.state == "amarillo":
            display.clear()
            display.set_pixel(self.x, self.y + 1, 9)
            if utime.ticks_diff(current_time, self.start_time) > 2000:
                self.state = "rojo"
                self.start_time = current_time

traffic_light = TrafficLight(2, 0)

while True:
    traffic_light.update()
    utime.sleep(0.1)
```

### 1. Estados del Semáforo.
Los estados representan las diferentes luces del semáforo:

- rojo
- rojo_amarillo
- verde
- amarillo

### 2. Eventos evaluados en cada estado

- rojo: Tiempo > 4000 ms
- rojo_amarillo: Tiempo > 2000 ms
- verde: Tiempo > 4000 ms
- amarillo: Tiempo > 2000 ms

### 3. Acciones ejecutadas

- rojo: Borra la pantalla y enciende la luz roja en (x, y).
- rojo_amarillo: Borra la pantalla, enciende la luz roja en (x, y) y la luz amarilla en (x, y + 1).
- verde: Borra la pantalla y enciende la luz verde en (x, y + 2).
- amarillo: Borra la pantalla y enciende la luz amarilla en (x, y + 1).





