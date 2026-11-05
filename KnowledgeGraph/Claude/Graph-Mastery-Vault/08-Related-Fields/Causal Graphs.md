---
tags: [related, causality]
phase: 5
status: not-started
---
# Causal Graphs

> [!summary]
> A causal DAG encodes *how data is generated*. It lets you answer interventional ("what if we do X?") and counterfactual questions that correlations can't.

## Core concepts
- **Structural causal model (SCM):** $X_i := f_i(\mathrm{PA}_i, U_i)$
- **d-separation:** read conditional independences from the DAG (chains, forks block when conditioned; colliders block unless conditioned)
- **do-operator:** $P(y \mid do(x))$ ≠ $P(y\mid x)$
- **Backdoor adjustment:** if $Z$ blocks all backdoor paths, $P(y\mid do(x)) = \sum_z P(y\mid x,z)P(z)$
- Pearl's ladder: association → intervention → counterfactual

## Causal discovery
- Constraint-based: **PC**, FCI (latent confounders)
- Score-based: **GES**
- Continuous optimisation: **NOTEARS** — acyclicity constraint $h(W)=\mathrm{tr}(e^{W\circ W}) - d = 0$
- Tools: `causal-learn`, DoWhy, `pgmpy`

## Links to KGs
Causal KGs (cause–effect relations extracted from text), using KGs as priors for discovery, causal reasoning in LLM agents.

## Reading
Pearl, *Causality*; Peters, Janzing & Schölkopf, *Elements of Causal Inference* (free).

## My notes


## Self-test #flashcards/related
Backdoor adjustment formula?::P(y | do(x)) = Σ_z P(y | x, z) P(z), with Z blocking all backdoor paths.
When does a collider block a path?::When neither the collider nor its descendants are conditioned on.
NOTEARS acyclicity constraint?::h(W) = tr(exp(W∘W)) − d = 0
