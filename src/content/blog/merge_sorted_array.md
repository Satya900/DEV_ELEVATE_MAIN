---
title: "Merge Sorted Array"
description: "Learn how to merge two sorted arrays efficiently in-place."
pubDate: 2024-03-28
category: "DSA"
author: "Satyabrata Mohanty"
tags: ["arrays-strings", "algorithms", "data-structures"]
---

# Merge Sorted Array

Given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively, merge `nums2` into `nums1` as one sorted array.

The final sorted array should be stored inside `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to 0 and should be ignored.

## Problem Description

### Input:
- Two sorted integer arrays `nums1` and `nums2`
- Two integers `m` and `n`, representing the number of elements in `nums1` and `nums2`
- `nums1` has a length of `m + n` to accommodate the merged result

### Output:
- Modify `nums1` in-place to contain the merged sorted array
- The final array should be sorted in non-decreasing order

### Example 1:
```plaintext
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6].
```

### Example 2:
```plaintext
Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
Explanation: The arrays we are merging are [1] and [].
The result of the merge is [1].
```

### Constraints:
- `nums1.length == m + n`
- `nums2.length == n`
- `0 <= m, n <= 200`
- `1 <= m + n <= 200`
- `-109 <= nums1[i], nums2[j] <= 109`

## Implementation

The key insight is to merge the arrays from the back, utilizing the extra space at the end of `nums1`. This approach prevents overwriting elements that we still need.

### Algorithm
1. Start from the end of both arrays
2. Compare elements from both arrays and place the larger one at the end of `nums1`
3. Move pointers accordingly
4. Handle remaining elements from `nums2` if any

### Code Implementation
Here's the Python implementation of the algorithm:

```python
def merge(nums1, m, nums2, n):
    # Initialize pointers for nums1, nums2, and the merged array
    p1 = m - 1  # Last element in nums1
    p2 = n - 1  # Last element in nums2
    p = m + n - 1  # Last position in merged array
    
    # While there are elements to compare in both arrays
    while p1 >= 0 and p2 >= 0:
        if nums1[p1] > nums2[p2]:
            nums1[p] = nums1[p1]
            p1 -= 1
        else:
            nums1[p] = nums2[p2]
            p2 -= 1
        p -= 1
    
    # If there are remaining elements in nums2
    while p2 >= 0:
        nums1[p] = nums2[p2]
        p2 -= 1
        p -= 1
```

### Explanation of Code
1. Initialize three pointers:
   - `p1`: Points to the last valid element in `nums1`
   - `p2`: Points to the last element in `nums2`
   - `p`: Points to the last position in the merged array
2. Compare elements from both arrays and place the larger one at position `p`
3. Move pointers accordingly
4. Handle any remaining elements from `nums2`

### Complexity Analysis
- **Time Complexity:** `O(m + n)` where we process each element exactly once
- **Space Complexity:** `O(1)` since we modify the array in-place

## Common Pitfalls

1. **Starting from the Front**
   - Starting the merge from the front of the arrays would require additional space to prevent overwriting elements
   - The problem requires an in-place solution

2. **Not Handling Remaining Elements**
   - Forgetting to copy remaining elements from `nums2` can lead to incorrect results
   - This is especially important when `nums2` has smaller elements than all elements in `nums1`

## Testing

Here's how you can test the implementation:

```python
# Test Case 1
nums1 = [1, 2, 3, 0, 0, 0]
nums2 = [2, 5, 6]
merge(nums1, 3, nums2, 3)
print(nums1)  # Expected: [1, 2, 2, 3, 5, 6]

# Test Case 2
nums1 = [1]
nums2 = []
merge(nums1, 1, nums2, 0)
print(nums1)  # Expected: [1]
```

## Conclusion

The merge sorted array problem demonstrates the importance of:
1. Utilizing available space efficiently
2. Working backwards to avoid overwriting needed elements
3. Handling edge cases properly

This solution provides an efficient, in-place approach to merging sorted arrays, making optimal use of the extra space provided in the first array.