# Quick Sort Algorithm
## Comprehensive Study Notes - DSA Series

---

## Table of Contents

1. [Introduction to Quick Sort](#1-introduction-to-quick-sort)
2. [Core Concepts: Pivot and Partition](#2-core-concepts-pivot-and-partition)
3. [How Quick Sort Works](#3-how-quick-sort-works)
4. [Step-by-Step Algorithm](#4-step-by-step-algorithm)
5. [Implementation Details](#5-implementation-details)
6. [Time and Space Complexity](#6-time-and-space-complexity)
7. [Quick Sort vs Merge Sort](#7-quick-sort-vs-merge-sort)
8. [Key Takeaways](#8-key-takeaways)

---

## 1. Introduction to Quick Sort

### What is Quick Sort?

**Quick Sort** is a highly efficient, **fast and smart** sorting algorithm that uses the **Divide and Conquer** paradigm.

### Key Characteristics

- **In-place sorting** - Requires no extra array space
- **Divide and Conquer** - Breaks problem into smaller subproblems
- **Uses Pivot and Partition** - Core mechanism different from Merge Sort
- **Fast in practice** - One of the fastest sorting algorithms on average

### Learning Objectives

By the end of this guide, you will understand:
1. What Quick Sort is and how it works
2. The pivot and partition mechanism
3. Step-by-step code implementation
4. Time and space complexity analysis
5. Comparison with Merge Sort
6. Real-world applications

---

## 2. Core Concepts: Pivot and Partition

### The Pivot

**Definition:** The pivot is a chosen element from the array around which we partition (divide) the array.

**Purpose:**
- Acts as a reference point for comparison
- After partitioning, the pivot is in its final sorted position
- Elements smaller than pivot go to its left
- Elements larger than pivot go to its right

### Pivot Selection Strategies

There are multiple ways to choose a pivot:

| Strategy | Description | Pros | Cons |
|----------|-------------|------|------|
| **First Element** | Choose `arr[0]` | Simple to implement | Worst case on sorted arrays |
| **Last Element** | Choose `arr[n-1]` | Simple to implement | Worst case on sorted arrays |
| **Middle Element** | Choose `arr[n/2]` | Better for sorted arrays | Slightly more complex |
| **Random Element** | Choose random index | Avoids worst case | Requires randomization |
| **Median of Three** | Median of first, middle, last | Best average performance | Most complex |

**In this guide, we use the FIRST ELEMENT as pivot for simplicity.**

### The Partition

**Definition:** Partition is the process of rearranging array elements so that:
- All elements less than the pivot are on the left
- All elements greater than the pivot are on the right
- The pivot ends up in its correct sorted position

**Key Point:** After partition, the pivot is in its final position in the sorted array.

---

## 3. How Quick Sort Works

### The Big Picture

```
Original Array: [5, 2, 9, 1, 7, 6, 3]

Step 1: Choose Pivot (first element = 5)
Step 2: Partition around pivot
Result: [2, 1, 3, 5, 7, 6, 9]
         └─left─┘ ↑  └─right─┘
                pivot (sorted position)

Step 3: Recursively sort left subarray [2, 1, 3]
Step 4: Recursively sort right subarray [7, 6, 9]
```

### The Divide and Conquer Strategy

1. **Divide:** Partition the array around a pivot
2. **Conquer:** Recursively sort the left and right subarrays
3. **Combine:** No combination needed (in-place sorting)

### Visual Example

```
Initial Array: [8, 3, 1, 7, 0, 10, 2]

Pick Pivot = 8 (first element)

After Partition: [3, 1, 7, 0, 2, 8, 10]
                  └───left───┘  ↑  └right┘
                            pivot in correct position

Recursively sort:
- Left:  [3, 1, 7, 0, 2]
- Right: [10]

Continue until all subarrays are of size 1
```

---

## 4. Step-by-Step Algorithm

### The Partitioning Process

This is the **heart** of Quick Sort. Understanding this is crucial.

### Two-Pointer Approach

We use two pointers `i` and `j` to partition the array:

- **i** - Starts from `first + 1`, moves forward
- **j** - Starts from `last`, moves backward

### Detailed Algorithm Steps

```
Given: arr[first...last], pivot = arr[first]

1. Initialize:
   i = first + 1  (start after pivot)
   j = last       (start from end)

2. Loop while i <= j:
   
   a) Move i forward while arr[i] < pivot
      (find element that should be on right)
   
   b) Move j backward while arr[j] > pivot
      (find element that should be on left)
   
   c) If i < j, swap arr[i] and arr[j]
      (put elements in correct partitions)

3. After loop ends (when i >= j):
   Swap pivot with arr[j]
   (place pivot in its correct position)

4. Return j (pivot index)
```

### Example Walkthrough

Let's partition `[8, 3, 1, 7, 0, 10, 2]` with pivot = 8

```
Initial: [8, 3, 1, 7, 0, 10, 2]
          ↑                 ↑
       pivot              last
          
i starts at index 1 (element 3)
j starts at index 6 (element 2)

Step 1: Move i forward while arr[i] < 8
  arr[1]=3 < 8 ✓  i=1
  arr[2]=1 < 8 ✓  i=2
  arr[3]=7 < 8 ✓  i=3
  arr[4]=0 < 8 ✓  i=4
  arr[5]=10 >= 8 ✗  Stop at i=5

Step 2: Move j backward while arr[j] > 8
  arr[6]=2 < 8 ✗  Stop at j=6

Step 3: i < j? (5 < 6 = true)
  Swap arr[5] and arr[6]
  [8, 3, 1, 7, 0, 2, 10]

Step 4: Continue loop
  Move i: arr[5]=2 < 8 ✓  i=6
          arr[6]=10 >= 8 ✗  Stop at i=6
  
  Move j: arr[6]=10 > 8 ✓  j=5
          arr[5]=2 < 8 ✗  Stop at j=5

Step 5: i < j? (6 < 5 = false)
  Exit loop

Step 6: Swap pivot with arr[j]
  Swap arr[0] with arr[5]
  [2, 3, 1, 7, 0, 8, 10]
   └───left───┘  ↑  └right┘
              pivot at index 5

Return 5
```

### After Partitioning

```
[2, 3, 1, 7, 0, 8, 10]

Left subarray:  [2, 3, 1, 7, 0]  (indices 0-4)
Pivot:          8                 (index 5) ← SORTED!
Right subarray: [10]              (index 6)
```

---

## 5. Implementation Details

### Main Quick Sort Function

```javascript
function quickSort(arr, first, last) {
  // Base case: subarray has 0 or 1 element
  if (first >= last) {
    return;
  }
  
  // Find pivot index through partitioning
  let pivotIndex = findPivotIndex(arr, first, last);
  
  // Recursively sort left subarray
  quickSort(arr, first, pivotIndex - 1);
  
  // Recursively sort right subarray
  quickSort(arr, pivotIndex + 1, last);
}
```

### Partition Function (Find Pivot Index)

```javascript
function findPivotIndex(arr, first, last) {
  let pivot = arr[first];  // Choose first element as pivot
  let i = first + 1;       // Start after pivot
  let j = last;            // Start from end
  
  while (i <= j) {
    // Move i forward while elements are smaller than pivot
    while (i <= last && arr[i] <= pivot) {
      i++;
    }
    
    // Move j backward while elements are larger than pivot
    while (j >= first && arr[j] > pivot) {
      j--;
    }
    
    // Swap if pointers haven't crossed
    if (i < j) {
      swap(arr, i, j);
    }
  }
  
  // Place pivot in correct position
  swap(arr, first, j);
  
  return j;  // Return pivot's final position
}
```

### Swap Helper Function

```javascript
function swap(arr, i, j) {
  let temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
}
```

### Usage Example

```javascript
let arr = [8, 3, 1, 7, 0, 10, 2];
console.log("Original:", arr);

quickSort(arr, 0, arr.length - 1);

console.log("Sorted:", arr);
// Output: Sorted: [0, 1, 2, 3, 7, 8, 10]
```

### Important Loop Conditions

**Why `i <= last` in inner while loop?**
```javascript
while (i <= last && arr[i] <= pivot) {
  i++;
}
```
- Prevents `i` from going out of bounds
- Ensures we stay within array limits

**Why `j >= first` in inner while loop?**
```javascript
while (j >= first && arr[j] > pivot) {
  j--;
}
```
- Prevents `j` from going out of bounds
- Ensures we don't go before the first element

**Why `arr[i] <= pivot` (with equals)?**
- Handles duplicate values correctly
- Ensures elements equal to pivot can be on either side

**Why swap only if `i < j`?**
```javascript
if (i < j) {
  swap(arr, i, j);
}
```
- Once `i >= j`, pointers have crossed
- Swapping would undo correct partitioning

---

## 6. Time and Space Complexity

### Time Complexity Analysis

#### Best and Average Case: O(n log n)

**Reasoning:**

1. **Partition Operation:** O(n)
   - Traverse entire array with two pointers
   - Total operations: n (incrementing i + decrementing j)

2. **Recursion Depth:** O(log n)
   - Each partition divides array roughly in half
   - Recursion tree has log n levels

3. **Total:** O(n) × O(log n) = **O(n log n)**

**Visual Representation:**

```
Level 0:  [─────────n─────────]  → n operations
           ↙               ↘
Level 1:  [───n/2───]  [───n/2───]  → n operations total
           ↙     ↘      ↙     ↘
Level 2: [n/4][n/4]  [n/4][n/4]  → n operations total
         ...
Level log n: [1][1][1]...[1]  → n operations total

Total levels: log n
Operations per level: n
Total time: n × log n
```

#### Worst Case: O(n²)

**When does it occur?**

1. **Already sorted array** (with first element as pivot)
2. **Reverse sorted array** (with first element as pivot)
3. **All elements equal**

**Why O(n²)?**

When pivot is always the smallest or largest element:

```
Partition 1: [8] | [3, 1, 7, 0, 10, 2]  → n operations
Partition 2: [3] | [1, 7, 0, 10, 2]     → n-1 operations
Partition 3: [1] | [7, 0, 10, 2]        → n-2 operations
...
Partition n: [0] |                       → 1 operation

Total: n + (n-1) + (n-2) + ... + 1 = n(n+1)/2 ≈ n²/2 = O(n²)
```

**Recursion Tree:**

```
Instead of balanced:        We get unbalanced:

      [n]                        [n]
     ↙   ↘                        ↓
  [n/2] [n/2]                   [n-1]
   ↙↘    ↙↘                       ↓
  ... (log n levels)            [n-2]
                                  ↓
                                 ... (n levels)
```

### Space Complexity

**Space Complexity: O(1)** (excluding recursion stack)

**Why O(1)?**
- No auxiliary arrays created
- All sorting done in-place
- Only a constant amount of extra variables (i, j, pivot)

**Recursion Stack Space: O(log n) average, O(n) worst**
- Each recursive call uses stack space
- Best/Average: O(log n) depth
- Worst: O(n) depth

### Complexity Summary Table

| Case | Time Complexity | Space Complexity | When it Occurs |
|------|----------------|------------------|----------------|
| **Best** | O(n log n) | O(log n) stack | Balanced partitions |
| **Average** | O(n log n) | O(log n) stack | Random data |
| **Worst** | O(n²) | O(n) stack | Sorted/reverse sorted |

---

## 7. Quick Sort vs Merge Sort

### Detailed Comparison

| Feature | Quick Sort | Merge Sort |
|---------|-----------|------------|
| **Algorithm Type** | Divide and Conquer | Divide and Conquer |
| **Best Time** | O(n log n) | O(n log n) |
| **Average Time** | O(n log n) | O(n log n) |
| **Worst Time** | O(n²) | O(n log n) |
| **Space (Auxiliary)** | O(1) | O(n) |
| **Space (Stack)** | O(log n) avg, O(n) worst | O(log n) |
| **Stability** | Not stable | Stable |
| **In-place** | Yes | No |
| **Partition Method** | Pivot-based | Mid-point split |
| **Merge Required** | No | Yes (extra work) |

### Stability Explanation

**Stable Sort:** Maintains relative order of equal elements.

```javascript
// Input with equal values marked
[3a, 2, 3b, 1]

// Stable sort preserves order of 3a and 3b
[1, 2, 3a, 3b]  ✓ Merge Sort

// Unstable may reverse order
[1, 2, 3b, 3a]  ? Quick Sort
```

### When to Use Quick Sort

✅ **Use Quick Sort when:**
- Memory is limited (in-place sorting needed)
- Average case performance is acceptable
- Data is randomly distributed
- Stability is not required
- Fast average performance is priority

### When to Use Merge Sort

✅ **Use Merge Sort when:**
- Consistent O(n log n) time is critical
- Stability is required
- Extra O(n) space is available
- Dealing with linked lists
- Worst-case guarantee needed

### Real-World Applications

**Quick Sort is used in:**
- Programming language libraries:
  - JavaScript's `Array.sort()` (V8 engine uses modified Quick Sort)
  - Java's `Arrays.sort()` for primitives
  - C++ STL's `std::sort()`
- Database query optimization
- File system organization

**Merge Sort is used in:**
- Java's `Arrays.sort()` for objects (stability needed)
- External sorting (sorting data larger than memory)
- Linked list sorting
- Stable sorting requirements

### Performance Comparison

```
Dataset: 1 million random integers

Quick Sort:
- Best case: ~50-60 ms
- Average: ~70-80 ms
- Worst case: ~5000 ms (sorted input)

Merge Sort:
- All cases: ~80-90 ms (consistent)
```

---

## 8. Key Takeaways

### Essential Concepts

1. **Pivot is Key**
   - The pivot element determines partition quality
   - Poor pivot choice leads to worst-case performance
   - Good pivot choice leads to balanced partitions

2. **In-Place Sorting**
   - Quick Sort modifies the original array
   - No extra array needed for sorting
   - Space efficient compared to Merge Sort

3. **Not Stable**
   - Equal elements may be reordered
   - Use Merge Sort if stability is required

4. **Fast in Practice**
   - Despite O(n²) worst case, Quick Sort is fast on average
   - Real-world data is usually random
   - Modern implementations use optimizations

### Algorithm Pattern

```
QuickSort(arr, first, last):
  IF first >= last:
    RETURN  // Base case
  
  pivotIndex = Partition(arr, first, last)
  
  QuickSort(arr, first, pivotIndex - 1)  // Left
  QuickSort(arr, pivotIndex + 1, last)   // Right
```

### Partition Pattern

```
Partition(arr, first, last):
  pivot = arr[first]
  i = first + 1
  j = last
  
  WHILE i <= j:
    WHILE arr[i] <= pivot: i++
    WHILE arr[j] > pivot: j--
    IF i < j: SWAP(arr[i], arr[j])
  
  SWAP(arr[first], arr[j])
  RETURN j
```

### Common Mistakes to Avoid

❌ **Forgetting boundary checks**
```javascript
while (arr[i] <= pivot) {  // ❌ Can go out of bounds!
  i++;
}

while (i <= last && arr[i] <= pivot) {  // ✓ Safe
  i++;
}
```

❌ **Wrong swap condition**
```javascript
if (i <= j) {  // ❌ Will swap after crossing
  swap(arr, i, j);
}

if (i < j) {  // ✓ Correct
  swap(arr, i, j);
}
```

❌ **Not handling equal elements**
```javascript
while (arr[i] < pivot) {  // ❌ Infinite loop with duplicates
  i++;
}

while (arr[i] <= pivot) {  // ✓ Handles duplicates
  i++;
}
```

❌ **Wrong final swap**
```javascript
swap(arr, first, i);  // ❌ Wrong index

swap(arr, first, j);  // ✓ Correct
```

### Optimization Techniques

1. **Random Pivot Selection**
   ```javascript
   let randomIndex = first + Math.floor(Math.random() * (last - first + 1));
   swap(arr, first, randomIndex);  // Move random element to first
   ```

2. **Median-of-Three Pivot**
   ```javascript
   let mid = Math.floor((first + last) / 2);
   let median = medianOfThree(arr[first], arr[mid], arr[last]);
   // Use median as pivot
   ```

3. **Insertion Sort for Small Subarrays**
   ```javascript
   if (last - first < 10) {
     insertionSort(arr, first, last);
     return;
   }
   ```

4. **Three-Way Partitioning** (for many duplicates)
   - Partition into: < pivot, = pivot, > pivot
   - Skip equal elements in recursive calls

### Debugging Tips

1. **Print array state at each partition**
   ```javascript
   console.log(`Before: [${arr}]`);
   let pivotIndex = findPivotIndex(arr, first, last);
   console.log(`After: [${arr}], pivot at ${pivotIndex}`);
   ```

2. **Trace pointer movements**
   ```javascript
   console.log(`i=${i}, j=${j}, arr[i]=${arr[i]}, arr[j]=${arr[j]}`);
   ```

3. **Verify partition correctness**
   ```javascript
   // After partition, check:
   // All left elements <= pivot
   // All right elements >= pivot
   ```

### Practice Problems

1. **Basic Implementation**
   - Implement Quick Sort with first element as pivot
   - Implement with last element as pivot
   - Implement with random pivot

2. **Variations**
   - Implement three-way Quick Sort
   - Quick Sort with insertion sort for small subarrays
   - Iterative Quick Sort (using stack instead of recursion)

3. **Analysis**
   - Count number of comparisons
   - Count number of swaps
   - Measure actual runtime on different inputs

4. **Applications**
   - Find kth smallest element using Quick Select
   - Sort array of objects by custom comparator
   - Partition array based on custom predicate

### Interview Tips

**Common Questions:**
1. "Explain how Quick Sort works"
   - Focus on pivot and partition
   - Walk through example

2. "What's the time complexity?"
   - Average: O(n log n)
   - Worst: O(n²)
   - Explain why

3. "Quick Sort vs Merge Sort?"
   - Compare time, space, stability
   - Mention use cases

4. "How to avoid worst case?"
   - Random pivot
   - Median-of-three
   - Explain impact

**What interviewers look for:**
- Understanding of partition logic
- Correct pointer movement
- Boundary condition handling
- Recursion base case
- Complexity analysis

### Summary Formulas

**Time Complexity:**
```
Best/Average: T(n) = 2T(n/2) + O(n) = O(n log n)
Worst: T(n) = T(n-1) + O(n) = O(n²)
```

**Space Complexity:**
```
Auxiliary: O(1)
Stack: O(log n) average, O(n) worst
```

**Key Inequality:**
```
If pivot divides array as (k, n-k-1):
Best case: k ≈ n/2 (balanced)
Worst case: k = 0 or k = n-1 (unbalanced)
```

---

## Resources for Further Learning

- Visualize Quick Sort: VisualAlgo, Algorithm Visualizer
- Practice: LeetCode, HackerRank sorting problems
- Advanced: Study introsort (hybrid of Quick Sort and Heap Sort)
- Read: "Introduction to Algorithms" by CLRS

---

## Final Tips

1. **Practice implementing from scratch**
   - Don't just copy code
   - Write it multiple times
   - Test with different inputs

2. **Understand pointer logic deeply**
   - Trace through manually
   - Draw diagrams
   - Understand why conditions work

3. **Test edge cases**
   - Empty array
   - Single element
   - All duplicates
   - Already sorted
   - Reverse sorted

4. **Compare with other algorithms**
   - Implement Merge Sort too
   - Compare performance
   - Understand trade-offs

5. **Master the analysis**
   - Derive time complexity yourself
   - Understand recursion tree
   - Explain to someone else

**Remember:** Quick Sort is one of the most important algorithms in computer science. Master it well!

---

**Happy Coding! 🚀**

---

**End of Study Notes**
