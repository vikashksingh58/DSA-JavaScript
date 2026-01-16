# Hashing, Sets, and Maps - Complete Study Guide

## 📚 Introduction to Hashing

### What is Hashing?

**Definition:** Hashing is a technique (not a data structure) that converts a value into a unique-sized code called a **hash code**, used for fast storing and accessing of data.

**Key Characteristics:**
- **Technique** like recursion (not a data structure itself)
- Converts values to hash codes for quick access
- Enables **O(1)** average-case operations
- Used internally by Objects, Maps, and Sets

### Real-World Analogy

**Gym Locker System:**
```
Member → Given Key (Hash Code) → Direct Access to Locker
```

Instead of searching through all lockers randomly, you use a key (hash code) to directly access your specific locker. Similarly, hashing provides direct access to data using hash codes.

---

## 🎯 Why Do We Need Hashing?

### Comparison: Arrays vs Hashing

| Operation | Unsorted Array | Hashing (Average Case) |
|-----------|---------------|----------------------|
| **Search** | O(n) - Linear search | O(1) - Direct access |
| **Insertion** | O(n) - May need shifting | O(1) - Direct placement |
| **Deletion** | O(n) - Shifting required | O(1) - Direct removal |

**Example:**
```javascript
// Array: Finding element 7 in [1, 3, 5, 7, 9, 11]
// Worst case: Check all 6 elements → O(n)

// Hash Map: Finding element with key "name"
// Direct access using hash code → O(1)
```

### Key Benefits

1. **Constant Time Operations** - O(1) average case
2. **Fast Data Retrieval** - No need to search linearly
3. **Efficient Memory Usage** - Smart storage organization
4. **Flexible Data Types** - Store any type of data

---

## 📦 Data Structures Using Hashing

### Three Main Structures

1. **Objects** (JavaScript)
   - Key-value pairs
   - Keys must be strings or symbols
   - No guaranteed order

2. **Maps**
   - Key-value pairs
   - Keys can be any data type
   - Maintains insertion order

3. **Sets**
   - Stores unique values only
   - No key-value pairs
   - Maintains insertion order

---

## 🔷 Set Data Structure

### What is a Set?

A **Set** is a collection that stores **only unique values** in insertion order.

**Key Features:**
- **Unique elements only** - duplicates automatically ignored
- **Maintains insertion order**
- **Fast membership testing** - O(1)
- **Iterable** - can use for...of loops

### Creating and Using Sets

```javascript
// Create an empty set
let mySet = new Set();

// Create set from array
let numbers = new Set([1, 2, 3, 4, 5]);

// Duplicates are automatically removed
let withDuplicates = new Set([1, 2, 2, 3, 3, 3]);
console.log(withDuplicates);  // Set {1, 2, 3}
```

### Set Methods

| Method | Description | Returns | Example |
|--------|-------------|---------|---------|
| `set.add(value)` | Adds value to set | The set itself | `set.add(5)` |
| `set.delete(value)` | Removes value | true/false | `set.delete(5)` |
| `set.has(value)` | Checks existence | true/false | `set.has(5)` |
| `set.size` | Number of elements | Number | `set.size` |
| `set.clear()` | Removes all elements | undefined | `set.clear()` |

**Important:** `size` is a **property**, not a method (no parentheses!)

### Examples

```javascript
let fruits = new Set();

// Adding elements
fruits.add("apple");
fruits.add("banana");
fruits.add("orange");
fruits.add("apple");  // Duplicate - ignored

console.log(fruits.size);  // 3 (not 4!)

// Checking membership
console.log(fruits.has("banana"));  // true
console.log(fruits.has("grape"));   // false

// Deleting
fruits.delete("banana");
console.log(fruits.size);  // 2

// Iterating
for (let fruit of fruits) {
    console.log(fruit);
}
// Output:
// apple
// orange
```

### Converting Between Arrays and Sets

```javascript
// Array to Set (removes duplicates)
let arr = [1, 2, 2, 3, 3, 3, 4];
let uniqueSet = new Set(arr);
console.log(uniqueSet);  // Set {1, 2, 3, 4}

// Set to Array
let backToArray = [...uniqueSet];
// or
let backToArray2 = Array.from(uniqueSet);
console.log(backToArray);  // [1, 2, 3, 4]
```

---

## 🗺️ Map Data Structure

### What is a Map?

A **Map** is a collection of **key-value pairs** where keys are unique and can be of any type.

**Key Features:**
- **Unique keys** - duplicate keys overwrite
- **Keys can be any type** - not just strings
- **Maintains insertion order**
- **Size property** - easily get count
- **Iterable** - can loop through entries

