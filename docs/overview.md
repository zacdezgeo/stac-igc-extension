# IGC STAC Extension Overview

## Why STAC?
The IGC STAC Extension aligns soaring flight records with a catalog standard that is already widely adopted for earth observation and mobility data. STAC offers:
- A consistent Item structure that mirrors the temporal and spatial nature of glider flights.
- Built-in cataloging, search, and validation tooling maintained by a large community.
- A well-defined mechanism for community extensions, making it easy to introduce new domains without fragmenting the ecosystem.

By reusing the STAC Item model, IGC flights become discoverable alongside satellite imagery, aerial surveys, and other spatiotemporal assets. This supports downstream workflows such as weather correlation, task debriefing, and cross-event analytics.

## Mapping IGC Metadata to STAC
The extension translates key IGC header and derived metrics into namespaced Item properties:
- `igc:pilot`, `igc:co_pilot`, and `igc:glider` retain information about the crew and aircraft.
- `igc:takeoff_time` and `igc:landing_time` provide precise temporal bounds.
- `igc:altitude_min_m` and `igc:altitude_max_m` summarize the altitude envelope, with `igc:altitude_reference` clarifying the sensor.
- `igc:turnpoints` captures declared tasks as ordered locations, enabling geographic filtering and visualization.

The original `.igc` file is cataloged as an Item asset, preserving the authoritative record. Additional derived outputs—such as a GeoParquet trajectory with full temporal sampling—are referenced as complementary assets so that analysts can choose the format that best suits their tools.

## GeoParquet Interoperability
GeoParquet is an open, columnar storage format optimized for analytics in cloud environments. Publishing a GeoParquet version of each flight track enables:
- Direct ingestion into big-data processing frameworks (Apache Spark, DuckDB, BigQuery).
- Efficient spatial querying and filtering with standard SQL.
- Interoperability with visualization and analysis libraries (GeoPandas, kepler.gl, HoloViz) that already understand Parquet-backed geometries.

The STAC Item schema encourages including both the IGC original and GeoParquet derivative, with `roles` clarifying provenance. This pattern mirrors best practices for other STAC datasets that maintain raw and analysis-ready assets side by side.

## Path to a Community Extension
To progress from this specification prototype to an official STAC Community Extension:
1. **Discuss in STAC forums** – Share the motivation and draft schema with the STAC community via the `#community-extensions` channel on the STAC Slack and the GitHub discussions board.
2. **Iterate on feedback** – Incorporate comments about field naming, optionality, and alignment with related mobility extensions.
3. **Publish documentation site** – Host the schema, examples, and narrative documentation using the standard `stac-extensions.github.io` pattern.
4. **Prepare validation tooling** – Contribute JSON Schema tests or linting snippets to help catalog maintainers validate Items adopting the extension.
5. **Submit a pull request** – Add the extension to the official STAC Community Extensions registry once consensus is reached.
