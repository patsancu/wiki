### Needed config
* Install and configure a user to use aws cli
* Create AIM
* More info [here](../AWS/Cli-Config.md)

### Create aws machine
creates a instance (default t2.micro)
```
docker-machine create --driver amazonec2 --amazonec2-region "us-east-1" machine_name
```

### Get env vars to connect the Docker Client to the Docker Engine
```
docker-machine env MACHINE_NAME
```

### Log into the machine
```
docker-machine ssh machine_name
```
or, get the path to the ssh key and log with it:
```
MACHINE_USERNAME=ubuntu;
IP_ADDRESS=$(docker-machine inspect --format='{{prettyjson .Driver.IPAddress}}' docker-machine-01 | tr -d '"');
SSH_DOCKER_MACHINE_KEYPATH=$(docker-machine inspect --format='{{prettyjson .Driver.SSHKeyPath}}' docker-machine-01 | tr -d '"');
ssh -i $SSH_DOCKER_MACHINE_KEYPATH $MACHINE_USERNAME@$IP_ADDRESS
```

### Get instance id
```
docker-machine inspect --format='{{prettyjson .Driver.InstanceId}}' machine_name
```
