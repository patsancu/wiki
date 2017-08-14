### Delete exited containers
```
docker rm -v $(docker ps -a -q -f status=exited)
```

### Remove dangling images
```
$ docker rmi $(docker images -f "dangling=true" -q)
```