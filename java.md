# Java Cheat Sheet

## Initial Collections
```java
List<Integer> toArrays = Arrays.asList(1, 10, 5);
Arrays.stream(list).boxed().collect(Collectors.toList());
```

## Binary Search
```java
List<Integer> list = Arrays.<Integer>asList(1, 5, 10);
Collections.binarySearch(list, 5); // 1
Collections.binarySearch(list, 2); // -2 => -((insert_position) + 1)
```
