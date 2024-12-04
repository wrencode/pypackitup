# pypackitup - Python Package Template

Template repository for developing Python packages.

---

<sub>***Do you like the Python Package Template? Star the repository on GitHub and please consider helping support its ongoing development:***</sub>

[<img src="https://raw.githubusercontent.com/wrencode/pypackitup/refs/heads/main/docs/wrencode-donation-venmo-qr-code.jpg" width="300"/>](https://venmo.com/wrencode?txn=pay)

<!-- https://venmo.com/<USER_NAME_1>,<USER_NAME_2>...?txn=<charge|pay>&note=<NOTE>&amount=<AMOUNT> -->

---

<div class="hide-next-element"></div>

**[READ THE DOCS HERE!](https://pypackitup.wrencode.dev)**
<br/>
<sup>Detailed documentation can be found at [https://pypackitup.wrencode.dev](https://pypackitup.wrencode.dev).</sup>

<div class="hide-next-element"></div>

### Table of Contents

<div class="hide-next-element"></div>

* [About](#about)
    * [Dependencies](#dependencies)
* [Setup](#setup)
    * [Configuration](#configuration)
    * [Version Control](#version-control)
    * [Documentation](#documentation)
    * [Code](#code)
* [Deployment](#deployment)

<div class="hide-next-element"></div>

---

<a name="about"></a>
### About

The Python Package Template is an example for Python package development.

<a name="dependencies"></a>
#### Dependencies

The Python Package Template does not have any third-party dependencies to run the code. It has several development dependencies, which can be seen in the package `pyproject.toml`.

---

<a name="setup"></a>
### Setup

The below list covers all updates needed in the Python Package Template when using it to create a new Python package:

<a name="configuration"></a>
#### Configuration

* `pyproject.toml`: Update all relevant fields as needed for the new package.

<a name="version-control"></a>
#### Version Control

* `.gitignore`: Add any package-specific files that should not be checked in to version control.
* `.github/ISSUE_TEMPLATE/`: Make any package-specific changes to the project issue templates.
* `.github/workflows/python-package.yml`: Update the supported Python versions and add any necessary CI/CD steps.

<a name="documentation"></a>
#### Documentation

* `README.md`: Update the `README.md` with all necessary package documentation.
* `mkdocs.yml`: Update the `nav` section with all necessary pages and their corresponding Markdown files (see below).
* `docs-mkdocs/CNAME`: Update the `CNAME` file with the desired mkdocs documentation GitHub Pages custom domain.
* `docs-mkdocs/extra.css`: Add any custom CSS for the mkdocs documentation.
* `docs-mkdocs/extra.js`: Add any custom JavaScript for the mkdocs documentation.
* `docs-mkdocs/*.md`: Add any necessary Markdown (`.md`) files for pages in the mkdocs documentation.
* `docs-mkdocs/*.svg/*.png/*.jpg/etc.`: Add any necessary images for the mkdocs documentation.

<a name="code"></a>
#### Code

* `src/pypackitup/`: Rename this directory to match the project directory and follow the [PEP naming conventions](https://peps.python.org/pep-0008/#package-and-module-names) for the package.
* `src/pypackitup/__init__.py`: Update the package `__init__.py` with available imports.
* `src/pypackitup/*.py`: Add package code.
* `tests/`: Add tests for package code.

---

<a name="deployment"></a>
### Deployment

*(Optional)* Check `pyproject.toml` for latest dependency versions.

&nbsp;

*(Optional)* Update virtual machine with the latest dependencies (`make update` in Makefile):
```shell
uv sync --all-extras --dev
```

&nbsp;

Lint code with `ruff` (`make lint` in Makefile):
```shell
ruff check .
```

&nbsp;

Check code security with `bandit` (`make secure` in Makefile):
```shell
bandit -c pyproject.toml -r .
```

&nbsp;

*(Optional)* Run *all* `pytest` tests (see following commands for running subsets of tests) (`make test_code` in Makefile):
```shell
uv run pytest tests
```

&nbsp;

*(Optional)* Run *all* `pytest` tests *verbosely*:
```shell
 uv run pytest -v -s tests
```

&nbsp;

*(Optional)* Run all tests from `pytest` file:
```shell
uv run pytest -v -s tests/test_helloworld.py
```

&nbsp;

*(Optional)* Run *specific* test from `pytest` file:
```shell
uv run pytest -v -s tests/test_helloworld.py -k test_main
```

&nbsp;

*(Optional)* Test Python support using [act](https://github.com/nektos/act) for GitHub Actions:
```shell
act -j build
```

***Note***: If `act` is unable to locate Docker, make sure that the required `/var/run/docker.sock` symlink exists. If it does not, you can fix it by running:
```shell
sudo ln -s "$HOME/.docker/run/docker.sock" /var/run/docker.sock`
```

***Note***: If you are running macOS on a devices with an M-series chip (Apple Silicon), you will need to specify `linux/amd64` architecture when running `act`:
```shell
act --container-architecture linux/amd64 -j build
```

&nbsp;

*(Optional)* Build the PyPI package independent of deployment:
```shell
make build
```

&nbsp;

*(Optional)* Test packages for PyPI deployment:
```shell
make verify_build
```

&nbsp;

*(Optional)* Check MkDocs documentation by serving it at [http://localhost:8000/](http://localhost:8000/) locally:
```shell
make test_docs
```

&nbsp;

*(Optional)* Build the PyPI package and MkDocs documentation independent of deployment:
```shell
make docs
```

***Note***: Running `make test_docs` from the previous step recreates the documentation without building the PyPI package.

&nbsp;

Create a git commit:
```shell
git add .
git commit -m 'commit message'
```

&nbsp;

Update the git tag with the new version (`git tag -a [tag_name/version] -m [message]`):
```shell
git tag -a v1.0.0 -m 'release message'
git push origin --tags
```

&nbsp;

*(Required for initial publication on PyPI as needed)* Register a [new account on PyPI](https://pypi.org/account/register/) (do the same for Test PyPI as needed).

&nbsp;

*(Required for initial publication on PyPI)* Configure [API token authentication for PyPI](https://pypi.org/help/#apitoken) by creating an API token (do the same for Test PyPI as needed) and copy the value of the API token.

&nbsp;

*(Required for initial publication on PyPI)* Create a `.env` file by running `cp .env.template .env` in the command line from the project root directory and paste the PyPI API token from the previous step as the value for `UV_PUBLISH_TOKEN` (this environment variable is used in the Makefile by `uv publish` to [publish the package using uv](https://docs.astral.sh/uv/guides/publish/#publishing-your-package)). 

&nbsp;

*(Optional after initial package publication on PyPI)* Configure a *new* [package-specific PyPI API token](https://pypi.org/manage/project/pypackitup/settings/) and update the above `UV_PUBLISH_TOKEN` environment variable in the `.env` to use it. 

&nbsp;

*(Optional if using Twine)* Install `twine` (if not already installed):
```shell
uv add twine
```

&nbsp;

*(Optional)* Test deployment by building the PyPI packages, recreating the documentation, and deploying to Test PyPI:
```shell
make test_deploy
```

&nbsp;

Deploy the package by building it, recreating the documentation, and deploying the package to PyPI:
```shell
make deploy
```

&nbsp;

Create a second git commit with updated version number and documentation:
```shell
git add .
git commit -m 'update version number and docs'
```

&nbsp;

Update package git repository:
```shell
git push
```

---
