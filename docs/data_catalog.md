# Gold Layer Data Catalog

Business-level semantic layer views for reporting and analytics.

---

## 1. `gold.dim_customers`

**Purpose:** Stores customer details enriched with demographic and geographic data.

**Columns:**

| Column Name       | Data Type      | Description |
|--------------------|---------------|-------------|
| customer_key       | INT           | Surrogate key uniquely identifying each customer record in the dimension table. |
| customer_id        | INT           | Unique numerical identifier assigned to each customer. |
| customer_number    | NVARCHAR(50)  | Alphanumeric identifier representing the customer, used for tracking and referencing. |
| first_name         | NVARCHAR(50)  | The customer's first name, as recorded in the system. |
| last_name          | NVARCHAR(50)  | The customer's last name or family name. |
| country            | NVARCHAR(50)  | The country of residence for the customer (e.g., 'Australia'). |
| marital_status     | NVARCHAR(50)  | The marital status of the customer (e.g., 'Married', 'Single'). |
| gender             | NVARCHAR(50)  | The gender of the customer (e.g., 'Male', 'Female', 'n/a'). |
| birthdate          | DATE          | The date of birth of the customer, formatted as YYYY-MM-DD (e.g., 1971-10-06). |
| create_date        | DATE          | The date the customer record was created in the source system. |

---

## 2. `gold.dim_products`

**Purpose:** Stores product information such as product attributes, category, and pricing, filtered to current (active) product records.

**Columns:**

| Column Name    | Data Type      | Description |
|-----------------|---------------|-------------|
| product_key     | INT           | Surrogate key uniquely identifying each product record in the dimension table. |
| product_id      | INT           | Unique identifier assigned to the product in the source system. |
| product_number  | NVARCHAR(50)  | Alphanumeric code identifying the product, used to join to sales transactions. |
| product_name    | NVARCHAR(50)  | Descriptive name of the product, often including type, color, and size. |
| category_id     | NVARCHAR(50)  | Identifier linking the product to its high-level category record. |
| category        | NVARCHAR(50)  | Broader classification of the product (e.g., 'Bikes', 'Components'). |
| subcategory     | NVARCHAR(50)  | More detailed classification of the product within its category. |
| maintenance     | NVARCHAR(50)  | Indicates whether the product requires maintenance (e.g., 'Yes', 'No'). |
| cost            | INT           | The base cost of the product, in whole currency units. |
| product_line    | NVARCHAR(50)  | The product line or series the item belongs to (e.g., 'Road', 'Mountain'). |
| start_date      | DATE          | The date the product became available for sale, formatted as YYYY-MM-DD. |

---

## 3. `gold.fact_sale`

**Purpose:** Stores transactional sales data at the order line level, linking each sale to the customer and product dimensions for analysis.

**Columns:**

| Column Name    | Data Type      | Description |
|-----------------|---------------|-------------|
| order_number    | NVARCHAR(50)  | Unique alphanumeric identifier for the sales order (e.g., 'SO54496'). |
| product_key     | INT           | Foreign key referencing `product_key` in `gold.dim_products`, identifying the product sold. |
| customer_key    | INT           | Foreign key referencing `customer_key` in `gold.dim_customers`, identifying the purchasing customer. |
| order_date      | DATE          | The date the order was placed. |
| shipping_date   | DATE          | The date the order was shipped to the customer. |
| due_date        | DATE          | The date by which payment for the order was due. |
| sales_amount    | INT           | Total monetary value of the sale for the line item (quantity x price), in whole currency units. |
| quantity        | INT           | The number of units of the product ordered in the line item. |
| price           | INT           | The price per unit of the product for the line item, in whole currency units. |
