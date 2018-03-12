## Determining the version number


We are using semantic versioning which assigns a MAJOR.MINOR.PATCH number as a version number.

Given a version number MAJOR.MINOR.PATCH, increment the:

MAJOR version when you make incompatible API changes (change of in/output),
MINOR version when you add functionality in a backwards-compatible manner (in/output remains), and
PATCH version when you make backwards-compatible bug fixes.
Instantiate new repository


When creating a new repository, use bumpversion for automatic release version bumping:

https://github.com/peritus/bumpversion

As taken from the bumpversion github page:

"A small command line tool to simplify releasing software by updating all version strings in your source code by the correct increment. Also creates commits and tags."

Making your repository bumpversion ready is as easy as to drop following .bumpversion.cfg file into the root of your repository:



[bumpversion]
current_version = 0.0.1
commit = True
tag = True
tag_name = {new_version}


Version a script
Then give a script a version number, in two easy steps:

Step 1: Add a version string to setup.py in the set up section:

```
setup(
name='cgstats',

# Versions should comply with PEP440. For a discussion on
# single-sourcing the version across setup.py and the project code,
# see http://packaging.python.org/en/latest/tutorial.html#version
version='1.2.2'
```


Register the script name in the .bumpversion.cfg file, e.g. append [bumpversion:file:path/to/script]

```
[bumpversion]
current_version = 1.2.2
commit = True
tag = True
tag_name = {new_version}

[bumpversion:file:setup.py]
```




## Increase version

To increase the version number according to the semantic versioning rules, issue the bumpversion command in the repository root with either major, minor or patch as argument, e.g.:

```bumpversion minor```

==Only bump on up to date master!==

With abovementioned configuration, a git tag will be created and you still need to push it to github:

git push
git push --tags
