# Documentation

Your project documentation will inevitably be **[the most][rdd] [important part][most-important-doc]** of your project going forward. It's important to use any and all means at your disposal to document your code.

We like to write documentation in [Markdown][markdown] using [GitBook][gitbook]. It provides a very nice command line interface, free static hosting, and a nice default theme with integrated search. This site is generated using GitBook!

We focus on providing online prose documentation with tutorials and examples.

## Dedicated documentation

This is likely the main entry point for new users. The dedicated documentation should first and foremost provide a higher level description of the software. It's important to give a gentle introduction but still get to the point the point quickly.

It should be available online, either as part a README file for small projects or more likely a full web site. Liberally include code examples and if possible a short demo tutorial where the user can follow along.

## API documentation (Python)

Python provides many powerful alternatives for inline documentation. We prefer a combination of docstring to explain the purpose of individual classes/methods/function with extensive [type annotations][type-annotations]. We prefer explicit type annotations over e.g. [Google style docstrings][google-docstrings] since they provide a richer syntax, allow editors to provide useful auto-completions, and will probably make you think twice before breaking.

That said, here's an example of inline Python documentation, using docstrings:

```python
@curry
def grep(pattern, line):
    """Match a simple pattern substring in a given string.

    Note that the function would also work to check for an item in a list,
    a key in a dictionary etc.

    Args:
        pattern (str): substring to match with
        line (str): string to match against

    Returns:
        bool: if ``pattern`` was a substring in ``string``

    Examples:
        >>> directors = ['Quentin Tarantino', 'PT Anderson']
        >>> list(filter(grep('Anderson'), directors))
        ['PT Anderson']
    """
    return pattern in line
```

Find out [how to document functions][google-docstrings] in your language and stick to accepted conventions.

## Change log

Follow this [opinionated standard][keepachangelog] dubbed "Keep a CHANGELOG". Basically it should be written in Markdown, mark each release with a version and date, and clearly separate between different categories of changes.

## Flowcharts

Flowcharts can convey overview in ways that is impossible to put into words. It can be a great way to organize e.g. a pipeline of functions that will help you in the design of your project. My favorite software is the free and online tool [Kingfisher][kingfisher].

[rdd]: http://tom.preston-werner.com/2010/08/23/readme-driven-development.html
[most-important-doc]: http://zachholman.com/posts/documentation/
[markdown]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[gitbook]: https://www.gitbook.com/
[type-annotations]: https://docs.python.org/3/library/typing.html
[google-docstring]: http://www.sphinx-doc.org/en/stable/ext/napoleon.html
[keepachangelog]: http://keepachangelog.com/
[kingfisher]: https://kingfisher.link/
