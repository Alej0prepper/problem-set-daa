# Algoritmos Greedy

## Que es un algoritmo greedy?
Un algoritmo greedy es un paradigma de algoritmos que construye una solucion pieza a pieza, siempre escogiendo la  proxima parte que aporta el mejor beneficio.

## Caracteristicas
* una solucion optima local puede obtenerse al obtner un optimo local 
* una solucion optima de un problema es tambien una solucion optima para los subproblemas.

## Ejemplos de algoritmos Greedy:
* Algoritmos de Prim y Kruskal buscando el arbol abarcadoe de costo minimo 
* Dijsktra para encontrar el camino mas corto en un grafo
* huffman coding para compression de datos 
  

## Escenarios para usar Greedy
* Problemas con subestructuras optimas en que se puedan tomar decisiones greedy, por ejemplo siempre escoger el camino mejor.
* Situaciones en que una solucion aproximada es aceptable.
  
## Problemas Clasicos

## 2. Classic Problems

### 2.1 Frog Jumping Problem

- **Problem Statement**: Given a series of stones placed at integer locations, and a maximum jump length, determine the minimum number of jumps need to reach the end.
- **Greedy Approach**: Jump the fartest possible stone that is reachable for the current stone.

### 2.2 Activity Selection Problem

- **Problem Statement**: Given a set of activities with start and finish times, select the maximum number of activities that don’t overlap.
- **Greedy Approach**: Explain how sorting activities by finish time leads to an optimal selection strategy.

### 2.3 Fractional Knapsack Problem

- **Problem Statement**: Given weights and values of items that can be divided, maximize the total value in a knapsack with a weight limit $K$.
- **Greedy Approach**:
  - Calculate the value-to-weight ratio for each item.
  - Sort items based on this ratio in descending order.
  - Fill the knapsack starting from the item with the highest ratio, allowing for fractional amounts if necessary.

### 2.4 Minimize Cash Flow Among Friends

- **Problem Statement**: Given a list of debts among friends, minimize the total cash flow required to settle all debts.
- **Greedy Approach**: Discuss calculating net amounts for each person and settling debts by always addressing the largest creditor and debtor first.

## Frog Jumping Problem
Imagina que una rana quiere cruzar un río saltando sobre una serie de piedras dispuestas en posiciones enteras a lo largo de una línea. La rana comienza en la primera piedra y su objetivo es llegar a la última piedra con la menor cantidad de saltos posible.
Parámetros del problema:

    Se tiene un conjunto de piedras en posiciones enteras representadas como un array stones[], donde cada elemento indica la posición de una piedra en el río.
    La rana tiene un salto máximo max_jump, que representa la distancia máxima que puede saltar en un solo movimiento.
    La rana puede saltar solo a piedras que estén dentro de su rango de salto.
    Se debe calcular el mínimo número de saltos necesarios para llegar desde la primera piedra hasta la última.

Respuesta

El algoritmo greedy para el problema del salto de la rana es simple: siempre selecciona la opción más lejana para saltar. Lo interesante es entender por qué este enfoque es válido en este escenario.
Análisis de la Estrategia

Supongamos que saltar al lugar más lejano no es la mejor opción de forma global. Esto implicaría que había alguna ventaja en quedarse en la posición anterior. En este problema, una ventaja significativa es poder llegar más lejos en menos pasos.
Ventajas de Saltar al Lugar Más Lejano

Si saltar a la posición más lejana no fuera la mejor opción, significaría que había una ventaja en quedarse en la posición anterior. Sin embargo, en este problema, cualquier ventaja potencial en quedarse en una posición menos favorable se ve compensada por el hecho de que, después de saltar a esa posición, siempre podemos llegar a todas las demás posiciones a las que la rana podría haber saltado desde la posición original.
Inexistencia de Ventajas en Quedarse Atrás

Si hubiera una posición a la que no pudiéramos llegar después de haber saltado a una casilla menos favorable, entonces en un primer momento tampoco hubiéramos podido llegar a ella. Por lo tanto, dejar de saltar casillas no incluye ninguna ventaja significativa en términos de alcanzabilidad.
Conclusión

Nuestra variante greedy nos da la mejor solución porque siempre maximiza el progreso hacia la última piedra sin sacrificar la capacidad de alcanzar cualquier otra posición que fuera accesible desde la posición original. Esto se debe a que el problema no presenta situaciones en las que quedarse en una posición menos favorable ofrezca una ventaja significativa a largo plazo que no pueda ser compensada por saltar a la posición más lejana disponible.

## Activity Selection Problem

Es el mismo razonamiento del ejercicio anterior pero a la inversa como si se quisieran maximizar la cantidad de saltos.

Para maximizar el número de actividades que no se superpongan, se utiliza un enfoque greedy basado en ordenar las actividades por su tiempo de finalización. Este enfoque es óptimo porque seleccionar la actividad que termina primero permite iniciar otra actividad lo antes posible.

La única forma en que seleccionar la actividad que termina antes no sería la mejor opción sería si una actividad más tardía ofreciera una ventaja significativa, como prioridades o nuevas actividades desbloqueadas. Sin embargo, en este problema, cualquier actividad que pueda realizarse después de una actividad tardía también puede realizarse después de una actividad más corta. Además, entre la actividad corta y la tardía, pueden existir otras actividades que no se podrían realizar si se elige la actividad más tardía.

Por lo tanto, ordenar las actividades por su tiempo de finalización y seleccionar siempre la que termina primero garantiza una solución óptima.