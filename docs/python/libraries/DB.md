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
