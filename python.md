# Python Cheat Sheet

## Recursion Limit
```
import sys
sys.setrecursionlimit(1000)
```

## Collections
* List as stack
```python
s = []
s.append(1)
s.append(2)
s.pop() # 2
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

# 원본 리스트 변형하지 않음
list = [4,1,6]
sorted = list.sorted()
reversed = list.reversed()
```

## Import module
```python
import os,sys
sys.path.insert(1, os.path.join(sys.path[0], '..'))
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

## Singletone
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

## Date Parsing
```python
import datetime
import time

time = datetime.datetime.strptime("05/Dec/2018:10:27:18", "%d/%b/%Y:%H:%M:%S")
time.strftime("%Y-%m-%d")
```

## Regular expression
```python
import re

pattern = re.compile("(?P<date>\d{4}-\d{2}-\d{2}) (?P<time>\d{2}:\d{2}:\d{2}).*")
result = pattern.search(log)
result.group("date")
```

## Debug : Print with variable name
```python 
def __debug__(var) :
    callers_local_vars = inspect.currentframe().f_back.f_locals.items()
    name = [var_name for var_name, var_val in callers_local_vars if var_val is var]
    if len(name) == 0 :
        print(var)
    else :
        print("%s = %s" % (name[0], str(var)))
```
