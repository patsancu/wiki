### Currying functions
Function that returns a function
#### With lambdas
```python
import math
def make_cylinder_volume_fun(r):
    return lambda h: math.pi * r * r * h
```
#### Without lambdas
```python
import math
def make_cylinder_volume_func(r):
    def volume(h):
        return math.pi * r * r * h
    return volume
```
