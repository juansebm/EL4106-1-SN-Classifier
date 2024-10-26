Título
# EL4106-1-SN-Classifier
# Autores:

## Juan Miño Abarca

## Eduardo Toledo Muñoz

### Descripción del problema a abordar, motivación.

En este proyecto se busca clasificar, de forma supervisada, supernovas utilizando un conjunto de
features pre-calculadas de sus series de tiempo astronómicas. Estas series en astronomía son conocidas como curvas de luz, las cuáles entregan información sobre el brillo estelar, su error y el día en que
ocurrió. Dicha información será extraída de la base de datos provista por el equipo del Automatic
Learning for the Rapid Classification of Events (ALeRCE) el cual es un broker de alertas astronómicas que recibe y procesa observaciones provenientes del survey astronómico Zwicky Transient Facility
(ZTF). La base de datos está compuesta por cerca de 2000 curvas de luz de supernovas (correspondientes a SNIa, SNIbc, SNII, SNIIb, SNIIn, SNSL) y posee un alto desbalance entre la cantidad de
curvas de luz de cada clase.


Se deberá inspeccionar, visualizar y preprocesar los datos. Una vez teniendo las características deberán trabajarlas y proponer un modelo supervisado que permite clasificarlas según su determinada
clase. Para cumplir con lo anterior, propongan una estrategia para entrenar y evaluar el desempeño
bajo un contexto de desbalance. Finalmente se deberá estudiar la relevancia que tiene cada característica en la clasificación final.


Adicionalmente, se deberá diseñar una red MLP para clasificación que posteriormente se utilizará
en el algoritmo Multi-classSVDD, Además se deberá investigar e implementar técnicas de proyección/reducción de dimensionalidad (UMAP y t-SNE) de los vectores de características para realizar
clustering. Por último, se deberá realizar una inspección visual sobre aquellas muestras que se alejen
de estos grupos.


### Objetivos del proyecto.

En el marco del curso, uno de los objetivos clave es utilizar técnicas avanzadas de aprendizaje
automático. Inicialmente, se procederá a inspeccionar y preprocesar las características de los datos,
lo que implica una revisión exhaustiva de las propiedades y parámetros relevantes. A partir de este
análisis, se diseñará y propondrá un modelo supervisado específico para la tarea de clasificación de
supernovas y se explicarán diversos métodos de evaluación sobre el diseño de la red. Este proceso
permitirá una correcta identificación de las diferentes clases de supernovas con base en los datos
observacionales disponibles.


Como parte del desarrollo, se implementará una red MLP (Perceptrón Multicapa) como base para
un modelo Multi-class SVDD (Support Vector Data Description) y así dar un enfoque robusto a la
clasificación y en segundo lugar, a la detección de anomalías.


Se emplearán técnicas de proyección y reducción de dimensionalidad como UMAP y t-SNE para
visualizar y entender las distribuciones de las diferentes clases de supernovas en espacios de baja
dimensión. Finalmente, los modelos serán entrenados y evaluados exhaustivamente para medir su
desempeño, buscando optimizar su capacidad predictiva y generalización.


### Base datos: Datos a usar (la disponibilidad de estos es esencial para el éxito del proyecto).

Los datos utilizados provienen de ALeRCE y consisten en aproximadamente 2000 curvas de luz de diferentes tipos de supernovas (SNIa, SNIbc, SNII, SNIIb, SNIIn y SNSL). Este conjunto de datos tiene un marcado desbalance de clases, lo cual debe abordarse en el preprocesamiento y modelado para asegurar una clasificación precisa, los datos estan alojados en la carpeta data.


### Pre-procesamiento de datos, selección y transformación de variables, normalización.

Para asegurar la calidad de los datos y su adecuación al modelo, se realiza un join entre los archivos de clases etiquetadas y las características de las curvas de luz. Se seleccionaron 29 características de entre las 178 disponibles, basándose en un ranking de importancia. Este paso de selección permite optimizar el procesamiento y mitigar el riesgo de sesgo. También se aplicaron técnicas de normalización y ponderación para balancear las clases durante el entrenamiento del modelo.

### Definición y justificación del tipo de algoritmo a usar.

Se empleó un modelo Balanced Random Forest, que utiliza el criterio de entropía para maximizar la ganancia de información. Con 500 árboles sin límite de profundidad, este modelo capta patrones complejos. Para garantizar que las clases minoritarias estén bien representadas, se implementó un esquema de ponderación de clases. Adicionalmente, una red MLP de tres capas que se usará en el modelo Multi-class SVDD, proporcionando una representación de los datos en un espacio latente y permitiendo una mejora en la clasificación y la detección de anomalías.


