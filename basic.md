# DSA with JavaScript
## Comprehensive Study Notes

---

## 1. Variable Declaration: var vs let

### Understanding Hoisting

Variables declared with `var` exhibit hoisting behavior, meaning they can be accessed before their declaration in the code. However, they are initialized with `undefined`.

```javascript
console.log(x); // undefined (no error)
var x = 10;
```

In contrast, variables declared with `let` cannot be accessed before their declaration, resulting in a `ReferenceError`:

```javascript
console.log(y); // ReferenceError: Cannot access 'y' before initialization
let y = 20;
```

### Key Differences

- **undefined** is a value that indicates a variable has been declared but not yet assigned
- **ReferenceError** is an error thrown when trying to access a variable that hasn't been declared yet
- **Best Practice:** Always use `let` (or `const`) for safer, more predictable code behavior

### Practical Example

```javascript
let a = 10;
let b = 20;
console.log(a + b); // 30
```

**Note:** While semicolons are recommended for cleaner code, JavaScript can run without them due to automatic semicolon insertion.

---

## 2. Numbers vs Strings: A Critical Distinction

Understanding the difference between numbers and strings is fundamental to avoiding common JavaScript pitfalls.

### Type Identification

- **10** (without quotes) is a number
- **"10"** (with quotes) is a string

### Arithmetic Operations

```javascript
// Number addition
10 + 1 = 11

// String concatenation
"10" + "1" = "101"

// Mixed: number + string = string
12 + "13" = "1213"
```

### Using typeof Operator

To explicitly check variable types, use the `typeof` operator:

```javascript
console.log(typeof 10);    // "number"
console.log(typeof "10");  // "string"
```

**Console Output Colors:** In browser consoles, blue typically indicates a number, while black indicates a string.

### Template Literals

Use template literals for combining text with computed values:

```javascript
console.log(`sum of 10 and 20 is ${10 + 20}`);
// Output: sum of 10 and 20 is 30
```

---

## 3. Type Coercion and Type Casting

**Type coercion** is the automatic conversion of values from one data type to another by the JavaScript engine.

### How Different Operators Handle Types

**The + operator:** Performs concatenation if ANY operand is a string

```javascript
"10" + 1 = "101"  // string concatenation
```

**The -, *, / operators:** Convert strings to numbers automatically

```javascript
"10" - 1 = 9   // string coerced to number
"10" * 2 = 20  // string coerced to number
"10" / 2 = 5   // string coerced to number
```

### Explicit Type Casting

**Type casting** (also called type conversion) is when you explicitly convert one type to another.

#### Converting to Number

```javascript
let str = "123";
let num1 = Number(str);         // 123
let num2 = parseInt(str);       // 123
let num3 = parseFloat("3.14");  // 3.14
let num4 = +str;                // 123 (unary plus)
```

#### Converting to String

```javascript
let num = 123;
let str1 = String(num);      // "123"
let str2 = num.toString();   // "123"
let str3 = "" + num;         // "123"
```

### Handling User Input with prompt()

**⚠️ Critical:** Input from `prompt()` is ALWAYS a string, regardless of what the user types.

```javascript
let age = prompt("What is your age?");
console.log(typeof age); // "string"
```

To perform numeric operations, convert it explicitly:

```javascript
let age = Number(prompt("What is your age?"));
console.log(typeof age); // "number"
```

### Handling Invalid Input: NaN

When `Number()` cannot convert a value, it returns `NaN` (Not a Number):

```javascript
Number("abc")  // NaN
Number("")     // 0
Number("123")  // 123
```

Use `isNaN()` to validate conversions:

```javascript
let input = prompt("Enter a number:");
let num = Number(input);

if (isNaN(num)) {
  console.log("Invalid input!");
} else {
  console.log(`You entered: ${num}`);
}
```

---

## 4. Swapping Variables: Three Methods

Swapping is a fundamental operation in many algorithms. Here are three common approaches:

### Method 1: Using a Temporary Variable

**Pros:** Most readable, works with all data types  
**Cons:** Requires extra memory for temp variable

```javascript
let a = 10, b = 20;
let temp = a;  // temp = 10
a = b;         // a = 20
b = temp;      // b = 10
// Result: a = 20, b = 10
```

### Method 2: Using Arithmetic Operations

**Pros:** No extra variable needed  
**Cons:** Only works with numbers, risk of overflow with large numbers

```javascript
let a = 10, b = 20;
a = a + b;  // a = 30
b = a - b;  // b = 10
a = a - b;  // a = 20
// Result: a = 20, b = 10
```

### Method 3: Array Destructuring (Recommended)

**Pros:** Clean, concise, modern syntax; works with all types  
**Cons:** None (this is the preferred method)

```javascript
let a = 10, b = 20;
[a, b] = [b, a];
// Result: a = 20, b = 10
```

**✅ Best Practice:** Use array destructuring for its clarity and reliability across all data types.

---

## 5. Operators in JavaScript

