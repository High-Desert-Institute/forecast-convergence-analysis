# Forecast Convergence Analysis Monorepo

## Overview
Forecast Convergence Analysis is one analytical technique implemented and exposed through three packages in one monorepo:

1. `packages/pipeline` is the canonical Python implementation of the method.
2. `packages/site` renders public artifacts as a static website built by GitHub Actions.
3. `packages/tui` provides a terminal operator interface for local runs and inspection.

This repository is organized as method -> artifacts -> interfaces.

## What Forecast Convergence Analysis Is
Forecast Convergence Analysis treats weather forecasts as evolving claims about the future. It preserves those claims over time, compares how they change, evaluates where they converge or diverge, and tests them against observed reality at the line of now.

The method studies the unstable field between:
- a moving threshold where contradictory forecast claims begin to converge into actionable consensus
- a static boundary of now where forecast becomes fact and can be verified

## Monorepo Layout
```text
forecast-convergence-analysis/
|-- packages/
|   |-- pipeline/   # Python ingestion + normalization + analysis + artifact generation
|   |-- site/       # Static website that renders published artifacts
|   `-- tui/        # Terminal interface for local execution and inspection
|-- docs/
|   `-- pipeline/   # Detailed method and source reference material
|-- config/
|-- scripts/
|-- .github/workflows/
|-- agents/
`-- README.md
```

## Core Conceptual Model
The project uses a critical sociological lens: forecast systems are claimsmaking systems. Each run is a structured claim shaped by model family, institution, variable vocabulary, and processing lineage.

The method preserves:
- forecast claims and their revisions
- variable vocabularies and comparability classes
- full provenance chains
- convergence/divergence histories
- verification outcomes against observed reality

## Method Workflow (Pipeline-Centered)
The canonical workflow lives in `packages/pipeline`:

1. Ingest forecast and observation products.
2. Decode and normalize claims while preserving provenance.
3. Align comparable variables across overlapping and non-overlapping vocabularies.
4. Compute convergence/divergence and higher-order evolution signals.
5. Evaluate historical performance against observations at the line of now.
6. Emit standardized artifacts for downstream interfaces.

## Artifact Contract
`packages/pipeline` emits artifacts consumed by both `packages/site` and `packages/tui`.

Required artifact families:
- normalized forecast-claim records
- provenance metadata and lineage records
- variable-comparison metadata and comparability classes
- convergence/divergence and spread metrics
- derivative and stability signals
- verification outputs and historical skill profiles
- precomputed summaries for low-bandwidth publication

Contract implications:
- the website does not perform heavy analysis; it renders published artifacts
- the TUI may trigger pipeline runs locally, but it inspects the same artifact model
- both interfaces expose the same conceptual objects (convergence field, consensus boundary, provenance graph, hysteresis trace, line of now)

## Package Responsibilities and Non-Goals
### `packages/pipeline`
Responsibilities:
- ingestion, decode, normalization, provenance
- analysis, verification, artifact generation
- variable-universe modeling and comparability mapping

Non-goals:
- public presentation/UI rendering

### `packages/site`
Responsibilities:
- consume published artifacts
- render static explanatory/public visualizations
- publish through GitHub Actions

Non-goals:
- heavy analytical computation

### `packages/tui`
Responsibilities:
- local operator workflows
- run jobs, inspect artifacts, investigate convergence/provenance from CLI

Non-goals:
- public web publishing

## Visualization Philosophy
The site and TUI are two views of the same technique:
- site: public, static, explanatory rendering
- tui: operational, exploratory, analyst-oriented rendering

Both interfaces should expose the same analytical primitives, only with different interaction depth.

## Data Sources Overview
Data sources are inputs to the pipeline package, not to the monorepo in the abstract. The pipeline is expected to support a broad, resilient mix of:
- global deterministic and ensemble forecast products
- blended/post-processed products
- regional model products
- satellite and remote-sensing observations
- surface/radar/hydrological observations
- retrospective archives (reforecasts, hindcasts, archived operational runs)

Detailed source inventories and long-form source analysis are maintained in package docs rather than this root README.

## Monorepo Development Flow
1. Pipeline job runs and produces artifacts.
2. Artifacts are published to a known location/version.
3. Site build workflow ingests those artifacts and renders static outputs.
4. TUI uses local artifacts for execution, inspection, and operator analysis.

## Further Documentation
- Pipeline package docs: [`packages/pipeline/README.md`](packages/pipeline/README.md)
- Pipeline detailed docs index: [`docs/pipeline/README.md`](docs/pipeline/README.md)
- Site package docs: [`packages/site/README.md`](packages/site/README.md)
- TUI package docs: [`packages/tui/README.md`](packages/tui/README.md)
- Full pre-monorepo detailed reference preserved at [`docs/pipeline/detailed-technique-reference.md`](docs/pipeline/detailed-technique-reference.md)
