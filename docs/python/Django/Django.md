* [Django login](https://gist.github.com/6ae87971e458c6853318ea421fc9a3e3)

### How to Reset Migrations
more info [here](https://simpleisbetterthancomplex.com/tutorial/2016/07/26/how-to-reset-migrations.html)
#### Remove the all migrations files within your project
```
find . -path "*/migrations/*.py" -not -name "__init__.py" -delete
find . -path "*/migrations/*.pyc"  -delete
```
### Drop the current database, or delete the db.sqlite3 if it is your case.
```
rm db.sqlite3
```
### Create the initial migrations and generate the database schema:
```
python manage.py makemigrations
python manage.py migrate
```
### Sendmail debug 

For debugging purposes you could setup a local smtpserver with this command:

```
python -m smtpd -n -c DebuggingServer localhost:1025
```

and adjust your mail settings accordingly:

```
EMAIL_HOST = 'localhost'
EMAIL_PORT = 1025
```

### Basics
```django-admin startproject mysite```

```python manage.py startapp polls ```

```python manage.py runserver ```

```python manage.py createsuperuser```

```python manage.py makemigrations```

```python manage.py migrate```

### Override model save method

```python
class Model(model.Model):
    image=models.ImageField(upload_to='folder')
    thumb=models.ImageField(upload_to='folder')
    description=models.CharField()


    def save(self, *args, **kwargs):
        if 'form' in kwargs:
            form=kwargs['form']
        else:
            form=None

        if self.pk is None and form is not None and 'image' in form.changed_data:
            small=rescale_image(self.image,width=100,height=100)
            self.image_small=SimpleUploadedFile(name,small_pic)
        super(Model, self).save(*args, **kwargs)
```