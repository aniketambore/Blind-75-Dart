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

## Solution 2

```dart
class Solution {
  List<List<String>> groupAnagrams(List<String> strs) {
    final anagramMap = Map<String, List<String>>();

    // Iterate through each string in strs
    for (int i = 0; i < strs.length; i++) {
      String str = strs[i];

      // Sort the characters in the string to use as a key in the hash table
      String sortedKey = String.fromCharCodes(str.runes.toList()..sort());

      // If the sortedKey is not present in the hash table, add it with an empty list as the value
      if (!anagramMap.containsKey(sortedKey)) {
        anagramMap[sortedKey] = [];
      }

      // Add the original string to the list of values associated with the sortedKey
      anagramMap[sortedKey].add(str);
    }

    // Convert the values of the hash table to lists and return as the final result
    return anagramMap.values.toList();
  }
}
```

The time complexity of this solution depends on the length of the input array and the length of the longest string in `strs`. Sorting the characters in each string takes **O(K log K)** time, where `K` is the length of the longest string. So the overall time complexity is **O(NK log K)**, where `N` is the length of the input array. The space complexity is **O(N)** as we need to store the anagram groups in a hash table.