
# SUPPLY CHAIN ANALYSIS
**Sessions** 

    1. Project Details
        - Domain short description
        - Problem
        - Goal
        - Dataset Information
    2. Data work (What I  did)
        - Data collection
        - Data Cleaning
        - Data Modeling
        - Data Analysis & Visualization
    3. Power BI Dashboard
        - Dashboard 
        - Interactive Dashboard Link
## PROJECT DETAILS 
**1.Domain (Hospitality)**

The supply chain domain encompasses the entire journey of products from raw materials to the final consumer. It involves the planning, control, and execution of processes that ensure products are manufactured, stored, and distributed efficiently. The goal is to deliver the right products to the right place, at the right time, and in the right quantity.

**Important KPIs**

*On-Time Delivery (OT)*: Measures the percentage of orders delivered on the promised date.

*In-Full Delivery (IF)*: Indicates the percentage of orders delivered with the correct quantity.

*On-Time In-Full (OTIF)*: Combines both OT and IF to assess overall delivery performance.

*Order Cycle Time*: The average time taken to fulfill an order from placement to delivery.

*Inventory Turnover*: Shows how often inventory is sold and replaced over a period, indicating efficiency in inventory management.

**2.Problem**

FMCG manufacturer company is facing revolves around service issues with their deliveries. Specifically, some key customers did not renew their annual contracts because essential products were either not delivered on time or not delivered in full over a continued period. This led to bad customer service, which management wants to address before expanding to other cities. They need to track and improve their delivery service levels daily to ensure that all customer orders are delivered on time and in full.

**3.Goal of the project**

The goal of the project is to monitor and improve FMCG manufacturer's delivery service levels daily. This involves measuring On-Time Delivery (OT) %, In-Full Delivery (IF) %, and On-Time In-Full (OTIF) % for customer orders. By tracking these KPIs, the supply chain team can quickly identify and address any delivery issues. This ensures that all orders are delivered on time and in full, improving customer satisfaction and supporting the company's expansion plans.

**4.Dataset Information**

FMCG manufacturer's company data:
  
dim_customers:
| Column Names | Datatype | Description| 
| ----------- | -----------|-----------|
| customer_id | Integer | Unique customer ID |
| customer_name | String | Name of the customer|
| city | String | Customer's city |

dim_products:
| Column Names | Datatype | Description |
| ----------- | -----------|-----------|
| product_name | String | Name of the product|
| product_id | Integer | Unique product ID | 
| category | String | Product category | 

dim_date:
| Column Names | Datatype | Description |
| ----------- | -----------|-----------| 
| date | Date | Daily level date | 
| mmm_yy | String | Monthly level date |
| week_no | Integer | Week number of the year|

dim_targets_orders:
| Column Names | Datatype | Description |
| ----------- | -----------|-----------| 
| customer_id | Integer | Unique customer ID |
| ontime_target % | Float | Target for OnTime %|
| infull_target % | Float | Target for InFull %|
| otif_target % | Float | Target for OTIF % | 

fact_order_lines:
| Column Names | Datatype | Description |
| ----------- | -----------|-----------|
| order_id | Integer | Unique order ID |
| order_placement_date | Date | Order placement date |
| customer_id | Integer | Unique customer ID |
| product_id | Integer | Unique product ID |
| order_qty | Integer | Requested product quantity |
| agreed_delivery_date | Date | Agreed delivery date |
| actual_delivery_date | Date | Actual delivery date |
| delivered_qty | Integer | Delivered product quantity |

fact_orders_aggregate:
| Column Names | Datatype | Description |
| ----------- | -----------|-----------|
| order_id | Integer | Unique order ID |
| customer_id | Integer | Unique customer ID |
| order_placement_date | Date | Order placement date |
| on_time | Boolean | 1: Delivered on time, 0: Not|
| in_full | Boolean | 1: Delivered in full, 0: Not |
| otif | Boolean | 1: Both on time and full, 0: Not |


## Data/Project work (What I  did)
**1.Data Collection**

   *Data Source:* The data was downloaded in CSV format from the "codebasis" website, which contains relevant information for the project. 

  *Import Process:* The CSV file was imported into Power BI using the Get Data feature, selecting the Folder option to load the data.

*Import Mode:* The data was imported in Import Mode, where a copy of the data is loaded into Power BI's internal memory for faster querying and analysis.

**2.Data preparation**

In this phase, various data cleaning and transformation steps were applied to ensure data quality and consistency. Key steps include:

* *Data Type Conversion:* Adjusted column data types to ensure accurate representation and facilitate analysis.
* *String Corrections:* Standardized text data to maintain consistency across string columns
* *Date Extraction:* Extracted month and week from the main date column to enable time-based analysis.
* *Duplicate Removal:* Identified and removed duplicate records to maintain data accuracy.

**3.Data Modeling**

In this project, a Star Schema data model was implemented to structure data efficiently for reporting and analysis. This model consists of fact and dimension tables, linked by key relationships to support analytical queries. Below is an overview of the data model.

![star_schema](https://github.com/user-attachments/assets/7b6e7005-f85c-4be8-8174-ed43fdcc87c6)



These relationships enable quick and efficient querying of data across dimensions, supporting complex calculations and insights into hotel performance, booking patterns, and revenue.

**4.Data Analysis & Visualization**

**KPIs :**  On-Time Delivery(OT) ,In-Full Delivery(IF) ,On-Time In-Full(OTIF) ,Volume Fulfillment Rate(VFR) ,Line Fill Rate (LFR).

**DAX :**

``` 
1.OnTimeDelivery = 
DIVIDE(
    CALCULATE(COUNTROWS(fact_order_lines), fact_order_lines[actual_delivery_date] <= fact_order_lines[agreed_delivery_date]),
    COUNTROWS(fact_order_lines)
) * 100

```

```
2.InFullDelivery = 
DIVIDE(
    CALCULATE(COUNTROWS(fact_order_lines), fact_order_lines[delivered_qty] >= fact_order_lines[order_qty]),
    COUNTROWS(fact_order_lines)
) * 100

```

```
3.OnTimeInFull = 
DIVIDE(
    CALCULATE(COUNTROWS(fact_order_lines), 
        fact_order_lines[actual_delivery_date] <= fact_order_lines[agreed_delivery_date] && 
        fact_order_lines[delivered_qty] >= fact_order_lines[order_qty]
    ),
    COUNTROWS(fact_order_lines)
) * 100

```

```
4.VolumeFulfillmentRate = 
DIVIDE(
    SUM(fact_order_lines[delivered_qty]),
    SUM(fact_order_lines[order_qty])
) * 100

```
```
5.LineFillRate = 
DIVIDE(
    CALCULATE(
        COUNTROWS(fact_order_lines),
        fact_order_lines[delivered_qty] = fact_order_lines[order_qty]
    ),
    COUNTROWS(fact_order_lines)
) * 100

```
***Here are the questions I was interested in answering:***
* What are the target values for OT%, IF%, and OTIF%, and how do our current metrics compare to these targets?
* How many days, on average, are orders delayed from the agreed delivery date, and what factors contribute most to these delays?
* Which customers (e.g., Lotus Mart, Coolblue, Acclaimed Stores) experience the highest number of delayed orders, and what are the common reasons for these delays?
* Which specific products (e.g., Ghee, curd, butter) are most frequently delayed in delivery, and what can be done to improve their production and delivery timelines?
* Have there been any trends or changes in the key metrics (OT%, IF%, OTIF%) over the past few months, and what actions can be taken to address the lack of noticeable improvements?


## Power BI Dashboard

![Screenshot 2024-11-08 165225](https://github.com/user-attachments/assets/fc342448-27ab-4a9d-b06b-ee92dc90b18f)
![Screenshot 2024-11-08 165405](https://github.com/user-attachments/assets/12ea396c-3185-4a4b-b787-11ae98db1221)
![Screenshot 2024-11-08 165429](https://github.com/user-attachments/assets/e9126083-0c5f-45b0-b707-fc1db5d88ed7)
![Screenshot 2024-11-08 165454](https://github.com/user-attachments/assets/d907ad08-be0f-4ade-9165-fea0eb954e9e)


***Here are my key takeaways:***

* The target values for OT%, IF%, and OTIF% are not met, with current metrics significantly below the desired targets.
* Orders are delayed by an average of 0.42 days, primarily due to incorrect delivery date estimations and higher-than-expected order volumes.
* Lotus Mart, Coolblue, and Acclaimed Stores have the highest delayed orders, mainly due to inaccurate delivery date estimations and excessive orders.
* Ghee, curd, and butter are the most delayed products, requiring improved production efficiency and better demand forecasting.
* No significant improvements in OT%, IF%, and OTIF% have been observed, necessitating enhanced production, supply chain management, and accurate forecasting.

**Interactive Dashboard :** https://www.novypro.com/profile_projects/novyprobalajipk?Popup=memberProject&Data=1700732309079x592372203894031600






