### Creating and Using Maps

```javascript
// Create empty map
let myMap = new Map();

// Create from array of [key, value] pairs
let students = new Map([
    ["Alice", 85],
    ["Bob", 92],
    ["Charlie", 78]
]);
```

### Map Methods

| Method | Description | Returns | Example |
|--------|-------------|---------|---------|
| `map.set(key, value)` | Adds/updates entry | The map itself | `map.set("name", "John")` |
| `map.get(key)` | Gets value for key | Value or undefined | `map.get("name")` |
| `map.has(key)` | Checks if key exists | true/false | `map.has("name")` |
| `map.delete(key)` | Removes entry | true/false | `map.delete("name")` |
| `map.size` | Number of entries | Number | `map.size` |
| `map.clear()` | Removes all entries | undefined | `map.clear()` |
| `map.keys()` | Iterator of keys | Iterator | `map.keys()` |
| `map.values()` | Iterator of values | Iterator | `map.values()` |
| `map.entries()` | Iterator of [k,v] | Iterator | `map.entries()` |

### Examples

```javascript
let studentGrades = new Map();

// Setting values
studentGrades.set("Alice", 85);
studentGrades.set("Bob", 92);
studentGrades.set("Charlie", 78);
studentGrades.set("Alice", 90);  // Updates Alice's grade

console.log(studentGrades.size);  // 3

// Getting values
console.log(studentGrades.get("Bob"));      // 92
console.log(studentGrades.get("David"));    // undefined

// Checking existence
console.log(studentGrades.has("Alice"));    // true
console.log(studentGrades.has("David"));    // false

// Deleting
studentGrades.delete("Charlie");
console.log(studentGrades.size);  // 2

// Iterating over keys
for (let name of studentGrades.keys()) {
    console.log(name);
}
// Alice
// Bob

// Iterating over values
for (let grade of studentGrades.values()) {
    console.log(grade);
}
// 90
// 92

// Iterating over entries
for (let [name, grade] of studentGrades) {
    console.log(`${name}: ${grade}`);
}
// Alice: 90
// Bob: 92
```

### Map vs Object

| Feature | Map | Object |
|---------|-----|--------|
| Key Types | Any type | String/Symbol only |
| Order | Insertion order maintained | Not guaranteed (mostly insertion) |
| Size | `map.size` property | `Object.keys(obj).length` |
| Iteration | Direct iteration | Need `Object.keys()` |
| Performance | Optimized for frequent add/remove | Better for simple storage |

---

## 💡 Common Problems and Solutions

### Problem 1: Remove Duplicates from Array

**Problem:** Given an array with duplicates, return array with unique elements.

**Solution using Set:**
```javascript
function removeDuplicates(arr) {
    return [...new Set(arr)];
}

// Test
let numbers = [1, 2, 2, 3, 4, 4, 5];
console.log(removeDuplicates(numbers));  // [1, 2, 3, 4, 5]
```

**Complexity:**
- Time: O(n)
- Space: O(n)

---

### Problem 2: Check if String is Pangram

**Problem:** A pangram contains all 26 English letters at least once. Check if a lowercase string is a pangram.

**Example:**
- Input: `"thequickbrownfoxjumpsoverthelazydog"`
- Output: `true`

**Solution using Set:**
```javascript
function isPangram(str) {
    let letters = new Set();
    
    for (let char of str) {
        if (char >= 'a' && char <= 'z') {
            letters.add(char);
        }
    }
    
    return letters.size === 26;
}

// Test
console.log(isPangram("thequickbrownfoxjumpsoverthelazydog"));  // true
console.log(isPangram("hello world"));  // false
```

**Complexity:**
- Time: O(n) where n is string length
- Space: O(1) - max 26 letters

---

### Problem 3: Frequency Counting

**Problem:** Count frequency of each element in an array.

**Example:**
- Input: `[1, 2, 2, 3, 3, 3, 4]`
- Output: `Map { 1 => 1, 2 => 2, 3 => 3, 4 => 1 }`

**Solution using Map:**
```javascript
function countFrequency(arr) {
    let freqMap = new Map();
    
    for (let num of arr) {
        if (freqMap.has(num)) {
            freqMap.set(num, freqMap.get(num) + 1);
        } else {
            freqMap.set(num, 1);
        }
    }
    
    return freqMap;
}

// Shorter version using ternary
function countFrequency_v2(arr) {
    let freqMap = new Map();
    
    for (let num of arr) {
        freqMap.set(num, (freqMap.get(num) || 0) + 1);
    }
    
    return freqMap;
}

// Test
let numbers = [1, 2, 2, 3, 3, 3, 4];
let freq = countFrequency(numbers);

for (let [num, count] of freq) {
    console.log(`${num} appears ${count} times`);
}
// 1 appears 1 times
// 2 appears 2 times
// 3 appears 3 times
// 4 appears 1 times
```

