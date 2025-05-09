### Respuestas
1. Gestión de memoria

En la gestión de memoria, como las particulas son elementos que se mantienen generando constantemente, eso supone un uso muy elevado de memoria, hasta el punto que puede gastarse toda la RAM de un computador si no se maneja con precaución. Acá se hace una gestión de estos elementos a base de arrays, todos los elementos estarán asignados a una arreglo o lista que dirá si el objeto existe o no, ya de ahí se utilizará el tiempo (esta vez solo utilizando el reloj interno del lenguaje si se utiliza), haciendo uso de eso se puede tener una condición de que cuando el tiempo asignado llegue a 0, el objeto será eliminado tanto del array como de la memoria en general.

2. Motion 101

En el marco de Motion 101 aplicado, acá igual que en las otras unidades que se utiliza este marco y el uso de fuerzas, cada particula viene de una clase, y cada una va a tener sus propias variables, en estas va a utilizar internamente el uso de posición y velocidad (Y también aceleración), lo cual ya entra en el amrco al utilizar ese movimiento simulado a base de la variables y manejando los vectores dentro de ese sistema.

3. Aplicación de fuerzas

Igual que en el capitulo de fuerzas, las particulas responden a una fuerzza que uno le pasa, pero la forma en que reaccionan varias es a base de poder sumarlas y resetearlas cada vez que pase un frame. Pero más que todo, en la aplicación de los sistemas de particulas, cada particula, ya que es un elemento de un array o una lista, cada particula viene de una clase, y de esa clase se tiene una función que aplicará las fuerzas sumandolas para el objeto, de manera que cada particula reacciona independientemente a las fuerzas aplicadas sobre.

4. Herencia

Aunque están los temas de polimorfismo también, para mi y mi entendimiento solo se ha aplicado el uso de la herencia, la cual permite que de una clase padre, las clases hijas van a tener las mismas variables y funciones, pero no se hace a la inversa, siendo que las clases hijas tienen más cosas y comportamientos únicos de sí. Acá como dije, en esta unidad y los ejercicios se terminó haciendo herencia en la gran mayoría de ocasiones, las cuales, por ejemplo en el del conffeti, cada particula que se generará tendría una misma funcionalidad, aparecer y caer (Y en mi cambio, que salieran disparadas a diferentes velocidades), pero había otra clase hija que tenía una función extra, que aparecieran cuadrados en vez de circulos, y estos girarían sobre su eje.
