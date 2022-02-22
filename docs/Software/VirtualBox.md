Install VBox additions!


### Port forward from the CLI (to allow to ssh into the virtual machine)
```
VBoxManage modifyvm "ubuntu20.04" --natpf1 "SSH,tcp,127.0.0.1,2522,10.0.2.15,22"
```

After that, just ssh into the machine with:

`ssh 127.0.0.1 -p 2522`

### Start headless machine CLI
VBoxManage startvm ubuservloc --type headless


### Get ip(v4) address of a vbox machine (named **ubuntu**)
Put *Bridged Adapter* in the Network Settings
```
VBoxManage guestproperty enumerate ubuntu | grep "Net.*V4.*IP"
```
### Add shared folder from ubuntu guest

`sudo mount -t vboxsf -o uid=$UID,gid=$(id -g) NAME_OF_SHARED_FOLDER_IN_VBOX FOLDER_IN_WHICH_TO_MOUNT`

### Share folder between ubuntu host and windows guest
* Add folder to shared folders in VBox settings
* In windows cli: ```net use <letra>: \\vboxsvr\shared_folder_name```


### Resize emulated hard drive

`user@pc :~$ VBoxManage modifyhd filename.vdi --resize 46080`


### Problems
#### SSH doesn't work
Try bridged mode
#### Premature end of data in tag VirtualBox line 2
* Looks like it was caused (in my case) because of the host machine running out of space
* Found [this](https://forums.virtualbox.org/viewtopic.php?f=8&t=26839#p326401) and some luck.
* backup the vbox file, and substitute the `/path/to/vm/win7/win7.vbox` file with the contents of `/path/to/vm/win7/win7.vbox`. Lost some progress, though.

