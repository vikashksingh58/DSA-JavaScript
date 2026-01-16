# Koko Eating Bananas - Complete Study Guide

## 📚 Problem Overview

### LeetCode #875: Koko Eating Bananas

**Difficulty:** Medium  
**Pattern:** Binary Search on Answer Space  
**Similar To:** Allocate Minimum Pages, Capacity to Ship Packages

---

## 🍌 Problem Statement

### The Story

Koko loves eating bananas. There are `n` piles of bananas, where the `i-th` pile has `piles[i]` bananas. 

**Situation:**
- The security guards have left and will return in `h` hours
- Koko wants to eat **all the bananas** before the guards return
- Koko can decide her eating **speed** `k` (bananas per hour)

**Rules:**
1. Each hour, Koko chooses **one pile** and eats `k` bananas from it
2. If the pile has **fewer than k** bananas, she eats all of them and **waits** for the next hour (cannot eat from another pile)
3. Koko prefers to eat **slowly** (minimize eating speed)

**Goal:** Return the **minimum integer k** such that Koko can eat all bananas within `h` hours.

---

## 🎯 Understanding the Problem

### Example 1: Basic Case

**Input:**
```
piles = [3, 6, 7, 11]
h = 8 hours
```

**Question:** What's the minimum eating speed to finish all bananas in 8 hours?

**Let's test different speeds:**

**Speed k = 1 banana/hour:**
```
Pile [3]:  takes 3 hours  (3÷1 = 3)
Pile [6]:  takes 6 hours  (6÷1 = 6)
Pile [7]:  takes 7 hours  (7÷1 = 7)
Pile [11]: takes 11 hours (11÷1 = 11)
Total: 3 + 6 + 7 + 11 = 27 hours ❌ (exceeds 8 hours)
```

**Speed k = 4 bananas/hour:**
```
Pile [3]:  takes 1 hour  (3÷4 = 0.75 → ceil = 1)
Pile [6]:  takes 2 hours (6÷4 = 1.5 → ceil = 2)
Pile [7]:  takes 2 hours (7÷4 = 1.75 → ceil = 2)
Pile [11]: takes 3 hours (11÷4 = 2.75 → ceil = 3)
Total: 1 + 2 + 2 + 3 = 8 hours ✓ (exactly 8 hours)
```

**Speed k = 5 bananas/hour:**
```
Pile [3]:  takes 1 hour  (3÷5 = 0.6 → ceil = 1)
Pile [6]:  takes 2 hours (6÷5 = 1.2 → ceil = 2)
Pile [7]:  takes 2 hours (7÷5 = 1.4 → ceil = 2)
Pile [11]: takes 3 hours (11÷5 = 2.2 → ceil = 3)
Total: 1 + 2 + 2 + 3 = 8 hours ✓
```

**Speed k = 11 bananas/hour:**
```
Pile [3]:  takes 1 hour  (3÷11 = 0.27 → ceil = 1)
Pile [6]:  takes 1 hour  (6÷11 = 0.54 → ceil = 1)
Pile [7]:  takes 1 hour  (7÷11 = 0.63 → ceil = 1)
Pile [11]: takes 1 hour  (11÷11 = 1)
Total: 1 + 1 + 1 + 1 = 4 hours ✓ (finishes early)
```

**Answer:** k = 4 (minimum speed that works)

---

### Example 2: More Piles

**Input:**
```
piles = [30, 11, 23, 4, 20]
h = 5 hours
```

**Analysis:**
- We have 5 piles and 5 hours
- Best case: eat one pile per hour
- This requires speed = max(piles) = 30 bananas/hour

**Speed k = 30:**
```
Pile [30]: 1 hour
Pile [11]: 1 hour
Pile [23]: 1 hour
Pile [4]:  1 hour
Pile [20]: 1 hour
Total: 5 hours ✓
```

**Can we go slower? Try k = 29:**
```
Pile [30]: 2 hours (30÷29 = 1.03 → ceil = 2) ❌
Already exceeds 5 hours with first pile!
```

**Answer:** k = 30

---

### Example 3: Extra Time Available

**Input:**
```
piles = [30, 11, 23, 4, 20]
h = 6 hours
```

**Now we have 6 hours for 5 piles (1 extra hour)**

