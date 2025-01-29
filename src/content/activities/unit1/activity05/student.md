### Números aleatorios con distribución normal

```js
let heigh = 350;
let widt = 350;

function setup() {
  createCanvas(heigh, widt);

  let backgr = randomGaussian(200,10);
  background(backgr);
  frameRate(5);
}

function draw(){
  let x = randomGaussian(heigh/2,50);
  let y = randomGaussian(widt/2,50);
  
  circle(x, y, 25);
}
```

Centrandonos directamente en el código, en la función draw estaremos controlando las dos variables de X y Y, asignandoles un número aleatorio con distribución normal, tomando el dato de la altura y el ancho de la pantalla y poniendolo en toda la mitad, de ahí obtiene un número grande desviación estandar y permite que los circulos se generen en un área grande, bajando el valor de la DA hará que los circulos se generen más cercanos los unos a los otros.
