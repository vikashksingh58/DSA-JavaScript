# Complete Data Structures & Algorithms - Master Study Guide

> **Comprehensive guide covering Pattern Programming, Arrays, Two Pointers, Binary Search, and Hashing**  
> **Source:** Sharians Coding School - Ali Ansari & Harsh Vandana Sharma

---

## 📚 Table of Contents

1. [Pattern Programming](#1-pattern-programming)
2. [Arrays in JavaScript](#2-arrays-in-javascript)
3. [Two Pointer Algorithms](#3-two-pointer-algorithms)
4. [Binary Search Problems](#4-binary-search-problems)
   - Search in Rotated Sorted Array
   - Allocate Minimum Pages
   - Koko Eating Bananas
5. [Hashing, Sets, and Maps](#5-hashing-sets-and-maps)

---

# 1. Pattern Programming

## Core Philosophy
- **Observation over Memorization**: Learn through understanding logic, not rote learning
- **Foundation for Algorithms**: Essential for developing algorithmic thinking

## Environment Setup

### Node.js vs Browser

| Method | Environment | Behavior |
|--------|-------------|----------|
| `console.log()` | Both | Prints with newline |
| `process.stdout.write()` | Node.js only | Prints without newline |

### Running Node.js
```bash
# Open terminal: Ctrl + `
node app.js
```

### User Input
```bash
npm install prompt-sync
```
```javascript
const prompt = require('prompt-sync')();
let n = prompt("Enter number: ");
```

## Essential Patterns

### 1. Square Pattern (n × n)
```javascript
for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= n; j++) {
        process.stdout.write("* ");
    }
    console.log();
}
```

### 2. Right-Angled Triangle
```javascript
for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= i; j++) {
        process.stdout.write("* ");
    }
    console.log();
}
```

### 3. Inverted Triangle
```javascript
for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= n - i + 1; j++) {
        process.stdout.write("* ");
    }
    console.log();
}
```

### 4. Mirror Triangle (Right-Aligned)
```javascript
for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= n - i; j++) {
        process.stdout.write("  ");
    }
    for (let j = 1; j <= i; j++) {
        process.stdout.write("* ");
    }
    console.log();
}
```

### 5. X Pattern
```javascript
for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= n; j++) {
        if (i === j || i + j === n + 1) {
            process.stdout.write("* ");
        } else {
            process.stdout.write("  ");
        }
    }
    console.log();
}
```

## Key Concepts
- Outer loop controls rows
- Inner loop controls columns
- Use conditions for diagonal patterns
- Nested loops for 2D patterns

---

# 2. Arrays in JavaScript

## Array Fundamentals

### What is an Array?
- **Linear data structure** storing multiple values in contiguous memory
- **Zero-based indexing**: first element at index 0
- **Dynamic length** in JavaScript

### Basic Operations

```javascript
// Create array
let arr = [10, 20, 30, 40, 50];

// Access elements
console.log(arr[0]);  // 10

// Add element (end)
arr.push(60);

// Remove element (end)
arr.pop();

// Length
console.log(arr.length);
```

## Common Array Operations

### 1. Sum of Elements
```javascript
let sum = 0;
for(let i = 0; i < arr.length; i++) {
    sum += arr[i];
}
```
**Complexity:** O(n)

### 2. Find Maximum
```javascript
let max = arr[0];
for(let i = 1; i < arr.length; i++) {
    if(arr[i] > max) {
        max = arr[i];
    }
}
```
**Complexity:** O(n)

### 3. Find Second Maximum
```javascript
let max = Math.max(arr[0], arr[1]);
let secondMax = Math.min(arr[0], arr[1]);

