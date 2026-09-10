# Matrix Representation Using Arrays

## 1. Introduction to Matrix

A **matrix** is a collection of elements arranged in the form of **rows and columns**.

For example:

```text
        Column
         0   1   2
       +---+---+---+
Row 0  | 10| 20| 30|
       +---+---+---+
Row 1  | 40| 50| 60|
       +---+---+---+
Row 2  | 70| 80| 90|
       +---+---+---+
```

The above matrix contains:

- **3 rows**
- **3 columns**
- Total elements = `3 × 3 = 9`
- Order of matrix = **3 × 3**

Mathematically:

$$
A =
\begin{bmatrix}
10 & 20 & 30\\
40 & 50 & 60\\
70 & 80 & 90
\end{bmatrix}
$$

---

# 2. Matrix Representation Using Arrays

In C, a matrix can be represented using a **two-dimensional array**.

```c
int matrix[3][3];
```

The general syntax is:

```c
data_type array_name[rows][columns];
```

For example:

```c
int A[3][4];
```

means:

```text
3 rows
4 columns
```

Therefore, total elements:

$$
3 \times 4 = 12
$$

---

# 3. How `A[i][j]` Works

In a 2D array:

```c
A[i][j]
```

means:

```text
A[row][column]
```

C uses **zero-based indexing**.

For:

```c
int A[3][3];
```

the valid indexes are:

```text
Rows    → 0, 1, 2
Columns → 0, 1, 2
```

Example:

```text
A[0][0] → first row, first column
A[0][1] → first row, second column
A[1][0] → second row, first column
A[2][2] → third row, third column
```

For:

```text
10 20 30
40 50 60
70 80 90
```

we have:

```text
A[0][0] = 10
A[0][1] = 20
A[0][2] = 30

A[1][0] = 40
A[1][1] = 50
A[1][2] = 60

A[2][0] = 70
A[2][1] = 80
A[2][2] = 90
```

---

# 4. How Matrix is Stored in Memory

This is an important DSA concept.

We see a matrix as **two-dimensional**:

```text
10 20 30
40 50 60
70 80 90
```

But computer memory is essentially **linear**.

Conceptually, memory looks like:

```text
10 → 20 → 30 → 40 → 50 → 60 → 70 → 80 → 90
```

Therefore, the computer needs a method to convert a two-dimensional location:

```text
A[i][j]
```

into a one-dimensional memory location.

There are two important ways:

1. **Row-Major Order**
2. **Column-Major Order**

---

# 5. Row-Major Order

## Definition

In **Row-Major Order**, elements are stored in memory **row by row**.

Consider:

```text
A =

10 20 30
40 50 60
70 80 90
```

First, the complete first row is stored:

```text
10 20 30
```

Then the second row:

```text
40 50 60
```

Then the third row:

```text
70 80 90
```

Therefore, memory representation becomes:

```text
10 → 20 → 30 → 40 → 50 → 60 → 70 → 80 → 90
```

### Easy way to remember

> **Row-Major = Complete one row before moving to the next row.**

---

# 6. Row-Major Example

Consider:

```text
A[3][4]

       C0   C1   C2   C3
     +----+----+----+----+
R0   | 10 | 20 | 30 | 40 |
     +----+----+----+----+
R1   | 50 | 60 | 70 | 80 |
     +----+----+----+----+
R2   | 90 |100 |110 |120 |
     +----+----+----+----+
```

Row-major representation:

```text
10 → 20 → 30 → 40
50 → 60 → 70 → 80
90 → 100 → 110 → 120
```

Linear order:

```text
10 → 20 → 30 → 40 → 50 → 60 → 70 → 80 → 90 → 100 → 110 → 120
```

---

# 7. Row-Major Address Formula

Suppose we have:

```c
int A[rows][columns];
```

The address of:

```c
A[i][j]
```

in row-major order is:

$$
Address(A[i][j])
=
Base
+
((i \times NumberOfColumns)+j)
\times SizeOfElement
$$

Where:

| Term | Meaning |
|---|---|
| `Base` | Starting address of array |
| `i` | Row index |
| `j` | Column index |
| `NumberOfColumns` | Total number of columns |
| `SizeOfElement` | Size of each element in bytes |

