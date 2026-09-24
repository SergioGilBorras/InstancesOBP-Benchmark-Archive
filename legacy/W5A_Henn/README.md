# Warehouse Instance Dataset Documentation (Henn W5A Datasets)

[← Back to repository README](../../README.md)

This folder contains datasets divided into four groups: **abc1**, **abc2**, **ran1**, and **ran2**, which correspond to four dataset groups in this collection. "ABC" and "RAN" indicate the item placement strategy within the warehouse.

The **ArrivalTimes** folder contains the order arrival times.

## Instance Types

Each folder with datasets contains two types of files to represent each instance:

1. **Warehouse Layout Instances**
    - **File naming convention**: `sett<number_of_setting>.txt`
        - `<number_of_setting>`: An integer number related to a specific layout configuration of the warehouse.
    - **Structure**: The structure of the setting file is described in the section `Structure of the Setting Files`.


2. **Order Instances**
    - **File naming convention**: `<setting_number>[s|l]-<number_of_orders>-<picker_capacity>-<number_of_instance>.txt`
        - `<setting_number>`: The number of the setting.
        - `[s|l]`: Inherited from the set of instances of Sebastian Henn.
        - `<number_of_orders>`: The number of orders in that instance (40, 60, 80, 100).
        - `<picker_capacity>`: The picker capacity (30, 45, 60, 75).
        - `<number_of_instance>`: The number of the instance (just 0 in this case).

   **Important lines in the file**:
    - For every order:
        - `Order <number_of_order> number of articles <number_of_articles>`:
            - `<number_of_order>`: The number of the order.
            - `<number_of_articles>`: The number of articles in that order.
        - A list of `<number_of_articles>` with the following information:
            - `<number_of_item_inside_the_order>`: Integer number with the number of the item.
            - `Aisle <number_of_aisle>`: The aisle number where the article is located (note: there are twice as many aisles as in reality).
            - `Location <position_in_aisle>`: The storage location of the item within an aisle, from 0 to the length of the aisle.

3. **ArrivalTimes Folder**
   The files in this folder contain the arrival times of the orders.

   **File naming convention**: `TiemposOrders_<type_of_distribution>_<number_of_orders>_H<operationalHours>.txt`
    - `<type_of_distribution>`: Distribution type recorded in the filename. The files preserved here use `E` (Exponential).
    - `<number_of_orders>`: Number of orders (40, 60, 80, and 100 orders).
    - `<operationalHours>`: The number of operational hours during which orders arrive at the warehouse. (1...4 Hours)

   **Important lines in the file**:
    - `<Numero de pedidos iniciales>`: Initial number of orders (usually 0).
    - `<Numero de pedidos entregados>`: Number of delivered orders (usually equal to the number of orders).
    - The remaining lines: Each line contains the arrival time (in milliseconds) of the next order.

## ArrivalTimes provenance

The benchmark setting and order files in this folder originate from the
documented Henn benchmark source below. The `ArrivalTimes/` files are
supplemental data generated later by the InstancesOBP authors for Online Order
Batching experiments. Attribute these files to their later authors while
retaining the original Henn attribution for the benchmark instances.

The related experimental publications are:

- Gil-Borrás, S., Pardo, E.G., Alonso-Ayuso, A., Duarte, A. (2021).
  *A heuristic approach for the online order batching problem with multiple
  pickers*. Computers & Industrial Engineering, 160, 107517.
  https://doi.org/10.1016/j.cie.2021.107517
  https://www.sciencedirect.com/science/article/pii/S0360835221004216

- Gil-Borrás, S., Pardo, E.G., Jiménez, E., Sörensen, K. (2024).
  *The time-window strategy in the online order batching problem*.
  International Journal of Production Research, 62(12), 4446–4469.
  https://doi.org/10.1080/00207543.2023.2263884
  https://www.tandfonline.com/doi/full/10.1080/00207543.2023.2263884

The cited 2021 and 2024 works document the experimental context of these
preserved ArrivalTimes files. Their publication as article supplements remains
undocumented in this archive.

## Structure of the Setting Files

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
| `routing`    | Routing scheme: (s): S-Shape-Routing (l): Largest Gap-Routing |
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

## Related Publications

The datasets in this folder have been used in the following publications:

### Original Dataset:

- S. Henn and G. Wäscher. Tabu search heuristics for the order batching problem in manual order picking systems. European Journal of Operational Research, 222(3):484-494, 2012. doi:10.1016/j.ejor.2012.05.049
  - Sciencedirect: https://www.sciencedirect.com/science/article/abs/pii/S0377221712004389?via%3Dihub 

### Derived Studies:

- Menéndez, B., Pardo, E.G., Duarte, A., Alonso-Ayuso, A., Molina, E., 2015. General variable neighborhood search applied to the picking process in a warehouse. Electronic Notes in Discrete Mathematics 47, 77–84. doi:10.1016/j.endm.2014.11.011
    - Sciencedirect: https://www.sciencedirect.com/science/article/abs/pii/S1571065314000535?via%3Dihub

