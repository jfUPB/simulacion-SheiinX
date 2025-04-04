```js
let t = 0;
let direction = 1;

function setup() {
    createCanvas(300, 300);
}

function draw() {
    background(200);
  
    let v0 = createVector(width/2, height/2);
    let v1 = createVector((mouseX - width / 2) * 0.8, (mouseY - height / 2) * 0.8);
    let v2 = createVector((mouseX - width / 5) * -0.8, (mouseY - height / 5) * -0.8);
  
    //v1.add(v0);
    //v2.add(v0);
    let v3 = p5.Vector.lerp(v1, v2, t);
    let v4 = p5.Vector.sub(v2, v1);
    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple');
    drawArrow(v1.add(v0), v4, 'peru');
    
    t += 0.01 * direction;
  
    if(t >= 1 || t <= 0){
      direction *= -1;
    }
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```

Igual que en la anterior unidad, pongo el movimiento del mouse relacionado al tamaño del canvas y lo pongo para que tome en cuenta la mitad del mismo canvas.

Los v1 y v2 serían los que se están moviendo con respecto a la posición del mouse, con el v2 teniendo un movimiento opuesto para que haya un espacio entre los dos y se pueda ir actualizando la posición de todos los vectores.
