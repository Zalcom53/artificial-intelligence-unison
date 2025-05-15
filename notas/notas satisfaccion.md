**Conceptos Fundamentales de CSPs**

* Los Problemas de Satisfacción de Restricciones (CSPs) son un **subconjunto especial de los problemas de búsqueda**.
* A diferencia de los problemas de búsqueda estándar donde el estado es una "caja negra" con una estructura de datos arbitraria, en los CSPs el estado se define por **variables Xi** que toman **valores de un dominio D**. El dominio D a veces puede depender de la variable i.
* La prueba de objetivo en los problemas de búsqueda estándar puede ser cualquier función sobre estados, mientras que en los CSPs, la prueba de objetivo es un **conjunto de restricciones** que especifican **combinaciones permitidas de valores** para subconjuntos de variables.
* Los CSPs están **especializados para problemas de identificación**. En estos problemas, lo **importante es el objetivo en sí**, no el camino para alcanzarlo. Esto contrasta con los problemas de planificación en la búsqueda estándar, donde el camino hacia el objetivo es lo importante y los caminos tienen costos o profundidades.
* Los CSPs permiten el uso de **algoritmos generales útiles** con más potencia que los algoritmos de búsqueda estándar.
* Una **solución** a un CSP es una asignación de valores a las variables que satisface todas las restricciones.

**Ejemplos de CSPs**

* **Coloración de Mapas**: Las variables son regiones, los dominios son colores, y las restricciones son que las regiones adyacentes deben tener colores diferentes.
* **N-Reinas**: Se mencionan dos formulaciones. Las restricciones típicas son que no haya dos reinas en la misma fila, columna o diagonal.
* **Criptoaritmética**: Las variables son letras que representan dígitos, los dominios son {0, 1, ..., 9} (con algunas restricciones implícitas o explícitas), y las restricciones son que la suma de las columnas sea correcta, tratando las letras como números.
* **Sudoku**: Las variables son cada cuadrado abierto, los dominios son {1, 2, ..., 9}, y las restricciones son que haya un `alldiff` de 9 vías para cada fila, cada columna y cada región. También se pueden representar con un conjunto de restricciones de desigualdad por pares.
* **Algoritmo de Waltz**: Un ejemplo temprano de un cálculo de IA planteado como CSP para interpretar dibujos lineales de poliedros sólidos como objetos 3D. El enfoque usa intersecciones como variables y restricciones entre intersecciones adyacentes.

**Variedades de CSPs y Restricciones**

* **Variables Discretas**:

  * **Dominios Finitos**: Tamaño `d` implica `O(dn)` asignaciones completas. Ejemplos: CSPs Booleanos, Satisfacibilidad Booleana (que es NP-completo).
  * **Dominios Infinitos**: Ejemplos: enteros, cadenas. Aplicado en programación de trabajos, donde las variables son tiempos de inicio/fin. Las restricciones lineales son resolubles, las no lineales son indecidibles.
* **Variables Continuas**:

  * Ejemplo: Tiempos de inicio/fin para observaciones del Telescopio Hubble.
  * Las restricciones lineales son resolubles en tiempo polinomial usando métodos LP.
* **Variedades de Restricciones**:

  * **Restricciones Unarias**: Involucran una sola variable. Son equivalentes a reducir los dominios.
  * **Restricciones Binarias**: Involucran pares de variables.
  * **Restricciones de Orden Superior**: Involucran 3 o más variables. Ejemplo: restricciones de columna en criptoaritmética.
  * **Preferencias (Restricciones Flexibles/Soft Constraints)**: Ej. "el rojo es mejor que el verde". A menudo representables por un costo para cada asignación de variable. Esto da lugar a problemas de optimización con restricciones. (Estas se ignorarán hasta el estudio de las redes Bayesianas).

**CSPs en el Mundo Real**

* Los CSPs tienen muchas aplicaciones en el mundo real, incluyendo:

  * Problemas de asignación (ej. quién enseña qué clase).
  * Problemas de horarios (ej. qué clase se ofrece cuándo y dónde).
  * Configuración de hardware.
  * Programación de transporte.
  * Programación de fábrica.
  * Diseño de circuitos.
  * Diagnóstico de fallas.
* Muchos problemas del mundo real involucran variables de valor real.

**Resolviendo CSPs**

* **Formulación de Búsqueda Estándar**:

  * Los estados se definen por los valores asignados hasta el momento (asignaciones parciales).
  * Estado inicial: la asignación vacía, `{}`.
  * Función sucesora: asignar un valor a una variable sin asignar.
  * Prueba de objetivo: la asignación actual está completa y satisface todas las restricciones.
  * Un enfoque ingenuo comenzaría con esto, pero tiene problemas.
