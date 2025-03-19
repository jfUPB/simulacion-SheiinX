### heading()
p5.Vector.heading() es una función que permite calcular cual es el ángulo de inclinación del vector con respecto al del eje positivo x, lo cual permite saber a donde apuntará el vector con respecto al origen.

### push() y pop()
push() y pop() son funciones que funcionan en conjunto, con push() al inicio y pop() al final; la función de estás dos funciones son las de tener un método de draw() especificamente a las líneas que están dentro de push() y pop(), en otras palabras, si tengo dos cuadrados en el canvas, y decido poner una función para mover general, se moverán los dos cuadrados que tenía en el canvas, pero si por ejemplo especifico al inicio un cuadrado y luego dentro de entre push() y pop() pongo el otro cuadrado, y en esas mismas lineas del cuadrado (sin escribir después de pop()) escribo la función de movimiento, solo el cuadrado dentro del push() y pop() se moverá, y el que quedó por fuera no se moverá. En resumen, lo que se escribe dentro de ese intervalo del push y pop, solo funcionará en esas líneas y no se aplicará a lo demás que esté por fuera.

### rectMode(CENTER)
Lo que hace el rectMode(CENTER) es cambiar la zona donde se dibujará lo que especifique en el código en cierta posición ya del código, en este caso pasa el sistema para dibujar justo en el centro del canvas.

### Relación
x
