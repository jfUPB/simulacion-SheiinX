#### Motion Aceleración
Dentro del mismo código que se aplicó la aceleración (Con uso de POO)

```js
class Mover {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = createVector(random(-5, 5), random(-5, 5));

    this.acceleration = createVector(0.001, 0.1);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
  }

  show() {
    .
    .
    .  
  }

  checkEdges() {
    .
    .
    .
  }
}
```

Casi todo lo que fue aplicado en la aceleración del objeto fue directamente crear ese vector con un valor bajo y sumarselo al vector de la velocidad, de manera que se hacía el efecto de que se movía cada vez más rápido, ya que es más que todo un proceso de movimiento exponencial al sumar dos variables que se van aumentando con el tiempo.

Otro ejemplo fue en el movimiento con teclas, que dependiendo en cual iba a ser la dirección, se cambiaba el vector de la aceleración para que pudiera sumarselo a la velocidad en el mivimiento que uno quería hacer
```js
if(keyIsDown(68)) //Movimiento para la derecha
{
    this.acceleration = createVector(0.1, 0);
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
}
```
#### Leyes
Aquí, ¿En qué relación hay el motion y las leyes de newton?, porque según la física, el resultado de una fuerza ejercida sobre un objeto será el movimiento de este, lo cual hace que uno con diferentes tipos de fuerza y con diferentes direcciones se genere un movimiento dentro de un objeto. Además la fuerza total como se describe en el texto, es igual a masa por aceleración, donde ahí ya se aplica parte del motion sobre el objeto y se puede ver el resultado de esa aplicación de la fuerza sobre ese objeto.
