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

### Get particular changeset for revision
```
hg log -p -r 678
```

### Get commits from a user
```
changeset:   324:5c78393273fe
branch:      some_branch
parent:      307:f7866d748366
user:        Some user <some.user@some.company.com>
date:        Thu Feb 22 13:32:50 2018 +0900
summary:     Some summary
```

```
hg log --user "<some.user@some.company.com>"
```
or
```
hg log --user "some.user"
```



### Aliases
in ~/.hgrc, under the [alias] section
#### clone from a fixed url without typing it each time
mclone = clone ssh://username@repository//srv/hg/repos/$1
