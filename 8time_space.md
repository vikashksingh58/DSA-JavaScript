# Time and Space Complexity
## Comprehensive Study Notes - DSA Series

---

## Table of Contents

1. [Introduction to Complexity](#1-introduction-to-complexity)
2. [Time Complexity Fundamentals](#2-time-complexity-fundamentals)
3. [Complexity Notations](#3-complexity-notations)
4. [Types of Time Complexity](#4-types-of-time-complexity)
5. [Calculating Time Complexity](#5-calculating-time-complexity)
6. [Understanding TLE (Time Limit Exceeded)](#6-understanding-tle-time-limit-exceeded)
7. [Space Complexity](#7-space-complexity)
8. [Practical Examples](#8-practical-examples)
9. [Key Takeaways](#9-key-takeaways)

---

## 1. Introduction to Complexity

### What is Complexity?

**Complexity** refers to **how complicated or difficult a task is** to complete. It measures the "level" of difficulty.

### Real-World Analogies

| Easy Task | Hard Task |
|-----------|-----------|
| Solving Sudoku | Solving Rubik's Cube |
| Courting a single girl | Maintaining a relationship |
| Making a sandwich | Preparing a 5-course meal |
| Calculating factors of one number | Finding prime numbers from 1 to n |

**Key Insight:** Complexity describes the **behavior or measure** of a task's difficulty, not just a yes/no answer.

### Why Complexity Matters

- **Small inputs** - Complexity is often negligible
- **Large inputs** - Complexity becomes critical for:
  - Performance
  - Resource management
  - Scalability
  - Meeting time constraints

**Example:**
- Managing 10 employee records → Any approach works
- Managing 1 billion records → Need efficient algorithms

---

## 2. Time Complexity Fundamentals

### What is Time Complexity?

**Time Complexity** is the amount of time (operations) an algorithm takes as a function of input size **n**.

### Critical Understanding: NOT Clock Time

**❌ Common Misconception:**
Time complexity measures actual seconds/minutes taken by a program.

**✅ Correct Understanding:**
Time complexity measures the **number of operations** performed relative to input size.

### Why Not Clock Time?

```
Scenario: Same algorithm running on different computers

Supercomputer:    Runs code in 0.001 seconds
Basic 4GB PC:     Runs code in 10 seconds

Same algorithm, different actual times!
But time complexity is IDENTICAL for both.
```

**The algorithm's efficiency remains the same** regardless of hardware.

### Formal Definition

**Time Complexity = Number of Operations as a Function of Input Size (n)**

Where:
- **n** = size of input
- **Operations** = basic steps like:
  - Addition/subtraction
  - Comparison
  - Assignment
  - Loop iterations
  - Function calls

---

### Understanding "As a Function of n"

**Example 1: Single Operation**
```javascript
function addOne(x) {
  return x + 1;  // 1 operation
}
```
**Operations:** 1 (constant, regardless of input)

**Example 2: Loop from 1 to n**
```javascript
function printNumbers(n) {
  for (let i = 1; i <= n; i++) {
    console.log(i);
  }
}
```
**Operations:** n (one for each iteration)

**Example 3: Loop from 1 to n/2**
```javascript
function printHalf(n) {
  for (let i = 1; i <= n/2; i++) {
    console.log(i);
  }
}
```
**Operations:** n/2

### Linear Search Example

**Problem:** Find a target element in an array.

```javascript
function linearSearch(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
      return i;
    }
  }
  return -1;
}
```

**Analysis:**
- **Best case:** Target is first element → 1 operation
- **Average case:** Target is in middle → n/2 operations
- **Worst case:** Target is last or not found → n operations

**For time complexity, we ALWAYS consider WORST CASE.**

### Input Size Impact

| Array Length | Operations (Worst Case) |
|--------------|-------------------------|
| 100 | 100 |
| 2000 | 2000 |
| 1,000,000 | 1,000,000 |

**Pattern:** As input size increases, operations increase proportionally.

---

## 3. Complexity Notations

### Why Notations?

Just like we measure:
- **Weight** in kilograms
- **Distance** in meters
- **Volume** in liters

We measure **complexity** using standard notations.

### Three Primary Notations

| Notation | Name | Meaning | Represents | Usage |
|----------|------|---------|------------|-------|
| **Big O (O)** | Big Oh | Upper bound | Worst case | Most common |
| **Theta (Θ)** | Theta | Tight bound | Average case | Theoretical analysis |
| **Omega (Ω)** | Omega | Lower bound | Best case | Rarely used |

### Big O Notation (Most Important)

**Big O describes the WORST CASE scenario.**

**Why focus on worst case?**
- Gives an upper limit on performance
- Guarantees algorithm won't perform worse
- Most relevant for real-world applications
- Standard in interviews and competitive programming

**Example:**
```javascript
function findMax(arr) {
  let max = arr[0];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
      max = arr[i];
    }
  }
  return max;
}
```

**Analysis:**
- Always checks all n elements
- Time Complexity: **O(n)**
- No matter what, loops n times

---

## 4. Types of Time Complexity

### 4.1 Constant Time - O(1)

**Definition:** Operations remain constant regardless of input size.

**Characteristics:**
- Single operation or fixed number of operations
- Does not depend on n

**Examples:**

```javascript
// Example 1: Direct access
function getFirstElement(arr) {
  return arr[0];  // O(1)
}

// Example 2: Using formula
function sumOfN(n) {
  return (n * (n + 1)) / 2;  // O(1)
}

// Example 3: Hash table lookup
function getValue(map, key) {
  return map[key];  // O(1)
}
```

**Graph:**
```
Operations
    |
  1 |__________ (flat line)
    |
    +-----------> Input Size (n)
```

---

### 4.2 Linear Time - O(n)

**Definition:** Operations grow proportionally with input size.

**Characteristics:**
- Single loop from 0 to n
- One pass through data

**Examples:**

```javascript
// Example 1: Linear search
function linearSearch(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) return i;
  }
  return -1;
}  // O(n)

// Example 2: Sum array
function sumArray(arr) {
  let sum = 0;
  for (let i = 0; i < arr.length; i++) {
    sum += arr[i];
  }
  return sum;
}  // O(n)

// Example 3: Print all elements
function printAll(arr) {
  for (let element of arr) {
    console.log(element);
  }
}  // O(n)
```

**Graph:**
```
Operations
    |     /
    |    /
    |   /
    |  /
    | /
    |/__________ Input Size (n)
```

---

### 4.3 Quadratic Time - O(n²)

**Definition:** Operations grow with square of input size.

**Characteristics:**
- Nested loops (both running n times)
- Checking all pairs
- Two-dimensional processing

**Examples:**

```javascript
// Example 1: Nested loops
function printPairs(n) {
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      console.log(i, j);
    }
  }
}  // O(n²)

// Example 2: Bubble sort
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }
}  // O(n²)

// Example 3: Check duplicates
function hasDuplicate(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] === arr[j]) return true;
    }
  }
  return false;
}  // O(n²)
```

**Graph:**
```
Operations
    |         ___/
    |      __/
    |    _/
    |   /
    |  /
    |_/__________ Input Size (n)
```

---

### 4.4 Logarithmic Time - O(log n)

**Definition:** Input size reduces drastically (usually by half) each step.

**Characteristics:**
- Dividing problem in half repeatedly
- Binary search pattern
- Very efficient for large inputs

**Examples:**

```javascript
// Example 1: Binary search
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;
  
  while (left <= right) {
    let mid = Math.floor((left + right) / 2);
    
    if (arr[mid] === target) return mid;
    if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
  }
  return -1;
}  // O(log n)

// Example 2: Finding power (divide & conquer)
function power(x, n) {
  if (n === 0) return 1;
  if (n === 1) return x;
  
  let half = power(x, Math.floor(n / 2));
  
  if (n % 2 === 0) {
    return half * half;
  } else {
    return x * half * half;
  }
}  // O(log n)

// Example 3: Loop dividing by 2
function countDivisions(n) {
  let count = 0;
  while (n > 1) {
    n = Math.floor(n / 2);
    count++;
  }
  return count;
}  // O(log n)
```

**How it works:**

Starting with n = 1000:
```
Step 1: n = 1000
Step 2: n = 500
Step 3: n = 250
Step 4: n = 125
Step 5: n = 62
Step 6: n = 31
Step 7: n = 15
Step 8: n = 7
Step 9: n = 3
Step 10: n = 1
```

Only **10 steps** for n = 1000!

**Graph:**
```
Operations
    |___
    |   ----___
    |          ----___
    |                 ----___ Input Size (n)
```

---

### 4.5 Linearithmic Time - O(n log n)

**Definition:** Combination of linear and logarithmic.

**Characteristics:**
- Efficient sorting algorithms
- Divide and conquer with merging
- Processing n items, each taking log n time

**Examples:**

```javascript
// Example 1: Merge Sort
function mergeSort(arr) {
  if (arr.length <= 1) return arr;
  
  let mid = Math.floor(arr.length / 2);
  let left = mergeSort(arr.slice(0, mid));
  let right = mergeSort(arr.slice(mid));
  
  return merge(left, right);
}  // O(n log n)

// Example 2: Quick Sort (average case)
function quickSort(arr) {
  if (arr.length <= 1) return arr;
  
  let pivot = arr[arr.length - 1];
  let left = arr.filter(x => x < pivot);
  let right = arr.filter(x => x > pivot);
  
  return [...quickSort(left), pivot, ...quickSort(right)];
}  // O(n log n) average

// Example 3: Binary search in loop
function findMultiple(arr, targets) {
  let results = [];
  for (let target of targets) {  // n times
    results.push(binarySearch(arr, target));  // log n
  }
  return results;
}  // O(n log n)
```

---

### 4.6 Exponential Time - O(2ⁿ)

**Definition:** Operations double with each increase in input.

**Characteristics:**
- Recursive algorithms with multiple branches
- Generating all subsets
- Fibonacci (naive recursive)
- Very slow for large n

**Examples:**

```javascript
// Example 1: Fibonacci (naive)
function fibonacci(n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}  // O(2ⁿ)

// Example 2: Generate all subsets
function generateSubsets(arr) {
  if (arr.length === 0) return [[]];
  
  let first = arr[0];
  let rest = arr.slice(1);
  let subsetsWithoutFirst = generateSubsets(rest);
  let subsetsWithFirst = subsetsWithoutFirst.map(
    subset => [first, ...subset]
  );
  
  return [...subsetsWithoutFirst, ...subsetsWithFirst];
}  // O(2ⁿ)

// Example 3: Tower of Hanoi
function towerOfHanoi(n) {
  if (n === 1) return 1;
  return 2 * towerOfHanoi(n - 1) + 1;
}  // O(2ⁿ)
```

**Growth illustration:**

| n | Operations |
|---|------------|
| 1 | 2 |
| 2 | 4 |
| 3 | 8 |
| 5 | 32 |
| 10 | 1,024 |
| 20 | 1,048,576 |
| 30 | 1,073,741,824 |

---

### 4.7 Factorial Time - O(n!)

**Definition:** Operations grow factorially with input size.

**Characteristics:**
- Generating all permutations
- Traveling salesman problem
- Extremely slow, only feasible for very small n

**Examples:**

```javascript
// Example 1: Generate all permutations
function permute(arr) {
  if (arr.length === 0) return [[]];
  
  let result = [];
  for (let i = 0; i < arr.length; i++) {
    let current = arr[i];
    let remaining = arr.slice(0, i).concat(arr.slice(i + 1));
    let perms = permute(remaining);
    
    for (let perm of perms) {
      result.push([current, ...perm]);
    }
  }
  return result;
}  // O(n!)

// Example 2: Brute force TSP
function travelingSalesmanBruteForce(cities) {
  let allRoutes = permute(cities);
  let minDistance = Infinity;
  
  for (let route of allRoutes) {
    let distance = calculateDistance(route);
    minDistance = Math.min(minDistance, distance);
  }
  return minDistance;
}  // O(n!)
```

**Growth illustration:**

| n | n! |
|---|-----|
| 1 | 1 |
| 2 | 2 |
| 3 | 6 |
| 4 | 24 |
| 5 | 120 |
| 10 | 3,628,800 |
| 15 | 1,307,674,368,000 |

---

### Complexity Comparison Graph

```
Operations
    |
    |                                    O(n!)
    |                                 /
    |                            O(2ⁿ)/
    |                           /
    |                    O(n²) /
    |                   /    /
    |            O(n log n) /
    |              /   /  /
    |        O(n)/  /  /
    |          //  /  /
    |    O(log n)/  /
    |      /   /  /
    | O(1)___/__/_________________ Input Size (n)
```

### Complexity Ranking (Best to Worst)

1. **O(1)** - Constant ⭐⭐⭐⭐⭐
2. **O(log n)** - Logarithmic ⭐⭐⭐⭐
3. **O(n)** - Linear ⭐⭐⭐
4. **O(n log n)** - Linearithmic ⭐⭐
5. **O(n²)** - Quadratic ⭐
6. **O(2ⁿ)** - Exponential ⚠️
7. **O(n!)** - Factorial ❌

---

## 5. Calculating Time Complexity

### Rules for Calculating Time Complexity

#### Rule 1: Count Loop Iterations

```javascript
// Single loop
for (let i = 0; i < n; i++) {
  // O(1) operations
}
// Time Complexity: O(n)
```

#### Rule 2: Nested Loops Multiply

```javascript
// Two nested loops
for (let i = 0; i < n; i++) {
  for (let j = 0; j < n; j++) {
    // O(1) operations
  }
}
// Time Complexity: O(n) × O(n) = O(n²)
```

#### Rule 3: Sequential Loops Add

```javascript
// Three separate loops
for (let i = 0; i < n; i++) {
  // O(1)
}

for (let j = 0; j < n; j++) {
  // O(1)
}

for (let k = 0; k < n; k++) {
  // O(1)
}

// Time Complexity: O(n) + O(n) + O(n) = O(3n) = O(n)
```

#### Rule 4: Drop Constants

```javascript
// Example 1
function example1(n) {
  for (let i = 0; i < 5 * n; i++) {
    console.log(i);
  }
}
// 5n operations → O(5n) → **O(n)**

// Example 2
function example2(n) {
  for (let i = 0; i < n/2; i++) {
    console.log(i);
  }
}
// n/2 operations → O(n/2) → **O(n)**
```

**Why?** Constants don't affect growth rate for large n.

#### Rule 5: Drop Lower-Order Terms

```javascript
function example(n) {
  // Part 1: O(n²)
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      console.log(i, j);
    }
  }
  
  // Part 2: O(n)
  for (let k = 0; k < n; k++) {
    console.log(k);
  }
}

// Total: O(n²) + O(n)
// Simplified: O(n²)
```

**Why?** For large n, n² dominates n.

### Simplification Examples

| Original Expression | Simplified |
|---------------------|------------|
| O(3n²/2 + n log n + n) | O(n²) |
| O(n log n + log n + n) | O(n log n) |
| O(5n + 100) | O(n) |
| O(n²/2 + 3n + 10) | O(n²) |
| O(2ⁿ + n³) | O(2ⁿ) |

### Complex Examples

#### Example 1: Nested with Different Ranges

```javascript
function example(n) {
  for (let i = 0; i < n; i++) {
    for (let j = i; j < n; j++) {
      console.log(i, j);
    }
  }
}
```

**Analysis:**
- Outer loop: n iterations
- Inner loop: n, n-1, n-2, ..., 1 iterations
- Total: n + (n-1) + (n-2) + ... + 1 = n(n+1)/2
- **Time Complexity: O(n²)**

#### Example 2: Logarithmic in Nested Loop

```javascript
function example(n) {
  for (let i = 0; i < n; i++) {
    let j = 1;
    while (j < n) {
      console.log(i, j);
      j *= 2;
    }
  }
}
```

**Analysis:**
- Outer loop: O(n)
- Inner loop: O(log n) (j doubles each time)
- **Time Complexity: O(n log n)**

#### Example 3: Multiple Operations

```javascript
function example(arr) {
  // Step 1: Linear search
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) return i;
  }  // O(n)
  
  // Step 2: Bubble sort
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }  // O(n²)
  
  // Step 3: Print
  for (let item of arr) {
    console.log(item);
  }  // O(n)
}

// Total: O(n) + O(n²) + O(n) = O(n²)
```

---

## 6. Understanding TLE (Time Limit Exceeded)

### What is TLE?

**TLE (Time Limit Exceeded)** occurs when your algorithm takes longer than the allowed time limit to execute.

### Why Does TLE Happen?

Every problem has **constraints** that limit:
- Maximum input size (n)
- Maximum execution time

If your algorithm's time complexity is **too slow** for the given input size, you get TLE.

### Constraints and Allowed Complexity

**General Guidelines:**

| Input Size (n) | Max Allowed Complexity | Explanation |
|----------------|------------------------|-------------|
| n ≤ 10 | O(n!) | Even factorial is fast enough |
| n ≤ 20 | O(2ⁿ) | Exponential acceptable |
| n ≤ 500 | O(n³) | Cubic time works |
| n ≤ 5,000 | O(n²) | Quadratic acceptable |
| n ≤ 10⁴ | O(n² log n) | Quadratic with log factor |
| n ≤ 10⁵ | O(n log n) | Linearithmic preferred |
| n ≤ 10⁶ | O(n) or O(n log n) | Linear or better |
| n ≤ 10⁸ | O(n) | Only linear |
| n ≤ 10⁹ | O(log n) or O(1) | Only logarithmic or constant |

### Rough Time Calculations

**Assumption:** Modern computers can perform about **10⁸ to 10⁹ operations per second**.

| Complexity | n = 10⁴ | n = 10⁶ | n = 10⁸ |
|------------|---------|---------|---------|
| O(n) | 10⁴ ops | 10⁶ ops | 10⁸ ops |
| O(n log n) | ~10⁵ ops | ~10⁷ ops | ~10⁹ ops |
| O(n²) | 10⁸ ops | 10¹² ops | 10¹⁶ ops |

**Red flags:**
- O(n²) with n = 10⁶ → 10¹² operations → **TLE!**
- O(n³) with n = 10⁴ → 10¹² operations → **TLE!**

### How to Avoid TLE

1. **Check Constraints First**
   - Always read problem constraints before coding
   - Determine maximum input size

2. **Choose Appropriate Algorithm**
   - Calculate required time complexity
   - Select algorithm accordingly

3. **Optimize Your Code**
   - Use efficient data structures
   - Avoid unnecessary operations
   - Break early when possible

4. **Test with Large Inputs**
   - Test with maximum constraints
   - Measure execution time

### Example Scenario

**Problem:** Find if array has duplicate elements.

**Constraints:** n ≤ 10⁶

**Bad Solution (TLE):**
```javascript
function hasDuplicate(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] === arr[j]) return true;
    }
  }
  return false;
}
// O(n²) → For n = 10⁶ → 10¹² operations → TLE!
```

**Good Solution:**
```javascript
function hasDuplicate(arr) {
  let seen = new Set();
  for (let num of arr) {
    if (seen.has(num)) return true;
    seen.add(num);
  }
  return false;
}
// O(n) → For n = 10⁶ → 10⁶ operations → Passes!
```

---

## 7. Space Complexity

### What is Space Complexity?

**Space Complexity** measures the amount of memory an algorithm uses relative to input size.

### Components of Space

1. **Input Space** - Space for input data (usually not counted)
2. **Auxiliary Space** - Extra space used by algorithm
3. **Output Space** - Space for output (sometimes counted)

**We focus on AUXILIARY SPACE.**

### Common Space Complexities

#### O(1) - Constant Space

**No extra space** that grows with input size.

```javascript
// Example 1: Using single variables
function sum(n) {
  let total = 0;  // O(1) space
  for (let i = 1; i <= n; i++) {
    total += i;
  }
  return total;
}

// Example 2: Swap
function swap(a, b) {
  let temp = a;  // O(1) space
  a = b;
  b = temp;
}

// Example 3: Find max
function findMax(arr) {
  let max = arr[0];  // O(1) space
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) max = arr[i];
  }
  return max;
}
```

**Key:** Variables are reused, not accumulated.

#### O(n) - Linear Space

**Extra space grows linearly** with input.

```javascript
// Example 1: Creating new array
function double(arr) {
  let result = [];  // O(n) space
  for (let num of arr) {
    result.push(num * 2);
  }
  return result;
}

// Example 2: Recursion depth
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}
// Call stack: O(n) space

// Example 3: Hash table
function countFrequency(arr) {
  let freq = {};  // O(n) space worst case
  for (let num of arr) {
    freq[num] = (freq[num] || 0) + 1;
  }
  return freq;
}
```

#### O(n²) - Quadratic Space

**2D array or nested data structures.**

```javascript
// Example 1: 2D matrix
function createMatrix(n) {
  let matrix = [];
  for (let i = 0; i < n; i++) {
    matrix[i] = [];
    for (let j = 0; j < n; j++) {
      matrix[i][j] = i * n + j;
    }
  }
  return matrix;
}  // O(n²) space

// Example 2: Adjacency matrix
function createGraph(n) {
  let graph = Array(n).fill(0).map(
    () => Array(n).fill(0)
  );
  return graph;
}  // O(n²) space
```

### Space Complexity Examples

| Code Pattern | Space Complexity |
|--------------|------------------|
| Single variable | O(1) |
| Array of size n | O(n) |
| 2D array n×n | O(n²) |
| Recursion depth n | O(n) |
| Hash table with n unique keys | O(n) |

### Space vs Time Trade-off

Often, you can trade space for time:

**Example: Fibonacci**

**Approach 1: Recursive (less space, more time)**
```javascript
function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
}
// Time: O(2ⁿ), Space: O(n) [call stack]
```

**Approach 2: Memoization (more space, less time)**
```javascript
function fib(n, memo = {}) {
  if (n <= 1) return n;
  if (memo[n]) return memo[n];
  
  memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
  return memo[n];
}
// Time: O(n), Space: O(n)
```

**Approach 3: Iterative (optimal)**
```javascript
function fib(n) {
  if (n <= 1) return n;
  
  let prev = 0, curr = 1;
  for (let i = 2; i <= n; i++) {
    let next = prev + curr;
    prev = curr;
    curr = next;
  }
  return curr;
}
// Time: O(n), Space: O(1)
```

---

## 8. Practical Examples

### Example 1: Simple Loop

```javascript
function printNumbers(n) {
  for (let i = 0; i < n; i++) {
    console.log(i);
  }
}
```

**Analysis:**
- Loop runs n times
- Each iteration: O(1) work
- **Time:** O(n)
- **Space:** O(1) (only variable i)

---

### Example 2: Nested Loops

```javascript
function printPairs(n) {
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      console.log(i, j);
    }
  }
}
```

**Analysis:**
- Outer loop: n iterations
- Inner loop: n iterations for each outer
- Total: n × n = n²
- **Time:** O(n²)
- **Space:** O(1)

---

### Example 3: Loop with Array Building

```javascript
function buildArray(n) {
  let arr = [];
  for (let i = 0; i < n; i++) {
    arr.push(i);
  }
  return arr;
}
```

**Analysis:**
- Loop: n iterations
- Array grows to size n
- **Time:** O(n)
- **Space:** O(n)

---

### Example 4: Nested Loop with Array

```javascript
function build2DArray(n) {
  let matrix = [];
  for (let i = 0; i < n; i++) {
    let row = [];
    for (let j = 0; j < n; j++) {
      row.push(i * n + j);
    }
    matrix.push(row);
  }
  return matrix;
}
```

**Analysis:**
- Nested loops: n × n iterations
- Creates n × n matrix
- **Time:** O(n²)
- **Space:** O(n²)

---

### Example 5: Logarithmic Loop

```javascript
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;
  
  while (left <= right) {
    let mid = Math.floor((left + right) / 2);
    
    if (arr[mid] === target) return mid;
    if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
  }
  return -1;
}
```

**Analysis:**
- Search space halves each iteration
- Starts at n, then n/2, n/4, n/8...
- **Time:** O(log n)
- **Space:** O(1)

**Illustration:**
```
n = 1000
Step 1: 1000
Step 2: 500
Step 3: 250
Step 4: 125
Step 5: 62
Step 6: 31
Step 7: 15
Step 8: 7
Step 9: 3
Step 10: 1
```

Only 10 steps for n = 1000!

---

### Example 6: Loop Halving

```javascript
function countHalving(n) {
  let count = 0;
  let i = n;
  
  while (i > 1) {
    i = Math.floor(i / 2);
    count++;
  }
  
  return count;
}
```

**Analysis:**
- i starts at n
- Each iteration: i = i / 2
- Stops when i ≤ 1
- **Time:** O(log n)
- **Space:** O(1)

---

### Example 7: Multiple Separate Loops

```javascript
function multipleLoops(n) {
  // Loop 1
  for (let i = 0; i < n; i++) {
    console.log(i);
  }
  
  // Loop 2
  for (let j = 0; j < n; j++) {
    console.log(j);
  }
  
  // Loop 3
  for (let k = 0; k < n; k++) {
    console.log(k);
  }
}
```

**Analysis:**
- Three separate loops
- Each runs n times
- Total: n + n + n = 3n
- **Time:** O(3n) = O(n)
- **Space:** O(1)

---

### Example 8: Complex Mixed

```javascript
function complex(n) {
  // Part 1: O(n²)
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n; j++) {
      console.log(i, j);
    }
  }
  
  // Part 2: O(n log n)
  for (let i = 0; i < n; i++) {
    let j = 1;
    while (j < n) {
      console.log(i, j);
      j *= 2;
    }
  }
  
  // Part 3: O(n)
  for (let k = 0; k < n; k++) {
    console.log(k);
  }
}
```

**Analysis:**
- Part 1: O(n²)
- Part 2: O(n log n)
- Part 3: O(n)
- **Total:** O(n²) + O(n log n) + O(n)
- **Simplified:** O(n²)

---

## 9. Key Takeaways

### Essential Concepts

1. **Time Complexity ≠ Clock Time**
   - Measures operations, not seconds
   - Independent of hardware

2. **Always Consider Worst Case**
   - Big O notation represents worst case
   - Most relevant for practical scenarios

3. **Drop Constants and Lower Terms**
   - O(5n) → O(n)
   - O(n² + n) → O(n²)

4. **Check Constraints First**
   - Determine max input size
   - Choose appropriate algorithm
   - Avoid TLE

5. **Space vs Time Trade-off**
   - Sometimes use more space for less time
   - Balance based on requirements

### Complexity Hierarchy (Best to Worst)

```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)
```

### Loop Patterns Quick Reference

| Pattern | Time Complexity |
|---------|-----------------|
| Single loop to n | O(n) |
| Two nested loops to n | O(n²) |
| Three nested loops to n | O(n³) |
| Loop halving each time | O(log n) |
| Loop + binary search | O(n log n) |
| Recursive with 2 calls | O(2ⁿ) |

### Input Size Guidelines

| n Range | Allowed Complexity |
|---------|-------------------|
| n ≤ 10 | O(n!) |
| n ≤ 20 | O(2ⁿ) |
| n ≤ 500 | O(n³) |
| n ≤ 10⁴ | O(n²) |
| n ≤ 10⁶ | O(n log n) |
| n ≤ 10⁸ | O(n) |
| n ≥ 10⁹ | O(log n) or O(1) |

### Common Mistakes

❌ **Confusing time with actual seconds**
✅ Count operations, not clock time

❌ **Forgetting to drop constants**
✅ O(5n) = O(n)

❌ **Not considering worst case**
✅ Always analyze worst case

❌ **Ignoring constraints**
✅ Check constraints before coding

❌ **Overcomplicating analysis**
✅ Focus on dominant term

### Practical Tips

1. **Before Coding:**
   - Read constraints
   - Determine required complexity
   - Plan algorithm

2. **While Coding:**
   - Count nested loops
   - Watch for recursive calls
   - Consider space usage

3. **After Coding:**
   - Verify complexity
   - Test with large inputs
   - Use tools to verify (ChatGPT, etc.)

### Study Strategy

1. **Understand concepts** - Don't just memorize
2. **Practice analysis** - Break down real code
3. **Solve problems** - Apply to actual questions
4. **Use tools** - Verify with ChatGPT or calculators
5. **Review patterns** - Recognize common structures

### Interview Preparation

**Always mention:**
- Time complexity
- Space complexity
- Trade-offs considered
- Why you chose this approach

**Example response:**
> "My solution uses O(n log n) time due to sorting and O(n) space for the hash table. I chose this approach because the constraints allow n up to 10⁶, which makes O(n²) too slow. I could optimize space to O(1) but it would increase time to O(n²), which violates constraints."

---

## Resources for Practice

- **LeetCode** - Practice with real constraints
- **HackerRank** - Time complexity challenges
- **Codeforces** - Competitive programming
- **ChatGPT** - Verify your analysis
- **Big-O Cheat Sheet** - Quick reference

---

## Final Motivation

**Remember:**
- Complexity analysis is a skill that improves with practice
- Don't get discouraged by initial confusion
- Every expert was once a beginner
- Understanding complexity is crucial for:
  - Technical interviews
  - Writing efficient code
  - Scaling applications
  - Problem-solving

**Keep practicing and you'll master it!**

**If this guide helped you, remember to:**
- Practice analyzing code
- Test your understanding
- Share your knowledge
- Keep learning

---

**Happy Coding! 🚀**

**End of Study Notes**