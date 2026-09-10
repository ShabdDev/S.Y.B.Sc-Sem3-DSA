# Sorting Techniques in C

## Bubble Sort, Insertion Sort, Merge Sort and Quick Sort

Sorting means arranging data elements in a particular order, usually ascending or descending.

This file covers four important sorting techniques:

1. Bubble Sort
2. Insertion Sort
3. Merge Sort
4. Quick Sort

---

# 1. Important Sorting Terminology

## Stable Sorting

A sorting algorithm is **stable** if equal elements maintain their original relative order.

Example:

```text
Before:
(80,A) (70,B) (80,C)

After stable sorting:
(70,B) (80,A) (80,C)
```

## In-place Sorting

An algorithm is called **in-place** when it uses only a small amount of extra memory apart from the input array.

Examples:

- Bubble Sort → In-place
- Insertion Sort → In-place
- Quick Sort → Generally in-place
- Merge Sort → Standard array implementation is not in-place

## Divide and Conquer

Divide and Conquer means:

```text
Divide
  ↓
Solve smaller problems
  ↓
Combine
```

Merge Sort and Quick Sort use this approach.

---

# 2. Bubble Sort

## Definition

**Bubble Sort** repeatedly compares adjacent elements and swaps them if they are in the wrong order.

After each pass, one element reaches its correct position.

---

## Real-Life Example

Imagine students standing in a line according to height.

Compare neighboring students. If the taller student is before the shorter student, swap them.

This repeated adjacent comparison is similar to Bubble Sort.

---

## Example

Input:

```text
5  3  8  4  2
```

### Pass 1

```text
5 3 8 4 2
↓
3 5 8 4 2
↓
3 5 8 4 2
↓
3 5 4 8 2
↓
3 5 4 2 8
```

`8` reaches its correct position.

### Pass 2

```text
3 5 4 2 8
↓
3 4 5 2 8
↓
3 4 2 5 8
```

### Pass 3

```text
3 4 2 5 8
↓
3 2 4 5 8
```

### Pass 4

```text
3 2 4 5 8
↓
2 3 4 5 8
```

Final:

```text
2 3 4 5 8
```

---

## Algorithm

```text
BubbleSort(A, n)

for i = 0 to n-2
    swapped = false

    for j = 0 to n-i-2
        if A[j] > A[j+1]
            swap A[j], A[j+1]
            swapped = true

    if swapped == false
        break
```

---

## C Program

```c
#include <stdio.h>

void bubbleSort(int arr[], int n)
{
    int i, j, temp;
    int swapped;

    for (i = 0; i < n - 1; i++)
    {
        swapped = 0;

        for (j = 0; j < n - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;

                swapped = 1;
            }
        }

        if (swapped == 0)
            break;
    }
}

int main()
{
    int arr[] = {5, 3, 8, 4, 2};
    int n = sizeof(arr) / sizeof(arr[0]);

    bubbleSort(arr, n);

    printf("Sorted array: ");

    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);

    return 0;
}
```

---

## Program Explanation

### `arr[]`

Stores the input elements.

### `sizeof(arr) / sizeof(arr[0])`

Calculates the number of elements.

### Outer loop

```c
for (i = 0; i < n - 1; i++)
```

Controls the passes.

### Inner loop

```c
for (j = 0; j < n - i - 1; j++)
```

Compares adjacent elements.

### Comparison

```c
if (arr[j] > arr[j + 1])
```

If the left element is greater, swap the two elements.

### `swapped`

If no swap occurs during a complete pass, the array is already sorted.

---

## Time and Space Complexity

| Case | Complexity |
|---|---:|
| Best Case | `O(n)`* |
| Average Case | `O(n²)` |
| Worst Case | `O(n²)` |
| Space | `O(1)` |

`*` Best case is `O(n)` with the `swapped` optimization.

### Properties

