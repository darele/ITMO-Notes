# Repaso para Examen de algo

# Table of Contents
1. [1. DFS](#depth-first-search) 
2. &emsp;[1.1 DFS](#11-dfs)
2. &emsp;[1.2 Topological Sort](#12-topological-sort)
3. [2. Advanced DFS](#advanced-dfs)
4. &emsp;[2.1 Finding Bridges and Articulation Points](#21-finding-bridges-and-articulation-points)
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

# Advanced DFS

- ## 2.1 Finding Bridges and Articulation points

    Save for every vertex its discovery time $d[v]$, and its lowest discovery time of any of its neighbors. it is, when visiting a vertex $v$, if one of its neighbors $u$ has already been visited, we will update $min[v] = min(d[u], min[v])$.
    
    A vertex is an articulation point, if $min[v] >= d[u]$, i.e. from its descendants in the dfs tree, there is not a back edge (since the minimum discovery time that could be found corresponds at least to the studied point).

    A vertex $v$ is the end of the bridge $(u,v), if $min(min[v], min[u]) >= max(d[u], d[v])$
    
- ## 2.3 Korasaju's algorithm

    1. After the recursive call of DFS, let's insert in a stack the corresponding vertex, then we will have a stack with the vertices in the order of their exit from the recursive call.  


    ![Example graph with two SCCs](SCC.png)

    In the above graph, the final queue looks like: $0,1, 2, 4, 3, 0$  
    
    2. Now we will run DFS on the transposed graph, taking vertices from stack one by one, and we will go to the next vertex in the stack after the recursive call (if it has been visited, do nothing). We will also keep track of the number of vertices in the current component. If we reach a vertex that has already been visited, we will start a new component.  

    Why does it work? Basically, because we add the vertex to the stack only when it has already gone recursively to all of its neighbors, we guarantee that a vertex that connects a component to another one, will be added to the stack after all the vertices of the component that it connects to, then, since we are taking the vertices according to the stack, we can guarantee that if a vertex connects to another component in this transposed graph, that component will be visited before the current one.

## Algoritmo Hungariano

<details>
    <summary>Descripción del problema</summary>

    Hay un conjunto de tareas, que las pueden ejecutar todos los agentes disponibles (la misma cantidad de agentes que de tareas, osea una matriz cuadrada), pero cada uno cobra un precio distinto por cada tarea, distribuir las tareas tal que cada agente tenga una sola tarea, y el precio total sea el menor posible.
</details>
    
<details>
    <summary>Algoritmo</summary>

    1. A cada fila de la matriz le restamos el menor elemento en ella
    2. A cada columna le restamos el menor elemento en ella
    3. Cubrimos con el mínimo número posible de líneas, las filas y columnas que contienen un cero (Osea, si conviene más cubrir con una línea horizontal o vertical para cada celda no cubierta)
    4. Si el número de líneas que se usaron es n, entonces solo hace falta repartir cada tarea (Osea, darsela a un agente, solo si en esa celda hay un cero, y repartirlas tal que a cada agente le toque una tarea)
    5. Si el número de líneas que se usaron no es n, buscar el menor valor que no está cubierto por una línea y restárselo a todas las filas **des**cubiertas, y sumarlo a todas las filas cubiertas y repetir desde el paso 3.
</details>
 
