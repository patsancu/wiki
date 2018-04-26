### Start simple http server python

```
$ python -m SimpleHTTPServer [port]
```

```
$ python3 -m http.server [port]
```

### Progress bar with tdqm

```python
from tqdm
```


trange(i) is a special optimised instance of tqdm(range(i)):
```python
# worse
for i in tqdm(xrange(10**6)):
    pass

# better (according to docs)
for i in trange(10**6):
    pass
```

##### Manual
```python
with tqdm(total=100) as pbar:
    for i in range(10):
        pbar.update(10)
```