---

# 8. Row-Major Address Calculation Example

Suppose:

```text
Matrix = A[3][4]

Base address = 1000
Size of integer = 4 bytes
```

Find the address of:

```text
A[2][1]
```

We have:

```text
i = 2
j = 1
Number of columns = 4
Size = 4 bytes
```

Formula:

$$
Address =
Base + [(i \times columns)+j]\times size
$$

Substitute:

$$
=1000+[(2\times4)+1]\times4
$$

$$
=1000+[8+1]\times4
$$

$$
=1000+9\times4
$$

$$
=1000+36
$$

Therefore:

```text
Address(A[2][1]) = 1036
```

---

# 9. Why `Number of Columns` is Used?

Suppose:

```text
A[3][4]
```

and we want:

```text
A[2][1]
```

Before reaching row `2`, we need to completely skip:

```text
Row 0 → 4 elements
Row 1 → 4 elements
```

Total skipped:

```text
2 × 4 = 8 elements
```

Then move one position inside row 2:

```text
+ 1
```

Therefore:

```text
8 + 1 = 9 elements
```

Then:

```text
9 × 4 bytes = 36 bytes
```

So:

```text
1000 + 36 = 1036
```

---

# 10. Column-Major Order

## Definition

In **Column-Major Order**, elements are stored in memory **column by column**.

Consider:

```text
A =

10 20 30
40 50 60
70 80 90
```

First column:

```text
10
40
70
```

Second column:

```text
20
50
80
```

Third column:

```text
30
60
90
```

Therefore memory representation becomes:

```text
10 → 40 → 70 → 20 → 50 → 80 → 30 → 60 → 90
```

### Easy way to remember

> **Column-Major = Complete one column before moving to the next column.**

---

# 11. Column-Major Example

Consider:

```text
       C0   C1   C2
     +----+----+----+
R0   | 10 | 20 | 30 |
     +----+----+----+
R1   | 40 | 50 | 60 |
     +----+----+----+
R2   | 70 | 80 | 90 |
     +----+----+----+
```

Column-major:

```text
Column 0:
10
40
70

Column 1:
20
50
80

Column 2:
30
60
90
```

Linear representation:

```text
10 → 40 → 70 → 20 → 50 → 80 → 30 → 60 → 90
```

---

# 12. Column-Major Address Formula

The formula is:

$$
Address(A[i][j])
=
Base
+
((j \times NumberOfRows)+i)
\times SizeOfElement
$$

Notice the difference:

### Row-Major

$$
(i \times columns)+j
$$

### Column-Major

$$
(j \times rows)+i
$$

---

# 13. Column-Major Address Calculation

Suppose:

```text
A[3][4]

Base = 1000
Integer size = 4 bytes
```

Find:

```text
A[2][1]
```

Here:

```text
i = 2
j = 1
rows = 3
```

Formula:

$$
Address =
Base+[(j\times rows)+i]\times size
$$

$$
=1000+[(1\times3)+2]\times4
$$

$$
=1000+[3+2]\times4
$$

$$
=1000+20
$$

Therefore:

```text
Address(A[2][1]) = 1020
```

---

# 14. Row-Major vs Column-Major

| Feature | Row-Major | Column-Major |
|---|---|---|
| Storage | Row by row | Column by column |
| First priority | Row | Column |
| Formula | `(i × columns) + j` | `(j × rows) + i` |
| C | Uses Row-Major | Not native |
| Fortran | Not native | Uses Column-Major |

### Important

> **C stores multidimensional arrays in Row-Major Order.**

---

# 15. Matrix Operations

Common operations on matrices include:

1. Traversal
2. Addition
3. Subtraction
4. Multiplication
5. Transpose
6. Searching
7. Updating elements

---

# 16. Matrix Traversal

## Definition

**Traversal** means visiting every element of the matrix exactly once.

Example:

```text
10 20 30
40 50 60
70 80 90
```

Traversal:

```text
10
20
30
40
50
60
70
80
90
```

In C, we use **nested loops**.

