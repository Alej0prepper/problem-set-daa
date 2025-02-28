# Greedy

## Criminal y policías

Javier es un criminal buscado, y $N$ policías están dispuestos a atraparlo. Los oficiales quieren capturar a Javier sin importar el costo, y Javier también quiere eliminar a la mayor cantidad de oficiales posible (preferentemente a todos) antes de ser atrapado (o antes de escapar después de eliminarlos a todos). Ni los oficiales ni Javier se retirarán antes de lograr sus objetivos.

Javier y los oficiales están en una cuadrícula unidimensional con coordenadas que van desde $-10^{10}$ hasta $10^{10}$. Javier está inicialmente en la coordenada $C$, y el $i$-ésimo oficial está inicialmente en la coordenada $P_i$. Los oficiales y Javier luego se turnan para moverse, siendo el equipo de oficiales el que se mueve primero.

Durante su turno, los oficiales tendrán que moverse a una celda adyacente desocupada uno por uno, en el orden que prefieran. Cada oficial tendrá que moverse. En cada momento del tiempo, ningún oficial puede estar en la misma celda que otro oficial, y tampoco puede estar en la misma celda que Javier. Si un oficial no puede moverse a una celda adyacente desocupada, será eliminado (y la celda en la que estaba se desocupa). Es importante notar que el equipo de oficiales intentará moverse de tal manera que se eliminen la menor cantidad posible de oficiales. Por ejemplo, con $P = [2, 3, 4]$ y $C = 6$, las siguientes posiciones posibles de los oficiales pueden ser $[1, 2, 3]$, $[1, 2, 5]$, $[1, 4, 5]$, o $[3, 4, 5]$. Sin embargo, con $P = [2, 3, 4]$ y $C = 5$, el único conjunto posible de las siguientes posiciones de los oficiales es $[1, 2, 3]$.

Después del turno del equipo de oficiales, Javier también se mueve a una celda adyacente desocupada o es atrapado si no puede encontrar ninguna celda adyacente desocupada. El proceso se repite hasta que Javier es atrapado o todos los oficiales son eliminados y Javier escapa.

Debes encontrar el número máximo de oficiales que pueden ser eliminados por Javier, y si Javier puede escapar o no.

Como recordatorio, dos celdas con coordenadas $X$ y $Y$ son adyacentes si y solo si $|X - Y| = 1$.

### Statement

Javier y $N$ oficiales de policía están parados en posiciones distintas en una cuadrícula unidimensional. Se mueven por turnos: primero, cada oficial se mueve un paso a la izquierda o a la derecha hacia un cuadrado desocupado, luego el Javier se mueve a la izquierda o a la derecha hacia un cuadrado desocupado. Un oficial que no puede moverse es eliminado, y si el Javier no puede moverse, es capturado. Encuentra el número máximo de oficiales que pueden ser eliminados.

### Solution

EXPLICACIÓN RÁPIDA

Si el conjunto ordenado de posiciones es $P_1 < P_2 < \dots < P_i < C < P_{i+1} < \dots < P_N$, Javier puede eliminar el prefijo más largo de oficiales comenzando en $i+1$ y el sufijo más largo terminando en $i$, tal que $C(\text{mod}2)\neq P_j(\text{mod}2)$.

EXPLICACIÓN:

Supongamos que Javier comienza en la posición $C$. Por ahora, concentremos nuestra atención solo en los oficiales cuyas posiciones iniciales son mayores que $C$ — el otro caso resulta ser simétrico.

Supongamos que tenemos $C < P_1 < P_2 < \dots < P_N$.

Una observación inicial es que la paridad relativa de $C$ y $P_i$ siempre se mantiene igual, es decir, si inicialmente tienen la misma paridad, después de cualquier conjunto de movimientos seguirán teniendo la misma paridad; y si inicialmente son diferentes, cualquier conjunto de movimientos los mantendrá distintos.

Ahora, miremos primero a $P_1$. Hay dos casos:

-**$C$ y $P_1$ tienen la misma paridad**

  En este caso, $P_1$ nunca puede ser eliminado — de hecho, ninguno de los oficiales puede ser eliminado.

    s**Prueba**

    Dado que tienen la misma paridad y deben comenzar en casillas distintas al inicio de cada turno de los oficiales, debemos tener$P_1\geq C +2$.

    Esto significa que$P_1$ siempre puede simplemente dar un paso hacia Javier independientemente de los movimientos de los otros oficiales, y en particular, nunca será eliminado.

    Además, debido a que$P_1$ siempre puede moverse hacia la izquierda hacia Javier, ese movimiento dejará al menos un espacio vacío para que $P_2$ también se mueva hacia la izquierda, lo que permite que $P_3$ se mueva hacia la izquierda, y así sucesivamente.

    Por lo tanto, cada oficial siempre tiene al menos un movimiento legal, lo que significa que ninguno de ellos puede ser eliminado.

