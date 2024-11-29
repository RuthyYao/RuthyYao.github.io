---
layout: post
title: Boost the Business Growth Through Effective Campaigns
image: "/clique bait/6.png"
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
- [01. Data Overview](#data-overview)
- [02. Exploratory Analysis](#exploratory-analysis)
- [03. Results & Application](#results-application)
- [04. Growth & Next Steps](#growth-next-steps)

___

# Project Overview  <a name="overview-main"></a>

### Business Problem <a name="overview-business-problem"></a>
Clique Bait has established the e-commerce channel dive months ago. The management team wants to establish a view on the online store performance and identify the areas for improvement so they achieve faster business growth. 

### Actions <a name="overview-actions"></a>
I first compiled the necessary data from five datasets that provided the customer data, page visits and campaigns information.

Based on the business requirement, I splited the analysis task into three parts:

 - **Part 1 - Digital Analysis**  - to extract insights on the customer visits, page views and purchases.
 - **Part 2 - Product Funnel** - create a product funnel to analyse the add-to-cart rate nad purchase rate.
 - **Part 3 - Campaign Analysis** - to evaluate the success of each campaign.
   
For each part of the analysis, I used SQL for data extraction and manipulation, gaining the insights on customer behaviours, online store conversions and top performing products.  

### Results <a name="overview-results"></a>
Clique Bait has acquired 500 customers over the last four to five months. On avereage each customer visits the online store for 7.1 times over five-months period. The purchase rate is ~50%. The average add-to-cart rate is 61% and the conversion from add-to-cart to purchase is ~76%. About 15.5% of time customers visit the checkout page but didn't maake a purchase.

The most purchased product is lobster which also has the highest view-to-purchase conversion rate. The top 3 visited pages are Oyster, Crab followed by Russian Caviar. Ironically,  Russian Caviar is the most likely to be abandoned product(add to cart but not purchased) with an abandoned rate of 26%. 

### Insights & Recommendations <a name="overview-insights-recommendations"></a>
To support the management team to monitor the business performance ongoingly, I would leverage the data insights to build a dahsboard that allows us to track the key metrics over time. Specifically, I would call out the following KPIs:
* **Monthly Revenue Growth** - how does the business grow their revenue monty-over-month.
* **Total subscribers** - how many customers the business has in total at a point. This reflects the reach and popularity of Foodie Fi.
* **The customer growth** - how customers increase month-over-month. THis reveals the momentum of the expansion of their customer base.
* **Conversion rate** - how many customers stay in Foodie Fi after the trial. Howe does the rate look like.
* **Churn rate** - how many customers cancel their plan each month?  This signals customer dissatisfaction and can help pinpoint areas for improvements in suer expereince, pricing or content library etc.
