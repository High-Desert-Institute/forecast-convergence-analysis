# Pipeline Package (`packages/pipeline`)

## Purpose
This package is the canonical implementation of Forecast Convergence Analysis.

It owns the method itself: ingestion, normalization, provenance, analysis, verification, and artifact generation.

## Scope
Responsibilities:
- ingest forecast and observation products
- decode source formats and normalize forecast claims
- preserve provenance and lineage metadata
- model overlapping and non-overlapping variable vocabularies
- assign comparability classes for cross-source analysis
- compute convergence/divergence, spread, and derivative stability signals
- evaluate historical performance against observations at the line of now
- emit standardized artifacts for downstream consumers

Non-goals:
- public web presentation
- heavy UI concerns

## Method Workflow
1. Ingest claims and observations.
2. Normalize claims into comparison-ready schema.
3. Preserve provenance for every transformation and source.
4. Align variables through overlap/non-overlap comparability mapping.
5. Compute convergence and instability signals.
6. Verify against observed outcomes.
7. Emit artifact bundles for interface packages.

## Artifact Outputs
The package should emit at least:
- `forecast_claims` normalized records
- `provenance` records and lineage pointers
- `variable_comparison` metadata
- `convergence_metrics`
- `stability_metrics` and derivative signals
- `verification_metrics`
- `historical_skill_profiles`
- `publication_summaries` (compact outputs for low-bandwidth publishing)

## Package Contract to Other Packages
- `packages/site` consumes published artifacts and renders them statically.
- `packages/tui` consumes local artifacts for operator inspection and execution workflows.
- Neither interface package should redefine analytical truth independently of this package.

## Variable Universe and Sociological Lens
This package implements the project's claimsmaking lens directly:
- forecasts are treated as claims, not neutral facts
- provenance is part of claim meaning
- overlap and non-overlap in variable vocabularies are first-class analytical inputs
- convergence is interpreted as an emergent process, not a single final value

## Data Sources
Data source strategy and detailed inventories are maintained in:
- [`../../docs/pipeline/README.md`](../../docs/pipeline/README.md)
- [`../../docs/pipeline/data-sources.md`](../../docs/pipeline/data-sources.md)
- [`../../docs/pipeline/detailed-technique-reference.md`](../../docs/pipeline/detailed-technique-reference.md)

These docs preserve the full detailed source and methodological framing from the pre-monorepo README.
