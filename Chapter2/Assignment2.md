Recursive Sorting Techniques 

```
INTRODUCTION 
1. Quick Sort 
Quick Sort is a Divide and Conquer algorithm. It picks an element as pivot and partitions the 
given array around the picked pivot. 
Key Idea: 
• Pick a pivot (we'll choose the first element). 
• Partition the array so that: 
o Elements less than the pivot go to the left. 
o Elements greater than the pivot go to the right. 
• Recursively apply this process to the left and right sub-arrays. 
Algorithm: 
Step 1: start. 
Step 2: A is an array of n element. 
Step 3:lb=0 //lb = lower bound     
       ub=n-1 //ub = upper bound. 
Step 4: if(lb<ub)  
          j=partition(A,lb,ub) // j is the pivot position 
 
quicksort(A,lb,j-1); 
quicksort(A,j+1,ub); 
 
• Now, we must write the function to partition the array. There are many methods to do the 
partitioning depending upon which element is chosen as the pivot. 
• We will be selecting the first element as the pivot element and do the partitioning accordingly. 
• We shall choose the first element of the sub- array as the pivot and find its correct position in the sub
array. 
• We will be using two variables down and up for moving down and up array. 
 
Algorithm for partitioning 
Step 1:down=lb+1 
Step 2:up=ub  
Step 3:pivot=A[lb] 
Step 4: perform step 5 to 7 as long as down<up else go to step 8.  
Step 5: while (A[down]<=pivot&&down<ub) 
          down++;  
Step 6: while(A[up]>pivot) 
          up--; 
Step 7: if (down<up) interchange A[down] and A[up] 
Step 8: interchange A[up]and pivot,j=up  
Step 9: return up 
Step 10: stop. 
• In this algorithm we want to find the position of pivot i.e.A[lb]. 
• We use two pointers up and down initialized to the first and last elements respectively. 
• We repeatedly increase down as long as the element is < pivot. 
• We repeatedly decrease up as long as the element is > pivot. 
 
Assignment No: 2 Recursive Sorting Techniques 
6 
 
• If up and down cross each other i.e. up<=down, the correct position of the pivot is up and  A[up] and 
pivot are inter changed. 
• If up and down do not cross A[up] and A[down] are interchanged and process is repeated till they do 
not cross or coincide. 
 
• Efficiency of quicksort. 
Best case = average case = O(nlogn) 
Worst case = O(n2) 
 
Example: Array Elements:9,-3,5,2,6,8,-6,1,3

-----------------------------------------------------------------------------------------------------------------------

 Merge Sort 
• Merging is the process of combining two or more sorted data lists into a third list such that it is 
also sorted. 
• Merge sort follows Divide and Conquer strategy. - Divide :- Divide the list or array recursively into two halves until it can no more be divided. - Conquer :- Each subarray is sorted individually using the merge sort algorithm. - Combine :- The sorted subarrays are merged back together in sorted order. The process  
continues until all elements from both subarrays have been merged. 
• In this, two lists are compared and the smallest element is stored in the third array. 
Algorithm:-  
Step 1: Start 
Step 2: initially the data is considered as a single array of n element. 
Step 3: divide the array into n/2 sub-array each of length 2i (i is 0 for 0th   
        iteration). i.e. array is divided into n sub-arrays each of 1    
        element. 
Step 4: merge two consecutive pairs of sub-arrays such that the  
        resulting sub-array is also sorted.  
Step 5: The sub-array having no pairs is carried as it is. 
Step 6: step 3 and 4 are repeated till there is only one sub- 
        array remaining of size n.  
Step 7: stop. 
7 
 
Example: Array Elements: 6,5,12,10,9,1 
```

