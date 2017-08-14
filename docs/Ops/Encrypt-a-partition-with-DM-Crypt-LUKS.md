### Encrypt partition
```
$ sudo cryptsetup -y -v luksFormat /dev/xvdc 
WARNING!
========
This will overwrite data on /dev/xvdc irrevocably.

Are you sure? (Type uppercase yes): YES
Enter passphrase: 
Verify passphrase: 
Command successful.
```

### Create mapping
```
cryptsetup luksOpen /dev/xvdc backup2
```

### Format partition
```
pv -tpreb /dev/zero | dd of=/dev/mapper/backup2 bs=128M
mkfs.ext4 /dev/mapper/backup2
```

### Unmount
```
umount /backup2
cryptsetup luksClose backup2
```

### Mount
```
cryptsetup luksOpen /dev/xvdc backup2
mount /dev/mapper/backup2 /backup2
```