-**$C$ y $P_1$ tienen diferente paridad**

  En este caso, $P_1$ siempre puede ser eliminado.

  **Prueba**

    Supongamos que$P_1 > C +1$. Entonces, $P_1\geq C +3$, por lo que, sin importar qué movimiento haga $P_1$, Javier siempre puede moverse un paso hacia la derecha.

    Así, la distancia entre Javier y$P_1$ o se mantiene igual, o disminuye en $2$ — en particular, no aumenta.

    ¿Qué pasa si$P_1 = C +1$?

    $P_1$ no tiene más opción que moverse hacia la derecha, lo que permite que Javier también se mueva hacia la derecha en su turno.

    Sin embargo, nuestra cuadrícula es finita, por lo que$P_1$ no puede moverse hacia la derecha indefinidamente.

    Por lo tanto, llegará un momento en que$P_1 = C +1$, pero $P_1+1, P_1+2, \dots, 10^{10}$ estarán ocupados por oficiales.

    Esto obligará a que$P_1$ sea eliminado, como se requiere.

Ahora que $P_1$ ha sido eliminado, veamos a $P_2$.

Si $P_2$ y $C$ tienen diferentes paridades, un argumento similar al anterior nos dice que $P_2$ también puede ser eliminado — ya sea después de eliminar a $P_1$ siguiendo la misma estrategia, o $P_2$ ya fue eliminado antes que $P_1$.

Por otro lado, si $P_2$ y $C$ tienen la misma paridad, nuestro primer argumento nos dice que $P_2$ nunca puede ser eliminado — y, por lo tanto, $P_i$ para $i \geq2$ nunca puede ser eliminado.

Esto nos lleva al siguiente resultado:

**Lema**: Sea $k$ el índice más pequeño tal que $\text{paridad}(C) = \text{paridad}(P_i)$. Entonces, cuando los oficiales se mueven de manera óptima, solo $P_1, P_2, \dots, P_{i-1}$ pueden ser eliminados, y ninguno más allá de eso.

La prueba sigue fácilmente de los procesos descritos anteriormente.

Por supuesto, el mismo resultado se aplica para los oficiales a la izquierda de Javier, es decir, algún sufijo de ellos con paridad diferente a la de $C$ puede ser eliminado, y ninguno más allá de eso.

Por lo tanto, tenemos nuestro algoritmo final:

1. Ordena el conjunto de oficiales.
2. Entre los oficiales a la derecha de Javier, elige el prefijo más largo tal que su paridad sea diferente a la de $C$.
3. Entre los oficiales a la izquierda de Javier, elige el sufijo más largo tal que su paridad sea diferente a la de $C$.
4. La respuesta es la suma de las dos cantidades anteriores.

Finalmente, Javier escapa si y solo si todos los oficiales son eliminados, así que imprime $1$ si todos los $N$ oficiales pueden ser eliminados y $-1$ en caso contrario.

**COMPLEJIDAD TEMPORAL:**

$O(N \log N)$
# Greedy

## Distancia de Árboles

Un árbol se define como un grafo conectado y no dirigido con $n$ vértices y $n - 1$ aristas. La distancia entre dos vértices en un árbol es igual al número de aristas en el camino simple único entre ellos.

Te dan dos enteros $x$ y $y$. Construye un árbol con las siguientes propiedades:

- El número de pares de vértices con una distancia par entre ellos es igual a $x$.
- El número de pares de vértices con una distancia impar entre ellos es igual a $y$.

Por un par de vértices, nos referimos a un par ordenado de dos vértices (posiblemente, el mismo o diferente).

### Statement

Te dan dos enteros $x$ y $y$. Tu tarea es construir un árbol con las siguientes propiedades:

- El número de pares de vértices con una distancia par entre ellos es igual a $x$.
- El número de pares de vértices con una distancia impar entre ellos es igual a $y$.

Por un par de vértices, nos referimos a un par ordenado de dos (posiblemente, el mismo o diferente) vértices.

### Solution

La primera observación básica que podemos hacer es que la suma de $x$ y $y$ debe ser un cuadrado perfecto.

¿Por qué?
Dado que cada vértice forma un par con cada otro vértice de un árbol, incluido él mismo, para cualquier árbol de $N$ vértices, el número total de pares ordenados de vértices será $N^2$.

