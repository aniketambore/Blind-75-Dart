---
layout: post
author: Aniket Ambore
tags: [arrays, hashing, easy]
---

## Leetcode PS: [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/description/)

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

### Example 1:

```dart
Input: s = "anagram", t = "nagaram"
Output: true
```

### Example 2:

```dart
Input: s = "rat", t = "car"
Output: false
```

### Constraints
- `1 <= s.length, t.length <= 5 * 104`
- `s and t consist of lowercase English letters.`

**Follow up**: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?


## Solution 1: O(n^2) Not Efficient

```dart
class Solution {
  bool isAnagram(String s, String t) {
      if(s.length != t.length) return false;

      var sList = s.split('')..sort();
      var tList = t.split('')..sort();
      
      for(int i=0; i<sList.length; i++){
          if(sList[i] != tList[i]) return false;
      }
        
        return true;
    }
}
```

Dart uses the insertion sort algorithm for lists with 32 or fewer elements, the `sort` method defaults to an insertion sort. Only for larger collections does Dart make use of a different sorting algorithm.

Insertion sort has an average time complexity of **O(n²)**

## Solution 2: O(S + T) Time and Space

```dart
class Solution {
  bool isAnagram(String s, String t) {
      if(s.length != t.length) return false;

      var sMap = Map(); // character : occurence
      var tMap = Map(); // character : occurence

      for(int i=0; i<s.length; i++){
          sMap[s[i]] = 1 + (sMap[s[i]] ?? 0);
          tMap[t[i]] = 1 + (tMap[t[i]] ?? 0);
      }

      for(final k in sMap.keys){
          if(sMap[k] != tMap[k]) return false;
      }

      return true;

  }
}
```

Its actually **O(S + S)** because length of both of the strings is 's'. So filling both the hash maps with frequencies would take just **O(s)** as it can be done in a single loop. Another **O(S)** to compare the frequencies in both the hash tables. 

So ultimately **O(2S)** drop the constants we get **O(S)** or **O(n)** where `n` is length of string.

Space complexity = **O(s)** for first string and **O(s)** for another string. So total **O(2s)** ultimately -> **O(s)**

Reference:
- [List use of double dot (.) in dart?](https://stackoverflow.com/questions/49447736/list-use-of-double-dot-in-dart)
- [Valid Anagram - Leetcode 242 - Python](https://www.youtube.com/watch?v=9UtInBqnCgA)