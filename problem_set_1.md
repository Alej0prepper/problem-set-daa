## Definiciones

- **La clase de complejidad P** corresponde a todos los problemas que pueden ser resueltos en tiempo polinomial.
- **La clase de complejidad NP** (viene de tiempo polinomial no-determinístico) corresponde a la clase de problemas cuya solución puede ser verificada en tiempo polinomial.

## Demostración de NP-completitud

Para demostrar que un problema es NP-completo se requieren dos pasos principales:

1. **Demostrar que el problema está en NP**:

   - Esto significa que, dada una solución candidata, podemos verificar en tiempo polinomial si esa solución es correcta.
2. **Demostrar que el problema es NP-duro**:

   - Esto significa que el problema es al menos tan difícil como cualquier otro problema en NP.
   - Se logra mostrando que un problema conocido como NP-completo se puede reducir en tiempo polinomial al problema en cuestión.

## Ejercicio 0: Demostrar que k-coloring es NP-completo (K≥3)

3-coloring es NP-completo

### Demostrar que está en NP

El problema de la k-coloración de grafos está en NP porque, dado un grafo G y k colores, un certificado de que la respuesta es "sí" es una asignación de colores a los vértices. Para verificar este certificado en tiempo polinomial, se puede comprobar que se utilizan como máximo k colores y que ningún par de nodos adyacentes (unidos por una arista) recibe el mismo color. Ambas verificaciones se pueden realizar en tiempo lineal respecto al número de vértices y aristas del grafo, lo que demuestra que el problema pertenece a la clase NP.

### Demostrar que es NP-duro mediante reducción desde 3-SAT

Al igual que otros problemas en esta sección, 3-Coloring es difícil de relacionar superficialmente con otros problemas NP-completos que hemos visto. Por lo tanto, vamos a reducirlo desde 3-SAT.

Dada una instancia arbitraria de 3-SAT con variables x₁,...,xₙ y cláusulas C₁,...,Cₖ, la reduciremos a una instancia de 3-coloring.

#### Construcción inicial del grafo G

El poder principal de 3-Coloring para codificar expresiones booleanas radica en que podemos asociar nodos del grafo con términos particulares, y al unirlos con aristas aseguramos que obtengan diferentes colores; esto se puede usar para establecer uno verdadero y otro falso.

1. Por cada variable xᵢ:

   - Creamos nodos vᵢ y v̄ᵢ (correspondientes a xᵢ y su negación)
   - Los unimos entre sí con una arista
   - Los unimos a un nodo especial "Base"
2. Creamos tres nodos especiales:

   - T (True/Verdadero)
   - F (False/Falso)
   - B (Base)
   - Los unimos formando un triángulo

![Grafo inicial con los nodos True, False, Base y los nodos de variables](images/3-colored-initial.png)

Esta construcción inicial garantiza las siguientes propiedades fundamentales:

a) En cualquier 3-coloración de G:

- Los nodos vᵢ y v̄ᵢ deben tener colores diferentes, y ambos diferentes de Base
- Los nodos True, False y Base deben obtener los tres colores en alguna permutación
- Podemos referirnos a los tres colores como color "Verdadero", "Falso" y "Base", según qué nodo especial recibe cada color
- Para cada i, uno de vᵢ o v̄ᵢ obtiene el color Verdadero y el otro el color Falso
- Consideraremos que la variable xᵢ está establecida en 1 si y solo si el nodo vᵢ recibe el color Verdadero

#### Construcción del subgrafo para las cláusulas

Para una cláusula como x₁ ∨ x₂ ∨ x₃, necesitamos que "al menos uno de los nodos v₁, v₂, o v₃ debe obtener el color Verdadero".

Para cada cláusula:

1. Creamos un subgrafo de 6 nodos que se conecta a:
   - Los tres nodos correspondientes a los literales de la cláusula
   - Los nodos True y False
2. Este subgrafo está diseñado de manera que:
   - Si los tres nodos de los literales tienen color Falso:
     * Los dos nodos inferiores deben recibir el color Base
     * Los tres nodos intermedios deben recibir, respectivamente, Falso, Base y Verdadero
     * Es imposible asignar un color válido al nodo superior
   - Si al menos uno de los nodos de los literales tiene color Verdadero:
     * Existe una forma válida de colorear todo el subgrafo

![Grafo con el subgrafo de 6 nodos añadido para una cláusula](images/3-colored-six-nodes-atttacht.png)

#### Demostración de la equivalencia

1. Si la instancia 3-SAT es satisfacible:
   a) Coloreamos Base, True y False arbitrariamente con los tres colores
   b) Para cada i:

   - Si xᵢ = 1, asignamos a vᵢ el color Verdadero y a v̄ᵢ el color Falso
   - Si xᵢ = 0, asignamos a vᵢ el color Falso y a v̄ᵢ el color Verdadero
     c) Como la asignación satisface todas las cláusulas, cada subgrafo de cláusula puede ser coloreado correctamente
