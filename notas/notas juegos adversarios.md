# CS 188: Artificial Intelligence - Game Trees: Adversarial Search

## Conceptos Fundamentales
**Juegos Adversarios**: Entornos donde agentes de IA compiten con objetivos opuestos.

### Características clave de los juegos (Ejes):
- **Determinista** vs. Estocástico
- **Información perfecta** (completamente observable) vs. imperfecta
- Número de jugadores: 2, 3 o más
- **Equipos** vs. Individuos
- **Por turnos** vs. Simultáneos
- **Suma cero** vs. Suma general

## Juegos Deterministas
**Formalización**:
- **Estados (S)**: Estado inicial (s0)
- **Jugadores (P)**: Turnos alternados
- **Acciones (A)**: Dependen del jugador/estado
- **Función de Transición**: S × A → S
- **Prueba Terminal**: S → {true, false}
- **Utilidades Terminales**: S × P → ℝ

**Solución**: Política S → A (mapea estados a acciones)

## Tipos de Juegos
### Juegos de Suma Cero
- Utilidades opuestas (competencia pura)
- Un jugador **maximiza**, el otro **minimiza**
- Ejemplo: Ajedrez, Tic-Tac-Toe

### Juegos de Suma General
- Utilidades independientes
- Permite cooperación, alianzas, etc.
- Ejemplo: Negociaciones

### Juegos en Equipo
- Recompensa común para miembros del equipo
- Ejemplo: Deportes en equipo

## Árboles de Juegos y Minimax
### Conceptos Clave
- **Árbol de Juego**: Representación de estados y transiciones
- **Valor de un Estado**: Mejor utilidad alcanzable
- **Nodos MAX/MIN**: Alternancia de turnos

### Algoritmo Minimax
- **Propósito**: Encontrar estrategia óptima contra adversario racional
- **Mecánica**:
  - MAX elige máximo valor entre hijos
  - MIN elige mínimo valor entre hijos
- **Valores terminales**: Definidos por el juego
- **Valores minimax**: Calculados recursivamente

### Propiedades
- **Optimalidad**: Estrategia óptima contra oponente perfecto
- **Complejidad**:
  - Tiempo: O(bᵐ) (b = factor de ramificación, m = profundidad)
  - Espacio: O(bm)

## Poda Alpha-Beta
### Conceptos Clave
- **Alpha (α)**: Mejor valor garantizado para MAX (inicial: -∞)
- **Beta (β)**: Mejor valor garantizado para MIN (inicial: +∞)
- **Poda**: Eliminar ramas no prometedoras sin afectar resultado raíz

### Condiciones de Poda
1. **Nodos MIN**: Podar si v ≤ α
2. **Nodos MAX**: Podar si v ≥ β

### Beneficios
- **Mismo resultado** que Minimax en la raíz
- **Eficiencia mejorada**: O(b^(m/2)) con ordenamiento perfecto
- **Ordenamiento crítico**: Movimientos prometedores primero aumentan la poda

## Limitaciones Prácticas
### Funciones de Evaluación
- **Propósito**: Estimar utilidad en estados no terminales
- **Implementaciones**:
  - Sumas lineales ponderadas de características
  - Redes neuronales (ej: AlphaGo)
- **Profundidad**: Más búsqueda reduce dependencia de calidad de la función

### Estado del Arte
| Juego   | Hito IA                             | Año   |
|---------|-------------------------------------|-------|
| Damas   | Resuelto (Chinook)                  | 2007  |
| Ajedrez | Deep Blue vence a Kasparov          | 1997  |
| Go      | AlphaGo vence a Lee Sedol           | 2016  |

## Conclusiones
1. Minimax provee soluciones óptimas en juegos deterministas de suma cero.
2. Alpha-Beta mejora eficiencia mediante poda sin sacrificar optimalidad.
3. Funciones de evaluación permiten manejar complejidad en juegos profundos.
4. Ordenamiento inteligente de movimientos maximiza la poda.
