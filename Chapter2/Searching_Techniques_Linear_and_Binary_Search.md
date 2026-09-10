# Searching Techniques in C

## Linear Search and Binary Search

Searching means finding a particular element, called the **key** or **target**, from a collection of data.

For example:

```text
Array:
10  25  30  45  60

Search for:
45
```

If `45` is present, we need to find its position.

The two basic searching techniques covered in this file are:

1. **Linear Search**
2. **Binary Search**

---

# 1. Important Searching Terminology

## Key / Target

The value that we want to search for.

Example:

```text
Array: 10 20 30 40 50
Key:   30
```

Here, `30` is the search key.

## Index

The position of an element in an array.

In C, array indexing starts from `0`.

```text
Value:  10  20  30  40  50
Index:   0   1   2   3   4
```

Therefore, the index of `30` is `2`.

---

# 2. Linear Search

## 2.1 Definition

**Linear Search** is a searching technique in which each element is checked one by one from the beginning of the array until:

- the required element is found, or
- the end of the array is reached.

It is also called **Sequential Search**.

---

## 2.2 Basic Idea

Suppose:

```text
Array:

10  25  30  45  60
```

Search for:

```text
45
```

Linear Search checks:

```text
10 → 25 → 30 → 45
```

When `45` is found, the search stops.

---

## 2.3 Real-Life Example

Suppose you have a list of student roll numbers:

```text
15  23  8  41  19
```

You want to find roll number `41`.

You start from the first student:

```text
15 → Not found
23 → Not found
8  → Not found
41 → Found
```

This is exactly how Linear Search works.

---

## 2.4 Step-by-Step Dry Run

Consider:

```text
Array = {10, 25, 30, 45, 60}
Key = 45
```

### Step 1

```text
i = 0

arr[0] = 10

10 == 45 ? No
```

Move to the next element.

### Step 2

```text
i = 1

arr[1] = 25

25 == 45 ? No
```

### Step 3

```text
i = 2

arr[2] = 30

30 == 45 ? No
```

### Step 4

```text
i = 3

arr[3] = 45

45 == 45 ? Yes
```

Element found.

```text
Index = 3
Position = 4
```

Remember:

```text
Index    → starts from 0
Position → starts from 1
```

---

## 2.5 Example When Element Is Not Present

Array:

```text
10  25  30  45  60
```

Search:

```text
50
```

Comparisons:

```text
10 == 50 → No
25 == 50 → No
30 == 50 → No
45 == 50 → No
60 == 50 → No
```

End of array is reached.

Therefore:

```text
Element not found
```

---

# 3. Linear Search Algorithm

```text
LinearSearch(A, n, key)

for i = 0 to n-1

    if A[i] == key

        return i

return -1
```

Here:

- `A` → array
- `n` → number of elements
- `key` → element to search
- `i` → current index
- `-1` → indicates that the element was not found

---

# 4. Linear Search C Program

```c
#include <stdio.h>

int linearSearch(int arr[], int n, int key)
{
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == key)
        {
            return i;
        }
    }

    return -1;
}

int main()
{
    int arr[] = {10, 25, 30, 45, 60};
    int n = sizeof(arr) / sizeof(arr[0]);

    int key = 45;

    int result = linearSearch(arr, n, key);

    if (result != -1)
    {
        printf("Element found at index %d\n", result);
    }
    else
    {
        printf("Element not found\n");
    }

    return 0;
}
```

---

# 5. Linear Search Program Explanation

## Array

```c
int arr[] = {10, 25, 30, 45, 60};
```

Creates an integer array.

The indexes are:

```text
Value:  10  25  30  45  60
Index:   0   1   2   3   4
```

## Calculate Array Size

```c
int n = sizeof(arr) / sizeof(arr[0]);
```

Suppose an integer occupies 4 bytes.

```text
sizeof(arr)    = 5 × 4 = 20 bytes
sizeof(arr[0]) = 4 bytes

n = 20 / 4
n = 5
```

So the array contains 5 elements.

## Search Key

```c
int key = 45;
```

We want to search for `45`.

## Function Call

```c
int result = linearSearch(arr, n, key);
```

The function searches the array.

## Loop

```c
for (int i = 0; i < n; i++)
```

Starts from index `0` and checks every element.

## Comparison

```c
if (arr[i] == key)
```

Checks whether the current element is equal to the key.

