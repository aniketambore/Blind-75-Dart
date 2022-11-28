---
layout: post
author: Aniket Ambore
tags: [arrays, hashing, easy]
---

## Leetcode PS: [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/description/)

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

### Example 1:

```dart
Input: nums = [1,2,3,1]
Output: true
```

### Example 2:

```dart
Input: nums = [1,2,3,4]
Output: false
```

### Example 3:

```dart
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```

### Constraints
- `1 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

## Hint
hashset to get unique values in array, to check for duplicates easily

## Solution

```dart
class Solution {
  bool containsDuplicate(List<int> nums) {
      var hashSet = <int>{};
      for(int n in nums){
          if(hashSet.contains(n)) return true;
          hashSet.add(n);
      }
      return false;
  }
}
```

### Time Complextiy: O(n)
Linear Time: As the input list `nums` increases in size, the number of iterations that the `for` loop makes increases by the same amount.

### Space Complexity: O(n)
Linear Space: As the input list `nums` increases in size, the space increases proportionally with the values in the list to store in `Set`.