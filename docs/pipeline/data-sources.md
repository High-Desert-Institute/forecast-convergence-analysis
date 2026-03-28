## Data Sources

The project should be designed to ingest the broadest practical mix of forecast, observational, and verification data that is legally accessible, technically retrievable, and useful for comparative profiling.

The project should not be framed around ingesting one preferred model. It should be framed around building a diverse forecast constellation and then profiling how that constellation evolves over time.

## Source Strategy

The goal is to ingest a heterogeneous set of products across:

* global deterministic models
* global ensemble systems
* blended and post-processed forecast products
* regional and limited-area models
* satellite and remote-sensing observations
* surface and environmental observations
* historical reforecasts, hindcasts, and archives

This diversity matters for both scientific and political reasons. It reduces dependence on any one provider, improves resilience when agencies are degraded or underfunded, and creates the raw material needed to build stronger meta-ensemble forecasts and confidence diagnostics.

## Forecast Model Sources

### ECMWF Forecast Products

ECMWF should be treated as a major first-class source family, not as an optional add-on.

Use cases:

* high-skill global forecast guidance
* deterministic and ensemble comparison
* long-range signal analysis
* historical profiling of stability and skill
* comparison of raw guidance with other model families

Important characteristics:

* strong international reputation for forecast skill
* open real-time catalogue availability for many products
* open data products are a subset of the broader ECMWF real-time catalogue
* current open real-time IFS and AIFS products are available in GRIB2 at 0.25 degree resolution on a rolling archive basis

Potential products of interest include:

* deterministic forecast products
* ensemble products
* AIFS and other machine-learning-related forecast products where available
* oceanographic and related forecast fields where relevant
* reanalysis and retrospective products where licensing and access permit

### DWD ICON Family

DWDâ€™s ICON products should be included as another major source family.

Use cases:

* global model comparison
* limited-area and regional analysis where available
* cross-family divergence and convergence tracking
* contrasting physics and model structure against other systems

Important characteristics:

* DWD distributes numerical forecast data from all models in GRIB2
* forecast data for each weather element are made available in standard packages on the DWD Open Data Server
* the ICON family spans global, European nested, and short-range high-resolution regional products

Potential products of interest include:

* ICON global guidance
* ICON-EU
* ICON-D2
* ICON-D2 EPS
* aerosol, dust, radiation, and specialized ICON-related products where accessible

### UK Met Office Products

Met Office forecast products should be included wherever legally and technically accessible through current public-task or other supported access paths.

Use cases:

* additional independent model family comparison
* regional and global guidance comparison where available
* post-processed product comparison
* institutional-diversity support in the meta-ensemble layer

Important characteristics:

* Weather DataHub is the current access pathway for public-task and related weather data services
* products can be subset by region, time step, model run, and parameter
* current products include deterministic and probabilistic site-specific offerings built from multiple models and runs

### NOAA / NCEP Products

NOAA and NCEP products remain important, but they should be treated as one source family among many rather than the center of the architecture.

Potential products of interest include:

* GFS
* GEFS
* GDAS
* NBM
* related open NCEP products
* emerging AI-ensemble and hybrid products where open access is available

Use cases:

* deterministic and ensemble comparison
* blended guidance comparison
* long-run historical continuity in many workflows
* broad open-data availability

Important characteristics:

* GFS products are distributed in multiple packaged forms, including most commonly used and least commonly used parameter groupings
* a single sample GFS 0.25 degree forecast file can contain hundreds of GRIB records for one forecast step, reflecting the fact that operational forecast systems carry many more variables than end users ever directly inspect
* GEFS inventories are explicitly intended to guide parameter selection through NOMADS filtering workflows

### Environment and Climate Change Canada Products

Canadian forecast products should be supported where open access and practical retrieval make that possible.

Use cases:

* independent global or regional guidance comparison
* additional ensemble diversity
* seasonal and regional reliability profiling

### JMA and Other National Meteorological Agency Products

The project should be architected to include forecast products from additional meteorological agencies whenever legally accessible.

Examples may include:

* JMA products
* Meteo-France products where accessible
* AEMET and other European services where accessible
* Australian Bureau of Meteorology products where accessible
* other national agencies with open forecast or observational feeds

The exact list should remain flexible and expand over time.

### Regional and Specialized Forecast Products

The system should also support specialized or regional products such as:

* convection-allowing models
* fire-weather-oriented products
* hydrological forecast products
* marine and wave products
* downscaled regional guidance
* machine-learning or hybrid forecast systems

These are especially valuable because some impacts are better captured by regional or specialized systems than by the major global models alone.

## Variable Universes, Overlap, and Non-Overlap