```c
#include <stdio.h>

int main()
{
    int A[3][3] = {
        {10, 20, 30},
        {40, 50, 60},
        {70, 80, 90}
    };

    for(int i = 0; i < 3; i++)
    {
        for(int j = 0; j < 3; j++)
        {
            printf("%d ", A[i][j]);
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
10 20 30
40 50 60
70 80 90
```

---

# 17. Understanding the Nested Loops

```c
for(int i = 0; i < 3; i++)
```

controls the **rows**.

```c
for(int j = 0; j < 3; j++)
```

controls the **columns**.

Therefore:

```c
A[i][j]
```

means:

```text
A[row][column]
```

Execution:

```text
i = 0

j = 0 → A[0][0]
j = 1 → A[0][1]
j = 2 → A[0][2]

i = 1

j = 0 → A[1][0]
j = 1 → A[1][1]
j = 2 → A[1][2]

i = 2

j = 0 → A[2][0]
j = 1 → A[2][1]
j = 2 → A[2][2]
```

---

# 18. Matrix Addition

Two matrices can be added **only when they have the same dimensions**.

For example:

$$
A=
\begin{bmatrix}
1&2\\
3&4
\end{bmatrix}
$$

$$
B=
\begin{bmatrix}
5&6\\
7&8
\end{bmatrix}
$$

Then:

$$
A+B=
\begin{bmatrix}
1+5&2+6\\
3+7&4+8
\end{bmatrix}
$$

Therefore:

$$
A+B=
\begin{bmatrix}
6&8\\
10&12
\end{bmatrix}
$$

---

# 19. Matrix Addition Rule

Each element is added with the element at the **same position**.

```text
C[0][0] = A[0][0] + B[0][0]

C[0][1] = A[0][1] + B[0][1]

C[1][0] = A[1][0] + B[1][0]

C[1][1] = A[1][1] + B[1][1]
```

In general:

$$
C[i][j]=A[i][j]+B[i][j]
$$

---

# 20. C Program – Matrix Addition

```c
#include <stdio.h>

int main()
{
    int A[2][2] = {
        {1, 2},
        {3, 4}
    };

    int B[2][2] = {
        {5, 6},
        {7, 8}
    };

    int C[2][2];

    for(int i = 0; i < 2; i++)
    {
        for(int j = 0; j < 2; j++)
        {
            C[i][j] = A[i][j] + B[i][j];
        }
    }

    printf("Matrix Addition:\n");

    for(int i = 0; i < 2; i++)
    {
        for(int j = 0; j < 2; j++)
        {
            printf("%d ", C[i][j]);
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
Matrix Addition:
6 8
10 12
```

### Time Complexity

For an `m × n` matrix:

$$
O(mn)
$$

For an `n × n` matrix:

$$
O(n^2)
$$

---

# 21. Matrix Subtraction

Matrix subtraction follows the same rule as addition.

Both matrices must have the **same dimensions**.

Example:

$$
A=
\begin{bmatrix}
10&20\\
30&40
\end{bmatrix}
$$

$$
B=
\begin{bmatrix}
1&2\\
3&4
\end{bmatrix}
$$

Then:

$$
A-B=
\begin{bmatrix}
10-1&20-2\\
30-3&40-4
\end{bmatrix}
$$

Result:

$$
\begin{bmatrix}
9&18\\
27&36
\end{bmatrix}
$$

In C:

```c
C[i][j] = A[i][j] - B[i][j];
```

### Complexity

$$
O(mn)
$$

---

# 22. Matrix Multiplication

Matrix multiplication is different from addition.

Suppose:

```text
A = m × n
B = n × p
```

Multiplication is possible because:

```text
columns of A = rows of B
```

The resulting matrix will have dimensions:

```text
m × p
```

### General Rule

$$
(m\times n)(n\times p)=m\times p
$$

---

# 23. Matrix Multiplication Example

Consider:

$$
A=
\begin{bmatrix}
1&2\\
3&4
\end{bmatrix}
$$

and:

$$
B=
\begin{bmatrix}
5&6\\
7&8
\end{bmatrix}
$$

Both are:

```text
2 × 2
```

Therefore result is:

```text
2 × 2
```

---

