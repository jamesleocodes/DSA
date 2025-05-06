# Merge Sorted Array

## Problem Statement
You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

Merge `nums1` and `nums2` into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to 0 and should be ignored.

## Examples

### Example 1:
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6].

### Example 2:
Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
Explanation: The arrays we are merging are [1] and [].
The result of the merge is [1].

### Example 3:
Input: nums1 = [0], m = 0, nums2 = [1], n = 1
Output: [1]
Explanation: The arrays we are merging are [] and [1].
The result of the merge is [1].

## Constraints
* nums1.length == m + n
* nums2.length == n
* 0 <= m, n <= 200
* 1 <= m + n <= 200
* -109 <= nums1[i], nums2[j] <= 109

## Approach

### Two-Pointer Approach
The most efficient approach is to use three pointers and work backwards:

1. Initialize three pointers:
   - p1: points to the last element in nums1 (m-1)
   - p2: points to the last element in nums2 (n-1)
   - p: points to the last position in the merged array (m+n-1)

2. Compare elements from both arrays and place the larger one at position p
3. Move the corresponding pointer backwards
4. Continue until all elements from nums2 are placed

```python
def merge(nums1, m, nums2, n):
    p1 = m - 1  # Pointer for nums1
    p2 = n - 1  # Pointer for nums2
    p = m + n - 1  # Pointer for the merged array
    
    while p2 >= 0:
        if p1 >= 0 and nums1[p1] > nums2[p2]:
            nums1[p] = nums1[p1]
            p1 -= 1
        else:
            nums1[p] = nums2[p2]
            p2 -= 1
        p -= 1
```
## Step by step Exectuioon
| p1  | p2  | nums1[p1] | nums2[p2] | Condition Check          | Action Taken     | Updated nums1      |
|-----|-----|-----------|-----------|--------------------------|------------------|--------------------|
| 2   | 2   | 3         | 6         | nums1[p1] < nums2[p2]   | nums1[5] = 6     | [1,2,3,0,0,6]      |
| 2   | 1   | 3         | 5         | nums1[p1] < nums2[p2]   | nums1[4] = 5     | [1,2,3,0,5,6]      |
| 2   | 0   | 3         | 2         | nums1[p1] > nums2[p2]   | nums1[3] = 3     | [1,2,3,3,5,6]      |
| 1   | 0   | 2         | 2         | nums1[p1] ≤ nums2[p2]   | nums1[2] = 2     | [1,2,2,3,5,6]      |

## Complexity Analysis

### Time Complexity
- **O(m + n)**: We process each element exactly once
- Where m is the number of elements in nums1 and n is the number of elements in nums2

### Space Complexity
- **O(1)**: We modify nums1 in-place without using extra space

## Key Points
1. The solution must handle:
   - Empty arrays
   - Arrays of different lengths
   - Arrays with duplicate elements
2. The two-pointer approach is efficient because:
   - We work backwards to avoid overwriting elements in nums1
   - We don't need extra space
   - We process each element exactly once

## Test Cases
1. Basic case:
   - Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
   - Expected Output: [1,2,2,3,5,6]

2. Empty second array:
   - Input: nums1 = [1], m = 1, nums2 = [], n = 0
   - Expected Output: [1]

3. Empty first array:
   - Input: nums1 = [0], m = 0, nums2 = [1], n = 1
   - Expected Output: [1]

4. Arrays with duplicate elements:
   - Input: nums1 = [1,1,1,0,0,0], m = 3, nums2 = [1,1,1], n = 3
   - Expected Output: [1,1,1,1,1,1]

## Implementation Details
The implementation is available in the following files:
- `merge_sorted_array.py`: Python implementation file

## Usage
To run the implementation:
1. Import the function from `merge_sorted_array.py` in your Python code
2. Call the function with appropriate parameters

## Notes
- The problem is a good example of the two-pointer technique
- Working backwards is crucial to avoid overwriting elements
- No extra space is needed as we modify nums1 in-place 