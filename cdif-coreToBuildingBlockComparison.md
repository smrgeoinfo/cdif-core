# Comparison: cdif-core vs. metadataBuildingBlocks

## Architectural Approach

| Aspect | cdif-core (earlier) | metadataBuildingBlocks (current) |
|--------|-------------------|----------------------------------|
| **Organizing principle** | Resource types (Dataset, Person, Organization...) | Properties and composable concerns (identifier, spatialExtent, cdifProv...) |
| **Module granularity** | One module per schema.org type | One building block per reusable property group |
| **Composition model** | Implicit — templates show which properties go together | Explicit — profiles compose building blocks via `allOf`/`$ref` |
| **Validation** | Minimal (1 JSON Schema for Service) | Comprehensive — JSON Schema + SHACL shapes per building block |
| **Artifacts per module** | Templates + Examples + (optional) Validation | `schema.yaml` + JSON Schema + `rules.shacl` + `bblock.json` + examples |
| **Schema generation** | None — hand-written | `generate_graph_schema.py` and `generate_shacl_shapes.py` compose building blocks into unified schemas |

## Coverage Comparison

### Resource types in cdif-core but NOT directly represented in building blocks

| cdif-core module | Building blocks equivalent |
|-----------------|--------------------------|
| **Dataset** | Handled at profile level (CDIFDiscovery, CDIFcomplete) — not a standalone BB |
| **CreativeWork** | No dedicated BB — this is a high-level schema.org class, only used for very generic content in CDIF e.g. labeledLink and derivedFrom  |
| **Event** | No equivalent — EventSeries/subEvent patterns not included--what is the use case?; use schema:Action for prov mapping. |
| **Map** | Subsumed under Dataset; a likely extension point |
| **Product** | No standalone BB |
| **Project** | No equivalent — ResearchProject/funding patterns partially covered by `funder` BB |
| **Service** | `webAPI` covers the API subset as a distribution type. Service as a resource type in a catalog is currently out os scope. |
| **Thing** | Generic top class — base properties absorbed into `cdifMandatory` |
| **DataRepository** | No equivalent |

### Building blocks with NO cdif-core predecessor

| Building block | What's new |
|---------------|-----------|
| **cdifProv** | Full provenance activity with schema.org Action properties |
| **provActivity** | PROV-O native provenance alternative |
| **ddicdiProv** | DDI-CDI native provenance (multi-node `@graph`) |
| **generatedBy** | Base provenance foundation |
| **derivedFrom** | `prov:wasDerivedFrom` lineage |
| **qualityMeasure** | DQV quality measurements |
| **cdifTabularData** | CSVW + DDI-CDI tabular structure |
| **cdifLongData** | Long/narrow data format |
| **cdifDataCube** | Multi-dimensional data structure |
| **cdifPhysicalMapping** | Logical-to-physical variable mapping |
| **cdifVariableMeasured** | DDI-CDI extended variables (roles, data types) |
| **cdifArchiveDistribution** | Archive files with sub-components |
| **cdifCatalogRecord** | Metadata-about-metadata records |
| **instrument** | Hierarchical instrument systems |
| **agentInRole** | Role wrappers for contributors |
| **labeledLink** | Typed related links |
| **additionalProperty** | Soft-typed key-value properties |
| **statisticalVariable** | Statistical measures |
| **spdx:checksum** (in dataDownload) | File integrity via SPDX |
| **All 8 XAS blocks** | Entire XAS domain extension |
| **cdifBioschemasProperties** | Lab workflow provenance |

### Properties present in BOTH (evolved)

| Property area | cdif-core | Building blocks |
|--------------|-----------|----------------|
| **Person** | 1 example (56 lines) | Full BB with schema, SHACL, contactPoint, affiliation |
| **Organization** | 5 examples | Full BB with schema, SHACL, subtypes |
| **DefinedTerm** | 1 example | Full BB with SPARQL-targeted SHACL |
| **Action** | 1 template (14 properties) | BB with 11 Action subtypes, SPARQL SHACL |
| **WebAPI** | 1 template | BB with schema + SHACL + potentialAction validation |
| **spatialCoverage** | 4 examples (various geo formats) | BB with GeoCoordinates, GeoShape, WKT, named places |
| **temporalCoverage** | 1 example (ISO 8601 + time:ProperInterval) | BB with ProperInterval, ordinal eras, numeric ages |
| **variableMeasured** | 1 example (PropertyValue) | BB + separate `cdifVariableMeasured` with DDI-CDI roles |
| **Identifier** | Inline in templates | Dedicated BB with PropertyValue pattern |
| **DataDownload/Distribution** | Sparse in templates | Full BB with checksum, conformsTo, provider |
| **Funder/Funding** | In Project template (MonetaryGrant) | Dedicated `funder` BB |

## Key Differences in Philosophy

1. **Type-centric vs. property-centric**: cdif-core asks "what does a Dataset look like?" and provides a monolithic template. Building blocks ask "what does an identifier look like?" and compose them into profiles.

2. **Documentation vs. validation**: cdif-core templates contain inline prose explaining properties — they're human-readable guides. Building blocks produce machine-executable JSON Schema + SHACL that can automatically validate documents.

3. **Flat vs. layered profiles**: cdif-core has no concept of "discovery only" vs. "complete" — each type template shows everything. Building blocks have explicit CDIFDiscovery (64 SHACL shapes) and CDIFcomplete (76 shapes) profile levels.

4. **Vocabulary scope**: cdif-core is almost entirely schema.org. Building blocks integrate 10+ vocabularies (schema.org, PROV-O, DDI-CDI, CSVW, DQV, SPDX, DCAT, GeoSPARQL, Time Ontology, Bioschemas).

5. **Domain extensibility**: cdif-core has no domain extension mechanism. Building blocks have a proven extension pattern (XAS profile adds 8 domain BBs on top of core CDIF).

## What cdif-core had that building blocks could still use

- **Richer examples from multiple communities** — ODIS, ESIP, BCO-DMO dataset examples provide real-world variety that the current test suite (mostly ADA-focused) lacks
- **CreativeWork as a first-class type** — cdif-core's 260+ property template covers a much broader surface than `labeledLink`
- **Event/EventSeries patterns** — time series and event-based metadata have no building block equivalent
- **DataRepository description** — the DRAWG mapping to schema.org/Organization is a use case not currently addressed
- **Project/ResearchProject** — funding relationships beyond MonetaryGrant (legalName, ethicsPolicy, diversityPolicy, areaServed)