2. Si el grafo G es 3-coloreable:
   a) En esta coloración, cada nodo vᵢ tiene asignado el color Verdadero o Falso
   b) Establecemos xᵢ = 1 si vᵢ tiene el color Verdadero, xᵢ = 0 en caso contrario
   c) Para cada cláusula:

   - Al menos uno de sus literales debe tener valor 1
   - Si no fuera así, los tres nodos correspondientes tendrían color Falso
   - Esto haría imposible colorear el subgrafo de la cláusula
   - Lo cual contradice que G sea 3-coloreable

### Extensión a k-coloring (k > 3)

Para demostrar que k-coloring es NP-completo para k > 3:

1. Tomamos una instancia de 3-coloring (grafo G)
2. Añadimos k-3 nuevos nodos
3. Conectamos estos nuevos nodos:
   - Entre sí formando un clique
   - Con todos los nodos originales de G
4. En el nuevo grafo G':
   - Si G es 3-coloreable:
     * Usamos 3 colores para G
     * Los k-3 nuevos nodos requieren k-3 colores diferentes
     * G' es k-coloreable
   - Si G' es k-coloreable:
     * Los k-3 nuevos nodos requieren k-3 colores diferentes
     * Quedan 3 colores para G
     * G debe ser 3-coloreable

Por lo tanto, k-coloring es NP-completo para todo k ≥ 3.

## Problema del número cromático

El número cromático de un grafo es el número mínimo de colores necesarios para colorear los vértices del grafo de manera que ningún par de vértices adyacentes (conectados por una arista) compartan el mismo color.

Matemáticamente, para un grafo G = (V, E), el número cromático (denotado como χ(G)) es el número más pequeño de colores que necesitamos para pintar todos los vértices de manera que ningún par de vértices conectados por una arista tengan el mismo color.

El problema consiste en encontrar el número cromático de un grafo.

### Pertenencia o no a NP:
No se conoce ningún algoritmo que permita determinar en tiempo polinomial para un k y un grafo si este k es su número cromático.

### Pertenencia a NP-Hard
Podemos asegurar la pertenencia de este problema al conjunto de problemas NP-hard porque podemos reducirlo polinomialmente desde 3-coloring, un problema que demostramos NP-completo anteriormente.

El problema del número cromático se puede interpretar como una generalización del problema de 3-coloreo, particularmente el caso en que el número cromático sea 3.
La entrada del problema del número cromático será la misma que la de 3-coloring, un grafo como una colección de nodos y aristas.

Y la salida del número cromático obtenemos la cantidad mínima de colores necesarios para colorear el grafo cumpliéndose la condición inicial de este problema, a continuación se muestra cómo se mapea esta solución al problema de 3-coloreo

* Si el número cromático es mayor que 3 o menor o igual a 3, entonces 3-coloring es true, esto ocurre por la propiedad de los grafos de que si son k-coloreables también serán C-coloreables con C>K
* En caso contrario ocurre que 3-coloring es false

### Luego
Resolver el problema del Número Cromático nos permite resolver el problema de 3-coloring por tanto este problema pertenece a la clase de problemas NP-duros pero no se puede asegurar la NP-completitud dado que no se conoce algoritmo que en tiempo polinomial verifique una solución de este problema. 


## El Problema del Clique Máximo

El objetivo es identificar el clique más grande dentro de un grafo dado. Este problema presenta particularidades interesantes desde la perspectiva de la complejidad computacional.

### Análisis de Complejidad

#### Pertenencia a NP

A diferencia de variantes como el problema k-Clique, no existe una demostración conocida que establezca la pertenencia del problema del clique máximo a la clase NP. Esto se debe a la naturaleza particular del problema y las limitaciones actuales en la teoría de la complejidad computacional.

#### Demostración de NP-Dureza

La NP-dureza del problema se establece mediante una reducción polinomial desde el problema k-Clique, que es NP-Completo.

##### Reducción desde k-Clique

La reducción se construye de la siguiente manera:

1. **Entrada**: Un grafo G = (V, E) y un entero k
2. **Transformación**: 
   - La entrada para el problema del clique máximo es simplemente el grafo G = (V, E)
   - Se resuelve el problema del clique máximo para obtener el clique más grande y su tamaño

3. **Conversión de la solución**:
   - Si el tamaño del clique máximo es mayor o igual que  k, entonces k-Clique es verdadero, ya que si existe un clique de tamaño t > k tambien existe un clique de tamaño k.
   - Si el tamaño del clique máximo es menor que k, entonces k-Clique es falso

##### Conclusión

