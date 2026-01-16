# Search in Rotated Sorted Array - Complete Study Guide

## 📚 Problem Overview

### LeetCode Problem #33: Search in Rotated Sorted Array

**Problem Statement:**
Given an integer array `nums` sorted in ascending order (with distinct values), which has been rotated at an unknown pivot index, and a target value, return the index of the target if it is in the array, or -1 if it is not.

**Key Constraints:**
- Array was originally sorted in ascending order
- Array has been rotated at some unknown pivot
- All values in the array are **unique/distinct**
- Must achieve **O(log n)** time complexity
- Return the index of target, or -1 if not found

---

## 🔄 Understanding Array Rotation

### What is Array Rotation?

**Rotation** means taking some elements from the beginning and moving them to the end.

**Example:**
```
Original sorted array: [0, 1, 2, 4, 5, 6, 7]
                             ↑
                       Rotate at index 3

After rotation:        [4, 5, 6, 7, 0, 1, 2]
                        -------  -------
                        Part 2   Part 1
```

### Key Observations About Rotated Arrays

1. **Two Sorted Subarrays:**
   - A rotated sorted array consists of two individually sorted subarrays
   - The entire array is NOT sorted as a whole
   - Example: `[4, 5, 6, 7]` and `[0, 1, 2]` are both sorted

2. **Pivot Point:**
   - The rotation point (pivot) is where the maximum element meets the minimum
   - In `[4, 5, 6, 7, 0, 1, 2]`, the pivot is between index 3 (value 7) and index 4 (value 0)

3. **At Least One Half is Always Sorted:**
   - When you divide the array at any mid point, at least one half will be completely sorted
   - This is the KEY insight for solving the problem

**Visual Representation:**
```
[4, 5, 6, 7, 0, 1, 2]
 ↑           ↑       ↑
first       mid    last

Left half:  [4, 5, 6, 7]  ✓ Sorted
Right half: [0, 1, 2]     ✓ Sorted
```

---

## 🎯 Why Standard Binary Search Fails

### Standard Binary Search Assumption

Traditional binary search requires the **entire array to be sorted**:
```
If target < mid: search left
If target > mid: search right
```

### Problem with Rotated Arrays

In a rotated array like `[4, 5, 6, 7, 0, 1, 2]`:
- If target = 0 and mid = 7
- Standard logic would say: "0 < 7, search left"
- But 0 is actually on the RIGHT side!

**Conclusion:** We need a MODIFIED binary search that accounts for rotation.

---

## 💡 The Key Insight

### Core Strategy

In each iteration:
1. **Identify which half is sorted** (left or right)
2. **Check if target lies within the sorted half**
3. **Search the appropriate half** based on where target could be

### How to Identify Sorted Half?

**Rule:**
- If `nums[first] <= nums[mid]` → **Left half is sorted**
- Otherwise → **Right half is sorted**

**Why does this work?**
```
Case 1: Left half sorted
[4, 5, 6, 7, 0, 1, 2]
 ↑        ↑
first    mid
4 <= 7 ✓ → Left is sorted

Case 2: Right half sorted  
[7, 0, 1, 2, 4, 5, 6]
 ↑        ↑
first    mid
7 <= 2 ✗ → Right is sorted (left is rotated)
```

---

## 🔍 The Algorithm

### Step-by-Step Approach

**Step 1: Initialize Pointers**
```javascript
let first = 0;
let last = nums.length - 1;
```

**Step 2: Binary Search Loop**
```javascript
while (first <= last) {
    let mid = Math.floor((first + last) / 2);
    
    // Step 3: Check if mid is the target
    if (nums[mid] === target) {
        return mid;
    }
    
    // Step 4: Identify sorted half and decide direction
    // (Details below)
}

return -1;  // Target not found
```

**Step 3: Identify Sorted Half and Search**

