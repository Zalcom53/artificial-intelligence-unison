## Árboles de Decisión

### Definición y Estructura
- Son hipótesis `f : X → Y`.
- Cada **nodo interno** prueba un atributo `xi`.
- Hay **una rama por cada posible valor** del atributo `xi = v`.
- Cada **hoja** asigna una clase `y`.

### Clasificación
- Para clasificar una entrada `x`, se **recorre el árbol desde la raíz hasta la hoja**, y se produce la salida `y` etiquetada en la hoja.

### Interpretación Humana
- Son interpretables por humanos.

## Espacio de Hipótesis

- Los árboles de decisión pueden **representar cualquier función** de los atributos de entrada.
- Para funciones Booleanas, el camino a la hoja da la fila de la tabla de verdad.
- Esto **podría requerir exponencialmente muchos nodos**.

## Aprendizaje de Árboles de Decisión

- Aprender el **árbol de decisión más simple (más pequeño) es un problema NP-completo** [Hyafil & Rivest ’76].
- Por lo tanto, se recurre a una **heurística voraz (greedy)**.
- La idea clave es **aprender árboles de forma voraz usando recursión**.
- El proceso comienza desde un árbol de decisión vacío.
- En cada paso, se **divide según el siguiente mejor atributo (característica)**.
- Luego, se **recurre** en los subconjuntos de datos resultantes.
- Se toma el conjunto de datos original y **se particiona** según el valor del atributo sobre el que se dividió.

## Selección de Atributos (Splitting)

- Para elegir un buen atributo para dividir, la idea es usar los conteos en las hojas para definir distribuciones de probabilidad y así **medir la incertidumbre**.
- Un buen split es aquel en el que estamos **más seguros sobre la clasificación después de la división**.
  - Una distribución determinista (todo verdadero o todo falso) es buena.
  - Una distribución uniforme es mala.

### Entropía (`H(Y)`)
- Es una medida de la incertidumbre de una variable aleatoria `Y`.
- **Más incertidumbre, más entropía**.
- Interpretación de la Teoría de la Información: `H(Y)` es el número esperado de bits necesarios para codificar un valor de `Y` extraído aleatoriamente (bajo el código más eficiente).
- **Alta entropía**: distribución parecida a la uniforme (valores menos predecibles).
- **Baja entropía**: distribución con picos y valles (valores más predecibles).
- Ejemplo de cálculo de entropía para un conjunto de datos.

### Entropía Condicional (`H(Y|X)`)
- Entropía de una variable aleatoria `Y` condicionada a una variable aleatoria `X`.
- Ejemplo de cálculo de entropía condicional.

### Ganancia de Información (`IG(X)`)
- Es la **disminución de la entropía (incertidumbre) después de dividir**.
- `IG(X) = H(Y) – H(Y|X)`
- Se prefiere un split con una ganancia de información mayor que 0.
- Para seleccionar el atributo, se puede usar la **ganancia de información**.

## Criterios de Parada (When to Stop)

- Se necesitan reglas para saber cuándo detener la recursión.

### Caso Base Uno
- No dividir un nodo si **todos los registros coincidentes tienen el mismo valor de salida**.

### Caso Base Dos
- No dividir un nodo si los puntos de datos son **idénticos en los atributos restantes**.

### Caso Base Tres (propuesta no recomendable)
- No dividir si **todos los atributos tienen poca ganancia de información**.
- Esto **no es una buena idea** (por ejemplo, en la función XOR).

## Sobreajuste (Overfitting)

- Los árboles de decisión **sobreajustan**.
- No tienen sesgo de aprendizaje; el error en entrenamiento es cero (si no hay ruido).
- Tienen **mucha varianza**.
- Se debe introducir algún **sesgo hacia árboles más simples**.
- Estrategias para árboles más simples:
  - **Profundidad fija**.
  - **Número mínimo de muestras por hoja**.
  - **Poda (pruning)** después de construir el árbol.
  - Usar **conjuntos (ensembles)** de diferentes árboles (como los bosques aleatorios).

## Manejo de Entradas con Valores Reales (Continuos)

- Para atributos de **valor real**, hay infinitos valores de split posibles.
- La idea de "una rama para cada valor numérico" no es útil.
- Se utilizan **splits por umbral**:
  - Una rama: `X < t`
  - Otra rama: `X ≥ t`

- Permite **splits repetidos en la misma variable** a lo largo de un camino.

- Aunque hay infinitos posibles valores `t`, **solo un número finito importa**:
  - Ordenar los datos según `X`: `{x1, ..., xm}`
  - Usar puntos `xi + (xi+1 – xi)/2`
  - Solo importan splits entre ejemplos de **diferentes clases**

### Cálculo de mejor umbral
- Ganancia de información para umbral `t`:
  - `H(Y|X:t) = p(X < t) H(Y|X < t) + p(X ≥ t) H(Y|X ≥ t)`
  - `IG(Y|X:t) = H(Y) - H(Y|X:t)`
  - `IG*(Y|X) = max_t IG(Y|X:t)`
- Se usa `IG*(Y|X)` para variables continuas.

## Métodos de Conjunto (Ensemble Methods)

- Permiten **reducir la varianza sin aumentar el sesgo**.
- **Averaging reduce la varianza**.
- Problema: solo se tiene un conjunto de entrenamiento.

### Bagging (Bootstrap Aggregation)
- Introducido por Leo Breiman (1994).
- **Muestras bootstrap repetidas** del conjunto de entrenamiento `D`.
- **Muestreo Bootstrap**: se crean conjuntos `D'` tomando `N` ejemplos con reemplazo.
- **Proceso**:
  - Crear `k` muestras bootstrap `D1 ... Dk`
  - Entrenar un clasificador distinto en cada `Di`
  - Clasificar una nueva instancia por **votación mayoritaria/promedio**

### Bosques Aleatorios (Random Forests)
- Método de conjunto diseñado para árboles de decisión.
- Introduce dos fuentes de aleatoriedad:
  - **Bagging**
  - **Vectores de entrada aleatorios**
- En cada nodo, el mejor split se elige de una **muestra aleatoria de `m` atributos**, no de todos.

## Conclusión sobre Árboles de Decisión

- Son una de las herramientas de Machine Learning **más populares**.
- Son **fáciles de entender, implementar y usar**.
- **Computacionalmente baratos** (para resolver heurísticamente).
- Utilizan **ganancia de información** para seleccionar atributos (ID3, C4.5, etc.).
- Se usan para **clasificación**, pero también para **regresión y estimación de densidad**.
- **¡Sobreactúan!**
- Se deben usar estrategias para encontrar árboles simples:
  - Profundidad fija / detención temprana
  - Poda
  - Uso de **conjuntos de árboles** (como bosques aleatorios)

