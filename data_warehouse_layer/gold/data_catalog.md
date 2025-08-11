# Data Catalog for Gold Layer

## 1. Table: `gold.TD_Customer`  

**Purpose:** Stores mapping between plant codes and customer codes for reporting and integration purposes.  

**Columns:**  

| Column Name | Data Type     | Description |
|-------------|--------------|-------------|
| plant_code  | NVARCHAR(50)  | Code identifying the plant or factory associated with the customer. |
| customers   | NVARCHAR(100) | Code identifying the customer. |

---

## 2. Table: `gold.TD_Plant`  

**Purpose:** Stores plant details including port mapping, daily production capacity, and operating costs for reporting and planning purposes.  

**Columns:**  

| Column Name     | Data Type     | Description |
|-----------------|--------------|-------------|
| plant_code      | NVARCHAR(50) | Code identifying the plant or factory. |
| port_code       | NVARCHAR(50) | Code identifying the port associated with the plant. |
| daily_capacity  | INT          | Maximum daily production capacity of the plant (units). |
| plant_cost      | FLOAT        | Operating cost of the plant. |

---

## 3. Table: `gold.TD_Product`  

**Purpose:** Stores mapping between plants and products for production tracking and reporting purposes.  

**Columns:**  

| Column Name | Data Type     | Description |
|-------------|--------------|-------------|
| plant_code  | NVARCHAR(50)  | Code identifying the plant or factory producing the product. |
| product_id  | NVARCHAR(100) | Code identifying the product. |

---

## 4. Table: `gold.TF_Order`  

**Purpose:** Stores detailed order transaction data including customer, product, shipping, and production plant information for analysis and reporting.  

**Columns:**  

| Column Name            | Data Type      | Description |
|------------------------|---------------|-------------|
| order_id               | INT           | Unique identifier for the order. |
| order_date             | DATE          | Date when the order was placed. |
| customer               | NVARCHAR(100) | Code identifying the customer placing the order. |
| origin_port            | NVARCHAR(50)  | Code of the port from which the shipment originates. |
| destination_port       | NVARCHAR(50)  | Code of the destination port for the shipment. |
| carrier                | NVARCHAR(50)  | Name or code of the carrier handling the shipment. |
| service_level          | NVARCHAR(50)  | Shipping service level (e.g., Standard, Express). |
| TPT                    | INT           | Transit time in days for the shipment. |
| ship_ahead_day_count   | INT           | Number of days the shipment is sent ahead of schedule. |
| ship_late_day_count    | INT           | Number of days the shipment is delayed beyond schedule. |
| product_id             | NVARCHAR(100) | Code identifying the product in the order. |
| unit_quantity          | INT           | Quantity of product units in the order. |
| weight                 | FLOAT         | Total weight of the shipment. |
| plant_code             | NVARCHAR(50)  | Code identifying the plant fulfilling the order. |
