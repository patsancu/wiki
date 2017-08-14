* [Basics](https://github.com/patsancu/wiki/wiki/Python-basics)
* [Input/Output](https://github.com/patsancu/wiki/wiki/Python-input-output)
* [File management](https://github.com/patsancu/wiki/wiki/File-management)
* [HTTP verbs/curl-like stuff](https://github.com/patsancu/wiki/wiki/HTTP-Verbs-and-curl-like-stuff)
* [Generators](https://gist.github.com/patsancu/416a1ba88294277d1d51e562f5fd97cf)
* [Email function](https://gist.github.com/patsancu/262b7a492e225fc3471024753781a219) or [email CLI](https://gist.github.com/patsancu/ae20beaac4a8d8783a121b47d4181a18)
* [CLI option parser](https://gist.github.com/patsancu/ae20beaac4a8d8783a121b47d4181a18)
* [Date arithmetic](https://gist.github.com/patsancu/beb0f888fdcb52fd70137a1b2905a306)
* [Misc](https://github.com/patsancu/wiki/wiki/Misc)
* [csv to json](https://gist.github.com/patsancu/0aa0c518f0d0e6ea7bf99416a741aa55)


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