## Calculating `C[0][0]`

Take:

```text
First row of A:       1   2

First column of B:    5
                      7
```

Multiply and add:

$$
C[0][0]=(1\times5)+(2\times7)
$$

$$
=5+14
$$

$$
=19
$$

---

## Calculating `C[0][1]`

First row of A × second column of B:

$$
C[0][1]=(1\times6)+(2\times8)
$$

$$
=6+16
$$

$$
=22
$$

---

## Calculating `C[1][0]`

$$
C[1][0]=(3\times5)+(4\times7)
$$

$$
=15+28
$$

$$
=43
$$

---

## Calculating `C[1][1]`

$$
C[1][1]=(3\times6)+(4\times8)
$$

$$
=18+32
$$

$$
=50
$$

Therefore:

$$
C=
\begin{bmatrix}
19&22\\
43&50
\end{bmatrix}
$$

---

# 24. C Program – Matrix Multiplication

```c
#include <stdio.h>

int main()
{
    int A[2][2] = {
        {1, 2},
        {3, 4}
    };

    int B[2][2] = {
        {5, 6},
        {7, 8}
    };

    int C[2][2] = {0};

    for(int i = 0; i < 2; i++)
    {
        for(int j = 0; j < 2; j++)
        {
            for(int k = 0; k < 2; k++)
            {
                C[i][j] =
                    C[i][j] + A[i][k] * B[k][j];
            }
        }
    }

    printf("Matrix Multiplication:\n");

    for(int i = 0; i < 2; i++)
    {
        for(int j = 0; j < 2; j++)
        {
            printf("%d ", C[i][j]);
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
Matrix Multiplication:
19 22
43 50
```

---

# 25. Why Three Loops Are Required?

This is an important concept.

```c
for(i)
{
    for(j)
    {
        for(k)
        {
        }
    }
}
```

Each loop has a specific purpose:

```text
i → selects row of A / row of result

j → selects column of B / column of result

k → performs multiplication and addition
```

Mathematically:

$$
C[i][j]
=
\sum_{k=0}^{n-1} A[i][k]\times B[k][j]
$$

For example:

```text
C[0][0]

= A[0][0] × B[0][0]
+ A[0][1] × B[1][0]
```

Therefore, the third loop is required to perform the summation.

### Time Complexity

For two `n × n` matrices:

$$
O(n^3)
$$

---

# 26. Matrix Transpose

## Definition

Transpose means:

> Convert rows into columns and columns into rows.

Consider:

$$
A=
\begin{bmatrix}
1&2&3\\
4&5&6
\end{bmatrix}
$$

Original:

```text
1 2 3
4 5 6
```

Transpose:

```text
1 4
2 5
3 6
```

Therefore:

$$
A^T=
\begin{bmatrix}
1&4\\
2&5\\
3&6
\end{bmatrix}
$$

---

# 27. Transpose Formula

The basic rule is:

$$
A^T[i][j]=A[j][i]
$$

In other words:

```text
row becomes column
column becomes row
```

For example:

```text
A[0][2]
```

becomes:

```text
T[2][0]
```

---

# 28. C Program – Matrix Transpose

```c
#include <stdio.h>

int main()
{
    int A[2][3] = {
        {1, 2, 3},
        {4, 5, 6}
    };

    int T[3][2];

    for(int i = 0; i < 2; i++)
    {
        for(int j = 0; j < 3; j++)
        {
            T[j][i] = A[i][j];
        }
    }

    printf("Transpose:\n");

    for(int i = 0; i < 3; i++)
    {
        for(int j = 0; j < 2; j++)
        {
            printf("%d ", T[i][j]);
        }

        printf("\n");
    }

    return 0;
}
```

Output:

```text
Transpose:
1 4
2 5
3 6
```

### Complexity

For an `m × n` matrix:

$$
O(mn)
$$

---

# 29. Searching an Element in a Matrix

Suppose:

```text
10 20 30
40 50 60
70 80 90
```

We want to search for:

```text
50
```

We can use nested loops.

