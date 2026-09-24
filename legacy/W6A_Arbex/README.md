# Warehouse Instance Dataset Documentation (Arbex / W6A)

[← Back to repository README](../../README.md)

This folder preserves the legacy Arbex W6A warehouse instance collection from the documented Arbex distribution.

## Dataset contents

An Arbex W6A order-picking instance is described by **four related file types**. The product catalog adds product names, categories, and supplementary information to the instance description.

1. Warehouse layout and graph representation.
2. Product catalog (list of products, names, categories).
3. Product-to-location assignments within the warehouse.
4. Customer order files.

## Instance types / file types

- **Warehouse layout file** (graph + geometry), e.g. `warehouse_8_1_3_1560`
- **Product list file**, e.g. `productsDB_1560_list`
- **Product locations file**, e.g. `productsDB_1560_locations`
- **Customer order files**, e.g. `instances_dXX_ordYY`

## Naming conventions (quick reference)

- `warehouse_<a>_<b>_<c>_<p>`
  - `<a>`: number of aisles
  - `<b>`: number of extra cross-aisles
  - `<c>`: number of shelves
  - `<p>`: minimum number of products required

- `productsDB_<p>_list` and `productsDB_<p>_locations`
  - `<p>` matches the product count in the dataset version (e.g., 1560)

- `instances_dXX_ordYY`
  - `XX`: number of days merged to produce larger order sets
  - `YY`: number of orders in the file

---

## Instance Components

A single instance is defined by the following four components:

1. **Warehouse Layout File**  
   Example name: `warehouse_8_1_3_1560`

   This file contains the **warehouse layout and its graph representation**, pairing numeric parameters with text headers and labels that clarify each parameter. A typical file of this kind is generated for a warehouse with:

   - 8 aisles
   - 1 extra cross-aisle (resulting in 3 cross-aisles in total: top, middle, bottom)
   - 3 shelves stacked vertically
   - Enough locations to hold at least 1560 products

   Within the file, there are several sections:

   ### 1.1 INPUT_PARAMETERS

   Example fields:

   - `numAisles`: Number of aisles.
   - `numExtraCrossAisles`: Number of extra cross-aisles (beyond the implicit top and bottom ones).
   - `numShelves`: Number of shelves stacked vertically.
   - `minimumProductsRequired`: Minimum number of products the warehouse must be able to hold.
   - Walking distance parameters (all in standardized units):
     - `aisleWidth`
     - `rackDepth`
     - `locationWidth`
     - `crossAisleWidth`
     - `sourceToFirstCrossAisle`

   These parameters define distances such as:

   - Distance between consecutive product vertices in the same subaisle: `[locationWidth]`.
   - Distance from an artificial vertex to the nearest product vertex (north or south): `[(locationWidth + crossAisleWidth) / 2]`.
   - Horizontal distance between two consecutive artificial vertices: `[aisleWidth + 2 * rackDepth]`.
   - Distance from the origin to the first artificial vertex: `[sourceToFirstCrossAisle + crossAisleWidth / 2]`.
   - Distances from the origin to the remaining artificial vertices `a = 2, ..., N`:
     - `[ sqrt( (sourceToFirstCrossAisle + crossAisleWidth/2)^2 + ((a-1) * (aisleWidth + 2 * rackDepth))^2 ) ]`

   A **matrix of distances** is also provided later in the file, so these formulas are mainly explanatory.

   ### 1.2 DATA Section

   Typical parameters include:

   - `numLocationsPerAisleSide`: Number of locations in each shelf and each aisle side.  
     Example: `33` locations per aisle side.
   - `totalLocations`: Total number of product locations.  
     Computed as: `numAisles * 2 (sides) * numLocationsPerAisleSide * numShelves`.  
     Example: `1584`.
   - `totalVertices`: Number of vertices in the graph (origin + product vertices + artificial vertices).  
     Example: `289`.
   - `numProductVertices`: Number of product vertices.  
     Each product vertex serves multiple locations (e.g., one per aisle side and shelf).  
     Example: `264`.
   - `numArtificialVertices`: Number of artificial vertices, typically `numAisles * numCrossAisles`.  
     Example: `24`.
   - `crossAislesPositions`: Positions (in terms of location index) of each cross-aisle along the aisle.  
     Example: `0 16 32` for 33 locations per aisle side (0 to 32), with 3 cross-aisles.

   ### 1.3 Locations

   Under a section like `all_locations_X_aislePos_Y_aisleSide_Z_shelf`, the file lists all locations that can store products. Each line typically has the format:

   ```text
   locationIndex positionInAisleSide aisleSide shelf
   ```

   For an example with 8 aisles, 3 shelves, and 33 positions per aisle side:

   - `positionInAisleSide` ranges from `0` to `32`.
   - `aisleSide` ranges from `0` to `15` (2 sides per aisle * 8 aisles).
   - `shelf` ranges from `0` to `2` (0 = bottom shelf, 2 = top shelf).

   ### 1.4 Product Vertices

   Under a section like `position_product_vertices_X_aislePos_Y_aisle`, the file lists the positions of **product vertices** in 2D (shelves are implicit). Each product vertex is located in the middle of an aisle and can pick products on both sides and all shelves.

   Format:

   ```text
   productVertexIndex positionInAisle aisle
   ```

   For the same example (8 aisles, 33 positions per aisle):

   - `productVertexIndex` ranges from `1` to `numProductVertices` (e.g., 264).  
     Index `0` is reserved for the origin.
   - `positionInAisle` ranges from `0` to `32`.
   - `aisle` ranges from `0` to `7`.

   ### 1.5 Vertices and Locations Mapping

   Section `vertices_pick_which_locations` describes, for each vertex in the graph, which physical locations it can pick from.

   - There are `totalVertices` vertices (e.g., 289):
     - `0`: origin (source).
     - `1..numProductVertices`: product vertices.
     - Remaining indices: artificial vertices.
   - There are `totalLocations` locations (e.g., 1584). Each product vertex typically serves multiple locations (e.g., 6 locations for 8 aisles, 3 shelves).

   ### 1.6 Graph Arcs and Distances

   Section `arcs_distances` encodes the graph in sparse form. For each vertex:

   ```text
   vertexIndex numberOfArcs arc1 distanceArc1 arc2 distanceArc2 ...
   ```

   - Vertex `0` (origin) is connected to every artificial vertex in the first cross-aisle.
   - Each artificial vertex has between 2 and 4 neighbours.
   - Each product vertex is connected to exactly 2 neighbours.

