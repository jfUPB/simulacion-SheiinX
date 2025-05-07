### FlowField
1. Array 2D

En como funciona y es asignado este array, no tengo mucho conocimiento de como funciona llamar el "new Array(...)" (En sí llamar a la clase), pero por como veo que está escrito esta primera parte: El this.field = new Array(this.colums); sirve para crear en la variable de field la primera dimensión del array, asignandole así elnúmero de columnas que este va a presentarse

```
field = [ 0, 0, 0, 0, 0, 0, 0, 0, ... ]
[ 0 0 0 0 0 0 0 0 0 0 0 0 0 ...]
```

De aquí utiliza un ciclo for para asignarle ya la otra dimensión al array y así quedar en las dos dimensiones, pero asignandoselo a cada elemento del primer array

```
field = [ 0, 0, 0, 0, 0, 0, 0, 0, ... ] , [ 0, 0, 0, 0, 0, 0, 0, 0, ... ] , [ 0, 0, 0, 0, 0, 0, 0, 0, ... ] , [ 0, 0, 0, 0, 0, 0, 0, 0, ... ] , ...

  _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
[ 0 0 0 0 0 0 0 0 0 0 0 0 0 ...]
[ 0 0 0 0 0 0 0 0 0 0 0 0 0 ...]
[ 0 0 0 0 0 0 0 0 0 0 0 0 0 ...]
[ 0 0 0 0 0 0 0 0 0 0 0 0 0 ...]
[ . . . . . . . . . . . . . ...]
[ . . . . . . . . . . . . . ...]
[ . . . . . . . . . . . . . ...]
  - - - - - - - - - - - - - - -
```

Ya con esto ya tenemos un array que es a base de la resolución entregada al principio desde el constructor de la clase; y por último el tema del uso del noise para tener la dirección de los vectores, esto se maneja en init(), acá utilizando un map() para poder calcular los angulos de cada elemento del array this.field[i][j] con un fromAngle(el cual a base de un ángulo pasado, creará un vector).

2. Follow

Dentro de la clase de Flow, tenemos que cuando vamos a pasar la información de los vectores, estos ya en sí en el constructor ya están creados, su posición en el canvas, la cantidad y todo lo demás, así que en la clase hay una función llamada lookup la cual límita a base de la posición, los espacios a los que puede ver un objetoen temas de columnas y filas, y con ello se retorno con paso de valor la posición a la que se puede mover (En este caso solo entregaría el valor para la cuadricula al rededor de la posición entre x y y posibles, o a la que es deseada).

Ya con el vector de dirección encontrado, primero se límita la velocidad al max speed específicado, luego se resta la dirección deseada con la velocidad especificada anteriormente, y con ello con un limit(), se limitará la magnitud del vector a la que se haya específicado en el constructor y dea hí se tendrá la fuerza a la que se moverá el objeto en el campo.

3. Parámetros

En el constructor del FlowField se dará un parámetro en entero el cual luego se pasará a una variable resolution, y la cual será pasada a otras dos variables de colum y row las cuales calcularán dividiendo y pasarán el resultado al calculo del array

```js
constructor(r) {
    this.resolution = r;
    //{!2} Determine the number of columns and rows.
    this.cols = width / this.resolution;
    this.rows = height / this.resolution;
    //{!4} A flow field is a two-dimensional array of vectors. The example includes as separate function to create that array
    this.field = new Array(this.cols);
    for (let i = 0; i < this.cols; i++) {
      this.field[i] = new Array(this.rows);
    }
    this.init();
  }
```

Ya en la clase Vehicle en el constructor se pasarán dos variables las cuales serán el máximo de velocidad y fuerza, de ahí estás dos en la función follow (Y update, pero es más notable en el follow) para limitar el movimiento y así que el objeto siga el movimiento deseado

```js
constructor(x, y, ms, mf) {
    ...
    this.maxspeed = ms;
    this.maxforce = mf;
  }
```

```js
follow(flow) {
    // What is the vector at that spot in the flow field?
    let desired = flow.lookup(this.position);
    // Scale it up by maxspeed
    desired.mult(this.maxspeed);
    // Steering is desired minus velocity
    let steer = p5.Vector.sub(desired, this.velocity);
    steer.limit(this.maxforce); // Limit to maximum steering force
    this.applyForce(steer);
  }
```
4. Experimentación

Cambiando las variables de noise por otras funciones para la aleatoriedad, terminé utilizando el más básico, el random para que no haya un flujo controlado dentro del sistema

```js
let angle = random(TWO_PI);
```

Además de también utilizando los sin y cos para tener un movimiento más controlado pero que no genera diferentes flujos cada vez que se da un clic

```js
let angle = sin(xoff) * cos(yoff) * TWO_PI;
```
---
También tomé para manejar los valores de la velocidad máxima y la fuerza máxima justo en el sketch.js, cambiandole el random y manejando manualmente los valores, y vi que en la fuerza máxima no hay mucha diferencia, solo en la aceleración, pero cuando cambio a valores muy grandes, los objetos terminan  ignorando el flujo y se quedán moviendo en una dirección fija todo el rato

```js
for (let i = 0; i < 120; i++) {
    vehicles.push(
      new Vehicle(random(width), random(height), 100, 0.1)
    );
  }
```

