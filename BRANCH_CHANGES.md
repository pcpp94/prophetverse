# Branch change rationale

This branch, `piecewiseflattrend_and_minors`, adds focused coverage for the
inference engines and verifies the default random-key behavior introduced by
the related engine changes.

## Why these changes were made

- `tests/engine/test_mcmc.py` checks `MCMCInferenceEngine` defaults, custom
  configuration, tags, and NUTS kernel construction. This protects the public
  inference configuration from regressions.
- `tests/engine/test_prior.py` checks
  `PriorPredictiveInferenceEngine` defaults, substitutions, and tags. This
  confirms that prior-predictive inference preserves its expected setup.
- `tests/engine/test_map.py` now verifies that `MAPInferenceEngine` uses the
  deterministic default JAX key when no key is supplied. This makes the
  reproducibility contract explicit in the tests.

Together, these changes document and enforce the expected initialization and
configuration behavior across the MCMC, prior-predictive, and MAP engines.