for(let i = 2; i < arr.length; i++) {
    if(arr[i] > max) {
        secondMax = max;
        max = arr[i];
    } else if(arr[i] > secondMax && arr[i] !== max) {
        secondMax = arr[i];
    }
}
```
**Complexity:** O(n)

### 4. Reverse Array (In-Place)
```javascript
let i = 0, j = arr.length - 1;
while(i < j) {
    [arr[i], arr[j]] = [arr[j], arr[i]];
    i++;
    j--;
}
```
**Complexity:** O(n), Space: O(1)

### 5. Segregate 0s and 1s
```javascript
let i = 0, j = 0;
while(i < arr.length) {
    if(arr[i] === 0) {
        [arr[i], arr[j]] = [arr[j], arr[i]];
        i++;
        j++;
    } else {
        i++;
    }
}
```
**Complexity:** O(n)

---

# 3. Two Pointer Algorithms

## Core Technique
Use two pointers to traverse array efficiently, often reducing O(n²) to O(n).

## Pattern Types

### 1. Opposite Direction
```javascript
let i = 0, j = arr.length - 1;
while(i < j) {
    // Process arr[i] and arr[j]
    i++;
    j--;
}
```

### 2. Same Direction (Fast-Slow)
```javascript
let i = 0, j = 0;
while(i < arr.length) {
    if(condition) {
        i++; j++;
    } else {
        i++;
    }
}
```

## Array Rotation Problems

### Left Rotation by One
```javascript
let temp = arr[0];
for(let i = 0; i < n - 1; i++) {
    arr[i] = arr[i + 1];
}
arr[n - 1] = temp;
```

### Right Rotation by One
```javascript
let temp = arr[n - 1];
for(let i = n - 1; i > 0; i--) {
    arr[i] = arr[i - 1];
}
arr[0] = temp;
```

### Rotation by K (Optimal - Reversal Algorithm)
```javascript
function reverse(arr, start, end) {
    while(start < end) {
        [arr[start], arr[end]] = [arr[end], arr[start]];
        start++;
        end--;
    }
}

// Left rotation by k
reverse(arr, 0, k - 1);
reverse(arr, k, n - 1);
reverse(arr, 0, n - 1);
```
**Complexity:** O(n), Space: O(1)

## Classic Two Pointer Problems

### 1. Remove Duplicates (Sorted Array)
```javascript
function removeDuplicates(nums) {
    let j = 1;
    for(let i = 0; i < nums.length - 1; i++) {
        if(nums[i] !== nums[i + 1]) {
            nums[j] = nums[i + 1];
            j++;
        }
    }
    return j;
}
```
**LeetCode #26** | O(n) time, O(1) space

### 2. Merge Sorted Arrays
```javascript
function merge(arr1, arr2) {
    let i = 0, j = 0, k = 0;
    let merged = [];
    
    while(i < arr1.length && j < arr2.length) {
        if(arr1[i] < arr2[j]) {
            merged[k++] = arr1[i++];
        } else {
            merged[k++] = arr2[j++];
        }
    }
    
    while(i < arr1.length) merged[k++] = arr1[i++];
    while(j < arr2.length) merged[k++] = arr2[j++];
    
    return merged;
}
```
**O(n + m) time**

### 3. Sort Colors (Dutch National Flag)
```javascript
function sortColors(nums) {
    let i = 0, j = 0, k = nums.length - 1;
    
    while(i <= k) {
        if(nums[i] === 0) {
            [nums[i], nums[j]] = [nums[j], nums[i]];
            i++; j++;
        } else if(nums[i] === 1) {
            i++;
        } else {
            [nums[i], nums[k]] = [nums[k], nums[i]];
            k--;
        }
    }
}
```
**LeetCode #75** | O(n) time, O(1) space

## Famous Algorithms

### Kadane's Algorithm (Maximum Subarray)
```javascript
function maxSubArray(nums) {
    let currentSum = 0;
    let maxSum = -Infinity;
    
    for(let num of nums) {
        currentSum += num;
        maxSum = Math.max(maxSum, currentSum);
        if(currentSum < 0) currentSum = 0;
    }
    
    return maxSum;
}
```
**LeetCode #53** | O(n) time, O(1) space

### Moore's Voting Algorithm (Majority Element)
```javascript
function majorityElement(nums) {
    let candidate = nums[0];
    let count = 1;
    
    for(let i = 1; i < nums.length; i++) {
        if(nums[i] === candidate) {
            count++;
        } else {
            count--;
            if(count === 0) {
                candidate = nums[i];
                count = 1;
            }
        }
    }
    
    return candidate;
}
```
**LeetCode #169** | O(n) time, O(1) space

### Trapping Rain Water
```javascript
function trap(height) {
    let n = height.length;
    let leftMax = new Array(n);
    let rightMax = new Array(n);
    
    leftMax[0] = height[0];
    for(let i = 1; i < n; i++) {
        leftMax[i] = Math.max(leftMax[i-1], height[i]);
    }
    
    rightMax[n-1] = height[n-1];
    for(let i = n-2; i >= 0; i--) {
        rightMax[i] = Math.max(rightMax[i+1], height[i]);
    }
    
    let water = 0;
    for(let i = 0; i < n; i++) {
        water += Math.min(leftMax[i], rightMax[i]) - height[i];
    }
    
    return water;
}
```
**LeetCode #42** | O(n) time, O(n) space

---

# 4. Binary Search Problems

## Pattern: Binary Search on Answer Space

When you see:
- "Minimize the maximum" or "Maximize the minimum"
- Contiguous allocation required
- Feasibility check possible

→ Use Binary Search on Answer!

## Problem 1: Search in Rotated Sorted Array

**LeetCode #33** | Medium

### Problem
Search for target in rotated sorted array in O(log n) time.

### Key Insight
At any mid point, at least one half is sorted.

### Solution
```javascript
function search(nums, target) {
    let first = 0, last = nums.length - 1;
    
    while(first <= last) {
        let mid = Math.floor((first + last) / 2);
        
        if(nums[mid] === target) return mid;
        
        if(nums[first] <= nums[mid]) {
            // Left half sorted
            if(nums[first] <= target && target < nums[mid]) {
                last = mid - 1;
            } else {
                first = mid + 1;
            }
        } else {
            // Right half sorted
            if(nums[mid] < target && target <= nums[last]) {
                first = mid + 1;
            } else {
                last = mid - 1;
            }
        }
    }
    
    return -1;
}
```
**Complexity:** O(log n) time, O(1) space

## Problem 2: Allocate Minimum Pages

**GFG** | Medium-Hard

### Problem
Allocate books to k students such that:
- Each student gets at least one book
- Books are contiguous
- Minimize maximum pages to any student

### Solution Template
```javascript
function allocateMinPages(arr, k) {
    if(k > arr.length) return -1;
    
    let first = Math.max(...arr);
    let last = arr.reduce((a, b) => a + b, 0);
    let answer = -1;
    
    while(first <= last) {
        let mid = Math.floor((first + last) / 2);
        
        if(isValid(arr, k, mid)) {
            answer = mid;
            last = mid - 1;
        } else {
            first = mid + 1;
        }
    }
    
    return answer;
}