```javascript
if (nums[first] <= nums[mid]) {
    // LEFT HALF IS SORTED: [first...mid]
    
    if (nums[first] <= target && target < nums[mid]) {
        // Target is in the sorted left half
        last = mid - 1;
    } else {
        // Target must be in right half
        first = mid + 1;
    }
} else {
    // RIGHT HALF IS SORTED: [mid...last]
    
    if (nums[mid] < target && target <= nums[last]) {
        // Target is in the sorted right half
        first = mid + 1;
    } else {
        // Target must be in left half
        last = mid - 1;
    }
}
```

---

## 💻 Complete Code Implementation

### JavaScript Solution

```javascript
function search(nums, target) {
    let first = 0;
    let last = nums.length - 1;
    
    while (first <= last) {
        let mid = Math.floor((first + last) / 2);
        
        // Found the target
        if (nums[mid] === target) {
            return mid;
        }
        
        // Determine which half is sorted
        if (nums[first] <= nums[mid]) {
            // Left half is sorted
            if (nums[first] <= target && target < nums[mid]) {
                // Target is in left sorted half
                last = mid - 1;
            } else {
                // Target is in right half
                first = mid + 1;
            }
        } else {
            // Right half is sorted
            if (nums[mid] < target && target <= nums[last]) {
                // Target is in right sorted half
                first = mid + 1;
            } else {
                // Target is in left half
                last = mid - 1;
            }
        }
    }
    
    return -1;  // Target not found
}

// Test cases
console.log(search([4, 5, 6, 7, 0, 1, 2], 0));  // Output: 4
console.log(search([4, 5, 6, 7, 0, 1, 2], 3));  // Output: -1
console.log(search([1], 0));                     // Output: -1
```

### Python Solution

```python
def search(nums, target):
    first, last = 0, len(nums) - 1
    
    while first <= last:
        mid = (first + last) // 2
        
        # Found the target
        if nums[mid] == target:
            return mid
        
        # Determine which half is sorted
        if nums[first] <= nums[mid]:
            # Left half is sorted
            if nums[first] <= target < nums[mid]:
                # Target is in left sorted half
                last = mid - 1
            else:
                # Target is in right half
                first = mid + 1
        else:
            # Right half is sorted
            if nums[mid] < target <= nums[last]:
                # Target is in right sorted half
                first = mid + 1
            else:
                # Target is in left half
                last = mid - 1
    
    return -1  # Target not found

# Test cases
print(search([4, 5, 6, 7, 0, 1, 2], 0))  # Output: 4
print(search([4, 5, 6, 7, 0, 1, 2], 3))  # Output: -1
```

---

## 📊 Detailed Example Walkthrough

### Example 1: Finding Target 0

**Array:** `[4, 5, 6, 7, 0, 1, 2]`  
**Target:** `0`  
**Expected Output:** `4`

**Iteration 1:**
```
Array:  [4, 5, 6, 7, 0, 1, 2]
Index:   0  1  2  3  4  5  6
         ↑        ↑        ↑
       first     mid     last

first = 0, last = 6
mid = (0 + 6) / 2 = 3
nums[mid] = 7

Check: nums[mid] == target? → 7 == 0? NO

Identify sorted half:
nums[first] <= nums[mid]? → 4 <= 7? YES
→ Left half [4,5,6,7] is sorted

Is target in sorted left half?
nums[first] <= target < nums[mid]? → 4 <= 0 < 7? NO

→ Search right half
first = mid + 1 = 4
```

**Iteration 2:**
```
Array:  [4, 5, 6, 7, 0, 1, 2]
Index:   0  1  2  3  4  5  6
                     ↑  ↑  ↑
                   first mid last

first = 4, last = 6
mid = (4 + 6) / 2 = 5
nums[mid] = 1

Check: nums[mid] == target? → 1 == 0? NO

Identify sorted half:
nums[first] <= nums[mid]? → 0 <= 1? YES
→ Left half [0,1] is sorted

Is target in sorted left half?
nums[first] <= target < nums[mid]? → 0 <= 0 < 1? YES

→ Search left half
last = mid - 1 = 4
```

