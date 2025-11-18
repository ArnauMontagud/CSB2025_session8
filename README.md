# CSB2025 - Practical Material for the Computational Systems Biology course, Fall 2025, session 8

This repository contains the practical material for the Computational Systems Biology (CSB 2025) course. It includes a Jupyter notebook used in the hands-on sessions, example models in GINsim format, and setup instructions to reproduce the analyses.

## Contents

- `CSB2025_practica.ipynb` — Main hands-on notebook used in the practical sessions. It demonstrates model loading, attractor analysis and stochastic simulations with the CoLoMoTo toolchain (GINsim, bioLQM and MaBoSS).
- `models/Metastasis_Master_Model.zginml` — Metastasis master model (GINsim `.zginml`) used in the tutorial.
- `models/PKN.zginml` — Prior Knowledge Network (PKN) model used in exercises.
- `Setting-up.txt` — Installation notes and minimal setup commands.
- `LICENSE` — BSD 3-Clause license for the repository.

## Citation and references

This material is adapted from:

Vincent Noël, Aurélien Naldi, Laurence Calzone, Loïc Paulevé, and Denis Thieffry (2025). "Reproducible Boolean model analyses and simulations with the CoLoMoTo software suite: a tutorial". *Interface Focus*. **15**: 20250002.

Please cite the original papers for the tools used (GINsim, bioLQM, MaBoSS) when reusing or adapting this material.

## Quick overview

The notebook walks through:

- Loading models with GINsim
- Converting to `bioLQM` for fixpoint (stable-state) analysis
- Converting to `MaBoSS` for stochastic simulations
- Running simulations (wild-type and mutants) and plotting trajectories, pie charts and entropy curves
- Several tasks: analyses on the PKN model, mutant simulations, and comparisons with literature results

## Requirements

These analyses were developed using the CoLoMoTo toolchain (GINsim, bioLQM, MaBoSS). Two recommended ways to reproduce the environment:

1) Conda environment (recommended for users who prefer a native setup)

 - Conda (Anaconda/Miniconda) installed.
 - Create the environment with the CoLoMoTo channels and required packages.

Example (PowerShell / WSL / macOS shell):

```pwsh
conda create -n CSB2025 -c colomoto -c potassco -c conda-forge \
	ginsim-python bns-python boolsim-python pymaboss notebook seaborn numpy pandas matplotlib
conda activate CSB2025
```

Notes:
- On Windows, using WSL (Ubuntu) is recommended for better compatibility with scientific tooling. If you prefer native Windows, install Anaconda and run the commands in a PowerShell session with conda initialized.
- `pip install ipylab` might be needed if not installed already


2) Docker (recommended for strongest reproducibility)

The CoLoMoTo Docker image packages all required tools and versions. Example commands:

```pwsh
pip install -U colomoto-docker
colomoto-docker -V 2025-03-01 --bind .
```

This will start a container with the environment and bind the current folder so you can open the notebook from the container.

## How to run the notebook

1. Open the repository folder in VS Code (or a terminal) and activate the environment:

```pwsh
# if using conda environment
conda activate CSB2025
# start jupyter notebook (or use VS Code's Jupyter extension)
jupyter notebook
```

2. Open `CSB2025_practica.ipynb` in VS Code or the browser.

3. Run the cells top-to-bottom. The notebook uses GINsim, bioLQM and MaBoSS; loading the models from `./models/`.

Notes and tips:
- The first time you run the notebook, imports may take a while while packages initialize.
- If a plotting cell does not render in VS Code, try running the notebook in the browser via `jupyter notebook`.
- If a model viewer call (e.g., `ginsim.show(...)`) does not open a graphical window in your environment, consider running the notebook inside the CoLoMoTo Docker container or using an environment that supports the required GUI/display backends.

## Models included

- `Metastasis_Master_Model.zginml`: The main model used in the tutorial. Used for attractor detection (bioLQM) and stochastic simulations (MaBoSS). Source: Cohen, D. P. A., Martignetti, L., Robine, S., Barillot, E., Zinovyev, A., & Calzone, L. (2015). Mathematical Modelling of Molecular Pathways Enabling Tumour Cell Invasion and Migration. *PLoS Comput Biol*, **11**(11), e1004571. https://doi.org/10.1371/journal.pcbi.1004571

- `PKN.zginml`: Prior Knowledge Network used in the exercises. Several notebook tasks ask you to load this model, define outputs, set initial conditions and run MaBoSS simulations to compare behaviours. Source: Traynard, P., Tobalina, L., Eduati, F., Calzone, L., & Saez-Rodriguez, J. (2017). Logic Modeling in Quantitative Systems Pharmacology. *CPT: Pharmacometrics & Systems Pharmacology*. https://doi.org/10.1002/psp4.12225


## Notebook tasks / exercises

The notebook contains several hands-on tasks. Highlights:

- **Task 1**: Inspect the PKN model and compute stable states.
- **Task 2**: Run MaBoSS simulations on the PKN model with different initial conditions and compare results.
- **Task 3**: Simulate mutants (KO/ON perturbations) on the PKN model with MaBoSS and compare with published results.

Follow the cell comments and hints inside `CSB2025_practica.ipynb` to complete the exercises.


## License

This repository is released under the BSD 3-Clause License. See `LICENSE` for details.

## Contact / support

If you find issues or need help, open an issue in the repository or contact the course instructor.

## Launch this repo in a Binder server

Click the badge below to launch the notebook in a free, cloud-based Binder environment (no installation needed, but with limited resources and a 10-minute inactivity timeout):

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/ArnauMontagud/CSB2025/HEAD?urlpath=%2Fdoc%2Ftree%2FCSB2025_practica.ipynb)

**Note on Binder (as of November 2025):** Binder sessions have access to up to 2 GB of RAM. Sessions shut down after 10 minutes of inactivity but can run for up to 6 hours. See [Binder usage guidelines](https://mybinder.readthedocs.io/en/latest/user-guidelines.html) for details.
