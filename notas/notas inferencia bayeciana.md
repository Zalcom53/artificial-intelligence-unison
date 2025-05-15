# Notas de Estudio: CS 221 - Inteligencia Artificial - Inferencia Probabilística

## Probabilidad e Inferencia Probabilística

- La probabilidad se describe como el "sentido común reducido a cálculo".
- La inferencia probabilística es el cálculo de alguna cantidad a partir de una distribución de probabilidad conjunta.

## Redes Bayesianas (Bayesian Networks - BNs)

- Se utilizan como ejemplos la Red de Alarma (Burglary, Earthquake, Alarm, John calls, Mary calls) y el Dominio de Tráfico (Raining, Traffic, Late for class).
- Una red bayesiana incluye variables aleatorias y sus probabilidades condicionales (CPTs).

## Inferencia Exacta

### Inferencia por Enumeración

- Si se tiene tiempo ilimitado, la inferencia en BNs es sencilla con este método.
- Declarar probabilidades incondicionales necesarias, enumerar todas las probabilidades atómicas necesarias y calcular la suma de productos.
- Ejemplo para P(+b, +j, +m) en la red de alarma:
  ```
  ∑e ∑a P(+b) P(e) P(a|+b,e) P(+j|a) P(+m|a)
  ```
- Optimización: sacar términos de las sumas.
- **¿Por qué es lenta?** Se construye la distribución conjunta completa antes de sumar, repitiendo mucho trabajo.

### Eliminación de Variables (Variable Elimination - VE)

- Intercalar la unión (joining) de factores con la marginalización (sumar variables).
- Aunque NP-hard, suele ser más rápida que la enumeración.
- Requiere álgebra de factores.

#### Factores

- P(X,Y), P(x,Y), P(X|Y), P(Y|x), P(y|X), P(Y₁... YN | X₁... XM)
- Variables de evidencia "seleccionadas" no aparecen en la matriz.

#### Factores Iniciales

- Son las CPTs locales. Si hay evidencia, se seleccionan los valores correspondientes.

#### Operaciones

- **Unir Factores:** Producto punto a punto de factores que comparten variables.
  - Ej: Unir P(R) y P(T|R) → P(R,T) = P(r)P(t|r)
- **Eliminar:** Sumar sobre una variable → reduce el tamaño del factor.
  - Ej: Sumar R de P(R,T) para obtener P(T)

#### Esquema General

1. Comenzar con factores iniciales.
2. Mientras haya variables ocultas:
   - Elegir H
   - Unir factores que mencionan H
   - Eliminar H
3. Unir factores restantes
4. Normalizar el resultado

## Inferencia Aproximada

- Alternativa cuando la inferencia exacta es lenta/imposible.
- Se toman N muestras de una distribución de muestreo S.
- Se estima la probabilidad posterior y se demuestra convergencia a P.

### Muestreo Prior

- Genera muestras de la distribución conjunta.
- Orden topológico de muestreo.
- Estimación por conteo de eventos y normalización.

### Muestreo por Rechazo

- Estimar probabilidades condicionales como P(C | +s).
- Se ignoran muestras que no coinciden con la evidencia.
- **Problema:** Se desperdician muestras si la evidencia es improbable.

### Muestreo por Verosimilitud (Likelihood Weighting)

- Fija evidencia y muestrea el resto.
- Asigna un peso a cada muestra.
- **Ventaja:** La evidencia influye en la muestra.
- **Limitación:** No influye sobre variables aguas arriba.

### Cadenas de Markov Monte Carlo (MCMC)

- Genera muestras similares entre sí.
- Se remuestrea una variable a la vez, condicionada al resto (evidencia fija).
- **Propiedades:** Muestras no independientes, pero promedios consistentes.
- **Ventaja:** Variables aguas arriba y abajo se condicionan.

## Otros Conceptos/Ejemplos

- Google usa filtrado bayesiano como un "if" en programación.
- Ejemplo clásico de probabilidad: Problema de Monty Hall.
