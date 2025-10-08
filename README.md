# Gaussian Processes with PyMC and LLMs

Gaussian Processes are incredibly useful for modeling messy, real-world data where traditional regression methods typically fail. They do this by modeling unknown functions with calibrated estimates of uncertainty, excelling on small-to-medium sized datasets, with messy or seasonal trends, and patterns that can't be described with simple lines. In this 2‑day, hands‑on course you’ll learn when GPs are appropriate, how to fit them in Python with PyMC using LLMs for coding support, how to choose kernels and likelihoods (including robust options), and how to scale them to larger datasets. We’ll apply these skills to real problems like time series and multi‑output data, with practical diagnostics, model comparison, and production tips.

Gaussian processes are a cornerstone of flexible, probabilistic modeling in fields from biostatistics to machine learning; they provide a principled way to capture uncertainty, build hierarchical and multi-output models, and encode smoothness in ways that align with modern empirical research questions. This two-day workshop led by Chris Fonnesbeck (PyMC Labs, Vanderbilt University Medical Center) brings together rigorous theory and practical, reproducible implementations of GPs with the help of LLMs for researchers who want to use this type of Bayesian nonparametrics in their work. The workshop emphasizes not just conceptual understanding but hands-on competence with PyMC and Python supported by Gen AI via Cursor and VSCode, so participants leave able to specify, fit, diagnose, and scale GP models for publication-quality analyses.

The course is split across two intensive days: Day 1 builds foundations and core implementations (GP theory, manual kernels, PyMC GP primitives, marginal vs latent formulations, and inference choices), while Day 2 focuses on scaling and applied workflows (HSGP spectral approximations, sparse methods, multi-output models, and real-world case studies such as sports analytics). Through live coding, curated notebooks adapted from the pymc-examples gallery, short exercises, and comparative demonstrations (NUTS vs VI vs MAP; exact GP vs HSGP), participants will acquire immediate, research-ready skills applicable to complex datasets and computational constraints commonly encountered in academic projects.

## Day 1

### Session 1: Introduction to Gaussian Processes and PyMC

- GPs as functions
- Prior and posterior
- Manual kernels
- Covariance matrices
- PyMC basics
- Marginal vs Latent
- Posterior predictive checks

### Session 2: Kernels, Likelihoods, and Model Building

- Kernel families
- Kernel composition
- Additive models
- Marginal vs Latent
- Non-Gaussian likelihoods
- Inference trade-offs
- T-process robustness


## Day 2

### Session 3: Scaling with HSGP and Sparse methods

- Computational bottlenecks
- HSGP theory
- HSGP implementation
- Choosing m and L
- Convergence diagnostics
- Inducing point methods
- Multidimensional inputs

### Session 4: Case Studies, Multi-Output, and Deployment

- Sports analytics case
- Data preparation
- Model fitting
- LMC multi-output
- Sparse multi-output
- Model diagnostics
- Deployment strategies


