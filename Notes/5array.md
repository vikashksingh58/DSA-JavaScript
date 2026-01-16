# Arrays in JavaScript - Comprehensive Study Notes

## 📚 Introduction to Arrays

### What is an Array?
An **array** is a linear data structure that stores multiple values in a continuous manner, enclosed within square brackets `[]`.

**Key Characteristics:**
- Collection of multiple elements
- Elements separated by commas
- Can hold different data types (numbers, strings, booleans, objects)
- Zero-based indexing (first element at index 0)
- Dynamic length in JavaScript

**Pronunciation Note:** Correctly pronounce as "array" (not "arre")

### Array as a Linear Data Structure

Arrays are defined by two key properties:

1. **Linear**: Elements are arranged sequentially, one after another
2. **Continuous**: Elements are stored in contiguous (adjacent) memory locations

**Comparison with Other Data Structures:**

| Data Structure | Linear? | Contiguous Memory? | Description |
|----------------|---------|-------------------|-------------|
| Array | ✓ | ✓ | Elements stored sequentially in adjacent memory |
| Linked List | ✓ | ✗ | Elements linked but scattered in memory |
| Tree | ✗ | ✗ | Hierarchical, non-linear structure |
| Graph | ✗ | ✗ | Network-based, non-linear structure |

---

## 🔧 Creating and Manipulating Arrays

### 1. Array Declaration

**Empty Array:**
```javascript
let arr = [];
```

**Array with Elements:**
```javascript
let arr = [10, 20, 30, 40, 50];
```

**Array with Mixed Data Types:**
```javascript
let arr = [100, "hello", true, {name: "John"}];
```

**Best Practice:** Although JavaScript allows mixed types, keep elements of the same data type for better data structure consistency.

### 2. Adding Elements - Push Method

The `.push()` method adds elements to the end of an array.

**Syntax:**
```javascript
arr.push(value);
```

**Example:**
```javascript
let arr = [];
arr.push(100);
arr.push(10);
arr.push(20);
arr.push(30);

console.log(arr);  // Output: [100, 10, 20, 30]
```

**Key Points:**
- Adds element at the end
- Array length increases by 1
- Returns the new length of the array

### 3. Removing Elements - Pop Method

The `.pop()` method removes the last element from an array.

**Syntax:**
```javascript
arr.pop();
```

**Example:**
```javascript
let arr = [10, 20, 30, 40];
arr.pop();
console.log(arr);  // Output: [10, 20, 30]
```

**Key Points:**
- Removes last element
- No arguments needed
- Returns the removed element
- Array length decreases by 1

### 4. Accessing Elements - Indexing

Arrays use **zero-based indexing**: first element is at index 0.

**Syntax:**
```javascript
arr[index]
```

**Example:**
```javascript
let arr = [10, 20, 30, 40, 50];

console.log(arr[0]);  // Output: 10 (first element)
console.log(arr[1]);  // Output: 20 (second element)
console.log(arr[4]);  // Output: 50 (fifth element)
```

**Index Range:**
- First element: `arr[0]`
- Last element: `arr[arr.length - 1]`

### 5. Assigning Values to Specific Indices

You can directly assign values to any index position.

**Syntax:**
```javascript
arr[index] = value;
```

**Example:**
```javascript
let arr = [];
arr[0] = 100;
arr[1] = 20;
arr[2] = 30;

console.log(arr);  // Output: [100, 20, 30]
```

### 6. Dynamic Length Arrays

JavaScript arrays are **dynamic** - they can grow or shrink as needed, unlike fixed-size arrays in Java or C++.

**Example of Dynamic Expansion:**
```javascript
let arr = [10, 20, 30];  // Length: 3
arr[7] = 100;            // Assign at index 7

console.log(arr);        
// Output: [10, 20, 30, undefined, undefined, undefined, undefined, 100]
console.log(arr.length); // Output: 8
```

