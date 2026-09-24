# Assignment 6 – Binary Search Tree (Dynamic)

## SET B

---

# 1. Implement Binary Search Tree with Tree Copy and Comparison of Two Trees

## 1.1 Concept Explanation

A **Binary Search Tree (BST)** is a binary tree in which:

- Values smaller than a node are stored in its left subtree.
- Values greater than a node are stored in its right subtree.
- The left and right subtrees also follow the same BST property.

A dynamic BST is represented using linked nodes. Each node contains:

```text
+--------+--------+---------+
|  Left  |  Data  |  Right  |
+--------+--------+---------+
```

- `data` stores the integer value.
- `left` stores the address of the left child.
- `right` stores the address of the right child.
- `NULL` indicates that a child does not exist.
- `root` stores the address of the first node.

The two operations required in this program are:

1. `tcopy()` – creates a copy of an existing BST.
2. `tcompare()` – compares two BSTs.

### Tree Copy

Tree copying means creating a new tree having the same structure and data as the original tree.

For example:

```text
Original Tree:              Copied Tree:

       50                         50
      /  \                       /  \
    30    70                   30    70
   /  \    \                  /  \    \
 20   40    80               20   40    80
```

The copied tree contains separate dynamically allocated nodes. It is not simply another pointer pointing to the original tree.

### Tree Comparison

Two trees are considered equal when:

1. Both corresponding nodes contain the same data.
2. Their corresponding left subtrees are equal.
3. Their corresponding right subtrees are equal.
4. Both trees have the same structure.

For example:

```text
Tree 1:                    Tree 2:

    50                        50
   /  \                      /  \
 30    70                   30    70
```

These trees are equal.

But:

```text
Tree 1:                    Tree 2:

    50                        50
   /                           \
 30                             30
```

These trees are not equal because their structures are different.

---

## 1.2 Program

```c
#include <stdio.h>
#include <stdlib.h>

struct BST
{
    int data;
    struct BST *left;
    struct BST *right;
};

struct BST* insert(struct BST *root, int value)
{
    struct BST *newNode;

    if (root == NULL)
    {
        newNode = (struct BST*)malloc(sizeof(struct BST));

        newNode->data = value;
        newNode->left = NULL;
        newNode->right = NULL;

        return newNode;
    }

    if (value < root->data)
    {
        root->left = insert(root->left, value);
    }
    else if (value > root->data)
    {
        root->right = insert(root->right, value);
    }

    return root;
}

struct BST* tcopy(struct BST *root)
{
    struct BST *newNode;

    if (root == NULL)
    {
        return NULL;
    }

    newNode = (struct BST*)malloc(sizeof(struct BST));

    newNode->data = root->data;
    newNode->left = tcopy(root->left);
    newNode->right = tcopy(root->right);

    return newNode;
}

int tcompare(struct BST *root1, struct BST *root2)
{
    if (root1 == NULL && root2 == NULL)
    {
        return 1;
    }

    if (root1 == NULL || root2 == NULL)
    {
        return 0;
    }

    if (root1->data != root2->data)
    {
        return 0;
    }

    return tcompare(root1->left, root2->left) &&
           tcompare(root1->right, root2->right);
}

void inorder(struct BST *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

int main()
{
    struct BST *root1 = NULL;
    struct BST *root2 = NULL;
    int n, value, i;

    printf("Enter number of elements for Tree 1: ");
    scanf("%d", &n);

    printf("Enter elements:\n");

    for (i = 0; i < n; i++)
    {
        scanf("%d", &value);
        root1 = insert(root1, value);
    }

    root2 = tcopy(root1);

    printf("\nTree 1 Inorder: ");
    inorder(root1);

    printf("\nTree 2 Inorder: ");
    inorder(root2);

    if (tcompare(root1, root2))
    {
        printf("\nTrees are equal.");
    }
    else
    {
        printf("\nTrees are not equal.");
    }

    return 0;
}
```

---

## 1.3 Program Explanation

### 1. Header Files

```c
#include <stdio.h>
```

Provides input/output functions such as `printf()` and `scanf()`.

```c
#include <stdlib.h>
```

Provides `malloc()` for dynamic memory allocation.

### 2. Define the BST Node

```c
struct BST
{
    int data;
    struct BST *left;
    struct BST *right;
};
```

Each node contains three fields:

```text
left  → address of left child
data  → integer value
right → address of right child
```

