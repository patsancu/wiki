### Get list of info aobut EBS volumes
```
aws ec2 describe-volumes --profile profile-name
```

### Get public dns name for machines in us-east-1 region
```
aws ec2 --region us-east-1 describe-instances --query 'Reservations[*].Instances[*].[PublicDnsName]' | grep -v "\[\|\]" | tr -d ' ' | tr -d '"'
```
