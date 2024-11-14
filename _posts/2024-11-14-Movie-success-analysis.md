---
layout: post
title: Movie Success Analysis
image: "/movie-success-analysis/front_image.png"
tags: [Exploratory Analysis, Python]
---

Our client is preparing to enter the movie production market. To increase their chances of success, I analysed over 2000 movie titles and provide recommendation on genres, release month and production budget.


## Overview

This project analyses the key successful factors of a movie studio to prepare Microsoft to enter the movie production market. Description analysis of the popularity score, gross revenue, production budget and profit shows that the top performing genres are Animations, Sci-fi and Adventures and the best months to release movies in a year are May, July and Novemeber. It is advisable to allocate at least $500m of budget to movie production each year.

## Business Problem

As a new entrant to the movie production market, Microsoft has limited industry knowledge. To complete with globally well-established production companies which have generally over seven to eight decades of history, it is crucial to dive into the vast movie database to distill insights on where to start, when to start and how much funding is required. This will help Microsoft to bridge the knowledge gap, allocate the resources more efficeintly and increase its chances of success for the new studio. 

## Data and Methods

The analysis is built on the data collated from four well-known movie databases - IMDB, The Numbers, The Movie DataBase and Box Office Mojo. Consolidation of the four datasets brings in over 2000 movies released between 2010 and 2018. Each movie is featured with genre, release date, studio, popularity score, gross revenue and production budget.

The project uses descriptive analysis, including description of the average popularity and gross revenue by genres, the year-over-year production budget of an average studio and the trend/pattern of box office performance on a month-by-month basis over nine years' period. This provides valuable data insights to support the success of the new studio.  

## Results

Based on the average popularity socre of each genre and the aerage worldwide gross revenue of each genre, the most popular and the best performing genres are Animation, Sci-fi and Adventure.

![popularity_score_per_genre](./images/popularity_score_per_genre.png)
<br>
![alt text](/img/movie-success-analysis/popularity_score_per_genre.png "Popularity Score per Genre")
![gross_revenue_per_genre](./images/gross_revenue_per_genre.png)
<br>
![alt text](/img/movie-success-analysis/gross_revenue_per_genre.png "Gross Revenue per Genre")
<br>
The worldwide gross revenue typically peaks in May, July and November, potentially due to school holiday and the "Academy Awards" effect - studios release their movies two or three months before the Awards in order to be eligible for the nomination. 

![average_gross_revenue_by_month](./images/average_gross_revenue_by_month.png)

![alt text](/img/movie-success-analysis/average_gross_revenue_by_month.png "Average Gross Revenue by Month")


Studios commit a production budget of averagely $550-$700 per annum. 
![studio_annual_production_budget](./images/Studio_annual_production_budget.png)

![alt text](/img/movie-success-analysis/Studio_annual_production_budget.png "Studio Annual Production Budget")

## Conclusions

This analysis leads to three recommendations for Microsoft to start the movie production business successfully.

- **Focus on genres with a mix of Animation, Sci-fi and Adventure.** This type of movies have potentially the broadest span of audience demographics. Hence from popularity and box office performance persepctives, those types of movie deliver the most success. 

- **Allocate at least $500m budget to movie production each year.** Given that a movie costs averagely $40m to $50m to produce with the Animation/Sci-fi/Adventure requiring even higher budget(at least $80m), Microsoft need to be prepared to invest at least $500m per year to to the new studio in order to make an impactful debut to the movie market and sustain the ongoing success of the studio. 

- **Release movies in May/July or November to maximize the box office revenue and achieve the best theatrical view.** School holiday season is the best time to relase movie, especially for the Animation/Sci-fi/Adventure movies that target kids and families. Novermber is also a good time to release movie if Microsoft wants to compete in the upcoming Academy Awards as releasing a movie two or three months before the nomination of the awards will make it fresh in the voters' mind, increasing the chances of win.   

### Nest Steps
Further analyses could yield additional insights to further increase the chances of success of the new studio:

- **Modelling to extract the insights from movie reviews and critiques** - Extracting and analysing data from reviews and critiques can unveil further insights on what kinds of movies are liked or disliked by the public.  

- **Customer segmentation analysis** - Segmenting the customers based on demographics to analyze the genre prefernece and viewing behaviours of different customer groups. This will allow Miscrosoft to target certain customer groups for the movie production.

- **Awards analysis** - Dive into the Oscar-awarded movies to identify the key attributes of successful movies. 

## For More Information

See the full analysis in my [Jupyter Notebook](https://github.com/RuthyYao/Movie_Success_Analysis/blob/main/Data_Insights_for_New_Movie_Studio.ipynb) or review this [presentation](https://github.com/RuthyYao/Movie_Success_Analysis/blob/main/Data_Insights_for_New_Movie_Studio_presentation.pdf).

```

