# Práctica Obstacle Avoidance
## 1. Objetivo de la práctica
El objetivo de esta práctica es conseguir que un coche de Fórmula 1 complete un circuito de manera autónoma, siguiendo una trayectoria y evitando los coches que hay parados por el camino.
Para ello se utiliza el sensor, que permite conocer la posición del coche y los puntos por los que tiene que pasar, y el sensor láser, que detecta los obstáculos que tiene alrededor.
La navegación se realiza mediante el algoritmo VFF (Virtual Force Field), que utiliza fuerzas atractivas y repulsivas para decidir hacia dónde tiene que dirigirse el coche.
Además de conseguir que termine el circuito sin chocarse, también se intenta que lo haga lo más rápido posible.
## 2. Desarrollo de la práctica
### Primera versión
Al principio empecé haciendo un código bastante sencillo utilizando las fuerzas atractivas y repulsivas.
La fuerza atractiva hacía que el coche se dirigiera hacia el siguiente objetivo GPS, mientras que la repulsiva servía para alejarlo de los obstáculos detectados por el láser.
En las primeras pruebas el coche conseguía avanzar por el circuito, pero en cuanto se encontraba con otro coche parado se quedaba bloqueado.
Esto ocurría porque al acercarse demasiado a un obstáculo la velocidad bajaba hasta 0. El problema era que, al tratarse de un coche así no podía girar sobre sí mismo para salir de esa situación.
Para intentar solucionarlo cambié las distancias de detección e hice que el coche empezara a girar antes de llegar al obstáculo.

### Seguimiento de la línea roja
Después de los primeros cambios, el coche ya conseguía esquivar algunos obstáculos y recorrer parte del circuito.
Sin embargo, había otro problema: no seguía demasiado bien la línea roja y en algunos momentos se alejaba bastante de la trayectoria.
Esto pasaba porque las fuerzas repulsivas hacían que el coche cambiara mucho de dirección.
Para solucionarlo modifiqué el programa para que siguiera principalmente los puntos GPS y solo se desviara de la trayectoria cuando encontrara un obstáculo.
Con este cambio el coche empezó a seguir mucho mejor el recorrido.

## 3. Problemas encontrados
### El coche se quedaba parado
Fue uno de los primeros problemas que aparecieron.
Cuando el láser detectaba un obstáculo demasiado cerca, la velocidad se reducía hasta 0 y el coche ya no podía esquivarlo.
Para solucionarlo se aumentó la distancia desde la que comenzaba el adelantamiento y se añadieron los puntos temporales para rodear los obstáculos.
### Problemas en las curvas
Otro problema apareció cuando el coche encontraba un obstáculo en mitad de una curva.
En algunas pruebas no conseguía adelantarlo y terminaba quedándose parado.
Se modificó la detección de obstáculos para que también pudiera comenzar un adelantamiento mientras estaba girando.

### El coche se salía de la carretera
Cuando empecé a aumentar bastante las velocidades, aparecieron problemas en algunas curvas.
En una de las pruebas el coche se salió de la carretera y tardó bastante tiempo en conseguir volver a la trayectoria.
Por eso fue necesario ajustar la velocidad dependiendo del giro, para que pudiera ir rápido en las rectas pero redujera la velocidad cuando la curva fuera demasiado cerrada.

## 4. Funcionamiento del algoritmo VFF

El programa funciona mediante un bucle infinito en el que se actualizan continuamente los datos del GPS y del láser.
En cada iteración se calculan las fuerzas necesarias para dirigir el coche.
### Fuerza atractiva
La fuerza atractiva se encarga de dirigir el coche hacia el siguiente objetivo.
Se calcula utilizando la posición actual del coche y la posición del objetivo GPS.
La diferencia entre ambas posiciones permite obtener la dirección hacia la que tiene que avanzar.
### Fuerza repulsiva
La fuerza repulsiva sirve para evitar los obstáculos.
Para calcularla se utilizan las distancias obtenidas con el sensor láser.
Cuando hay un obstáculo cerca, se genera una fuerza en dirección contraria para que el coche intente alejarse de él.
Cuanto menor es la distancia al obstáculo, mayor es la fuerza repulsiva.

### Combinación de fuerzas
Una vez calculadas las fuerzas atractivas y repulsivas, se suman para obtener la fuerza total.
A partir de esta fuerza se calcula la velocidad angular W, que controla hacia dónde gira el coche.
La velocidad lineal V se calcula dependiendo de cuánto tenga que girar y de los obstáculos que haya delante.
Así, cuando el camino está despejado puede avanzar más rápido, mientras que en las curvas o al encontrar otro coche reduce la velocidad.

## 5. Resultado
Después de bastantes pruebas y cambios en el código, conseguí que el coche completara el circuito siguiendo los objetivos GPS y esquivando los obstáculos.
La mejora más importante fue añadir las fases de adelantamiento, ya que antes el coche se quedaba parado o se desviaba demasiado de la trayectoria.
También fue importante ajustar las fuerzas repulsivas para que no se acercara tanto a los obstáculo.
Una vez conseguido que completara la vuelta, seguí probando distintas velocidades para intentar reducir el tiempo.

## 6. Conclusión
Esta práctica me ha servido para entender mejor cómo funciona la navegación autónoma de un vehículo utilizando el GPS, el láser y el algoritmo VFF.
Lo que más me ha costado ha sido conseguir que el coche pudiera adelantar a los obstáculos sin quedarse parado y que después volviera correctamente a la línea roja.
Al final, lo que mejor resultado dio fue combinar las fuerzas VFF con los puntos GPS y utilizar distintas fases para realizar los adelantamientos.


