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
