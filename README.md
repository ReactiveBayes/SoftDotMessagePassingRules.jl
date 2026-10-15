# SoftDotMessagePassingRules

[![CI](https://github.com/ReactiveBayes/SoftDotMessagePassingRules.jl/actions/workflows/CI.yml/badge.svg?branch=main)](https://github.com/ReactiveBayes/SoftDotMessagePassingRules.jl/actions/workflows/CI.yml)
[![Docs: stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://reactivebayes.github.io/SoftDotMessagePassingRules.jl/stable/)
[![Docs: dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://reactivebayes.github.io/SoftDotMessagePassingRules.jl/dev/)
[![Coverage](https://codecov.io/gh/ReactiveBayes/SoftDotMessagePassingRules.jl/graph/badge.svg)](https://codecov.io/gh/ReactiveBayes/SoftDotMessagePassingRules.jl)
[![Code style: Runic](https://img.shields.io/badge/code_style-%E1%9A%B1%E1%9A%A2%E1%9A%BE%E1%9B%81%E1%9A%B2-black)](https://github.com/fredrikekre/Runic.jl)

The SoftDot node, `y ~ N(θᵀx, γ⁻¹)`: a dot product of `θ` and `x` softened by Gaussian noise of
precision `γ`, with its variational rules, all in closed form. It serves Bayesian linear
regression with a learnt noise precision, and dot products of two Gaussian unknowns, which the
deterministic dot product node has no closed form for. The rules run under mean-field or the
structured `q(y, x)q(θ)q(γ)`, with an average energy for each; there are no belief-propagation
rules.

```julia
using MessagePassingRulesBase, SoftDotMessagePassingRules, ExponentialFamily

q = (y = NormalMeanVariance(1.0, 1.0), θ = NormalMeanVariance(1.0, 1.0), x = NormalMeanVariance(1.0, 1.0))
getresult(@call_message_update_rule(node = SoftDot, target = :γ, q = q))   # GammaShapeRate(1.5, 2.0)
```

```julia
import Pkg; Pkg.add("SoftDotMessagePassingRules")
```

- Documentation: <https://reactivebayes.github.io/SoftDotMessagePassingRules.jl/stable/>.
  `make docs` builds it locally, into `docs/build`.
- Tests: `make test` runs the suite as CI does, ending with the rule-coverage gate: every rule
  must be selected by some test. `make test test_args="name:rules"` selects items by tag, by
  name or by file; `make help` lists the other targets.
- Julia 1.10 or later. MIT licence.
