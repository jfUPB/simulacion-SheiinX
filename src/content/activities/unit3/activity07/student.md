### Paso por referencia
Cuando pasamos por referencia, la variable original en el espacio de memoria también se ve afectado, lo cual traducido es que las fuerzas que aplicamos y luego hacemos la función force.div(10), cambian por completo, cuando la volvamos a llamar ya no será el mismo vector, sino que será un valor cada vez más pequeño conforme lo llamemos.

Entonces una manera de poder evitar que se modifique la variable original, o el vector original en este caso puede ser:
```js
applyForce(force) {
    let f = force.copy()
    f.div(10);
    this.acceleration.add(f);
}
```
La cual lo que hace es que directamente pasa en una variable la copia de la fuerza, practicamente le pasa a un nuevo vector la variable original y esta nunca afecta a la original, de manera que pasamos por valor.
