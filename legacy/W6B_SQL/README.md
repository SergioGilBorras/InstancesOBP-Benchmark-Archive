# Warehouse Instance Dataset Documentation (SQL / W6B)

[← Back to repository README](../../README.md)

This folder preserves the W6B monthly sales-fact collection from the documented FoodMart source.

## Dataset contents

Each subfolder corresponds to a **month**, and each month folder contains one or more `sales_fact_19****.txt` files with detailed transactional records.

These monthly transaction records can support order-batching and order-picking studies; interpretation depends on the associated study and warehouse context.

## Directory structure

Under this folder you will typically find subdirectories by month, for example:

- `January/`
- `February/`
- `March/`
- `April/`
- ...

Inside each month directory there are text files with names such as:

- `sales_fact_1998_January.txt`
- `sales_fact_1998_February.txt`
- `sales_fact_1998_March.txt`
- `sales_fact_1998_April.txt`
- ...

Each of these files contains **line-level sales transactions** for the given month.

## Instance types / file types

### Sales fact files (`sales_fact_19****.txt`)

Each `sales_fact_19****.txt` file is a **tab-separated text file** with a header row, followed by one line per transaction.

## Naming conventions

- File pattern: `sales_fact_<year>_<Month>.txt`
  - Example: `sales_fact_1998_April.txt`

## File format

### Header

The first line of the file contains the column names:

```text
product_id\ttime_id\tcustomer_id\tunit_sales
```

### Data rows

Each subsequent line contains a single transaction with the following fields:

- `product_id`
  Identifier of the product sold.

- `time_id`
  Identifier of the time period (e.g., a day or finer granularity) within the month.

- `customer_id`
  Identifier of the customer associated with the transaction.

- `unit_sales`
  Number of units sold in this transaction line (stored as a floating-point number, e.g. `1.0000`, `2.0000`).

#### Example

A small excerpt from one of the files (e.g., `sales_fact_1998_April.txt`) looks like:

```text
product_id\ttime_id\tcustomer_id\tunit_sales
1531\t822\t4605\t1.0000
1111\t822\t6507\t1.0000
1421\t822\t6507\t1.0000
905\t822\t6507\t2.0000
894\t822\t6507\t2.0000
1308\t822\t6004\t1.0000
1218\t822\t6004\t2.0000
```

Interpretation of the last two lines:

- Transaction 1:
  - `product_id = 1308`
  - `time_id = 822`
  - `customer_id = 6004`
  - `unit_sales = 1.0000` (one unit sold)

- Transaction 2:
  - `product_id = 1218`
  - `time_id = 822`
  - `customer_id = 6004`
  - `unit_sales = 2.0000` (two units sold)

Multiple lines can share the same `customer_id` and `time_id` but different `product_id`, meaning that the same customer bought several products in the same time period.

## Monthly sales-fact representation

Each monthly text file is a prepared tabular representation of sales-fact
records derived from the FoodMart `data.sql` source. Fields such as
`customer_id`, `time_id`, `product_id`, and `unit_sales` retain the source
meaning described above. The archive preserves 23 months with sales data:
January through December 1997 and January through November 1998. The source
`time_by_day` calendar contains 31 dates in December 1998, while
`sales_fact_1998` contains zero corresponding December sales rows; the
preserved collection therefore contains no December 1998 monthly instance.

## Related publications / provenance

### Original dataset repository

- Repository: https://github.com/julianhyde/foodmart-data-mysql
- Version/tag: `foodmart-data-mysql-0.10`
- Tag archive URL: https://github.com/julianhyde/foodmart-data-mysql/archive/refs/tags/foodmart-data-mysql-0.10.zip
- Source archive recorded for this collection: `foodmart-data-mysql-foodmart-data-mysql-0.10.zip`
- Source commit: `22d7853a3e08570b01a7aa3b6ef0e38277ca6aff`
- Commit date: `2015-03-05`
- SHA-256: `b7974c605f258b5578f1a50657715b578db2c0cf0f128d81c78736d517359deb`
- Verification recorded: `2026-09-16`


### Related papers

Some order-batching studies consider sales-derived demand alongside a warehouse layout, including the separately documented Arbex W6A collection. The references below provide related research context for these data.

- Valle, C. A., Beasley, J. E., & da Cunha, A. S. (2017). *Optimally solving the joint order batching and picker routing problem*. **European Journal of Operational Research**, 262(3), 817–834. https://doi.org/10.1016/j.ejor.2017.03.069
  - ScienceDirect: https://www.sciencedirect.com/science/article/pii/S0377221717303004

- Briant, O., Cambazard, H., Cattaruzza, D., Catusse, N., Ladier, A.-L., & Ogier, M. (2020). *An efficient and general approach for the joint order batching and picker routing problem*. **European Journal of Operational Research**, 285(2), 497–512. https://doi.org/10.1016/j.ejor.2020.01.059
  - ScienceDirect: https://www.sciencedirect.com/science/article/pii/S0377221720300977

- Valle, C. A., & Beasley, J. E. (2020). *Order batching using an approximation for the distance travelled by pickers*. **European Journal of Operational Research**, 284(2), 460–484. https://doi.org/10.1016/j.ejor.2020.01.022
  - ScienceDirect: https://www.sciencedirect.com/science/article/pii/S0377221720300436

### Related warehouse layout context

In related studies, sales-derived demand may be considered together with warehouse layout models:

- Theys, C., Bräysy, O., Dullaert, W., & Raa, B. (2010). *Using a TSP heuristic for routing order pickers in warehouses*. **European Journal of Operational Research**, 200(3), 755–763. https://doi.org/10.1016/j.ejor.2009.01.036
  - ScienceDirect: https://www.sciencedirect.com/science/article/pii/S0377221709000514

## Notes

- Reuse conditions may depend on the original source. Consult the original distribution and associated documentation.
- Please acknowledge the original data and publication authors cited above when using this collection.
