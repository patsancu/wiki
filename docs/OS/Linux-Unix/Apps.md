#### Curl

get curl to set error code to error if it fails
```
curl --fail http://non_existing_domain.com || echo "curl failed"
curl --fail http://example.com && echo "curl succeeded!"
```
