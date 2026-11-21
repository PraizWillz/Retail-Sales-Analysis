# ShopSmart Retail Analytics

**AnalystLab Africa Experience Lab | Week 1 | Data Analytics | Batch F**  
**Prepared by Praise Akubue-Williams**

## Project overview

This project analyzes ShopSmart Retail Group's supplied retail datasets in Microsoft Excel. The workbook covers data understanding and cleaning, formulas, lookups, PivotTables, charts, an executive dashboard with slicers, answers to the assigned business questions, and inventory checks.

Order activity is from 2025. The source files do not identify the currency, so monetary results are reported in dataset units without a currency symbol.

## Required submission files

The Week 1 assignment specifies these four files for the submission package:

- `ShopSmart_Analysis.xlsx` - the Excel workbook with cleaned tables, formulas, lookups, PivotTables, charts, dashboard, and business-question answers.
- `Executive_Dashboard.pdf` - the executive dashboard exported from Excel.
- `Business_Report.pdf` - the one-page findings and recommendations report.
- `README.md` - this project and metric guide.

The workbook and dashboard PDF are produced in Excel; the report and this README document the analysis and its results.

## Source data

| Dataset | Rows | Role |
|---|---:|---|
| Customers | 5,000 | Customer profiles and membership details |
| Orders | 50,000 | Order dates, status, customer, product, store, quantities and prices |
| Order_Items | 50,000 | Order-line quantities, prices, discounts and line totals |
| Products | 500 | Product names, categories, brands, cost and selling prices |
| Stores | 25 | Store identifiers, names, regions, states and cities |
| Returns | 2,500 | Return records, order references, reasons and refund amounts |
| Employees | 125 | Employee and store assignments |
| Suppliers | 489 | Supplier contact and location details |
| Inventory | 500 | Product and store stock on hand, reorder level and restock date |
| Data Dictionary | 41 | Field descriptions for the supplied datasets |

## Preparation and relationships

The CSV files were imported into Excel, organized as tables, and checked for missing values, duplicate rows, numeric fields and date consistency. The data review found no blank cells or duplicate records in the supplied tables; numeric fields were usable for calculations. Order dates were standardized in Excel and grouped by month and year.

The main relationships used in the analysis are:

- Customers.Customer_ID -> Orders.Customer_ID
- Products.Product_ID -> Orders.Product_ID
- Stores.Store_ID -> Orders.Store_ID
- Orders.Order_ID -> Order_Items.Order_ID
- Products.Product_ID -> Order_Items.Product_ID
- Orders.Order_ID -> Returns.Order_ID
- Stores.Store_ID -> Employees.Store_ID
- Products.Product_ID -> Inventory.Product_ID
- Stores.Store_ID -> Inventory.Store_ID

The supplied Orders and Order_Items records match one to one by Order_ID. Store names are not unique across the 25 physical stores, so Store_ID is used to distinguish individual locations.

## Metric definitions

- **Sales_Amount:** Quantity x Unit_Price - Discount. Shipping_Cost is not included in this sales measure.
- **Completed revenue:** Sum of Sales_Amount for orders with Order_Status = Completed: **2,496,824,383**.
- **Total orders:** Count of all Order_ID values regardless of status: **50,000**. Completed orders: **16,529**.
- **Quantity sold:** **49,432** on completed orders.
- **Average selling price:** Completed revenue divided by completed quantity: **50,510.28**.
- **Average order value:** Completed revenue divided by completed orders: **151,057.20**.
- **Return rate:** Count each completed order once if its Order_ID appears in Returns, divided by completed orders: **798 / 16,529 = 4.8%**. The binary Return_Flag avoids counting an order multiple times if it has multiple return records.
- **Inventory value on the dashboard:** Stock_On_Hand x product Selling_Price: **4,595,268,089**. This is potential retail value, not inventory carrying cost. For a cost-based stock valuation, use Products.Cost_Price instead.
- **Total customers KPI:** 5,000 customer profiles in the Customers table; this is the master customer count, not the distinct count of customers with completed purchases.

## Business findings

- Beauty was the top category by revenue (**580,991,275**). Beauty Item 210 was the top-revenue product (**8,075,117**).
- December was the highest-revenue month (**229,848,212**).
- The South was the strongest region (**805,370,701**). STR003 was the top individual store (**113,445,250**).
- Melissa Shaffer (CUST03257) was the highest-spending customer (**2,282,021**).
- Groceries Item 304 had the most returned completed orders (**7**). Electronics had the highest category return rate (**5.3%**).
- STR006 and STR014 tied for the most low-stock items, with **3** each.

## Data limitations and interpretation

- The Suppliers table has Supplier_ID but Products has no Supplier_ID, and Suppliers has no Product_ID. The supplier with the largest product count cannot be determined from the supplied files.
- Monetary values have no confirmed currency in the source material; no currency symbol is applied.
- The Year slicer contains a single year (2025), so it cannot compare different years.
- Dashboard slicers filter the connected PivotCharts. KPI cards currently link to fixed overall metrics and do not change with slicer selections.
- The dashboard inventory KPI is valued at selling price; it should be interpreted as potential retail value. Cost-based inventory value should use Product Cost_Price.

## Reproduction and use

Open `ShopSmart_Analysis.xlsx` in Excel. Refresh the workbook's queries and PivotTables if the source tables change. Use the dashboard slicers for Year, Month, Region, Store_ID, Category and Membership_Level to filter the connected charts. The KPI cards display the overall values described above.

