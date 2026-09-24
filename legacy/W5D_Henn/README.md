# Warehouse Instance Dataset Documentation (W5D / OBSP, Henn-style)

[<- Back to repository README](../../README.md)

This folder preserves 96 W5D instances distributed in the OBSP collection. Their setting/order files use the Henn-style structure, and the routing flags follow Henn instance notation. The local metadata identifies the source collection as OBSP and cites Menéndez et al. (2017); authorship of these specific 96 instances is recorded as unknown.

## Dataset contents

The dataset is organized into two MTCR groups:

- `MTCR_05_06_07/`
  - MTCR values observed in the setting files: `0.5`, `0.6`, and `0.7`.
  - 48 setting files (`sett*.txt`).
  - 48 order instance files.

- `MTCR_055_065_075/`
  - MTCR values observed in the setting files: `0.55`, `0.65`, and `0.75`.
  - 48 setting files (`sett*.txt`).
  - 48 order instance files.

MTCR stands for **Modified Traffic Congestion Rate** and controls due-date
tightness. W5D uses six MTCR levels (`0.50`, `0.55`, `0.60`, `0.65`, `0.70`,
and `0.75`); larger MTCR values produce more concentrated and restrictive order
due dates.

Each MTCR group contains files for:

- Routing policies inherited from the Sebastian Henn instance notation:
  - `s` - S-Shape routing.
  - `l` - Largest Gap routing.
- Number of orders: `20`, `40`, `60`, and `80`.
- Picker capacities: `45` and `75`.
- Instance index: `0`.

For every combination of MTCR group, routing policy, number of orders, and picker capacity, this directory contains three files/settings.

### Folder structure overview

```text
legacy/W5D_Henn/
  README.txt
  README.md
  MTCR_05_06_07/
    sett*.txt
    <setting_number>[s|l]-<number_of_orders>-<picker_capacity>-0.txt
  MTCR_055_065_075/
    sett*.txt
    <setting_number>[s|l]-<number_of_orders>-<picker_capacity>-0.txt
```

## Instance types / file types

Each MTCR folder contains two types of files: files that describe the layout and parameters of the warehouse, and files that describe the orders with their items.

1. **Warehouse Layout Instances**
   - **File naming convention**: `sett<number_of_setting>.txt`
     - `<number_of_setting>` is an integer number related to a specific layout configuration of the warehouse.
   - **Structure**: The structure of the setting file is described in **Setting file format (`sett*.txt`)** below.
   - W5D specifies a 3-minute setup/depot time in its source configuration. This source-specific parameter is documented here as part of the preserved source description.

2. **Order Instances**
   - **File naming convention**: `<setting_number>[s|l]-<number_of_orders>-<picker_capacity>-<number_of_instance>.txt`
     - `<setting_number>` is the number of the setting.
     - `[s|l]` is inherited from the set of instances of Sebastian Henn.
     - `<number_of_orders>` is the number of orders in that instance (`20`, `40`, `60`, or `80` in this directory).
     - `<picker_capacity>` is the picker capacity (`45` or `75` in this directory).
     - `<number_of_instance>` is the number of the instance (`0` in this directory).

   **Important lines in the order files**:

   - For every order:
     - `Order <number_of_order> number of articles <number_of_articles> due date <due_date>`
       - `<number_of_order>` is the number of the order.
       - `<number_of_articles>` is the number of articles in that order.
       - `<due_date>` is the due date value present in the order file.
   - And a list of `<number_of_articles>` with the following information:
     - `<number_of_item_inside_the_order>` is an integer number with the number of the item.
     - `Aisle <number_of_aisle>`, where `<number_of_aisle>` is the number of the aisle in which the article is located. The model uses twice as many aisle indices as physical aisles; for example, if a warehouse has 4 aisles, the first aisle index would be 0 and the last aisle index would be 7.
     - `Location <position_in_aisle>`, where `<position_in_aisle>` is the storage location of the item within an aisle, from 0 to the length of the aisle.

## Naming conventions

- `sett<number_of_setting>.txt`
  - `<number_of_setting>` is an integer number related to a specific layout configuration of the warehouse.

- `<setting_number>[s|l]-<number_of_orders>-<picker_capacity>-<number_of_instance>.txt`
  - `<setting_number>` is the number of the setting.
  - `[s|l]` is inherited from the set of instances of Sebastian Henn.
  - `s` indicates S-Shape routing.
  - `l` indicates Largest Gap routing.
  - `<number_of_orders>` is the number of orders in that instance.
  - `<picker_capacity>` is the picker capacity.
  - `<number_of_instance>` is the number of the instance.

