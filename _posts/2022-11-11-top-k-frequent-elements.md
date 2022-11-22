---
layout: post
author: Aniket Ambore
tags: [arrays, hashing, medium]
---

## Leetcode PS: [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/description/)

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. You may return the answer in **any order**.

### Example 1:

```dart
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

### Example 2:

```dart
Input: nums = [1], k = 1
Output: [1]
```

### Constraints
- `1 <= nums.length <= 105`
- `-104 <= nums[i] <= 104`
- `k` is in the range `[1, the number of unique elements in the array]`.
- It is **guaranteed** that the answer is **unique**.

**Follow up**: Your algorithm's time complexity must be better than `O(n log n)`, where n is the array's size.

## Solution: O(n) Time and Space
Using Bucket sort algrorithm.

```dart
class Solution {
  List<int> topKFrequent(List<int> nums, int k) {
    final result = <int>[];
    final valueCount = {}; // value : occurrence
    final bucket = List.generate(nums.length + 1,(_) => <int>[]);
    
    for(int n in nums){
      valueCount[n] = 1 + (valueCount[n] ?? 0);
    }
    
    for(int k in valueCount.keys){
      bucket[valueCount[k]].add(k);
    }
    
    for(int i=bucket.length - 1 ; i>=0 ; i--){
        for(final n in bucket[i]){
            result.add(n);
            if(result.length == k) return result;
        }
    }
    return [];
  }
}
```

## Reference:
- [Top K Frequent Elements - Bucket Sort - Leetcode 347 - Python](https://www.youtube.com/watch?v=YPTqKIgVk-k)