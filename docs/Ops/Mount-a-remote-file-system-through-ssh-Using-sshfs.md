### Install
```
sudo apt-get install -y sshfs
```

### make sure the following condition is met. In the local system, type (as root)
Should return nothing
```
# sudo modprobe fuse
```

### create the mount point
```
$ sudo mkdir /mnt/remote
$ sudo chown [user-name]:[group-name] /mnt/remote/
```

### Add yourself to the fuse group
```
adduser [your-user] fuse
```

### switch to your user and mount the remote filesystem.
```
sshfs remote-user@remote.server:/remote/directory /mnt/remote/
```
### If you want to mount a directory other than the home directory, you can specify it after the colon. Actually, a generic sshfs command looks like this:
```
$ sshfs [user@]host:[dir] mountpoint [options]
```
### Unmount Your Directory
Try:
```
sudo umount /mnt/remote
```
or
```
fusermount -u mountpoint
```