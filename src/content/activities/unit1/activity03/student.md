### Mini Experimento de código Random Walk
Gracias a la documentación, voy a dejar un poco este espacio también para resumir más o menos el proceso del código que el autor hizo y entenderlo.
``` js
let walker;



function draw() {
  walker.step();
  walker.show();
}



```

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
