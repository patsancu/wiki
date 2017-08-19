## Reloading submodules in IPython
* From [here](https://stackoverflow.com/a/5399339)
* Edit the `~/.ipython/profile_default/ipython_config.py` file, and add:
```
c = get_config()
c.InteractiveShellApp.extensions = ['autoreload']
c.InteractiveShellApp.exec_lines = ['%autoreload 2']
```

