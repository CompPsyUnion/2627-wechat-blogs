# Introduction to Time Complexity and Space Complexity

Hi, everyone! Today, we are going to learn about time complexity and space complexity.  

In computer science, time complexity and space complexity are important metrics for measuring algorithm efficiency. They help us understand the time and space resources required by an algorithm when processing inputs of different sizes.

## 1. What Are Time Complexity and Space Complexity?

**Time Complexity** Represents the growth trend of the time required to execute an algorithm as the input size changes. It tells us how fast or slow the algorithm runs.  

**Space Complexity** Represents the growth trend of the additional memory space required during algorithm execution as the input size changes. It tells us how much memory the algorithm occupies.

*Note:  
It is worth mentioning that an algorithm’s running time is not entirely determined by the input size; it is also related to the contents of the input. Therefore, time complexity is generally divided into:  

1. Worst-case time complexity  
2. Average-case time complexity  
3. Best-case time complexity*  
  
- In general, time complexity refers to the **worst-case time complexity** by default.

## 2. Why Do We Need Complexity?

**Evaluate Efficiency** Through complexity analysis, we can predict how an algorithm will perform when processing large amounts of data and avoid choosing inefficient algorithms.

**Optimize Resources** Understanding time and space consumption helps us design more reasonable programs under limited resources.

**Compare Algorithms** When different algorithms solve the same problem, complexity is an important basis for selecting the optimal algorithm.

## 3. How Do We Represent Time & Space Complexity?

### Big $O$ Notation

Q: The same piece of code takes 0.01 seconds to run on your computer but only 0.0001 seconds on a supercomputer. Can we say that its time complexity on the supercomputer is lower than on your computer?  

A: Of course not. The same piece of code should have the same complexity.

In real life, we often encounter situations like this. The so-called “growth trend of execution time as the data size increases” is a vague concept. To make complexity concrete and standardized, we introduce the widely used “**Big $O$ notation**” to uniformly describe the time complexity and space complexity of algorithms.

Examples: $O(n)$ ; $O(n^2)$ ; $O(logn)$ ; $O(1)$ ...  
*Here, “ $n$ ” represents the data size*

(The meanings and calculation methods will be explained in the next section.)

## 4. Calculating and Understanding Time Complexity and Space Complexity

### ***Core Idea: Focus on the Big and Ignore the Small***

- Identify the **determining factor** that affects complexity; everything else can be ignored.  
(For example, in the function $y = n^2 + n + 1$ , the determining factor is $n^2$ , so only $n^2$ needs to be considered when calculating the time complexity.)

---

### 1.Calculating Time Complexity

#### ① $O(1)$ —— Constant Order (Fastest)

- **Meaning**: No matter how large the amount of data $n$ is, the execution time remains constant and does not change as $n$ changes.
- **Simple Analogy**: Whether a dictionary has 100 pages or 10,000 pages, turning to page 1 takes only 1 second.
- **Code Example** (Python):

  ```python
  def get_first_element(arr):
      return arr[0]  
      # No matter how long the array is, only the first item is retrieved in one step
  ```

#### ② $O(\log n)$ —— Logarithmic Order (Extremely Fast)

- **Meaning**: With each loop, the amount of data to be processed is halved. As $n$ increases, the time increases very slowly.
- **Simple Analogy**: **Binary search**. To find a word in a thick dictionary, first open it in the middle. If the target is in the first half, tear away the second half; then open the middle of the first half again. Each time, half of the pages are eliminated.
- **Code Example**（Python）:

  ```python
  # Binary search
  def binary_search(arr, target):
      low, high = 0, len(arr) - 1
      while low <= high:
          mid = (low + high) // 2
          if arr[mid] == target:
              return mid
          elif arr[mid] < target:
              low = mid + 1
          else:
              high = mid - 1
      return -1
  ```

#### ③ $O(n \log n)$ —— Linearithmic Order (Relatively Fast)

