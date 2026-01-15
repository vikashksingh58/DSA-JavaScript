# JavaScript Conditional Statements
## Comprehensive Study Notes - DSA Series Part 2

---

## Table of Contents

1. [Introduction to Conditional Statements](#1-introduction-to-conditional-statements)
2. [If-Else Fundamentals](#2-if-else-fundamentals)
3. [Valid Voter Problem](#3-valid-voter-problem)
4. [Shop Discount Problem](#4-shop-discount-problem)
5. [Electricity Bill Problem](#5-electricity-bill-problem)
6. [INR Denomination Problem](#6-inr-denomination-problem)
7. [Ternary Operators](#7-ternary-operators)
8. [Switch-Case Statements](#8-switch-case-statements)
9. [Floating Point Precision Issues](#9-floating-point-precision-issues)
10. [Key Takeaways](#10-key-takeaways)

---

## 1. Introduction to Conditional Statements

Conditional statements allow your program to make decisions and execute different code blocks based on specific conditions. They are fundamental to programming logic and problem-solving.

### Topics Covered in This Session

- Valid Voter eligibility checking
- Shop discount calculation
- Electricity bill calculation
- Currency denomination breakdown
- Ternary operator and nested ternary operators
- Switch-case statements
- Handling fall-through behavior
- Floating-point precision issues

---

## 2. If-Else Fundamentals

### Basic Syntax

```javascript
if (condition) {
  // Executes if condition is true
} else {
  // Executes if condition is false
}
```

### Key Rules

1. **If can exist independently** - You can have an `if` without an `else`
2. **Else cannot exist without if** - Using `else` without a preceding `if` causes a syntax error
3. **The if block executes only when its condition evaluates to true**
4. **The else block executes only when the if condition is false AND an else block is present**

### Condition Evaluation Examples

```javascript
// False condition
if (12 > 13) {
  console.log("This won't execute");
}

// True condition
if (12 < 13) {
  console.log("This will execute");
}

// Multiple conditions
if (age >= 18 && age <= 60) {
  console.log("Working age");
}
```

### Important Notes

- **Conditions must evaluate to boolean** (true or false)
- **String inputs don't automatically evaluate as conditions** - they need conversion or validation
- Use comparison operators: `>`, `<`, `>=`, `<=`, `===`, `!==`
- Use logical operators: `&&` (AND), `||` (OR), `!` (NOT)

---

## 3. Valid Voter Problem

### Problem Statement

Check if a person is eligible to vote based on their age. The minimum voting age is 18 years.

### Requirements

- Take age input from user
- Validate if input is a valid number
- Check if age >= 18
- Handle invalid inputs gracefully

### Solution Approach

```javascript
// Step 1: Get input from user
let ageInput = prompt("Enter your age:");

// Step 2: Convert to number
let age = Number(ageInput);

// Step 3: Check for invalid input
if (isNaN(age)) {
  console.log("Invalid Input");
} else if (age >= 18) {
  console.log("You can vote");
} else {
  console.log("You cannot vote");
}
```

### Key Concepts

**1. Prompt Returns String**

```javascript
let input = prompt("Enter age:");
// input is ALWAYS a string, even if user types "25"
console.log(typeof input); // "string"
```

**2. Type Conversion is Essential**

```javascript
let age = Number(input);  // Convert string to number
```

**3. Input Validation with isNaN()**

```javascript
if (isNaN(age)) {
  // Not a valid number (e.g., "abc", "12abc")
  console.log("Invalid Input");
}
```

### Edge Cases to Handle

- **Non-numeric input:** "abc", "twenty", "12abc"
- **Empty input:** User presses Cancel or submits empty
- **Negative numbers:** -5 (technically a number, but illogical for age)
- **Decimal numbers:** 17.5 (valid but needs decision on how to handle)

### Complete Implementation

```javascript
let ageInput = prompt("Enter your age:");
let age = Number(ageInput);

if (isNaN(age) || age < 0) {
  console.log("Invalid Input");
} else if (age >= 18) {
  console.log("You are eligible to vote");
} else {
  console.log("You are not eligible to vote");
}
```

---

## 4. Shop Discount Problem

### Problem Statement

Calculate the discount and final payable amount based on the shopping bill amount using tiered discount slabs.

### Discount Slabs

| Bill Amount Range (₹) | Discount (%) |
|-----------------------|--------------|
| 0 - 5000              | 0%           |
| 5001 - 7000           | 5%           |
| 7001 - 9000           | 10%          |
| Above 9000            | 20%          |

### Examples

**Example 1: Bill Amount = ₹8000**
- Falls in 7001-9000 range
- Discount = 10%
- Discount Amount = 8000 × 10% = ₹800
- Payable Amount = 8000 - 800 = ₹7200

**Example 2: Bill Amount = ₹6000**
- Falls in 5001-7000 range
- Discount = 5%
- Discount Amount = 6000 × 5% = ₹300
- Payable Amount = 6000 - 300 = ₹5700

**Example 3: Bill Amount = ₹12000**
- Falls in Above 9000 range
- Discount = 20%
- Discount Amount = 12000 × 20% = ₹2400
- Payable Amount = 12000 - 2400 = ₹9600

### Solution Approach

```javascript
let amount = Number(prompt("Enter bill amount:"));
let discountPercent = 0;
let discountAmount = 0;
let payableAmount = 0;

// Determine discount percentage based on bill amount
if (amount <= 5000) {
  discountPercent = 0;
} else if (amount <= 7000) {
  discountPercent = 5;
} else if (amount <= 9000) {
  discountPercent = 10;
} else {
  discountPercent = 20;
}

// Calculate discount and payable amount
discountAmount = Math.floor((discountPercent * amount) / 100);
payableAmount = amount - discountAmount;

console.log(`Bill Amount: ₹${amount}`);
console.log(`Discount: ${discountPercent}%`);
console.log(`Discount Amount: ₹${discountAmount}`);
console.log(`Payable Amount: ₹${payableAmount}`);
```

### Key Concepts

**1. If-Else If Ladder**

```javascript
if (condition1) {
  // Block 1
} else if (condition2) {
  // Block 2
} else if (condition3) {
  // Block 3
} else {
  // Default block
}
```

**2. Range Checking with <=**

```javascript
if (amount <= 5000) {
  // 0 to 5000
} else if (amount <= 7000) {
  // 5001 to 7000 (already checked > 5000)
} else if (amount <= 9000) {
  // 7001 to 9000
}
```

**3. Discount Formula**

```javascript
discountAmount = (discountPercent * amount) / 100;
// or
discountAmount = amount * (discountPercent / 100);

// Use Math.floor() to get integer amount
discountAmount = Math.floor((discountPercent * amount) / 100);
```

### Important Notes

- **Order matters** - Check conditions in sequence
- **Use else if** for mutually exclusive ranges
- **Math.floor()** removes decimal places for cleaner currency amounts
- This is a "brute force" approach - more efficient solutions exist for complex scenarios

---

## 5. Electricity Bill Problem

### Problem Statement

Calculate electricity bill based on tiered unit pricing. Different price rates apply to different consumption ranges.

### Pricing Tiers

| Unit Range     | Price per Unit (₹) |
|----------------|--------------------|
| 0 - 100        | 4.2                |
| 101 - 200      | 6                  |
| 201 - 400      | 8                  |
| 401+           | 13                 |

### Key Concept: Cumulative Billing

**Important:** Unlike the discount problem, electricity billing is **cumulative**. You pay different rates for different portions of your consumption.

### Example: 120 Units Consumed

```
First 100 units  → 100 × 4.2 = ₹420
Next 20 units    → 20 × 6 = ₹120
Total Bill       → ₹420 + ₹120 = ₹540
```

### Example: 350 Units Consumed

```
First 100 units  → 100 × 4.2 = ₹420
Next 100 units   → 100 × 6 = ₹600
Next 150 units   → 150 × 8 = ₹1200
Total Bill       → ₹420 + ₹600 + ₹1200 = ₹2220
```

### Solution Approach (Bottom-Up Method)

```javascript
let units = Number(prompt("Enter units consumed:"));
let bill = 0;

// Calculate from highest slab downward
if (units > 400) {
  // Units above 400
  bill += (units - 400) * 13;
  units = 400;
}

if (units > 200) {
  // Units from 201 to 400
  bill += (units - 200) * 8;
  units = 200;
}

if (units > 100) {
  // Units from 101 to 200
  bill += (units - 100) * 6;
  units = 100;
}

// Remaining units (0 to 100)
bill += units * 4.2;

console.log(`Total Electricity Bill: ₹${bill.toFixed(2)}`);
```

### Step-by-Step Breakdown for 120 Units

```javascript
let units = 120;
let bill = 0;

// Check if units > 400 → No
// Check if units > 200 → No
// Check if units > 100 → Yes
if (units > 100) {
  bill += (120 - 100) * 6;  // bill = 20 × 6 = 120
  units = 100;
}

// Calculate remaining 100 units
bill += 100 * 4.2;  // bill = 120 + 420 = 540

console.log(`Total Bill: ₹${bill}`); // ₹540
```

### Alternative Approach (Top-Down Method)

```javascript
let units = Number(prompt("Enter units consumed:"));
let bill = 0;

// First 100 units
if (units > 0) {
  let unitsInSlab = Math.min(units, 100);
  bill += unitsInSlab * 4.2;
  units -= unitsInSlab;
}

// Next 100 units (101-200)
if (units > 0) {
  let unitsInSlab = Math.min(units, 100);
  bill += unitsInSlab * 6;
  units -= unitsInSlab;
}

// Next 200 units (201-400)
if (units > 0) {
  let unitsInSlab = Math.min(units, 200);
  bill += unitsInSlab * 8;
  units -= unitsInSlab;
}

// Remaining units (401+)
if (units > 0) {
  bill += units * 13;
}

console.log(`Total Bill: ₹${bill.toFixed(2)}`);
```

### Key Concepts

**1. Tiered Calculation**

Each tier is calculated independently and added to the total.

**2. Bottom-Up vs Top-Down**

- **Bottom-Up:** Start from highest tier, work down
- **Top-Down:** Start from lowest tier, work up
- Both methods produce the same result

**3. Using Math.min()**

```javascript
let unitsInSlab = Math.min(remainingUnits, slabLimit);
// Takes the smaller of two values
```

**4. Accumulating Total**

```javascript
bill += slabAmount;  // Shorthand for: bill = bill + slabAmount
```

---

## 6. INR Denomination Problem

### Problem Statement

Given an amount, calculate the minimum number of currency notes needed for each denomination.

### Indian Currency Denominations

₹500, ₹200, ₹100, ₹50, ₹20, ₹10, ₹5, ₹2, ₹1

### Algorithm: Greedy Approach

1. Start with the **largest denomination**
2. Calculate how many notes of that denomination fit in the amount
3. Calculate the **remainder** after removing those notes
4. Move to the **next smaller denomination**
5. Repeat until the amount becomes zero

### Example: ₹4823

| Denomination (₹) | Calculation | Notes Count | Remaining Amount (₹) |
|------------------|-------------|-------------|----------------------|
| 500              | 4823 ÷ 500  | 9           | 4823 - 4500 = 323    |
| 200              | 323 ÷ 200   | 1           | 323 - 200 = 123      |
| 100              | 123 ÷ 100   | 1           | 123 - 100 = 23       |
| 50               | 23 ÷ 50     | 0           | 23                   |
| 20               | 23 ÷ 20     | 1           | 23 - 20 = 3          |
| 10               | 3 ÷ 10      | 0           | 3                    |
| 5                | 3 ÷ 5       | 0           | 3                    |
| 2                | 3 ÷ 2       | 1           | 3 - 2 = 1            |
| 1                | 1 ÷ 1       | 1           | 1 - 1 = 0            |

**Total:** 9×₹500 + 1×₹200 + 1×₹100 + 1×₹20 + 1×₹2 + 1×₹1 = ₹4823 ✓

### Solution Implementation

```javascript
let amount = Number(prompt("Enter amount:"));
let originalAmount = amount;

// Calculate for ₹500
let note500 = Math.floor(amount / 500);
amount = amount % 500;

// Calculate for ₹200
let note200 = Math.floor(amount / 200);
amount = amount % 200;

// Calculate for ₹100
let note100 = Math.floor(amount / 100);
amount = amount % 100;

// Calculate for ₹50
let note50 = Math.floor(amount / 50);
amount = amount % 50;

// Calculate for ₹20
let note20 = Math.floor(amount / 20);
amount = amount % 20;

// Calculate for ₹10
let note10 = Math.floor(amount / 10);
amount = amount % 10;

// Calculate for ₹5
let note5 = Math.floor(amount / 5);
amount = amount % 5;

// Calculate for ₹2
let note2 = Math.floor(amount / 2);
amount = amount % 2;

// Calculate for ₹1
let note1 = amount;

// Display results
console.log(`Amount: ₹${originalAmount}`);
console.log(`₹500: ${note500}`);
console.log(`₹200: ${note200}`);
console.log(`₹100: ${note100}`);
console.log(`₹50: ${note50}`);
console.log(`₹20: ${note20}`);
console.log(`₹10: ${note10}`);
console.log(`₹5: ${note5}`);
console.log(`₹2: ${note2}`);
console.log(`₹1: ${note1}`);
```

### Key Concepts

**1. Integer Division with Math.floor()**

```javascript
let noteCount = Math.floor(amount / denomination);
// Returns the largest integer ≤ result
// Example: Math.floor(4823 / 500) = Math.floor(9.646) = 9
```

**2. Modulus Operator for Remainder**

```javascript
let remainder = amount % denomination;
// Returns what's left after division
// Example: 4823 % 500 = 323
```

**3. Combined Operation Pattern**

```javascript
let notes = Math.floor(amount / denomination);
amount = amount % denomination;
// or shorthand:
amount %= denomination;
```

**4. Why Use Independent If Statements?**

```javascript
// ❌ WRONG - Using if-else
if (amount >= 500) {
  // ...
} else if (amount >= 200) {
  // This won't execute if amount was >= 500
}

// ✅ CORRECT - Using independent if statements
if (amount >= 500) {
  // ...
  amount %= 500;
}
if (amount >= 200) {
  // This will execute with the updated amount
  amount %= 200;
}
```

**5. Importance of Order**

Always process denominations from **largest to smallest** to minimize the number of notes.

### Optimized Version with Array

```javascript
let amount = Number(prompt("Enter amount:"));
const denominations = [500, 200, 100, 50, 20, 10, 5, 2, 1];

console.log(`Amount: ₹${amount}`);

for (let denom of denominations) {
  if (amount >= denom) {
    let count = Math.floor(amount / denom);
    console.log(`₹${denom}: ${count}`);
    amount %= denom;
  }
}
```

---

## 7. Ternary Operators

### What is a Ternary Operator?

The ternary operator is a shorthand for simple if-else statements. It's called "ternary" because it takes three operands.

### Syntax

```javascript
condition ? expressionIfTrue : expressionIfFalse
```

### Basic Examples

```javascript
// Traditional if-else
let age = 20;
let status;
if (age >= 18) {
  status = "Adult";
} else {
  status = "Minor";
}

// Ternary operator equivalent
let status = age >= 18 ? "Adult" : "Minor";
```

```javascript
// Example 2
console.log(12 > 13 ? "Hello" : "Huhu"); // Prints "Huhu"

// Example 3
let num = 5;
let result = num % 2 === 0 ? "Even" : "Odd";
console.log(result); // "Odd"
```

### Nested Ternary Operators

You can nest ternary operators for multiple conditions, but use them carefully as they can become hard to read.

```javascript
let num = 0;
let result = num > 0 ? "Positive" : (num < 0 ? "Negative" : "Zero");
console.log(result); // "Zero"
```

**Breaking down the nested ternary:**

```javascript
// Outer ternary
num > 0 ? "Positive" : (inner ternary)

// Inner ternary (executes if num is not > 0)
num < 0 ? "Negative" : "Zero"
```

### More Nested Examples

```javascript
// Age category
let age = 25;
let category = age < 13 ? "Child" 
             : age < 20 ? "Teenager"
             : age < 60 ? "Adult"
             : "Senior";
console.log(category); // "Adult"

// Grade evaluation
let score = 85;
let grade = score >= 90 ? "A"
          : score >= 80 ? "B"
          : score >= 70 ? "C"
          : score >= 60 ? "D"
          : "F";
console.log(grade); // "B"
```

### When to Use Ternary Operators

**✅ Good Use Cases:**

```javascript
// Simple conditional assignment
let status = isLoggedIn ? "Welcome" : "Please login";

// Inline conditional display
console.log(`You ${age >= 18 ? "can" : "cannot"} vote`);

// Setting default values
let name = userName ? userName : "Guest";
// or with nullish coalescing
let name = userName ?? "Guest";
```

**❌ Avoid When:**

- Logic becomes too complex
- Multiple statements needed in each branch
- Readability suffers
- More than 2 levels of nesting

### Comparison: If-Else vs Ternary

```javascript
// If-Else (better for multiple statements)
if (age >= 18) {
  console.log("You are an adult");
  canVote = true;
  canDrive = true;
} else {
  console.log("You are a minor");
  canVote = false;
  canDrive = false;
}

// Ternary (better for simple assignments)
let canVote = age >= 18 ? true : false;
// or simply: let canVote = age >= 18;
```

---

## 8. Switch-Case Statements

### What is Switch-Case?

Switch-case is a conditional control structure used for matching **exact values** against multiple possible cases. It's most useful when you have many specific values to check against.

### Syntax

```javascript
switch (expression) {
  case value1:
    // Code to execute if expression === value1
    break;
  case value2:
    // Code to execute if expression === value2
    break;
  case value3:
    // Code to execute if expression === value3
    break;
  default:
    // Code to execute if no case matches
}
```

### Basic Example: Day of the Week

```javascript
let day = 2;

switch (day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  case 3:
    console.log("Wednesday");
    break;
  case 4:
    console.log("Thursday");
    break;
  case 5:
    console.log("Friday");
    break;
  case 6:
    console.log("Saturday");
    break;
  case 7:
    console.log("Sunday");
    break;
  default:
    console.log("Invalid day");
}
// Output: Tuesday
```

### The Break Statement

**Critical:** The `break` statement is essential to prevent **fall-through** behavior.

#### Without Break (Fall-Through)

```javascript
let day = 2;

switch (day) {
  case 1:
    console.log("Monday");
  case 2:
    console.log("Tuesday");  // Matches here
  case 3:
    console.log("Wednesday"); // Also executes
  case 4:
    console.log("Thursday");  // Also executes
  default:
    console.log("Invalid");   // Also executes
}

// Output:
// Tuesday
// Wednesday
// Thursday
// Invalid
```

#### With Break (Correct)

```javascript
let day = 2;

switch (day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;  // Stops execution here
  case 3:
    console.log("Wednesday");
    break;
  default:
    console.log("Invalid");
}

// Output:
// Tuesday
```

### Multiple Cases with Same Code

You can stack multiple case labels to execute the same code for different values:

```javascript
let day = 3;

switch (day) {
  case 1:
  case 2:
  case 3:
  case 4:
  case 5:
    console.log("Weekday");
    break;
  case 6:
  case 7:
    console.log("Weekend");
    break;
  default:
    console.log("Invalid day");
}
// Output: Weekday
```

### Practical Example: Menu Selection

```javascript
let choice = prompt("Choose an option: 1-Add, 2-Edit, 3-Delete, 4-Exit");
choice = Number(choice);

switch (choice) {
  case 1:
    console.log("Adding new record...");
    break;
  case 2:
    console.log("Editing record...");
    break;
  case 3:
    console.log("Deleting record...");
    break;
  case 4:
    console.log("Exiting program...");
    break;
  default:
    console.log("Invalid choice");
}
```

### Practical Example: Grade Converter

```javascript
let grade = "B";

switch (grade) {
  case "A":
    console.log("Excellent! 90-100%");
    break;
  case "B":
    console.log("Good! 80-89%");
    break;
  case "C":
    console.log("Average! 70-79%");
    break;
  case "D":
    console.log("Below Average! 60-69%");
    break;
  case "F":
    console.log("Failed! Below 60%");
    break;
  default:
    console.log("Invalid grade");
}
```

### Switch vs If-Else: When to Use Each

#### Use Switch-Case When:

✅ Checking **exact equality** against multiple constant values
✅ Working with **discrete options** (menu, days, grades, status codes)
✅ Values are **known at compile time**
✅ Need **cleaner code** for many exact matches

```javascript
// Good use of switch
switch (statusCode) {
  case 200: return "OK";
  case 404: return "Not Found";
  case 500: return "Server Error";
}
```

#### Use If-Else When:

✅ Checking **ranges** or **complex conditions**
✅ Using **comparison operators** (<, >, <=, >=)
✅ Combining multiple conditions with **logical operators**
✅ Conditions involve **expressions or calculations**

```javascript
// Good use of if-else
if (age < 13) {
  category = "Child";
} else if (age < 20) {
  category = "Teenager";
} else {
  category = "Adult";
}

// This CANNOT be done with switch
if (score >= 90 && attendance >= 80) {
  console.log("Excellent performance");
}
```

### Switch Limitations

❌ **Cannot use expressions in cases:**

```javascript
// ❌ This doesn't work
let x = 10;
switch (x) {
  case x > 5:  // Wrong! Case must be a value, not expression
    console.log("Greater than 5");
    break;
}

// ✅ Use if-else instead
if (x > 5) {
  console.log("Greater than 5");
}
```

❌ **Cannot use ranges:**

```javascript
// ❌ This doesn't work
switch (age) {
  case 0-12:  // Wrong! Cannot specify range
    console.log("Child");
    break;
}
```

### Important Notes

1. **Strict Equality:** Switch uses `===` for comparison (type and value must match)

```javascript
let value = "2";
switch (value) {
  case 2:  // Won't match because "2" !== 2
    console.log("Two");
    break;
  case "2":  // This will match
    console.log("String Two");
    break;
}
```

2. **Default is Optional:** You don't need a default case, but it's good practice

3. **Break in Default:** Break in the default case is optional if it's last, but include it for consistency

---

## 9. Floating Point Precision Issues

### The Problem

Floating-point numbers in JavaScript (and most programming languages) cannot always be represented exactly in binary, leading to precision errors.

### Example of the Issue

```javascript
console.log(0.1 + 0.2);  // 0.30000000000000004 (not exactly 0.3!)
console.log(0.1 + 0.2 === 0.3);  // false
```

### Why This Happens

Computers store numbers in binary (base-2), but some decimal fractions cannot be represented exactly in binary, just like 1/3 cannot be exactly represented in decimal (0.333...).

### Impact on Switch Statements

```javascript
let value = 0.1 + 0.2;

switch (value) {
  case 0.3:
    console.log("Matched 0.3");
    break;
  default:
    console.log("Did not match");  // This executes!
}
// Output: Did not match
```

### Solutions

#### Solution 1: Use Epsilon Comparison

```javascript
const EPSILON = 0.0001;

function areEqual(a, b) {
  return Math.abs(a - b) < EPSILON;
}

let value = 0.1 + 0.2;
if (areEqual(value, 0.3)) {
  console.log("Approximately equal to 0.3");
}
```

#### Solution 2: Convert to Integers

```javascript
// Multiply by power of 10 to work with integers
let value = (0.1 * 10 + 0.2 * 10) / 10;  // Still has issues

// Better: work with cents instead of dollars
let price1 = 10;  // 10 cents
let price2 = 20;  // 20 cents
let total = price1 + price2;  // 30 cents
```

#### Solution 3: Use toFixed() for Rounding

```javascript
let value = (0.1 + 0.2).toFixed(2);  // "0.30" (string)
let valueNum = parseFloat(value);     // 0.3 (number)

console.log(valueNum === 0.3);  // true
```

#### Solution 4: Avoid Floating Point Equality

```javascript
// ❌ Don't do this
if (value === 0.3) { }

// ✅ Do this instead
if (Math.abs(value - 0.3) < 0.0001) { }
```

### Best Practices

1. **Avoid direct equality comparisons** with floating-point numbers
2. **Use integers** when possible (e.g., work with cents instead of dollars)
3. **Round or fix precision** when displaying to users
4. **Use libraries** like decimal.js or big.js for precise decimal arithmetic
5. **Be aware** of the limitations when working with money or precise measurements

### Example: Working with Money

```javascript
// ❌ Bad Practice
let price = 10.1;
let tax = 1.2;
let total = price + tax;
console.log(total);  // 11.299999999999999

// ✅ Good Practice (work with cents)
let priceCents = 1010;  // 10.10 in cents
let taxCents = 120;     // 1.20 in cents
let totalCents = priceCents + taxCents;  // 1130 cents
let totalDollars = totalCents / 100;     // 11.30
console.log(totalDollars.toFixed(2));    // "11.30"
```

---

## 10. Key Takeaways

### Conditional Statements Summary

| Feature | If-Else | Ternary | Switch-Case |
|---------|---------|---------|-------------|
| **Use Case** | Any condition | Simple conditions | Exact value matching |
| **Complexity** | Can be complex | Best when simple | Multiple discrete values |
| **Ranges** | ✅ Yes | ✅ Yes | ❌ No |
| **Expressions** | ✅ Yes | ✅ Yes | ❌ No |
| **Multiple Statements** | ✅ Yes | ❌ Limited | ✅ Yes |
| **Readability** | Good for complex | Good for simple | Good for many cases |

### Important Principles

1. **Input Validation is Critical**
   - Always validate user input
   - Convert types appropriately
   - Handle invalid cases gracefully

2. **Understand Data Types**
   - prompt() returns strings
   - Use Number() or parseInt() for conversion
   - Use isNaN() to check validity

3. **Choose the Right Tool**
   - If-else: ranges, expressions, complex conditions
   - Ternary: simple conditional assignments
   - Switch: exact value matching, menu systems

4. **Break Statements Matter**
   - Required in switch to prevent fall-through
   - Intentional fall-through can be useful but document it

5. **Floating Point Caution**
   - Never use === for floating-point comparisons
   - Use epsilon comparison or work with integers
   - Be especially careful with money calculations

### Problem-Solving Patterns

**Pattern 1: Range-Based Decisions (Discount, Bill Tiers)**
```javascript
if (value <= threshold1) {
  // Range 1
} else if (value <= threshold2) {
  // Range 2
} else {
  // Range 3
}
```

**Pattern 2: Cumulative Calculation (Electricity Bill)**
```javascript
// Bottom-up approach
if (value > tier3) {
  total += (value - tier3) * rate3;
  value = tier3;
}
if (value > tier2) {
  total += (value - tier2) * rate2;
  value = tier2;
}
// ... continue
```

**Pattern 3: Greedy Algorithm (Denomination)**
```javascript
for each denomination (largest to smallest) {
  count = Math.floor(amount / denomination);
  amount = amount % denomination;
}
```

### Practice Exercises

1. **Grade Calculator:** Input marks, output grade (A/B/C/D/F) and percentage
2. **Leap Year Checker:** Determine if a year is a leap year
3. **Tax Calculator:** Calculate tax based on income slabs
4. **BMI Calculator:** Calculate and categorize BMI (underweight/normal/overweight/obese)
5. **Traffic Light:** Simulate traffic light logic with switch-case
6. **Triangle Type:** Determine if triangle is equilateral, isosceles, or scalene
7. **Palindrome Checker:** Check if a number is a palindrome
8. **Simple Calculator:** Implement +, -, *, / operations using switch

### Common Mistakes to Avoid

❌ Using else without if
❌ Forgetting to convert prompt() input to number
❌ Not validating input with isNaN()
❌ Forgetting break in switch statements
❌ Using == instead of === (unless you have a reason)
❌ Comparing floating-point numbers with ===
❌ Wrong range conditions (e.g., overlapping ranges)
❌ Forgetting Math.floor() when you need integer results

### Quick Reference

```javascript
// Type Conversion
Number(string)
parseInt(string)
parseFloat(string)
+string

// Validation
isNaN(value)
typeof value

// Integer Operations
Math.floor(value)    // Round down
Math.ceil(value)     // Round up
Math.round(value)    // Round to nearest

// Remainder and Division
value % divisor      // Modulus (remainder)
Math.floor(value / divisor)  // Integer division

// Logical Operators
&&  // AND
||  // OR
!   // NOT

// Comparison Operators
===  // Strict equality
!==  // Strict inequality
<, >, <=, >=
```

---

## Resources for Further Learning

- Practice conditional logic problems on coding platforms
- Study the IEEE 754 floating-point standard
- Learn about algorithmic complexity (Big O notation)
- Explore more advanced control flow (loops, functions)
- Study design patterns for decision-making code

---

**Remember:** Practice is key! Work through problems multiple times, try different approaches, and always test edge cases.

**Happy Coding! 🚀**

---

## FAQ

**Q: Can 'else' be used without 'if'?**  
A: No, using else without a preceding if causes a syntax error in JavaScript.

**Q: Why convert prompt input to number?**  
A: Prompt returns input as a string; for numeric comparisons, conversion (e.g., Number()) is essential.

**Q: How to handle invalid inputs?**  
A: Use isNaN() to check if input is not a number and display appropriate error messages.

**Q: When to use switch-case vs if-else?**  
A: Use switch-case for matching exact constant values. Use if-else for ranges or complex expressions.

**Q: What is fall-through in switch-case?**  
A: If break is omitted, subsequent cases execute until a break is found. This is called fall-through.

**Q: Why does 0.1 + 0.2 not equal 0.3?**  
A: Floating-point numbers cannot always be precisely represented in binary, leading to tiny rounding errors.

**Q: Should I always use ===?**  
A: Yes, unless you specifically need type coercion. === checks both type and value, preventing bugs.

**Q: How do I calculate remainders?**  
A: Use the modulus operator (%). Example: 17 % 5 = 2

---

**End of Study Notes**