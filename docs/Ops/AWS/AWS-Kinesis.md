* [AWS-CLI](https://github.com/patsancu/wiki/wiki/AWS-Kinesis#aws-cli)
* [Python](https://github.com/patsancu/wiki/wiki/AWS-Kinesis#python)

### AWS CLI
**Warning** Before using check that you have properly set the `AWS_PROFILE` env variable to some profile existing in `~/.aws/credentials`, or comfortable using the aws default profile
as 
```shell
$ export AWS_PROFILE=analytics-storm
```

### Get kinesis decoded data
aws kinesis get-records --shard-iterator some_shard_hash --profile some-profile | jq ".Records [] .Data" | tr -d '
"' | base64 -d

```
$ aws kinesis describe-stream --stream-name stream_name --profile user2

{
    "StreamDescription": {
        "RetentionPeriodHours": 24, 
        "StreamName": "stream_name", 
        "Shards": [
            {
                "ShardId": "shardId-000000000000", 
                "HashKeyRange": {
                    "EndingHashKey": "whateverhashkey", 
                    "StartingHashKey": "0"
                }, 
                "SequenceNumberRange": {
                    "StartingSequenceNumber": "whateversequencenumber"
                }
            }, 
            {
                "ShardId": "shardId-000000000001", 
                "HashKeyRange": {
                    "EndingHashKey": "whateverhashke", 
                    "StartingHashKey": "whatevernumber"
                }, 
                "SequenceNumberRange": {
                    "StartingSequenceNumber": "somenumber"
                }
            }
        ], 
        "StreamARN": "arn:aws:kinesis:region:accountNumber:stream/stream_name", 
        "EnhancedMonitoring": [
            {
                "ShardLevelMetrics": []
            }
        ], 
        "StreamStatus": "ACTIVE"
    }
}
```

```
$ aws kinesis get-shard-iterator --stream-name tvmetrix --shard-id shardId-000000000001 --shard-iterator-type LATEST
{
    "ShardIterator": "whateversharditeratorwithnumberslettersandslashes "
}

```

get shard iterator for specific date (take into account the retention policy for your kinesis service)
```
$ aws kinesis get-shard-iterator --stream-name tvmetrix --shard-id shardId-000000000001 --shard-iterator-type AT_TIMESTAMP --timestamp "2017-05-25 08:00:00"
```

* shardId is one appearing in the describe-stream command above  

* for more info about shard-iterator-type
http://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax


```
$ aws kinesis get-records --shard-iterator whateversharditeratorwithnumberslettersandslashes --limit 1 --profile user2
{
    "Records": [
        {
            "Data": "some_encoded_data", 
            "PartitionKey": "some_numbers", 
            "ApproximateArrivalTimestamp": 1490964900.808, 
            "SequenceNumber": "some_very_long_number"
        }
    ], 
    "NextShardIterator": "some_sequence_of_letters_and_numbers_and_slashes", 
    "MillisBehindLatest": 0
}

```


### Python
```python
import json
import time
from boto import kinesis

STREAM_NAME="stream_name"
STREAM_REGION="stream_region"

# Kinesis initialization and information
kinesis = kinesis.connect_to_region(STREAM_REGION)
kinesis.describe_stream(STREAM_NAME)

# Put data
c = open('sample_data.json').read()
print "********************"
print "Will try to send data: "
print c
kinesis.put_record(STREAM_NAME, c, "partitonkey")
print "Data sent"
print "********************"

# Read data
print "********************"
print "Will try to read data"
shard_id = 'shardId-00000000001'
shard_it = kinesis.get_shard_iterator(STREAM_NAME, shard_id, "LATEST")["ShardIterator"]
while True:
    out = kinesis.get_records(shard_it, limit=2)
    shard_it = out['NextShardIterator']
    print out
    time.sleep(0.2)
print "********************"
```

```python
import sys
from time import strftime, gmtime
import logging
import json

# Boto stuff
from boto import kinesis
import boto3
import botocore

max_records = 20000

logging.basicConfig(level=logging.ERROR)

STREAM_NAME="STREAM_NAME"
STREAM_REGION="us-east-1"

session = boto3.Session(profile_name='some-profile')
client = session.client(service_name='kinesis')

if len(sys.argv) > 1:
    timestamp = sys.argv[1]
else:
    timestamp = "2017-07-17T17:00:00.000-00:00"

# Get shard iterator dict
shardId="shardId-000000000001"
d = client.get_shard_iterator(ShardIteratorType="AT_TIMESTAMP", ShardId=shardId, Timestamp=timestamp, StreamName='tvmetrix')
iterator = d.get('ShardIterator')
nextIterator = iterator

# Debug stuff files
file_name_debug = "debug_file_{}.debug".format(strftime("%Y-%m-%d_%H-%M-%S", gmtime()))
debug_file = open(file_name_debug, 'w')
file_name_data = "data_file_{}.log".format(strftime("%Y-%m-%d_%H-%M-%S", gmtime()))
data_file = open(file_name_data, 'w')
print "Debug file will be: {}".format(file_name_debug)
print "Data file will be: {}".format(file_name_data)

counter = 0
while counter < max_records:
    try:
        response = client.get_records(ShardIterator=nextIterator, Limit=20)
        logging.debug(response)
        print response
        debug_file.write(str(response) + '\n')
        records = response.get('Records')
        nextIterator = response.get("NextShardIterator")
        print "There are {} records".format(len(records))
        counter += len(records)
        for record in records:
            print "*" * 10
            print "Record"
            print "-" * 10
            data = record.get('Data')
            tokens = data.split('\n')
            for token in tokens:
                data_dict = json.loads(token)
                ### read stuff
    except ValueError as valueError:
        print valueError
    except botocore.exceptions.ClientError as ce:
        print "*" * 6, "WARNING", "*" * 6
        print ce
        print "Limit exceeded"
        print "*" * 6, "WARNING", "*" * 6
        break
debug_file.close()
data_file.close()
```