[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

# Data Science Project Template
A template file and folder project skeleton structure. The layout is inspired by and borrows from [The Good Research Code Handbook](https://goodresearch.dev/setup#), [Cookie Cutter Data Science](http://drivendata.github.io/cookiecutter-data-science/), and [Nico Spiller](https://github.com/nspiller/template_data_pipelines/tree/main) as a reasonably standardized but flexible project structure for data science heavy and computational modelling workflows written in in jupyter notebooks and python scripts. This template also contains GitHub pre-commit scripts to:
-  run Python linters to:
    - check for coding standard adherence
    - detect errors
    - enforce customizable coding guidelines (ex. PEP8)
- sync jupyter notebooks and python scripts for easy diffing and merging of branches in GitHub (ignores .ipynb files in notebooks folder)

## Requirements
### Python
Python version 3.8+ (Can be installed when creating `conda env` for new project.)

### Conda
Download and install [Anaconda](https://www.anaconda.com/download). How to work with `conda` environments is explained in the [`conda`](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) user guide.

### Git
Download and install [`git`](https://git-scm.com/downloads) version control.

## Installation
### Create a new project
#### 1. Install cookiecutter:
Open an Anaconda Command Prompt (WindowsOS) or Terminal (MacOS)  It is recommended to create a separate `conda env` for each project. Activate `conda env` for project and install [Cookiecutter](http://cookiecutter.readthedocs.org/en/latest/installation.html) >= 1.4.0 (This can be installed with pipx (recommended) or pip.):
``` bash
$ pipx install cookiecutter
```
or
``` bash
$ pip install cookiecutter
```
#### 2. Navigate to desired project dir:
Navigate to the directory where you would like your project to reside.
#### 3. Run and follow prompts:
``` bash
$ cookiecutter -c https://github.com/porter-colin93/DataModellingTemplate
```
#### 4. Install the project code as a local python module:
*Navigate into the project directory and then run:*
``` bash
$ pip install -e
```

### Make Project a GitHub Repository
Using GitHub desktop, one can make the project a GitHub repository to track changes not just locally, but also on GitHub.

### Setup pre-commits
#### 1. Install pre-commit:
*While IN the project directory that is also a Git repository, run:*
``` bash
$ pip install pre-commit
```
Check the install of pre-commit worked. `pre-commit --version` should show the version you are running.
``` bash
$ pre-commit --version
pre-commit 3.7.0
```
#### 2. Add a pre-commit configuration
- Skeleton template comes configured with a file named `.pre-commit-config.yaml` and the following pre-commit hooks that format python code. However, other [supported hooks](https://pre-commit.com/hooks.html) are available.
```
repos:
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v2.3.0
    hooks:
    -   id: check-yaml
    -   id: end-of-file-fixer
    -   id: trailing-whitespace
-   repo: https://github.com/psf/black
    rev: 22.10.0
    hooks:
    -   id: black
```
#### 3. Install the git hook scripts:
``` bash
$ pre-commit install
pre-commit installed at .git/hooks/pre-commit
```
#### 4. Run pre-commit hooks against all files (optional):
- It's usually a good idea to run the hooks against all of the files when adding new hooks (usually pre-commit will only run on the changed files during git hooks). For more details on pre-commit hooks, see the [pre-commit usage guide](https://pre-commit.com/).
```
$ pre-commit run --all-files
[INFO] Initializing environment for https://github.com/pre-commit/pre-commit-hooks.
[INFO] Initializing environment for https://github.com/psf/black.
[INFO] Installing environment for https://github.com/pre-commit/pre-commit-hooks.
[INFO] Once installed this environment will be reused.
[INFO] This may take a few minutes...
[INFO] Installing environment for https://github.com/psf/black.
[INFO] Once installed this environment will be reused.
[INFO] This may take a few minutes...
Check Yaml...............................................................Passed
Fix End of Files.........................................................Passed
Trim Trailing Whitespace.................................................Failed
- hook id: trailing-whitespace
- exit code: 1

Files were modified by this hook. Additional output:

Fixing sample.py

black....................................................................Passed
```

## Project/Directory Structure
The directory structure of your new project looks like this:

```
├── LICENSE
├── Makefile           <- Makefile with commands like `make data` or `make train`
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- A default Sphinx project; see sphinx-doc.org for details
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks and synced python scripts. Naming convention is a
│                         number (for ordering), the creator's initials, and a short `-`
│                         delimited description, e.g. `1.0-jqp-initial-data-exploration`.
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
│
├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
├── src                <- Source code for use in this project.
│   ├── __init__.py    <- Makes src a Python module
│   │
│   ├── data           <- Scripts to download or generate data
│   │   └── make_dataset.py
│   │
│   ├── features       <- Scripts to turn raw data into features for modeling
│   │   └── build_features.py
│   │
│   ├── models         <- Scripts to train models and then use trained models to make
│   │   │                 predictions
│   │   ├── predict_model.py
│   │   └── train_model.py
│   │
│   └── visualization  <- Scripts to create exploratory and results oriented visualizations
│       └── visualize.py
│
├── tests              <- Scripts to run tests
├── .pre-commit-config <- .yaml file for running pre-commit actions; see pre-commit.com
└── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io
```

## Syncing Jupyter Notebooks and Python Scripts
This project template has a pre-commit implementation of jupytext to sync jupyter notebooks and scripts. However, this only checks that the notebooks in the `code/notebooks` folder are in sync with the corresponding python scripts in `code/scripts`. To sync a jupyter notebook with a python script without committing, run:
``` 
$ jupytext --sync notebook.ipynb                  # Update whichever of notebook.ipynb/notebook.py is outdated
```

## References
- https://goodresearch.dev/
- https://drivendata.github.io/cookiecutter-data-science/
- https://github.com/nspiller/template_data_pipelines/tree/main

- https://cookiecutter.readthedocs.io/en/stable/#
- https://pre-commit.com/
- https://desktop.github.com/
