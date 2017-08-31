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
