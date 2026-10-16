# Follow Line

## Descripción del proyecto

En esta práctica se desarrolla el comportamiento de un vehículo autónomo capaz de seguir una línea roja utilizando la información obtenida mediante una cámara frontal. El objetivo principal es conseguir que el vehículo complete el circuito siguiendo la línea de forma estable y con la mayor velocidad posible, evitando salirse del recorrido sobre todo en las curvas.
Para ello se utilizan principalmente:
  - Cámara frontal.
  - Procesamiento de imágenes con OpenCV.
  - Espacio de color HSV.
  - Detección de color.
  - Cálculo del centroide de la línea.
  - Velocidad lineal.
  - Velocidad angular.

# Desarrollo
## 1. Obtención y procesamiento de la imagen

  El primer paso fue obtener las imágenes proporcionadas por la cámara frontal del vehículo. La imagen se obtiene continuamente mediante HAL.getImage(). Las imágenes recibidas se encuentran inicialmente en formato     BGR. Para facilitar la detección de la línea roja se realiza una conversión al espacio de color HSV mediante OpenCV. De esta forma resulta más sencillo detectar la línea roja incluso cuando existen pequeñas          variaciones en la iluminación de la escena.
  
## 2. Detección de la línea roja

Una vez obtenida la imagen en HSV se definen diferentes rangos correspondientes al color rojo. Debido a la representación del tono en HSV utilizada por OpenCV, el rojo se encuentra dividido entre los dos extremos del canal H. Por este motivo se utilizan dos intervalos de detección y posteriormente se combinan. Mediante cv2.inRange() se genera una máscara binaria. En esta máscara: Los píxeles detectados como rojos aparecen en blanco. El resto de la imagen aparece en negro. Esto permite aislar la línea del resto de elementos presentes en la imagen.

##


