#### Generate gmail password for mutt
https://security.google.com/settings/security/apppasswords

#### Send email with attachment
```
$ mutt -s "Test from mutt" user@mail.com < /tmp/message.txt -a /tmp/file.jpg
```

#### .muttrc Gmail configuration
```
set ssl_starttls=yes
set ssl_force_tls=yes
set from='gmail_email_address'
set realname='Real Name'
set folder = imaps://imap.gmail.com/
set spoolfile = imaps://imap.gmail.com/INBOX
set postponed="imaps://imap.gmail.com/[Gmail]/Drafts"
set header_cache = "~/.mutt/cache/headers"
set message_cachedir = "~/.mutt/cache/bodies"
set certificate_file = "~/.mutt/certificates"
set imap_user = 'gmail_email_address'
set imap_pass = 'gmail_generated_password_for_insecure_apps'
set smtp_url = "smtps://'gmail_email_address'@smtp.gmail.com:465/"
set smtp_pass = 'gmail_generated_password_for_insecure_apps'
set record=""
set move = no
set imap_keepalive = 900
```