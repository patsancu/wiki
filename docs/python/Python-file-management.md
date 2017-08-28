## Walk the tree
Returns a tuple consisting of:
* the folder being traversed
* a list of the files immediately beneath the folder being traversed
* a list of the folders immediately beneath the folder being traversed

### Quicktest
```python
import os

for item in os.walk("."):
    print item
```

### Traverse all the tree from the current folder
```
folder_tree_generator = os.walk(".")
for dirpath, dirnames, filenames in gen:

    if len(filenames) > 0:
        print "*" * 9
        print "Files contained in dirpath: {}".format(dirpath)
        print "*" * 9
        for filename in filenames:
            full_file_name = dirpath + os.path.sep + filename
            print "{} (full path is {})".format(filename, full_file_name)

    if len(dirnames) > 0:
        print "*" * 9
        print "Subdirs of dirpath: {}".format(dirpath)
        print "*" * 9
        for dirname in dirnames:
            full_folder_name = dirpath + os.path.sep + dirname
            print "{} (full path is: {})".format(dirname, full_folder_name)
            if os.path.isdir(full_folder_name):
                print "And it is!"
            else:
                print " But it's not"

```
