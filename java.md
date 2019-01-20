# Java Cheat Sheet

## Initial, Conversion Collections
```java
// Initial
List<Integer> toArrays = Arrays.asList(1, 10, 5);
List<Integer> toList = Arrays.stream(list).boxed().collect(Collectors.toList());

// Conversion
Integer[] toWrapperArray = toList.toArray(new Integer[]{});
int[] toPrimitiveArray = toList.stream().mapToInt(Integer::intValue).toArray();
```

## Binary Search
```java
List<Integer> list = Arrays.<Integer>asList(1, 5, 10);
Collections.binarySearch(list, 5); // 1
Collections.binarySearch(list, 2); // -2 => -((insert_position) + 1)
```
