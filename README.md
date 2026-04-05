# cdif-core

Core interoperability specifications for CDIF (Cross-Domain Interoperability Framework). This repository contains examples and guidance for CDIF Core profile metadata — the base level of CDIF conformance covering fundamental resource description properties (identifier, title, distribution, rights, type, dates, creator, publisher, keywords, etc.).

Examples that use Discovery-level properties (spatialCoverage, temporalCoverage, variableMeasured, measurementTechnique) are in the [Discovery repository](https://github.com/Cross-Domain-Interoperability-Framework/Discovery/tree/main/examples).

## Examples

The `examples/` directory contains JSON-LD dataset metadata that validates against the [cdifCore](https://github.com/Cross-Domain-Interoperability-Framework/metadataBuildingBlocks) schema. Sources include:

- **CDIF examples** — Minimal, simple, and multi-distribution dataset templates
- **ESIP SOSO examples** — Minimal Science-on-Schema.org records (core-only subset)
- **ADA core-stripped examples** — Records from the ADA (Analytics & Data Archive) test corpus, stripped to cdifCore-only properties from full records that also conform to discovery, data_description, manifest, and provenance profiles
- **ODIS examples** — Ocean Data and Information System core examples

All ADA-core examples and existing CDIF/ESIP examples validate against the cdifCore resolved schema.

## Contributing

- Create (or identify an existing) issue that explains the need for an update
- Fork this repo (or create a branch if you have permission) and make updates
- Create a pull request referencing the issue as background
- Request review from appropriate team members
- After review, the CDIF team will pull the updates

## License

See [LICENSE](LICENSE).
