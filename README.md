# to-pypi-using-flit
 An action to build and publish Python 🐍 package to PyPI using Flit.

## Usage

To use the action add the following step to your workflow file (e.g. .github/workflows/main.yml)

<br>

### Example Workflow

```yaml
name: publish

# Controls when the workflow will run
on:
    
    # Workflow will run when a release has been published for the package
    release:
        types:
            - published

    # Allows you to run this workflow manually from the Actions tab
    workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:

    # This workflow contains a single job called "publish"
    publish:

        # The type of runner that the job will run on
        runs-on: ubuntu-latest

        # Steps represent a sequence of tasks that will be executed as part of the job
        steps:

            # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
            -   uses: actions/checkout@v3

            -   name: Set up Python 3.9
                uses: actions/setup-python@v3
                with:
                    python-version: 3.9
                    cache: pip

            -   name: Publish to PyPI
                uses: asifarmanrahman/to-pypi-using-flit@v1
                with:
                    password: ${{ secrets.PYPI_API_TOKEN }}

```

> **_The action assume:_**
> * The project has a `pyproject.toml` (or `setup.py`) in the top-level directory.
> * Python and pip are installed.


<br>

### To use with PyPI API token

```yaml
- name: Publish package to PyPI using API TOKEN
  use: asifarmanrahman/to-pypi-using-flit@v1
  with:
     password: ${{ secrets.PYPI_API_TOKEN }}
```

<br>

### To use with PyPI Username and Password

```yaml
- name: Publish package to PyPI using Username and Password
  use: asifarmanrahman/to-pypi-using-flit@v1
  with:
     user-name: ${{ secrets.PYPI_USERNAME }}
     password: ${{ secrets.PYPI_PASSWORD }}
```

<br>

### To use with TestPyPI API token

```yaml
- name: Publish package to TestPyPI using API TOKEN
  use: asifarmanrahman/to-pypi-using-flit@v1
  with:
     password: ${{ secrets.TESTPYPI_API_TOKEN }}
     repository-url: https://test.pypi.org/legacy/
```

<br>

### To use with TestPyPI Username and Password

```yaml
- name: Publish package to TestPyPI using Username and Password
  use: asifarmanrahman/to-pypi-using-flit@v1
  with:
     user-name: ${{ secrets.TESTPYPI_USERNAME }}
     password: ${{ secrets.TESTPYPI_PASSWORD }}
     repository-url: https://test.pypi.org/legacy/
```

---

## Inputs

|     Variable     |           Description            |             Default             | Required |
|:----------------:|:--------------------------------:|:-------------------------------:|:--------:|
|   `user-name`    |      PyPI/TestPyPI Username      |           `__token__`           |  False   | 
|    `password`    | PyPI/TestPyPI Password/API TOKEN |              null               |   True   |
| `repository-url` |       PyPI Repository URL        | https://upload.pypi.org/legacy/ |  False   |

---


## License

The source code for this project is released under the [MIT License](/LICENSE). This project is not associated with GitHub.