function isValid(arr, k, maxPages) {
    let students = 1, currentSum = 0;
    
    for(let pages of arr) {
        if(pages > maxPages) return false;
        
        if(currentSum + pages <= maxPages) {
            currentSum += pages;
        } else {
            students++;
            currentSum = pages;
            if(students > k) return false;
        }
    }
    
    return true;
}
```
**Complexity:** O(n log m) where m = sum of array

## Problem 3: Koko Eating Bananas

**LeetCode #875** | Medium

### Problem
Find minimum eating speed to finish all banana piles in h hours.

### Solution
```javascript
function minEatingSpeed(piles, h) {
    let low = 1;
    let high = Math.max(...piles);
    
    while(low < high) {
        let mid = Math.floor((low + high) / 2);
        
        if(canFinish(piles, mid, h)) {
            high = mid;
        } else {
            low = mid + 1;
        }
    }
    
    return low;
}

function canFinish(piles, speed, h) {
    let totalHours = 0;
    
    for(let pile of piles) {
        totalHours += Math.ceil(pile / speed);
        if(totalHours > h) return false;
    }
    
    return true;
}
```
**Complexity:** O(n log m) where m = max(piles)

### Binary Search Pattern Summary

| Problem | Search Space | Low Bound | High Bound | Goal |
|---------|-------------|-----------|------------|------|
| Rotated Array | Array indices | 0 | n-1 | Find target |
| Allocate Pages | Max pages | max(arr) | sum(arr) | Minimize max |
| Koko Bananas | Eating speed | 1 | max(piles) | Minimize speed |

---

# 5. Hashing, Sets, and Maps

## What is Hashing?

**Hashing** is a technique that converts values into hash codes for O(1) average-case operations.

### Why Hashing?

| Operation | Array | Hashing |
|-----------|-------|---------|
| Search | O(n) | O(1) |
| Insert | O(n) | O(1) |
| Delete | O(n) | O(1) |

## Set Data Structure

### Features
- Stores **unique values only**
- Maintains insertion order
- O(1) operations

### Methods
```javascript
let set = new Set();

set.add(5);           // Add element
set.delete(5);        // Remove element
set.has(5);           // Check existence → boolean
set.size;             // Get count (property!)
set.clear();          // Remove all

