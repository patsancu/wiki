#!/usr/bin/env python
# -*- coding: utf-8 -*-

## S3
```python
import boto3

class S3wrapper(object):

    """Docstring for S3wrapper. """

    def __init__(self):
        # Create an S3 client
        session = boto3.Session(profile_name='some-profile')
        self.s3 = session.client('s3')


    def upload(self, file_name = 'tags', bucket_name = 'some-bucket',
            file_path = "some-path"):

        self.file_name = file_name
        self.bucket_name = bucket_name
        self.file_path = file_path
        self.key = file_path + file_name

        # Uploads the given file using a managed uploader, which will split up large
        # files automatically and pload parts in parallel.
        self.s3.upload_file(self.file_name, self.bucket_name, self.key)

```

### Kinesis
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
