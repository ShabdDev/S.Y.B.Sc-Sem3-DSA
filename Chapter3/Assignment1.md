Linked List 

```
 
INTRODUCTION 

Linked List: 
A linked list is a linear data structure. It is collection of items, which are not stored at contiguous memory locations.
The elements in a linked list are connected using pointers. 
IMPLEMENTATION OF LINKED LIST 
A linked list may be implemented in two ways 
1) Static representation 
2) Dynamic representation. 
 
1) Static Representation:  
   An array is used to store the elements of the list. Two arrays are used : first array to store data and 
second array to store link. 
  Index   Data             Link (Next Index) 
           ------------------------------------------------- 
  0     Mango          3   → points to index 3 
  3     Banana         1   → points to index 1 
  1     Orange         6   → points to index 6 
  6     Grapes        -1   → end of list 
 
2) Dynamic Representation:  
• A linked list is a dynamic data structure when a new data is added, the size should increase and  
    when elements are deleted, its size should decrease. 
• To store a list in memory, dynamically memory is allocated for each node and linking them by  
     means of pointers since each node will be at random memory location. We will need a pointer to    
    store the address of the first node(head).

 TYPES OF LINKED LIST 
•  Singly Linkedlist 
•  Singly Circular Linkedlist 
•  Doubly Linkedlist 
•  Doubly Circular Linkedlist 
1) Singly Linked list- Each node has two parts: data and next. In ‘data’ we can store any type of data 
and ‘next’ is a pointer pointing to nextnode.
2) Singly Circular Linked list - In this list, the last node points back to the first node i.e. last  
    node contains the address of the first node.
3) Doubly Linked list - Each node in this contains two pointers, one pointing to the previous node  
  and the other pointing to the next node. This list is used when traversing in both directions is  
  required.
4) Doubly Circular Linked list – 
In this list, the last node does not contain a NULL pointer but points back to the first node i.e. it 
contains the address of the first node.

 OPERATIONS ON A LIST -The following are some of the basic list operation  
 
1. Insertion 
a) Insert at Beginning b) Insert at End c) Insert at Position 
• Create a new node. 
• Point its next to the 
current head. 
• Update head to point to 
the new node. 
• Traverse to the last 
node. 
• Point its next to the new 
node. 
• Traverse to the node 
before the position. 
• Insert the new node 
between them. 
Before:                                  
[10] → [20]        
After: 
[5] → [10] → [20] 
Before:      
[10] → [20]                                                     
After: 
 [10] → [20] → [30] 
Before:  
[10] → [30]                                                         
After: 
[10] → [20] → [30] 
 
 
2. Deletion 
a) Delete from Beginning b) Delete from End c) Delete by Value/ Position 
• Update head to head->next • Traverse to the second
last node. 
• Set its next to NULL. 
• Find node before the 
target. 
• Change its next to skip 
the target node. 
Before: 
[10] → [20]                                  
After: 
 [20] 
Before: 
[10] → [20]                                                             
After: 
     [10] 
Before:  
[10] → [30]                                                         
After: 
[10] → [20] → [30] 
 
 
3. Traversal 
• Start at the head. 
• Move node by node using the next pointer. 
• Display or process data at each node. 
4. Search 
• Traverse the list. 
• Compare each node's data with the target. 
• Return position or address if found. 
 
Search for 20: 
[10] → [20] → [30] 
            ↑ 
                 Match! 
5. Count Nodes / Length 
• Similar to traversal. 
• Use a counter and increment at each node.

6. Reverse the Linked List 
• Re-point the next pointers in reverse. 
• Use three pointers: prev, current, next. 
                   Before: Head → [10] → [20] → [30] → NULL 
                   After:  Head → [30] → [20] → [10] → NULL 
 
7. Sort the List 
• Use basic sorting algorithms (Bubble, Insertion). 
• Compare node data and swap.
```

