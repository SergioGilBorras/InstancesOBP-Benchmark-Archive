# InstancesOBP Benchmark Archive

## About

The InstancesOBP Benchmark Archive is an independent, versioned preservation and distribution mirror of legacy benchmark collections for order batching and related warehouse order-picking problems. It preserves documented representations of collections originally made available through their authors or documented source repositories. Original benchmark authorship remains with the respective third parties.

## Purpose

Historical benchmark source locations can become unavailable, move, or change over time. Versioned snapshots in this archive preserve stable access and provenance across those changes. The archive provides versioned distribution, attribution, bibliographic documentation, historical source references, checksums, file-level manifests, family documentation, and preserved descriptive metadata. Selected auxiliary material and explicitly documented author-generated data accompany some collections. These collections also serve as legacy source material in the InstancesOBP project.

## Collections

The prepared-instance counts below give the documented logical collection sizes; `manifest.tsv` and `archives.tsv` record physical file counts.

| Family | Collection | Instances | Primary reference |
| ------ | ---------- | --------: | --------------- |
| W1-W4 | Albareda warehouse instances | 80 | Albareda-Sambola et al. (2009) |
| W5A | Henn instances | 64 | Menéndez et al. (2017) |
| W5B | Henn instances | 400 | Menéndez et al. (2018) |
| W5C | Henn instances | 5840 | Henn & Wäscher (2012) |
| W5D | W5D / OBSP instances | 96 | Menéndez et al. (2017) |
| W6A | Arbex order-picking collection | 592 | Valle et al. (2016) |
| W6B | FoodMart-derived monthly collection | 23 | FoodMart `foodmart-data-mysql-0.10` |
| W7 | FENG instances | 10 | Feng & Hu (2021) |
| W8 | JIANG instances | 200 | Jiang et al. (2022) |
| W9 | BASR instances | 780 | Cao et al. (2023) |
| **Total** | | **8085** | |

## Repository structure

```text
legacy/
├── W1-W2-W3-W4_Albareda/
├── W5A_Henn/
├── W5B_Henn/
├── W5C_Henn/
├── W5D_Henn/
├── W6A_Arbex/
├── W6B_SQL/
├── W7_FENG/
├── W8_JIANG/
└── W9_BASR/
```

## Data provenance

Each collection preserves source and publication information in its family README and included metadata where available. `provenance.tsv` provides a resource-level summary of original authors, publications, DOI, historical URLs, source names, and preparation notes. Fields use `unknown` or remain empty according to the archive's metadata convention; family documentation provides citations and context.

## Prepared representations

Some historical collections appear here as documented prepared representations. Preparation may include organization, normalization, or conversion; family notes record these steps and identify the source material. Original authorship remains attributed to the benchmark's respective creators.

## Author-generated data

The `ArrivalTimes/` files accompanying W1-W4 and W5A are supplemental data generated later by the authors of the Online Order Batching experiments. The family READMEs document their use alongside the Albareda and Henn instances and their relationship to the 2021 and 2024 publications. The original benchmark collections retain their original attribution; ArrivalTimes files are classified as `AUTHOR_GENERATED_DATA`.

## Integrity

`manifest.tsv` inventories every file under `legacy/`, with its relative path, size, SHA-256 digest, archive role, family, and resource identifier. `SHA256SUMS` provides standard checksums for those preserved files. The root-level documentation and metadata describe the archive and its integrity records.

Manifest roles are `BENCHMARK_DATA`, `AUXILIARY_DATA`, `AUTHOR_GENERATED_DATA`, and `PROVENANCE_METADATA`. `PROVENANCE_METADATA` identifies documentation and attribution files.

`BENCHMARK_DATA` identifies the preserved benchmark collections; `AUXILIARY_DATA` identifies related source material such as `productsDB_1560_list`; and `AUTHOR_GENERATED_DATA` identifies later supplemental data such as the ArrivalTimes files. Family README files and descriptive family JSON metadata are both retained as `PROVENANCE_METADATA`.

## Release archives

`legacy/` stores the canonical, versioned family contents. The prepared release archive set consists of one ZIP per family. Each ZIP contains the complete corresponding family folder under its family-name root, including benchmark data, auxiliary data, ArrivalTimes where present, family READMEs, descriptive provenance JSON, and other family-specific metadata.

The release preparation builds archives from the validated family contents using stable path ordering, a fixed timestamp, normalized ZIP attributes, and the exact source-file bytes. Validation checks each source file against `manifest.tsv`, verifies every generated archive and its extracted file paths, sizes, and SHA-256 values, and confirms byte-identical output through a second build. `archives.tsv` records each ZIP's family, filename, SHA-256, size in bytes, file count, and release version. The preparation also generates `SHA256SUMS.release` and `RELEASE-MANIFEST.txt` alongside the ten family ZIPs.

`SHA256SUMS` records checksums for the files under `legacy/`, while `archives.tsv` records the identity of each family ZIP. `SHA256SUMS.release` provides SHA-256 checksums for the ten release ZIPs, and `RELEASE-MANIFEST.txt` provides a human-readable summary of the release archive set.

## Versioning

Each archive snapshot has its own version, for example `InstancesOBP Benchmark Archive v1.0.0`. Cite the exact archive version used so that the preserved collection can be identified and verified.

## Citation

Cite this archive version and the original publication(s) associated with each collection used. `CITATION.cff` identifies this archive as an independent dataset by title, authors, and version.

## Licensing and reuse

Reuse conditions are resource-specific. Family documentation and original sources provide the available attribution and reuse information for each collection. The archive records source provenance and attribution alongside those resource-specific conditions.