Dado que k-Clique es NP-Completo y hemos establecido una reducción polinomial al problema del clique máximo, podemos concluir que el problema del clique máximo es NP-Duro.

## Cobertura de Clique

Dado un grafo $G = (V, E)$ , una cobertura de cliques es un conjunto de cliques $\left( C_1, C_2, \dots, C_k \right)$
 tal que cada arista $(u, v) \in E$ pertenece a al menos uno de estos cliques.

El objetivo del problema de cobertura de cliques es encontrar el número mínimo de cliques necesarios para cubrir todas las aristas del grafo.

### Pertenencia o no a NP
Dado un conjunto de cliques, es posible determinar en tiempo polinomial si en este conjunto están cubiertas todas las aristas del grafo.

### Pertenencia o no a NP-duro
Haremos una reducción desde el problema del número cromático. El problema del número cromático busca el número mínimo de colores necesarios tal que no haya dos nodos adyacentes con el mismo color. 

Podemos darnos cuenta de que un conjunto de nodos con el mismo color es un conjunto independiente de nodos, ya que son nodos que no son adyacentes. Luego, un conjunto de vértices de un grafo es un clique si y solo si el mismo conjunto de nodos en el grafo complementario es un conjunto independiente. Por lo tanto, si hallamos la menor cantidad de colores para el grafo complementario, hallamos a su vez la menor cantidad de cliques que abarquen todas las aristas del grafo original.

Dado un grafo, construimos el grafo complementario en tiempo polinomial. La entrada para el problema será $G^c$. Luego de resolver la cobertura de clique con $G^c$, obtenemos un \( k \) que coincide con el menor número de cliques necesarios para cubrir todas las aristas del grafo. Este número es equivalente a su número cromático. Así, resolver el problema de cobertura de clique nos permite conocer el número cromático de \( G \), completando su reducción.

Como el problema del número cromático es NP-completo, la cobertura de clique es NP-dura. Y como demostramos anteriormente que está en NP, la cobertura de clique es NP-completo.

## Conjunto Dominante 
## 6. Conjunto Dominante

Conjunto Dominante

En un grafo G = ( V , E ) , un conjunto de vértices D ⊆ V es un conjunto dominante si cada vértice de V que no está en D es adyacente a al menos un vértice en D .

Una partición de los vértices V en k conjuntos D 1 , D 2 , … , D k ​ es una partición domática si cada D i ​ (para i = 1 , 2 , … , k ) es un conjunto dominante. El numero dominante es la cardinalidad del menor conjunto dominante de G .

Hallar el numero dominante de G .

### Pertenencia a NP
Dado un conjunto D podemos verificar si "domina" a todos los vertices del grafo

### Pertenencia a NP-duro
haremos una reducción desde el problema de Vertex Cover que es un conocido problema NP-completo.
Construiremos un Grafo G' = (V',E') que cumplirá con lo siguiente:
    V' = contiene todos los vértices de V y, además, por cada arista (u,v) que pertenece a E, tendrá un nuevo vértice w 
    E' = incluye todas las aristas de E y, por cada arista (u,v), anadira al conjunto las aristas (u,w) y (w,v).

La construcción de este grafo se puede hacer en tiempo polinomial

Probemos en primera instancia que 
* S es un vertex cover de G => S es un conjunto dominante de G'

dado que S es un vertex cover de G, cada arista tiene al menos un extremo en S. Consideremos v que pertenece a G'. Si v es un nodo de G, entonces o v pertenece a S o existe una arista que conecta a v con un nodo u que pertenece a S, luego hay un nodo adyacente a v en S, entonces v está cubierto por algún elemento de S. Por otra parte, si w es un nodo adicional en G', entonces tiene dos nodos adyacentes u y v que pertenecen a G, por lo mismo, uno de ellos está en S, entonces los nodos adicionales también están cubiertos por S. Entonces, si G tiene un vertex cover => G' tendrá un conjunto dominante de al menos el mismo tamaño.

* D es un conjunto dominante de tamaño k en G' => en G existe un vertex cover de tamaño a lo sumo k

Si D es un conjunto dominante de tamaño k en G', consideremos todos los vértices adicionales w que pertenecen a D. Luego w está conectado solo a dos nodos, u y v, y podemos reemplazar a w de forma segura por v o u y seguir dominando a todos los vértices que w dominaba anteriormente, luego podemos eliminar todos los vértices adicionales de la forma descrita, así nos quedaría un conjunto D modificado que, por el mismo razonamiento, seguiría siendo un conjunto dominante, luego si G' tiene un conjunto dominante de tamaño k, entonces G tiene un vertex cover de a lo sumo tamaño k.

Luego, el problema del conjunto dominante pertenece a NP y a NP-duro, entonces es NP-completo.