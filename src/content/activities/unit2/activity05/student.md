```js
let t = 0;
let direction = 1;

function setup() {
    createCanvas(300, 300);
}

function draw() {
    background(200);
  
    let v0 = createVector(50, 50);
    let v1 = createVector(200, 20);
    let v2 = createVector(20, 200);
    let v3 = p5.Vector.lerp(v1, v2, t);
    let v4 = p5.Vector.sub(v2, v1);
    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, lerpColor('purple','peru',t));
    drawArrow(v1.add(v0), v4, 'peru');
    
    t += 0.01 * direction;
  
    if(t >= 1 || t <= 0){
      direction *= -1; //cambia la dirección
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

### lerp()/lerpColor()
lerp() es una función que en términos generales, saca un valor intermedio entre dos vectores (o dos números) con una tendencia que se especifíca en el tercer valor, entre 0 y 1, si es 0 va para el primer valor entregado y si es 1 va para el segundo valor.

Lo mismo con lerpColor(), se entregan 2 valores que son colores (RGB) y con un tercer valor saca un resultado entre los dos que tiende a más dependiendo de 0 o 1.

### drawArrow(base, vec, myColor)
Para dibujar las flechas con esta función, primero la combinación push(), translate(), pop(), que son funciones que al combinar mueve todo lo que se hace en el canvas y la mueve con el translate() específicado en esa función específica, luego en pop() reinicia todas las posiciones y vuelve a hacer el proceso si se vuelve a llamar.

El translate() mueve la base a la posición entregada y la mueve en el canvas a esa posición. Ya de ahí va dibujando la línea de acuerdo al vector, y al final le pone un triangulo calculando cual es el punto final.
