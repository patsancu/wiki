### Assign key to reindent

You can find it in Edit → Line → Reindent, but it does not have a shortcut by default. You can add a shortcut by going to the menu Preferences → Keybindings → User, then add there:

```
{ "keys": ["f12"], "command": "reindent"}   
(example of using the F12 key for that functionality)
```

The config files use JSON-syntax, so these curly braces have to be placed comma-separated in the square-brackets that are there by default. If you dont have any other key-bindings already, then your whole Keybindings → User file would look like this, of course:

```
[
{ "keys": ["Ctrl+i"], "command": "reindent"}   
]
```

### Sublime text code completion config path
```
~/.config/sublime-text-2/Packages/SublimeCodeIntel
```

### Regex replace
```
(?:def (?<funcName>.*)(?<patata>\())
def $1(self, 
```
#### before
```def curateText(name):```
#### after
```def curateText(self, name):```

