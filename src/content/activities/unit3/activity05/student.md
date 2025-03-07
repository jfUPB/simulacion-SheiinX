### Problema del pnateamiento
Según ese planteamiento y según el mismo texto base, hacer ese tipo de código, o más específicamente la función de esa manera, hace que siempre que se vaya a aplicar una nueva fuerza, la anterior va a ser sobreescrita, ya que lo que se está haciendo ahí es asignar la fuerza a la variable de la aceleración, haciendo que nunca se aumente dependiendo de qué fuerzas se aplican sobre el objeto.

Entonces la solución a esto de la suma de fuerzas sobre la aceleración es hacer la suma y no la asignación de esas variables, ya que en la difinición de las leyes, el movimiento del objeto será igual a la suma de todas las fuerzas aplicadas sobre este.
```js
applyForce(force) {
  this.acceleration.add(force);
  //Esto en vez de hacer this.acceleration = force
}
```
De esta manera ya sí varias fuerzas se suman entre sí y nunca se sobreescriben.