**Try k = 23:**
```
Pile [30]: 2 hours (30÷23 = 1.3 → ceil = 2)
Pile [11]: 1 hour  (11÷23 = 0.47 → ceil = 1)
Pile [23]: 1 hour  (23÷23 = 1)
Pile [4]:  1 hour  (4÷23 = 0.17 → ceil = 1)
Pile [20]: 1 hour  (20÷23 = 0.86 → ceil = 1)
Total: 2 + 1 + 1 + 1 + 1 = 6 hours ✓
```

**Answer:** k = 23

---

## 💡 Key Insights

### Why Binary Search?

**Pattern Recognition:**
1. **Minimize the maximum** (minimum eating speed)
2. **Fixed constraint** (h hours available)
3. **Feasibility check possible** (can we finish in h hours at speed k?)

**The Answer Space:**
- **Minimum possible speed:** 1 banana/hour (Koko must eat at least 1)
- **Maximum possible speed:** max(piles) (eating faster than biggest pile is wasteful)
- **Answer lies somewhere in range [1, max(piles)]**

**Why not try all speeds?**
- Range could be huge (up to 10^9)
- Testing each speed: O(n × max(piles)) → Too slow!
- Binary search: O(n × log(max(piles))) → Efficient! ✓

---

### How Time Calculation Works

**For each pile at speed k:**

```javascript
hours = Math.ceil(pile / k)
```

**Understanding ceil (ceiling function):**
```
pile = 7, k = 3
7 ÷ 3 = 2.33...
ceil(2.33) = 3 hours

Hour 1: eat 3 bananas (4 left)
Hour 2: eat 3 bananas (1 left)
Hour 3: eat 1 banana (0 left, wait remainder)
```

**Alternative calculation (without Math.ceil):**
```javascript
// If pile divides evenly
if (pile % k === 0) {
    hours = pile / k;
} else {
    hours = Math.floor(pile / k) + 1;
}
```

**Example:**
```
pile = 10, k = 3
10 % 3 = 1 (not evenly divisible)
hours = Math.floor(10/3) + 1 = 3 + 1 = 4 ✓

pile = 9, k = 3
9 % 3 = 0 (evenly divisible)
hours = 9/3 = 3 ✓
```

---

## 🔍 The Algorithm

### Step-by-Step Approach

**Step 1: Define Search Space**
```javascript
let low = 1;                    // Minimum possible speed
let high = Math.max(...piles);  // Maximum possible speed
```

**Step 2: Binary Search**
```javascript
while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    
    if (canFinish(piles, mid, h)) {
        // Can finish at this speed, try slower
        high = mid - 1;
    } else {
        // Too slow, need faster speed
        low = mid + 1;
    }
}

return low;  // Minimum valid speed
```

**Step 3: Feasibility Check**
```javascript
function canFinish(piles, speed, h) {
    let totalHours = 0;
    
    for (let pile of piles) {
        totalHours += Math.ceil(pile / speed);
        
        // Early termination optimization
        if (totalHours > h) {
            return false;
        }
    }
    
    return totalHours <= h;
}
```

---

## 💻 Complete Implementation

### JavaScript Solution

```javascript
/**
 * @param {number[]} piles
 * @param {number} h
 * @return {number}
 */
function minEatingSpeed(piles, h) {
    // Define search space
    let low = 1;
    let high = Math.max(...piles);
    
    // Binary search for minimum speed
    while (low < high) {
        let mid = Math.floor((low + high) / 2);
        
        if (canFinish(piles, mid, h)) {
            // Can finish, try slower speed
            high = mid;
        } else {
            // Too slow, need faster speed
            low = mid + 1;
        }
    }
    
    return low;
}

/**
 * Check if Koko can finish all bananas at given speed within h hours
 */
function canFinish(piles, speed, h) {
    let totalHours = 0;
    
    for (let pile of piles) {
        // Calculate hours needed for this pile
        totalHours += Math.ceil(pile / speed);
        
        // Early exit if already exceeds h
        if (totalHours > h) {
            return false;
        }
    }
    
    return totalHours <= h;
}

// Alternative: Using low <= high pattern
function minEatingSpeed_v2(piles, h) {
    let low = 1;
    let high = Math.max(...piles);
    let answer = high;
    
    while (low <= high) {
        let mid = Math.floor((low + high) / 2);
        
        if (canFinish(piles, mid, h)) {
            answer = mid;
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }
    
    return answer;
}

// Test cases
console.log(minEatingSpeed([3, 6, 7, 11], 8));           // Output: 4
console.log(minEatingSpeed([30, 11, 23, 4, 20], 5));     // Output: 30
console.log(minEatingSpeed([30, 11, 23, 4, 20], 6));     // Output: 23
```

