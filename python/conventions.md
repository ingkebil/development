# Conventions

First some general stuff. We use Python 3.6+. We encourage the use of type annotations even if it doesn't cover 100% of your functions. We encourage using the new format strings:

```python
name = 'Paul Anderson'
string = f"Hello {name}!"
```

## Folders/packages

A common folder structure for a Python projects looks like:

```
myPackage
├── __init__.py
├── exc.py                   <-- custom exceptions
├── cli/
│   ├── __init__.py
│   ├── base.py              <-- read app config, set up logging, import subcommands
│   └── subcommand.py
├── server/
│   ├── templates/
│   ├── __init__.py
│   └── app.py
└── store/
    ├── __init__.py
    ├── api.py
    └── models.py            <-- database models, DB schema definitions
```

The important thing to note is how functionality is split up across the project. It's common that the same or similar functionality is available through many interfaces. For example it might be possible to list all recently added records in a database:

- on the command line printed to the console
- over HTTP through a JSON API
- programmatically through accessing an API class

The `cli` package contains all command line related code and nothing more. Logic such as how to handle and report error messages to the user goes here. **Avoid** putting logic in CLI modules that directly handle things like manually filtering database queries. More generally think [DRY][dry] - avoid doing the same thing manually in both CLI and server code. **Always** go through your Python API to interact with e.g. the database.

## Command line interface (CLI)

We highly recommend implementing the CLI using [Click][click]. It has a very nice Pythonic interface for defining your interface and comes with helpers for reading input, printing colorful output, etc.

## Logging

We recommend using [Coloredlogs][coloredlogs] which makes it _super easy_ to enable logging for your package:

```python
import coloredlogs
coloredlogs.install(level=log_level)
```

## Server

If it makes sense, a general app exposes a JSON API over HTTP(S). This API can then be consumed by a client side web app. Sometimes it makes sense to provide a the web interface as part of the Python package and other times it will be consumed by the central web portal interface.

We write our web servers in [Flask][flask] which shares many similarities with [Click][click]. To connect to the store/backend we use [Flask-Alchy][flask-alchy].

We generally configure servers using environment variables which is a flexible and well supported option.

## Store

We start out with a SQL backend unless our needs require something different. We run all production SQL databases in MySQL. For development and testing it's often nice to work against a SQLite copy. For that reason and to make database interactions more pythonic, we make heavy use of the SQLAlchemy-wrapper, [Alchy][alchy].

> Note that Alchy has been **deprecated** in favor of SQLService, however, we have not been able to successfully set up the latter package with Flask to work with the request context which is why we stay with Alchy for now.

### Store API

Alchy shares the database connection with associated model classes. This allows you to perform queries by simply importing them like:

```python
# ... connect to database
from trailblazer.store import models

for record in models.Sample.query:
    print(record)
```

However, this feels a little magic and it's not so clear how the model exactly got access to that database connection. Therefore, we advocate explicitly passing around an API class holding the database connection.

```python
from . import models

class DatabaseAPI():
    Sample = models.Sample

    def __init__(self, uri):
        self.connect(uri)

    def samples(self):
        return self.Sample.query
```

## Exceptions

We recommend that you base all your custom exceptions on a app-specific exception class. This way, 3-party packages that depend on it easily catch all exceptions from your package if they so choose.

```python
class TrailblazerError(Exception):
    def __init__(self, message):
        self.message = message

class MissingFileError(TrailblazerError):
    pass
```


[dry]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
[click]: http://click.pocoo.org/
[coloredlogs]: https://coloredlogs.readthedocs.io/en/latest/
[flask]: http://flask.pocoo.org/
[alchy]: http://alchy.readthedocs.io/en/latest/
[flask-alchy]: https://github.com/dgilland/flask-alchy