# SET A 
```

1) Write a C program to implement a Singly linked list with following operations: 
create() , display(), insert(),delete()

#include <stdio.h>
#include <stdlib.h>

/* Structure for a node */
struct Node
{
    int data;
    struct Node *next;
};

struct Node *head = NULL;

/* Function to create linked list */
void create()
{
    int n, i, value;
    struct Node *newNode, *temp;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    if (n <= 0)
    {
        printf("Invalid number of nodes.\n");
        return;
    }

    head = NULL;

    for (i = 0; i < n; i++)
    {
        newNode = (struct Node *)malloc(sizeof(struct Node));

        if (newNode == NULL)
        {
            printf("Memory allocation failed.\n");
            return;
        }

        printf("Enter data for node %d: ", i + 1);
        scanf("%d", &value);

        newNode->data = value;
        newNode->next = NULL;

        if (head == NULL)
        {
            head = newNode;
        }
        else
        {
            temp = head;

            while (temp->next != NULL)
            {
                temp = temp->next;
            }

            temp->next = newNode;
        }
    }

    printf("Linked list created successfully.\n");
}

/* Function to display linked list */
void display()
{
    struct Node *temp = head;

    if (head == NULL)
    {
        printf("Linked list is empty.\n");
        return;
    }

    printf("Linked List: ");

    while (temp != NULL)
    {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }

    printf("NULL\n");
}

/* Function to insert a node */
void insert()
{
    int value, position, i;
    struct Node *newNode, *temp;

    printf("Enter value to insert: ");
    scanf("%d", &value);

    printf("Enter position: ");
    scanf("%d", &position);

    if (position <= 0)
    {
        printf("Invalid position.\n");
        return;
    }

    newNode = (struct Node *)malloc(sizeof(struct Node));

    if (newNode == NULL)
    {
        printf("Memory allocation failed.\n");
        return;
    }

    newNode->data = value;
    newNode->next = NULL;

    /* Insert at beginning */
    if (position == 1)
    {
        newNode->next = head;
        head = newNode;

        printf("Node inserted successfully.\n");
        return;
    }

    if (head == NULL)
    {
        printf("Invalid position.\n");
        free(newNode);
        return;
    }

    temp = head;

    /* Move to node before required position */
    for (i = 1; i < position - 1; i++)
    {
        if (temp->next == NULL)
        {
            printf("Invalid position.\n");
            free(newNode);
            return;
        }

        temp = temp->next;
    }

    newNode->next = temp->next;
    temp->next = newNode;

    printf("Node inserted successfully.\n");
}

/* Function to delete a node */
void delete()
{
    int position, i;
    struct Node *temp, *delNode;

    if (head == NULL)
    {
        printf("Linked list is empty.\n");
        return;
    }

    printf("Enter position to delete: ");
    scanf("%d", &position);

    if (position <= 0)
    {
        printf("Invalid position.\n");
        return;
    }

    /* Delete first node */
    if (position == 1)
    {
        delNode = head;
        head = head->next;

        free(delNode);

        printf("Node deleted successfully.\n");
        return;
    }

    temp = head;

    /* Move to node before the node to be deleted */
    for (i = 1; i < position - 1; i++)
    {
        if (temp->next == NULL)
        {
            printf("Invalid position.\n");
            return;
        }

        temp = temp->next;
    }

    if (temp->next == NULL)
    {
        printf("Invalid position.\n");
        return;
    }

    delNode = temp->next;
    temp->next = delNode->next;

    free(delNode);

    printf("Node deleted successfully.\n");
}

/* Main function */
int main()
{
    int choice;

    while (1)
    {
        printf("\n===== Singly Linked List =====\n");
        printf("1. Create\n");
        printf("2. Display\n");
        printf("3. Insert\n");
        printf("4. Delete\n");
        printf("5. Exit\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                create();
                break;

            case 2:
                display();
                break;

            case 3:
                insert();
                break;

            case 4:
                delete();
                break;

            case 5:
                printf("Program terminated.\n");
                exit(0);

            default:
                printf("Invalid choice.\n");
        }
    }

    return 0;
}
---------------------------------------------------------------------------------------------------------------------
===== Singly Linked List =====
1. Create
2. Display
3. Insert
4. Delete
5. Exit

Enter your choice: 1
Enter number of nodes: 3
Enter data for node 1: 10
Enter data for node 2: 20
Enter data for node 3: 30
Linked list created successfully.

Enter your choice: 2
Linked List: 10 -> 20 -> 30 -> NULL

Enter your choice: 3
Enter value to insert: 15
Enter position: 2
Node inserted successfully.

Enter your choice: 2
Linked List: 10 -> 15 -> 20 -> 30 -> NULL

Enter your choice: 4
Enter position to delete: 3
Node deleted successfully.

Enter your choice: 2
Linked List: 10 -> 15 -> 30 -> NULL

---------------------------------------------------------------------------------------------------------------------

| Operation   | Complexity |
| ----------- | ---------- |
| `create()`  | O(n)       |
| `display()` | O(n)       |
| `insert()`  | O(n)       |
| `delete()`  | O(n)       |


```
```
2) Write a C program to implement a Singly Circular linked list with following operations: 
create(), display(), search(),length()

#include <stdio.h>
#include <stdlib.h>

/* Structure of a node */
struct Node
{
    int data;
    struct Node *next;
};

struct Node *head = NULL;

/* Function to create circular linked list */
void create()
{
    int n, i, value;
    struct Node *newNode, *temp;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    if (n <= 0)
    {
        printf("Invalid number of nodes.\n");
        return;
    }

    head = NULL;

    for (i = 0; i < n; i++)
    {
        newNode = (struct Node *)malloc(sizeof(struct Node));

        if (newNode == NULL)
        {
            printf("Memory allocation failed.\n");
            return;
        }

        printf("Enter data for node %d: ", i + 1);
        scanf("%d", &value);

        newNode->data = value;

        if (head == NULL)
        {
            head = newNode;
            newNode->next = head;
        }
        else
        {
            temp = head;

            while (temp->next != head)
            {
                temp = temp->next;
            }

            temp->next = newNode;
            newNode->next = head;
        }
    }

    printf("Circular linked list created successfully.\n");
}

/* Function to display circular linked list */
void display()
{
    struct Node *temp;

    if (head == NULL)
    {
        printf("Circular linked list is empty.\n");
        return;
    }

    temp = head;

    printf("Circular Linked List: ");

    do
    {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    while (temp != head);

    printf("HEAD\n");
}

/* Function to search an element */
void search()
{
    int value, position = 1;
    struct Node *temp;

    if (head == NULL)
    {
        printf("Circular linked list is empty.\n");
        return;
    }

    printf("Enter value to search: ");
    scanf("%d", &value);

    temp = head;

    do
    {
        if (temp->data == value)
        {
            printf("%d found at position %d.\n", value, position);
            return;
        }

        temp = temp->next;
        position++;

    }
    while (temp != head);

    printf("%d not found in the list.\n", value);
}

/* Function to find length */
void length()
{
    int count = 0;
    struct Node *temp;

    if (head == NULL)
    {
        printf("Length of circular linked list = 0\n");
        return;
    }

    temp = head;

    do
    {
        count++;
        temp = temp->next;
    }
    while (temp != head);

    printf("Length of circular linked list = %d\n", count);
}

/* Main function */
int main()
{
    int choice;

    while (1)
    {
        printf("\n===== Singly Circular Linked List =====\n");
        printf("1. Create\n");
        printf("2. Display\n");
        printf("3. Search\n");
        printf("4. Length\n");
        printf("5. Exit\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                create();
                break;

            case 2:
                display();
                break;

            case 3:
                search();
                break;

            case 4:
                length();
                break;

            case 5:
                printf("Program terminated.\n");
                exit(0);

            default:
                printf("Invalid choice.\n");
        }
    }

    return 0;
}
-----------------------------------------------------------------------------------------------------------------------

| Operation   | Time Complexity |
| ----------- | --------------: |
| `create()`  |           O(n²) |
| `display()` |            O(n) |
| `search()`  |            O(n) |
| `length()`  |            O(n) |

-----------------------------------------------------------------------------------------------------------------------
```
```
3) Write a C program to implement a Doubly linked list with create(),display(),insert(),delete() 
operation.

#include <stdio.h>
#include <stdlib.h>

/* Structure of a node */
struct Node
{
    int data;
    struct Node *prev;
    struct Node *next;
};

struct Node *head = NULL;

/* Create doubly linked list */
void create()
{
    int n, i, value;
    struct Node *newNode, *temp;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    if (n <= 0)
    {
        printf("Invalid number of nodes.\n");
        return;
    }

    head = NULL;

    for (i = 0; i < n; i++)
    {
        newNode = (struct Node *)malloc(sizeof(struct Node));

        if (newNode == NULL)
        {
            printf("Memory allocation failed.\n");
            return;
        }

        printf("Enter data for node %d: ", i + 1);
        scanf("%d", &value);

        newNode->data = value;
        newNode->prev = NULL;
        newNode->next = NULL;

        if (head == NULL)
        {
            head = newNode;
        }
        else
        {
            temp = head;

            while (temp->next != NULL)
            {
                temp = temp->next;
            }

            temp->next = newNode;
            newNode->prev = temp;
        }
    }

    printf("Doubly linked list created successfully.\n");
}

/* Display doubly linked list */
void display()
{
    struct Node *temp;

    if (head == NULL)
    {
        printf("Doubly linked list is empty.\n");
        return;
    }

    temp = head;

    printf("Doubly Linked List: ");

    while (temp != NULL)
    {
        printf("%d <-> ", temp->data);
        temp = temp->next;
    }

    printf("NULL\n");
}

/* Insert node at a given position */
void insert()
{
    int value, position, i;
    struct Node *newNode, *temp;

    printf("Enter value to insert: ");
    scanf("%d", &value);

    printf("Enter position: ");
    scanf("%d", &position);

    if (position <= 0)
    {
        printf("Invalid position.\n");
        return;
    }

    newNode = (struct Node *)malloc(sizeof(struct Node));

    if (newNode == NULL)
    {
        printf("Memory allocation failed.\n");
        return;
    }

    newNode->data = value;
    newNode->prev = NULL;
    newNode->next = NULL;

    /* Insert at beginning */
    if (position == 1)
    {
        newNode->next = head;

        if (head != NULL)
        {
            head->prev = newNode;
        }

        head = newNode;

        printf("Node inserted successfully.\n");
        return;
    }

    if (head == NULL)
    {
        printf("Invalid position.\n");
        free(newNode);
        return;
    }

    temp = head;

    /* Move to node before required position */
    for (i = 1; i < position - 1; i++)
    {
        if (temp->next == NULL)
        {
            printf("Invalid position.\n");
            free(newNode);
            return;
        }

        temp = temp->next;
    }

    newNode->next = temp->next;
    newNode->prev = temp;

    if (temp->next != NULL)
    {
        temp->next->prev = newNode;
    }

    temp->next = newNode;

    printf("Node inserted successfully.\n");
}

/* Delete node from a given position */
void delete()
{
    int position, i;
    struct Node *temp;

    if (head == NULL)
    {
        printf("Doubly linked list is empty.\n");
        return;
    }

    printf("Enter position to delete: ");
    scanf("%d", &position);

    if (position <= 0)
    {
        printf("Invalid position.\n");
        return;
    }

    temp = head;

    /* Delete first node */
    if (position == 1)
    {
        head = head->next;

        if (head != NULL)
        {
            head->prev = NULL;
        }

        free(temp);

        printf("Node deleted successfully.\n");
        return;
    }

    /* Move to node to be deleted */
    for (i = 1; i < position; i++)
    {
        if (temp == NULL)
        {
            printf("Invalid position.\n");
            return;
        }

        temp = temp->next;
    }

    if (temp == NULL)
    {
        printf("Invalid position.\n");
        return;
    }

    /* Connect previous node to next node */
    temp->prev->next = temp->next;

    /* Connect next node to previous node */
    if (temp->next != NULL)
    {
        temp->next->prev = temp->prev;
    }

    free(temp);

    printf("Node deleted successfully.\n");
}

/* Main function */
int main()
{
    int choice;

    while (1)
    {
        printf("\n===== Doubly Linked List =====\n");
        printf("1. Create\n");
        printf("2. Display\n");
        printf("3. Insert\n");
        printf("4. Delete\n");
        printf("5. Exit\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                create();
                break;

            case 2:
                display();
                break;

            case 3:
                insert();
                break;

            case 4:
                delete();
                break;

            case 5:
                printf("Program terminated.\n");
                exit(0);

            default:
                printf("Invalid choice.\n");
        }
    }

    return 0;
}

---------------------------------------------------------------------------------------------------------------------

===== Doubly Linked List =====
1. Create
2. Display
3. Insert
4. Delete
5. Exit

Enter your choice: 1
Enter number of nodes: 3
Enter data for node 1: 10
Enter data for node 2: 20
Enter data for node 3: 30

Doubly linked list created successfully.

Enter your choice: 2
Doubly Linked List: 10 <-> 20 <-> 30 <-> NULL

Enter your choice: 3
Enter value to insert: 15
Enter position: 2
Node inserted successfully.

Enter your choice: 2
Doubly Linked List: 10 <-> 15 <-> 20 <-> 30 <-> NULL

Enter your choice: 4
Enter position to delete: 3
Node deleted successfully.

Enter your choice: 2
Doubly Linked List: 10 <-> 15 <-> 30 <-> NULL

---------------------------------------------------------------------------------------------------------------------

| Operation   | Time Complexity |
| ----------- | --------------: |
| `create()`  |           O(n²) |
| `display()` |            O(n) |
| `insert()`  |            O(n) |
| `delete()`  |            O(n) |
---------------------------------------------------------------------------------------------------------------------

```

