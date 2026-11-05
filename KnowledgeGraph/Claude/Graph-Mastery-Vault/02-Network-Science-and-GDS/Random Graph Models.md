---
tags: [network-science]
phase: 1
status: not-started
---
# Random Graph Models

> [!summary]
> Null models tell you what "random" looks like, so you can tell whether a real network's structure (hubs, clustering, communities) is surprising.

## Erdős–Rényi $G(n,p)$
- Each edge independently with prob. $p$. Mean degree $\langle k\rangle = p(n-1)$; degrees ~ **Poisson**.
- **Giant component** emerges when $\langle k\rangle > 1$; graph becomes connected when $p \gtrsim \ln n / n$.
- Low clustering $C \approx p$; short paths $\ell \sim \ln n / \ln\langle k\rangle$.

## Watts–Strogatz (small world)
- Ring lattice + random rewiring prob. $\beta$ → **high clustering AND short paths** for small $\beta$.

## Barabási–Albert (scale-free)
- Growth + **preferential attachment** $\Pi(k_i) = k_i / \sum_j k_j$ → $P(k) \sim k^{-3}$.
- Hubs, robustness to random failure, fragility to targeted attacks.
- ⚠️ Debate: Broido & Clauset (2019) found strict power laws are rarer than claimed — always fit carefully (e.g., `powerlaw` package, compare to log-normal).

## Configuration model
- Random graph with a **given degree sequence** — the null model behind **modularity** ([[Community Detection]]).

## Stochastic Block Model (SBM)
- Nodes in blocks; edge prob. depends on block pair. Generative model for communities; used to make synthetic GNN benchmarks (homophily vs heterophily).

## Key network statistics
| Statistic | Definition | Meaning |
|---|---|---|
| Clustering coefficient | $C_i = \frac{2T_i}{k_i(k_i-1)}$ | Friends of friends are friends |
| Assortativity | Degree correlation across edges | Social (+), technological/biological (−) |
| Average path length | Mean shortest-path distance | "Six degrees" |
| Degree distribution | $P(k)$ | Hubs? Heavy tail? |
| Friendship paradox | Neighbours have higher mean degree | Sampling bias |

## Exercise
- [ ] Generate ER, WS, BA graphs with n=2000, ⟨k⟩≈6; compare $P(k)$ (log-log), $C$, $\ell$, and robustness under random vs targeted node removal.

## Resources
- Barabási, *Network Science*, ch. 3–5, 8
- Newman, *Networks*, ch. 11–13

## My notes


## Self-test #flashcards/network-science
Degree distribution of an Erdős–Rényi graph?::Binomial, approximately Poisson for large n.
When does a giant component appear in G(n,p)?::When the mean degree exceeds 1.
Mechanism behind the BA model?::Growth plus preferential attachment, giving P(k) ~ k^-3.
What two properties does the Watts–Strogatz model combine?::High clustering and short average path length.
Which null model underlies modularity?::The configuration model (random graph with the same degree sequence).
