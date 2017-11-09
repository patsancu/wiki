### Systemd

```
vim /etc/systemd/system/service_name.service
```

```
[Unit]
Description = making network connection up
After = network.target
[Service]
# ExecStart can point to any executable file
ExecStart = /root/scripts/conup.sh
[Install]
WantedBy = multi-user.target
```

#### Create executable script
```
vim /root/scripts/conup.sh;
chmod +x /root/scripts/conup.sh;
```

#### Enable service
```
# systemctl enable connection.service
```

#### Basic operations
```
# systemctl start connection.service
# systemctl stop connection.service
```

## Grub
### Change grub boot order
```
sudo vim /etc/default/grub
```
Change **GRUB_DEFAULT** to one of [number of entry (zero-based), 'Title'subindex]
Examples:
```
'Advanced options for Ubuntu>'3
2
```
Then, update the grub menu
```
sudo update-grub
```
Check the file `/boot/grub/grub.cfg` for reference

### Reinstall grub
* boot from livecd
* mount partition where grub was contained (usually OS's partition)
* ``` sudo tune2fs -L "partition_name" /dev/sdXX ( e.g.: /dev/sda6/ ) ```
* `sudo os-prober`
* `sudo grub-install --root-directory=/media/partition_name/ /dev/sda`
* reboot

### Create passwordless user programmatically
```
# useradd -m -c "Samwise the Brave" sam  -s /bin/bash
```
Creates user with home /home/sam and shell /bin/bash

### Find
```sh
# Search all files with .old extension and delete them:
find / -name "*.old" -exec /bin/rm {} \;
# Search all files with size > of 100 MB and delete them:
find / -size +100M -exec /bin/rm {} \;
# Recursively change the permissions of all directories
find . -type d -exec chmod 755 {} \;
```

### Top
* **W** writes config changes to .toprc
* **E** cycles through memory units in the total memory info

### Configure stuff
#### Change locale

With `/usr/bin/tzselect` you can check what is the timezone your computer should be using

```sudo dpkg-reconfigure tzdata```
If it doesn't work, try the following:

With that timezone, paste the timezone to **~/.profile** or **~/.bash_profile**, depending on your use case.
One of those files (it'll probably work with any sourced file at login) should have one line such as:
```
TZ='Europe/London'; export TZ
```
or just execute

#### Insert unicode characters
Hold down the shift and control keys while typing the letter u and the hex values of the Unicode character you wish to enter.
Example:
Hold control and shift and type U1F60F ‍😏



#### Add dictionaries to /usr/share/dict/

```
$ sudo apt-cache search --names-only swedish
$ sudo apt-get install wswedish
```

#### Mouse - Third button

```
sudo vim /usr/share/X11/xorg.conf.d/middle-mouse-button.conf
```
And paste this

```
Section "InputClass"
    Identifier "middle button emulation class"
    MatchIsPointer "on"
    Option "Emulate3Buttons" "on"
EndSection
```

or check this
[wiki ubuntu](https://wiki.ubuntu.com/X/Quirks# A2-button_Mice)

### Webcam
#### List video devices
* `v4l2-ctl --list-formats-ext`
* `v4l2-ctl --list-devices`

#### Find resolution of webcam
* `lsusb` list usb devices, get params of webcam
* `lsusb -s 003:074 -v | egrep "Width|Height"`


down vote
accepted
I had the same problem and managed to fix it by setting the defaults for both gvfs as well as xdg.

check defaults with:

### Change default app for magnet links
This probably will only work with gnome, kde and xfce


```
#Check currently available apps
xdg-mime query default x-scheme-handler/magnet
gvfs-mime --query x-scheme-handler/magnet
```

```
# Set new app, providing it's in /usr/share/applications/
xdg-mime default qBittorrent.desktop x-scheme-handler/magnet
gvfs-mime --set x-scheme-handler/magnet qBittorrent.desktop
```
### Notifications
```
notify-send -u critical "The potato finished cooking"
```

### Get OS version
```
uname -a
```
and
```
$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 16.04.2 LTS
Release:        16.04
Codename:       xenial
```

### Motion
#### Make folders accessible
```
sudo mkdir -p /var/run/motion; sudo chown -R $USER:$USER /var/run/motion;
sudo mkdir -p /etc/motion/; sudo chown -R $USER:$USER /etc/motion/;
sudo mkdir -p /var/log/motion/; sudo chown -R $USER:$USER /var/log/motion/;
```
#### Configuration file
`/etc/motion/motion.conf`

### Generate random chars
```shell
tr -c -d '0123456789abcdefghijklmnopqrstuvwxyz'  < /dev/urandom | dd bs=32 count=1 2>/dev/null; echo
```

### Monitor screen locking
```
exit_report(){
echo "$(date) Monitoring Terminated."
}
trap "exit_report; exit;" 0
lockmon() {
adddate() {
    while IFS= read ­r line; do
      echo "$(date) $line" | grep "boolean" | sed 's/   boolean true/Screen Locked/'
| sed 's/   boolean false/Screen Unlocked/'
    done
}
echo "$(date) Monitoring Started."
dbus­monitor ­­session "type='signal',interface='org.gnome.ScreenSaver'" | adddate
}
lockmon >> lock_screen.log
```

### How to fix ‘$MFTMirr does not match $MFT (record 0)’
* install ntfsprogs
* `sudo ntfsfix /dev/partitionName`
