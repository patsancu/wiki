### Find which process is using a specific port
```
PS C:\Users\MyUser> $port=8080
PS C:\Users\MyUser> Get-Process -Id (Get-NetTCPConnection -LocalPort $port).OwningProcess

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
    819      61  1005000     577488      58.92  23076   1 java
```
