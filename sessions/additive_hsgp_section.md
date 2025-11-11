# New Section: Additive Covariance Functions in HSGP

## Section 3.6.5: Additive Covariance Functions with HSGP

One of the powerful features of Gaussian processes is the ability to compose complex kernels from simpler building blocks through **addition** and **multiplication**. We saw earlier how to add kernels to model different components of a signal—for instance, combining a long-term trend with short-term variation, or a smooth base signal with periodic fluctuations.

When working with HSGP approximations, you might initially think you need to create separate HSGP objects for each kernel component and then add them together. However, there's a much more efficient approach that exploits the spectral representation of HSGP.

### The Naive Approach: Adding Independent HSGPs

The straightforward way to combine two GP components would be:

```python
# Naive approach - less efficient
cov1 = eta1**2 * pm.gp.cov.ExpQuad(1, ls=ell1)
cov2 = eta2**2 * pm.gp.cov.Matern32(1, ls=ell2)

gp1 = pm.gp.HSGP(m=[m], c=c, cov_func=cov1)
gp2 = pm.gp.HSGP(m=[m], c=c, cov_func=cov2)

f1 = gp1.prior('f1', X=X)
f2 = gp2.prior('f2', X=X)
f_total = f1 + f2
```

This works, but it has a major computational inefficiency: **we're computing two separate sets of basis functions and two sets of basis coefficients**, even though they're both evaluated at the same locations. For $m$ basis functions, we now have $2m$ parameters and double the computational cost.

### The Efficient Approach: Combined Power Spectral Densities

The key insight from HSGP theory is that **addition of covariance functions corresponds to addition of their power spectral densities (PSDs)**. If we have two kernels $k_1$ and $k_2$ with PSDs $S_1(\omega)$ and $S_2(\omega)$, then the combined kernel $k = k_1 + k_2$ has PSD:

$$
S(\omega) = S_1(\omega) + S_2(\omega)
$$

This means **we can create a single HSGP that represents the sum** by first adding the covariance functions, then creating one HSGP approximation. The HSGP will automatically compute the combined PSD and use a single shared set of basis functions.

Instead of constructing and then directly adding two HSGPs, the sum of two HSGPs can be computed more efficiently by first taking the sum of their power spectral densities, and then creating a single GP from the combined power spectral density. **This reduces the number of unknown parameters because the two GPs can share the same basis set.**

Here's the efficient approach:

```python
# Efficient approach - recommended
cov1 = eta1**2 * pm.gp.cov.ExpQuad(1, ls=ell1)
cov2 = eta2**2 * pm.gp.cov.Matern32(1, ls=ell2)
cov_combined = cov1 + cov2  # Add covariances BEFORE creating HSGP

gp = pm.gp.HSGP(m=[m], c=c, cov_func=cov_combined)
f_total = gp.prior('f', X=X)
```

Now we have just $m$ basis functions and $m$ basis coefficients, cutting the parameter count in half and significantly speeding up both sampling and prediction.

### Why This Works: The Mathematical Foundation

The HSGP approximation represents a GP as:

$$
f(x) \approx \sum_{j=1}^m \beta_j \sqrt{S(\omega_j)} \phi_j(x)
$$

where:
- $\beta_j$ are standard normal coefficients
- $S(\omega_j)$ is the power spectral density evaluated at eigenfrequencies
- $\phi_j(x)$ are the eigenvector basis functions (shared across all kernels!)

When we add two kernels, their PSDs add: $S(\omega) = S_1(\omega) + S_2(\omega)$. The eigenvectors $\phi_j(x)$ depend only on the domain and $m$, $c$ parameters—**not on the specific kernel**. So we can use the same basis functions for any combination of stationary kernels!

This is fundamentally different from sparse GP approximations with inducing points, where combining GPs typically requires separate inducing points for each component.

### Practical Example: Trend + Seasonal Pattern

Let's see this in action with a common modeling scenario: data with both a long-term smooth trend and short-term seasonal variation.
