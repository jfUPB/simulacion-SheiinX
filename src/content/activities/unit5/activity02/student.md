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

### Ejemplo 4.5
Con este ya pasamos a la unidad de vectores, esta vez con el fin de cambiar los comportamientos del sistema, para esta parte se utilizará la función de lerp() proporcionada por p5.js, acá admito que no recuerdo mucho como es el funcionamiento de lerp, así que leyendo de nuevo, es la interpolación entre dos vectores, entonces la idea será hacer que estos en objetivos aleatorios, dispare las particulas y lasponga en diferentes puntos dependiendo de esa interpolación. Adicionalmente de que se dé colores diferentes para las particulas.

Los cambios serían relativamente sencillos, donde se irían cambiando las clases Particle y Confetti, donde en ambos se aplicaría el lerp para las posiciones (Como Confetti ya es parte de un sistema de inheritance con padre el Particle, la posición y el lerp se manejaría más desde el Particle), y lerpColor para los colores de las particulas que se generen.

```js
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.target = createVector(random(width), random(height));
    this.lerpAmt = 0;

    this.startColor = color(255, 150, 0);
    this.endColor = color(0, 150, 255);

    this.lifespan = 255.0;
  }

  run() {
    this.update();
    this.show();
  }

  update() {
    this.position = p5.Vector.lerp(this.position, this.target, 0.05); //Interpolacíon
    this.lerpAmt += 0.01;
    this.lerpAmt = constrain(this.lerpAmt, 0, 1);
    this.lifespan -= 2;
  }

  show() {
    let col = lerpColor(this.startColor, this.endColor, this.lerpAmt); //Cambio del color
    col.setAlpha(this.lifespan);
    stroke(col);
    strokeWeight(2);
    fill(col);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}
```
```js
class Confetti extends Particle {
  show() {
    let angle = map(this.position.x, 0, width, 0, TWO_PI * 2);
    let col = lerpColor(this.startColor, this.endColor, this.lerpAmt); //Cambio del color
    col.setAlpha(this.lifespan);

    rectMode(CENTER);
    fill(col);
    stroke(col);
    strokeWeight(2);
    push();
    translate(this.position.x, this.position.y);
    rotate(angle);
    square(0, 0, 12);
    pop();
  }
}
```

#### Código y link

```js
let emitter;

function setup() {
  createCanvas(640, 240);
  emitter = new Emitter(width / 2, 20);
}

function draw() {
  background(255);
  emitter.addParticle();
  emitter.run();
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.target = createVector(random(width), random(height)); // Destino aleatorio
    this.lerpAmt = 0;

    this.startColor = color(255, 150, 0);
    this.endColor = color(0, 150, 255);

    this.lifespan = 255.0;
  }

  run() {
    this.update();
    this.show();
  }

  update() {
    this.position = p5.Vector.lerp(this.position, this.target, 0.05);
    this.lerpAmt += 0.01;
    this.lerpAmt = constrain(this.lerpAmt, 0, 1);
    this.lifespan -= 2;
  }

  show() {
    let col = lerpColor(this.startColor, this.endColor, this.lerpAmt);
    col.setAlpha(this.lifespan);
    stroke(col);
    strokeWeight(2);
    fill(col);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

class LerpParticle extends Particle {
  constructor(x, y) {
    super(x, y);
    this.startColor = color(255, 0, 0);
    this.endColor = color(0, 0, 255);
    this.target = createVector(random(width), random(height));
    this.lerpAmt = 0;
  }

  update() {
    this.position = p5.Vector.lerp(this.position, this.target, 0.05);
    
    this.lerpAmt += 0.01;
    this.lerpAmt = constrain(this.lerpAmt, 0, 1);
    
    this.lifespan -= 2;
  }

  show() {
    let col = lerpColor(this.startColor, this.endColor, this.lerpAmt);
    col.setAlpha(this.lifespan);

    fill(col);
    stroke(col);
    strokeWeight(2);
    ellipse(this.position.x, this.position.y, 10, 10);
  }
}

class Confetti extends Particle {
  show() {
    let angle = map(this.position.x, 0, width, 0, TWO_PI * 2);
    let col = lerpColor(this.startColor, this.endColor, this.lerpAmt);
    col.setAlpha(this.lifespan);

    rectMode(CENTER);
    fill(col);
    stroke(col);
    strokeWeight(2);
    push();
    translate(this.position.x, this.position.y);
    rotate(angle);
    square(0, 0, 12);
    pop();
  }
}

class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    let r = random(1);
    if (r < 0.5) {
      this.particles.push(new Particle(this.origin.x, this.origin.y));
    } else if (r < 0.66) {
      this.particles.push(new Confetti(this.origin.x, this.origin.y));
    } else {
      this.particles.push(new LerpParticle(this.origin.x, this.origin.y));
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.run();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}
```

https://editor.p5js.org/SheiinX/sketches/0M083OpVI

