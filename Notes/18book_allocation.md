# Allocate Minimum Pages - Complete Study Guide

## 📚 Problem Overview

### Problem Statement: Allocate Minimum Number of Pages

**Source:** GeeksforGeeks (GFG Practice)  
**Difficulty:** Medium (Conceptually Hard)  
**Category:** Binary Search on Answer Space

**Given:**
- An array `arr[]` where `arr[i]` represents the number of pages in book `i`
- An integer `k` representing the number of students

**Objective:**
Allocate books to `k` students such that:
1. Every student gets **at least one book**
2. Books allocated to a student must be **contiguous** (continuous sequence)
3. Each book is allocated to **exactly one student** (no sharing)
4. **Minimize the maximum** number of pages assigned to any student

**Return:** The minimum possible value of the maximum pages assigned to any student, or `-1` if allocation is impossible.

---

## 🎯 Understanding the Problem

### Visual Example

**Input:** `arr = [2, 5, 7, 3, 1, 8]`, `k = 2` students

**Different Allocation Possibilities:**

```
Allocation 1:
Student 1: [2, 5, 7]       → Total = 14 pages
Student 2: [3, 1, 8]       → Total = 12 pages
Maximum pages = 14
```

```
Allocation 2:
Student 1: [2, 5]          → Total = 7 pages
Student 2: [7, 3, 1, 8]    → Total = 19 pages
Maximum pages = 19
```

```
Allocation 3:
Student 1: [2, 5, 7, 3]    → Total = 17 pages
Student 2: [1, 8]          → Total = 9 pages
Maximum pages = 17
```

```
Allocation 4:
Student 1: [2]             → Total = 2 pages
Student 2: [5, 7, 3, 1, 8] → Total = 24 pages
Maximum pages = 24
```

**Answer:** Among all allocations, Allocation 1 has the **minimum maximum** (14 pages)

---

### Another Example with 3 Students

**Input:** `arr = [2, 5, 7, 3, 8]`, `k = 3` students

**Some Valid Allocations:**

```
Allocation A:
Student 1: [2]       → 2 pages
Student 2: [5, 7]    → 12 pages
Student 3: [3, 8]    → 11 pages
Maximum = 12
```

```
Allocation B:
Student 1: [2, 5]    → 7 pages
Student 2: [7]       → 7 pages
Student 3: [3, 8]    → 11 pages
Maximum = 11 ✓ (Better!)
```

```
Allocation C:
Student 1: [2, 5, 7] → 14 pages
Student 2: [3]       → 3 pages
Student 3: [8]       → 8 pages
Maximum = 14
```

**Answer:** Allocation B gives minimum maximum = 11 pages

---

## 🚫 Invalid Allocations

### Why Some Allocations Don't Work

**Example:** `arr = [10, 20, 30, 40]`, `k = 5` students

```
❌ INVALID: More students than books (5 > 4)
Cannot give at least one book to each student
Return: -1
```

**Example:** Non-contiguous allocation
```
arr = [2, 5, 7, 3]
Student 1: [2, 7]    ❌ NOT CONTIGUOUS (skipped 5)
Student 2: [5, 3]    ❌ NOT CONTIGUOUS (skipped 7)
```

**Example:** Overlapping books
```
arr = [2, 5, 7, 3]
Student 1: [2, 5]
Student 2: [5, 7]    ❌ Book with 5 pages allocated twice
```

---

## 💡 Key Insights

### Why Can't We Use Standard Binary Search?

**Important Distinction:**
- The input array is **NOT sorted** (pages can be in any order)
- But the **answer space IS sorted** (minimum max pages ranges from low to high)

### The Answer Space

**Lower Bound:** 
- The maximum number of pages in any single book
- Why? At minimum, one student must read the largest book entirely
- Example: `arr = [12, 34, 67, 90]` → Lower bound = 90

**Upper Bound:**
- Sum of all pages in all books
- Why? In worst case, one student reads all books
- Example: `arr = [12, 34, 67, 90]` → Upper bound = 203

**Search Space:** `[max(arr), sum(arr)]`

This range represents all possible values for "maximum pages assigned to a student"

---

## 🔍 When to Apply Binary Search on Answer?

### Three Key Criteria

**1. Minimize Maximum or Maximize Minimum Problem**
- "Minimize the maximum pages"
- "Minimize the maximum time"
- "Maximize the minimum distance"

**2. Contiguous/Adjacent Allocation Required**
- Elements must be assigned in continuous blocks
- Cannot skip or reorder elements

