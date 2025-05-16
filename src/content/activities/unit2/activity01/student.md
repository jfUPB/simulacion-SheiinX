### Suma de dos vectores

Igual que los conceptos básicos de matemáticas, la conexión de dos puntos en un espacio, la cual una va hacia la otra, una flecha que empieza desde un punto y termina en otro, literalmente la dirección.

Ahora la suma de dos vectores, tomando dos puntos en un espacio y sumandolos, y es sencillo, tenemos un vector tipo (a,b) donde a está parado en el plano X y b está parado en el plano Y, y otro vector (v,w) que va igual, v en X y w en Y. La suma de estos vectores es igual a la suma de sus correspondientes, X con X y Y con Y, terminando con un vector nuevo ((a+v),(b+w)).

Ahora, la razón por la que la línea position = position + velocity; no funciona es un tema del lenguaje, JavaScript como menciona el libro guía, solo puede hacer operaciones fundamentales como suma, resta, multiplicación y división, entonces para poder hacer la suma de ambos vectores se necesita una función construida a mano en el código o por ejemplo p5 tiene una función construida que permite hacer la suma que es el add().
