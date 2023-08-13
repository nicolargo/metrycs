# Metrycs

Maage metrics through this Python lib.

Example:

```
from metrics import Metric

foo = Metric()
foo.add(80)
foo.last() # return 80
foo.add(82)
foo.last() # return 82
foo.get() # return [80, 82]
foo.reset()
foo.last() # return None

rate = Metric(rate=True)
foo.add(80)
foo.last() # return None
foo.add(82)
foor.last() # return 2
foor.add(86)
foo.last() # return 4
foo.get() # return [2, 4]
```
