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

## Solution 3: O(n) Time and Space

```dart
class Solution {
  bool isAnagram(String s, String t) {
      // Check Input
      if(s.length != t.length) return false;

      final az = 'az'.codeUnits;    // [97, 122]
      final charList = List<int>.generate(az.last - az.first + 1 , (index) => 0);   // [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]

      for(int i=0 ; i<s.length ; i++){
          var sIndex = s.codeUnitAt(i) - az.first;
          charList[sIndex] += 1;

          var tIndex = t.codeUnitAt(i) - az.first;
          charList[tIndex] -= 1;
      }

      return charList.every((e) => e == 0);
  }
}
```

The Unicode standard tells us that the letters of a particular word should be mapped to numbers and the number associated with each character is called a **code point**.

Example: `a = 97`, `b = 98`, `c = 99`, ..., `z = 122`

- `codeUnitAt(index)`: Returns the 16-bit UTF-16 code unit at the given `index`.
    - Example:
    ```dart
    void main(){
        var str = 'anagram'.codeUnitAt(2);
        print(str); // 97
    }
    ```
- `generate()`: Creates a list of the given length and fills each position according with the value returned by the generator.
    - Example:
    ```dart
    void main(){
        final charList = List<int>.generate(26 , (index) => 0);
        print(charList);  // [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    }
    ```


- `every()`: returns a boolean indicating if every element of the collection satisfies the given condition.

## Solution 4: O(n) Time and O(1) space

```dart
class Solution {
  bool isAnagram(String s, String t) {
    if (s.length != t.length) return false; // If the lengths are not equal, they cannot be anagrams

    final countMap = Map<String, int>();

    // Count occurrences of characters in string s
    for (int i = 0; i < s.length; i++) {
      String char = s[i];
      if (countMap.containsKey(char)) {
        countMap[char]++;
      } else {
        countMap[char] = 1;
      }
    }

    // Compare occurrences of characters in string t with the counts in countMap
    for (int i = 0; i < t.length; i++) {
      String char = t[i];
      if (countMap.containsKey(char) && countMap[char] > 0) {
        countMap[char]--;
      } else {
        return false;
      }
    }

    return true;
  }
}
```

In this solution, we use a hash table (`countMap`) to store the counts of characters in string `s`. We iterate through `s` and increment the count of each character in `countMap`. Then, we iterate through string `t` and decrement the count of each character in `countMap` if it exists and has a count greater than `0`. If at any point we encounter a character in `t` that does not exist in `countMap` or has a count of `0`, we can immediately return `false` as it means `t` is not an anagram of `s`. If we successfully iterate through both strings and all counts in `countMap` are zero, then `t` is an anagram of `s`.

The time complexity of this solution is **O(N)**, where N is the length of the strings, as we need to iterate through both strings once. The space complexity is **O(1)** as the hash table (`countMap`) will have a constant number of entries since the character set is assumed to be fixed.

Reference:
- [List use of double dot (.) in dart?](https://stackoverflow.com/questions/49447736/list-use-of-double-dot-in-dart)
- [Valid Anagram - Leetcode 242 - Python](https://www.youtube.com/watch?v=9UtInBqnCgA)