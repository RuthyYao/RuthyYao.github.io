---
layout: post
title: Boost the Business Growth Through Effective Campaigns
image: "/clique-bait/6.png"
tags: [digital analysis, product funnel, campaign analysis, SQL]
---

Clique Bait, an online seafood shop wants to gain detailed insights into their store and customers. In particular, the management team would like to track their customer journeys and optimize marketing strategies.

# Table of contents

- [00. Project Overview](#overview-main)
    - [Business Problem](#overview-business-problem)
    - [Actions](#overview-actions)
    - [Results](#overview-results)
    - [Insights & Recommendations](#overview-insights-recommendations)
    - [Growth/Next Steps](#overview-growth)
- [01. Data Understanding](#data-understanding)
- [02. Data Analysis](#Data-analysis)
    - [Digital Analysis](#digital-analysis)
    - [Product Funnel](#product-funnel)
    - [Campaign Analysis](#campaign-analysis)
- [03. Insights & Recommendations](#insights-recommendations)
- [04. Growth & Next Steps](#growth-next-steps)

___

# Project Overview  <a name="overview-main"></a>

### Business Problem <a name="overview-business-problem"></a>
Clique Bait, an online seafood shop established the e-commerce five months ago. The management team wants to review the online store performance and gain some insights on how customers interact with the website from page visits to make a purchase. They also want to check whether the campaigns drove more sales and conversion and get some guidance on how to make the campaigns more effective in future.

### Actions <a name="overview-actions"></a>
I first compiled the necessary data from five datasets that provided the customer data, page visits and campaigns information.

Based on the business requirement, I split the analysis task into three parts:

 - **Part 1 - Digital Analysis**  - to extract insights on the customer visits, page views and purchases.
 - **Part 2 - Product Funnel** - create a product funnel to analyse the add-to-cart rate and purchase rate.
 - **Part 3 - Campaign Analysis** - to evaluate the success of each campaign.
   
For each part of the analysis, I used SQL for data extraction and manipulation, gaining the insights on online store conversions, top performing products and the most effective campaigns.  

### Results <a name="overview-results"></a>
Clique Bait has acquired 500 customers over the last four to five months. On average each customer visits the online store for 7.1 times over five-months period. The purchase rate is ~50%. The average add-to-cart rate is 61% and the conversion from add-to-cart to purchase is ~76%. About 15.5% of time customers visit the checkout page but didn't make a purchase.

The most purchased product is lobster which also has the highest view-to-purchase conversion rate. The top 3 visited pages are Oyster, Crab followed by Russian Caviar. Ironically, Russian Caviar is also the most likely to be abandoned product (add to cart but not purchased) with an abandoned rate of 26%. 

Campaigns uplifted page views and attract more purchases from customers. From January to March, Clique Bait run three campaigns, resulting in page view reaching above 800 marks. In contrast, during April and May when there aren’t any campaigns, the page visits dropped to 200. Comparing the customers who received the campaign ad impression with those who didn't receive the impressions, we see page views per visit uplifted by 3 (8.6 vs 5.5) and purchase rate dramatically increased by 58% (89% vs 27%), which proved that campaigns did effectively drive the sales. 

Of the three campaigns, "half-price" promotion achieves the highest impression-to-purchase conversion rate - 85.3% followed by "Buy-one-get-one-free" achieved 84.6%. 


### Insights & Recommendations <a name="overview-insights-recommendations"></a>

To boost the sales growth, the management team should focus on managing the conversion rate, particularly the conversion from page view to add-to-cart and from add-to-cart to finally making the purchase. In this aspect, the management should keep an eye on the customers who visit the checkout page but didn't make purchases. It is recommended that we collect further information to understand what caused the customers abandoned the checkout. 

The management team could consider optimize the campaigns to drive further sales uplift. Based on the sales and click-view performance of the previous three campaigns, "Half-Price" and "Buy-one-get-one-free" are the most effective. Management team could consider extend the reach of those campaigns in future if the budget permits. Suggest do further customer behaviours analysis to identify what types of customers are more likely to click the ad so we can target the customers for promotion to driver better outcome.

The analysis shows that Oyster and Crab are the most purchased products. The management team could leverage the data insights to plan the purchase and stocking. With the luxury category, our data reveals very distinctive shopping behaviours - high views yet low conversion. The management team could consider implement some limited-time promotions such as flash sales to generate excitement and drive sales. This could also help clear out excessive stocks.

### Growth/Next Steps <a name="overview-growth"></a>

* To drive the conversion rate up, we could test different promotional strategies and track the change of the product funnel conversion and fallout rate. 

* We could also collect external data to establish a benchmark for the key metrics to help us better gauge our performance. 

* Further analysis on customers visits and shopping basket to segment the customers and develop more customized campaigns and promotions.


# Data Understanding  <a name="data-understanding"></a>

Entity Relationship Diagram:

<img src="https://github.com/RuthyYao/RuthyYao.github.io/blob/master/img/clique-bait/case-study-6-erd.PNG">

<br>


The original dataset has five data tables. The primary data table is "events" which is the raw data of the customer visits. It stores the visits id, the visit time, the page visited and the activities on the page. 

<br>

The "users" table stores the customers information including their user id and the cookies they have and the time each cookie generated. 
<br>

"Event_identifier" and "Page Hierarchy" are mapping tables. The former provides the activities names for each event_id and the page name and the latter maps out the page_name and product hierarchy for each page id. Note that each product has a page Hence it has a unique page id and product id. 
<br>

Finally, the "campaign identifier" table provide the three campaigns’ start date and end date and the products that the campaign was on.


# Data Analysis  <a name="data-analysis"></a>

## Part 1 - Digital Analysis <a name="digital-analysis"></a>

### 1. Calculate total number of customers.

```
SELECT 
	COUNT(DISTINCT user_id) AS customer_count
FROM users;
```

| customer_count |
|----------------|
| 500            |


### 2. What is the unique number of visits by all users per month?

```
SELECT 
	DATE_FORMAT(event_time,'%Y-%m') As period,
    COUNT(DISTINCT visit_id) AS visits
FROM events
GROUP BY period;
```

| period  | visits |
|---------|--------|
| 2020-01 | 876    |
| 2020-02 | 1488   |
| 2020-03 | 916    |
| 2020-04 | 248    |
| 2020-05 | 36     |

### 3. What is the number of events for each event type?

```
SELECT
	e.event_type,
    ei.event_name,
    COUNT(DISTINCT visit_id) AS event_count
FROM events AS e
LEFT JOIN event_Identifier AS ei
	ON e.event_type = ei.event_type
GROUP BY e.event_type, ei.event_name;
```

| event_type | event_name    | event_count |
|------------|---------------|-------------|
| 1          | Page View     | 3564        |
| 2          | Add to Cart   | 2510        |
| 3          | Purchase      | 1777        |
| 4          | Ad Impression | 876         |
| 5          | Ad Click      | 702         |

### 4. Breakdown the number of events by months

```
WITH event_count AS(
SELECT
	DISTINCT DATE_FORMAT(e.event_time, '%Y-%m') AS period,
    e.event_type,
    ei.event_name,
    COUNT(DISTINCT visit_id)  AS event_count
FROM events AS e
LEFT JOIN event_Identifier AS ei
	ON e.event_type = ei.event_type
GROUP BY period, e.event_type, ei.event_name
ORDER BY period, e.event_type, ei.event_name
)
SELECT
	period,
    MAX(CASE WHEN event_name = 'Page View' THEN event_count ELSE 0 END) AS page_view,
	MAX(CASE WHEN event_name = 'Add to Cart' THEN event_count ELSE 0 END) AS add_to_cart,   
    MAX(CASE WHEN event_name = 'Purchase' THEN event_count ELSE 0 END) AS purchase,   
    MAX(CASE WHEN event_name = 'Ad Impression' THEN event_count ELSE 0 END) AS impression,   
    MAX(CASE WHEN event_name = 'Ad Click' THEN event_count ELSE 0 END) AS clicks
FROM event_count
GROUP BY period;
```

| period  | page_view | add_to_cart | purchase | impression | clicks |
|---------|-----------|-------------|----------|------------|--------|
| 2020-01 | 876       | 614         | 430      | 216        | 173    |
| 2020-02 | 1488      | 1054        | 744      | 371        | 291    |
| 2020-03 | 916       | 635         | 448      | 214        | 178    |
| 2020-04 | 248       | 177         | 134      | 63         | 48     |
| 2020-05 | 36        | 30          | 21       | 12         | 12     |

Jan to March has more website activities than April and May. This was because Clique Bait run three campaigns in Q1. 


### 5. What is the percentage of visits which have a purchase event?

```
SELECT
	ROUND(COUNT(DISTINCT visit_id) * 100 / (SELECT COUNT(DISTINCT visit_id) FROM events),1) AS purchase_percentage
FROM events AS e
LEFT JOIN event_Identifier AS ei
	ON e.event_type = ei.event_type
WHERE event_name = 'Purchase';
```

| purchase_percentage |
|---------------------|
| 49.9                |

About half of the visits lead to a purchase. 

### 6. What is the percentage of visits which view the checkout page but do not have a purchase event?

```
WITH cte AS(
SELECT 
	COUNT(DISTINCT e.visit_id) AS checkout_page_visits
FROM events AS e
LEFT JOIN event_Identifier AS ei
	ON e.event_type = ei.event_type
LEFT JOIN page_hierarchy AS p
	ON e.page_id = p.page_id
WHERE ei.event_name = 'Page View'
	AND p.page_name = 'Checkout'
)
SELECT
	ROUND((1- COUNT(DISTINCT e.visit_id) /  (SELECT checkout_page_visits FROM cte)) * 100,2)  AS checkout_page_no_purchase 
FROM events AS e
LEFT JOIN event_Identifier AS ei
	ON e.event_type = ei.event_type
WHERE ei.event_name = 'Purchase';
```

| checkout_page_no_purchase |
|---------------------------|
| 15.50                     |

15.5% of the visits abandoned the checkout.

### 7. What are the top 3 product pages by number of views?

```
SELECT
    p.page_name,
    COUNT(e.visit_id) AS num_views
FROM events AS e
LEFT JOIN page_hierarchy AS p
	ON	e.page_id = p.page_id
WHERE e.event_type = 1
	AND p.product_category IS NOT NULL
GROUP BY p.page_name
ORDER BY num_views DESC
LIMIT 3;
```

| page_name      | num_views |
|----------------|-----------|
| Oyster         | 1568      |
| Crab           | 1564      |
| Russian Caviar | 1563      |


### 8. What is the number of views and cart adds for each product category?

```
SELECT
	p.product_category,
    SUM(CASE WHEN event_type = 1 THEN 1 ELSE 0 END) AS num_views,
    SUM(CASE WHEN event_type = 2 THEN 1 ELSE 0 END) AS num_add_cart
FROM events AS e
LEFT JOIN page_hierarchy AS p
	ON	e.page_id = p.page_id
WHERE product_category IS NOT NULL
GROUP BY p.product_category;
```

| product_category | num_views | num_add_cart |
|------------------|-----------|--------------|
| Luxury           | 3032      | 1870         |
| Shellfish        | 6204      | 3792         |
| Fish             | 4633      | 2789         |


### 9. What are the top 3 products by purchases?

```
-- Solution structure: 
	-- Purchased products are those which are add to the cart in the product page AND are purchased in the confirmation page.
    	-- Hence break down the question into two layers:
		-- 1. products are add to cart.
		-- 2. products are purchased (use subquery)

SELECT
    p.page_name,
    p.product_category,
    COUNT(e.visit_id) AS purchases
FROM events AS e 
LEFT JOIN page_hierarchy AS p
	ON p.page_id = e.page_id
WHERE e.event_type = 2  -- 1st layer - products are add to cart.
AND e.visit_id IN 
	(SELECT
		visit_id
	FROM events
    WHERE event_type = 3) -- 2nd layer - products are purchased.
GROUP BY p.product_id, p.page_name, p.product_category
ORDER BY purchases DESC
LIMIT 3;
```

| page_name | product_category | purchases |
|-----------|------------------|-----------|
| Lobster   | Shellfish        | 754       |
| Oyster    | Shellfish        | 726       |
| Crab      | Shellfish        | 719       |


### 10. How many times did each customer visit the online store averagely? And what is the customer number distribution by visits?
```
WITH visit_cte AS(
SELECT 
	users.user_id,
    COUNT(DISTINCT events.visit_id) AS visits
FROM users
LEFT JOIN events
	ON users.cookie_id = events.cookie_id
GROUP BY users.user_id
)
SELECT
	AVG(visits) AS avg_visits_per_customer
FROM visit_cte;
```

| avg_visits_per_customer |
|-------------------------|
| 7.1280                  |

On average, customers visited the store 7.1 times over the five-months period.

```
WITH visit_cte AS(
SELECT 
	users.user_id,
    COUNT(DISTINCT events.visit_id) AS visits
FROM users
LEFT JOIN events
	ON users.cookie_id = events.cookie_id
GROUP BY users.user_id
)
SELECT
	visits AS visit_freqency,
    COUNT(DISTINCT user_id) AS customer_count
FROM visit_cte
GROUP BY visits;
```

| visit_freqency | customer_count |
|----------------|----------------|
| 2              | 18             |
| 4              | 77             |
| 6              | 138            |
| 8              | 166            |
| 10             | 74             |
| 12             | 27             |

### 11. How many purchases did each customer make averagely?
```
WITH purchase_cte AS(
SELECT 
	users.user_id,
    COUNT(DISTINCT events.visit_id) AS visits
FROM users
LEFT JOIN events
	ON users.cookie_id = events.cookie_id
WHERE event_type = 3
GROUP BY users.user_id
)
SELECT
	AVG(visits) AS avg_purchases_per_customer
FROM purchase_cte;
```

| avg_purchases_per_customer |
|----------------------------|
| 3.6715                     |

On average, customers did 3.7 times shopping with Clique Bait over the five-months period.

## Part 2 - Product Funnel <a name="product-funnel"></a>
I'll create a new output table that contains the following details.

* How many times was each product viewed?
* How many times was each product added to cart?
* How many times was each product added to a cart but not purchased (abandoned)?
* How many times was each product purchased?

```
-- Solution Structure
    -- Create a CTE prod_view: calculate the number of views and number of cart_adds for each product using CASE() and SUM()
    -- Create a CTE prod_abandon: calculate the number of abandoned products (Note: use the solution for Q9 in the Digital Analysis section. Only need to replace IN by NOT IN in the subquery).
    -- Create a CTE prod_purchased: calculate the number of purchased products (solution for Q9 in the Digital Analysis section)
    -- JOIN the above three CTEs using product_id, product_name and product_category of each product
    -- Store the result in a temporary table product_summary for further analysis

CREATE TABLE product_summary
WITH prod_view AS (
SELECT 
    p.product_id,
    p.page_name,
    p.product_category,
    SUM(CASE WHEN e.page_id NOT IN (1,2,12,13) AND e.event_type = 1 THEN 1 ELSE 0 END) AS views,
    SUM(CASE WHEN e.event_type = 2 THEN 1 ELSE 0 END) AS add_to_cart
FROM events AS e
LEFT JOIN page_hierarchy as p
	ON e.page_id = p.page_id
WHERE product_id IS NOT NULL
GROUP BY  p.product_id, p.page_name, p.product_category
),
prod_abandon AS(
SELECT
    p.product_id,
    p.page_name,
    p.product_category,
    COUNT(e.visit_id) AS abandoned
FROM events AS e 
LEFT JOIN page_hierarchy AS p
	ON p.page_id = e.page_id
WHERE e.event_type = 2  -- 1st layer - products are add to cart.
AND e.visit_id NOT IN 
	(SELECT
		visit_id
	FROM events
    WHERE event_type = 3) -- 2nd layer - products NOT purchased.
GROUP BY p.product_id, p.page_name, p.product_category
),
prod_purchased AS(
SELECT
    p.product_id,
    p.page_name,
    p.product_category,
    COUNT(e.visit_id) AS purchases
FROM events AS e 
LEFT JOIN page_hierarchy AS p
	ON p.page_id = e.page_id
WHERE e.event_type = 2  -- 1st layer - products are add to cart.
AND e.visit_id IN 
	(SELECT
		visit_id
	FROM events
    WHERE event_type = 3) -- 2nd layer - products are purchased.
GROUP BY p.product_id, p.page_name, p.product_category
)
SELECT
	pv.*,
    pa.abandoned,
    pp.purchases
FROM prod_view AS pv
LEFT JOIN prod_abandon AS pa
	ON pv.product_id = pa.product_id
LEFT JOIN prod_purchased AS pp
	ON pv.product_id = pp.product_id
ORDER BY pv.product_id;
;

SELECT
	*
fROM product_summary;
```


| product_id | page_name      | product_category | views | add_to_cart | abandoned | purchases |
|------------|----------------|------------------|-------|-------------|-----------|-----------|
| 1          | Salmon         | Fish             | 1559  | 938         | 227       | 711       |
| 2          | Kingfish       | Fish             | 1559  | 920         | 213       | 707       |
| 3          | Tuna           | Fish             | 1515  | 931         | 234       | 697       |
| 4          | Russian Caviar | Luxury           | 1563  | 946         | 249       | 697       |
| 5          | Black Truffle  | Luxury           | 1469  | 924         | 217       | 707       |
| 6          | Abalone        | Shellfish        | 1525  | 932         | 233       | 699       |
| 7          | Lobster        | Shellfish        | 1547  | 968         | 214       | 754       |
| 8          | Crab           | Shellfish        | 1564  | 949         | 230       | 719       |
| 9          | Oyster         | Shellfish        | 1568  | 943         | 217       | 726       |


#### Convert the value in the above table to percentage.
```
SELECT
    page_name,
    product_category,
    ROUND(100*views/views,1) AS views,
    ROUND(100*add_to_cart/views,1) AS add_to_cart_rate,
    ROUND(100*purchases/views,1) AS purchase_rate,
    ROUND(100*abandoned/views,1) AS fallout_rate
FROM product_summary
ORDER BY fallout_rate DESC;
```

| page_name    | product_category | views | add_to_cart_rate | purchase_rate | fallout_rate |
|----------------|------------------|-------|------------------|---------------|--------------|
| Russian Caviar | Luxury           | 100.0 | 60.5             | 44.6          | 15.9         |
| Tuna           | Fish             | 100.0 | 61.5             | 46.0          | 15.4         |
| Abalone        | Shellfish        | 100.0 | 61.1             | 45.8          | 15.3         |
| Black Truffle  | Luxury           | 100.0 | 62.9             | 48.1          | 14.8         |
| Crab           | Shellfish        | 100.0 | 60.7             | 46.0          | 14.7         |
| Salmon         | Fish             | 100.0 | 60.2             | 45.6          | 14.6         |
| Lobster        | Shellfish        | 100.0 | 62.6             | 48.7          | 13.8         |
| Oyster         | Shellfish        | 100.0 | 60.1             | 46.3          | 13.8         |
| Kingfish       | Fish             | 100.0 | 59.0             | 45.3          | 13.7         |

#### Further aggregate the data to create a funnel at the product category level.

```
CREATE TABLE category_summary
WITH cat_view AS (
SELECT 
    p.product_category,
    SUM(CASE WHEN e.event_type = 1 THEN 1 ELSE 0 END) AS views,
    SUM(CASE WHEN e.event_type = 2 THEN 1 ELSE 0 END) AS add_to_cart
FROM events AS e
LEFT JOIN page_hierarchy as p
	ON e.page_id = p.page_id
WHERE p.product_id IS NOT NULL
GROUP BY  p.product_category
),
cat_abandon AS(
SELECT
    p.product_category,
    COUNT(e.visit_id) AS abandoned
FROM events AS e 
LEFT JOIN page_hierarchy AS p
    ON p.page_id = e.page_id
WHERE e.event_type = 2  -- 1st layer - products are add to cart.
AND e.visit_id NOT IN 
	(
	SELECT
        	visit_id
	FROM events
    	WHERE event_type = 3) -- 2nd layer - products NOT purchased.
	GROUP BY p.product_category
	),
cat_purchased AS(
SELECT
    p.product_category,
    COUNT(e.visit_id) AS purchases
FROM events AS e 
LEFT JOIN page_hierarchy AS p
	ON p.page_id = e.page_id
WHERE e.event_type = 2  -- 1st layer - products are add to cart.
AND e.visit_id IN 
	(SELECT
		visit_id
	FROM events
    WHERE event_type = 3) -- 2nd layer - products are purchased.
GROUP BY p.product_category
)
SELECT
    cv.*,
    ca.abandoned,
    cp.purchases
FROM cat_view AS cv
LEFT JOIN cat_abandon AS ca
	ON cv.product_category = ca.product_category
LEFT JOIN cat_purchased AS cp
	ON cv.product_category = cp.product_category
;

SELECT
	*
FROM category_summary;
```

| product_category | views | add_to_cart | abandoned | purchases |
|------------------|-------|-------------|-----------|-----------|
| Luxury           | 3032  | 1870        | 466       | 1404      |
| Shellfish        | 6204  | 3792        | 894       | 2898      |
| Fish             | 4633  | 2789        | 674       | 2115      |

#### Convert the value in the above table to percentage.
```
SELECT
    product_category,
    ROUND(100*views/views,1) AS views,
    ROUND(100*add_to_cart/views,1) AS add_to_cart_rate,
    ROUND(100*purchases/views,1) AS purchase_rate,
    ROUND(100*abandoned/views,1) AS fallout_rate
FROM category_summary;
```

| product_category | views | add_to_cart_rate | purchase_rate | fallout_rate |
|------------------|-------|------------------|---------------|--------------|
| Luxury           | 100.0 | 61.7             | 46.3          | 15.4         |
| Shellfish        | 100.0 | 61.1             | 46.7          | 14.4         |
| Fish             | 100.0 | 60.2             | 45.7          | 14.5         |

Luxury products have higher fallout rate than the other two categories.

### 1. Which product had the most views, cart adds and purchases?
```
SELECT
	(SELECT page_name FROM product_summary ORDER BY views DESC LIMIT 1) AS most_view,
	(SELECT page_name FROM product_summary ORDER BY add_to_cart DESC LIMIT 1) AS most_add_to_cart,
        (SELECT page_name FROM product_summary ORDER BY purchases DESC LIMIT 1) AS most_purchases;
 ```

| # most_view | most_add_to_cart | most_purchases |
|-------------|------------------|----------------|
| Oyster      | Lobster          | Lobster        |

   
### 2. Which product was most likely to be abandoned?
```
SELECT
	*
FROM product_summary
ORDER BY abandoned DESC
LIMIT 1;
```

| # product_id | page_name      | product_category | views | add_to_cart | abandoned | purchases |
|--------------|----------------|------------------|-------|-------------|-----------|-----------|
| 4            | Russian Caviar | Luxury           | 1563  | 946         | 249       | 697       |

### 3. Which product had the highest view to purchase percentage?
```
SELECT
	page_name,
	ROUND(100*purchases / views,2) AS conversion_rate
FROM product_summary
ORDER BY conversion_rate DESC
LIMIT 1;
```

| page_name | conversion_rate |
|-----------|-----------------|
| Lobster   | 48.74           |

### 4.  What is the average conversion rate from view to cart add?
```
SELECT 
    ROUND(100*AVG(add_to_cart / views),2) AS conversion_rate
FROM product_summary;
```

| conversion_rate |
|-----------------|
| 60.95           |

### 5. What is the average conversion rate from cart add to purchase?
```
SELECT 
    ROUND(100*AVG(purchases / add_to_cart),2) AS conversion_rate
FROM product_summary;
```

| conversion_rate |
|-----------------|
| 75.93           |



## Part 3 - Campaign Analysis <a name="campaign-analysis"></a>
I'll create a new output table that contains the following details:
* user_id
* visit_id
* visit_start_time: the earliest event_time for each visit
* page_views: count of page views for each visit
* cart_adds: count of product cart add events for each visit
* purchase: 1/0 flag if a purchase event exists for each visit
* campaign_name: map the visit to a campaign if the visit_start_time falls between the start_date and end_date
* impression: count of ad impressions for each visit
* click: count of ad clicks for each visit
* cart_products: a comma separated text value with products added to the cart sorted by the order they were added to the cart (hint: use the sequence_number)

```
CREATE TABLE campaign_summary
SELECT
	users.user_id,
	e.visit_id,
    MIN(e.event_time) AS visit_start_time,
    SUM(CASE WHEN ei.event_name = 'Page View' THEN 1 ELSE 0 END) AS page_views,
    SUM(CASE WHEN ei.event_name = 'Add to Cart' THEN 1 ELSE 0 END) AS cart_adds,
	SUM(CASE WHEN ei.event_name = 'Purchase' THEN 1 ELSE 0 END) AS purchase,
    c.campaign_name,
	SUM(CASE WHEN ei.event_name = 'Ad Impression' THEN 1 ELSE 0 END) AS impression,
    SUM(CASE WHEN ei.event_name = 'Ad Click' THEN 1 ELSE 0 END) AS click,
    GROUP_CONCAT(CASE WHEN ei.event_name = 'Add to Cart' THEN page_name ELSE NULL END ORDER BY e.sequence_number) AS cart_products
FROM events AS e
LEFT JOIN users
	ON e.cookie_id = users.cookie_id
LEFT JOIN event_identifier AS ei
	ON e.event_type = ei.event_type
LEFT JOIN page_hierarchy AS p
	ON e.page_id = p.page_id
LEFT JOIN campaign_identifier AS c
	ON e.event_time BETWEEN c.start_date AND c.end_date
GROUP BY users.user_id, e.visit_id, c.campaign_name;

SELECT * FROM campaign_summary LIMIT 10;
```

| user_id | visit_id | visit_start_time    | page_views | cart_adds | purchase | campaign_name                     | impression | click | cart_products                                                        |
|---------|----------|---------------------|------------|-----------|----------|-----------------------------------|------------|-------|----------------------------------------------------------------------|
| 1       | 02a5d5   | 2020-02-26 16:57:26 | 4          | 0         | 0        | Half Off - Treat Your Shellf(ish) | 0          | 0     | null                                                                 |
| 1       | 0826dc   | 2020-02-26 05:58:38 | 1          | 0         | 0        | Half Off - Treat Your Shellf(ish) | 0          | 0     | null                                                                 |
| 1       | 0fc437   | 2020-02-04 17:49:50 | 10         | 6         | 1        | Half Off - Treat Your Shellf(ish) | 1          | 1     | Tuna,Russian Caviar,Black Truffle,Abalone,Crab,Oyster                |
| 1       | 30b94d   | 2020-03-15 13:12:54 | 9          | 7         | 1        | Half Off - Treat Your Shellf(ish) | 1          | 1     | Salmon,Kingfish,Tuna,Russian Caviar,Abalone,Lobster,Crab             |
| 1       | 41355d   | 2020-03-25 00:11:18 | 6          | 1         | 0        | Half Off - Treat Your Shellf(ish) | 0          | 0     | Lobster                                                              |
| 1       | ccf365   | 2020-02-04 19:16:09 | 7          | 3         | 1        | Half Off - Treat Your Shellf(ish) | 0          | 0     | Lobster,Crab,Oyster                                                  |
| 1       | eaffde   | 2020-03-25 20:06:32 | 10         | 8         | 1        | Half Off - Treat Your Shellf(ish) | 1          | 1     | Salmon,Tuna,Russian Caviar,Black Truffle,Abalone,Lobster,Crab,Oyster |
| 1       | f7c798   | 2020-03-15 02:23:26 | 9          | 3         | 1        | Half Off - Treat Your Shellf(ish) | 0          | 0     | Russian Caviar,Crab,Oyster                                           |
| 2       | 0635fb   | 2020-02-16 06:42:43 | 9          | 4         | 1        | Half Off - Treat Your Shellf(ish) | 0          | 0     | Salmon,Kingfish,Abalone,Crab                                         |
| 2       | 1f1198   | 2020-02-01 21:51:55 | 1          | 0         | 0        | Half Off - Treat Your Shellf(ish) | 0          | 0     | null                                                                 |

To evaluate the effectiveness of the campaigns, let's comparing the key metrics between customers who received the ad impression vs customers who didn't receive the ad impression. 

* I'll create two customer groups:
	* Group 1: Received impression.
	* Group 2: Didn't receive impression.
* Under Group 1, create two sub-groups:
  	* Sub-group 1: received impressions and also click the impressions.
  	* Sub-group 2: received impressions but didn't click the impressions.
* Create a performance metrics for each group and compare the metrics between the customer groups.

 	-> Performance metrics includes the page_views per user, page_views per visit, average number of products add to cart, purchase rate. 

#### Customer Group 1 - Received impression (impression > 0)

The number of customer and the visit count in this group.

```
SELECT 
	COUNT(DISTINCT user_id) AS users_count,
    COUNT(DISTINCT visit_id) AS visits
FROM campaign_summary
WHERE campaign_name IS NOT NULL
	AND impression > 0;
```

| users_count | visits |
|-------------|--------|
| 417         | 747    |


Calculate the key performance metrics for this user group.

```
SET @received_and_clicked_users = 367;
SET @received_and_clicked_visits = 599;

SELECT 
    SUM(page_views) / @received_and_clicked_users AS page_views_per_user,
    SUM(page_views) / @received_and_clicked_visits AS page_views_per_visit,
    AVG(cart_adds) AS cart_adds_per_visit,
    ROUND(AVG(purchase)*100,1) AS purchase_rate
FROM campaign_summary
WHERE campaign_name IS NOT NULL
	AND impression > 0
    AND click > 0;
```

| page_views_per_user | page_views_per_visit | cart_adds_per_visit | purchase_rate |
|---------------------|----------------------|---------------------|---------------|
| 15.3213             | 8.5529               | 5.0482              | 85.0          |

#### Customer Sub-group 1 - Received impressions and clicked the impression (impression > 0 AND click > 0)
 The number of customers and visits in this group.
 ```
 SELECT 
	COUNT(DISTINCT user_id) AS users_count,
    	COUNT(DISTINCT visit_id) AS visits
FROM campaign_summary
WHERE campaign_name IS NOT NULL
	AND impression > 0
    	AND click > 0;
```

| users_count | visits |
|-------------|--------|
| 367         | 599    |

The performance metrics of this customer group.
```
SET @received_and_clicked_users = 367;
SET @received_and_clicked_visits = 599;

SELECT 
    SUM(page_views) / @received_and_clicked_users AS page_views_per_user,
    SUM(page_views) / @received_and_clicked_visits AS page_views_per_visit,
    AVG(cart_adds) AS cart_adds_per_visit,
    ROUND(AVG(purchase)*100,1) AS purchase_rate
FROM campaign_summary
WHERE campaign_name IS NOT NULL
 	AND impression > 0
    	AND click > 0;
```

| page_views_per_user | page_views_per_visit | cart_adds_per_visit | purchase_rate |
|---------------------|----------------------|---------------------|---------------|
| 14.8038             | 9.0701               | 5.7162              | 89.6          |



#### Customer Sub-group 2 - Received impressions but didn't click the impression
 The number of customers and visits in this group.

```
Solution structure:
    -- use subquery to define the user group who received and click the impression.
    -- users who are not in the above group are those who received but not clicked the impression.
 SELECT 
	COUNT(DISTINCT user_id) AS users_count,
    	COUNT(DISTINCT visit_id) AS visits
FROM campaign_summary
WHERE campaign_name IS NOT NULL
	AND impression > 0
    	AND user_id NOT IN
    (
    SELECT
	user_id
	FROM campaign_summary 
    WHERE campaign_name IS NOT NULL
	AND impression > 0
        AND click > 0);
```

| users_count | visits |
|-------------|--------|
| 50          | 61     |


The performance metrics for this customer group.
```
SET @received_not_clicked_users = 50;
SET @received_not_clicked_visits = 61;

SELECT 
    SUM(page_views) / @received_not_clicked_users AS page_views_per_user,
    SUM(page_views) / @received_not_clicked_visits AS page_views_per_visit,
    AVG(cart_adds) AS cart_adds_per_visit,
    ROUND(AVG(purchase)*100,1) AS purchase_rate
FROM campaign_summary
WHERE campaign_name IS NOT NULL
    AND impression > 0
    AND user_id NOT IN
    (
    SELECT
        user_id
	FROM campaign_summary 
    WHERE campaign_name IS NOT NULL
	AND impression > 0
        AND click > 0);
```

| page_views_per_user | page_views_per_visit | cart_adds_per_visit | purchase_rate |
|---------------------|----------------------|---------------------|---------------|
| 7.6200              | 6.2459               | 2.2295              | 65.6          |


#### Customer Group 2 - didn't receive impressions

The number of customers in this group.
```
solution structure:
-- Note: We can't use impression = 0 as the condition to filter the data as a user could have visited the website for twice during the campaign but recieved the impression only once. In this case, when you count the users using the condition of impression is 0, this customer will be counted in which is incorrect.
-- The right way is to use subquery to create a group who received impression; users who do not fall into this group will be the group who didn't receive impressions.

SELECT 
      COUNT(DISTINCT user_id) AS users_count,	  
      COUNT(DISTINCT visit_id) AS visits
FROM campaign_summary
WHERE campaign_name IS NOT NULL
      AND user_id NOT IN
    (
    SELECT
	user_id 
	FROM campaign_summary
    WHERE impression > 0
	AND campaign_name IS NOT NULL
    );
```

| users_count | visits |
|-------------|--------|
| 78          | 368    |


The performance metrics for this customer group.

```
SET @not_received_users = 56;
SET @not_received_visits = 268;

SELECT 
    SUM(page_views) / @not_received_users AS page_views_per_user,
    SUM(page_views) / @not_received_visits AS page_views_per_visit,
    AVG(cart_adds) AS cart_adds,
    ROUND(AVG(purchase)*100,1) AS purchase_rate
FROM campaign_summary
WHERE campaign_name IS NOT NULL
	AND user_id NOT IN
    (
    SELECT
	user_id 
	FROM campaign_summary
    WHERE impression > 0
	AND campaign_name IS NOT NULL
    );
```

| page_views_per_user | page_views_per_visit | cart_adds | purchase_rate |
|---------------------|----------------------|-----------|---------------|
| 26.4821             | 5.5336               | 1.1848    | 27.2          |


Now put all the four customer groups together.


| **Customer Group**                     | **user_count** | **visits** | **page_views_per_user** | **page_views_per_visit** | **cart_adds** | **purchase_rate %** |
|----------------------------------------|----------------|------------|-------------------------|--------------------------|---------------|---------------------|
| Received impressions                   | 417            | 747        | 15.3213                 | 8.5529                   | 5.0482        | 85                  |
| Received impressions and clicked       | 367            | 599        | 14.8038                 | 9.0701                   | 5.7162        | 89.6                |
| Received impressions but didn't  click | 50             | 61         | 7.62                    | 6.2459                   | 2.2295        | 65.6                |
| Didn't receive impressions             | 56             | 268        | 26.4821                 | 5.5336                   | 1.1848        | 27.2                |


Customers who received the promotions visited more pages in each visit than customers who didn't receive the promotion (8.6 vs 5.5 page views per visit). Customers who received the promotion also purchase more than those who didn't receive the ad (average 5 cart-add vs 1.2). The purchase conversion rate is substantially higher (85% vs 27.2%). 

Those who click the ad displayed higher page views, cart-add and purchases than those who didn't click the ad. Also note 88% of the users who received the promotion clicked the promotion ad with only 12% didn't click. This also shows that promotions did draw the attention of the customers. 

Finally, Let's compare the performance between the three campaigns.

```
WITH campaign_performance AS(
SELECT
    campaign_name,
    SUM(impression) AS no_of_impressions,
    SUM(click) AS no_of_clicks,
    SUM(click) / SUM(impression) AS click_rate
FROM campaign_summary
WHERE campaign_name IS NOT NULL
GROUP BY campaign_name
),
campaign_purchase_rate AS(
SELECT 
    campaign_name,
    AVG(purchase) AS purchase_rate
FROM campaign_summary
WHERE impression > 0
    AND campaign_name IS NOT NULL
GROUP BY campaign_name
)
SELECT
    campaign_performance.*,
    campaign_purchase_rate.purchase_rate
FROM campaign_performance
LEFT JOIN campaign_purchase_rate
    ON campaign_performance.campaign_name = campaign_purchase_rate.campaign_name;
```

| campaign_name                     | no_of_impressions | no_of_clicks | click_rate | purchase_rate |
|-----------------------------------|-------------------|--------------|------------|---------------|
| Half Off - Treat Your Shellf(ish) | 578               | 463          | 0.8010     | 0.8529        |
| 25% Off - Living The Lux Life     | 104               | 81           | 0.7788     | 0.8365        |
| BOGOF - Fishing For Compliments   | 65                | 55           | 0.8462     | 0.8462        |

* Half Off campaign has the broadest reach of users and achieved the highest purchase rate. 
* BOGOF had the highest click rate. The purchase rate is also very impressive. Clique Bait could consider run this campaign in a larger scale in future.
* 25% Off campaign has the lowest click rate among the three campaigns. However, the purchase rate is not too far off compared with the other two campaigns. 


# Insights & Recommendations  <a name="insights-recommendations"></a>
To boost the sales growth, the management team should focus on managing the conversion rate, particularly the conversion from page view to add-to-cart and from add-to-cart to finally making the purchase. In this aspect, the management should keep an eye on the customers who visit the checkout page but didn't make purchases. It is recommended that we collect further information to understand what caused the customers abandoned the checkout. 

The management team could consider optimize the campaigns to driver further sales uplift. Based on the sales and click-view performance of the previous three campaigns, "Half-Price" and "Buy-one-get-one-free" are the most effective. Management team could consider extend the reach of those campaigns in future if the budget permits. Suggest do further customer behaviours analysis to identify what types of customers are more likely to click the ad so we can target the customers to run the promotion to driver better outcome.

The analysis shows that Oyster and Crab are the most purchased products. The management team could leverage the data insights to plan the purchase and stocking. Luxury category reveals very distinctive shopping behaviours - high views but low conversion. The management team could consider implement some limited-time promotions such as flash sales to generate excitement, drive sales and this could also help clear out excessive stocks.


# Growth/Next Steps <a name="growth-next-steps"></a>

* To drive the conversion rate up, we could test different promotional strategies and track the change of the product funnel conversion and fallout rate. 

* We could also collect external data to establish a benchmark for the key metrics to help us better gauge our performance. 

* Further analysis on customers visits and shopping basket to segment the customers and develop more customized campaigns and promotions.

<br>

Note: This project comes from [#8WeekSQLChallenge-CaseStudy#6](https://8weeksqlchallenge.com/case-study-6/)
