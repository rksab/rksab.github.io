# RamanK.github.io

Personal website and blog for Raman, a UBC Master of Data Science student, built
with [Quarto](https://quarto.org). The blog has two computational posts on the
Palmer Penguins data: one in R (`blog/penguins-r/`) and one in Python
(`blog/penguins-python/`). A third post (`blog/r-and-python/`) runs R and
Python in one document and passes objects between them with `reticulate`.

The site is published at <https://rksab.github.io/>.

## What to install first

Versions used to build this site:

- [Quarto](https://quarto.org/docs/get-started/) 1.10.18
- [uv](https://docs.astral.sh/uv/) 0.12.9 (it installs Python 3.14 itself, as pinned in `.python-version`)
- [R](https://cran.r-project.org/) 4.6.1 (`renv` bootstraps itself on first launch)

## Build the site

Run everything from the top level of the repository.

In a shell:

```bash
git clone git@github.com:rksab/rksab.github.io.git
cd rksab.github.io
uv sync
```

In R, started from the top level of the repository (so `.Rprofile` turns `renv` on):

```r
renv::restore()
```

Back in the shell:

```bash
uv run quarto render
```

Quarto renders the site into `docs/`. The Python post runs through the `uv`
environment, and the R post picks up the `renv` library. The R-and-Python post
uses both: `reticulate` finds the Python in `.venv` (created by `uv sync`), so
run `uv sync` before rendering.

To preview it locally, run `uv run quarto preview`, or open
`docs/index.html` in a browser after rendering.

## Environments

| Language | Files                                          | Tool |
|----------|------------------------------------------------|------|
| Python   | `pyproject.toml`, `uv.lock`, `.python-version` | uv   |
| R        | `renv.lock`, `.Rprofile`, `renv/activate.R`    | renv |

After adding a package, use `uv add` (Python) or
`renv::install()` then `renv::snapshot()` (R), and commit the updated lockfile.

## Data

Both posts use the Palmer Penguins data
([Horst, Hill and Gorman](https://allisonhorst.github.io/palmerpenguins/), Palmer
Station Antarctica LTER, CC0 licence). It ships inside the `palmerpenguins`
R and Python packages, so building the site needs no network access to fetch
data. Installing the packages does need the network.
