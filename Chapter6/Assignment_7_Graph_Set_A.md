# Assignment 7 – Graph

## SET A

---

# 1. Graph Using Adjacency Matrix – Indegree, Outdegree and Display

## 1.1 Concept Explanation

A **graph** is a non-linear data structure represented as:

```text
G = (V, E)
```

where:

- `V` is the set of vertices (nodes).
- `E` is the set of edges connecting vertices.

A graph can be:

- **Directed graph** – an edge has a direction from one vertex to another.
- **Undirected graph** – an edge has no direction.

For this program, the graph is stored using an **adjacency matrix** so that indegree and outdegree can be calculated.

### Adjacency Matrix

An adjacency matrix is a two-dimensional array of size:

```text
V × V
```

For a directed graph, if there is an edge from vertex `i` to vertex `j`:

```text
matrix[i][j] = 1
```

Otherwise:

```text
matrix[i][j] = 0
```

For example, if there is an edge:

```text
1 → 2
```

then:

```text
matrix[1][2] = 1
```

The row represents the source vertex and the column represents the destination vertex.

### Indegree

**Indegree** of a vertex is the number of edges ending at that vertex.

For vertex `i`:

```text
Indegree(i) = number of 1s in column i
```

Example:

```text
1 → 2
3 → 2
```

Vertex `2` has:

```text
Indegree(2) = 2
```

because two edges end at vertex `2`.

### Outdegree

**Outdegree** of a vertex is the number of edges going out from that vertex.

For vertex `i`:

```text
Outdegree(i) = number of 1s in row i
```

Example:

```text
2 → 1
2 → 3
```

Vertex `2` has:

```text
Outdegree(2) = 2
```

because two edges originate from vertex `2`.

The workbook defines indegree as the number of edges ending on a vertex and outdegree as the number of edges moving out of a vertex. It also describes the adjacency matrix as a `V × V` two-dimensional array. 

---

## 1.2 Program

```c
#include <stdio.h>

#define MAX 20

void displayMatrix(int graph[MAX][MAX], int vertices)
{
    int i, j;

    printf("\nAdjacency Matrix:\n");

    for (i = 0; i < vertices; i++)
    {
        for (j = 0; j < vertices; j++)
        {
            printf("%d ", graph[i][j]);
        }

        printf("\n");
    }
}

void printIndegree(int graph[MAX][MAX], int vertices)
{
    int i, j;
    int indegree;

    printf("\nIndegree of each vertex:\n");

    for (i = 0; i < vertices; i++)
    {
        indegree = 0;

        for (j = 0; j < vertices; j++)
        {
            indegree = indegree + graph[j][i];
        }

        printf("Indegree of vertex %d = %d\n",
               i + 1, indegree);
    }
}

void printOutdegree(int graph[MAX][MAX], int vertices)
{
    int i, j;
    int outdegree;

    printf("\nOutdegree of each vertex:\n");

    for (i = 0; i < vertices; i++)
    {
        outdegree = 0;

        for (j = 0; j < vertices; j++)
        {
            outdegree = outdegree + graph[i][j];
        }

        printf("Outdegree of vertex %d = %d\n",
               i + 1, outdegree);
    }
}

int main()
{
    int graph[MAX][MAX] = {0};

    int vertices;
    int edges;
    int source, destination;
    int i;

    printf("Enter number of vertices: ");
    scanf("%d", &vertices);

    printf("Enter number of edges: ");
    scanf("%d", &edges);

    printf("\nEnter directed edges (source destination):\n");

    for (i = 0; i < edges; i++)
    {
        scanf("%d %d", &source, &destination);

        graph[source - 1][destination - 1] = 1;
    }

    displayMatrix(graph, vertices);

    printIndegree(graph, vertices);

    printOutdegree(graph, vertices);

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

which are used for displaying and accepting data.

---

### 2. Define Maximum Number of Vertices

```c
#define MAX 20
```

Defines the maximum number of vertices that can be stored in the matrix.

Therefore:

```c
int graph[MAX][MAX];
```

creates a matrix capable of storing up to:

```text
20 × 20
```

positions.

---

### 3. Adjacency Matrix

```c
int graph[MAX][MAX] = {0};
```

Creates the adjacency matrix.

The `{0}` initializes all elements to zero.

Initially:

```text
0 0 0
0 0 0
0 0 0
```

means there are no edges.

If an edge exists from vertex `1` to vertex `2`:

```c
graph[0][1] = 1;
```

The matrix becomes:

```text
0 1 0
0 0 0
0 0 0
```

---

### 4. `displayMatrix()` Function

```c
void displayMatrix(int graph[MAX][MAX], int vertices)
```

Displays the complete adjacency matrix.

The outer loop:

```c
for (i = 0; i < vertices; i++)
```

selects each row.

The inner loop:

```c
for (j = 0; j < vertices; j++)
```

selects each column.

```c
printf("%d ", graph[i][j]);
```

prints each matrix element.

---

### 5. `printIndegree()` Function

```c
void printIndegree(int graph[MAX][MAX], int vertices)
```

Calculates the indegree of every vertex.

For vertex `i`, we need to examine its entire column.

```c
indegree = indegree + graph[j][i];
```

Notice the order:

```text
graph[j][i]
```

The first index changes through rows, while the second index remains fixed.

Therefore, the entire column is checked.

For example:

```text
0 1 0
1 0 1
0 0 0
```

For vertex `2`, column `2` is:

```text
1
0
0
```

Therefore:

```text
Indegree(2) = 1
```

---

### 6. `printOutdegree()` Function

```c
void printOutdegree(int graph[MAX][MAX], int vertices)
```

Calculates the outdegree of every vertex.

For vertex `i`, we examine its complete row.

```c
outdegree = outdegree + graph[i][j];
```

The first index remains fixed while the second index changes.

Therefore, the entire row is checked.

For example:

```text
0 1 0
1 0 1
0 0 0
```

For vertex `2`, row `2` is:

```text
1 0 1
```

Therefore:

```text
Outdegree(2) = 2
```

---

### 7. Accept Number of Vertices

```c
printf("Enter number of vertices: ");
scanf("%d", &vertices);
```

Accepts the number of vertices in the graph.

For example:

```text
Enter number of vertices: 4
```

The vertices are treated as:

```text
1 2 3 4
```

---

### 8. Accept Number of Edges

```c
printf("Enter number of edges: ");
scanf("%d", &edges);
```

Accepts the number of edges.

---

### 9. Accept Edges

```c
for (i = 0; i < edges; i++)
{
    scanf("%d %d", &source, &destination);

    graph[source - 1][destination - 1] = 1;
}
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

