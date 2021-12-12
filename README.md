# King County Sale Price Predictions

Morgan Didjurgis
Flex 40 Weeks
Instructor: Abhineet Kulkarni

## Project Overview

This project uses King County sales data from 2014-2015 to build a regression model that predicts sales prices for single-family home buyers based on property features. 

### Business Problem

Single Family home buyers can benefit from tools to help them evaluate how much more or less different features/locations should cost.  This can help them narrow down homes to visit and also determine if a list price is reasonable before making an offer.

### The Data

The data set used to fit the model is a list of ~18,000 properties sold in King County in 2014-2015 with accompanying prices and characteristics. The description of the column names can be found in 'column_names.md' in the data folder in this repo.

Most single family home buyers work with agents if they are not already very familiar with real estate.  Therefore, while I did aim to only include features  that the home buyer would care about, there are some features which improve accuracy that an agent may assist the home buyer in selecting or that an application might provide suggestions for based on averages in that city.

Throughout the process of model development, one must consider the tradeoff between ability to interpret the model and determine which features affect price most and the accuracy of the price prediction.  While it is useful to tell a buyer which features or locations are 'most expensive', it is often easier for actually see price predictions based on combinations of features.  I will prioritize the ability for a buyer to 'play' with different features and see predictions rather than having to compare 'impact' of those features. For this audience, actual price predictions are easier to comprehend and more user friendly.

## Features

Features used in this model are below. Starred features were engineered.

- waterfront
- yr_built
- renovated*
- basement*
- city
- bedrooms
- bathrooms
- sqft_living
- sqft_lot
- floors
- grade (King County grading system on quality of construction)

## Model

A polynomial regression model was used with the features above. R-squared of the model is ~.81, meaning it explains approximately 81% of the variance in price. 

Log transformations were performed on price, bedrooms, bathrooms, sqft_living, sqft_lot, floors, and grade to increase normality and the linear relationships with price.

Three models were considered. One used no interactions, the second used two interactions that slightly increased r2, and the third was the polynomial model. All models had good fit and performed well when test data was used to make predictions.

***

**Justification for Selection of Polynomial Model**

The quadratic polynomial model has the highest r-squared and does not appear to be overfit as the test data has a similar r-squared. However, it is extremely difficult to interpret.  

But- the model with no interactions is almost equally difficult to interpret due to high multicollinearity of many features.  We can use the coefficients to examine the impact of cities, waterfront, and basement but not other features that single family homebuyers are generally interested in like bedrooms, bathrooms, and sqft.

If the overall goal of this model is prediction, then the polynomial interaction model should be used.  Ideally, home buyers would be able to input features they are interested in on an app and the model would predict price.  They are more likely to get meaningful information from these predictions by changing features than if we were to provide specific information about how much price increases by selecting certain cities or changing features by a %.  The predicted prices are more understandable for the audience and are more helpful when determining if a house is properly priced.  I will provide a sample of different inputs a home-buyer may use while considering their options.

***

## Example Home Buyer

Below is a series of predictions that a home buyer might like to see while searching for a home. The other way this can be used is to validate whether a list price is reasonable before making an offer.

Assume the buyer is looking for a house in Redmond with at least 3 bedrooms, 2 bathrooms, and 1500 sqft of living area.

The hardest inputs for the buyer are sqft_lot and grade. As stated, these can be recommended by an agent or an app could suggest average values for the Redmond area.  In Redmond, average grade is 8.0 and average sqft_lot is 8645. Therefore we will recommend these values for inputs if the buyer does not have a specific value in mind. For use validating list prices, these inputs would be readily available.

*First Price Prediction*

- Not on waterfront
- Year: 2000
- Not renovated
- No basement
- City: Redmond
- Bedrooms: 3
- Bathrooms: 2
- Sqft Living: 1500
- Sqft Lot: 8645
- Floors: 1
- Grade: 8

Predicted Price: **$463,509**
***
*Second Price Prediction*

- Add a half bath

Predicted Price: **$515,362**
***
*Third Price Prediction*

-Add 500sqft to living space

Predicted Price: **$598,969**
***
*Fourth Price Prediction*

-Property that is 10yrs newer

Predicted Price: **$606,408**
***
*Fifth Price Prediction*

-Add second floor

Predicted Price: **$580,740**
It appears the a second floor in this area is not more expensive.


## Conclusions

The model produced in this project explains over 80% of variance in price using features input by a home-buyer.  

The model uses polynomial regression and log transformation of certain features.  Focus was placed on increasing accuracy of the model, prioritizing it over the ability to provide insights on specific impact of each feature.  This choice was made with the single-family home-buyer in mind, who would more easily interpret a predicted price than information on impact of individual features.


## Next Steps

- Create an app where buyers can input desired features and receive predicted price.
- App can provide suggested inputs based on city averages if the buyer is not familiar with the types of houses found in that area
- App can plot any houses on market or recently sold with similar characteristics
***
- Use another type of model to take inputs including price and return city most likely to find property in
- App would plot heatmap showing likelihood of finding property at the price with those characteristics
