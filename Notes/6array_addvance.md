# Two Pointer Algorithms - Comprehensive Study Guide

## 📚 Introduction to Two Pointer Technique

### What is Two Pointer Technique?
The **two-pointer technique** is a powerful algorithmic approach that uses two pointers (indices) to traverse an array or data structure, often from different positions or directions, to solve problems efficiently.

### Why Use Two Pointers?
- **Reduces Time Complexity**: Often converts O(n²) solutions to O(n)
- **Space Efficient**: Usually requires O(1) extra space
- **Elegant Solutions**: Provides clean, intuitive code
- **Wide Applicability**: Used in sorting, searching, array manipulation, and more

### Common Two Pointer Patterns
1. **Opposite Direction**: One pointer from start, one from end
2. **Same Direction**: Both pointers moving forward at different speeds
3. **Sliding Window**: Two pointers forming a dynamic window
4. **Fast-Slow Pointers**: One pointer moves faster than the other

---

## 🔄 Array Rotation Problems

### Problem 1: Left Rotation by One Element

**Problem Statement:** Rotate all elements of an array one position to the left. The first element moves to the last position.

**Example:**
- Input: `[1, 2, 3, 4, 5]`
- Output: `[2, 3, 4, 5, 1]`

**Visual Representation:**
```
Original:  [1, 2, 3, 4, 5]
            ↓  ↓  ↓  ↓  ↓
Rotated:   [2, 3, 4, 5, 1]
```

**Algorithm:**
1. Store the first element in a temporary variable
2. Shift all elements one position to the left (from index 0 to length-2)
3. Place the stored element at the last position

**Code Implementation:**
```javascript
function leftRotateByOne(arr) {
    let n = arr.length;
    let temp = arr[0];  // Store first element
    
    // Shift elements left
    for(let i = 0; i < n - 1; i++) {
        arr[i] = arr[i + 1];
    }
    
    // Place first element at end
    arr[n - 1] = temp;
    
    return arr;
}

// Test
let arr = [1, 2, 3, 4, 5];
console.log(leftRotateByOne(arr));  // [2, 3, 4, 5, 1]
```

**Dry Run:**

| Step | i | arr[i] | arr[i+1] | Action | Array State |
|------|---|--------|----------|--------|-------------|
| Initial | - | - | - | temp = 1 | [1, 2, 3, 4, 5] |
| 1 | 0 | 1 | 2 | arr[0] = arr[1] | [2, 2, 3, 4, 5] |
| 2 | 1 | 2 | 3 | arr[1] = arr[2] | [2, 3, 3, 4, 5] |
| 3 | 2 | 3 | 4 | arr[2] = arr[3] | [2, 3, 4, 4, 5] |
| 4 | 3 | 4 | 5 | arr[3] = arr[4] | [2, 3, 4, 5, 5] |
| Final | - | - | - | arr[4] = temp | [2, 3, 4, 5, 1] |

**Key Points:**
- Loop from `0` to `n-2` to avoid array out of bounds
- Store first element before loop starts
- Each element moves to previous index position

**Complexity:**
- **Time Complexity**: O(n) - single pass through array
- **Space Complexity**: O(1) - only one temporary variable

---

### Problem 2: Right Rotation by One Element

**Problem Statement:** Rotate all elements of an array one position to the right. The last element moves to the first position.

**Example:**
- Input: `[1, 2, 3, 4, 5]`
- Output: `[5, 1, 2, 3, 4]`

**Visual Representation:**
```
Original:  [1, 2, 3, 4, 5]
            ↓  ↓  ↓  ↓  ↓
Rotated:   [5, 1, 2, 3, 4]
```

**Why Not Left-to-Right?**
If we iterate from left to right (`arr[i+1] = arr[i]`), we overwrite values before using them:
```
[1, 2, 3, 4, 5]
[1, 1, 3, 4, 5]  // arr[1] = arr[0], but we lost original arr[1]!
[1, 1, 1, 4, 5]  // Problem continues...
```

**Correct Approach: Right-to-Left Iteration**