- **Meaning**: Combines linear order and logarithmic order. Many efficient sorting algorithms, such as merge sort and quicksort, are at this level.
- **Simple Analogy**: Divide a large set of data into two halves, sort them separately, and then merge them.  
- **Code Example** (Python):

  ```python
  # Core idea of merge sort (divide and conquer)
  def merge_sort(arr):
      if len(arr) <= 1:
         return arr
      mid = len(arr) // 2
      left = merge_sort(arr[:mid])
      right = merge_sort(arr[mid:])
      return left + right  # Simplified illustration of the merging process
  ```

#### ④ $O(n)$ —— Linear Order (Moderate)

- **Meaning**: The running time is directly proportional to the amount of data $n$. If the data doubles, the time also doubles.
- **Simple Analogy**: Sequential search. Turn through the pages one by one from beginning to end until the word is found.
- **Code Example** (Python):

  ```python
  # Sequential search
  def sequential_search(arr, target):
      for i in range(len(arr)):
          if arr[i] == target:
              return i
      return -1
  ```

#### ⑤ $O(n^2)$ —— Quadratic Order (Relatively Slow)

- **Meaning**: Usually appears in two nested loops. If the amount of data doubles, the time becomes four times the original amount.
- **Simple Analogy**: Double traversal. Check the handshakes between every student in the class and every other student.
- **Code Example** (Python):

  ```python
  # Print a multiplication table or use a double loop
  for i in range(n):
      for j in range(n):
          print(i, j)
  ```

#### ⑥ $O(2^n)$ —— Exponential Order (Disastrously Slow)

- **Meaning**: As $n$ increases, the running time grows explosively and should generally be avoided as much as possible in algorithm design.
- **Simple Analogy**: Recursively calculating the Fibonacci sequence
- **Code Example** (Python):

  ```python
  # Recursively calculate the Fibonacci sequence (exponential repeated calculations)
    def fibonacci(n):
        if n <= 1:
           return n
        return fibonacci(n - 1) + fibonacci(n - 2)
  ```

---

### 2.Calculating Space Complexity

#### ① $O(1)$ —— Constant Order

- **Meaning**: The amount of additional memory space allocated by the algorithm is a fixed value and does not change with the input data $n$.
- **Code Example** (Python):

  ```python
  def sum_two(a, b):
    c = a + b  
    return c
    # Only the fixed variables a, b, and c are used, so the additional memory remains unchanged regardless of the input size
  ```

#### ② $O(n)$ —— Linear Order

- **Meaning**: The additionally allocated storage space is directly proportional to the amount of input data $n$.
- **Code Example** (Python):

  ```python
  def create_list(n):
    new_list = []
    for i in range(n):
        new_list.append(i)  # The list grows linearly as n increases
    return new_list
  ```

#### ③ $O(n^2)$ —— Quadratic Order

- **Meaning**: This usually requires creating a two-dimensional matrix or grid to store data. Memory consumption grows with the square of $n$ (for example, an $n \times n$ chessboard or adjacency matrix).
- **Code Example** (Python):

  ```python
  def create_matrix(n):
    matrix = []
    for i in range(n):
        row = [0] * n  # Each row contains n elements
        matrix.append(row)
    return matrix  # The overall storage space grows with the square of n
  ```

## 5. Summary

| Complexity Type  | Meaning                                 | Calculation Focus                    | Example                   |
| :--------------- | :-------------------------------------- | :----------------------------------- | :------------------------ |
| Time Complexity  | Growth trend of algorithm running time  | Number of basic operation executions | Number of loop iterations |
| Space Complexity | Growth trend of algorithm memory usage  | Additionally allocated memory space  | Array size                |

---

### When calculating complexity,remember to “**focus on the big and ignore the small**.”  

- When calculating time complexity, identify the basic operations (such as comparisons and assignments within loops).  

- When calculating space complexity, calculate the space occupied by variables (including input data, auxiliary variables, recursion stacks, etc.).

### Understanding time and space complexity helps us write efficient and resource-saving programs

### A reminder once again

- Big $O$ notation represents the growth trend of an algorithm, not its specific execution time or memory size.

## ***That’s All!!! Hope Everyone Learned Something!!!***
