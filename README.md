# apirator
easily add simple http api to your django web app

### install
run `pip install apirator`

add `"apirator"` to `INSTALLED_APPS`

### create some api endpoints
in `foo/views.py` for example
```python
import apirator

@apirator.expose("foo", "POST")
def foo(foo=1, bar=2):
    return {"foo": foo, "bar": bar}

@apirator.expose("some/spam")
def spam():
    return {"spam": "eggs"}
```
and somewhere in urls configuration
```python
url(r'^api/(.+)$', apirator.router("foo.views"))
```

### use
```
$ http 127.0.0.1:8000/api/foo foo:=100
HTTP/1.0 200 OK
Content-Type: application/json
Date: Wed, 24 Jul 2013 12:13:27 GMT
Server: WSGIServer/0.1 Python/2.7.2

{
    "bar": 2,
    "foo": 100
}
```

```
$ http 127.0.0.1:8000/api/some/spam Accept:application/x-yaml
HTTP/1.0 200 OK
Content-Type: application/x-yaml
Date: Wed, 24 Jul 2013 12:12:02 GMT
Server: WSGIServer/0.1 Python/2.7.2

{spam: eggs}
```
