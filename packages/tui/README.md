# TUI Package (`packages/tui`)

## Purpose
This package provides a terminal interface for local operator workflows.

It supports running analysis jobs and inspecting artifacts from the command line.

## Scope
Responsibilities:
- run ingestion and analysis workflows locally (through pipeline package integrations)
- inspect artifact status and execution results
- explore convergence/divergence fields from CLI views
- inspect provenance and variable overlap/non-overlap metadata
- support operator-oriented troubleshooting and validation

Non-goals:
- public web publishing
- replacing canonical artifact generation logic in the pipeline package

## Interface Role
The TUI is the operational complement to the site package:
- site: public, static, explanatory
- tui: local, exploratory, operational

Both consume the same artifact contract and conceptual model.

## Typical Local Lifecycle
1. trigger or monitor a pipeline run
2. load produced artifacts locally
3. inspect convergence metrics, verification status, and provenance traces
4. compare variable overlap/non-overlap across source families
5. export or hand off artifacts for site rendering