## Return Index

```c
return i;
```

If the element is found, its index is returned.

## Return `-1`

```c
return -1;
```

If the loop finishes without finding the key, `-1` indicates that the element does not exist.

---

# 6. Linear Search Complexity

The number of comparisons depends on where the element is located.

## Best Case

The element is at the first position.

Example:

```text
Array:
45 10 20 30 40

Key = 45
```

Only one comparison is required.

Therefore:

```text
Best Case = O(1)
```

## Average Case

The element is somewhere in the middle on average.

Approximately:

```text
n / 2
```

comparisons are required.

Therefore:

```text
Average Case = O(n)
```

## Worst Case

Two situations can produce the worst case:

1. The element is the last element.
2. The element does not exist.

Example:

```text
10 20 30 40 50

Search = 100
```

All elements must be checked.

Therefore:

```text
Worst Case = O(n)
```

## Space Complexity

Linear Search requires only a few variables:

```text
Space = O(1)
```

---

## Linear Search Complexity Table

| Case | Time Complexity |
|---|---:|
| Best Case | `O(1)` |
| Average Case | `O(n)` |
| Worst Case | `O(n)` |
| Space | `O(1)` |

### Properties

| Property | Linear Search |
|---|---|
| Requires sorted array? | No |
| Works on unsorted array? | Yes |
| Best Case | `O(1)` |
| Worst Case | `O(n)` |
| Extra Space | `O(1)` |
| Technique | Sequential checking |

---

# 7. Binary Search

## 7.1 Definition

**Binary Search** is a searching technique that repeatedly divides the search range into two halves.

Instead of checking every element, it compares the key with the middle element and eliminates half of the remaining search space.

---

# 8. Important Requirement of Binary Search

## The array must be sorted.

For example:

```text
10 20 30 40 50 60 70
```

Binary Search can be applied.

But:

```text
40 10 70 20 50 30 60
```

is not sorted, so standard Binary Search cannot be directly applied.

If the data is unsorted, you must first sort it or use another searching technique such as Linear Search.

---

# 9. Basic Idea of Binary Search

Consider:

```text
10 20 30 40 50 60 70
```

Search for:

```text
60
```

Find the middle element:

```text
10 20 30 40 50 60 70
         ↑
        40
```

Compare:

```text
60 > 40
```

Therefore, `60` cannot be in the left half.

Discard:

```text
10 20 30
```

Search only:

```text
50 60 70
```

Find the middle:

```text
50 60 70
   ↑
  60
```

Found.

---

# 10. Real-Life Example

Imagine searching for a word in a dictionary.

You normally do not start from the first word and check every word.

Instead, you open the dictionary near the middle.

Suppose you are looking for:

```text
"Tree"
```

If the current page contains words beginning with `M`, then:

```text
Tree > M
```

So you know the required word must be in the later half.

You discard the earlier half and repeat the process.

This is the basic idea of Binary Search.

---

# 11. Binary Search Step-by-Step Dry Run

Consider:

```text
Array:

10  20  30  40  50  60  70

Index:

0   1   2   3   4   5   6
```

Search:

```text
Key = 60
```

Initially:

```text
low = 0
high = 6
```

Calculate:

```text
mid = low + (high - low) / 2
mid = 0 + (6 - 0) / 2
mid = 3
```

Therefore:

```text
arr[mid] = arr[3] = 40
```

Compare:

```text
60 > 40
```

Therefore search the right half.

Update:

```text
low = mid + 1
low = 4
```

Now:

```text
low = 4
high = 6
```

Calculate:

```text
mid = 4 + (6 - 4) / 2
mid = 5
```

Therefore:

```text
arr[5] = 60
```

Compare:

```text
60 == 60
```

Element found.

```text
Index = 5
Position = 6
```

---

# 12. Binary Search Dry Run: Element Not Found

Array:

```text
10 20 30 40 50 60 70
```

Search:

```text
65
```

### Step 1

```text
low = 0
high = 6
mid = 3

arr[3] = 40
```

Since:

```text
65 > 40
```

Search right side.

```text
low = 4
```

### Step 2

```text
low = 4
high = 6
mid = 5

arr[5] = 60
```

Since:

```text
65 > 60
```

Search right side.

```text
low = 6
```

### Step 3

```text
low = 6
high = 6
mid = 6

arr[6] = 70
```

Since:

