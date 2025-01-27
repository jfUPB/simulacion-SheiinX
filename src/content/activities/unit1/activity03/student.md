### Mini Experimento de código Random Walk
Gracias a la documentación, voy a dejar un poco este espacio también para resumir más o menos el proceso del código que el autor hizo y entenderlo.

Ahora voy a ir poco a poco.

``` js
class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}
```

La primera parte es una clase, la clase Walker, igual que en otros lenguajes de programación, acá la clase servirá para hacer todos los procesos relacionados a una instancia que se generará cuando la llame dentro del código. En este caso, tendremos el constructor que tendra las variables que serán parte del objeto de la clase, y tendremos 2 funciones: show() y step().

De parte de la función show(), tendremos que va a hacer todo el procedimiento de dibujar el objeto dentro de un canvas que estará inicializado dentro de:
``` js
function setup() {
//CreateCanvas() inicializa la pantalla y define una dimensión
  createCanvas(640, 240);
//Inicializa el objeto
  walker = new Walker();
//background define el color del fondo del canvas
  background(255);
}
```
Y step() será la parte del código centrado en hacer el movimiento del objeto dentro del canvas, solo generando movimiento de arriba a abajo e izquierda para la derecha.

También para notar, dentro hay un calculo que utiliza una función floor() y dentro está el random(), de parte del random() tenemos que nos dará un número aleatorio dentro del rango especificado, y el floor(), según la documentación, es una función que permite redondear el dato obtenido al número entero más cercano al valor.

```js
function draw() {
  walker.step();
  walker.show();
}
```
Y por último está la función draw() que directamente llama las funciones del walker para dibujarlo en el canvas
``` js
let walker;
```
Y el let, que es practicamente una manera de llamar a la función para el resto del código... O así es como lo interpreto.

### Experimento
Ahora sí, para ir directamente al assigment, lo más sencillo que quiero hacer es que se mueva en una dirección diagonal, y creería que la forma más fácil es solo poniendo en la función step una nueva condición más que permita al menos tener una sola nueva dirección

```js
step() {
    const choice = floor(random(8));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else if (choice == 3){
      this.y--;
    } else if (choice == 4){
      this.x++;
      this.y++;
    } else if (choice == 5){
      this.x--;
      this.y++;
    } else if (choice == 6){
      this.x--;
      this.y--;
    } else if {
      this.x++;
      this.y--;
    }
  }
```

No era lo que esperaba ya que no conseguí ver nada, así que decidí cambiar un poco el código para que se vea más, y terminé eliminando las condiciones para moverlo arriba y que solo se moviera en diagonal

```js
step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
      this.y++;
    } else if (choice == 1){
      this.x--;
      this.y++;
    } else if (choice == 2) {
      this.x--;
      this.y--;
    } else {
      this.x++;
      this.y--;
    }
  }
```

Con este termino coonsiguiendo ver algo interesante, con el poco tiempo que lo dejé, practicamente no consigue haber algún punto en el que haya dos puntos paralelos, todos son diagonales entre sí, y no sé como, pero tal vez sea por como funciona los pixeles, y se haga un efecto similar al alfil en ajedrez, se puede mover diagonalmente, pero nunca toca los puntos del color opuesto al que está parado. Y es interesante, ahí pude confirmar los pixeles y como más o menos funciona una pantalla con relación a tales para dibujar cosas, necesitando de los 8 movimientos para dibujar.
