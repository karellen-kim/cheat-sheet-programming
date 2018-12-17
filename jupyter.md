# Jupyter Cheat Sheet

## Render
#### Data Rendering
```python
from IPython.display import HTML
from json2html import *

HTML(json2html.convert(data))
```
#### Screen Width
```python
from IPython.core.display import display, HTML

display(HTML("<style>.container { width:100% !important; }</style>"))
```
