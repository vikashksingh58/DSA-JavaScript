# Recursion Fundamentals Study Notes
**Sherians Coding School - DSA Series Level 1**

---

## Table of Contents
1. [Stack Memory & Call Stack](#stack-memory--call-stack)
2. [Understanding Return](#understanding-return)
3. [What is Recursion?](#what-is-recursion)
4. [Why Use Recursion?](#why-use-recursion)
5. [Recursion Examples](#recursion-examples)
6. [When to Use Return Keyword](#when-to-use-return-keyword)
7. [Practice Problems](#practice-problems)

---

## Stack Memory & Call Stack

### Stack Data Structure
**LIFO Principle**: Last In, First Out
- The last element inserted is the first one removed

### Real-Life Examples
- **Stack of books**: Last book placed on top is picked first
- **Stack of plates**: At weddings, last plate is taken first
- **Stack of chairs**: Last chair added is first removed
- **Undo/Redo**: Computer operations use stack structure

### Stack Operations
| Operation | Description |
|-----------|-------------|
| **Push** | Insert element into the stack |
| **Pop** | Remove element from the stack |
| **Peek** | Top element of the stack |

### Call Stack
The call stack stores:
1. **Function calls** (in order of invocation)
2. **Primitive variables**: number, string, boolean, undefined, null, bigint

**Memory Distribution**:
- Stack Memory: ~5% (approximate)
- Heap Memory: ~95% (stores objects and non-primitive data)

### How Call Stack Works
```
Function A calls Function B
Function B calls Function C

Stack visualization:
┌─────────────┐
│ Function C  │ ← Top (most recent)
├─────────────┤
│ Function B  │
├─────────────┤
│ Function A  │
└─────────────┘

When C returns → C pops off
When B returns → B pops off
When A returns → A pops off (LIFO)
```

---

## Understanding Return

### Two Purposes of Return

#### 1. Primary Purpose: Terminate Function
- **Immediately exits** the function
- No code after `return` executes
- Pops the function off the call stack

#### 2. Secondary Purpose: Send Value Back
- Returns a value to the caller
- Caller can use this value

### Example
```javascript
function check(num) {
    if (num === 0) {
        return; // terminates here
    }
    console.log("Number is not zero");
}

check(0);  // No output (returns immediately)
check(5);  // Output: "Number is not zero"
```

---

## What is Recursion?

### Definition
**A function calling itself repeatedly until it reaches a stopping point (base case).**

### Two Essential Components

#### 1. Base Case
- The stopping condition
- Prevents infinite recursion
- Returns a fixed value without further recursive calls

#### 2. Recursive Case
- The function calls itself with a **smaller/simpler** problem
- Eventually reaches the base case

### Recursion Formula
```
Recursion = Base Case + Recursive Call
```

---

## Why Use Recursion?

### Problem-Solving Approaches

| Approach | Method |
|----------|--------|
| **Iterative** | Use loops (for, while) |
| **Recursive** | Function calls itself |

### Recursion Benefits
- **Breaks big problems** into smaller subproblems
- **Solves each subproblem** independently
- **Combines results** to get final answer

### Real-Life Analogy
**Teacher with 100 copies to check**:
- Instead of checking all alone
- Divides among 4 teachers (25 each)
- Each teacher solves their part
- Problem solved collectively

### Delegation Analogy
**Project Management**:
```
Client → Manager → Developers
              ├→ Front-end Dev
              ├→ Back-end Dev
              └→ Database Dev

Manager waits for all developers to finish
Then delivers complete project to client
(Similar to recursive calls waiting for subcalls)
```

---

## Recursion Examples

### 1. Print "Hello World" n Times

#### Iterative Approach
```javascript
function printHello(n) {
    for (let i = 0; i < n; i++) {
        console.log("Hello World");
    }
}
```

#### Recursive Approach
```javascript
function printHello(n) {
    if (n === 0) return;        // Base case
    console.log("Hello World");  // Action
    printHello(n - 1);          // Recursive call
}
```

**Stack Behavior**:
- Each call pushed onto stack
- Base case stops recursion
- Functions pop off after completion

---

### 2. Print Numbers from n to 1

```javascript
function printDown(n) {
    if (n === 0) return;    // Base case
    console.log(n);         // Print BEFORE recursion
    printDown(n - 1);       // Recursive call
}

printDown(5); // Output: 5 4 3 2 1
```

**Pattern**: Print → Recurse

---

### 3. Print Numbers from 1 to n

```javascript
function printUp(n) {
    if (n === 0) return;    // Base case
    printUp(n - 1);         // Recursive call FIRST
    console.log(n);         // Print AFTER recursion
}

printUp(5); // Output: 1 2 3 4 5
```

**Pattern**: Recurse → Print

**Why this works**:
- Due to LIFO stack behavior
- Printing happens during **backtracking**
- Functions resume after recursive calls return

---

### 4. Sum of Natural Numbers (1 to n)

#### Recursive Leap of Faith
Trust that `sum(n-1)` returns the correct sum of numbers from 1 to n-1

```javascript
function sum(n) {
    if (n === 1) return 1;      // Base case
    return n + sum(n - 1);      // Recursive call
}

sum(5); // Returns: 15 (1+2+3+4+5)
```

**Execution Flow**:
```
sum(5) = 5 + sum(4)
       = 5 + (4 + sum(3))
       = 5 + (4 + (3 + sum(2)))
       = 5 + (4 + (3 + (2 + sum(1))))
       = 5 + (4 + (3 + (2 + 1)))
       = 15
```

---

### 5. Factorial of n

```javascript
function factorial(n) {
    if (n === 1) return 1;          // Base case
    return n * factorial(n - 1);    // Recursive call
}

factorial(6); // Returns: 720
```

**Calculation**:
```
6! = 6 × 5!
   = 6 × 5 × 4!
   = 6 × 5 × 4 × 3!
   = 6 × 5 × 4 × 3 × 2!
   = 6 × 5 × 4 × 3 × 2 × 1
   = 720
```

---

### 6. Fibonacci Series

#### Definition
```
F(0) = 0
F(1) = 1
F(n) = F(n-1) + F(n-2)  for n ≥ 2

Series: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34...
```

#### Iterative Approach (Print first n terms)
```javascript
function fibIterative(n) {
    let a = 0, b = 1;
    console.log(a); // F(0)
    console.log(b); // F(1)
    
    for (let i = 2; i < n; i++) {
        let next = a + b;
        console.log(next);
        a = b;
        b = next;
    }
}
```

#### Recursive Approach (Return nth term)
```javascript
function fib(n) {
    if (n === 0) return 0;      // Base case 1
    if (n === 1) return 1;      // Base case 2
    return fib(n-1) + fib(n-2); // Recursive calls
}

fib(6); // Returns: 8
```

#### Fibonacci Recursion Tree
```
                    fib(5)
                   /      \
              fib(4)      fib(3)
             /     \      /     \
        fib(3)   fib(2) fib(2) fib(1)
        /   \    /   \  /   \
    fib(2) fib(1) ...
    /   \
fib(1) fib(0)
```

**Key Points**:
- Each call waits for TWO recursive calls
- Left subtree resolved before right subtree
- Base cases trigger backtracking
- Multiple calls to same values (inefficient for large n)

---

## When to Use Return Keyword

### Rule of Thumb
**Use `return` with recursive calls when the calling function depends on the result**

### Scenarios

#### ✅ Use Return (Dependent Calls)
```javascript
// Caller needs the result
function sum(n) {
    if (n === 1) return 1;
    return n + sum(n - 1);  // MUST use return
}

function factorial(n) {
    if (n === 1) return 1;
    return n * factorial(n - 1);  // MUST use return
}

function fib(n) {
    if (n === 0) return 0;
    if (n === 1) return 1;
    return fib(n-1) + fib(n-2);  // MUST use return
}
```

#### ❌ Don't Need Return (Independent Calls)
```javascript
// Caller doesn't need result, just executes
function printHello(n) {
    if (n === 0) return;
    console.log("Hello World");
    printHello(n - 1);  // No return needed
}

function printDown(n) {
    if (n === 0) return;
    console.log(n);
    printDown(n - 1);  // No return needed
}
```

---

## Key Concepts Summary

### Backtracking
**Execution of code AFTER recursive calls return, during stack unwinding**

Example:
```javascript
function printUp(n) {
    if (n === 0) return;
    printUp(n - 1);        // Goes down first
    console.log(n);        // Executes during backtracking
}
```

### Recursion vs Iteration

| Aspect | Recursion | Iteration |
|--------|-----------|-----------|
| **Approach** | Function calls itself | Uses loops |
| **Memory** | Uses call stack | Uses loop variables |
| **Base case** | Required | Loop condition |
| **Readability** | Often cleaner for complex problems | Straightforward for simple loops |
| **Performance** | Stack overhead | Generally faster |

---

## Practice Problems

### Beginner Level
1. ✅ Print "Hello World" n times
2. ✅ Print numbers n to 1
3. ✅ Print numbers 1 to n
4. ✅ Sum of natural numbers 1 to n
5. ✅ Factorial of n

### Intermediate Level
6. ✅ Fibonacci nth term
7. Print Fibonacci series (first n terms)
8. Power function: x^n
9. Count digits in a number
10. Reverse a number

### Advanced Level
11. Check if string is palindrome
12. Tower of Hanoi
13. Generate all subsets
14. Generate all permutations

---

## Common Mistakes to Avoid

### 1. Missing Base Case
```javascript
// ❌ WRONG - Infinite recursion!
function print(n) {
    console.log(n);
    print(n - 1);  // Never stops
}

// ✅ CORRECT
function print(n) {
    if (n === 0) return;  // Base case
    console.log(n);
    print(n - 1);
}
```

### 2. Forgetting Return Keyword
```javascript
// ❌ WRONG - Returns undefined
function sum(n) {
    if (n === 1) return 1;
    n + sum(n - 1);  // Missing return!
}

// ✅ CORRECT
function sum(n) {
    if (n === 1) return 1;
    return n + sum(n - 1);  // Has return
}
```

### 3. Wrong Base Case
```javascript
// ❌ WRONG - May skip base case
function factorial(n) {
    if (n === 0) return 1;
    return n * factorial(n - 1);  // What if n is negative?
}

// ✅ BETTER
function factorial(n) {
    if (n <= 1) return 1;  // Handles 0 and 1
    return n * factorial(n - 1);
}
```

---

## Study Tips

### Understanding Recursion
1. **Draw stack diagrams** for each example
2. **Trace execution** step by step
3. **Identify base case** first
4. **Trust the recursive leap** - assume smaller problem works
5. **Practice backtracking** examples (print 1 to n)

### Memory Aid
**"BRAC" for Recursion**:
- **B**ase case (stopping condition)
- **R**ecursive call (smaller problem)
- **A**ction (what to do)
- **C**ombine results (if needed)

### Debugging Recursion
- Add `console.log` before and after recursive calls
- Print current parameter values
- Track stack depth
- Verify base case is reachable

---

## Interview Preparation

### Common Questions
1. What is recursion?
2. Explain call stack behavior in recursion
3. What is a base case and why is it needed?
4. Difference between recursion and iteration?
5. What is stack overflow?
6. When to use return with recursive calls?

### Problem-Solving Strategy
1. **Identify** if problem can be broken into smaller subproblems
2. **Define** base case(s)
3. **Define** recursive case
4. **Determine** if return is needed
5. **Test** with small inputs
6. **Trace** execution with stack diagram

---

## Additional Resources

### Practice Platforms
- LeetCode (Recursion tag)
- HackerRank (Recursion problems)
- CodeForces (Beginners section)

### Visual Tools
- Python Tutor (visualize call stack)
- Recursion Tree visualizers
- Stack memory diagrams

---

## Lecture Timeline Reference

| Time | Topic |
|------|-------|
| 00:00 - 02:16 | Introduction, Stack memory basics |
| 02:16 - 08:15 | Call stack and stack operations |
| 08:15 - 13:22 | Return keyword explained |
| 14:19 - 21:30 | Why and what is recursion |
| 22:26 - 30:24 | Print examples with recursion |
| 30:24 - 45:38 | Print n to 1 and 1 to n |
| 46:08 - 58:10 | Sum of natural numbers |
| 58:10 - 01:01:51 | When to use return keyword |
| 01:00:08 - 01:01:51 | Factorial of n |
| 01:01:51 - 01:29:10 | Fibonacci series |

---

## Quick Reference Card

```
RECURSION CHECKLIST
□ Base case defined?
□ Recursive call with smaller problem?
□ Need return keyword?
□ Base case reachable?
□ Tested with small inputs?
```

**Remember**: Practice with stack diagrams for deep understanding! 🚀