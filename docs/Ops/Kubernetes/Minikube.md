### Mount local folder mount-dir to minikube's cluster "channels-folder" folder
```
minikube mount mount-dir:/channels-folder
```

This will mount the local folder mount-dir at the path /channels-folder within the Hyperkit VM. The process remains active so you should leave this terminal alone.

### unset docker minikube stuff
```
eval $(minikube docker-env -u)
```

### set docker minikube stuff
```
eval $(minikube docker-env)
```