**Iteration 3:**
```
Array:  [4, 5, 6, 7, 0, 1, 2]
Index:   0  1  2  3  4  5  6
                     ↑
                first,mid,last

first = 4, last = 4
mid = (4 + 4) / 2 = 4
nums[mid] = 0

Check: nums[mid] == target? → 0 == 0? YES ✓

FOUND! Return mid = 4
```

**Step-by-Step Table:**

| Iteration | first | last | mid | nums[mid] | Sorted Half | Target in Range? | Action |
|-----------|-------|------|-----|-----------|-------------|------------------|--------|
| 1 | 0 | 6 | 3 | 7 | Left [4-7] | No (0 not in 4-7) | first = 4 |
| 2 | 4 | 6 | 5 | 1 | Left [0-1] | Yes (0 in 0-1) | last = 4 |
| 3 | 4 | 4 | 4 | 0 | - | Target found! | Return 4 |

---

### Example 2: Target Not Found

**Array:** `[4, 5, 6, 7, 0, 1, 2]`  
**Target:** `3`  
**Expected Output:** `-1`

**Iteration 1:**
```
first = 0, last = 6, mid = 3
nums[mid] = 7 ≠ 3
Left half sorted: [4,5,6,7]
3 in range [4,7]? YES
→ Search left: last = 2
```

**Iteration 2:**
```
first = 0, last = 2, mid = 1
nums[mid] = 5 ≠ 3
Left half sorted: [4,5]
3 in range [4,5]? YES  
→ Search left: last = 0
```

**Iteration 3:**
```
first = 0, last = 0, mid = 0
nums[mid] = 4 ≠ 3
Left half sorted: [4]
3 in range [4,4]? NO
→ Search right: first = 1
```

**Loop ends:** `first > last` (1 > 0)  
**Return:** `-1`

---

## 🎓 Pointer Update Logic

### Decision Tree for Pointer Updates

```
                     [Check nums[mid] == target]
                              |
                         Yes  |  No
                              ↓
                    [Identify Sorted Half]
                              |
                    ┌─────────┴─────────┐
                    ↓                   ↓
          [Left Half Sorted]    [Right Half Sorted]
          nums[first]<=nums[mid]  nums[mid]<=nums[last]
                    |                   |
         ┌──────────┴──────────┐       ┌┴────────────┐
         ↓                     ↓       ↓             ↓
    [Target in        [Target not  [Target in   [Target not
     left range]      in left]     right range]  in right]
         |                 |            |             |
    last=mid-1       first=mid+1   first=mid+1   last=mid-1
```

### Summary Table: Pointer Update Logic

| Condition | Sorted Half | Target Range Check | Pointer Update |
|-----------|-------------|-------------------|----------------|
| `nums[first] <= nums[mid]` | Left | `nums[first] <= target < nums[mid]` | `last = mid - 1` |
| `nums[first] <= nums[mid]` | Left | Target NOT in left range | `first = mid + 1` |
| `nums[first] > nums[mid]` | Right | `nums[mid] < target <= nums[last]` | `first = mid + 1` |
| `nums[first] > nums[mid]` | Right | Target NOT in right range | `last = mid - 1` |

---

## ⚠️ Important Edge Cases

### 1. Single Element Array
```javascript
nums = [1], target = 0
→ Output: -1

nums = [1], target = 1
→ Output: 0
```

### 2. Two Element Array
```javascript
nums = [3, 1], target = 1
→ Output: 1

nums = [1, 3], target = 3
→ Output: 1
```

### 3. No Rotation (Already Sorted)
```javascript
nums = [1, 2, 3, 4, 5], target = 3
→ Still works! Left half always sorted
→ Output: 2
```

### 4. Target at Boundaries
```javascript
nums = [4, 5, 6, 7, 0, 1, 2], target = 4
→ Output: 0 (first element)

nums = [4, 5, 6, 7, 0, 1, 2], target = 2
→ Output: 6 (last element)
```

