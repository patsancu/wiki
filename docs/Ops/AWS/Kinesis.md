* [Python](../../python/snippets/Python-AWS.md#kinesis)
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
