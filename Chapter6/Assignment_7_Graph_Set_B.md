# Assignment 7 – Graph

## SET B

---

# 1. Graph Traversal Using Depth First Search (DFS)

## 1.1 Concept Explanation

A **graph** is a non-linear data structure represented as:

```text
G = (V, E)
```

where:

- `V` represents the set of vertices.
- `E` represents the set of edges connecting vertices.

A graph can be represented using an **adjacency matrix**.

An adjacency matrix is a two-dimensional array of size:

```text
V × V
```

For a directed graph, if an edge exists from vertex `i` to vertex `j`:

```text
graph[i][j] = 1
```

Otherwise:

```text
graph[i][j] = 0
```

### Depth First Search (DFS)

**Depth First Search** is a graph traversal technique in which we start from a selected vertex and explore as far as possible along one path before returning and exploring another path.

DFS uses a `visited[]` array to remember which vertices have already been visited.

The basic process is:

```text
Start from a vertex
       ↓
Mark it as visited
       ↓
Print/process it
       ↓
Check its adjacent vertices
       ↓
If an adjacent vertex is not visited
       ↓
Recursively perform DFS on that vertex
```

The source material describes DFS as:

1. Mark the start vertex as visited.
2. Print/process the vertex.
3. For each neighbor, if it is not visited, recursively call DFS.

The stated time complexity is:

```text
O(V + E)
```

For this assignment, the graph is read as an **adjacency matrix** and then traversed using DFS.

---

## 1.2 Program

```c
#include <stdio.h>

#define MAX 20

void DFS(int graph[MAX][MAX], int vertices, int vertex,
         int visited[MAX])
{
    int i;

    visited[vertex] = 1;

    printf("%d ", vertex + 1);

    for (i = 0; i < vertices; i++)
    {
        if (graph[vertex][i] == 1 && visited[i] == 0)
        {
            DFS(graph, vertices, i, visited);
        }
    }
}

int main()
{
    int graph[MAX][MAX];
    int visited[MAX] = {0};

    int vertices;
    int edges;
    int source, destination;
    int startVertex;
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

    printf("\nEnter directed edges (source destination):\n");

    for (i = 0; i < edges; i++)
    {
        scanf("%d %d", &source, &destination);

        graph[source - 1][destination - 1] = 1;
    }

    printf("\nEnter starting vertex: ");
    scanf("%d", &startVertex);

    printf("\nDFS Traversal: ");

    DFS(graph, vertices, startVertex - 1, visited);

    printf("\n");

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

It provides:

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

### 3. `DFS()` Function

```c
void DFS(int graph[MAX][MAX], int vertices, int vertex,
         int visited[MAX])
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

### 4. Mark the Current Vertex as Visited

```c
visited[vertex] = 1;
```

When DFS reaches a vertex, it marks that vertex as visited.

For example:

```text
visited[0] = 1
```

means vertex `1` has been visited.

The program uses zero-based array indexing internally:

```text
Vertex 1 → index 0
Vertex 2 → index 1
Vertex 3 → index 2
```

---

### 5. Display the Current Vertex

```c
printf("%d ", vertex + 1);
```

The current vertex is printed.

`+ 1` is used because the array uses indexes starting from `0`, while the user sees vertices starting from `1`.

---

### 6. Check All Adjacent Vertices

```c
for (i = 0; i < vertices; i++)
```

This loop checks every possible vertex.

The condition:

```c
graph[vertex][i] == 1
```

checks whether an edge exists from the current vertex to vertex `i`.

The second condition:

```c
visited[i] == 0
```

checks whether vertex `i` has not already been visited.

Therefore:

```c
if (graph[vertex][i] == 1 && visited[i] == 0)
```

means:

```text
There is an edge
        AND
The vertex has not been visited
```

---

### 7. Recursive DFS Call

```c
DFS(graph, vertices, i, visited);
```

If an unvisited adjacent vertex is found, DFS is called recursively for that vertex.

This is what makes DFS go deeper into the graph before returning to another vertex.

For example:

