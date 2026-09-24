# Assignment 7 – Graph

## SET C

---

# 1. Find Cycle in an Undirected Graph

## 1.1 Concept Explanation

A **graph** is a non-linear data structure represented as:

```text
G = (V, E)
```

where:

- `V` represents the set of vertices.
- `E` represents the set of edges connecting vertices.

An **undirected graph** is a graph in which an edge has no direction.

For example:

```text
1 ----- 2
 \       /
  \     /
    3
```

If there is an edge between vertex `1` and vertex `2`, the connection can be represented in both directions:

```text
1 → 2
2 → 1
```

An undirected graph can be represented using an **adjacency matrix**.

The adjacency matrix is a two-dimensional array of size:

```text
V × V
```

If an edge exists between vertex `i` and vertex `j`:

```text
graph[i][j] = 1
graph[j][i] = 1
```

If no edge exists:

```text
graph[i][j] = 0
```

### Cycle in an Undirected Graph

A **cycle** exists when we can start from a vertex, follow edges, and return to the same vertex without repeating a vertex.

For example:

```text
1 ----- 2
 \       /
  \     /
    3
```

contains a cycle:

```text
1 → 2 → 3 → 1
```

To detect a cycle in an undirected graph using DFS, we maintain:

- `visited[]` to remember visited vertices.
- `parent` to remember the vertex from which the current vertex was reached.

While checking an adjacent vertex:

- If it is not visited, continue DFS.
- If it is already visited and it is not the parent of the current vertex, a cycle exists.

The basic idea is:

```text
Start DFS
   ↓
Mark vertex visited
   ↓
Check adjacent vertices
   ↓
If neighbor is not visited
   ↓
DFS(neighbor)
   ↓
If neighbor is already visited
and neighbor is not parent
   ↓
Cycle exists
```

---

## 1.2 Program

```c
#include <stdio.h>

#define MAX 20

int isCyclicUtil(int graph[MAX][MAX], int vertices,
                 int vertex, int visited[MAX], int parent)
{
    int i;

    visited[vertex] = 1;

    for (i = 0; i < vertices; i++)
    {
        if (graph[vertex][i] == 1)
        {
            if (visited[i] == 0)
            {
                if (isCyclicUtil(graph, vertices, i, visited, vertex))
                {
                    return 1;
                }
            }
            else if (i != parent)
            {
                return 1;
            }
        }
    }

    return 0;
}

int containsCycle(int graph[MAX][MAX], int vertices)
{
    int visited[MAX] = {0};
    int i;

    for (i = 0; i < vertices; i++)
    {
        if (visited[i] == 0)
        {
            if (isCyclicUtil(graph, vertices, i, visited, -1))
            {
                return 1;
            }
        }
    }

    return 0;
}

int main()
{
    int graph[MAX][MAX];

    int vertices;
    int edges;
    int source, destination;
    int i, j;

    printf("Enter number of vertices: ");
    scanf("%d", &vertices);

    for (i = 0; i < vertices; i++)
    {
        for (j = 0; j < vertices; j++)
        {
            graph[i][j] = 0;
        }
    }

    printf("Enter number of edges: ");
    scanf("%d", &edges);

    printf("\nEnter undirected edges (source destination):\n");

    for (i = 0; i < edges; i++)
    {
        scanf("%d %d", &source, &destination);

        graph[source - 1][destination - 1] = 1;
        graph[destination - 1][source - 1] = 1;
    }

    if (containsCycle(graph, vertices))
    {
        printf("\nGraph contains a cycle.\n");
    }
    else
    {
        printf("\nGraph does not contain a cycle.\n");
    }

    return 0;
}
```

---

## 1.3 Program Explanation

### 1. Header File

```c
#include <stdio.h>
```

Includes the standard input/output library.

It provides functions such as:

```text
printf()
scanf()
```

for displaying and accepting values.

---

### 2. Maximum Number of Vertices

```c
#define MAX 20
```

Defines the maximum number of vertices as `20`.

Therefore, the adjacency matrix can contain:

```text
20 × 20
```

elements.

---

### 3. `isCyclicUtil()` Function

```c
int isCyclicUtil(int graph[MAX][MAX], int vertices,
                 int vertex, int visited[MAX], int parent)
```

This is the recursive function used to detect a cycle.

It receives:

```text
graph     → adjacency matrix
vertices  → number of vertices
vertex    → current vertex
visited   → array used to track visited vertices
parent    → vertex from which current vertex was reached
```

The `parent` is important because in an undirected graph, when we move:

```text
1 → 2
```

vertex `2` will naturally see vertex `1` again.

That does not mean a cycle exists because `1` is simply the parent of `2`.

---

### 4. Mark Current Vertex as Visited

```c
visited[vertex] = 1;
```

The current vertex is marked as visited.

For example:

```text
visited[0] = 1
```

means vertex `1` has been visited.

---

### 5. Check All Adjacent Vertices

```c
for (i = 0; i < vertices; i++)
```

