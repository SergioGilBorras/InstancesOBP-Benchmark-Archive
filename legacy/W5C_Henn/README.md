# Warehouse Instance Dataset Documentation (Henn / W5C)

[← Back to repository README](../../README.md)

This folder preserves the legacy W5C setting and order files identified in the local metadata as Henn W5C.

## Dataset contents

Unlike `W5B_Henn`, where the structure is split into `abc1` and `ran1`, the W5C datasets are structured by:

- **`uniform/`** – problem classes and instances where the number of articles per order follows a **uniform distribution**.
- **`large/`** – additional large-scale instances organized by order count and picker capacity.
- **`abc/`** – instances where items follow an ABC classification (A/B/C classes) in the warehouse layout (if present).

The preserved setting files and order files use the Henn-style formats documented for the W5 collections.

### Folder structure overview

#### `uniform/`

This folder contains:

- `problem classes/` – **setting files** describing the warehouse layouts and demand characteristics.
  Example files: `sett1.txt`, `sett2.txt`, ..., `sett72.txt`.

- `Instances S-Shape/` – order instances generated under the **S-Shape routing** policy.

- `Instances Largest Gap/` – order instances generated under the **Largest Gap routing** policy.

Inside `Instances S-Shape/` (and analogously in `Instances Largest Gap/`), you will find subfolders such as:

- `SS O20 C30/`
- `SS O20 C45/`
- `SS O20 C60/`
- `SS O20 C75/`
- `SS O30 C30/`
- ...
- `SS O100 C75/`

Each subfolder represents a **problem class** with:

- `OXX` – number of **orders** per instance (e.g. `O20`, `O40`, `O60`, `O80`, `O100`).
- `CYY` – **picker capacity** in number of articles (e.g. `C30`, `C45`, `C60`, `C75`).

Within each of these folders you will find files named like:

- `1s-20-30-0.txt`
- `21s-20-30-0.txt`
- `21s-20-30-1.txt`
- ...

which follow the same order-file structure described below.

#### `large/`

The `large/` folder contains larger instances, grouped similarly by routing policy and problem parameters. For example:

- `SS O200 C6/`
- `SS O200 C9/`
- `SS O200 C12/`
- `SS O200 C15/`
- `SS O300 C6/`
- `SS O400 C6/`
- `SS O500 C6/`
- `SS O600 C6/`

Inside a folder like `SS O200 C6/` you will find files such as:

- `1s-200-6-0.txt`
- `1s-200-6-1.txt`
- ...
- `1s-200-6-9.txt`
- `settings.txt` (optional aggregated description)

Interpreting the name `1s-200-6-0.txt`:

- `1` – **setting number** (links back to `sett1.txt` in `uniform/problem classes/`).
- `s` – routing policy flag (`s` = S-Shape, `l` = Largest Gap), uses the Henn-style filename notation.
- `200` – **number of orders** in the instance.
- `6` – **picker capacity** (in number of articles) for this large instance.
- `0` – index of the instance within that problem class.

#### `abc/`

If present, the `abc/` folder mirrors the structure of `uniform/` but assumes that items are placed according to an **ABC classification** in the warehouse (A: high demand, B: medium, C: low).
The naming conventions and file formats remain the same; only the item placement and demand classes differ.

- Subfolders: `Instances S-Shape/`, `Instances Largest Gap/`, and `problem classes/`.
- `sett*.txt` within `problem classes/` describe ABC-based layouts.

## Instance types / file types

Across all subfolders (`uniform`, `large`, `abc`), there are two main types of files:

1. **Warehouse layout instances (setting files)**
   - **Folders**:
     - `uniform/problem classes/`
     - `abc/problem classes/` (if present)
   - **File naming convention**: `sett<number_of_setting>.txt`
     - `<number_of_setting>`: integer number identifying a specific layout and demand configuration.
   - **Structure**: same as in the Henn W5B datasets and described in detail below in `Structure of the Setting Files`.

2. **Order instances (customer orders)**
   - **Folders**:
     - `uniform/Instances S-Shape/SS OXX CYY/`
     - `uniform/Instances Largest Gap/SS OXX CYY/`
     - `large/SS OXXX CYY/`
     - (and analogous paths under `abc/`, if present)
   - **File naming convention**: `<setting_number>[s|l]-<number_of_orders>-<picker_capacity>-<number_of_instance>.txt`

## Naming conventions

- `sett<number>.txt`
  - `<number>`: setting/layout identifier

- `<setting_number>[s|l]-<num_orders>-<capacity>-<instance_index>.txt`
  - `s` – S-Shape routing
  - `l` – Largest Gap routing
  - `<setting_number>`: the number of the setting (e.g., `1`, `21`, ...).
  - `<num_orders>`: number of customer orders in the instance (e.g., 20, 40, 60, 80, 100, 200, 300, ...).
  - `<capacity>`: picker capacity in number of articles (e.g., 6, 9, 12, 15, 30, 45, 60, 75).
  - `<instance_index>`: index of the instance within the problem class (often from `0` up to `9` or higher).

- `SS O<orders> C<capacity>/` and `LG O<orders> C<capacity>/` (folder names vary by subfamily)

## File formats

### Order file format

For each order, the file follows the Henn format:

```text
Order <number_of_order> number of articles <number_of_articles>
<item_index_0> Aisle <aisle_0> Location <location_0>
<item_index_1> Aisle <aisle_1> Location <location_1>
...
<item_index_(k-1)> Aisle <aisle_(k-1)> Location <location_(k-1)>
```

Where:

