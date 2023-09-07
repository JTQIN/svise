# State estimation without governing equations

Accompanying code for "State estimation without governing equations" by Kevin Course
and Prasanth B. Nair.

<p align="center">
  <img align="middle" src="./experiments/extras/output.gif" alt="Example usage" width="700"/>
</p>

## Index

1. [Installation](#1-installation)
2. [Usage](#2-usage)
3. [Building documentation](#3-building-documentation)
4. [Reference](#4-reference)

## 1. Installation

If you just want to use the package, 
you can install `svise` [from PyPI](#install-from-pypi).

If you wish to reproduce experiments / figures, we recommend
[duplicating the experiment environment](#duplicating-the-experiment-environment).

### Install from PyPI

```bash
pip install svise
```

### Duplicating the experiment environment
We make use of [conda-lock](https://github.com/conda/conda-lock) 
and [poetry](https://python-poetry.org/) to
create reproducible experiment environments.
 After installing conda-lock, follow the steps below to duplicate the experiment environment.

1. Clone the repository.

```bash
git clone https://github.com/coursekevin/svi-state-estimation.git
```

2. Navigate into the directory and create a new conda environment.

```bash
conda-lock install --name svi-state-estimation conda-lock.yml
```

3. Activate the environment that was just created.

```bash
conda activate svi-state-estimation
```

4. Install the remaining dependencies.

```bash
poetry install --with dev
```

5. Run tests to confirm everything was install correctly. (Some tests are stochastic so might fail on some attempts.
   If any tests fail, run again before filing an issue.)

```bash
pytest
```

**Dependencies:**
- see `pyproject.toml` for a complete list of dependencies.

---

## 2. Usage

The numerical studies can be rerun from the `experiments` directory using
the command-line script `main.py`. All numerical studies follow the
same basic structure: (i) generate datasets, (ii) train models / run
methods, and (iii) post process for figures and tables.

1. Generate dataset for a specific experiment. The newly generated
   dataset can be found in the experiment subdirectory.

```bash
python main.py [experiment] generate-data
```

- Experiments in main text:

  - `pure-se` (state estimation without corruptions)
  - `corrupted-se` (state estimation without probabilistic corruptions)
  - `disc-goveq` (discovering governing equation experiments)
  - `high-dim-ex` (Lorenz '96 experiment)
  - `cylinder-flow` (Cylinder-flow reduced-order modeling experiment)

- Examples in appendix:

  - `newtonian-ex` (Newtonian system example in Appendix)

2. Train a model on a dataset optionally specifying the random seed.
   The model will be saved in the experiment subdirectory.

```bash
python main.py [experiment] run-[method] -dp path/to/dataset.pt -rs seed
```

- Methods:
  - `svise` (stochastic variational inference for state estimation)
  - `pf` (particle filter)
  - `sindy` (SINDy with STLSQ + SINDy with SR3)

3. Post process results for figures and tables. Any figures or tables
   can be found in the experiment subdirectory. This script expects
   there to be one model / dataset. Undefined behavior may occur if
   this is not the case.

```bash
python main.py [experiment] post-process
```

## 3. Building documentation

Building documentation requires [Sphinx](https://www.sphinx-doc.org/en/master/)
and the [Read the Docs Sphinx Theme](https://github.com/readthedocs/sphinx_rtd_theme).
First navigate into the `docs` directory.

Building html docs:

```bash
make html
```

Building pdf docs:

```bash
make latexpdf
```

Completed docs can be found in the `docs/_build` directory.

## 4. Reference