**3. Feasibility Check Possible**
- For any candidate answer, we can verify if allocation is possible
- Typically uses a greedy approach

**If all three conditions met → Binary Search on Answer Space!**

---

## 🎲 The Algorithm

### Overview: Binary Search + Greedy Validation

**Two-Part Approach:**

1. **Binary Search on Answer Space**
   - Search for the minimum possible maximum pages
   - Range: `[max(arr), sum(arr)]`

2. **Greedy Validation Function**
   - For a given `mid` (candidate max pages)
   - Check if books can be allocated such that no student gets more than `mid` pages

---

### Step 1: Binary Search Setup

```javascript
function allocateMinPages(arr, k) {
    let n = arr.length;
    
    // Edge case: More students than books
    if (k > n) return -1;
    
    // Define search space
    let first = Math.max(...arr);  // Minimum possible max
    let last = arr.reduce((a, b) => a + b, 0);  // Maximum possible max
    
    let answer = -1;
    
    while (first <= last) {
        let mid = Math.floor((first + last) / 2);
        
        // Check if allocation is possible with max = mid
        if (isValid(arr, n, k, mid)) {
            answer = mid;      // Valid allocation found
            last = mid - 1;    // Try to find smaller max
        } else {
            first = mid + 1;   // Need larger max
        }
    }
    
    return answer;
}
```

---

### Step 2: Greedy Validation Function

**Logic:** Try to allocate books greedily. If we can allocate to ≤ k students, it's valid.

```javascript
function isValid(arr, n, k, maxPages) {
    let studentCount = 1;      // Start with first student
    let currentSum = 0;        // Pages assigned to current student
    
    for (let i = 0; i < n; i++) {
        // If single book exceeds maxPages, allocation impossible
        if (arr[i] > maxPages) {
            return false;
        }
        
        // Try to assign current book to current student
        if (currentSum + arr[i] <= maxPages) {
            currentSum += arr[i];
        } else {
            // Current student full, move to next student
            studentCount++;
            currentSum = arr[i];
            
            // If we need more students than available
            if (studentCount > k) {
                return false;
            }
        }
    }
    
    // Successfully allocated within k students
    return true;
}
```

---

## 📊 Complete Implementation

### JavaScript Solution

```javascript
function allocateMinPages(arr, k) {
    let n = arr.length;
    
    // Edge case: impossible to allocate
    if (k > n) return -1;
    
    // Special case: one student gets all books
    if (k === 1) {
        return arr.reduce((a, b) => a + b, 0);
    }
    
    // Special case: each student gets one book
    if (k === n) {
        return Math.max(...arr);
    }
    
    // Binary search on answer space
    let first = Math.max(...arr);
    let last = arr.reduce((a, b) => a + b, 0);
    let answer = -1;
    
    while (first <= last) {
        let mid = Math.floor((first + last) / 2);
        
        if (isValid(arr, n, k, mid)) {
            answer = mid;
            last = mid - 1;  // Try to minimize
        } else {
            first = mid + 1;  // Increase max pages
        }
    }
    
    return answer;
}

function isValid(arr, n, k, maxPages) {
    let studentCount = 1;
    let currentSum = 0;
    
    for (let i = 0; i < n; i++) {
        if (arr[i] > maxPages) {
            return false;
        }
        
        if (currentSum + arr[i] <= maxPages) {
            currentSum += arr[i];
        } else {
            studentCount++;
            currentSum = arr[i];
            
            if (studentCount > k) {
                return false;
            }
        }
    }
    
    return true;
}

// Test cases
console.log(allocateMinPages([12, 34, 67, 90], 2));  // Expected: 113
console.log(allocateMinPages([15, 17, 20], 2));      // Expected: 32
console.log(allocateMinPages([10, 20, 30], 1));      // Expected: 60
console.log(allocateMinPages([10, 20], 3));          // Expected: -1
```

---

### Python Solution

```python
def allocate_min_pages(arr, k):
    n = len(arr)
    
    # Edge case
    if k > n:
        return -1
    
    # Binary search bounds
    first = max(arr)
    last = sum(arr)
    answer = -1
    
    while first <= last:
        mid = (first + last) // 2
        
        if is_valid(arr, n, k, mid):
            answer = mid
            last = mid - 1
        else:
            first = mid + 1
    
    return answer

def is_valid(arr, n, k, max_pages):
    student_count = 1
    current_sum = 0
    
    for i in range(n):
        if arr[i] > max_pages:
            return False
        
        if current_sum + arr[i] <= max_pages:
            current_sum += arr[i]
        else:
            student_count += 1
            current_sum = arr[i]
            
            if student_count > k:
                return False
    
    return True

# Test
print(allocate_min_pages([12, 34, 67, 90], 2))  # 113
```