**Complexity:**
- Time: O(n)
- Space: O(k) where k is number of unique elements

---

### Problem 4: Sort People by Height

**LeetCode-style Problem:**

**Problem:** Given two arrays `names` and `heights` of equal length, return names sorted by heights in descending order.

**Example:**
- Input: `names = ["Mary","John","Emma"]`, `heights = [180,165,170]`
- Output: `["Mary","Emma","John"]`

**Solution:**
```javascript
function sortPeople(names, heights) {
    let map = new Map();
    
    // Map height to name
    for (let i = 0; i < names.length; i++) {
        map.set(heights[i], names[i]);
    }
    
    // Sort heights in descending order
    heights.sort((a, b) => b - a);
    
    // Map back to names
    let result = [];
    for (let height of heights) {
        result.push(map.get(height));
    }
    
    return result;
}

// Test
let names = ["Mary", "John", "Emma"];
let heights = [180, 165, 170];
console.log(sortPeople(names, heights));  // ["Mary", "Emma", "John"]
```

**Complexity:**
- Time: O(n log n) - due to sorting
- Space: O(n) - for map

---

### Problem 5: Two Sum (LeetCode #1)

**Problem:** Given an array of integers and a target, return indices of two numbers that add up to target.

**Constraints:**
- Exactly one solution exists
- Cannot use same element twice

**Example:**
- Input: `nums = [2, 7, 11, 15]`, `target = 9`
- Output: `[0, 1]` (nums[0] + nums[1] = 2 + 7 = 9)

**Brute Force O(n²):**
```javascript
function twoSum_bruteforce(nums, target) {
    for (let i = 0; i < nums.length; i++) {
        for (let j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] === target) {
                return [i, j];
            }
        }
    }
    return [];
}
```

**Optimized O(n) using Map:**
```javascript
function twoSum(nums, target) {
    let map = new Map();  // value → index
    
    for (let i = 0; i < nums.length; i++) {
        let complement = target - nums[i];
        
        if (map.has(complement)) {
            return [map.get(complement), i];
        }
        
        map.set(nums[i], i);
    }
    
    return [];
}

// Test
console.log(twoSum([2, 7, 11, 15], 9));     // [0, 1]
console.log(twoSum([3, 2, 4], 6));          // [1, 2]
console.log(twoSum([3, 3], 6));             // [0, 1]
```

**How it works:**
```
nums = [2, 7, 11, 15], target = 9

i=0: nums[0]=2, complement=7
     map doesn't have 7
     map.set(2, 0) → map = {2: 0}

i=1: nums[1]=7, complement=2
     map has 2! → return [0, 1] ✓
```

**Complexity:**
- Time: O(n) - single pass
- Space: O(n) - for map

---

### Problem 6: Intersection of Two Arrays

**Problem:** Given two arrays, return their intersection (common unique elements).

**Example:**
- Input: `nums1 = [1,2,2,1]`, `nums2 = [2,2]`
- Output: `[2]`

**Solution using Set:**
```javascript
function intersection(nums1, nums2) {
    let set1 = new Set(nums1);
    let result = new Set();
    
    for (let num of nums2) {
        if (set1.has(num)) {
            result.add(num);
        }
    }
    
    return [...result];
}

// Alternative: One-liner
function intersection_v2(nums1, nums2) {
    let set1 = new Set(nums1);
    return [...new Set(nums2.filter(num => set1.has(num)))];
}

// Test
console.log(intersection([1,2,2,1], [2,2]));         // [2]
console.log(intersection([4,9,5], [9,4,9,8,4]));     // [9, 4] or [4, 9]
```

**Complexity:**
- Time: O(n + m) where n, m are array lengths
- Space: O(n) for set

---

### Problem 7: Subarray Sum Equals K (LeetCode #560)

**Problem:** Given an array and integer k, return count of continuous subarrays whose sum equals k.

**Example:**
- Input: `nums = [1, 1, 1]`, `k = 2`
- Output: `2` (subarrays [1,1] appear twice)

**Brute Force O(n²):**
```javascript
function subarraySum_bruteforce(nums, k) {
    let count = 0;
    
    for (let i = 0; i < nums.length; i++) {
        let sum = 0;
        for (let j = i; j < nums.length; j++) {
            sum += nums[j];
            if (sum === k) count++;
        }
    }
    
    return count;
}
```

