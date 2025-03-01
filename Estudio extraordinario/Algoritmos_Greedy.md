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
