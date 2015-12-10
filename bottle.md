# Bottle

This is part of my Bottle talk converted to Markdown.

---

# Bottle

* micro web-framework for Python

* one file (`bottle.py`), no external dependencies

* runs on top of WSGI ("whisky")

* supports Python 3

---

# Hello World

```python
from bottle import route, run

@route('/')
def index():
    return 'Hello World!'

run(host='localhost', port=8080)
```

---

# Routing

```python
@get('/food')
    
@post('/food')

@route('/food', method='GET')

@route('/food')
def food():
    if request.method == 'GET': 
        ...
```

---

# Templates

```python
from bottle import template

@get('/hello/<name>')
def hello(name='World'):
    return template('hello_template', name=name)
```

This renders `template.tpl` (from `bottle.TEMPLATE_PATH`).

---

# View Decorator

```python
@get('/hello/<name>')
@view('hello_template')
def hello(name='World'):
    return dict(name=name)
```

---

# Request / Response

```python
from bottle import request, response

@get('/food')
def food():
    cookie = request.get_cookie()
    ...
    response.content_type = 'text/html'
    response.charset = 'latin9'
```

---

# Query

http://moviedb/search?title=King+Kong

```python
@get('/search')
def movie_search():
    title = request.query.title
    if title == 'King Kong':
        ...
```

Default value is an empty string.
