# Awesome Python Packaging [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

Python packaging recently got awesome!

**pyproject.toml** is the standard place to configure everything,
defined in [PEP 518](https://www.python.org/dev/peps/pep-0518).
Because lack of `pyproject.toml` support in some tools
is the only part about Python packaging that isn’t awesome already,
each tool has a little ✅ or ❌ to indicate support.

## Testing / Checking

Make sure your program behaves as you intended in different environments.

- [tox](https://tox.readthedocs.io/)
  [✅ (pyproject.toml, setup.cfg, tox.ini)](https://tox.readthedocs.io/en/latest/example/basic.html#pyproject-toml-tox-legacy-ini)

  Use this to define environments in which to test your package.
  Like continuous integration on your local machine.
  Can be integrated into CI like GH Actions, AppVeyor or Travis.

- [pytest](https://pytest.org/)
  [✅ (pyproject.toml, setup.cfg, tox.ini, pytest.ini)](https://docs.pytest.org/en/stable/customize.html#pyproject-toml)

  Unofficial standard for Python testing.
  Many Plugins, user-friendly error reporting using just `assert`.
  Good defaults make lack of `pyproject.toml` support painless.

- [mypy](http://mypy-lang.org/)
  [❌ (setup.cfg, mypy.ini)](https://github.com/python/mypy/issues/5205)

  Static type checking. It tests if the values you pass to
  and return from functions match the type annotations.

- [Coverage.py](https://coverage.readthedocs.io/)
  [✅ (pyproject.toml, .coveragerc)](https://coverage.readthedocs.io/en/latest/config.html#configuration-reference)

  Code coverage measurement for Python.

## Code Style

Make sure feedback in PRs isn’t mostly about code style, but about actual content.

- [pylint](https://www.pylint.org/)
  [✅ (pyproject.toml, setup.cfg, pylintrc, .pylintrc)](http://pylint.pycqa.org/en/latest/user_guide/run.html#command-line-options)
  – upcoming in v2.5,  
  [flake8](http://flake8.pycqa.org/)
  [❌ (setup.cfg, tox.ini, .flake8)](https://gitlab.com/pycqa/flake8/issues/428)

  Generic style checkers for many possible code smells.

- [pycodestyle](http://pycodestyle.pycqa.org/)
  [❌ (setup.cfg, tox.ini)](https://github.com/PyCQA/pycodestyle/issues/813)

  A style checker focused on [PEP 8](https://www.python.org/dev/peps/pep-0008/) compliance.
  Is included in `flake8`.

- [black](https://black.readthedocs.io/)
  [✅ (pyproject.toml)](https://black.readthedocs.io/en/stable/pyproject_toml.html)

  A optionless code formatter that frees your mind from having to think about style.

- [isort](https://pypi.org/project/isort/)
  [✅ (pyproject.toml, setup.cfg, tox.ini, .isort.cfg)](https://github.com/timothycrosley/isort#configuring-isort)

  A formatter for reordering imports. Many options!

## Package Creation Tools

Manage your package’s dependencies, and publish it to the PyPI.
With `poetry` and `flit`, there’s two easy to use command line applications.
No `pip`, `twine`, and `./setup.py` juggling!

- [poetry](https://poetry.eustace.io/)
  [✅ (pyproject.toml)](https://github.com/sdispater/poetry#the-pyprojecttoml-file)
  
  A tool for application and library development that manages dependencies.
  Keeps an unchanging project environment via lockfile and
  other than pip has an actual dependency solver.
  
- [flit](https://flit.readthedocs.io/)
  [✅ (pyproject.toml, flit.ini)](https://flit.readthedocs.io/en/latest/pyproject_toml.html)

  A tool for simple packages without compilation step.
  Use e.g. [get_version](https://github.com/flying-sheep/get_version)
  if you think your git tags are good as a source of versioning.

- [twine](https://twine.readthedocs.io/)

  If you’re still stuck in `setup.py` world, this might soothe your pain.
  It allows you to upload a `wheel` to PyPI with little hassle. It has no configuration.

- [setuptools_scm](https://pypi.org/project/setuptools-scm/)
  [✅ (pyproject.toml, setup.cfg)](https://github.com/pypa/setuptools_scm#pyprojecttoml-usage)
  

  A package that allows you to have one true source of versions: Your SCM metadata (e.g. `git tag`).
  Installing a “dirty” untagged version will automatically give you a version string that comparse as newer than the last clean one.
  It can work at build time as a command line tool/Python API or as a runtime library.

## Package managers

These don’t need to be configured per project with `pyproject.toml`,
but need to read its `[build-system]` section to install the project!

- [pip](https://pip.pypa.io/)
  [✅ (pyproject.toml, setup.py)](https://pip.pypa.io/en/stable/reference/pip/#pep-517-and-518-support)

  Python’s classic package manager. Widespread like no other and therefore very robust.
  Except for actually [resolving dependencies](https://github.com/pypa/pip/issues/988),
  which it does rather duct-tape-and-hope like.

- `poetry` (and to a small degree `flit`) is a package manager itself.
- [pipenv](https://docs.pipenv.org/)
  ❌ (Pipfile)
  
  `pipenv` is not a package creation tool, it’s an application creation tool.
  If you want to build a library, choose `poetry` or `flit`.

## Others

- [dephell](https://github.com/dephell/dephell#readme)
  [✅ (pyproject.toml)](https://github.com/dephell/dephell#usage)

  A dependency management tool that converts between and allows reasoning about all above.
