## Análisis del uso de máquina de estados en la bomba con p5.js y micro:bit

### ¿Por qué esta técnica es poderosa para la escalabilidad de tu aplicación en términos de concurrencia y manejo de eventos?

La técnica de máquina de estados permite organizar la lógica de una aplicación dividiéndola en estados bien definidos y transiciones claras entre ellos. Esta estructura tiene múltiples beneficios:

Escalabilidad: Es más fácil agregar nuevas funcionalidades (como nuevos eventos o comportamientos) porque solo necesitas añadir nuevos estados o transiciones sin afectar el resto del código.

Manejo eficiente de eventos: Separar los eventos del comportamiento según el estado permite manejar eventos concurrentes de forma controlada. Por ejemplo, un evento puede tener efecto en un estado, pero ser ignorado en otro.

Código más limpio y entendible: La máquina de estados actúa como una guía sobre qué puede pasar en cada momento de la aplicación, lo cual facilita el mantenimiento y colaboración con otros desarrolladores.

Modularidad: Puedes implementar cada estado como un módulo o función aparte, haciendo el sistema más modular y testeable.

### Ventajas y desventajas del tipo de pruebas realizadas
Ventajas:

Se realizaron pruebas manuales inmediatas, lo que permite comprobar rápidamente el comportamiento esperado al presionar botones o enviar eventos desde el micro:bit.

Se pueden detectar problemas visuales o de interacción fácilmente (por ejemplo, si la bomba explota antes de tiempo).

Las pruebas fueron contextuales: se probó el sistema completo, no solo partes individuales.

Desventajas:

No hay pruebas automáticas, por lo tanto:

Las pruebas pueden ser inconsistentes o incompletas si se omiten casos.

Requieren tiempo manual cada vez que se hace una modificación.

Es más difícil detectar errores que solo se presentan en condiciones específicas o poco comunes.

### ¿Por qué son importantes las pruebas de regresión?
Las pruebas de regresión consisten en verificar que el sistema siga funcionando correctamente después de realizar cambios (como agregar funciones o corregir errores).

Importancia:

Garantizan que los cambios no rompan funcionalidades anteriores.

Ayudan a mantener la estabilidad del sistema a lo largo del tiempo.

Son esenciales en sistemas complejos o colaborativos, donde muchos cambios pueden tener efectos no deseados.

### ¿Qué pasa si modificas tu aplicación y no haces pruebas de regresión?
Puedes romper funcionalidades sin darte cuenta, generando errores difíciles de rastrear.

El comportamiento del sistema puede volverse inconsistente o impredecible.

Puede causar una mala experiencia de usuario o incluso fallos graves en producción.

A medida que el proyecto crece, se vuelve casi imposible saber si todo sigue funcionando sin las pruebas.

### Conclusión
El uso de máquinas de estados en este proyecto permitió un diseño más ordenado y escalable. Las pruebas manuales ayudaron a validar el funcionamiento, pero deben complementarse con pruebas de regresión automáticas en el futuro para asegurar que el sistema siga siendo confiable con cada cambio. La única forma de poder escalar un código sin romper otras funciones es por medio de pruebas de regresión.  Es muy fácil romper otra funcionalidad del coódigo (o el código entero) al momento de añadir una nueva función o modificación, por eso se deben repetir todas las pruebas siempre que se cambie cualquier cosa.
