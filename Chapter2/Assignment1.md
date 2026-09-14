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
