---
layout: post
author: Aniket Ambore
tags: [arrays, string, medium]
---

## Leetcode PS: [271. Encode and Decode Strings](https://leetcode.com/problems/encode-and-decode-strings/)
## Lintcode PS: [659· Encode and Decode Strings](https://www.lintcode.com/problem/659/)

Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

Please implement `encode` and `decode`.

### Example 1:

```dart
Input: ["lint","code","love","you"]
Output: ["lint","code","love","you"]
```

**Explanation**: One possible encode method is: "`lint:;code:;love:;you`"

### Example 2:

```dart
Input: ["we", "say", ":", "yes"]
Output: ["we", "say", ":", "yes"]
```

**Explanation**: One possible encode method is: "`we:;say:;:::;yes`"

# Solution

## Intuition & Approach
The encoding method for List of strings would be something like this:
- `${str.length} + '#' + $s`
    - Example: ["lint","code","love","you"] => `4#lint4#code4#love3#you`

The decoding method would be:
- Initial counter `i = 0`
- Then another counter `j = i`
    - Iterating `j` till it founds `str[j] == '#'`
- Getting the `length` of individual string element as:
    - `var length = int.tryParse(str.substring(i,j))`
- Finally adding the element in an empty list as:
    `result.add(str.substring(j+1 , j+1+length));`
- Updating the `i` counter `i = j+1+length`

## Complexity
- Time complexity: **O(n)**
- Space complexity: **O(n)**

## Code

```dart
void main(){
  var encodeString = encode(['lint','code','love','you']);
  print(encodeString);  // 4#lint4#code4#love3#you
  
  var decodeString = decode(encodeString);
  print(decodeString);  // [lint, code, love, you]
}

String encode(List<String> strs){
  var buffer = StringBuffer();
  for(final s in strs){
    buffer.write('${s.length}#$s');
  }
  return buffer.toString();
}

List<String> decode(String str){
  var result = <String>[];
  int i = 0;
  while(i < str.length){
    int j = i;
    while(str[j] != '#'){
      j += 1;
    }
    
    var length = int.tryParse(str.substring(i,j)) ?? 0;
    result.add(str.substring(j+1 , j+1+length));
    i = j+1+length;
  }
  
  return result;
}
```

## Reference:
- [Encode and Decode Strings - Leetcode 271 - Python](https://www.youtube.com/watch?v=B1k_sxOSgv8)