Como la suma de $x$ y $y$ representa el número total de pares ordenados de vértices, esto debe ser un cuadrado perfecto. Por lo tanto, $x + y$ debe ser un cuadrado perfecto.

Ahora, debemos encontrar si es posible tener un árbol que tenga $x$ pares de vértices con una distancia par entre ellos y $y$ pares de vértices con una distancia impar entre ellos.

Está bastante claro que cualquier vértice del árbol puede estar en un nivel par o en un nivel impar. La raíz del árbol está en el nivel par ($0$ - indexado de manera base $0$). Veamos cuántos pares de vértices tienen una distancia impar entre ellos.

Teorema:
Cualquier par de vértices $(x, y)$ tiene una distancia impar entre ellos si los vértices $x$ y $y$ provienen de niveles de paridad opuesta.

Prueba
Supongamos que el vértice $x$ está en un nivel par y el vértice $y$ en un nivel impar. La distancia entre dos nodos se puede obtener en términos del menor ancestro común (lca). A continuación se muestra la fórmula para la misma:

$$
dis(x, y) = dis(root, x) + dis(root, y) - 2 \times dis(root, lca)
$$

Dado que $x$ está en un nivel par, $dis(root, x)$ es par, mientras que $y$ está en un nivel impar, por lo que $dis(root, y)$ es impar. Por lo tanto, podemos ver que:

$$
dis(x, y) = Par + Impar - Par
$$

Esto significa que si los vértices están en niveles de paridad opuesta, la distancia entre ellos es impar.

Cálculo de los pares de vértices con una distancia impar
Para las distancias impares, cada vértice en un nivel impar formará un par con cada vértice en un nivel par, y viceversa.

Supongamos que $[e_1, e_2, e_3, \dots, e_i]$ son los vértices en niveles pares, y $[o_1, o_2, o_3, \dots, o_j]$ son los vértices en niveles impares. Ahora, para cada vértice en un nivel par, formará un par con cada vértice en un nivel impar, y viceversa. Por lo tanto:

$$
Odd \ pairs' = (e_1 \times o_1 + e_1 \times o_2 + \dots + e_1 \times o_j + \dots + e_i \times o_1 + \dots + e_i \times o_j)
$$

$$
Odd \ pairs' = (e_1 + e_2 + e_3 + \dots + e_i) \times (o_1 + o_2 + o_3 + \dots + o_j)
$$

$$
Odd \ pairs' = E \times O
$$

Donde $E$ y $O$ representan el número de nodos en niveles pares e impares, respectivamente.

Dado que estamos considerando pares ordenados, el número de estos pares se duplicará. Si $(x, y)$ es un par con una distancia impar entre ellos, entonces $(y, x)$ también tendrá una distancia impar. Por lo tanto:

$$
Odd \ pairs = 2 \times E \times O
$$

Esto significa que solo nos importa el número de vértices en niveles pares e impares. La raíz es el único nodo en el nivel $0$, y si queremos más nodos en un nivel par, debe existir al menos un vértice en un nivel impar. Ahora podemos verificar todas las posibilidades y encontrar si existe una disposición de vértices que satisfaga $x$ y $y$ según el problema. Si es así, podemos construir y mostrar el árbol.

COMPLEJIDAD TEMPORAL:
$O(\sqrt{X + Y})$




# DP

## Tramposo

Leandro es profesor de programación. En sus ratos libres, le gusta divertirse con las estadísticas de sus pobres estudiantes reprobados. Los estudiantes están separados en $n$ grupos. Casualmente, este año, todos los estudiantes reprobaron alguno de los dos exámenes finales: $P$ (POO) y $R$ (Recursividad).

Esta tarde, Leandro decide entretenerse separando a los estudiantes suspensos en conjuntos de tamaño $k$ que cumplan lo siguiente: En un mismo conjunto, todos los estudiantes son del mismo grupo $i$ ($1 \leq i \leq n$) o suspendieron por el mismo examen $P$ o $R$.

Conociendo el grupo y la prueba suspendida de cada estudiante, y el tamaño de los conjuntos, ayude a Leandro a saber cuántos conjuntos de estudiantes suspensos puede formar.

### Statement

Dado que hay $n$ arbustos, cada uno con $a_i$ bayas rojas y $b_i$ bayas azules, y cada canasta puede contener $k$ bayas, pero cada canasta solo puede contener bayas del mismo arbusto o bayas del mismo color (rojo o azul):

