### Javascript: Show password for websites which remember your login details
```
$x('//input[@type="password"]')[0].setAttribute("type", "text")
```

### Javascript play with xpath
https://gist.github.com/patsancu/7d19c0db94d624e185de9ca748c374ae


### Use Tor with Chromium

* Install tor and polipo
* In /etc/polipo/config uncomment lines:
```
socksParentProxy = "localhost:9050"
socksProxyType = socks5
```
* Use chromium

`chromium-browser --proxy-server="127.0.0.1:8118;https=127.0.0.1:8118;socks=127.0.0.1:8118;sock4=127.0.0.1:8118;sock5=127.0.0.1:8118,ftp=127.0.0.1:8118" --incognito check.torproject.org`