# SET B 
```
--------------------------------------------------------------------------------------------------------------
1) Write a C program to implement a Doubly Circular linked list with following operations      
      create() and display()

#include <stdio.h>
#include <stdlib.h>

/* Structure of a node */
struct Node
{
    int data;
    struct Node *prev;
    struct Node *next;
};

struct Node *head = NULL;

/* Function to create doubly circular linked list */
void create()
{
    int n, i, value;
    struct Node *newNode, *temp;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    if (n <= 0)
    {
        printf("Invalid number of nodes.\n");
        return;
    }

    head = NULL;

    for (i = 0; i < n; i++)
    {
        newNode = (struct Node *)malloc(sizeof(struct Node));

        if (newNode == NULL)
        {
            printf("Memory allocation failed.\n");
            return;
        }

        printf("Enter data for node %d: ", i + 1);
        scanf("%d", &value);

        newNode->data = value;

        if (head == NULL)
        {
            /* First node */
            head = newNode;

            newNode->next = head;
            newNode->prev = head;
        }
        else
        {
            temp = head;

            /* Move to the last node */
            while (temp->next != head)
            {
                temp = temp->next;
            }

            /* Connect new node */
            temp->next = newNode;
            newNode->prev = temp;

            newNode->next = head;
            head->prev = newNode;
        }
    }

    printf("Doubly Circular Linked List created successfully.\n");
}

/* Function to display doubly circular linked list */
void display()
{
    struct Node *temp;

    if (head == NULL)
    {
        printf("List is empty.\n");
        return;
    }

    temp = head;

    printf("Doubly Circular Linked List: ");

    do
    {
        printf("%d <-> ", temp->data);
        temp = temp->next;
    }
    while (temp != head);

    printf("HEAD\n");
}

/* Main function */
int main()
{
    int choice;

    while (1)
    {
        printf("\n===== Doubly Circular Linked List =====\n");
        printf("1. Create\n");
        printf("2. Display\n");
        printf("3. Exit\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                create();
                break;

            case 2:
                display();
                break;

            case 3:
                printf("Program terminated.\n");
                exit(0);

            default:
                printf("Invalid choice.\n");
        }
    }

    return 0;
}
-------------------------------------------------------------------------------------------------------------
```
```
2) Write a C program to implement a Doubly Circular linked list with following operations       
   create() and display(), append(),delete()

#include <stdio.h>
#include <stdlib.h>

/* Structure of a node */
struct Node
{
    int data;
    struct Node *prev;
    struct Node *next;
};

struct Node *head = NULL;

/* Function to create doubly circular linked list */
void create()
{
    int n, i, value;
    struct Node *newNode, *temp;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    if (n <= 0)
    {
        printf("Invalid number of nodes.\n");
        return;
    }

    /* Start with an empty list */
    head = NULL;

    for (i = 0; i < n; i++)
    {
        newNode = (struct Node *)malloc(sizeof(struct Node));

        if (newNode == NULL)
        {
            printf("Memory allocation failed.\n");
            return;
        }

        printf("Enter data for node %d: ", i + 1);
        scanf("%d", &value);

        newNode->data = value;

        /* First node */
        if (head == NULL)
        {
            head = newNode;

            newNode->next = head;
            newNode->prev = head;
        }
        else
        {
            temp = head;

            /* Find the last node */
            while (temp->next != head)
            {
                temp = temp->next;
            }

            /* Insert new node at the end */
            newNode->prev = temp;
            newNode->next = head;

            temp->next = newNode;
            head->prev = newNode;
        }
    }

    printf("Doubly Circular Linked List created successfully.\n");
}

/* Function to display the list */
void display()
{
    struct Node *temp;

    if (head == NULL)
    {
        printf("List is empty.\n");
        return;
    }

    temp = head;

    printf("Doubly Circular Linked List: ");

    do
    {
        printf("%d <-> ", temp->data);
        temp = temp->next;
    }
    while (temp != head);

    printf("HEAD\n");
}

/* Function to append a node at the end */
void append()
{
    int value;
    struct Node *newNode, *last;

    printf("Enter value to append: ");
    scanf("%d", &value);

    newNode = (struct Node *)malloc(sizeof(struct Node));

    if (newNode == NULL)
    {
        printf("Memory allocation failed.\n");
        return;
    }

    newNode->data = value;

    /* If list is empty */
    if (head == NULL)
    {
        head = newNode;

        newNode->next = head;
        newNode->prev = head;
    }
    else
    {
        /* Last node is head->prev */
        last = head->prev;

        newNode->next = head;
        newNode->prev = last;

        last->next = newNode;
        head->prev = newNode;
    }

    printf("Node appended successfully.\n");
}

/* Function to delete a node from a given position */
void delete()
{
    int position, i;
    struct Node *temp;

    if (head == NULL)
    {
        printf("List is empty.\n");
        return;
    }

    printf("Enter position to delete: ");
    scanf("%d", &position);

    if (position <= 0)
    {
        printf("Invalid position.\n");
        return;
    }

    temp = head;

    /* Move to the required position */
    for (i = 1; i < position; i++)
    {
        temp = temp->next;

        /* If we come back to head, position is invalid */
        if (temp == head)
        {
            printf("Invalid position.\n");
            return;
        }
    }

    /* Only one node in the list */
    if (temp->next == temp)
    {
        head = NULL;
        free(temp);

        printf("Node deleted successfully.\n");
        return;
    }

    /* If deleting the first node */
    if (temp == head)
    {
        head = head->next;
    }

    /* Connect previous and next nodes */
    temp->prev->next = temp->next;
    temp->next->prev = temp->prev;

    free(temp);

    printf("Node deleted successfully.\n");
}

/* Main function */
int main()
{
    int choice;

    while (1)
    {
        printf("\n===== Doubly Circular Linked List =====\n");
        printf("1. Create\n");
        printf("2. Display\n");
        printf("3. Append\n");
        printf("4. Delete\n");
        printf("5. Exit\n");

        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                create();
                break;

            case 2:
                display();
                break;

            case 3:
                append();
                break;

            case 4:
                delete();
                break;

            case 5:
                printf("Program terminated.\n");
                exit(0);

            default:
                printf("Invalid choice.\n");
        }
    }

    return 0;
}

| Operation   | Time Complexity |
| ----------- | --------------: |
| `create()`  |           O(n²) |
| `display()` |            O(n) |
| `append()`  |        **O(1)** |
| `delete()`  |            O(n) |

--------------------------------------------------------------------------------------------------------------

```
Set C

