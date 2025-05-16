* Constant
```js
//let mover;

function setup() {
  createCanvas(640, 540);
  mover = new Mover();
}

function draw() {
  background(255);

  strokeWeight(10);
  stroke('orange');
  line(0,0,width,0);
  strokeWeight(10);
  stroke('blue');
  line(0,height,width,height);
  
  mover.update();
  mover.checkEdges();
  mover.show();
}

class Mover {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = createVector(random(-5, 5), random(-5, 5));
    
    this.acceleration = createVector(0.001, 0.1);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    console.log(this.velocity.toString());
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 100);
  }

  checkEdges() {
    if (this.position.x > width) {
      this.velocity.x *= -1;
    } else if (this.position.x < 0) {
      this.velocity.x *= -1;
    }

    if (this.position.y > height) {
      //this.velocity.y *= -1;
      this.position.y = 0;
    } else if (this.position.y < 0) {
      //this.velocity.y *= -1;
      this.velocity.y = height;
    }
  }
}
```

Con este código probé la aceleración constante, donde simplemente la velocidad va aumentando a un ritmo uniforme. Con esta forma directamente pude ver una aplicación de fuerzas, sobre todo una similar a la gravedad, lo cual la velocidad a veces intentaba ir para arriba en como lo vemos, pero como iba sumando rápido para abajo, constantemente, eventualmente generó un movimiento parabólico afectado por algo similar a la gravedad y lo empujaba para abajo.

* Random
```js
//let mover;

function setup() {
  createCanvas(640, 540);
  mover = new Mover();
}

function draw() {
  background(255);

  mover.update();
  mover.checkEdges();
  mover.show();
}

class Mover {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = createVector(random(-5, 5), random(-5, 5));
    
    this.acceleration = createVector(0, 0);
  }

  update() {
    this.acceleration = p5.Vector.random2D();
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    console.log(this.velocity.toString());
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 100);
  }

  checkEdges() {
    if (this.position.x > width) {
      this.velocity.x *= -1;
    } else if (this.position.x < 0) {
      this.velocity.x *= -1;
    }

    if (this.position.y > height) {
      this.velocity.y *= -1;
      //this.position.y = 0;
    } else if (this.position.y < 0) {
      this.velocity.y *= -1;
      //this.velocity.y = height;
    }
  }
}
```

Este es bastante curioso, ya que a diferencia del constante que aplica una fuerza a una dirección en específico (Al escribir el código de una forma muy básica como presentado anteriormente) o los suma a una dirección siempre, este mantiene cambiando a diferentes direcciones, y ahí no sé ve aplicada una fuerza, sino que se puede ver que se puede mover por el entorno como un random walker, estilo levy flight por los cambios bruscos de velocidad que se generan.

* Perseguir mouse
```js
//let mover;

function setup() {
  createCanvas(640, 540);
  mover = new Mover();
}

function draw() {
  background(255);

  mover.update();
  mover.checkEdges();
  mover.show();
}

class Mover {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = createVector(random(-5, 5), random(-5, 5));
    
    this.acceleration = createVector(0, 0);
  }

  update() {
    let mouse = createVector(mouseX, mouseY);
    let dir = p5.Vector.sub(mouse, this.position);
    dir.normalize();
    dir.mult(0.2);
    this.acceleration = dir;
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 100);
  }

  checkEdges() {
    if (this.position.x > width) {
      this.velocity.x *= -1;
    } else if (this.position.x < 0) {
      this.velocity.x *= -1;
    }

    if (this.position.y > height) {
      //this.velocity.y *= -1;
      this.position.y = 0;
    } else if (this.position.y < 0) {
      //this.velocity.y *= -1;
      this.position.y = height;
    }
  }
}
```

Ya para el comportamiento mientras va siguiente un objeto (En este caso el mouse), tiene un sistema particular y es que directamente siempre buscará el mouse pero nunca se detendrá, significando que la aceleración seguirá sumando constantemente no importa qué, mientras más cercano y menos velocidad tengo sobre el mouse, menor será la suma de los vectores, pero siempre se mantendrá orbitando, y según como tenga uno el entorno hecho, es posible que pueda sacar inclusive más velocidad de lo que se espera.
