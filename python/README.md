# Python

Python is a popular and easy-to-learn interpreted programming language. To get a feel for the language, take a look at this [comprehensive reference][python-ref]. With the surge in adoption of the most recent version of Python we are encouraging all new code to support [Python 3][python3] _first and foremost_.

## Separate topics

- [Testing](testing.md)
- [Logging](logging.md)
- [Packaging](count_variants/overview.md)

## Style guide

We generally follow PEP8. Written code should pass linting using [PyLint][pylint]. Ignored rules include:

- E501: "wrap lines at 80 characters" => we use a **100 character** limit

### Linting code

A linter is a great way to ensure you are writing code of good quality; following best practices and without avoidable errors relating to missing imports and misspelled variable names. We recommend [PyLint][pylint] for working with Python code. You can set it up to run in the background when you edit code.

## Packaging

Packaging Python code is a known pain point that many developers struggle with. There are some [moves][pipenv] to [standardize][pipfile] the experience but for now a great place to start would be to follow [this guide][mini-guide]. It will give you an idea of the minimal structure you need and beyond.

We also have our own guide to packaging [here](count_variants/overview.md)

For detailed information or if you need to look up specific options there a very [detailed resource](https://packaging.python.org/) available as well.

We should be using Pipfile, pipenv.

## Uploading a package to Pypi

In order to be able to install a Python package directly from the pip command, or from the requirements file of another software package, it is necessary to upload the package into PyPI. A basic tutorial on how to so that is available [here](uploading_to_pypi.md).


## Conda setup

See [conda](conda.md).

## Awesome Python

A curated list of _awesome_ Python tools and libraries!

- Command line interface

  - [Click][click]: composable and Flask-like CLI framework
  - [Halo][halo]: beautiful terminal spinners

- Testing

  - [Py.test][pytest]

    - [Py.test Coverage][pytest-cov]: easily integrate test coverage with Py.test
    - [Py.test Flask][pytest-flask]: easily integrate Py.test and Flask
    - [All plugin-ins][pytest-plugins]: list of all Py.test plugins!
    - Suggested command:

      ```bash
      py.test --cov-report html --cov "$(basename "$PWD")" --verbose --color=yes tests/
      ```

- Logging

  - [Coloredlogs][coloredlogs]: super simple setup for colorized logging

[mini-guide]: https://python-packaging.readthedocs.io/en/latest/minimal.html
[pipenv]: https://github.com/kennethreitz/pipenv
[pipfile]: https://github.com/pypa/pipfile
[python-ref]: https://github.com/justmarkham/python-reference/blob/master/reference.py
[python3]: https://docs.python.org/3/
[pylint]: https://www.pylint.org/
[click]: http://click.pocoo.org/
[halo]: https://github.com/ManrajGrover/halo
[pytest]: https://docs.pytest.org/en/latest/
[pytest-cov]: http://pytest-cov.readthedocs.io/en/latest/readme.html
[pytest-flask]: https://pypi.python.org/pypi/pytest-flask
[pytest-plugins]: https://pytest.readthedocs.io/en/2.7.3/plugins_index/index.html
[coloredlogs]: https://coloredlogs.readthedocs.io/en/latest/
