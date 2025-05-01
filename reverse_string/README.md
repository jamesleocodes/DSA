# Reverse String

## Problem Description
Write a function that reverses a string. The input string is given as an array of characters `s`. The function must modify the input array in-place with O(1) extra memory.

### Examples
1. Input: `s = ["h","e","l","l","o"]`
   Output: `["o","l","l","e","h"]`

2. Input: `s = ["H","a","n","n","a","h"]`
   Output: `["h","a","n","n","a","H"]`

### Constraints
- 1 <= s.length <= 105
- s[i] is a printable ascii character

## Solution Approach
The solution uses the Two-Pointer Technique to reverse the string in place:
1. Initialize two pointers: `left` at the start (index 0) and `right` at the end (index len(s)-1)
2. Swap characters at `left` and `right` positions
3. Move `left` pointer forward and `right` pointer backward
4. Continue until the pointers meet or cross each other

### Time Complexity
- O(n) where n is the length of the string
- We only need to iterate through half of the string since we're swapping pairs of characters

### Space Complexity
- O(1) as we're modifying the input array in place without using any extra space

## Implementation
```python
def reverseString(s):
    left, right = 0, len(s) - 1
    while left < right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
```

## Usage
```python
s = ["h","e","l","l","o"]
reverseString(s)
print(s)  # Output: ["o","l","l","e","h"]
``` 