**Algorithm:**
1. Store the last element in a temporary variable
2. Shift all elements one position to the right (from end to beginning)
3. Place the stored element at the first position

**Code Implementation:**
```javascript
function rightRotateByOne(arr) {
    let n = arr.length;
    let temp = arr[n - 1];  // Store last element
    
    // Shift elements right (iterate backwards)
    for(let i = n - 1; i > 0; i--) {
        arr[i] = arr[i - 1];
    }
    
    // Place last element at beginning
    arr[0] = temp;
    
    return arr;
}

// Test
let arr = [1, 2, 3, 4, 5];
console.log(rightRotateByOne(arr));  // [5, 1, 2, 3, 4]
```

**Dry Run:**

| Step | i | arr[i] | arr[i-1] | Action | Array State |
|------|---|--------|----------|--------|-------------|
| Initial | - | - | - | temp = 5 | [1, 2, 3, 4, 5] |
| 1 | 4 | 5 | 4 | arr[4] = arr[3] | [1, 2, 3, 4, 4] |
| 2 | 3 | 4 | 3 | arr[3] = arr[2] | [1, 2, 3, 3, 4] |
| 3 | 2 | 3 | 2 | arr[2] = arr[1] | [1, 2, 2, 3, 4] |
| 4 | 1 | 2 | 1 | arr[1] = arr[0] | [1, 1, 2, 3, 4] |
| Final | - | - | - | arr[0] = temp | [5, 1, 2, 3, 4] |

**Key Points:**
- **Must iterate backwards** to avoid overwriting values
- Loop from `n-1` down to `1`
- Store last element before loop starts

**Complexity:**
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)

---

## 🔁 Understanding Nested Loops

### Concept
A **nested loop** is a loop inside another loop. The inner loop executes completely for each iteration of the outer loop.

### Basic Example

**Code:**
```javascript
for(let i = 0; i < 4; i++) {           // Outer loop: 4 iterations
    for(let j = 0; j < 3; j++) {       // Inner loop: 3 iterations each
        console.log("Hello");
    }
}
// Total prints: 4 × 3 = 12
```

**Execution Pattern:**
```
Outer i=0: Inner prints "Hello" 3 times (j=0,1,2)
Outer i=1: Inner prints "Hello" 3 times (j=0,1,2)
Outer i=2: Inner prints "Hello" 3 times (j=0,1,2)
Outer i=3: Inner prints "Hello" 3 times (j=0,1,2)
Total: 12 prints
```

### Time Complexity of Nested Loops
- **Two nested loops**: O(n × m) or O(n²) if both iterate n times
- **Three nested loops**: O(n × m × p) or O(n³) if all iterate n times

### Example with Array Processing
```javascript
// Print all pairs in an array
let arr = [1, 2, 3, 4];
for(let i = 0; i < arr.length; i++) {
    for(let j = 0; j < arr.length; j++) {
        console.log(arr[i], arr[j]);
    }
}
// Prints all 16 combinations (4²)
```

---

## 🎯 Rotation by K Elements

### Problem 3: Left Rotation by K Elements

**Problem Statement:** Rotate an array k positions to the left.

**Example:**
- Input: `arr = [1, 2, 3, 4, 5]`, `k = 2`
- Output: `[3, 4, 5, 1, 2]`

**Visual:**
```
Original:     [1, 2, 3, 4, 5]
After k=1:    [2, 3, 4, 5, 1]
After k=2:    [3, 4, 5, 1, 2]
```

### Approach 1: Brute Force (Nested Loops)

**Idea:** Perform single-step left rotation k times.

**Code:**
```javascript
function leftRotateByK_BruteForce(arr, k) {
    let n = arr.length;
    k = k % n;  // Optimize: reduce k if k > n
    
    // Perform single rotation k times
    for(let count = 0; count < k; count++) {
        let temp = arr[0];
        for(let i = 0; i < n - 1; i++) {
            arr[i] = arr[i + 1];
        }
        arr[n - 1] = temp;
    }
    
    return arr;
}

// Test
console.log(leftRotateByK_BruteForce([1, 2, 3, 4, 5], 2));  // [3, 4, 5, 1, 2]
```

