# Binary Search Study Notes
**Sharians Coding School - DSA Series**

---

## Table of Contents
1. [What is Binary Search?](#what-is-binary-search)
2. [How Binary Search Works](#how-binary-search-works)
3. [Algorithm Steps](#algorithm-steps)
4. [Implementation](#implementation)
5. [Complexity Analysis](#complexity-analysis)
6. [Comparison with Linear Search](#comparison-with-linear-search)
7. [Common Mistakes](#common-mistakes)
8. [Practice Problems](#practice-problems)

---

## What is Binary Search?

### Definition
**Binary Search** is a searching algorithm that efficiently finds a target element in a **sorted** dataset by repeatedly dividing the search space in half.

### Key Requirements
✅ **Data MUST be sorted** (ascending or descending order)
❌ Binary search does NOT work on unsorted data

### Why is it Fast?
- **Eliminates half** of the remaining elements in each step
- **Logarithmic time complexity**: O(log n)
- **Most efficient** searching algorithm for sorted data

---

## How Binary Search Works

### Core Concept
Instead of checking each element sequentially (like linear search), binary search:
1. Looks at the **middle element**
2. **Compares** it with the target
3. **Eliminates** half of the search space based on comparison
4. **Repeats** until target is found or search space is empty

### Visual Example
```
Sorted Array: [10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110]
Indices:       0   1   2   3   4   5   6   7   8    9   10

Target = 67 (not in array, for demonstration)

Step 1: Check middle
first = 0, last = 10
mid = (0 + 10) / 2 = 5
array[5] = 60
60 < 67 → Search RIGHT half

Step 2: Check middle of right half
first = 6, last = 10
mid = (6 + 10) / 2 = 8
array[8] = 90
90 > 67 → Search LEFT half (of current range)

Step 3: Check middle of remaining
first = 6, last = 7
mid = (6 + 7) / 2 = 6
array[6] = 70
70 > 67 → Search LEFT half

Step 4: Only one element left
first = 6, last = 5
first > last → Target NOT FOUND
```

---

## Algorithm Steps

### Step-by-Step Process

| Step | Action | Description |
|------|--------|-------------|
| **1** | **Initialize pointers** | Set `first = 0`, `last = array.length - 1` |
| **2** | **Calculate mid** | `mid = first + (last - first) / 2` |
| **3** | **Compare** | Check `array[mid]` vs `target` |
| **4** | **Update pointers** | Adjust search range based on comparison |
| **5** | **Repeat** | Continue until found or `first > last` |
| **6** | **Return result** | Index if found, -1 if not found |

### Three Comparison Cases

#### Case 1: Target EQUALS Mid Element
```
array[mid] == target
✅ FOUND! Return mid
```

#### Case 2: Target GREATER than Mid Element
```
array[mid] < target
Target is in RIGHT half
→ Update: first = mid + 1
→ Discard left half (including mid)
```

#### Case 3: Target SMALLER than Mid Element
```
array[mid] > target
Target is in LEFT half
→ Update: last = mid - 1
→ Discard right half (including mid)
```

### Detailed Example: Finding 67

**Array**: [10, 25, 30, 45, 50, 67, 80, 95, 100, 200, 300]

```
Iteration 1:
first = 0, last = 10
mid = 5, array[5] = 67
67 == 67 → FOUND at index 5! ✅
```

### Detailed Example: Finding 25

**Array**: [10, 25, 30, 45, 50, 67, 80, 95, 100, 200, 300]

```
Iteration 1:
first = 0, last = 10
mid = 5, array[5] = 67
25 < 67 → Search LEFT
Update: last = 4

Iteration 2:
first = 0, last = 4
mid = 2, array[2] = 30
25 < 30 → Search LEFT
Update: last = 1

Iteration 3:
first = 0, last = 1
mid = 0, array[0] = 10
25 > 10 → Search RIGHT
Update: first = 1

Iteration 4:
first = 1, last = 1
mid = 1, array[1] = 25
25 == 25 → FOUND at index 1! ✅
```

### Termination Condition
```
Loop continues while: first <= last

Terminates when: first > last
Meaning: Search space is exhausted, target not found
```

---

## Implementation

### Basic Implementation
```javascript
function binarySearch(arr, target) {
    let first = 0;
    let last = arr.length - 1;
    
    while (first <= last) {
        // Calculate mid
        let mid = Math.floor(first + (last - first) / 2);
        
        // Compare with target
        if (arr[mid] === target) {
            return mid;  // Found!
        } else if (arr[mid] < target) {
            first = mid + 1;  // Search right half
        } else {
            last = mid - 1;   // Search left half
        }
    }
    
    return -1;  // Not found
}
```

### Using the Function
```javascript
let arr = [10, 25, 30, 45, 50, 67, 80, 95, 100, 200, 300];

// Test case 1: Element present
let result1 = binarySearch(arr, 67);
if (result1 !== -1) {
    console.log(`Target found at index ${result1}`);
} else {
    console.log("Not Found");
}
// Output: Target found at index 5

// Test case 2: Element not present
let result2 = binarySearch(arr, 75);
if (result2 !== -1) {
    console.log(`Target found at index ${result2}`);
} else {
    console.log("Not Found");
}
// Output: Not Found
```

### Recursive Implementation
```javascript
function binarySearchRecursive(arr, target, first = 0, last = arr.length - 1) {
    // Base case: search space exhausted
    if (first > last) {
        return -1;
    }
    
    // Calculate mid
    let mid = Math.floor(first + (last - first) / 2);
    
    // Check if found
    if (arr[mid] === target) {
        return mid;
    }
    
    // Recursive cases
    if (arr[mid] < target) {
        // Search right half
        return binarySearchRecursive(arr, target, mid + 1, last);
    } else {
        // Search left half
        return binarySearchRecursive(arr, target, first, mid - 1);
    }
}
```

---

## Mid Calculation: Critical Detail

### Two Formulas

#### ❌ Naive Formula (Not Recommended)
```javascript
mid = (first + last) / 2
```

**Problem**: Can cause **integer overflow** in languages like Java, C++

**Example of Overflow**:
```java
// In Java with 32-bit integers
int first = 2000000000;  // Large index
int last = 2000000000;
int mid = (first + last) / 2;  // OVERFLOW! Negative result
```

#### ✅ Recommended Formula (Safe)
```javascript
mid = first + (last - first) / 2
```

**Why it's better**:
- **Prevents integer overflow** in all languages
- Mathematically equivalent but safer
- **Best practice** even in JavaScript/Python

### Detailed Comparison

| Formula | Pros | Cons |
|---------|------|------|
| `(first + last) / 2` | Simple, intuitive | Integer overflow in Java/C++ |
| `first + (last - first) / 2` | Safe, no overflow | Slightly more complex |

### Mathematical Proof (They're Equivalent)
```
first + (last - first) / 2
= first + last/2 - first/2
= first/2 + last/2
= (first + last) / 2

They give the same result, but the first prevents overflow!
```

---

## Complexity Analysis

### Time Complexity: O(log n) ⭐

#### Why Logarithmic?
Each iteration **halves** the search space:
```
n elements → n/2 → n/4 → n/8 → ... → 1

Number of steps = log₂(n)
```

#### Example Calculations

| Array Size (n) | Max Steps (log₂ n) |
|----------------|-------------------|
| 10 | ~4 |
| 100 | ~7 |
| 1,000 | ~10 |
| 1,000,000 | ~20 |
| 1,000,000,000 | ~30 |

#### Derivation
```
After k steps: n / 2^k elements remain
When search ends: n / 2^k = 1
Therefore: 2^k = n
Taking log: k = log₂(n)
```

### Space Complexity

| Implementation | Space Complexity | Reason |
|----------------|------------------|--------|
| **Iterative** | O(1) | Only uses a few variables |
| **Recursive** | O(log n) | Call stack depth = log n |

**Iterative is preferred** for space efficiency.

---

## Comparison with Linear Search

### Linear Search
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

### Performance Comparison

| Metric | Linear Search | Binary Search |
|--------|---------------|---------------|
| **Requirements** | Any data | **Sorted data only** |
| **Time Complexity** | O(n) | O(log n) |
| **Space Complexity** | O(1) | O(1) iterative |
| **100 elements (worst)** | 100 steps | ~7 steps |
| **1000 elements (worst)** | 1000 steps | ~10 steps |
| **1,000,000 elements (worst)** | 1,000,000 steps | ~20 steps |

### Visual Comparison

```
For n = 100:

Linear Search:
Step 1: Check index 0
Step 2: Check index 1
Step 3: Check index 2
...
Step 100: Check index 99 ← Worst case

Binary Search:
Step 1: Check index 50 (mid of 0-99)
Step 2: Check index 25 (mid of 0-49)
Step 3: Check index 12 (mid of 0-24)
Step 4: Check index 6 (mid of 0-11)
Step 5: Check index 3 (mid of 0-5)
Step 6: Check index 1 (mid of 0-2)
Step 7: Check index 0 or 2 ← Worst case
```

### When to Use Which?

| Use Linear Search | Use Binary Search |
|-------------------|-------------------|
| Unsorted data | Sorted data |
| Small dataset (n < 100) | Large dataset |
| Single search operation | Multiple searches |
| Data changes frequently | Static or infrequently changing data |

---

## Real-World Applications

### 1. Database Queries
**Example**: Finding customer by ID in a sorted database
```
Database with 10 million users
Binary search: ~24 steps maximum
Linear search: 10 million steps maximum
```

### 2. E-commerce Platforms
**Example**: MNTRa (myntra) finding products
- Sorted product IDs
- Fast lookup for millions of products
- Binary search enables instant results

### 3. Dictionary/Phone Book Lookup
- Entries sorted alphabetically
- Binary search mimics how humans search
- Jump to middle, compare, eliminate half

### 4. Version Control Systems
- Finding when a bug was introduced
- Binary search through commit history
- Git bisect uses binary search

### 5. Finding Boundaries
- First occurrence of element
- Last occurrence of element
- Lower bound, upper bound queries

---

## Common Mistakes to Avoid

### Mistake 1: Using on Unsorted Data
```javascript
// ❌ WRONG - Array not sorted
let arr = [50, 10, 90, 30, 70];
binarySearch(arr, 30);  // May return wrong result!

// ✅ CORRECT - Sort first
arr.sort((a, b) => a - b);
binarySearch(arr, 30);  // Now works correctly
```

### Mistake 2: Wrong Mid Calculation
```javascript
// ❌ WRONG - Can overflow in Java/C++
let mid = (first + last) / 2;

// ✅ CORRECT - Safe formula
let mid = first + Math.floor((last - first) / 2);
```

### Mistake 3: Forgetting to Update Pointers
```javascript
// ❌ WRONG - Infinite loop!
if (arr[mid] < target) {
    first = mid;  // Should be mid + 1
}

// ✅ CORRECT
if (arr[mid] < target) {
    first = mid + 1;
}
```

### Mistake 4: Off-by-One Errors
```javascript
// ❌ WRONG - Loop condition
while (first < last) {  // Misses case when first == last
    // ...
}

// ✅ CORRECT
while (first <= last) {  // Includes all cases
    // ...
}
```

### Mistake 5: Forgetting Math.floor()
```javascript
// ❌ WRONG - Decimal index in JavaScript
let mid = first + (last - first) / 2;  // Could be 4.5

// ✅ CORRECT
let mid = Math.floor(first + (last - first) / 2);
```

---

## Binary Search Variations

### 1. First Occurrence
Find the first occurrence of target in array with duplicates.

```javascript
function findFirst(arr, target) {
    let first = 0, last = arr.length - 1;
    let result = -1;
    
    while (first <= last) {
        let mid = Math.floor(first + (last - first) / 2);
        
        if (arr[mid] === target) {
            result = mid;      // Store result
            last = mid - 1;    // Continue searching left
        } else if (arr[mid] < target) {
            first = mid + 1;
        } else {
            last = mid - 1;
        }
    }
    
    return result;
}

// Example
let arr = [1, 2, 2, 2, 3, 4, 5];
findFirst(arr, 2);  // Returns 1 (first occurrence)
```

### 2. Last Occurrence
```javascript
function findLast(arr, target) {
    let first = 0, last = arr.length - 1;
    let result = -1;
    
    while (first <= last) {
        let mid = Math.floor(first + (last - first) / 2);
        
        if (arr[mid] === target) {
            result = mid;      // Store result
            first = mid + 1;   // Continue searching right
        } else if (arr[mid] < target) {
            first = mid + 1;
        } else {
            last = mid - 1;
        }
    }
    
    return result;
}

// Example
let arr = [1, 2, 2, 2, 3, 4, 5];
findLast(arr, 2);  // Returns 3 (last occurrence)
```

### 3. Count Occurrences
```javascript
function countOccurrences(arr, target) {
    let first = findFirst(arr, target);
    if (first === -1) return 0;
    
    let last = findLast(arr, target);
    return last - first + 1;
}

// Example
let arr = [1, 2, 2, 2, 3, 4, 5];
countOccurrences(arr, 2);  // Returns 3
```

---

## Practice Problems

### Beginner Level
1. ✅ Implement basic binary search
2. Find element in rotated sorted array
3. Find first and last position of element
4. Count occurrences of element
5. Search in descending order array

### Intermediate Level
6. Find peak element
7. Find minimum in rotated sorted array
8. Search in 2D matrix
9. Find square root using binary search
10. Find smallest letter greater than target

### Advanced Level
11. Median of two sorted arrays
12. Kth smallest element in sorted matrix
13. Split array largest sum
14. Capacity to ship packages within D days
15. Aggressive cows problem

---

## Study Tips

### Understanding Binary Search
1. **Visualize** the halving process with diagrams
2. **Trace** examples step by step on paper
3. **Practice** writing code without looking
4. **Test** edge cases (empty array, single element, duplicates)

### Memory Aid: "BCS"
- **B**oundaries: Update first/last correctly
- **C**alculate: Use safe mid formula
- **S**orted: Verify data is sorted first

### Debugging Checklist
- ✅ Is array sorted?
- ✅ Using `first <= last` in loop?
- ✅ Updating `first = mid + 1` or `last = mid - 1`?
- ✅ Using Math.floor() for mid?
- ✅ Handling edge cases?

---

## Interview Preparation

### Common Questions
1. Explain binary search algorithm
2. What's the time complexity and why?
3. Why must data be sorted?
4. What's the difference from linear search?
5. How to handle duplicates?
6. Explain the mid calculation formula

### Problem-Solving Template
```
1. Verify array is sorted
2. Initialize first = 0, last = n-1
3. Loop while first <= last
4. Calculate mid safely
5. Compare and update boundaries
6. Return result or -1
```

### Code Template
```javascript
function binarySearch(arr, target) {
    let first = 0;
    let last = arr.length - 1;
    
    while (first <= last) {
        let mid = Math.floor(first + (last - first) / 2);
        
        if (arr[mid] === target) {
            return mid;
        } else if (arr[mid] < target) {
            first = mid + 1;
        } else {
            last = mid - 1;
        }
    }
    
    return -1;
}
```

---

## Quick Reference

### Algorithm Summary
```
BINARY SEARCH (Iterative)
1. first = 0, last = n - 1
2. while first <= last:
     mid = first + (last - first) / 2
     if arr[mid] == target: return mid
     if arr[mid] < target: first = mid + 1
     else: last = mid - 1
3. return -1
```

### Complexity Cheat Sheet
| Aspect | Value |
|--------|-------|
| Time (Best) | O(1) - element at mid |
| Time (Average) | O(log n) |
| Time (Worst) | O(log n) - not found |
| Space (Iterative) | O(1) |
| Space (Recursive) | O(log n) |

### Mid Formula
```
✅ ALWAYS USE: mid = first + Math.floor((last - first) / 2)
```

---

## Lecture Timeline

| Time | Topic |
|------|-------|
| 00:00 - 00:54 | Introduction to Binary Search |
| 00:54 - 04:51 | Basic concept and mid comparison |
| 04:51 - 08:22 | Visualization and boundary updates |
| 08:22 - 14:08 | Iterative examples and termination |
| 14:08 - 16:10 | Code implementation overview |
| 16:10 - 20:23 | Mid calculation best practice |
| 20:23 - 24:05 | Complexity analysis |
| 24:05 - 27:11 | Comparison and real-world applications |
| 27:11 - 28:05 | Summary and key takeaways |

---

## Additional Resources

### Practice Platforms
- **LeetCode**: Problems 704, 35, 34, 33, 153
- **HackerRank**: Binary Search challenges
- **CodeForces**: Div 2 problems

### Visualization Tools
- Binary Search Visualizer
- Algorithm visualization websites
- Step-by-step tracers

---

**Remember**: Binary Search is one of the most important algorithms in computer science. Master it thoroughly! 🚀

**Key Mantra**: "Sorted data + Halving search space = Binary Search"