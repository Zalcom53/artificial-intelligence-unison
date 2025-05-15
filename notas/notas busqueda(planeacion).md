# **Notas de Estudio: Búsqueda en Inteligencia Artificial**

El tema central es la resolución de problemas mediante **búsqueda**. Esto implica encontrar una secuencia de acciones para transformar un estado inicial en un estado deseado (estado objetivo).

## **1. Problemas de Búsqueda**

- Un problema de búsqueda consta de:
    - Un **espacio de estados**: El conjunto de todas las posibles configuraciones del problema. En el ejemplo de Rumania, son las ciudades. En el rompecabezas de 8, son las diferentes disposiciones de las fichas.
    - Un **modelo de transición**: Describe cómo pasar de un estado a otro. Se puede definir con:
        - Una **función sucesora** (`Successors(s)`): Retorna pares (acción, costo, estado resultante) para un estado `s`.
        - Funciones separadas: `Actions(s)` (acciones posibles en `s`), `Result(s, a)` (estado después de la acción `a` en `s`), `Cost(s, a, s')` (costo de la acción `a` de `s` a `s'`).
    - Un **estado inicial** (`start state`).
    - Una **prueba de objetivo** (`goal test`): Una forma de saber si un estado es un estado objetivo.
    - Una **función de costo de camino** (`path cost function`): El costo total de una secuencia de acciones desde el inicio.

- Una **solución** es una **secuencia de acciones (un plan)** que transforma el estado inicial en un estado objetivo.

- **Ejemplos de aplicaciones y sus elementos**:
    - **Sistemas multi-robot**: Acciones: trasladar y rotar juntas; aceleración y dirección de todos los robots. Objetivo: ¿más rápido? ¿más eficiente energéticamente?
    - **Resolución de rompecabezas**: Acciones: mover piezas (ej: `Move12Down`). Objetivo: alcanzar una cierta configuración.
    - **Traducción automática**: Acciones: añadir palabras individuales (ej: `the`). Objetivo: inglés fluido y que conserve el significado.

- Ejemplo detallado: **Rumania**
    - Espacio de estados: Ciudades.
    - Función sucesora: Ir a la ciudad adyacente con costo igual a la distancia.
    - Estado inicial: Arad.
    - Prueba de objetivo: ¿Es el estado `Bucharest`?.

- Ejemplo: **Granjero, Col, Cabra, Lobo**. Se listan acciones como F. (el granjero cruza solo), FC. (granjero cruza con col), F/ (granjero regresa solo), etc.

## **2. Árbol de Búsqueda vs. Espacio de Estados**

- **Nodos en el espacio de estados** son los estados del problema. Representan un estado abstracto del mundo, tienen sucesores, pueden ser objetivo o no, y pueden tener múltiples predecesores.
- **Nodos en el árbol de búsqueda** son **caminos**. Representan una secuencia de acciones que resulta en el estado del nodo. Tienen un estado del problema y un padre, una longitud de camino (profundidad) y un costo. El **mismo estado del problema puede ser alcanzado por múltiples nodos** del árbol de búsqueda.
- Tanto el espacio de estados como el árbol de búsqueda se construyen "bajo demanda", construyendo lo mínimo posible.

## **3. Algoritmos de Búsqueda General**

- **Ideas importantes**: **Frontier** (también llamado `fringe`), **Expansión** (generar sucesores de un nodo), **Estrategia de exploración** (elegir qué nodo expandir a continuación).
- **Búsqueda en Árbol General** (`General Tree Search`).
- **Búsqueda Primero en Profundidad** (`Depth First Search` - DFS):
    - Estrategia: Expandir el nodo **más profundo** primero.
    - Implementación: La `Frontier` es una **pila LIFO**.
- **Búsqueda Primero en Anchura** (`Breadth First Search` - BFS):
    - Estrategia: Expandir el nodo **menos profundo** primero.
    - Implementación: La `Fringe` es una **cola FIFO**.
    - **BFS encuentra el camino más corto en términos de número de transiciones**. **No encuentra el camino de menor costo**.

## **4. Búsqueda en Grafo (`Graph Search`)**

- No detectar estados repetidos puede causar un trabajo exponencialmente mayor.
- Solución simple: **nunca expandir un estado dos veces**.
- La búsqueda en grafo es **casi siempre mejor que la búsqueda en árbol**.
- Se implementa un conjunto o diccionario (`dict` or `set`) para llevar registro de los estados **explorados** (`explored`).
- La `frontier` puede implementarse como una cola de prioridad (`priority Q`) y un conjunto (`set`).