A central design principle of the project is that different forecast systems do not speak in exactly the same variable vocabulary.

Some variables overlap heavily across systems:

* 2 m temperature
* dew point or humidity near the surface
* wind components
* pressure
* precipitation accumulations
* cloud cover
* geopotential height
* common pressure-level fields

Other variables are only present in some systems, are available only on certain levels, are packaged differently, or are derived using different parameterizations, assimilations, or post-processing pipelines.

Examples include:

* hydrometeor-specific fields such as graupel, cloud liquid water, cloud ice, rain mixing ratio, and snow mixing ratio
* aerosol and dust products
* specialized convective diagnostics
* soil and land-surface states
* radiation flux variants
* wave, marine, and coastal fields
* blended probability products and calibrated site-specific outputs
* machine-learning-generated forecast products

This matters because the public often experiences weather as a small set of consumer-facing outcomes, while the underlying model systems are built from much larger internal state spaces.

A user may only care about rain tomorrow, but that forecast may depend on a huge interacting field of temperature structure, winds, humidity, pressure, surface fluxes, cloud physics, soil conditions, ocean coupling, radiation balances, hydrometeor distributions, and assimilation inputs.

The result is that each model family carries a distinct variable universe:

* a set of variables it shares with others
* a set of variables it alone exposes or emphasizes
* a set of variables it derives differently from others
* a set of variables that are hidden internally, downsampled, blended, or omitted in public products

The project should therefore model not only forecast values, but forecast provenance through variable coverage and variable comparability.

### Why Variable Coverage Matters

Differences in confidence, chaos, variability, and accuracy across models are not only about headline skill scores. They are also partly consequences of:

* what each model measures or assimilates
* what each model outputs publicly
* how each variable is defined and encoded
* the vertical levels and temporal resolutions used
* the resolution and domain of the model
* the post-processing and blending applied before dissemination
* what variables are absent, latent, or inaccessible in public data

That means overlapping variables should not be treated as automatically identical, and non-overlapping variables should not be dismissed as irrelevant.

Both overlap and non-overlap are informative.

Overlap allows direct comparative profiling.

Non-overlap reveals different ways of seeing the atmosphere, different assumptions about what matters, and different internal structures through which forecast systems construct their claims about the future.

### Provenance and Interpretive Consequences

The same apparent forecast product may arise from very different upstream realities.

For example:

* one provider may expose raw gridded fields directly from a deterministic model
* another may expose ensemble summaries
* another may expose statistically calibrated or blended site-specific products
* another may package variables by forecast element rather than by monolithic full-state output
* another may provide only a public subset of a much larger catalogue

This means provenance is not a metadata footnote. It is part of the claim itself.

The project should preserve, compare, and expose:

* model family
* data producer
* product type
* deterministic versus ensemble versus blended status
* forecast resolution and domain
* level structure
* variable definitions
* public subset versus full-catalogue status where relevant
* known changes in model configuration over time

Without that, consensus can become misleading. Apparent agreement may simply reflect shared ancestry, shared data assimilation assumptions, shared post-processing, or the fact that two products are not independent in the first place.

### Variable Comparison Matrix

The project should include and maintain a detailed comparison matrix of variables across source families.

At minimum, that matrix should track for each source family:

* variable name
* standard name where available
* short code or parameter identifier
* units
* level or layer type
* temporal resolution
* spatial resolution
* deterministic, ensemble, derived, or blended status
* whether the variable is raw, post-processed, or probabilistic
* whether the variable has a close analogue in other systems
* notes on comparability caveats

This matrix should be a first-class research object of the project, not an afterthought.

### Initial Comparison Categories

The first implementation should likely organize variables into categories such as:

* core surface state variables
* pressure-level atmospheric variables
* moisture and precipitation variables
* cloud and hydrometeor variables
* land and soil variables
* radiation and energy flux variables
* aerosol and atmospheric composition variables
* severe-weather and convective diagnostics
* ocean, marine, and wave variables
* blended probabilities and percentile products
* verification and observational analogs

### Example of the Scale of the Problem

Official product documentation already illustrates the scale and heterogeneity of the variable universe.

NCEP GFS documentation separates â€œmost commonly usedâ€ and â€œleast commonly usedâ€ parameter packages, and a sample single GFS forecast file inventory lists 743 records for one forecast step. Those records include common public-interest variables such as mean sea-level pressure and visibility, but also internal or specialist variables such as cloud mixing ratio, ice water mixing ratio, rain mixing ratio, snow mixing ratio, graupel, reflectivity, and boundary-layer ventilation metrics.

ECMWF explicitly documents that its open data offerings are only a subset of the broader real-time catalogue, meaning that any public-facing comparative system must remain aware that the exposed variable universe may not be the full internal or licensable one.

