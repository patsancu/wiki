### Get process using port
get-Process -Id (Get-NetTCPConnection -LocalPort 8080).OwningProcess
