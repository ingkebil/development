# Python

Python is a popular and easy-to-learn interpreted programming language. To get a feel for the language, take a look at this [comprahensive reference][python-ref]. With the surge in adoption of the most recent version of Python we are incouraging all new code to support [Python 3][python3] _first and foremost_.

## Separate topics

- [Testing](testing.md)

## Packaging

Packaging Python code is a known pain point that many developers struggle with. There are some [moves][pipenv] to [standardize][pipfile] the experience but for now a great place to start would be to follow [this guide][mini-guide]. It will give you an idea of the minimal structure you need and beyond.

For detailed information or if you need to look up specific options there a very [detailed resource](https://packaging.python.org/) available as well.

## Conda setup

See [conda](conda.md).

## Logging

Logging is the logical next step when you realize the limitations of printing. Python includes a very useful logging module in the standard library so it's rather easy to get started. First make sure you know [the basics][logging]. Now when you want to log some progress or program state in a module:

```python
import logging

log = logging.getLogger(__name__)


def foo(bar):
    """My fancy function."""
    log.info("incrementing the input: %s", bar)
    return bar + 1
```

The not-so-intuative part is that you need to configure the logging module to see any output from these calls. Luckily we can reduce the setup to a simple function call most of the time using the [coloredlogs][coloredlogs] package. During e.g. your CLI initialization include:

```python
import click
import coloredlogs


@click.command()
@click.option('-l', '--log-level', default='INFO', help='Log message level to display')
def cli(log_level):
    """Base command line entry point."""
    coloredlogs.install(level=log_level)
    # ... more code here
```



[mini-guide]: https://python-packaging.readthedocs.io/en/latest/minimal.html
[pipenv]: https://github.com/kennethreitz/pipenv
[pipfile]: https://github.com/pypa/pipfile
[logging]: http://mussol.org/2016/12/15/understanding-logging-in-python/
[coloredlogs]: https://coloredlogs.readthedocs.io/en/latest/
[python-ref]: https://github.com/justmarkham/python-reference/blob/master/reference.py
[python3]: https://docs.python.org/3/