## **5. Búsqueda de Costo Uniforme (`Uniform Cost Search` - UCS)**

- **Encuentra el camino de menor costo**.
- Estrategia: Expandir el nodo **más barato** primero.
- La `Frontier` es una **cola de prioridad** ordenada por costo.
- Explora **contornos de costo crecientes**.
- Lo bueno: **UCS es completo y óptimo**.
- Lo malo: Explora opciones en "todas direcciones", no tiene información sobre la ubicación del objetivo. Comparado con A*, UCS se expande en todas direcciones.

## **6. Heurísticas**

- Cualquier **estimación de cuán cerca está un estado de un objetivo**.
- Diseñada para un problema de búsqueda particular.
- Ejemplos: Distancia Manhattan, Distancia Euclidiana.
- "Para hacer más, saber más" (Lección de IA).

## **7. Búsqueda Greedy Best-First**

- Estrategia: Expandir el nodo que **parece más cercano al objetivo**.
- Ordena por la distancia al objetivo, o **costo hacia adelante `h(n)`**.
- Puede haber problemas (`Greedy goes wrong`).

## **8. Búsqueda A\* (`A* Search`)**

- Combina la búsqueda de costo uniforme (costo del camino `g(n)`, o costo hacia atrás) y la búsqueda `Greedy Best-First` (distancia al objetivo `h(n)`, o costo hacia adelante).
- Ordena por la **suma: `f(n) = g(n) + h(n)`**. `g(n)` es el costo hasta el nodo `n`, `h(n)` es el costo estimado desde `n` hasta el objetivo más cercano (heurística), `f(n)` es el costo total estimado vía `n`.
- ¿Cuándo termina A\*?: **Solo se detiene cuando saca un objetivo de la cola** (`dequeue a goal`), no cuando lo encola (`enqueue a goal`).
- A\* es **óptimo** si utiliza una heurística admisible. Se expande principalmente hacia el objetivo, pero también "cubre sus apuestas" para asegurar la optimalidad.
- **Optimalidad de A***: La prueba implica que un objetivo subóptimo (`G`) no puede ser sacado de la frontera antes que un nodo (`n`) que forma parte del camino óptimo (`G*`). Esto no puede suceder porque `n` será sacado antes que `G` si la heurística es admisible.

## **9. Heurísticas Admisibles (`Admissible Heuristics`)**

- Una heurística `h` es **admisible (optimista)** si **`h(n)` ≤ `h*(n)`**, donde `h*(n)` es el costo verdadero hasta el objetivo más cercano desde `n`.
- **¡Nunca sobreestime el costo real!**.
- Crear heurísticas admisibles es clave para resolver problemas de búsqueda difíciles de manera óptima.
- A menudo, las heurísticas admisibles son soluciones a **problemas relajados**, donde hay nuevas acciones disponibles (ej: en el rompecabezas de 8, permitir que cualquier ficha se deslice a cualquier posición adyacente ignorando otras fichas).
- Las heurísticas inadmisibles a veces también son útiles (aunque no garantizan optimalidad).

## **10. Dominancia de Heurísticas**

- Una heurística `ha` domina a `hc` (`ha` ≥ `hc`) si `ha(n)` ≥ `hc(n)` para todos los nodos `n`.
- El **máximo de heurísticas admisibles es una heurística admisible**.

## **11. Ejemplo: Rompecabezas de 8**

- ¿Qué son los estados? ¿Cuántos estados hay? ¿Cuáles son las acciones? ¿Qué estados se pueden alcanzar desde el inicio? ¿Cuáles deberían ser los costos?.
- Heurística: **Número de fichas mal colocadas** (`Number tiles misplaced`). Es **admisible** porque es una solución a un problema relajado (donde cualquier ficha puede moverse a cualquier posición vacía).
- Heurística: **Distancia Manhattan total** (`Total Manhattan distance`). Es la suma de las distancias Manhattan para cada ficha desde su posición actual hasta su posición objetivo. Es **admisible** porque es una solución a un problema relajado (donde cualquier ficha puede deslizarse un paso en cualquier momento ignorando otras fichas).
- Comparación del número promedio de nodos expandidos para encontrar el camino óptimo (para caminos de longitud 4, 8, 12):
    - UCS: 112, 6300, 3.6 x 10^6
    - Heurística de Fichas (`TILES`): 13, 39, 227
    - Heurística Manhattan (`MANHATTAN`): 12, 25, 73
    - Se observa que las heurísticas (especialmente Manhattan) **reducen significativamente** el número de nodos expandidos.
