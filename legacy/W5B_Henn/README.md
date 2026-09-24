# Warehouse Instance Dataset Documentation (Henn / W5B)

[← Back to repository README](../../README.md)

This folder preserves the **legacy Henn W5B** instance files from the documented source distribution below.


This folder contains datasets divided into two groups: **abc1** and **ran1**, which correspond to two item placement strategies within the warehouse (ABC vs Random).

---

## Instance types / file types

Each folder contains two types of files to represent each instance:

1. **Warehouse Layout Instances**
   - **File naming convention**: `sett<number_of_setting>.txt`
     - `<number_of_setting>`: Integer number related to a specific layout configuration of the warehouse.
   - **Structure**: The structure of the setting file is described in the section **Structure of the Setting Files** below.

2. **Order Instances**
   - **File naming convention**: `<setting_number>[s|l]-<number_of_orders>-<picker_capacity>-<number_of_instance>.txt`
     - `<setting_number>`: The number of the setting.
     - `[s|l]`: Routing policy flag inherited from the original Henn instances:
       - `s` – S-Shape routing.
       - `l` – Largest Gap routing.
     - `<number_of_orders>`: Number of orders in the instance (typically 20, 40, 60, 80, 100).
     - `<picker_capacity>`: Picker capacity in number of articles (30, 45, 60, 75).
     - `<number_of_instance>`: Index of the instance within the problem class (0, 1, ..., 9).

   **Important lines in the order files**:

   For each order the file contains:

   - `Order <number_of_order> number of articles <number_of_articles>`:
     - `<number_of_order>`: Identifier of the order.
     - `<number_of_articles>`: Number of articles in that order.
   - Followed by `<number_of_articles>` lines of the form:
     - `<item_index> Aisle <aisle_index> Location <position_in_aisle>`

   where:

   - `<item_index>`: Integer index of the item inside the order (0-based).
   - `<aisle_index>`: Index of the aisle where the article is located. Note: the model uses twice as many aisle indices as the physical warehouse (e.g. a 4‑aisle warehouse uses indices 0–7).
   - `<position_in_aisle>`: Storage location of the item within an aisle, from 0 to the aisle length.

---

## Structure of the setting files

The `sett*.txt` files share the following keys and meanings:

| Abbreviation | Description                                                   |
|--------------|---------------------------------------------------------------|
| `no_aisles_` | Number of aisles                                              |
| `no_cells`   | Number of storage locations on each side of an aisle          |
| `opgrade`    | Source setting-file field preserved                            |
| `cell_lengt` | Length of a storage location                                  |
| `cell_width` | Width of a storage location                                   |
| `aisle_widt` | Width of an aisle                                             |
| `dis_ais_wa` | Distance between depot and front cross aisle                  |
| `no_aisle_a` | Number of aisles containing articles of class a               |
| `no_aisle_b` | Number of aisles containing articles of class b               |
| `no_aisle_c` | Number of aisles containing articles of class c               |
| `arrangemen` | Source setting-file field preserved                            |
| `routing`    | Routing scheme: `s` = S-Shape, `l` = Largest Gap              |
| `type`       | Source setting-file field preserved                            |
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
| `m_ca_p_b`   | Source setting-file field preserved                            |
| `no_of_work` | Source setting-file field preserved                            |
| `speed_move` | Source setting-file field preserved                            |
| `speed_pick` | Source setting-file field preserved                            |
| `art_capacy` | Source setting-file field preserved                            |
| `empty_posi` | Source setting-file field preserved                            |
| `chaotical_` | Source setting-file field preserved                            |
---

## Related publications / provenance

The datasets in this folder have been used in the following publications:

### Original dataset paper

- Henn, S., & Wäscher, G. (2012). *Tabu search heuristics for the order batching problem in manual order picking systems*. **European Journal of Operational Research**, 222(3), 484–494. https://doi.org/10.1016/j.ejor.2012.05.049
  - ScienceDirect: https://www.sciencedirect.com/science/article/pii/S0377221712004389

### Derived Studies:

- Menéndez, B., Pardo, E.G., Duarte, A., Alonso-Ayuso, A., Molina, E., 2015. General variable neighborhood search applied to the picking process in a warehouse. Electronic Notes in Discrete Mathematics 47, 77–84. doi:10.1016/j.endm.2014.11.011
    - Sciencedirect: https://www.sciencedirect.com/science/article/abs/pii/S1571065314000535?via%3Dihub

- Menéndez, B., Bustillo, M., Pardo, E.G., Duarte, A., 2017. General Variable Neighborhood Search for the Order Batching and Sequencing Problem. European Journal of Operational Research 263, 82–93. doi:10.1016/j.ejor.2017.05.001
    - Sciencedirect: https://www.sciencedirect.com/science/article/abs/pii/S0377221717304101?via%3Dihub

### Documented source and distribution

The documented source and distribution page for the Henn instances and documentation is listed below:

- Repository/page: `https://grafo.etsii.urjc.es/optsicom/obp.html`
  - Download URL: `https://grafo.etsii.urjc.es/optsicom/obp/obp-files/obp_instances_ilst.zip`
  - Source archive: `obp_instances_ilst.zip`
  - SHA-256: `e3c5cefbbdcb314cac289ba90f4d5de0392f793f7d5a7377a206b65ea3f95db0`
  - Verification recorded: `2026-09-16`

Please credit the original authors and cite this archive version when using the preserved collection.

---

## Notes

- Reuse conditions may depend on the original source. Consult the original distribution and associated documentation.
- Please acknowledge the original Henn dataset authors and cite the relevant original publications when using this collection.
- Please cite the relevant articles listed above when using this dataset in your work.
