# Fixtures (and pytest)

Python has a number of test runners to extend and simplify writing (unit) tests. We recommend [pytest]: a super robust and feature rich test framework. It lets you write tests as simple “asserts“, has a brilliant plugin ecosystem that “just works” after pip install pytest-[somePlugin], and let’s you leverage powerful fixtures to keep things DRY.

A small flavor of what tests look like with pytest:

```
import pytest
from mypackage import best_movie, perform_division

def test_best_movie():
    movie = best_movie(director='P.T. Anderson')
    assert movie == 'There Will Be Blood'

def test_perform_division():
    with pytest.raises(ValueError):
        # call with parameters that should yield error
        perform_division(12, 0)
```

Running your tests is as easy as:

```
$ py.test --verbose
```

## Organizing tests

pytest does a great job of detecting tests. All you need to do is name test modules with a prefix: `test_*`. Each test function should similarly be named `def test_*:`.

Furthermore, organize test files to reflect the source code. The following package:

```
myPackage
|-- utils.py
|-- tools
     |-- docker.py
```

… would result in the following test structure:

```
tests
|-- test_utils.py
|-- tools
     |-- test_tools_docker.py
```

You notice that the term “tools” is “repeating” for the “docker”-test module. This is because pytest requires globally unique test module names!

## Test fixtures

[Fixtures] is the key concept to start mastering tests. They are pluggable components that can be shared across many tests to setup pre-conditions like:

- setup a database connection
- read in lines form a file

They each have their own setup and tear down blocks and you control if they are reset on a function/module/session basis.

Let’s add a few items to our setup:

```
tests
|-- fixtures                    # store static files here
|-- test_utils.py
|-- tools
     |-- test_tools_docker.py
|-- conftest.py                 # write fixture functions here
```

Inside conftest.py you can add fixture functions that will be exposed to your tests. You mark a function as a fixture with a decorator. If you don’t need setup/tear down you can use a simple `@pytest.fixture`. Otherwise it's easiest to use `@pytest.yield_fixture`.

```
# conftest.py
import pytest
from myPackage import DatabaseAPI

@pytest.yield_fixture(scope='function')
def db_connection():
    _db_connection = DatabaseAPI(uri=':memory:')
    _db_connection.create_tables()
    yield _db_connection
    _db_connection.teardown_tables()
```

```
# test_utils.py
def test_add_row(db_connection):
    name = 'Paul T. Anderson'
    add_row(name=name, age=34)
    db_connection.save()
    assert db_connection.get_row(name=name).age == 34
```

When pytest runs the above function it will look for a fixture called `db_connection` and run it. Whatever is yielded (or returned) will be passed along to the test function. We set the “scope” of the fixture to “function” so as soon as the test is complete, the block after the yield statement will run. You can pass as many fixtures as you want to a test.

> Tip: test fixtures accept parameter-dependencies the same way as test functions. It’s perfectly possible to combine several test fixtures.

Additional fixtures can be installed through plugins and pytest itself comes with a few built in. For example there’s the handy tmpdir fixture that provides unique temporary folders where you can test various side effects.

```
from mypackage import touch

def test_write_file(tmpdir):
    # GIVEN an empty dir
    assert len(tmpdir.listdir()) == 0
    # WHEN touching a new file
    new_path = tmpdir.join('newfile.txt')
    touch(str(new_path))
    # THEN there should be a new file created
    assert len(tmpdir.listdir()) == 1
```

[pytest]: http://docs.pytest.org/en/latest/
[Fixtures]: https://docs.pytest.org/en/latest/fixture.html