### 5. Target at Pivot Point
```javascript
nums = [4, 5, 6, 7, 0, 1, 2], target = 7
→ Output: 3 (max before pivot)

nums = [4, 5, 6, 7, 0, 1, 2], target = 0
→ Output: 4 (min after pivot)
```

---

## 🧮 Complexity Analysis

### Time Complexity: O(log n)

**Reasoning:**
- Each iteration divides the search space in half
- Similar to standard binary search
- Maximum iterations = log₂(n)

**Example:**
- Array size = 1000 elements
- Maximum iterations ≈ log₂(1000) ≈ 10 iterations

### Space Complexity: O(1)

**Reasoning:**
- Only using constant extra space (variables: first, last, mid)
- No recursive calls (iterative approach)
- No additional data structures

**Comparison with Other Approaches:**

| Approach | Time Complexity | Space Complexity | Notes |
|----------|----------------|------------------|-------|
| Linear Search | O(n) | O(1) | Simple but slow |
| Modified Binary Search | O(log n) | O(1) | Optimal! ✓ |
| Find Pivot + 2 Binary Searches | O(log n) | O(1) | More complex |

---

## 🔧 Common Mistakes & How to Avoid Them

### Mistake 1: Incorrect Sorted Half Detection

**Wrong:**
```javascript
if (nums[first] < nums[mid]) {  // Missing equality!
    // Left half sorted
}
```

**Correct:**
```javascript
if (nums[first] <= nums[mid]) {  // Include equality
    // Left half sorted
}
```

**Why?** When `first == mid`, left half is trivially sorted (single element).

---

### Mistake 2: Wrong Target Range Check

**Wrong:**
```javascript
if (nums[first] <= target <= nums[mid]) {  // Doesn't work in JS!
    // Search left
}
```

**Correct:**
```javascript
if (nums[first] <= target && target < nums[mid]) {
    // Search left
}
```

**Note:** Use `<` not `<=` for upper bound to avoid re-checking mid.

---

### Mistake 3: Incorrect Pointer Updates

**Wrong:**
```javascript
last = mid;  // Might cause infinite loop if target == nums[mid]
```

**Correct:**
```javascript
last = mid - 1;  // Exclude mid since we already checked it
```

---

### Mistake 4: Integer Overflow (in some languages)

**Potential Issue (C++/Java):**
```cpp
int mid = (first + last) / 2;  // Can overflow if first + last > INT_MAX
```

**Safe Alternative:**
```cpp
int mid = first + (last - first) / 2;  // Avoids overflow
```

**JavaScript Note:** Not an issue in JS due to how numbers work, but good practice.

---

## 💭 Intuition Building

### Why Does This Work?

**Key Properties:**
1. **Rotation preserves sorted subarrays**
   - Original: `[0,1,2,4,5,6,7]`
   - After rotation: `[4,5,6,7]` + `[0,1,2]` (both sorted)

2. **At any mid point, one half must be sorted**
   - If mid falls in first part: left is sorted
   - If mid falls in second part: right is sorted

3. **Sorted half enables binary search decision**
   - We can definitively say if target is in sorted half
   - If not, target must be in other half

### Visual Understanding

```
Original Array (sorted):
[0, 1, 2, 4, 5, 6, 7]
 └─────────────────┘
   Fully sorted

After Rotation at index 3:
[4, 5, 6, 7, 0, 1, 2]
 └─────────┘ └─────┘
  Sorted      Sorted
  Part 2      Part 1

Any mid point:
[4, 5, 6, 7 | 0, 1, 2]
 └─────────┘   └─────┘
  Sorted (✓)   Sorted (✓)
  
At least one half is always fully sorted!
```

---

## 🎯 Practice Problems

### Related LeetCode Problems

