### Create matrix
#### Create matrix of None
```python
A = [[ None for _ in xrange(M)] for _ in xrange(N)]
```
#### Create matrix of random numbers
```python
import random
A = [[ random.random() for _ in xrange(M)] for _ in xrange(N)]
```

#### Generator for lists of M random elements
```python
import random
A = ([ random.random() for _ in xrange(M)] for _ in iter(int, 1))
for i in A:
    print i
    sleep(0.2)
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

### Permutations
From [python lexical analysis docs](https://docs.python.org/3/reference/lexical_analysis.html)

```python
def perm(l):
    # Compute the list of all permutations of l
    if len(l) <= 1:
        return [l]
    r = []
    for i in range(len(l)):
         s = l[:i] + l[i+1:]
         p = perm(s)
         for x in p:
             r.append(l[i:i+1] + x)
    return r
```
