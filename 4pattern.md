# JavaScript Loops
## Comprehensive Study Notes - DSA Series Part 4

---

## Table of Contents

1. [Introduction to Loops](#1-introduction-to-loops)
2. [For Loops](#2-for-loops)
3. [Variable Scope: var vs let](#3-variable-scope-var-vs-let)
4. [Practical Problems with Loops](#4-practical-problems-with-loops)
5. [While Loops](#5-while-loops)
6. [Do-While Loops](#6-do-while-loops)
7. [Loop Control Statements](#7-loop-control-statements)
8. [Optimization Techniques](#8-optimization-techniques)
9. [Practical Applications](#9-practical-applications)
10. [Key Takeaways](#10-key-takeaways)

---

## 1. Introduction to Loops

### What are Loops?

Loops are programming constructs that allow you to execute a block of code repeatedly without writing the same code multiple times.

### Why Use Loops?

**❌ Without Loops:**

```javascript
console.log("Hello");
console.log("Hello");
console.log("Hello");
console.log("Hello");
console.log("Hello");
// ... repeat 6000 times
```

**Problems with this approach:**

- **Increased file size** - More code = larger files
- **Slower loading time** - Takes longer to load and parse
- **Poor maintainability** - Hard to update or modify
- **Deteriorated user experience** - Slow websites lose customers
- **Negative business impact** - Poor performance affects brand reputation

**✅ With Loops:**

```javascript
for (let i = 1; i <= 6000; i++) {
  console.log("Hello");
}
```

**Benefits:**

- **3 lines instead of 6000** - Dramatically reduced code
- **Smaller file size** - Faster downloads
- **Better performance** - Quicker execution
- **Easy maintenance** - Change once, affects all iterations
- **Professional code** - Industry standard practice

---

## 2. For Loops

### What is a For Loop?

A for loop executes a block of code a specific number of times. It's best used when you know exactly how many iterations you need.

### Syntax

```javascript
for (initialization; condition; increment/decrement) {
  // Code to execute repeatedly
}
```

### Components Breakdown

1. **Initialization** - Sets the starting point
2. **Condition** - Determines when to stop
3. **Increment/Decrement** - Updates the counter after each iteration

```javascript
for (let i = 1; i <= 5; i++) {
  console.log(i);
}

// Breakdown:
// i = 1        → Start at 1
// i <= 5       → Continue while i is less than or equal to 5
// i++          → Increase i by 1 after each iteration
```

### Basic Examples

#### Example 1: Printing Numbers 1 to 10

```javascript
for (let i = 1; i <= 10; i++) {
  console.log(i);
}
// Output: 1 2 3 4 5 6 7 8 9 10
```

#### Example 2: Printing Numbers 1 to 100

```javascript
for (let i = 1; i <= 100; i++) {
  console.log(i);
}
```

#### Example 3: Printing Even Numbers (1 to 20)

```javascript
for (let i = 2; i <= 20; i += 2) {
  console.log(i);
}
// Output: 2 4 6 8 10 12 14 16 18 20
```

#### Example 4: Printing Odd Numbers (1 to 20)

```javascript
for (let i = 1; i <= 20; i += 2) {
  console.log(i);
}
// Output: 1 3 5 7 9 11 13 15 17 19
```

### Reverse Loops (Descending Order)

#### Example 1: Count Down from 10 to 1

```javascript
for (let i = 10; i >= 1; i--) {
  console.log(i);
}
// Output: 10 9 8 7 6 5 4 3 2 1
```

#### Example 2: Count Down from 100 to 1

```javascript
for (let i = 100; i >= 1; i--) {
  console.log(i);
}
```

### Understanding Loop Execution

Let's trace through a simple loop step by step:

```javascript
for (let i = 1; i <= 3; i++) {
  console.log("Iteration " + i);
}
```

**Execution Flow:**

| Step | i value | Condition (i <= 3) | Action | Output |
|------|---------|-------------------|--------|---------|
| 1 | 1 | true | Execute body | "Iteration 1" |
| 2 | 2 | true | Execute body | "Iteration 2" |
| 3 | 3 | true | Execute body | "Iteration 3" |
| 4 | 4 | false | Exit loop | - |

### Loop Counter Variable

**Traditionally:**
- Variable name `i` is used (short for "index" or "iterator")
- For nested loops: `i`, `j`, `k`, etc.

**You can use any valid variable name:**

```javascript
for (let count = 1; count <= 5; count++) {
  console.log(count);
}

for (let num = 10; num >= 1; num--) {
  console.log(num);
}
```

### Comparison: < vs <=

```javascript
// Using <
for (let i = 1; i < 5; i++) {
  console.log(i);
}
// Output: 1 2 3 4 (stops before 5)

// Using <=
for (let i = 1; i <= 5; i++) {
  console.log(i);
}
// Output: 1 2 3 4 5 (includes 5)
```

### Increment/Decrement Variations

```javascript
// Increment by 1
for (let i = 0; i < 10; i++) { }   // i++

// Increment by 2
for (let i = 0; i < 10; i += 2) { }

// Increment by 5
for (let i = 0; i < 50; i += 5) { }

// Decrement by 1
for (let i = 10; i > 0; i--) { }   // i--

// Decrement by 2
for (let i = 10; i > 0; i -= 2) { }
```

### Common For Loop Patterns

**Pattern 1: Iterating Over a Range**

```javascript
// Start at 0, end before n
for (let i = 0; i < n; i++) { }

// Start at 1, end at n (inclusive)
for (let i = 1; i <= n; i++) { }

// Start at 0, end at n (inclusive)
for (let i = 0; i <= n; i++) { }
```

**Pattern 2: Processing Arrays (Preview)**

```javascript
let numbers = [10, 20, 30, 40, 50];
for (let i = 0; i < numbers.length; i++) {
  console.log(numbers[i]);
}
```

---

## 3. Variable Scope: var vs let

### Understanding Scope

**Scope** determines where a variable can be accessed in your code.

### var vs let in Loops

#### Using var (Function/Global Scope)

```javascript
for (var i = 1; i <= 3; i++) {
  console.log("Inside: " + i);
}
console.log("Outside: " + i);  // i is accessible here!
// Output:
// Inside: 1
// Inside: 2
// Inside: 3
// Outside: 4
```

**Key Point:** Variable declared with `var` is accessible **outside the loop**.

#### Using let (Block Scope)

```javascript
for (let i = 1; i <= 3; i++) {
  console.log("Inside: " + i);
}
console.log("Outside: " + i);  // ReferenceError: i is not defined
```

**Key Point:** Variable declared with `let` is **NOT accessible** outside the loop.

### Why This Matters

#### Problem with var

```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(() => console.log(i), 1000);
}
// Output: 5 5 5 5 5 (not what we expected!)
```

#### Solution with let

```javascript
for (let i = 0; i < 5; i++) {
  setTimeout(() => console.log(i), 1000);
}
// Output: 0 1 2 3 4 (correct!)
```

### Best Practice

**✅ Always use `let` (or `const`) in loops**

- Prevents accidental variable leakage
- Avoids bugs in asynchronous code
- Creates new binding for each iteration
- More predictable behavior

---

## 4. Practical Problems with Loops

### Problem 1: Sum of Natural Numbers

#### Problem Statement

Calculate the sum of first `n` natural numbers.

**Example:**
- Input: n = 5
- Output: 1 + 2 + 3 + 4 + 5 = 15

#### Mathematical Formula

```
Sum = n × (n + 1) / 2
```

#### Solution with Loop

```javascript
let n = Number(prompt("Enter a positive number:"));

// Input validation
if (isNaN(n)) {
  console.log("Invalid Input");
} else if (n <= 0) {
  console.log("Number should be positive");
} else {
  let sum = 0;
  
  for (let i = 1; i <= n; i++) {
    sum += i;  // sum = sum + i
  }
  
  console.log(`Sum of first ${n} natural numbers: ${sum}`);
}
```

#### Execution Trace (n = 5)

| Iteration | i | sum before | sum after | Calculation |
|-----------|---|------------|-----------|-------------|
| 1 | 1 | 0 | 1 | 0 + 1 |
| 2 | 2 | 1 | 3 | 1 + 2 |
| 3 | 3 | 3 | 6 | 3 + 3 |
| 4 | 4 | 6 | 10 | 6 + 4 |
| 5 | 5 | 10 | 15 | 10 + 5 |

#### Key Concepts

1. **Initialize sum to 0** - Starting point for accumulation
2. **Loop from 1 to n** - Process each number
3. **Accumulate in sum** - Add each number to running total
4. **Validate input** - Check for valid, positive number

#### Input Validation Table

| Input Condition | Action |
|----------------|--------|
| Non-numeric input (e.g., "abc") | Show "Invalid Input" |
| Number ≤ 0 | Show "Should be positive" |
| Valid positive number | Calculate sum |

---

### Problem 2: Factorial of a Number

#### Problem Statement

Calculate the factorial of `n` (denoted as n!).

**Definition:** n! = n × (n-1) × (n-2) × ... × 2 × 1

**Examples:**
- 5! = 5 × 4 × 3 × 2 × 1 = 120
- 3! = 3 × 2 × 1 = 6
- 0! = 1 (by definition)

#### Solution

```javascript
let n = Number(prompt("Enter a positive number:"));

if (isNaN(n)) {
  console.log("Invalid Input");
} else if (n < 0) {
  console.log("Factorial not defined for negative numbers");
} else {
  let factorial = 1;  // IMPORTANT: Initialize to 1, not 0!
  
  for (let i = 1; i <= n; i++) {
    factorial *= i;  // factorial = factorial * i
  }
  
  console.log(`${n}! = ${factorial}`);
}
```

#### Why Initialize to 1, Not 0?

```javascript
// ❌ WRONG: Initializing to 0
let factorial = 0;
for (let i = 1; i <= 5; i++) {
  factorial *= i;  // 0 * 1 = 0, 0 * 2 = 0, ... always 0!
}
// Result: 0 (incorrect!)

// ✅ CORRECT: Initializing to 1
let factorial = 1;
for (let i = 1; i <= 5; i++) {
  factorial *= i;  // 1 * 1 = 1, 1 * 2 = 2, 2 * 3 = 6, ...
}
// Result: 120 (correct!)
```

#### Execution Trace (n = 5)

| Iteration | i | factorial before | factorial after | Calculation |
|-----------|---|------------------|-----------------|-------------|
| 1 | 1 | 1 | 1 | 1 × 1 |
| 2 | 2 | 1 | 2 | 1 × 2 |
| 3 | 3 | 2 | 6 | 2 × 3 |
| 4 | 4 | 6 | 24 | 6 × 4 |
| 5 | 5 | 24 | 120 | 24 × 5 |

#### Special Cases

```javascript
// 0! = 1 (by mathematical definition)
// 1! = 1

if (n === 0 || n === 1) {
  console.log(`${n}! = 1`);
}
```

---

### Problem 3: Finding Factors of a Number

#### Problem Statement

Find all factors of a given number `n`.

**Definition:** A factor is a number that divides `n` completely (remainder = 0).

**Example:** Factors of 12
- 12 ÷ 1 = 12 (remainder 0) ✓
- 12 ÷ 2 = 6 (remainder 0) ✓
- 12 ÷ 3 = 4 (remainder 0) ✓
- 12 ÷ 4 = 3 (remainder 0) ✓
- 12 ÷ 5 = 2.4 (remainder 2) ✗
- 12 ÷ 6 = 2 (remainder 0) ✓
- ...
- 12 ÷ 12 = 1 (remainder 0) ✓

**Factors:** 1, 2, 3, 4, 6, 12

#### Basic Solution

```javascript
let n = Number(prompt("Enter a number:"));

if (isNaN(n) || n <= 0) {
  console.log("Invalid Input");
} else {
  console.log(`Factors of ${n}:`);
  
  for (let i = 1; i <= n; i++) {
    if (n % i === 0) {
      console.log(i);
    }
  }
}
```

#### Optimized Solution

**Key Insight:** No factor greater than n/2 exists (except n itself).

```javascript
let n = Number(prompt("Enter a number:"));

if (isNaN(n) || n <= 0) {
  console.log("Invalid Input");
} else {
  console.log(`Factors of ${n}:`);
  
  for (let i = 1; i <= n / 2; i++) {
    if (n % i === 0) {
      console.log(i);
    }
  }
  console.log(n);  // n itself is always a factor
}
```

**Performance Comparison:**

| Number | Basic Approach | Optimized Approach | Improvement |
|--------|---------------|-------------------|-------------|
| 100 | 100 iterations | 50 iterations | 50% fewer |
| 1000 | 1000 iterations | 500 iterations | 50% fewer |
| 10000 | 10000 iterations | 5000 iterations | 50% fewer |

#### Even More Optimized (Square Root Method)

```javascript
let n = Number(prompt("Enter a number:"));

if (isNaN(n) || n <= 0) {
  console.log("Invalid Input");
} else {
  console.log(`Factors of ${n}:`);
  
  for (let i = 1; i <= Math.sqrt(n); i++) {
    if (n % i === 0) {
      console.log(i);
      if (i !== n / i) {  // Avoid printing the same factor twice for perfect squares
        console.log(n / i);
      }
    }
  }
}
```

**Example for n = 36:**
- Check 1: Print 1 and 36
- Check 2: Print 2 and 18
- Check 3: Print 3 and 12
- Check 4: Print 4 and 9
- Check 6: Print 6 only (since 6 × 6 = 36)

---

### Problem 4: Prime Number Checker

#### Problem Statement

Determine if a given number is prime.

**Definition:** A prime number is a number greater than 1 that has exactly two factors: 1 and itself.

**Examples:**
- Prime: 2, 3, 5, 7, 11, 13, 17, 19, 23, 29...
- Not Prime: 1, 4, 6, 8, 9, 10, 12, 14, 15...

#### Basic Approach

```javascript
let n = Number(prompt("Enter a number:"));

if (isNaN(n) || n <= 1) {
  console.log("Invalid input or not prime");
} else if (n === 2) {
  console.log(`${n} is prime`);
} else {
  let isPrime = true;  // Assume number is prime
  
  for (let i = 2; i <= n / 2; i++) {
    if (n % i === 0) {
      isPrime = false;  // Found a divisor, not prime
      break;  // Exit early, no need to check further
    }
  }
  
  if (isPrime) {
    console.log(`${n} is prime`);
  } else {
    console.log(`${n} is not prime`);
  }
}
```

#### How It Works

**Example: Check if 17 is prime**

```javascript
n = 17
isPrime = true

Check i = 2: 17 % 2 = 1 (not divisible)
Check i = 3: 17 % 3 = 2 (not divisible)
Check i = 4: 17 % 4 = 1 (not divisible)
Check i = 5: 17 % 5 = 2 (not divisible)
Check i = 6: 17 % 6 = 5 (not divisible)
Check i = 7: 17 % 7 = 3 (not divisible)
Check i = 8: 17 % 8 = 1 (not divisible)

isPrime is still true → 17 is prime
```

**Example: Check if 15 is prime**

```javascript
n = 15
isPrime = true

Check i = 2: 15 % 2 = 1 (not divisible)
Check i = 3: 15 % 3 = 0 (divisible!)
isPrime = false
break (exit loop early)

isPrime is false → 15 is not prime
```

#### Optimized Approach (Square Root)

```javascript
function isPrime(n) {
  // Handle edge cases
  if (n <= 1) return false;
  if (n === 2) return true;
  if (n % 2 === 0) return false;  // Even numbers (except 2) aren't prime
  
  // Check odd divisors up to square root
  for (let i = 3; i <= Math.sqrt(n); i += 2) {
    if (n % i === 0) {
      return false;
    }
  }
  
  return true;
}

let num = Number(prompt("Enter a number:"));
if (isPrime(num)) {
  console.log(`${num} is prime`);
} else {
  console.log(`${num} is not prime`);
}
```

#### Why Check Only Up to Square Root?

**Mathematical Proof:**
If n = a × b, then one of a or b must be ≤ √n

**Example for n = 36:**
- √36 = 6
- Factors: 1×36, 2×18, 3×12, 4×9, 6×6
- Notice: One factor from each pair is ≤ 6

**Performance Improvement:**

| Number | Basic (n/2) | Optimized (√n) | Improvement |
|--------|------------|---------------|-------------|
| 100 | 50 checks | 10 checks | 80% fewer |
| 10000 | 5000 checks | 100 checks | 98% fewer |
| 1000000 | 500000 checks | 1000 checks | 99.8% fewer |

#### Function-Based Implementation

```javascript
function isPrime(n) {
  if (n <= 1) return false;
  if (n === 2) return true;
  if (n % 2 === 0) return false;
  
  for (let i = 3; i <= Math.sqrt(n); i += 2) {
    if (n % i === 0) return false;
  }
  
  return true;
}

// Usage
console.log(isPrime(17));  // true
console.log(isPrime(15));  // false
console.log(isPrime(2));   // true
console.log(isPrime(1));   // false
```

---

## 5. While Loops

### What is a While Loop?

A while loop executes a block of code as long as a specified condition is true. It's best used when you don't know in advance how many iterations you need.

### Syntax

```javascript
initialization;
while (condition) {
  // Code to execute
  // Update statement
}
```

### Comparison with For Loop

**For Loop (Compact):**

```javascript
for (let i = 1; i <= 5; i++) {
  console.log(i);
}
```

**While Loop (Expanded):**

```javascript
let i = 1;              // Initialization
while (i <= 5) {        // Condition
  console.log(i);       // Body
  i++;                  // Update
}
```

### Basic Examples

#### Example 1: Print Numbers 1 to 5

```javascript
let i = 1;
while (i <= 5) {
  console.log(i);
  i++;
}
// Output: 1 2 3 4 5
```

#### Example 2: Sum of Numbers

```javascript
let n = 10;
let sum = 0;
let i = 1;

while (i <= n) {
  sum += i;
  i++;
}

console.log(`Sum: ${sum}`);  // 55
```

#### Example 3: Count Down

```javascript
let count = 10;
while (count > 0) {
  console.log(count);
  count--;
}
console.log("Blast off!");
```

### When to Use While Loops

**✅ Use While Loop When:**

- Number of iterations is **unknown**
- Loop depends on **user input**
- Loop continues until a **specific condition** is met
- Processing data until a **sentinel value** is encountered

**Examples:**

```javascript
// Keep asking until valid input
let password;
while (password !== "secret") {
  password = prompt("Enter password:");
}

// Process until user wants to stop
let continueLoop = true;
while (continueLoop) {
  // Do something
  let response = prompt("Continue? (yes/no)");
  continueLoop = (response === "yes");
}

// Shopping example - continue until money runs out
let money = 1000;
while (money > 0) {
  let itemPrice = Number(prompt("Enter item price:"));
  if (itemPrice <= money) {
    money -= itemPrice;
    console.log(`Remaining money: ${money}`);
  } else {
    console.log("Not enough money!");
  }
}
```

### For vs While: Use Cases

| Scenario | Best Choice | Reason |
|----------|-------------|--------|
| Iterate 1 to 100 | For Loop | Known count |
| Process array | For Loop | Known length |
| User guessing game | While Loop | Unknown attempts |
| Read until EOF | While Loop | Unknown data size |
| Menu selection | While Loop | Until user exits |
| Shopping cart | While Loop | Until done or money out |

### Real-World Example: Number Guessing Game

```javascript
let secretNumber = Math.floor(Math.random() * 100) + 1;
let guess;
let attempts = 0;

while (guess !== secretNumber) {
  guess = Number(prompt("Guess a number between 1 and 100:"));
  attempts++;
  
  if (guess < secretNumber) {
    console.log("Too low! Try again.");
  } else if (guess > secretNumber) {
    console.log("Too high! Try again.");
  } else {
    console.log(`Correct! You guessed it in ${attempts} attempts.`);
  }
}
```

### Infinite Loops (Be Careful!)

**❌ Infinite Loop - Missing Update:**

```javascript
let i = 1;
while (i <= 5) {
  console.log(i);
  // Missing i++
}
// This will run forever!
```

**❌ Infinite Loop - Wrong Condition:**

```javascript
let i = 1;
while (i >= 0) {  // Condition always true
  console.log(i);
  i++;
}
// This will run forever!
```

**✅ Intentional Infinite Loop with Break:**

```javascript
while (true) {
  let input = prompt("Enter a number (0 to exit):");
  if (input === "0") {
    break;  // Exit loop
  }
  console.log(`You entered: ${input}`);
}
```

---

## 6. Do-While Loops

### What is a Do-While Loop?

A do-while loop executes the code block **at least once** before checking the condition. It's an **exit-controlled loop** (condition checked after execution).

### Syntax

```javascript
do {
  // Code to execute
  // This runs AT LEAST ONCE
} while (condition);
```

### Key Difference from While Loop

**While Loop (Entry-Controlled):**
- Checks condition **before** executing body
- May not execute at all if condition is initially false

**Do-While Loop (Exit-Controlled):**
- Executes body **first**
- Checks condition **after** execution
- Always executes at least once

### Comparison Example

```javascript
// While Loop
let x = 10;
while (x < 5) {
  console.log("This will NOT print");
  x++;
}
// Output: (nothing - condition false from start)

// Do-While Loop
let y = 10;
do {
  console.log("This WILL print once");
  y++;
} while (y < 5);
// Output: "This WILL print once"
```

### Basic Examples

#### Example 1: Print at Least Once

```javascript
let i = 1;
do {
  console.log(i);
  i++;
} while (i <= 5);
// Output: 1 2 3 4 5
```

#### Example 2: Menu System

```javascript
let choice;
do {
  console.log("Menu:");
  console.log("1. Option A");
  console.log("2. Option B");
  console.log("3. Exit");
  
  choice = Number(prompt("Enter your choice:"));
  
  switch (choice) {
    case 1:
      console.log("You selected Option A");
      break;
    case 2:
      console.log("You selected Option B");
      break;
    case 3:
      console.log("Goodbye!");
      break;
    default:
      console.log("Invalid choice");
  }
} while (choice !== 3);
```

#### Example 3: Input Validation

```javascript
let number;
do {
  number = Number(prompt("Enter a positive number:"));
  if (number <= 0 || isNaN(number)) {
    console.log("Invalid input. Try again.");
  }
} while (number <= 0 || isNaN(number));

console.log(`You entered: ${number}`);
```

### When to Use Do-While Loops

**✅ Use Do-While When:**

- You need to execute code at least once
- Input validation (always prompt at least once)
- Menu systems (show menu at least once)
- Game loops (play at least one round)

**Common Patterns:**

```javascript
// Pattern 1: Input validation
do {
  input = prompt("Enter value:");
} while (!isValid(input));

// Pattern 2: Repeat until condition
let continueGame;
do {
  playGame();
  continueGame = confirm("Play again?");
} while (continueGame);

// Pattern 3: Process until sentinel
let value;
do {
  value = prompt("Enter value (0 to stop):");
  process(value);
} while (value !== "0");
```

### Real-World Example: ATM PIN Entry

```javascript
const correctPIN = "1234";
let attempts = 0;
const maxAttempts = 3;
let enteredPIN;

do {
  enteredPIN = prompt("Enter your PIN:");
  attempts++;
  
  if (enteredPIN === correctPIN) {
    console.log("Access granted!");
    break;
  } else {
    console.log(`Incorrect PIN. ${maxAttempts - attempts} attempts remaining.`);
  }
} while (attempts < maxAttempts && enteredPIN !== correctPIN);

if (enteredPIN !== correctPIN) {
  console.log("Card blocked. Too many incorrect attempts.");
}
```

---

## 7. Loop Control Statements

### Break Statement

The `break` statement immediately **exits the loop**, regardless of the loop condition.

#### Syntax

```javascript
break;
```

#### Example 1: Exit Loop Early

```javascript
for (let i = 1; i <= 10; i++) {
  if (i === 5) {
    break;  // Exit when i is 5
  }
  console.log(i);
}
// Output: 1 2 3 4
```

#### Example 2: Search and Exit

```javascript
let numbers = [10, 25, 30, 45, 50];
let target = 30;
let found = false;

for (let i = 0; i < numbers.length; i++) {
  if (numbers[i] === target) {
    console.log(`Found ${target} at index ${i}`);
    found = true;
    break;  // Stop searching once found
  }
}

if (!found) {
  console.log(`${target} not found`);
}
```

#### Example 3: Prime Number Check (Optimized)

```javascript
let n = 29;
let isPrime = true;

for (let i = 2; i <= Math.sqrt(n); i++) {
  if (n % i === 0) {
    isPrime = false;
    break;  // Found a divisor, no need to continue
  }
}

console.log(isPrime ? "Prime" : "Not Prime");
```

### Continue Statement

The `continue` statement **skips the current iteration** and moves to the next one.

#### Syntax

```javascript
continue;
```

#### Example 1: Skip Specific Numbers

```javascript
for (let i = 1; i <= 10; i++) {
  if (i === 5) {
    continue;  // Skip 5
  }
  console.log(i);
}
// Output: 1 2 3 4 6 7 8 9 10 (5 is skipped)
```

#### Example 2: Print Only Odd Numbers

```javascript
for (let i = 1; i <= 10; i++) {
  if (i % 2 === 0) {
    continue;  // Skip even numbers
  }
  console.log(i);
}
// Output: 1 3 5 7 9
```

#### Example 3: Skip Invalid Data

```javascript
let scores = [85, -1, 92, 78, -1, 88];

for (let i = 0; i < scores.length; i++) {
  if (scores[i] < 0) {
    continue;  // Skip invalid scores
  }
  console.log(`Score: ${scores[i]}`);
}
// Output: Score: 85, Score: 92, Score: 78, Score: 88
```

### Break vs Continue

| Feature | Break | Continue |
|---------|-------|----------|
| **Action** | Exits loop completely | Skips current iteration |
| **Loop** | Terminates | Continues |
| **Next Line** | After loop | Next iteration |
| **Use Case** | Found what you need | Skip unwanted items |

**Visual Comparison:**

```javascript
// Break - stops at 5
for (let i = 1; i <= 10; i++) {
  if (i === 5) break;
  console.log(i);
}
// Output: 1 2 3 4

// Continue - skips 5
for (let i = 1; i <= 10; i++) {
  if (i === 5) continue;
  console.log(i);
}
// Output: 1 2 3 4 6 7 8 9 10
```

### Practical Example: Number Processor

```javascript
let numbers = [12, -5, 18, 0, 25, -3, 30];

console.log("Processing numbers:");
for (let i = 0; i < numbers.length; i++) {
  let num = numbers[i];
  
  // Skip negative numbers
  if (num < 0) {
    console.log(`Skipping negative: ${num}`);
    continue;
  }
  
  // Stop at zero
  if (num === 0) {
    console.log("Found zero. Stopping.");
    break;
  }
  
  // Process positive numbers
  console.log(`Processing: ${num} → Square: ${num * num}`);
}
```

---

## 8. Optimization Techniques

### Why Optimize?

- **Faster execution** - Programs run quicker
- **Less CPU usage** - More efficient resource utilization
- **Better scalability** - Handles larger inputs
- **Professional code** - Industry best practices

### Technique 1: Reduce Loop Iterations

#### Factor Finding Optimization

**❌ Unoptimized (n iterations):**

```javascript
function findFactors(n) {
  for (let i = 1; i <= n; i++) {
    if (n % i === 0) {
      console.log(i);
    }
  }
}
// For n = 1000: 1000 iterations
```

**✅ Optimized (n/2 iterations):**

```javascript
function findFactors(n) {
  for (let i = 1; i <= n / 2; i++) {
    if (n % i === 0) {
      console.log(i);
    }
  }
  console.log(n);  // n itself
}
// For n = 1000: 500 iterations (50% reduction)
```

**✅ Highly Optimized (√n iterations):**

```javascript
function findFactors(n) {
  for (let i = 1; i <= Math.sqrt(n); i++) {
    if (n % i === 0) {
      console.log(i);
      if (i !== n / i) {  // Avoid duplicate for perfect squares
        console.log(n / i);
      }
    }
  }
}
// For n = 1000: ~31 iterations (97% reduction!)
```

### Technique 2: Early Exit with Break

**❌ Checking all elements:**

```javascript
function isPrime(n) {
  let isPrime = true;
  for (let i = 2; i < n; i++) {  // Checks all numbers
    if (n % i === 0) {
      isPrime = false;
      // Continues checking unnecessarily
    }
  }
  return isPrime;
}
```

**✅ Exit early:**

```javascript
function isPrime(n) {
  for (let i = 2; i <= Math.sqrt(n); i++) {
    if (n % i === 0) {
      return false;  // Exit immediately
    }
  }
  return true;
}
```

### Technique 3: Skip Unnecessary Checks

**❌ Checking all numbers:**

```javascript
function isPrime(n) {
  if (n <= 1) return false;
  for (let i = 2; i < n; i++) {
    if (n % i === 0) return false;
  }
  return true;
}
```

**✅ Skip even numbers:**

```javascript
function isPrime(n) {
  if (n <= 1) return false;
  if (n === 2) return true;
  if (n % 2 === 0) return false;  // Skip all even numbers
  
  for (let i = 3; i <= Math.sqrt(n); i += 2) {  // Only check odd numbers
    if (n % i === 0) return false;
  }
  return true;
}
```

### Technique 4: Cache Repeated Calculations

**❌ Calculating repeatedly:**

```javascript
for (let i = 0; i < array.length; i++) {  // .length calculated each time
  console.log(array[i]);
}
```

**✅ Cache the value:**

```javascript
let len = array.length;  // Calculate once
for (let i = 0; i < len; i++) {
  console.log(array[i]);
}
```

### Performance Comparison

**Prime checking for n = 1,000,000:**

| Method | Iterations | Time (approx) |
|--------|-----------|---------------|
| Basic (2 to n-1) | ~1,000,000 | Very slow |
| Up to n/2 | ~500,000 | Slow |
| Up to √n | ~1,000 | Fast |
| Up to √n, skip evens | ~500 | Very fast |

---

## 9. Practical Applications

### Application 1: Number Guessing Game (Complete)

```javascript
function playGuessingGame() {
  // Generate random number between 1 and 100
  const secretNumber = Math.floor(Math.random() * 100) + 1;
  let attempts = 0;
  const maxAttempts = 10;
  
  console.log("I'm thinking of a number between 1 and 100.");
  console.log(`You have ${maxAttempts} attempts to guess it.`);
  
  while (attempts < maxAttempts) {
    let guess = Number(prompt(`Attempt ${attempts + 1}: Enter your guess:`));
    
    // Validate input
    if (isNaN(guess) || guess < 1 || guess > 100) {
      console.log("Please enter a valid number between 1 and 100.");
      continue;
    }
    
    attempts++;
    
    if (guess === secretNumber) {
      console.log(`🎉 Congratulations! You guessed it in ${attempts} attempts!`);
      return;
    } else if (guess < secretNumber) {
      console.log("Too low! Try a higher number.");
    } else {
      console.log("Too high! Try a lower number.");
    }
    
    console.log(`Attempts remaining: ${maxAttempts - attempts}`);
  }
  
  console.log(`😞 Game over! The number was ${secretNumber}.`);
}

playGuessingGame();
```

### Application 2: Simple Calculator

```javascript
function calculator() {
  let continueCalc = true;
  
  while (continueCalc) {
    console.log("\n=== Simple Calculator ===");
    console.log("1. Addition (+)");
    console.log("2. Subtraction (-)");
    console.log("3. Multiplication (*)");
    console.log("4. Division (/)");
    console.log("5. Exit");
    
    let choice = Number(prompt("Select operation (1-5):"));
    
    if (choice === 5) {
      console.log("Thank you for using the calculator!");
      break;
    }
    
    if (choice < 1 || choice > 5 || isNaN(choice)) {
      console.log("Invalid choice. Please try again.");
      continue;
    }
    
    let num1 = Number(prompt("Enter first number:"));
    let num2 = Number(prompt("Enter second number:"));
    
    if (isNaN(num1) || isNaN(num2)) {
      console.log("Invalid input. Please enter valid numbers.");
      continue;
    }
    
    let result;
    switch (choice) {
      case 1:
        result = num1 + num2;
        console.log(`${num1} + ${num2} = ${result}`);
        break;
      case 2:
        result = num1 - num2;
        console.log(`${num1} - ${num2} = ${result}`);
        break;
      case 3:
        result = num1 * num2;
        console.log(`${num1} * ${num2} = ${result}`);
        break;
      case 4:
        if (num2 === 0) {
          console.log("Error: Cannot divide by zero!");
        } else {
          result = num1 / num2;
          console.log(`${num1} / ${num2} = ${result}`);
        }
        break;
    }
  }
}

calculator();
```

### Application 3: Multiplication Table Generator

```javascript
function multiplicationTable(n) {
  console.log(`Multiplication Table for ${n}:`);
  console.log("=".repeat(30));
  
  for (let i = 1; i <= 10; i++) {
    console.log(`${n} × ${i} = ${n * i}`);
  }
}

let number = Number(prompt("Enter a number:"));
if (!isNaN(number)) {
  multiplicationTable(number);
}
```

### Application 4: Pattern Printing

```javascript
// Right-angled triangle
function printTriangle(n) {
  for (let i = 1; i <= n; i++) {
    let line = "";
    for (let j = 1; j <= i; j++) {
      line += "* ";
    }
    console.log(line);
  }
}

// Output for n = 5:
// *
// * *
// * * *
// * * * *
// * * * * *

printTriangle(5);
```

### Application 5: Sum of Digits

```javascript
function sumOfDigits(n) {
  let sum = 0;
  
  while (n > 0) {
    sum += n % 10;  // Get last digit
    n = Math.floor(n / 10);  // Remove last digit
  }
  
  return sum;
}

console.log(sumOfDigits(12345));  // 1+2+3+4+5 = 15
console.log(sumOfDigits(999));    // 9+9+9 = 27
```

---

## 10. Key Takeaways

### Loop Comparison Summary

| Feature | For Loop | While Loop | Do-While Loop |
|---------|----------|------------|---------------|
| **Best For** | Known iterations | Condition-based | Execute at least once |
| **Syntax** | Compact | Expanded | Block first, condition after |
| **Condition Check** | Before iteration | Before iteration | After iteration |
| **Minimum Executions** | 0 | 0 | 1 |
| **Use Case** | Counting, arrays | User input, games | Menus, validation |

### Essential Concepts

1. **Loop Efficiency**
   - Loops prevent code repetition
   - Reduce file size and improve performance
   - Essential for professional development

2. **Input Validation**
   - Always validate user input
   - Check for numeric values with `isNaN()`
   - Handle edge cases (negative, zero, invalid)

3. **Variable Scope**
   - Use `let` for block scope
   - Avoid `var` to prevent variable leakage
   - Be mindful of where variables are accessible

4. **Optimization Strategies**
   - Reduce iterations when possible (n/2, √n)
   - Use early exit with `break`
   - Skip unnecessary checks with `continue`
   - Cache repeated calculations

5. **Common Patterns**
   - **Accumulation:** Sum, factorial
   - **Search:** Find factors, check prime
   - **Validation:** Input checking, range validation
   - **Iteration:** Process each element

### Input Validation Checklist

```javascript
// Complete validation pattern
let input = prompt("Enter a number:");
let num = Number(input);

if (isNaN(num)) {
  console.log("Invalid input - not a number");
} else if (num <= 0) {
  console.log("Number must be positive");
} else {
  // Process valid input
}
```

### Loop Selection Guide

**Use For Loop When:**
- ✅ Number of iterations is known
- ✅ Iterating through arrays
- ✅ Counting operations
- ✅ Compact syntax preferred

**Use While Loop When:**
- ✅ Iterations depend on condition
- ✅ Processing until user action
- ✅ Unknown iteration count
- ✅ Event-driven logic

**Use Do-While Loop When:**
- ✅ Must execute at least once
- ✅ Menu systems
- ✅ Input validation loops
- ✅ Game loops

### Performance Tips

1. **Minimize Loop Iterations**
   ```javascript
   // Good: Check up to √n instead of n
   for (let i = 2; i <= Math.sqrt(n); i++)
   ```

2. **Exit Early**
   ```javascript
   // Use break when you find what you need
   if (found) break;
   ```

3. **Skip Unnecessary Work**
   ```javascript
   // Use continue to skip iterations
   if (invalid) continue;
   ```

4. **Cache Values**
   ```javascript
   // Calculate once, use many times
   let len = array.length;
   for (let i = 0; i < len; i++)
   ```

### Common Mistakes to Avoid

❌ **Infinite loops** - Forgetting to update counter
❌ **Wrong initialization** - Starting sum/factorial at wrong value
❌ **Off-by-one errors** - Using < instead of <=
❌ **Scope issues** - Using var instead of let
❌ **Missing validation** - Not checking user input
❌ **Inefficient loops** - Not optimizing when possible

### Quick Reference

```javascript
// For Loop
for (let i = start; i <= end; i++) { }

// While Loop
let i = start;
while (i <= end) {
  // code
  i++;
}

// Do-While Loop
let i = start;
do {
  // code
  i++;
} while (i <= end);

// Break (exit loop)
if (condition) break;

// Continue (skip iteration)
if (condition) continue;

// Input Validation
let num = Number(prompt("Enter:"));
if (isNaN(num) || num <= 0) {
  console.log("Invalid");
}
```

### Practice Exercises

1. **Print all even numbers from 1 to 100**
2. **Calculate sum of even numbers and odd numbers separately (1-50)**
3. **Print Fibonacci sequence up to n terms**
4. **Check if a number is perfect (sum of factors equals the number)**
5. **Find GCD (Greatest Common Divisor) of two numbers**
6. **Reverse a number (123 → 321)**
7. **Check if a number is palindrome**
8. **Print all prime numbers between 1 and 100**
9. **Create a countdown timer**
10. **Build a number guessing game with hints**

### Advanced Topics Preview

- **Nested Loops** - Loops within loops
- **Loop with Arrays** - Processing collections
- **Loop with Objects** - Iterating properties
- **Recursive alternatives** - Functions calling themselves
- **Array methods** - forEach, map, filter, reduce

---

## Resources for Further Learning

- Practice loop problems on coding platforms (LeetCode, HackerRank)
- Study algorithm complexity (Big O notation)
- Learn about nested loops and patterns
- Explore array iteration methods
- Understand recursion as an alternative to loops

---

## Final Tips

1. **Practice with pen and paper** - Trace loops manually
2. **Start simple** - Master basic loops before optimization
3. **Test edge cases** - Try n=0, n=1, negative numbers
4. **Think efficiency** - Can you reduce iterations?
5. **Write clean code** - Use meaningful variable names
6. **Comment your logic** - Explain complex loops
7. **Validate inputs** - Always check user data
8. **Break down problems** - Solve step by step

---

**Remember:** Loops are fundamental to programming. Master them well, and you'll be able to solve countless algorithmic problems!

**Happy Coding! 🚀**

---

## FAQ

**Q: What's the difference between for and while loops?**  
A: For loops are best when you know how many iterations you need. While loops are best when iterations depend on a condition.

**Q: Can I use any variable name for loop counter?**  
A: Yes, but `i`, `j`, `k` are conventional. Use descriptive names when helpful.

**Q: Why initialize factorial to 1 instead of 0?**  
A: Because multiplying by 0 always gives 0. Starting at 1 preserves the multiplication chain.

**Q: How do I prevent infinite loops?**  
A: Ensure your loop has a condition that eventually becomes false, and always update your counter/variable.

**Q: When should I use break vs continue?**  
A: Use `break` to exit the loop completely. Use `continue` to skip the current iteration but continue looping.

**Q: Why optimize loops?**  
A: Optimization reduces execution time, especially with large inputs, making programs faster and more efficient.

---
