# Python Solutions

#### Python Singleton
There are many ways of implementing singleton in python3.7. Here's one that worked for me:

```python
from __future__ import annotations
from typing import Optional

class SingletonMeta(type):
    _instance: Optional[Singleton] = None

    def __call__(self) -> Singleton:
        if self._instance is None:
            self._instance = super().__call__()
        return self._instance


class HybridInstances(metaclass=SingletonMeta):
    def __init__(self, att2):
        self._att1 = []
        self._att2 = att2
    def some_method(self, asd):
      # Do some stuff
      pass
```

I'm not sure if it is the best way but it's the one that worked for me. Take into account that this solution only works for Python 3.7 and not prior version. For other ways of implementing python singletons read [Stackoverflow post](https://stackoverflow.com/questions/6760685/creating-a-singleton-in-python) or this other [post](https://python-3-patterns-idioms-test.readthedocs.io/en/latest/Singleton.html) 

