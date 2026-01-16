# Search Insert Position - Binary Search
## Comprehensive Study Notes - LeetCode #35

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Problem Statement](#2-problem-statement)
3. [Understanding Binary Search](#3-understanding-binary-search)
4. [Solution Approach](#4-solution-approach)
5. [Detailed Examples](#5-detailed-examples)
6. [Implementation](#6-implementation)
7. [Time and Space Complexity](#7-time-and-space-complexity)
8. [Key Takeaways](#8-key-takeaways)

---

## 1. Introduction

### What is Search Insert Position?

**Search Insert Position** (LeetCode #35) is a classic problem that combines:
- **Binary Search** algorithm
- **Sorted array** manipulation
- **Insertion index** finding

### Problem Classification

- **LeetCode:** #35
- **Difficulty:** Easy
- **Category:** Binary Search, Array
- **Topic:** Search Algorithms

### Prerequisites

Before attempting this problem, you should understand:
- Binary Search algorithm
- How sorted arrays work
- Index-based array access
- Loop termination conditions

---

## 2. Problem Statement

### The Problem

Given a **sorted array** of **distinct integers** and a **target value**, return:
1. The **index** if the target is found in the array
2. The **index where it would be inserted** if not found (to maintain sorted order)

### Input Format

```
nums: Sorted array of distinct integers
target: Integer value to search or insert
```

### Output Format

```
Return: Integer (index of target or insertion position)
```

### Constraints

- Array is **sorted** in ascending order
- All integers are **distinct** (unique)
- Must achieve **O(log n)** time complexity
- Array can be empty or have multiple elements

### Examples

**Example 1: Target Found**
```
Input: nums = [1, 3, 5, 6], target = 5
Output: 2
Explanation: 5 exists at index 2
```

**Example 2: Target Not Found (Insert in Middle)**
```
Input: nums = [1, 3, 5, 6], target = 2
Output: 1
Explanation: 2 should be inserted at index 1 (between 1 and 3)
```

**Example 3: Target Not Found (Insert at End)**
```
Input: nums = [1, 3, 5, 6], target = 7
Output: 4
Explanation: 7 should be inserted at index 4 (after 6)
```

**Example 4: Target Not Found (Insert at Beginning)**
```
Input: nums = [1, 3, 5, 6], target = 0
Output: 0
Explanation: 0 should be inserted at index 0 (before 1)
```

**Example 5: Empty Array**
```
Input: nums = [], target = 5
Output: 0
Explanation: First element position
```

### Key Observations

1. **Sorted Array** - Essential for binary search
2. **Distinct Elements** - No duplicates to handle
3. **O(log n) Required** - Linear search won't work
4. **Insertion Maintains Order** - Result keeps array sorted

---

## 3. Understanding Binary Search

### What is Binary Search?

**Binary Search** is an efficient algorithm for finding an element in a **sorted array** by repeatedly dividing the search space in half.

### Core Principle

Instead of checking every element (linear search), binary search eliminates half of the remaining elements with each comparison.

### How It Works

```
1. Start with entire array
2. Check middle element
3. If target equals middle → Found!
4. If target < middle → Search left half
5. If target > middle → Search right half
6. Repeat until found or space exhausted
```

### Visual Example

```
Array: [1, 3, 5, 7, 9, 11, 13]
Target: 7

Step 1: Check middle (index 3)
[1, 3, 5, 7, 9, 11, 13]
         ↑
    7 == 7 → Found at index 3!

Target: 6

Step 1: Check middle (index 3)
[1, 3, 5, 7, 9, 11, 13]
         ↑
    6 < 7 → Search left half

Step 2: Check middle of left half (index 1)
[1, 3, 5]
    ↑
    6 > 3 → Search right half

Step 3: Check middle of right half (index 2)
[5]
 ↑
    6 > 5 → No more elements
    Not found, insert at index 3
```

### Binary Search Components

**Three Pointers:**
1. **first (start)** - Beginning of search space
2. **last (end)** - End of search space
3. **mid** - Middle of current search space

**Three Actions:**
1. **Found** - Return mid
2. **Go Left** - Update last = mid - 1
3. **Go Right** - Update first = mid + 1

---

## 4. Solution Approach

### The Key Insight

**When binary search terminates without finding the target, the `first` pointer indicates the correct insertion position.**

**Why?**
- All elements before `first` are less than target
- All elements from `first` onwards are greater than target
- Therefore, target should be inserted at position `first`

### Algorithm Steps

```
1. Initialize:
   first = 0
   last = length - 1

2. While first <= last:
   a. Calculate mid = floor((first + last) / 2)
   
   b. If nums[mid] == target:
      - Return mid (found!)
   
   c. If nums[mid] < target:
      - Target is in right half
      - first = mid + 1
   
   d. If nums[mid] > target:
      - Target is in left half
      - last = mid - 1

3. If loop ends (target not found):
   - Return first (insertion position)
```

### Why Return `first` Not `last`?

When loop terminates:
- `first > last` (pointers have crossed)
- `first` points to first element greater than target
- This is exactly where target should be inserted

**Visual Proof:**

```
[1, 3, 5, 6], target = 2

Final state:
[1, 3, 5, 6]
 ↑ ↑
last first

first = 1 (correct insertion position)
last = 0
```

---

## 5. Detailed Examples

### Example 1: Target Found

**Input:** `nums = [1, 3, 5]`, `target = 5`

```
Iteration 1:
Array: [1, 3, 5]
first = 0, last = 2
mid = (0 + 2) / 2 = 1
nums[1] = 3
3 < 5 → Move right
first = mid + 1 = 2

Iteration 2:
Array: [1, 3, 5]
first = 2, last = 2
mid = (2 + 2) / 2 = 2
nums[2] = 5
5 == 5 → Found!
Return 2
```

**Output:** `2`

---

### Example 2: Target Not Found (Insert Middle)

**Input:** `nums = [1, 3, 5, 6]`, `target = 2`

```
Iteration 1:
Array: [1, 3, 5, 6]
        ↑
first = 0, last = 3
mid = (0 + 3) / 2 = 1
nums[1] = 3
2 < 3 → Move left
last = mid - 1 = 0

Iteration 2:
Array: [1, 3, 5, 6]
       ↑
first = 0, last = 0
mid = (0 + 0) / 2 = 0
nums[0] = 1
2 > 1 → Move right
first = mid + 1 = 1

Loop ends: first (1) > last (0)
Return first = 1

Result: [1, 2, 3, 5, 6]
            ↑
         Insert at index 1
```

**Output:** `1`

**Verification:**
```
Original: [1, 3, 5, 6]
After insertion: [1, 2, 3, 5, 6]
Still sorted? ✓
```

---

### Example 3: Target Not Found (Insert End)

**Input:** `nums = [1, 3, 5, 6]`, `target = 7`

```
Iteration 1:
Array: [1, 3, 5, 6]
        ↑
first = 0, last = 3
mid = (0 + 3) / 2 = 1
nums[1] = 3
7 > 3 → Move right
first = mid + 1 = 2

Iteration 2:
Array: [1, 3, 5, 6]
              ↑
first = 2, last = 3
mid = (2 + 3) / 2 = 2
nums[2] = 5
7 > 5 → Move right
first = mid + 1 = 3

Iteration 3:
Array: [1, 3, 5, 6]
                 ↑
first = 3, last = 3
mid = (3 + 3) / 2 = 3
nums[3] = 6
7 > 6 → Move right
first = mid + 1 = 4

Loop ends: first (4) > last (3)
Return first = 4

Result: [1, 3, 5, 6, 7]
                     ↑
         Insert at index 4 (end)
```

**Output:** `4`

---

### Example 4: Target Not Found (Insert Beginning)

**Input:** `nums = [1, 3, 5, 6]`, `target = 0`

```
Iteration 1:
Array: [1, 3, 5, 6]
        ↑
first = 0, last = 3
mid = (0 + 3) / 2 = 1
nums[1] = 3
0 < 3 → Move left
last = mid - 1 = 0

Iteration 2:
Array: [1, 3, 5, 6]
       ↑
first = 0, last = 0
mid = (0 + 0) / 2 = 0
nums[0] = 1
0 < 1 → Move left
last = mid - 1 = -1

Loop ends: first (0) > last (-1)
Return first = 0

Result: [0, 1, 3, 5, 6]
        ↑
         Insert at index 0 (beginning)
```

**Output:** `0`

---

### Example 5: Empty Array

**Input:** `nums = []`, `target = 5`

```
first = 0
last = -1

Loop condition: first (0) > last (-1)
Loop doesn't execute

Return first = 0

Result: [5]
        ↑
         Insert at index 0
```

**Output:** `0`

---

### Example 6: Single Element (Target Found)

**Input:** `nums = [5]`, `target = 5`

```
Iteration 1:
first = 0, last = 0
mid = (0 + 0) / 2 = 0
nums[0] = 5
5 == 5 → Found!
Return 0
```

**Output:** `0`

---

### Example 7: Single Element (Insert Before)

**Input:** `nums = [5]`, `target = 3`

```
Iteration 1:
first = 0, last = 0
mid = (0 + 0) / 2 = 0
nums[0] = 5
3 < 5 → Move left
last = mid - 1 = -1

Loop ends: first (0) > last (-1)
Return first = 0

Result: [3, 5]
        ↑
         Insert at index 0
```

**Output:** `0`

---

### Example 8: Single Element (Insert After)

**Input:** `nums = [5]`, `target = 7`

```
Iteration 1:
first = 0, last = 0
mid = (0 + 0) / 2 = 0
nums[0] = 5
7 > 5 → Move right
first = mid + 1 = 1

Loop ends: first (1) > last (0)
Return first = 1

Result: [5, 7]
           ↑
         Insert at index 1
```

**Output:** `1`

---

## 6. Implementation

### JavaScript Solution

```javascript
/**
 * @param {number[]} nums - Sorted array of distinct integers
 * @param {number} target - Target value to search
 * @return {number} - Index of target or insertion position
 */
function searchInsert(nums, target) {
    let first = 0;
    let last = nums.length - 1;
    
    while (first <= last) {
        // Calculate middle index (avoid overflow)
        let mid = Math.floor((first + last) / 2);
        
        // Target found
        if (nums[mid] === target) {
            return mid;
        }
        
        // Target is in right half
        if (nums[mid] < target) {
            first = mid + 1;
        }
        // Target is in left half
        else {
            last = mid - 1;
        }
    }
    
    // Target not found, return insertion position
    return first;
}

// Test cases
console.log(searchInsert([1, 3, 5, 6], 5));  // 2
console.log(searchInsert([1, 3, 5, 6], 2));  // 1
console.log(searchInsert([1, 3, 5, 6], 7));  // 4
console.log(searchInsert([1, 3, 5, 6], 0));  // 0
console.log(searchInsert([], 5));            // 0
```

### Alternative Implementation (Ternary Operator)

```javascript
function searchInsert(nums, target) {
    let first = 0;
    let last = nums.length - 1;
    
    while (first <= last) {
        const mid = Math.floor((first + last) / 2);
        
        if (nums[mid] === target) return mid;
        
        nums[mid] < target ? first = mid + 1 : last = mid - 1;
    }
    
    return first;
}
```

### Python Solution

```python
def searchInsert(nums: list[int], target: int) -> int:
    first = 0
    last = len(nums) - 1
    
    while first <= last:
        mid = (first + last) // 2
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            first = mid + 1
        else:
            last = mid - 1
    
    return first

# Test cases
print(searchInsert([1, 3, 5, 6], 5))  # 2
print(searchInsert([1, 3, 5, 6], 2))  # 1
print(searchInsert([1, 3, 5, 6], 7))  # 4
```

### Java Solution

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int first = 0;
        int last = nums.length - 1;
        
        while (first <= last) {
            int mid = first + (last - first) / 2;
            
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                first = mid + 1;
            } else {
                last = mid - 1;
            }
        }
        
        return first;
    }
}
```

### C++ Solution

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int first = 0;
        int last = nums.size() - 1;
        
        while (first <= last) {
            int mid = first + (last - first) / 2;
            
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                first = mid + 1;
            } else {
                last = mid - 1;
            }
        }
        
        return first;
    }
};
```

### Avoiding Integer Overflow

**Problem:** `(first + last) / 2` can overflow with large indices

**Solutions:**

```javascript
// Method 1: Subtract first
let mid = first + Math.floor((last - first) / 2);

// Method 2: Bitwise shift (JavaScript safe up to 2^31-1)
let mid = (first + last) >>> 1;

// Method 3: Math.floor (safest in JavaScript)
let mid = Math.floor((first + last) / 2);
```

---

## 7. Time and Space Complexity

### Time Complexity Analysis

**Time Complexity: O(log n)**

**Reasoning:**

With each iteration, the search space is divided in half:
- Iteration 1: n elements
- Iteration 2: n/2 elements
- Iteration 3: n/4 elements
- ...
- Iteration k: n/(2^k) elements

The loop continues until search space reduces to 1 element:
```
n / 2^k = 1
n = 2^k
k = log₂(n)
```

**Example:**
```
Array size: 1,000,000 elements
Linear search: 1,000,000 operations (worst case)
Binary search: ~20 operations (log₂(1,000,000) ≈ 20)

Speedup: 50,000x faster!
```

### Space Complexity Analysis

**Space Complexity: O(1)**

**Reasoning:**

- Only using a constant number of variables:
  - `first` (1 variable)
  - `last` (1 variable)
  - `mid` (1 variable)
- No extra data structures created
- No recursion (no call stack)
- Memory usage doesn't depend on input size

### Complexity Comparison

| Algorithm | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
| **Binary Search** | O(log n) | O(1) |
| Linear Search | O(n) | O(1) |
| Binary Search (Recursive) | O(log n) | O(log n) |

### Performance on LeetCode

According to the video:
- **Runtime:** 0 ms
- **Beats:** 100% of submissions
- **Optimal solution** for this problem

---

## 8. Key Takeaways

### Core Concepts

1. **Binary Search Requirement**
   - Problem requires O(log n) time
   - Sorted array is prerequisite
   - Only viable algorithm for this constraint

2. **Insertion Position Logic**
   - When target not found, `first` pointer gives insertion index
   - All elements before `first` are < target
   - All elements from `first` onwards are > target

3. **Loop Termination**
   - Loop ends when `first > last`
   - At this point, pointers have "crossed"
   - `first` is always the answer

### Problem-Solving Pattern

```
1. Recognize sorted array + O(log n) → Binary Search
2. Apply standard binary search
3. If found → return mid
4. If not found → return first
```

### Common Mistakes to Avoid

❌ **Using linear search**
```javascript
// ❌ WRONG: O(n) time
for (let i = 0; i < nums.length; i++) {
    if (nums[i] >= target) return i;
}
```

❌ **Returning wrong pointer**
```javascript
// ❌ WRONG: Should return first, not last
return last;  // Incorrect insertion position
```

❌ **Wrong loop condition**
```javascript
// ❌ WRONG: Should be <=
while (first < last) {  // Misses single element check
```

❌ **Not handling empty array**
```javascript
// ❌ WRONG: Crashes on empty array
if (nums[0] > target) return 0;  // Index out of bounds
```

### Edge Cases Checklist

- [ ] Empty array `[]`
- [ ] Single element array
- [ ] Target at beginning
- [ ] Target at end
- [ ] Target in middle
- [ ] Target smaller than all elements
- [ ] Target larger than all elements
- [ ] Target equals first element
- [ ] Target equals last element
- [ ] Target equals middle element

### Testing Template

```javascript
function testSearchInsert() {
    const tests = [
        { nums: [1,3,5,6], target: 5, expected: 2 },
        { nums: [1,3,5,6], target: 2, expected: 1 },
        { nums: [1,3,5,6], target: 7, expected: 4 },
        { nums: [1,3,5,6], target: 0, expected: 0 },
        { nums: [], target: 5, expected: 0 },
        { nums: [5], target: 5, expected: 0 },
        { nums: [5], target: 3, expected: 0 },
        { nums: [5], target: 7, expected: 1 },
    ];
    
    for (const test of tests) {
        const result = searchInsert(test.nums, test.target);
        const status = result === test.expected ? '✓' : '✗';
        console.log(`${status} Input: [${test.nums}], ${test.target} → ${result} (expected ${test.expected})`);
    }
}

testSearchInsert();
```

### Interview Tips

**What interviewers look for:**

1. **Problem Recognition**
   - Identify sorted array
   - Recognize O(log n) requirement
   - Choose binary search immediately

2. **Implementation Quality**
   - Clean, readable code
   - Proper variable names
   - Avoid integer overflow
   - Handle edge cases

3. **Explanation Ability**
   - Explain why binary search
   - Walk through example
   - Clarify insertion logic
   - Discuss complexity

**Common Follow-up Questions:**

Q: "What if array has duplicates?"
A: Problem states distinct integers, but for duplicates, we'd need to specify if we want leftmost or rightmost position.

Q: "Can you do it recursively?"
A: Yes, but iterative is better (O(1) space vs O(log n) stack space).

Q: "What if target is a float?"
A: Same logic applies, comparison operators work with floats.

Q: "How would you test this?"
A: Use edge cases: empty, single element, target at boundaries, target in middle.

### Visual Summary

```
Binary Search Insert Position Pattern:

Given: Sorted array + Target
Goal: Find index or insertion position

Step 1: Binary search
        ↓
Step 2a: Found → Return index
        ↓
Step 2b: Not found → Return first pointer
        ↓
Result: Index that maintains sorted order
```

### Practice Problems

**Similar LeetCode Problems:**

| # | Problem | Difficulty | Concept |
|---|---------|-----------|---------|
| 35 | Search Insert Position | Easy | Basic binary search |
| 704 | Binary Search | Easy | Standard binary search |
| 278 | First Bad Version | Easy | Binary search variant |
| 34 | Find First and Last Position | Medium | Binary search range |
| 74 | Search 2D Matrix | Medium | Binary search in 2D |
| 33 | Search in Rotated Array | Medium | Modified binary search |

### Algorithm Template

```javascript
function binarySearchInsert(arr, target) {
    let first = 0;
    let last = arr.length - 1;
    
    while (first <= last) {
        let mid = Math.floor((first + last) / 2);
        
        if (arr[mid] === target) {
            return mid;  // Found
        }
        
        if (arr[mid] < target) {
            first = mid + 1;  // Search right
        } else {
            last = mid - 1;   // Search left
        }
    }
    
    return first;  // Insertion position
}
```

### Quick Reference

**Binary Search Formula:**
```
mid = floor((first + last) / 2)
```

**Update Rules:**
```
If arr[mid] < target: first = mid + 1
If arr[mid] > target: last = mid - 1
If arr[mid] = target: return mid
```

**Termination:**
```
When first > last: return first
```

---

## Resources for Further Learning

- **LeetCode:** Practice problem #35
- **Visualizer:** Algorithm Visualizer for binary search
- **Related Topics:** Binary search variations
- **Video:** Binary search tutorial (mentioned in original video)

---

## Final Tips

1. **Master binary search first** - This problem is an application
2. **Draw it out** - Visualize pointer movements
3. **Test edge cases** - Empty, single element, boundaries
4. **Understand why `first`** - The key insight
5. **Practice variations** - Similar problems reinforce concept

**Remember:** When you see "sorted array" + "O(log n)" → Think Binary Search!

---

**Happy Coding! 🚀**

---

**End of Study Notes**