---

### Python Solution

```python
import math

def minEatingSpeed(piles, h):
    """
    Find minimum eating speed to finish all bananas in h hours
    """
    low = 1
    high = max(piles)
    
    while low < high:
        mid = (low + high) // 2
        
        if can_finish(piles, mid, h):
            high = mid
        else:
            low = mid + 1
    
    return low

def can_finish(piles, speed, h):
    """
    Check if we can finish all piles at given speed within h hours
    """
    total_hours = 0
    
    for pile in piles:
        total_hours += math.ceil(pile / speed)
        
        if total_hours > h:
            return False
    
    return total_hours <= h

# Alternative: Without math.ceil
def can_finish_no_ceil(piles, speed, h):
    total_hours = 0
    
    for pile in piles:
        hours = pile // speed
        if pile % speed != 0:
            hours += 1
        total_hours += hours
        
        if total_hours > h:
            return False
    
    return True

# Test
print(minEatingSpeed([3, 6, 7, 11], 8))        # 4
print(minEatingSpeed([30, 11, 23, 4, 20], 5))  # 30
```

---

## 🔬 Detailed Walkthrough

### Example: piles = [3, 6, 7, 11], h = 8

**Initial Setup:**
```
low = 1
high = 11 (max of piles)
```

**Iteration 1:**
```
mid = (1 + 11) / 2 = 6

Can finish at speed 6?
  Pile 3:  ceil(3/6) = 1 hour
  Pile 6:  ceil(6/6) = 1 hour
  Pile 7:  ceil(7/6) = 2 hours
  Pile 11: ceil(11/6) = 2 hours
  Total: 1 + 1 + 2 + 2 = 6 hours ≤ 8 ✓

Can finish! Try slower speed.
high = 6 - 1 = 5
```

**Iteration 2:**
```
low = 1, high = 5
mid = (1 + 5) / 2 = 3

Can finish at speed 3?
  Pile 3:  ceil(3/3) = 1 hour
  Pile 6:  ceil(6/3) = 2 hours
  Pile 7:  ceil(7/3) = 3 hours
  Pile 11: ceil(11/3) = 4 hours
  Total: 1 + 2 + 3 + 4 = 10 hours > 8 ✗

Cannot finish! Need faster speed.
low = 3 + 1 = 4
```

**Iteration 3:**
```
low = 4, high = 5
mid = (4 + 5) / 2 = 4

Can finish at speed 4?
  Pile 3:  ceil(3/4) = 1 hour
  Pile 6:  ceil(6/4) = 2 hours
  Pile 7:  ceil(7/4) = 2 hours
  Pile 11: ceil(11/4) = 3 hours
  Total: 1 + 2 + 2 + 3 = 8 hours ≤ 8 ✓

Can finish! Try slower speed.
high = 4 - 1 = 3
```

**Loop ends:** low > high (4 > 3)

**Answer:** 4 bananas/hour

**Step Table:**

| Iteration | low | high | mid | Hours at mid | Valid? | Action |
|-----------|-----|------|-----|--------------|--------|--------|
| 1 | 1 | 11 | 6 | 6 ≤ 8 | ✓ | high = 5 |
| 2 | 1 | 5 | 3 | 10 > 8 | ✗ | low = 4 |
| 3 | 4 | 5 | 4 | 8 ≤ 8 | ✓ | high = 3 |
| Done | 4 | 3 | - | - | - | Return 4 |

---

## 📈 Complexity Analysis

### Time Complexity: O(n × log m)

**Breakdown:**
- Binary search iterations: O(log m) where m = max(piles)
- Each iteration validates in O(n) where n = number of piles
- Total: O(n × log m)

**Example:**
- piles = [3, 6, 7, 11] → n = 4
- max(piles) = 11 → log₂(11) ≈ 4 iterations
- Total operations: 4 × 4 = 16 operations