- `<number_of_order>`: order identifier (0, 1, 2, ...).
- `<number_of_articles>`: number of articles in that order.
- `<item_index_i>`: index of the item within the order (0-based counter).
- `<aisle_i>`: aisle index where the article is located.
  Note: There are **twice as many aisles in the model** as in the physical warehouse.
- `<location_i>`: location of the item within that aisle, from 0 to the aisle length.

**Example (from `large/SS O200 C6/1s-200-6-0.txt`)**:

```text
Order 0	number of articles 3
0	Aisle 6	Location 28
1	Aisle 11	Location 34
2	Aisle 14	Location 43
Order 1	number of articles 2
0	Aisle 11	Location 36
1	Aisle 2	Location 41
...
```

### Setting file format (`sett*.txt`)

The `sett*.txt` files have the same field structure as in `W5B_Henn`.
For convenience, the key abbreviations are summarized here:

| Abbreviation | Description                                                   |
|--------------|---------------------------------------------------------------|
| `no_aisles_` | Number of aisles                                              |
| `no_cells__` | Number of storage locations on each side of an aisle          |
| `opgrade___` | Source setting-file field preserved                            |
| `cell_lengt` | Length of a storage location                                  |
| `cell_width` | Width of a storage location                                   |
| `aisle_widt` | Width of an aisle                                             |
| `dis_ais_wa` | Distance between depot and front cross aisle                  |
| `no_aisle_a` | Number of aisles containing articles of class a               |
| `no_aisle_b` | Number of aisles containing articles of class b               |
| `no_aisle_c` | Number of aisles containing articles of class c               |
| `arrangemen` | Source setting-file field preserved                            |
| `routing___` | Routing scheme: (s): S-Shape-Routing (l): Largest Gap-Routing |
| `type______` | Source setting-file field preserved                            |
| `no_orders_` | Number of customer orders                                     |
| `a_p_or_mea` | Average number of articles per customer order                 |
| `a_p_or_var` | Variance for the number of articles per customer order        |
| `qntity_exp` | Source setting-file field preserved                            |
| `prop_cla_a` | Percent of demand belonging to articles of class a            |
| `prop_cla_b` | Percent of demand belonging to articles of class b            |
| `prop_cla_c` | Percent of demand belonging to articles of class c            |
| `no_instanc` | Number of instances per problem class                         |
| `m_no_o_p_b` | Source setting-file field preserved                            |
| `m_no_a_p_b` | Capacity of the picking device in number of articles          |
| `m_ca_p_b__` | Source setting-file field preserved                            |
| `no_of_work` | Source setting-file field preserved                            |
| `speed_move` | Source setting-file field preserved                            |
| `speed_pick` | Source setting-file field preserved                            |
| `art_capacy` | Source setting-file field preserved                            |
| `empty_posi` | Source setting-file field preserved                            |
| `chaotical_` | Source setting-file field preserved                            |
Below these parameters, many `sett*.txt` files also include **four integers per line** representing:

- Specific instance-level parameters for that problem class (e.g., seeds or internal identifiers).
  The original dataset supplies these four integer values, which this archive preserves in their source form; their detailed semantics remain undocumented in the included materials.

## How to use (legacy)

1. Choose a subfamily (`uniform`, `large`, or `abc` if present).
2. Select a **setting** file `sett*.txt` from `problem classes/`.
3. Select an order instance file matching the desired routing policy (`s` or `l`), number of orders, and picker capacity.

## Related publications / provenance

### Original dataset paper

- Henn, S., & Wäscher, G. (2012). *Tabu search heuristics for the order batching problem in manual order picking systems*. **European Journal of Operational Research**, 222(3), 484–494. https://doi.org/10.1016/j.ejor.2012.05.049
  - ScienceDirect: https://www.sciencedirect.com/science/article/pii/S0377221712004389

> The family metadata identifies this collection as Henn W5C and records Henn & Wäscher (2012), Žulj et al. (2018), the historical source page, and the source archive checksum below. The preserved files use Henn-style formats; instance-level derivation from a particular Henn distribution is not documented in the included records. Cite additional references listed in the source distribution when relevant.

### Related papers

- Žulj, I., Kramer, S., & Schneider, M. (2018). *A hybrid of adaptive large neighborhood search and tabu search for the order-batching problem*. **European Journal of Operational Research**, 264(2), 653–664. https://doi.org/10.1016/j.ejor.2017.06.056
  - ScienceDirect: https://www.sciencedirect.com/science/article/pii/S0377221717305970

### Historical source and distribution URLs

- Original source page: https://www.mansci.ovgu.de/Forschungsmaterialien/Materialien/2012+_+II_-p-392.html
- Historical distribution URL (mutable): https://www.dropbox.com/scl/fo/madfy1j39fmkf1zft3yc4/AOsSJG5vOVNGBpcHiMDvfRM?rlkey=lyco0fwn1nc829sfzekfga6cd&e=1&dl=0
- Source archive recorded for this collection: `instances_results_obp.zip`
- Recorded source archive SHA-256: `9d282e2bf90e1c11112747e5f84dcdca85586e139c94c81e6354ce80af7060f1`
- Verification recorded: `2026-09-16`
- Note: the Dropbox URL records a mutable historical distribution location. The SHA-256 above identifies the source archive preserved for this collection.

Please credit the original authors and cite this archive version when using the preserved collection.

## Notes

- Reuse conditions may depend on the original source. Consult the original distribution and associated documentation.
- Please acknowledge the original Henn dataset authors and cite the relevant original publications when using this collection.
