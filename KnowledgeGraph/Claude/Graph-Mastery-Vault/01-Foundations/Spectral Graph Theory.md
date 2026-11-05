---
tags: [foundations, spectral, linear-algebra]
phase: 0
status: not-started
---
# Spectral Graph Theory

> [!summary]
> The eigenvalues/eigenvectors of graph matrices (especially the **Laplacian**) encode connectivity, clusters and smoothness. GCN is literally a cheap spectral filter.

## The Laplacians
- **Combinatorial:** $L = D - A$
- **Symmetric normalised:** $L_{sym} = I - D^{-1/2} A D^{-1/2}$, eigenvalues in $[0, 2]$
- **Random-walk:** $L_{rw} = I - D^{-1}A$; $P = D^{-1}A$ is the transition matrix

## Key properties (undirected)
1. **Quadratic form (smoothness):** $x^\top L x = \sum_{(i,j)\in E} (x_i - x_j)^2 \ge 0$ → $L$ is PSD.
2. Multiplicity of eigenvalue $0$ = number of **connected components**.
3. Second-smallest eigenvalue $\lambda_2$ = **algebraic connectivity**; its eigenvector = **Fiedler vector** (sign gives a good 2-way cut).
4. **Cheeger inequality** (normalised Laplacian): $\tfrac{\lambda_2}{2} \le h(G) \le \sqrt{2\lambda_2}$, where $h(G)$ is the conductance — small $\lambda_2$ ⇔ graph has a bottleneck. (Also explains [[Oversmoothing and Oversquashing]].)

## Spectral clustering (Ng–Jordan–Weiss style)
1. Build $L_{sym}$.
2. Take the $k$ eigenvectors with smallest eigenvalues → matrix $U\in\mathbb{R}^{n\times k}$.
3. Row-normalise $U$, run k-means on rows.

```python
import numpy as np, networkx as nx
from sklearn.cluster import KMeans
G = nx.karate_club_graph()
L = nx.normalized_laplacian_matrix(G).toarray()
w, U = np.linalg.eigh(L)
X = U[:, :2]; X = X / np.linalg.norm(X, axis=1, keepdims=True)
labels = KMeans(2, n_init=10).fit_predict(X)
```

## Graph Fourier transform (bridge to GNNs)
$L = U\Lambda U^\top$. Signal $x$ → $\hat x = U^\top x$. A spectral filter: $g_\theta(L)x = U g_\theta(\Lambda) U^\top x$.
- ChebNet: approximate $g_\theta$ with Chebyshev polynomials (K-hop localised).
- **GCN** = first-order approximation + renormalisation trick → $\tilde D^{-1/2}\tilde A \tilde D^{-1/2} X W$. See [[Graph Signal Processing]] and [[Message Passing and GNNs]].

## Exercises
- [ ] Verify numerically that #zero eigenvalues = #components on a graph with 3 components.
- [ ] Show $x^\top L x$ identity by expanding $x^\top D x - x^\top A x$.
- [ ] Compare Fiedler-vector split of the karate club with the real faction labels.

## Resources
- Spielman, *Spectral and Algebraic Graph Theory* (free draft book)
- von Luxburg, "A Tutorial on Spectral Clustering" (2007)
- Shuman et al., "The Emerging Field of Signal Processing on Graphs" (2013)

## My notes


## Self-test #flashcards/foundations
What does the multiplicity of eigenvalue 0 of L tell you?::The number of connected components.
Write the Laplacian quadratic form.::xᵀLx = Σ_(i,j)∈E (x_i − x_j)²
What is the Fiedler vector?::The eigenvector of the second-smallest Laplacian eigenvalue; its signs give a good 2-way partition.
Range of eigenvalues of the symmetric normalised Laplacian?::[0, 2]
How is GCN related to spectral filtering?::It is a first-order (K=1) Chebyshev approximation of a spectral filter with a renormalisation trick.
