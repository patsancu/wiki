### Restart ssh daemon
```
sudo launchctl stop com.openssh.sshd
sudo launchctl start com.openssh.sshd
```
### How to Refresh Control Strip
```killall ControlStrip```
### Refresh touch bar
```pkill "Touch Bar agent"```

### Generate random string
```
openssl rand -base64 6
```
