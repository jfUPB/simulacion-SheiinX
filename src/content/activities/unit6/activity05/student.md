### 1. Diferencias

Cada uno de estos métodos sirve para generar un movimiento coordinado de agentes que se mueven o tienen alguna interacción dentro de su propio sistema, pero para ambos métodos hay diferencias con como se interactua con este sistema. Primero está el flowfield, todos los agentes tienen una fuerza que los hace moverse hacia un lugar, pero la dirección hacia donde se mueven está determinada por el espacio, el flowfield da una dirección en una zona específica la cual los agentes tenderán a seguir esa dirección de esa zona.

Mientras tanto el flocking son más reglas centradas en los agentes en sí que del entorno, estas reglas las tiene cada uno de los agentes, y se activarán cuando otro agente se acerca a este. A diferencia del flowfield, no depende del entorno, pero las reglas que se le asignan sobre sus propios elementos.

### 2. Comportamientos

Con el caso de los flowfields, para mi el comportamiento más fácil de estos es el de direcciones controladas a base de ángulos y funciones, los cuales permiten orden dentro de lo visual hasta cierta medida. Y de parte de flocking, es el comportamiento de ave el cual todos los elementos actuarán separados pero en orden hacía el conjunto completo.

### 3. Ventajas y desventajas

Ya mencioné varias veces, pero para el flowfield tenemos ventajas de comportamientos un poco más agresivos pero más controlados, y de parte de flocking tenemos que se pueden simular muy bien comportamientos de "horda" o "bandadas". Ya de parte de las desventajas tenemos que el flowfield puede volverse un poco catástrofico en los espacios controlados, y también de que el movimiento se vuelve muy limitado a la zona que está designada; Y de flocking, la desventaja es la de que es un sistema mucho más complejo para construir a comparación del flowfield, y de que es dependiente de varios elementos, si solo hay uno o varios pero no llegan a interactuar, se quedan esas reglas sin mucho efecto.

### 4. Agente aútonomo

Aunque "aútonomo" puede volverse un término abstracto, en este caso me hizo entender que no todo se puede tener control para generar cosas, y de que puedes generar aleatoriedad pero controlada a base de reglas que siguen estos agentes.

Las características de estos agentes es la de tener unas reglas que te limitan el movimiento, pero igualmente el agente seguirá de una manera menos controlada y menos cuadrada.

### 5. Comportamiento Emergente

Conseguí ver que, incluso teniendo reglas, hay veces en las que los límites del sistema hacen que varios elementos dejen de seguir la ruta y hagan su propio camino, por ejemplo en flowfields, si cambiabas la velocidad y los vectores para que fueran aleatorios, los agentes no lograban seguir las reglas del campo, pero intentaban seguirlas e iban derecho, incluso si el camino era un poco ortodoxo.
