Cogiendo el levy flight, simplemente fue borrar los elementos que tomaban this.x y this.y y cambiarlos por el createVectory utilizar el .add() para moverlo

```js
//Levy Flight con vectores
let walker;
let position;
let prevPosition;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
  frameRate(240)
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    //this.x = width / 2;
    //this.y = height / 2;
    position = createVector(width/2, height/2);
    
    //this.prevX = this.x;
    //this.prevY = this.y;
    prevPosition = createVector(position.x,position.y);
  }

  show() {
    stroke(0);
    line(position.x, position.y, prevPosition.x, prevPosition.y);
  }

step() {
    let r = random(1);

    if(r < 0.01){
      //this.prevX = this.x;
      //this.prevY = this.y;
      prevPosition = position.copy();
      //Vector.copy() que me retorna la copia del vector especificado,
      //Así puedo guardar la posición anterior
      
      //this.x += random(-30, 30);
      //this.y += random(-30, 30);
      position.add(random(-30,30),random(-30,30));
    } else{
      //this.prevX = this.x;
      //this.prevY = this.y;
      prevPosition = position.copy();
      
      //this.x += random(-1, 1);
      //this.y += random(-1, 1);
      position.add(random(-1,1),random(-1,1));
    }
  }
}
```