- Menendez, B., Pardo, E. G., Sanchez-Oro, J., & Duarte, A. 2017. Parallel variable neighborhood search for the min-max order batching problem. International Transactions in Operational Research, 24, 635-662. https://doi.org/10.1111/itor.12309
    - Wiley: https://onlinelibrary.wiley.com/doi/10.1111/itor.12309

- Menéndez, B., Pardo, E.G., Alonso-Ayuso, A., Molina, E., Duarte, A., 2017. Variable neighborhood search strategies for the order batching problem. Computers & Operations Research 78, 500–512. doi:10.1016/j.cor.2016.01.020
    - Sciencedirect: https://www.sciencedirect.com/science/article/abs/pii/S0305054816300027?via%3Dihub

- Gil-Borrás, S., Pardo, E.G., Alonso-Ayuso, A., Duarte, A., 2018. New VNS Variants for the Online Order Batching Problem. Lecture Notes in Computer Science 11328, 89–100. doi:10.1007/978-3-030-15843-9_8
    - Springer: https://link.springer.com/chapter/10.1007/978-3-030-15843-9_8

- Gil-Borrás, S., Pardo, E.G., Alonso-Ayuso, A., Duarte, A., 2019. Basic VNS for a variant of the Online Order Batching Problem. Lecture Notes in Computer Science 12010, 17–36. doi:10.1007/978-3-030-44932-2_2
    - Springer: https://link.springer.com/chapter/10.1007/978-3-030-44932-2_2

- Gil-Borrás, S., Pardo, E.G., Alonso-Ayuso, A., Duarte, A., 2020. Fixed versus variable time window warehousing strategies in real time. Progress in Artificial Intelligence 9, 315–324. doi:10.1007/s13748-020-00215-1
    - Springer: https://link.springer.com/article/10.1007/s13748-020-00215-1

- Gil-Borrás, S., Pardo, E.G., Alonso-Ayuso, A., Duarte, A., 2020. GRASP with Variable Neighborhood Descent for the Online Order Batching Problem. Journal of Global Optimization 78, 295–325. doi:10.1007/s10898-020-00910-2
    - Springer: https://link.springer.com/article/10.1007/s10898-020-00910-2

- Gil-Borrás, S., Pardo, E.G., Alonso-Ayuso, A., Duarte, A., 2021. A heuristic approach for the online order batching problem with multiple pickers. Computers & Industrial Engineering 160, 107517. doi:10.1016/j.cie.2021.107517
    - Sciencedirect: https://www.sciencedirect.com/science/article/pii/S0360835221004216?via%3Dihub

- Gil Borrás, S., 2022. Online Order Batching Problem: a heuristic approach for single and multiple pickers. Ph.D. thesis. ETSI Sistemas Informáticos Universidad Politécnica de Madrid. doi:10.20868/UPM.thesis.72538
    - Universidad Politécnica de Madrid: https://oa.upm.es/72538/

- Gil-Borrás, S., Pardo, E.G., Jiménez, E., Sörensen, K., 2024. The time-window strategy in the online order batching problem. International Journal of Production Research 62, 4446–4469. doi:10.1080/00207543.2023.2263884
    - Tandfonline: https://www.tandfonline.com/doi/full/10.1080/00207543.2023.2263884

### Documented source and distribution

The documented source and distribution pages for the Henn instances and documentation are listed below. W1-W4 and W5A use the same shared upstream source archives; each family extracts the relevant files for its legacy folder.

- Repository/page: `https://grafo.etsii.urjc.es/optsicom/obp.html`
  - Download URL: `https://grafo.etsii.urjc.es/optsicom/obp/obp-files/obp_instances.zip`
  - Shared upstream source archive: `obp_instances.zip`
  - SHA-256: `ba5c4ea8d6e1fccdbca0b4dcd79c5e618e661cede24be95ce6248c6c34062c29`
  - Verification recorded: `2026-09-16`
 
- Repository/page: `https://grafo.etsii.urjc.es/optsicom/mmobp.html`
  - Download URL: `https://grafo.etsii.urjc.es/optsicom/mmobp/mmobp-files/mmobp_instances.zip`
  - Shared upstream source archive: `mmobp_instances.zip`
  - SHA-256: `eefcee8c0638d577a5f1f7dc5f460bda25bc334724c998144a97cd8db749385c`
  - Verification recorded: `2026-09-16`

Please credit the original authors and cite this archive version when using the preserved collection.


## Notes

- Reuse conditions may depend on the original source. Consult the original distribution and associated documentation.
- Please acknowledge the original Henn dataset authors and cite the relevant original publications when using this collection.
- Please cite the relevant articles listed above when using this dataset in your work.
