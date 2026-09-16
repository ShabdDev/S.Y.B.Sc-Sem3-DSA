Searching Techniques

```
1. Linear Search: 
• Linear search is one of the most basic search techniques. 
•  It involves checking each element in a list or array one by one until the desired item is found. 
•  If a match is located, that item is returned immediately; otherwise, the search goes on until all 
elements have been examined.  
• Time Complexity of Linear Search is Best Case O (1), Worst case O(n) where n is the number of 
elements. 
Example 1: 
Input arr[] = {15, 25, 45, 90, 35, 60, 75, 120, 30, 55} 
Search element x = 75; 
Output: 
The element is present at 6th index position. 
Example 2: 
Input: arr[] = {5, 18, 25, 33, 47, 59, 68, 72, 89, 95} 
Search element x = 50; 
Output: 
Element x is not present in arr[]. 
 
Algorithm: Linear_Search(arr, n, x) 
1. Start 
2. Input:  
      - arr[]: array of elements 
      - n: number of elements in arr[] 
      - x: element to search for 
3. Repeat for i = 0 to n - 1 
      a. If arr[i] == x 
            - Return i (index where x is found) 
4. If loop completes and no match is found 
      - Return -1 (x not found) 
5. End 
 
2. Binary Search:  
• In binary search, the array must be sorted before start searching process.  
• The method starts by comparing the target value with the middle item.  
• Based on the comparison, the algorithm eliminates half of the remaining elements and 
focuses on the relevant half. 
• This continues until the value is found or the subarray becomes empty.  
• The search is efficient, with a time complexity of O(log₂ n).

Algorithm: BINARY_SEARCH(arr, n, x) 
 
1. Start 
2. Input:  
      arr[]: a sorted array of 'n' elements 
      x: the target value to search 
3. Initialize: 
      low = 0 
      high = n - 1 
4. Repeat while low ≤ high: 
     a. mid = (low + high) / 2 
     b. If arr[mid] == x: 
           Return mid (element found) 
     c. Else if x < arr[mid]: 
           high = mid - 1 (search in left half) 
     d. Else: 
           low = mid + 1 (search in right half) 
5. If loop ends, element not found: 
      Return -1 
6. End
```

# Set A
```

1) Write a C program to implement linear search on an integer array. Search a given key in an 
array.

#include <stdio.h>

int main()
{
    int A[100], n, key, i, found = 0;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter %d elements:\n", n);

    for (i = 0; i < n; i++)
    {
        scanf("%d", &A[i]);
    }

    printf("Enter the key to search: ");
    scanf("%d", &key);

    for (i = 0; i < n; i++)
    {
        if (A[i] == key)
        {
            printf("Key %d found at position %d\n", key, i + 1);
            found = 1;
            break;
        }
    }

    if (found == 0)
    {
        printf("Key %d not found in the array\n", key);
    }

    return 0;
}

=====================================================================================================================
| Case            | Time Complexity |
| --------------- | --------------- |
| Best Case       | O(1)            |
| Average Case    | O(n)            |
| Worst Case      | O(n)            |
| Auxiliary Space | O(1)            |
======================================================================================================================
```
```
2) Write a C program that accepts an integer input from the user and search for key element in a 
sorted array using binary search.

#include <stdio.h>

int main()
{
    int A[100], n, key;
    int low, high, mid;
    int found = 0;
    int i;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter %d elements in sorted order:\n", n);

    for (i = 0; i < n; i++)
    {
        scanf("%d", &A[i]);
    }

    printf("Enter the key to search: ");
    scanf("%d", &key);

    low = 0;
    high = n - 1;

    while (low <= high)
    {
        mid = (low + high) / 2;

        if (A[mid] == key)
        {
            printf("Key %d found at position %d\n", key, mid + 1);
            found = 1;
            break;
        }
        else if (key < A[mid])
        {
            high = mid - 1;
        }
        else
        {
            low = mid + 1;
        }
    }

    if (found == 0)
    {
        printf("Key %d not found in the array\n", key);
    }

    return 0;
}
================================================================================================================
| Case            | Time Complexity |
| --------------- | --------------- |
| Best Case       | O(1)            |
| Average Case    | O(log n)        |
| Worst Case      | O(log n)        |
| Auxiliary Space | O(1)            |
================================================================================================================

```
# Set B