```text
65 < 70
```

Search left side.

```text
high = mid - 1
high = 5
```

Now:

```text
low = 6
high = 5
```

Since:

```text
low > high
```

the search stops.

Therefore:

```text
65 not found
```

---

# 13. Binary Search Algorithm

```text
BinarySearch(A, n, key)

low = 0
high = n - 1

while low <= high

    mid = low + (high-low)/2

    if A[mid] == key
        return mid

    else if key < A[mid]
        high = mid - 1

    else
        low = mid + 1

return -1
```

---

# 14. Why Do We Use `low + (high-low)/2`?

You may commonly see:

```c
mid = (low + high) / 2;
```

It works for normal array sizes, but:

```text
low + high
```

can potentially overflow for very large integer values.

Therefore, a safer expression is:

```c
mid = low + (high - low) / 2;
```

Both calculate the same middle index when overflow is not an issue.

---

# 15. Binary Search C Program

```c
#include <stdio.h>

int binarySearch(int arr[], int n, int key)
{
    int low = 0;
    int high = n - 1;

    while (low <= high)
    {
        int mid = low + (high - low) / 2;

        if (arr[mid] == key)
        {
            return mid;
        }
        else if (key < arr[mid])
        {
            high = mid - 1;
        }
        else
        {
            low = mid + 1;
        }
    }

    return -1;
}

int main()
{
    int arr[] = {10, 20, 30, 40, 50, 60, 70};
    int n = sizeof(arr) / sizeof(arr[0]);

    int key = 60;

    int result = binarySearch(arr, n, key);

    if (result != -1)
    {
        printf("Element found at index %d\n", result);
    }
    else
    {
        printf("Element not found\n");
    }

    return 0;
}
```

---

# 16. Binary Search Program Explanation

## `low`

```c
int low = 0;
```

Represents the first index of the current search range.

Initially, the search starts from index `0`.

## `high`

```c
int high = n - 1;
```

Represents the last index of the current search range.

For 7 elements:

```text
high = 7 - 1
high = 6
```

## Calculate Middle

```c
int mid = low + (high - low) / 2;
```

Finds the middle index.

## Case 1: Element Found

```c
if (arr[mid] == key)
```

If the middle element is equal to the key, return the index.

## Case 2: Key Is Smaller

```c
else if (key < arr[mid])
{
    high = mid - 1;
}
```

Because the array is sorted, if the key is smaller than the middle element, it must be on the left side.

So:

```text
Discard right half
```

## Case 3: Key Is Larger

```c
else
{
    low = mid + 1;
}
```

If the key is larger than the middle element, it must be on the right side.

So:

```text
Discard left half
```

## Search Ends

```c
return -1;
```

If:

```text
low > high
```

there is no remaining search range, so the element is not present.

---

# 17. Binary Search Complexity

## Best Case

The key is the middle element in the first comparison.

Example:

```text
10 20 30 40 50 60 70
         ↑
        key
```

Only one comparison is needed.

Therefore:

```text
Best Case = O(1)
```

## Average Case

The search space is divided approximately in half each time.

Therefore:

```text
Average Case = O(log n)
```

## Worst Case

Even in the worst case, Binary Search repeatedly halves the search space.

Therefore:

```text
Worst Case = O(log n)
```

## Space Complexity

The iterative implementation uses:

```text
low
high
mid
```

Only a constant amount of extra memory is required.

Therefore:

```text
Space = O(1)
```

---

# 18. Why Is Binary Search `O(log n)`?

Suppose there are:

```text
16 elements
```

After every comparison, approximately half of the elements are eliminated.

```text
16
 ↓
8
 ↓
4
 ↓
2
 ↓
1
```

Number of divisions:

```text
log₂(16) = 4
```

Therefore, Binary Search takes approximately logarithmic time.

In general:

```text
Number of comparisons ≈ log₂(n)
```

Hence:

```text
Time Complexity = O(log n)
```

---

# 19. Binary Search Complexity Table

| Case | Time Complexity |
|---|---:|
| Best Case | `O(1)` |
| Average Case | `O(log n)` |
| Worst Case | `O(log n)` |
| Space | `O(1)` for iterative implementation |

### Properties

| Property | Binary Search |
|---|---|
| Requires sorted array? | Yes |
| Works directly on unsorted array? | No |
| Best Case | `O(1)` |
| Average Case | `O(log n)` |
| Worst Case | `O(log n)` |
| Extra Space | `O(1)` iterative |
| Technique | Divide search space into halves |

