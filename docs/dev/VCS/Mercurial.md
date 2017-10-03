#### Show changeset information by line for each file
`hg annotate -u`

### Delete untracked files, enabling purge extension
From (here)[https://stackoverflow.com/a/1212486]
#### Enable purge extension
Add to .hgrc this
```
[extensions]
purge =
```

#### Purge
```
hg purge
```
#### Delete untracked files, without purge extension
From (here)[https://stackoverflow.com/a/1212893]
```
hg st -un0 | xargs -0 rm
```

#### Forget tracked file

If file to forget is contained in .hgignore,

`$ hg forget _filename_`

#### Serve repo
`$ hg serve`
