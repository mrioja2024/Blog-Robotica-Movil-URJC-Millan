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

Una vez obtenida la imagen en HSV se definen diferentes rangos correspondientes al color rojo. Debido a la representación del tono en HSV utilizada por OpenCV, el rojo se encuentra dividido entre los dos extremos del canal H. Por este motivo se utilizan dos intervalos de detección y posteriormente se combinan. Mediante cv2.inRange() se genera una máscara binaria. En esta máscara: Los píxeles detectados como rojos aparecen en blanco, el resto de la imagen aparece en negro. Esto permite aislar la línea del resto de elementos presentes en la imagen.

## 3. Regiones de interés

Procesar toda la imagen de la cámara no siempre es necesario, ya que la información más importante para controlar el vehículo se encuentra principalmente en la zona de la carretera situada delante de él. Por este motivo se utilizan regiones de interés. Durante el desarrollo he realizado pruebas utilizando una única región situada en la parte inferior de la imagen. Posteriormente he probado varias franjas horizontales situadas a diferentes alturas para obtener información tanto de la línea cercana al vehículo como de zonas situadas más adelante. El objetivo de utilizar varias franjas es conseguir que el vehículo pueda anticiparse a las curvas antes de llegar a ellas.

## 4. Calculo del centroide
Después de generar la máscara se calculan los momentos de la imagen mediante: cv2.moments() El valor m00 permite comprobar si se ha detectado una cantidad de píxeles correspondiente a la línea. Si m00 es mayor que cero, se puede calcular la posición horizontal del centroide mediante los momentos de la máscara. El centroide representa aproximadamente el centro de la zona roja detectada. La coordenada horizontal del centroide se utiliza para saber si la línea se encuentra:
  - A la izquierda del vehículo.
  - En el centro.
  - A la derecha del vehículo.

## 5. Calculo del error
Para controlar el vehículo se calcula un error comparando la posición de la línea con el centro de la imagen.Se utiliza la expresión: error = cx - centro_imagen. Si el error es aproximadamente cero, significa que la línea se encuentra centrada. Si el error es positivo, la línea se encuentra hacia uno de los lados de la imagen. Si el error es negativo, se encuentra hacia el lado contrario. La magnitud del error indica cuánto se ha desviado la línea respecto al centro de la cámara.

[Grabación de pantalla desde 2026-10-16 20-21-27.webm](https://github.com/user-attachments/assets/9a7f771e-099d-459e-bf2a-41d1cda17534)

  