```c
#include <stdio.h>

int main()
{
    int A[3][3] = {
        {10, 20, 30},
        {40, 50, 60},
        {70, 80, 90}
    };

    int key = 50;
    int found = 0;

    for(int i = 0; i < 3; i++)
    {
        for(int j = 0; j < 3; j++)
        {
            if(A[i][j] == key)
            {
                printf("Element found at [%d][%d]\n", i, j);
                found = 1;
            }
        }
    }

    if(found == 0)
    {
        printf("Element not found\n");
    }

    return 0;
}
```

Output:

```text
Element found at [1][1]
```

### Complexity

Worst case:

$$
O(mn)
$$

---

# 30. Sparse Matrix

Now consider this matrix:

$$
A=
\begin{bmatrix}
0&0&0&5\\
0&0&0&0\\
0&8&0&0\\
0&0&0&0
\end{bmatrix}
$$

Number of elements:

$$
4\times4=16
$$

Non-zero elements:

```text
5
8
```

Zero elements:

```text
14
```

Most elements are zero.

Therefore, this is a:

> **Sparse Matrix**

---

# 31. Definition of Sparse Matrix

A **Sparse Matrix** is a matrix in which the number of **zero elements is much greater than the number of non-zero elements**.

Example:

```text
0 0 0 5
0 0 0 0
0 8 0 0
0 0 0 0
```

Here:

```text
Total elements     = 16
Non-zero elements  = 2
Zero elements      = 14
```

Since most elements are zero, the matrix is sparse.

---

# 32. Dense Matrix

The opposite of a sparse matrix is a **dense matrix**.

Example:

```text
1 2 3
4 5 6
7 8 9
```

Almost all elements contain useful values.

Therefore, it is a dense matrix.

---

# 33. Why Do We Need Sparse Matrix Representation?

Suppose we have:

```text
1000 × 1000 matrix
```

Total elements:

$$
1000\times1000=1,000,000
$$

Suppose only 100 elements are non-zero.

Normal array would store:

```text
1,000,000 elements
```

But only:

```text
100 elements
```

contain meaningful values.

The remaining:

```text
999,900 elements
```

are zero.

This results in unnecessary memory usage.

Therefore:

> Instead of storing every zero, we can store only the non-zero elements.

This is called **Sparse Matrix Representation**.

---

# 34. Triplet Representation

One common method of representing a sparse matrix is:

> **3-Tuple / Triplet Representation**

For every non-zero element, we store:

```text
Row
Column
Value
```

Consider:

```text
0 0 0 5
0 0 0 0
0 8 0 0
0 0 0 0
```

Non-zero elements:

```text
5 → row 0, column 3
8 → row 2, column 1
```

Therefore:

| Row | Column | Value |
|---:|---:|---:|
| 0 | 3 | 5 |
| 2 | 1 | 8 |

---

# 35. Complete Triplet Representation

Usually, the first row stores:

```text
Number of rows
Number of columns
Number of non-zero elements
```

For our matrix:

```text
Rows = 4
Columns = 4
Non-zero = 2
```

So:

```text
+-----+--------+-------+
| Row | Column | Value |
+-----+--------+-------+
|  4  |   4    |   2   |  ← Matrix information
|  0  |   3    |   5   |
|  2  |   1    |   8   |
+-----+--------+-------+
```

The first row:

```text
4 4 2
```

means:

```text
4 → number of rows
4 → number of columns
2 → number of non-zero elements
```

---

# 36. C Program – Sparse Matrix Representation

```c
#include <stdio.h>

int main()
{
    int A[4][4] = {
        {0, 0, 0, 5},
        {0, 0, 0, 0},
        {0, 8, 0, 0},
        {0, 0, 0, 0}
    };

    int sparse[10][3];

    int rows = 4;
    int columns = 4;

    int nonZero = 0;
    int k = 1;

    // Count non-zero elements
    for(int i = 0; i < rows; i++)
    {
        for(int j = 0; j < columns; j++)
        {
            if(A[i][j] != 0)
            {
                nonZero++;
            }
        }
    }

    // Store matrix information
    sparse[0][0] = rows;
    sparse[0][1] = columns;
    sparse[0][2] = nonZero;

    // Store non-zero elements
    for(int i = 0; i < rows; i++)
    {
        for(int j = 0; j < columns; j++)
        {
            if(A[i][j] != 0)
            {
                sparse[k][0] = i;
                sparse[k][1] = j;
                sparse[k][2] = A[i][j];

                k++;
            }
        }
    }

    printf("Sparse Matrix:\n");

    for(int i = 0; i <= nonZero; i++)
    {
        printf("%d %d %d\n",
               sparse[i][0],
               sparse[i][1],
               sparse[i][2]);
    }

    return 0;
}
```