### 3. `insert()` Function

```c
struct BST* insert(struct BST *root, int value)
```

This function inserts a value into the BST.

If:

```c
root == NULL
```

the current position is empty, so a new node is created.

```c
newNode = (struct BST*)malloc(sizeof(struct BST));
```

Memory is allocated dynamically.

Then:

```c
newNode->data = value;
newNode->left = NULL;
newNode->right = NULL;
```

The new node stores the value and initially has no children.

If:

```c
value < root->data
```

the value is inserted into the left subtree.

If:

```c
value > root->data
```

the value is inserted into the right subtree.

### 4. `tcopy()` Function

```c
struct BST* tcopy(struct BST *root)
```

This function creates a separate copy of the complete tree.

First:

```c
if (root == NULL)
{
    return NULL;
}
```

If there is no node, there is nothing to copy.

Then a new node is created:

```c
newNode = (struct BST*)malloc(sizeof(struct BST));
```

The current node's data is copied:

```c
newNode->data = root->data;
```

The left subtree is copied recursively:

```c
newNode->left = tcopy(root->left);
```

The right subtree is copied recursively:

```c
newNode->right = tcopy(root->right);
```

Finally:

```c
return newNode;
```

returns the address of the newly created copy.

Every node of the original tree gets a new dynamically allocated node in the copied tree.

### 5. `tcompare()` Function

```c
int tcompare(struct BST *root1, struct BST *root2)
```

This function compares two trees.

#### Case 1: Both Trees Are Empty

```c
if (root1 == NULL && root2 == NULL)
{
    return 1;
}
```

If both corresponding positions are `NULL`, they match.

So the function returns `1`.

#### Case 2: Only One Tree Has a Node

```c
if (root1 == NULL || root2 == NULL)
{
    return 0;
}
```

If one node exists and the other does not, the structures are different.

Therefore, the function returns `0`.

#### Case 3: Data Is Different

```c
if (root1->data != root2->data)
{
    return 0;
}
```

If corresponding nodes contain different values, the trees are not equal.

#### Case 4: Compare Left and Right Subtrees

```c
return tcompare(root1->left, root2->left) &&
       tcompare(root1->right, root2->right);
```

The left subtrees are compared first.

Then the right subtrees are compared.

The `&&` operator means that both comparisons must return `1`.

Therefore:

```text
Current data is equal
        AND
Left subtrees are equal
        AND
Right subtrees are equal
```

### 6. `inorder()` Function

```c
void inorder(struct BST *root)
```

This function displays the tree using:

```text
Left → Root → Right
```

It is used to display both the original and copied trees.

### 7. `main()` Function

```c
struct BST *root1 = NULL;
struct BST *root2 = NULL;
```

Two root pointers are created.

```text
root1 → Original Tree
root2 → Copied Tree
```

The first tree is created using `insert()`.

```c
root1 = insert(root1, value);
```

After creating Tree 1:

```c
root2 = tcopy(root1);
```

creates a separate copy.

The two trees are then compared:

```c
if (tcompare(root1, root2))
```

If `tcompare()` returns `1`, the trees are equal.

If it returns `0`, the trees are not equal.

---

# 2. Implement Binary Search Tree with Search and Mirror Operations

## 2.1 Concept Explanation

This program implements a dynamic Binary Search Tree with the following operations:

1. `insert()` – inserts a new element into the BST.
2. `search()` – searches for an element in the BST.
3. `mirror()` – finds the mirror image of the tree.

### Searching in BST

In a BST, searching uses the BST property.

For a node containing `50`:

```text
       50
      /  \
```

If the search value is smaller than `50`, search the left subtree.

If the search value is greater than `50`, search the right subtree.

If the search value is equal to `50`, the element is found.

The search process is:

```text
Key < Root
   ↓
Search Left

Key > Root
   ↓
Search Right

Key == Root
   ↓
Element Found
```

### Mirror of a Binary Tree

The mirror operation exchanges the left and right child of every node.

Original:

```text
             50
           /    \
         30      70
        /  \    /  \
      20   40  60   80
```

Mirror:

```text
             50
           /    \
         70      30
        /  \    /  \
      80   60  40   20
```

For each node:

```text
Swap Left and Right
        ↓
Mirror Left Subtree
        ↓
Mirror Right Subtree
```

---

## 2.2 Program

