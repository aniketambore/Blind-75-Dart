---
layout: post
author: Aniket Ambore
tags: [arrays, string, easy]
---

Given 2 arrays that are sorted, can you merge these 2 arrays into one array that still needs to be sorted.

### Example

```dart
Input:
listA = [0, 3, 4, 31];
listB = [4, 6, 30];

Output:
result = [0, 3, 4, 4, 6, 30, 31]
```

## Solution

### Merge Sort Algorithm
The idea behind merge sort is to **divide and conquer** — to break up a big problem into several smaller, easier-to-solve problems and then combine the solutions into a final result. The merge sort mantra is to split first and merge later.

### Merging List Method

```dart
List<E> _merge<E extends Comparable<dynamic>>(List<E> listA, List<E> listB){
  var indexA = 0;
  var indexB = 0;
  final result = <E>[];
  
  while(indexA < listA.length && indexB < listB.length){
    final valueA = listA[indexA];
    final valueB = listB[indexB];
    
    if(valueA.compareTo(valueB) < 0){
      result.add(valueA);
      indexA += 1;
    } else if(valueA.compareTo(valueB) > 0){
      result.add(valueB);
      indexB += 1;
    } else{
      result.add(valueA);
      result.add(valueB);
      indexA += 1;
      indexB += 1;
    }
  }
  
  if(indexA < listA.length){
    result.addAll(listA.getRange(indexA,listA.length));
  }
  
  if(indexB < listB.length){
    result.addAll(listB.getRange(indexB, listB.length));
  }
  
  return result;
}
```

- [compareTo method](https://api.flutter.dev/flutter/dart-core/num/compareTo.html)
    - Example Code:
    ```dart
    void main(){
        print(1.compareTo(2)); // => -1 because 1 < 2
        print(2.compareTo(1)); // => 1 because 2 > 1
        print(1.compareTo(1)); // => 0 because 1 == 1
    }
    ```

- [getRange method](https://api.dart.dev/stable/1.10.1/dart-core/List/getRange.html)
    - Example Code:
    ```dart
    void main(){
        final colors = ['red', 'green', 'blue', 'orange', 'pink'];
        final range = colors.getRange(0, 4);
        print(range); // (red, green, blue, orange)
    }
    ```

> **Note**: `getRange` is similar to `substring` except that it doesn’t return a new list. It just returns an iterable pointing to the elements of the current list. No need to spend time creating unnecessary objects.

### Splitting

```dart
List<E> mergeSort<E extends Comparable<dynamic>>(List<E> list){
  if(list.length < 2) return list;
  
  final middle = list.length ~/ 2;
  final left = mergeSort(list.sublist(0,middle));
  final right = mergeSort(list.sublist(middle));
  
  return _merge(left,right);
}
```

- [sublist method](https://api.dart.dev/be/138159/dart-core/List/sublist.html)
    - Example Code:
    ```dart
        void main(){
        final colors = ['red', 'green', 'blue', 'orange', 'pink'];
        final range = colors.sublist(0, 4);
        final middle = colors.sublist(3);
        print(range); // [red, green, blue, orange]
        print(middle);  // [orange, pink]
    }
    ```

### main

```dart
void main(){
  final listA = [0, 3, 4, 31];
  final listB = [4, 6, 30];
  final result = mergeSort([...listA,...listB]);
  print(result);    // [0, 3, 4, 4, 6, 30, 31]
}
```