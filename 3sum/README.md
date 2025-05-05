# 3Sum

## Problem Statement
Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

## Examples
### Example 1:
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
- nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0
- nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0
- nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0
The distinct triplets are [-1,0,1] and [-1,-1,2].

### Example 2:
Input: nums = []
Output: []

### Example 3:
Input: nums = [0]
Output: []

## Constraints
* 3 <= nums.length <= 3000
* -105 <= nums[i] <= 105

## Approach

### Two-Pointer Approach with Sorting
The most efficient approach is to use sorting and two-pointer technique:

1. Sort the array
2. Use three pointers: one for the first number, and two pointers (left and right) for the other two numbers
3. Skip duplicates to avoid duplicate triplets
4. Use the two-pointer technique to find pairs that sum to the negative of the first number

```python
def threeSum(nums):
    nums.sort()
    result = []
    
    for i in range(len(nums) - 2):
        # Skip duplicates for the first number
        if i > 0 and nums[i] == nums[i-1]:
            continue
            
        left = i + 1
        right = len(nums) - 1
        
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            
            if total < 0:
                left += 1
            elif total > 0:
                right -= 1
            else:
                result.append([nums[i], nums[left], nums[right]])
                
                # Skip duplicates for the second number
                while left < right and nums[left] == nums[left+1]:
                    left += 1
                # Skip duplicates for the third number
                while left < right and nums[right] == nums[right-1]:
                    right -= 1
                    
                left += 1
                right -= 1
                
    return result
```

## Complexity Analysis

### Time Complexity
- **O(n²)**: 
  - Sorting takes O(n log n)
  - For each number, we use two-pointer technique which takes O(n)
  - Total: O(n log n) + O(n²) = O(n²)

### Space Complexity
- **O(1)** or **O(n)** depending on the sorting algorithm:
  - If we use in-place sorting: O(1)
  - If we use a sorting algorithm that requires extra space: O(n)
  - The result list is not counted in space complexity as it's required for output

## Key Points
1. The solution must handle:
   - Duplicate triplets
   - Empty array
   - Array with less than 3 elements
   - Arrays with all zeros
2. The two-pointer approach is efficient because:
   - Sorting helps avoid duplicates
   - Two-pointer technique reduces the search space
   - We can skip duplicate numbers to avoid duplicate triplets

## Test Cases
1. Basic case:
   - Input: nums = [-1,0,1,2,-1,-4]
   - Expected Output: [[-1,-1,2],[-1,0,1]]

2. Empty array:
   - Input: nums = []
   - Expected Output: []

3. No solution:
   - Input: nums = [1,2,3,4]
   - Expected Output: []

4. All zeros:
   - Input: nums = [0,0,0]
   - Expected Output: [[0,0,0]]

5. Duplicate numbers:
   - Input: nums = [-2,0,1,1,2]
   - Expected Output: [[-2,0,2],[-2,1,1]]

## Implementation Details
The implementation is available in the following files:
- `3sum.ipynb`: Jupyter notebook with detailed explanations and interactive examples
- `3sum.py`: Python implementation file

## Usage
To run the implementation:
1. Open the Jupyter notebook `3sum.ipynb` for interactive examples
2. Or import the functions from `3sum.py` in your Python code

## Notes
- The problem is a good example of the two-pointer technique
- Sorting is crucial for both efficiency and handling duplicates
- The solution can be extended to solve similar problems like 4Sum
- Consider edge cases carefully, especially with duplicates 