Determina el número máximo de canastas que se puede llenar completamente.

### Solution

Solución 1:

No existe una solución ávida obvia, por lo que intentaremos la programación dinámica. Sea $dp[i][j]$ un arreglo booleano que indica si podemos tener $j$ bayas rojas extra después de considerar los primeros $i$ arbustos. Una baya es extra si no se coloca en una canasta llena (de cualquier tipo). Ten en cuenta que si sabemos que hay $j$ bayas rojas extra, también podemos calcular fácilmente cuántas bayas azules extra hay. Nota que podemos elegir nunca tener más de $k-1$ bayas rojas extra, porque de lo contrario podemos llenar alguna cantidad de canastas con ellas.

Para la transición del arbusto $i-1$ al arbusto $i$, recorremos todos los posibles valores $l$ desde $0$ hasta $\min(k-1, a_i)$ y verificamos si podemos dejar $l$ bayas rojas extra del arbusto actual $i$. Para algunos $i$ y $j$, podemos dejar $l$ bayas rojas extra y poner las bayas rojas restantes en canastas, posiblemente con bayas azules del mismo arbusto si $(a_i - l) \mod k + b_i \geq k$. El razonamiento para esto es el siguiente:

En primer lugar, estamos dejando $l$ bayas rojas (o al menos intentándolo). Mostramos que de este arbusto, habrá como máximo una canasta que contenga tanto bayas rojas como azules (todas de este arbusto). Para colocar las bayas rojas restantes en canastas llenas, cuantas más bayas azules tengamos, mejor. Es óptimo colocar las bayas rojas restantes $a_i - l$ en sus propias canastas separadas antes de fusionarlas con las bayas azules (de esta manera se requieren menos bayas azules para satisfacer la condición). Luego, si $(a_i - l) \mod k + b_i$ es al menos $k$, podemos llenar alguna canasta con las bayas rojas restantes y posiblemente algunas bayas azules. Recuerda que no nos importa cuántas bayas azules extra dejamos porque eso está determinado de manera única por la cantidad de bayas rojas extra.

También observa que siempre podemos dejar $a_i \mod k$ bayas rojas extra.

Denota el número total de bayas como $t$. La respuesta será el máximo sobre todos los $(t-j)/k$ tales que $dp[n][j]$ es verdadero, $0 \leq j \leq k-1$.

Solución 2:

Usamos programación dinámica. Sea $dp[i][j]$ verdadero si, después de considerar los primeros $i$ arbustos, $j$ es el número de bayas rojas en canastas heterogéneas módulo $k$. Las canastas heterogéneas contienen bayas del mismo arbusto, y las canastas homogéneas contienen bayas del mismo tipo.

Supongamos que conocemos el número de bayas rojas en canastas heterogéneas módulo $k$. Esto determina el número de bayas azules en canastas heterogéneas módulo $k$. Dado que el número de bayas rojas en canastas homogéneas es un múltiplo de $k$, también determina el número de bayas rojas que no están en ninguna canasta (podemos asumir de manera segura que es menos de $k$, ya que de lo contrario podemos formar otra canasta). De manera similar, podemos determinar el número de bayas azules que no están en ninguna canasta, y así deducir el número de canastas.

Para calcular los posibles números de bayas rojas en canastas heterogéneas módulo $k$, basta con observar cada arbusto por separado y determinar los posibles números de bayas rojas módulo $k$ en canastas heterogéneas para ese arbusto. Si hay más de una canasta heterogénea para un arbusto, podemos reorganizar las bayas para dejar como máximo una heterogénea. Ahora tenemos dos casos. Si no hay canastas heterogéneas, el número de bayas rojas en esas canastas es obviamente cero. Si hay una canasta heterogénea, sea $x$ el número de bayas rojas en ella y $k-x$ el número de bayas azules en ella. Claramente, $0 \leq x \leq a_i$ y $0 \leq k - x \leq b_i$. Reorganizando, obtenemos $\max(0, k - b_i) \leq x \leq \min(a_i, k)$. Estos corresponden a las transiciones para nuestra programación dinámica.

COMPLEJIDAD TEMPORAL:
$O(nk^2)$

# DP

## MEX Subsecuencia

Daniel tiene un array
$a_1, a_2, \dots, a_N$. Necesita encontrar el número de formas de dividir el array en subarrays contiguos tal que:

- Cada elemento de la secuencia $a$ pertenezca exactamente a uno de los subarrays.
- Existe un número entero $m$ tal que el MEX de cada subarray sea igual a $m$. El MEX de una secuencia es el menor número entero no negativo que no aparece en dicha secuencia.