**What Happens:**
- Assigning beyond current length expands the array
- Intermediate indices (3-6) become `undefined`
- Array length automatically adjusts

### 7. Push with Predefined Length

When you push to an array with predefined length, the new element goes after the existing elements.

**Example:**
```javascript
let arr = new Array(3);  // Create array of length 3
arr[0] = 10;
arr[1] = 20;
arr[2] = 30;

arr.push(40);  // Adds at index 3

console.log(arr);        // Output: [10, 20, 30, 40]
console.log(arr.length); // Output: 4
```

---

## 📝 Taking Array Input from User

### Using Prompt in a Loop

To take multiple inputs from the user, use `prompt()` inside a loop.

**Code Pattern:**
```javascript
let arr = [];
let n = 5;  // Number of inputs

for(let i = 0; i < n; i++) {
    arr[i] = prompt("Enter value " + (i + 1) + ": ");
}

console.log(arr);
```

**For Numeric Input:**
```javascript
let arr = [];
let n = parseInt(prompt("How many numbers? "));

for(let i = 0; i < n; i++) {
    arr[i] = parseInt(prompt("Enter number " + (i + 1) + ": "));
}

console.log(arr);
```

**Key Points:**
- Use loop to avoid repetitive code
- Convert string input to number using `parseInt()` or `Number()`
- Store each input at current index `i`

---

## 🔄 Array Traversal

### Basic Traversal Pattern

**Using For Loop:**
```javascript
let arr = [10, 20, 30, 40, 50];

for(let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
```

**Key Components:**
- **Initialization**: `i = 0` (start at first index)
- **Condition**: `i < arr.length` (loop until last element)
- **Increment**: `i++` (move to next element)
- **Access**: `arr[i]` (current element)

---

## 📊 Common Array Operations

### 1. Sum of Array Elements

**Problem:** Calculate the sum of all elements in an array.

**Algorithm:**
1. Initialize sum variable to 0
2. Traverse the array
3. Add each element to sum
4. Print final sum

**Code:**
```javascript
let arr = [10, 20, 30, 40, 50];
let sum = 0;

for(let i = 0; i < arr.length; i++) {
    sum = sum + arr[i];  // or sum += arr[i]
}

console.log("Sum:", sum);  // Output: Sum: 150
```

**Important Note:** 
- Initialize `sum = 0` **outside** the loop
- If initialized inside, sum resets on each iteration
- Use `sum = sum + arr[i]` not `sum = arr[i]` (which would just assign, not accumulate)

**Dry Run Example (arr = [10, 20, 30]):**

| Iteration | i | arr[i] | sum before | sum after |
|-----------|---|--------|------------|-----------|
| Initial | - | - | - | 0 |
| 1 | 0 | 10 | 0 | 10 |
| 2 | 1 | 20 | 10 | 30 |
| 3 | 2 | 30 | 30 | 60 |

---

### 2. Finding Maximum Element

**Problem:** Find the largest element in an array without sorting.

**Algorithm:**
1. Assume first element as maximum
2. Traverse array from second element
3. Compare each element with current maximum
4. If element is greater, update maximum
5. Return maximum

**Code:**
```javascript
let arr = [13, 78, 100, 4];
let max = arr[0];  // Assume first element is max

for(let i = 1; i < arr.length; i++) {
    if(arr[i] > max) {
        max = arr[i];
    }
}

console.log("Maximum:", max);  // Output: Maximum: 100
```

**Dry Run Example (arr = [13, 78, 100, 4]):**

| Iteration | i | arr[i] | max before | Condition | max after |
|-----------|---|--------|------------|-----------|-----------|
| Initial | - | - | - | - | 13 |
| 1 | 1 | 78 | 13 | 78 > 13 ✓ | 78 |
| 2 | 2 | 100 | 78 | 100 > 78 ✓ | 100 |
| 3 | 3 | 4 | 100 | 4 > 100 ✗ | 100 |

