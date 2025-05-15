#### 1. Flujo

En setup se configura de manera que se inicia el Engine (Y si uno busca solo utilizar matter.js, se utiliza noCanvas() y configurar el canvas a base de las funciones de matter.js), eso con el proposito para iniciar el sistema de matter.js cuando se inicia el código y otras instancias como los objetos.

Segundo en el draw, ya se hace que el Engine siempre se mantenga actualizandose (update), de manera que se ejecute todo el sistema mientras corra en p5.js. Además también se hacen todas las otras funciones para mostrar los elementos de matter.js (Cómo el rectángulo, el cual se inicializa con el Bodies.rectangle() y se tiene que agregar al Composite.add() de manera que sea añadido al mundo del matter.js que se tiene; De ahí ya es ir combinando funciones con p5.js).

#### 2. Representación visual

No hay mucho desafío en dibujar los elementos, debido a que uno puede acceder a las variables de los objetos creados por matter.js de manera fácil, lo cual permite pasar esos datos y esas variables a un nuevo objeto de p5.js, lo cual permitía una fácil representación visual del objeto en pantalla (this.body = Bodies.rectangle(x, y, w, h); let pos = this.body.position; el objeto tiene los valores y se acceden y luego se pasan a un objeto de p5 translate(pos.x, pos.y); rect(0, 0, this.w, this.h);)

#### 3. Formas complejas

Igual que mencioné, no hice las formas, directamente utilice una forma que dibujaba una letra sin ningún collider encima del objeto mientras no se mostraba. Pero estoy seguro que hay una manera de hacerlos físicos como tal, pero por ejemplo en internet muestran el uso de otra librería para hacer que sean físicos los elementos dentro de matter.js; Y también de otra manera ahí pensada, es la de hacer objetos individuales con sus respectivas variables, hasta formar las formas de las letras, pero, poco optimo y mucho código.

#### 4. Física de la Semántica

Dependiendo de la palabra, es fácil hacer esas simulaciones, ya que hay muchas palabras que denotan directamente un evento de la física como la conocemos, pero luego están las palabras más abstractas como el de vampiro, que muestrán una posibilidad para hacerlos, más compleja, ya que se necesita hacer cambios muy específicos de la letra, lo cual hace que sea más difícil hacerlos.

#### 5. Potencial

Juegos, matter.js directamente es un sistema de físicas más controlado y mejor que el de p5.js, lo cual permitiría el desarrollo de juegos simples con esto.