---

# 20. Linear Search vs Binary Search

| Feature | Linear Search | Binary Search |
|---|---|---|
| Basic idea | Check one by one | Divide search range in half |
| Sorted array required? | No | Yes |
| Unsorted data | Works | Does not work directly |
| Best Case | `O(1)` | `O(1)` |
| Average Case | `O(n)` | `O(log n)` |
| Worst Case | `O(n)` | `O(log n)` |
| Space | `O(1)` | `O(1)` iterative |
| Simplicity | Very simple | Slightly more complex |
| Suitable for | Small/unsorted data | Large sorted data |

---

# 21. Example: Why Binary Search Is Faster

Consider an array containing:

```text
1,000,000 elements
```

### Linear Search

In the worst case, it may need to check:

```text
1,000,000 elements
```

Therefore:

```text
O(n)
```

### Binary Search

It repeatedly divides the search space by 2.

Approximately:

```text
log₂(1,000,000) ≈ 20
```

comparisons are needed in the worst case.

Therefore:

```text
O(log n)
```

This is why Binary Search can be dramatically faster for large **sorted** datasets.

---

# 22. When Should We Use Linear Search?

Use Linear Search when:

- The array is unsorted.
- The dataset is small.
- Simplicity is more important than search speed.
- The data is stored in a structure where binary search is not convenient.
- You only need to perform a small number of searches.

Example:

```text
Unsorted array:
40 10 70 20 50
```

Search:

```text
20
```

Linear Search can directly search this array.

---

# 23. When Should We Use Binary Search?

Use Binary Search when:

- The data is sorted.
- The dataset is large.
- Many search operations are performed.
- Fast searching is required.

Example:

```text
10 20 30 40 50 60 70
```

Search:

```text
60
```

Binary Search can eliminate half of the remaining elements after each comparison.

---

# 24. Important Exam Questions

## Short Answer Questions

1. What is searching?
2. Define Linear Search.
3. Define Binary Search.
4. What is a search key?
5. What is the difference between index and position?
6. Is a sorted array required for Linear Search?
7. Is a sorted array required for Binary Search?
8. What is the purpose of `low` and `high` in Binary Search?
9. What is the purpose of `mid`?
10. Why is Binary Search called a logarithmic search?

## Complexity Questions

### Q1. What is the best-case complexity of Linear Search?

```text
O(1)
```

### Q2. What is the worst-case complexity of Linear Search?

```text
O(n)
```

### Q3. What is the best-case complexity of Binary Search?

```text
O(1)
```

### Q4. What are the average and worst-case complexities of Binary Search?

```text
Average = O(log n)
Worst   = O(log n)
```

### Q5. Which searching technique can work on an unsorted array?

```text
Linear Search
```

### Q6. What is the most important prerequisite for standard Binary Search?

```text
The array must be sorted.
```

---

# 25. Quick Revision

```text
LINEAR SEARCH
-------------
Check elements one by one.

Example:
10 20 30 40 50
          ↑
        search

Best:     O(1)
Average:  O(n)
Worst:    O(n)
Space:    O(1)

Sorted array required?
NO


BINARY SEARCH
-------------
Repeatedly divide the search range into half.

Example:
10 20 30 40 50 60 70
         ↑
       middle

If key < middle:
    search left half

If key > middle:
    search right half

If key == middle:
    found

Best:     O(1)
Average:  O(log n)
Worst:    O(log n)
Space:    O(1) iterative

Sorted array required?
YES
```

---

# 26. Easy Way to Remember

```text
Linear Search
      ↓
One by one
      ↓
O(n)


Binary Search
      ↓
Middle element
      ↓
Discard half
      ↓
O(log n)
```

---

# 27. Final Comparison to Remember

```text
                 SEARCHING
                     |
             -----------------
             |               |
          LINEAR           BINARY
             |               |
        One by one       Divide by 2
             |               |
       Sorted? NO        Sorted? YES
             |               |
        Worst O(n)       Worst O(log n)
```

## Key Takeaway

**Linear Search:**

> Simple, works on unsorted data, but can take `O(n)` time.

**Binary Search:**

> Much faster for sorted data because it eliminates half of the search space at every step, giving `O(log n)` average/worst-case time.

