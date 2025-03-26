```js
let angle = 0;
let angleVelocity = 0.2;
let amplitude = 100;

function setup() {
  createCanvas(640, 240);
  frameRate(24);
}

function draw(){
  background(255);

  stroke(0);
  strokeWeight(2);
  fill(127, 127);

  for (let x = 0; x <= width; x += 24) {
    // 1) Calculate the y position according to amplitude and sine of the angle.
    let y = amplitude * sin(angle);
    // 2) Draw a circle at the (x,y) position.
    circle(x, y + height / 2, 48);
    // 3) Increment the angle according to angular velocity.
    angle += angleVelocity;
  }
}
```

Primera alternativa, pasar la función para draw y bajarle los frames para poder ver el movimiento en ola del canva

![First Sin](../../../../assets/)

```js
let angle = 0;
let angleVelocity = 0.2;
let amplitude = 100;
let startAngle = 0;

function setup() {
  createCanvas(640, 240);
  //frameRate(24);
}

function draw(){
  background(255);

  stroke(0);
  strokeWeight(2);
  fill(127, 127);
  
  angle = startAngle;
  startAngle += 0.02;
  
  for (let x = 0; x <= width; x += 24) {
    // 1) Calculate the y position according to amplitude and sine of the angle.
    //let y = amplitude * sin(angle);
    let y = map(sin(angle), -1, 1, 0, height);
    // 2) Draw a circle at the (x,y) position.
    circle(x, y, 48);
    // 3) Increment the angle according to angular velocity.
    angle += angleVelocity;
  }
}
```

Segunda manera, utilizando un ángulo inicial para controlar el movimiento y que este no se mueva en x pero se quede fijo y solo se mueva en y

![Second Sin](../../../../assets/)
