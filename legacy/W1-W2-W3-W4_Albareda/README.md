# Warehouse Instance Dataset Documentation (Albareda W1-W4 Datasets)

[← Back to repository README](../../README.md)

This folder contains datasets divided into four groups: **W1**, **W2**, **W3**, and **W4**, corresponding to the four warehouses used in this dataset. Each warehouse is further divided into five folders, each related to the number of orders used.

The **ArrivalTimes** folder contains the order arrival times.

## Instance Types

Each folder with datasets contains two types of files to represent each instance:

1. **Warehouse Layout Instances**  
   These files describe the layout of the warehouse.  
   **File naming convention**: `wsrp_input_layout_<number_of_warehouse>_<number_of_instance>.txt`
    - `<number_of_warehouse>`: A two-digit number representing the warehouse (e.g., `01` for W1).
    - `<number_of_instance>`: A three-digit number representing the instance (e.g., `090`).

   **Important lines in the file**:
    - **Line 2**: Number of aisles and total number of items.
    - **Line 4**: Depot location (`0` -> bottom left, `1` -> bottom center).
    - **Line 6**: Item location (`0` -> ABC, `1` -> Random).
    - **Line 8**: Length and width of shelves.
    - **Line 10**: Width of aisles.
    - **Line 12**: Picker capacity.
    - **Line 14**: Picking time (usually `0.0`).
    - **Line 16**: Out-turning and in-turning time (usually `0.0`).
    - **Line 18 and onwards**: Aisle number, distance to the right origin, distance to the left origin, and side relative to the depot (`-1` -> left, `0` -> in front, `1` -> right).

   **Note**: The final line carries the source-format `9999` marker.


2. **Order Instances**  
   These files describe the orders and their items.  
   **File naming convention**: `wsrp_input_pedido_<number_of_warehouse>_<number_of_instance>.txt`
    - `<number_of_warehouse>`: A two-digit number representing the warehouse (e.g., `01` for W1).
    - `<number_of_instance>`: A three-digit number representing the instance (e.g., `090`).

   **Important lines in the file**:
    - **Line 2**: Number of orders.
    - **From Line 4 onwards**: For each order:
        - `<duedate>`: Due date of the order.
        - `<number_of_items>`: Number of items in the order.
        - For each item:
            - `<aisle>`: Integer representing the aisle (0 to number of aisles - 1).
            - `<side>`: `0` -> left side, `1` -> right side.
            - `<position>`: Float representing the position of the item in the aisle (0 to aisle length).
            - `<weight>`: Float representing the weight of the item.
            - `<id>`: Integer representing the unique item identifier.


3. **ArrivalTimes Folder**
   The files in this folder contain the arrival times of the orders.
   
   **File naming convention**: `TiemposOrders_<type_of_distribution>_<number_of_orders>_H<operationalHours>.txt`
     - `<type_of_distribution>`: Distribution type recorded in the filename. The files preserved here use `E` (Exponential).
     - `<number_of_orders>`: Number of orders (50, 100, 150, 200, and 250 orders).
     - `<operationalHours>`: The number of operational hours during which orders arrive at the warehouse. (1...4 Hours)

   **Important lines in the file**:
     - `<Numero de pedidos iniciales>`: Initial number of orders (usually 0).
     - `<Numero de pedidos entregados>`: Number of delivered orders (usually equal to the number of orders).
     - The remaining lines: Each line contains the arrival time (in milliseconds) of the next order.

## ArrivalTimes provenance

The benchmark layout and order files in this folder originate from the
documented Albareda-related benchmark sources below. The `ArrivalTimes/` files
are supplemental data generated later by the InstancesOBP authors for Online
Order Batching experiments. Attribute these files to their later authors while
retaining the original benchmark attribution for the layout and order files.

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

## Related Publications

The datasets in this folder have been used in the following publications:

### Original Dataset:

- Albareda-Sambola, M., Alonso-Ayuso, A., Molina, E., De Blas, C.S., 2009. Variable neighborhood search for order batching in a warehouse. Asia-Pacific Journal of Operational Research 26, 655–683. doi:10.1142/S0217595909002390.
   - WorldScientific: https://www.worldscientific.com/doi/abs/10.1142/S0217595909002390

This dataset was developed based on the previous datasets presented in the following studies:

- De Koster, R.B.M., Roodbergen, K.J., Van Voorden, R., 1999. Reduction of walking time in the distribution center of De Bijenkorf. Lecture Notes in economics and mathematical systems. New Trends in Distribution Logistics 480, 215–234. doi:10.1007/978-3-642-58568-5_11
   - Springer: https://link.springer.com/chapter/10.1007/978-3-642-58568-5_11
  
- Ho, Y.C., Tseng, Y.Y., 2006. A study on order-batching methods of order picking in a distribution centre with two cross-aisles. International Journal of Production Research 44, 3391–3417. doi:10.1080/00207540600558015.
  - Tandfonline: https://www.tandfonline.com/doi/abs/10.1080/00207540600558015


### Derived Studies:

- Menéndez, B., Pardo, E.G., Duarte, A., Alonso-Ayuso, A., Molina, E., 2015. General variable neighborhood search applied to the picking process in a warehouse. Electronic Notes in Discrete Mathematics 47, 77–84. doi:10.1016/j.endm.2014.11.011
  - Sciencedirect: https://www.sciencedirect.com/science/article/abs/pii/S1571065314000535?via%3Dihub

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

The documented source and distribution pages for the Albareda instances and documentation are listed below. W1-W4 and W5A use the same shared upstream source archives; each family extracts the relevant files for its legacy folder.

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
- Please acknowledge the original Albareda (W1–W4) dataset authors and cite the relevant original publications when using this collection.
- Please cite the relevant articles listed above when using this dataset in your work.