```text
1 → 2 → 3
```

Starting from `1`:

```text
Visit 1
 ↓
Visit 2
 ↓
Visit 3
```

The function keeps moving forward until there are no more unvisited adjacent vertices.

---

### 8. `main()` Function

```c
int graph[MAX][MAX];
```

Creates the adjacency matrix.

```c
int visited[MAX] = {0};
```

Creates the visited array.

Initially all values are `0`:

```text
0 0 0 0 ...
```

which means no vertex has been visited.

---

### 9. Accept Number of Vertices

```c
scanf("%d", &vertices);
```

Accepts the number of vertices.

For example:

```text
Enter number of vertices: 5
```

---

### 10. Initialize the Adjacency Matrix

```c
for (i = 0; i < vertices; i++)
{
    for (j = 0; j < vertices; j++)
    {
        graph[i][j] = 0;
    }
}
```

Initially, every position is set to `0`.

This means no edges exist yet.

---

### 11. Accept Number of Edges

```c
scanf("%d", &edges);
```

Accepts the number of edges in the graph.

---

### 12. Accept Graph Edges

```c
scanf("%d %d", &source, &destination);
```

Each edge is entered as:

```text
source destination
```

For example:

```text
1 2
```

means:

```text
1 → 2
```

The edge is stored using:

```c
graph[source - 1][destination - 1] = 1;
```

The `-1` converts the user's vertex number into the corresponding C array index.

---

### 13. Accept Starting Vertex

```c
scanf("%d", &startVertex);
```

DFS needs a starting vertex.

For example:

```text
Enter starting vertex: 1
```

means DFS begins from vertex `1`.

---

### 14. Call DFS

```c
DFS(graph, vertices, startVertex - 1, visited);
```

The starting vertex is converted to a zero-based index and passed to the DFS function.

The `visited[]` array is also passed so that recursive calls share the same visited information.

---

# 2. Graph Traversal Using Breadth First Search (BFS)

## 2.1 Concept Explanation

**Breadth First Search (BFS)** is a graph traversal technique that visits vertices level by level.

Instead of going as deep as possible like DFS, BFS first visits all immediate neighbors of the current vertex and then moves to the next level.

BFS uses a **queue**.

The basic process is:

```text
Create Queue
     ↓
Mark starting vertex as visited
     ↓
Enqueue starting vertex
     ↓
While Queue is not empty
     ↓
Dequeue a vertex
     ↓
Print/process it
     ↓
Check all its neighbors
     ↓
If neighbor is not visited
     ↓
Mark it visited
     ↓
Enqueue it
```

The source material describes BFS using:

1. A queue `Q`.
2. The start vertex is marked as visited.
3. The start vertex is inserted into the queue.
4. While the queue is not empty:
   - Dequeue a vertex.
   - Process the vertex.
   - Check every neighbor.
   - Mark unvisited neighbors and enqueue them.

The source material states the time complexity as:

```text
O(V + E)
```

For this assignment, the graph is read as an **adjacency matrix** and traversed using BFS.

---

## 2.2 Program

```c
#include <stdio.h>

#define MAX 20

void BFS(int graph[MAX][MAX], int vertices, int startVertex)
{
    int visited[MAX] = {0};
    int queue[MAX];

    int front = 0;
    int rear = 0;

    int currentVertex;
    int i;

    visited[startVertex] = 1;

    queue[rear] = startVertex;
    rear++;

    while (front < rear)
    {
        currentVertex = queue[front];
        front++;

        printf("%d ", currentVertex + 1);

        for (i = 0; i < vertices; i++)
        {
            if (graph[currentVertex][i] == 1 &&
                visited[i] == 0)
            {
                visited[i] = 1;

                queue[rear] = i;
                rear++;
            }
        }
    }
}

int main()
{
    int graph[MAX][MAX];

    int vertices;
    int edges;
    int source, destination;
    int startVertex;
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

    printf("\nEnter directed edges (source destination):\n");

    for (i = 0; i < edges; i++)
    {
        scanf("%d %d", &source, &destination);

        graph[source - 1][destination - 1] = 1;
    }

    printf("\nEnter starting vertex: ");
    scanf("%d", &startVertex);

    printf("\nBFS Traversal: ");

    BFS(graph, vertices, startVertex - 1);

    printf("\n");

    return 0;
}
```

