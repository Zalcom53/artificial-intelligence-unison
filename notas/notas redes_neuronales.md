# Machine Learning: Redes Neuronales

## Predictores Lineales
- Se definen como `fw(x) = w · φ(x)`, donde `φ(x)` es una representación simple del input, como `[1, x]` para un input unidimensional `x`.

## Predictores No Lineales
- Son más complejos que los lineales.
- Ejemplo de predictor no lineal (cuadrático): `fw(x) = w · φ(x)`, donde `φ(x)` podría ser `[1, x, x^2]`.
- **Las redes neuronales no lineales** son un tipo de predictor no lineal. Su forma general es:  
  `fw(x) = w · ψ(Vφ(x))`,  
  donde `φ(x)` es la representación del input, `V` y `w` son pesos, y `ψ` es una función de activación.

---

## Ejemplo Motivador: Predicción de Colisión de Coches

- **Input**: Posiciones de dos coches que se aproximan, `x = [x1, x2]`.
- **Output**:  
  - Seguro → `y = +1`  
  - Colisión → `y = -1`
- **Regla de Seguridad** (desconocida):  
  `y = sign(|x1 - x2| - 1)`
- **Datos de Ejemplo**:
  - `x = ?, y = +1`
  - `x = ?, y = +1`
  - `x = ?, y = -1`
  - `x = ?, y = -1`

---

## Descomponiendo el Problema

- El problema se puede dividir en subproblemas intermedios.

### Subproblema 1
- ¿Está el coche 1 muy a la derecha del coche 2?  
  `h1(x) = 1[x1 - x2 ≥ 1]`
- Notación vectorial:  
  `h1(x) = 1[[-1, +1, -1] · [1, x1, x2] ≥ 0]`

### Subproblema 2
- ¿Está el coche 2 muy a la derecha del coche 1?  
  `h2(x) = 1[x2 - x1 ≥ 1]`
- Notación vectorial:  
  `h2(x) = 1[[-1, -1, +1] · [1, x1, x2] ≥ 0]`

### Predicción Final
- Es seguro si al menos uno de los subproblemas es verdadero:  
  `f(x) = sign(h1(x) + h2(x))`
- Notación vectorial:  
  `f(x) = sign(w · h(x))`,  
  donde `h(x)` representa los resultados de `h1(x)` y `h2(x)`.

---

## Evitar Gradientes Cero

- **Problema**: El gradiente de funciones escalón como  
  `h1(x) = 1[v1 · φ(x) ≥ 0]`  
  es cero en casi todos los puntos → difícil aprendizaje.
- **Solución**: Reemplazar la función escalón con una **función de activación** `ψ(z)` con gradientes distintos de cero.

### Ejemplos de Funciones de Activación
- Umbral (Threshold): `1[z ≥ 0]` _(problemática)_
- Logística (Sigmoide): `1 / (1 + e^-z)`
- ReLU: `max(z, 0)`

- Subproblemas redefinidos:  
  `h1(x) = ψ(v1 · φ(x))`

---

## Redes Neuronales de Dos Capas

- Formalizan la idea de subproblemas intermedios.
- Capa intermedia:  
  `h(x) = ψ(Vφ(x))`
- Predictor final:  
  `fV,w(x) = sign(w · h(x))`
- `h(x)` = **representación de características aprendida**.
- Hipótesis: incluye todos los predictores posibles al variar `V` y `w`.

---

## Redes Neuronales Profundas (Deep Neural Networks)

- Añaden más capas entre input y output.

### Ejemplos de Profundidad
- **1 capa**: `score = w · φ(x)` → predictor lineal
- **2 capas**: `score = w · ψ(Vφ(x))`
- **3 capas**: `score = w · ψ(V2ψ(V1φ(x)))`

- Cada capa extra = **nivel de abstracción adicional**

### ¿Por qué la profundidad?
- Intuitivamente: múltiples niveles de abstracción
- Computacionalmente: múltiples pasos de procesamiento
- Empíricamente: funcionan muy bien
- Teoría: aún en desarrollo

---

## Resumen Clave

- Intuición principal: **descomponer el problema** en subproblemas intermedios paralelos.
- Redes profundas: **iteran esta descomposición** en múltiples capas.
- Hipótesis: incluye predictores para diferentes combinaciones de pesos `V`, `w`, etc.
- Próximo paso: aprender a **entrenar** estas redes (ajustar pesos).