# SET A: 
```
1) Write a program in C to accept 5 numbers from the user and sort the numbers in ascending order by 
using Quicksort.

#include <stdio.h>

void quickSort(int a[], int low, int high)
{
    int i, j, pivot, temp;

    if (low < high)
    {
        pivot = a[low];
        i = low;
        j = high;

        while (i < j)
        {
            // Find element greater than pivot
            while (a[i] <= pivot && i < high)
            {
                i++;
            }

            // Find element smaller than pivot
            while (a[j] > pivot)
            {
                j--;
            }

            // Swap elements
            if (i < j)
            {
                temp = a[i];
                a[i] = a[j];
                a[j] = temp;
            }
        }

        // Put pivot in its correct position
        temp = a[low];
        a[low] = a[j];
        a[j] = temp;

        // Sort left part
        quickSort(a, low, j - 1);

        // Sort right part
        quickSort(a, j + 1, high);
    }
}

int main()
{
    int a[5], i;

    printf("Enter 5 numbers:\n");

    for (i = 0; i < 5; i++)
    {
        scanf("%d", &a[i]);
    }

    quickSort(a, 0, 4);

    printf("Array after sorting in ascending order:\n");

    for (i = 0; i < 5; i++)
    {
        printf("%d ", a[i]);
    }

    return 0;
}

=========================================================================================================================

| Case    | Time Complexity |
| ------- | --------------: |
| Best    |      O(n log n) |
| Average |      O(n log n) |
| Worst   |           O(n²) |

Average Auxiliary Space → O(log n)
Worst Auxiliary Space   → O(n)

=========================================================================================================================
```
```
2) Write a C program to sort a random array of n integers by using Quick Sort algorithm in ascending 
order.

#include <stdio.h>
#include <stdlib.h>

void quickSort(int a[], int low, int high)
{
    int i, j, pivot, temp;

    if (low < high)
    {
        pivot = a[low];
        i = low;
        j = high;

        while (i < j)
        {
            // Find element greater than pivot
            while (a[i] <= pivot && i < high)
            {
                i++;
            }

            // Find element smaller than pivot
            while (a[j] > pivot)
            {
                j--;
            }

            // Swap elements
            if (i < j)
            {
                temp = a[i];
                a[i] = a[j];
                a[j] = temp;
            }
        }

        // Place pivot at its correct position
        temp = a[low];
        a[low] = a[j];
        a[j] = temp;

        // Sort left part
        quickSort(a, low, j - 1);

        // Sort right part
        quickSort(a, j + 1, high);
    }
}

int main()
{
    int a[100], n, i;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    // Generate random numbers
    printf("\nRandom array:\n");

    for (i = 0; i < n; i++)
    {
        a[i] = rand() % 100;
        printf("%d ", a[i]);
    }

    // Apply Quick Sort
    quickSort(a, 0, n - 1);

    // Display sorted array
    printf("\n\nArray after sorting in ascending order:\n");

    for (i = 0; i < n; i++)
    {
        printf("%d ", a[i]);
    }

    return 0;
}

========================================================================================================================
| Case    | Time Complexity |
| ------- | --------------: |
| Best    |      O(n log n) |
| Average |      O(n log n) |
| Worst   |           O(n²) |

Auxiliary Space:
Average → O(log n)
Worst   → O(n)
========================================================================================================================

```
```
3) Write a C program to accept and sort n elements in ascending order by using Quicksort.

#include <stdio.h>

void quickSort(int a[], int low, int high)
{
    int i, j, pivot, temp;

    if (low < high)
    {
        pivot = a[low];
        i = low;
        j = high;

        while (i < j)
        {
            // Find element greater than pivot
            while (a[i] <= pivot && i < high)
            {
                i++;
            }

            // Find element smaller than or equal to pivot
            while (a[j] > pivot)
            {
                j--;
            }

            // Swap elements
            if (i < j)
            {
                temp = a[i];
                a[i] = a[j];
                a[j] = temp;
            }
        }

        // Place pivot in its correct position
        temp = a[low];
        a[low] = a[j];
        a[j] = temp;

        // Sort left part
        quickSort(a, low, j - 1);

        // Sort right part
        quickSort(a, j + 1, high);
    }
}

int main()
{
    int a[100], n, i;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter %d elements:\n", n);

    for (i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
    }

    quickSort(a, 0, n - 1);

    printf("Array after sorting in ascending order:\n");

    for (i = 0; i < n; i++)
    {
        printf("%d ", a[i]);
    }

    return 0;
}

====================================================================================================================
Best Case    : O(n log n)
Average Case : O(n log n)
Worst Case   : O(n²)

Auxiliary Space:
Average : O(log n)
Worst   : O(n)

====================================================================================================================

```

