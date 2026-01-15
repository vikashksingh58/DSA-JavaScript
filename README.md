# DSA-JavaScript

# Type Coercion
This is when JavaScript automatically converts one data type to another. It happens implicitly during operations:
```
// String coercion
console.log("5" + 3);        // "53" (number 3 becomes string)
console.log("5" - 3);        // 2 (string "5" becomes number)

// Boolean coercion
console.log(5 == "5");       // true (loose equality coerces types)
console.log(0 == false);     // true
console.log("" == false);    // true

// Truthy/Falsy
if ("hello") { }  // strings are truthy
if (0) { }        // 0 is falsy
```
# Type Casting
This is when you explicitly convert one type to another:
javascript
```
// To Number
let str = "123";
let num1 = Number(str);      // 123
let num2 = parseInt(str);    // 123
let num3 = parseFloat("3.14"); // 3.14
let num4 = +str;             // 123 (unary plus)

// To String
let num = 123;
let str1 = String(num);      // "123"
let str2 = num.toString();   // "123"
let str3 = "" + num;         // "123"

// To Boolean
let bool1 = Boolean(1);      // true
let bool2 = Boolean(0);      // false
let bool3 = !!"hello";       // true (double negation)
```

# Swapping
Several techniques to swap two variables:

```
let a = 5, b = 10;

// Method 1: Using temporary variable (most readable)
let temp = a;
a = b;
b = temp;
// a = 10, b = 5

// Method 2: Array destructuring (modern, clean)
[a, b] = [b, a];

// Method 3: Arithmetic (works only with numbers)
a = a + b;  // a = 15
b = a - b;  // b = 5
a = a - b;  // a = 10

// Method 4: XOR bitwise (works only with integers)
a = a ^ b;
b = a ^ b;
a = a ^ b;
```