---
layout: post
author: Aniket Ambore
tags: [arrays, string, easy]
---

Create a function that reverses a String.

### Example

```dart
Input: 'Hi My name is Aniket'
Output: 'tekinA si eman yM iH'
```

## Solution 1

```dart
String reverse1(String str){
  // Check Input
  if(str.length < 2) return str;
  
  final backwards = [];
  final totalItems = str.length -1;
  for(int i=totalItems; i>=0; i--){
    backwards.add(str[i]);
  }
  
  // print(backwards);
  return backwards.join('');
}

void main(){
  var reverseIt = reverse1('Hi My name is Aniket');
  print(reverseIt);
  // tekinA si eman yM iH
}
```

## Solution 2: Using Built-In Methods

```dart
String reverse2(String str){
  return str.split('').reversed.join('');
}

void main(){
  var reverseIt = reverse1('Hi My name is Aniket');
  print(reverseIt);
  // tekinA si eman yM iH
}
```

> **NOTE**: The way you should reverse a list in production code is to call the `reversed` method that List provides. This method is **O(1)** in time and space. This is because as an iterable it’s lazy and only creates a reversed view into the original collection. If you traverse the items and print out all of the elements,it predictably makes the operation **O(n)** in time while remaining **O(1)** in space.

- [split method](https://api.dart.dev/stable/2.1.1/dart-core/String/split.html)
- [join method](https://api.flutter.dev/flutter/dart-core/Iterable/join.html)