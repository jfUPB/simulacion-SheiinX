Paso por valor: Tenemos dos espacios de memorias y dos diferentes variables están apuntando por separado a los dos espacios de memoria.

Paso por referencia: Dos espacios de memoria y dos diferentes variables, pero que están apuntando al mismo espacio de memoria.

Lo cual en resultado hace que en el de referencia se cambia el valor original, mientras que por el valor el original se mantiene igual.

En este caso en el código, la primera línea es un paso por valor, lo cual hace que se asigne un nuevo espacio de memoria para la variable del friction, mientras que la segunda línea es por referencia, lo cual puede terminar afectando a la variable de la velocidad original si se tiene de esa manera.
