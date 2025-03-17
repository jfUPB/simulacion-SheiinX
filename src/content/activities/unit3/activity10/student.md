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

### Fricción
```js
function setup() {
  createCanvas(600, 200);
  user = new CircleObject();
}

function draw() {
  background(255, 50);
  
  let gravity = createVector(0.2,0.1);
  
  user.update();
  user.applyForce(gravity);
  user.checkedFloor();
  user.checkedEdges();
  
  if(user.contactEdge()){
    let c = 0.1;
    let friction = user.velocity.copy();
    friction.mult(-1);
    friction.setMag(c);
    user.applyForce(friction);
  }
  
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
  
  contactEdge() {
    return (this.position.y > height - this.radius - 1);
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
      this.position.x = width - this.radius;
      this.velocity.x *= -1;
    } else if (this.position.x - this.radius < 0) {
      this.position.x = 0 + this.radius;
      this.velocity.x *= -1;
    }
  }
}
```

Con la fricción igual que en el libro, tenemos una nueva función contactEdge la cual devuelve un valor bool diciendo si el objeto ya está en el piso, sea verdadero, cogiendo referencia del height y restandolo para que simule el suelo. De ahí en el draw hago una confirmación de lo que me acaban de devolver y tomo una variable por valor de la velocidad y la paso a una nueva variable fricción, y cambio la dirección de la variable fricción, de ahí le paso la constante de fricción pi y sumo las fuerzas restantes, de manera que esa línea hace la simulación de la fricción y el objeto baje la velocidad hasta que se queda quieto en el borde. (P.D: Si se quita por un momento el if del draw, el objeto quedará rebotando en las esquinas en el piso de manera indefinida).

https://editor.p5js.org/SheiinX/sketches/DCfWkwNtm

### Resistencia del aire y fluidos
```js
let liquid;
let user;

function setup() {
  createCanvas(600, 540);
  liquid = new Liquid(0, height / 2, width, height / 2, 0.1);
  user = new CircleObject();
}

function draw() {
  background(255, 50);
  
  liquid.show();
  
  let gravity = createVector(0.5,1.2);
  
  user.applyForce(gravity);
  
  if(user.contactEdge()){
    let c = 0.1;
    let friction = user.velocity.copy();
    friction.mult(-1);
    friction.setMag(c);
    user.applyForce(friction);
  }
  
  if (liquid.contains(user)) {
    let dragForce = liquid.calculateDrag(user);
    user.applyForce(dragForce);
  } 
  
  user.update();
  user.show();
  user.bounceEdges();
}

class CircleObject{
  constructor() {
    this.radius = 50;
    this.mass = 10;
    this.position = createVector(this.radius, 50);
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
    fill(127,127);
    circle(this.position.x, this.position.y, this.radius);
  }
  
  applyForce(force){
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }
  
  contactEdge() {
    return (this.position.y > height - this.radius - 1);
  }
  
  bounceEdges() {
    let bounce = -0.9;
    if (this.position.x > width - this.radius) {
      this.position.x = width - this.radius;
      this.velocity.x *= bounce;
    } else if (this.position.x < this.radius) {
      this.position.x = this.radius;
      this.velocity.x *= bounce;
    }
    if (this.position.y > height - this.radius) {
      this.position.y = height - this.radius;
      this.velocity.y *= bounce;
    }
  }
}

class Liquid {
  constructor(x, y, w, h, c) {
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    
    this.c = c;
  }

  show() {
    noStroke();
    fill(200);
    rect(this.x, this.y, this.w, this.h);
  }
  
  contains(user) {
    let pos = user.position;
    return (pos.x > this.x && pos.x < this.x + this.w && 
          pos.y > this.y && pos.y < this.y + this.h);
  }
  
  calculateDrag(user) {
    let speed = user.velocity.mag();
    let dragMagnitude = this.c * speed * speed;
    let dragForce = user.velocity.copy();
    dragForce.mult(-1);
    dragForce.setMag(dragMagnitude);
    return dragForce;
  }
}
```

Bueno, sigo sin saber por qué está tan robusto el movimiento pero con este hice unos cuantos cambios, lo primero volví a utilizar el a=f/m de manera que esta vez sí se mueve, también cambié los checks que tenía sobre el objeto para evitar tenerlo más como el ejemplo del libro, aunque ahora no tengo idea por qué el movimiento quedó tan robusto, pero igualmente ahí ya con este código al implementar la resistencia del agua no sale volando el objeto.

Ahora sí con la explicación, un nuevo objeto que es el líquido, que contiene dos métodos los cuales son contain (Que recibe el objeto y detecta si está dentro de los límites retornados o no) y calculateDrag que permite calcular la función de la resistencia de un líquido. Ya en el draw se hace la suma de las fuerzas y ya hay una resistencia del líquido.

https://editor.p5js.org/SheiinX/sketches/3IFt6f6U2

### Ahora sí Atracción Gravitacional
```js
let user = [];
let attractor;

let G;

function setup() {
  createCanvas(600, 540);
  
  for (let i = 0; i < 10; i++){
    user[i] = new CircleObject();
  }
  
  attractor = new Attractor();
}

function draw() {
  background(255, 50);
  
  attractor.show();
  
  for (let i = 0; i < user.length; i++){
    let force = attractor.attract(user[i]);
    
    user[i].applyForce(force);
    user[i].update();
    user[i].show();
  }
  //user.bounceEdges();
}

class CircleObject{
  constructor() {
    this.radius = 50;
    this.mass = 10;
    this.position = createVector(random(width), random(height));
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
    fill(127,127);
    circle(this.position.x, this.position.y, this.radius);
  }
  
  applyForce(force){
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }
  
  contactEdge() {
    return (this.position.y > height - this.radius - 1);
  }
  
  bounceEdges() {
    let bounce = -0.9;
    if (this.position.x > width - this.radius) {
      this.position.x = width - this.radius;
      this.velocity.x *= bounce;
    } else if (this.position.x < this.radius) {
      this.position.x = this.radius;
      this.velocity.x *= bounce;
    }
    if (this.position.y > height - this.radius) {
      this.position.y = height - this.radius;
      this.velocity.y *= bounce;
    }
  }
}

class Attractor {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.mass = 20;
  }

  attract(user) {
    let force = p5.Vector.sub(this.position, user.position);
    let distance = force.mag();
    distance = constrain(distance, 5, 25);

    let strength = (G * this.mass * user.mass) / (distance * distance);
    force.setMag(strength);
    return force;
  }

  show() {
    stroke(0);
    fill(175, 200);
    circle(this.position.x, this.position.y, this.mass * 2);
  }
}
```

Aplicando los temas presentados en el libro, se tiene una clase Attractor(), la cual contiene las funciones para poder calcular la atracción gravitatoria en un punto recibiendo de la clase que se pase al llamar la función, de esta manera basandose en la función Fg=(Gm1*m2/r^2)*r. Ya de ahí genéro un arreglo de objetos user y que directamente estos los voy a pasar para que empiecen a orbitar alrededor del attractor en el programa.

https://editor.p5js.org/SheiinX/sketches/ZUOSZGqtd