for(let val of set) {
    console.log(val);
}
```

### Common Uses

**Remove Duplicates:**
```javascript
let arr = [1, 2, 2, 3, 3, 4];
let unique = [...new Set(arr)];  // [1, 2, 3, 4]
```

**Pangram Check:**
```javascript
function isPangram(str) {
    let letters = new Set();
    for(let char of str) {
        if(char >= 'a' && char <= 'z') {
            letters.add(char);
        }
    }
    return letters.size === 26;
}
```

## Map Data Structure

### Features
- Stores **key-value pairs**
- Keys are unique (any type)
- Maintains insertion order
- O(1) operations

### Methods
```javascript
let map = new Map();

map.set("key", "value");    // Add/update
map.get("key");             // Get value
map.has("key");             // Check key → boolean
map.delete("key");          // Remove entry
map.size;                   // Get count (property!)
map.clear();                // Remove all

map.keys();                 // Iterator of keys
map.values();               // Iterator of values
map.entries();              // Iterator of [k,v]

for(let [key, value] of map) {
    console.log(key, value);
}
```

## Common Problems

### 1. Frequency Counting
```javascript
function countFrequency(arr) {
    let map = new Map();
    for(let num of arr) {
        map.set(num, (map.get(num) || 0) + 1);
    }
    return map;
}
```
**O(n) time, O(k) space**

### 2. Two Sum
```javascript
function twoSum(nums, target) {
    let map = new Map();
    
    for(let i = 0; i < nums.length; i++) {
        let complement = target - nums[i];
        
        if(map.has(complement)) {
            return [map.get(complement), i];
        }
        
        map.set(nums[i], i);
    }
    
    return [];
}
```
**LeetCode #1** | O(n) time, O(n) space

### 3. Subarray Sum Equals K
```javascript
function subarraySum(nums, k) {
    let map = new Map([[0, 1]]);
    let sum = 0, count = 0;
    
    for(let num of nums) {
        sum += num;
        
        if(map.has(sum - k)) {
            count += map.get(sum - k);
        }
        
        map.set(sum, (map.get(sum) || 0) + 1);
    }
    
    return count;
}
```
**LeetCode #560** | O(n) time, O(n) space

### 4. Longest Consecutive Sequence
```javascript
function longestConsecutive(nums) {
    let set = new Set(nums);
    let maxLen = 0;
    
    for(let num of set) {
        if(!set.has(num - 1)) {  // Start of sequence
            let currentNum = num;
            let currentLen = 1;
            
            while(set.has(currentNum + 1)) {
                currentNum++;
                currentLen++;
            }
            
            maxLen = Math.max(maxLen, currentLen);
        }
    }
    
    return maxLen;
}
```
**LeetCode #128** | O(n) time, O(n) space

### 5. Intersection of Arrays
```javascript
function intersection(nums1, nums2) {
    let set1 = new Set(nums1);
    let result = new Set();
    
    for(let num of nums2) {
        if(set1.has(num)) {
            result.add(num);
        }
    }
    
    return [...result];
}
```
**O(n + m) time, O(n) space**

## When to Use What?

### Use Set When:
- Need unique values only
- Fast membership testing
- Remove duplicates
- No key-value relationship

### Use Map When:
- Need key-value associations
- Count frequencies
- Keys can be any type
- Track indices/positions
- Memoization/caching

### Use Object When:
- Simple static configuration
- Keys are strings only
- JSON compatibility needed

---

# 📊 Complexity Summary

## Time Complexities

| Algorithm/Operation | Best | Average | Worst |
|---------------------|------|---------|-------|
| Array Access | O(1) | O(1) | O(1) |
| Array Search (unsorted) | O(1) | O(n) | O(n) |
| Binary Search | O(1) | O(log n) | O(log n) |
| Two Pointers | - | O(n) | O(n) |
| Hash Set/Map Operations | O(1) | O(1) | O(n) |
| Kadane's Algorithm | - | O(n) | O(n) |
| Moore's Voting | - | O(n) | O(n) |

## Space Complexities

| Technique | Space |
|-----------|-------|
| In-place operations | O(1) |
| Extra array | O(n) |
| Hash Set/Map | O(n) |
| Recursion (depth d) | O(d) |

---

# 🎯 Problem-Solving Strategies

## Step-by-Step Approach

1. **Understand the Problem**
   - Read carefully
   - Identify input/output
   - Note constraints

2. **Choose Data Structure**
   - Array manipulation → Two pointers
   - Uniqueness → Set
   - Counting/mapping → Map
   - Search optimization → Binary search

3. **Think of Approach**
   - Brute force first
   - Identify inefficiencies
   - Apply patterns

4. **Implement**
   - Write clean code
   - Handle edge cases
   - Add comments

5. **Test**
   - Dry run with examples
   - Test edge cases
   - Verify complexity

## Common Patterns Recognition

| Pattern | Keywords | Data Structure |
|---------|----------|----------------|
| Contiguous subarray | Sum, maximum, k elements | Prefix sum, sliding window |
| Unique elements | Duplicates, distinct | Set |
| Counting frequency | Occurrences, appears | Map |
| Two elements sum | Target, pair | Map (two sum) |
| Sorted array search | Find, search | Binary search |
| Minimize maximum | Allocate, distribute | Binary search on answer |
| Consecutive sequence | Longest, consecutive | Set |

---

# 💡 Quick Tips

## Arrays
- Always check bounds (`i < arr.length`)
- Initialize accumulators outside loops
- Use two pointers for O(n) solutions

## Binary Search
- Define search space carefully
- Remember: `while(low < high)` vs `while(low <= high)`
- Binary search on answer when minimizing maximum

## Hashing
- Set for uniqueness
- Map for counting/associations
- O(1) average operations

## Two Pointers
- Opposite direction for reversal/two sum
- Same direction for remove duplicates
- Three pointers for partitioning

---

# 🏆 Practice Roadmap

## Week 1: Fundamentals
- [ ] Pattern programming (10 patterns)
- [ ] Array basics and operations
- [ ] Simple two pointer problems

## Week 2: Intermediate
- [ ] Array rotations (all methods)
- [ ] Two sum variants
- [ ] Binary search basics

## Week 3: Advanced Two Pointers
- [ ] Sort colors
- [ ] Trapping rain water
- [ ] Kadane's algorithm
- [ ] Moore's voting

## Week 4: Binary Search Mastery
- [ ] Rotated array search
- [ ] Allocate minimum pages
- [ ] Koko eating bananas
- [ ] Similar problems

## Week 5: Hashing
- [ ] Set operations
- [ ] Map operations
- [ ] Frequency problems
- [ ] Subarray sum problems

## Week 6: Integration
- [ ] Mixed problems
- [ ] LeetCode contests
- [ ] Mock interviews

---

# 📚 Resources

## Online Platforms
- **LeetCode** - Practice problems
- **GeeksforGeeks** - Tutorials and problems
- **HackerRank** - Skill certification

## Problem Lists

### Must-Solve Array Problems
1. Two Sum (#1)
2. Best Time to Buy and Sell Stock (#121)
3. Contains Duplicate (#217)
4. Maximum Subarray (#53)
5. Product of Array Except Self (#238)

### Must-Solve Two Pointer
1. Remove Duplicates from Sorted Array (#26)
2. Container With Most Water (#11)
3. 3Sum (#15)
4. Sort Colors (#75)
5. Trapping Rain Water (#42)

### Must-Solve Binary Search
1. Binary Search (#704)
2. Search in Rotated Sorted Array (#33)
3. Find Minimum in Rotated Sorted Array (#153)
4. Koko Eating Bananas (#875)
5. Capacity To Ship Packages (#1011)

### Must-Solve Hashing
1. Two Sum (#1)
2. Group Anagrams (#49)
3. Longest Consecutive Sequence (#128)
4. Subarray Sum Equals K (#560)
5. LRU Cache (#146)

---

# 🎓 Final Notes

## Key Takeaways

1. **Master the basics** before moving to advanced topics
2. **Practice consistently** - solve problems daily
3. **Understand patterns** rather than memorizing solutions
4. **Dry run examples** to build intuition
5. **Analyze complexity** for every solution
6. **Code from scratch** - don't just read solutions
7. **Review mistakes** and learn from them
8. **Time yourself** to improve speed

## Success Formula

```
Consistent Practice + Pattern Recognition + Problem Solving = Interview Success
```

## Remember

- **Observation > Memorization**
- **O(n) > O(n²)** - Always optimize
- **Space-time tradeoff** - Know when to use extra space
- **Edge cases matter** - Test thoroughly
- **Comment your code** - For interviews and clarity

---

**Good luck with your DSA journey! 🚀**