Output:

```text
Sparse Matrix:

4 4 2
0 3 5
2 1 8
```

---

# 37. Understanding the Sparse Matrix Program

## Step 1 — Original Matrix

```c
int A[4][4] = {
    {0, 0, 0, 5},
    {0, 0, 0, 0},
    {0, 8, 0, 0},
    {0, 0, 0, 0}
};
```

We have:

```text
4 rows
4 columns
```

---

## Step 2 — Count Non-Zero Elements

```c
if(A[i][j] != 0)
{
    nonZero++;
}
```

This checks every element.

If the element is not zero:

```text
nonZero++
```

For our matrix:

```text
5 → non-zero
8 → non-zero
```

Therefore:

```text
nonZero = 2
```

---

## Step 3 — Store Matrix Information

```c
sparse[0][0] = rows;
sparse[0][1] = columns;
sparse[0][2] = nonZero;
```

This produces:

```text
4 4 2
```

---

## Step 4 — Store Non-Zero Elements

For:

```text
A[0][3] = 5
```

we store:

```text
0 3 5
```

For:

```text
A[2][1] = 8
```

we store:

```text
2 1 8
```

Final result:

```text
4 4 2
0 3 5
2 1 8
```

---

# 38. Memory Comparison

Suppose:

```text
Matrix = 1000 × 1000
Non-zero elements = 100
```

## Normal Representation

Number of elements:

$$
1000\times1000=1,000,000
$$

So we store:

```text
1,000,000 integers
```

---

## Triplet Representation

For each non-zero element, we store:

```text
Row
Column
Value
```

Therefore, approximately:

```text
100 × 3 = 300 values
```

plus the metadata row.

So approximately:

```text
Normal representation → ~1,000,000 values
Sparse representation → ~303 values
```

This demonstrates why sparse representation can save significant memory.

---

# 39. When Should We Use Sparse Representation?

Sparse representation is useful when:

```text
Number of zero elements >> Number of non-zero elements
```

For example:

```text
1000 × 1000 matrix
999,000 zeros
1,000 non-zero values
```

Sparse representation is highly useful here.

But if the matrix looks like:

```text
1 2 3
4 5 6
7 8 9
```

then almost everything is non-zero.

Using sparse representation provides little or no benefit.

---

# 40. Advantages of Sparse Matrix

### 1. Saves Memory

Zeros don't need to be stored explicitly.

### 2. Efficient Storage

Only meaningful/non-zero values are stored.

### 3. Useful for Large Matrices

Especially when matrices contain very few non-zero elements.

### 4. Faster Processing in Some Applications

Algorithms can operate only on non-zero elements instead of repeatedly processing zeros.

---

# 41. Disadvantages of Sparse Matrix

### 1. Additional Representation Complexity

Instead of simply accessing:

```c
A[i][j]
```

we may need to search the sparse representation.

### 2. Direct Access May Not Be O(1)

In a simple triplet representation, finding a particular `(row, column)` may require searching the stored entries.

### 3. Not Useful for Dense Matrices

If most elements are non-zero, storing row and column information adds overhead.

---

# 42. Matrix Operations — Complexity

For an `m × n` matrix:

| Operation | Time Complexity |
|---|---:|
| Access `A[i][j]` | `O(1)` |
| Traversal | `O(m × n)` |
| Addition | `O(m × n)` |
| Subtraction | `O(m × n)` |
| Transpose | `O(m × n)` |
| Searching | `O(m × n)` |

For two `n × n` matrices:

| Operation | Time Complexity |
|---|---:|
| Addition | `O(n²)` |
| Subtraction | `O(n²)` |
| Transpose | `O(n²)` |
| Multiplication | `O(n³)` |

