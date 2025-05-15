
# Marco de Clasificación Lineal

El marco de clasificación lineal en aprendizaje automático involucra varios componentes clave para construir un clasificador. Estos componentes son:

## 1. Datos de Entrenamiento (Dtrain)

Este es el conjunto de ejemplos que se utiliza para entrenar el clasificador. Cada ejemplo típicamente consiste en características de entrada (representadas como un vector `x`) y una etiqueta de destino (`y`).

**Ejemplo de datos de entrenamiento proporcionado:**

```
x1   x2   y
0    2    1
-2   0    1
1   -1   -1
```

## 2. Algoritmo de Aprendizaje

Este es el proceso que utiliza los datos de entrenamiento para encontrar el mejor clasificador.

## 3. Clasificador / Clase de Hipótesis (F)

Define qué tipos de clasificadores son posibles. En el contexto lineal, un clasificador binario general se define como:

```
fw(x) = sign(w · φ(x))
```

- `w` es un vector de pesos.
- `φ(x)` es una función que transforma el vector de entrada `x`. En los ejemplos dados, a menudo `φ(x)` es simplemente el propio vector de entrada `[x1, x2]`.
- La función `sign(z)` devuelve +1 si `z > 0`, -1 si `z < 0`, y 0 si `z = 0`.

**Clase de hipótesis:**

```
F = {fw : w ∈ ℝ²} si φ(x) = [x1, x2]
```

**Ejemplo de clasificador lineal:**

```
f(x) = sign([-0.6, 0.6] · [x1, x2])
```

## 4. Función de Pérdida (Loss function)

Mide qué tan bueno (o malo) es un clasificador `fw` para predecir la etiqueta correcta `y` para un ejemplo `x` o un conjunto de datos. Cuanto menor sea la pérdida, mejor será el clasificador.

### Conceptos relacionados con la pérdida:

- **Puntuación (Score):** Para un ejemplo `(x, y)`, la puntuación es `w · φ(x)`.
- **Margen (Margin):** Para un ejemplo `(x, y)`, el margen es `(w · φ(x))y`.

  - Un margen positivo significa que la predicción tiene el mismo signo que la etiqueta real `y`.
  - La pérdida generalmente disminuye a medida que el margen aumenta.

### Tipos de Funciones de Pérdida (para clasificación):

#### Pérdida Cero-Uno (Zero-one loss)

```math
Loss₀₋₁(x, y, w) = 1[fw(x) ≠ y] = 1[(w · φ(x))y ≤ 0]
```

La pérdida para el conjunto de entrenamiento (`TrainLoss`) es el promedio sobre todos los ejemplos.

#### Pérdida Hinge (Hinge loss)

```math
Loss_hinge(x, y, w) = max{1 - (w · φ(x))y, 0}
```

- Es 0 si el margen `(w · φ(x))y` es ≥ 1.
- Crece linealmente a medida que el margen disminuye por debajo de 1.

#### Pérdida Logística (Logistic loss)

```math
Loss_logistic(x, y, w) = log(1 + e^-(w·φ(x))y)
```

## 5. Algoritmo de Optimización

El objetivo es encontrar el vector de pesos `w` que minimice la pérdida total en los datos de entrenamiento (`TrainLoss(w)`).

### Descenso de Gradiente (Gradient Descent)

Un algoritmo común para minimizar la pérdida. Requiere calcular el gradiente de la función de pérdida con respecto a `w`.

- El gradiente de la pérdida cero-uno es **cero** en casi todas partes, lo que lo hace difícil de usar.
- Las pérdidas **hinge** y **logística** son alternativas convexas que permiten el uso eficiente de descenso de gradiente.

**Gradiente de la pérdida hinge** para un ejemplo `(x, y)`:

```
∇Loss = -φ(x)y  si 1 - (w · φ(x))y > 0  
∇Loss = 0       en caso contrario
```

El gradiente total es el **promedio** de los gradientes individuales.

---

## Resumen de Clasificación vs. Regresión

| Característica                | Regresión                    | Clasificación              |
|------------------------------|------------------------------|----------------------------|
| Predicción `fw(x)`           | puntuación (`score`)         | signo(puntuación)          |
| Relación con el target `y`   | residuo (`score - y`)        | margen (`score * y`)       |
| Funciones de Pérdida         | cuadrática, desviación absoluta | cero-uno, hinge, logística |
| Algoritmo                    | descenso de gradiente        | descenso de gradiente      |
