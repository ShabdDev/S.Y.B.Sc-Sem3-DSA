# Assignment 6 – Binary Search Tree (Dynamic)

## SET C

---

# 1. Create Binary Search Tree and Delete a Specific Node

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

The operation required in this program is:

1. `insert()` – creates the BST by inserting elements.
2. `delete()` – deletes a specific node from the BST.

## Node Deletion in BST

Deleting a node from a BST has three cases.

### Case 1: Node is a Leaf

A leaf node has no children.

Example:

```text
       50
      /  \
    30    70
```

If `30` is deleted:

```text
       50
         \
          70
```

The parent's pointer is changed to `NULL`.

---

### Case 2: Node Has One Child

Example:

```text
       50
      /
    30
      \
       40
```

If `30` is deleted, its child `40` takes its position:

```text
       50
      /
    40
```

The parent is connected directly to the deleted node's child.

---

### Case 3: Node Has Two Children

Example:

```text
          50
         /  \
       30    70
            /  \
           60   80
```

If `70` is deleted, it has two children.

We replace its value with the **inorder successor**.

The inorder successor is the smallest value in the right subtree.

For `70`:

```text
Right subtree:
       80
```

If the right subtree were:

```text
       70
      /  \
    60    80
         /
        75
```

the inorder successor of `70` would be `75`.

The deletion process is:

```text
Find node
   ↓
Node has 0 children → delete directly
   ↓
Node has 1 child → connect parent to child
   ↓
Node has 2 children → find inorder successor
                       ↓
                    Copy value
                       ↓
                 Delete successor
```

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

struct BST* findMin(struct BST *root)
{
    while (root->left != NULL)
    {
        root = root->left;
    }

    return root;
}

struct BST* deleteNode(struct BST *root, int key)
{
    struct BST *temp;

    if (root == NULL)
    {
        return NULL;
    }

    if (key < root->data)
    {
        root->left = deleteNode(root->left, key);
    }
    else if (key > root->data)
    {
        root->right = deleteNode(root->right, key);
    }
    else
    {
        if (root->left == NULL && root->right == NULL)
        {
            free(root);
            return NULL;
        }

        if (root->left == NULL)
        {
            temp = root->right;
            free(root);
            return temp;
        }

        if (root->right == NULL)
        {
            temp = root->left;
            free(root);
            return temp;
        }

        temp = findMin(root->right);

        root->data = temp->data;

        root->right = deleteNode(root->right, temp->data);
    }

    return root;
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

    int n, value, key, i;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter elements:\n");

    for (i = 0; i < n; i++)
    {
        scanf("%d", &value);
        root = insert(root, value);
    }

    printf("\nInorder before deletion: ");
    inorder(root);

    printf("\nEnter element to delete: ");
    scanf("%d", &key);

    root = deleteNode(root, key);

    printf("\nInorder after deletion: ");
    inorder(root);

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

Provides dynamic memory functions such as `malloc()` and `free()`.

---

### 2. Define the BST Node

```c
struct BST
{
    int data;
    struct BST *left;
    struct BST *right;
};
```

Each BST node contains:

```text
left  → address of left child
data  → integer value
right → address of right child
```

---

### 3. `insert()` Function

```c
struct BST* insert(struct BST *root, int value)
```

This function inserts a value into the BST.

If:

```c
root == NULL
```

the current position is empty.

A new node is created:

```c
newNode = (struct BST*)malloc(sizeof(struct BST));
```

The value is stored:

```c
newNode->data = value;
```

Both child pointers are initially set to `NULL`:

```c
newNode->left = NULL;
newNode->right = NULL;
```

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

---

### 4. `findMin()` Function

```c
struct BST* findMin(struct BST *root)
```

This function finds the smallest node in a subtree.

In a BST, the smallest value is always found by repeatedly moving to the left.

```c
while (root->left != NULL)
{
    root = root->left;
}
```

When `root->left` becomes `NULL`, the current node contains the minimum value.

For example:

```text
        70
       /
     60
    /
   50
```

The minimum value is:

```text
50
```

Therefore:

```c
return root;
```

returns the address of the node containing the smallest value.

---

### 5. `deleteNode()` Function

```c
struct BST* deleteNode(struct BST *root, int key)
```

This function searches for and deletes the specified node.

There are three main deletion cases.

---

### 6. Empty Tree

```c
if (root == NULL)
{
    return NULL;
}
```

If the tree/subtree is empty, the required node does not exist.

---

### 7. Search in Left Subtree

```c
if (key < root->data)
{
    root->left = deleteNode(root->left, key);
}
```

If the key is smaller than the current node's value, the node must be somewhere in the left subtree.

The deletion function is therefore called recursively on the left subtree.

---

### 8. Search in Right Subtree

```c
else if (key > root->data)
{
    root->right = deleteNode(root->right, key);
}
```

If the key is greater than the current node's value, the node must be somewhere in the right subtree.

The deletion function is therefore called recursively on the right subtree.

---

### 9. Node Found

```c
else
```

This means:

```c
key == root->data
```

The node to be deleted has been found.

Now we determine whether it has:

```text
0 children
1 child
2 children
```

---

### 10. Case 1 – Leaf Node

```c
if (root->left == NULL && root->right == NULL)
{
    free(root);
    return NULL;
}
```

Both child pointers are `NULL`.

Therefore, the node is a leaf.

```c
free(root);
```

releases the dynamically allocated memory occupied by the node.

```c
return NULL;
```

tells the parent that this child no longer exists.

---

### 11. Case 2 – Only Right Child

```c
if (root->left == NULL)
{
    temp = root->right;
    free(root);
    return temp;
}
```

The node has no left child but has a right child.

The right child is saved:

```c
temp = root->right;
```

The current node is deleted:

```c
free(root);
```

The right child is returned:

```c
return temp;
```

The parent will then point directly to that child.

---

### 12. Case 2 – Only Left Child

```c
if (root->right == NULL)
{
    temp = root->left;
    free(root);
    return temp;
}
```

The node has no right child but has a left child.

The left child is saved, the current node is freed, and the left child is returned.

---

### 13. Case 3 – Two Children

If the code reaches this point, the node has both children.

```c
temp = findMin(root->right);
```

The smallest node in the right subtree is found.

This node is the **inorder successor**.

Then:

```c
root->data = temp->data;
```

The inorder successor's value is copied into the node being deleted.

The original successor node is then deleted:

```c
root->right = deleteNode(root->right, temp->data);
```

This works because the inorder successor is located in the right subtree.

---

### 14. Return the Root

```c
return root;
```

The updated root of the current subtree is returned.

This is important because deletion can change the root of a subtree.

---

### 15. `inorder()` Function

```c
void inorder(struct BST *root)
```

Displays the BST using:

```text
Left → Root → Right
```

For a normal BST, this displays the elements in ascending order.

It is used before and after deletion so that the effect of deletion can be observed.

---

### 16. `main()` Function

```c
struct BST *root = NULL;
```

Initially, the tree is empty.

The user enters the number of elements:

```c
scanf("%d", &n);
```

Each element is inserted:

```c
root = insert(root, value);
```

The tree is displayed before deletion:

```c
inorder(root);
```

The user enters the node to delete:

```c
scanf("%d", &key);
```

The deletion operation is performed:

```c
root = deleteNode(root, key);
```

The updated tree is displayed:

```c
inorder(root);
```
