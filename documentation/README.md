# Documentation

We like to write documentation in [Markdown][markdown] using [GitBook][gitbook]. It provides a very nice command line interface, free static hosting, and a nice default theme with integrated search. This site is generated using GitBook!

We focus on providing online prose documentation with tutorials and examples.

## API documentation (Python)

Python provides many powerful alternatives for inline documentation. We prefer a combination of docstring to explain the purpose of individual classes/methods/function with extensive [type annotations][type-annotations]. We prefer explicit type annotations over e.g. [Google style docstrings][google-docstrings] since they provide a richer syntax, allow editors to provide useful auto-completions, and will probably make you think twice before breaking.


[markdown]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[gitbook]: https://www.gitbook.com/
[type-annotations]: https://docs.python.org/3/library/typing.html
[google-docstring]: http://www.sphinx-doc.org/en/stable/ext/napoleon.html
