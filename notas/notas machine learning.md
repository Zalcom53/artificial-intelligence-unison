# Notas de Estudio: Extracción de Características y Predictores No Lineales en Machine Learning

El machine learning generalmente se divide en dos pasos principales: la **extracción de características** y el **aprendizaje**.

* El objetivo es encontrar un predictor `fw(x)` dentro de un conjunto de posibles predictores `F = {fw(x) = sign(w · (x)) : w ∈ Rd}`.

## 1. Extracción de Características (Feature Extraction)

* La **extracción de características** es el proceso de **elegir el conjunto F**, o más precisamente, la **función de extracción de características (x)**, basándose en el conocimiento del dominio del problema.
* El objetivo es que el conjunto F contenga **buenos predictores**, pero que no sea excesivamente grande.
* Dada una entrada `x`, el extractor de características (x) produce un conjunto de **pares (nombre de característica, valor de característica)**. Esta elección es inicialmente arbitraria.
* **Ejemplo:** Para la entrada "abc@gmail.com":
  * `length>10`: 1
  * `fracOfAlpha`: 0.85
  * `contains @`: 1
  * `endsWith com`: 1
  * `endsWith org`: 0
* Estas características se organizan en un **vector de características (x)**.

## 2. Predicción con Características

* La predicción se basa en un **vector de pesos `w`** y el vector de características `(x)`.
* La puntuación (score) se calcula como una **combinación ponderada** de las características y los pesos, usando el **producto punto**: `w · (x) = ∑ dj=1 wj(x)j`.
* **Ejemplo de cálculo de puntuación:** Con pesos `w = [-1.2, 0.6, 3, 2.2, 1.4]` y características `(x) = [1, 0.85, 1, 1, 0]` (para `length>10`, `fracOfAlpha`, `contains @`, `endsWith com`, `endsWith org`):
  * Puntuación = `(-1.2 * 1) + (0.6 * 0.85) + (3 * 1) + (2.2 * 1) + (1.4 * 0) = -1.2 + 0.51 + 3 + 2.2 + 0 = 4.51`.

## 3. Organización de Características: Plantillas de Características (Feature Templates)

* Para decidir qué características incluir, se utilizan las **plantillas de características**.
* Una **plantilla de características** es una **agrupación de características que se calculan de manera similar**.
* Permiten definir **tipos generales de patrones** a buscar, en lugar de listar cada patrón individualmente.
* **Ejemplos de plantillas y características generadas:**
  * Plantilla: "Los últimos tres caracteres son iguales a..." -> Genera características como `endsWith aaa`, ..., `endsWith com`, ..., `endsWith zzz`. Para "abc@gmail.com", `endsWith com` tiene valor 1, las otras 0.
  * Plantilla: "Longitud mayor que..." -> `Length greater than 10`.
  * Plantilla: "Fracción de caracteres alfanuméricos" -> `Fraction of alphanumeric characters`.
  * Plantilla: "Intensidad del píxel en fila y columna (canal)" -> `Pixel intensity of image at row 10 and column 93 (red channel)`.
  * Plantilla: "Latitud está en [ , ] y longitud está en [ , ]" -> `Latitude is in [ 37.4, 37.5 ] and longitude is in [ -122.2, -122.1 ]`.

## 4. Esparsidad y Representación de Vectores de Características

* El uso de plantillas puede generar **vectores de características muy esparsos**, donde la mayoría de los valores son cero.
* **Representación Compacta:**
  * **Arrays:** Buenos para características **densas** (pocos ceros).
  * **Diccionarios (o mapas):** Muy eficientes para características **esparsas**, almacenando solo los pares (nombre, valor) distintos de cero.
  * **Ejemplo de diccionario:** `{"fracOfAlpha": 0.85, "contains @": 1}` o `{"endsWith com": 1}`.

## 5. Predictores No Lineales

* Para modelar datos más complejos, a menudo se necesitan **predictores no lineales**.
* La forma del predictor sigue siendo **`fw(x) = w · (x)`**.
* Se obtienen predictores no lineales **cambiando la función de extracción de características (x)**.
* La puntuación `w · (x)` es **siempre lineal en `w` y lineal en `(x)`**, pero **no necesariamente lineal en `x`**.
* **Idea Clave de la No Linealidad:**
  * **Expresividad:** La puntuación `w · (x)` puede representar una **función no lineal de la entrada original x**.
  * **Eficiencia:** La puntuación siempre es **lineal en `w`**, lo que permite usar los mismos algoritmos de aprendizaje lineal para encontrar el vector de pesos `w`, incluso cuando se ajusta un modelo no lineal respecto a `x`.

## 6. Tipos de Características No Lineales (Ejemplos de (x))

* **Características Cuadráticas:** Incluyen términos de x al cuadrado. Ej: `(x) = [1, x, x²]` para entrada escalar; `(x) = [x₁, x₂, x₁² + x₂²]` para entrada vectorial.
* **Características Constantes a Trozos (Piecewise Constant):** Dividen el espacio de entrada en regiones usando funciones indicadoras. Ej: `(x) = [1[0 < x ≤ 1], 1[1 < x ≤ 2], ...]`.
* **Características con Estructura de Periodicidad:** Incluyen funciones periódicas. Ej: `(x) = [1, x, x², cos(3x)]`.
* Se puede incorporar **cualquier tipo de característica** que parezca relevante en (x).

## 7. Clasificación No Lineal y Límites de Decisión

* Para clasificación, el predictor es a menudo `sign(w · (x))`.
* El **límite de decisión** se define donde `w · (x) = 0`. La forma de este límite en el espacio de entrada `x` depende de (x).
* Si `(x)` es lineal en `x` (ej. `(x) = [x₁, x₂]`), el límite de decisión en el espacio de entrada `x` es una **línea**.
* Si `(x)` incluye términos no lineales de `x` (ej. `(x) = [x₁, x₂, x₁² + x₂²]`), el límite de decisión en el espacio de entrada `x` puede ser una forma no lineal, como un **círculo**.
* **Visualización:** En el **espacio de entrada `x`**, el límite puede ser curvo. Sin embargo, al transformar los datos al **espacio de características `(x)`**, el límite de decisión siempre aparece como un **hiperplano (una línea en 2D)** en ese espacio.
