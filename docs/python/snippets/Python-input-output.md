### Read/write file
```python
import sys

# Read
with open('../first.js', 'r') as reading_file:
    remove_newlines = lambda x: x.replace('\n', '')
    lines = list(reading_file)
    formatted_lines = [remove_newlines(line) for line in lines]

# Write
with open('output_file', 'w') as output_file:
    for line in lines:
        output_file.write(line)
```
or
```
with open('output_file', 'w') as output_file:
    output_file.writelines(lines)
```

### Standard input/output read and write
```python
#### Write to stdout
import sys
sys.stdout.write(str(last_answer ))
```
or
```python
import sys
with sys.stdout as stdout:
    sdout.write(str(last_answer))
```
#### Read from stdin
```python
import sys
with sys.stdin as stdin:
    remove_newlines = lambda x: x.replace('\n', '')
    lines = [remove_newlines(line) for line in stdin]
```
or
```python
lines = sys.stdin.readlines()
```

### Remove trailing and beginning newlines from string
```python
remove_newlines = lambda x: x.trim('\r\n')
```

#### Gzip
##### read compressed file
```python
import gzip
with gzip.open('file.txt.gz', 'rb') as f:
    file_content = f.read()
```
##### compress file

```python
import gzip
content = "Lots of content here"
with gzip.open('file.txt.gz', 'wb') as f:
    f.write(content)
```

### Misc
#### Blink led of caps key
```python
import fcntl,os,time;
exec "fcntl.ioctl(os.open('/dev/console',os.O_NOCTTY),19250,%d);time.sleep(.5);"*2%(4,0)
```