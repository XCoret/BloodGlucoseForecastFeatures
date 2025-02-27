# Influencia de variables adicionales en la predicción de niveles de glucosa

[Xavi Coret Mayoral](https://xcoret.github.io/portfolio/)

Universidad Internacional de la Rioja [UNIR](https://unir.net)


## Resumen
La diabetes mellitus afecta a millones de personas y requiere un monitoreo continuo de la glucosa para prevenir complicaciones. La predicción precisa de los niveles de glucosa es crucial para la dosificación de insulina y la gestión del estilo de vida de los pacientes. Este estudio analiza la influencia de diferentes conjuntos de variables utilizadas en tres modelos de redes neuronales LSTM para predecir los niveles de glucosa en sangre en pacientes con Diabetes Tipo 1. Con la incorporación de variables adicionales las predicciones tienden a mejorar, especialmente cuando están relacionadas con la fluctuación de los niveles de glucosa. Sin embargo, la inclusión de variables aumenta la complejidad computacional, resultando en un aumento de aproximadamente el 30% en los tiempos de entrenamiento. Este estudio resalta la importancia de encontrar un equilibrio entre la inclusión de variables adicionales y la viabilidad práctica para aplicar modelos predictivos de manera exitosa en escenarios del mundo real.

**Palabras clave:** `Diabetes Mellitus`, `Predicción de Glucosa`, `Selección de Características`, `Memoria a Corto y Largo Plazo (LSTM)`

### I. INTRODUCCIÓN
La diabetes mellitus afecta a millones de personas en todo el mundo y requiere un monitoreo continuo de la glucosa para prevenir complicaciones [1]. La diabetes tipo 1 se caracteriza, además, por la necesidad de que los pacientes reciban administración de insulina, ya sea mediante inyecciones o mediante una bomba de insulina. La investigación médica y la Inteligencia Artificial, en particular el Aprendizaje Automático, trabajan en conjunto para lograr predicciones precisas y confiables del nivel de glucosa. Esto aporta mejoras significativas en la calidad de vida de los pacientes con diabetes, ya que les permite planificar mejor sus actividades diarias y tomar decisiones más informadas sobre su salud. 

Este estudio tiene como objetivo llevar a cabo un análisis del efecto que la inclusión de variables adicionales tiene en las predicciones de los niveles de glucosa. Para lograrlo, se procede a entrenar diversos modelos de redes neuronales recurrentes LSTM y se efectúan predicciones empleando diferentes conjuntos de variables en distintos escenarios. El propósito es determinar si la incorporación de estas variables resulta en un impacto positivo, negativo o neutral en la precisión y fiabilidad de las predicciones realizadas.

### II. ESTADO DEL ARTE
En la actualidad, se han llevado a cabo numerosas investigaciones para predecir los niveles de glucosa en sangre, utilizando gran variedad paradigmas de la Inteligencia Artificial y Aprendizaje Profundo [2], la mayoría de los estudios indicaron que las Redes Neuronales Profundas y la Máquina de Vectores de Soporte (SVM)[3,4,5] consiguen ofrecer resultados muy precisos. Estas últimas han sido utilizadas en problemas de regresión combinadas con modelos fisiológicos para predecir los niveles de glucosa en sangre a partir de características como la hora del día, la actividad del paciente y la ingesta de insulina para realizar predicciones en tiempo real [6] la simplicidad, precisión y desempeño en tiempo real de este enfoque ha permitido la aplicación de este en dispositivos móviles [7]. 

Con la aparición de las redes neuronales, enfoques como las Redes Neuronales Convolucionales (CNN), que permiten procesar datos con topología de cuadrícula como imágenes y series temporales [8,9] como por ejemplo GluNet [10] y las Redes Neuronales Recurrentes (RNN)[11,12] y específicamente las Redes Neuronales Recurrentes de memoria a corto y largo plazo (LSTM)[13,14], las cuales tienen la capacidad de aprender patrones en datos distribuidos en forma de series temporales, han demostrado obtener resultados competitivos en comparación con las SVM [15,16].

El progreso tecnológico actual está impulsando un rápido desarrollo en este campo, permitiendo la implementación efectiva de métodos previamente limitados por recursos computacionales. Estas técnicas están demostrando ser prometedoras en la gestión de la diabetes al mejorar la precisión de las predicciones y personalizar la atención médica. Un ejemplo de ello es el el Desafío de Predicción de Niveles de Glucosa en Sangre, BGLP [17,18] donde investigadores en inteligencia artificial colaboraron para mejorar la predicción de glucosa en sangre con enfoques de aprendizaje automático en una competencia conjunta donde se presentaron propuestas innovadoras.

Un ejemplo fue una arquitectura novedosa propuesta por los ganadores del desafío [19] que empleaba una red neuronal recurrente para predecir gradualmente en etapas, mejorando el rendimiento y alcanzando un error promedio de 18.2 mg/dL en la predicción de glucosa para 30 minutos. Otra estrategia innovadora [20] se centró en transferir conocimiento entre modelos entrenados en diferentes conjuntos de datos mediante transferencia de aprendizaje de modo que mostró que usar un modelo preentrenado en datos de monitores de glucosa para predecir en el conjunto de datos OhioT1DM ofreció resultados comparables, con errores cuadráticos medios de 19.21 y 31.77 mg/dl para horizontes de 30 y 60 minutos.
El tercer clasificado de la competición adoptó una arquitectura modificada de Red Generativa Adversarial (GAN), combinando una red neuronal recurrente generadora y una convolucional discriminatoria para predecir glucosa en sangre [21]. Este enfoque demostró su prometedor rendimiento en métricas clave y relevancia clínica, como la rejilla de error de Clarke [22], respaldando su eficacia en la predicción de glucosa. 

La actualidad de la investigación en la predicción de niveles de glucosa en sangre está caracterizada por una diversidad de enfoques metodológicos avanzados que se nutren del progreso tecnológico. Estas estrategias no solo elevan la precisión de las predicciones, sino que también abren nuevas perspectivas para la personalización de la atención médica y la gestión efectiva de la diabetes. La selección de características relevantes sigue teniendo un papel importante para lograr una alta precisión y confianza en los modelos de predicción. Algunas de las características más utilizadas incluyen los niveles de glucosa anteriores, la variabilidad de los niveles de glucosa, la hora del día, la actividad física y la ingesta de alimentos. La identificación de las características más influyentes sigue siendo objeto de investigación activa.

### III. OBJETIVOS Y METODOLOGÍA
El objetivo general de este trabajo es evaluar el impacto de utilizar variables adicionales relacionadas con las mediciones de glucosa, la fecha y la hora de medición, en la predicción de los niveles de glucosa en pacientes con diabetes tipo 1. Determinando si la inclusión de variables adicionales inferidas a partir de estas variables utilizadas inicialmente mejora, empeora o no afecta la exactitud y coherencia de las predicciones. 

Este objetivo se pretende conseguir mediante el conseguimiento de objetivos específicos como: Estudiar el contexto y estado del arte de las técnicas y modelos utilizados en este ámbito; realizar un análisis exploratorio de los datos; implementar los modelos de predicción utilizando tanto las variables originales como las adicionales inferidas y finalmente comparar los resultados obtenidos para evaluar el impacto del uso de variables adicionales.

La metodología definida a seguir durante el desarrollo de este trabajo consiste en una serie de pasos establecidos para cumplir con los objetivos específicos y así conseguir cumplir también con el objetivo general de este trabajo. A continuación, se describen los pasos de esta metodología:
1.	Investigar acerca del estado del arte. Se realizó una investigación exhaustiva sobre el estado del arte en la predicción de niveles de glucosa en pacientes diabéticos. Esto implicó analizar numerosos artículos científicos, tesis doctorales y libros de referencia para comprender las técnicas y modelos utilizados. Esta investigación orientó la elección de la arquitectura y enfoque del estudio.
2.	Análisis exploratorio de los datos. Se ha empleado Python, un lenguaje común en Inteligencia Artificial, junto con librerías como Pandas y Numpy para procesar los archivos y los datos. Esto ha facilitado el procesamiento y ha permitido obtener información estadística y contextual. El objetivo ha sido identificar valores faltantes, discontinuidades y comprender los rangos de cada variable. De esta manera, se ha formado una idea general de los datos disponibles, lo que ha ayudado a planear la estrategia para extraer y utilizar variables adicionales en el entrenamiento y la evaluación de los modelos en la comparación de soluciones.
3.	Extracción de variables adicionales. Se ha decidido qué variables se pueden extraer de los datos originales, y se ha argumentado su posible utilidad e impacto en las predicciones que realizan los modelos. Estas variables se han añadido al conjunto de datos utilizado.
4.	Creación de series temporales. Se han organizado los datos de manera que se formen conjuntos de datos dispuestos en series temporales. Estas series temporales han servido para abastecer posteriormente a los modelos de predicción implementados. Se ha determinado el número de elementos que formarán cada serie temporal, así como el lapso que estas abarcarán.
5.	Segmentación del conjunto de datos. El quinto paso ha consistido en la creación de los conjuntos necesarios para entrenar una red neuronal y evaluar su rendimiento. Estos han sido el conjunto de entrenamiento, utilizado para que el modelo haya aprendido patrones de los datos, el conjunto de validación, utilizado para haber evaluado el modelo y durante el entrenamiento para haber mejorado su rendimiento, y el conjunto de prueba utilizado para haber probado la eficacia real del modelo, ya que ha consistido en ejemplos nuevos para el modelo que nunca antes ha visto. Esta segmentación del conjunto de datos se ha realizado a partir de funcionalidades de la librería de Python Scikit-Learn.
6.	Implementación de los modelos de predicción. En esta fase se han definido e implementado las arquitecturas de modelos de redes neuronales que han formado cada modelo. Para ello se han utilizado los “frameworks” de Keras y Tensorflow, los cuales han ofrecido recursos para la creación, entrenamiento y evaluación de redes neuronales de una forma más amigable para los programadores.
7.	Definición de los casos de prueba. Para poder realizar la comparación de soluciones, se han definido distintos casos que han sido definidos por las variables que se han utilizado en cada uno.
8.	Entrenamiento y obtención de resultados. Se ha procedido al entrenamiento y evaluación de los modelos implementados para cada caso de prueba definido y se han registrado los resultados para su posterior análisis. El entrenamiento de los modelos de predicción se ha realizado con GPU mediante la tarjeta gráfica NVIDIA GeForce GTX 1650 [23].
El código implementado para el desarrollo de este trabajo puede ser consultado en el repositorio público dedicado [24].

> TABLA I. CASOS DE PRUEBA DEFINIDOS

|Caso|Variables|
|:-|:-|
|Caso1 (C1)|Measurement|
|Caso2 (C2)|Measurement, Month, Day|
|Caso3 (C3)|Measurement, Weekday|
|Caso4 (C4)|Measurement, Hour, Minute|
|Caso5 (C5)|Measurement, Daytime|
|Caso6 (C6)|Measurement, Trend, Diagnostic|
|Caso7 (C7)|Measurement, Difference|
|Caso8 (C8)|Measurement, Month, Day, Weekday, Daytime, Trend, Diagnostic, Difference|

La Tabla I muestra las variables utilizadas en cada caso de prueba.

### IV. CONTRIBUCIÓN
El presente trabajo tiene como propósito brindar información valiosa para la optimización de modelos de predicción en el ámbito médico. Esto se logra al analizar el impacto que puede surgir al emplear diversos conjuntos de variables adicionales durante el entrenamiento y la realización de predicciones en estos modelos. De esta manera, se contribuye a obtener una comprensión más precisa sobre los beneficios o perjuicios derivados de la incorporación de variables adicionales. Estos beneficios abarcan desde la mejora de la precisión hasta la optimización del modelo y la comprensión del fenómeno estudiado. Todo ello respalda la toma de decisiones fundamentadas y la construcción de modelos más efectivos y confiables.

### V. EVALUACIÓN Y RESULTADOS 
Se han empleado dos enfoques para evaluar los resultados de los experimentos basados en los datos disponibles.
#### Evaluación de cada modelo
El primer enfoque ha implicado analizar el promedio de los resultados de cada modelo, lo que ha permitido obtener una comprensión más clara acerca de qué modelo ha exhibido un rendimiento superior. Esta información ha resultado útil para determinar si la utilización de diferentes conjuntos de variables puede haber tenido un impacto positivo o negativo dependiendo del modelo.

> TABLA II. MEDIA DE LAS MÉTRICAS PARA CADA MODELO

|Métrica|Modelo1|Modelo2|Modelo3|
|:-|:-|:-|:-|
|RMSE|0,41476433|12,6296951|4,39244588|
|R^2|0,99993964|0,93973385|0,99498558|
|Tiempo entrenamiento (seg.)|54,2037613|114,941446|102,911749|

La Tabla II muestra como el modelo M1 consigue los mejores resultados, en las tres métricas analizadas, seguido del modelo M3 y finalmente el modelo M2.

#### Evaluación de cada caso
El segundo enfoque se enfoca en examinar el promedio de los resultados de cada caso para cada modelo, lo que proporciona una visión más profunda sobre cómo la utilización de conjuntos específicos de variables influye en el rendimiento general de los diversos modelos.

> TABLA III. MEDIA DE LAS MÉTRICAS PARA CADA CASO

|Caso|RMSE|R^2|Tiempo entrenamiento (seg.)|
|:-|:-|:-|:-|
|C1|11,728|0,915|86,641|
|C2|5,459|0,990|85,835|
|C3|3,707|0,995|87,661|
|C4|4,416|0,992|88,295|
|C5|9,688|0,952|88,004|
|C6|4,151|0,993|88,397|
|C7|2,611|0,998|88,750|
|C8|4,738|0,991|111,902|

La Tabla III muestra como en el caso C7 se consigue el RMSE medio entre los tres modelos menor y también el mayor coeficiente de determinación.
También se denota como el caso C8 que utiliza todas las variables resulta un incremento del tiempo de entrenamiento significativo.

### VI. DISCUSIÓN
Los resultados obtenidos han sido analizados a partir de los dos enfoques definidos previamente. De este modo se obtiene una visión del impacto del uso de variables adicionales en cada modelo y también en cada caso. En este análisis se ha tenido en cuenta las métricas de RMSE, R^2, el tiempo de entrenamiento y los resultados obtenidos al aplicar la rejilla de error de Clarke a las predicciones realizadas.

#### Evaluación de cada modelo
El modelo más simple (M1) en el caso C1 (usando únicamente la variable del nivel de glucosa) logra los mejores resultados, demostrando su eficacia con un RMSE de 0.035, un valor de R^2 de 0.9999997 y un tiempo de entrenamiento de aproximadamente 47 segundos.
Sin embargo, esta aparente superioridad de un enfoque más simple se contradice cuando se observa el rendimiento del modelo M2 en el mismo caso, que presenta un rendimiento inferior en términos de RMSE y R^2, lo que resalta la importancia del modelo de aprendizaje profundo utilizado. Además, se nota que el rendimiento más destacado del modelo M1 se repite en el caso C6, donde se han incorporado variables adicionales, como “Trend” y “Diagnostic”, relacionadas con el estado general de la glucosa en sangre y su evolución. En este caso, el modelo M1 logra un RMSE de 0,12424 y un R^2 de 0,99999629 , con un tiempo de entrenamiento apenas 2 segundos mayor que en el mejor caso.  

La tendencia general en el análisis de rendimiento revela que el modelo M1 muestra la mayor exactitud y eficiencia en el tiempo de entrenamiento en la mayoría de los casos, seguido por M3, mientras que M2 presenta resultados menos satisfactorios. Además, es importante destacar que la inclusión de más variables no necesariamente mejora la precisión de los modelos. En algunos casos, como en el caso C3, resulta más efectivo utilizar un número limitado de variables, como “Measurement” y “Weekday”, en lugar de utilizar todas las variables disponibles, como se hizo en el caso C8. Esto resalta la importancia de seleccionar cuidadosamente las variables más relevantes para mejorar la capacidad predictiva.

En términos de métricas de exactitud y variabilidad, se observa que los modelos M1 y M3 obtienen bajos valores de RMSE y altos valores de R^2, denotando su capacidad para ajustarse y explicar la variabilidad de los datos. El modelo M2, aunque explica mucha variabilidad, presenta un RMSE más alto y un R^2 ligeramente inferior. En cuanto a la eficiencia temporal, M1 destaca por su rapidez en los entrenamientos debido en gran parte a la simplicidad de su arquitectura, mientras que M2 y M3 requieren más tiempo, especialmente en casos con más variables.


#### Evaluación de cada caso
El caso C7 muestra un menor RMSE promedio, lo que sugiere que las variables "Measurement" y "Difference" contribuyen a predicciones más precisas en comparación con otras combinaciones. Sin embargo, es importante destacar que en todos los casos, excepto el primero que no utilizó variables adicionales, el RMSE promedio se mantuvo por debajo de 10 mg/dl.

![Fig. 1.  Comparación de la media de RMSE por caso.](Output/Metrics/MediaRMSE.png)
> Fig. 1.  Comparación de la media de RMSE por caso.

Además, se en la figura 1 observa que el uso de un mayor número de variables no siempre mejora la precisión de los modelos. Por ejemplo, el caso 7 obtuvo mejores resultados con solo dos variables, mientras que el caso 8 tuvo un rendimiento inferior al utilizar las 8 variables disponibles. 

En todos los casos, representados en la figura 2, los modelos han logrado una explicación casi perfecta de la variabilidad de los datos, con una media del coeficiente de determinación (R^2) superior a 0,99. Notablemente, incluso en el caso 1 donde no se emplearon variables adicionales, los casos restantes mostraron un R^2 más alto. Esto sugiere que la inclusión de variables adicionales posiblemente mejoró la precisión de los modelos entrenados.

![Fig. 2.  Comparación de la media del coeficiente de determinación por caso.](Output/Metrics/MediaR2.png)
> Fig. 2.  Comparación de la media del coeficiente de determinación por caso.

En la figura 3 se puede observar como el modelo M1 completó todos sus entrenamientos en menos de un minuto, excepto en el caso 8, donde el tiempo de entrenamiento se extendió a un minuto y medio. Este último caso utilizó más de tres variables, lo que sugiere que un aumento en el número de variables puede ralentizar el proceso de entrenamiento de los modelos debido a la necesidad de procesar una mayor cantidad de datos. Este fenómeno está relacionado con el problema de la maldición de la dimensionalidad mencionado anteriormente.

Es importante destacar que el incremento en el tiempo de entrenamiento puede ser impracticable, especialmente si se utilizan herramientas menos potentes. Aunque en este estudio se empleó una GPU para el entrenamiento de los modelos, el uso de una CPU podría prolongar significativamente el tiempo de entrenamiento.

![Fig. 3.  Comparación de la media de la duración del entrenamiento por caso.](Output/Metrics/MediaTiempo.png)
> Fig. 3.  Comparación de la media de la duración del entrenamiento por caso.

Finalmente, el análisis de la rejilla de error de Clarke respalda la confianza en la capacidad de los modelos para realizar predicciones de niveles de glucosa seguros que no conllevan a diagnósticos erróneos, ya que, como se puede ver en la figura 4 la mayoría de las predicciones caen en las regiones A y B de la rejilla, indicando un buen ajuste y exactitud en las predicciones. Estos hallazgos subrayan la importancia de la elección adecuada de variables y modelos en la construcción de modelos de predicción para problemas de este tipo.

![Fig. 4.  Media de predicciones por región en la rejilla de error de Clarke](Output/Metrics/MediaClarke.png)
> Fig. 4.  Media de predicciones por región en la rejilla de error de Clarke


### VII. CONCLUSIONES Y LÍNEAS DE TRABAJO FUTURO
#### Conclusiones
En este trabajo se ha evaluado el impacto del uso de variables adicionales en la predicción de los niveles de glucosa en pacientes con diabetes tipo 1. 
Para ello, se ha realizado un estudio del conjunto de datos disponible inicialmente, el cual consistía en mediciones de los niveles de glucosa en sangre en mg/dl, junto con la fecha y la hora de dichas mediciones. A partir de estas tres variables iniciales, se extrajeron variables adicionales relacionadas con la fecha y la hora de la medición, con el propósito de comprender si los niveles de glucosa seguían algún patrón predecible según el día de la semana o la hora del día en que se realizaron las mediciones, entre otros factores, y también variables relacionadas con el nivel de glucosa en sangre para entender cómo varía entre una medición y otra, y si esto puede mejorar las predicciones de los niveles de glucosa.

Aunque se exploraron diferentes enfoques comúnmente utilizados para abordar problemas de predicción, como las máquinas de vectores de soporte (SVM) y las redes neuronales convolucionales (CNN), finalmente se optó por utilizar redes neuronales recurrentes LSTM debido a su capacidad para aprender patrones en conjuntos de datos distribuidos en series temporales, como las mediciones de glucosa contenidas en el conjunto de datos disponible.

Se crearon tres modelos de redes neuronales LSTM diferentes que varían en su complejidad estructural. Cada modelo realiza más operaciones sobre los datos que el anterior y, por lo tanto, conlleva un mayor costo computacional. De este modo, el primer modelo es el más simple, con una sola capa LSTM y dos capas densas. El segundo es más complejo, con dos capas LSTM, la primera de las cuales genera secuencias completas como salida para luego ser utilizadas en la segunda capa, junto con capas de “dropout” y normalización por lotes. El tercer modelo es el más robusto y profundo, con múltiples capas densas y técnicas de regularización para evitar el sobreajuste.

Cada uno de estos tres modelos se sometió a 8 casos diferentes definidos por el uso de distintos conjuntos de variables, desde el uso exclusivo del nivel de glucosa en sangre hasta el uso de todas las variables adicionales inferidas. Esto permitió obtener resultados que se pudieron comparar y analizar para determinar el impacto del uso de variables adicionales en la predicción del nivel de glucosa en pacientes con diabetes tipo 1.

Una vez obtenidos los resultados, se observó que el modelo más simple obtuvo los mejores resultados en todos los casos. Considerando la media de los resultados obtenidos por los tres modelos en cada caso, se pudo comprobar que el uso de variables adicionales tendió a mejorar la exactitud de las predicciones y la explicabilidad de los datos. Sin embargo, el uso de un mayor número de variables adicionales también aumentó el tiempo de entrenamiento de los modelos debido al incremento en el costo computacional.

Finalmente, se observó que, en los diferentes casos de prueba realizados, las variables que tuvieron más influencia a la hora de realizar predicciones precisas y con mayor capacidad para explicar los datos fueron aquellas utilizadas en el caso 7, las cuales proporcionaron información contextual sobre la fluctuación de los niveles de glucosa que permitió obtener un RMSE de 2,61 mg/dl, el bajo de entre todos los casos. Se trata de la variable “Difference,” que representó cuántos miligramos por decilitro varió la medición del nivel de glucosa en un momento dado en comparación con la medición de glucosa realizada 15 minutos antes, y la variable “Trend” que indicó si la fluctuación de la glucosa en sangre siguió una tendencia positiva, negativa o se mantuvo constante en ese momento.

#### Líneas de trabajo futuro
Debido al tiempo limitado para llevar a cabo este estudio, algunas líneas de investigación no se pudieron explorar completamente, lo que abre oportunidades para futuras investigaciones.

Una de las líneas de investigación prometedoras para el futuro es realizar un análisis exhaustivo de las combinaciones de variables que podrían tener un mayor impacto en la precisión y eficacia de los modelos de predicción de los niveles de glucosa en sangre. Este análisis permitiría determinar qué variables son realmente relevantes y cuáles podrían ser innecesarias para la tarea de predicción.

Otra línea interesante para futuras investigaciones sería proponer un caso de uso para completar un conjunto de datos con valores faltantes entre registros, utilizando las predicciones obtenidas. En el presente trabajo, se excluyeron los registros cuya distancia temporal era mayor a 15 minutos respecto al siguiente registro. Sin embargo, se podría explorar la posibilidad de predecir el valor de glucosa en sangre para reducir el número de valores faltantes en el conjunto de datos.

Ambas líneas de trabajo futuro tienen el potencial de mejorar la comprensión y la precisión de los modelos de predicción de glucosa en sangre, lo que contribuiría significativamente a la investigación en esta área y a la aplicación de estos modelos en situaciones prácticas 

### VIII. REFERENCIAS

[1]	Global report on diabetes. 2016. Accessed: Apr. 16, 2023. [Online].Available: https://www.who.int/publications/i/item/9789241565257.

[2]	J. Chaki, S. Thillai Ganesh, S. K. Cidham, and S. Ananda Theertan, “Machine learning and artificial intelligence based Diabetes Mellitus detection and self-management: A systematic review,” Journal of King Saud University - Computer and Information Sciences, vol. 34, no. 6, pp. 3204–3225, Jun. 2022, doi: 10.1016/j.jksuci.2020.06.013.

[3]	B. E. Boser, I. M. Guyon, and V. N. Vapnik, “A training algorithm for optimal margin classifiers,” in Proceedings of the fifth annual workshop on Computational learning theory, New York, NY, USA: ACM, Jul. 1992, pp. 144–152. doi: 10.1145/130385.130401.

[4]	G. James, D. Witten, T. Hastie, and R. Tibshirani, “An Introduction to Statistical Learning with Applications in R Second Edition,” 2021. Accessed: May 14, 2023. [Online]. Available: https://hastie.su.domains/ISLR^2/ISLRv2_website.pdf

[5]	T. Hastie, R. Tibshirani, and J. Friedman, “Springer Series in Statistics The Elements of Statistical Learning Data Mining, Inference, and Prediction.”

[6]	R. Bunescu, N. Struble, C. Marling, J. Shubrook, and F. Schwartz, “Blood Glucose Level Prediction Using Physiological Models and Support Vector Regression,” in 2013 12th International Conference on Machine Learning and Applications, IEEE, Dec. 2013, pp. 135–140. doi: 10.1109/ICMLA.2013.30.

[7]	M. P. Reymann, E. Dorschky, B. H. Groh, C. Martindale, P. Blank, and B. M. Eskofier, Blood Glucose Level Prediction based on Support Vector Regression using Mobile Platforms *. 2016. doi: 10.0/Linux-x86_64.

[8]	Y. LeCun et al., “Backpropagation Applied to Handwritten Zip Code Recognition,” Neural Comput, vol. 1, no. 4, pp. 541–551, Dec. 1989, doi: 10.1162/neco.1989.1.4.541.

[9]	K. Li, J. Daniels, C. Liu, P. Herrero, and P. Georgiou, “Convolutional Recurrent Neural Networks for Glucose Prediction,” IEEE J Biomed Health Inform, vol. 24, no. 2, pp. 603–613, Feb. 2020, doi: 10.1109/JBHI.2019.2908488.

[10]	K. Li, C. Liu, T. Zhu, P. Herrero, and P. Georgiou, “GluNet: A Deep Learning Framework for Accurate Glucose Forecasting.,” IEEE J Biomed Health Inform, vol. 24, no. 2, pp. 414–423, Feb. 2020, doi: 10.1109/JBHI.2019.2931842.

[11]	J. L. Elman, “Finding Structure in Time,” Cogn Sci, vol. 14, no. 2, pp. 179–211, Mar. 1990, doi: 10.1207/s15516709cog1402_1.

[12]	Fei-Fei Li, Justin Johnson, and Serena Yeung, “Lecture 10: Recurrent Neural Networks.” 2017. Accessed: Jun. 19, 2023. [Online]. Available: http://cs231n.stanford.edu/slides/2017/cs231n_2017_lecture10.pdf

[13]	S. Hochreiter and J. Schmidhuber, “Long Short-Term Memory,” Neural Comput, vol. 9, no. 8, pp. 1735–1780, Nov. 1997, doi: 10.1162/neco.1997.9.8.1735.

[14]	Christopher Olah, “Understanding LSTM Networks,” Aug. 27, 2015. http://colah.github.io/posts/2015-08-Understanding-LSTMs/ (accessed Jun. 19, 2023).

[15]	S. Mirshekarian, R. Bunescu, C. Marling, and F. Schwartz, “Using LSTMs to learn physiological models of blood glucose behavior,” in 2017 39th Annual International Conference of the IEEE Engineering in Medicine and Biology Society (EMBC), IEEE, Jul. 2017, pp. 2887–2891. doi: 10.1109/EMBC.2017.8037460.

[16]	Qingnan Sun, Marko V. Jankovic, Lia Bally, and Stavroula G. Mougiakakou, “Predicting Blood Glucose with an LSTM and Bi-LSTM Based Deep Neural Network,” 2018. doi: 10.48550/arXiv.1809.03817.

[17]	International Workshop on Knowledge Discovery in Healthcare Data, “Blood Glucose Level Prediction Challenge,” 2020. https://sites.google.com/view/kdh-2020/bglp-challenge?authuser=0 (accessed Jul. 28, 2023).

[18]	Knowledge Discovery in Healthcare Data, “The BGLP Challenge: Results, Papers, and Source Code ,” 2020, Accessed: Jul. 28, 2023. [Online]. Available: http://smarthealth.cs.ohio.edu/bglp/bglp-results.html

[19]	H. Rubin-Falcone, I. Fox, and J. Wiens, “Deep Residual Time-Series Forecasting: Application to Blood Glucose Prediction,” 2020. [Online]. Available: https://gitlab.eecs.umich.edu/mld3/deep-residual-time-series-forecasting

[20]	H. Hameed and S. Kleinberg, “Investigating potentials and pitfalls of knowledge distillation across datasets for blood glucose forecasting,” 2020. Accessed: Aug. 01, 2023. [Online]. Available: https://github.com/iupui-soic/bglp2G.

[21]	T. Zhu, X. Yao, K. Li, P. Herrero, and P. Georgiou, “Blood Glucose Prediction for Type 1 Diabetes Using Generative Adversarial Networks,” 2020.

[22]	W. L. Clarke, D. Cox, L. A. Gonder-Frederick, W. Carter, and S. L. Pohl, “Evaluating Clinical Accuracy of Systems for Self-Monitoring of Blood Glucose,” Diabetes Care, vol. 10, no. 5, pp. 622–628, Sep. 1987, doi: 10.2337/diacare.10.5.622

[23]	NVIDIA, “NVIDIA GeForce GTX 1650,” 2019. https://www.nvidia.com/en-us/geforce/graphics-cards/gtx-1650/ (accessed Jul. 26, 2023).

[24]	X. Coret, “Repositorio BloodGlucoseForecast,” 2023. https://github.com/XCoret/BloodGlucoseForecastFeatures (accessed Jul. 22, 2023).