The program uses:

```c
source - 1
destination - 1
```

because C arrays use zero-based indexing.

Therefore:

```text
Vertex 1 → index 0
Vertex 2 → index 1
Vertex 3 → index 2
```

---

### 10. Display the Matrix

```c
displayMatrix(graph, vertices);
```

Displays the graph's adjacency matrix.

---

### 11. Display Indegree

```c
printIndegree(graph, vertices);
```

Calculates and prints the indegree of every vertex.

---

### 12. Display Outdegree

```c
printOutdegree(graph, vertices);
```

Calculates and prints the outdegree of every vertex.

---

# 2. Graph Using Adjacency List – Outdegree of Vertex i

## 2.1 Concept Explanation

An **adjacency list** stores the list of neighboring vertices for every vertex.

The workbook describes an adjacency list as a representation where each index corresponds to a vertex and stores the list of adjacent vertices. It can be implemented using an array of linked lists or arrays.

For this program, an **array of linked lists** is used.

For example, consider:

```text
1 → 2
1 → 3
2 → 4
3 → 4
```

The adjacency list is:

```text
1 → 2 → 3 → NULL
2 → 4 → NULL
3 → 4 → NULL
4 → NULL
```

Each vertex has a linked list containing its adjacent vertices.

### Why Use an Adjacency List?

Instead of storing every possible pair of vertices, we store only the edges that actually exist.

For example:

```text
Vertex 1 → 2, 3
```

means vertex `1` has edges to vertices `2` and `3`.

### Outdegree Using Adjacency List

The outdegree of a vertex is the number of adjacent vertices in its list.

For:

```text
1 → 2 → 3 → NULL
```

the outdegree of vertex `1` is:

```text
Outdegree(1) = 2
```

because there are two outgoing edges:

```text
1 → 2
1 → 3
```

---

## 2.2 Program

```c
#include <stdio.h>
#include <stdlib.h>

struct Node
{
    int vertex;
    struct Node *next;
};

struct Node* createNode(int vertex)
{
    struct Node *newNode;

    newNode = (struct Node*)malloc(sizeof(struct Node));

    newNode->vertex = vertex;
    newNode->next = NULL;

    return newNode;
}

void insertEdge(struct Node *graph[], int source, int destination)
{
    struct Node *newNode;

    newNode = createNode(destination);

    if (graph[source] == NULL)
    {
        graph[source] = newNode;
    }
    else
    {
        newNode->next = graph[source];
        graph[source] = newNode;
    }
}

void displayAdjList(struct Node *graph[], int vertices)
{
    int i;
    struct Node *temp;

    printf("\nAdjacency List:\n");

    for (i = 0; i < vertices; i++)
    {
        printf("%d -> ", i + 1);

        temp = graph[i];

        while (temp != NULL)
        {
            printf("%d -> ", temp->vertex + 1);
            temp = temp->next;
        }

        printf("NULL\n");
    }
}

void printOutdegree(struct Node *graph[], int vertex)
{
    struct Node *temp;
    int count = 0;

    temp = graph[vertex];

    while (temp != NULL)
    {
        count++;
        temp = temp->next;
    }

    printf("Outdegree of vertex %d = %d\n",
           vertex + 1, count);
}

int main()
{
    struct Node *graph[20] = {NULL};

    int vertices;
    int edges;
    int source, destination;
    int vertex;
    int i;

    printf("Enter number of vertices: ");
    scanf("%d", &vertices);

    printf("Enter number of edges: ");
    scanf("%d", &edges);

    printf("\nEnter directed edges (source destination):\n");

    for (i = 0; i < edges; i++)
    {
        scanf("%d %d", &source, &destination);

        insertEdge(graph, source - 1, destination - 1);
    }

    displayAdjList(graph, vertices);

    printf("\nEnter vertex i to find its outdegree: ");
    scanf("%d", &vertex);

    printOutdegree(graph, vertex - 1);

    return 0;
}
```

