```js
let aKey = false;
let dKey = false;
let wKey = false;

function setup() {
  createCanvas(640, 540);
  user = new CircleObject();
}

function draw() {
  background(255, 50);

  //square(550, 350, 100);
  
  user.update();
  //user.floorCheck();
  user.gravity();
  user.checkedEdges();
  user.moveCircle();
  user.show();
}

function keyPressed() {
  if (key === 'd' || key === 'D') {
    dKey = true;
  }
  if (key === 'a' || key === 'A') {
    aKey = true;
  }
  if (key === 'w' || key === 'W') {
    wKey = true;
  }
}

function keyReleased() {
  if (key === 'd' || key === 'D') {
    dKey = false;
  }
  if (key === 'a' || key === 'A') {
    aKey = false;
  }
  if (key === 'w' || key === 'W') {
    wKey = false;
  }
}

class CircleObject{
  constructor() {
    this.position = createVector(width/2, height/2);
    this.velocity = createVector(0, 0);
    
    this.acceleration = createVector(0, 0);
    
    //this.canMove = true;
  }

  update() {
    this.position.add(this.velocity);
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 100);
  }
  
  gravity(){
    if(this.position.y + 50 < height){
      this.acceleration = createVector(0, 0.1);
      this.velocity.add(this.acceleration);
      this.position.add(this.velocity);
    } else {
      this.velocity.y = 0;
    }
    
  }
  
  checkPlatform(){
    
  }
  
 moveCircle() {
  // derecha
  if(keyIsDown(68)){
    this.acceleration = createVector(0.1, 0);
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
  }
  // izquierda
  if(keyIsDown(65)){
    this.acceleration = createVector(-0.1, 0);
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
  }
  // salto
  if(keyIsDown(87) && this.position.y + 50 >= height){
    this.acceleration = createVector(0, -5); // Jump only when on the ground
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
  }
}
  
  checkedEdges(){
    if (this.position.x + 50 > width) {
      this.velocity.x = 0;
    } else if (this.position.x - 50 < 0) {
      this.velocity.x = 0;
    }
  }
}
```