| Property | Value |
|---|---|
| Stable | Yes |
| In-place | Yes |
| Extra Space | `O(1)` |
| Type | Comparison-based |

---

# 3. Insertion Sort

## Definition

**Insertion Sort** builds the sorted array one element at a time.

Each new element is inserted into its correct position in the already sorted portion.

---

## Real-Life Example

Insertion Sort is similar to arranging playing cards.

If you have:

```text
5
```

and receive `3`, place it before `5`:

```text
3 5
```

Receive `8`:

```text
3 5 8
```

Receive `4`:

```text
3 4 5 8
```

Receive `2`:

```text
2 3 4 5 8
```

---

## Example

Input:

```text
5 3 8 4 2
```

Initially:

```text
5 | 3 8 4 2
```

Insert `3`:

```text
3 5 | 8 4 2
```

Insert `8`:

```text
3 5 8 | 4 2
```

Insert `4`:

```text
3 4 5 8 | 2
```

Insert `2`:

```text
2 3 4 5 8
```

---

## Algorithm

```text
InsertionSort(A, n)

for i = 1 to n-1
    key = A[i]
    j = i - 1

    while j >= 0 AND A[j] > key
        A[j+1] = A[j]
        j = j - 1

    A[j+1] = key
```

---

## C Program

```c
#include <stdio.h>

void insertionSort(int arr[], int n)
{
    int i, j, key;

    for (i = 1; i < n; i++)
    {
        key = arr[i];
        j = i - 1;

        while (j >= 0 && arr[j] > key)
        {
            arr[j + 1] = arr[j];
            j--;
        }

        arr[j + 1] = key;
    }
}

int main()
{
    int arr[] = {5, 3, 8, 4, 2};
    int n = sizeof(arr) / sizeof(arr[0]);

    insertionSort(arr, n);

    printf("Sorted array: ");

    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);

    return 0;
}
```

---

## Program Explanation

### `key`

Stores the current element that must be inserted.

### `j`

Starts from the element immediately before `key`.

### While condition

```c
while (j >= 0 && arr[j] > key)
```

Moves larger elements one position to the right.

### Insert

```c
arr[j + 1] = key;
```

Places the key at its correct position.

---

## Time and Space Complexity

| Case | Complexity |
|---|---:|
| Best Case | `O(n)` |
| Average Case | `O(n²)` |
| Worst Case | `O(n²)` |
| Space | `O(1)` |

### Properties

| Property | Value |
|---|---|
| Stable | Yes |
| In-place | Yes |
| Extra Space | `O(1)` |
| Type | Comparison-based |

---

# 4. Merge Sort

## Definition

**Merge Sort** is a Divide and Conquer sorting algorithm.

It:

1. Divides the array into smaller parts.
2. Recursively sorts those parts.
3. Merges the sorted parts.

---

## Real-Life Example

Suppose 8 students need to be sorted according to marks.

Instead of sorting all 8 at once:

```text
8
↓
4 + 4
↓
2 + 2 + 2 + 2
↓
1 + 1 + 1 + 1 + 1 + 1 + 1 + 1
```

Then merge the smaller sorted groups.

---

## Example

Input:

```text
5 3 8 4 2 7 1 6
```

### Divide

```text
5 3 8 4 2 7 1 6
        ↓
5 3 8 4       2 7 1 6
        ↓
5 3   8 4     2 7   1 6
        ↓
5  3  8  4    2  7  1  6
```

### Merge

```text
5 + 3 → 3 5
8 + 4 → 4 8
2 + 7 → 2 7
1 + 6 → 1 6
```

Then:

```text
3 5 + 4 8 → 3 4 5 8
2 7 + 1 6 → 1 2 6 7
```

Final merge:

```text
3 4 5 8 + 1 2 6 7
```

Result:

```text
1 2 3 4 5 6 7 8
```

---

## Algorithm

```text
MergeSort(A, left, right)

if left < right
    mid = left + (right-left)/2

    MergeSort(A, left, mid)
    MergeSort(A, mid+1, right)

    Merge(A, left, mid, right)
```

