### Lo que ocurre
De la primera modificación se tiene que desde el p5.Vector.fromAngle() solo recibe la primera parte de la función, que es directamente el theta y la otra parte que es la longitud se le asigna el base que es 1, lo cual al darselo al iniciar el círculo hace que se mantenga estático, no es suficiente la longitud como para moverlo al ir cambiandole el valor del theta.

Ya de la segunda ya se tiene una longitud mayor a 1, la cual es la magnitud r, esto permite ya tener una posición en el plano cartesiano grande para poder ir moviendolo mientras se va actualizando el theta. p5.Vector.fromAngle(theta,r)
