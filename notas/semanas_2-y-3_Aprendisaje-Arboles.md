Notas semana 2 y semana 3: Aprendizaje supervisado y arboles.

* **Aprendizaje Automático (Machine Learning)**: En lugar de programar explícitamente cada tarea, el aprendizaje automático permite a las computadoras aprender de los datos. Esto es especialmente útil en problemas complejos donde las reglas son difíciles de definir o cambian constantemente.

* **Generalización**: Es la capacidad de un modelo de aprendizaje automático de desempeñarse bien en datos no vistos.
  
  * **Error en muestra (Ein)**: Mide el error del modelo en los datos de entrenamiento. La fórmula para calcularlo es:
    
    `Ein = (1/N) * Σ(e(y(i), ŷ(i)))`, donde `N` es el número de muestras, `y(i)` es el valor real y `ŷ(i)` es el valor predicho.
  
  * **Error fuera de muestra (Eout)**: Mide el error del modelo en datos no vistos. Se define como:
    
    `Eout = Ex∈X [e(y, ŷ)]`.
  
  * **Condiciones para la generalización**: Para que el aprendizaje sea efectivo, **`Ein` debe ser cercano a 0** y **`Ein` debe ser similar a `Eout`**.

* **Método del vecino más próximo**: Un método no paramétrico que guarda todos los datos de entrenamiento y clasifica nuevos puntos basándose en la clase del dato más cercano en el conjunto de entrenamiento.

* **Árboles de Decisión**: Modelos que dividen recursivamente el espacio de los datos basándose en los valores de los atributos para predecir una variable objetivo.
  
  * **Entropía (H(Y))**: Mide la incertidumbre de una variable aleatoria Y. Se utiliza para determinar la mejor división en cada nodo del árbol. Una entropía alta indica mayor incertidumbre, mientras que una entropía baja indica menor incertidumbre.
    
    `H(Y) = - Σ P(y) log2 P(y)`.
  
  * **Ganancia de Información (IG)**: Mide la reducción en la entropía después de dividir un conjunto de datos en función de un atributo. Se utiliza para seleccionar el atributo más informativo para la división.
    
    `IG(X) = H(Y) – H(Y|X)`.
  
  * **Entropía Condicional H(Y|X)**: Mide la incertidumbre restante de una variable Y dado que se conoce el valor de otra variable X.
    
    `H(Y|X) = - Σ P(x) Σ P(y|x) log2 P(y|x)`
  
  * **Sobrecogimiento (Overfitting)**: Los árboles de decisión tienden a sobreajustarse a los datos de entrenamiento, lo que lleva a un mal rendimiento en datos no vistos. Para evitar esto, se utilizan técnicas como la poda, establecer una profundidad fija o un número mínimo de muestras por hoja.

* **Ensamble (Ensemble)**: Combina múltiples modelos para mejorar la precisión y reducir la varianza.
  
  * **Bagging (Bootstrap Aggregation)**: Crea múltiples conjuntos de entrenamiento mediante el muestreo con reemplazo del conjunto de datos original. Luego, entrena un modelo diferente en cada conjunto y combina sus predicciones.
  * **Bosques Aleatorios (Random Forests)**: Un método de ensamble específicamente diseñado para árboles de decisión. Introduce aleatoriedad tanto en el muestreo de datos (bagging) como en la selección de atributos en cada nodo.

* **Generalización PAC (Probably Approximately Correct)**: Un marco teórico para entender la generalización en el aprendizaje supervisado.
  
  * **Desigualdad de Hoeffding**: Proporciona una cota superior en la probabilidad de que la diferencia entre el error en muestra y el error fuera de muestra sea mayor que un valor dado.
  * **Dimensión VC**: Una medida de la complejidad de un modelo que indica su capacidad para ajustarse a diferentes conjuntos de datos. Una dimensión VC más alta implica una mayor complejidad y, por lo tanto, un mayor riesgo de sobreajuste.

* **Scikit-learn**: Una biblioteca de Python que ofrece herramientas eficientes para el aprendizaje automático, incluyendo modelos, algoritmos y funciones de evaluación. Es compatible con otras bibliotecas como NumPy y Matplotlib.
