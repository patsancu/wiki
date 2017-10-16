### Home and end keys not working as expected
From [here](https://wiki.archlinux.org/index.php/Home_and_End_keys_not_working#Readline).
Insert/uncomment this
```
"\e[1~": beginning-of-line
"\e[4~": end-of-line
```
in the **/etc/inputrc** file

