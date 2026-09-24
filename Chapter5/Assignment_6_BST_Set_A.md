# Assignment 6 -- Binary Search Tree (Dynamic)

## SET A

------------------------------------------------------------------------

# 1. Create and Display BST Using Inorder, Preorder and Postorder Traversal

## 1.1 Concept Explanation

A **Binary Search Tree (BST)** is a binary tree in which each node
follows this property:

-   Values smaller than the current node are stored in the **left
    subtree**.
-   Values greater than the current node are stored in the **right
    subtree**.
-   The left and right subtrees are also Binary Search Trees.

A BST is dynamically represented using nodes. Each node contains:

``` text
+--------+--------+---------+
|  Left  |  Data  |  Right  |
+--------+--------+---------+
```

-   `data` stores the integer value.
-   `left` stores the address of the left child.
-   `right` stores the address of the right child.
-   `NULL` means that the corresponding child does not exist.
-   `root` stores the address of the first node of the tree.

Since the tree is dynamic, every new node is created using `malloc()`.

### Tree Traversals

A traversal means visiting every node of the tree exactly once.

### Inorder Traversal

``` text
Left → Root → Right
```

For a BST, inorder traversal displays the elements in ascending order.

### Preorder Traversal

``` text
Root → Left → Right
```

The root node is visited first.

### Postorder Traversal

``` text
Left → Right → Root
```

The root node is visited last.

For example, if the following values are inserted:

``` text
50 30 70 20 40 60 80
```

The BST becomes:

``` text
             50
           /    \
         30      70
        /  \    /  \
      20   40  60   80
```

The traversal orders are:

``` text
Inorder:    20 30 40 50 60 70 80
Preorder:   50 30 20 40 70 60 80
Postorder:  20 40 30 60 80 70 50
```

------------------------------------------------------------------------

## 1.2 Program

``` c
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

void inorder(struct BST *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

void preorder(struct BST *root)
{
    if (root != NULL)
    {
        printf("%d ", root->data);
        preorder(root->left);
        preorder(root->right);
    }
}

void postorder(struct BST *root)
{
    if (root != NULL)
    {
        postorder(root->left);
        postorder(root->right);
        printf("%d ", root->data);
    }
}

int main()
{
    struct BST *root = NULL;
    int n, value, i;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter %d elements:\n", n);

    for (i = 0; i < n; i++)
    {
        scanf("%d", &value);
        root = insert(root, value);
    }

    printf("\nInorder Traversal: ");
    inorder(root);

    printf("\nPreorder Traversal: ");
    preorder(root);

    printf("\nPostorder Traversal: ");
    postorder(root);

    return 0;
}
```

------------------------------------------------------------------------

## 1.3 Program Explanation

### 1. `#include <stdio.h>`

``` c
#include <stdio.h>
```

Includes the standard input/output library.

It provides functions such as:

-   `printf()` for displaying output.
-   `scanf()` for accepting input.

### 2. `#include <stdlib.h>`

``` c
#include <stdlib.h>
```

Includes functions related to dynamic memory allocation.

It provides `malloc()`, which is used to create BST nodes dynamically.

------------------------------------------------------------------------

### 3. Define the BST Node

``` c
struct BST
{
    int data;
    struct BST *left;
    struct BST *right;
};
```

This structure represents one node of the BST.

``` text
data
```

Stores the integer value.

``` text
left
```

Stores the address of the left child.

``` text
right
```

Stores the address of the right child.

A node can therefore be visualized as:

``` text
+--------+--------+---------+
|  left  |  data  |  right  |
+--------+--------+---------+
```

------------------------------------------------------------------------

### 4. `insert()` Function

``` c
struct BST* insert(struct BST *root, int value)
```

This function inserts a new value into the BST.

It returns a pointer to the root of the tree/subtree.

------------------------------------------------------------------------

### 5. Create a New Node

``` c
if (root == NULL)
```

Checks whether the current position is empty.

If it is `NULL`, there is no node at that position, so a new node can be
created there.

``` c
newNode = (struct BST*)malloc(sizeof(struct BST));
```

`malloc()` dynamically allocates memory for one `struct BST`.

``` c
newNode->data = value;
```

Stores the value in the new node.

``` c
newNode->left = NULL;
newNode->right = NULL;
```

Initially, the new node has no children.

``` c
return newNode;
```

Returns the address of the newly created node.

------------------------------------------------------------------------

### 6. Insert on the Left

``` c
if (value < root->data)
```

If the new value is smaller than the current node, it belongs in the
left subtree.

``` c
root->left = insert(root->left, value);
```

The insertion function is called recursively for the left subtree.

------------------------------------------------------------------------

### 7. Insert on the Right

``` c
else if (value > root->data)
```

If the new value is greater than the current node, it belongs in the
right subtree.

``` c
root->right = insert(root->right, value);
```

The insertion function is called recursively for the right subtree.

------------------------------------------------------------------------

### 8. Return Root

``` c
return root;
```