1. **Find Minimum in Rotated Sorted Array** (#153)
   - Find the minimum element
   - Similar concept, different goal

2. **Search in Rotated Sorted Array II** (#81)
   - Array may contain duplicates
   - Slightly more complex

3. **Find Peak Element** (#162)
   - Find any peak in array
   - Uses modified binary search

4. **Find First and Last Position** (#34)
   - Find range of target
   - Binary search variant

---

## 📝 Step-by-Step Implementation Guide

### How to Code This from Scratch

**Step 1: Set up binary search framework**
```javascript
function search(nums, target) {
    let first = 0;
    let last = nums.length - 1;
    
    while (first <= last) {
        let mid = Math.floor((first + last) / 2);
        // TODO: Add logic
    }
    
    return -1;
}
```

**Step 2: Add target found check**
```javascript
if (nums[mid] === target) {
    return mid;
}
```

**Step 3: Add sorted half detection**
```javascript
if (nums[first] <= nums[mid]) {
    // Left half is sorted
} else {
    // Right half is sorted
}
```

**Step 4: Add target range checks and pointer updates**
```javascript
if (nums[first] <= nums[mid]) {
    if (nums[first] <= target && target < nums[mid]) {
        last = mid - 1;
    } else {
        first = mid + 1;
    }
} else {
    if (nums[mid] < target && target <= nums[last]) {
        first = mid + 1;
    } else {
        last = mid - 1;
    }
}
```

---

## 🧪 Testing Strategy

### Test Cases to Consider

```javascript
// Test Case 1: Target exists
console.log(search([4,5,6,7,0,1,2], 0));  // Expected: 4

// Test Case 2: Target doesn't exist
console.log(search([4,5,6,7,0,1,2], 3));  // Expected: -1

// Test Case 3: Single element (found)
console.log(search([1], 1));               // Expected: 0

// Test Case 4: Single element (not found)
console.log(search([1], 0));               // Expected: -1

// Test Case 5: No rotation
console.log(search([1,2,3,4,5], 3));      // Expected: 2

// Test Case 6: Target at start
console.log(search([4,5,6,7,0,1,2], 4));  // Expected: 0

// Test Case 7: Target at end
console.log(search([4,5,6,7,0,1,2], 2));  // Expected: 6

// Test Case 8: Two elements
console.log(search([3,1], 1));             // Expected: 1
```

---

## 📌 Key Takeaways

1. **Rotated sorted array = Two sorted subarrays**
   - Understanding this is crucial

2. **At least one half is always sorted**
   - This enables modified binary search

3. **Identify sorted half first**
   - Then check if target is in that half

4. **O(log n) is achievable**
   - By eliminating half the search space each iteration

5. **Boundary conditions matter**
   - Use `<=` and `<` carefully
   - Update pointers as `mid ± 1` to avoid infinite loops

6. **Works for any rotation**
   - Algorithm handles all rotation positions
   - Even handles no rotation (sorted array)

7. **Unique values simplify logic**
   - No need to handle duplicate comparisons
   - (Different problem if duplicates exist)

---

## 🎓 Quick Reference

### Algorithm Template
```javascript
function search(nums, target) {
    let first = 0, last = nums.length - 1;
    
    while (first <= last) {
        let mid = Math.floor((first + last) / 2);
        if (nums[mid] === target) return mid;
        
        if (nums[first] <= nums[mid]) {
            // Left sorted
            if (nums[first] <= target && target < nums[mid]) 
                last = mid - 1;
            else 
                first = mid + 1;
        } else {
            // Right sorted
            if (nums[mid] < target && target <= nums[last]) 
                first = mid + 1;
            else 
                last = mid - 1;
        }
    }
    return -1;
}
```

### Mental Checklist
- [ ] Initialize first and last pointers
- [ ] Loop while first <= last
- [ ] Calculate mid
- [ ] Check if mid is target
- [ ] Identify which half is sorted
- [ ] Check if target in sorted half's range
- [ ] Update pointers appropriately
- [ ] Return -1 if not found

---

**Problem Source:** LeetCode #33 - Search in Rotated Sorted Array  
**Difficulty:** Medium  
**Optimal Solution:** Modified Binary Search  
**Time Complexity:** O(log n)  
**Space Complexity:** O(1)

**Remember:** Practice is key! Implement this yourself and test with various inputs to build muscle memory!