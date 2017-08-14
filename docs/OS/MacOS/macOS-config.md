
### Mac OS X: ValueError: unknown locale: UTF-8 in Python

If you have faced the error on MacOS X, here's the quick fix - add these lines to your ~/.bash_profile:

```sh
$ export LC_ALL=en_US.UTF-8
$ export LANG=en_US.UTF-8
```


### Git completion
* download https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash
* add 
```
source ~/git-completion.bash
```
to ~/.bashrc

### Basic stuff that should be included, but it's not
`$ brew install coreutils`