Returns the current root after insertion.

This is important because the root pointer must remain connected to the
complete tree.

------------------------------------------------------------------------

### 9. Inorder Traversal

``` c
void inorder(struct BST *root)
```

The function performs:

``` text
Left → Root → Right
```

``` c
if (root != NULL)
```

Checks whether the current node exists.

``` c
inorder(root->left);
```

First visits the left subtree.

``` c
printf("%d ", root->data);
```

Then displays the current node.

``` c
inorder(root->right);
```

Finally visits the right subtree.

Therefore:

``` text
Left
  ↓
Root
  ↓
Right
```

------------------------------------------------------------------------

### 10. Preorder Traversal

``` c
void preorder(struct BST *root)
```

The function performs:

``` text
Root → Left → Right
```

``` c
printf("%d ", root->data);
```

The current node is displayed first.

``` c
preorder(root->left);
```

Then the left subtree is visited.

``` c
preorder(root->right);
```

Then the right subtree is visited.

------------------------------------------------------------------------

### 11. Postorder Traversal

``` c
void postorder(struct BST *root)
```

The function performs:

``` text
Left → Right → Root
```

``` c
postorder(root->left);
```

First visits the left subtree.

``` c
postorder(root->right);
```

Then visits the right subtree.

``` c
printf("%d ", root->data);
```

Finally displays the current node.

------------------------------------------------------------------------

### 12. `main()` Function

``` c
struct BST *root = NULL;
```

Creates the root pointer.

Initially the tree is empty, so:

``` text
root = NULL
```

------------------------------------------------------------------------

### 13. Accept Number of Elements

``` c
scanf("%d", &n);
```

Accepts the number of elements that the user wants to insert.

------------------------------------------------------------------------

### 14. Insert All Elements

``` c
for (i = 0; i < n; i++)
{
    scanf("%d", &value);
    root = insert(root, value);
}
```

The loop accepts each value one by one.

For every value:

``` text
Input value
    ↓
insert()
    ↓
Compare with root
    ↓
Move left or right
    ↓
Create node at NULL position
```

------------------------------------------------------------------------

### 15. Display Traversals

``` c
inorder(root);
```

Displays the tree using inorder traversal.

``` c
preorder(root);
```

Displays the tree using preorder traversal.

``` c
postorder(root);
```

Displays the tree using postorder traversal.

------------------------------------------------------------------------

# 2. Implement BST with Insert, Count Non-Leaf, Count Leaf and Count Total Nodes

## 2.1 Concept Explanation

This program implements a dynamic Binary Search Tree containing integer
values.

The operations required are:

1.  `insert()` -- inserts a new element into the BST.
2.  `count_nonleaf()` -- counts nodes having at least one child.
3.  `count_leaf()` -- counts nodes having no children.
4.  `count_total_nodes()` -- counts all nodes in the tree.

### Leaf Node

A node is called a **leaf node** when it has no child.

``` text
left == NULL
AND
right == NULL
```

Example:

``` text
       50
      /
    30
   /  \
 20   40
```

Here `20` and `40` are leaf nodes.

### Non-Leaf Node

A node is called a **non-leaf node** when it has at least one child.

In the same tree:

``` text
       50
      /
    30
```

Both `50` and `30` are non-leaf nodes.

### Total Nodes

The total number of nodes includes both leaf and non-leaf nodes.

The relationship is:

``` text
Total Nodes = Leaf Nodes + Non-Leaf Nodes
```

For example:

``` text
             50
           /    \
         30      70
        /  \    /  \
      20   40  60   80
```

There are:

``` text
Leaf Nodes     = 4
Non-Leaf Nodes = 3
Total Nodes    = 7
```

------------------------------------------------------------------------

## 2.2 Program

``` c
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

int count_leaf(struct BST *root)
{
    if (root == NULL)
    {
        return 0;
    }

    if (root->left == NULL && root->right == NULL)
    {
        return 1;
    }

    return count_leaf(root->left) + count_leaf(root->right);
}

int count_nonleaf(struct BST *root)
{
    if (root == NULL)
    {
        return 0;
    }

    if (root->left == NULL && root->right == NULL)
    {
        return 0;
    }

    return 1 + count_nonleaf(root->left)
             + count_nonleaf(root->right);
}

int count_total_nodes(struct BST *root)
{
    if (root == NULL)
    {
        return 0;
    }

    return 1 + count_total_nodes(root->left)
             + count_total_nodes(root->right);
}

int main()
{
    struct BST *root = NULL;
    int choice;
    int value;

    do
    {
        printf("\n\n----- BINARY SEARCH TREE -----");
        printf("\n1. Insert");
        printf("\n2. Count Leaf Nodes");
        printf("\n3. Count Non-Leaf Nodes");
        printf("\n4. Count Total Nodes");
        printf("\n5. Exit");

        printf("\nEnter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                printf("Enter value to insert: ");
                scanf("%d", &value);

                root = insert(root, value);

                printf("Element inserted successfully.");
                break;

            case 2:
                printf("Number of leaf nodes = %d",
                       count_leaf(root));
                break;

            case 3:
                printf("Number of non-leaf nodes = %d",
                       count_nonleaf(root));
                break;

            case 4:
                printf("Total number of nodes = %d",
                       count_total_nodes(root));
                break;

            case 5:
                printf("Exiting...");
                break;

            default:
                printf("Invalid choice!");
        }

    } while (choice != 5);

    return 0;
}
```