Checks every possible vertex to determine whether it is connected to the current vertex.

The condition:

```c
graph[vertex][i] == 1
```

means an edge exists between the current vertex and vertex `i`.

---

### 6. If the Neighbor Is Not Visited

```c
if (visited[i] == 0)
```

checks whether the neighboring vertex has not been visited yet.

If it is not visited, the function performs DFS on that vertex:

```c
isCyclicUtil(graph, vertices, i, visited, vertex)
```

Here, the current vertex becomes the `parent` of vertex `i`.

---

### 7. Recursive DFS Call

```c
if (isCyclicUtil(graph, vertices, i, visited, vertex))
{
    return 1;
}
```

The function recursively explores the neighboring vertex.

If the recursive call finds a cycle, it returns `1`.

That `1` is then passed back through the previous recursive calls.

---

### 8. Already Visited Neighbor

```c
else if (i != parent)
{
    return 1;
}
```

This is the main cycle detection condition.

The neighbor has already been visited.

If:

```text
i == parent
```

then the edge is simply going back to the vertex from which we came.

That is not considered a cycle.

But if:

```text
i != parent
```

then we have found another already visited vertex that is not the parent.

Therefore, a cycle exists.

---

### 9. Return No Cycle from Current Path

```c
return 0;
```

If all adjacent vertices have been checked and no cycle is found, the function returns `0`.

---

### 10. `containsCycle()` Function

```c
int containsCycle(int graph[MAX][MAX], int vertices)
```

This function starts cycle detection for the entire graph.

It creates:

```c
int visited[MAX] = {0};
```

Initially:

```text
0 0 0 0 ...
```

means no vertex has been visited.

---

### 11. Check Every Vertex

```c
for (i = 0; i < vertices; i++)
```

The loop checks every vertex.

This is important because the graph may be **disconnected**.

For example:

```text
1 ----- 2       3 ----- 4
```

There are two separate components.

The program must start DFS from every unvisited vertex to check all components.

---

### 12. Start DFS for an Unvisited Vertex

```c
if (visited[i] == 0)
{
    if (isCyclicUtil(graph, vertices, i, visited, -1))
    {
        return 1;
    }
}
```

If a vertex has not yet been visited, DFS is started from that vertex.

The initial parent is:

```text
-1
```

because the starting vertex does not have a parent.

---

### 13. Return Cycle Result

```c
return 0;
```

If all connected components have been checked and no cycle is found, the function returns `0`.

---

### 14. Create the Adjacency Matrix

```c
int graph[MAX][MAX];
```

Creates a two-dimensional array to store the graph.

---

### 15. Initialize the Matrix

```c
for (i = 0; i < vertices; i++)
{
    for (j = 0; j < vertices; j++)
    {
        graph[i][j] = 0;
    }
}
```

Initially all values are set to `0`.

This means no edges are present.

---

### 16. Accept Number of Edges

```c
scanf("%d", &edges);
```

Accepts the total number of edges.

For example:

```text
Enter number of edges: 3
```

means the program will accept three edges.

---

### 17. Accept Undirected Edges

```c
scanf("%d %d", &source, &destination);
```

Accepts an edge as:

```text
source destination
```

For example:

```text
1 2
```

means there is an undirected edge between vertices `1` and `2`.

---

### 18. Store Both Directions

```c
graph[source - 1][destination - 1] = 1;
graph[destination - 1][source - 1] = 1;
```

Because the graph is undirected, both directions are stored.

For input:

```text
1 2
```

the program stores:

```text
graph[0][1] = 1
graph[1][0] = 1
```

The `-1` converts the user-facing vertex number into a zero-based C array index.

---

### 19. Check Whether the Graph Contains a Cycle

```c
if (containsCycle(graph, vertices))
```

Calls the cycle detection function.

If it returns `1`:

```text
Graph contains a cycle.
```

is displayed.

If it returns `0`:

```text
Graph does not contain a cycle.
```

is displayed.

---

# 2. Check Whether the Graph Is Fully Connected

## 2.1 Concept Explanation

A graph is **fully connected** (connected) when there is a path between every pair of vertices.

For example:

```text
1 ----- 2
|       |
|       |
4 ----- 3
```

is connected because every vertex can be reached from every other vertex through one or more edges.

A graph such as:

```text
1 ----- 2

3 ----- 4
```

is not fully connected because there is no path between the first group and the second group.

To check connectivity, we can use **DFS**.

The basic process is:

```text
Start DFS from one vertex
        ↓
Mark reachable vertices as visited
        ↓
Finish DFS
        ↓
Check visited[]
        ↓
If every vertex is visited
        ↓
Graph is fully connected
```

If even one vertex remains unvisited, the graph is not fully connected.

The graph is represented using an adjacency matrix.

---

## 2.2 Program

