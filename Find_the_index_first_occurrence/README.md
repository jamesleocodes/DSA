# Find the Index of First Occurrence

## Problem Statement
Given two strings `needle` and `haystack`, return the index of the first occurrence of `needle` in `haystack`, or `-1` if `needle` is not part of `haystack`.

## Examples
### Example 1:
Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6. The first occurrence is at index 0, so we return 0.

### Example 2:
Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.

## Constraints
* 1 <= haystack.length, needle.length <= 104 # 
* haystack and needle consist of only lowercase English letters.

## Approach

### Two-Pointer Approach
An efficient approach using two pointers to compare characters.

```python
def strStr(haystack: str, needle: str) -> int:
    if not needle:
        return 0
    
    n = len(haystack)
    m = len(needle)
    
    for i in range(n - m + 1):
        left = i
        right = 0
        while right < m and haystack[left] == needle[right]:
            left += 1
            right += 1
        if right == m:
            return i
    
    return -1
```

## Complexity Analysis

### Time Complexity
- **Worst Case**: O(m*n)
  - Where m is the length of haystack and n is the length of needle
  - Occurs when we need to check almost every position in haystack
  - For each position i, we might need to compare up to n characters
  - Example: haystack = "aaaaa", needle = "aaaab"

- **Best Case**: O(n)
  - Occurs when the needle is found at the beginning of haystack
  - We only need to compare n characters once
  - Example: haystack = "hello", needle = "he"

- **Average Case**: O(m)
  - In practice, we often find a mismatch early in the comparison
  - Most comparisons stop after checking a few characters
  - This makes the average case much better than the worst case

### Space Complexity
- **O(1)**: Constant Space
  - We only use a few variables (i, left, right) regardless of input size
  - No additional data structures are created
  - The space used does not grow with the input size

## Key Points
1. The two-pointer approach is efficient and easy to understand:
   - Uses two pointers to compare characters
   - Stops comparison as soon as a mismatch is found
   - Avoids creating substring copies
2. Edge cases to consider:
   - Empty needle string
   - Needle longer than haystack
   - No occurrence of needle in haystack
   - Multiple occurrences of needle in haystack

## Test Cases
1. Basic case:
   - Input: haystack = "hello", needle = "ll"
   - Expected Output: 2

2. No occurrence:
   - Input: haystack = "aaaaa", needle = "bba"
   - Expected Output: -1

3. Empty needle:
   - Input: haystack = "hello", needle = ""
   - Expected Output: 0

4. Needle equals haystack:
   - Input: haystack = "hello", needle = "hello"
   - Expected Output: 0

5. Multiple occurrences:
   - Input: haystack = "mississippi", needle = "issi"
   - Expected Output: 1

## Implementation Details
The implementation is available in the following files:
- `first_occurrence.ipynb`: Jupyter notebook with detailed explanations and interactive examples
- `first_occurrence.py`: Python implementation file

## Usage
To run the implementation:
1. Open the Jupyter notebook `first_occurrence.ipynb` for interactive examples
2. Or import the functions from `first_occurrence.py` in your Python code

## Notes
- The two-pointer approach is efficient in practice
- It avoids creating substring copies, which can be expensive for large strings
- The approach is easy to understand and implement
- The problem is a good example of string manipulation and pattern matching 