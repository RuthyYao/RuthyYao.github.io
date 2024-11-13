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
