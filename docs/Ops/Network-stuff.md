### Set static IP
Edit the following file
```
/etc/dhcpcd.conf
```
with the following contents (adapted of course)
```
interface eth0

static ip_address=192.168.0.10/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1

interface wlan0

static ip_address=192.168.0.200/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1

```
### Get listening ports without netstat
```
ss -aut
```

### Scan ip range
```
sudo nmap -sP 192.168.*.*
```

### Forward packets
```
echo 1 > /proc/sys/net/ipv4/ip_forward
```
### OpenVPN automatic login
* Create file with username in the first line and password in the second, i.e. auth.txt
* Change the line
```
auth-user-pass

```
to
```
auth-user-pass auth.txt
```
in the .ovpn file
* (Optional) Change the line in all the ovpn files with:
```
sed -i 's/auth-user-pass/#&1\n&1 auth.txt/' vpn_file.ovpn
```
