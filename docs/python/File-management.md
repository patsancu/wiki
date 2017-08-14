#### Hidden file/folder (linux-osx)

```python
def folder_is_not_hidden(p):
    is_hidden =  p.startswith('.') #linux-osx
    return not is_hidden
```

#### Check if file is folder
```python
os.path.isdir
```
#### Get current working directory
```python
previous_folder = os.getcwd()
```
#### Change to folder
```python
os.chdir("some/relative/or/absolute/path")
```