**Complexity:**
- **Time**: O(n × k) → O(n²) in worst case
- **Space**: O(1)

**Problem:** Inefficient for large k values!

---

### Approach 2: Using Extra Space

**Idea:** Create a new array and place each element at its rotated position using modulo arithmetic.

**Formula for Left Rotation:**
- New position = `(i - k + n) % n`
- Or place `arr[i]` at position `(i + k) % n` in reverse logic

**Alternative Approach:**
- Copy last `n-k` elements to start of new array
- Copy first `k` elements to end of new array

**Code:**
```javascript
function leftRotateByK_ExtraSpace(arr, k) {
    let n = arr.length;
    k = k % n;  // Handle k > n
    
    let temp = new Array(n);
    
    // Place elements at new positions
    for(let i = 0; i < n; i++) {
        temp[i] = arr[(i + k) % n];
    }
    
    // Copy back to original array
    for(let i = 0; i < n; i++) {
        arr[i] = temp[i];
    }
    
    return arr;
}

// Alternative implementation
function leftRotateByK_ExtraSpace_Alt(arr, k) {
    let n = arr.length;
    k = k % n;
    
    let temp = [];
    
    // Copy from k to end
    for(let i = k; i < n; i++) {
        temp.push(arr[i]);
    }
    
    // Copy from 0 to k-1
    for(let i = 0; i < k; i++) {
        temp.push(arr[i]);
    }
    
    return temp;
}

// Test
console.log(leftRotateByK_ExtraSpace([1, 2, 3, 4, 5], 2));  // [3, 4, 5, 1, 2]
```

**Dry Run (k=2, arr=[1,2,3,4,5]):**

| i | (i + k) % n | arr[(i+k)%n] | temp[i] |
|---|-------------|--------------|---------|
| 0 | (0+2)%5 = 2 | arr[2] = 3 | 3 |
| 1 | (1+2)%5 = 3 | arr[3] = 4 | 4 |
| 2 | (2+2)%5 = 4 | arr[4] = 5 | 5 |
| 3 | (3+2)%5 = 0 | arr[0] = 1 | 1 |
| 4 | (4+2)%5 = 1 | arr[1] = 2 | 2 |

Result: `[3, 4, 5, 1, 2]` ✓

**Complexity:**
- **Time**: O(n)
- **Space**: O(n) - temporary array

**Optimization Tip:**
Always reduce k: `k = k % n`
- If k = 7 and n = 5, rotating 7 times = rotating 2 times
- If k = 5 and n = 5, rotating 5 times = no change (k becomes 0)

---

### Approach 3: Reversal Algorithm (Optimal)

**Idea:** Use array reversal operations to achieve rotation in O(n) time with O(1) space.

**Algorithm for Left Rotation by k:**
1. Reverse first k elements
2. Reverse remaining n-k elements
3. Reverse the entire array

**Visual Example (arr=[1,2,3,4,5], k=2):**
```
Original:           [1, 2, 3, 4, 5]
                     ------  -------
Step 1: Reverse     [2, 1, 3, 4, 5]  (reverse first 2)
       first k            -------
Step 2: Reverse     [2, 1, 5, 4, 3]  (reverse last 3)
       last n-k     
Step 3: Reverse     [3, 4, 5, 1, 2]  (reverse all)
       entire
```

**Code:**
```javascript
// Helper function to reverse a portion of array
function reverse(arr, start, end) {
    while(start < end) {
        let temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        start++;
        end--;
    }
}

function leftRotateByK_Optimal(arr, k) {
    let n = arr.length;
    k = k % n;  // Handle k > n
    
    if(k === 0) return arr;  // No rotation needed
    
    // Step 1: Reverse first k elements
    reverse(arr, 0, k - 1);
    
    // Step 2: Reverse remaining n-k elements
    reverse(arr, k, n - 1);
    
    // Step 3: Reverse entire array
    reverse(arr, 0, n - 1);
    
    return arr;
}

// Test
console.log(leftRotateByK_Optimal([1, 2, 3, 4, 5], 2));  // [3, 4, 5, 1, 2]
```