------------------------------------------------------------------------

## 2.3 Program Explanation

### 1. Header Files

``` c
#include <stdio.h>
```

Provides `printf()` and `scanf()`.

``` c
#include <stdlib.h>
```

Provides `malloc()` for dynamic memory allocation.

------------------------------------------------------------------------

### 2. BST Structure

``` c
struct BST
{
    int data;
    struct BST *left;
    struct BST *right;
};
```

Each node contains:

``` text
left  → address of left child
data  → integer value
right → address of right child
```

------------------------------------------------------------------------

### 3. `insert()` Function

``` c
struct BST* insert(struct BST *root, int value)
```

Inserts a new integer into the BST.

If:

``` c
root == NULL
```

a new node is created using:

``` c
malloc(sizeof(struct BST))
```

The new node stores:

``` c
newNode->data = value;
newNode->left = NULL;
newNode->right = NULL;
```

If:

``` c
value < root->data
```

the value is inserted into the left subtree.

If:

``` c
value > root->data
```

the value is inserted into the right subtree.

------------------------------------------------------------------------

### 4. `count_leaf()` Function

``` c
int count_leaf(struct BST *root)
```

Counts all leaf nodes.

First:

``` c
if (root == NULL)
{
    return 0;
}
```

If there is no node, there are no leaf nodes.

Then:

``` c
if (root->left == NULL && root->right == NULL)
{
    return 1;
}
```

This checks whether the current node has no children.

If both child pointers are `NULL`, the current node is a leaf, so the
function returns `1`.

Otherwise:

``` c
return count_leaf(root->left) + count_leaf(root->right);
```

The function counts leaf nodes in both subtrees and adds them.

------------------------------------------------------------------------

### 5. `count_nonleaf()` Function

``` c
int count_nonleaf(struct BST *root)
```

Counts nodes that are not leaf nodes.

If the tree is empty:

``` c
if (root == NULL)
{
    return 0;
}
```

If the current node has no children:

``` c
if (root->left == NULL && root->right == NULL)
{
    return 0;
}
```

It is a leaf, so it should not be counted as a non-leaf.

Otherwise:

``` c
return 1 + count_nonleaf(root->left)
         + count_nonleaf(root->right);
```

The `1` counts the current non-leaf node.

The remaining two function calls count non-leaf nodes in the left and
right subtrees.

------------------------------------------------------------------------

### 6. `count_total_nodes()` Function

``` c
int count_total_nodes(struct BST *root)
```

Counts every node in the tree.

If:

``` c
root == NULL
```

there is no node:

``` c
return 0;
```

Otherwise:

``` c
return 1 + count_total_nodes(root->left)
         + count_total_nodes(root->right);
```

Here:

``` text
1
```

counts the current node.

``` text
count_total_nodes(root->left)
```

counts nodes in the left subtree.

``` text
count_total_nodes(root->right)
```

counts nodes in the right subtree.

Therefore:

``` text
Total =
Current Node
+
Left Subtree Nodes
+
Right Subtree Nodes
```

------------------------------------------------------------------------

### 7. `main()` Function

``` c
struct BST *root = NULL;
```

Initially, the BST is empty.

``` c
int choice;
int value;
```

`choice` stores the menu selection and `value` stores the integer to
insert.

------------------------------------------------------------------------

### 8. `do-while` Menu

``` c
do
{
    ...
} while (choice != 5);
```

The menu is displayed at least once.

The menu continues until the user selects option `5`.

------------------------------------------------------------------------

### 9. Insert Operation

``` c
case 1:
```

Executes when the user selects Insert.

``` c
scanf("%d", &value);
```

Accepts the value.

``` c
root = insert(root, value);
```

Inserts the value into the BST and updates the root pointer.

------------------------------------------------------------------------

### 10. Count Leaf Nodes

``` c
case 2:
```

Calls:

``` c
count_leaf(root)
```

and displays the number of leaf nodes.

------------------------------------------------------------------------

### 11. Count Non-Leaf Nodes

``` c
case 3:
```

Calls:

``` c
count_nonleaf(root)
```

and displays the number of non-leaf nodes.

------------------------------------------------------------------------

### 12. Count Total Nodes

``` c
case 4:
```

Calls:

``` c
count_total_nodes(root)
```

and displays the total number of nodes.

------------------------------------------------------------------------

### 13. Exit

``` c
case 5:
```

Terminates the menu loop.

The condition:

``` c
while (choice != 5);
```

becomes false when the user enters `5`, so the program ends.