**Optimized O(n) using Prefix Sum + Map:**

**Key Insight:**
- If `prefixSum[j] - prefixSum[i] = k`
- Then `prefixSum[i] = prefixSum[j] - k`
- Store prefix sums in map with their frequencies

```javascript
function subarraySum(nums, k) {
    let map = new Map([[0, 1]]);  // prefixSum → frequency
    let sum = 0;
    let count = 0;
    
    for (let num of nums) {
        sum += num;
        
        // Check if (sum - k) exists
        if (map.has(sum - k)) {
            count += map.get(sum - k);
        }
        
        // Update map with current sum
        map.set(sum, (map.get(sum) || 0) + 1);
    }
    
    return count;
}

// Test
console.log(subarraySum([1, 1, 1], 2));        // 2
console.log(subarraySum([1, 2, 3], 3));        // 2
```

**Detailed Walkthrough (nums=[1,2,3], k=3):**
```
Initialize: map = {0: 1}, sum = 0, count = 0

i=0, num=1:
  sum = 0 + 1 = 1
  sum - k = 1 - 3 = -2 (not in map)
  map.set(1, 1) → map = {0: 1, 1: 1}

i=1, num=2:
  sum = 1 + 2 = 3
  sum - k = 3 - 3 = 0 (in map! frequency = 1)
  count += 1 → count = 1
  map.set(3, 1) → map = {0: 1, 1: 1, 3: 1}

i=2, num=3:
  sum = 3 + 3 = 6
  sum - k = 6 - 3 = 3 (in map! frequency = 1)
  count += 1 → count = 2
  map.set(6, 1) → map = {0: 1, 1: 1, 3: 1, 6: 1}

Return count = 2 ✓
Subarrays: [1,2] and [3]
```

**Complexity:**
- Time: O(n)
- Space: O(n)

---

### Problem 8: Longest Consecutive Sequence (LeetCode #128)

**Problem:** Given unsorted array, find length of longest consecutive sequence. Must be O(n).

**Example:**
- Input: `[100, 4, 200, 1, 3, 2]`
- Output: `4` (sequence [1, 2, 3, 4])

**Brute Force (Sort first):**
```javascript
function longestConsecutive_sort(nums) {
    if (nums.length === 0) return 0;
    
    nums.sort((a, b) => a - b);
    let maxLen = 1;
    let currentLen = 1;
    
    for (let i = 1; i < nums.length; i++) {
        if (nums[i] === nums[i-1]) continue;  // Skip duplicates
        if (nums[i] === nums[i-1] + 1) {
            currentLen++;
        } else {
            maxLen = Math.max(maxLen, currentLen);
            currentLen = 1;
        }
    }
    
    return Math.max(maxLen, currentLen);
}
// Time: O(n log n) - sorting
```

**Optimized O(n) using Set:**

**Key Insight:**
- Only start counting from beginning of sequence
- Element is start if `element - 1` not in set

```javascript
function longestConsecutive(nums) {
    let set = new Set(nums);
    let maxLen = 0;
    
    for (let num of set) {
        // Check if this is start of sequence
        if (!set.has(num - 1)) {
            let currentNum = num;
            let currentLen = 1;
            
            // Count consecutive numbers
            while (set.has(currentNum + 1)) {
                currentNum++;
                currentLen++;
            }
            
            maxLen = Math.max(maxLen, currentLen);
        }
    }
    
    return maxLen;
}

// Test
console.log(longestConsecutive([100, 4, 200, 1, 3, 2]));  // 4
console.log(longestConsecutive([0,3,7,2,5,8,4,6,0,1]));   // 9
```

**Detailed Walkthrough ([100, 4, 200, 1, 3, 2]):**
```
set = {100, 4, 200, 1, 3, 2}

Check 100:
  99 not in set → start of sequence
  101 not in set → length = 1

Check 4:
  3 in set → NOT start, skip

Check 200:
  199 not in set → start of sequence
  201 not in set → length = 1

Check 1:
  0 not in set → start of sequence ✓
  2 in set → continue (length = 2)
  3 in set → continue (length = 3)
  4 in set → continue (length = 4)
  5 not in set → stop
  maxLen = 4

Check 3:
  2 in set → NOT start, skip

Check 2:
  1 in set → NOT start, skip

Return maxLen = 4
Sequence: [1, 2, 3, 4]
```

**Why O(n)?**
- Even though nested loops, each element visited at most twice
- Inner while loop only runs for sequence starts
- Total operations = O(n)