**Time Complexity:** O(n) - single pass through array
**Space Complexity:** O(1) - only one extra variable

---

### 3. Finding Second Maximum Element

**Problem:** Find the second largest element without sorting.

**Algorithm:**
1. Initialize `max` and `secondMax` using first two elements
   - `max` = larger of first two
   - `secondMax` = smaller of first two
2. Traverse from third element
3. For each element:
   - If element > max: `secondMax = max`, `max = element`
   - Else if element > secondMax AND element ≠ max: `secondMax = element`
4. Return secondMax

**Code:**
```javascript
let arr = [13, 78, 100, 4, 95];

// Initialize with first two elements
let max, secondMax;
if(arr[0] > arr[1]) {
    max = arr[0];
    secondMax = arr[1];
} else {
    max = arr[1];
    secondMax = arr[0];
}

// Traverse from third element
for(let i = 2; i < arr.length; i++) {
    if(arr[i] > max) {
        secondMax = max;
        max = arr[i];
    } else if(arr[i] > secondMax && arr[i] !== max) {
        secondMax = arr[i];
    }
}

console.log("Second Maximum:", secondMax);  // Output: Second Maximum: 95
```

**Dry Run Example (arr = [13, 78, 100, 4, 95]):**

| Step | Element | max before | secondMax before | Action | max after | secondMax after |
|------|---------|------------|------------------|--------|-----------|-----------------|
| Initialize | arr[0]=13, arr[1]=78 | - | - | 78 > 13 | 78 | 13 |
| i=2 | 100 | 78 | 13 | 100 > 78 | 100 | 78 |
| i=3 | 4 | 100 | 78 | 4 < 78 | 100 | 78 |
| i=4 | 95 | 100 | 78 | 78 < 95 < 100 | 100 | 95 |

**Edge Cases Handled:**
- Duplicate maximum values (using `arr[i] !== max` condition)
- Ensures secondMax is always less than max

**Time Complexity:** O(n)
**Space Complexity:** O(1)

---

### 4. Reversing an Array

There are two approaches to reverse an array:

#### Method 1: With Extra Space

Create a new array and copy elements in reverse order.

**Algorithm:**
1. Create new array of same length
2. Copy elements from original array in reverse
3. Return new array

**Code:**
```javascript
let arr = [10, 20, 30, 40, 50];
let reversed = [];

for(let i = arr.length - 1; i >= 0; i--) {
    reversed.push(arr[i]);
}

console.log("Original:", arr);      // [10, 20, 30, 40, 50]
console.log("Reversed:", reversed);  // [50, 40, 30, 20, 10]
```

**Characteristics:**
- Uses O(n) extra space
- Original array remains unchanged
- Simple to implement

#### Method 2: In-Place Reversal (Without Extra Space)

Use two pointers to swap elements from both ends.

**Algorithm:**
1. Initialize two pointers: `i` at start (0), `j` at end (length-1)
2. While `i < j`:
   - Swap elements at `i` and `j`
   - Increment `i`, decrement `j`
3. Array is reversed when pointers meet

**Code:**
```javascript
let arr = [10, 20, 30, 40, 50];
let i = 0;
let j = arr.length - 1;

while(i < j) {
    // Swap arr[i] and arr[j]
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    
    i++;
    j--;
}

console.log("Reversed:", arr);  // [50, 40, 30, 20, 10]
```

**Dry Run Example (arr = [10, 20, 30, 40, 50]):**

| Step | i | j | arr[i] | arr[j] | Action | Array After Swap |
|------|---|---|--------|--------|--------|------------------|
| Initial | 0 | 4 | 10 | 50 | Swap | [50, 20, 30, 40, 10] |
| 2 | 1 | 3 | 20 | 40 | Swap | [50, 40, 30, 20, 10] |
| 3 | 2 | 2 | 30 | 30 | Stop (i >= j) | [50, 40, 30, 20, 10] |

**Characteristics:**
- Uses O(1) extra space (only temp variable)
- Original array is modified
- More memory efficient
- **Preferred for large arrays**

