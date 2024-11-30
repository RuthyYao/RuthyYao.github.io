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
- [03. Results & Application](#results-application)
- [04. Growth & Next Steps](#growth-next-steps)

___

# Project Overview  <a name="overview-main"></a>

### Business Problem <a name="overview-business-problem"></a>
Clique Bait has established the e-commerce channel dive months ago. The management team wants to establish a view on the online store performance and identify the areas for improvement so they achieve faster business growth. 

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

Campaigns had substantially boosted the page views. From January to March, Clique Bait run three campaigns, resulting in page view reaching above 800 marks. In contrast, during April and May when there aren’t any campaigns, the page visits dropped to 200. Compare the customers who receive the campaign ad impression with those who didn't receive the impression, the purchase rate was substantially higher for the former - 89% vs the latter 28%, which proved that campaigns effectively drive the sales. 

Of the three campaigns, "half-price" promotion achieves the highest impression-to-purchase conversion rate - 85.3% followed by "Buy-one-get-one-free" achieved 84.6%. 


### Insights & Recommendations <a name="overview-insights-recommendations"></a>

To boost the sales growth, the management team should focus on managing the conversion rate, particularly the conversion from page view to add-to-cart and from add-to-cart to finally making the purchase. In this aspect, the management should keep an eye on the customers who visit the checkout page but didn't make purchases. It is recommended that we collect further information to understand what caused the customers drop the basket. 

The management team could consider optimize the campigns to driver further sales uplift. Based on the sales and click-view performance of the previous three campaigns, "Half-Price" and "Buy-one-get-one-free" are the most effective. Management team could consider extend the reach of those campaigns in future if the budget permits. Suggest do further customer behaviours analysis to identify what types of customers are more likely to click the ad so we can target the customers to run the promotion to driver better outcome.

The analysis shows that Oyster and Crab are the most purchased products. The management team could leverage the data insights to plan the purchase and stocking. Luxury category reveals very distinctive shopping behaviours - high views but low conversion. The management team could consider implement some limited-time promotions such as flash sales to generate excitement, drive sales and this could also help clear out excessive stocks.

### Growth/Next Steps <a name="overview-growth"></a>

* To drive the conversion rate up, we could test different promotional strategies and track the change of the product funnel conversion and fallout rate. 

* We could also collect external data to establish a benchmark for the key metrics to help us better gauge our performance. 

* Further analysis on customers visits and shopping basket to segment the customers and develop more customerized campaigns and promotions.


# Data Overview  <a name="data-overview"></a>

Entity Relationship Diagram:

<img src="https://github.com/RuthyYao/RuthyYao.github.io/blob/master/img/clique-bait/case-study-6-erd.PNG">

<br>
![alt text](/img/clique-bait/case-study-6-erd.PNG "Entity Relationship Diagram")
<br>

The original dataset have five data tables. The primary data table is "events" which is the raw data of the customer visits. It stores the visits id, the visti time, the page visited and the activities on the page. 

<br>

The "users" table stores the customers information including their user id and the cookies they have and the time each cookie generated. 
<br>

"Event_identifier"  and "Page Hierarchy" are mapping tables. The former provides the activities names for each event_id and the page name and the latter maps out the page_name and product hierarchy for each page id. Note that each product has a page Hence it has a unique page id and product id. 
<br>

Finally, the "campaign identifier" table provide the three campaigns's start date and end date and the products that the camppaign was on.


# Data Analysis  <a name="data-analysis"></a>

## Digital Analysis <a name="digital-analysis"></a>

### 1. Calculate total number of customers.
```SQL
SELECT 
	COUNT(DISTINCT user_id) AS customer_count
FROM users;
```
| customer_count |
| -------------- |
| 500            |



### 2. What is the unique number of visits by all users per month?
```SQL
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