### Arithmetic Operators

```javascript
+   Addition
-   Subtraction
*   Multiplication
/   Division (always returns float)
%   Modulus (remainder)
```

#### Division Behavior

**Important:** JavaScript always returns floating-point results for division, even with integers:

```javascript
7 / 2 = 3.5  // not 3
```

To get integer division (floor division), use `Math.floor()`:

```javascript
Math.floor(7 / 2) = 3
```

#### Modulus Operator (%)

Returns the remainder after division:

```javascript
4 % 2 = 0  // 4 divided by 2 leaves no remainder
7 % 2 = 1  // 7 divided by 2 leaves remainder 1
10 % 3 = 1 // 10 divided by 3 leaves remainder 1
```

**Use cases:** Extracting digits, checking even/odd, modular arithmetic

#### Extracting Digits from Numbers

Using division and modulus to manipulate digits:

```javascript
let num = 12345;

// Extract last digit
let lastDigit = num % 10;  // 5

// Remove last digit
num = Math.floor(num / 10);  // 1234

// Extract multiple digits
let lastTwoDigits = num % 100;  // Gets last 2 digits
num = Math.floor(num / 100);    // Removes last 2 digits
```

### Relational (Comparison) Operators

```javascript
<    Less than
>    Greater than
<=   Less than or equal to
>=   Greater than or equal to
==   Loose equality (with type coercion)
===  Strict equality (no type coercion)
!=   Loose inequality
!==  Strict inequality
```

#### Equality: == vs ===

**⚠️ Critical Difference:** Always use `===` (strict equality) unless you have a specific reason to use `==`

```javascript
// Loose equality (==) - performs type coercion
5 == "5"    // true (string coerced to number)
0 == false  // true (boolean coerced to number)

// Strict equality (===) - checks type AND value
5 === "5"    // false (different types)
0 === false  // false (different types)
5 === 5      // true (same type and value)
```

### Logical Operators

```javascript
&&  AND - returns true if ALL conditions are true
||  OR  - returns true if ANY condition is true
!   NOT - negates a boolean value
```

#### Short-Circuit Evaluation

Logical operators evaluate from left to right and stop as soon as the result is determined:

```javascript
// AND (&&) - stops at first false
true && true && false && true  // false
// Evaluation stops at 'false', doesn't check last 'true'

// OR (||) - stops at first true
false || false || true || false  // true
// Evaluation stops at 'true', doesn't check last 'false'
```

---

## 6. Increment and Decrement Operators

JavaScript provides two unary operators for incrementing and decrementing values:

### Postfix Increment (a++)

**Behavior:** Returns the current value, THEN increments

```javascript
let a = 10;
let b = a++;
// b = 10 (gets old value)
// a = 11 (incremented after)
```

### Prefix Increment (++a)

**Behavior:** Increments FIRST, then returns the new value

```javascript
let a = 10;
let b = ++a;
// a = 11 (incremented first)
// b = 11 (gets new value)
```

### Decrement Operators

Decrement (--) works identically but subtracts instead of adds:

```javascript
let a = 10;
let b = a--;  // b = 10, a = 9
let c = --a;  // a = 8, c = 8
```

### Boolean Type Coercion

Booleans convert to numbers in arithmetic operations:

```javascript
true  → 1
false → 0

let a = true;
console.log(a++); // Outputs 1
console.log(a);   // Outputs 2
```

---

## 7. Math Library Functions

JavaScript's Math object provides essential mathematical functions for DSA problems.

### Rounding Functions

```javascript
Math.round(x)  // Rounds to nearest integer
Math.round(4.5)  // 5
Math.round(4.4)  // 4

Math.floor(x)  // Rounds DOWN (toward negative infinity)
Math.floor(4.9)  // 4
Math.floor(-4.1) // -5

Math.ceil(x)   // Rounds UP (toward positive infinity)
Math.ceil(4.1)   // 5
Math.ceil(-4.9)  // -4

Math.trunc(x)  // Removes decimal part (no rounding)
Math.trunc(4.9)  // 4
Math.trunc(-4.9) // -4
```

### Power and Root Functions

```javascript
Math.pow(x, y)  // x raised to the power y
Math.pow(2, 3)  // 8 (2³)
Math.pow(5, 2)  // 25 (5²)

Math.sqrt(x)    // Square root of x
Math.sqrt(25)   // 5
Math.sqrt(2)    // 1.414...
```

### Absolute Value and Min/Max

```javascript
Math.abs(x)     // Absolute value (distance from zero)
Math.abs(-5)    // 5
Math.abs(5)     // 5

Math.max(a, b, c, ...)  // Returns largest value
Math.max(5, 10, 3, 8)   // 10

Math.min(a, b, c, ...)  // Returns smallest value
Math.min(5, 10, 3, 8)   // 3
```

### Random Number Generation

```javascript
Math.random()  // Random float: 0 <= x < 1
```

