# Supply Chain Analysis
## Problem Statement

AtliQ Mart is a growing FMCG manufacturer headquartered in Gujarat, India. It is currently operational in three cities Surat, Ahmedabad and Vadodara. They want to expand to other metros/Tier 1 cities in the next 2 years.AtliQ Mart is currently facing a problem where a few key customers did not extend their annual contracts due to service issues. It is speculated that some of the essential products were either not delivered on time or not delivered in full over a continued period, which could have resulted in bad customer service. Management wants to fix this issue before expanding to other cities and requested their supply chain analytics team to track the ’On time’ and ‘In Full’ delivery service level for all the customers on a daily basis so that they can respond swiftly to these issues.

## Tables
#### dim_products:

* product_name - It is the name of the product
* product_id - Unique ID is given to each of the products
* category - It is the class to which the product belongs

#### dim_date:
* date - date at the daily level
* mmm_yy - date at the monthly level
* week_no - week number of the year as per the date column

#### dim_targets_orders:
* customer_id - Unique ID that is given to each of the customers
* ontime_target % - Target assigned for Ontime % for a given customer
* infull_target % - Target assigned for infull % for a given customer
* otif_target % - Target assigned for otif % for a given customer

#### fact_order_lines:
* order_id - Unique ID for each order the customer placed
* order_placement_date - It is the date when the customer placed the order
* customer_id - Unique ID that is given to each of the customers
* product_id - Unique ID that is given to each of the products
* order_qty - It is the number of products requested by the customer to be delivered
* agreed_delivery_date - It is the date agreed between the customer and Atliq Mart to deliver the products
* actual_delivery_date - It is the actual date Atliq Mart delivered the product to the customer
* delivered_qty - It is the number of products that are actually delivered to the customer

#### fact_orders_aggregate:
* order_id - Unique ID for each order the customer placed
* customer_id - Unique ID that is given to each of the customers
* order_placement_date - It is the date when the customer placed the order
* on_time - '1' denotes the order is delviered on time. '0' denotes the order is not delivered on time.
* in_full - '1' denotes the order is delviered in full quantity. '0' denotes the order is not delivered in full quantity.
* otif - '1' denotes the order is delviered both on time and in full quantity. '0' denotes the order is either not delivered on time or not in full quantity.



## TOOLS & APPROACH 
  Power BI, SQL, and Canva

  Power BI - Data Cleaning, Data Processing, Data Modeling, Measures, visuals and Interactive Dashboard.
  
  Canva - Documentation.

## FINDINGS & INSIGHTS 

* All the Key Metrics (OT%, IF%, OTIF%) are far behind the target.
* On average, orders are delayed 0.42 days from the agreed date of delivery.
* Lotus Mart, Coolblue, Acclaimed stores have the highest orders as well as delayed the most to deliver the products on time.
     Because we are not estimating the right delivery date.
     Because we are receiving more orders than expected.
* Ghee, curd, and butter products are most delayed in delivery. 
* There have been no noticeable improvements in any of the key metrics in the last few months.
* There is a huge gap in IF% for most of the customers because of less production.

## Interactive Dashboard 

Novypro: https://www.novypro.com/project/supply-chain-analysis-power-bi-4



