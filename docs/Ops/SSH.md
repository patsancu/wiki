## Basics

### Create a new SSH Key
```bash
ssh-keygen -t rsa -C "your-email-address"
```
Be careful that you don't over-write your existing key for your personal account. Instead, when prompted, save the file as id_rsa_key. In my case, I've saved the file to ~/.ssh/id_rsa_other_key

## Check key fingerprint
### SHA-256
```
ssh-keygen -lf ~/.ssh/id_rsa.pub
1024 SHA256:19n6fkdz0qqmowiBy6XEaA87EuG/jgWUr44ZSBhJl6Y (DSA)
```
### MD5
```
ssh-keygen -E md5 -lf ~/.ssh/id_rsa.pub
2048 MD5:4d:5b:97:19:8c:fe:06:f0:29:e7:f5:96:77:cb:3c:71 (DSA)
```

## Passwordless login to machine via SSH
`ssh-keygen -t rsa (Optional)`

`ssh b@B mkdir -p ~/.ssh`

`cat ~/.ssh/id_rsa.pub | ssh b@B 'cat >> ~/.ssh/authorized_keys'`

`ssh b@B `(should not ask for pw anymore)

where B is the host and b is the user


## Execute graphical command in remote computer
```
ssh user@host "DISPLAY=:0 nohup vlc /path/to/media/movie.mp4"
```

## Disable SSH password authentication

edit ```/etc/ssh/sshd_config```
with contents
```
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
```
Restart daemon
```# /etc/init.d/sshd restart```

## Add private key
`ssh-add public_key_folder/public_key_file`

_Identity added: public_key_folder/public_key_file (public_key_folder/public_key_file)_

## SSH Config File
[instructions](goo.gl/Rdgf0s)
