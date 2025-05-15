# Procesos de Decisión de Markov (MDPs)

## Visión general de los MDPs

* Los MDPs son un **modelo matemático para la toma de decisiones bajo incertidumbre**.
* Fueron introducidos por primera vez entre las décadas de 1950 y 1960.
* El término 'Markov' se refiere a Andrey Markov, ya que los MDPs son **extensiones de las Cadenas de Markov**.
* La diferencia clave es que los MDPs **permiten tomar decisiones** (realizar acciones o tener opciones).
* A diferencia de los problemas de búsqueda donde la función de sucesor `Succ(s, a)` es determinista, en los MDPs, tomar una acción `a` en un estado `s` puede llevar a un **estado aleatorio** (`s01`, `s02`, etc.).

## Aplicaciones de los MDPs

* Los MDPs se aplican en diversas áreas, como:
    * **Robótica**: decidir hacia dónde moverse cuando los actuadores pueden fallar o encontrar obstáculos imprevistos.
    * **Asignación de recursos**: decidir qué producir sin conocer la demanda exacta del cliente.
    * **Agricultura**: decidir qué plantar sin conocer el clima ni el rendimiento de los cultivos resultante.
    * **Juegos de azar**, como un juego de dados.

## Definición de un Proceso de Decisión de Markov (MDP)

Un MDP se define por los siguientes componentes:

* **Estados**: El conjunto de estados.
* **sstart**: El estado inicial, que pertenece al conjunto de Estados.
* **Actions(s)**: Las acciones posibles desde un estado `s`.
* **T(s, a, s')**: La **probabilidad de transición**, que especifica la probabilidad de terminar en el estado `s'` si se toma la acción `a` en el estado `s`. Para cada estado `s` y acción `a`, la suma de las probabilidades `T(s, a, s')` sobre todos los posibles `s'` es igual a 1. Los **sucesores** son los estados `s'` tales que `T(s, a, s') > 0`.
* **Reward(s, a, s')**: La **recompensa** por la transición de `s` a `s'` al tomar la acción `a`. Esto contrasta con los problemas de búsqueda que tienen un costo `Cost(s, a)`.
* **IsEnd(s)**: Indica si el estado `s` es un estado final (de fin de juego).
* **γ**: Un **factor de descuento** (`0 <= γ <= 1`).

## Policy (Política)

* Una **política (π)** es una **función que mapea cada estado `s` a una acción `a`** dentro de las acciones posibles en ese estado (`Actions(s)`).
* Se considera la **solución a un MDP**.

## Evaluación de una Política

* Seguir una política genera una **ruta (path)** que es una variable aleatoria.
* La **utilidad (utility)** de una política es la **suma (descontada) de las recompensas en la ruta**; esta suma también es una variable aleatoria.
* La **función de valor (value)** de una política `Vπ(s)` es la **utilidad esperada** que se recibe al seguir la política `π` desde el estado `s`.
* La **función Q-value** de una política `Qπ(s, a)` es la **utilidad esperada de tomar la acción `a` desde el estado `s` y luego seguir la política `π`**.

## Descuento (Discounting)

* El **factor de descuento (γ)**, entre 0 y 1, se usa para calcular la utilidad total de una ruta.
* Para una ruta `s0, a1r1s1, a2r2s2, ...` (acción, recompensa, nuevo estado), la utilidad con descuento `γ` es `u = r1 + γr2 + γ²r3 + γ³r4 + ...`.
* Un descuento `γ = 1` significa que las recompensas futuras son tan valiosas como las inmediatas (ahorrar para el futuro).
* Un descuento `γ = 0` significa que solo importa la recompensa inmediata (vivir el momento).
* Un descuento `0 < γ < 1` da un valor balanceado a las recompensas inmediatas y futuras.

## Relaciones de Recurrencia (Bellman equations para una política fija)

* La función de valor `Vπ(s)` y la función Q-value `Qπ(s, a)` están relacionadas por las siguientes recurrencias:
    * `Vπ(s) = Qπ(s, π(s))` si `s` no es un estado final. `Vπ(s) = 0` si `IsEnd(s)` es verdadero.
    * `Qπ(s, a) = Sumatoria sobre s' de T(s'|s, a) * [Reward(s, a, s') + γVπ(s')]`.

## Algoritmo de Evaluación de Política (Policy Evaluation)

* La evaluación de política es un **algoritmo iterativo para computar el valor `Vπ(s)` de una política dada `π` para todos los estados `s`**.
* Se inicializa `V(0)π(s) = 0` para todos los estados.
* En cada iteración `t`, se actualiza `V(t)π(s)` para cada estado `s` usando la recurrencia: `V(t)π(s) = Sumatoria sobre s' de T(s'|s, π(s)) * [Reward(s, π(s), s') + γV(t-1)π(s')]`.
* Este proceso se repite (`t = 1, ..., tPE`) hasta que los valores convergen, es decir, el cambio máximo entre iteraciones es menor a un umbral `ε`.

## Valor y Política Óptimos

* El **valor óptimo Vopt(s)** es el **máximo valor (utilidad esperada) que se puede alcanzar por cualquier política** comenzando desde el estado `s`.
* La **política óptima πopt(s)** es la política que **alcanza el valor óptimo** para cada estado.

## Relaciones de Recurrencia Óptimas (Bellman optimality equations)

* El Q-value óptimo `Qopt(s, a)` es el valor óptimo si se toma la acción `a` en el estado `s`, y luego se sigue la política óptima:
    * `Qopt(s, a) = Sumatoria sobre s' de T(s, a, s') * [Reward(s, a, s') + γVopt(s')]`.
* El valor óptimo `Vopt(s)` es el máximo Q-value posible desde el estado `s`:
    * `Vopt(s) = max_a en Actions(s) Qopt(s, a)` si `s` no es un estado final. `Vopt(s) = 0` si `IsEnd(s)` es verdadero.

## Algoritmo de Iteración de Valor (Value Iteration)

* La iteración de valor es un **algoritmo para computar el valor óptimo `Vopt(s)` y la política óptima `πopt(s)`**. Fue propuesto por Bellman en 1957.
* Se inicializa `V(0)opt(s) = 0` para todos los estados.
* En cada iteración `t`, se actualiza `V(t)opt(s)` para cada estado `s` usando la recurrencia basada en las relaciones de optimalidad: `V(t)opt(s) = max_a en Actions(s) (Sumatoria sobre s' de T(s, a, s') * [Reward(s, a, s') + γV(t-1)opt(s')])`. La parte de la sumatoria es `Q(t-1)opt(s, a)`.
* Este proceso se repite (`t = 1, ..., tVI`).
* Una vez que `Vopt` ha convergido, la política óptima se puede obtener directamente eligiendo la acción que maximiza el Q-value óptimo en cada estado: `πopt(s) = arg max_a en Actions(s) Qopt(s, a)`.

## Convergencia de la Iteración de Valor

* La iteración de valor **converge a la respuesta correcta** si:
    * El **factor de descuento γ es menor que 1** (`γ < 1`), o
    * El **grafo del MDP es acíclico**.

## Resumen de Algoritmos

* **Policy evaluation**: Dados un MDP y una política `π`, calcula `Vπ`.
* **Value iteration**: Dado un MDP, calcula `Qopt` y `πopt`.

En esencia, los MDPs extienden los problemas de búsqueda al incluir la incertidumbre en las transiciones entre estados, y utilizan conceptos como políticas, valor esperado y algoritmos iterativos (como la evaluación de políticas y la iteración de valor) para encontrar la mejor forma de actuar bajo esta incertidumbre.
