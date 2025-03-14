### Fuerza por 0
Este método de multiplicar por 0 en cada frame el vector, sirve para resetearlo, por así decirlo, de manera que en cada frame tengamos el calculo de las fuerzas correspondientes sin que se esté sumando sobre el tiempo de manera indefinida y no controlada hasta que o va muy rápido o se queda quieto o hay algún problema dentro del código que genere un movimiento extraño.

De esta manera, el mult() practicamente es como resetear el vector cada frame de manera que al inicio del frame pueda estar de nuevo calculado sin que se apile con el calculo del anterior frame.

Y eso se hace al final del update() para que pueda aplicar antes la fuerza correspondiente.
