---
layout: post
author: Aniket Ambore
tags: [arrays, hashing, medium]
---

## Leetcode PS: [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/description/)

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

### Example 1:

```dart
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

### Example 2:

```dart
Input: strs = [""]
Output: [[""]]
```

### Example 3:

```dart
Input: strs = ["a"]
Output: [["a"]]
```

### Constraints
- `1 <= strs.length <= 104`
- `0 <= strs[i].length <= 100`
- `strs[i]` consists of lowercase English letters.

## Solution 1

```dart
class Solution {
  List<List<String>> groupAnagrams(List<String> strs) {
      final result = <String, List<String>>{};
      final az = 'az'.codeUnits;

      for(final s in strs){
          final charList = List<int>.generate(az.last-az.first + 1, (index) => 0);

          for(int i=0 ; i<s.length ; i++){
              final index = s.codeUnitAt(i) - az.first;
              charList[index] += 1;
          }

          if(result[charList.toString()] == null){
              result[charList.toString()] = [s];
          } else{
              result[charList.toString()]?.add(s);
          }
      }

      return result.values.toList();
  }
}
```

- Time Complexity: **O(m * n)**
    - `m` is the total number of input strings that are given in the `strs` list.
    - `n` is the average length of a string in `s`, like how many characters are their in a particular string.

# Reference
- [Group Anagrams - Categorize Strings by Count - Leetcode 49](https://www.youtube.com/watch?v=vzdNOK2oB2E)
