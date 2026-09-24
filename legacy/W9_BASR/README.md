# Warehouse Instance Dataset Documentation (BASR / W9)

[← Back to repository README](../../README.md)

This folder preserves the **legacy BASR** instance files from the documented BASR source repository and distribution below.

## Dataset contents

### Folder layout (scenario selection)

Instances are stored in `legacy/W9_BASR/<group>/<orders>/<mtcr>/`. The observed top-level `<group>` values are `1` and `2`: group `1` contains the `20`- and `40`-order folders, while group `2` contains the `60`-, `80`-, and `100`-order folders. The included records leave the specific meaning of these group labels undocumented, so this README identifies them as grouping levels observed in the preserved distribution.

The `<group>` directory is a directory level distinct from filename field `[a]`: files in both groups use `[a] = 2` (ABC item distribution). The `<orders>` directory gives the order count and corresponds to filename field `[b]`; `<mtcr>` gives the MTCR value and corresponds to filename field `[c]`. Replication files reside directly in each MTCR directory, and filename field `[d]` identifies the replication index.

Example:

- `legacy/W9_BASR/2/80/0.7/` stores files for **80 orders** and **MTCR = 0.7**.

The replication index is encoded as `[d]`, the final component of the shared filename suffix `[a]_[b]_[c]_[d]`. Matching `orderList_..._[d].txt` and `orderlineList_..._[d].txt` files are stored directly in the corresponding MTCR directory.

## Instance types / file types

Each BASR instance is represented by **two plain-text files** that share the same encoded suffix `[a]_[b]_[c]_[d]`:

1. **Order file**
   - Pattern: `orderList_[a]_[b]_[c]_[d].txt`
   - Describes high-level properties of each order (ID, number of lines, due/arrival information, etc.).

2. **Order-line file**
   - Pattern: `orderlineList_[a]_[b]_[c]_[d].txt`
   - Contains the detailed picking information for each order line (aisle and storage cell identifiers).

## Naming codes (what `[a]_[b]_[c]_[d]` means)

| Code | Meaning | Values in this dataset |
|------|---------|-----------------------|
| `a`  | Item distribution | `2` (ABC distribution) |
| `b`  | Order-count class | `1` → 20, `2` → 40, `3` → 60, `4` → 80, `5` → 100 |
| `c`  | MTCR index | `2` → 0.6, `3` → 0.7, `4` → 0.8 |
| `d`  | Replication index | `1` to `52` |

> Important: although the original BASR specification mentions random (`a = 1`) and ABC (`a = 2`) distributions,
> this repository only provides the **ABC distribution**, hence `a = 2` in all filenames.

## File formats

### Order file format (`orderList_*`)

Each line represents one order and contains **six whitespace-separated columns**:

| Column | Description |
|--------|-------------|
| `[1]`  | `OrderID` – unique identifier of the order |
| `[2]`  | `NumberOfOrderLines` – number of order lines (references) in the order |
| `[3]`  | `DueDateSeconds` – due date (seconds) |
| `[4]`  | `FirstOrderLineID` – first OrderLineID that belongs to `[1]` (offset within the orderline file) |
| `[5]`  | `ArrivalTimeSeconds` – arrival time (seconds) |
| `[6]`  | `WaitingTimeSeconds` – waiting time (seconds) |

### Order-line file format (`orderlineList_*`)

Each line represents one order line and contains **four whitespace-separated columns**:

| Column | Description |
|--------|-------------|
| `[1]`  | `OrderID` – matches the order ID in the order file |
| `[2]`  | `OrderLineID` – sequential identifier of the order line |
| `[3]`  | `PickAisleID` – aisle where the item must be picked |
| `[4]`  | `StorageCellID` – storage cell within the aisle |

## How to use (legacy)

1. **Select a scenario**: choose the folder that matches your desired number of orders and MTCR.
2. **Select a replication**: choose the desired replication index `[d]` from the filenames stored directly in the scenario MTCR directory; the available index range is documented below.
3. **Pick a matching pair**: `orderList_[a]_[b]_[c]_[d].txt` must be paired with `orderlineList_[a]_[b]_[c]_[d].txt` with the same suffix.

## Related publications / provenance

### Original dataset repository

The documented BASR source repository and distribution are listed below:

- Repository: https://github.com/Julie-buct/Instances-of-BASR
- Source archive: `Instance of BASR.zip`
- URL: https://github.com/Julie-buct/Instances-of-BASR/blob/main/Instance%20of%20BASR.zip
- Git commit: `7dab918b651916b95494790df6feb4e8637bd7d2`
- Commit date: `2022-02-03`
- SHA-256: `63280c94cec3f3d075826e4b4af41c9a2bb52e807b35dd47046eb54ea54e025e`
- Verification recorded: `2026-09-16`

### Original dataset paper

- Cao, Z., Zhou, L., Lin, C., & Zhou, M. (2023). *Solving an order batching, picker assignment, batch sequencing and picker routing problem via information integration*. **Journal of Industrial Information Integration**, 31, 100414. https://doi.org/10.1016/j.jii.2022.100414
  - ScienceDirect: https://www.sciencedirect.com/science/article/pii/S2452414X22000814

## Notes

- All times are expressed in **seconds**.
- Reuse conditions may depend on the original source. Consult the original distribution and associated documentation. Please acknowledge the BASR dataset authors and cite the relevant original publication when using this collection.