**Comparison:**

| Aspect | With Extra Space | In-Place |
|--------|------------------|----------|
| Space Complexity | O(n) | O(1) |
| Original Array | Unchanged | Modified |
| Implementation | Simple | Slightly complex |
| Memory Efficiency | Lower | Higher ✓ |

---

### 5. Segregating Zeros and Ones

**Problem:** Move all zeros to the left side and all ones to the right side of an array containing only 0s and 1s.

**Example:**
- Input: `[1, 0, 1, 0, 0, 1, 1, 0]`
- Output: `[0, 0, 0, 0, 1, 1, 1, 1]`

**Algorithm (Two-Pointer Technique):**
1. Initialize two pointers: `i = 0`, `j = 0`
2. Traverse array with `i`:
   - If `arr[i] == 0`: swap `arr[i]` with `arr[j]`, increment both `i` and `j`
   - If `arr[i] == 1`: only increment `i`
3. Result: all zeros before index `j`, all ones after

**Code:**
```javascript
let arr = [1, 0, 1, 0, 0, 1, 1, 0];
let i = 0;
let j = 0;

while(i < arr.length) {
    if(arr[i] === 0) {
        // Swap arr[i] and arr[j]
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        
        i++;
        j++;
    } else {
        i++;
    }
}

console.log("Segregated:", arr);  // [0, 0, 0, 0, 1, 1, 1, 1]
```

**Detailed Dry Run:**

| Step | i | j | arr[i] | Action | Array State | Explanation |
|------|---|---|--------|--------|-------------|-------------|
| Initial | 0 | 0 | 1 | i++ | [1, 0, 1, 0, 0, 1, 1, 0] | Found 1, skip |
| 1 | 1 | 0 | 0 | Swap, i++, j++ | [0, 1, 1, 0, 0, 1, 1, 0] | Swap positions 0 and 1 |
| 2 | 2 | 1 | 1 | i++ | [0, 1, 1, 0, 0, 1, 1, 0] | Found 1, skip |
| 3 | 3 | 1 | 0 | Swap, i++, j++ | [0, 0, 1, 1, 0, 1, 1, 0] | Swap positions 1 and 3 |
| 4 | 4 | 2 | 0 | Swap, i++, j++ | [0, 0, 0, 1, 1, 1, 1, 0] | Swap positions 2 and 4 |
| 5 | 5 | 3 | 1 | i++ | [0, 0, 0, 1, 1, 1, 1, 0] | Found 1, skip |
| 6 | 6 | 3 | 1 | i++ | [0, 0, 0, 1, 1, 1, 1, 0] | Found 1, skip |
| 7 | 7 | 3 | 0 | Swap, i++, j++ | [0, 0, 0, 0, 1, 1, 1, 1] | Swap positions 3 and 7 |
| Done | 8 | 4 | - | Stop | [0, 0, 0, 0, 1, 1, 1, 1] | i reached end |

**Key Points:**
- **Pointer `j`**: Tracks the position where next zero should go
- **Pointer `i`**: Traverses the entire array
- When zero is found, it's swapped to position `j`
- `j` only increments when a zero is placed
- All elements before `j` are zeros
- All elements from `j` onward are ones

**Time Complexity:** O(n) - single pass
**Space Complexity:** O(1) - constant extra space
**Technique:** Two-pointer with conditional swap

---

## 🎯 Summary of Operations

### Quick Reference Table

| Operation | Method/Technique | Time Complexity | Space Complexity |
|-----------|------------------|-----------------|------------------|
| Create Array | `let arr = []` | O(1) | O(n) |
| Add Element | `arr.push(value)` | O(1) | - |
| Remove Last | `arr.pop()` | O(1) | - |
| Access Element | `arr[index]` | O(1) | - |
| Traverse | For loop | O(n) | O(1) |
| Sum Elements | Loop + accumulator | O(n) | O(1) |
| Find Max | Loop + comparison | O(n) | O(1) |
| Find Second Max | Loop + two variables | O(n) | O(1) |
| Reverse (extra space) | New array + reverse copy | O(n) | O(n) |
| Reverse (in-place) | Two pointers + swap | O(n) | O(1) |
| Segregate 0s & 1s | Two pointers + conditional swap | O(n) | O(1) |

