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
