# Assignment 5 — Stack and Queue
## S.Y. B.Sc. (Computer Applications) — Data Structures
### C Programming Solutions — SET A, SET B and SET C

**Source:** SPPU CA-202 MJP Lab Course on CA201-MJ Data Structures workbook, Assignment No. 5 — Stack and Queue.

---

## Table of Contents

1. [Assignment Requirements](#assignment-requirements)
2. [Basic Theory](#basic-theory)
3. [SET A — Q1 Static Stack](#set-a--q1-static-implementation-of-stack)
4. [SET A — Q2 Dynamic Stack](#set-a--q2-dynamic-implementation-of-stack)
5. [SET B — Q1 Static Queue](#set-b--q1-static-implementation-of-queue)
6. [SET B — Q2 Dynamic Queue](#set-b--q2-dynamic-implementation-of-queue)
7. [SET C — Q1 Reverse Stack Recursively](#set-c--q1-reverse-stack-using-recursion)
8. [SET C — Q2 Infix to Postfix](#set-c--q2-infix-expression-to-postfix-expression)
9. [SET C — Q3 Static Circular Queue](#set-c--q3-static-circular-queue)
10. [How to Compile and Run](#how-to-compile-and-run)
11. [Important Viva Questions](#important-viva-questions)

---

# Assignment Requirements

According to the lab book, Assignment 5 is **Stack and Queue**.

### SET A

1. Write a C program to perform **Static implementation of Stack on integers** with:
   - `Initialize()`
   - `push()`
   - `pop()`
   - `isempty()`
   - `isfull()`

2. Write a C program to perform **Dynamic implementation of Stack on character data** with:
   - `Initialize()`
   - `push()`
   - `pop()`
   - `display()`
   - `peek()`

### SET B

1. Write a C program to perform **Static implementation of Queue on integers** with:
   - `Initialize()`
   - `insert()`
   - `delete()`
   - `isempty()`
   - `display()`

2. Write a C program to perform **Dynamic implementation of Queue on character data** with:
   - `Initialize()`
   - `insert()`
   - `delete()`
   - `isempty()`
   - `display()`
   - `peek()`

### SET C

1. Write a C program to **reverse the stack using a recursive function**.
2. Write a C program to **convert infix expression to postfix expression**.
3. Write a C program to perform **Static implementation of circular queue of integers** with:
   - `Initialize()`
   - `insert()`
   - `delete()`

---

# Basic Theory

## 1. Stack

A stack is a linear data structure in which insertion and deletion are performed from one end called the **TOP**.

Stack follows:

**LIFO — Last In, First Out**

Example:

```text
Push 10
Push 20
Push 30

TOP
 ↓
30
20
10
```

If `pop()` is performed, `30` is removed first.

### Common Stack Operations

| Operation | Meaning |
|---|---|
| Initialize | Create/initialize an empty stack |
| Push | Add an element at TOP |
| Pop | Remove the element from TOP |
| Peek | Read TOP without removing it |
| IsEmpty | Check whether stack contains no elements |
| IsFull | Check whether a fixed-size stack is full |
| Display | Print stack elements |

---

## 2. Queue

A queue is a linear data structure that follows:

**FIFO — First In, First Out**

Insertion takes place at the **REAR** and deletion takes place from the **FRONT**.

```text
FRONT                         REAR
  ↓                             ↓
[10] → [20] → [30] → [40]
```

The first inserted element, `10`, is deleted first.

### Common Queue Operations

| Operation | Meaning |
|---|---|
| Initialize | Create/initialize an empty queue |
| Insert | Add an element at REAR |
| Delete | Remove an element from FRONT |
| Peek/Front | Read FRONT without deleting |
| IsEmpty | Check whether queue is empty |
| IsFull | Check whether fixed queue is full |
| Display | Print queue elements |

---

# SET A — Q1: Static Implementation of Stack

## Problem

Write a C program to perform static implementation of Stack on integer data with:

`Initialize(), push(), pop(), isempty(), isfull()`

## Program

```c
#include <stdio.h>

#define MAX 5

int stack[MAX];
int top;

void initialize()
{
    top = -1;
}

int isEmpty()
{
    return top == -1;
}

int isFull()
{
    return top == MAX - 1;
}

void push(int value)
{
    if (isFull())
    {
        printf("Stack Overflow! Stack is full.\n");
        return;
    }

    top++;
    stack[top] = value;

    printf("%d pushed into stack.\n", value);
}

void pop()
{
    if (isEmpty())
    {
        printf("Stack Underflow! Stack is empty.\n");
        return;
    }

    printf("%d popped from stack.\n", stack[top]);
    top--;
}

int main()
{
    int choice, value;

    initialize();

    do
    {
        printf("\n--- STATIC STACK ---\n");
        printf("1. Push\n");
        printf("2. Pop\n");
        printf("3. Is Empty\n");
        printf("4. Is Full\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                printf("Enter integer value: ");
                scanf("%d", &value);
                push(value);
                break;

            case 2:
                pop();
                break;

            case 3:
                if (isEmpty())
                    printf("Stack is Empty.\n");
                else
                    printf("Stack is not Empty.\n");
                break;

            case 4:
                if (isFull())
                    printf("Stack is Full.\n");
                else
                    printf("Stack is not Full.\n");
                break;

            case 5:
                printf("Program terminated.\n");
                break;

            default:
                printf("Invalid choice.\n");
        }

    } while (choice != 5);

    return 0;
}
```

## Important Logic

### Initialize

```text
top = -1
```

`-1` means there is no element in the stack.

### Push

```text
if top == MAX-1
    Stack Full
else
    top = top + 1
    stack[top] = value
```

### Pop

```text
if top == -1
    Stack Empty
else
    remove stack[top]
    top = top - 1
```

### Complexity

| Operation | Complexity |
|---|---:|
| Initialize | O(1) |
| Push | O(1) |
| Pop | O(1) |
| IsEmpty | O(1) |
| IsFull | O(1) |

---

# SET A — Q2: Dynamic Implementation of Stack

## Problem

Write a C program to perform dynamic implementation of Stack on character data with:

`Initialize(), push(), pop(), display(), peek()`

## Program

```c
#include <stdio.h>
#include <stdlib.h>

struct Node
{
    char data;
    struct Node *next;
};

struct Node *top;

void initialize()
{
    top = NULL;
}

void push(char value)
{
    struct Node *newNode;

    newNode = (struct Node *)malloc(sizeof(struct Node));

    if (newNode == NULL)
    {
        printf("Memory allocation failed.\n");
        return;
    }

    newNode->data = value;
    newNode->next = top;
    top = newNode;

    printf("%c pushed into stack.\n", value);
}

void pop()
{
    struct Node *temp;

    if (top == NULL)
    {
        printf("Stack Underflow! Stack is empty.\n");
        return;
    }

    temp = top;

    printf("%c popped from stack.\n", top->data);

    top = top->next;

    free(temp);
}

void peek()
{
    if (top == NULL)
    {
        printf("Stack is empty.\n");
        return;
    }

    printf("Top element = %c\n", top->data);
}

void display()
{
    struct Node *temp;

    if (top == NULL)
    {
        printf("Stack is empty.\n");
        return;
    }

    temp = top;

    printf("Stack elements from TOP to BOTTOM:\n");

    while (temp != NULL)
    {
        printf("%c ", temp->data);
        temp = temp->next;
    }

    printf("\n");
}

int main()
{
    int choice;
    char value;

    initialize();

    do
    {
        printf("\n--- DYNAMIC STACK ---\n");
        printf("1. Push\n");
        printf("2. Pop\n");
        printf("3. Display\n");
        printf("4. Peek\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                printf("Enter character: ");
                scanf(" %c", &value);
                push(value);
                break;

            case 2:
                pop();
                break;

            case 3:
                display();
                break;

            case 4:
                peek();
                break;

            case 5:
                printf("Program terminated.\n");
                break;

            default:
                printf("Invalid choice.\n");
        }

    } while (choice != 5);

    return 0;
}
```

## Important Logic

A dynamic stack uses a linked list.

```text
TOP
 ↓
[C] → [B] → [A] → NULL
```

For `push()`:

```text
newNode->next = top
top = newNode
```

For `pop()`:

```text
temp = top
top = top->next
free(temp)
```

There is no fixed `MAX` limit in the implementation. It grows according to available dynamic memory.

### Complexity

| Operation | Complexity |
|---|---:|
| Initialize | O(1) |
| Push | O(1) |
| Pop | O(1) |
| Peek | O(1) |
| Display | O(n) |

---

# SET B — Q1: Static Implementation of Queue

## Problem

Write a C program to perform static implementation of Queue on integer data with:

`Initialize(), insert(), delete(), isempty(), display()`

## Program

```c
#include <stdio.h>

#define MAX 5

int queue[MAX];
int front, rear;

void initialize()
{
    front = -1;
    rear = -1;
}

int isEmpty()
{
    return front == -1;
}

int isFull()
{
    return rear == MAX - 1;
}

void insert(int value)
{
    if (isFull())
    {
        printf("Queue Overflow! Queue is full.\n");
        return;
    }

    if (front == -1)
        front = 0;

    rear++;
    queue[rear] = value;

    printf("%d inserted into queue.\n", value);
}

void deleteElement()
{
    if (isEmpty())
    {
        printf("Queue Underflow! Queue is empty.\n");
        return;
    }

    printf("%d deleted from queue.\n", queue[front]);

    if (front == rear)
    {
        front = -1;
        rear = -1;
    }
    else
    {
        front++;
    }
}

void display()
{
    int i;

    if (isEmpty())
    {
        printf("Queue is empty.\n");
        return;
    }

    printf("Queue elements from FRONT to REAR:\n");

    for (i = front; i <= rear; i++)
    {
        printf("%d ", queue[i]);
    }

    printf("\n");
}

int main()
{
    int choice, value;

    initialize();

    do
    {
        printf("\n--- STATIC QUEUE ---\n");
        printf("1. Insert\n");
        printf("2. Delete\n");
        printf("3. Is Empty\n");
        printf("4. Display\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                printf("Enter integer value: ");
                scanf("%d", &value);
                insert(value);
                break;

            case 2:
                deleteElement();
                break;

            case 3:
                if (isEmpty())
                    printf("Queue is Empty.\n");
                else
                    printf("Queue is not Empty.\n");
                break;

            case 4:
                display();
                break;

            case 5:
                printf("Program terminated.\n");
                break;

            default:
                printf("Invalid choice.\n");
        }

    } while (choice != 5);

    return 0;
}
```

## Important Logic

Initially:

```text
front = -1
rear = -1
```

After inserting `10, 20, 30`:

```text
FRONT              REAR
  ↓                  ↓
[10] [20] [30]
```

Deletion removes from `front`.

### Complexity

| Operation | Complexity |
|---|---:|
| Initialize | O(1) |
| Insert | O(1) |
| Delete | O(1) |
| IsEmpty | O(1) |
| Display | O(n) |

### Note

This is a **linear static queue**, not a circular queue. Therefore, positions released at the beginning are not reused until the queue becomes empty. SET C below implements the circular queue to solve this space-reuse issue.

---

# SET B — Q2: Dynamic Implementation of Queue

## Problem

Write a C program to perform dynamic implementation of Queue on character data with:

`Initialize(), insert(), delete(), isempty(), display(), peek()`

## Program

```c
#include <stdio.h>
#include <stdlib.h>

struct Node
{
    char data;
    struct Node *next;
};

struct Node *front;
struct Node *rear;

void initialize()
{
    front = NULL;
    rear = NULL;
}

int isEmpty()
{
    return front == NULL;
}

void insert(char value)
{
    struct Node *newNode;

    newNode = (struct Node *)malloc(sizeof(struct Node));

    if (newNode == NULL)
    {
        printf("Memory allocation failed.\n");
        return;
    }

    newNode->data = value;
    newNode->next = NULL;

    if (rear == NULL)
    {
        front = rear = newNode;
    }
    else
    {
        rear->next = newNode;
        rear = newNode;
    }

    printf("%c inserted into queue.\n", value);
}

void deleteElement()
{
    struct Node *temp;

    if (isEmpty())
    {
        printf("Queue Underflow! Queue is empty.\n");
        return;
    }

    temp = front;

    printf("%c deleted from queue.\n", front->data);

    front = front->next;

    if (front == NULL)
        rear = NULL;

    free(temp);
}

void peek()
{
    if (isEmpty())
    {
        printf("Queue is empty.\n");
        return;
    }

    printf("Front element = %c\n", front->data);
}

void display()
{
    struct Node *temp;

    if (isEmpty())
    {
        printf("Queue is empty.\n");
        return;
    }

    temp = front;

    printf("Queue elements from FRONT to REAR:\n");

    while (temp != NULL)
    {
        printf("%c ", temp->data);
        temp = temp->next;
    }

    printf("\n");
}

int main()
{
    int choice;
    char value;

    initialize();

    do
    {
        printf("\n--- DYNAMIC QUEUE ---\n");
        printf("1. Insert\n");
        printf("2. Delete\n");
        printf("3. Is Empty\n");
        printf("4. Display\n");
        printf("5. Peek\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                printf("Enter character: ");
                scanf(" %c", &value);
                insert(value);
                break;

            case 2:
                deleteElement();
                break;

            case 3:
                if (isEmpty())
                    printf("Queue is Empty.\n");
                else
                    printf("Queue is not Empty.\n");
                break;

            case 4:
                display();
                break;

            case 5:
                peek();
                break;

            case 6:
                printf("Program terminated.\n");
                break;

            default:
                printf("Invalid choice.\n");
        }

    } while (choice != 6);

    return 0;
}
```

## Important Logic

Dynamic queue uses two pointers:

```text
front → first node
rear  → last node
```

Example:

```text
front                       rear
  ↓                           ↓
[A] → [B] → [C] → NULL
```

Insertion occurs at `rear`.

Deletion occurs at `front`.

### Complexity

| Operation | Complexity |
|---|---:|
| Initialize | O(1) |
| Insert | O(1) |
| Delete | O(1) |
| Peek | O(1) |
| IsEmpty | O(1) |
| Display | O(n) |

---

# SET C — Q1: Reverse Stack Using Recursion

## Problem

Write a C program to reverse the stack using a recursive function.

## Approach

Suppose the stack is:

```text
TOP
 ↓
4
3
2
1
```

After reversing:

```text
TOP
 ↓
1
2
3
4
```

The important idea is:

1. Pop the top element recursively.
2. Reverse the remaining stack.
3. Insert the popped element at the bottom.
4. Continue until the stack becomes empty.

## Program

```c
#include <stdio.h>

#define MAX 100

int stack[MAX];
int top = -1;

void push(int value)
{
    if (top == MAX - 1)
    {
        printf("Stack Overflow.\n");
        return;
    }

    stack[++top] = value;
}

int pop()
{
    if (top == -1)
        return -1;

    return stack[top--];
}

void insertAtBottom(int value)
{
    int temp;

    if (top == -1)
    {
        push(value);
        return;
    }

    temp = pop();

    insertAtBottom(value);

    push(temp);
}

void reverseStack()
{
    int temp;

    if (top == -1)
        return;

    temp = pop();

    reverseStack();

    insertAtBottom(temp);
}

void display()
{
    int i;

    if (top == -1)
    {
        printf("Stack is empty.\n");
        return;
    }

    printf("Stack from TOP to BOTTOM:\n");

    for (i = top; i >= 0; i--)
    {
        printf("%d ", stack[i]);
    }

    printf("\n");
}

int main()
{
    int n, i, value;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    if (n < 0 || n > MAX)
    {
        printf("Invalid number of elements.\n");
        return 1;
    }

    printf("Enter %d elements:\n", n);

    for (i = 0; i < n; i++)
    {
        scanf("%d", &value);
        push(value);
    }

    printf("\nOriginal ");
    display();

    reverseStack();

    printf("\nReversed ");
    display();

    return 0;
}
```

## Example

Input:

```text
Enter number of elements: 4
Enter 4 elements:
1 2 3 4
```

Output:

```text
Original Stack from TOP to BOTTOM:
4 3 2 1

Reversed Stack from TOP to BOTTOM:
1 2 3 4
```

## New Concept: Recursion

A recursive function calls itself.

Here:

```text
reverseStack()
    ↓
pop()
    ↓
reverseStack()
    ↓
pop()
    ↓
...
```

When the base condition is reached, the recursive calls return one by one.

---

# SET C — Q2: Infix Expression to Postfix Expression

## Problem

Write a C program to convert an infix expression to postfix expression.

## Example

Infix:

```text
A+B*C
```

Postfix:

```text
ABC*+
```

### Why Stack is Used

Operators are temporarily stored in a stack.

Operands are directly added to the postfix expression.

### Operator Precedence

| Operator | Precedence |
|---|---:|
| `^` | 3 |
| `* / %` | 2 |
| `+ -` | 1 |

Parentheses are handled separately.

## Program

```c
#include <stdio.h>
#include <ctype.h>

#define MAX 100

char stack[MAX];
int top = -1;

void push(char value)
{
    if (top == MAX - 1)
    {
        printf("Stack Overflow.\n");
        return;
    }

    stack[++top] = value;
}

char pop()
{
    if (top == -1)
        return '\0';

    return stack[top--];
}

char peek()
{
    if (top == -1)
        return '\0';

    return stack[top];
}

int precedence(char operator)
{
    if (operator == '^')
        return 3;

    if (operator == '*' || operator == '/' || operator == '%')
        return 2;

    if (operator == '+' || operator == '-')
        return 1;

    return 0;
}

int isOperator(char ch)
{
    return ch == '+' || ch == '-' ||
           ch == '*' || ch == '/' ||
           ch == '%' || ch == '^';
}

void infixToPostfix(char infix[], char postfix[])
{
    int i = 0;
    int j = 0;
    char ch;

    while (infix[i] != '\0')
    {
        ch = infix[i];

        if (isalnum((unsigned char)ch))
        {
            postfix[j++] = ch;
        }
        else if (ch == '(')
        {
            push(ch);
        }
        else if (ch == ')')
        {
            while (top != -1 && peek() != '(')
            {
                postfix[j++] = pop();
            }

            if (top != -1 && peek() == '(')
                pop();
        }
        else if (isOperator(ch))
        {
            while (top != -1 &&
                   peek() != '(' &&
                   precedence(peek()) >= precedence(ch))
            {
                postfix[j++] = pop();
            }

            push(ch);
        }

        i++;
    }

    while (top != -1)
    {
        postfix[j++] = pop();
    }

    postfix[j] = '\0';
}

int main()
{
    char infix[MAX];
    char postfix[MAX];

    printf("Enter infix expression: ");
    scanf("%99s", infix);

    infixToPostfix(infix, postfix);

    printf("Postfix expression: %s\n", postfix);

    return 0;
}
```

## Example

Input:

```text
A+B*C
```

Output:

```text
Postfix expression: ABC*+
```

Another example:

Input:

```text
(A+B)*C
```

Output:

```text
Postfix expression: AB+C*
```

### Important Note

This lab implementation treats operands as **single characters/digits**, such as:

```text
A
B
C
1
2
3
```

It does not tokenize multi-digit numbers such as `123` as one operand.

---

# SET C — Q3: Static Circular Queue

## Problem

Write a C program to perform static implementation of circular queue of integers with:

`Initialize(), insert(), delete()`

## Why Circular Queue?

In a normal linear queue, after deletions there may be unused positions at the beginning of the array.

A circular queue reuses those positions.

Example:

```text
        ┌───────────────────────┐
        ↓                       │
[10] [20] [30] [40] [50] ──────┘
```

The last position connects logically back to the first position.

## Full Condition

```text
(rear + 1) % MAX == front
```

## Empty Condition

```text
front == -1
```

## Program

```c
#include <stdio.h>

#define MAX 5

int queue[MAX];
int front, rear;

void initialize()
{
    front = -1;
    rear = -1;
}

int isEmpty()
{
    return front == -1;
}

int isFull()
{
    return (rear + 1) % MAX == front;
}

void insert(int value)
{
    if (isFull())
    {
        printf("Circular Queue Overflow! Queue is full.\n");
        return;
    }

    if (isEmpty())
    {
        front = 0;
        rear = 0;
    }
    else
    {
        rear = (rear + 1) % MAX;
    }

    queue[rear] = value;

    printf("%d inserted into circular queue.\n", value);
}

void deleteElement()
{
    int value;

    if (isEmpty())
    {
        printf("Circular Queue Underflow! Queue is empty.\n");
        return;
    }

    value = queue[front];

    printf("%d deleted from circular queue.\n", value);

    if (front == rear)
    {
        front = -1;
        rear = -1;
    }
    else
    {
        front = (front + 1) % MAX;
    }
}

void display()
{
    int i;

    if (isEmpty())
    {
        printf("Circular Queue is empty.\n");
        return;
    }

    printf("Circular Queue elements:\n");

    i = front;

    while (1)
    {
        printf("%d ", queue[i]);

        if (i == rear)
            break;

        i = (i + 1) % MAX;
    }

    printf("\n");
}

int main()
{
    int choice, value;

    initialize();

    do
    {
        printf("\n--- STATIC CIRCULAR QUEUE ---\n");
        printf("1. Insert\n");
        printf("2. Delete\n");
        printf("3. Display\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
            case 1:
                printf("Enter integer value: ");
                scanf("%d", &value);
                insert(value);
                break;

            case 2:
                deleteElement();
                break;

            case 3:
                display();
                break;

            case 4:
                printf("Program terminated.\n");
                break;

            default:
                printf("Invalid choice.\n");
        }

    } while (choice != 4);

    return 0;
}
```

## Circular Queue Logic

Suppose `MAX = 5`.

When:

```text
rear = 4
```

the next rear position is:

```text
(rear + 1) % MAX
= (4 + 1) % 5
= 0
```

Therefore, the rear wraps around to index `0`.

### Complexity

| Operation | Complexity |
|---|---:|
| Initialize | O(1) |
| Insert | O(1) |
| Delete | O(1) |
| Display | O(n) |

---

# How to Compile and Run

These programs can be compiled using **GCC** on Ubuntu/Linux or Windows with a GCC environment.

## 1. Check GCC

```bash
gcc --version
```

## 2. Compile

For example, if the file is named:

```text
setA_static_stack.c
```

run:

```bash
gcc setA_static_stack.c -o setA_static_stack
```

### Meaning

- `gcc` → GNU C Compiler
- `setA_static_stack.c` → C source file
- `-o` → specifies the output executable name
- `setA_static_stack` → executable name

## 3. Run on Linux

```bash
./setA_static_stack
```

---

# Suggested GitHub Repository Structure

You can keep the assignment in one Markdown file and the C programs separately:

```text
Assignment-5-Stack-and-Queue/
│
├── README.md
│
├── setA_static_stack.c
├── setA_dynamic_stack.c
│
├── setB_static_queue.c
├── setB_dynamic_queue.c
│
├── setC_reverse_stack.c
├── setC_infix_to_postfix.c
└── setC_circular_queue.c
```

If your teacher specifically wants **one file**, use this document alone as:

```text
Assignment-5-Stack-and-Queue.md
```

---

# Important Viva Questions

## Q1. What is a stack?

A stack is a linear data structure in which insertion and deletion occur at one end called TOP. It follows LIFO.

## Q2. What is LIFO?

LIFO means **Last In, First Out**. The last inserted element is removed first.

## Q3. What is a queue?

A queue is a linear data structure in which insertion occurs at REAR and deletion occurs at FRONT. It follows FIFO.

## Q4. What is FIFO?

FIFO means **First In, First Out**. The first inserted element is removed first.

## Q5. What is stack overflow?

Stack overflow occurs when we try to push into a full fixed-size stack.

## Q6. What is stack underflow?

Stack underflow occurs when we try to pop from an empty stack.

## Q7. What is the difference between static and dynamic stack?

| Static Stack | Dynamic Stack |
|---|---|
| Uses array | Uses linked list |
| Fixed capacity | Grows dynamically |
| Uses `top` index | Uses `top` pointer |
| Can become full at MAX | Limited by available memory |

## Q8. What is the difference between linear and circular queue?

A linear queue moves from the beginning toward the end of the array. A circular queue logically connects the last position back to the first position and can reuse free positions.

## Q9. Why do we use `% MAX` in circular queue?

The modulo operation makes the index wrap around from the last array position to the first position.

```text
(rear + 1) % MAX
```

## Q10. What is peek?

`peek()` returns the top element of a stack or the front element of a queue without deleting it.

## Q11. Why is a linked list useful for dynamic stack/queue?

It allows nodes to be allocated at runtime, so the data structure does not require a fixed array capacity.

## Q12. What data structure is used for infix-to-postfix conversion?

A **stack** is used to temporarily store operators and parentheses.

## Q13. What is postfix notation?

In postfix notation, the operator is written after its operands.

```text
Infix:    A + B
Postfix:  AB+
```

## Q14. What is the time complexity of push and pop?

For both static and linked-list implementations, push and pop are **O(1)**.

## Q15. What is the time complexity of display?

Display visits all elements, so it is **O(n)**.

---

# Assignment 5 Quick Revision

```text
STACK
  |
  +-- LIFO
  |
  +-- TOP
  |
  +-- Push
  +-- Pop
  +-- Peek
  +-- IsEmpty
  +-- IsFull

QUEUE
  |
  +-- FIFO
  |
  +-- FRONT → Delete
  +-- REAR  → Insert
  |
  +-- Insert
  +-- Delete
  +-- Peek
  +-- IsEmpty
  +-- IsFull

IMPLEMENTATIONS
  |
  +-- Static → Array
  |
  +-- Dynamic → Linked List

SPECIAL
  |
  +-- Recursive Stack Reverse
  +-- Infix → Postfix
  +-- Circular Queue
```

---
