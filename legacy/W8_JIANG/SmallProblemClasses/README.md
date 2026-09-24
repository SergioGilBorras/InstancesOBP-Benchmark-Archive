# Warehouse Instance Dataset Documentation (JIANG W8 - Small Problem Classes)

[← Back to JIANG (W8) README](../README.md)

This folder contains the **small problem classes** for the JIANG dataset. Each text file in this directory is an order list representing a specific small-sized instance.

- There are **10 small problem classes**.
- There are **5 specific instances** in each small problem class.

Each `.txt` document is an **order list**:

- It consists of a certain number of **orders**.
- Each order is a **set of items**.
- Each item is represented by its **two-dimensional coordinates** in the warehouse:
  - The **first coordinate** is the aisle index where the item is located.
  - The **second coordinate** is the specific position inside that aisle.

These instances correspond to smaller problem sizes compared to the large problem classes (W8 JIANG Large Problem Classes), but share the same structural format.

---

## Class Parameters

The following parameters describe each of the 10 small problem classes (as given in the original JIANG documentation):

- `|J|`  – Number of **orders** in the class.
- `z`   \u2013 Buffer size: the maximum number of batches that can be held in the buffer.
- `L/W` – Ratio of **length to width** of the warehouse (e.g., `45/5`).
- `D`   – **Item distribution pattern** in the warehouse (e.g., `ABC`).
- `Vt`  – Picker **travel speed**.
- `tc / tp` – Relationship between **travel time** (`tc`) and **picking time** (`tp`) per item.
- `q`   \u2013 Distribution of order sizes; `U(1, 9)` denotes a uniform distribution from 1 to 9 items per order.
- `O`   \u2013 Capacity of one picking cart (20 for these small problem classes).

For the provenance of the `O` and `z` definitions, see [Related publication for parameter definitions](../README.md#related-publication-for-parameter-definitions). Jiang et al. (2022) remains the primary publication associated with this dataset.

### Parameter Table

| Class | \|J\| | z  | L/W   | D   | Vt | tc / tp    | q        | O |
|:-----:|:-----:|:--:|:-----:|:---:|:--:|:----------:|:--------:|:--:|
| 1     | 50    | 1  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 20 |
| 2     | 50    | 3  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 20 |
| 3     | 100   | 1  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 20 |
| 4     | 100   | 5  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 20 |
| 5     | 150   | 1  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 20 |
| 6     | 150   | 8  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 20 |
| 7     | 200   | 1  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 20 |
| 8     | 200   | 10 | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 20 |
| 9     | 250   | 2  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 20 |
| 10    | 250   | 13 | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 20 |

> The values above follow the original JIANG small problem class specification: smaller order sets than the large problem classes, but with the same warehouse layout (`L/W`), item distribution (`D`), and travel/picking time parameters (`Vt`, `tc/tp`).

---

## File Format

Each small problem class contains **5 instances**. Each instance is provided as a `.txt` file containing an order list.

A generic order file has the following structure:

- Each **line** corresponds to one **order**.
- Each **order** is represented as a set of items.
- Each **item** is given by two integer coordinates `(i, j)`, where:
  - `i` is the **aisle index**.
  - `j` is the **position** within that aisle.

The exact delimiter and encoding follow the original JIANG format.

---

## Notes

- Reuse conditions may depend on the original source. Consult the original distribution and associated documentation.
- Please acknowledge the original JIANG dataset authors and cite the relevant original publication when using this collection.
