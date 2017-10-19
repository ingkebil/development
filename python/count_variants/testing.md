# Testing

There are tons of smart things written about testing, we have linked to a few in the [pyhon/testing][python_testing] section.
In general we like to use [pytest][pytest] to handle everything in our packages. Let's start with to add `pytest` to our requirement file and make a git commit(you should know how to do that now ✌️). Also install pytest with `pip install pytest`

## Writing the first simple test

We like to keep our tests outside of the codebase so in the root of our package we create a directory called `tests`. Within that directory we create sub folders that looks similar to our package, we then keep the tests separated for each sub module in our package. This might not seem relevant at the moment, when a package grow it is nice to have the structure right from the beginning. Also we will need static files, like VCFs, for our tests. These will be stored in a `fixtures` folder in `tests`:

```bash
$ mkdir tests
$ mkdir tests/cli tests/utils tests/fixtures
```

Structure of package should now look like:

```bash
count_variants/
├── LICENSE
├── README.md
├── MANIFEST.in
├── .gitignore
├── setup.py
├── count_variants/
    ├── __init__.py
    ├── __version__.py
    ├── cli/
        ├── __init__.py
        ├── root.py
    ├── utils/
        ├── __init__.py
        ├── count.py
├── tests/
    ├── cli/
    ├── fixtures/
    ├── utils/
```

Let's write the first test for our `count_variants` function. Remember that the docstring looks like:
```python
    """Count the number of variants in a vcf file
    
    Args:
        vcf(iterable): An iterable with variants
    
    Returns:
        nr_variants(int): Number of variants in file
    """

```
So we have stated that the function takes an iterable as the argument `vcf`, this could be any [iterable][iterables] in python. We could therefore send in a list(at least at the moment since our program is very simple).
Let's open a file in `tests/utils/test_count_variants.py`. All files that includes tests should have the prefix `test_` to tell pytest that tests are coming here. Write the file so it looks like:

```python
from count_variants.utils.count import count_variants

def test_count_empty():
    ## GIVEN an empty iteable
    variants = []
    
    ## WHEN counting the variants
    nr_variants = count_variants(variants)
    
    ## THEN assert that the number of variants is 0
    assert nr_variants == 0
```

When you run pytest and point to a folder, all files will be searched and executed if they start with `test_` and include functions that starts with `test_`. The `-v` flag is for `vebose` output

```bash
$ py.test -v tests
================================================================================ test session starts ================================================================================
platform darwin -- Python 3.6.0, pytest-3.2.3, py-1.4.34, pluggy-0.4.0 -- /Users/mansmagnusson/miniconda3/envs/cg_dev/bin/python
cachedir: .cache
rootdir: /Users/mansmagnusson/Projects/count_variants, inifile:
collected 1 item

tests/utils/test_count_variants.py::test_count_empty PASSED

============================================================================= 1 passed in 0.01 seconds ==============================================================================
```

















[iterables]: https://stackoverflow.com/questions/9884132/what-exactly-are-pythons-iterator-iterable-and-iteration-protocols
[python_testing]: ../testing.md
[pytest]: http://docs.pytest.org/en/latest/