---

## C Program

```c
#include <stdio.h>

void merge(int arr[], int left, int mid, int right)
{
    int i = left;
    int j = mid + 1;
    int k = 0;

    int temp[right - left + 1];

    while (i <= mid && j <= right)
    {
        if (arr[i] <= arr[j])
        {
            temp[k] = arr[i];
            i++;
        }
        else
        {
            temp[k] = arr[j];
            j++;
        }

        k++;
    }

    while (i <= mid)
    {
        temp[k] = arr[i];
        i++;
        k++;
    }

    while (j <= right)
    {
        temp[k] = arr[j];
        j++;
        k++;
    }

    for (i = left, k = 0; i <= right; i++, k++)
        arr[i] = temp[k];
}

void mergeSort(int arr[], int left, int right)
{
    if (left < right)
    {
        int mid = left + (right - left) / 2;

        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);

        merge(arr, left, mid, right);
    }
}

int main()
{
    int arr[] = {5, 3, 8, 4, 2, 7, 1, 6};
    int n = sizeof(arr) / sizeof(arr[0]);

    mergeSort(arr, 0, n - 1);

    printf("Sorted array: ");

    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);

    return 0;
}
```

---

## Program Explanation

### Base condition

```c
if (left < right)
```

Stops recursion when the subarray contains one element.

### Middle index

```c
int mid = left + (right - left) / 2;
```

Divides the array into two halves.

### Recursive calls

```c
mergeSort(arr, left, mid);
mergeSort(arr, mid + 1, right);
```

Sort the left and right halves.

### Merge

```c
merge(arr, left, mid, right);
```

Combines two sorted halves.

---

## Time Complexity

Merge Sort follows the recurrence:

```text
T(n) = 2T(n/2) + O(n)
```

Therefore:

```text
T(n) = O(n log n)
```

| Case | Complexity |
|---|---:|
| Best Case | `O(n log n)` |
| Average Case | `O(n log n)` |
| Worst Case | `O(n log n)` |
| Auxiliary Space | `O(n)` |

### Properties

| Property | Value |
|---|---|
| Stable | Yes |
| In-place | No, standard array implementation |
| Extra Space | `O(n)` |
| Type | Divide and Conquer |

---

# 5. Quick Sort

## Definition

**Quick Sort** is a Divide and Conquer sorting algorithm.

It selects a **pivot**, partitions the array around that pivot, and recursively sorts the left and right parts.

Conceptually:

```text
Smaller elements | Pivot | Larger elements
```

---

## Important Terms

### Pivot

The element selected as the reference element.

### Partition

The process of rearranging elements so that elements on one side belong before the pivot and elements on the other side belong after it.

---

## Real-Life Example

Suppose students have marks:

```text
30 40 50 60 70 80
```

Choose `50` as a reference:

```text
30 40 | 50 | 60 70 80
```

Now sort the left and right groups independently.

---

## Example

Input:

```text
5 3 8 4 2
```

Using the last element as pivot:

```text
Pivot = 2
```

After partitioning:

```text
2 | 3 8 4 5
```

Now sort the right side.

Choose `5` as pivot:

```text
3 4 | 5 | 8
```

The left side:

```text
3 4
```

is already sorted.

Final result:

```text
2 3 4 5 8
```

---

## Algorithm

```text
QuickSort(A, low, high)

if low < high

    pivotIndex = Partition(A, low, high)

    QuickSort(A, low, pivotIndex-1)

    QuickSort(A, pivotIndex+1, high)
```

---

## Lomuto Partition

```text
Partition(A, low, high)

pivot = A[high]
i = low - 1

for j = low to high-1

    if A[j] <= pivot
        i++
        swap A[i], A[j]

swap A[i+1], A[high]

return i+1
```

---

## C Program

