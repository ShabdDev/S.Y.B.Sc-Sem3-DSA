# Assignment No: 1 Non-Recursive Sorting Techniques 

### BUBBLE SORT 
- Introduction 
- • Bubble Sort is a simple, comparison-based sorting algorithm that repeatedly compares and swaps 
- adjacent elements if they are in the wrong order. It's called "Bubble" sort because smaller values gradually 
- "bubble" to the top (front) of the list. 
 
- Working Principle: 
- • Compare each pair of adjacent elements (A[i] and A[i+1]). 
- • Swap them if they are not in the correct order (ascending or descending). 
- • Repeat the process for all elements until the entire list is sorted.

### Algorithm:
- Step1: Start 
- Step2: Accept ‘n’ numbers in array ‘A’ 
- Step3: set i=0 
- Step4: if i<n-1 then goto next step else goto step 9 
- Step4: set j=0 
- Step5: if j<n-i-1 then goto next step else goto step 8 
- Step6: if A[j] > A[j+1] then interchange A[j] and A[j+1] 
- Step7: j=j+1 and goto step 5 
- Step8: i=i+1 and goto step 4 
- Step9: Stop

### Characteristics: 
- ```
  1. Stable Sorting
  A sorting algorithm is stable if two elements having the same key/value maintain their original relative order after sorting.
  Example - Suppose we have students:
  (A, 80)
  (B, 70)
  (C, 80)
  (D, 60)
  We sort by marks:
  Before:
  A → 80
  B → 70
  C → 80
  D → 60
  After stable sorting:
  D → 60
  B → 70
  A → 80
  C → 80
  Notice:
  A → 80
  C → 80
  A was before C originally, and A is still before C.
  Therefore, the sort is stable.
  ```
- • Stable: Does not change the relative order of equal elements.
- ```
  2. In-place Sorting
  An in-place sorting algorithm performs the sorting using very little additional memory, usually O(1) extra space.
  Example:
  Original array:
  [40, 10, 30, 20]
  The algorithm rearranges the elements inside the same array:
  [10, 20, 30, 40]
  It doesn't create another array of size n.
  ```
- • In-place: Requires no additional space other than the input array.
- ```
  3. Simple Sorting

    Simple generally means the algorithm is easy to understand and implement.
    
    This is not a strict mathematical property like time complexity.
    
    For example:

    Bubble Sort
    Compare adjacent elements
            ↓
    Swap if they are in wrong order
            ↓
    Repeat

    It's very easy to understand.
    
    Selection Sort
    Find minimum
          ↓
    Put it at the beginning
          ↓
    Find next minimum
          ↓
    Repeat
    
    Also simple.
    
    Insertion Sort
    Take one element
          ↓
    Find its correct position
          ↓
    Insert it
          ↓
    Repeat
    
    Also simple.
    
    So Bubble Sort, Selection Sort, and Insertion Sort are generally called simple sorting algorithms.
  ```
- • Simple: Easy to understand and implement.

- • Worst and Average Case Time Complexity: O(n*n). Worst case occurs when array is reverse sorted. 
- • Best Case Time Complexity: O(n). Best case occurs when array is already sorted. 
- • Auxiliary Space: O(1) 
- • Boundary Cases: Bubble sort takes minimum time (Order of n) when elements are already sorted. 


-------


### INSERTION SORT 
  - Introduction 
    - It is a simple and efficient comparison-based sorting algorithm used for small datasets.
    - It builds the final sorted list one element at a time by inserting each new element into its correct position in the already sorted part of the array. 
 
  - Working Principle: 
   - • Start with the second element, compare it with the previous elements. 
   - • Shift all larger elements to the right. 
   - • Insert the current element at its correct position. 
   - • Repeat for all elements in the list. 

   - Algorithm:
      - Step1: Start 
      - Step2: Accept ‘n’ numbers and store all in array ‘A’ 
      - Step3: set i=1 
      - Step4: if i<=n-1 then goto next step else goto step 10 
      - Step5: set Temp=A[i] and j=i-1 
      - Step6: if Temp < A[j] && j>=0 then goto next step else goto step 9 
      - Step7: set A[j+1]=A[j] 
      - Step8: set j=j-1 
      - Step9: set A[j+1]=Temp 
      - Step10: Stop
    
   - Characteristics: 
   ```
    1) Time Complexity: 
    • O(n²) in the worst and average case. 
    • This happens when the list is in reverse order. 
    2) Auxiliary Space: 
    • O(1) — It uses only a small, fixed amount of extra memory (in-place sorting). 
    3) Boundary Cases: 
    • Takes the most time when the list is sorted in reverse order. 
    • Takes the least time (O(n)) when the list is already sorted. 
    4) Algorithm Type: 
    • Based on the Incremental Approach — builds the sorted list one element at a time. 
    5) In-Place Sorting: 
    • Yes, it doesn’t need extra memory to sort. 
    6) Stable Sort: 
    • Yes, equal elements stay in the same relative order after sorting.
   ```

