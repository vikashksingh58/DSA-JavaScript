# Sorting Algorithms Study Notes

## Overview
Three fundamental sorting algorithms with O(n²) time complexity and O(1) space complexity:
- Bubble Sort
- Selection Sort
- Insertion Sort

---

## 1. Bubble Sort

### Concept
Repeatedly compares adjacent elements and swaps them if they're in the wrong order, "bubbling" larger elements toward the end.

### How It Works
1. Start with the first element as the "bubble element"
2. Compare it with the next element
3. If bubble > next element → swap them
4. If bubble ≤ next element → move forward
5. Repeat until the array is sorted

### Key Details
- **Phases**: n-1 phases for an array of size n
- **Each phase**: Places one element in its correct position
- **Comparisons per phase**: Decrease by 1 each time
  - Phase 1: n-1 comparisons
  - Phase 2: n-2 comparisons
  - Phase n-1: 1 comparison

### Implementation Structure
```
Outer loop: Controls phases (runs n-1 times)
Inner loop: Performs comparisons and swaps within unsorted portion
```

### Complexity
- **Time**: O(n²) - approximately n(n-1)/2 comparisons
- **Space**: O(1) - in-place sorting

---

## 2. Selection Sort

### Concept
Divides array into sorted and unsorted parts. Repeatedly selects the minimum element from unsorted part and places it at the end of sorted part.

### How It Works
1. Find the minimum element in the unsorted part
2. Swap it with the first element of the unsorted part
3. Expand sorted part by one element
4. Shrink unsorted part by one element
5. Repeat until entire array is sorted

### Key Details
- **Initial state**: Sorted part is empty, unsorted part is entire array
- **Swapping**: Done using indices, not direct values
- **Progress**: Each iteration adds exactly one element to sorted part

### Implementation Structure
```
Outer loop: Iterates from start to n-1
Inner loop: Finds minimum element index in unsorted part (i+1 to n)
Swap: Exchange elements at current position and minimum index
```

### Complexity
- **Time**: O(n²) - nested loops scanning unsorted portion
- **Space**: O(1) - in-place swapping

---

## 3. Insertion Sort

### Concept
Builds sorted array one element at a time by inserting each element into its correct position within the already sorted portion.

### How It Works
1. Assume first element is already sorted
2. Pick next element (key)
3. Compare key backward with sorted elements
4. Shift elements greater than key one position right
5. Insert key at the correct position
6. Repeat for all elements

### Key Details
- **Starting point**: Begin from index 1 (index 0 is considered sorted)
- **Shifting**: Elements move right to make room for the key
- **Comparison direction**: Backward through sorted portion

### Boundary Conditions
- Inner loop stops when:
  - Reaches index -1, OR
  - Finds element ≤ key

### Implementation Structure
```
Outer loop: Starts from index 1 to n-1
Inner loop: Moves backward from i-1 to 0, shifting elements
Insert: Place key at correct position
```

### Complexity
- **Time**: O(n²) worst case (reverse sorted), better for nearly sorted data
- **Space**: O(1) - in-place shifting

---

## Comparison Table

| Algorithm | Main Strategy | Best Use Case | Stable? |
|-----------|--------------|---------------|---------|
| **Bubble Sort** | Swap adjacent pairs | Educational purposes | Yes |
| **Selection Sort** | Select minimum, swap to front | When swaps are costly | No |
| **Insertion Sort** | Insert into sorted position | Nearly sorted data | Yes |

---

## Common Characteristics

### All Three Algorithms Share:
- **Time Complexity**: O(n²) in worst case
- **Space Complexity**: O(1) - in-place sorting
- **Method**: Comparison-based sorting
- **Implementation**: Use nested loops
- **Suitability**: Small datasets only

---

## Key Terminology

| Term | Definition |
|------|------------|
| **Bubble Element** | Element being positioned in Bubble Sort through adjacent swaps |
| **Phase** | One complete pass that places one element correctly |
| **Sorted Part** | Portion of array already sorted |
| **Unsorted Part** | Portion of array yet to be sorted |
| **Swap** | Exchanging two elements' positions using indices |
| **Shift** | Moving elements one position right to make room |
| **Key** | Current element being inserted in Insertion Sort |

---

## Practice Tips

1. **Master nested loops** - Understand how outer and inner loops interact
2. **Dry run manually** - Work through examples on paper with sample arrays
3. **Track indices carefully** - Avoid off-by-one errors and boundary issues
4. **Test edge cases**:
   - Already sorted array
   - Reverse sorted array
   - Array with duplicates
   - Single element array
   - Empty array
5. **Code from scratch** - Implement without looking at references
6. **Analyze performance** - Count comparisons and swaps for different inputs

---

## Interview Preparation

### Common Questions
- Explain how each algorithm works
- What's the time/space complexity?
- When would you use one over another?
- Can you optimize Bubble Sort with a flag?
- Why is Insertion Sort better for nearly sorted data?

### Remember
- These are foundational algorithms frequently tested
- Understanding loop control and boundary handling is crucial
- Be able to trace execution step-by-step
- Know the differences between swapping and shifting operations

---

## Study Resources Timeline

| Time | Topic |
|------|-------|
| 00:00-00:10 | Bubble Sort theory and examples |
| 00:10-00:18 | Bubble Sort implementation |
| 00:18-00:37 | Selection Sort theory and implementation |
| 00:37-00:50 | Insertion Sort theory and implementation |

---

## Next Steps

1. Review pattern programming and loop concepts
2. Implement each algorithm in your preferred language
3. Test with various input arrays
4. Compare execution traces
5. Explore optimizations (e.g., early exit for Bubble Sort)
6. Move on to advanced sorting (Merge Sort, Quick Sort)