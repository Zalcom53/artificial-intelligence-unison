# Notas de Estudio: Regresión Lineal

## Introducción Histórica

- El descubrimiento de **Ceres** en 1801 por el astrónomo Piazzi sirvió como un ejemplo temprano de la aplicación de métodos similares a la regresión lineal.
- Piazzi hizo 19 observaciones de la ubicación de Ceres (tiempo, ascensión recta, declinación) antes de que fuera oscurecido por el sol.
- El problema era predecir cuándo y dónde se podría observar Ceres nuevamente.
- En septiembre de 1801, **Gauss** usó los datos de Piazzi para crear un modelo de la órbita de Ceres y hacer una predicción.
- El 7 de diciembre de 1801, Ceres fue localizado dentro de 1/2 grado de la predicción de Gauss, siendo mucho más preciso que otros astrónomos. Este evento es conocido como el "triunfo de Gauss" y a menudo se asocia con el desarrollo temprano del método de mínimos cuadrados.

## Marco de la Regresión Lineal (Método: Mínimos Cuadrados Lineal Regresión)

- Involucra **datos de entrenamiento** (ejemplos con entradas `x` y salidas `y`).
- Se utiliza un **algoritmo de aprendizaje** para encontrar un **predictor** (o función) `f`.
- El objetivo es que `f` pueda predecir la salida `y` para una nueva entrada `x`.  
  Por ejemplo, para una entrada de `3`, el predictor podría dar una salida de `2.71`.

## Decisiones de Diseño Clave

Para construir un modelo de regresión lineal, se deben tomar varias decisiones de diseño:

1. **¿Qué predictores son posibles?** (Clase de Hipótesis)  
2. **¿Qué tan bueno es un predictor?** (Función de Pérdida)  
3. **¿Cómo calculamos el mejor predictor?** (Algoritmo de Optimización)

---

### 1. Clase de Hipótesis

- Define el conjunto de predictores posibles.
- En la regresión lineal, la clase de hipótesis típicamente incluye **funciones lineales**.
- Estas funciones pueden ser representadas en **notación vectorial** como:  
  `fw(x) = w · φ(x)`
- `w` es el **vector de pesos** (ej. `w = [w1, w2]`)
- `φ(x)` es el **vector de características** (ej. `φ(x) = [1, x]`)
- La función `fw(x)` calcula un **puntaje**.  
  Por ejemplo, si `w = [1, 0.57]` y `φ(x) = [1, 3]`, entonces:  
  `fw(3) = [1, 0.57] · [1, 3] = 1 + (0.57 * 3) = 2.71`
- La clase de hipótesis `F` es el conjunto de todas las funciones `fw` para todos los posibles vectores `w` en ℝ² (para este ejemplo con dos pesos).

---

### 2. Función de Pérdida

- Mide qué tan bueno (o malo) es un predictor `fw` para un par `(x, y)` dado en los datos de entrenamiento.
- La **pérdida cuadrática (squared loss)** es una función de pérdida común.  
  Se define como:  
  `Loss(x, y, w) = (fw(x) - y)^2`
- La **pérdida de entrenamiento (TrainLoss)** para un vector `w` es el promedio de la pérdida cuadrática sobre todos los ejemplos `(x, y)` en los datos de entrenamiento `Dtrain`:  
  `TrainLoss(w) = (1 / |Dtrain|) * Σ_{(x,y)∈Dtrain} Loss(x, y, w)`
- Ejemplo con `w = [1, 0.57]` y datos `(1, 1), (2, 3), (4, 3)`:
  - `Loss(1, 1, w) = 0.32`
  - `Loss(2, 3, w) = 0.74`
  - `Loss(4, 3, w) = 0.08`

---

### 3. Algoritmo de Optimización

- El objetivo es **encontrar el vector de pesos `w` que minimice `TrainLoss(w)`**.
- El **Descenso de Gradiente (Gradient Descent)** es un algoritmo común para lograr esto.

#### Pasos del Descenso de Gradiente:

1. **Inicializar** el vector `w` (por ejemplo, con ceros).
2. Por cada iteración (o **época** `t`):
   - **Actualizar** `w` restando el gradiente de la pérdida de entrenamiento multiplicado por un **tamaño de paso (`η`)**.  
     Regla de actualización:  
     `w ← w - η * ∇TrainLoss(w)`
   - Esto mueve `w` en la dirección opuesta al gradiente, disminuyendo así la pérdida.

#### Cálculo del Gradiente (con pérdida cuadrática):

```
∇TrainLoss(w) = (1 / |Dtrain|) * Σ_{(x,y)∈Dtrain} 2 * (w · φ(x) - y) * φ(x)
```

- Aquí, `(w · φ(x) - y)` es la diferencia entre la predicción y el objetivo.

- El algoritmo continúa por un número fijo de épocas o hasta que la pérdida converja.

- En el ejemplo con 3 puntos de datos, después de 200 épocas con un tamaño de paso de `0.1`, el vector de pesos convergió a `[1, 0.57]`.  
  En ese punto, el gradiente era casi cero, indicando que se alcanzó un mínimo.