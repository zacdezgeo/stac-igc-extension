# STAC IGC Extension Specification

## What Is IGC?
The International Gliding Commission (IGC) defines a compact text format for recording soaring flights. A single IGC file stores both structured metadata and a chronological GPS track in a human-readable format. Common metadata includes:
- Pilot name(s)
- Glider type and competition identifiers
- Takeoff and landing timestamps
- Declared task turnpoints (start, turn, finish waypoints with required order)
- Altitude profile information derived from barometric and GPS sensors

The flight track is embedded in the same file as a sequence of time-stamped records, so a single `.igc` file encapsulates both event metadata and the underlying trajectory.

## Why Build a STAC Extension?
While IGC files are widely adopted within the soaring community, the monolithic text format makes it difficult to integrate flights with modern, cloud-native geospatial tooling. Typical workflows require custom parsers to extract metadata and convert the track into formats that analytic engines understand, which limits discoverability and reuse.

The STAC (SpatioTemporal Asset Catalog) specification offers a mature, interoperable ecosystem for describing geospatial datasets. By expressing IGC flight metadata as STAC Item properties, and linking the original IGC file alongside derived geospatial assets (e.g., GeoParquet flight tracks), we can:
- Separate metadata from data assets while preserving provenance
- Reuse established STAC discovery, cataloguing, and validation tools
- Integrate soaring flights with analytics-ready formats used across the geospatial industry

## Repository Contents
- `schemas/igc-item.json`: JSON Schema defining the `igc` STAC Item Extension properties.
- `examples/`: Example STAC Items illustrating how to link native IGC files and derived GeoParquet assets.
- `docs/`: Supplemental documentation covering STAC alignment, GeoParquet interoperability, and the extension proposal process.