---

## 🔬 Detailed Walkthrough

### Example: `arr = [12, 34, 67, 90]`, `k = 2`

**Step 1: Initialize Search Space**
```
first = max(arr) = 90
last = sum(arr) = 203
answer = -1
```

**Iteration 1:**
```
mid = (90 + 203) / 2 = 146

Check isValid(arr, 2, 146):
  Student 1: 12 + 34 + 67 = 113 ≤ 146 ✓
  Student 2: 90 ≤ 146 ✓
  Total students = 2 ✓

Valid! answer = 146
Search for smaller: last = 145
```

**Iteration 2:**
```
first = 90, last = 145
mid = (90 + 145) / 2 = 117

Check isValid(arr, 2, 117):
  Student 1: 12 + 34 = 46 ≤ 117 ✓
             46 + 67 = 113 ≤ 117 ✓
  Student 2: 90 ≤ 117 ✓
  Total students = 2 ✓

Valid! answer = 117
Search for smaller: last = 116
```

**Iteration 3:**
```
first = 90, last = 116
mid = (90 + 116) / 2 = 103

Check isValid(arr, 2, 103):
  Student 1: 12 + 34 = 46 ≤ 103 ✓
             46 + 67 = 113 > 103 ✗
  Student 2: 67
  Student 3: 90
  Total students = 3 > 2 ✗

Invalid! first = 104
```

**Iteration 4:**
```
first = 104, last = 116
mid = (104 + 116) / 2 = 110

Check isValid(arr, 2, 110):
  Student 1: 12 + 34 = 46 ≤ 110 ✓
             46 + 67 = 113 > 110 ✗
  Student 2: 67
  Student 3: 90
  Total students = 3 > 2 ✗

Invalid! first = 111
```

**Iteration 5:**
```
first = 111, last = 116
mid = (111 + 116) / 2 = 113

Check isValid(arr, 2, 113):
  Student 1: 12 + 34 = 46 ≤ 113 ✓
             46 + 67 = 113 ≤ 113 ✓
  Student 2: 90 ≤ 113 ✓
  Total students = 2 ✓

Valid! answer = 113
Search for smaller: last = 112
```

**Iteration 6:**
```
first = 111, last = 112
mid = (111 + 112) / 2 = 111

Check isValid(arr, 2, 111):
  Student 1: 12 + 34 = 46 ≤ 111 ✓
             46 + 67 = 113 > 111 ✗
  Student 2: 67
  Student 3: 90
  Total students = 3 > 2 ✗

Invalid! first = 112
```

**Iteration 7:**
```
first = 112, last = 112
mid = 112

Check isValid(arr, 2, 112):
  Student 1: 12 + 34 = 46 ≤ 112 ✓
             46 + 67 = 113 > 112 ✗
  Student 2: 67
  Student 3: 90
  Total students = 3 > 2 ✗

Invalid! first = 113
```

**Loop ends:** `first > last` (113 > 112)

**Answer:** 113

**Allocation:**
- Student 1: [12, 34, 67] = 113 pages
- Student 2: [90] = 90 pages
- Maximum = 113 ✓

---

## 📈 Complexity Analysis

### Time Complexity: O(n log m)

**Breakdown:**
- Binary search iterations: O(log m) where m = sum(arr) - max(arr)
- Each validation check: O(n) where n = number of books
- Total: O(n × log m)

**Example:**
- If sum = 1000, max = 100, search space = 900
- Binary search iterations ≈ log₂(900) ≈ 10
- With n = 100 books: 100 × 10 = 1000 operations

### Space Complexity: O(1)

**Reasoning:**
- Only using constant extra variables (first, last, mid, studentCount, currentSum)
- No recursive calls
- No additional data structures
- In-place validation

---

## 🎓 Edge Cases and Special Scenarios

### 1. More Students than Books
```javascript
arr = [10, 20, 30], k = 5
// Impossible: Cannot give each student at least one book
return -1;
```

### 2. One Student
```javascript
arr = [10, 20, 30, 40], k = 1
// One student reads all books
return 100; // sum of all
```

