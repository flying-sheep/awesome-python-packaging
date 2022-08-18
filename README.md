# Awesome Python Packaging [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

Python packaging recently got awesome!

**pyproject.toml** is the standard place to configure everything,
defined in [PEP 518](https://www.python.org/dev/peps/pep-0518).
Because lack of `pyproject.toml` support in some tools
is the only part about Python packaging that isn’t awesome already,
each tool has a little ✅ or ❌ to indicate support.

## Testing / Checking

Make sure your program behaves as you intended in different environments.
Apart from locally running these, you also want to set up Continuous Integration (CI) like GitHub Actions or AppVeyor.

- [pre-commit](https://pre-commit.com/)
  [❌ (.pre-commit-config.yaml)](https://github.com/pre-commit/pre-commit/issues/1165)

  Automatically run checks (as e.g. the ones below) and formatters when committing changes.
  You probably want to configure this to run all checks except for slow ones like unit tests.
  Has its own CI provider that runs very quickly.

- [tox](https://tox.readthedocs.io/)
  [✅ (pyproject.toml, setup.cfg, tox.ini)](https://tox.readthedocs.io/en/latest/example/basic.html#pyproject-toml-tox-legacy-ini)

  Use this to define environments in which to test your package.
  Like continuous integration on your local machine.
  Can be integrated into CI.

- [pytest](https://pytest.org/)
  [✅ (pyproject.toml, setup.cfg, tox.ini, pytest.ini)](https://docs.pytest.org/en/stable/customize.html#pyproject-toml)

  Unofficial standard for Python testing.
  Many Plugins, user-friendly error reporting using just `assert`.
  Good defaults make lack of `pyproject.toml` support painless.

- [mypy](http://mypy-lang.org/)
  [✅ (pyproject.toml, setup.cfg, mypy.ini)](https://mypy.readthedocs.io/en/stable/config_file.html#using-a-pyproject-toml-file)
  – [since version 0.900](https://mypy-lang.blogspot.com/2021/06/mypy-0900-released.html)

  Static type checking. It tests if the values you pass to
  and return from functions match the type annotations.

- [Coverage.py](https://coverage.readthedocs.io/)
  [✅ (pyproject.toml, .coveragerc)](https://coverage.readthedocs.io/en/latest/config.html#configuration-reference)

  Code coverage measurement for Python.

## Code Style

Make sure feedback in PRs isn’t mostly about code style, but about actual content.

- [pylint](https://www.pylint.org/)
  [✅ (pyproject.toml, setup.cfg, pylintrc, .pylintrc)](http://pylint.pycqa.org/en/latest/user_guide/run.html#command-line-options)
  – since version 2.5,  
  [flake8](http://flake8.pycqa.org/)
  [❌ (setup.cfg, tox.ini, .flake8)](https://github.com/PyCQA/flake8/issues/234)

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
All of the below tools come with a Command Line Interface (CLI) and a
[build backend](https://peps.python.org/pep-0517/).
Except for flit, all of the CLIs allow you to manage package environments for your package’s dependencies.
  
- [flit](https://flit.readthedocs.io/)
  [✅ (pyproject.toml, flit.ini)](https://flit.readthedocs.io/en/latest/pyproject_toml.html)

  A tool for simple packages without compilation step.
  Does not manage package environments, which makes it very obvious and unsurprising.

- [PDM](https://pdm.fming.dev/latest/)
  [✅ (pyproject.toml)](https://pdm.fming.dev/latest/pyproject/pep621/)
  
  Has advanced features entirely based on standards.
  if you e.g. want to use its environment management with `hatch`’s build plugins, do it.
  The only not yet standardized function: Allows to synchronize your package dependencies using a lockfile.

- [poetry](https://poetry.eustace.io/)
  [✅ (pyproject.toml)](https://github.com/sdispater/poetry#the-pyprojecttoml-file)
  
  Also has lockfile support, but does more things not following standards.
  As a result, it contributes/uses the ecosystem less,
  is less interoperable, but well-tread paths work very well.
  
- [hatch](https://hatch.pypa.io/latest/)
  [✅ (pyproject.toml, hatch.toml)](https://hatch.pypa.io/latest/config/metadata/)

  (Optionally) allows a more fine grained and manual environment management than the above, similarly to `tox`.
  Has plugins, e.g. [hatch-vcs](https://pypi.org/project/hatch-vcs/) which derives your package version from Git tags.

Tools you can rely on that are not project managers / build backends:

- [build](https://pypa-build.readthedocs.io/en/stable/)

  Allows you to call into any of the build backends above and use it to build a `wheel` file for your package.
  It has no configuration.

- [twine](https://twine.readthedocs.io/)

  Allows you to upload a built `wheel` to PyPI with little hassle.
  It has no configuration.

- [setuptools_scm](https://pypi.org/project/setuptools-scm/)
  [✅ (pyproject.toml, setup.cfg)](https://github.com/pypa/setuptools_scm#pyprojecttoml-usage)
  
  A package that allows you to have one true source of versions: Your SCM metadata (e.g. `git tag`).
  Installing a “dirty” untagged version will automatically give you a version string that comparse as newer than the last clean one.
  It can work at build time as a command line tool/Python API or as a runtime library.
  `hatch-vcs` wraps its functionality.

## Package managers

These don’t need to be configured per project with `pyproject.toml`,
but need to read its `[build-system]` section to install the project!

- [pip](https://pip.pypa.io/)
  [✅ (pyproject.toml, setup.py)](https://pip.pypa.io/en/stable/reference/pip/#pep-517-and-518-support)

  Python’s classic package manager. Widespread like no other and therefore very robust.
  Except for actually [resolving dependencies](https://github.com/pypa/pip/issues/988),
  which it does rather duct-tape-and-hope like.

- The Package Creation Tools above can be used as package managers.
- [pipenv](https://pipenv.pypa.io/en/latest/)
  ❌ (Pipfile)
  
  `pipenv` is not a package creation tool, it’s an application creation tool.
  If you want to build a library, choose one of the package creation tools above.

## Others

- [dephell](https://github.com/dephell/dephell#readme)
  [✅ (pyproject.toml)](https://github.com/dephell/dephell#usage)

  A dependency management tool that converts between and allows reasoning about all above.
