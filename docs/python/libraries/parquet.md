### Read parquet file

`$ pip install parquet`

Writes parquet file contents in plain text to "output" file.
```python
import parquet
import json

jsons = []
outputFile = open('output', 'w')
with open("/home/patrick/0_0_0.parquet") as input_file:
    labels = ['hour_timestamp', 'region','class', 'appVersion', 'session_count']
    for row in parquet.DictReader(input_file, columns=labels):
        jsonObj = json.loads(json.dumps(row))
        jsons.append(jsonObj)
        for label in labels:
            outputFile.write(str(jsonObj[label]))
            outputFile.write(',')
            outputFile.write("\n")
            outputFile.close()
```


