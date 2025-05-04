# Remove Element

## Problem Statement
Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` in-place. The order of the elements may be changed. Then return the number of elements in `nums` which are not equal to `val`.

## Examples
### Example 1:
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 2.

### Example 2:
Input: nums = [0,1,2,2,3,0,4,2], val = 2
Output: 5, nums = [0,1,3,0,4,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

## Constraints
* 0 <= nums.length <= 100
* 0 <= nums[i] <= 50
* 0 <= val <= 100

## Approach
We can solve this problem efficiently using the two-pointer technique. There are two common approaches:

1. **Slow-Fast Pointer Approach (O(n))**:
   - Use a slow pointer (`i`) to track the position of elements not equal to val
   - Use a fast pointer (`j`) to scan through the array
   - When we find an element not equal to val, move it to the position after the last valid element
   - This approach maintains the relative order of elements that are not equal to val

2. **Left-Right Pointer Approach (O(n))**:
   - Use a left pointer at the start and right pointer at the end
   - Swap elements equal to val with elements from the end
   - This approach is more efficient when val is rare in the array
   - Note: This approach does not maintain the relative order of elements

### Time Complexity
- O(n) where n is the length of the array
- We only need to iterate through the array once

### Space Complexity
- O(1) as we're modifying the array in-place
- No additional space is required

## Implementation
```python
# Slow-Fast Pointer Approach
def removeElement(nums, val):
    # Initialize slow pointer
    i = 0
    
    # Fast pointer j moves through the array
    for j in range(len(nums)):
        # If current element is not equal to val
        if nums[j] != val:
            # Move the element to the position after the last valid element
            nums[i] = nums[j]
            # Move slow pointer forward
            i += 1
    
    # Return the number of elements not equal to val
    return i

# Left-Right Pointer Approach
def removeElement(nums, val):
    # Handle empty array case
    if not nums:
        return 0
        
    left, right = 0, len(nums) - 1
    
    while left <= right:
        # If current element is val, swap with right element
        if nums[left] == val:
            nums[left] = nums[right]
            right -= 1
        else:
            # If current element is not val, just move left pointer
            left += 1
    
    return left

# Example usage:
nums = [3,2,2,3]
val = 3
k = removeElementLR(nums, val)
print(k)        # Output: 2
print(nums)     # Output: [2,2,3,3]

# Edge cases:
# Empty array
nums = []
val = 3
k = removeElementLR(nums, val)
print(k)        # Output: 0
print(nums)     # Output: []

# All elements are val
nums = [3,3,3,3]
val = 3
k = removeElementLR(nums, val)
print(k)        # Output: 0
print(nums)     # Output: [3,3,3,3]

# No elements are val
nums = [1,2,3,4]
val = 5
k = removeElementLR(nums, val)
print(k)        # Output: 4
print(nums)     # Output: [1,2,3,4]