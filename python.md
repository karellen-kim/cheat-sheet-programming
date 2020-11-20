# Python Cheat Sheet

## Class 
* toString, Hash, Compare
```python
class Pos :
    def __init__(self, x, y):
        self.x = x
        self.y = y
    def __str__(self):
        return "x=%d, y=%d" % (self.x, self.y)
    def __hash__(self):
        return hash((self.x, self.y))
    def __eq__(self, other):
        return (self.x, self.y) == (other.x, other.y)
    def __lt__(self, other):
        return other != None and self.x < other.x and self.y < other.y
```
* Singletone
```python
def singleton(class_):
  instances = {}
  def getinstance(*args, **kwargs):
    if class_ not in instances:
        instances[class_] = class_(*args, **kwargs)
    return instances[class_]
  return getinstance

@singleton
class MyClass(BaseClass):
  pass
```

## Collections
* List
```python
items = ['a', 'b', 'c', 'd', 'e']
items[::2] # [a, c, e]
items[::-2] # [e, c, a]
items[::-1] # == reverse

items.extend(['f', 'g']) # ['a', 'b', 'c', 'd', 'e', 'f', 'g']

items.index('d') # 2
'd' in items # True
items.count('d') 

del items[0] # [b', 'c', 'd', 'e', 'f', 'g']
items.remove('d')
```
* Dic
```python
items = { 'a' : 1, 'b' : 2}
# items[c] # ERROR
items.get('c') # None
items.get('c', 'default') # default
```
* Set
```python
items1 = {1, 2, 3}
items2 = {3, 4, 5}
items1.intersection(items2) # {3}
items1.union(items2) # {1, 2, 3, 4, 5}
items1.difference(items2) # {1, 2}
items1.symmetric_difference(items2) # {1, 2, 4, 5}
items1.issubset(items2) # False
```
* List as stack
```python
s = []
s.append(1)
s.append(2)
s.append(3)
s.pop(0) # 1
s.pop() # 3
```
* Deque as queue
```python
from collections import deque
q = deque()
q.append(1)
q.append(2)
q.popleft() # 1
```
* Deque as stack
```python
from collections import deque
q = deque()
q.append(1)
q.append(2)
q.pop() # 2
```
* sort, reverse
```python
list1 = [4,1,6]
list1.sort() # 1,4,6 

list2 = [4,1,6]
list2.sort(reverse=True) # 6,4,1

list3 = [4,1,6]
list3.reverse() # 6,1,4

strs = ["a", "ccc", "bb"]
strs.sort(key=len) # a, bb, ccc
list = [[100, 200], [200, 1300], [1000, 1250], [2000, 3200]]
list.sort(key=lambda item: item[1])

# 원본 리스트 변형하지 않음
list = [4,1,6]
sorted = list.sorted()
reversed = list.reversed()
```

* Initialize Matrix
```python
matrix = [[ 0 for i in range(n) ] for j in range(m)]
```

* Enumerate
```python
arr = [2, 7, 10]
for idx, val in enumerate(arr):
    print(idx, val)
```

## Algorithm
* Min heapq
```python
import heapq
h = []
heapq.heappush(h, 1)
heapq.heappush(h, 10)
print(heapq.heappop(h)) # 1
```
* Max heapq
```python
import heapq
h = []
heapq.heappush(h, 1 * -1)
heapq.heappush(h, 10 * -1)
print(heapq.heappop(h) * -1) # 10
```
* heapq with tuple
```python
heapq.heappush(h, (2, 'a'))
heapq.heappush(h, (1, 'b'))
heapq.heappop(h) # 1 sort by first element
```
* heapq with priority
```python
import heapq
h = []
heapq.heappush(h, ((x,y), n, other))
(x,y), n, other = heapq.heappop(h)
```
* Binary search
```python
import bisect
list = []
bisect.insort(list, 1)
bisect.insort(list, 10)
bisect.insort(list, 5)

print(list) # [1,5,10]
print(bisect.bisect(list, 3)) # 3이 들어갈 index : 1

print(bisect.bisect(list, 3)) # 5가 들어갈 index : 2
print(bisect.bisect_right(list, 5)) # 5가 들어갈 index : 2
print(bisect.bisect_left(list, 5)) # 5가 들어갈 index : 1 (같은 값인 경우 left)
```

## System 
* Import module
```python
import os,sys
sys.path.insert(1, os.path.join(sys.path[0], '..'))
```
* Recursion Limit
```python
import sys
sys.setrecursionlimit(1000)
```
* Force division to be floating point
```python
from __future__ import division
```

## Json
```python
import json

# load from json string
jsonStrings =  '{ "name":"Kim", "age":30 }'
json.loads(jsonStrings)

# load from obj
obj = { "name":"Kim", "age":30 }
json.dumps(obj)
```

## Parsing
* Date
```python
import datetime
import time

time = datetime.datetime.strptime("05/Dec/2018:10:27:18", "%d/%b/%Y:%H:%M:%S")
time.strftime("%Y-%m-%d")
```
* Regular expression
```python
import re

pattern = re.compile("(?P<date>\d{4}-\d{2}-\d{2}) (?P<time>\d{2}:\d{2}:\d{2}).*")
result = pattern.search(log)
result.group("date")
```

## Conversion
* Convert to character/int
```python
chr(97) // 'a'
ord('a') // 97
```

## String
* trim
```python
s.strip()
s.rstrip()
s.lstrip()
```

## Debug
* Print with variable name
```python 
def __debug__(var) :
    callers_local_vars = inspect.currentframe().f_back.f_locals.items()
    name = [var_name for var_name, var_val in callers_local_vars if var_val is var]
    if len(name) == 0 :
        print(var)
    else :
        print("%s = %s" % (name[0], str(var)))
```
* Assert equals
```python
def eq(expected, func, *params) :
	actual = func(*params)
	
	if expected == actual :
		print("[PASS] params={}, actual={}\n".format(params, actual))
	else :
		print("[ERROR] params={}, expected={}, actual={}\n".format(params, expected, actual))
```
