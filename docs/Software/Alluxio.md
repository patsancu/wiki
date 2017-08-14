### Refresh cache
```
root@alluxio-master-0:/opt/alluxio# alluxio fs ls -Rf /raw
```

### Remount folder
```
root@alluxio-master-0:/opt/alluxio# alluxio fs unmount /sushi
Unmounted /sushi
root@alluxio-master-0:/opt/alluxio# alluxio fs mount /sushi s3a://path-to-mount
```