**Compared to Brute Force:**
- Brute force: Try every speed from 1 to max(piles) → O(n × m)
- For m = 10^9: Brute force = 10^9 operations vs Binary search ≈ 30 operations!

### Space Complexity: O(1)

**Reasoning:**
- Only using constant extra variables (low, high, mid, totalHours)
- No recursion
- No additional data structures
- In-place calculation

---

## 🎓 Edge Cases

### 1. Single Pile
```javascript
piles = [1000000000], h = 2
// Must eat all in 1 pile over 2 hours
// Speed = ceil(1000000000 / 2) = 500000000
```

### 2. Each Pile Needs Exact 1 Hour
```javascript
piles = [30, 11, 23, 4, 20], h = 5
// 5 piles, 5 hours → need max(piles) speed
// Answer: 30
```

### 3. Lots of Extra Time
```javascript
piles = [3, 6, 7, 11], h = 100
// So much time, can eat very slowly
// Answer: 1 (minimum possible speed)
```

### 4. All Piles Same Size
```javascript
piles = [5, 5, 5, 5], h = 8
// Each pile takes ceil(5/k) hours
// Need 4 × ceil(5/k) ≤ 8
// ceil(5/k) ≤ 2
// k ≥ 3
// Answer: 3
```

### 5. Large Numbers
```javascript
piles = [1000000000], h = 1000000000
// Can eat extremely slowly
// Answer: 1
```

---

## 🧠 Pattern Recognition

### This is the SAME pattern as:

**1. Allocate Minimum Pages**
- Minimize maximum pages per student
- Contiguous book allocation
- Binary search on pages

**2. Capacity to Ship Packages**
- Minimize ship capacity
- Ship packages in order
- Binary search on capacity

**3. Koko Eating Bananas** (This problem!)
- Minimize eating speed
- Eat piles in order
- Binary search on speed

### Common Structure

```
Problem Type: Minimize Maximum under Constraint

Setup:
  low = minimum possible answer
  high = maximum possible answer

Binary Search:
  while low < high:
    mid = (low + high) / 2
    if (feasible at mid):
      high = mid      // Try to minimize
    else:
      low = mid + 1   // Need to increase

Return: low
```

---

## 🔧 Common Mistakes

### Mistake 1: Wrong Search Space

**Wrong:**
```javascript
let low = 0;  // ❌ Speed must be at least 1!
```

**Correct:**
```javascript
let low = 1;  // ✓ Minimum speed is 1 banana/hour
```

---

### Mistake 2: Integer Division Issues

**Wrong:**
```javascript
totalHours += pile / speed;  // ❌ Gives decimal!
// 7/3 = 2.33, but need 3 hours
```

**Correct:**
```javascript
totalHours += Math.ceil(pile / speed);  // ✓ Rounds up
```

---

### Mistake 3: Off-by-One in Binary Search

**Wrong:**
```javascript
while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    if (canFinish(piles, mid, h)) {
        high = mid;  // ❌ Infinite loop possible!
    }
}
```

**Correct:**
```javascript
while (low < high) {  // ✓ Use < not <=
    let mid = Math.floor((low + high) / 2);
    if (canFinish(piles, mid, h)) {
        high = mid;
    } else {
        low = mid + 1;
    }
}
```

**OR (alternative correct version):**
```javascript
while (low <= high) {
    let mid = Math.floor((low + high) / 2);
    if (canFinish(piles, mid, h)) {
        answer = mid;
        high = mid - 1;  // ✓ Move to mid - 1
    } else {
        low = mid + 1;
    }
}
```

---

### Mistake 4: Not Handling Early Exit

**Inefficient:**
```javascript
function canFinish(piles, speed, h) {
    let totalHours = 0;
    for (let pile of piles) {
        totalHours += Math.ceil(pile / speed);
    }
    return totalHours <= h;  // Calculates all even if already exceeded
}
```

**Optimized:**
```javascript
function canFinish(piles, speed, h) {
    let totalHours = 0;
    for (let pile of piles) {
        totalHours += Math.ceil(pile / speed);
        if (totalHours > h) {
            return false;  // ✓ Exit early!
        }
    }
    return true;
}
```

---

## 💭 Intuition Building

### Why Greedy Works