```c
#include <stdio.h>

#define MAX 20

void DFS(int graph[MAX][MAX], int vertices,
         int vertex, int visited[MAX])
{
    int i;

    visited[vertex] = 1;

    for (i = 0; i < vertices; i++)
    {
        if (graph[vertex][i] == 1 && visited[i] == 0)
        {
            DFS(graph, vertices, i, visited);
        }
    }
}

int isConnected(int graph[MAX][MAX], int vertices)
{
    int visited[MAX] = {0};
    int i;

    DFS(graph, vertices, 0, visited);

    for (i = 0; i < vertices; i++)
    {
        if (visited[i] == 0)
        {
            return 0;
        }
    }

    return 1;
}

int main()
{
    int graph[MAX][MAX];

    int vertices;
    int edges;
    int source, destination;
    int i, j;

    printf("Enter number of vertices: ");
    scanf("%d", &vertices);

    for (i = 0; i < vertices; i++)
    {
        for (j = 0; j < vertices; j++)
        {
            graph[i][j] = 0;
        }
    }

    printf("Enter number of edges: ");
    scanf("%d", &edges);

    printf("\nEnter undirected edges (source destination):\n");

    for (i = 0; i < edges; i++)
    {
        scanf("%d %d", &source, &destination);

        graph[source - 1][destination - 1] = 1;
        graph[destination - 1][source - 1] = 1;
    }

    if (isConnected(graph, vertices))
    {
        printf("\nGraph is fully connected.\n");
    }
    else
    {
        printf("\nGraph is not fully connected.\n");
    }

    return 0;
}
```

---

## 2.3 Program Explanation

### 1. Header File

```c
#include <stdio.h>
```

Includes the standard input/output library.

It provides:

```text
printf()
scanf()
```

---

### 2. Maximum Number of Vertices

```c
#define MAX 20
```

Defines the maximum number of vertices as `20`.

---

### 3. `DFS()` Function

```c
void DFS(int graph[MAX][MAX], int vertices,
         int vertex, int visited[MAX])
```

This function performs Depth First Search.

It receives:

```text
graph     → adjacency matrix
vertices  → number of vertices
vertex    → current vertex
visited   → array used to track visited vertices
```

---

### 4. Mark Vertex as Visited

```c
visited[vertex] = 1;
```

Marks the current vertex as visited.

For example:

```text
visited[0] = 1
```

means vertex `1` has been reached.

---

### 5. Find Adjacent Vertices

```c
for (i = 0; i < vertices; i++)
```

Checks every possible vertex.

The condition:

```c
graph[vertex][i] == 1
```

checks whether there is an edge between the current vertex and vertex `i`.

The condition:

```c
visited[i] == 0
```

ensures that DFS does not visit the same vertex repeatedly.

---

### 6. Recursive DFS

```c
DFS(graph, vertices, i, visited);
```

If an adjacent vertex has not been visited, DFS continues from that vertex.

Therefore, after DFS finishes, all vertices reachable from the starting vertex are marked as visited.

---

### 7. `isConnected()` Function

```c
int isConnected(int graph[MAX][MAX], int vertices)
```

This function determines whether the graph is fully connected.

It creates:

```c
int visited[MAX] = {0};
```

Initially, every vertex is unvisited.

---

### 8. Start DFS from Vertex 1

```c
DFS(graph, vertices, 0, visited);
```

DFS starts from vertex `1`.

The array index is `0` because C arrays use zero-based indexing.

If the graph is connected, DFS starting from vertex `1` should be able to reach every other vertex.

---

### 9. Check the `visited[]` Array

```c
for (i = 0; i < vertices; i++)
{
    if (visited[i] == 0)
    {
        return 0;
    }
}
```

The loop checks every vertex.

If any vertex is still:

```text
visited[i] == 0
```

then that vertex could not be reached from vertex `1`.

Therefore, the graph is not fully connected.

The function returns:

```text
0
```

---

### 10. Return Connected Result

```c
return 1;
```

If every vertex has been visited, the graph is fully connected.

The function returns:

```text
1
```

---

### 11. Create Adjacency Matrix

```c
int graph[MAX][MAX];
```

Creates the two-dimensional adjacency matrix.

---

### 12. Initialize Matrix

```c
for (i = 0; i < vertices; i++)
{
    for (j = 0; j < vertices; j++)
    {
        graph[i][j] = 0;
    }
}
```

Sets every matrix element to `0`.

Therefore, initially there are no edges.

---

### 13. Accept Edges

```c
scanf("%d %d", &source, &destination);
```

Accepts each undirected edge.

For example:

```text
1 2
```

represents a connection between vertex `1` and vertex `2`.

---

### 14. Store Undirected Edge

```c
graph[source - 1][destination - 1] = 1;
graph[destination - 1][source - 1] = 1;
```

Both directions are stored because the graph is undirected.

For example, for:

```text
1 2
```

the matrix stores:

```text
graph[0][1] = 1
graph[1][0] = 1
```

---

### 15. Check the Graph

```c
if (isConnected(graph, vertices))
```

Calls the connectivity-checking function.

If it returns `1`:

```text
Graph is fully connected.
```

is displayed.

If it returns `0`:

```text
Graph is not fully connected.
```

is displayed.
