# JavaScript Strings
## Comprehensive Study Notes - DSA Series Part 5

---

## Table of Contents

1. [Introduction to Strings](#1-introduction-to-strings)
2. [String Properties and Characteristics](#2-string-properties-and-characteristics)
3. [String Methods](#3-string-methods)
4. [Practical String Problems](#4-practical-string-problems)
5. [Character Frequency Analysis](#5-character-frequency-analysis)
6. [ASCII Values and Character Codes](#6-ascii-values-and-character-codes)
7. [Key Takeaways](#7-key-takeaways)

---

## 1. Introduction to Strings

### What is a String?

A **string** is a collection, combination, or group of characters enclosed in quotes.

**Important:** Characters become a string ONLY when enclosed in quotes (single or double).

### String Declaration

```javascript
// ❌ WRONG - Without quotes
let name = Ali;  // ReferenceError: Ali is not defined

// ✅ CORRECT - With quotes
let name = "Ali";  // Valid string
let name = 'Ali';  // Also valid in JavaScript
```

### Key Points

- **In JavaScript:** Both single quotes (`'`) and double quotes (`"`) work
- **In Java/C++:** Only double quotes (`"`) are mandatory for strings
- Without quotes, JavaScript thinks it's a variable or keyword

### Examples

```javascript
let name = "Sheriyas";     // String
let address = "Kolkata";   // String
let description = "Learning DSA with JavaScript";  // String

console.log(name);  // Displays in black color in console (indicates string)
```

---

## 2. String Properties and Characteristics

### Strings Behave Like Arrays (But Are NOT Arrays)

**Critical Distinction:**
- Strings **behave like** arrays of characters
- Strings are **NOT** arrays of characters
- Strings are a **sequence of characters**

### Index-Based Access

Just like arrays, strings support index-based access:

```javascript
let s = "Sheriyas";

console.log(s[0]);  // "S"
console.log(s[1]);  // "h"
console.log(s[2]);  // "e"
console.log(s[3]);  // "r"
```

**Index Mapping:**

| Character | S | h | e | r | i | y | a | s |
|-----------|---|---|---|---|---|---|---|---|
| Index     | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

### Why Strings Are NOT Arrays

Arrays have methods like `push()` and `pop()`, but strings don't:

```javascript
let arr = [10, 20, 30];
arr.push(40);  // Works fine - [10, 20, 30, 40]

let s = "Sheriyas";
s.push("y");  // ❌ ERROR: s.push is not a function
```

**Proof:** Strings don't have array methods, confirming they are NOT arrays.

### Immutability of Strings

**Strings are IMMUTABLE** - you cannot change the original string directly.

```javascript
let arr = [10, 20, 30, 40];
arr[2] = 100;
console.log(arr);  // [10, 20, 100, 40] - Changed!

let s = "Sheriyas";
s[2] = "y";
console.log(s);  // "Sheriyas" - NOT changed!
```

**Why?**
- Arrays are **mutable** - can change original state
- Strings are **immutable** - cannot change original state

### Reassignment Creates New String

```javascript
let s = "Sheriyas";
s = s + " World";
console.log(s);  // "Sheriyas World"
```

**What happened:**
- We didn't modify the original string
- We created a **NEW string** by concatenation
- Then **reassigned** it to the variable `s`

---

## 3. String Methods

### Overview of String Methods

Strings have built-in methods for manipulation and analysis:

- `length` - Get string length
- `slice()` - Extract substring
- `substring()` - Extract substring (no negative indices)
- `substr()` - Extract substring (deprecated)
- `toUpperCase()` - Convert to uppercase
- `toLowerCase()` - Convert to lowercase
- `concat()` - Join strings
- `trim()` - Remove whitespace
- `charAt()` - Get character at index
- `charCodeAt()` - Get ASCII code at index
- `indexOf()` - Find first occurrence
- `lastIndexOf()` - Find last occurrence
- `includes()` - Check if substring exists
- `startsWith()` - Check if starts with substring
- `endsWith()` - Check if ends with substring
- `replace()` - Replace first occurrence
- `replaceAll()` - Replace all occurrences
- `split()` - Split string into array

---

### 3.1 length Property

**Note:** `length` is a **property**, NOT a method (no parentheses needed).

```javascript
let s = "Sheriyas";
console.log(s.length);  // 8

// ❌ WRONG
console.log(s.length());  // ERROR: length is not a function
```

---

### 3.2 slice() Method

**Purpose:** Extract a substring from a string.

**Syntax:** `string.slice(startIndex, endIndex)`

**Parameters:**
- `startIndex` - Starting position (inclusive)
- `endIndex` - Ending position (exclusive)

```javascript
let s = "Sheriyas";

// Extract "herry"
console.log(s.slice(1, 5));  // "herr"
// Note: Extracts from index 1 up to (but not including) index 5

// Extract "harry"
console.log(s.slice(1, 6));  // "herri"
```

**Important:** End index is **exclusive** - characters are extracted UP TO but NOT including the end index.

### Negative Indices with slice()

`slice()` supports negative indices to extract from the end:

```javascript
let s = "Sheriyas";

// Negative indexing
// -8  -7  -6  -5  -4  -3  -2  -1
//  S   h   e   r   i   y   a   s

// Extract "iyas" (from -4 to end)
console.log(s.slice(-4));  // "iyas"

// Extract from -4 to -1 (exclusive)
console.log(s.slice(-4, -1));  // "iya"

// Extract from -4 to end (using length)
console.log(s.slice(-4, s.length));  // "iyas"
```

---

### 3.3 substring() Method

**Purpose:** Similar to `slice()` but does NOT support negative indices.

**Syntax:** `string.substring(startIndex, endIndex)`

```javascript
let s = "Sheriyas";

// Extract substring from index 2 to 5 (exclusive)
console.log(s.substring(2, 6));  // "eriy"

// From index 2 to end
console.log(s.substring(2));  // "eriyas"
```

**Key Difference from slice():**
- `slice()` - Supports negative indices (from end)
- `substring()` - Only supports positive indices (from start)

---

### 3.4 toUpperCase() and toLowerCase()

```javascript
let s = "Sheriyas";

console.log(s.toUpperCase());  // "SHERIYAS"
console.log(s.toLowerCase());  // "sheriyas"
```

**Self-explanatory:** Converts entire string to uppercase or lowercase.

---

### 3.5 concat() Method

**Purpose:** Concatenate (join) strings together.

```javascript
let s = "Sheriyas";

// Concatenate with one string
console.log(s.concat(" World"));  // "Sheriyas World"

// Concatenate with multiple strings
console.log(s.concat(" ", "World", " ", "Hello"));  // "Sheriyas World Hello"

// Using underscores
console.log(s.concat("_", "World", "_", "Hello"));  // "Sheriyas_World_Hello"
```

---

### 3.6 trim() Method

**Purpose:** Remove leading and trailing whitespace (spaces).

```javascript
let s = "    Sheriyas    ";

console.log(s.trim());  // "Sheriyas"
```

**Use Case:** Clean up user input by removing unnecessary spaces at the beginning and end.

---

### 3.7 charAt() Method

**Purpose:** Get character at a specific index.

```javascript
let s = "Sheriyas";

console.log(s.charAt(2));  // "e"
console.log(s.charAt(3));  // "r"

// Alternative (bracket notation)
console.log(s[2]);  // "e"
console.log(s[3]);  // "r"
```

**Both methods work the same way.**

---

### 3.8 charCodeAt() Method

**Purpose:** Get the **ASCII code** of a character at a specific index.

```javascript
let s = "Sheriyas";

console.log(s.charCodeAt(3));  // 114 (ASCII code of 'r')
```

### Understanding ASCII Codes

**ASCII (American Standard Code for Information Interchange)** assigns numeric codes to characters.

**Common ASCII Values:**

| Character | ASCII Code |
|-----------|------------|
| 'A' (capital A) | 65 |
| 'B' (capital B) | 66 |
| 'C' (capital C) | 67 |
| ... | ... |
| 'Z' (capital Z) | 90 |
| 'a' (small a) | 97 |
| 'b' (small b) | 98 |
| 'c' (small c) | 99 |
| ... | ... |
| 'z' (small z) | 122 |
| '0' (digit 0 as char) | 48 |
| '1' (digit 1 as char) | 49 |
| ... | ... |
| '9' (digit 9 as char) | 57 |

**Important Differences:**
- `0` (number) ≠ `"0"` (character)
- Number 0 is a numeric value
- Character "0" has ASCII code 48

---

### Additional String Methods Summary

```javascript
let s = "Sheriyas";

// indexOf() - Find first occurrence
console.log(s.indexOf("i"));  // 4

// lastIndexOf() - Find last occurrence
console.log(s.lastIndexOf("s"));  // 7

// includes() - Check if substring exists
console.log(s.includes("riya"));  // true

// startsWith() - Check prefix
console.log(s.startsWith("She"));  // true

// endsWith() - Check suffix
console.log(s.endsWith("yas"));  // true

// replace() - Replace first occurrence
console.log(s.replace("i", "I"));  // "SherIyas"

// replaceAll() - Replace all occurrences
console.log(s.replaceAll("s", "S"));  // "SheriyaS"

// split() - Split into array
console.log(s.split(""));  // ['S','h','e','r','i','y','a','s']
```

**Homework:** Implement and test all these methods yourself!

---

## 4. Practical String Problems

### Problem 1: Print Each Character on a New Line

**Problem:** Given a string, print each character on a separate line.

**Approach:** Since strings behave like arrays, we can iterate through them.

```javascript
let s = "Sheriyas";

// Method 1: Using bracket notation
for (let i = 0; i < s.length; i++) {
  console.log(s[i]);
}

// Method 2: Using charAt()
for (let i = 0; i < s.length; i++) {
  console.log(s.charAt(i));
}
```

**Output:**
```
S
h
e
r
i
y
a
s
```

### Reverse Order Printing

```javascript
let s = "Sheriyas";

// Print characters in reverse order
for (let i = s.length - 1; i >= 0; i--) {
  console.log(s.charAt(i));
}
```

**Output:**
```
s
a
y
i
r
e
h
S
```

---

### Problem 2: Reverse a String

**Problem:** Print the entire string in reversed order (not character by character).

**Example:**
- Input: "Sheriyas"
- Output: "sayirehS"

#### Approach 1: Using Concatenation (Not Optimal)

```javascript
let s = prompt("Enter a string:");
let reverse = "";

for (let i = s.length - 1; i >= 0; i--) {
  reverse = reverse + s.charAt(i);
}

console.log(reverse);
```

**How it works:**

| Iteration | i | Current char | reverse before | reverse after |
|-----------|---|--------------|----------------|---------------|
| 1 | 7 | 's' | "" | "s" |
| 2 | 6 | 'a' | "s" | "sa" |
| 3 | 5 | 'y' | "sa" | "say" |
| 4 | 4 | 'i' | "say" | "sayi" |
| 5 | 3 | 'r' | "sayi" | "sayir" |
| 6 | 2 | 'e' | "sayir" | "sayire" |
| 7 | 1 | 'h' | "sayire" | "sayireh" |
| 8 | 0 | 'S' | "sayireh" | "sayirehS" |

**Problem with this approach:**
- Creates a new string with each concatenation
- If string length is 10, we create 10 new strings in memory
- **High memory cost** - inefficient!

---

### Problem 3: Check if String is Palindrome

**Definition:** A palindrome reads the same forwards and backwards.

**Examples:**
- "madam" - Palindrome ✓
- "malayalam" - Palindrome ✓
- "naman" - Palindrome ✓
- "abba" - Palindrome ✓
- "start" - NOT palindrome ✗

#### Approach 1: Reverse and Compare (Not Optimal)

```javascript
let s = prompt("Enter a string:");
let reverse = "";

// Reverse the string
for (let i = s.length - 1; i >= 0; i--) {
  reverse = reverse + s.charAt(i);
}

// Compare
if (reverse === s) {
  console.log("Palindrome");
} else {
  console.log("No palindrome");
}
```

**Problem:** Same memory issue as above - creates multiple new strings.

#### Approach 2: Two Pointer Algorithm (Optimal)

**Key Insight:** Use two pointers - one at start, one at end. Compare characters moving towards center.

```javascript
let s = prompt("Enter a string:");
let isPalindrome = true;
let i = 0;
let j = s.length - 1;

while (i < j) {
  if (s.charAt(i) !== s.charAt(j)) {
    isPalindrome = false;
    break;  // Exit early
  }
  i++;
  j--;
}

if (isPalindrome) {
  console.log("Palindrome");
} else {
  console.log("No palindrome");
}
```

**How it works:**

Example: "madam"

```
Step 1:
i=0, j=4
m === m? Yes
Move: i++, j--

Step 2:
i=1, j=3
a === a? Yes
Move: i++, j--

Step 3:
i=2, j=2
i is no longer < j
Stop - it's a palindrome!
```

Example: "start"

```
Step 1:
i=0, j=4
s === t? No
isPalindrome = false
Break - not a palindrome!
```

**Visual Representation:**

```
     s  t  a  r  t
     ↑           ↑
     i           j
     
Compare s and t → Not equal
Result: Not palindrome
```

**Advantages:**
- ✅ No extra memory for reversed string
- ✅ Exits early when mismatch found
- ✅ Time efficient: O(n/2) comparisons
- ✅ Space efficient: O(1) extra space

---

### Problem 4: Toggle Case of Each Character

**Problem:** Convert uppercase letters to lowercase and lowercase to uppercase.

**Example:**
- Input: "AaBbCc"
- Output: "aAbBcC"

**Approach:**
1. Check if character is uppercase or lowercase
2. If uppercase → convert to lowercase
3. If lowercase → convert to uppercase

### Understanding Case Conversion

**Key Facts:**
- Capital 'A' ASCII = 65
- Small 'a' ASCII = 97
- **Difference = 32**

This means:
- To convert uppercase to lowercase: ASCII + 32
- To convert lowercase to uppercase: ASCII - 32

### Checking Character Case

```javascript
// Check if uppercase
if (asciiCode >= 65 && asciiCode <= 90) {
  // It's uppercase (A-Z)
}

// Check if lowercase
if (asciiCode >= 97 && asciiCode <= 122) {
  // It's lowercase (a-z)
}
```

### Complete Solution

```javascript
let s = prompt("Enter a string:");
let toggled = "";

for (let i = 0; i < s.length; i++) {
  let ch = s.charAt(i);
  let ascii = s.charCodeAt(i);
  
  if (ascii >= 65 && ascii <= 90) {
    // Uppercase - convert to lowercase
    toggled += String.fromCharCode(ascii + 32);
  } else if (ascii >= 97 && ascii <= 122) {
    // Lowercase - convert to uppercase
    toggled += String.fromCharCode(ascii - 32);
  } else {
    // Not a letter - keep as is
    toggled += ch;
  }
}

console.log(toggled);
```

### Step-by-Step Example

Input: "AbC"

| Character | ASCII | Check | Action | New ASCII | New Char |
|-----------|-------|-------|--------|-----------|----------|
| 'A' | 65 | Uppercase | +32 | 97 | 'a' |
| 'b' | 98 | Lowercase | -32 | 66 | 'B' |
| 'C' | 67 | Uppercase | +32 | 99 | 'c' |

Output: "aBc"

### Converting Between ASCII and Character

```javascript
// Character to ASCII
let ascii = s.charCodeAt(i);  // Gets ASCII code

// ASCII to Character
let char = String.fromCharCode(ascii);  // Converts ASCII to character
```

---

## 5. Character Frequency Analysis

### Problem: Count Frequency of Each Character

**Problem:** Given a string, count how many times each character appears.

**Example:**
- Input: "hello"
- Output:
  ```
  h: 1
  e: 1
  l: 2
  o: 1
  ```

### Approach: Bitmap/Frequency Array

**Key Concept:** Use an array where:
- **Index** = ASCII value of character
- **Value** = Frequency (count) of that character

### Why Array Size 128?

Standard ASCII has 128 characters (0-127):
- Uppercase letters: A-Z (65-90)
- Lowercase letters: a-z (97-122)
- Digits: 0-9 (48-57)
- Special characters

### Algorithm Steps

1. Create an array of size 128, initialized with 0
2. For each character in string:
   - Get ASCII value
   - Use ASCII value as index
   - Increment count at that index
3. Traverse array and print characters with count > 0

### Implementation

```javascript
let s = prompt("Enter a string:");
let arr = new Array(128).fill(0);  // Initialize with zeros

// Count frequencies
for (let i = 0; i < s.length; i++) {
  let ascii = s.charCodeAt(i);
  arr[ascii] = arr[ascii] + 1;  // or arr[ascii]++
}

// Print frequencies
for (let i = 0; i < arr.length; i++) {
  if (arr[i] > 0) {
    console.log(String.fromCharCode(i) + " appears " + arr[i] + " times");
  }
}
```

### Detailed Example

Input: "abacdb"

**Step 1: Initialize array**
```
Index:  0   1   2   ...  97  98  99  100  ...  127
Value:  0   0   0   ...   0   0   0    0  ...    0
```

**Step 2: Process each character**

| Character | ASCII | Action | Array at index |
|-----------|-------|--------|----------------|
| 'a' | 97 | arr[97]++ | arr[97] = 1 |
| 'b' | 98 | arr[98]++ | arr[98] = 1 |
| 'a' | 97 | arr[97]++ | arr[97] = 2 |
| 'c' | 99 | arr[99]++ | arr[99] = 1 |
| 'd' | 100 | arr[100]++ | arr[100] = 1 |
| 'b' | 98 | arr[98]++ | arr[98] = 2 |

**Step 3: Final array state**
```
Index:  ...  97  98  99  100  ...
Value:  ...   2   2   1    1  ...
```

**Step 4: Convert back and print**
```
a appears 2 times  (index 97 → 'a')
b appears 2 times  (index 98 → 'b')
c appears 1 times  (index 99 → 'c')
d appears 1 times  (index 100 → 'd')
```

### Visual Representation

```
String: "abacdb"

ASCII Array Mapping:
┌─────┬─────┬─────┬─────┬─────┐
│  97 │  98 │  99 │ 100 │ ... │  (Indices = ASCII values)
├─────┼─────┼─────┼─────┼─────┤
│  2  │  2  │  1  │  1  │  0  │  (Values = Frequencies)
└─────┴─────┴─────┴─────┴─────┘
   ↓     ↓     ↓     ↓
   a     b     c     d
```

### How Index Maps to Character

```javascript
// Character → ASCII (Index)
let ascii = s.charCodeAt(i);  // 'a' → 97
arr[ascii]++;                  // arr[97]++

// ASCII (Index) → Character
for (let i = 0; i < arr.length; i++) {
  if (arr[i] > 0) {
    let char = String.fromCharCode(i);  // 97 → 'a'
    console.log(char + ": " + arr[i]);
  }
}
```

### Homework Challenge

**Problem:** The current solution prints characters in ASCII order (sorted), not in the order they appeared in the input.

**Example:**
- Input: "hello"
- Current Output: e:1, h:1, l:2, o:1 (sorted)
- Expected: h:1, e:1, l:2, o:1 (order of appearance)

**Your Task:** Modify the code to print frequencies in the order characters first appeared.

**Hint:** You may need to track the order of first occurrence separately.

---

## 6. ASCII Values and Character Codes

### What are ASCII Codes?

**ASCII** (American Standard Code for Information Interchange) is a character encoding standard that assigns numeric codes to characters.

### Why Do We Need Character Encoding?

Computers only understand numbers (binary). To represent text, we need a standard way to map:
- Characters → Numbers (encoding)
- Numbers → Characters (decoding)

### Common ASCII Ranges

| Range | Characters | Starting Code |
|-------|------------|---------------|
| 48-57 | Digits (0-9) | '0' = 48 |
| 65-90 | Uppercase (A-Z) | 'A' = 65 |
| 97-122 | Lowercase (a-z) | 'a' = 97 |

### Key ASCII Values to Remember

```
Capital Letters:
A = 65, B = 66, C = 67, ..., Z = 90

Small Letters:
a = 97, b = 98, c = 99, ..., z = 122

Digits (as characters):
'0' = 48, '1' = 49, '2' = 50, ..., '9' = 57

Special:
Space = 32
```

### Difference Between Number and Character

```javascript
// Number
let num = 0;  // This is numeric zero
console.log(typeof num);  // "number"

// Character
let char = "0";  // This is character zero
console.log(typeof char);  // "string"
console.log(char.charCodeAt(0));  // 48 (ASCII code)
```

### Unicode vs ASCII

**ASCII:**
- 128 characters (0-127)
- Covers English and basic symbols
- Limited to Latin alphabet

**Unicode:**
- Over 1 million characters
- Covers all languages (Chinese, Arabic, Hindi, etc.)
- Includes emojis, mathematical symbols
- Backward compatible with ASCII

**JavaScript uses Unicode**, but ASCII is a subset of it.

### Homework: Research Task

**Research and explain in comments:**
1. What are Unicode characters?
2. Why do we need Unicode?
3. Why do we need ASCII values?
4. How does character encoding work?
5. What's the difference between ASCII and Unicode?

**Share your findings in the comments!**

---

## 7. Key Takeaways

### String Fundamentals

1. **Strings are NOT arrays** - They behave like arrays but don't have array methods
2. **Strings are immutable** - Original string cannot be changed
3. **Reassignment creates new string** - Concatenation creates a new string object
4. **Index-based access** - Can access characters using bracket notation or charAt()

### Important Concepts

| Concept | Description |
|---------|-------------|
| **Indexing** | Strings use 0-based indexing like arrays |
| **Length** | Use `.length` property (not a method) |
| **Immutability** | Cannot modify original string directly |
| **ASCII Codes** | Each character has a numeric code |
| **Case Conversion** | Uppercase ↔ Lowercase differs by 32 |

### Method Categories

**Extraction Methods:**
- `slice()` - Supports negative indices
- `substring()` - Only positive indices
- `charAt()` / `[]` - Single character access

**Transformation Methods:**
- `toUpperCase()` / `toLowerCase()` - Case conversion
- `trim()` - Remove whitespace
- `concat()` - Join strings
- `replace()` / `replaceAll()` - Substitution

**Analysis Methods:**
- `indexOf()` / `lastIndexOf()` - Find position
- `includes()` / `startsWith()` / `endsWith()` - Check content
- `charCodeAt()` - Get ASCII code

### Problem-Solving Patterns

**Pattern 1: Character Iteration**
```javascript
for (let i = 0; i < s.length; i++) {
  // Process s[i] or s.charAt(i)
}
```

**Pattern 2: Two Pointer**
```javascript
let i = 0, j = s.length - 1;
while (i < j) {
  // Compare s[i] and s[j]
  i++;
  j--;
}
```

**Pattern 3: Frequency Counting**
```javascript
let freq = new Array(128).fill(0);
for (let i = 0; i < s.length; i++) {
  freq[s.charCodeAt(i)]++;
}
```

**Pattern 4: ASCII Manipulation**
```javascript
let ascii = s.charCodeAt(i);
if (ascii >= 65 && ascii <= 90) {
  // Uppercase: convert to lowercase
  ascii += 32;
} else if (ascii >= 97 && ascii <= 122) {
  // Lowercase: convert to uppercase
  ascii -= 32;
}
let newChar = String.fromCharCode(ascii);
```

### Common Mistakes to Avoid

❌ **Using .length() with parentheses**
```javascript
s.length()  // ERROR: length is a property, not a method
```

❌ **Trying to modify string directly**
```javascript
s[0] = 'X';  // Won't work - strings are immutable
```

❌ **Using array methods on strings**
```javascript
s.push('a');  // ERROR: push is not available on strings
```

❌ **Forgetting string methods return new strings**
```javascript
s.toUpperCase();  // Doesn't change s
s = s.toUpperCase();  // Correct - reassign
```

### Optimization Tips

1. **Use charAt() over bracket notation** for better browser compatibility
2. **Break early** in search loops when found
3. **Use frequency array** for character counting instead of multiple searches
4. **Two-pointer technique** for palindrome checks saves memory
5. **Cache length** if using in loop condition

### ASCII Reference Quick Guide

```
Uppercase Range: 65-90  (A-Z)
Lowercase Range: 97-122 (a-z)
Digit Range:     48-57  (0-9)
Space:           32
Difference:      32     (between upper and lower case)
```

### Practice Exercises

1. **Reverse a string** without using extra space
2. **Check palindrome** with two-pointer approach
3. **Count vowels and consonants** in a string
4. **Remove duplicates** from a string
5. **Find first non-repeating character**
6. **Check if two strings are anagrams**
7. **Toggle case** of all characters
8. **Count frequency** and print in order of appearance
9. **Find longest word** in a sentence
10. **Check if string is a rotation** of another string

### Study Tips

1. **Practice with pen and paper** - Trace through algorithms manually
2. **Understand ASCII values** - Memorize key ranges
3. **Master string methods** - Know when to use which method
4. **Think before coding** - Plan your approach first
5. **Test edge cases** - Empty strings, single character, special characters

### Five-Step Learning Process

1. **Understand the problem** - Read carefully, identify requirements
2. **Try to solve** - Attempt coding yourself
3. **Write on paper** - Dry run with sample inputs
4. **Code the solution** - Implement in IDE
5. **Dry run your code** - Trace execution step-by-step

**Only after these 5 steps will concepts truly stick in your mind!**

---

## Resources for Further Learning

- Research ASCII and Unicode character encoding
- Practice string manipulation on coding platforms
- Study regex patterns for advanced string matching
- Learn about string interning and memory optimization
- Explore UTF-8, UTF-16, and other encodings

---

## Final Note

**Remember:** 
- String problems are fundamental in coding interviews
- Understanding ASCII is crucial for many algorithms
- Immutability concept is important across programming languages
- Practice is key - implement every method and problem yourself!

**If you found this helpful:**
- Share your learnings in comments
- Complete the homework assignments
- Practice all the problems with different test cases
- Ask questions if anything is unclear

**Happy Coding! 🚀**

---

**End of Study Notes**