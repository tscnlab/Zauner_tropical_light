# Tropical light exposure & health

This repository contains a reproducible [Quarto](https://quarto.org/) document for the seminar **Open science and FAIR data practices for personal light exposure research**. The document demonstrates how open, FAIR workflows can be used to inspect personal light exposure data from the MeLiDos project and evaluate exposure patterns against published recommendations for healthy lighting.

The rendered website is configured at: <https://tscnlab.github.io/Zauner_tropical_light/>.

## What is in this repository?

| File or directory | Purpose |
| --- | --- |
| `index.qmd` | The main Quarto document. It combines explanatory text, executable R code, figures, tables, and session information for the tropical light exposure analysis. |
| `_quarto.yml` | Quarto project configuration for rendering this repository as a website. It sets the website title, navigation, GitHub links, HTML theme, table of contents, and execution options. |
| `renv.lock` | A lockfile that records the R version and package versions used for the analysis so that the computational environment can be restored. |
| `renv/activate.R` | The `renv` activation script used by the project. |
| `license.qmd` | The license page included in the Quarto website navigation. |
| `assets/` | Static files used by the Quarto document, including figures referenced by `index.qmd`. |

## About the Quarto document

The main analysis lives in `index.qmd`. It is both a readable seminar document and an executable R analysis script. The document:

- introduces why personal light exposure matters for acute wellbeing and long-term mental, metabolic, and cardiovascular health;
- introduces the MeLiDos project, which collected harmonized personal light exposure datasets across several countries;
- loads the Costa Rica (`UCR`) 1-minute wearable light exposure dataset from the `melidosData` R package;
- visualizes light exposure patterns with `LightLogR`;
- computes common exposure summaries;
- loads and merges sleep-wake annotations with personal light exposure data;
- classifies wake, pre-sleep, and sleep intervals;
- evaluates adherence to the Brown et al. recommendations for healthy daytime, evening, and nighttime light exposure;
- produces summary plots, formatted tables, and session information for reproducibility.

The default Quarto parameters in `index.qmd` are:

```yaml
params:
  site: UCR
  dataset: glasses
```

You can adapt the document to another supported MeLiDos site by changing `params.site` in the document YAML or by passing parameters at render time.

## About Quarto

[Quarto](https://quarto.org/) is an open-source scientific and technical publishing system. A Quarto document (`.qmd`) can combine:

- narrative text written in Markdown;
- executable code cells, including R code;
- generated figures and tables;
- citations, cross-references, callouts, and other publication features;
- multiple output formats such as HTML, PDF, Word, and websites.

In this repository, Quarto is used to render `index.qmd` into a website. Rendering the document executes the R code, captures the outputs, and assembles the analysis into a navigable HTML page using the settings in `_quarto.yml`.

## Clone or fork the repository

### Option 1: Clone the repository

Clone the repository if you want a local copy for running or editing the analysis:

```bash
git clone https://github.com/tscnlab/Zauner_tropical_light.git
cd Zauner_tropical_light
```

If you use SSH with GitHub, you can clone with:

```bash
git clone git@github.com:tscnlab/Zauner_tropical_light.git
cd Zauner_tropical_light
```

### Option 2: Fork the repository

Fork the repository if you want your own GitHub copy before making changes:

1. Open <https://github.com/tscnlab/Zauner_tropical_light> in a browser.
2. Click **Fork** in the upper-right corner.
3. Choose your GitHub account or organization as the destination.
4. Clone your fork locally, replacing `<YOUR-USER>` with your GitHub username or organization:

```bash
git clone https://github.com/<YOUR-USER>/Zauner_tropical_light.git
cd Zauner_tropical_light
```

If you plan to contribute changes back, add the original repository as an upstream remote:

```bash
git remote add upstream https://github.com/tscnlab/Zauner_tropical_light.git
git fetch upstream
```

## Restore the R environment with renv

This project uses [`renv`](https://rstudio.github.io/renv/) to make the R package environment reproducible. The `renv.lock` file records the package versions needed by the analysis.

Before restoring packages, make sure you have:

- R installed;
- Quarto installed;
- system libraries required by R packages on your operating system;
- internet access for downloading packages the first time you restore the environment.

From the repository root, start R and run:

```r
install.packages("renv") # only needed if renv is not installed yet
renv::restore()
```

When prompted, confirm that you want to restore the project library from `renv.lock`. After restoration, the project-local package library should contain the packages needed by `index.qmd`, including `melidosData`, `LightLogR`, `tidyverse`, `gt`, `svglite`, `xml2`, and `downlit`.

## Execute or render the analysis

You can execute the analysis through Quarto from a terminal in the repository root.

Render the full website:

```bash
quarto render
```

Render only the main document:

```bash
quarto render index.qmd
```

Render with explicit parameters, for example the default Costa Rica site and glasses dataset:

```bash
quarto render index.qmd -P site:UCR -P dataset:glasses
```

Preview the website locally while editing:

```bash
quarto preview
```

Quarto will execute the R code cells in `index.qmd`, generate figures and tables, and write the rendered site to Quarto's output directory. If rendering fails because a package is missing, re-run `renv::restore()` from R and then render again.

## Typical workflow

```bash
# 1. Get the code
git clone https://github.com/tscnlab/Zauner_tropical_light.git
cd Zauner_tropical_light

# 2. Restore packages from R
R -e 'install.packages("renv", repos = "https://cloud.r-project.org"); renv::restore()'

# 3. Render the Quarto document
quarto render index.qmd
```

## Additional resources

- Quarto documentation: <https://quarto.org/docs/>
- Quarto websites: <https://quarto.org/docs/websites/>
- `renv` documentation: <https://rstudio.github.io/renv/>
- `melidosData` documentation: <https://melidosproject.github.io/melidosData/>
- `LightLogR` documentation: <https://tscnlab.github.io/LightLogR/>
