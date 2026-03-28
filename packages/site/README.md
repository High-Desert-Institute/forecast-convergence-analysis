# Site Package (`packages/site`)

## Purpose
This package renders public-facing outputs from pipeline artifacts.

It is a static website package intended to be built and published through GitHub Actions.

## Scope
Responsibilities:
- ingest published artifacts from `packages/pipeline`
- render static pages, charts, and summaries
- expose convergence, consensus, provenance, and verification views for public use
- produce low-bandwidth friendly outputs where possible
- publish through `.github/workflows`

Non-goals:
- heavy analytical computation
- replacing pipeline artifact generation

## Build Contract
Input contract:
- versioned artifact bundle produced by `packages/pipeline`
- standardized metadata for provenance and variable comparability

Output contract:
- static site assets suitable for GitHub Pages or equivalent static hosting
- explanatory/public visualizations over precomputed analysis objects

## GitHub Actions Flow
Expected workflow shape:
1. fetch pipeline artifact bundle
2. validate artifact schema/version
3. build static site from artifacts
4. publish rendered output

## Public Visualization Role
This package is the explanatory and public interface over shared analytical objects:
- convergence field
- moving consensus boundary
- line of now verification boundary
- variable overlap map
- provenance graph
- hysteresis/evolution traces
