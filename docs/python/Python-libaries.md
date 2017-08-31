## Start simple python http server
2
```
$ python -m SimpleHTTPServer [port]
```
3
```
$ python3 -m http.server [port]
```


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

### DB
#### [dbms](https://pypi.python.org/pypi/dbms/1.1.1)
DataBases Made Simpler - Uniform interface for multiple adapters.
`$ pip install dbms`
```python
import dbms
db = dbms.connect.oracle('cms', 'cloud_PW', "CMSDB", "host") # cms cloud ingest
cur = db.cursor()
cur.execute('SELECT * FROM CMS_IRIS_DELIVERY where rownum < 5')
deliveries = cur.fetchall()
deliveries[rowNum]['name of the column']
deliveries[0]['id']
```

### Web
#### Python requests - HTTP for humans
[requests](https://github.com/kennethreitz/requests)
```python

headers = {'Content-Type': 'application/json'}
payload = {'longUrl': 'http://www.google.it'}
params={'key': 'GOOGLE_URL_SHORTENER_API_KEY'}
r = requests.post("https://www.googleapis.com/urlshortener/v1/url", data=json.dumps(payload), params=params, headers=headers)
r.json()
```
More elaborate [example](https://gist.github.com/patsancu/ef394b2ff6104ec9918a08af1fe7aaf3)
### Plot time series with mat
Install
```
pip install matplotlib numpy
```
```
import matplotlib.pyplot as plt
import datetime
import numpy as np

x = np.array([datetime.datetime(2013, 9, 28, i, 0) for i in range(24)])
y = np.random.randint(100, size=x.shape)

plt.plot(x,y)
plt.show()
```

#### Camelipsum
cli lore ipsum generator
```
pip install camelipsum
camelipsum.py NUMBER_OF_LINES
```
#### [Human name parsing](https://nameparser.readthedocs.io/en/latest/)
A simple Python module for parsing human names into their individual components.

#### [Faker](https://pypi.python.org/pypi/Faker)
Generate random data on the fly
```python
from faker import Factory
fake = Factory.create('fr_FR') # Localized names

for _ in range(0, 10):
   print fake.first_name()
   print fake.last_name()
```
More elaborate [example](https://gist.github.com/patsancu/416a1ba88294277d1d51e562f5fd97cf), with custom providers

#### [q](http://harelba.github.io/q/examples.html)
q - text as data

```
$ sudo apt-get install python-q-text-as-data
```
From this [data](https://gist.githubusercontent.com/patsancu/70df300b055f8c8501f19de287d8c213/raw/c15188bf6313cafd40576d2f01b57538d0c37fd8/Global%2520Superstore%2520Returns%25202016.csv)

**-H** flag ignores the header row, and **-d** flag instructs to read header fields separated by commas
```
$ q -H -d "," "SELECT Region FROM Global_Superstore_Returns_2016.csv" | head
Central US
Eastern Asia
Central US
Oceania
Oceania
Eastern Asia
Western Europe
Central US
Southern Europe
Eastern Asia
...
```
