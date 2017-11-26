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
