## System Architecture

## 1. Ingestion Layer

The ingestion layer is responsible for detecting new forecast cycles and observational data products, downloading the relevant content, and preserving raw files.

Responsibilities:

* poll source endpoints for newly available runs
* fetch new forecast products as soon as they are published
* fetch observations and satellite-derived products as needed
* store raw files in durable object storage
* maintain inventories and checksums
* support partial, filtered, or indexed retrieval where possible to save bandwidth

### Ingestion Cadence

Examples:

* ingest each GFS cycle as it becomes available
* ingest ensemble products as they are published
* ingest blended products on their own release cadence
* ingest observations on a schedule suitable for verification workflows
* ingest direct-broadcast or satellite-derived products on a separate near-real-time path

## 2. Decode and Normalization Layer

This layer converts raw source files into a common internal schema while retaining source-specific metadata.

Responsibilities:

* decode GRIB and GRIB2 products
* preserve native metadata such as levels, member numbers, and grid definitions
* extract selected variables, levels, and geographic regions
* normalize units and naming where needed
* generate structured forecast-claim records
* support regridding only when necessary, while preserving provenance

## 3. Storage Layer

The storage layer should separate raw archives from analysis-ready records.

Recommended storage types:

* object storage for raw files
* columnar or analytical storage for extracted forecast claims
* time-series indexed storage for run-history analysis
* relational metadata store for inventories, provenance, and configuration
* geospatial indexing for regions, points, and derived map layers

The most important design requirement is preserving both:

* run initialization time
* forecast valid time

Without both, the project cannot reconstruct the history of forecast evolution.

## 4. Analysis Layer

This layer computes the actual forecast-evolution intelligence.

Responsibilities:

* run-to-run drift calculations
* second- and third-derivative calculations
* sign-flip detection
* consensus and clustering analysis across models
* ensemble spread and spread-change analysis
* persistence and stability scoring
* regime-aware and season-aware skill analysis
* impact-oriented summarization

## 5. Verification Layer

This layer compares past forecasts to observed outcomes.

Responsibilities:

* align forecast claims with real observations at matching valid times and locations
* compute deterministic and probabilistic verification metrics
* maintain historical skill profiles by model, variable, lead time, region, and season
* identify systematic biases
* characterize when forecast-stability signals actually correspond to increased skill

## 6. Publishing Layer

This layer turns analysis outputs into public products.

Responsibilities:

* website generation
* APIs for downstream use
* static reports and charts
* location pages
* compact summaries for intermittent connectivity
* future offline and mesh-distribution formats

---

## Recommended Data Model

### Forecast Claim

Every extracted forecast record should contain at minimum:

* source
* model family
* product name
* run initialization timestamp
* valid timestamp
* lead time
* variable name
* units
* vertical level or layer if relevant
* location or grid coordinates
* ensemble member identifier if relevant
* raw value
* normalized value if applicable
* provenance information
* file identifier

### Observation Record

Observation and verification records should contain:

* source
* observation timestamp
* variable
* units
* location
* measured value
* quality-control flags
* provenance

### Derived Metric Record

Derived analysis records should contain:

* referenced forecast claims
* metric type
* computation time
* variable and location
* output score
* confidence classification if applicable
* explanatory metadata

---

