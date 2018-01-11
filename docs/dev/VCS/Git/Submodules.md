## [Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
```
git submodule add submodule-url
```

```
git submodule init
git submodule update
```

```
git clone --recurse-submodules repo-with-submodules-url
```

Update a submodule. Go inside a submodule and
```
git fetch
git merge origin/master
```
Or, simply:
```
git submodule update --remote submodule-name
```
If the needed submodule branch is not master:
```
git config -f .gitmodules submodule.DbConnector.branch stable
```
(The -f .gitmodules makes the change persistent)

Configuration to pretty print submodule changes
```
git config --global diff.submodule log
```

* Push to the remotes to make sure they're externally available and then try this push again

```
git push --recurse-submodules=on-demand
```
* Let the on-demand option be the default
```
git config push.recurseSubmodules on-demand
```