Ayuda a Daniel con esta tarea.

### Statement

Te dan un arreglo de $N$ enteros como $A_1, A_2, A_3, \dots, A_N$. Tu tarea es encontrar el número de formas de dividir el arreglo en subarreglos contiguos tales que:

1. Cada elemento del arreglo dado $A$ pertenezca exactamente a uno de los subarreglos.
2. Existe un entero $m$, tal que el $MEX$ de cada subarreglo es igual a $m$.

El $MEX$ de una secuencia es el menor entero no negativo que no aparece en la secuencia.

### Solution

EXPLICACIÓN RÁPIDA:
Podemos notar que el MEX($m$) es siempre único a lo largo de todo el proceso y es igual al MEX del array dado.

Cualquier subarray de este array es válido solamente cuando el MEX de ese subarray es igual al MEX del array dado.

Podemos usar un enfoque de programación dinámica para encontrar el número de formas de dividir el array en subarrays contiguos de manera que el MEX de cada subarray sea $m$.

El estado de DP se representa como $(x)$, representando el número de formas de dividir un array de longitud $x$, tal que el MEX de cada subarray sea $m$.

El estado de DP se calcula en orden de $1$ a $N$, y el número de formas se calcula en consecuencia.

Finalmente, se debe imprimir el número de formas para la secuencia de longitud $N$.

EXPLICACIÓN:
Se nos da un array de $N$ enteros como $A_1, A_2, A_3, \dots, A_N$. Nuestra tarea es encontrar el número de formas de dividir el array en subarrays contiguos de manera que el MEX de cada subarray sea el mismo, es decir, $m$.

La primera observación que podemos hacer es que el MEX es siempre único a lo largo de todo el proceso y es igual al MEX del array dado.

Prueba:
Ahora, pasemos a la programación dinámica.

Definamos nuestro DP como $(y)$, que se define de la siguiente manera:

DP$(y)$ se define como el número de formas de dividir un array de longitud $y$ en subarrays contiguos de manera que el MEX de cada subarray sea el mismo y sea igual a $m$. Ahora nuestro objetivo es encontrar los subarrays cuyo MEX sea igual a $m$, lo cual se puede hacer encontrando subarrays donde estén presentes todos los enteros menores que $m$.

Establecemos, $DP[0] = 1$.

Ahora, encontraremos el subarray de longitud mínima tal que este subarray contenga todos los enteros menores que $m$. Por lo tanto, el MEX de este subarray es $m$. Supongamos que tenemos dicho subarray, llamado $S$.

$A_1, A_2, \dots, A_x, A_{x+1}, A_{x+2}, \dots, A_y$

$S = [A_{x+1}, A_{x+2}, \dots, A_y]$

Aquí, $S$ es el subarray cuyo MEX es igual a $m$. Esto significa que si dividimos el array antes de $x$, entonces el MEX seguirá siendo $m$. Por lo tanto, podemos dividir el array de la siguiente manera:

$[A_1][A_2, A_3, \dots, A_y]$

$[A_1, A_2][A_3, \dots, A_Y]$

$\dots$

$[A_1, A_2, \dots, A_x][A_{x+1}, A_{x+2}, \dots, A_y]$

Dado que estamos seguros de que el último subarray tendrá un MEX igual a $m$, y ya hemos calculado el número de formas de dividir un array de longitud menor a $x$ tal que el MEX sea $m$, la expresión matemática para el DP será:

$DP[y] = \sum_{i=0}^{x} DP[i]$

Donde $DP[i]$ se define como el número de formas de dividir un array de longitud $i$ tal que el MEX sea $m$.

Podemos usar la suma de prefijos para precomputar la suma de todos los $DP[i]$ para longitudes menores a $x$, cuando llegamos a la longitud $x$ del array dado.

Nuestra respuesta será el número de formas de dividir un array de longitud $N$ en subarrays contiguos tal que el MEX de cada subarray sea $m$. Esto estará representado por $DP[N]$.

COMPLEJIDAD TEMPORAL:
$O(N)$ por caso de prueba.

## Subsecuencia Buena

Supongamos que tienes un array binario $B$ de longitud $N$. Una secuencia $x_1, x_2, \dots, x_k$ se llama buena con respecto a $B$ si satisface las siguientes condiciones:

- $1 \leq x_1 < x_2 < \dots < x_k \leq N + 1$
- Para cada par $(i, j)$ tal que $1 \leq i < j \leq k$, el subarray $B[x_i : x_j - 1]$ contiene $(j - i)$ unos más que ceros. Es decir, si $B[x_i : x_j - 1]$ contiene $c_1$ unos y $c_0$ ceros, entonces se debe cumplir que $c_1 - c_0 = j - i$.

