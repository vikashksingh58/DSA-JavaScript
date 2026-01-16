# Merge Sort Study Notes
**Sharians Coding School - DSA Series**

---

## Table of Contents
1. [What is Merge Sort?](#what-is-merge-sort)
2. [Divide and Conquer Strategy](#divide-and-conquer-strategy)
3. [The Conquer Part: Merging](#the-conquer-part-merging)
4. [The Divide Part: Splitting](#the-divide-part-splitting)
5. [Complete Algorithm](#complete-algorithm)
6. [Complexity Analysis](#complexity-analysis)
7. [Implementation Guide](#implementation-guide)
8. [Common Mistakes](#common-mistakes)
9. [Practice Problems](#practice-problems)

---

## What is Merge Sort?

### Definition
**Merge Sort** is a powerful, efficient sorting algorithm based on the **Divide and Conquer** paradigm that guarantees O(n log n) time complexity in all cases.

### Key Characteristics
✅ **Stable sorting** algorithm  
✅ **Guaranteed O(n log n)** performance  
✅ **Works on any data** (doesn't require sorted input)  
✅ **Predictable** performance (best = average = worst case)  
❌ **Requires O(n) extra space**

### Why is it Powerful?
- More efficient than O(n²) algorithms (Bubble, Selection, Insertion)
- Consistent performance regardless of input
- Foundation for understanding advanced algorithms
- Frequently asked in technical interviews

---

## Divide and Conquer Strategy

### Two Main Phases

#### 1. **DIVIDE** Phase
- Split the array into **two halves**
- Continue recursively until each piece has **1 element**
- Single elements are inherently sorted (base case)

#### 2. **CONQUER** Phase (Merging)
- **Merge** two sorted halves into one sorted array
- Happens during **backtracking** from recursion
- Uses a **temporary array** to hold merged results

### Visual Overview
```
DIVIDE (Top-down):
[8, 2, 1, 9, 5, 12, 4, 20]
         ↓
[8, 2, 1, 9]    [5, 12, 4, 20]
    ↓               ↓
[8, 2] [1, 9]   [5, 12] [4, 20]
  ↓       ↓       ↓       ↓
[8] [2] [1] [9] [5] [12] [4] [20]  ← Base case reached

CONQUER (Bottom-up - during backtracking):
[8] [2] [1] [9] [5] [12] [4] [20]
  ↓       ↓       ↓       ↓
[2, 8] [1, 9]   [5, 12] [4, 20]
    ↓               ↓
[1, 2, 8, 9]    [4, 5, 12, 20]
         ↓
[1, 2, 4, 5, 8, 9, 12, 20]  ← Fully sorted
```

---

## The Conquer Part: Merging

### Why Learn Merging First?
Understanding merging is the **foundation** of Merge Sort. If you master merging, the divide part becomes straightforward.

### Problem: Merge Two Sorted Partitions
Given an array with two sorted partitions, merge them into one sorted partition.

**Example Array**: `[1, 2, 8, 9, 4, 5, 12, 20]`
- **Left partition** (indices 0-3): `[1, 2, 8, 9]` ✓ sorted
- **Right partition** (indices 4-7): `[4, 5, 12, 20]` ✓ sorted
- **Goal**: Merge into `[1, 2, 4, 5, 8, 9, 12, 20]`

### Merging Strategy: Three Pointers

| Pointer | Purpose | Initial Value |
|---------|---------|---------------|
| `i` | Traverse left partition | `first` |
| `j` | Traverse right partition | `mid + 1` |
| `k` | Index in temporary array | `0` |

### Merging Algorithm Steps

#### Step 1: Initialize
```javascript
let tempArray = new Array(last - first + 1);
let i = first;        // Start of left partition
let j = mid + 1;      // Start of right partition
let k = 0;            // Temp array index
```

#### Step 2: Compare and Copy
```
While both partitions have elements:
    Compare arr[i] and arr[j]
    Copy smaller element to tempArray[k]
    Increment corresponding pointer (i or j) and k
```

#### Step 3: Copy Remaining Elements
```
If left partition has remaining elements:
    Copy them to tempArray
    
If right partition has remaining elements:
    Copy them to tempArray
```

#### Step 4: Copy Back to Original Array
```
Copy all elements from tempArray back to arr[first...last]
```

### Detailed Merging Example

**Array**: `[1, 2, 8, 9, 4, 5, 12, 20]`  
**first** = 0, **mid** = 3, **last** = 7

```
Initial state:
i = 0 (points to 1)
j = 4 (points to 4)
k = 0

Step 1: Compare arr[0]=1 vs arr[4]=4
1 < 4 → temp[0] = 1, i=1, k=1

Step 2: Compare arr[1]=2 vs arr[4]=4
2 < 4 → temp[1] = 2, i=2, k=2

Step 3: Compare arr[2]=8 vs arr[4]=4
8 > 4 → temp[2] = 4, j=5, k=3

Step 4: Compare arr[2]=8 vs arr[5]=5
8 > 5 → temp[3] = 5, j=6, k=4

Step 5: Compare arr[2]=8 vs arr[6]=12
8 < 12 → temp[4] = 8, i=3, k=5

Step 6: Compare arr[3]=9 vs arr[6]=12
9 < 12 → temp[5] = 9, i=4, k=6

Step 7: i > mid (left exhausted)
Copy remaining: temp[6] = 12, temp[7] = 20

Result: temp = [1, 2, 4, 5, 8, 9, 12, 20]
Copy back to original array
```

### Merging Code Implementation

```javascript
function merge(arr, first, mid, last) {
    // Step 1: Create temporary array
    let tempSize = last - first + 1;
    let temp = new Array(tempSize);
    
    // Step 2: Initialize pointers
    let i = first;      // Left partition start
    let j = mid + 1;    // Right partition start
    let k = 0;          // Temp array index
    
    // Step 3: Compare and copy smaller elements
    while (i <= mid && j <= last) {
        if (arr[i] <= arr[j]) {
            temp[k] = arr[i];
            i++;
        } else {
            temp[k] = arr[j];
            j++;
        }
        k++;
    }
    
    // Step 4: Copy remaining from left partition
    while (i <= mid) {
        temp[k] = arr[i];
        i++;
        k++;
    }
    
    // Step 5: Copy remaining from right partition
    while (j <= last) {
        temp[k] = arr[j];
        j++;
        k++;
    }
    
    // Step 6: Copy back to original array
    for (let idx = 0; idx < tempSize; idx++) {
        arr[first + idx] = temp[idx];
    }
}
```

---

## The Divide Part: Splitting

### Division Strategy
Split the array at the **midpoint**, similar to binary search.

### Key Variables

| Variable | Meaning |
|----------|---------|
| `first` | Starting index of current segment |
| `last` | Ending index of current segment |
| `mid` | Midpoint: `Math.floor((first + last) / 2)` |

### Recursive Division Process

```
Initial call: mergeSort(arr, 0, n-1)

If first >= last:
    return  // Base case: 1 or 0 elements
    
Calculate mid = Math.floor((first + last) / 2)

Recursively divide left half:
    mergeSort(arr, first, mid)
    
Recursively divide right half:
    mergeSort(arr, mid + 1, last)
    
Merge the two sorted halves:
    merge(arr, first, mid, last)
```

### Division Tree Example

**Array**: `[8, 2, 1, 9, 5, 12, 4, 20]`

```
Level 0: [8, 2, 1, 9, 5, 12, 4, 20]  first=0, last=7, mid=3
              ↓
         _____|_____
        |           |
Level 1: [8,2,1,9]  [5,12,4,20]     mid=1, mid=5
         ↓          ↓
      ___|___    ___|___
     |       |  |       |
Level 2: [8,2] [1,9] [5,12] [4,20]  mid=0,2,4,6
         ↓   ↓   ↓  ↓   ↓  ↓   ↓  ↓
Level 3: [8][2][1][9][5][12][4][20] Base case reached!
```

### Base Case
```
When first >= last:
    - Segment has 1 or 0 elements
    - Already sorted by definition
    - Return immediately
```

---

## Complete Algorithm

### Full Merge Sort Implementation

```javascript
function mergeSort(arr, first = 0, last = arr.length - 1) {
    // Base case: 1 or fewer elements
    if (first >= last) {
        return;
    }
    
    // Calculate midpoint
    let mid = Math.floor((first + last) / 2);
    
    // Recursively sort left half
    mergeSort(arr, first, mid);
    
    // Recursively sort right half
    mergeSort(arr, mid + 1, last);
    
    // Merge the two sorted halves
    merge(arr, first, mid, last);
}

function merge(arr, first, mid, last) {
    let temp = new Array(last - first + 1);
    let i = first;
    let j = mid + 1;
    let k = 0;
    
    // Compare and merge
    while (i <= mid && j <= last) {
        if (arr[i] <= arr[j]) {
            temp[k++] = arr[i++];
        } else {
            temp[k++] = arr[j++];
        }
    }
    
    // Copy remaining from left
    while (i <= mid) {
        temp[k++] = arr[i++];
    }
    
    // Copy remaining from right
    while (j <= last) {
        temp[k++] = arr[j++];
    }
    
    // Copy back to original
    for (let idx = 0; idx < temp.length; idx++) {
        arr[first + idx] = temp[idx];
    }
}
```

### Usage Example

```javascript
let arr = [8, 2, 1, 9, 5, 12, 4, 20];
console.log("Before:", arr);

mergeSort(arr);
console.log("After:", arr);

// Output:
// Before: [8, 2, 1, 9, 5, 12, 4, 20]
// After:  [1, 2, 4, 5, 8, 9, 12, 20]
```

---

## Complexity Analysis

### Time Complexity: O(n log n) ⭐

#### Why O(n log n)?

**Divide Part**: O(log n)
- Array split in half each time
- Number of levels = log₂(n)
- Similar to binary search tree height

**Conquer Part**: O(n)
- At each level, all n elements are processed during merging
- Each element is compared and copied once per level

**Total**: O(n) × O(log n) = **O(n log n)**

#### Detailed Analysis

```
Level 0: 1 merge of n elements        = n operations
Level 1: 2 merges of n/2 elements     = n operations
Level 2: 4 merges of n/4 elements     = n operations
...
Level log n: n merges of 1 element    = n operations

Total levels: log₂(n)
Work per level: n
Total work: n × log₂(n) = O(n log n)
```

#### Example: n = 8

```
Array size: 8 elements
Levels: log₂(8) = 3

Level 0: [8,2,1,9,5,12,4,20]          8 operations
         ↓
Level 1: [8,2,1,9] + [5,12,4,20]      4+4 = 8 operations
         ↓
Level 2: [8,2][1,9] + [5,12][4,20]    2+2+2+2 = 8 operations
         ↓
Level 3: [8][2][1][9][5][12][4][20]   Base case (no merging)

Total: 3 levels × 8 operations = 24 operations ≈ 8 log₂(8)
```

### Space Complexity: O(n)

**Why O(n) space?**
- Temporary array needed for merging
- Size of temp array = size of segment being merged
- In worst case, merging entire array requires O(n) space

**Space Usage**:
```
Main array: O(n)
Temp arrays during merge: O(n)
Recursion call stack: O(log n)
Total auxiliary space: O(n)
```

### Complexity Comparison Table

| Algorithm | Best Case | Average Case | Worst Case | Space |
|-----------|-----------|--------------|------------|-------|
| **Bubble Sort** | O(n) | O(n²) | O(n²) | O(1) |
| **Selection Sort** | O(n²) | O(n²) | O(n²) | O(1) |
| **Insertion Sort** | O(n) | O(n²) | O(n²) | O(1) |
| **Merge Sort** ⭐ | O(n log n) | O(n log n) | O(n log n) | O(n) |
| **Quick Sort** | O(n log n) | O(n log n) | O(n²) | O(log n) |

### Performance Visualization

| Array Size | Merge Sort | Bubble Sort |
|------------|------------|-------------|
| 10 | ~33 ops | ~100 ops |
| 100 | ~664 ops | ~10,000 ops |
| 1,000 | ~9,966 ops | ~1,000,000 ops |
| 10,000 | ~132,877 ops | ~100,000,000 ops |

---

## Implementation Guide

### Step-by-Step Implementation

#### Phase 1: Implement Merging First
1. Write the `merge()` function
2. Test it with pre-divided sorted partitions
3. Verify correct merging with various test cases

#### Phase 2: Add Division
1. Write the recursive `mergeSort()` function
2. Calculate mid correctly
3. Make recursive calls for left and right halves
4. Call merge after recursive calls

#### Phase 3: Test Thoroughly
1. Test with small arrays (2-8 elements)
2. Test edge cases (empty, single element)
3. Test with duplicates
4. Test with already sorted arrays
5. Test with reverse sorted arrays

### Debugging Tips

#### Print Intermediate States
```javascript
function merge(arr, first, mid, last) {
    console.log(`Merging [${first}...${mid}] and [${mid+1}...${last}]`);
    console.log(`Before: [${arr.slice(first, last+1)}]`);
    
    // ... merging logic ...
    
    console.log(`After: [${arr.slice(first, last+1)}]`);
}
```

#### Verify Pointers
```javascript
// Check boundary conditions
if (i > mid) console.log("Left partition exhausted");
if (j > last) console.log("Right partition exhausted");
```

#### Trace Recursion
```javascript
function mergeSort(arr, first, last, depth = 0) {
    let indent = "  ".repeat(depth);
    console.log(`${indent}Sort [${first}...${last}]`);
    
    if (first >= last) {
        console.log(`${indent}Base case`);
        return;
    }
    
    // ... rest of code ...
}
```

---

## Common Mistakes to Avoid

### Mistake 1: Wrong Mid Calculation
```javascript
// ❌ WRONG - Can cause integer overflow
let mid = (first + last) / 2;

// ✅ CORRECT - Use floor and safe formula
let mid = Math.floor(first + (last - first) / 2);
```

### Mistake 2: Incorrect Base Case
```javascript
// ❌ WRONG - Infinite recursion
if (first < last) {
    return;
}

// ✅ CORRECT
if (first >= last) {
    return;
}
```

### Mistake 3: Wrong Pointer Initialization
```javascript
// ❌ WRONG
let i = 0;           // Should be first
let j = mid;         // Should be mid + 1

// ✅ CORRECT
let i = first;
let j = mid + 1;
```

### Mistake 4: Forgetting to Copy Back
```javascript
// ❌ WRONG - Temp array created but not copied back
function merge(arr, first, mid, last) {
    let temp = [];
    // ... merging logic ...
    // Missing: copy temp back to arr
}

// ✅ CORRECT - Always copy back
for (let idx = 0; idx < temp.length; idx++) {
    arr[first + idx] = temp[idx];
}
```

### Mistake 5: Incorrect Remaining Elements Logic
```javascript
// ❌ WRONG - Might copy wrong elements
while (i < arr.length) {  // Should be i <= mid
    temp[k++] = arr[i++];
}

// ✅ CORRECT
while (i <= mid) {
    temp[k++] = arr[i++];
}

while (j <= last) {
    temp[k++] = arr[j++];
}
```

### Mistake 6: Calling Merge Before Recursion
```javascript
// ❌ WRONG - Merge before dividing
function mergeSort(arr, first, last) {
    if (first >= last) return;
    
    let mid = Math.floor((first + last) / 2);
    merge(arr, first, mid, last);  // Wrong order!
    mergeSort(arr, first, mid);
    mergeSort(arr, mid + 1, last);
}

// ✅ CORRECT - Divide first, then merge
function mergeSort(arr, first, last) {
    if (first >= last) return;
    
    let mid = Math.floor((first + last) / 2);
    mergeSort(arr, first, mid);        // Divide left
    mergeSort(arr, mid + 1, last);     // Divide right
    merge(arr, first, mid, last);      // Then merge
}
```

---

## Prerequisites

### Essential Concepts to Understand First

1. **Merging Two Sorted Arrays** ⭐ CRITICAL
   - Practice standalone merging problems
   - Master the two-pointer technique

2. **Recursion** ⭐ CRITICAL
   - Understand base cases
   - Comfortable with backtracking
   - Know how recursive calls build up and return

3. **Binary Search Logic**
   - Calculating midpoint
   - Dividing ranges

4. **Array Manipulation**
   - Index handling
   - Creating and copying arrays

### Learning Sequence
```
1. Master recursion basics
   ↓
2. Practice merging two sorted arrays
   ↓
3. Understand divide and conquer concept
   ↓
4. Code merge function separately
   ↓
5. Add recursive division
   ↓
6. Test and debug complete algorithm
```

---

## Real-World Applications

### 1. External Sorting
- Sorting data too large to fit in memory
- Disk-based sorting in databases
- Processing log files

### 2. Inversion Count
- Count pairs where arr[i] > arr[j] and i < j
- Used in collaborative filtering

### 3. Stable Sorting Requirement
- When order of equal elements matters
- Sorting records with multiple fields

### 4. Parallel Processing
- Merge sort is easily parallelizable
- Each half can be sorted independently
- Used in multi-threaded applications

### 5. Linked List Sorting
- Merge sort is efficient for linked lists
- No random access needed
- O(1) space for linked lists

---

## Practice Problems

### Beginner Level
1. ✅ Implement merge function
2. ✅ Implement merge sort
3. Sort array in descending order
4. Count inversions in array
5. Merge k sorted arrays

### Intermediate Level
6. Sort linked list using merge sort
7. Count smaller elements on right
8. Reverse pairs (arr[i] > 2*arr[j])
9. Sort array with custom comparator
10. Find median in stream

### Advanced Level
11. External merge sort
12. Parallel merge sort
13. In-place merge sort (reduce space)
14. Merge sort with limited extra space
15. Sort nearly sorted array

---

## Study Tips

### Understanding Merge Sort

1. **Start with merging** - Master this first
2. **Visualize recursion tree** - Draw it on paper
3. **Trace small examples** - Use 4-8 elements
4. **Focus on backtracking** - Understand when merging happens
5. **Print intermediate states** - See the algorithm in action

### Memory Aid: "DMB"
- **D**ivide: Split at mid
- **M**erge: Combine sorted halves
- **B**acktrack: Merge during return

### Practice Strategy
```
Day 1: Implement and test merge function
Day 2: Add recursive division
Day 3: Debug with various test cases
Day 4: Optimize and handle edge cases
Day 5: Solve related problems
```

---

## Interview Preparation

### Common Interview Questions

1. **Explain merge sort algorithm**
   - Describe divide and conquer
   - Walk through example

2. **What's the time complexity and why?**
   - O(n log n) in all cases
   - Explain levels × work per level

3. **What's the space complexity?**
   - O(n) for temporary arrays
   - Trade-off for guaranteed performance

4. **When would you use merge sort?**
   - Need stable sort
   - Need guaranteed O(n log n)
   - Sorting linked lists
   - External sorting

5. **Merge sort vs Quick sort?**
   - Merge: Guaranteed O(n log n), needs O(n) space
   - Quick: Average O(n log n), worst O(n²), O(log n) space

6. **Can you implement in-place merge sort?**
   - Possible but complex
   - Loses simplicity advantage

### Problem-Solving Template

```javascript
// Template for merge sort problems
function mergeSort(arr, first, last) {
    // 1. Base case
    if (first >= last) return;
    
    // 2. Divide
    let mid = Math.floor(first + (last - first) / 2);
    
    // 3. Conquer (recursive calls)
    mergeSort(arr, first, mid);
    mergeSort(arr, mid + 1, last);
    
    // 4. Combine (merge)
    merge(arr, first, mid, last);
}

function merge(arr, first, mid, last) {
    // 1. Create temp array
    // 2. Initialize pointers
    // 3. Compare and copy
    // 4. Copy remaining
    // 5. Copy back to original
}
```

---

## Quick Reference

### Algorithm Summary
```
MERGE SORT (Divide and Conquer)

Function mergeSort(arr, first, last):
    if first >= last:
        return  // Base case
    
    mid = floor((first + last) / 2)
    mergeSort(arr, first, mid)      // Sort left
    mergeSort(arr, mid+1, last)     // Sort right
    merge(arr, first, mid, last)    // Merge sorted halves

Function merge(arr, first, mid, last):
    Create temp array
    i = first, j = mid+1, k = 0
    
    while i <= mid AND j <= last:
        if arr[i] <= arr[j]:
            temp[k++] = arr[i++]
        else:
            temp[k++] = arr[j++]
    
    Copy remaining from left (i to mid)
    Copy remaining from right (j to last)
    Copy temp back to arr[first...last]
```

### Complexity Cheat Sheet
| Aspect | Value |
|--------|-------|
| Best Time | O(n log n) |
| Average Time | O(n log n) |
| Worst Time | O(n log n) |
| Space | O(n) |
| Stable | Yes |
| In-place | No |

---

## Lecture Timeline

| Time | Topic |
|------|-------|
| 00:00 - 01:00 | Introduction to Merge Sort |
| 01:00 - 02:18 | Understanding the Conquer (Merge) part |
| 02:18 - 08:42 | Visualizing merging process |
| 08:42 - 15:39 | Merging code implementation |
| 15:39 - 19:19 | Transition to Divide part |
| 19:19 - 25:25 | Recursive divide process |
| 25:25 - 30:22 | Backtracking and merging |
| 30:22 - 34:07 | Final algorithm outline |
| 34:07 - 36:31 | Implementation details |
| 36:31 - 37:22 | Complexity analysis and closing |

---

## Key Takeaways

### Why Merge Sort is Important
1. **Guaranteed performance** - Always O(n log n)
2. **Stable algorithm** - Preserves order of equal elements
3. **Foundation concept** - Understanding divide and conquer
4. **Interview favorite** - Frequently asked in coding interviews
5. **Practical applications** - External sorting, parallel processing

### When to Use Merge Sort
✅ Need guaranteed O(n log n) performance  
✅ Stability is required  
✅ Sorting linked lists  
✅ External sorting (large datasets)  
✅ Have extra O(n) space available  

### When NOT to Use Merge Sort
❌ Limited memory (use quick sort or heap sort)  
❌ Small datasets (simple sorts like insertion sort faster)  
❌ Need in-place sorting (use quick sort)  

---

**Remember**: Master merging first, then division becomes easy! 🚀

**Practice Mantra**: "Divide, Recurse, Merge, Repeat"