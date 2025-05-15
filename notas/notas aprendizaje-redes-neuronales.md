# Introducción y Motivación

- El objetivo es entrenar redes neuronales.
- Un método común para entrenar redes neuronales es el **descenso de gradiente estocástico** (*Stochastic Gradient Descent*).
- Este método requiere calcular el gradiente de la función de pérdida con respecto a los parámetros del modelo (como las matrices `V1`, `V2`, `V3` y el vector `w` en una red de cuatro capas, o `V` y `w` en una red de dos capas).
- Por ejemplo, para una red de cuatro capas en un problema de regresión con pérdida al cuadrado, la pérdida en un ejemplo `(x, y)` es:

  ```
  Loss(x, y, V1, V2, V3, w) = (w · ϕ(V3ϕ(V2ϕ(V1x))) − y)^2
  ```

- El descenso de gradiente implica actualizar los parámetros en la dirección opuesta al gradiente de la pérdida, usando una tasa de aprendizaje `η`. Por ejemplo:

  ```
  w ← w − η ∇w Loss(x, y, V1, V2, V3, w)
  ```

- Calcular estos gradientes "sin hacer trabajo manual" es el desafío.

---

# La Solución: Grafos de Computación y Retropropagación

- La solución general para calcular gradientes automáticamente es el **algoritmo de retropropagación**.
- La retropropagación se basa en los **grafos de computación**.

## Grafos de Computación

- Son **grafos dirigidos acíclicos**.
- El nodo raíz representa la **expresión matemática final** (la pérdida).
- Cada nodo representa **subexpresiones intermedias**.
- Ayudan a visualizar y entender los gradientes.

### Nodos Básicos y sus Gradientes Locales

Los grafos se construyen a partir de operaciones básicas. Aquí algunos ejemplos:

- **Suma** (`c = a + b`):  
  - ∂c/∂a = 1, ∂c/∂b = 1

- **Resta** (`c = a - b`):  
  - ∂c/∂a = 1, ∂c/∂b = -1

- **Multiplicación** (`c = a · b`):  
  - ∂c/∂a = b, ∂c/∂b = a

- **Cuadrado** (`c = a^2`):  
  - ∂c/∂a = 2a

- **Máximo** (`c = max(a, b)`):  
  - ∂c/∂a = 1 si a > b, 0 si a < b (indicador `1[a > b]`)  
  - ∂c/∂b = 1 si b > a, 0 si b < a (indicador `1[b > a]`)

- **Función Sigmoide** (`c = ϕ(a)`):  
  - ∂c/∂a = ϕ(a)(1 − ϕ(a))

### La Regla de la Cadena

Fundamental para calcular gradientes en grafos de computación. Si:

- `c = f(b)`  
- `b = g(a)`  
- Entonces:  
  - ∂c/∂a = (∂c/∂b) · (∂b/∂a)

Esto se extiende a caminos más largos en el grafo.

---

# El Algoritmo de Retropropagación

- Es un **algoritmo de propósito general** para calcular gradientes.
- Utilizado por librerías como **TensorFlow** y **PyTorch**.

## Propósitos

- Calcular gradientes automáticamente.
- Permitir una estructura **modular** para los cálculos de gradiente.

## Valores Clave

- **Forward (hacia adelante):**  
  - `fi` es el valor de la subexpresión representada por el nodo `i`.

- **Backward (hacia atrás):**  
  - `gi = ∂loss/∂fi` indica cuánto influye `fi` en la pérdida total.

## Pasos del Algoritmo

1. **Paso hacia adelante (Forward Pass):**  
   Calcular los valores `fi` desde las entradas hasta la salida (la pérdida).

2. **Paso hacia atrás (Backward Pass):**  
   Calcular los gradientes `gi` desde la raíz hasta las hojas, usando la regla de la cadena y los gradientes locales.

---

# Aplicaciones y Ejemplos en las Fuentes

- **Regresión con redes de cuatro capas:**  
  La pérdida es el error cuadrático entre la salida y el valor real.

- **Clasificación lineal con Hinge Loss:**  
  Pérdida: `max{1 − margen, 0}`  
  Donde: `margen = w · ϕ(x)y`  
  Se muestra el grafo correspondiente.

- **Redes neuronales de dos capas:**  
  Pérdida:

  ```
  Loss(x, y, V, w) = (w · ϕ(Vx) − y)^2
  ```

  Se presenta el grafo de computación y los gradientes `∇wLoss` y `∇VLoss`.  
  También se incluye un ejemplo numérico de cómo calcular `∇wLoss`.

---

# Notas sobre la Optimización de Redes Neuronales

- Minimizar `TrainLoss(V, w)` es un problema de **optimización no convexo**.
- A diferencia de los modelos lineales, donde la optimización suele ser convexa.
- Por tanto, entrenar redes neuronales es **difícil en principio**.

## Estrategias Complementarias

- **Inicialización cuidadosa:** Ruido aleatorio o preentrenamiento.
- **Sobreparametrización:** Usar más unidades ocultas de las necesarias.
- **Tasas de aprendizaje adaptativas:** Algoritmos como **AdaGrad**, **Adam**.
- Es crucial evitar el **desvanecimiento o explosión** de los gradientes.

---

# Resumen

- Los **grafos de computación** ayudan a visualizar y entender los gradientes.
- La **retropropagación** es el algoritmo de propósito general para calcularlos de manera eficiente.