```c
#include <stdio.h>

void swap(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

int partition(int arr[], int low, int high)
{
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j < high; j++)
    {
        if (arr[j] <= pivot)
        {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }

    swap(&arr[i + 1], &arr[high]);

    return i + 1;
}

void quickSort(int arr[], int low, int high)
{
    if (low < high)
    {
        int pivotIndex = partition(arr, low, high);

        quickSort(arr, low, pivotIndex - 1);
        quickSort(arr, pivotIndex + 1, high);
    }
}

int main()
{
    int arr[] = {5, 3, 8, 4, 2};
    int n = sizeof(arr) / sizeof(arr[0]);

    quickSort(arr, 0, n - 1);

    printf("Sorted array: ");

    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);

    return 0;
}
```

---

## Program Explanation

### Pivot

```c
int pivot = arr[high];
```

The last element is selected as the pivot.

This implementation uses the **Lomuto partition scheme**.

### `i`

```c
int i = low - 1;
```

Maintains the boundary of elements that belong on the smaller/equal side.

### `j`

```c
for (int j = low; j < high; j++)
```

Scans the array.

### Comparison

```c
if (arr[j] <= pivot)
```

Moves an element to the left partition.

### Final pivot placement

```c
swap(&arr[i + 1], &arr[high]);
```

Places the pivot in its final position.

### Recursive calls

```c
quickSort(arr, low, pivotIndex - 1);
quickSort(arr, pivotIndex + 1, high);
```

Sort the two partitions.

---

## Time Complexity

### Best Case

Pivot divides the array approximately equally:

```text
n
├── n/2
└── n/2
```

Therefore:

```text
O(n log n)
```

### Average Case

With reasonably balanced partitions:

```text
O(n log n)
```

### Worst Case

If the pivot repeatedly becomes the smallest or largest element:

```text
n
|
n-1
|
n-2
|
n-3
...
```

Therefore:

```text
O(n²)
```

### Complexity Table

| Case | Complexity |
|---|---:|
| Best Case | `O(n log n)` |
| Average Case | `O(n log n)` |
| Worst Case | `O(n²)` |
| Average Auxiliary Space | `O(log n)` |
| Worst Auxiliary Space | `O(n)` |

### Properties

| Property | Value |
|---|---|
| Stable | No, standard implementation |
| In-place | Yes, apart from recursion stack |
| Type | Divide and Conquer |
| Pivot | Required |

---

# 6. Comparison of All Four

| Algorithm | Best | Average | Worst | Extra Space | Stable | In-place |
|---|---:|---:|---:|---:|---|---|
| Bubble Sort | `O(n)`* | `O(n²)` | `O(n²)` | `O(1)` | Yes | Yes |
| Insertion Sort | `O(n)` | `O(n²)` | `O(n²)` | `O(1)` | Yes | Yes |
| Merge Sort | `O(n log n)` | `O(n log n)` | `O(n log n)` | `O(n)` | Yes | No** |
| Quick Sort | `O(n log n)` | `O(n log n)` | `O(n²)` | `O(log n)` average | No | Yes |

`*` Bubble Sort best case is `O(n)` when the optimized `swapped` flag is used.

`**` Standard array-based Merge Sort uses an auxiliary array.

---

# 7. When Should We Use Which Algorithm?

| Situation | Suitable Algorithm |
|---|---|
| Learning basic sorting | Bubble Sort |
| Small or nearly sorted data | Insertion Sort |
| Guaranteed `O(n log n)` | Merge Sort |
| Fast average-case, low extra array memory | Quick Sort |
| Stability required | Merge / Insertion / Bubble |
| Very large data where quadratic algorithms are unsuitable | Merge / Quick |

---

# 8. Why Is `O(n log n)` Better Than `O(n²)`?

Suppose:

```text
n = 1000
```

For `O(n²)`:

```text
1000² = 1,000,000
```

For approximately `O(n log₂n)`:

```text
1000 × log₂(1000)
≈ 1000 × 10
≈ 10,000
```

