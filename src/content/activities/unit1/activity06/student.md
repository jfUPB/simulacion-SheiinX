

### Extra
Dejaré este pequeño código acá antes de hacer que funcionará el levy flight, ya que me pareció curioso como se pueso a dibujar las líneas alrededor del centro
```js
let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
    this.prevX = this.x;
    this.prevY = this.y;
  }

  show() {
    stroke(0);
    line(this.x, this.y, this.prevX, this.prevY);
  }

step() {
    const choice = floor(random(8));
    let r = random(1);
    
    if(r < 0.01){
      //Can be changed to have more space between jumps
      this.x += random(-30, 30);
      this.y += random(-30, 30);
    } else{
      this.x += random(-1, 1);
      this.y += random(-1, 1);
    }
  }
}
```
