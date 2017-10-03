### Mount local folder mount-dir to minikube's cluster "channels-folder" folder
```
minikube mount mount-dir:/channels-folder
```

### unset docker minikube stuff
```
eval $(minikube docker-env -u)
```

### set docker minikube stuff
```
eval $(minikube docker-env)
```