Aquí, $B[L : R]$ denota el subarray que consiste en los elementos $[B_L, B_{L + 1}, B_{L + 2}, \dots, B_R]$. Nota que, en particular, una secuencia de tamaño $1$ siempre es buena.

Por ejemplo, supongamos que $B = [0, 1, 1, 0, 1, 1]$. Entonces:

- La secuencia $[1, 4, 7]$ es una secuencia buena. Los subarrays que necesitan ser revisados son $B[1 : 3]$, $B[1 : 6]$ y $B[4 : 6]$, que todos cumplen con la condición.
- La secuencia $[1, 5]$ no es buena, porque $B[1 : 4] = [0, 1, 1, 0]$ contiene un número igual de ceros y unos (cuando debería contener un $1$ extra).

Alice le dio a Bob un array binario $A$ de tamaño $N$ y le pidió que encontrara la secuencia más larga que sea buena con respecto a $A$. Ayuda a Bob a encontrar una de estas secuencias.

Si existen múltiples secuencias más largas posibles, puedes imprimir cualquiera de ellas.

### Statement 2

Dado un arreglo binario $A$, encuentra la secuencia buena más larga $x_1, x_2, \dots, x_k$ tal que satisface:

$1 \leq x_1 < x_2 < \dots < x_k \leq N + 1$

$A[x_i : x_j - 1]$ contiene un número igual de ceros y unos para cada $i < j$.

### Solution 2

Primero, note que es suficiente asegurar que $A[x_i : x_{i+1} - 1]$ (es decir, el subarreglo entre elementos consecutivos) satisfaga la condición, es decir, contiene un uno extra.

Prueba
Esto no es difícil de ver. El subarreglo $A[x_i : x_j - 1]$ se puede pensar como la concatenación de $A[x_i : x_{i+1} - 1], A[x_{i+1} : x_{i+2} - 1], \dots, A[x_{j-1}, x_j - 1]$. Note que hay $j - i$ subarreglos de este tipo.

Si cada uno de estos contiene un uno extra, por supuesto, todos juntos tendrán exactamente $j - i$ unos extra.

Ahora, usemos un pequeño truco: reemplace cada $0$ en el arreglo con $-1$. Llamemos al arreglo obtenido de esta manera $B$. Por ejemplo, si $A = [0, 1, 1, 0, 1]$, entonces $B = [-1, 1, 1, -1, 1]$.

Observe que "A[L:R] contiene un uno extra" se traduce a "B[L:R] tiene una suma de $1$" en el nuevo arreglo, lo cual es mucho más fácil de manejar.

Dado que estamos tratando con sumas de subarreglos, es natural pensar en sumas prefixadas. Entonces, sea $P_i = B_1 + B_2 + \dots + B_i$ (con $P_0 = 0$) denotando el arreglo de sumas prefixadas de $B$.

Ahora, para que $B[L:R]$ tenga una suma de $1$, debemos tener $P_R - P_{L-1} = 1$, o $P_R = P_{L-1} + 1$.

Aplicando esto a la definición de una secuencia buena, vemos que debemos tener $P_{x_{i+1} - 1} = P_{x_i - 1} + 1$ para cada $1 \leq i < k$. En otras palabras, necesitamos elegir una secuencia de índices cuyas sumas prefixadas sean $k, k + 1, k + 2, \dots$ para algún valor de $k$.

La secuencia buena más larga, por lo tanto, corresponde a la secuencia más larga de sumas prefixadas de esta forma.

Esto se puede calcular usando programación dinámica.

Sea $dp_i$ la longitud de la secuencia más larga de sumas prefixadas que termina en la posición $i$ y que satisface la condición anterior. Las transiciones para un índice dado son fáciles de calcular en $O(N)$. Simplemente tenemos $dp_i = 1 + \max(dp_j)$ en todos los $j < i$ tales que $P_j + 1 = P_i$.

Sin embargo, hacer esta computación $O(N)$ para cada índice es demasiado lento, necesitamos acelerarlo un poco. Esto se puede hacer observando que solo nos importan aquellos índices cuyos valores $P_j$ sean iguales a $P_i - 1$; de hecho, solo nos importa el valor máximo de $dp_j$ entre estos índices.

Así que, mantengamos otro arreglo $mx$, donde $mx[x]$ es el valor más grande de $dp_i$ en todos los índices $i$ tales que $P_i = x$. Inicialmente, lo inicializamos a todos ceros.

