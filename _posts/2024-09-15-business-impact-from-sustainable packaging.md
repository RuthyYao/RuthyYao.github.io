---
layout: post
title: Business Impact Analysis From Change to Sustainable Packaging
image: "/data-mart/5.png"
tags: [event analysis, SQL]
---

Clique Bait, an online seafood shop wants to gain detailed insights into their store and customers. In particular, the management team would like to track their customer journeys and optimize marketing strategies.

# Table of contents

- [00. Project Overview](#overview-main)
    - [Business Problem](#overview-business-problem)
    - [Actions](#overview-actions)
    - [Results](#overview-results)
    - [Insights & Recommendations](#overview-insights-recommendations)
    - [Growth/Next Steps](#overview-growth)


# Project Overview  <a name="overview-main"></a>

### Business Problem <a name="overview-business-problem"></a>
Data Mart is an online supermarket that specializes in fresh produce. In June 2020 - large scale supply changes were made at Data Mart. All Data Mart products now use sustainable packaging methods in every single step from the farm all the way to the customer.

The management wants to quantify the impact of this change on the sales performance for Data Mart and it’s separate business areas.

The key business questions they'd like to answer are the following:

* What was the quantifiable impact of the changes introduced in June 2020?
* Which platform, region, segment and customer types were the most impacted by this change?
* What can we do about future introduction of similar sustainability updates to the business to minimise impact on sales?

### Actions <a name="overview-actions"></a>

I took the following steps to complete the analysis:

* **Data Cleaning and Preparation** - This involves converting the incorrect data type, creating new columns.
* **Data Understanding and Exploration** - To understand what information contained in the dataset, such as the month/period covered in this dataset, transactions by platforms, sales by platforms and etc.
* **Event Analysis** - Compare the "before-the-event" and "After-the-event" sales to quantify the sales impact from the packaging change.
   
For each part of the analysis, I used SQL for data extraction, manipulation and gaining the insights on the business performance.  

### Results <a name="overview-results"></a>

The analysis shows that Data Mart's sales has declined post the change to sustainable packaging. On a 4-weeks period, the sales dropped by 1.15%. The magnitude of the decline increased to -2.14% if looking at a 12-weeks period. 

Region wise, Asia and Oceania have the largest percentage of decline (-3.26% and -3.03% respectively). To the opposite, sales in Europe jumped up by 4.73%.

Platform wise, Retail sales fell by -2.43% whereas sales in Shopify surprisingly increased by 7.18%.

From a customer age band and demographic perspective, Middle aged customers and families saw the most sales decline. This is after we exclude the "unknown" customer groups where we don't have the information on their age and demographic.

Finally, guests and existing customers' sales declined whereas we saw new customers sales are surging. This gives us the confidence that the packaging change doesn't pose any threat to our customer acquisition strategy. 



### Insights & Recommendations <a name="overview-insights-recommendations"></a>


We need to proactively manage the transition to the sustainable packaging to minimize the impact on our sales. 
	
Particularly, in the most negatively impacted regions, we could slow down the pace of introducing the new packages. For example, we could offer the two types of packages at the same time for an extended period to help customers transition to the new packages.

When it comes to the platform, as Retail comprised of 97% of our total sales, even a slightly decrease in retail sales will drag the total company's sales performance down. Hence, we need to put in much more efforts to the retail channel to manage the sales impact. For instance, we could give customers more support in the transition period such as giving out the re-usable bags for free to help customers adapt to the change.

Furthermore, as we see middle aged customers and families got the largest hit in sales, we could consider implementing some educational programs drive more the public awareness on why to make the change on packaging and to win their support.  

Finally, we should leverage this opportunity to accelerate new customer acquisition and drive more sales from new customers, particularly in our Shopify platform. For example, we could run some brand marketing activities to strengthen our sustainable brand, increasing the coverage to maximize the reach to customers. 



### Growth/Next Steps <a name="overview-growth"></a>

We could run the same analysis for an extended period, such as in six months and in a year to inspect whether our sales rebound - the magnitude and the speed. This could also help us to measure the effectiveness of our prescribed actions above.
___

To see details of the analysis and [my SQL syntax solutions](https://github.com/RuthyYao/8-Weeks-SQL-Challenge/tree/main/Case%20Study%20%235%20-%20Data%20Mart)

<br>

Note: This project comes from [#8WeekSQLChallenge-CaseStudy#5](https://8weeksqlchallenge.com/case-study-5/)
