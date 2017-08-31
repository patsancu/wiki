#### Camelipsum
cli lore ipsum generator
```
pip install camelipsum
camelipsum.py NUMBER_OF_LINES
```

#### [Human name parsing](https://nameparser.readthedocs.io/en/latest/)
A simple Python module for parsing human names into their individual components.

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


