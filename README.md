# CDIF Core

Core interoperability specification for CDIF (Cross-Domain Interoperability Framework). The CDIF Core profile defines the mandatory and optional base properties for any CDIF metadata record, implemented using the schema.org vocabulary.

## Specification

- **[CDIFCoreClasses.md](CDIFCoreClasses.md)** — Complete documentation of all classes and properties for the CDIF Core profile, including required/optional properties, data types, and JSON-LD implementation guidance.
- **[cdifCoreStructuredSchema.json](cdifCoreStructuredSchema.json)** — JSON Schema (Draft 2020-12) for validating CDIF Core profile instances. Generated from the [metadataBuildingBlocks](https://github.com/Cross-Domain-Interoperability-Framework/metadataBuildingBlocks) source schemas.
- **[rules.shacl](rules.shacl)** — SHACL validation shapes for CDIF Core. Copied from [`metadataBuildingBlocks/_sources/cdifProperties/cdifCore/rules.shacl`](https://github.com/Cross-Domain-Interoperability-Framework/metadataBuildingBlocks/blob/main/_sources/cdifProperties/cdifCore/rules.shacl) and should be updated whenever the source changes.

## Required properties

Every valid CDIF Core instance must include:

- `@id` — Resource identifier (IRI)
- `@type` — Must include `schema:Dataset`
- `@context` — JSON-LD context with `schema`, `dcterms`, `dcat`, `prov` prefixes
- `schema:name` — Descriptive name
- `schema:identifier` — Primary identifier (string or PropertyValue)
- `schema:dateModified` — Last update date (ISO 8601)
- `schema:license` OR `schema:conditionsOfAccess` — Rights/access information
- `schema:url` OR `schema:distribution` — Access to the resource
- `schema:subjectOf` — CatalogRecord with `dcterms:conformsTo` including `https://w3id.org/cdif/core/1.0`

## Examples

The `examples/` directory contains 40+ validated JSON-LD dataset examples that conform to the CDIF Core profile. These are records that do NOT use Discovery-level properties (spatialCoverage, temporalCoverage, variableMeasured) — records with those properties are in the [Discovery repository](https://github.com/Cross-Domain-Interoperability-Framework/Discovery/tree/main/examples).

Sources include:

| Source | Count | Description |
|--------|-------|-------------|
| **CDIF/ESIP/ODIS** | 9 | Minimal, simple, and template examples |
| **ADA** | 10 | Core-stripped records from ADA test corpus |
| **Kaggle** | 10 | Iris, Netflix, Titanic, etc. — harvested from landing page JSON-LD |
| **Dataverse** | 7 | Harvard, Borealis, DANS, JHU — via Dataverse schema.org export API |
| **PSDI DCAT** | 5 | CSD, ChASe, AFLOW, etc. — converted from DCAT via `DCAT/dcat_to_cdif.py` |
| **FEDEO** | 1 | Satellite data collection with WebAPI distribution (OpenSearch) |

All examples pass cdifCore JSON Schema validation.

## Repository structure

```
├── CDIFCoreClasses.md              Classes and properties documentation
├── cdifCoreStructuredSchema.json   JSON Schema for validation
├── rules.shacl                     SHACL validation shapes (synced from metadataBuildingBlocks)
├── examples/                       40+ validated Core-only JSON-LD examples
├── ODIS/                           Archived ODIS type-specific templates and examples
└── LICENSE
```

## Relationship to other CDIF repositories

- **[Discovery](https://github.com/Cross-Domain-Interoperability-Framework/Discovery)** — Extends Core with spatialCoverage, temporalCoverage, variableMeasured, measurementTechnique, quality
- **[metadataBuildingBlocks](https://github.com/Cross-Domain-Interoperability-Framework/metadataBuildingBlocks)** — Source building block schemas, SHACL rules, and profile definitions
- **[validation](https://github.com/Cross-Domain-Interoperability-Framework/validation)** — Framing, batch validation, conformance checking, harvesting, and DCAT conversion tools

## License

See [LICENSE](LICENSE).
