---
icon: fontawesome/brands/python
---

# :fontawesome-brands-python: Python

## Upgrade Table
A quick lookup table listing the main features (or at least the features that interest me) of each Python version.


<div class="grid cards" markdown>

-   __Python 3.13__ (2024-10-07)

    ---

    - [`@warnings.deprecated`](https://docs.python.org/3/library/warnings.html#warnings.deprecated) decorator.
    - [`typing.TypeIs`](https://docs.python.org/3/library/typing.html#typing.TypeIs) for type narrowing.

-   __Python 3.12__ (2023-10-02)

    ---

    - [`TypedDict`](https://docs.python.org/3/library/typing.html#typing.TypedDict) to annotate `**kwargs`
    - [`@typing.override()`](https://docs.python.org/3/library/typing.html#typing.override) decorator.
    - [Type Parameter Syntax](https://docs.python.org/3/whatsnew/3.12.html#pep-695-type-parameter-syntax)
    - Improved [f-strings](https://docs.python.org/3/whatsnew/3.12.html#pep-701-syntactic-formalization-of-f-strings) syntax support.

-   __Python 3.11__ (2022-10-24)

    ____

    - `Required` and `NotRequired` for [`TypedDict`](https://docs.python.org/3/library/typing.html#typing.TypedDict).
    - [`Self`](https://docs.python.org/3/library/typing.html#typing.Self) type.

-   __Python 3.10__ (2021-10-04)

    ____

    - [Structural Pattern Matching](https://docs.python.org/3/whatsnew/3.10.html#pep-634-structural-pattern-matching), aka `match ... case`.
    - Union types as `X | Y` (instead of `Union[X, Y]`).

</div>

## Package version from `__version__`

In my python libraries, I prefer maintaining the module version in a `__version__` variable. The following is used to load the version from the module itself:

```toml title="pyproject.toml"
[project]
dynamic = ["version"]

[tool.setuptools.dynamic]
version = { attr = "package_name.__version__" }
```


## Requirements from `requirements.txt`

Set the module's requirement list from a file.

```toml title="pyproject.toml"
[project]
dynamic = ["dependencies"]

[tool.setuptools.dynamic]
dependencies = { file = ["requirements.txt"] }
```

Optional dependencies can also be set from a file:

```toml title="pyproject.toml"
[project]
dynamic = ["optional-dependencies"]

[tool.setuptools.dynamic.optional-dependencies]
docs = { file = ["requirements-docs.txt"] }
testing = { file = ["requirements-testing.txt"] }
```

## :simple-ruff: Ruff Config

I use [Ruff](https://docs.astral.sh/ruff/) in most of my Python projects to keep consistent formatting and detect possible bugs. I usually have to go and copy my ruff config from another project and adjust it.


```toml title="pyproject.toml"
[tool.ruff.lint]
select = [
    "E", "W293", # pycodestyle
    "F", # Pyflakes
    "N", # pep8-naming
    "D", # pydocstyle
    "UP", # pyupgrade
    "S", # flake8-bandit
    "B", # flake8-bugbear
    "COM", # flake8-commas
    "C4", # flake8-comprehensions
    "FA", # flake8-future-annotations
    "ISC", # flake8-implicit-str-concat
    "G", # flake8-logging-format
    "PIE", # flake8-pie
    "Q", # flake8-quotes
    "RET", # flake8-return
    "SIM", # flake8-simplify
    "ARG", # flake8-unused-arguments
    "PERF", # Perflint
    "RUF", # Ruff-specific rules
    "ANN", # flake8-annotations
    "DTZ", # flake8-datetimez
    "PL", # Pylint
    "FURB", # refurb
]
ignore = [
    "D105", # Missing docstring in magic method
    "D107", # Missing docstring in `__init__`
    "RUF012", # Mutable class attributes should be annotated with `typing.ClassVar`
    "RUF013", # PEP 484 prohibits implicit `Optional`
    "ANN101", # Missing type annotation for {name} in method
    "ANN102", # Missing type annotation for {name} in classmethod
    "ANN202", # Missing return type annotation for private function {name}
    "ANN204", # Missing return type annotation for special method {name}
    "ANN401", # Dynamically typed expressions ({name}) are disallowed in `other`
    "PLR0913", # Too many arguments in function definition
    "PLR2004", #  Magic value used in comparison, consider replacing `{number}` with a constant variable
    "PLW2901", #  Outer {outer_kind} variable {name} overwritten by inner {inner_kind} target
]


[tool.ruff.lint.pycodestyle]
max-line-length = 120

[tool.ruff.lint.pep8-naming]
extend-ignore-names = ["assert*"]

[tool.ruff.lint.pyupgrade]
# Preserve types, even if a file imports `from __future__ import annotations`.
keep-runtime-typing = true

[tool.ruff.lint.flake8-bugbear]
# Allow default arguments like, e.g., `data: List[str] = fastapi.Query(None)`.
extend-immutable-calls = ["fastapi.Depends", "fastapi.Query", "fastapi.Path"]

[tool.ruff.lint.flake8-type-checking]
runtime-evaluated-base-classes = ["pydantic.BaseModel"]
```

