# Gaussian Processes with PyMC and LLMs

Gaussian Processes are incredibly useful for modeling messy, real-world data where traditional regression methods typically fail. They do this by modeling unknown functions with calibrated estimates of uncertainty, excelling on small-to-medium sized datasets, with messy or seasonal trends, and patterns that can't be described with simple lines. In this 2‑day, hands‑on course you’ll learn when GPs are appropriate, how to fit them in Python with PyMC using LLMs for coding support, how to choose kernels and likelihoods (including robust options), and how to scale them to larger datasets. We’ll apply these skills to real problems like time series and multi‑output data, with practical diagnostics, model comparison, and production tips.

Gaussian processes are a cornerstone of flexible, probabilistic modeling in fields from biostatistics to machine learning; they provide a principled way to capture uncertainty, build hierarchical and multi-output models, and encode smoothness in ways that align with modern empirical research questions. This two-day workshop led by Chris Fonnesbeck (PyMC Labs, Vanderbilt University Medical Center) brings together rigorous theory and practical, reproducible implementations of GPs with the help of LLMs for researchers who want to use this type of Bayesian nonparametrics in their work. The workshop emphasizes not just conceptual understanding but hands-on competence with PyMC and Python supported by Gen AI via Cursor and VSCode, so participants leave able to specify, fit, diagnose, and scale GP models for publication-quality analyses.

The course is split across two intensive days: Day 1 builds foundations and core implementations (GP theory, manual kernels, PyMC GP primitives, marginal vs latent formulations, and inference choices), while Day 2 focuses on scaling and applied workflows (HSGP spectral approximations, sparse methods, multi-output models, and real-world case studies such as sports analytics). Through live coding, curated notebooks adapted from the pymc-examples gallery, short exercises, and comparative demonstrations (NUTS vs VI vs MAP; exact GP vs HSGP), participants will acquire immediate, research-ready skills applicable to complex datasets and computational constraints commonly encountered in academic projects.

## Environment Setup

### Installing Dependencies

We recommend using **pixi** for environment management, as it provides fast, reproducible dependency resolution and is configured for this repository via `pixi.toml`. However, conda/mamba instructions are also provided as an alternative.

#### Option 1: Pixi (Recommended)

Install pixi following the instructions at [https://pixi.sh](https://pixi.sh), then:

```bash
# Clone the repository
git clone https://github.com/fonnesbeck/instats_gp.git
cd instats_gp

# Install all dependencies
pixi install

# Activate the environment
pixi shell
```

To verify the installation:

```bash
python --version  # Should be 3.13+
python -c "import pymc; print(pymc.__version__)"  # Should be 5.26+
```

#### Option 2: Conda/Mamba

If you prefer using conda or mamba:

```bash
# Create environment from environment.yml
conda env create -f environment.yml

# Activate the environment
conda activate instats_gp

# Verify installation
python --version
python -c "import pymc; print(pymc.__version__)"
```

### IDE Setup for LLM-Assisted Exercises

The workshop includes hands-on exercises designed to be completed with LLM assistance for coding support. You will need either **VSCode** or **Cursor** installed to work with the Jupyter notebooks effectively.

#### Required Extensions

Install the following extensions in VSCode/Cursor:

1. **Jupyter** - Microsoft's official Jupyter extension for running notebooks
2. **Python** - Microsoft's Python language support and debugging
3. **Pixi Code** - Pixi environment integration (if using pixi)

If you want to use Claude Code, Gemini, or another external LLM tool, ensure you have the respective extensions installed as well.

To install extensions:
- Open the Extensions view (Ctrl+Shift+X / Cmd+Shift+X)
- Search for each extension by name
- Click "Install"

Once installed, you can open and run the workshop notebooks directly in your IDE with full LLM-assisted coding support.

#### Colab

If you prefer to use Google Colab, each session notebook includes a badge at the top that allows you to open it directly in Colab. Note that LLM-assisted exercises may require additional setup depending on your chosen LLM tool.

## Day 1

### Session 1: Introduction to Gaussian Processes and PyMC

- Bayesian non-parametric models
- Bayesian inference primer (Bayes' theorem, posterior updating)
- Introduction to PyMC with real data (baseball launch angles)
- Multivariate normal models with coordinates
- From multivariate normals to Gaussian processes
- Mean functions (zero, constant, linear)
- Covariance functions (ExpQuad, Matérn family, Periodic)

### Session 2: Kernels, Likelihoods, and Model Building

- The Kernel Zoo (ExpQuad, Matérn, Rational Quadratic, Periodic, Linear)
- Understanding kernel parameters (lengthscale, variance)
- Marginal likelihood with `pm.gp.Marginal`
- Latent GPs with `pm.gp.Latent`
- Additive kernel composition (trend + seasonal)
- Multiplicative kernel composition (locally periodic patterns)
- Kernel properties (stationarity, isotropy, ARD)
- Non-Gaussian likelihoods (Poisson, Student-T for robust regression)


## Day 2

### Session 3: Scaling with HSGP and Sparse methods

- Understanding computational bottlenecks
- Sparse GP approximations with inducing points
- Hilbert Space GP (HSGP) theory and implementation
- 2D spatial modeling with HSGP
- Automatic Relevance Determination (ARD)
- Decision guide for choosing scaling methods

### Session 4: Multi-Output GPs and Case Study

- Intrinsic Coregionalization Model (ICM) for correlated outputs
- Linear Coregionalization Model (LCM) for multiple timescales
- Baseball pitcher spin rate analysis
- Hierarchical logistic regression with factor models
- Soccer player skill modeling with temporal dynamics
- Three-timescale HSGP modeling (match-to-match, within-season, career trajectory)
- Maximum entropy priors for lengthscale specification
- Comprehensive case study: Separating player skill from team context


