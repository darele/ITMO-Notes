# Repaso para Examen de algo

Things to study

Euler path

Korasaju

BFS proof of work

# Table of Contents
1. [1. DFS](#depth-first-search) 
2. &emsp;[1.1 DFS](#11-dfs)
3. &emsp;[1.2 Topological Sort](#12-topological-sort)
4. [2. Advanced DFS](#advanced-dfs)
5. &emsp;[2.1 Finding Bridges and Articulation Points](#21-finding-bridges-and-articulation-points)
6. &emsp;[2.3 Korasaju's Algorithm !](#23-korasajus-algorithm)
7. &emsp;[2.4 Counter-Examples of Korasaju's Algorithm !](#24-counter-examples-to-korasajus-algorithm)
7. &emsp;[2.6 Eulerian graphs !](#26-eulerian-graphs-criteria-and-algorithm-for-finding-euler-cycle)
8. [3. BFS](#3-breadth-first-search)
9. &emsp;[3.1 Base Algorithm !](#31-base-algorithm-bfs-proof-of-correctness)
10. &emsp;[3.2 (0-k) BFS](#32-0-1-bfs-0-k-bfs)
11. &emsp;[3.3 Djikstra's algorithm](#33-djikstras-algorithm)
12. &emsp;[3.4 Bellman Ford](#34-bellman-fords-algorithm)
13. &emsp;[3.5 Floyd-Warshall](#35-floyd-warshalls-algorithm)
14. &emsp;[3.6 Negative cycle finding](#36-negative-cycle-detection)
3. [Hungarian Algorithm](#algoritmo-hungariano)

# Depth-First Search

## 1.1 DFS

- Base Algorithm

    ```
        dfs(v):
            vis[v] = true
            for (u in g[v]):
                if (!vis[u]):
                    dfs(u);

        call_dfs():
            for (i = 1 .. n):
                if (!vis[i]):
                    dfs(i)
    ```
    I. e. we recursively check all possible paths, but never go through the same portion of a path more than once.

- Finding Connected Components

    Just run an usual DFS, all vertices marked as visited, belong to a single connected component, then for all non-visited vertices, repeat the algorithm untill all vertices had been visited.
    

- Cycle finding

    - Undirected Graph.

        Use DFS from every unvisited node. Depth First Traversal can be used to detect a cycle in a Graph. There is a cycle in a graph only if there is a back edge present in the graph. A back edge is an edge that is indirectly joining a node to itself (self-loop) or one of its ancestors in the tree produced by DFS. 

        To find the back edge to any of its ancestors keep a visited array and if there is a back edge to any visited node then there is a loop and return true.

    - Directed Graph.

        We color the vertices in three colors, white if has not already been seen, in the DFS execution, gray if it is in the recursion stack now, and black if it has already been visited. If we find a gray vertex, then we have found a cycle.

- Bipartite check

    We will have an array of colors, and an array of visited, so we can check if a vertex is visited and what color it has. We will start with a vertex, and color it with one color, then we will run DFS on all of its neighbors, and color them with the other color, and so on. If we find a vertex that has already been visited, and it has the same color as the current one, then we have found an odd cycle, and the graph is not bipartite.

    [Back to Table of Contents](#table-of-contents)

## 1.2 Topological sort

- With stack.

    We will run DFS on the graph, and when we exit from the recursive call, we will insert the vertex in a stack. Then, we will print the stack.  
    It works for the same reason as the algorithm for SCC, because whenever we push a vertex to the stack, all of its neighbors have already been visited, 
    so in reverse order, it will appear before any neighbor.  
    This is the same as keeping track of departure time and printing all vertices in
    decreasing order of departure time.  

    - Proof of correctness.
    
        let $f(x)$ be the position of a vertex $x$ in the topological order.
        We will prove that $\forall{(x, y) \in E}, f(x) > f(y)$ if and only if $d(x) > d(y)$, where $d(x)$ is departure (exit) time.  
        If $d(x) > d(y)$, then $f(x) > f(y)$ because of parentheses theorem ($x$ has a greater exit time, then it is an ancestor of $y$ and the theorem states that the discovery time of descendants is always greater).  
        If $f(x) > f(y)$, There is a path from $x$ to $y$ (because of the definition of topological sorting), then we should have exited from $y$ before $x$ then $d(x) > d(y) $.




- With queue.

    We will keep track of the indegree of every vertex, and we will insert in a queue all the vertices with indegree 0. Then, we will take the first vertex in the queue, and for every neighbor of that vertex, we will decrease its indegree by 1, and if the indegree of that neighbor becomes 0, we will insert it in the queue. We will repeat this process until the queue is empty.

- Example tasks

    1. Scheduling depending jobs (like order of compilation).  
    2. Coloring of a graph.  
    3. Finding longest path in a DAG (find a toposort, and then run over it, and for every non-assigned vertex, assign a distance of $0$, and for all of its neighbors, assign $max(d[u], d[v] + 1)$).
    4. Finding the number of paths from $s$ to $t$ in a DAG.
    5. Finding the number of paths from $s$ to $t$ in a DAG with weights.  
    6. Finding the minimum path from $s$ to $t$ in a DAG with weights.

    [Back to Table of Contents](#table-of-contents)

# 2. Advanced DFS

- ## 2.1 Finding Bridges and Articulation points

    Save for every vertex its discovery time $d[v]$, and its lowest discovery time of any of its neighbors. it is, when visiting a vertex $v$, if one of its neighbors $u$ has already been visited, we will update $min[v] = min(d[u], min[v])$.
    
    A vertex is an articulation point, if $min[v] >= d[u]$, i.e. from its descendants in the dfs tree, there is not a back edge (since the minimum discovery time that could be found corresponds at least to the studied point).

    A vertex $v$ is the end of the bridge $(u,v), if $min(min[v], min[u]) >= max(d[u], d[v])$

    [Back to Table of Contents](#table-of-contents)
    
- ## 2.3 Korasaju's algorithm

    1. After the recursive call of DFS, let's insert in a stack the corresponding vertex, then we will have a stack with the vertices in the order of their exit time from the recursive call.  

    ![Example graph with two SCCs](img/SCC.png)

    In the above graph, the final queue looks like: $0,1, 2, 4, 3, 0$  
    
    2. Now we will run DFS on the transposed graph, taking vertices from stack one by one, and we will go to the next vertex in the stack after the recursive call (if it has been visited, do nothing). We will also keep track of the number of vertices in the current component. If we reach a vertex that has already been visited, we will start a new component (a gray vertex, in case of finding a black vertex, do nothing).  

    Why does it work? Basically, because we add the vertex to the stack only when it has already gone recursively to all of its neighbors, we guarantee that a vertex that connects a component to another one, will be added to the stack after all the vertices of the component that it connects to, then, since we are taking the vertices according to the stack, we can guarantee that if a vertex connects to another component in this transposed graph, that component will have been visited before the current one.

    [Back to Table of Contents](#table-of-contents)

- ## 2.4 Counter-Examples to Korasaju's Algorithm
    
    - ### Not using the transpose graph.

        ![A graph in which Korasaju's algorithm does not work if the transpose graph is not used](img/Korasaju%201.jpg)

        The idea of Korasaju's algorithm when the stack has been created, is to run DFS and whenever a visited vertex is found (a gray vertex), start a new component, in which we will introduce all reachable vertices in that run of the DFS, since it is guaranteed that all vertices that are already black, do not belong to the component.  
        For this graph, if we apply the same strategy, we will insert the vertices in component 2 as part of component 1, which is not true.

    - ### Using arrival time instead of departure time

        Here any graph with more than one SCC can be drawn, let's take the graph in the last point for example, assuming we start first DFS in the left component, here the last vertex in the stack will be some vertex in the right component.  
        Then when using the transpose graph, we will visit all vertices and in total we get only one component, which is not true.


    - ### Sorting vertices in the opposite order

        If we sort the vertices in opposite order we guarantee that the vertices that were visited first in the DFS will appear last in our stack, then, in the transpose we when taking the first vertex, we will run a DFS that visits all SCC (as all reachable components are marked white), they will be marked as one whole component which is not true.

    [Back to Table of Contents](#table-of-contents)

- ## 2.6 Eulerian graph's criteria and algorithm for finding euler cycle.

    - Criterium for Eulerian graphs.

        - An undirected graph has an Eulerian cycle if and only if every vertex has even degree, and all of its vertices with nonzero degree belong to a single connected component.

        - An undirected graph has an Eulerian trail if and only if exactly zero or two vertices have odd degree, and all of its vertices with nonzero degree belong to a single connected component

        - A directed graph has an Eulerian cycle if and only if every vertex has equal in degree and out degree, and all of its vertices with nonzero degree belong to a single strongly connected component.

        - A directed graph has an Eulerian trail if and only if at most one vertex has (out-degree) − (in-degree) = 1, at most one vertex has (in-degree) − (out-degree) = 1, every other vertex has equal in-degree and out-degree, and all of its vertices with nonzero degree belong to a single connected component of the underlying undirected graph.  

        All of this criteria can be proved by contradiction (let's assume that some edge is not included in the cycle, then we note that we cannot form a cycle, since the parity of the degree of the two ends of the given edge has been changed).

    - Finding Eulerian Path in $\mathcal{O}(n)$

        ```
            procedure FindEulerPath(V)
            1. iterate through all the edges outgoing from vertex V;
                remove this edge from the graph,
                and call FindEulerPath from the second end of this edge;
            2. add vertex V to the answer.
        ```

        An equivalent algorithm is

        ```
            stack St;
            put start vertex in St;
            until St is empty
                let V be the value at the top of St;
                if degree(V) = 0, then
                    add V to the answer;
                    remove V from the top of St;
                otherwise
                    find any edge coming out of V;
                    remove it from the graph;
                    put the second end of this edge in St;
        ```

        But this one works faster.

        !Add proof of correctness.

    [Back to Table of Contents](#table-of-contents)


# 3 Breadth-first Search

- ## 3.1 Base algorithm BFS, proof of correctness.

    ```
        bfs(int s):
            queue q
            dist.assign(n, -1)
            q.push(s)
            dist[s] = 0
            while (!q.empty):
                v = q.front
                q.pop
                for u in g[v]:
                    if dist[u] == -1:
                        q.push(u)
                        dist[u] = dist[v] + 1
    ```

    !Agregar prueba de por que funciona

    [Back to Table of Contents](#table-of-contents)

- ## 3.2 (0-1)-BFS, (0-k)-BFS

    - ### (0-1) BFS

        If all edges in the graph have weights either 0 or 1, then in every iteration, every vertex is at a distance of either $0$ or $1$ respect to the vertex that has been extracted from the queue.

        Let's save in a deque the new coming vertices.
        When doing BFS, if the edge has weight of 1, we push it to the end of the queue, otherwise to the beginning, but we get elements only from the beginning of the queue, as the smallest distances are there, the minimum distance to every vertex is computed as usual.

    - ## (0-k) BFS (Dial's algorithm)

        The idea is similar, but since every edge has weight $\leq k$, we create $k+1$ buckets (arrays, stacks, queues, etc.), in which every vertex that is at a distance $0 \cdots k$ accordingly will be stored.  
        Then we will empty the buckets in increasing order.

    [Back to Table of Contents](#table-of-contents)

- ## 3.3 Djikstra's Algorithm

    Let's create a min priority queue, in which we will insert the edges such that they were sorted by edge weight, this is necessary when the weights of the edges are not constrained, or the constrain is too big. The idea is the same as the 0-k BFS.

    !Add proof of correctness  
    [Back to Table of Contents](#table-of-contents)

- ## 3.4 Bellman-Ford's Algorithm

    We initialize all vertices to have a distance of inf except the source vertex, which will be initialized to $0$, we will relaxate this distances on every iteration ($n$ in total).  
    For each iteration, we will run over the list of edges, and if using the edge $e$ the distance to one of the ends of this edge can be reduce, let's reduce it, otherwise, just ignore it.

    Therefore, we can find the shorest paths of $k$ edges using only k iterations of this algorithm

    !Add proof of correctness  
    [Back to Table of Contents](#table-of-contents)

- ## 3.5 Floyd-Warshall's Algorithm

    We set a matrix of adjacency to infinite in all cells, except the diagonals where we will initialize to $0$.  
    Then we will initialize all cells that correspond to the edges in the graph to their actual value.

    For each of the $n$ vertices, we will take such a vertex as a pivot, i. e., for an edge $(v, u)$, if by going from $v$ to $k$, and then from $k$ to $u$ the total distance from $v$ to $u$ can be reduces, we will update the corresponding cell in the matrix of adjacency.

    ### Negative cycle detection

    We set the distances of all nodes to themselves to be 0, therefore, if after the execution of the algorithm the distance from a node to itself can be reduced, then a negative cycle can be found

    !Add proof of correctness  
    [Back to Table of Contents](#table-of-contents) 

- ## 3.6 Negative cycle detection

    ### Using Bellman-Ford algorithm

    For every vertex let's save its parent, i. e. that vertex from which the distance to the current vertex could be relaxated, then let's let's backtrack using this array, untill we found an already visited vertex.

    [Back to Table of Contents](#table-of-contents) 

# 4 Minimum Spanning Tree

- ## 4.1 Lemma of safe edge

    Let $A$ and $B$ be two disjoint sets of vertices, and let a set of edges join both of these sets, then the minimum of these edges will be in some minimum spanning tree

    - **Corollary**: if more than one edge has the minimum weight, then theres is more than one MST exists. And if only one edge with the minimum weight exists, then the MST is unique

    ### Proof

    Let $u$ and $v$ be the minimum edge joining sets $A$ and $B$ and let $x$ and $y$ be the ends of some other edge joining $A$ and $B$.  
    Let's try to build a MST that includes edge $xy$ but does not include edge $uv$, then let's take the same portion of the MST in components $A$ and $B$ that does not include edge $xy$ but includes edge $uv$, by definition $w(uv) < w(x, y)$, hence, we have built a MST that has less weight than the last one, which is contradiction.

    [Back to Table of Contents](#table-of-contents)

- ## 4.2 Prim's algorithm

    We start from any vertex, and add the all of its edges to a priority_queue, so that then we could extract this edges and if the other end of the edge has not already been seen, we add all of the edges of the neighbor to the heap, we repeat it untill the queue has been completely empty.

    !Add proof of correctness and running time  
    [Back to Table of Contents](#table-of-contents)

- ## 4.3 Kruskal's algorithm

    We maintain a DSU of vertices, then sort the list of edges by weight and take each edge one by one, if the pair of vertices that the corresponding edge already belong to the same set, do nothing, otherwise, join them in the DSU and add the corresponding edge to the answer tree untill all vertices belong to the same set.

    !Add proof of correctness and running time  
    [Back to Table of Contents](#table-of-contents)

# 5 Games on graphs

- ## 5.2 Sum of games, Grundy function

    Let graphs $A$ and $B$ be graphs in which both players can make moves (there is a piece that can be moved in both graphs). A first approach is to build a graph with $n^2$ vertices, in which all possible moves (either on the first graph or on the second are drawn).  
    But we can study every graph independently, defining the winning state of the vertices, and consequently defining is a graph is a winning graph or losing graph.  
    Then for every vertex we can define the Grundy function, which is $g(v) = MEX(g(u))$ for all $u$ - neighbors of $v$

    Hence, for every graph, it is a losing graph if its $g[v] = 0$ for the starting vertex $v$, 

    Then Grundy function for the game is defined as $G(A + B) = G(A) \oplus G(B)$

    ### Proof

    In an inductive way, we assume that for two games $A$ and $B$, we either made the next step in $A$, or in $B$, and the two Grundy functions for this games are $g(a') \oplus g(b)$ and $g(a) \oplus g(b')$ respectively.  
    Then, we need to prove two observations:

    1. $g(a) \oplus g(b)$ is not in either graph.
    2. All $x < g(a) \oplus g(b)$ are in the set of values of Grundy for all vertices (the two we are looking at, but it can be generalized).

    Let's prove both:

    1. $g(a) \oplus g(b)$ is equal to $g(a') \oplus g(b)$ of $g(a) \oplus g(b')$ Without loss of generality, let's set: $g(a) \oplus g(b) = g(a') \oplus g(b)$, we do $\oplus g(b)$ on both sides, and we get $g(a)=g(a')$ wich is contradictory.

    ![Alt text](img/Grundy%20proof.png)

    2. We set $x < g(a) \oplus g(b)$, then, both of these numbers share prefix, but at some bit, $g(a)\oplus g(b) = 1$ and $x = 0$ (because of the less criterium), then, when doing the operation $x \oplus g(b)$ we get the same prefix as in $g(a)$ (since prefix of $g(a)\oplus g(b)$ is composed of $g(a)$ and $g(b)$), but in that specific bit, we get a $0$, which means that $x \oplus g(b) < g(a)$, and it means that in game $A$ we can move to a state $a'$, that has that value of Grundy function, therefor we get $g(a')\oplus g(b) = x$(see image)  
    This basically shows that for every $x < g(a) \oplus g(b)$, we can find a move that leads to a grundy functions with that value. [insert square of proof]

    [Back to Table of Contents](#table-of-contents)

# 6 Matchings

- ## 6.1 

# 7 Flows

- ## 7.1 Ford-Fulkerson's algorithm

    In the graph, the weight of an edge represent the current capacity of the corresponding edge.  
    For every edge in the graph we will add its transpose edge, which will have a weight equal to the current flow through that edge.  
    Then, We will find any augmenting path from source to sink (i. e. a path whose minimum capacity is positive) and send a flow to that path (consequently reducing the capacity of all edges along the path and increasing the flow on the transpose edges).  
    When no augmenting path could be found, we have found the maximum flow on that graph.

    !Add proof of correctness and running time  
    [Back to Table of Contents](#table-of-contents)

- ## 7.2 Edmon-Karp algorithm

    This algorithm finds augmenting paths of the minimum distance using a BFS every time, the distance of the paths is constrained by $V$, if no path could be found on the BFS, then we have found the maximum flow.

    !Add proof of correctness and running time  
    [Back to Table of Contents](#table-of-contents)

- ## 7.3 Dinic's algorithm

    Since Edmon-Karp finds always the shortest paths, Dinic proposed to build a graph of only minimal paths from source to sink and run Ford-Fulkerson's algorithm.

    !Add proof of correctness and running time  
    [Back to Table of Contents](#table-of-contents)

- # Algoritmo Hungariano

- Descripción del problema

    Hay un conjunto de tareas, que las pueden ejecutar todos los agentes disponibles (la misma cantidad de agentes que de tareas, osea una matriz cuadrada), pero cada uno cobra un precio distinto por cada tarea, distribuir las tareas tal que cada agente tenga una sola tarea, y el precio total sea el menor posible.
    
- Algoritmo

    1. A cada fila de la matriz le restamos el menor elemento en ella
    2. A cada columna le restamos el menor elemento en ella
    3. Cubrimos con el mínimo número posible de líneas, las filas y columnas que contienen un cero (Osea, si conviene más cubrir con una línea horizontal o vertical para cada celda no cubierta)
    4. Si el número de líneas que se usaron es n, entonces solo hace falta repartir cada tarea (Osea, darsela a un agente, solo si en esa celda hay un cero, y repartirlas tal que a cada agente le toque una tarea)
    5. Si el número de líneas que se usaron no es n, buscar el menor valor que no está cubierto por una línea y restárselo a todas las filas **des**cubiertas, y sumarlo a todas las filas cubiertas y repetir desde el paso 3.
 
!Add proof of correctness and running time  
    [Back to Table of Contents](#table-of-contents)