### Common Code Patterns

#### 1. Array Traversal Pattern
```javascript
for(let i = 0; i < arr.length; i++) {
    // Process arr[i]
}
```

#### 2. Accumulator Pattern (Sum, Product, etc.)
```javascript
let result = initialValue;  // Outside loop!
for(let i = 0; i < arr.length; i++) {
    result = result operator arr[i];
}
```

#### 3. Finding Max/Min Pattern
```javascript
let max = arr[0];
for(let i = 1; i < arr.length; i++) {
    if(arr[i] > max) {
        max = arr[i];
    }
}
```

#### 4. Two-Pointer Swap Pattern
```javascript
let i = startIndex;
let j = endIndex;
while(i < j) {
    // Swap arr[i] and arr[j]
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    i++;
    j--;
}
```

#### 5. User Input Collection Pattern
```javascript
let arr = [];
for(let i = 0; i < n; i++) {
    arr[i] = prompt("Enter value: ");
}
```

---

## 💡 Important Concepts & Best Practices

### 1. Variable Placement in Loops

**❌ Wrong - Variable Inside Loop:**
```javascript
for(let i = 0; i < arr.length; i++) {
    let sum = 0;  // WRONG: Resets every iteration
    sum += arr[i];
}
```

**✓ Correct - Variable Outside Loop:**
```javascript
let sum = 0;  // CORRECT: Maintains value across iterations
for(let i = 0; i < arr.length; i++) {
    sum += arr[i];
}
```

### 2. Array Length Property

**Dynamic Property:**
```javascript
let arr = [10, 20, 30];
console.log(arr.length);  // 3

arr.push(40);
console.log(arr.length);  // 4

arr[10] = 50;
console.log(arr.length);  // 11 (not 5!)
```

### 3. Undefined vs Empty Slots

```javascript
let arr = new Array(5);
console.log(arr);  // [undefined, undefined, undefined, undefined, undefined]

arr[2] = 100;
console.log(arr);  // [undefined, undefined, 100, undefined, undefined]
```

### 4. Data Type Consistency

**Technically Allowed:**
```javascript
let arr = [1, "hello", true, {x: 10}];  // Works but not recommended
```

**Recommended:**
```javascript
let numbers = [1, 2, 3, 4, 5];          // All numbers
let strings = ["a", "b", "c"];          // All strings
let objects = [{x:1}, {x:2}];           // All objects
```

### 5. Assignment vs Accumulation

**Assignment (Wrong for sum):**
```javascript
sum = arr[i];  // Just assigns current value
```

**Accumulation (Correct for sum):**
```javascript
sum = sum + arr[i];  // or sum += arr[i];
```

---

## 📝 Homework Assignments

### 1. Find Minimum Element
Write a program to find the smallest element in an array.

**Hint:** Similar to finding maximum, but use `<` comparison instead of `>`

**Expected Approach:**
```javascript
let min = arr[0];
for(let i = 1; i < arr.length; i++) {
    if(arr[i] < min) {
        min = arr[i];
    }
}
```

### 2. Find Second Minimum Element
Write a program to find the second smallest element without sorting.

**Hint:** Similar to second maximum algorithm, adjust comparison operators

**Expected Variables:**
- `min`: smallest element
- `secondMin`: second smallest element

### 3. Segregate Negative and Positive Numbers
Move all negative numbers to the left and positive numbers to the right.