Luego, para cada $i$ desde $0$ hasta $N$,

$dp_i = 1 + mx[P_i]$

$mx[P_i] = \max(dp_i, mx[P_i])$

El elemento máximo de $dp$ es la respuesta final.

Reconstituir una secuencia válida no es difícil, cuando se realiza el $dp$, se mantiene un enlace al elemento anterior en la secuencia, luego se siguen estos en reversa al final.

COMPLEJIDAD TEMPORAL:

$O(N)$ por caso de prueba.

# Grafos

## PCC

Han pasado 20 años desde que Lázaro se graduó de Ciencias de la Computación  
(haciendo una muy buena tesis) y las vueltas de la vida lo llevaron a convertirse  
en el presidente del Partido Comunista de Cuba. Una de sus muchas responsabilidades  
consiste en visitar zonas remotas. En esta ocasión debe visitar una  
ciudad campestre de Pinar del Río.

También han pasado 20 años desde que Marié consiguió su título en MATCOM.  
Tras años de viaje por las grandes metrópolis del mundo, en algún punto  
decidió que prefería vivir una vida tranquila, aislada de la urbanización, en una  
tranquila ciudad de Pinar del Río. Las vueltas de la vida quisieron que precisamente  
Marié fuera la única universitaria habitando la ciudad que Lázaro se  
dispone a visitar.

Los habitantes de la zona entraron en pánico ante la visita de una figura tan  
importante y decidieron reparar las calles de la ciudad por las que transitaría  
Lázaro. El problema está en que nadie sabía qué ruta tomaría el presidente y  
decidieron pedirle ayuda a Marié.

La ciudad tiene $n$ puntos importantes, unidos entre sí por calles cuyos  
tamaños se conoce. Se sabe que Lázaro comenzará en alguno de esos puntos  
($s$) y terminará el viaje en otro ($t$). Los ciudadanos quieren saber, para  
cada par $s$, $t$, cuántas calles participan en algún camino de distancia mínima  
entre $s$ y $t$.

### Statement

Dado un país con n ciudades y m caminos. Cada camino conecta un par de ciudades distintas y es bidireccional. Entre cualquier par de ciudades, como máximo hay un camino. Para cada camino, se conoce su longitud.

Sabemos que el Presidente pronto viajará desde la ciudad s hasta la ciudad t y elegirá uno de los caminos más cortos de s a t, pero no se sabe cuál camino escogerá.

se desea reparar los caminos en las posibles rutas del Presidente.

Para todos los pares distintos s, t (s < t), encuentra el número de caminos que están en al menos un camino más corto entre s y t.

### Solution

Necesitamos contar la cantidad de aristas en todos los caminos más cortos entre cada par de vértices. Hagamos algo más sencillo primero: en lugar de contar todas las aristas, contaremos solo aquellas que tienen el vértice de destino en su lado. Por ejemplo, estas son las aristas que pertenecen a los caminos más cortos desde 4 a 2 que están conectadas al vértice 2:

Denotemos este número de la siguiente manera: inEdgessource, v — número de aristas que llegan al vértice v en algún camino más corto desde el vértice fuente al vértice v. En el ejemplo dado, inEdges4, 2 = 3. También denotemos el conjunto Ssource, dest — es el conjunto de los vértices que pertenecen a al menos un camino más corto desde source a dest. Por ejemplo, S4, 2 = {1, 2, 3, 4}. Con estas dos variables se puede ver que la respuesta para los vértices source y dest será:

$Edges(s,d) = \sum_{v \in S_{s,d}} InEdges(s,v)$

En otras palabras, la respuesta para los vértices s y d será igual a la suma de inEdgess, v para todos los vértices v que pertenecen a algún camino más corto de s a d. Entonces, lo único que queda es calcular estos S y inEdges. Ambos se pueden calcular fácilmente si se tienen las distancias mínimas entre todos los pares de vértices. Y estas distancias se pueden calcular utilizando el algoritmo de Floyd-Warshall. Por lo tanto, la solución completa es:

1. Calcular las distancias mínimas entre todos los pares de vértices utilizando el algoritmo de Floyd-Warshall.

2. Contar inEdges. Simplemente itera sobre todos los vértices fuente y todas las aristas. Para cada arista, verifica si alguno de sus extremos pertenece a algún camino más corto desde la fuente.

