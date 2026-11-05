---
tags: [related, gsp, spectral]
phase: 5
status: not-started
---
# Graph Signal Processing (GSP)

> [!summary]
> Treat node features as **signals on a graph** and generalise Fourier analysis and filtering. This gives the cleanest explanation of what GCNs actually compute.

## Essentials
- Signal $x\in\mathbb{R}^n$; **smoothness** $x^\top L x$ ([[Spectral Graph Theory]])
- **Graph Fourier transform:** $\hat x = U^\top x$ (eigenvectors of $L$); eigenvalues = frequencies
- **Filtering:** $y = U\, g(\Lambda)\, U^\top x$
- **Polynomial filters:** $g(L) = \sum_{k=0}^{K}\theta_k L^k$ → K-hop localised, no eigendecomposition needed
- **Chebyshev filters** (ChebNet), Cayley filters, ARMA filters
- **GCN = low-pass filter**; heterophilous graphs need high-pass/band-pass (GPR-GNN, FAGCN, BernNet)
- Sampling & reconstruction of graph signals; graph wavelets

## Reading
Shuman et al. (IEEE SPM 2013); Ortega et al. "Graph Signal Processing: Overview, Challenges and Applications" (Proc. IEEE 2018); Ortega, *Introduction to Graph Signal Processing* (CUP 2022).

## My notes


## Self-test #flashcards/related
Graph Fourier transform of x?::x̂ = Uᵀx, where U are Laplacian eigenvectors.
Why are polynomial filters attractive?::They are K-hop localised and need no eigendecomposition.
What type of filter is a GCN layer?::A low-pass filter (smooths signals over neighbours).
