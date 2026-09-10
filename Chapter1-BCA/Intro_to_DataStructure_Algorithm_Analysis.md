**Introduction**

**The core need for data structures in C stems from the requirement to organize, store, and manipulate data efficiently within computer memory**

Because C is a low-level programming language that interfaces directly with system hardware, 
it does not have built-in automated memory management or complex, pre-packaged collections like modern high-level languages. 
As a result, data structures are absolutely essential in C to write performant, organized, and scalable code.

**Need of Data Structure**

1. Memory Efficiency & Dynamic Allocation
  - In C, standard primitive variables and static arrays require fixed amounts of memory decided at compile time.
  - Data structures help bypass this limitation:
      - Dynamic Sizing:
      Using data structures like Linked Lists, you can allocate memory at runtime using pointers and structures.
      Data structures that utilize dynamic memory allocation (e.g., heaps or linked lists) allow you to allocate and reallocate    memory within the life of the program.
      - Preventing Wastage: Instead of guessing a large array size and leaving memory unused, data structures grow and shrink as needed
2. Time Efficiency (Faster Operations) Different data structures are optimized for different operations, reducing the execution time and CPU cycles required
   - Quick Access: An Array provides instantaneous data retrieval if you know the index.
   - Hierarchical Fast Search: A Binary Search Tree allows you to search through millions of data points rapidly compared to      scanning a sequential file one item at a time.

3. Representing Complex, Real-World Relationships Simple data types (like int, float, or char) can only hold single values.      Data structures allow programmers to model real-world concepts by combining diverse types.
   - Grouped Data: Using C structs, you can group a student's name, ID, and marks into a single unit.
   - Complex Data Modeling: Networks, maps, and hierarchies cannot be expressed in basic variables. They require non-linear       data structures like Trees (for folder directories) and Graphs (for social networks or maps).

6. Code Reusability and Maintainability
   - Once a specific data structure (like a Stack or Queue) is written and debugged in C,
   - it can be repurposed across multiple application modules.
   - Data structures can be used in multiple programs and applications, reducing the need for redundant code.
   - This makes complex code clean, standardized, and much easier to maintain over time

--- 

**Data and Information**

In computing and C programming, data and information represent two distinct stages of processing, where data is the raw input and information is the processed output

Data: The Raw Material Data refers to raw, unorganized, and unprocessed facts, figures, or symbols.
- Characteristics: 
It has no inherent meaning on its own and cannot be used for decision-making.
- C Programming Context: 
In C, data is represented by raw values stored in variables, such as an integer 23, a float 98.6, or a character array "XYZ".

Information: The Meaningful Output Information is data that has been processed, structured, organized, or contextualized to make it meaningful and useful.
- Characteristics: 
It carries clear meaning, provides context, and helps in making decisions.
- C Programming Context: 
In C, when you process raw variables (data) through logic, conditions, or mathematical formulas, the resulting output printed on the screen is information (e.g., printing "The average student score is 85%").

-----

**Data Types**

In C programming, data types define the type and size of data that a variable can hold, as well as the operations that can be performed on it. Because C is a strongly typed language, every variable must be declared with a specific data type before it can be used, allowing the compiler to allocate the exact amount of memory needed.

1. Primitive (Basic) Data Types These are built-in, fundamental data types provided natively by C.
   - int: Used to store integers (whole numbers).
   - char: Used to store single characters or ASCII values.
   - float: Used to store single-precision floating-point numbers (decimals).
   - double: Used to store double-precision floating-point numbers (larger decimals).

2. Derived Data Types These types are formed by combining or deriving from the primitive data types.
   - Arrays: A collection of homogeneous (same type) elements stored in sequential memory.
   - Pointers: Special variables that store the memory address of another variable.
   - Functions: Blocks of code that accept arguments and return a specific type of value.

3. User-Defined Data Types These allow programmers to create customized data types to model real-world concepts.
   - struct (Structure): Groups variables of different data types under a single name.
   - union: Similar to a struct, but all members share the same memory location to save space.
   - enum (Enumeration): Assigns names to integer constants to make code more readable.

4. Void Data Type (void)void:
   Represents the absence of a value.
   It is commonly used to specify that a function does not return any data or to create generic pointers (void*).

----

**Data Object**

In computer science and C programming, a data object is a region of storage (memory) that holds a value or a collection of values.
While a data type is an abstract blueprint or definition, a data object is the actual concrete instance created in memory based on that blueprint.

Key Characteristics of a Data Object

Every data object in C has four core properties:
- Memory Address: The physical location in the RAM where the object resides.
- Size: The amount of space it occupies, which is determined by its data type (e.g., 4 bytes for an int).
- Value: The actual data or contents currently stored inside that memory region.
- Lifetime: The duration during the program's execution for which that memory remains allocated.

**Data Object vs. Variable**

People often use these terms interchangeably, but there is a distinct technical difference:
- Variable: A variable is a named identifier that refers to a data object. It is a label we use in our code to easily access a memory location.
- Data Object: This is the underlying memory itself. Not all data objects have names. 
For example, when you dynamically allocate memory using malloc(), you create a data object that does not have a variable name; it can only be accessed via a pointer.