# SET B: 
```
1) Write a program in C to accept 5 numbers from the user and sort the numbers in ascending order by 
using Merge sort.

#include <stdio.h>

void merge(int a[], int low, int mid, int high)
{
    int i, j, k;
    int temp[5];

    i = low;
    j = mid + 1;
    k = low;

    while (i <= mid && j <= high)
    {
        if (a[i] < a[j])
        {
            temp[k] = a[i];
            i++;
        }
        else
        {
            temp[k] = a[j];
            j++;
        }
        k++;
    }

    while (i <= mid)
    {
        temp[k] = a[i];
        i++;
        k++;
    }

    while (j <= high)
    {
        temp[k] = a[j];
        j++;
        k++;
    }

    for (i = low; i <= high; i++)
    {
        a[i] = temp[i];
    }
}

void mergeSort(int a[], int low, int high)
{
    int mid;

    if (low < high)
    {
        mid = (low + high) / 2;

        mergeSort(a, low, mid);
        mergeSort(a, mid + 1, high);

        merge(a, low, mid, high);
    }
}

int main()
{
    int a[5], i;

    printf("Enter 5 numbers:\n");

    for (i = 0; i < 5; i++)
    {
        scanf("%d", &a[i]);
    }

    mergeSort(a, 0, 4);

    printf("Array after sorting in ascending order:\n");

    for (i = 0; i < 5; i++)
    {
        printf("%d ", a[i]);
    }

    return 0;
}

===================================================================================================================
| Case            | Time Complexity |
| --------------- | --------------- |
| Best            | O(n log n)      |
| Average         | O(n log n)      |
| Worst           | O(n log n)      |
| Auxiliary Space | O(n)            |
===================================================================================================================

```
```
2) Write a C program to sort a random array of n integers by using Merge Sort algorithm in ascending 
order.

#include <stdio.h>
#include <stdlib.h>

void merge(int a[], int low, int mid, int high)
{
    int i, j, k;
    int temp[100];

    i = low;
    j = mid + 1;
    k = low;

    while (i <= mid && j <= high)
    {
        if (a[i] < a[j])
        {
            temp[k] = a[i];
            i++;
        }
        else
        {
            temp[k] = a[j];
            j++;
        }
        k++;
    }

    while (i <= mid)
    {
        temp[k] = a[i];
        i++;
        k++;
    }

    while (j <= high)
    {
        temp[k] = a[j];
        j++;
        k++;
    }

    for (i = low; i <= high; i++)
    {
        a[i] = temp[i];
    }
}

void mergeSort(int a[], int low, int high)
{
    int mid;

    if (low < high)
    {
        mid = (low + high) / 2;

        mergeSort(a, low, mid);
        mergeSort(a, mid + 1, high);

        merge(a, low, mid, high);
    }
}

int main()
{
    int a[100], n, i;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("\nRandom array:\n");

    for (i = 0; i < n; i++)
    {
        a[i] = rand() % 100;
        printf("%d ", a[i]);
    }

    mergeSort(a, 0, n - 1);

    printf("\n\nArray after sorting in ascending order:\n");

    for (i = 0; i < n; i++)
    {
        printf("%d ", a[i]);
    }

    return 0;
}

================================================================================================================
| Case            | Time Complexity |
| --------------- | --------------- |
| Best            | O(n log n)      |
| Average         | O(n log n)      |
| Worst           | O(n log n)      |
| Auxiliary Space | O(n)            |
================================================================================================================
```

# Set C

```
1) Write a C program to sort the elements by initializing the array (e.g. int A[5] = {20,30,44,51,87}) 
using Merge sort.

#include <stdio.h>

void merge(int A[], int low, int mid, int high)
{
    int i, j, k;
    int temp[5];

    i = low;
    j = mid + 1;
    k = low;

    while (i <= mid && j <= high)
    {
        if (A[i] < A[j])
        {
            temp[k] = A[i];
            i++;
        }
        else
        {
            temp[k] = A[j];
            j++;
        }
        k++;
    }

    while (i <= mid)
    {
        temp[k] = A[i];
        i++;
        k++;
    }

    while (j <= high)
    {
        temp[k] = A[j];
        j++;
        k++;
    }

    for (i = low; i <= high; i++)
    {
        A[i] = temp[i];
    }
}

void mergeSort(int A[], int low, int high)
{
    int mid;

    if (low < high)
    {
        mid = (low + high) / 2;

        mergeSort(A, low, mid);
        mergeSort(A, mid + 1, high);

        merge(A, low, mid, high);
    }
}

int main()
{
    int A[5] = {20, 30, 44, 51, 87};
    int i;

    printf("Original array:\n");

    for (i = 0; i < 5; i++)
    {
        printf("%d ", A[i]);
    }

    mergeSort(A, 0, 4);

    printf("\n\nArray after sorting using Merge Sort:\n");

    for (i = 0; i < 5; i++)
    {
        printf("%d ", A[i]);
    }

    return 0;
}

```
```
2) Write a C program to sort the elements by initializing the array (e.g. int A[5] = {17,12,23,4,8}) 
using Quick Sort.


#include <stdio.h>

void quickSort(int A[], int low, int high)
{
    int i, j, pivot, temp;

    if (low < high)
    {
        pivot = A[low];

        i = low;
        j = high;

        while (i < j)
        {
            while (A[i] <= pivot && i < high)
            {
                i++;
            }

            while (A[j] > pivot)
            {
                j--;
            }

            if (i < j)
            {
                temp = A[i];
                A[i] = A[j];
                A[j] = temp;
            }
        }

        temp = A[low];
        A[low] = A[j];
        A[j] = temp;

        quickSort(A, low, j - 1);
        quickSort(A, j + 1, high);
    }
}

int main()
{
    int A[5] = {17, 12, 23, 4, 8};
    int i;

    printf("Original array:\n");

    for (i = 0; i < 5; i++)
    {
        printf("%d ", A[i]);
    }

    quickSort(A, 0, 4);

    printf("\n\nArray after sorting using Quick Sort:\n");

    for (i = 0; i < 5; i++)
    {
        printf("%d ", A[i]);
    }

    return 0;
}
```
