### Install java
Download tar gz from [here](https://jdk.java.net/)
```
sudo mv openjdk-17.0.1_macos-x64_bin.tar.gz /Library/Java/JavaVirtualMachines/
cd /Library/Java/JavaVirtualMachines/
sudo tar -xzf openjdk-17.0.1_macos-x64_bin.tar.gz
sudo rm openjdk-17.0.1_macos-x64_bin.tar.gz
```

### Remap keys
From [superuser.com](https://superuser.com/a/1405422).

Run this to assign the mapping of tilde from paragraph (the one that was showing, but was not meant to be there)
```
hidutil property --set '{"UserKeyMapping":[{"HIDKeyboardModifierMappingSrc":0x700000064,"HIDKeyboardModifierMappingDst":0x700000035}]}'
```

For other keys, take a look [here](http://web.archive.org/web/20201211211934/https://developer.apple.com/library/archive/technotes/tn2450/_index.html)

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

### Increase keyboard repeat rate
From [here](https://apple.stackexchange.com/a/83923).

Run in terminal
```
defaults write -g InitialKeyRepeat -int 10 # normal minimum is 15 (225 ms)
defaults write -g KeyRepeat -int 1 # normal minimum is 2 (30 ms)
```
Important: Then logout for the changes to be applied