# Set A
## 1) Write a C program to accept n integers from user and sort it in ascending order by using bubble sort. 
```
#include <stdio.h>

int main()
{
    int a[100], n, i, j, temp;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter %d integers:\n", n);
    for(i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
    }

    // Bubble Sort
    for(i = 0; i < n - 1; i++)
    {
        for(j = 0; j < n - 1 - i; j++)
        {
            if(a[j] > a[j + 1])
            {
                temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
            }
        }
    }

    printf("Array after sorting in ascending order:\n");

    for(i = 0; i < n; i++)
    {
        printf("%d ", a[i]);
    }

    return 0;
}
```
----

## 2) Write a C program to sort an array of n integers in ascending order by using insertion sort algorithm. 

```
#include <stdio.h>

int main()
{
    int a[100], n, i, j, key;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter %d integers:\n", n);
    for(i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
    }

    // Insertion Sort
    for(i = 1; i < n; i++)
    {
        key = a[i];
        j = i - 1;

        while(j >= 0 && a[j] > key)
        {
            a[j + 1] = a[j];
            j--;
        }

        a[j + 1] = key;
    }

    printf("Array after sorting in ascending order:\n");

    for(i = 0; i < n; i++)
    {
        printf("%d ", a[i]);
    }

    return 0;
}
```
----

```
| Feature                     | Bubble Sort                      | Insertion Sort |
| --------------------------- | -------------------------------- | -------------- |
| Basic operation             | Compare & swap adjacent elements | Shift & insert |
| Best case                   | O(n)*                            | O(n)           |
| Average                     | O(n²)                            | O(n²)          |
| Worst                       | O(n²)                            | O(n²)          |
| Auxiliary Space             | O(1)                             | O(1)           |
| Stable                      | Yes                              | Yes            |
| In-place                    | Yes                              | Yes            |
| Good for nearly sorted data | Not as good                      | **Yes**        |

```
-----

# SET B: 
## 1) Write a C program to read the data from “studinfo.txt” file which contains student’s information: rollno and student_name and sort the data on student_name alphabetically using Bubble Sort (use strcmp). 

```
studinfo.txt
The file can contain data like:

101 Rahul
102 Amit
103 Priya
104 Neha
105 Kiran

#include <stdio.h>
#include <string.h>

struct Student
{
    int rollno;
    char student_name[50];
};

int main()
{
    struct Student s[100], temp;
    FILE *fp;
    int n = 0;
    int i, j;

    // Open file for reading
    fp = fopen("studinfo.txt", "r");

    if (fp == NULL)
    {
        printf("Unable to open file.\n");
        return 1;
    }

    // Read data from file
    while (fscanf(fp, "%d %s", &s[n].rollno, s[n].student_name) == 2)
    {
        n++;
    }

    fclose(fp);

    // Bubble Sort based on student_name
    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - 1 - i; j++)
        {
            if (strcmp(s[j].student_name, s[j + 1].student_name) > 0)
            {
                temp = s[j];
                s[j] = s[j + 1];
                s[j + 1] = temp;
            }
        }
    }

    // Display sorted data
    printf("\nStudent information sorted by name:\n");

    for (i = 0; i < n; i++)
    {
        printf("%d\t%s\n", s[i].rollno, s[i].student_name);
    }

    return 0;
}
```
----
  
## 2) Write a C program to read the data from the file “emp.txt” which contains emp_id and emp_age and sort the data on age in ascending order using insertion Sort. 

