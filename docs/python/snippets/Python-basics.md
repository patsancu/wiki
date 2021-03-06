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

### Flatten list of lists (only one level of nesting)
```python
import itertools
list2d = [[1,2,3],[4,5,6], [7], [8,9]]
list(itertools.chain.from_iterable(list2d))
>>> [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Flatten json

```python
def flattenjson( b, delim ):
    val = {}
    for i in b.keys():
        if isinstance( b[i], dict ):
            get = flattenjson( b[i], delim )
            for j in get.keys():
                val[ i + delim + j ] = get[j]
        else:
            val[i] = b[i]

    return val
```
#### Strip punctuation of string
```python
s.translate(None, string.punctuation)
```

### Flatten list of lists (only one level of nesting)
```python
import itertools
list2d = [[1,2,3],[4,5,6], [7], [8,9]]
list(itertools.chain.from_iterable(list2d))
>>> [1, 2, 3, 4, 5, 6, 7, 8, 9]
```


### Misc
#### Dissassemble python code

```python
def myfunc(alist):
    return len(alist)
>>> import dis
>>> dis.dis(my_func)
 dis.dis(myfunc)
  2           0 LOAD_GLOBAL              0 (len)
              3 LOAD_FAST                0 (alist)
              6 CALL_FUNCTION            1
              9 RETURN_VALUE
```

### Python program from CLI
```
#!/usr/bin/env bash
echo "somebody" | python -c "
import sys
for line in sys.stdin:
    print line
"
```

or

```
#!/usr/bin/env bash

echo "somebody" | python -c "
import fileinput
for line in fileinput.input():
        print line
"
somebody
```

### Generator
#### Take n elements from a generator

```python
n = 5
array = (x**2 for x in xrange(10))
smaller = itertools.islice(array, n) ## get a new generator
list(smaller) ## or a list
>>> [0, 1, 4, 9, 16]
```

### Json
#### Read json ignoring trailing commas
```python
import json
from jsoncomment import JsonComment

with open(filename) as data_file:
    parser = JsonComment(json)
    data = parser.load(data_file)
```

#### Flatten json
```python
def flattenjson( b, delim ):
    val = {}
    for i in b.keys():
        if isinstance( b[i], dict ):
            get = flattenjson( b[i], delim )
            for j in get.keys():
                val[ i + delim + j ] = get[j]
        else:
            val[i] = b[i]

    return val
```