* **Búsqueda con Retroceso (Backtracking Search)**:

  * Es el **algoritmo no informado básico** para resolver CSPs.
  * Idea 1: **Una variable a la vez**. Las asignaciones de variables son conmutativas (ej. WA=red y NT=green es lo mismo que NT=green y WA=red), por lo que se fija un orden. Solo se necesita considerar asignaciones a una única variable en cada paso.
  * Idea 2: **Verificar las restricciones a medida que se avanza**. Solo se consideran valores que no entran en conflicto con asignaciones previas. Esto es una "prueba de objetivo incremental".
  * La búsqueda en profundidad (DFS) con estas dos mejoras se llama búsqueda con retroceso.
  * Puede resolver el problema de las n-reinas para `n <= 25`.
  * Backtracking = DFS + ordenación de variables + fallo en la violación.
* **Mejorando la Búsqueda con Retroceso**:

  * Ideas generales pueden ofrecer **grandes ganancias de velocidad**.
  * **Ordenación**: ¿Qué variable asignar a continuación? ¿En qué orden probar sus valores?
  * **Filtrado**: ¿Podemos detectar fallos inevitables de forma temprana?
  * **Estructura**: ¿Podemos explotar la estructura del problema? (Ej. Tasmania es un subproblema independiente en la coloración de mapas debido a la estructura del grafo).

**Técnicas de Filtrado**

* **Filtrado**: Mantener un registro de los dominios para las variables sin asignar y **eliminar las malas opciones**.
* **Verificación Adelantada (Forward Checking)**:

  * Elimina los valores que violan una restricción cuando se añaden a la asignación existente.
  * Propaga información de las variables asignadas a las no asignadas.
  * No proporciona detección temprana para *todos* los fallos (ej. no detecta que NT y SA no pueden ser azules simultáneamente si ambos aún tienen azul en su dominio después de una asignación inicial a otra variable).
  * Consiste en **forzar la consistencia de los arcos** que apuntan a cada nueva asignación.
* **Propagación de Restricciones**:

  * Razonar de restricción a restricción para detectar fallos antes.
* **Consistencia de Arco**:

  * Un arco X -> Y es consistente si, para cada valor `x` en el dominio de X, existe algún valor `y` en el dominio de Y que podría asignarse sin violar la restricción entre X e Y.
  * **Importante: Si X pierde un valor, los vecinos de X deben ser verificados nuevamente**.
  * La consistencia de arco **detecta fallos antes** que la verificación adelantada.
  * Puede ejecutarse como un preprocesador o después de cada asignación.
  * Consiste en **eliminar valores del dominio de la variable "cola"** del arco (la primera variable en X -> Y).
  * La imposición de consistencia de arco en todo un CSP tiene una complejidad de tiempo `O(n^2d^3)`, que puede reducirse a `O(n^2d^2)`. Sin embargo, detectar todos los posibles problemas futuros (encontrar una solución o probar que no existe) es NP-hard.
* **Limitaciones de la Consistencia de Arco**:

  * Después de imponer la consistencia de arco, aún pueden quedar **una solución**, **múltiples soluciones** o **ninguna solución** (y no saberlo).
  * La consistencia de arco aún se ejecuta **dentro de una búsqueda con retroceso**.

**Heurísticas de Ordenación**

* **Ordenación de Variables: Mínimo de Valores Restantes (MRV)**:

  * Elige la variable con la **menor cantidad de valores legales** restantes en su dominio.
  * Se elige el mínimo en lugar del máximo porque es un ordenamiento de "fallo rápido" (si una variable tiene muy pocas opciones, es mejor intentar asignarla pronto para detectar si lleva a un fallo).
  * También se le llama la "variable más restringida".
* **Ordenación de Valores: Valor Menos Restringente (LCV)**:

  * Dada una variable elegida, elige el valor que **menos restringe** a las variables restantes.
  * Es decir, el valor que **elimina la menor cantidad de valores** en los dominios de las variables restantes.
  * Se elige el menos restringente en lugar del más restringente porque deja más opciones para las variables futuras, aumentando la probabilidad de encontrar una solución.
  * Puede requerir algo de computación determinar este valor (ej. volviendo a ejecutar el filtrado).
* La **combinación** de estas ideas de ordenación (MRV para variables, LCV para valores) hace que problemas como 1000 reinas sean factibles.

