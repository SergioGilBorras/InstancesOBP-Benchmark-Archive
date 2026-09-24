# Warehouse Instance Dataset Documentation (JIANG W8 - Large Problem Classes)

[← Back to JIANG (W8) README](../README.md)

This folder contains the **large problem classes** for the JIANG dataset. Each text file in this directory is an order list representing a specific instance.

- There are **15 large problem classes**.
- There are **10 specific instances** in each large problem class.

Each `.txt` document is an **order list**:

- It consists of a certain number of **orders**.
- Each order is a **set of items**.
- Each item is represented by its **two-dimensional coordinates** in the warehouse:
  - The **first coordinate** is the aisle index where the item is located.
  - The **second coordinate** is the specific position inside that aisle.

---

## Class Parameters

The following parameters describe each of the 15 large problem classes:

- `|J|`  – Number of **orders** in the class.
- `z`   \u2013 Buffer size: the maximum number of batches that can be held in the buffer.
- `L/W` – Ratio of **length to width** of the warehouse (e.g., `45/5`).
- `D`   – **Item distribution pattern** in the warehouse (e.g., `ABC`).
- `Vt`  – Picker **travel speed** (e.g., `48`).
- `tc / tp` – Relationship between **travel time** (`tc`) and **picking time** (`tp`) per item (e.g., `0.3/0.05`).
- `q`   \u2013 Distribution of order sizes; `U(1, 9)` denotes a uniform distribution from 1 to 9 items per order.
- `O`   \u2013 Capacity of one picking cart (e.g., `50`).

For the provenance of the `O` and `z` definitions, see [Related publication for parameter definitions](../README.md#related-publication-for-parameter-definitions). Jiang et al. (2022) remains the primary publication associated with this dataset.

### Parameter Table

| Class | \|J\| | z  | L/W   | D   | Vt | tc / tp    | q        | O  |
|:-----:|:-----:|:--:|:-----:|:---:|:--:|:----------:|:--------:|:--:|
| 1     | 800   | 1  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 2     | 800   | 10 | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 3     | 800   | 20 | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 4     | 900   | 1  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 5     | 900   | 10 | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 6     | 900   | 20 | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 7     | 1000  | 1  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 8     | 1000  | 10 | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 9     | 1000  | 20 | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 10    | 1100  | 1  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 11    | 1100  | 10 | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 12    | 1100  | 20 | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 13    | 1200  | 1  | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 14    | 1200  | 10 | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |
| 15    | 1200  | 20 | 45/5  | ABC | 48 | 0.3 / 0.05 | U(1, 9)  | 50 |

---

## File Format

Each large problem class contains **10 instances**. Each instance is provided as a `.txt` file containing an order list.

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
