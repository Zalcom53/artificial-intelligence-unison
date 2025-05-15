# Notas de Estudio: Descenso de Gradiente Estocástico (SGD)

## Concepto General
El aprendizaje automático utiliza algoritmos como el descenso de gradiente para optimizar modelos ajustando los pesos (*w*) y minimizando una función de pérdida.

## Función de Pérdida de Entrenamiento (TrainLoss)
- **Definición**:  
  Ambos algoritmos (GD y SGD) minimizan la misma función `TrainLoss(w)`.  
  `TrainLoss(w) = (1 / |Dtrain|) * Σ_{(x,y) ∈ Dtrain} Loss(x, y, w)`  
  - `Dtrain`: Conjunto de entrenamiento  
  - `Loss(x, y, w)`: Función de pérdida para un ejemplo individual  

## Descenso de Gradiente (Gradient Descent - GD)
### Algoritmo Básico
1. Inicializar pesos: `w = [0, ..., 0]`  
2. Para cada iteración `t = 1, ..., T`:  
   - Calcular gradiente de `TrainLoss(w)`  
   - Actualizar pesos:  
     `w ← w - η * ∇w TrainLoss(w)`  
     *(η es el tamaño del paso, a veces implícito en las fuentes)*  

### Problema Principal
- **Costo computacional**: Cada iteración requiere procesar **todos** los ejemplos de entrenamiento, lo que es lento para grandes conjuntos de datos.

## Descenso de Gradiente Estocástico (SGD)
### Idea Clave
- **Actualizaciones estocásticas**:  
  La diferencia no está en la calidad de cada paso, sino en la **cantidad de pasos** posibles al ser más eficientes.  

### Algoritmo
1. Inicializar pesos: `w = [0, ..., 0]`  
2. Para cada iteración `t = 1, ..., T`:  
   - Para cada ejemplo `(x, y)` en `Dtrain`:  
     - Calcular gradiente de `Loss(x, y, w)` (pérdida individual)  
     - Actualizar pesos:  
       `w ← w - η * ∇w Loss(x, y, w)`  

## Comparación: GD vs. SGD
| **Aspecto**               | **GD**                          | **SGD**                          |
|---------------------------|---------------------------------|----------------------------------|
| **Actualización**         | Gradiente promedio de todo `Dtrain` | Gradiente de un ejemplo individual |
| **Costo por iteración**   | Alto (procesa todo el dataset)  | Bajo (procesa un ejemplo)        |
| **Velocidad de convergencia** | Lenta (menos actualizaciones) | Rápida (más actualizaciones)     |
| **Estabilidad**           | Más estable                     | Más ruidosa (varianza alta)      |

> **Frase clave**: *"No se trata de la calidad, se trata de la cantidad"* (SGD permite más actualizaciones).

## Tamaño del Paso (η)
### Definición
- Factor que escala el gradiente: `w ← w - η * ∇w Loss(x, y, w)`  

### Importancia
- **η pequeño**:  
  - Conservador y estable.  
  - Convergencia lenta.  
- **η grande**:  
  - Agresivo y rápido.  
  - Riesgo de inestabilidad.  

### Estrategias para η
1. **Constante**:  
   Ejemplo: `η = 0.1` (valor fijo).  
2. **Decreciente**:  
   Ejemplo: `η = 1 / √(número de actualizaciones)`.  

---
*Estas notas resumen los conceptos clave del Descenso de Gradiente Estocástico y su comparación con el Descenso de Gradiente tradicional.*# Notas de Estudio: Descenso de Gradiente Estocástico (SGD)

## Concepto General
El aprendizaje automático utiliza algoritmos como el descenso de gradiente para optimizar modelos ajustando los pesos (*w*) y minimizando una función de pérdida.

## Función de Pérdida de Entrenamiento (TrainLoss)
- **Definición**:  
  Ambos algoritmos (GD y SGD) minimizan la misma función `TrainLoss(w)`.  
  `TrainLoss(w) = (1 / |Dtrain|) * Σ_{(x,y) ∈ Dtrain} Loss(x, y, w)`  
  - `Dtrain`: Conjunto de entrenamiento  
  - `Loss(x, y, w)`: Función de pérdida para un ejemplo individual  

## Descenso de Gradiente (Gradient Descent - GD)
### Algoritmo Básico
1. Inicializar pesos: `w = [0, ..., 0]`  
2. Para cada iteración `t = 1, ..., T`:  
   - Calcular gradiente de `TrainLoss(w)`  
   - Actualizar pesos:  
     `w ← w - η * ∇w TrainLoss(w)`  
     *(η es el tamaño del paso, a veces implícito en las fuentes)*  

### Problema Principal
- **Costo computacional**: Cada iteración requiere procesar **todos** los ejemplos de entrenamiento, lo que es lento para grandes conjuntos de datos.

## Descenso de Gradiente Estocástico (SGD)
### Idea Clave
- **Actualizaciones estocásticas**:  
  La diferencia no está en la calidad de cada paso, sino en la **cantidad de pasos** posibles al ser más eficientes.  

### Algoritmo
1. Inicializar pesos: `w = [0, ..., 0]`  
2. Para cada iteración `t = 1, ..., T`:  
   - Para cada ejemplo `(x, y)` en `Dtrain`:  
     - Calcular gradiente de `Loss(x, y, w)` (pérdida individual)  
     - Actualizar pesos:  
       `w ← w - η * ∇w Loss(x, y, w)`  

## Comparación: GD vs. SGD
| **Aspecto**               | **GD**                          | **SGD**                          |
|---------------------------|---------------------------------|----------------------------------|
| **Actualización**         | Gradiente promedio de todo `Dtrain` | Gradiente de un ejemplo individual |
| **Costo por iteración**   | Alto (procesa todo el dataset)  | Bajo (procesa un ejemplo)        |
| **Velocidad de convergencia** | Lenta (menos actualizaciones) | Rápida (más actualizaciones)     |
| **Estabilidad**           | Más estable                     | Más ruidosa (varianza alta)      |

> **Frase clave**: *"No se trata de la calidad, se trata de la cantidad"* (SGD permite más actualizaciones).

## Tamaño del Paso (η)
### Definición
- Factor que escala el gradiente: `w ← w - η * ∇w Loss(x, y, w)`  

### Importancia
- **η pequeño**:  
  - Conservador y estable.  
  - Convergencia lenta.  
- **η grande**:  
  - Agresivo y rápido.  
  - Riesgo de inestabilidad.  

### Estrategias para η
1. **Constante**:  
   Ejemplo: `η = 0.1` (valor fijo).  
2. **Decreciente**:  
   Ejemplo: `η = 1 / √(número de actualizaciones)`.  

---
*Estas notas resumen los conceptos clave del Descenso de Gradiente Estocástico y su comparación con el Descenso de Gradiente tradicional.*
