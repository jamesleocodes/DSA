# Remove Duplicates from Sorted Array

## Problem Statement
Given an integer array `nums` sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in `nums`.

## Examples
### Example 1:
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.

### Example 2:
Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.

## Constraints
* 1 <= nums.length <= 3 * 10^4
* -100 <= nums[i] <= 100
* nums is sorted in non-decreasing order

## Approach
We can solve this problem efficiently using the two-pointer technique with left and right pointers:

1. **Two Pointer Approach (O(n))**:
   - Use a left pointer to track the position of unique elements
   - Use a right pointer to scan through the array
   - When we find a new unique element, move it to the position after the last unique element
   - This approach maintains the relative order of elements

### Time Complexity
- O(n) where n is the length of the array
- We only need to iterate through the array once

### Space Complexity
- O(1) as we're modifying the array in-place
- No additional space is required

## Implementation
```python
def removeDuplicates(nums):
    if not nums:
        return 0
    
    # Initialize left pointer at the start
    left = 0
    
    # Right pointer starts from 1 and moves through the array
    for right in range(1, len(nums)):
        # If we find a new unique element
        if nums[right] != nums[left]:
            # Move left pointer forward
            left += 1
            # Place the unique element at left's new position
            nums[left] = nums[right]
    
    # Return the number of unique elements
    return left + 1
```

## Usage
```python
nums = [1,1,2]
k = removeDuplicates(nums)
print(k)        # Output: 2
print(nums)     # Output: [1,2,2]

nums = [0,0,1,1,1,2,2,3,3,4]
k = removeDuplicates(nums)
print(k)        # Output: 5
print(nums)     # Output: [0,1,2,3,4,2,2,3,3,4]
```

## Explanation of Two Pointer Approach
1. We use two pointers:
   - `left`: tracks the position of the last unique element
   - `right`: scans through the array to find new unique elements

2. The algorithm works because:
   - The array is sorted, so duplicates are adjacent
   - When we find a new unique element (nums[right] != nums[left]), we:
     - Move the left pointer forward (left += 1)
     - Copy the new unique element to the left pointer's position
   - This effectively compresses all unique elements to the front of the array

3. The final number of unique elements is left + 1 because:
   - left starts at 0 (first element is always unique)
   - We count the number of unique elements we've found

4. Visual Example:
   ```
   Initial: [1,1,2]
   Step 1:  [1,1,2]  left=0, right=1 (duplicate, do nothing)
   Step 2:  [1,2,2]  left=1, right=2 (unique, move to left+1)
   Final:   [1,2,2]  k = left + 1 = 2
   ```