### Ejemplo 4.6
Particulas aplicandole fuerzas, ya en sí se estaba aplicando la gravedad sobre las particulas, pero esta vez aplicandole otro tipo de fuerza natural se le aplicará una fuerza del resorte, y para ello, aunque un poco ortodoxo en la forma y entenderlo, se aplicará otra función dentro del Emitter la cual se pondrá a aplicar a cada particula tal fuerza cuando se aplique la gravedad.

```js
class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
    this.restLength = 100;
    this.k = 0.05;
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  applyForce(force) {
    for (let particle of this.particles) {
      particle.applyForce(force);
      this.applySpringForce(particle);
    }
  }

  applySpringForce(particle) {
    let dir = p5.Vector.sub(particle.position, this.origin);
    let currentLength = dir.mag();
    let stretch = currentLength - this.restLength;

    dir.normalize();
    dir.mult(-1 * this.k * stretch);

    particle.applyForce(dir);
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      const particle = this.particles[i];
      particle.run();
      if (particle.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}
```

#### Código y link

```js
let emitter;

function setup() {
  createCanvas(680, 480);
  emitter = new Emitter(width / 2, height/2);
}

function draw() {
  background(255,30);

  let gravity = createVector(0, 0.1);
  emitter.applyForce(gravity);

  emitter.addParticle();
  emitter.run();
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0.0);
    this.velocity = createVector(random(-0.1, 0.1), random(-0.1, 0.1));
    this.lifespan = 255.0;
    this.mass = 1;
  }

  run() {
    this.update();
    this.show();
  }

  applyForce(force) {
    let f = force.copy();
    f.div(this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
    this.lifespan -= 2.0;
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
    this.restLength = 100;
    this.k = 0.05;
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  applyForce(force) {
    for (let particle of this.particles) {
      particle.applyForce(force);
      this.applySpringForce(particle);
    }
  }

  applySpringForce(particle) {
    let dir = p5.Vector.sub(particle.position, this.origin);
    let currentLength = dir.mag();
    let stretch = currentLength - this.restLength;

    dir.normalize();
    dir.mult(-1 * this.k * stretch);

    particle.applyForce(dir);
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      const particle = this.particles[i];
      particle.run();
      if (particle.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}
```

https://editor.p5js.org/SheiinX/sketches/j97lsZCDB

### Ejmemplo 4.7
De este intenté meterle una aplicación de atracción gravitatoria antes de que fueran lanzadas, utilizando funciones trigonometricas dentro del código, pero un poco complicado cuando todo el rato está intentando alejar las particulas.

Igualmente se consiguió hacer un efecto parecido, lo cual hace que cuando lleguen al objeto repeledor, las particulas no serían repelidas de una vez, sino hasta que lleguen hasta abajo. Aplicandoselo a la clase repeller donde se cambiará un poco la lógica de la función repel para que se genere una tangente aplicando las funciones de sin y cos.

```js
if (distance < influenceRadius) {
      let angle = atan2(dir.y, dir.x);

      let tangent = createVector(cos(angle), sin(angle));

      let strength = map(distance, 0, influenceRadius, 0.5, 0);
      tangent.mult(strength * 4);

      return tangent;
    }
```

#### Código y link

```js
let emitter;

let repeller;

function setup() {
  createCanvas(640 , 640);
  emitter = new Emitter(width / 2, 60);
  repeller = new Repeller(width / 2, 250);
}

function draw() {
  background(255);
  emitter.addParticle();
  let gravity = createVector(0, 0.1);
  emitter.applyForce(gravity);
  emitter.applyRepeller(repeller);
  emitter.run();

  repeller.show();
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.acceleration = createVector(0, 0);
    this.lifespan = 255.0;
  }

  run() {
    this.update();
    this.show();
  }

  applyForce(f) {
    this.acceleration.add(f);
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
    return this.lifespan < 0.0;
  }
}

class Emitter {

  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  applyForce(force) {
    for (let particle of this.particles) {
      particle.applyForce(force);
    }
  }

  applyRepeller(repeller) {
    for (let particle of this.particles) {
      let force = repeller.repel(particle);
      particle.applyForce(force);
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      const particle = this.particles[i];
      particle.run();
      if (particle.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

class Repeller {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.power = 200;
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 32);

    // Zona de influencia visual
    noFill();
    stroke(0, 30);
    ellipse(this.position.x, this.position.y, 120);
  }

  repel(particle) {
    let dir = p5.Vector.sub(this.position, particle.position);
    let distance = dir.mag();
    let influenceRadius = 60;

    if (distance < influenceRadius) {
      let angle = atan2(dir.y, dir.x);

      let tangent = createVector(cos(angle), sin(angle));

      let strength = map(distance, 0, influenceRadius, 0.5, 0);
      tangent.mult(strength * 4);

      return tangent;
    }

    return createVector(0, 0);
  }
}
```

https://editor.p5js.org/SheiinX/sketches/97Kj6viu8