DWD explicitly distributes forecast data by weather element in standard packages across the ICON family, including not only conventional forecast elements but also specialized products such as dust-related variables in some contexts.

These differences are not incidental. They are part of why the long-tail forecast space is chaotic, uneven, and difficult to interpret.

## Variable Universes and the Liminal Forecast Field

The liminal forecast field is shaped by overlapping and non-overlapping variables.

The public often sees a tiny projection of this field through a handful of headline outputs. But underneath those outputs lies a much denser, unevenly exposed ensemble view of atmospheric ground truth assembled from many overlapping and non-overlapping perspectives.

Those perspectives differ because forecast producers:

* observe different things
* ingest different observations
* parameterize processes differently
* expose different variables publicly
* blend or calibrate outputs differently
* operate on different domains, resolutions, and timescales

This is part of what generates the chaotic long-tail space.

The long-tail is not chaotic only because the atmosphere is difficult. It is also chaotic because many partially overlapping systems of representation are competing to describe an unfinished future from different standpoints and with different internal vocabularies.

The project therefore needs to ask not only:

* what do the models say?

but also:

* what variables are they speaking through?
* where do those variables overlap?
* where do they not overlap?
* what kinds of atmospheric reality are overrepresented, underrepresented, or translated differently?
* how do these representational differences shape consensus, instability, and apparent skill?

This is the deeper terrain in which liminal consensus emerges.

The projectâ€™s goal is to identify the boundary in forecast space between:

* the liminal consensus field where signals are beginning to stabilize
* the edge-of-chaos boundary where coherence and incoherence are in tension
* the oracular hysterical frontier beyond that line, where forecasts remain unstable, contradictory, and weakly grounded

Understanding variable provenance and variable overlap is essential to locating that boundary honestly.

## Satellite and Remote-Sensing Sources

### GOES Direct Broadcast / GRB

GOES GRB and related satellite products are observational inputs, not the same thing as numerical model forecasts.

Use cases:

* cloud and moisture context
* lightning and convective development context where available
* smoke, fire, and atmospheric feature monitoring
* observational support for forecast interpretation
* near-real-time environmental awareness

### Other Geostationary and Polar Satellite Sources

The architecture should support future ingestion from additional open satellite sources where practical.

Possible examples:

* Meteosat products
* Himawari products
* polar-orbiting weather satellite products
* precipitation products
* soil moisture products
* land-surface and atmospheric derived products

These sources can strengthen the observational side of the platform and improve contextual understanding of forecast evolution.

## Observational and Verification Sources

These are needed to compare predictions against reality.

### Surface Observations

Use cases:

* temperature verification
* wind verification
* pressure verification
* precipitation verification where station data is appropriate
* historical skill profiling

Possible inputs:

* airport and meteorological station observations
* public surface observation feeds
* mesonet-style station networks
* community weather stations where quality control is possible

### Radar-Derived and Precipitation Observations

Use cases:

* precipitation verification
* event characterization
* storm evolution context
* comparison against forecast precipitation and convective guidance

### Hydrological and Environmental Observations

Use cases:

* river and streamflow context
* drought and soil conditions
* fire weather context
* environmental impact reporting

### Community and Hyperlocal Weather Station Networks

This project should be able to incorporate community-owned or hyperlocal weather stations over time.

Use cases:

* local calibration
* neighborhood-scale verification
* improved understanding of microclimates
* resilience-oriented local forecasting

This is especially relevant for community weather observatory efforts and for refining larger-scale models with local truth data.

## Historical and Retrospective Datasets

### Reforecasts and Hindcasts

Historical retrospective forecast datasets are important for profiling model behavior over long periods.

Use cases:

* train calibration layers
* compare current spread behavior with historical analogs
* estimate how often stable-looking tails actually verify well
* build climatological expectations for model skill
* compare how quickly different model families historically stabilize

### Archived Operational Runs

Archived forecasts should be preserved whenever feasible.

Use cases:

* reconstruct forecast evolution for past events
* retrospective case studies
* model-specific performance studies
* public examples of forecast stabilization or bust behavior
* multi-model comparison across historical events

## Why Source Diversity Is Central

A diverse source strategy is not just a nice feature. It is central to the whole point of the project.

The project is trying to identify where the most accurate view of the future lies by comparing:

* what each forecast system says
* how each forecast system changes over time
* how the higher derivatives of those changes behave
* where independent systems converge or diverge
* which systems have historically performed best for similar contexts
* how differences in variable universes shape what each system is capable of claiming in the first place

That means the architecture should be designed to absorb as many relevant forecast perspectives as possible rather than treating one model as authoritative.

