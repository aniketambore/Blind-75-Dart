---
layout: post
author: Aniket Ambore
tags: [arrays, set, medium]
---

## Leetcode PS: [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/description/)

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in `O(n)` time.

### Example 1:

```dart
Input: nums = [100,4,200,1,3,2]
Output: 4
```

**Explanation**: The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is 4.

### Example 2:

```dart
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

# Solution

## Intuition && Approach
- Iterate through the initial list.
- Use `Set` to check if value has left neighbour, if not, which means that the value is the start of the sequence.
- Iterate the `length` counter till the value has right neighbour.

## Complexity
- Time complexity: O(n)
- Space complexity: O(n)

## Code
```
import 'dart:math';

class Solution {
  int longestConsecutive(List<int> nums) {
      var listSet = nums.toSet();
      var longest = 0;

      for(int n in nums){
          if(!listSet.contains(n-1)){
              var length = 1;
              while(listSet.contains(n+length)){
                  length += 1;
              }
              longest = max(length , longest);
          }
      }

      return longest;
  }
}
```

## Reference:
- [Leetcode 128 - LONGEST CONSECUTIVE SEQUENCE](https://www.youtube.com/watch?v=P6RZZMu_maU)