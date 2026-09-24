# Warehouse Instance Dataset Documentation (FENG / W7)

[← Back to repository README](../../README.md)

This folder preserves the legacy FENG order-set workbooks and the picking-line parameter workbook from the documented source repository below.

These instances are commonly used to study:

- The effect of **order size and composition** on warehouse performance.
- Different **order structures** (e.g., number of item types, maximum quantity per item).
- The impact of **worker fatigue parameters** in picking-line environments.

## Dataset contents

This legacy dataset contains:

- **Order set files**: `orderset_new_*.xlsx` – tabular order lists (orders × item types).
- **Picking-line parameter workbook**: `picking line.xlsx`.

Local files (clickable examples):

- [`picking line.xlsx`](picking%20line.xlsx)
- [`orderset_new_600.xlsx`](orderset_new_600.xlsx)
- [`orderset_new_800.xlsx`](orderset_new_800.xlsx)
- [`orderset_new_1000.xlsx`](orderset_new_1000.xlsx)
- [`orderset_new_60-12.xlsx`](orderset_new_60-12.xlsx)

## Instance types / file types

### 1) Order set files (`orderset_new_*.xlsx`)

Each file represents a **set of customer orders** with a fixed number of orders and item types.
Files encode a matrix of **orders × item types**.

### 2) Picking-line and fatigue parameters (`picking line.xlsx`)

The `picking line.xlsx` workbook records the picking-line and fatigue parameters associated with the collection.

## Naming conventions

There are two main naming patterns for order sets:

1) **`orderset_new_XXXX.xlsx` series**  
Example: `orderset_new_1000.xlsx`

- `XXXX` indicates the **number of orders** in the file.
- The **number of item types** is determined by the number of `item` columns in the file (e.g., `item 1` … `item 17`).

2) **`orderset_new_<m>-<q>.xlsx` series**  
Example: `orderset_new_60-12.xlsx`

- `<m>` indicates there are **<m> item types** (e.g., 60).
- `<q>` indicates that **each item quantity is ≤ <q>** (e.g., 12).

> These naming patterns come directly from the original FENG documentation and are preserved here for compatibility.

## File formats

### Order set table format

Each order set file is a table with the following columns:

```text
order id | item 1 | item 2 | ... | item N
```

- **Header row**:
  - First column: `order id`
  - Remaining columns: `item 1`, `item 2`, …, `item N` (one column per item type)

- **Each subsequent row represents one order**:
  - `order id`: unique identifier for the order
  - `item k`: a **non-negative integer** quantity of item type `k` in that order

The actual number of `item` columns depends on the specific order set.

#### Example snippet

```text
order id  item 1  item 2  item 3  item 4  item 5  ...  item 16  item 17
427       0       0       0       0       0            0        0
773       0       0       0       0       0            0        0
80        4       0       0       0       0            8        0
...
171       7       0       2      10       0            0        0
100       6       0       0       0       0            0        0
341       0       0       9       0       0            0        9
```

Interpretation:

- Order `80` has 4 units of item 1 and 8 units of item 16 (0 units for the other shown items).
- Order `171` has 7 units of item 1, 2 of item 3, and 10 of item 4 (etc.).

## How to use (legacy)

1. Choose an order instance file (e.g., `orderset_new_800.xlsx`).
2. If you also study fatigue-aware picking lines, use `picking line.xlsx` alongside the order sets.

## Related publications / provenance

### Original dataset repository

- Source distribution: versioned Git repository.
- Repository: https://github.com/Xchunf/order-instances
- Git commit: `20b876d61885b034bd8b469f904b6ff230769dd1`
- Commit date: `2020-12-05`
- Source files: 11 XLSX files (10 `orderset_new_*.xlsx` order-set workbooks + 1 `picking line.xlsx` workbook).
- Verification recorded: `2026-09-16` (documentary/source-version verification).

### Original dataset paper

- Feng, X., & Hu, X. (2021). *A Heuristic Solution Approach to Order Batching and Sequencing for Manual Picking and Packing Lines considering Fatiguing Effect*. **Scientific Programming**, 2021(1), 8863391. https://doi.org/10.1155/2021/8863391
  - URL: https://onlinelibrary.wiley.com/doi/abs/10.1155/2021/8863391
  - PDF: https://onlinelibrary.wiley.com/doi/pdf/10.1155/2021/8863391

## Notes

- Reuse conditions may depend on the original source. Consult the original distribution and associated documentation.
- Please acknowledge the original FENG dataset authors and cite the relevant original publication when using this collection.