3. Calcular la respuesta. Utiliza tres ciclos para iterar sobre los vértices: fuente, destino y mid. Los primeros dos vértices son aquellos para los cuales estamos calculando la respuesta. El tercer vértice es el vértice que debería pertenecer a algún camino más corto (básicamente estamos verificando si v pertenece a Ssource, dest). Si mid pertenece a algún camino más corto de source a dest, entonces sumamos inEdgessource, mid a la respuesta.

Cada paso tiene una complejidad de O(n^3).

COMPLEJIDAD TEMPORAL:
O(n^3)

# Grafos

## Ciudades

El país de Berland tiene inicialmente $N$ ciudades aisladas, donde la $i$-ésima ciudad tiene una significancia de $A_i$. El Presidente de Berland quiere conectar todas las ciudades. Él puede construir una carretera bidireccional de longitud $L$ $(L > 0)$ desde la ciudad $X$ a la ciudad $Y$ si $(A_X \& A_Y \& L) = L$, donde $ \& $ representa el operador AND bit a bit.

¿Cuál es la longitud total mínima de las carreteras que tiene que construir para conectar todas las ciudades en Berland? Imprime $-1$ si es imposible.

Nota:

Se dice que la ciudad $X$ y la ciudad $Y$ están conectadas si existe una secuencia de ciudades $C_1, C_2, \dots, C_K$ $(K \geq 1)$ tal que $C_1 = X$, $C_K = Y$, y existe una carretera desde $C_i$ a $C_{i+1}$ $(1 \leq i < K)$. Todas las ciudades en Berland se dicen conectadas cuando cada par de ciudades en Berland está conectado.

### Statement

Dado $N$ vértices donde el $i$-ésimo tiene un valor $A_i$, puedes dibujar una arista entre $u$ y $v$ de longitud $L$ si $L$ es una submáscara tanto de $A_u$ como de $A_v$.

Encuentra el costo mínimo para conectar todas las ciudades, o indica si es imposible hacerlo.

### Solution

Por el momento, supongamos que podemos conectar todos los $N$ vértices. Hagamos un par de observaciones:

1. El grafo final va a ser un árbol.
2. Cualquier arista $L$ en el grafo final tendrá una longitud que es una potencia de $2$, es decir, $L = 2^k$ para algún $k \geq 0$.

Demostración:

El primer punto debería ser obvio: si tenemos un ciclo, podemos eliminar alguna arista de él para obtener un costo estrictamente menor mientras preservamos la conectividad.

El segundo punto tampoco es difícil de ver: si una longitud contiene más de un bit activado, eliminar cualquier bit activado en ella aún la mantendrá como una arista válida, pero reducirá el costo.

Esto nos da inmediatamente una solución, aunque lenta:
Considera el (multi)grafo $G$ en $N$ vértices, donde para cada $(u, v, k)$ hay una arista entre $u$ y $v$ de longitud $2^k$ si $u$ y $v$ tienen ambos el $k$-ésimo bit activado.
Nuestra respuesta no es más que el peso del árbol de expansión mínima (MST) de este grafo.

Sin embargo, este grafo puede tener hasta $30 \cdot N^2$ aristas, y calcularlas todas es obviamente imposible, por lo que necesitamos hacerlo mejor.

Para optimizar esto, veamos cómo funcionaría el algoritmo de Kruskal para el MST en este grafo:

- Primero, considerará todas las aristas con peso $2^0$.
- Luego, considerará todas las aristas con peso $2^1$.
- Luego, considerará todas las aristas con peso $2^2$.
- Y así sucesivamente...

¿Qué tiene de especial esto?

Sea $x_1 < x_2 < \dots < x_m$ todos los vértices con el $k$-ésimo bit activado. Entonces, las aristas con peso $2^k$ son exactamente todos los pares de estos $m$ vértices.

Ahora, supongamos que encontramos $x_1, \dots, x_m$ para un $k$ fijo.
No necesitamos considerar todos los pares de estos $m$ vértices: simplemente necesitamos mantener suficientes aristas para conectarlos todos. La forma más sencilla de hacer esto es considerar solo las aristas $(x_1, x_2), (x_2, x_3), \dots, (x_{m-1}, x_m)$.

Observa que hacer esto reduce inmediatamente el número de aristas a $< N$ por bit, para un total de $< 30 \cdot N$ aristas en total. Esto es lo suficientemente pequeño como para que podamos ejecutar un algoritmo de MST en estas aristas directamente y obtener la respuesta.

Nota:
Si el grafo final que obtenemos no está conectado, la respuesta es $-1$, ya que no hay forma de conectarlo.

COMPLEJIDAD TEMPORAL:
O(n^3)
