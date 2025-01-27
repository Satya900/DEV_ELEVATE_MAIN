---
title: "Remove Duplicates from Sorted Array"
description: "In-place removal of duplicates from a sorted array."
pubDate: 2024-03-28
category: "DSA"
author: "Satyabrata Mohanty"
tags: ["arrays-strings", "algorithms", "data-structures"]
---

# Remove Duplicates from Sorted Array

Given an integer array `nums` sorted in non-decreasing order, we aim to remove the duplicates **in-place** such that each unique element appears only once. The relative order of the elements should be maintained.

The task is to return the number of unique elements, `k`, while modifying the input array `nums` such that the first `k` elements contain the unique elements.

## Problem Description

### Input:
- An integer array `nums` of size `n` where:
  - `1 <= nums.length <= 3 * 10^4`
  - `-100 <= nums[i] <= 100`
  - `nums` is sorted in non-decreasing order.

### Output:
- An integer `k` representing the number of unique elements in `nums`.
- Modify `nums` in-place so that the first `k` elements are the unique elements in the order they were originally present.
- The remaining elements beyond `k` can be ignored.

### Example 1:
```plaintext
Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
Explanation: The first two elements are the unique elements 1 and 2. It does not matter what comes after index 1.
```

### Example 2:
```plaintext
Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
Explanation: The first five elements are the unique elements 0, 1, 2, 3, and 4.
```

### Constraints:
- The input array `nums` is always sorted in non-decreasing order.

## Implementation

The key insight is that the sorted nature of the array allows us to use a two-pointer technique to efficiently remove duplicates.

### Algorithm
1. Use a pointer `k` to track the position of the next unique element in the array.
2. Iterate through the array with another pointer `i`. Compare each element with the last placed unique element.
3. If a new unique element is found, place it at index `k` and increment `k`.
4. Return `k` as the count of unique elements.

### Code Implementation
Below is the Python implementation of the algorithm:

```python
def removeDuplicates(nums):
    if not nums:
        return 0

    k = 1  # The index for the next unique element

    for i in range(1, len(nums)):
        if nums[i] != nums[i - 1]:
            nums[k] = nums[i]
            k += 1

    return k
```

### Explanation of Code
- Start with `k = 1` because the first element is always unique.
- For each element in the array starting from index 1:
  - Compare it with the previous element.
  - If it's unique, copy it to position `k` and increment `k`.
- Return `k`, which represents the count of unique elements.

### Complexity Analysis
- **Time Complexity:** `O(n)` because we traverse the array once.
- **Space Complexity:** `O(1)` since we perform in-place modifications without using additional space.

## Custom Judge Code
To verify the solution, the custom judge runs the following:

```java
int[] nums = {...}; // Input array
int[] expectedNums = {...}; // Expected output array with unique elements

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
```

If all assertions pass, the solution is accepted.

## Conclusion
Using the two-pointer technique allows us to efficiently remove duplicates from a sorted array in-place. This approach leverages the sorted property of the input, ensuring optimal performance and simplicity.