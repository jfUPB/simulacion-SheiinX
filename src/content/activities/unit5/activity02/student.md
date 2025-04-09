### Ejemplo 4.2
Mi idea para este fue el de aplicar el Levy Flight, una distribución de probabilidad a esta simulación, mi objetivo era el hacer que algunas que otras particulas salieran disparadas a mayor velocidad que la mayoría, la cosa es que cunado se me ocurrió cambiar la velocidad y aplicarle, no fue lo que esperaba, pero se aplicaba esa distribución ya que estaban apareciendo particulas lejos de un punto de concentración que es el centro, y aunque se cambió como se comportaba el original ejemplo, ahí se aplicó este otro concepto, no completamente, pero se aplicó.
```js
//Set inicial speed at 0,0
constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(0,0);
    this.lifespan = 255.0;
  }
```

```js
//APply the distribution, with a new function and a if with the parameter of r
setVelocity(){
    let r = random(1);

    if(r < 0.001){
      this.velocity.set(random(-70,70), random(-70,70));
    } else{
      this.velocity.set(random(-3,3), random(-3,3));
    }
  }
```

```js
for (let i = particles.length - 1; i >= 0; i--) {
    let particle = particles[i];
    particle.setVelocity(); //Use the new function in the draw()
    particle.run();
    if (particle.isDead()) {
      //remove the particle
      particles.splice(i, 1);
    }
  }
```

#### Código y link

```js
let particles = [];

function setup() {
  createCanvas(640, 640);
}

function draw() {
  background(255);
  particles.push(new Particle(width / 2, height/4));

  // Looping through backwards to delete
  for (let i = particles.length - 1; i >= 0; i--) {
    let particle = particles[i];
    particle.setVelocity();
    particle.run();
    if (particle.isDead()) {
      //remove the particle
      particles.splice(i, 1);
    }
  }
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(0,0);
    this.lifespan = 255.0;
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);
    this.update();
    this.show();
  }
  
  setVelocity(){
    let r = random(1);

    if(r < 0.001){
      this.velocity.set(random(-70,70), random(-70,70));
    } else{
      this.velocity.set(random(-3,3), random(-3,3));
    }
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  // Method to update position
  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  // Method to display
  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  // Is the particle still useful?
  isDead() {
    return (this.lifespan < 0.0);
  }
}
```
https://editor.p5js.org/SheiinX/sketches/z4BwM7d3V

### Ejemplo 4.4
Con este, volví con los conceptos de aleatoriedad, el cual, el que elegí esta vez para este es el perlin noise, utilizando la función de noise() del lenguaje. En este caso quite la función de gravedad que tenía, entonces solo se ponían a flotar las particulas, y para la aplicación puse que directamente afectará el tamaño de las particulas creadas, primero haciendo unos cambios en las clase, primero en Particle que en su constructor recibiera una nueva variable que es es el 'd', y que se la pasará a la parte del código donde se estuviera ya dibujando las formas. En emitter hice para que se pudiera ya pasar los datos pero utilizando dentro de sí una función receiveDiameter() la cual cambiaría el valor del diametro que se le pasará, y este ya se lo pasaría a cuando se crea un nuevo objeto Particle. Por último ya está el tema en el draw, teniendo unas variable t y off las cuales servirían para cambiar el tiempo y cambiar el valor por el cual se pasaría al off y por consiguiente, a las funciones de las clases.

```js
constructor(x, y, d) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;
    this.d = d;
  }
show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, this.d);
  }
```

```js
constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
    this.diameter = 1.0;
  }
  
  receiveDiameter(diameter){
    this.diameter = diameter;
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y, this.diameter));
  }
```

```js
let off = t;
  
  for (let emitter of emitters) {
    let pNoise = noise(off);
    off += 0.1;
    
    let diameter = map(pNoise, 0, 1, 2, 60);

    emitter.receiveDiameter(diameter);
    emitter.run();
    emitter.addParticle();
  }
  
  t += 0.01;
```

#### Código y link
```js
let t = 0.0;
let emitters = [];

function setup() {
  createCanvas(640, 240);
  let text = createP("click to add particle systems");
}

function draw() {
  background(255);
  
  let off = t;
  
  for (let emitter of emitters) {
    let pNoise = noise(off);
    off += 0.1;
    
    let diameter = map(pNoise, 0, 1, 2, 60);

    emitter.receiveDiameter(diameter);
    emitter.run();
    emitter.addParticle();
  }
  
  t += 0.01;
}

function mousePressed() {
  emitters.push(new Emitter(mouseX, mouseY));
}

class Particle {
  constructor(x, y, d) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;
    this.d = d;
  }

  run() {
    //let gravity = createVector(0, 0.05);
    //this.applyForce(gravity);
    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  // Method to update position
  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  // Method to display
  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, this.d);
  }

  // Is the particle still useful?
  isDead() {
    return this.lifespan < 0.0;
  }
}

class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
    this.diameter = 1.0;
  }
  
  receiveDiameter(diameter){
    this.diameter = diameter;
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y, this.diameter));
  }

  run() {
    // Looping through backwards to delete
    for (let i = this.particles.length - 1; i >= 0; i--) {
      this.particles[i].run();
      if (this.particles[i].isDead()) {
        // Remove the particle
        this.particles.splice(i, 1);
      }
    }
  }
}

```

https://editor.p5js.org/SheiinX/sketches/dkHBmwks_
