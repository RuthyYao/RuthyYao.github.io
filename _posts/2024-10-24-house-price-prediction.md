---
layout: post
title: Develop a House Price Prediction Tool
image: "/house-price-predict/front__img.png"
tags: [Predictive Analysis, Regression, Python]
---

This project applies the linear regression analysis to build a house price prediction tool for the users of a residential property website. 

## Overview

The online real estate platform HomeConnect is looking to develop new functions and tools for its residential website so they can enhance the website user experience and increase the traffic. One idea is to create a housing valuation tool that allow users to self evaluate the houses they plan to buy or sell before they actually go to the market. They decided to use King County's property dataset to build a model as a trial. If the trial is successful, they will consider release it officially on the website. 

## Business Problem
HomeConnect's senior leadership team (SLT) highlighted three important things to consider for this house valuation model.  

* Reliability - The predicated house price from the model should explain as much as possible the variance with the actual sold price and minimize the prediction error. 
* Practicability - Users can easily input some housing price variables to work out the house value, i.e. the model shouldn't require the users to do any research in order to find out the value of the input.
* Insights - we should draw some insights from the model around what the high correlated features are with the house price so we can provide some value-add advices to the potentail home buyers and sellers.

The SLT doesn't quantify the model evaluation measurements. Hence, based on some researches, our data analytics team decide to use the following measures. For "Reliability", we use the adjusted R-squared - aiming for the model to have an adjusted R-squared of at least 60%. For the prediction error, we use root mean square error (RMSE). Based on the our research, we think an RMSE of \\$150k - \\$200k will be regarded as a good prediction.  Finally, For "Practicability", intuitively we think basic building parameters such as the property size, the number of bedrooms, etc should be the input variables. We will investigate the dataset to better define the input variables for the model. 

## Data and Methods

The predictive model is derived from King County's property dataset which contains over 21k pieces of data for houses sold between 2014 and 2015. The dataset provides the house selling price and a wide variety of characteristics, including the basic building features such as the land size, living area size, basement size, the number of bedrooms and bathrooms, etc. It also provides the location features - longitude, latitude and zipcode. Finally, the house condition and grade for construction quality are also in the dataset.  

The project used multilinear regression modelling to create a house valuation tool. The model is refined and evaluated through 4 iterations. In the iteration process, it applied train-test split to validate the model and used the "adjusted R-Squared" to evaluate the goodness of fit. To achieve the best fit for the prediction model, it uses the recursive feature elimination method to determine the optimal number of features. Finally, to accomodate reliability yet being practical, the model finds the trade-off between prediction accuracy and simplicity for users.  

## Results and Insights

The final model selected 8 variables across the construction and the location parameters, which explains 64% of the housing price with a prediction error of $185k.


![alt text](/img/house-price-predict/Final_Model.png)

The model also identified the the most correlated factors with the house price. 


![alt text](/img/house-price-predict/Feature_selected.png)

Some key inisghts are:

* Being waterfront can substaintially drive the house price up.
* Renovation can increase the house value.
* House price is more correlated with the size of the living area than the land size.
 

### Nest Steps
Additional dataset and further analysis will enhance the prediction of this tool and prepare it to be launched officially on HomeConnect's property website.

- **Categorize the houses into metro, regional and rural** - Houses in different regions display distinctive features. Adding a region parameter will help refine the model and reduce the prediction error.

- **Bring in the national geospatial data to the model** - we need to extend the geospatial dataset to the whole country for the tool to be officially published on the website.

- **Incorporate condos or apartment housing data** - - Adding different housing types will enrich the data and enhance the usability of the tool.

## For More Information

See the full analysis in my [Jupyter Notebook](https://github.com/RuthyYao/House_valuation_tool/blob/main/house_price_prediction_tool.ipynb) or review this [presentation](https://github.com/RuthyYao/House_valuation_tool/blob/main/house_price_prediction_tool_presentation.pdf).
