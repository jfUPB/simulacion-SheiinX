A la final en el primer concepto, me parecía mejor que pudiera dibujarlo, pero después de poner el background() con un alpha, me pareció incluso mejor lo que estaba saliendo, como un pequeño entorno interactivo más que el de dibujo.

Además no pude hacerlo como que el random walk pudiera orbitar, pero por jugar con el código pude hacer que tal intentará perseguir al mouse cuando se hiciera click y se mantuviera y dependiera de la posición del mouse en el canvas para que este intentará perseguirlo.

```js
let t = 0.0;
let prevX, prevY;
let firstClick = true;

function setup() {
  createCanvas(400, 400);
  //background(220);
  frameRate(25);
}

function draw() {
  background(220, 50);
  if(mouseIsPressed === true){
    circleGenerator();
    t+=0.1;
  }
  if(mouseIsPressed === true){
    walkerMouse(mouseX,mouseY);
  }
  console.log(firstClick);
}

function circleGenerator() {
  //Perlin noise
  let xoff = t;
  let perlinRadius = 0;

  for (let i = 0; i < 50; i++) {
    perlinRadius = noise(xoff) * 50;
    xoff += 0.1;
  }
  
  stroke(0);
  fill(random(250),random(250),random(250));
  circle(mouseX, mouseY, perlinRadius);
  stroke(random(250),random(250),random(250));
  line(mouseX, mouseY, width/2, height/2);
}

function mousePressed(){
  if(mouseIsPressed === true){
    firstClick = true;
  }
}

function mouseReleased(){
  firstClick = true;
}

function walkerMouse(xWalk, yWalk){
  if(firstClick === true){
    prevX = xWalk;
    prevY = yWalk;
    firstClick = false;
  }
  
  let offsetX = randomGaussian(mouseX/50,1);
  let offsetY = randomGaussian(mouseY/50,1);
  
  //let newX = prevX + random(randomGaussian(mouseX/50,5),-randomGaussian(mouseY/50,5));
  //console.log(newX);
  //let newY = prevY + random(randomGaussian(mouseY/50,5),-randomGaussian(mouseX/50,0.1));
  //console.log(newY);
  let newX;
  let newY;
  
  if(mouseX >= 200 && mouseY >= 200){
    newX = prevX + offsetX;
    newY = prevY + offsetY;
  } else if(mouseX >= 200 && mouseY <= 200){
    newX = prevX + offsetX;
    newY = prevY - offsetY;
  } else if(mouseX <= 200 && mouseY >= 200){
    newX = prevX - offsetX;
    newY = prevY + offsetY;
  } else if(mouseX <= 200 && mouseY <= 200){
    newX = prevX - offsetX;
    newY = prevY - offsetY;
  }
  
  console.log(mouseX);
  console.log(mouseY);
  
  stroke(random(250),random(250),random(250));
  line(prevX, prevY, newX, newY);
  
  prevX = newX;
  prevY = newY;
}
```
