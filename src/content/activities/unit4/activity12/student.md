### Tipo
Igual que como mencioné antes, dejé el más básico que fue el movimiento sinusoide cuando están orbitando alrededor del attractor.

```js
this.theta += this.angularSpeed * direction;

this.position.set(
      attractor.position.x + this.orbitRadius * cos(this.theta),
      attractor.position.y + this.orbitRadius * sin(this.theta)
    );
```
Donde la posición del objeto será cambiada constantemente con el angularSpeed cambiando el theta, ya en la posición con el set, este se moverá dentro de lo estipulado gracias al orbitRadius, y con el theta constantemente cambiando, utilizando sin y cos, estariamos moviendo el objeto en el círculo unitario constantemente generando el movimiento circular en la simulación, pero ahí para evitar que esté entre -1 y 1 el circulo de movimiento, se le multiplica por el valor del orbitRadius y ya de ahí se va cambiando en x y en y para que generé movimiento.

### Interacción
Puro teclado
* A/D: Cambia la dirección que se mueven los objetos orbitando en 1 o -1
* W/S: Acerca o aleja los objetos del attractor
* Q/E: Este hace también el cambio de dirección, la cosa es que este realmente cambia la velocidad, haciendo que el cambio de dirección sea más suave y se pueda variar también la velocidad de movimiento

### Desafíos
Más que todo fue la aplicación del movimiento, ya estaba el código en sí, solo era modificarlo para que se pudiera moverse, entonces fue el tema del cambio de dirección, fácil por poner algo multiplicandolo a la velocidad angular pero que fuera negativo y cambiaba la dirección; luego estaba el tema de acercarlos mientras se mantuviera el movimiento, la manera que se logró fue gracias a gpt proponiendo la función y que esta al llamrla sumara o restara al orbitRadius para que funcionará el cambio; Y por último el cambio de velocidad que fue el más sencillo solo leyendo el código y que viendo que la variable era del mismo contructor de la clase, era fácil llamarla y cambiarla desde afuera.

Y antes de que se me olvide, de parte del cambio de dirección, al principio se cambiaba la dirección dentro de la clase, pero por alguna razón esto me hacía desaparecer los objetos en la pantalla y luego los cambiaba la posición que al final tuvieron, a la final reseteando la simulación, entonces se sacó por donde se pudiera cambiar la dirección desde afuera y que se mantuvieran los objetos moviendo independiente si uno presiona o no la tecla.

### Aprender
Aunque las apliqué, aún tengo que ver como funcionan bien el uso de las osilaciones dentro de programación ya que aún se me hace muy abstracto el movimiento que se genera en el sentido de operaciones, así que aún tengo que mejorar eso.
