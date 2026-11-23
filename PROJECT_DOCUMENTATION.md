# E-Commerce Returns & Customer Behaviour Analysis

## 1. Project Overview

An end-to-end data analytics project focused on understanding e-commerce product returns, customer purchasing behaviour, delivery performance, and the financial impact of returns.

The objective is to identify return patterns, investigate possible contributing factors, and generate actionable business insights.

# 2. Business Understanding

## 2.1 Business Problem

E-commerce businesses face challenges related to product returns, customer satisfaction, product quality, delivery performance, and revenue loss.

Businesses need to understand why products are returned, which customers and products contribute most to returns, and whether certain return patterns indicate potential operational issues or unusual customer behaviour.

## 2.2 Business Objectives

- Analyze overall product and order return performance.
- Identify products and categories with high return rates.
- Understand customer purchasing and return behaviour.
- Investigate frequently reported return reasons and repeated return patterns.
- Examine the relationship between delivery performance and returns.
- Evaluate the financial impact of product returns.
- Generate actionable insights to support better return management.

## 2.3 Key Business Questions & Required Data

### A. Return Performance Analysis

1. What is the overall order return rate and product return rate?
   - Required data: Orders, Order Items, Returns.
   - Required columns: order_id, order_item_id, return_id, return_status, quantity.

2. How do product returns change over time?
   - Required data: Orders, Returns.
   - Required columns: order_date, return_date, return_status.

3. Which months or periods experience the highest return rates?
   - Required data: Orders, Returns.
   - Required columns: order_date, return_date, return_status.

### B. Product & Category Analysis

1. Which product categories have the highest return rates?
   - Required data: Products, Order Items, Returns.
   - Required columns: product_id, category, order_item_id, return_status.

2. Which individual products are returned most frequently?
   - Required data: Products, Order Items, Returns.
   - Required columns: product_id, product_name, order_item_id, return_id.

3. Which product categories contribute the most to the total returned value?
   - Required data: Products, Order Items, Returns.
   - Required columns: category, quantity, unit_price_at_sale, return_quantity, refund_amount.

### C. Customer Behaviour Analysis

1. Which customers have the highest return frequency?
   - Required data: Customers, Orders, Returns.
   - Required columns: customer_id, order_id, return_id.

2. Are some customers repeatedly returning products?
   - Required data: Customers, Orders, Returns.
   - Required columns: customer_id, order_id, return_date, return_status.

3. How does customer purchasing frequency relate to return behaviour?
   - Required data: Customers, Orders, Returns.
   - Required columns: customer_id, order_date, order_id, return_status.

4. Which customers show unusual return patterns compared with other customers?
   - Required data: Customers, Orders, Order Items, Returns.
   - Required columns: customer_id, product_id, return_date, return_reason, order_history.

### D. Return Reason & Validation Analysis

1. What are the most frequently reported product return reasons?
   - Required data: Returns.
   - Required columns: return_reason, return_id, return_date.

2. Are certain return reasons repeatedly reported by particular customers?
   - Required data: Customers, Returns.
   - Required columns: customer_id, return_reason, return_date.

3. Do return reasons vary across different product categories?
   - Required data: Products, Returns, Order Items.
   - Required columns: product_id, category, return_reason.

4. Are there customers who repeatedly report similar return reasons across different products?
   - Required data: Customers, Returns, Order Items.
   - Required columns: customer_id, product_id, return_reason, return_date.

5. Can available evidence help distinguish genuine product issues from potentially questionable return behaviour?
   - Required data: Returns, Products, Customers, Return Verification Records (if available).
   - Required columns: return_reason, product_condition, verification_status, inspection_result, customer_id, product_id.

Note: Repeated returns or frequently reported reasons do not automatically indicate misuse. The analysis will identify unusual patterns and investigate available supporting evidence. Customer behaviour will not be classified as fraudulent without sufficient verification.

### E. Delivery Performance Analysis

1. Are delayed deliveries associated with higher product return rates?
   - Required data: Orders, Deliveries, Returns.
   - Required columns: order_id, order_date, delivery_date, expected_delivery_date, return_status.

2. Do delivery durations differ between returned and non-returned orders?
   - Required data: Orders, Deliveries, Returns.
   - Required columns: order_id, delivery_date, order_date, return_status.

3. Are certain warehouses associated with higher return rates?
   - Required data: Orders, Warehouses, Returns.
   - Required columns: warehouse_id, order_id, return_status.

### F. Financial Impact Analysis

1. What is the total value of returned products?
   - Required data: Order Items, Returns.
   - Required columns: order_item_id, quantity, unit_price_at_sale, return_quantity, refund_amount.

