### Get rabbimqadmin
* Go to [your_host:your_port/cli/rabbitmqadmin](your_host:your_port/cli/rabbitmqadmin)
* For example: if host is localhost and port is the default port (15672),
it would be downloaded from [here](http://localhost:15672/cli/rabbitmqadmin)

### Delete exchange on some vhost with credentials
```
sudo rabbitmqadmin delete exchange --username=sdp_user --password=sdp_password name=cmsToSdpExchangeQueue --vhost=managetv
```