---

## 2.3 Program Explanation

### 1. Header Files

```c
#include <stdio.h>
```

Provides:

```text
printf()
scanf()
```

for input and output.

```c
#include <stdlib.h>
```

Provides:

```text
malloc()
```

for dynamic memory allocation.

---

### 2. Define the Linked List Node

```c
struct Node
{
    int vertex;
    struct Node *next;
};
```

Each adjacency-list node contains:

```text
+---------+---------+
| vertex  |  next   |
+---------+---------+
```

`vertex` stores the adjacent vertex.

`next` stores the address of the next adjacency-list node.

---

### 3. `createNode()` Function

```c
struct Node* createNode(int vertex)
```

Creates a new adjacency-list node.

```c
newNode = (struct Node*)malloc(sizeof(struct Node));
```

Dynamically allocates memory for the node.

```c
newNode->vertex = vertex;
```

Stores the adjacent vertex.

```c
newNode->next = NULL;
```

Initially, the node does not point to another node.

```c
return newNode;
```

Returns the address of the new node.

---

### 4. Graph Representation

```c
struct Node *graph[20] = {NULL};
```

This creates an array of pointers.

Each array position represents one vertex.

For example:

```text
graph[0] → adjacency list of vertex 1
graph[1] → adjacency list of vertex 2
graph[2] → adjacency list of vertex 3
```

Initially, every pointer is:

```text
NULL
```

because no edges have been inserted.

---

### 5. `insertEdge()` Function

```c
void insertEdge(struct Node *graph[],
                int source,
                int destination)
```

Adds an edge from `source` to `destination`.

For example:

```text
1 → 3
```

means:

```text
source = 0
destination = 2
```

because the program internally uses zero-based indexes.

A new node is created:

```c
newNode = createNode(destination);
```

If the source vertex has no adjacency list:

```c
if (graph[source] == NULL)
```

the new node becomes the first node.

Otherwise:

```c
newNode->next = graph[source];
graph[source] = newNode;
```

The new node is inserted at the beginning of the linked list.

---

### 6. `displayAdjList()` Function

```c
void displayAdjList(struct Node *graph[], int vertices)
```

Displays the adjacency list of every vertex.

The outer loop:

```c
for (i = 0; i < vertices; i++)
```

selects each vertex.

Then:

```c
temp = graph[i];
```

starts traversal from that vertex's adjacency list.

The linked list is traversed using:

```c
while (temp != NULL)
```

and each adjacent vertex is displayed.

---

### 7. `printOutdegree()` Function

```c
void printOutdegree(struct Node *graph[], int vertex)
```

Calculates the outdegree of a selected vertex.

The traversal starts from:

```c
temp = graph[vertex];
```

Then:

```c
while (temp != NULL)
{
    count++;
    temp = temp->next;
}
```

Each node in the adjacency list represents one outgoing edge.

Therefore, the number of nodes in the list is the outdegree.

For example:

```text
1 → 2 → 3 → NULL
```

There are two adjacency nodes:

```text
2
3
```

Therefore:

```text
Outdegree(1) = 2
```

---

### 8. Accept Number of Vertices

```c
scanf("%d", &vertices);
```

Accepts the total number of vertices.

For example:

```text
1 2 3 4
```

---

### 9. Accept Number of Edges

```c
scanf("%d", &edges);
```

Accepts the total number of edges.

---

### 10. Insert All Edges

```c
for (i = 0; i < edges; i++)
{
    scanf("%d %d", &source, &destination);

    insertEdge(graph, source - 1, destination - 1);
}
```

Each edge is accepted as:

```text
source destination
```

For example:

```text
1 2
```

represents:

```text
1 → 2
```

The values are converted to zero-based indexes using:

```c
source - 1
destination - 1
```

---

### 11. Display Adjacency List

```c
displayAdjList(graph, vertices);
```

Displays all adjacency lists.

---

### 12. Accept Vertex `i`

```c
scanf("%d", &vertex);
```

Accepts the vertex for which the outdegree must be calculated.

For example:

```text
Enter vertex i to find its outdegree: 2
```

---

### 13. Calculate Outdegree

```c
printOutdegree(graph, vertex - 1);
```

The selected vertex is passed to the function.

The function traverses its adjacency list and counts the nodes.

That count is the outdegree of vertex `i`.