2. Which product categories contribute the most to returned product value?
   - Required data: Products, Order Items, Returns.
   - Required columns: category, product_id, unit_price_at_sale, refund_amount.

3. What proportion of sales value is associated with product returns?
   - Required data: Orders, Order Items, Returns.
   - Required columns: order_id, order_amount, return_amount, return_status.

## 2.4 Key Performance Indicators (KPIs)

- Total Orders
- Total Returned Orders
- Total Products Sold
- Total Products Returned
- Order Return Rate
- Product Return Rate
- Customer Return Frequency
- Category-wise Return Rate
- Return Reason Distribution
- Total Returned Product Value
- Return Value as a Percentage of Sales

## 2.5 Project Scope

**Included:**
- Return performance analysis.
- Product and category analysis.
- Customer purchasing and return behaviour.
- Return reason and unusual pattern investigation.
- Delivery performance analysis.
- Financial impact of returns.

**Excluded from the initial scope:**
- Automated fraud detection.
- Definitive classification of customers as fraudulent.
- Predictive machine learning models.
- Implementation of actual business return policies.

## 2.6 Expected Outcomes

- Identify important product return patterns.
- Understand customer purchasing and return behaviour.
- Identify frequently reported return reasons.
- Highlight unusual return patterns for further investigation.
- Understand delivery-related return patterns.
- Quantify the financial impact of returns where data permits.
- Provide actionable business recommendations.

# 3. Data Understanding

### Orders Table – Data Understanding

Description: Each row represents one customer order and contains details such as order ID, customer ID, order date, warehouse, payment method, and order status.

Dataset Size: 10 lakh rows and 9 columns.
Observations: Three extra unnamed columns need to be removed, and order_date needs to be converted from string to datetime during ETL Data Cleaning.

### Orders Items Table – Data Understanding

The dataset contains 16,666,691 rows and 6 columns.

The Orders Items table records the individual products purchased within each order. Each row represents one order item and contains its `order_item_id`, associated `order_id`, `product_id`, purchased `quantity`, `unit_price_at_sale`, and `line_total` (the total amount for that particular item).

### Deliveries Table – Data Understanding

The Deliveries table contains 799,835 rows and 4 columns. Each row represents an order's delivery details, including its dispatch date (`ship_date`), delivery date, and carrier.

The `ship_date` indicates when the order was dispatched from the warehouse. Both date columns are stored as strings and will be converted to datetime during data cleaning.

The difference in order IDs between the Orders and Deliveries tables will be checked during cross-table validation.

### Products Table – Data Understanding

The Products table contains 300 rows and 6 columns. Each row represents a product with its ID, name, category, subcategory, selling price, and cost price.

`product_id` has 300 unique values, while `product_name` has only 25.

**Data Cleaning:** Rename `unit_price` to `selling_price` and `unit_cost` to `cost_price`.

### Customers Table – Data Understanding

The Customers table contains 50,000 rows and 6 columns. Each row represents a customer, including their ID, name, email, signup date, region, and city.

`customer_id`, `customer_name`, and `email_id` have 50,000 unique values. `signup_date` has 401 unique values, `region` has 9, and `city` has 10.

**Data Cleaning:** Convert `signup_date` from string to datetime and standardize region names to resolve capitalization inconsistencies.

### Returns Table – Data Understanding

The Returns table contains **2,99,404 rows and 6 columns**. Each row represents a return record for an order item, including its return ID, order item ID, return date, return reason, return quantity, and refund amount.

The `return_reason` column contains **50,063 null values**.
The five unique return reasons are: **Size Issue, Wrong Item, Not as Described, Damaged, and Change Mind.** These represent different return reasons.

**Data Cleaning:** Convert `return_date` from string to datetime.

### Warehouses Table – Data Understanding

The Warehouses table contains 4 rows and 3 columns. Each row represents a warehouse, including its ID, name, and region.
Each column has 4 unique values.

# Data Understanding – Data Quality Assessment & Cross-Check Findings

## 1. Data Profiling

The dataset contains the following tables:

| Table | Rows | Columns |
|---|---:|---:|
| Orders | 1,000,000 | 9 |
| Orders Items | 1,666,691 | 6 |
| Deliveries | 799,835 | 4 |
| Products | 300 | 6 |
| Customers | 50,000 | 6 |
| Returns | 299,404 | 6 |
| Warehouses | 4 | 3 |

## 2. Referential Integrity Validation

### Orders – Customers
- **Finding:** 4,000 order records contain customer IDs that do not exist in the Customers table.
- These records represent 3,296 unique unmatched customer IDs.
- The unmatched orders were observed between January and May 2024.
- **Cleaning Note:** Investigate the missing customer master records. The exact reason is not confirmed.

