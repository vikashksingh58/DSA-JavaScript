# Mathematical Algorithms Study Notes
**DSA Series - Share and Coding School**

---

## Table of Contents
1. [GCD (Greatest Common Divisor)](#gcd-greatest-common-divisor)
2. [Factors of a Number](#factors-of-a-number)
3. [Prime Numbers & Sieve of Eratosthenes](#prime-numbers--sieve-of-eratosthenes)
4. [Power Function (Fast Exponentiation)](#power-function-fast-exponentiation)
5. [Algorithm Comparison](#algorithm-comparison)

---

## GCD (Greatest Common Divisor)

### Definition
**GCD** (also called **HCF** - Highest Common Factor) is the highest factor common to two numbers.

### Understanding Factors
- **Factor**: An integer that divides a number completely (remainder = 0)
- **Range**: Factors lie between 1 and the number itself
- **Example**: Factors of 10 are 1, 2, 5, 10

### Example Problem
Find GCD of 20 and 30:
- Factors of 20: 1, 2, 4, 5, 10, 20
- Factors of 30: 1, 2, 3, 5, 6, 10, 15, 30
- Common factors: 1, 2, 5, 10
- **GCD = 10** (highest common factor)

---

### Approach 1: Brute Force Method

#### Algorithm
```
Loop from min(a, b) down to 1
For each i:
    If both a and b are divisible by i:
        Return i (this is GCD)
```

#### Code Implementation
```javascript
function gcdBruteForce(a, b) {
    let minNum = Math.min(a, b);
    
    for (let i = minNum; i >= 1; i--) {
        if (a % i === 0 && b % i === 0) {
            return i;  // First match is highest
        }
    }
    return 1;
}
```

#### Complexity Analysis
- **Time Complexity**: O(min(a, b))
- **Space Complexity**: O(1)
- **Issue**: Inefficient for large numbers

---

### Approach 2: Euclidean Algorithm (Subtraction)

#### Core Idea
Repeatedly subtract the smaller number from the larger until both become equal.

#### Algorithm Steps
```
While a ≠ b:
    If a > b:
        a = a - b
    Else:
        b = b - a
Return a (or b, they're equal)
```

#### Example: GCD(32, 20)
```
Step 1: 32 - 20 = 12  → (12, 20)
Step 2: 20 - 12 = 8   → (12, 8)
Step 3: 12 - 8 = 4    → (4, 8)
Step 4: 8 - 4 = 4     → (4, 4)
Result: GCD = 4
```

#### Code Implementation
```javascript
function gcdSubtraction(a, b) {
    while (a !== b) {
        if (a > b) {
            a = a - b;
        } else {
            b = b - a;
        }
    }
    return a;
}
```

#### Complexity Analysis
- **Time Complexity**: O(max(a, b)) - worst case
- **Space Complexity**: O(1)
- **Issue**: Still inefficient for large numbers with big differences

---

### Approach 3: Euclidean Algorithm (Modulus) ⭐ BEST

#### Core Formula
```
gcd(a, b) = gcd(b, a % b)
Base case: when b = 0, gcd = a
```

#### Why Modulus is Better
- Replaces multiple subtractions with one modulus operation
- Reduces problem size drastically faster
- Much more efficient

#### Algorithm Steps
```
While b ≠ 0:
    temp = b
    b = a % b
    a = temp
Return a
```

#### Example: GCD(48, 18)
```
Step 1: gcd(48, 18) → 48 % 18 = 12 → gcd(18, 12)
Step 2: gcd(18, 12) → 18 % 12 = 6  → gcd(12, 6)
Step 3: gcd(12, 6)  → 12 % 6 = 0   → gcd(6, 0)
Step 4: b = 0, so GCD = 6
```

#### Iterative Implementation
```javascript
function gcdIterative(a, b) {
    while (b !== 0) {
        let temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}
```

#### Recursive Implementation
```javascript
function gcdRecursive(a, b) {
    if (b === 0) return a;  // Base case
    return gcdRecursive(b, a % b);
}
```

#### Complexity Analysis
- **Time Complexity**: O(log(min(a, b)))
- **Space Complexity**: 
  - Iterative: O(1)
  - Recursive: O(log(min(a, b))) - recursion stack
- **Why Logarithmic**: Every two iterations reduce the smaller number by at least half

---

## Factors of a Number

### Naive Approach
Check all numbers from 1 to n for divisibility.

```javascript
function findFactorsNaive(n) {
    let factors = [];
    for (let i = 1; i <= n; i++) {
        if (n % i === 0) {
            factors.push(i);
        }
    }
    return factors;
}
```

**Time Complexity**: O(n)

---

### Optimized Approach Using √n ⭐

#### Key Insight
**Factors appear in pairs**: If `i` is a factor, then `n/i` is also a factor.

#### Algorithm
```
Loop from 1 to √n:
    If i divides n:
        Add i to factors
        If i ≠ n/i:  // Avoid duplicate for perfect squares
            Add n/i to factors
```

#### Example: Factors of 100
```
√100 = 10

Check 1: 1 and 100/1=100 → factors: 1, 100
Check 2: 2 and 100/2=50  → factors: 2, 50
Check 4: 4 and 100/4=25  → factors: 4, 25
Check 5: 5 and 100/5=20  → factors: 5, 20
Check 10: 10 and 100/10=10 → factor: 10 (same, add once)

All factors: 1, 2, 4, 5, 10, 20, 25, 50, 100
```

#### Code Implementation
```javascript
function findFactorsOptimized(n) {
    let factors = [];
    
    for (let i = 1; i <= Math.sqrt(n); i++) {
        if (n % i === 0) {
            factors.push(i);
            
            // Add pair factor if different
            if (i !== n / i) {
                factors.push(n / i);
            }
        }
    }
    
    return factors.sort((a, b) => a - b);
}
```

#### Complexity Analysis
- **Time Complexity**: O(√n)
- **Space Complexity**: O(k) where k = number of factors

#### Comparison Table

| n | Factors Count | Naive Checks | Optimized Checks |
|---|---------------|--------------|------------------|
| 100 | 9 | 100 | 10 (√100) |
| 30 | 8 | 30 | ~5 (√30) |
| 1000 | 16 | 1000 | ~31 (√1000) |

---

## Prime Numbers & Sieve of Eratosthenes

### Prime Number Definition
A number greater than 1 that has exactly two factors: 1 and itself.

**Examples**: 2, 3, 5, 7, 11, 13, 17, 19, 23, 29...

### Problem: Count Primes from 1 to n

---

### Approach 1: Brute Force (Check Each Number)

#### Algorithm
```
For each number from 2 to n:
    Check if prime (test divisibility from 2 to √num)
    If prime, increment count
```

#### Code
```javascript
function isPrime(num) {
    if (num <= 1) return false;
    for (let i = 2; i <= Math.sqrt(num); i++) {
        if (num % i === 0) return false;
    }
    return true;
}

function countPrimesBruteForce(n) {
    let count = 0;
    for (let i = 2; i <= n; i++) {
        if (isPrime(i)) count++;
    }
    return count;
}
```

#### Complexity
- **Time Complexity**: O(n × √n)
- **Issue**: TLE (Time Limit Exceeded) for large n

---

### Approach 2: Sieve of Eratosthenes ⭐ OPTIMAL

#### Core Idea
Mark multiples of each prime as non-prime, leaving only primes unmarked.

#### Algorithm Steps
```
1. Create boolean array of size n+1, initialize all to true
2. Mark arr[0] = false, arr[1] = false
3. For i = 2 to √n:
     If arr[i] is true (i is prime):
         Mark all multiples of i starting from i² as false
4. Count remaining true values
```

#### Why Start from i²?
All smaller multiples of i (like 2i, 3i, ..., (i-1)i) have already been marked by smaller primes.

#### Visual Example: n = 30

**Initial Array** (all true except 0, 1):
```
Index: 0  1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30
Value: F  F  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T  T
```

**Step 1**: i = 2 (prime), mark multiples from 2² = 4
```
Mark 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30 as false
```

**Step 2**: i = 3 (prime), mark multiples from 3² = 9
```
Mark 9, 12, 15, 18, 21, 24, 27, 30 as false
```

**Step 3**: i = 5 (prime), mark multiples from 5² = 25
```
Mark 25, 30 as false
```

**√30 ≈ 5.5**, so stop here.

**Final Primes**: 2, 3, 5, 7, 11, 13, 17, 19, 23, 29

#### Code Implementation
```javascript
function countPrimesSieve(n) {
    if (n <= 2) return 0;
    
    // Create array and initialize all to true
    let arr = new Array(n + 1).fill(true);
    arr[0] = false;
    arr[1] = false;
    
    // Sieve algorithm
    for (let i = 2; i <= Math.sqrt(n); i++) {
        if (arr[i]) {  // i is prime
            // Mark multiples starting from i²
            for (let j = i * i; j <= n; j += i) {
                arr[j] = false;
            }
        }
    }
    
    // Count primes
    let count = 0;
    for (let i = 2; i <= n; i++) {
        if (arr[i]) count++;
    }
    
    return count;
}
```

#### Complexity Analysis
- **Time Complexity**: O(n log log n) ≈ O(n log n) for practical purposes
- **Space Complexity**: O(n)
- **Trade-off**: Uses extra space for dramatic time improvement

#### Efficiency Demonstration

| n | Brute Force Time | Sieve Time |
|---|------------------|------------|
| 100 | ~1000 ops | ~200 ops |
| 1000 | ~31,000 ops | ~3000 ops |
| 10,000 | ~1,000,000 ops | ~40,000 ops |

---

## Power Function (Fast Exponentiation)

### Problem: Compute x^n
**LeetCode 50**: Implement pow(x, n)

---

### Approach 1: Brute Force

#### Algorithm
```
result = 1
Multiply x by itself n times
```

#### Code
```javascript
function powBruteForce(x, n) {
    if (n < 0) return 1 / powBruteForce(x, -n);
    
    let result = 1;
    for (let i = 0; i < n; i++) {
        result *= x;
    }
    return result;
}
```

#### Complexity
- **Time Complexity**: O(n)
- **Issue**: Fails for large n (e.g., n = 2³¹)

---

### Approach 2: Exponentiation by Squaring ⭐ OPTIMAL

#### Core Idea: Divide and Conquer
```
x^n = (x^(n/2))² when n is even
x^n = (x^(n/2))² × x when n is odd
x^0 = 1 (base case)
```

#### Why This Works
Instead of n multiplications, we do log(n) recursive calls by halving the exponent each time.

#### Example: 2^10
```
2^10 = (2^5)²
2^5 = (2^2)² × 2
2^2 = (2^1)²
2^1 = (2^0)² × 2
2^0 = 1

Working backwards:
2^1 = 1² × 2 = 2
2^2 = 2² = 4
2^5 = 4² × 2 = 32
2^10 = 32² = 1024
```

#### Recursive Implementation
```javascript
function myPow(x, n) {
    // Handle negative exponent
    if (n < 0) {
        return 1 / myPow(x, -n);
    }
    
    // Base case
    if (n === 0) return 1;
    
    // Recursive case
    let half = myPow(x, Math.floor(n / 2));
    
    if (n % 2 === 0) {
        // Even exponent
        return half * half;
    } else {
        // Odd exponent
        return half * half * x;
    }
}
```

#### Iterative Implementation
```javascript
function myPowIterative(x, n) {
    if (n < 0) {
        x = 1 / x;
        n = -n;
    }
    
    let result = 1;
    let base = x;
    
    while (n > 0) {
        if (n % 2 === 1) {
            result *= base;
        }
        base *= base;
        n = Math.floor(n / 2);
    }
    
    return result;
}
```

#### Handling Negative Powers
```
x^(-n) = 1 / (x^n)

Example: 2^(-3) = 1 / (2^3) = 1/8 = 0.125
```

#### Complexity Analysis
- **Time Complexity**: O(log n)
- **Space Complexity**: 
  - Recursive: O(log n) - call stack
  - Iterative: O(1)

#### Comparison

| n | Brute Force Ops | Fast Exponentiation Ops |
|---|-----------------|------------------------|
| 10 | 10 | 4 |
| 100 | 100 | 7 |
| 1000 | 1000 | 10 |
| 2³¹ | 2,147,483,648 | 31 |

---

## Algorithm Comparison Table

| Algorithm | Description | Time Complexity | Space Complexity | Use Case |
|-----------|-------------|-----------------|------------------|----------|
| **GCD Brute Force** | Check all factors | O(min(a,b)) | O(1) | Small numbers only |
| **GCD Euclidean (mod)** ⭐ | Modulus operation | O(log(min(a,b))) | O(1) | Best for any size |
| **Factors Naive** | Check 1 to n | O(n) | O(1) | Educational |
| **Factors √n Method** ⭐ | Check 1 to √n | O(√n) | O(1) | Practical use |
| **Prime Check Naive** | Check divisibility | O(√n) | O(1) | Single number |
| **Sieve of Eratosthenes** ⭐ | Mark multiples | O(n log log n) | O(n) | Multiple primes |
| **Power Brute Force** | Repeated multiplication | O(n) | O(1) | Small exponents |
| **Exponentiation by Squaring** ⭐ | Divide and conquer | O(log n) | O(log n) or O(1) | Large exponents |

---

## Key Insights & Takeaways

### 1. Optimization is Critical
- Naive solutions work for small inputs but fail for large data
- Understanding time complexity helps choose the right approach
- Often there's a mathematical property that enables optimization

### 2. Common Optimization Patterns

| Pattern | Improvement | Examples |
|---------|-------------|----------|
| **Use √n instead of n** | O(n) → O(√n) | Factors, Prime checking |
| **Use modulus instead of subtraction** | O(n) → O(log n) | GCD |
| **Precompute results** | Multiple O(√n) → One O(n) | Sieve of Eratosthenes |
| **Divide and conquer** | O(n) → O(log n) | Power function |

### 3. Space-Time Trade-offs
- **Sieve**: Uses O(n) space to improve time from O(n√n) to O(n log log n)
- **GCD**: Iterative version uses O(1) space vs recursive O(log n)
- Choose based on constraints

### 4. Mathematical Properties Drive Algorithms
- **Factors come in pairs** → Check only up to √n
- **Euclidean principle** → GCD(a,b) = GCD(b, a%b)
- **Multiples of primes aren't prime** → Sieve marks them
- **Exponent halving** → Fast power computation

---

## Practice Problems

### Beginner
1. ✅ Find GCD of two numbers (all methods)
2. ✅ List all factors of a number
3. ✅ Check if a number is prime
4. ✅ Count primes up to n
5. ✅ Compute x^n

### Intermediate
6. Find LCM using GCD: `LCM(a,b) = (a×b) / GCD(a,b)`
7. Count number of factors
8. Find all prime factors of a number
9. Implement modular exponentiation: `(x^n) % m`
10. Find nth prime number

### Advanced
11. Prime factorization with powers
12. Segmented Sieve (for range of primes)
13. Binary exponentiation for matrix multiplication
14. GCD of array of numbers
15. Euler's Totient Function

---

## Common Mistakes to Avoid

### 1. GCD Mistakes
```javascript
// ❌ WRONG - Infinite loop if b > a initially
function gcd(a, b) {
    while (a !== 0) {
        let temp = a;
        a = b % a;
        b = temp;
    }
    return b;
}

// ✅ CORRECT - Works regardless of order
function gcd(a, b) {
    while (b !== 0) {
        let temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}
```

### 2. Factor Finding Mistakes
```javascript
// ❌ WRONG - Adds duplicate for perfect squares
for (let i = 1; i <= Math.sqrt(n); i++) {
    if (n % i === 0) {
        factors.push(i);
        factors.push(n / i);  // Duplicates when i = n/i
    }
}

// ✅ CORRECT - Check for duplicate
for (let i = 1; i <= Math.sqrt(n); i++) {
    if (n % i === 0) {
        factors.push(i);
        if (i !== n / i) {  // Avoid duplicate
            factors.push(n / i);
        }
    }
}
```

### 3. Sieve Mistakes
```javascript
// ❌ WRONG - Inefficient, starts from 2i
for (let j = 2 * i; j <= n; j += i) {
    arr[j] = false;
}

// ✅ CORRECT - Starts from i² (smaller multiples already marked)
for (let j = i * i; j <= n; j += i) {
    arr[j] = false;
}
```

### 4. Power Function Mistakes
```javascript
// ❌ WRONG - Doesn't handle negative exponents
function myPow(x, n) {
    if (n === 0) return 1;
    let half = myPow(x, n / 2);
    return (n % 2 === 0) ? half * half : half * half * x;
}

// ✅ CORRECT - Handles negative exponents
function myPow(x, n) {
    if (n < 0) return 1 / myPow(x, -n);
    if (n === 0) return 1;
    let half = myPow(x, Math.floor(n / 2));
    return (n % 2 === 0) ? half * half : half * half * x;
}
```

---

## Study Tips

### Understanding the Concepts
1. **Draw diagrams** for each algorithm
2. **Trace examples** step by step
3. **Compare methods** side by side
4. **Analyze complexity** for each approach

### Practice Strategy
1. Implement brute force first
2. Identify bottleneck
3. Apply optimization technique
4. Test with edge cases
5. Verify complexity improvement

### Memory Aids

**"FOGS" for Optimization**:
- **F**actors: Use √n
- **O**perations: Use modulus over subtraction
- **G**CD: Euclidean algorithm
- **S**ieve: For multiple primes

---

## Interview Preparation

### Common Questions
1. Explain Euclidean algorithm and its complexity
2. Why is Sieve better than checking each number?
3. How does exponentiation by squaring work?
4. What's the difference between time and space complexity?
5. When would you use brute force vs optimized solution?

### Problem-Solving Template
```
1. Understand the problem
2. Consider brute force
3. Identify inefficiency
4. Apply mathematical property
5. Optimize using pattern
6. Analyze complexity
7. Handle edge cases
8. Test implementation
```

---

## Lecture Timeline

| Time | Topic |
|------|-------|
| 00:00 - 02:40 | Introduction, Factors concept |
| 02:40 - 07:30 | GCD brute force method |
| 07:30 - 09:00 | Euclidean algorithm (subtraction) |
| 09:00 - 29:15 | Euclidean algorithm (modulus) & complexity |
| 29:15 - 39:51 | Factors using √n optimization |
| 39:51 - 57:12 | Sieve of Eratosthenes |
| 57:12 - 01:12:01 | Power function & fast exponentiation |

---

## Quick Reference

### GCD Formula
```
gcd(a, b) = gcd(b, a % b)
Base: gcd(a, 0) = a
```

### Prime Sieve Pseudocode
```
arr[0..n] = true
arr[0] = arr[1] = false
for i = 2 to √n:
    if arr[i]:
        for j = i² to n step i:
            arr[j] = false
```

### Fast Power Formula
```
x^n = (x^(n/2))²     if n even
x^n = (x^(n/2))² × x if n odd
x^0 = 1
```

---

## Additional Resources

### Practice Platforms
- **LeetCode**: Problems 50 (Pow), 204 (Count Primes)
- **HackerRank**: Mathematics section
- **Project Euler**: Mathematical problems

### Visualization Tools
- Sieve visualizer
- GCD step-by-step calculators
- Factor trees

---

**Remember**: Mathematical intuition + Algorithmic thinking = Efficient solutions! 🚀