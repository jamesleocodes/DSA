# Squares of a Sorted Array

## Problem Statement
Given an integer array `nums` sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

## Examples
### Example 1:
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]

### Example 2:
Input: nums = [-7,-3,2,3,11]
Output: [4,9,9,49,121]

## Constraints
* 1 <= nums.length <= 10^4
* -10^4 <= nums[i] <= 10^4
* nums is sorted in non-decreasing order

## Approach
We can solve this problem using two approaches:

1. **Naive Approach (O(n log n))**:
   - Square each element in the array
   - Sort the resulting array
   - This approach is straightforward but not optimal

2. **Two Pointer Approach (O(n))**:
   - Since the input array is sorted, we can use two pointers
   - One pointer at the start (for negative numbers)
   - One pointer at the end (for positive numbers)
   - Compare absolute values and place the larger square in the result array
   - Move pointers accordingly
   - This approach is optimal with O(n) time complexity and O(n) space complexity

### Time Complexity
- O(n) where n is the length of the array
- We only need to iterate through the array once

### Space Complexity
- O(n) as we need to create a new array to store the result

## Implementation
```python
def sortedSquares(nums):
    # Initialize two pointers
    left, right = 0, len(nums) - 1
    # Create result array of same length
    result = [0] * len(nums)
    # Start filling from the end of result array
    index = len(nums) - 1
    
    while left <= right:
        # Compare absolute values
        if abs(nums[left]) > abs(nums[right]):
            result[index] = nums[left] * nums[left]
            left += 1
        else:
            result[index] = nums[right] * nums[right]
            right -= 1
        index -= 1
    
    return result
```

## Usage
```python
nums = [-4,-1,0,3,10]
print(sortedSquares(nums))  # Output: [0,1,9,16,100]

nums = [-7,-3,2,3,11]
print(sortedSquares(nums))  # Output: [4,9,9,49,121]
```