**Example:**
- Input: `[1, -2, 3, -4, -5, 6]`
- Output: `[-2, -4, -5, 1, 3, 6]` (order within group doesn't matter)

**Hint:** Use two-pointer technique similar to zero-one segregation
- When you find negative number, swap with position `j`
- Increment `j` only for negative numbers

---

## 🎓 Key Takeaways

1. **Arrays are linear, contiguous data structures** - Elements stored sequentially in adjacent memory locations

2. **JavaScript arrays are dynamic** - Length can change, unlike fixed arrays in Java/C++

3. **Zero-based indexing** - First element at index 0, last at `length - 1`

4. **Push adds to end, Pop removes from end** - Both are O(1) operations

5. **Always initialize accumulators outside loops** - Variables like sum, max need to persist across iterations

6. **Two-pointer technique is powerful** - Used for in-place operations like reversal and segregation

7. **In-place algorithms save memory** - Prefer O(1) space over O(n) when possible

8. **Traversal pattern is fundamental** - Master the basic for loop structure for arrays

9. **Direct index assignment creates gaps** - Assigning beyond length creates undefined slots

10. **Practice is essential** - Multiple viewings and hands-on coding needed for mastery

---

## 🚀 Practice Recommendations

### Beginner Level
1. Create arrays and practice push/pop operations
2. Write programs to print array elements
3. Calculate sum and product of array elements
4. Find maximum and minimum in arrays

### Intermediate Level
5. Find second maximum and second minimum
6. Reverse arrays using both methods
7. Implement segregation algorithms
8. Search for elements in arrays

### Advanced Level
9. Rotate arrays by k positions
10. Remove duplicates from arrays
11. Merge two sorted arrays
12. Find common elements in two arrays

---

## 📌 Common Mistakes to Avoid

### 1. Loop Boundary Errors
```javascript
// ❌ Wrong: Goes out of bounds
for(let i = 0; i <= arr.length; i++) {
    console.log(arr[i]);
}

// ✓ Correct
for(let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
```

### 2. Resetting Variables Inside Loop
```javascript
// ❌ Wrong
for(let i = 0; i < arr.length; i++) {
    let sum = 0;
    sum += arr[i];
}

// ✓ Correct
let sum = 0;
for(let i = 0; i < arr.length; i++) {
    sum += arr[i];
}
```

### 3. Not Converting String to Number
```javascript
// ❌ Wrong: Concatenates strings
let x = prompt("Enter number");
let y = prompt("Enter number");
console.log(x + y);  // "1020" if inputs are 10 and 20

// ✓ Correct
let x = parseInt(prompt("Enter number"));
let y = parseInt(prompt("Enter number"));
console.log(x + y);  // 30
```

### 4. Off-by-One in Two-Pointer
```javascript
// ❌ Wrong: Swaps middle element with itself
while(i <= j) {  // Should be i < j
    swap(arr[i], arr[j]);
}

// ✓ Correct
while(i < j) {
    swap(arr[i], arr[j]);
}
```

---

## 📚 Quick Reference Cheat Sheet

```javascript
// ARRAY BASICS
let arr = [];                    // Empty array
let arr = [1, 2, 3];            // Array with elements
arr.push(4);                     // Add to end
arr.pop();                       // Remove from end
arr[0];                          // Access first element
arr[arr.length - 1];            // Access last element

// TRAVERSAL
for(let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}

// SUM
let sum = 0;
for(let i = 0; i < arr.length; i++) {
    sum += arr[i];
}

// FIND MAX
let max = arr[0];
for(let i = 1; i < arr.length; i++) {
    if(arr[i] > max) max = arr[i];
}

// REVERSE IN-PLACE
let i = 0, j = arr.length - 1;
while(i < j) {
    [arr[i], arr[j]] = [arr[j], arr[i]];  // ES6 swap
    i++; j--;
}

// TWO-POINTER SEGREGATION
let i = 0, j = 0;
while(i < arr.length) {
    if(condition) {
        swap(arr[i], arr[j]);
        i++; j++;
    } else {
        i++;
    }
}
```

---