---

# 43. Important Rules to Remember

## Matrix Addition

```text
Same number of rows
AND
Same number of columns
```

Example:

```text
2 × 3 + 2 × 3 → Possible
```

But:

```text
2 × 3 + 3 × 2 → Not possible
```

---

## Matrix Multiplication

Condition:

```text
Columns of first matrix
=
Rows of second matrix
```

Example:

```text
A = 2 × 3
B = 3 × 4

A × B → Possible
Result = 2 × 4
```

But:

```text
A = 2 × 3
B = 2 × 4

A × B → Not possible
```

because:

```text
3 ≠ 2
```

---

# 44. Addition vs Multiplication

This distinction should be very clear.

## Addition

```text
Same position + same position
```

```c
C[i][j] = A[i][j] + B[i][j];
```

Example:

```text
A[1][2] + B[1][2]
```

---

## Multiplication

```text
Row of A × Column of B
```

```c
C[i][j] += A[i][k] * B[k][j];
```

Example:

```text
A row 1 × B column 2
```

---

# 45. Complete Concept Map

```text
MATRIX
│
├── Representation
│   │
│   ├── 2D Array
│   │
│   ├── Row-Major
│   │   ├── Row by Row
│   │   └── Formula
│   │
│   └── Column-Major
│       ├── Column by Column
│       └── Formula
│
├── Operations
│   │
│   ├── Traversal
│   ├── Addition
│   ├── Subtraction
│   ├── Multiplication
│   ├── Transpose
│   └── Searching
│
└── Sparse Matrix
    │
    ├── Mostly Zero
    ├── Dense vs Sparse
    ├── Need for Sparse Representation
    ├── Triplet Representation
    ├── C Program
    └── Memory Advantage
```

---

# 46. Exam-Oriented Questions

## Basic Questions

1. What is a matrix?
2. What is a two-dimensional array?
3. How is a matrix represented using arrays?
4. What is row-major representation?
5. What is column-major representation?
6. Which representation does C use?
7. Write the row-major address formula.
8. Write the column-major address formula.
9. What is matrix traversal?
10. What is matrix transpose?

## Conceptual Questions

11. Why is matrix addition possible only for matrices of the same order?
12. What is the condition for matrix multiplication?
13. Why are three loops required for matrix multiplication?
14. What is a sparse matrix?
15. What is a dense matrix?
16. Why do we need sparse matrix representation?
17. What is triplet representation?
18. What information is stored in a triplet representation?
19. What are the advantages of sparse matrix representation?
20. Compare normal and sparse matrix representation.

## Programming Questions

21. Write a C program to read and display a matrix.
22. Write a C program to add two matrices.
23. Write a C program to subtract two matrices.
24. Write a C program to multiply two matrices.
25. Write a C program to find the transpose.
26. Write a C program to search an element.
27. Write a C program to convert a matrix into triplet representation.
28. Write a C program to count zero and non-zero elements.

---

# 47. Quick Revision

```text
Matrix
    ↓
Rows + Columns
    ↓
2D Array
    ↓
Memory is Linear
    ↓
Row-Major / Column-Major
    ↓
Matrix Operations
    ↓
Addition
Subtraction
Multiplication
Transpose
Searching
    ↓
Sparse Matrix
    ↓
Store only non-zero elements
    ↓
Triplet Representation
(row, column, value)
```

## Most Important Formulas

### Row-Major

$$
\boxed{
Address(A[i][j])
=
Base+
[(i\times columns)+j]\times size
}
$$

### Column-Major

$$
\boxed{
Address(A[i][j])
=
Base+
[(j\times rows)+i]\times size
}
$$

### Matrix Multiplication

$$
\boxed{
C[i][j]
=
\sum_k A[i][k]B[k][j]
}
$$

### Transpose

$$
\boxed{
A^T[i][j]=A[j][i]
}
$$

### Matrix Multiplication Dimension

$$
\boxed{
(m\times n)(n\times p)=m\times p
}
$$

### Sparse Matrix

```text
Sparse Matrix
    =
Matrix with predominantly zero elements
```

### Triplet

```text
(row, column, value)
```
