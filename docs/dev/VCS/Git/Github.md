### Get single file from github repo
```
url=https://github.com/prometheus/alertmanager/blob/master/README.md
rawUrl=`echo "$1" | sed "s/github/raw.githubusercontent/g" | sed "s/blob\///"`; wget $rawUrl; 
wget $rawUrl
```

### Cloning and forking 

#### Updating a forked repo from github
http://stackoverflow.com/questions/7244321/how-do-i-update-a-github-forked-repository
```
base: mine 
head fork: original
```

### Change repo remote url from http to ssh
change url in .git/config from:
```
https://github.com/USERNAME/OTHERREPOSITORY.git
```
to
```
git@github.com:USERNAME/OTHERREPOSITORY.git
```


#### Having already cloned the repo, but not forked it

* Ideally, create the repo with: https://developer.github.com/v3/repos/#create
* If not, create it via forking the repo.
* In this example, it will be https://github.com/JAremko/alpine-vim
* Forking it will result in https://github.com/octosh/alpine-vim
* In your local, add a new remote to your fork; then fetch it, and push your changes up to it
```
    git remote add my-fork https://github.com/octosh/alpine-vim
    git fetch my-fork
    git push my-fork master
```

#### Traditionally
Otherwise, if you want to follow convention:

1. Fork their repo on Github
2. In your local, rename your origin remote to upstream

    git remote rename origin upstream

3. Add a new origin

    git remote add origin git@github...my-fork

4. Fetch & push

    git fetch origin
    git push origin