**Types of Data Objects in C**

Data objects can be categorized based on their complexity and how they are created:

- Primitive Data Objects: A single, simple region of memory holding one fundamental value (e.g., a single int or char).
- Structured (Composite) Data Objects: An aggregate region of memory holding multiple values grouped together, such as an
Array or a Structure (struct).
- Anonymous Data Objects: Memory spaces created at runtime using dynamic allocation (malloc, calloc). 
They don't have a source-code name and exist purely as objects in the heap memory.

**Abstract Data Types**

In computer science, an Abstract Data Type (ADT) is a mathematical model for data types that defines a data type solely by its behavior and operations, without specifying how it is implemented in code.Think of an ADT as a blueprint or user manual. It tells you exactly what the data structure does, but hides the details of how it does it.

The Two Core Components of an ADT
Every ADT is defined by two things:
- The Data: What kind of values or elements the type can hold.
- The Operations: The actions or functions you can perform on that data (e.g., insert, delete, search). 
- The Real-World Analogy: A SmartphoneWhen you use a smartphone, you know that pressing the volume button will increase the sound, and tapping the camera icon will take a photo. You do not need to know the circuit layout, the semiconductor engineering, or the underlying OS code to use it. The buttons are the ADT interface, and the internal electronics are the hidden implementation.

Common Examples of ADTs Here are the standard ADTs you will encounter in C programming, along with their defined operations:
- List ADT: A collection of elements in sequential order.
- Operations: insert(), delete(), get(), size().
- Stack ADT: A Last-In, First-Out (LIFO) collection.
- Operations: push() (add to top), pop() (remove from top), peek() (look at top element).
- Queue ADT: A First-In, First-Out (FIFO) collection.Operations: enqueue() (add to back), dequeue() (remove from front).
- Graph ADT: A collection of nodes (vertices) connected by lines (edges).Operations: addVertex(), addEdge(), getNeighbors().

**Why do we need ADTs? (Data Abstraction)**
In C, implementing an ADT involves Encapsulation. 
By creating custom header files (.h) for the interface and source files (.c) for the logic, 
you achieve:

- Code Flexibility: You can completely change the internal implementation (e.g., swapping an Array out for a Linked List) without changing a single line of code in the main application that uses it.

- Modular Coding: Different developers can work on the implementation and the application simultaneously, as long as they agree on the ADT specification.

-----

In computer science and C programming, a data structure is a specialised way of organizing, storing, and managing data in a computer's memory so that it can be accessed and modified efficiently.While an Abstract Data Type (ADT) tells you what operations can be performed, a data structure is the actual, concrete code implementation of that model.

**Classification of Data Structures**

Data structures are broadly divided into two main categories based on how the data elements are arranged in memory:

1. Linear Data Structures
   - In these structures, data elements are arranged sequentially or linearly
   - Where each element is attached to its previous and next adjacent elements.
   - Arrays: A collection of elements stored in contiguous (continuous) memory locations.
   - It allows fast, direct access via indexes.
   - Linked Lists: Elements (called nodes) are scattered in memory and connected using pointers.
   - They can grow or shrink dynamically at runtime.
   - Stacks: A structure following the LIFO (Last-In, First-Out) principle.
   - Elements are added and removed from the same end (e.g., undo operations, function call stacks).
   - Queues: A structure following the FIFO (First-In, First-Out) principle.
   - Elements are added at the back and removed from the front (e.g., CPU task scheduling, print spools).
   
2. Non-Linear Data Structures, In these structures, data elements are not arranged sequentially.
   - An element can be connected to multiple other elements, forming a hierarchy or a network.
   - Trees: A hierarchical structure consisting of nodes connected by edges, starting from a single "root" node (e.g., file directories, XML parsing).
   - Graphs: A network of nodes (vertices) connected by paths (edges).
   - There is no strict parent-child relationship (e.g., social networks, Google Maps routing).

Common Operations Performed on Data Structures Regardless of which data structure you choose, you will typically implement the following fundamental operations in C:

- Traversal: Accessing each element in the data structure exactly once to process or display it.
- Insertion: Adding a new data element at a specified position.
- Deletion: Removing an existing data element from the structure.
- Searching: Finding the location of a specific element within the structure.
- Sorting: Arranging the elements in a specific logical order (ascending or descending).
- Merging: Combining two different data structures of the same type into a single one.

------------

**Algorithm Analysis**

algorithms aren't just rated on whether they work, but on how well they scale as data grows (n -> infinity).

- Time Complexity: Total execution time required by an algorithm as a function of input size n.
- Space Complexity: Total memory needed by the algorithm,
  - consisting of: Fixed Space: Space for constants, simple variables, and program code.
  - Variable Space: Space required by dynamically allocated memory and call stack recursion.
 
-------------

## 1. Case Analysis

An algorithm's execution time depends heavily on the nature and order of the input data. We analyze performance using three standard cases:

* **Best Case ($\Omega$):** The scenario where the algorithm executes in the minimum number of steps. Represents the absolute lower bound of execution time.
* **Worst Case ($O$):** The scenario where the algorithm executes in the maximum number of steps. Represents the upper bound guarantee—the algorithm will never perform worse than this.
* **Average Case ($\Theta$):** The expected execution time averaged across all possible valid inputs of size $n$.

### Example: Linear Search on an Array of Size $n$

```c
int linearSearch(int arr[], int n, int target) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == target) {
            return i; // Target found
        }
    }
    return -1; // Target not found
}

```
- Best Case: The target element is at index 0. - Requires 1 comparison $\to O(1)$.
- Worst Case: The target element is at the last index (n-1) or not present at all. Requires $n$ comparisons $\to O(n)$.
- Average Case: The target element is randomly located somewhere in the array.
- On average, requires $\frac{n+1}{2}$ comparisons $\to O(n)$.

------

**Asymptotic Notation**

# Asymptotic Notations: History, Formulas & Graph Analysis

Asymptotic notations are mathematical tools used to describe the efficiency and scalability of algorithms as the input size ($n$) grows toward infinity ($n \to \infty$).

---

## 1. Big-O Notation ($O$)

### History of Big-O

* **Origins in Mathematics:** Big-O notation was invented by the German mathematician **Paul Bachmann** in 1894 in his book *Analytische Zahlentheorie* (Number Theory). The letter **O** stands for **"Order of"** (originally *Ordnung* in German), indicating the growth rate of a mathematical function.
  
* **Adoption in Computer Science:** In 1976, **Donald Knuth** (author of *The Art of Computer Programming*) popularized Big-O in computer science. He introduced it to standardize how programmers compare the efficiency of different algorithms, regardless of processor speed or hardware differences.

### What It Is Used For
Big-O is used to define the **Worst-Case Scenario** (Upper Bound) of an algorithm. It guarantees that an algorithm will **never take more time** than the specified limit.

### Mathematical Formula
$$f(n) = O(g(n)) \iff f(n) \le c \cdot g(n) \quad \forall n \ge n_0$$

### Formula Term Breakdown
* **$f(n)$**: The actual execution time function of your code (e.g., $f(n) = 3n^2 + 5n + 10$).
* **$g(n)$**: The simplified benchmark function (e.g., $g(n) = n^2$).
* **$c$**: A positive constant ($c > 0$) used to scale $g(n)$ so it covers $f(n)$. It absorbs hardware variances (like clock speeds).
* **$n_0$**: The minimum input threshold ($n_0 \ge 1$). Beyond this point ($n \ge n_0$), the upper bound inequality holds true forever.

-----------------------------------------

---

## 2. Big-Omega Notation ($\Omega$)

## History of Big-Omega
* **Origins & Adoption:** In the early 1970s, computer scientists frequently misused Big-O to represent both lower bounds and exact bounds.
* **Formalization:** To fix this lack of mathematical rigor, **Donald Knuth** published a seminal paper in 1976 introducing the Greek letter **$\Omega$ (Omega)** to explicitly denote lower bounds in computer science.


## What It Is Used For
Big-Omega is used to define the **Best-Case Scenario** (Lower Bound) of an algorithm. It guarantees that an algorithm will **take at least this much time** (or memory) in the best possible conditions.


## Mathematical Formula
$$f(n) = \Omega(g(n)) \iff f(n) \ge c \cdot g(n) \quad \forall n \ge n_0$$


## Formula Term Breakdown
* **$f(n)$**: The actual step-count function of your algorithm.
* **$g(n)$**: The simplified lower-bound target function.
* **$c$**: A positive constant ($c > 0$) chosen to scale $g(n)$ downwards beneath $f(n)$.
* **$n_0$**: The threshold point after which $f(n)$ never falls below $c \cdot g(n)$.

---

# 3. Big-Theta Notation ($\Theta$)

## History of Big-Theta
* **Origins & Adoption:** Along with Big-Omega, **Donald Knuth** introduced the Greek letter **$\Theta$ (Theta)** in his 1976 paper.
* **Purpose:** It was designed to represent a **Tight Bound**—a condition where an algorithm's upper bound and lower bound match the same rate of growth.

---

## What It Is Used For
Big-Theta represents the **Exact / Average-Case Complexity**. It is used when an algorithm's performance is tightly bounded from both above and below by the exact same order of growth (e.g., $n^2$).

---

## Mathematical Formula
$$f(n) = \Theta(g(n)) \iff c_1 \cdot g(n) \le f(n) \le c_2 \cdot g(n) \quad \forall n \ge n_0$$

---

## Formula Term Breakdown
* **$f(n)$**: The actual execution function of the algorithm.
* **$g(n)$**: The reference growth rate function.
* **$c_1$**: Constant multiplier for the lower bound floor ($c_1 > 0$).
* **$c_2$**: Constant multiplier for the upper bound ceiling ($c_2 > 0$).
* **$n_0$**: The input threshold after which $f(n)$ stays strictly trapped between $c_1 \cdot g(n)$ and $c_2 \cdot g(n)$.

---