### 3. Students Equal to Books
```javascript
arr = [10, 20, 30], k = 3
// Each student gets exactly one book
return 30; // max(arr)
```

### 4. All Books Same Pages
```javascript
arr = [50, 50, 50, 50], k = 2
// Student 1: [50, 50] = 100
// Student 2: [50, 50] = 100
return 100;
```

### 5. Single Book
```javascript
arr = [100], k = 1
return 100;

arr = [100], k = 2
return -1; // Impossible
```

### 6. Large Difference in Pages
```javascript
arr = [1, 1, 1, 100], k = 2
// Student 1: [1, 1, 1] = 3
// Student 2: [100] = 100
return 100; // Optimal distribution
```

---

## 🧠 Intuition Building

### Why Greedy Works for Validation

**Greedy Strategy:**
"Keep adding books to current student until adding next book would exceed limit"

**Why is this optimal?**
- If we can fit a book with current student without exceeding limit, we should
- Moving to next student too early wastes capacity
- This minimizes number of students needed

**Proof Sketch:**
- If allocation is possible with `k` students and max `mid` pages
- Greedy gives us minimum number of students needed
- If greedy needs ≤ k students, allocation is definitely possible

---

### Visual Understanding of Binary Search

```
Search Space: [90 ------------------- 203]
                ↑                       ↑
             max(arr)                sum(arr)

Iteration 1: mid=146 → Valid ✓
New Space:   [90 -------- 146]

Iteration 2: mid=117 → Valid ✓
New Space:   [90 --- 117]

Iteration 3: mid=103 → Invalid ✗
New Space:        [104 --- 117]

Iteration 4: mid=110 → Invalid ✗
New Space:             [111 --- 117]

Iteration 5: mid=113 → Valid ✓
New Space:             [111 - 113]

Continue until answer = 113
```

---

## 🔗 Related Problems (Same Pattern)

### 1. LeetCode 1011: Capacity To Ship Packages Within D Days

**Problem:** Ship packages in D days, minimize ship capacity

**Similarity:**
- Minimize maximum capacity
- Contiguous allocation (days are sequential)
- Binary search on capacity + greedy validation

**Solution Template:** Exactly same as allocate pages!

```javascript
function shipWithinDays(weights, days) {
    let first = Math.max(...weights);
    let last = weights.reduce((a, b) => a + b, 0);
    
    while (first <= last) {
        let mid = Math.floor((first + last) / 2);
        if (canShip(weights, days, mid)) {
            last = mid - 1;
        } else {
            first = mid + 1;
        }
    }
    return first;
}

function canShip(weights, days, capacity) {
    let daysNeeded = 1;
    let currentLoad = 0;
    
    for (let weight of weights) {
        if (currentLoad + weight <= capacity) {
            currentLoad += weight;
        } else {
            daysNeeded++;
            currentLoad = weight;
        }
    }
    
    return daysNeeded <= days;
}
```

---

### 2. LeetCode 410: Split Array Largest Sum

**Problem:** Split array into m subarrays, minimize largest sum

**Similarity:** Identical to allocate minimum pages!

---

### 3. Aggressive Cows / Magnetic Force Between Balls

**Problem:** Maximize minimum distance between elements

**Similarity:**
- Binary search on answer (distance)
- Greedy placement validation
- Maximize minimum (instead of minimize maximum)

---

### 4. Minimum Time to Complete Trips

**Problem:** Given trip times, find minimum time for totalTrips

**Similarity:**
- Binary search on time
- Check if totalTrips possible in given time

---

## 🎯 Pattern Recognition

### When You See These Keywords:

1. **"Minimize the maximum"** → Binary search on answer
2. **"Maximize the minimum"** → Binary search on answer
3. **"Contiguous allocation"** → Greedy validation
4. **"Distribute among k groups"** → Partition problem
5. **"Cannot exceed limit"** → Feasibility check needed

### General Template

```javascript
function solve(arr, k) {
    // Define search space
    let first = minimumPossibleAnswer();
    let last = maximumPossibleAnswer();
    let result = -1;
    
    // Binary search on answer
    while (first <= last) {
        let mid = Math.floor((first + last) / 2);
        
        if (isPossible(arr, k, mid)) {
            result = mid;
            // For minimize: last = mid - 1
            // For maximize: first = mid + 1
        } else {
            // Opposite of above
        }
    }
    
    return result;
}

function isPossible(arr, k, candidate) {
    // Greedy validation
    // Return true if allocation possible with candidate as limit
}
```

---

## 💡 Common Mistakes & How to Avoid

