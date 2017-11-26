### Needed config
* Install and configure a user to use aws cli
* Create AIM
More info [here](../AWS/Cli-Config.md)

### Create aws machine
creates a instance (default t2.micro)
```
docker-machine create --driver amazonec2 machine_name --amazonec2-region "us-east-1"
```

### Log into the machine
```
docker-machine ssh machine_name
```
or, get the path to the ssh key
```
docker-machine inspect --format='{{prettyjson .Driver.SSHKeyPath}}' aws01
```
and log with it:
```
ssh -i path_to_key public_dns_name
```

### Get instance id
```
docker-machine inspect --format='{{prettyjson .Driver.InstanceId}}' machine_name
```