2. **Product List File**  
   Example name: `productsDB_1560_list`

   This file contains the **catalog of products** available in the warehouse.

   Typical structure:

   ```text
   numberOfProducts
   Header
   Product 1
   Product 2
   ...
   ```

   - `numberOfProducts`: Total number of products.
   - `Header`: Column names (e.g., product ID, name, category).
   - `Product i`: One line per product with its attributes.

3. **Product Locations File**  
   Example name: `productsDB_1560_locations`

   This file maps **products to warehouse locations**.

   - Note: The warehouse may have more locations than products (e.g., 1584 locations vs 1560 products), so some locations are empty.

   Typical structure:

   ```text
   numberOfProducts
   Header
   productIndex locationIndex
   ```

   - `locationIndex` ranges from `1` to `totalLocations` (e.g., 1 to 1584).
   - Each product is assigned to exactly one location.

4. **Customer Order Files**  
   Example naming convention: `instances_dXX_ordYY`

   - `XX`: Number of days merged to produce larger order sets.
   - `YY`: Number of orders in the file.

   Typical structure:

   ```text
   numberOfOrders
   Header
   Order 1
   Order 2
   ...
   ```

   Each order line contains:

   ```text
   NumberOfProducts productIndex1 amountOfProduct1 productIndex2 amountOfProduct2 ...
   ```

   Where:

   - `NumberOfProducts`: Number of distinct product types in the order.
   - `productIndexk`: Identifier of the k-th product in the order.
   - `amountOfProductk`: Quantity of that product in the order.

---

## Usage notes

- These files are intended to be used together to fully define an order picking instance:
  - The **layout file** defines the physical warehouse and graph.
  - The **product list** defines the product catalog.
  - The **product locations file** maps products to specific slots.
  - The **order files** define customer demand.

## Related publications / provenance

### Documented Arbex source page

The documented historical distribution page for the Arbex W6A instances and documentation is listed below:

- Repository/page: https://homepages.dcc.ufmg.br/~arbex/orderpicking.html

- Source archive: `orders.tar.gz`
  - Download URL: https://homepages.dcc.ufmg.br/~arbex/orderpicking/orders.tar.gz
  - SHA-256: `5f7b973e521a5da953473f4547fd0280a05d8fbbb7c0fee601ac48c34d6a28fb`
  - Verification recorded: `2026-09-16`

