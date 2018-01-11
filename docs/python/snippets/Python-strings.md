[Source](https://pyformat.info/#simple)

### Positional args
```
'{1} {0}'.format('one', 'two')
```

### Keyword args
```
'{first} {last}'.format(first='Hodor', last='Hodor!')
```

### Getitem
```
person = {'first': 'Jean-Luc', 'last': 'Picard'}
'{p[first]} {p[last]}'.format(p=person)
```
### Value conversion
```
class Data(object):

    def __str__(self):
        return 'str'

    def __repr__(self):
        return 'repr'

'{0!s} {0!r}'.format(Data())
```

### Padding and aligning strings

where _ is the padding characer. default is space
#### align right
```
'{:_>10}'.format('test')
______test
```

#### align left
```
'{:10}'.format('test')
```


#### center align
```
'{:^10}'.format('test')
```

### truncate string
```
'{:.5}'.format('xylophone')
```

### Date time
```
'{:%Y-%m-%d %H:%M}'.format(datetime(2001, 2, 3, 4, 5))
```
