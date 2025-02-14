### Bueno, lo que espero conseguir es lo siguiente:
* El dato del vector base
* El dato del vector después de la función
* Además quitar y ver que pasa con el NoLoop

### ¿Qué obtuve?
* p5.Vector Object : [6, 9, 0]
* p5.Vector Object : [20, 30, 0]
* El console.log("Only once"); Corriendo y sacando el mismo mensaje hasta que acabe el programa

### Paso por valor y paso por referencia
Estos pasos hacen referencia para poder cambiar ciertas variables pasando algún tipo de dato a y cambiando su output. Por el paso por valor son las variables que uno pasa y cambia, pero nunca cambia su variable original, se mantiene en un espacio de memoria el valor de la variable original intacta y la versión modificada pasa a otro espacio de memoria. Ya de parte de paso por referencia, son aquellos que pueden cambiar el valor de la variable en el espacio de la memoria por completo, significando que no solo se pasa el valor para trabajar, sino que es la variable entera y se va cambiando conforme se utiliza en las funciones.

### JavaScript
De parte de javascript, el siguiente código utilizará ambas y devolverá los respectivos valores

```js
//Paso por valor
let n = 10;

modifyV(n);
console.log("Por valor modificado: ", n); //Este devuelve 10

//Paso por referencia
let obj = { m: 10 };

modifyR(obj);
console.log("Por referencia modificado: ", obj.m); //Este devuelve 20

function modifyV(x) {
    x = 20;
    console.log("Por valor en función: ", x); //Este devuelve 20
}

function modifyR(y) {
    y.m = 20;
    console.log("Por referencia en función: ", y.m); //Este devuelve 20
}
```

Para javascript, las variables o tipos de datos que son considerados "Primitivos" como los int, string, etc., serán los que vayan a ser cambiados por valor, no cambia el espacio de memoria original.

Los tipos de datos "No primitivos" como los arreglos, las funciones y los objetos, serán los que pueden cambiar los valores del espacio de memoria asignado, y ese paso es por referencia.

### ¿Qué aprendí?
Volví a acordar como funcionaba la ram en un pc y el uso de memoria.

![Sample Text](../../../../assets/cat-crying.jpg)
