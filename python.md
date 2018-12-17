# Python Cheat Sheet

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
