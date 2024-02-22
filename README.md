# Detección de Paneles Solares con Detectron2
![Ejemplo de Detectron2](https://github.com/tu_usuario/tu_repositorio/blob/main/images/detectron2.jpg?raw=true)
Este proyecto utiliza Detectron2, un framework de detección de objetos desarrollado por Facebook AI Research, para identificar paneles solares en imágenes aéreas capturadas por drones. A continuación, se describen los pasos necesarios para configurar el entorno de desarrollo y preparar los datos para el entrenamiento y la inferencia.

## Configuración del Entorno

Antes de comenzar, es crucial configurar correctamente el entorno de desarrollo para asegurar la compatibilidad y el rendimiento óptimo de Detectron2.

### Requisitos Previos

- Python 3.6 o superior
- PyTorch 1.5
- CUDA 10.1 (si se dispone de GPU compatible)

### Pasos de Instalación

1. **Instalar PyTorch y torchvision**:
   Asegúrate de tener instalada la versión adecuada de PyTorch para tu sistema, especialmente si planeas utilizar GPU.

   ```bash
   pip3 install -U torch==1.5 torchvision==0.6 -f https://download.pytorch.org/whl/cu101/torch_stable.html
   ```

2. **Instalar dependencias adicionales**:
   Cython y PyYAML son necesarios para el funcionamiento correcto de Detectron2 y cocoapi.

   ```bash
   pip3 install cython pyyaml==5.1
   ```

3. **Instalar cocoapi**:
   Útil para trabajar con el conjunto de datos COCO y evaluar los modelos.

   ```bash
   pip3 install -U 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
   ```

4. **Instalar Detectron2**:
   Con las dependencias en su lugar, instala Detectron2 usando pip.

   ```bash
   pip3 install detectron2==0.1.3 -f https://dl.fbaipublicfiles.com/detectron2/wheels/cu101/torch1.5/index.html
   ```

Con estos pasos, tu entorno estará listo para ejecutar Detectron2 y comenzar con la detección de paneles solares.

## Carga de Datos

Para entrenar un modelo de Detectron2 para la detección de paneles solares, necesitarás preparar y cargar tus datos. Este proyecto utiliza imágenes aéreas de paneles solares capturadas por drones, que deben ser etiquetadas adecuadamente antes del entrenamiento.

1. **Preparar el conjunto de datos**:
   Asegúrate de que tus imágenes estén etiquetadas con las ubicaciones de los paneles solares. Puedes utilizar herramientas como Labelbox para facilitar este proceso.

2. **Configurar claves de API para Labelbox**:
   Si utilizas Labelbox para la etiquetación, configura tus claves de API para acceder a tus proyectos y datos etiquetados.

   ```python
   LB_API_KEY = "TU_CLAVE_DE_API_AQUÍ"
   ENDPOINT = "https://api.labelbox.com/graphql"
   ```

3. **Cargar los datos etiquetados**:
   Con las imágenes y etiquetas preparadas, carga tus datos al entorno de Detectron2 para comenzar el proceso de entrenamiento.

Este esquema básico te ayudará a iniciar tu proyecto de detección de paneles solares con Detectron2. Recuerda ajustar los pasos de instalación y configuración según las especificaciones de tu entorno de desarrollo y las características de tu conjunto de datos.

## Entrenamiento y Personalización de la Red Neuronal

El proceso de entrenamiento y personalización de la red neuronal con Detectron2 implicó varios pasos clave, incluida la generación de etiquetas con Labelbox, la introducción de una etiqueta específica para paneles cortados y la selección de configuraciones basadas en experimentos exitosos.

### Uso de Labelbox para Generar Etiquetas

Labelbox se utilizó como herramienta principal para etiquetar las imágenes del conjunto de datos. Cada imagen fue cuidadosamente revisada y etiquetada para identificar la ubicación de los paneles solares. Este proceso fue fundamental para garantizar que el modelo pudiera aprender con precisión de los datos reales.

#### Etiqueta de Paneles Cortados

Se introdujo una etiqueta específica para "paneles cortados" en el conjunto de datos. Esta etiqueta fue crucial para enseñar al modelo a comprender mejor la escena y diferenciar entre paneles solares completos y aquellos parcialmente visibles o cortados por el borde de la imagen. Esto ayudó a mejorar significativamente la precisión del modelo, permitiéndole enfocarse solo en los paneles completamente visibles para la detección.

### Experimentos y Mejoras

Durante el proceso de entrenamiento, se llevaron a cabo varios experimentos para identificar las configuraciones y técnicas que ofrecían los mejores resultados. Algunas de las decisiones clave tomadas como resultado de estos experimentos incluyeron:

- **Ajuste de Hiperparámetros**: Se encontró que ciertos ajustes en los hiperparámetros, como la tasa de aprendizaje y el tamaño del lote, tenían un impacto significativo en la eficacia del modelo.
- **Aumento de Datos**: La implementación de técnicas de aumento de datos, como el volteo horizontal y el ajuste de brillo, resultó en una mejora de la robustez del modelo frente a variaciones en las imágenes de entrada.
- **Selección de Arquitectura**: Se experimentó con diferentes arquitecturas de Detectron2, y se seleccionó la que ofrecía el mejor equilibrio entre precisión y velocidad de procesamiento para nuestras necesidades específicas.

Estas decisiones, basadas en los resultados de los experimentos, fueron fundamentales para afinar el modelo y lograr un rendimiento óptimo en la tarea de detección de paneles solares.

Con estos pasos, se logró desarrollar un modelo altamente eficaz y personalizado para la detección de paneles solares en imágenes aéreas, capaz de comprender de manera intuitiva la escena y focalizarse en los elementos de interés.

## Detección y Análisis

Una vez el modelo de Detectron2 ha sido entrenado y personalizado, el siguiente paso es utilizarlo para la detección de objetos en nuevas imágenes. Este proceso implica cargar el modelo, procesar las imágenes de entrada y analizar los resultados obtenidos.

### Proceso de Detección

- **Carga del Modelo**: El modelo entrenado se carga en el entorno de ejecución.
- **Procesamiento de Imágenes**: Las imágenes capturadas por drones son procesadas por el modelo, identificando la presencia de paneles solares.
- **Interpretación de Resultados**: Los resultados incluyen la ubicación de cada panel detectado, junto con una puntuación de confianza para cada detección.

La precisión de la detección se evalúa utilizando métricas estándar, como el IoU (Intersección sobre la Unión), para asegurar que el modelo es capaz de identificar correctamente los paneles solares en diversas condiciones de iluminación y ángulos de visión.

## Resultados Destacables

A lo largo de la evaluación del modelo, se han obtenido resultados notables que demuestran la eficacia de Detectron2 para la tarea de detección de paneles solares. Algunas imágenes de ejemplo muestran paneles solares detectados con alta precisión, resaltando el potencial de esta tecnología para automatizar el monitoreo de instalaciones solares a gran escala.

## Conclusión y Usos Futuros

La implementación de Detectron2 para la detección de paneles solares en imágenes aéreas ha demostrado ser una herramienta poderosa, ofreciendo una base sólida para futuras aplicaciones en el mantenimiento y monitoreo de granjas fotovoltaicas.

### Aplicaciones Futuras

- **Detección de Fallos en Paneles Solares**: Utilizando técnicas adicionales, como el algoritmo de líneas de Hough, el sistema puede ser extendido para detectar automáticamente fallos en las celdas de los paneles solares.
- **Localización Geográfica de Paneles**: La integración de técnicas de localización permitirá situar geográficamente cada panel detectado dentro de la granja fotovoltaica, facilitando el envío de técnicos para su reparación basado en la información precisa de su ubicación.
- **Optimización de Rutas para Drones**: Conociendo la posición y el avance del drone, es posible optimizar las rutas de vuelo para maximizar la eficiencia del monitoreo y la detección.

Este proyecto sienta las bases para explorar estas y otras aplicaciones, aprovechando la potencia de Detectron2 y las técnicas de visión por computadora para mejorar la gestión y el mantenimiento de infraestructuras solares.

