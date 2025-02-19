### Motion 101
Como presentado en el texto, es practicamente aplicar las funciones de movimiento a un objeto y mostrarlo en pantalla. Con la utilización de vectores y una clase que encapsula estas funciones y se puede reutilizar en otros lugares de maneras indefinidas.
* Agregar velocidad a la posición (Variable)
* Dibujar el objeto en la posición nueva
Esto mientras va corriendo el programa y hace la sensación de que se está movimiento.

Todo esto utilizando los vectores proporcionados por el lenguaje. En p5 por ejemplo se tiene estas lineas de código:

```js
position.add(velocity); //Agregar velocidad a la posición
circle(position.x, position.y, 48); //Dibujar el objeto, este como ejemplo, pero cualquier objeto con posición cuenta
```
