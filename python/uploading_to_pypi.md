# Uploading a Python package to PyPI

First thing to do is registering a user account on both [TestPyPI](https://test.pypi.org/) and [PyPI](https://pypi.org/). TestPyPI is a test site where you can verify that the software package is ok before uploading it to the official PyPI repository. To handle these accounts and use the same settings for every submission to PyPI you'll do in the future, you could create a .pypirc file in your home directory. This file should contain the following lines:

<pre>
[distutils]
index-servers =
  pypi
  testpypi

[pypi]
username = your pypi username
password = your pypi password

[testpypi]
repository = https://test.pypi.org/legacy/
username = your testpypi username
password = your testpypi password
</pre>

Otherwise you could always specify repository name, user and password every time you upload a package. This latter would be the **safest option** because this way you'd be avoiding storing passwords in plaintext in your home directory.

After packaging your software as described [here](https://packaging.python.org/), you are ready to upload it to the Python Package Index (PyPI), a repository specific for Python software. Be sure that all files that have to be included in the package along with with the code are listed in the **manifest file** (MANIFEST.in). It is necessary for instance to include files such as requirements.txt and LICENSE.txt.<br>
Please note that markdown-formatted pages are rendered poorly on the PyPI web pages, so you might want to convert the README.md file to reStructuredText format (.rst). This can be done by using [Pandoc](https://pandoc.org/).

Next step of preparing your package for PyPI would be fixing the **setup.py** file to include a download_url link to a tarball url. According to the official documentation available on packaging.python.org, packages version should follow the flexible public version scheme specified in [PEP 440](https://www.python.org/dev/peps/pep-0440/). Some examples:

<pre>
1.2.0.dev1  # Development release
1.2.0a1     # Alpha Release
1.2.0b1     # Beta Release
1.2.0rc1    # Release Candidate
1.2.0       # Final Release
1.2.0.post1 # Post Release
15.10       # Date based release
23          # Serial release
</pre>is link should be taking into account the version number of the software.

If for instance the version of your software is 1.3.0, the setup.py file should be modified by adding this line:

<pre>
setup(
...
download_url = 'https://github.com/Clinical-Genomics/Name_of_your_package/tarball/1.3.0',
...
)
</pre>

Note that this url doesn't exist yet and will be created at a later stage. After committing this change and fixing this version of the repository you should add a git tag to the package. This commands adds basically a version number and release to the project and will be showed under the "releases" page of the git project. The syntax to **add a tag** is the following:

<pre>
git tag 1.3.0 -m "Added a 1.3.0 version tag for PyPI"
git push --tags origin master
</pre>

Next step consists in creating a distribution release of the package. If your package has different requirements under different platforms (Linux, Mac or Windows) you should create platform wheels to taking care of this issue. Here's a documentation page explaining [how to create wheel files](https://wheel.readthedocs.io/en/stable/). If you don't need to care about wheels instead you can just create a distribution using the setup file:

<pre>
python setup.py sdist
</pre>

After creating a distribution you can test the upload on test.pypi. To do the actual upload you'll need [**twine**](https://github.com/pypa/twine) (pip install twine if it isn't installed already).

Upload to test.pypi:

<pre>
twine upload --repository-url https://test.pypi.org/legacy/ dist/*
</pre>

Check now that your repository is on PyPI test, under "your packages". You could now attempt to install the package from pip. To do that type:

<pre>
pip install --index-url https://test.pypi.org/simple --extra-index-url https://pypi.org/simple name_of_package
</pre>

The "--extra-index-url https://pypi.org/simple" option would instruct pip to retrieve all dependencies for your package from pypi itself.
If your package can be found on the test repository and everything is as you expect, it is safe to upload it on the PyPI repository:

<pre>
twine upload --repository-url https://upload.pypi.org/legacy/ dist/*
</pre>

Your package should be now available for installation over internet by using the command "pip install your_package".
