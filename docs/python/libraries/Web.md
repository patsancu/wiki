### Posting to endpoint
#### With requests - HTTP for humans
[requests](https://github.com/kennethreitz/requests).
Example
```python
import requests
import json

gist_token = os.getenv("GITHUB_GIST_TOKEN")
github_root_api = "https://api.github.com"
gist_post_endpoint = "/gists"
gist_post_url = github_root_api + gist_post_endpoint

# Format headers with token
headers = {'Authorization': 'token {}'.format(gist_token)}
# Create data dict, according to https://developer.github.com/v3/gists/#create-a-gist
gist_dict = {"description": "Posted with python requests", "public": False, "files": {"some_file_name.txt": {"content": "print 'hello world'"}}}
# Put the dict data into json
json_data = json.dumps(gist_dict)
# Post data with a request, include token header
response = requests.post(gist_post_url, headers=headers, data=json_data)

# Not needed, check the results
response_json = json.loads(response.content)
```


#### With urllib, urllib2

```python
import os
import urllib
import urllib2
import json

gist_token = os.getenv("GITHUB_GIST_TOKEN")
access_url = "https://api.github.com/gists"

headers = {'Authorization': 'token {}'.format(gist_token)}

data = {"description": "some gist", "public": False, "files": {"some_file_name.txt": {"content": "print 'hello world'"}}}

json_data = json.dumps(data)
req = urllib2.Request(access_url, json_data, headers)
response = urllib2.urlopen(req)
the_page = response.read()
```


### Start simple python http server
2
```
$ python -m SimpleHTTPServer [port]
```
3
```
$ python3 -m http.server [port]
```

### Open page at browser
import webbrowser
webbrowser.open_new('http://www.python.org/')
#more info at: https://docs.python.org/3.4/library/webbrowser.html
