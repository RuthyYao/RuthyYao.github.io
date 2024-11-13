---
layout: post
title: Customer Acquistion and Monetization Analysis
image: "/posts/foodie-fi.png"
tags: [Customer Acquisition and Retention, Product Performance, Exploratory Analysis, SQL]
---

Foodie Fi, a streaming service provider, wants to utilise data-driven analysis to inform the investment decisions on products and customers to drive business growth!

# Table of contents

- [00. Project Overview](#overview-main)
    - [Business Problem](#overview-business-problem)
    - [Actions](#overview-actions)
    - [Results](#overview-results)
    - [Applications](#overview-applications)
    - [Growth/Next Steps](#overview-growth)
- [01. Data Overview](#data-overview)
- [02. Exploratory Analysis](#exploratory-analysis)
- [03. Results & Application](#results-application)
- [04. Growth & Next Steps](#growth-next-steps)

___

# Project Overview  <a name="overview-main"></a>

### Business Problem <a name="overview-business-problem"></a>
Foodie Fi started the video streaming service that only had food related content a year ago. They sell monthly and annual sbuscription plans, giving their customer unlimited on-demand access to exclusively food related vedios from around the world. The management team wants to review the product performance and would like to rely on data to inform their future investment decisions on new product features, customer acquisition and retention and other business growth strategies.
<br>
<br>

### Actions <a name="overview-actions"></a>
I first compiled the necessary data from the data tables that contains the plans and customer subscriptions data.
Then I consolidated the data tables and from there, I learned about the diffenet customer onboarding journeys. 
Next, I applied SQL syntax to perform the data analysis and exploration where I gained the insights on some key business performance metrics such as 
* The number of newly acquried customers
* The customers distribution by products
* The percentage of customers who upgrade their plans
* The average days for customers to upgrade from trial to a paid premium plan. etc.

On top of that, I also created a payment table that allows the business to work out the monthly revenue which would give us fruther insights on the business growth.
<br>

### Results <a name="overview-results"></a>
Foodie Fi have acquired 1000 customers since the business started with c.80 new customers each month. Of the total 1000 customers, 307 customers has churned - churn rate 30.7%.  Data shows that after the trial, 55% of the customers upgrade to the basic monthly plan, 32.5% of the customers subscribed the pro monthly plan, 3.7% of the customers upgraded to the pro annual plan straightaway and 9.2% of the customers churned. It took averagely 105 days from trial to upgrade to a pro plan (paid premium plans). In 2021, there were 123 customers upgraded to a pro plan.  

### Applications <a name="overview-applications"></a>
To support the management team to monitor the business performance ongoingly, I would leverage the data insights to build a dahsboard that allows us to track the key metrics over time. Specifically, I would call out the following KPIs:
* **Monthly Revenue Growth** - how does the business grow their revenue monty-over-month.
* **Total subscribers** - how many customers the business has in total at a point. This reflects the reach and popularity of Foodie Fi.
* **The customer growth** - how customers increase month-over-month. THis reveals the momentum of the expansion of their customer base.
* **Conversion rate** - how many customers stay in Foodie Fi after the trial. Howe does the rate look like.
* **Churn rate** - how many customers cancel their plan each month?  This signals customer dissatisfaction and can help pinpoint areas for improvements in suer expereince, pricing or content library etc.

### Growth/Next Steps <a name="overview-growth"></a>
* **Improve the customer retention** - Further analysis on customers engagement for the customer cohort who upgrade their plan, those who downgrade from pro to basic plans, and those who cancel their subscriptions to yield additional insights on on how to improve customer retentions.
* **Reduce the customer churn rate** - Leverage the data insights to design an exit survey to customers who wish to cancel thier subscriptions. This could help Foodie Fi to identify the common reasons for their cancellation and take measures to reduce the customer churn. We could monitor the churn rate and convertion rate to validate the effectiveness of those measures.

# Data Overview  <a name="data-overview"></a>
The original dataset has two data tables. 

Table 1: plans
<br>
| **plan_id** | **plan_name** | **price** |
|---|---|---|
| 0 | trial | 0 |
| 1 | basic monthly | 9.90 |
| 2 | pro monthly | 19.90 |
| 3 | pro annual | 199 |
| 4 | churn | null |


Table 2: subscriptions (example)
<br>
| **customer_id** | **plan_id** | **start_date** |
|---|---|---|
| 1 | 0 | 2020-08-01 |
| 1 | 1 | 2020-08-08 |
| 2 | 0 | 2020-09-20 |
| 2 | 3 | 2020-09-27 |

Entity Relationship Diagram:
<br>
<img src="https://github.com/RuthyYao/RuthyYao.github.io/blob/master/img/posts/foodie-fi-erd.png" >

We need to use the plan_id as the join key to join the two tables. 
<br>
<br>
# Exploratory Analysis  <a name="exploratory-analysis"></a>
## Customer Onboarding Journey 
```TSQL
SELECT 
	subscriptions.*,
	plans.plan_name,
	plans.price
FROM subscriptions
JOIN plans ON subscriptions.plan_id = plans.plan_id
WHERE customer_id IN (1, 2, 11, 13, 15, 16, 18, 19);
```
| customer_id | plan_id | start_date | plan_name     | price   |
|-------------|---------|------------|---------------|---------|
| 1           | 0       | 2020-08-01 | trial         | 0.00    |
| 1           | 1       | 2020-08-08 | basic monthly | 9.90    |
| 2           | 0       | 2020-09-20 | trial         | 0.00    |
| 2           | 3       | 2020-09-27 | pro annual    | 199.00  |
| 11          | 0       | 2020-11-19 | trial         | 0.00    |
| 11          | 4       | 2020-11-26 | churn         | NULL    |
| 13          | 0       | 2020-12-15 | trial         | 0.00    |
| 13          | 1       | 2020-12-22 | basic monthly | 9.90    |
| 13          | 2       | 2021-03-29 | pro monthly   | 19.90   |
| 15          | 0       | 2020-03-17 | trial         | 0.00    |
| 15          | 2       | 2020-03-24 | pro monthly   | 19.90   |
| 15          | 4       | 2020-04-29 | churn         | NULL    |
| 16          | 0       | 2020-05-31 | trial         | 0.00    |
| 16          | 1       | 2020-06-07 | basic monthly | 9.90    |
| 16          | 3       | 2020-10-21 | pro annual    | 199.00  |
| 18          | 0       | 2020-07-06 | trial         | 0.00    |
| 18          | 2       | 2020-07-13 | pro monthly   | 19.90   |
| 19          | 0       | 2020-06-22 | trial         | 0.00    |
| 19          | 2       | 2020-06-29 | pro monthly   | 19.90   |

* Customer 1 - signed up to 7-day free trial on 01/08/2020. After that time, he/she didn't cancel the subsciption, so the system automatically upgraded it to basic monthly plan on 08/08/2020.

* Customer 2 - signed up to 7-day free trial on 20/09/2020. After that time, he/she upgraded to pro annual plan on 27/09/2020.

* Customer 11 -  signed up to 7-day free trial on 19/11/2020. After that time, he/she cancelled the subsciption on 26/11/2020.

* Customer 13 - signed up to 7-day free trial on 15/12/2020. After that time, he/she didn't cancelled the subsciption, so the system automatically upgraded it to basic monthly plan on 22/12/2020. He/she continued using that plan for 2 months. On 29/03/2020 (still in the 3rd month using basic monthly plan), he/she upgraded to pro monthly plan.

* Customer 15 - signed up to 7-day free trial on 17/03/2020. After that time, he/she didn't cancel the subsciption, so the system automatically upgraded it basic monthly plan on 24/03/2020. He/she then cancelled that plan after 5 days (29/03/2020). He/she was able to use the basic monthly plan until 24/04/2020.

* Customer 16 - signed up to 7-day free trial on 31/05/2020. After that time, he/she didn't cancel the subsciption, so the system automatically upgraded it to basic monthly plan on 07/06/2020. He/she continued using that plan for 4 months. On 21/10/2020 (still in the 4th month using basic monthly plan), he/she upgraded to pro annual plan.

* Customer 18 - signed up to 7-day free trial on 06/07/2020. After the trial time, he/she upgraded the subscription to pro monthly plan on 13/07/2020.

* Customer 19 - signed up to 7-day free trial on 22/06/2020. After that time, he/she upgraded the subscription to pro monthly plan on 29/06/2020. After 2 months using that plan, he/she upgraded to pro annual plan on 29/08/2020.
<br>

## Data Analysis Questions
### 1. How many customers has Foodie-Fi ever had?
```TSQL
SELECT COUNT(DISTINCT customer_id) AS total_customers
FROM subscriptions;
```
| total_customers  |
|------------------|
| 1000             |

---
### 2. What is the monthly distribution of trial plan start_date values for our dataset - use the start of the month as the group by value?
```TSQL
SELECT 
    DATE_FORMAT(
		DATE_ADD(
			subscriptions.start_date, INTERVAL 1-DAYOFMONTH(subscriptions.start_date) DAY
            ),
		'%Y-%m'
    ) AS start_month,
    plans.plan_name,
    COUNT(subscriptions.customer_id) AS customer_count
FROM subscriptions
LEFT JOIN plans
	ON subscriptions.plan_id = plans.plan_id
WHERE plans.plan_name = 'trial'
GROUP BY start_month
ORDER BY start_month;
```

| start_month   | plan_name | customer_count|
|---------------|-----------|---------------|
| 2020-01       |trial      |	88          |
| 2020-02       |trial      |	68          |
| 2020-03	    |trial      |	94          |
| 2020-04	    |trial      |	81          |
| 2020-05	    |trial      |	88          |
| 2020-06	    |trial      |	79          |
| 2020-07	    |trial      |	89          |
| 2020-08	    |trial      |	88          |
| 2020-09	    |trial      |	87          |
| 2020-10	    |trial      |	79          |
| 2020-11	    |trial      |	75          |
| 2020-12	    |trial      |	84          |

---
### 3. What plan start_date values occur after the year 2020 for our dataset? Show the breakdown by count of events for each plan_name?
```TSQL
SELECT 
	subscriptions.plan_id,
    plans.plan_name,
    COUNT(customer_id) AS subs_count
FROM subscriptions
LEFT JOIN plans
	ON subscriptions.plan_id = plans.plan_id
WHERE YEAR(subscriptions.start_date) > 2020
GROUP BY subscriptions.plan_id, plans.plan_name
ORDER BY subscriptions.plan_id;
```
| plan_id | plan_name    | subs_count  |
|--------|---------------|-------------|
| 1      | basic monthly | 8           |
| 2      | pro monthly   | 60          |     
| 3      | pro annual    | 63          |
| 4      | churn         | 71          |

---
### 4. What is the customer count and percentage of customers who have churned rounded to 1 decimal place?
```TSQL
-- Label each row with 1 or 0 based on the plan name (churn) and sum all the values with 1 divided by total
SELECT
	SUM(CASE WHEN plans.plan_name = 'churn' THEN 1 ELSE 0 END) AS churn_count,
    ROUND(SUM(CASE WHEN plans.plan_name = 'churn' THEN 1 ELSE 0 END) *100 / COUNT(DISTINCT customer_id),1) AS churn_percentage
FROM subscriptions
LEFT JOIN plans
	ON subscriptions.plan_id = plans.plan_id;
```
| churn_count | churn_percentage   |
|-------------|--------------------|
| 307         | 30.7               |

---
### 5. How many customers have churned straight after their initial free trial - what percentage is this rounded to the nearest whole number?
```TSQL
WITH cte AS (
	SELECT 
		subscriptions.customer_id,
		subscriptions.plan_id,
		plans.plan_name AS current_plan,
        LEAD(plans.plan_name) OVER (PARTITION BY subscriptions.customer_id ORDER BY subscriptions.start_date) AS next_plan
	FROM subscriptions
	LEFT JOIN plans
		ON subscriptions.plan_id = plans.plan_id
  )
SELECT	
	COUNT(customer_id) AS churn_after_trial,
    ROUND(COUNT(customer_id) *100 / (SELECT COUNT(DISTINCT customer_id) FROM subscriptions),0) AS churn_percentage
FROM cte
WHERE current_plan = 'trial' AND next_plan = 'churn';
```
| churn_after_trial | churn_percentage |
|-------------------|------------------|
| 92                | 9                |

---
### 6. What is the number and percentage of customer plans after their initial free trial?
```TSQL
WITH cte AS (
	SELECT 
		subscriptions.customer_id,
		subscriptions.plan_id,
		plans.plan_name AS current_plan,
        LEAD(plans.plan_name) OVER (PARTITION BY subscriptions.customer_id ORDER BY subscriptions.start_date) AS next_plan
	FROM subscriptions
	LEFT JOIN plans
		ON subscriptions.plan_id = plans.plan_id
 )
 SELECT
	next_plan AS post_trial_plan,
    COUNT(customer_id) AS count,
    ROUND(COUNT(customer_id) *100 / (SELECT COUNT(customer_id) FROM subscriptions WHERE plan_id = 0),1) AS percentage
from cte
WHERE current_plan = 'trial'
GROUP BY next_plan;
```
| post_trial_plan | count | percentage  |
|-----------------|-------|-------------|
| basic monthly   | 546        | 54.6   |
| pro annual      | 37         | 3.7    |
| pro monthly     | 325        | 32.5   |
| churn           | 92         | 9.2    |

---
### 7. What is the customer count and percentage breakdown of all 5 plan_name values at 2020-12-31?
```TSQL
WITH cte AS (	
    SELECT 
		subscriptions.customer_id,
		subscriptions.plan_id,
		plans.plan_name AS current_plan,
        LEAD(plans.plan_name) OVER (PARTITION BY subscriptions.customer_id ORDER BY subscriptions.start_date) AS next_plan
	FROM subscriptions
    LEFT JOIN plans
        ON subscriptions.plan_id = plans.plan_id
	WHERE subscriptions.start_date <= '2020-12-31'
	)
SELECT 
    plan_id,
    current_plan,
    COUNT(customer_id) AS customer_count,
	ROUND(COUNT(customer_id) *100 / (SELECT COUNT(DISTINCT customer_ID) FROM subscriptions WHERE start_date <= '2020-12-31'),1) AS percentage
FROM cte
WHERE next_plan IS NULL
GROUP BY plan_id, current_plan
ORDER BY plan_id;
```
| plan_id | plan_name     | customer_count | percentage  |
|---------|---------------|-----------|------------------|
| 0       | trial         | 19        | 1.9              |
| 1       | basic monthly | 224       | 22.4             |
| 2       | pro monthly   | 326       | 32.6             |
| 3       | pro annual    | 195       | 19.5             |
| 4       | churn         | 235       | 23.6             |

---
### 8. How many customers have upgraded to an annual plan in 2020?
```TSQL
SELECT 
  plans.plan_name,
  COUNT(DISTINCT customer_id) AS customer_count
FROM subscriptions
JOIN plans ON subscriptions.plan_id = plans.plan_id
WHERE plans.plan_name = 'pro annual'
  AND YEAR(subscriptions.start_date) = 2020;
```
| plan_name  | customer_count  |
|------------|-----------------|
| pro annual |195              |

---
### 9. How many days on average does it take for a customer to an annual plan from the day they join Foodie-Fi?
```TSQL
WITH AnnualPlan AS (
SELECT
	subscriptions.customer_id,
    subscriptions.start_date AS annualplan_start_date
FROM subscriptions
LEFT JOIN plans
	ON subscriptions.plan_id = plans.plan_id    
WHERE plans.plan_name = 'pro annual'
),
JoinDate AS (
SELECT
	subscriptions.customer_id,
    subscriptions.start_date AS join_date
FROM subscriptions
LEFT JOIN plans
	ON subscriptions.plan_id = plans.plan_id
WHERE plans.plan_name = 'trial'
 )
 SELECT 
	ROUND(AVG(DATEDIFF(annualplan_start_date,join_date)),0) AS avg_days_to_annual
FROM AnnualPlan
JOIN JoinDate
WHERE AnnualPlan.customer_id = JoinDate.customer_id;
```
| avg_days_to_annual  |
|---------------------|
| 105                 |

On average, it takes 105 days for a customer to an annual plan from the day they join Foodie-Fi.

---
