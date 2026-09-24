# Warehouse Instance Dataset Documentation (JIANG / W8)

[← Back to repository README](../../README.md)

This folder preserves the **legacy JIANG** instance files from the documented source repository below.

## Dataset contents

The JIANG dataset is provided as two groups of problem classes:

- `LargeProblemClasses/` – 15 large problem classes, with 10 instances per class.
- `SmallProblemClasses/` – 10 small problem classes, with 5 instances per class.

Each class folder contains multiple `.txt` files, where each file is an **order list** instance.

### Folder layout

- `legacy/W8_JIANG/LargeProblemClasses/Class <k> (<|J|>,<z>)/`
- `legacy/W8_JIANG/SmallProblemClasses/Class <k> (<|J|>,<z>)/`

where:

- `<k>` is the class index.
- `|J|` is the number of orders in the class.
- `z` is the buffer size: the maximum number of batches that can be held in the buffer.

## Instance types / file types

### Order list files (`*.txt`)

Each `.txt` file represents an **order list**:

- Each **line** corresponds to one **order**.
- Each **order** is a set/list of **items**.
- Each **item** is represented by two integer coordinates `(i, j)`:
  - `i` is the **aisle index**.
  - `j` is the **position within the aisle**.

The exact delimiter/encoding follows the original JIANG distribution.

## Class parameters (as provided by the original JIANG documentation)

The per-class parameter tables are included in the subfolder READMEs:

- [`LargeProblemClasses/README.md`](LargeProblemClasses/README.md)
- [`SmallProblemClasses/README.md`](SmallProblemClasses/README.md)

Parameters used by JIANG include:

- `|J|` – number of orders
- `z` \u2013 buffer size, measured as the maximum number of batches held in the buffer
- `L/W` – warehouse length/width ratio
- `D` – item distribution pattern (e.g., `ABC`)
- `Vt` – travel speed
- `tc / tp` – relation between travel time per distance unit and picking time per item
- `q` \u2013 distribution of order sizes; `U(1,9)` denotes a uniform distribution from 1 to 9 items per order
- `O` \u2013 capacity of one picking cart

## How to use (legacy)

1. Choose either **Small** or **Large** problem classes.
2. Select a class folder (e.g., `Class 1 (50, 1)` or `Class 1 (800,1)`).
3. Select one `.txt` instance file from that class.

## Related publications / provenance

### Original dataset repository

- Repository: https://github.com/jixiangwu1993/OBSPPS
- Source archive: `OBSPPS_instances.zip`
- URL: https://github.com/jixiangwu1993/OBSPPS/blob/main/OBSPPS_instances.zip
- Git commit: `98cf77fb9fd25cce4f4d2f43bb9e14c2d52441f9`
- Commit date: `2021-05-16`
- SHA-256: `0d774d0a475d46d30854615ef1c6e397d5fecc785b2aec7e6e37b6b89a706b82`
- Verification recorded: `2026-09-16`
- Source/logical instances in the upstream archive and repository: 200 (150 large + 50 small).

### Original dataset paper

- Jiang, X., Sun, L., Zhang, Y., & Hu, X. (2022). *Order batching and sequencing for minimising the total order completion time in pick-and-sort warehouses*. **Expert Systems with Applications**, 187, 115943. https://doi.org/10.1016/j.eswa.2021.115943
  - ScienceDirect: https://www.sciencedirect.com/science/article/pii/S0957417421012975

### Related publication for parameter definitions

The definitions of picking-cart capacity (`O`) and buffer size (`z`) follow the earlier methodological source below. The 2022 publication above remains the primary dataset reference.

- Jiang, X., Zhou, Y., Zhang, Y., Sun, L., & Hu, X. (2018). *Order batching and sequencing problem under the pick-and-sort strategy in online supermarkets*. **Procedia Computer Science**, 126, 1985–1993. https://doi.org/10.1016/j.procs.2018.07.254

## Notes

- Reuse conditions may depend on the original source. Consult the original distribution and associated documentation.
- Please acknowledge the original JIANG dataset authors and cite the relevant original publication when using this collection.