**Complexity:**
- Time: O(n)
- Space: O(n)

---

## 📊 Problem Summary Table

| Problem | Data Structure | Time | Space | Key Technique |
|---------|---------------|------|-------|---------------|
| Remove Duplicates | Set | O(n) | O(n) | Set automatically handles uniqueness |
| Pangram Check | Set | O(n) | O(1) | Count unique letters |
| Frequency Counting | Map | O(n) | O(k) | Map value → count |
| Sort People | Map | O(n log n) | O(n) | Map height → name, sort |
| Two Sum | Map | O(n) | O(n) | Map value → index, check complement |
| Array Intersection | Set | O(n+m) | O(n) | Set for O(1) lookup |
| Subarray Sum = K | Map | O(n) | O(n) | Prefix sum + frequency map |
| Longest Consecutive | Set | O(n) | O(n) | Check sequence start, count forward |

---

## 🎯 When to Use Which?

### Use Set When:
- ✅ Need to store **unique values only**
- ✅ Need **fast membership testing** (has operation)
- ✅ Need to **remove duplicates** from array
- ✅ Order doesn't matter or insertion order is fine
- ✅ No key-value relationship needed

**Examples:** Unique elements, intersection, pangram check

### Use Map When:
- ✅ Need **key-value associations**
- ✅ Need to **count frequencies**
- ✅ Keys can be **any data type** (not just strings)
- ✅ Need to **maintain insertion order**
- ✅ Frequent additions and deletions
- ✅ Need to **track indices** or positions

**Examples:** Frequency counting, Two Sum, caching, memoization

### Use Object When:
- ✅ Simple **static configuration**
- ✅ Keys are always **strings**
- ✅ JSON compatibility needed
- ✅ No frequent additions/deletions
- ✅ Simple data structure

**Examples:** Config objects, JSON data, simple caches

---

## 💡 Important Concepts

### 1. Hash Code Generation

```javascript
// Simplified concept (not actual implementation)
function hashCode(key) {
    // Convert key to number
    // Apply mathematical operations
    // Return index in range [0, tableSize)
    return someNumber % tableSize;
}
```

### 2. Collision Handling

When two keys produce same hash code:
- **Chaining:** Store multiple values at same index (linked list)
- **Open Addressing:** Find next available slot

JavaScript handles this internally!

### 3. Load Factor

**Load Factor = Number of Elements / Table Size**

- High load factor → More collisions → Slower operations
- JavaScript automatically resizes hash tables to maintain performance

---

## 🚀 Practice Strategy

### Beginner Level
1. Convert array to set to remove duplicates
2. Count frequency of elements using map
3. Check if element exists in array using set
4. Store key-value pairs with map

### Intermediate Level
5. Two Sum problem
6. Intersection of arrays
7. First unique character in string
8. Group anagrams

### Advanced Level
9. Subarray sum equals K
10. Longest consecutive sequence
11. LRU Cache (using map)
12. Design HashMap from scratch

---

## 📝 Quick Reference

### Set Cheat Sheet
```javascript
let set = new Set([1, 2, 3]);

set.add(4);           // Add element
set.delete(2);        // Remove element
set.has(3);           // Check existence → true
set.size;             // Get count → 3
set.clear();          // Remove all

for (let val of set) {
    console.log(val);
}
```

### Map Cheat Sheet
```javascript
let map = new Map();

map.set("key", "value");     // Add/update
map.get("key");              // Get value
map.has("key");              // Check key → true
map.delete("key");           // Remove entry
map.size;                    // Get count
map.clear();                 // Remove all

map.keys();                  // Iterator of keys
map.values();                // Iterator of values
map.entries();               // Iterator of [k,v]

for (let [key, value] of map) {
    console.log(key, value);
}
```

---

## 🎯 Key Takeaways

1. **Hashing enables O(1) operations** - Fundamental for efficient algorithms

2. **Set = Unique values** - Use for membership and uniqueness

3. **Map = Key-value pairs** - Use for associations and counting

4. **Trade time for space** - Hash structures use O(n) space for O(1) time

5. **Prefix sum + Map** - Powerful pattern for subarray problems

6. **Set for sequence problems** - Efficient for consecutive checks

7. **Map for Two Sum variants** - Store complements for quick lookup

8. **Choose the right structure** - Set vs Map vs Object based on needs

---

**Video Source:** Sherian Schooling School - Ali Ansari  
**Topic:** Hashing, Sets, and Maps in JavaScript  
**Hashtag:** #beautyclear

**Remember:** Practice these problems multiple times to build intuition and muscle memory!