```

1) Write a C program to create an array of strings. Accept student name from user and use linear 
search method to check whether the given student’s name is present or not. Display proper message 
in output.

#include <stdio.h>
#include <string.h>

int main()
{
    char names[5][50];
    char key[50];
    int i, found = 0;

    printf("Enter names of 5 students:\n");

    for (i = 0; i < 5; i++)
    {
        scanf("%s", names[i]);
    }

    printf("Enter student name to search: ");
    scanf("%s", key);

    for (i = 0; i < 5; i++)
    {
        if (strcmp(names[i], key) == 0)
        {
            printf("Student name '%s' is present in the array.\n", key);
            found = 1;
            break;
        }
    }

    if (found == 0)
    {
        printf("Student name '%s' is not present in the array.\n", key);
    }

    return 0;
}
```
```
2) Write a C program to accept n elements from user store it in an array. Accept a value from the user 
and use recursive binary search method to check whether the value is present in array or not.

#include <stdio.h>

int binarySearch(int A[], int low, int high, int key)
{
    int mid;

    if (low > high)
    {
        return -1;
    }

    mid = (low + high) / 2;

    if (A[mid] == key)
    {
        return mid;
    }
    else if (key < A[mid])
    {
        return binarySearch(A, low, mid - 1, key);
    }
    else
    {
        return binarySearch(A, mid + 1, high, key);
    }
}

int main()
{
    int A[100], n, key;
    int i, j, temp, result;

    printf("Enter number of elements: ");
    scanf("%d", &n);

    printf("Enter %d elements:\n", n);

    for (i = 0; i < n; i++)
    {
        scanf("%d", &A[i]);
    }

    /* Sort the array */
    for (i = 0; i < n - 1; i++)
    {
        for (j = 0; j < n - 1 - i; j++)
        {
            if (A[j] > A[j + 1])
            {
                temp = A[j];
                A[j] = A[j + 1];
                A[j + 1] = temp;
            }
        }
    }

    printf("Sorted array:\n");

    for (i = 0; i < n; i++)
    {
        printf("%d ", A[i]);
    }

    printf("\nEnter value to search: ");
    scanf("%d", &key);

    result = binarySearch(A, 0, n - 1, key);

    if (result != -1)
    {
        printf("Value %d is present at position %d.\n", key, result + 1);
    }
    else
    {
        printf("Value %d is not present in the array.\n", key);
    }

    return 0;
}
```
# Set C

```

1) Write a C program to read the data from file 'cities.txt' containing names of 10 cities and their STD 
codes. Accept a name of the city from user and use linear search algorithm to check whether the 
name is present in the file and output the STD code, otherwise output “city not in the list”.

1. Create cities.txt

Keep the file in the same folder as your C program.

Example:

Pune 020
Mumbai 022
Delhi 011
Nagpur 0712
Nashik 0253
Bangalore 080
Chennai 044
Hyderabad 040
Kolkata 033
Ahmedabad 079

2. CProgram.c
#include <stdio.h>
#include <string.h>

int main()
{
    char city[50], searchCity[50];
    int stdCode;
    int found = 0;

    FILE *fp;

    fp = fopen("cities.txt", "r");

    if (fp == NULL)
    {
        printf("Unable to open cities.txt\n");
        return 1;
    }

    printf("Enter city name to search: ");
    scanf("%s", searchCity);

    while (fscanf(fp, "%s %d", city, &stdCode) == 2)
    {
        if (strcmp(city, searchCity) == 0)
        {
            printf("City: %s\n", city);
            printf("STD Code: %d\n", stdCode);

            found = 1;
            break;
        }
    }

    fclose(fp);

    if (found == 0)
    {
        printf("city not in the list\n");
    }

    return 0;
}
```




