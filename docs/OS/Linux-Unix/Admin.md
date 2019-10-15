### Add user to group
```
# Add user `some_user` to `docker` group
sudo usermod -aG docker some_user
```

### Connect to hidden wireless network
edit /etc/wpa_supplicant/wpa_supplicant.conf
with something like this:
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

# Important part below
network={
    scan_ssid=1
    ssid="NAME"
    psk="password"
}
```