**Detailed Dry Run:**

**Initial:** `[1, 2, 3, 4, 5]`, k=2

**Step 1 - Reverse first k (0 to 1):**
- Swap arr[0] and arr[1]: `[2, 1, 3, 4, 5]`

**Step 2 - Reverse last n-k (2 to 4):**
- Swap arr[2] and arr[4]: `[2, 1, 5, 4, 3]`
- Swap arr[3] and arr[3]: no change (middle element)

**Step 3 - Reverse entire array (0 to 4):**
- Swap arr[0] and arr[4]: `[3, 1, 5, 4, 2]`
- Swap arr[1] and arr[3]: `[3, 4, 5, 1, 2]`
- Middle element arr[2] stays: `[3, 4, 5, 1, 2]`

**Result:** `[3, 4, 5, 1, 2]` ✓

**Complexity:**
- **Time**: O(n) - three passes through array
- **Space**: O(1) - only temp variable for swaps

**This is the OPTIMAL solution!**

---

### Right Rotation by K Elements

**Algorithm for Right Rotation by k:**
1. Reverse last k elements
2. Reverse first n-k elements
3. Reverse entire array

**OR** simply: Right rotate by k = Left rotate by (n - k)

**Code:**
```javascript
function rightRotateByK(arr, k) {
    let n = arr.length;
    k = k % n;
    
    // Method 1: Reversal algorithm
    reverse(arr, n - k, n - 1);  // Reverse last k
    reverse(arr, 0, n - k - 1);  // Reverse first n-k
    reverse(arr, 0, n - 1);      // Reverse all
    
    return arr;
}

// Method 2: Use left rotation
function rightRotateByK_Alt(arr, k) {
    return leftRotateByK_Optimal(arr, arr.length - k);
}

// Test
console.log(rightRotateByK([1, 2, 3, 4, 5], 2));  // [4, 5, 1, 2, 3]
```

---

## 📋 Comparison of Rotation Methods

| Method | Time Complexity | Space Complexity | Pros | Cons |
|--------|----------------|------------------|------|------|
| Brute Force (Nested) | O(n × k) ≈ O(n²) | O(1) | Simple to understand | Very slow for large k |
| Extra Space | O(n) | O(n) | Fast, straightforward | Uses extra memory |
| Reversal Algorithm | O(n) | O(1) | Fast, no extra space | Slightly complex logic |

**Recommendation:** Use **Reversal Algorithm** for production code - it's optimal in both time and space!

---

## 🔍 Two Pointer Problems

### Problem 4: Remove Duplicates from Sorted Array

**Problem Statement:** Given a sorted integer array, remove duplicates in-place so each unique element appears only once. Return the number of unique elements.

**Example:**
- Input: `[1, 1, 2, 2, 3, 4, 4, 5]`
- Output: `5` (modified array: `[1, 2, 3, 4, 5, _, _, _]`)
- Note: Only first 5 elements matter

**Constraints:**
- Modify array in-place (no extra array)
- Maintain relative order
- Return count of unique elements

