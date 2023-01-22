# Repaso para Examen de algo

# Table of Contents
1. [DFS](#dfs)
2. [Hungarian Algorithm](#algoritmo-hungariano)

## DFS

- Base Algorithm

    ```
        dfs(v):
            vis[v] = true
            for (u in g[v]):
                if (!vis[u]):
                    dfs(u);
    ```
    I. e. we recursively check all possible paths, but never go through the same portion of a path more than once.

- Finding SCC

    1. After the recursive call of DFS, let's insert in a stack the corresponding vertex, then we will have a stack with the vertices in the order of their exit from the recursive call.  


    ![Example graph with two SCCs](SCC.png)

    In the above graph, the final queue looks like: $0,1, 2, 4, 3, 0$  
    
    2. Now we will run DFS on the transposed graph, taking vertices from stack one by one, and we will go to the next vertex in the stack after the recursive call (if it has been visited, do nothing). We will also keep track of the number of vertices in the current component. If we reach a vertex that has already been visited, we will start a new component.  

    Why does it work? Basically, because we add the vertex to the stack only when it has already gone recursively to all of its neighbors, we guarantee that a vertex that connects a component to another one, will be added to the stack after all the vertices of the component that it connects to, then, since we are taking the vertices according to the stack, we can guarantee that if a vertex connects to another component in this transposed graph, that component will be visited before the current one.

- Cycle finding

    - Undirected Graph.

        Use DFS from every unvisited node. Depth First Traversal can be used to detect a cycle in a Graph. There is a cycle in a graph only if there is a back edge present in the graph. A back edge is an edge that is indirectly joining a node to itself (self-loop) or one of its ancestors in the tree produced by DFS. 

        To find the back edge to any of its ancestors keep a visited array and if there is a back edge to any visited node then there is a loop and return true.

    - Directed Graph.

        We color the vertices in three colors, white if has not already been seen, in the DFS execution, gray if it is in the recursion stack now, and black if it has already been visited. If we find a gray vertex, then we have found a cycle.

- Bipartite check

    We will have an array of colors, and an array of visited, so we can check if a vertex is visited and what color it has. We will start with a vertex, and color it with one color, then we will run DFS on all of its neighbors, and color them with the other color, and so on. If we find a vertex that has already been visited, and it has the same color as the current one, then we have found an odd cycle, and the graph is not bipartite.
    

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
 