**Question:** Why can we just sum up hours pile by pile?

**Answer:** 
- Koko must eat piles in order (contiguous)
- Each pile takes a fixed number of hours at speed k
- No optimization possible - must eat each pile completely
- Therefore, simple summation is both greedy AND optimal

### Visual Understanding

```
piles = [3, 6, 7, 11], speed = 4

Hour 1: [3] → eat 3, wait 1 (pile done)
Hour 2: [6] → eat 4, 2 left
Hour 3: [6] → eat 2 (pile done), wait 2
Hour 4: [7] → eat 4, 3 left
Hour 5: [7] → eat 3 (pile done), wait 1
Hour 6: [11] → eat 4, 7 left
Hour 7: [11] → eat 4, 3 left
Hour 8: [11] → eat 3 (pile done), wait 1

Total: 8 hours ✓
```

### Binary Search Convergence

```
Search Space: [1 -------- 11]
                ↑          ↑
              slow       fast

Try mid=6: Works! → [1 -- 6]
Try mid=3: Fails! → [4 -- 6]
Try mid=5: Works! → [4 -- 5]
Try mid=4: Works! → Answer = 4
```

---

## 📝 Practice Problems

### Related LeetCode Problems

**1. Allocate Minimum Pages (GFG)**
- Same pattern
- Minimize maximum pages
- Binary search on answer

**2. Capacity to Ship Packages Within D Days (#1011)**
- Minimize ship capacity
- Ship in D days
- Binary search on capacity

**3. Split Array Largest Sum (#410)**
- Split into m subarrays
- Minimize largest sum
- Binary search on sum

**4. Minimum Limit of Balls in a Bag (#1760)**
- Minimize maximum balls
- K operations allowed
- Binary search on limit

**5. Magnetic Force Between Two Balls (#1552)**
- Maximize minimum distance
- Binary search on distance

---

## 🎯 Quick Reference Template

```javascript
// TEMPLATE: Minimize Maximum with Constraint

function minimizeMaximum(array, constraint) {
    // Define search space
    let low = minimumPossibleValue();
    let high = maximumPossibleValue();
    
    // Binary search
    while (low < high) {
        let mid = Math.floor((low + high) / 2);
        
        if (isFeasible(array, mid, constraint)) {
            high = mid;      // Try to minimize
        } else {
            low = mid + 1;   // Need to increase
        }
    }
    
    return low;
}

function isFeasible(array, candidateMax, constraint) {
    // Greedy check if possible at candidateMax
    // Return true if constraint satisfied
    // Return false otherwise
}
```

**For Koko Problem:**
```javascript
minimumPossibleValue = 1 (min speed)
maximumPossibleValue = max(piles) (max speed)
isFeasible = can finish in h hours at speed k
constraint = h hours
```

---

## 📊 Summary

### Key Concepts

1. **Binary Search on Answer Space**
   - Not searching the array
   - Searching for the answer value
   - Answer space is sorted even if input isn't

2. **Minimize Maximum Pattern**
   - Want smallest value that satisfies constraint
   - Binary search finds this efficiently
   - Greedy validation checks feasibility

3. **Ceiling Division**
   - `Math.ceil(pile / speed)` crucial
   - Represents waiting after finishing pile
   - Cannot move to next pile in same hour

4. **Early Termination**
   - Exit feasibility check when exceeds limit
   - Saves computation time
   - Doesn't affect correctness

5. **Search Space Bounds**
   - Lower: 1 (must eat at least 1 banana/hour)
   - Upper: max(piles) (eating faster is wasteful)
   - These bounds ensure we find minimum

### Complexity Summary

| Aspect | Complexity | Explanation |
|--------|-----------|-------------|
| Time | O(n log m) | n piles × log₂(max pile size) |
| Space | O(1) | Constant extra variables |
| Binary Search Iterations | O(log m) | m = max(piles) |
| Per Iteration Check | O(n) | Sum hours for all piles |

---

**Problem:** LeetCode #875 - Koko Eating Bananas  
**Difficulty:** Medium  
**Pattern:** Binary Search on Answer Space  
**Similar To:** Allocate Minimum Pages, Ship Packages  
**Key Technique:** Minimize Maximum with Feasibility Check

**Remember:** This is a classic pattern - master it for interviews at top tech companies!