### Definición de salidas deseadas, función objetivo, principio de optimización a usar.

Las salidas deseadas consisten en una clasificación precisa de las supernovas en las subclases especificadas. La función objetivo utilizada es CrossEntropyLoss, que se adapta bien a problemas de clasificación multiclase y permite la ponderación de clases para abordar el desbalance. El modelo también utiliza un optimizador Adam con una tasa de aprendizaje de 1e-4 y decay para mitigar el sobreajuste.

### Criterio de detención del algoritmo, listado de parámetros por definir y/o ajustar.

El modelo de mlp que se utilizo para visualizacion se entrena hasta un máximo de 1000 épocas, con un monitoreo de precisión y reducción de la pérdida. Algunos parámetros críticos a ajustar incluyen el número de neuronas en cada capa de la MLP, el radio de la esfera en Multi-class SVDD y los valores de hiperparámetros del Random Forest (por ejemplo, min_samples_split y min_samples_leaf).




### Software: Definición del software a usar, definir qué aspectos se programarán y en qué lenguaje (p.ej. rutinas complementarias a un toolbox específico).

Se utilizó PyTorch para construir la red MLP y scikit-learn para la implementación de Balanced Random Forest y cálculo de ponderación de clases. Además, se programaron complementos en Python para el preprocesamiento de datos y visualización de resultados.


### Resultados esperados, medidas de desempeño a usar para evaluar los modelos, forma en que se presentarán los resultados (tablas y gráficos).

Esperamos lograr una precisión elevada y un rendimiento equilibrado en todas las clases. Las métricas de evaluación incluyen la matriz de confusión, precisión, recall y F1-score, diferenciados por clase. Se emplearán gráficos para visualizar la proyección de datos en el espacio latente y tablas para comparar el rendimiento de los modelos.


### Estimación de recursos computacionales, número y tiempo de simulaciones a realizar para completar los experimentos necesarios que cumplen los objetivos.

Se espera realizar simulaciones de entrenamiento de los modelos y sus variantes por un total aproximado de 3 minutos en una máquina con GPU. Cada iteración de Random Forest o de entrenamiento de la red MLP tarda entre 1 y 3 minutos, dependiendo del número de capas y ajustes realizados.


### Carta GANTT semanal de pasos a seguir para cumplir el objetivo del proyecto, en concordancia con el calendario del curso.

Semana 1-2: Preprocesamiento de datos y selección de características.


Semana 3-4: Implementación y ajuste del Balanced Random Forest.


Semana 5-6: Implementación de MLP y Multi-class SVDD.


Semana 7: Pruebas de dimensionalidad (UMAP, t-SNE).


Semana 8: Evaluación final y visualización de resultados.


### Referencias completas con autores, título, revista o libro, volumen, año, páginas. Debe existir al menos un artículo clave en revista IEEE.  (Buscar en bases de datos IEEE, Elsevier, etc).

[1] Sánchez-Sáez, P., et al. ’Alert Classification for the ALeRCE Broker System: The Light Curve
Classifier.’ arXiv preprint arXiv:2008.03311 (2020).


[2] Förster, F., et al. ’The Automatic Learning for the Rapid Classification of Events (ALeRCE)
Alert Broker.’ arXiv preprint arXiv:2008.03303 (2020)


[3] Glorot, Xavier, and Yoshua Bengio. ’Understanding the difficulty of training deep feedforward
neural networks.’ Proceedings of the Thirteenth International Conference on Artificial Intelligence
and Statistics. 2010.


[4] Pérez-Carrasco, Manuel, Guillermo Cabrera-Vives, Lorena Hernández-García, Francisco Forster,
Paula Sánchez-Sáez, Alejandra Muñoz Arancibia, Nicolás Astorga, Franz Bauer, Amelia Bayo,
Martina Cádiz-Leyton, and Marcio Catelan. "Multi-Class Deep SVDD: Anomaly Detection Approach in Astronomy with Distinct Inlier Categories..arXiv preprint arXiv:2308.05011 (2023).
https://arxiv.org/abs/2308.05011.



### Resultados preliminares. Se pide un grado de avance tal que exista una primera solución al problema propuesto. Los resultados encontrados no han de ser perfectos, pero si una solución al problema propuesto.

El modelo Balanced Random Forest mostró resultados prometedores en la clasificación inicial de supernovas, con un buen desempeño en clases mayoritarias y un aumento en precisión para clases minoritarias al aplicar ponderación de clases. La MLP para el Multi-class SVDD también logró representar los datos en el espacio latente y permitió una proyección efectiva de las clases.
