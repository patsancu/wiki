### AWS endpoints
[List of AWS endpoints for service](http://docs.aws.amazon.com/general/latest/gr/rande.html)

### Block s3
* For some reason, it blocks requests from aws java sdk, but not for the ones made from aws cli.
* block the following host (it works with /etc/hosts, but it's *NOT SAFE*):
```
SOME_BUCKET_NAME.s3.amazonaws.com
```
