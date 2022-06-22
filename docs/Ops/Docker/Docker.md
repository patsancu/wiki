### Use docker remote host via ssh

If a machine is accessible via ssh, this should work

```
export DOCKER_HOST=ssh://username@host:port
```

```
2022-06-22 14:53:42 in some-folder on  master [⇡!?]
➜ export DOCKER_HOST=ssh://someUser@127.0.0.1:9191
2022-06-22 14:53:44 in some-folder on  master [⇡!?] on 🐳 v20.10.7 (someUser@127.0.0.1:9191)
➜ docker images
REPOSITORY                                                   TAG                                        IMAGE ID       CREATED         SIZE
gcr.io/distroless/java                                       11-nonroot                                 1f9a30825753   52 years ago    210MB
```


### Delete exited containers
```
docker rm -v $(docker ps -a -q -f status=exited)
```

### Remove dangling images
```
$ docker rmi $(docker images -f "dangling=true" -q)
```

### Create user
#### Simple way (alpine)
```
RUN addgroup groupname && adduser -s /bin/bash -D -G groupname username

```
#### Complex way
```

# User config
ENV UID="1000" \
    UNAME="developer" \
    GID="1000" \
    GNAME="developer" \
    SHELL="/bin/bash" \
    UHOME=/home/developer

# User creation stuff
RUN apk --no-cache add sudo \
    && mkdir -p "${UHOME}" \
    && chown "${UID}":"${GID}" "${UHOME}" \
    && echo "${UNAME}:x:${UID}:${GID}:${UNAME},,,:${UHOME}:${SHELL}" \
    >> /etc/passwd \
    && echo "${UNAME}::17032:0:99999:7:::" >> /etc/shadow \
    && echo "${UNAME} ALL=(ALL) NOPASSWD: ALL" > "/etc/sudoers.d/${UNAME}" \
    && chmod 0440 "/etc/sudoers.d/${UNAME}" \
    && echo "${GNAME}:x:${GID}:${UNAME}" \
    >> /etc/group

USER developer
WORKDIR $UHOME
ENV ANT_HOME $UHOME/process-tools/bin
```

### Private registry
* Run private docker registry. *Only* works in local, because there are no installed certs.
* Forwards container port 5000 to localhost's 8888
```
docker run -d -p 8888:5000 registry:2
```

### Docker commit
* Commit a new image with name commit, tag test, author Joe Bloggs, comment.
```
docker commit -a "Joe Bloggs" -m "Comment" RUNNING_IMAGE_ID commit:test
```
* Commit a new image with name svendowideit/testimage, tag version4, with changes: a CMD command and an EXPOSE one.
```
docker commit --change='CMD ["apachectl", "-DFOREGROUND"]' -c "EXPOSE 80" c3f279d17e0a  svendowideit/testimage:version4
```

### Get docker container's OS
* Info [here](https://serverfault.com/questions/805389/)
**DO NOT USE**
* `uname -a`
* uname will tell you the kernel that's running, which is the host OS kernel (containers, unlike VM's, share the same kernel).

#### Not perfect, but still...

```
### ubuntu
lsb_release -sirc
## centos
cat /etc/issue
### others
cat /etc/os-release
```
### Point to local machine from within container (macos)
```
docker run -p 8081 -e REDIS_HOST=host.docker.internal -e REDIS_PORT=6379 --rm rediscommander/redis-commander
```

### docker with minikube ip
```
echo "$(minikube ip)\t\t redis" | sudo tee -a /etc/hosts
```