**Important:** `Math.random()` returns a value between 0 (inclusive) and 1 (exclusive)

#### Generating Random Integers in a Range

To generate random integers within a specific range:

```javascript
// Random integer from 0 to max (exclusive)
Math.floor(Math.random() * max)

// Random integer from min to max (inclusive)
Math.floor(Math.random() * (max - min + 1)) + min
```

#### Example: Generating a 4-Digit OTP

```javascript
// Method 1: Scale and add minimum
let otp = Math.floor(Math.random() * 9000) + 1000;
// Generates: 1000 to 9999

// Method 2: Using the range formula
let otp = Math.floor(Math.random() * (9999 - 1000 + 1)) + 1000;
```

### Math Constants

```javascript
Math.PI     // 3.141592653589793
Math.E      // 2.718281828459045 (Euler's number)
```

---

## 8. Practical Problem-Solving Examples

### Example 1: Rectangle Area and Perimeter

```javascript
let length = 10;
let breadth = 5;

// Calculate area
let area = length * breadth;
console.log(`Area: ${area}`); // 50

// Calculate perimeter
let perimeter = 2 * (length + breadth);
console.log(`Perimeter: ${perimeter}`); // 30
```

### Example 2: Triangle Area (Heron's Formula)

When you know all three sides of a triangle, use Heron's formula:

```javascript
let a = 5, b = 6, c = 7;

// Step 1: Calculate semi-perimeter
let s = (a + b + c) / 2;

// Step 2: Apply Heron's formula
let area = Math.sqrt(s * (s - a) * (s - b) * (s - c));

// Handle potential negative values
if (s <= a || s <= b || s <= c) {
  console.log("Invalid triangle sides");
} else {
  console.log(`Area: ${area.toFixed(2)}`);
}
```

**Formula:** Area = √[s(s-a)(s-b)(s-c)], where s = (a+b+c)/2

### Example 3: Circle Circumference

```javascript
let radius = 7;

// Formula: circumference = 2 * π * r
let circumference = 2 * Math.PI * radius;

// Format to 2 decimal places
console.log(`Circumference: ${circumference.toFixed(2)}`);
// Output: Circumference: 43.98
```

---

## 9. Key Takeaways for DSA

### Essential Best Practices

1. **Variable Declaration:** Always use `let` or `const`, never `var`
2. **Type Awareness:** Be conscious of number vs string operations, especially with user input
3. **Equality Checks:** Use `===` (strict equality) to avoid type coercion bugs
4. **Type Conversion:** Always convert `prompt()` input using `Number()` before arithmetic
5. **Swapping:** Use array destructuring `[a, b] = [b, a]` for clean, reliable swaps
6. **Division:** Use `Math.floor()` for integer division; remember JS division always returns floats
7. **Modulus:** Master `%` operator for digit extraction and modular arithmetic
8. **Math Functions:** Familiarize yourself with `Math.floor()`, `Math.ceil()`, `Math.sqrt()`, `Math.pow()`, `Math.random()`

### Common Patterns in DSA

- **Digit Extraction:** `num % 10` (last digit), `Math.floor(num / 10)` (remove last)
- **Integer Division:** `Math.floor(a / b)`
- **Random Range:** `Math.floor(Math.random() * (max - min + 1)) + min`
- **Even/Odd Check:** `num % 2 === 0`
- **Type Checking:** `typeof variable`, `isNaN()`

### Quick Reference Table

| Operation | Syntax |
|-----------|--------|
| String to Number | `Number(str)`, `+str`, `parseInt(str)` |
| Number to String | `String(num)`, `num.toString()`, `"" + num` |
| Swap Variables | `[a, b] = [b, a]` |
| Integer Division | `Math.floor(a / b)` |
| Last Digit | `num % 10` |
| Remove Last Digit | `Math.floor(num / 10)` |
| Random Integer (0-n) | `Math.floor(Math.random() * (n + 1))` |
| Check Even/Odd | `num % 2 === 0` (even), `num % 2 === 1` (odd) |

---

## Remember

**These fundamentals form the foundation for all DSA problems in JavaScript. Master them well!**

---

### Additional Tips for DSA Success

1. **Practice type conversion** - Many bugs come from mixing strings and numbers
2. **Use strict equality** - Avoid subtle bugs from type coercion
3. **Understand operator precedence** - Know which operations happen first
4. **Master Math functions** - They're essential for algorithm implementation
5. **Test edge cases** - Always check with 0, negative numbers, and large values
6. **Use console.log strategically** - Debug by checking types and values at each step
7. **Write clean code** - Use meaningful variable names and consistent formatting
8. **Comment your logic** - Especially for complex calculations or algorithms

### Resources for Further Learning

- Practice digit manipulation problems
- Study number theory basics (prime numbers, GCD, LCM)
- Learn about JavaScript's quirks with floating-point arithmetic
- Understand when to use Math functions vs operators
- Practice converting between different number bases

---

**Happy Coding! 🚀**