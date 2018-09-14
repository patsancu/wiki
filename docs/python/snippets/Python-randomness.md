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
