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