```c
#include <stdio.h>
#include <stdlib.h>

struct BST
{
    int data;
    struct BST *left;
    struct BST *right;
};

struct BST* insert(struct BST *root, int value)
{
    struct BST *newNode;

    if (root == NULL)
    {
        newNode = (struct BST*)malloc(sizeof(struct BST));

        newNode->data = value;
        newNode->left = NULL;
        newNode->right = NULL;

        return newNode;
    }

    if (value < root->data)
    {
        root->left = insert(root->left, value);
    }
    else if (value > root->data)
    {
        root->right = insert(root->right, value);
    }

    return root;
}

struct BST* search(struct BST *root, int key)
{
    if (root == NULL)
    {
        return NULL;
    }

    if (key == root->data)
    {
        return root;
    }

    if (key < root->data)
    {
        return search(root->left, key);
    }

    return search(root->right, key);
}

void mirror(struct BST *root)
{
    struct BST *temp;

    if (root == NULL)
    {
        return;
    }

    temp = root->left;
    root->left = root->right;
    root->right = temp;

    mirror(root->left);
    mirror(root->right);
}

void inorder(struct BST *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

int main()
{
    struct BST *root = NULL;
    struct BST *result = NULL;
    int n, value, key, i;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter elements:\n");

    for (i = 0; i < n; i++)
    {
        scanf("%d", &value);
        root = insert(root, value);
    }

    printf("\nOriginal Tree Inorder: ");
    inorder(root);

    printf("\nEnter element to search: ");
    scanf("%d", &key);

    result = search(root, key);

    if (result != NULL)
    {
        printf("Element %d is found in the tree.", key);
    }
    else
    {
        printf("Element %d is not found in the tree.", key);
    }

    mirror(root);

    printf("\nMirror Tree Inorder: ");
    inorder(root);

    return 0;
}
```

---

## 2.3 Program Explanation

### 1. Header Files

```c
#include <stdio.h>
```

Provides `printf()` and `scanf()`.

```c
#include <stdlib.h>
```

Provides `malloc()` for dynamic memory allocation.

### 2. BST Structure

```c
struct BST
{
    int data;
    struct BST *left;
    struct BST *right;
};
```

The node contains:

```text
left  → address of left child
data  → integer value
right → address of right child
```

### 3. `insert()` Function

```c
struct BST* insert(struct BST *root, int value)
```

Inserts an integer into the BST.

If:

```c
root == NULL
```

a new node is dynamically created.

If:

```c
value < root->data
```

the value is inserted into the left subtree.

If:

```c
value > root->data
```

the value is inserted into the right subtree.

The function returns the root pointer.

### 4. `search()` Function

```c
struct BST* search(struct BST *root, int key)
```

Searches for the specified `key`.

#### Empty Tree

```c
if (root == NULL)
{
    return NULL;
}
```

If the current subtree is empty, the element is not present.

#### Element Found

```c
if (key == root->data)
{
    return root;
}
```

If the key matches the current node, its address is returned.

#### Search Left

```c
if (key < root->data)
{
    return search(root->left, key);
}
```

If the key is smaller than the current node, only the left subtree is searched.

#### Search Right

```c
return search(root->right, key);
```

If the key is greater than the current node, the right subtree is searched.

### 5. `mirror()` Function

```c
void mirror(struct BST *root)
```

Creates the mirror image of the tree.

If:

```c
root == NULL
```

there is nothing to mirror.

The left and right pointers are exchanged:

```c
temp = root->left;
root->left = root->right;
root->right = temp;
```

Before:

```text
        root
       /    \
    left   right
```

After:

```text
        root
       /    \
    right   left
```

The same operation is then performed recursively:

```c
mirror(root->left);
mirror(root->right);
```

Thus, every node is mirrored.

### 6. `inorder()` Function

```c
void inorder(struct BST *root)
```

Displays the tree using:

```text
Left → Root → Right
```

It is used to display the original and mirror trees.

### 7. `main()` Function

```c
struct BST *root = NULL;
```

Initially, the BST is empty.

The elements are inserted using:

```c
root = insert(root, value);
```

The original tree is displayed:

```c
inorder(root);
```

The user enters a value to search:

```c
scanf("%d", &key);
```

The search is performed:

```c
result = search(root, key);
```

If:

```c
result != NULL
```

the element is present.

Otherwise, it is not present.

Finally:

```c
mirror(root);
```

converts the tree into its mirror image.

The mirror tree is displayed using:

```c
inorder(root);
```
