### Generate keys
```
$ gpg --gen-key
```

### Encryption
```
$ gpg --encrypt --sign --armor -r recipient_email -r my@email.com file_to_encrypt
```
### Decrypt
```
$ gpg --output path/to/decrypted/file file_to_encrypt.asc
```


### Create subkey
#### Backup files
```
$ umask 077; tar -cf $HOME/gnupg-backup.tar -C $HOME .gnupg
```

#### Find key and edit it
gpg --list-keys yourname
gpg --edit-key 
gpg> addkey
### Choose the "RSA (sign only)"
### entropy stuff
gpg> save