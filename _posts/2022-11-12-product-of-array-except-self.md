---
layout: post
author: Aniket Ambore
tags: [arrays, hashing, medium]
---

## Leetcode PS: [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/description/)

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

The product of any prefix or suffix of nums is guaranteed to fit in a **32-bit integer**.

You must write an algorithm that runs in **O(n)** time and without using the division operation.

### Example 1:

```dart
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

### Example 2:

```dart
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

### Constraints
- `2 <= nums.length <= 105`
- `-30 <= nums[i] <= 30`
- The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit integer**.

**Follow up**: Can you solve the problem in **O(1)** extra space complexity? (The output array **does not** count as extra space for space complexity analysis.)

## Solution

### Intuition
Prefix operation followed by Postfix operation on the `result` array.

### Approach
1. Generating a result list of `nums.length`, holding 1 initially.
    - eg. `nums = [1,2,3,4]` => `result = [1,1,1,1]`
2. Initial `prefix` counter starting from the default value of 1. Updating the result with only `prefix` multiples.
    - eg. `result = [1,1,2,6]`
3. Initial `postfix` counter starting from the default value of 1. Updating the result with posfix multiple to the existing prefix.
    - eg. `result = [24, 12, 8, 6]`

### Code
```
class Solution {
  List<int> productExceptSelf(List<int> nums) {
      final result = List<int>.generate(nums.length , (_) => 1);

      var prefix = 1;
      for(int i=0 ; i<nums.length ; i++){
          result[i] *= prefix;
          prefix *= nums[i];
      }

      var postfix = 1;
      for(int i=nums.length-1 ; i>=0 ; i--){
          result[i] *= postfix;
          postfix *= nums[i];
      }

      return result;
  }
}
```

### Complexity
- Time complexity: **O(n)**

- Space complexity: **O(1)**

### Reference
- [Product of Array Except Self - Leetcode 238 - Python](https://www.youtube.com/watch?v=bNvIQI2wAjk)