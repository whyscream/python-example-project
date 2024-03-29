# Hello world

Hello world is a minimal example project to document how to add various parts to a basic Python project.

## The `helloworld` program

The `helloworld` program implements a few very simple functionalities.

1. A package with an importable method that you can use from other Python code:

```Python
>>> from helloworld import hello
>>> hello()
'Hello world!'
>>> hello("John")
'Hello John!'
>>>
```

2. A commandline script that executes the hello function:

```shell
$ pip install .
[...]
Successfully installed helloworld-0.0.0
$ hello
Hello world!
$ hello John
Hello John!
```

3. A python module that can be executed using Python from the commandline:

```shell
$ pip install .
[...]
Successfully installed helloworld-0.0.0
$ python -m helloworld
Hello world!
$ python -m helloworld John
Hello John!
```

## Building a pip package

The `pyproject.toml` defines a build system, so you can actually build this into an installable pip package.

```shell
$ pip install build
[...]
Successfully installed build-1.1.1 pyproject_hooks-1.0.0
$ python -m build
[...]
Successfully built helloworld-0.0.0.tar.gz and helloworld-0.0.0-py3-none-any.whl
$ ls dist/
helloworld-0.0.0-py3-none-any.whl  helloworld-0.0.0.tar.gz
$ pip install ./dist/helloworld-0.0.0-py3-none-any.whl
[...]
Successfully installed helloworld-0.0.0
```


## Test suite

A basic test suite is added, which tests functionality of the hello function. Note that the cli interface is
omitted from the tests: this can be done but is too complex for this example.

To run the test suite, install the package (from the repo) with test dependencies, and run the `pytest` command.

```shell
$ pip install -e .[test]
[...]
$ pytest
============================= test session starts ==============================
platform linux -- Python 3.10.12, pytest-8.0.2, pluggy-1.4.0
rootdir: /home/[...]/helloworld
configfile: pyproject.toml
plugins: cov-4.1.0
collected 2 items

tests/test_hello.py ..                                                   [100%]

---------- coverage: platform linux, python 3.10.12-final-0 ----------
Name                         Stmts   Miss Branch BrPart  Cover
--------------------------------------------------------------
src/helloworld/__init__.py       2      0      0      0   100%
src/helloworld/hello.py          2      0      0      0   100%
--------------------------------------------------------------
TOTAL                            4      0      0      0   100%


============================== 2 passed in 0.03s ===============================
```

## Tox testing

You can also execute the tests using tox, which allows you to quickly run the tests in different variants
(f.i. different Python versions). The added configuration will run pytest using 2 Python versions, and will also
check the code for formatting issues using `black` and `isort`, and it will check whether the code has proper 
type annotations using `mypy`.

```shell
$ pip install tox
[...]
tox run
[...] (lots of output)
  py38: OK (5.42=setup[5.11]+cmd[0.31] seconds)
  py310: OK (3.89=setup[3.59]+cmd[0.30] seconds)
  linters: OK (3.62=setup[3.31]+cmd[0.20,0.10] seconds)
  types: OK (3.97=setup[3.83]+cmd[0.14] seconds)
  congratulations :) (16.95 seconds)
```
