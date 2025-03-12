### Fuerza Gravitacional
```js
function setup() {
  createCanvas(640, 540);
  user = new CircleObject();
}

function draw() {
  background(255, 50);
  
  let gravity = createVector(0,0.2);
  
  user.update();
  user.applyForce(gravity);
  user.checkedFloor();
  user.checkedEdges();
  user.show();
}

class CircleObject{
  constructor() {
    this.radius = 50;
    this.mass = 10;
    this.position = createVector(width/2, 50);
    this.velocity = createVector(0, 0);
    
    this.acceleration = createVector(0, 0);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, this.radius);
  }
  
  applyForce(force){
    let f = p5.Vector.mult(force, this.mass);
    this.acceleration.add(f);
  }
  
  checkedFloor(){
    if(this.position.y + this.radius > height){
      this.position.y = height - this.radius;
      this.velocity.y *= -0.9;
    }
    
    if (abs(this.velocity.y) < 0.9) {
      this.velocity.y = 0;
    }
  }
  
  checkedEdges(){
    if (this.position.x + this.radius > width) {
      this.velocity.x *= -1;
    } else if (this.position.x - this.radius < 0) {
      this.velocity.x *= -1;
    }
  }
}
```

Aquí, la forma en que modelé la fuerza gravitacional fue de la manera que mostraba el libro, con un vector de gravity con dirección hacia abajo, una función de applyForce con la operación de this.acceleration.add(force), y de que también cada frame se reiniciara las fuerzas paa que cada frame calculara tales de manera independiente a su anterior frame.

Aquí hubo una cosa extra y es que al ponerle la formula, no hice la separación de f=m*a a a=f/m, sino que me quedé con la del f=m*a, esto debido a que con la primera mencionada no se me movía o en el aire no tenía peso, así que la segunda ya aplicaba la fuerza de manera normal.

https://editor.p5js.org/SheiinX/sketches/ASNL09CI-
