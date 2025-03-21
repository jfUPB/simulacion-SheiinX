* Para tener fuerzas acumulativas se necesita hacer que se vaya sumando las fuerzas o los vectores cada vez que se vean modificando (Si no se modifican y se tienen en cada frame, se necesita que en cada frame se resetee multiplicando por 0 la fuerza total), para esto está el vector.add(force).
* ````js
  display() {
    ellipseMode(CENTER);
    stroke(0);
    if (this.dragging) {
      fill(25,25,25);
    } else if (this.rollover) {
      fill(25,25,25);
    } else {
      fill(25,25,25);
    }
    ellipse(this.position.x, this.position.y, this.mass * 2);
  }
  ````
  En el código hay una clase que es el Attractor(), y en este en el display puedo ver en donde se dibuja el objeto dentro del canvas y cambiar su color.
* ````jsclass
  Attractor {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.mass = 20;
    this.G = 1;
    this.dragging = false;
    this.rollover = false; 
    this.offset = createVector(0, 0);
  }

  attract(mover) {
    // Calculate direction of force
    let force = p5.Vector.sub(this.position, mover.position);
    // Distance between objects
    let distance = force.mag();
    // Limiting the distance to eliminate "extreme" results for very close or very far objects
    distance = constrain(distance, 5, 25);

    // Calculate gravitional force magnitude
    let strength = (this.G * this.mass * mover.mass) / (distance * distance);
    // Get force vector --> magnitude * direction
    force.setMag(strength);
    return force;
  }
  
  mouseOver() {
    let d = dist(mouseX, mouseY, this.position.x, this.position.y);
    if (d < this.mass) {
      this.rollover = true;
    } else {
      this.rollover = false;
    }
  }
  
  
  mousePressed() {
    let d = dist(mouseX, mouseY, this.position.x, this.position.y);
    if (d < this.mass) {
      this.dragging = true;
      this.offset.x = this.position.x - mouseX;
      this.offset.y = this.position.y - mouseY;
    }
  }

  mouseDragged() {
    if (this.dragging) {
      this.position.x = mouseX + this.offset.x;
      this.position.y = mouseY + this.offset.y;
    }
  }

  mouseReleased() {
    this.dragging = false;
  }

  // Method to display
  display() {
    ellipseMode(CENTER);
    stroke(0);
    if (this.dragging) {
      fill(150, 0, 0); 
    } else if (this.rollover) {
      fill(145,0,145); 
    } else {
      fill(25); 
    }
    ellipse(this.position.x, this.position.y, this.mass * 2);
  }
  }
  ````
  Utilizando el cálculo de la distancia entre el mouse y la posición, y las funciones proporcionadas para cuando esté encima o sea presionado, así le agregaría para poder tener tales funcionando y que cambie los colores, ah y también para moverlo.
