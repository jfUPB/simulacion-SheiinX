### Modificación
En la propuesta de modificación, me gustaría directamente ver si puedo hacer que pueda rebotar sobre uno de los ejes cuando toca el borde.

Lo que me imagino es que espero que pueda hacer el rebote normal y que solo uno de los ejes pueda rebotar y el otro eje ya si se mueva de arriba/abajo o derecha/izquierda.

El cambio en cuestión fue en checkEdges
```js
checkEdges() {
    if (this.position.x > width) {
      //this.position.x *= -1;
      this.velocity.x *= -1;
    } else if (this.position.x < 0) {
      //this.position.x *= -1;
      this.velocity.x *= -1;
    }

    if (this.position.y > height) {
      this.position.y = 0;
    } else if (this.position.y < 0) {
      this.position.y = height;
    }
  }
```
La primera modificación fue directamente multiplicar la posición de x por -1 para que cambiara el sentido, pero lo que pasó fue que se mantenía en un borde, y el tema fue que como aún seguía la velocidad a una direcció, cada vez que cambiaba el sentido, volvía a cambiarse para la dirección original, quedandose rebotando en el mismo borde. Ya de ahí me dí cuenta que directamente como la velocidad no cambiaba en ningún momento, siempre iba a una dirección, entonces solo cambié el de posición por el de velocidad y ahí sí empezó a cambiar la dirección de movimiento.
