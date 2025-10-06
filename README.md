## AuToMATo: An Out-Of-The-Box Persistence-Based Clustering Algorithm

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Code for the paper ["AuToMATo: An Out-Of-The-Box Persistence-Based Clustering Algorithm"](https://arxiv.org/abs/2408.06958).
This repository contains source code for AuToMATo as well as the code used to produce the results and figures from the paper above.
The following instructions assume that the Python package and project manager [`uv`](https://docs.astral.sh/uv/) is installed; similar instructions apply for other such managers.

## Requirements

Required Python dependencies are specified in `pyproject.toml`, where developer dependencies indicate those that are needed only in order to run the scripts that reproduce results and figures from the paper, as opposed to just using AuToMATo on its own.

The environment specified in `uv.lock` can be recreated by running `uv sync` or `uv sync --no-dev`, depending on whether developer dependencies should be included or not, respectively.

## Running AuToMATo

The following may be used to recreate the environment specified in `uv.lock` and to launch an interactive shell in it.

```bash
$ git clone https://github.com/m-a-huber/automato_paper
$ cd automato_paper
$ uv run python  # implicitly runs `uv sync` if needed
```

Following the above, AuToMATo may be used by running, for example, the following.

```python
>>> from automato import Automato
>>> from sklearn.datasets import make_blobs
>>> X, y = make_blobs(centers=2, random_state=42)
>>> aut = Automato(random_state=42).fit(X)
>>> aut.n_clusters_
2
>>> (aut.labels_ == y).all()
True
>>> ...
```

Alternatively, AuToMATo is now on [PyPI](https://pypi.org/project/automato/) and can therefore be installed by running

```bash
$ uv add automato
```

or

```bash
$ pip install -U automato
```

Note, however, that the implementation of AuToMATo that is hosted on PyPI is maintained, and may thus end up being different in the future from the one implemented in this repo.

## Reproducing Results and Figures from the Paper

The following may be used to recreate the environment specified in `uv.lock`.

```bash
$ git clone https://github.com/m-a-huber/automato_paper
$ cd automato_paper
$ uv run python  # implicitly runs `uv sync` if needed
```

The results and figures from the paper may be reproduced by running one or more of the following.

```bash
$ uv run python -m eval.eval  # creates results from Table 1 in Section 4.4
$ uv run python -m mapper_applications.make_synth_pictures  # creates Figure 4 in Section 5
$ uv run python -m mapper_applications.make_diabetes_pictures  # creates Figure 5 in Section 5
```

__Warnings__
- For the above to work, the benchmark data used in the dependency `clustering-benchmarks` must be manually downloaded from [here](https://github.com/gagolews/clustering-data-v1/releases/tag/v1.1.0). Depending on the location of that data, the variable `data_path` in line 27 of `eval/eval.py` may need to be adjusted; it should point to the location of the downloaded directory `clustering-data-v1`.
- If the TTK-clustering algorithm is to be included in evaluation (set value of `include_ttk` to `True` in line 22 of `eval/eval.py` to do so), [ParaView](https://www.paraview.org/download/) and the [Topology ToolKit](https://topology-tool-kit.github.io/) must be installed.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.