---

## 2.3 Program Explanation

### 1. Header File

```c
#include <stdio.h>
```

Provides:

```text
printf()
scanf()
```

for input and output.

---

### 2. Maximum Number of Vertices

```c
#define MAX 20
```

Defines the maximum number of vertices that can be stored.

---

### 3. `BFS()` Function

```c
void BFS(int graph[MAX][MAX], int vertices, int startVertex)
```

This function performs Breadth First Search.

It receives:

```text
graph       → adjacency matrix
vertices    → number of vertices
startVertex → starting vertex
```

---

### 4. Visited Array

```c
int visited[MAX] = {0};
```

Stores whether a vertex has already been visited.

Initially:

```text
0 = not visited
```

When a vertex is visited:

```c
visited[i] = 1;
```

---

### 5. Queue

```c
int queue[MAX];
```

The queue stores vertices waiting to be processed.

Two variables are used:

```c
int front = 0;
int rear = 0;
```

`front` points to the next vertex to remove.

`rear` points to the next position where a vertex can be inserted.

The queue follows:

```text
FIFO
```

which means:

```text
First In → First Out
```

---

### 6. Mark Starting Vertex

```c
visited[startVertex] = 1;
```

The starting vertex is marked as visited before it is inserted into the queue.

This prevents the same vertex from being inserted again.

---

### 7. Insert Starting Vertex into Queue

```c
queue[rear] = startVertex;
rear++;
```

The starting vertex is inserted into the queue.

Initially:

```text
front = 0
rear  = 0
```

After insertion:

```text
queue[0] = startVertex
rear = 1
```

---

### 8. Continue While Queue Is Not Empty

```c
while (front < rear)
```

The queue contains elements when:

```text
front < rear
```

When:

```text
front == rear
```

there are no more vertices waiting to be processed.

---

### 9. Remove Vertex from Queue

```c
currentVertex = queue[front];
front++;
```

The vertex at the front of the queue is removed.

This follows FIFO behavior.

---

### 10. Display Current Vertex

```c
printf("%d ", currentVertex + 1);
```

The current vertex is displayed.

Again, `+1` converts the zero-based array index to the user's vertex numbering.

---

### 11. Check All Neighbors

```c
for (i = 0; i < vertices; i++)
```

Checks every possible adjacent vertex.

The condition:

```c
graph[currentVertex][i] == 1
```

checks whether an edge exists from the current vertex to vertex `i`.

The condition:

```c
visited[i] == 0
```

checks whether that neighbor has not been visited.

Together:

```c
if (graph[currentVertex][i] == 1 &&
    visited[i] == 0)
```

means:

```text
There is an edge
        AND
The neighbor is not visited
```

---

### 12. Mark Neighbor as Visited

```c
visited[i] = 1;
```

The neighbor is marked as visited before it is inserted into the queue.

This prevents duplicate entries in the queue.

---

### 13. Enqueue the Neighbor

```c
queue[rear] = i;
rear++;
```

The newly discovered vertex is inserted at the rear of the queue.

Therefore, vertices are processed in the same order in which they were discovered.

---

### 14. `main()` Function

```c
int graph[MAX][MAX];
```

Creates the adjacency matrix.

The matrix is initialized to zero using nested loops.

Then the program accepts:

```text
Number of vertices
Number of edges
Edges
Starting vertex
```

---

### 15. Store the Graph

```c
graph[source - 1][destination - 1] = 1;
```

Stores each directed edge in the adjacency matrix.

For example:

```text
Input:
1 2
```

is stored as:

```text
graph[0][1] = 1
```

---

### 16. Start BFS

```c
BFS(graph, vertices, startVertex - 1);
```

Calls the BFS function using the selected starting vertex.

The traversal continues until the queue becomes empty.