- Source archive: `largeInstances.tar.gz`
  - Download URL: https://homepages.dcc.ufmg.br/~arbex/orderpicking/largeInstances.tar.gz
  - SHA-256: `6bf4b85a5f34714190496e8073a73510396eafc58874377f6ea5d853f23f0de7`
  - Verification recorded: `2026-09-16`

- Source file: `warehouse_8_1_3_1560`
  - Download URL: https://homepages.dcc.ufmg.br/~arbex/orderpicking/warehouse_8_1_3_1560
  - SHA-256: `ab5973ce59a2e7f25f35b57a087f0a6e6abea8cb28c1774337a464d452895b4d`
  - Verification recorded: `2026-09-16`

- Source file: `warehouse_8_0_3_1560`
  - Download URL: https://homepages.dcc.ufmg.br/~arbex/orderpicking/warehouse_8_0_3_1560
  - SHA-256: `af7ba18e0db8cc79373517c59c9176ce975bcc02c34e35440b4a39e7b9e4f31c`
  - Verification recorded: `2026-09-16`

- Source file: `warehouse_16_1_3_1560`
  - Download URL: https://homepages.dcc.ufmg.br/~arbex/orderpicking/warehouse_16_1_3_1560
  - SHA-256: `366a9b416748dca565a37bbb6c0cbe7634a000d785550159e68a5a8d8b4f7538`
  - Verification recorded: `2026-09-16`

- Source file: `warehouse_16_0_3_1560`
  - Download URL: https://homepages.dcc.ufmg.br/~arbex/orderpicking/warehouse_16_0_3_1560
  - SHA-256: `e71c8b2e31ed40823654085f8d5d7eb83f4b7282a066fc26194a624e04933532`
  - Verification recorded: `2026-09-16`

- Source file: `productsDB_1560_list`
  - Download URL: https://homepages.dcc.ufmg.br/~arbex/orderpicking/productsDB_1560_list
  - SHA-256: `0503a7aec4300b37c79ccfd36cdcaf0d729cac8ede3402e8cceca4cfb8bdb529`
  - Verification recorded: `2026-09-16`

- Source file: `productsDB_1560_locations`
  - Download URL: https://homepages.dcc.ufmg.br/~arbex/orderpicking/productsDB_1560_locations
  - SHA-256: `e400c793d0bbb7b7fd5d2015f745b01f6ab20915908bb037cbbacaa5de9ea2c0`
  - Verification recorded: `2026-09-16`

- `productsDB_1560_locations` provides product-to-location assignments. `productsDB_1560_list` is retained as auxiliary collection information.

Please credit the original authors and cite this archive version when using the preserved collection.

### Relationship to the SQL-derived dataset (W6B)

W6A describes the Arbex warehouse and product-location collection. Some studies consider warehouse layouts alongside sales-derived demand, which is documented separately in [`W6B_SQL`](../W6B_SQL/README.md).

To avoid confusion:

- Related references concerning sales-derived demand are listed in:
  - [`W6B_SQL/README.md`](../W6B_SQL/README.md)
- The references below are the primary citations for the **Arbex W6A layout + product/location model** itself.

### References

When using this dataset, please consider citing the following works:

- Valle, C. A., Beasley, J. E., & da Cunha, A. S. (2016). *Modelling and Solving the Joint Order Batching and Picker Routing Problem in Inventories*. In **Combinatorial Optimization** (ISCO 2016), Lecture Notes in Computer Science, pp. 81–97. Springer. https://doi.org/10.1007/978-3-319-45587-7_8
  - SpringerLink: https://link.springer.com/chapter/10.1007/978-3-319-45587-7_8

- Valle, C. A., Beasley, J. E., & da Cunha, A. S. (2017). *Optimally solving the joint order batching and picker routing problem*. **European Journal of Operational Research**, 262(3), 817–834. https://doi.org/10.1016/j.ejor.2017.03.069
  - ScienceDirect: https://www.sciencedirect.com/science/article/pii/S0377221717303004

- Valle, C. A., & Beasley, J. E. (2020). *Order batching using an approximation for the distance travelled by pickers*. **European Journal of Operational Research**, 284(2), 460–484. https://doi.org/10.1016/j.ejor.2020.01.022
  - ScienceDirect: https://www.sciencedirect.com/science/article/pii/S0377221720300436

## Notes

- Reuse conditions may depend on the original source. Consult the original distribution and associated documentation.
- Please acknowledge the original Arbex W6A dataset authors and cite the relevant original publications when using this collection.