**LeetCode Problem:** [#26 - Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

**Algorithm (Two Pointers):**
1. Initialize pointer `j = 0` (marks position for next unique element)
2. Traverse with pointer `i` from 0 to n-1
3. When `arr[i] != arr[i+1]` (found unique element):
   - Place `arr[i+1]` at position `j`
   - Increment `j`
4. Return `j` as count of unique elements

**Code:**
```javascript
function removeDuplicates(nums) {
    if(nums.length === 0) return 0;
    
    let j = 1;  // Position for next unique element
    
    for(let i = 0; i < nums.length - 1; i++) {
        if(nums[i] !== nums[i + 1]) {
            nums[j] = nums[i + 1];
            j++;
        }
    }
    
    return j;  // Count of unique elements
}

// Test
let arr = [1, 1, 2, 2, 3, 4, 4, 5];
let k = removeDuplicates(arr);
console.log(k);                    // 5
console.log(arr.slice(0, k));     // [1, 2, 3, 4, 5]
```

**Dry Run:**

| i | nums[i] | nums[i+1] | Different? | Action | j | Array State |
|---|---------|-----------|------------|--------|---|-------------|
| 0 | 1 | 1 | No | Skip | 1 | [1, 1, 2, 2, 3, 4, 4, 5] |
| 1 | 1 | 2 | Yes | nums[1] = 2, j++ | 2 | [1, 2, 2, 2, 3, 4, 4, 5] |
| 2 | 2 | 2 | No | Skip | 2 | [1, 2, 2, 2, 3, 4, 4, 5] |
| 3 | 2 | 3 | Yes | nums[2] = 3, j++ | 3 | [1, 2, 3, 2, 3, 4, 4, 5] |
| 4 | 3 | 4 | Yes | nums[3] = 4, j++ | 4 | [1, 2, 3, 4, 3, 4, 4, 5] |
| 5 | 4 | 4 | No | Skip | 4 | [1, 2, 3, 4, 3, 4, 4, 5] |
| 6 | 4 | 5 | Yes | nums[4] = 5, j++ | 5 | [1, 2, 3, 4, 5, 4, 4, 5] |

**Result:** First 5 elements are `[1, 2, 3, 4, 5]`, return 5

**Complexity:**
- **Time**: O(n) - single pass
- **Space**: O(1) - in-place modification

---

### Problem 5: Merge Two Sorted Arrays

**Problem Statement:** Given two sorted arrays, merge them into a single sorted array.

**Example:**
- Input: `arr1 = [1, 3, 5, 7]`, `arr2 = [2, 4, 6, 8]`
- Output: `[1, 2, 3, 4, 5, 6, 7, 8]`

**Algorithm (Two Pointers):**
1. Initialize three pointers: `i = 0` (for arr1), `j = 0` (for arr2), `k = 0` (for merged array)
2. While both arrays have elements:
   - Compare `arr1[i]` and `arr2[j]`
   - Add smaller element to merged array
   - Increment corresponding pointer
3. Copy remaining elements from the non-empty array

**Code:**
```javascript
function mergeSortedArrays(arr1, arr2) {
    let n = arr1.length;
    let m = arr2.length;
    let merged = new Array(n + m);
    
    let i = 0, j = 0, k = 0;
    
    // Merge while both arrays have elements
    while(i < n && j < m) {
        if(arr1[i] < arr2[j]) {
            merged[k] = arr1[i];
            i++;
        } else {
            merged[k] = arr2[j];
            j++;
        }
        k++;
    }
    
    // Copy remaining elements from arr1
    while(i < n) {
        merged[k] = arr1[i];
        i++;
        k++;
    }
    
    // Copy remaining elements from arr2
    while(j < m) {
        merged[k] = arr2[j];
        j++;
        k++;
    }
    
    return merged;
}

// Test
let arr1 = [1, 3, 5, 7];
let arr2 = [2, 4, 6, 8];
console.log(mergeSortedArrays(arr1, arr2));  // [1, 2, 3, 4, 5, 6, 7, 8]
```

**Dry Run:**

| Step | i | j | k | arr1[i] | arr2[j] | Smaller | merged | Action |
|------|---|---|---|---------|---------|---------|--------|--------|
| 1 | 0 | 0 | 0 | 1 | 2 | 1 | [1] | i++, k++ |
| 2 | 1 | 0 | 1 | 3 | 2 | 2 | [1, 2] | j++, k++ |
| 3 | 1 | 1 | 2 | 3 | 4 | 3 | [1, 2, 3] | i++, k++ |
| 4 | 2 | 1 | 3 | 5 | 4 | 4 | [1, 2, 3, 4] | j++, k++ |
| 5 | 2 | 2 | 4 | 5 | 6 | 5 | [1, 2, 3, 4, 5] | i++, k++ |
| 6 | 3 | 2 | 5 | 7 | 6 | 6 | [1, 2, 3, 4, 5, 6] | j++, k++ |
| 7 | 3 | 3 | 6 | 7 | 8 | 7 | [1, 2, 3, 4, 5, 6, 7] | i++, k++ |
| 8 | 4 | 3 | 7 | - | 8 | 8 | [1, 2, 3, 4, 5, 6, 7, 8] | j++, k++ |

**Complexity:**
- **Time**: O(n + m) - each element visited once
- **Space**: O(n + m) - for merged array

---

### Problem 6: Best Time to Buy and Sell Stock

**Problem Statement:** Given an array of stock prices where `prices[i]` is the price on day i, find the maximum profit from one buy and one sell. You must buy before you sell.

**Example:**
- Input: `[7, 1, 5, 3, 6, 4]`
- Output: `5` (buy at 1, sell at 6)

**LeetCode:** [#121 - Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

**Algorithm:**
1. Track minimum price seen so far
2. For each price, calculate potential profit (current price - min price)
3. Update max profit if current profit is higher

**Code:**
```javascript
function maxProfit(prices) {
    let minPrice = Infinity;
    let maxProfit = 0;
    
    for(let i = 0; i < prices.length; i++) {
        // Update minimum price
        if(prices[i] < minPrice) {
            minPrice = prices[i];
        }
        
        // Calculate potential profit
        let profit = prices[i] - minPrice;
        
        // Update max profit
        if(profit > maxProfit) {
            maxProfit = profit;
        }
    }
    
    return maxProfit;
}

// Test
console.log(maxProfit([7, 1, 5, 3, 6, 4]));  // 5
console.log(maxProfit([7, 6, 4, 3, 1]));     // 0 (no profit possible)
```

**Dry Run ([7, 1, 5, 3, 6, 4]):**

| i | prices[i] | minPrice before | profit | maxProfit before | minPrice after | maxProfit after |
|---|-----------|-----------------|--------|------------------|----------------|-----------------|
| 0 | 7 | ∞ | - | 0 | 7 | 0 |
| 1 | 1 | 7 | 1-7=-6 | 0 | 1 | 0 |
| 2 | 5 | 1 | 5-1=4 | 0 | 1 | 4 |
| 3 | 3 | 1 | 3-1=2 | 4 | 1 | 4 |
| 4 | 6 | 1 | 6-1=5 | 4 | 1 | 5 |
| 5 | 4 | 1 | 4-1=3 | 5 | 1 | 5 |

**Result:** maxProfit = 5 (buy at 1, sell at 6)

**Key Insight:** We always buy at the lowest price seen so far and check if selling today gives better profit.

**Complexity:**
- **Time**: O(n) - single pass
- **Space**: O(1) - only two variables

---

### Problem 7: Sort Colors (Dutch National Flag Problem)

**Problem Statement:** Given an array with 0s, 1s, and 2s (representing red, white, blue), sort them in-place.

**Example:**
- Input: `[2, 0, 2, 1, 1, 0]`
- Output: `[0, 0, 1, 1, 2, 2]`

**Constraints:**
- No built-in sort function
- In-place sorting
- Single pass preferred

**LeetCode:** [#75 - Sort Colors](https://leetcode.com/problems/sort-colors/)

**Algorithm (Three Pointers):**
1. Initialize three pointers:
   - `j = 0`: boundary for 0s (next position to place 0)
   - `k = n-1`: boundary for 2s (next position to place 2)
   - `i = 0`: current element being examined
2. While `i <= k`:
   - If `arr[i] == 0`: swap with `arr[j]`, increment both `i` and `j`
   - If `arr[i] == 1`: just increment `i` (1s naturally settle in middle)
   - If `arr[i] == 2`: swap with `arr[k]`, decrement `k` (don't increment `i` yet!)

**Code:**
```javascript
function sortColors(nums) {
    let j = 0;              // Boundary for 0s
    let k = nums.length - 1;  // Boundary for 2s
    let i = 0;              // Current position
    
    while(i <= k) {
        if(nums[i] === 0) {
            // Swap with j position and move both forward
            [nums[i], nums[j]] = [nums[j], nums[i]];
            i++;
            j++;
        }