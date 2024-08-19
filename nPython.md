---
author: emchateau
tags: python
---

[**falcon**](https://github.com/falconry/falcon) — is a [high-performance Python framework](http://falconframework.org/index.html) for building cloud APIs. It encourages the REST architectural style, and tries to do as little as possible while remaining [highly effective](http://falconframework.org/index.html#Benefits).

Example:

```
import falcon
```

```
# Falcon follows the REST architectural style, meaning (among
# other things) that you think in terms of resources and state
# transitions, which map to HTTP verbs.
class ThingsResource(object):
    def on_get(self, req, resp):
        """Handles GET requests"""
        resp.status = falcon.HTTP_200  # This is the default status
        resp.body = ('\nTwo things awe me most, the starry sky '
                     'above me and the moral law within me.\n'
                     '\n'
                     '    ~ Immanuel Kant\n\n')
```

```
# falcon.API instances are callable WSGI apps
app = falcon.API()
```

```
# Resources are represented by long-lived class instances
things = ThingsResource()
```

```
# things will handle all requests to the '/things' URL path
app.add_route('/things', things)
```

------

[eve](https://github.com/nicolaiarocci/eve) — an open source Python REST API framework designed for human beings. It allows to effortlessly build and deploy highly customizable, fully featured RESTful Web Services.

Eve is powered by Flask, Redis, Cerberus, Events and offers support for both MongoDB and SQL backends.

```
from eve import Eve
```

```
app = Eve()
app.run()
```

The API is now live, ready to be consumed:

```
$ curl -i http://example.com/people
HTTP/1.1 200 OK
```

------

[**plotly.p**](https://github.com/plotly/plotly.py)**y** — an interactive, browser-based charting library for Python.

Screenshot:

[**cerberus**](https://github.com/nicolaiarocci/cerberus) — a lightweight and extensible data validation library for Python.

Example:

```
>>> v = Validator({'name': {'type': 'string'}})
>>> v.validate({'name': 'john doe'})
True
```

------

[**vispy**](https://github.com/vispy/vispy) *—* a high-performance interactive 2D/3D data visualization library for Python. [Example](https://github.com/vispy/vispy/blob/master/examples/demo/gloo/galaxy/galaxy.py):

[**Mimesis**](https://github.com/lk-geimfari/mimesis) is a fast and easier to use Python library for generate dummy data. These data are very useful when you need to bootstrap the database in the testing phase of your software. A great example of how you can use the library is a web applications on Flask or Django which need a data, such as users (email, username, name, surname etc.), posts (tags, text, title, publishing date and etc.) asf. The library use the JSON files as a datastore and doesn’t have any dependencies. The library offers more than 22 different data providers (from the personal to transport and not only).

Below you can see, how to generate fake paths using `Mimesis`:

```
>>> import mimesis
>>> person = mimesis.Personal(locale='en')

>>> person.full_name(gender='female')
'Antonetta Garrison'

>>> person.occupation()
'Backend Developer'

>>> templates = ['U_d', 'U-d', 'l_d', 'l-d']
>>> for template in templates:
...     person.username(template=template)

'Adders_1893'
'Abdel-1888'
'constructor_1884'
'chegre-2051'
```

------

[**expynent**](https://github.com/lk-geimfari/expynent) — a library that provides regex patterns for Python. If you hate to write regular expressions, then expynent can help you. Examples are below.

Just import the pattern that you wanna use:

```
import re
import expynent.patterns as expas
```

```
if re.match(expas.ZIP_CODE['RU'], '43134'):
    print('match')
else:
    print('not match')
```

```
# Output: 'not match'
```

also you can use compiled patterns:

```
from expynent.compiled import username
```

```
u = input('Enter username: ')
if username.match(u):
    print('valid')
else:
    print('invalid')
```

------

[**httpstat**](https://github.com/reorx/httpstat) *—* httpstat visualizes `curl` statistics in a way of beauty and clarity. httpstart written in Python.

[**pycallgraph**](https://github.com/gak/pycallgraph) — Python Call Graph is a Python module that creates [call graph](http://en.wikipedia.org/wiki/Call_graph)visualizations for Python applications.

[**pendulum**](https://github.com/sdispater/pendulum) *—* Python datetimes made easy.

[**furl**](https://github.com/gruns/furl) *—* a small Python library that makes manipulating URLs simple.

[**httpie**](https://github.com/jkbrzt/httpie) *—* a command line HTTP client. Its goal is to make CLI interaction with web services as human-friendly as possible. It provides a simple `http`command that allows for sending arbitrary HTTP requests using a simple and natural syntax, and displays colorized output. HTTPie can be used for testing, debugging, and generally interacting with HTTP servers.

[**bokeh**](https://github.com/bokeh/bokeh) — a Python interactive visualization library, enables beautiful and meaningful visual presentation of data in modern web browsers. With Bokeh, you can quickly and easily create interactive plots, dashboards, and data applications.