### Mistake 1: Wrong Search Space Bounds

**Wrong:**
```javascript
let first = 0;  // ❌ Too small!
let last = 10000;  // ❌ Arbitrary large number
```

**Correct:**
```javascript
let first = Math.max(...arr);  // ✓ Meaningful lower bound
let last = arr.reduce((a, b) => a + b, 0);  // ✓ Meaningful upper bound
```

---

### Mistake 2: Incorrect Validation Logic

**Wrong:**
```javascript
if (currentSum + arr[i] <= maxPages) {
    currentSum += arr[i];
    studentCount++;  // ❌ Incrementing student for each book!
}
```

**Correct:**
```javascript
if (currentSum + arr[i] <= maxPages) {
    currentSum += arr[i];  // ✓ Just add to current student
} else {
    studentCount++;  // ✓ Increment only when moving to next student
    currentSum = arr[i];
}
```

---

### Mistake 3: Forgetting Single Book Exceeds Limit

**Wrong:**
```javascript
function isValid(arr, k, maxPages) {
    for (let i = 0; i < arr.length; i++) {
        if (currentSum + arr[i] <= maxPages) {
            currentSum += arr[i];
        } else {
            studentCount++;
            currentSum = arr[i];  // ❌ What if arr[i] > maxPages?
        }
    }
}
```

**Correct:**
```javascript
function isValid(arr, k, maxPages) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] > maxPages) {
            return false;  // ✓ Check single book doesn't exceed limit
        }
        // ... rest of logic
    }
}
```

---

### Mistake 4: Wrong Pointer Update

**Wrong:**
```javascript
if (isValid(arr, k, mid)) {
    answer = mid;
    first = mid + 1;  // ❌ Moving in wrong direction!
}
```

**Correct:**
```javascript
if (isValid(arr, k, mid)) {
    answer = mid;
    last = mid - 1;  // ✓ Try to minimize further
}
```

---

## 📝 Practice Strategy

### Step-by-Step Learning Path

**Phase 1: Understanding**
1. Read problem multiple times
2. Work through examples manually
3. Identify the pattern (minimize maximum)
4. Understand why binary search applies

**Phase 2: Implementation**
1. Write the binary search skeleton
2. Implement validation function
3. Handle edge cases
4. Test with examples

**Phase 3: Practice**
1. Solve "Capacity to Ship Packages"
2. Solve "Split Array Largest Sum"
3. Try variations with maximize minimum

---

## 🎯 Quick Reference Card

```javascript
// TEMPLATE: Minimize Maximum Problems

function minimizeMaximum(arr, k) {
    if (k > arr.length) return -1;
    
    let first = Math.max(...arr);
    let last = arr.reduce((a,b) => a+b, 0);
    let answer = -1;
    
    while (first <= last) {
        let mid = Math.floor((first + last) / 2);
        
        if (canAllocate(arr, k, mid)) {
            answer = mid;
            last = mid - 1;  // Minimize
        } else {
            first = mid + 1;
        }
    }
    return answer;
}

function canAllocate(arr, k, limit) {
    let groups = 1;
    let current = 0;
    
    for (let val of arr) {
        if (val > limit) return false;
        
        if (current + val <= limit) {
            current += val;
        } else {
            groups++;
            current = val;
            if (groups > k) return false;
        }
    }
    return true;
}
```

---

## 📊 Summary

### Key Takeaways

1. **Binary Search on Answer ≠ Binary Search on Array**
   - Array can be unsorted
   - We search on the answer space (numeric range)

2. **Pattern: Minimize Maximum / Maximize Minimum**
   - Classic sign to use binary search on answer

3. **Greedy Validation is Crucial**
   - Must efficiently check if allocation possible
   - Usually O(n) time

4. **Search Space Bounds Matter**
   - Lower: max(arr) - at least one student gets largest book
   - Upper: sum(arr) - one student gets all books

5. **Same Pattern, Different Problems**
   - Ship packages, split arrays, aggressive cows
   - Template remains the same

6. **Time Complexity: O(n log m)**
   - Efficient for large inputs
   - m = sum of values

---

**Problem Source:** GeeksforGeeks - Allocate Minimum Pages  
**Related:** LeetCode 1011, LeetCode 410  
**Difficulty:** Medium-Hard  
**Pattern:** Binary Search on Answer Space  
**Companies:** Meta, Amazon, Netflix, Google

**Remember:** Master this pattern - it's a favorite in top company interviews!