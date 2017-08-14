### UnicodeEncodeError: 'ascii' codec can't encode character
Shows when displaying a not encoded string in Python2.7+ (with 

```python
from django.utils.encoding import python_2_unicode_compatible
[...]
#define unicode method
def __unicode__(self):
   return ",".join([str(self.tipo_lugar),self.nombre, str(self.autor)])
```

