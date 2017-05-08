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

The not-so-intuitive part is that you need to configure the logging module to see any output from these calls. Luckily we can reduce the setup to a simple function call most of the time using the [coloredlogs][coloredlogs] package. During e.g. your CLI initialization include:

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


[logging]: http://mussol.org/2016/12/15/understanding-logging-in-python/
[coloredlogs]: https://coloredlogs.readthedocs.io/en/latest/