Examples from this directory:

- `2l-20-45-0.txt`
- `42s-20-45-0.txt`
- `1l-20-45-0.txt`
- `48s-80-75-0.txt`

## File formats

### Order file format

For every order, the file contains a header line:

```text
Order <number_of_order> number of articles <number_of_articles> due date <due_date>
```

where:

- `<number_of_order>` is the number of the order.
- `<number_of_articles>` is the number of articles in that order.
- `<due_date>` is the due date value for that order.

The header is followed by a list of `<number_of_articles>` lines:

```text
<number_of_item_inside_the_order> Aisle <number_of_aisle> Location <position_in_aisle>
```

where:

- `<number_of_item_inside_the_order>` is an integer number with the number of the item.
- `<number_of_aisle>` is the number of the aisle in which the article is located.
- `<position_in_aisle>` is the storage location of the item within an aisle, from 0 to the length of the aisle.

The model uses twice as many aisle indices as physical aisles; for example, if a warehouse has 4 aisles, the first aisle index would be 0 and the last aisle index would be 7.

### Setting file format (`sett*.txt`)

The structure of the setting file is as follows (just the relevant parameters):

| Abbreviation | Description |
|--------------|-------------|
| `no_aisles_` | Number of aisles |
| `no_cells__` | Number of storage locations on each side of an aisle |
| `cell_lengt` | Length of a storage location |
| `cell_width` | Width of a storage location |
| `aisle_widt` | Width of an aisle |
| `dis_ais_wa` | Distance between depot and front cross aisle |
| `no_aisle_a` | Number of aisles containing articles of class a |
| `no_aisle_b` | Number of aisles containing articles of class b |
| `no_aisle_c` | Number of aisles containing articles of class c |
| `no_orders_` | Number of customer orders |
| `a_p_or_mea` | Average number of articles per customer order |
| `a_p_or_var` | Variance for the number of articles per customer order |
| `prop_cla_a` | Percent of demand belonging to articles of class a |
| `prop_cla_b` | Percent of demand belonging to articles of class b |
| `prop_cla_c` | Percent of demand belonging to articles of class c |
| `no_instanc` | Number of instances per problem class |
| `start_time` | Delay for starting to collect the items |
| `MTCR______` | Value of MTCR |
| `m_no_a_p_b` | Capacity of the picking device in number of articles |
| `no_of_work` | Number of workers working at the same time |
| `speed_move` | Speed of the worker expressed in LU per 100 seconds |
| `speed_pick` | Speed of the worker picking items from their locations |

The setting files also contain additional Henn-style fields such as `opgrade___`, `arrangemen`, `routing___`, `type______`, `qntity_exp`, `m_no_o_p_b`, `m_ca_p_b__`, `art_capacy`, `empty_posi`, and `chaotical_`.

After the labelled parameter block, the setting files include comma-separated numeric rows. These rows are preserved as provided in the original files.

## How to use (legacy)

1. Choose one MTCR group:
   - `MTCR_05_06_07/`
   - `MTCR_055_065_075/`
2. Select a setting file `sett<number_of_setting>.txt`.
3. Select the matching order instance file using the same setting number and the desired routing policy, number of orders, and picker capacity.

For example:

- `MTCR_05_06_07/sett2.txt`
- `MTCR_05_06_07/2l-20-45-0.txt`

## Related publications / provenance

The W5D / OBSP collection is associated with the following publication:

### Associated W5D / OBSP publication

- Menéndez, B., Bustillo, M., Pardo, E.G., Duarte, A., 2017. General Variable Neighborhood Search for the Order Batching and Sequencing Problem. European Journal of Operational Research 263, 82–93. doi:10.1016/j.ejor.2017.05.001
    - Sciencedirect: https://www.sciencedirect.com/science/article/abs/pii/S0377221717304101?via%3Dihub

### OBSP source page and distribution

- Repository/page: `https://grafo.etsii.urjc.es/optsicom/obsp.html`
- Download URL: `https://grafo.etsii.urjc.es/optsicom/obsp/obsp-files/obsp_instances.zip`
- Source archive: `obsp_instances.zip`
- SHA-256: `d162d43dd01f16b198419f839a280fe61abee4380280ccd2f5c58c8b013cea5f`
- Verification recorded: `2026-09-16`

Please credit the original authors and cite this archive version when using the preserved collection.

## Notes

- Reuse conditions may depend on the original source. Consult the original distribution and associated documentation.
- Please cite the W5D / OBSP collection publication identified above and acknowledge the source distribution.