Therefore, `O(n log n)` algorithms generally scale much better for large datasets.

---

# 9. Important Exam Questions

## Short Questions

1. What is sorting?
2. Define Bubble Sort.
3. Define Insertion Sort.
4. Define Merge Sort.
5. Define Quick Sort.
6. What is a stable sorting algorithm?
7. What is an in-place sorting algorithm?
8. What is a pivot?
9. What is partitioning?
10. What is Divide and Conquer?

## Complexity Questions

### Q1. What is the best-case complexity of Bubble Sort?

```text
O(n)
```

when the optimized `swapped` flag is used.

### Q2. What is the worst-case complexity of Bubble Sort?

```text
O(n²)
```

### Q3. What is the best-case complexity of Insertion Sort?

```text
O(n)
```

### Q4. What is the worst-case complexity of Insertion Sort?

```text
O(n²)
```

### Q5. What is the complexity of Merge Sort?

```text
O(n log n)
```

for best, average, and worst cases.

### Q6. What is the worst-case complexity of Quick Sort?

```text
O(n²)
```

### Q7. Which of these has guaranteed `O(n log n)` time?

```text
Merge Sort
```

---

# 10. Important Interview Questions

### Q1. Which sorting algorithm is suitable for nearly sorted data?

**Insertion Sort** is generally very suitable because its best case is `O(n)`.

### Q2. Which of these algorithms are stable?

```text
Bubble Sort     → Yes
Insertion Sort  → Yes
Merge Sort      → Yes
Quick Sort      → No, standard implementation
```

### Q3. Which algorithms use Divide and Conquer?

```text
Merge Sort
Quick Sort
```

### Q4. Why can Quick Sort become `O(n²)`?

Poor pivot selection can create highly unbalanced partitions.

### Q5. Why does Merge Sort require extra memory?

The standard array implementation uses temporary storage while merging two sorted portions.

### Q6. Which is often faster in practice: Merge Sort or Quick Sort?

Quick Sort is often very fast in practice because of good cache behavior and low constant factors, but its worst case is `O(n²)`. Merge Sort provides a guaranteed `O(n log n)` bound.

---

# 11. Quick Revision

```text
BUBBLE SORT
------------
Adjacent comparison + swapping

Best:     O(n)       [optimized]
Average:  O(n²)
Worst:    O(n²)
Space:    O(1)
Stable:   Yes
In-place: Yes


INSERTION SORT
--------------
Insert each element into sorted portion

Best:     O(n)
Average:  O(n²)
Worst:    O(n²)
Space:    O(1)
Stable:   Yes
In-place: Yes


MERGE SORT
----------
Divide → Sort → Merge

Best:     O(n log n)
Average:  O(n log n)
Worst:    O(n log n)
Space:    O(n)
Stable:   Yes
In-place: No [standard array implementation]


QUICK SORT
----------
Pivot → Partition → Recursively Sort

Best:     O(n log n)
Average:  O(n log n)
Worst:    O(n²)
Space:    O(log n) average recursion stack
Stable:   No [standard implementation]
In-place: Yes [apart from recursion stack]
```

---

# 12. Easy Way to Remember

```text
Bubble
   ↓
Adjacent comparison + Swap

Insertion
   ↓
Insert into sorted portion

Merge
   ↓
Divide + Sort + Merge

Quick
   ↓
Pivot + Partition
```

---

# 13. Final Takeaway

```text
Bubble Sort     → O(n²) average/worst
Insertion Sort  → O(n²) average/worst
Merge Sort      → O(n log n) guaranteed
Quick Sort      → O(n log n) average
                  O(n²) worst
```

The four core ideas to remember:

- **Bubble Sort** → adjacent comparison and swapping.
- **Insertion Sort** → insert an element into the sorted portion.
- **Merge Sort** → divide, sort, and merge.
- **Quick Sort** → choose a pivot and partition.
