# Python

Python is a popular and easy-to-learn interpreted programming language. To get a feel for the language, take a look at this [comprehensive reference][python-ref]. With the surge in adoption of the most recent version of Python we are encouraging all new code to support [Python 3][python3] _first and foremost_.

## Separate topics

- [Testing](testing.md)
- [Logging](logging.md)

## Style guide

We generally follow PEP8. Written code should pass linting using [PyLint][pylint]. Ignored rules include:

- E501: "wrap lines at 80 characters" => we use a **100 character** limit

### Linting code

A linter is a great way to ensure you are writing code of good quality; following best practices and without avoidable errors relating to missing imports and misspelled variable names. We recommend [PyLint][pylint] for working with Python code. You can set it up to run in the background when you edit code.

## Packaging

Packaging Python code is a known pain point that many developers struggle with. There are some [moves][pipenv] to [standardize][pipfile] the experience but for now a great place to start would be to follow [this guide][mini-guide]. It will give you an idea of the minimal structure you need and beyond.

For detailed information or if you need to look up specific options there a very [detailed resource](https://packaging.python.org/) available as well.

## Conda setup

See [conda](conda.md).



[mini-guide]: https://python-packaging.readthedocs.io/en/latest/minimal.html
[pipenv]: https://github.com/kennethreitz/pipenv
[pipfile]: https://github.com/pypa/pipfile
[python-ref]: https://github.com/justmarkham/python-reference/blob/master/reference.py
[python3]: https://docs.python.org/3/
[pylint]: https://www.pylint.org/
