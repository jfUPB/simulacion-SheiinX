### mag()
mag() es una función que devuelve la magnitud del vector especificado.

También está magSq() la cual es la función que devuelve la magnitud del vector pero al cuadrado.

Cual es más eficiente, dependerá de lo que uno necesite, el magSq() al menos te ahorra el calcula extra de elevar lo que a uno le dé en magnitud al cuadrado.

### normalize()
normalize() sirve para escalar la magnitud de un vector para que sea igual a 1, esto sirviendo para evitar que un vector tenga una magnitud muy grande.

### dot()
dot() es una función que hace el producto punto entre dos vectores, es como la "sombra" que se refleja sobre un vector.

### dot() instancia y estática
En la versión de instancia, dot() se llama directamente como v1.dot(v2).

En la versión estática, dot() se llama sin tener instanciado un vector p5.vector.dot(v1,v2). Pero este crea otro vector, y deja el original quieto.

Pero hacen practicamente lo mismo.

### dist()
p5.vector.dist() sirve para calcular la distancia entre dos vectores.

### limit()
Pone un límite a cuanto puede ser la magnitud del vector que utiliza la función.