```
1) Write a C program to concatenate two LinkedList.

#include <stdio.h>
#include <stdlib.h>

/* Structure of a node */
struct Node
{
    int data;
    struct Node *next;
};

/* Function to create a linked list */
struct Node* create()
{
    int n, i, value;
    struct Node *head = NULL;
    struct Node *newNode, *temp;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++)
    {
        newNode = (struct Node*)malloc(sizeof(struct Node));

        if (newNode == NULL)
        {
            printf("Memory allocation failed.\n");
            exit(1);
        }

        printf("Enter data for node %d: ", i + 1);
        scanf("%d", &value);

        newNode->data = value;
        newNode->next = NULL;

        if (head == NULL)
        {
            head = newNode;
        }
        else
        {
            temp = head;

            while (temp->next != NULL)
            {
                temp = temp->next;
            }

            temp->next = newNode;
        }
    }

    return head;
}

/* Function to display linked list */
void display(struct Node *head)
{
    struct Node *temp = head;

    while (temp != NULL)
    {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }

    printf("NULL\n");
}

/* Function to concatenate two linked lists */
struct Node* concatenate(struct Node *head1, struct Node *head2)
{
    struct Node *temp;

    /* If first list is empty */
    if (head1 == NULL)
    {
        return head2;
    }

    /* If second list is empty */
    if (head2 == NULL)
    {
        return head1;
    }

    /* Find last node of first list */
    temp = head1;

    while (temp->next != NULL)
    {
        temp = temp->next;
    }

    /* Connect last node of first list to second list */
    temp->next = head2;

    return head1;
}

/* Main function */
int main()
{
    struct Node *head1, *head2, *head3;

    printf("Enter elements for First Linked List:\n");
    head1 = create();

    printf("\nFirst Linked List:\n");
    display(head1);

    printf("\nEnter elements for Second Linked List:\n");
    head2 = create();

    printf("\nSecond Linked List:\n");
    display(head2);

    /* Concatenate the two lists */
    head3 = concatenate(head1, head2);

    printf("\nAfter Concatenation:\n");
    display(head3);

    return 0;
}

-----------------------------------------------------------------------------------------------------------------
| Operation   | Time Complexity |
| ----------- | --------------: |
| Create List |           O(n²) |
| Display     |            O(n) |
| Concatenate |        **O(n)** |
-----------------------------------------------------------------------------------------------------------------

```
```
2) Write a C program to find intersection of two LinkedList.
#include <stdio.h>
#include <stdlib.h>

/* Structure of a node */
struct Node
{
    int data;
    struct Node *next;
};

/* Function to create a linked list */
struct Node* create()
{
    int n, i, value;
    struct Node *head = NULL;
    struct Node *newNode, *temp;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++)
    {
        newNode = (struct Node*)malloc(sizeof(struct Node));

        if (newNode == NULL)
        {
            printf("Memory allocation failed.\n");
            exit(1);
        }

        printf("Enter data for node %d: ", i + 1);
        scanf("%d", &value);

        newNode->data = value;
        newNode->next = NULL;

        if (head == NULL)
        {
            head = newNode;
        }
        else
        {
            temp = head;

            while (temp->next != NULL)
            {
                temp = temp->next;
            }

            temp->next = newNode;
        }
    }

    return head;
}

/* Function to display linked list */
void display(struct Node *head)
{
    struct Node *temp = head;

    while (temp != NULL)
    {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }

    printf("NULL\n");
}

/* Function to check whether a value exists in a linked list */
int search(struct Node *head, int value)
{
    struct Node *temp = head;

    while (temp != NULL)
    {
        if (temp->data == value)
        {
            return 1;
        }

        temp = temp->next;
    }

    return 0;
}

/* Function to find intersection */
struct Node* intersection(struct Node *head1, struct Node *head2)
{
    struct Node *result = NULL;
    struct Node *newNode;
    struct Node *temp1 = head1;
    struct Node *tempResult;

    while (temp1 != NULL)
    {
        if (search(head2, temp1->data))
        {
            newNode = (struct Node*)malloc(sizeof(struct Node));

            if (newNode == NULL)
            {
                printf("Memory allocation failed.\n");
                exit(1);
            }

            newNode->data = temp1->data;
            newNode->next = NULL;

            if (result == NULL)
            {
                result = newNode;
            }
            else
            {
                tempResult = result;

                while (tempResult->next != NULL)
                {
                    tempResult = tempResult->next;
                }

                tempResult->next = newNode;
            }
        }

        temp1 = temp1->next;
    }

    return result;
}

/* Main function */
int main()
{
    struct Node *head1, *head2, *result;

    printf("Enter elements for First Linked List:\n");
    head1 = create();

    printf("\nFirst Linked List:\n");
    display(head1);

    printf("\nEnter elements for Second Linked List:\n");
    head2 = create();

    printf("\nSecond Linked List:\n");
    display(head2);

    /* Find intersection */
    result = intersection(head1, head2);

    printf("\nIntersection of Two Linked Lists:\n");

    if (result == NULL)
    {
        printf("No common elements found.\n");
    }
    else
    {
        display(result);
    }

    return 0;
}

```
```
3) Write a C program to reverse a singly LinkedList.

#include <stdio.h>
#include <stdlib.h>

/* Structure of a node */
struct Node
{
    int data;
    struct Node *next;
};

/* Function to create linked list */
struct Node* create()
{
    int n, i, value;
    struct Node *head = NULL;
    struct Node *newNode, *temp;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    for (i = 0; i < n; i++)
    {
        newNode = (struct Node*)malloc(sizeof(struct Node));

        if (newNode == NULL)
        {
            printf("Memory allocation failed.\n");
            exit(1);
        }

        printf("Enter data for node %d: ", i + 1);
        scanf("%d", &value);

        newNode->data = value;
        newNode->next = NULL;

        if (head == NULL)
        {
            head = newNode;
        }
        else
        {
            temp = head;

            while (temp->next != NULL)
            {
                temp = temp->next;
            }

            temp->next = newNode;
        }
    }

    return head;
}

/* Function to display linked list */
void display(struct Node *head)
{
    struct Node *temp = head;

    while (temp != NULL)
    {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }

    printf("NULL\n");
}

/* Function to reverse linked list */
struct Node* reverse(struct Node *head)
{
    struct Node *prev = NULL;
    struct Node *current = head;
    struct Node *next;

    while (current != NULL)
    {
        /* Store the next node */
        next = current->next;

        /* Reverse the link */
        current->next = prev;

        /* Move prev to current node */
        prev = current;

        /* Move current to next node */
        current = next;
    }

    /* New head is the previous node */
    head = prev;

    return head;
}

/* Main function */
int main()
{
    struct Node *head;

    printf("Create Singly Linked List\n");
    head = create();

    printf("\nOriginal Linked List:\n");
    display(head);

    head = reverse(head);

    printf("\nReversed Linked List:\n");
    display(head);

    return 0;
}

```

