```
Example emp.txt
101 35
102 22
103 40
104 28
105 25
After sorting by age:

102 22
105 25
104 28
101 35
103 40

#include <stdio.h>

struct Employee
{
    int emp_id;
    int emp_age;
};

int main()
{
    struct Employee emp[100], key;
    FILE *fp;
    int n = 0;
    int i, j;

    // Open file in read mode
    fp = fopen("emp.txt", "r");

    if (fp == NULL)
    {
        printf("Unable to open file.\n");
        return 1;
    }

    // Read employee data from file
    while (fscanf(fp, "%d %d",
                  &emp[n].emp_id,
                  &emp[n].emp_age) == 2)
    {
        n++;
    }

    fclose(fp);

    // Insertion Sort based on age
    for (i = 1; i < n; i++)
    {
        key = emp[i];
        j = i - 1;

        while (j >= 0 && emp[j].emp_age > key.emp_age)
        {
            emp[j + 1] = emp[j];
            j--;
        }

        emp[j + 1] = key;
    }

    // Display sorted employee data
    printf("\nEmployee data sorted by age:\n");

    for (i = 0; i < n; i++)
    {
        printf("%d\t%d\n", emp[i].emp_id, emp[i].emp_age);
    }

    return 0;
}

```
---
```
| Program               | Best Time | Average Time | Worst Time |          Space |
| --------------------- | --------: | -----------: | ---------: | -------------: |
| **1. Bubble Sort**    |     O(n)* |        O(n²) |      O(n²) | O(1) auxiliary |
| **2. Insertion Sort** |      O(n) |        O(n²) |      O(n²) | O(1) auxiliary |
```
---

# SET C: 
## 1) Write a C program to generate n random nos. using rand () function and store it in an array. Apply Bubble sort (in descending order) on this array. 

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int a[100], n, i, j, temp;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    // Generate random numbers
    printf("\nRandom numbers:\n");

    for(i = 0; i < n; i++)
    {
        a[i] = rand() % 100;
        printf("%d ", a[i]);
    }

    // Bubble Sort in descending order
    for(i = 0; i < n - 1; i++)
    {
        for(j = 0; j < n - 1 - i; j++)
        {
            if(a[j] < a[j + 1])
            {
                temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
            }
        }
    }

    // Display sorted array
    printf("\n\nArray after sorting in descending order:\n");

    for(i = 0; i < n; i++)
    {
        printf("%d ", a[i]);
    }

    return 0;
}
```
```
Generating n numbers → O(n)

Bubble Sort:
Best    → O(n²) for this exact unoptimized code
Average → O(n²)
Worst   → O(n²)

Auxiliary Space → O(1)
```

----
## 2) Write a C program to sort a random array of n integers (using rand () function) by using Insertion Sort algorithm in descending order. 

```
#include <stdio.h>
#include <stdlib.h>

int main()
{
    int a[100], n, i, j, key;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    // Generate random numbers
    printf("\nRandom array:\n");

    for(i = 0; i < n; i++)
    {
        a[i] = rand() % 100;
        printf("%d ", a[i]);
    }

    // Insertion Sort in descending order
    for(i = 1; i < n; i++)
    {
        key = a[i];
        j = i - 1;

        while(j >= 0 && a[j] < key)
        {
            a[j + 1] = a[j];
            j--;
        }

        a[j + 1] = key;
    }

    // Display sorted array
    printf("\n\nArray after sorting in descending order:\n");

    for(i = 0; i < n; i++)
    {
        printf("%d ", a[i]);
    }

    return 0;
}
```
```
| Case    |  Time |
| ------- | ----: |
| Best    |  O(n) |
| Average | O(n²) |
| Worst   | O(n²) |

Auxiliary Space = O(1)

```
-----

## 3) Write a C program to sort the elements by initializing the array (e.g int Arr[5] = {35,66,10,31}) using bubble sort.

```
#include <stdio.h>

int main()
{
    int Arr[4] = {35, 66, 10, 31};
    int i, j, temp;

    // Bubble Sort in ascending order
    for(i = 0; i < 4 - 1; i++)
    {
        for(j = 0; j < 4 - 1 - i; j++)
        {
            if(Arr[j] > Arr[j + 1])
            {
                temp = Arr[j];
                Arr[j] = Arr[j + 1];
                Arr[j + 1] = temp;
            }
        }
    }

    printf("Array after sorting:\n");

    for(i = 0; i < 4; i++)
    {
        printf("%d ", Arr[i]);
    }

    return 0;
}
```
```
Time:
Best    = O(n²)   // for this basic version
Average = O(n²)
Worst   = O(n²)

Auxiliary Space = O(1)
```
