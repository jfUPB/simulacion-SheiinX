Aquí hay dos versiones
```js
let pendulum;
let pendulum2;

function setup() {
  createCanvas(640, 640);
  // Make a new Pendulum with an origin position and armlength
  pendulum = new Pendulum(width / 2, 0, 175);
  pendulum2 = new Pendulum(pendulum.bob.x, pendulum.bob.y, 175);
}

function draw() {
  background(255);
  pendulum.update();
  pendulum.show();
  pendulum.drag(); // for user interaction
  
  pendulum2.setPivot(pendulum.bob.x, pendulum.bob.y);
  
  pendulum2.update();
  pendulum2.show();
  pendulum2.drag();
}

function mousePressed() {
  pendulum.clicked(mouseX, mouseY);
  pendulum2.clicked(mouseX, mouseY);
}

function mouseReleased() {
  pendulum.stopDragging();
  pendulum2.stopDragging();
}


class Pendulum {
  constructor(x, y, r) {
    // Fill all variables
    this.pivot = createVector(x, y);
    this.bob = createVector();
    this.r = r;
    this.angle = PI / 4;

    this.angleVelocity = 0.0;
    this.angleAcceleration = 0.0;
    this.damping = 0.995; // Arbitrary damping
    this.ballr = 24.0; // Arbitrary ball radius
  }

  // Function to update position
  update() {
    // As long as we aren't dragging the pendulum, let it swing!
    if (!this.dragging) {
      let gravity = 0.4; // Arbitrary constant
      this.angleAcceleration = ((-1 * gravity) / this.r) * sin(this.angle); // Calculate acceleration (see: http://www.myphysicslab.com/pendulum1.html)

      this.angleVelocity += this.angleAcceleration; // Increment velocity
      this.angle += this.angleVelocity; // Increment angle

      this.angleVelocity *= this.damping; // Apply some damping
    }
  }
  
  setPivot(x, y) {
    this.pivot.set(x, y);
  }

  show() {
    this.bob.set(this.r * sin(this.angle), this.r * cos(this.angle), 0); // Polar to cartesian conversion
    this.bob.add(this.pivot); // Make sure the position is relative to the pendulum's origin

    stroke(0);
    strokeWeight(2);
    // Draw the arm
    line(this.pivot.x, this.pivot.y, this.bob.x, this.bob.y);
    fill(127);
    // Draw the ball
    circle(this.bob.x, this.bob.y, this.ballr * 2);
  }

  // The methods below are for mouse interaction

  // This checks to see if we clicked on the pendulum ball
  clicked(mx, my) {
    let d = dist(mx, my, this.bob.x, this.bob.y);
    if (d < this.ballr) {
      this.dragging = true;
    }
  }

  // This tells us we are not longer clicking on the ball
  stopDragging() {
    this.angleVelocity = 0; // No velocity once you let go
    this.dragging = false;
  }

  drag() {
    // If we are draging the ball, we calculate the angle between the
    // pendulum origin and mouse position
    // we assign that angle to the pendulum
    if (this.dragging) {
      let diff = p5.Vector.sub(this.pivot, createVector(mouseX, mouseY)); // Difference between 2 points
      this.angle = atan2(-1 * diff.y, diff.x) - radians(90); // Angle relative to vertical axis
    }
  }
}
```
Que es directamente asignarle otro pendulo y que su punto de giro esté pegado al primero pero sin realmente tener la 
https://editor.p5js.org/SheiinX/sketches/-VD4xJLAU

Pero luego está esta otra solución de gpt la cual solo puede agregar dos y las operaciones depende de las mismas funciones de la clase

```js
let p;

function setup() {
  createCanvas(640, 360);
  p = new DoublePendulum(width / 2, 100, 125, 125);
}

function draw() {
  background(255);
  p.update();
  p.show();
}

function mousePressed() {
  p.clicked(mouseX, mouseY);
}

function mouseReleased() {
  p.stopDragging();
}

class DoublePendulum {
  constructor(x, y, r1, r2) {
    this.pivot = createVector(x, y);
    
    // Longitudes de los brazos
    this.r1 = r1;
    this.r2 = r2;
    
    // Masas de los péndulos
    this.m1 = 10;
    this.m2 = 10;
    
    // Ángulos iniciales
    this.a1 = PI / 2;
    this.a2 = PI / 2;
    
    // Velocidades y aceleraciones angulares
    this.a1_v = 0;
    this.a2_v = 0;
    this.a1_a = 0;
    this.a2_a = 0;
    
    // Gravedad
    this.g = 1;
    
    // Posiciones de los bobs
    this.bob1 = createVector();
    this.bob2 = createVector();
    
    this.dragging1 = false;
    this.dragging2 = false;
  }

  update() {
    if (!this.dragging1 && !this.dragging2) {
      // **Cálculo de aceleraciones usando la física del doble péndulo**
      let num1 = -this.g * (2 * this.m1 + this.m2) * sin(this.a1);
      let num2 = -this.m2 * this.g * sin(this.a1 - 2 * this.a2);
      let num3 = -2 * sin(this.a1 - this.a2) * this.m2;
      let num4 = this.a2_v * this.a2_v * this.r2 + this.a1_v * this.a1_v * this.r1 * cos(this.a1 - this.a2);
      let den = this.r1 * (2 * this.m1 + this.m2 - this.m2 * cos(2 * this.a1 - 2 * this.a2));
      this.a1_a = (num1 + num2 + num3 * num4) / den;

      num1 = 2 * sin(this.a1 - this.a2);
      num2 = (this.a1_v * this.a1_v * this.r1 * (this.m1 + this.m2));
      num3 = this.g * (this.m1 + this.m2) * cos(this.a1);
      num4 = this.a2_v * this.a2_v * this.r2 * this.m2 * cos(this.a1 - this.a2);
      den = this.r2 * (2 * this.m1 + this.m2 - this.m2 * cos(2 * this.a1 - 2 * this.a2));
      this.a2_a = (num1 * (num2 + num3 + num4)) / den;

      this.a1_v += this.a1_a;
      this.a2_v += this.a2_a;
      this.a1 += this.a1_v;
      this.a2 += this.a2_v;
    }

    this.bob1.set(this.pivot.x + this.r1 * sin(this.a1), this.pivot.y + this.r1 * cos(this.a1));
    this.bob2.set(this.bob1.x + this.r2 * sin(this.a2), this.bob1.y + this.r2 * cos(this.a2));
  }

  show() {
    stroke(0);
    strokeWeight(2);
    
    // Dibujar el primer brazo
    line(this.pivot.x, this.pivot.y, this.bob1.x, this.bob1.y);
    
    // Dibujar el segundo brazo
    line(this.bob1.x, this.bob1.y, this.bob2.x, this.bob2.y);
    
    fill(127);
    circle(this.bob1.x, this.bob1.y, 20);
    circle(this.bob2.x, this.bob2.y, 20);
  }

  clicked(mx, my) {
    if (dist(mx, my, this.bob1.x, this.bob1.y) < 10) {
      this.dragging1 = true;
    } else if (dist(mx, my, this.bob2.x, this.bob2.y) < 10) {
      this.dragging2 = true;
    }
  }

  stopDragging() {
    this.a1_v = 0;
    this.a2_v = 0;
    this.dragging1 = false;
    this.dragging2 = false;
  }
}
```