### Orders – Warehouses
- **Finding:** No unmatched warehouse IDs were found.
- **Conclusion:** All warehouse IDs in Orders exist in the Warehouses table.

### Orders Items – Orders
- **Finding:** No unmatched order IDs were found.
- **Conclusion:** All order IDs in Orders Items exist in the Orders table.

### Orders Items – Products
- **Finding:** 5,000 records contain an unmatched product ID, `P9999`.
- The same product ID appears in all 5,000 records.
- **Cleaning Note:** Investigate the missing product reference and decide how these records should be handled.

### Deliveries – Orders
- **Finding:** No unmatched order IDs were found.
- **Conclusion:** All delivery order IDs exist in the Orders table.

### Returns – Orders Items
- **Finding:** No unmatched order item IDs were found.
- **Conclusion:** All return order item IDs exist in Orders Items.

## 3. Business Rule & Data Consistency Validation

### Orders Items – Line Total Validation
- **Rule:** `line_total = quantity × unit_price_at_sale`
- Exact comparison initially identified floating-point differences.
- After applying a ₹0.01 tolerance, no meaningful calculation mismatches were found.
- **Cleaning Note:** No correction required based on this check.

### Returns – Return Quantity Validation
- **Finding:** 15,046 return records have a `return_quantity` greater than the original ordered quantity.
- Multiple return records for the same `order_item_id` were not found.
- **Cleaning Note:** Investigate these records. The exact reason is not confirmed.

### Customers – Signup Date vs Order Date
- **Rule:** An order should not be placed before the customer's signup date.
- **Finding:** No orders were found before the signup date among matched Orders and Customers records.
- **Conclusion:** No date-sequence inconsistency was found in the matched records.

### Returns – Refund Amount Validation
- Expected item value was calculated as:

  `return_quantity × unit_price_at_sale`

- **Finding:**
  - 5,647 records have refunds greater than the calculated item value.
  - 5,738 records have refunds lower than the calculated item value.
  - 288,019 records match the calculated item value.
- **Cleaning Note:** Refund differences may have valid business explanations, such as partial refunds or adjustments. The exact reason cannot be confirmed from the available columns.

## 4. Primary Key Uniqueness Validation

Duplicate primary key values were checked across all seven tables.

- Orders – `order_id`: 0 duplicates
- Orders Items – `order_item_id`: 0 duplicates
- Deliveries – `order_id`: 0 duplicates
- Products – `product_id`: 0 duplicates
- Customers – `customer_id`: 0 duplicates
- Returns – `return_id`: 0 duplicates
- Warehouses – `warehouse_id`: 0 duplicates

**Conclusion:** No duplicate key values were found in the checked columns.

## 5. Missing Value Assessment

### Returns – Missing Return Reasons
- **Finding:** 50,063 records have a missing `return_reason`.
- **Cleaning Note:** Review and handle missing return reasons during Data Cleaning.

## 6. Product Name & Category Consistency

### Product Name Investigation
- The Products table contains 300 product IDs but only 25 unique product names.
- The same product name appears with different product IDs and prices.
- Different brands or variants may explain the differences, but brand/variant details are unavailable.
- **Cleaning Note:** Do not treat repeated product names as duplicates automatically. Preserve product IDs and prices unless a reliable correction is identified.

### Category Standardization
- Category values contain inconsistent capitalization, for example:
  - `Electronics` / `electronics`
  - `Home & Kitchen` / `home & kitchen`
  - `Beauty` / `beauty`
  - `Apparel` / `apparel`
- **Cleaning Note:** Standardize category text during Data Cleaning.

## 7. Additional Data Standardization Finding

### Orders – Order Status
- **Finding:** The `order_status` column contains inconsistent capitalization:
  - `Cancelled`
  - `cancelled`
- **Cleaning Note:** Standardize text casing in categorical columns across the tables.

Other text-based categorical columns to review during Data Cleaning include:
- `payment_method`
- `category`
- `sub_category`
- `return_reason`
- `carrier`
- `region`
- `city`
- `warehouse_name`

## 8. Data Understanding – Conclusion

Data Profiling, Data Quality Assessment, Referential Integrity Validation, Business Rule Validation, and the planned Cross-Checks have been completed.

The findings above will guide the Data Cleaning phase. Records will not be dropped or modified automatically. Each issue will be reviewed, and the cleaning action will be selected based on the available evidence and project requirements.

# 4. Data Preparation

To be updated after data cleaning, transformation, and validation.

# 5. Modeling

To be updated if analytical or predictive models are required.

# 6. Evaluation

To be updated after evaluating analytical results and business findings.

# 7. Deployment & Visualization

To be updated with Power BI dashboards, reports, and final deliverables.