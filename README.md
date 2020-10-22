# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)

# Project 2 - Ames Housing Data Analysis



### Problem Statement

The aim of this project is to use linear model to best predict the price of houses in Ames at sale. The linear models that will be used are Linear Regression, LASSO, Ridge and Elastic Net. Therefore, my problem statement would be which linear model best predict the price of houses in Ames at sale and which features are the best predictors of housing price?

The success of a model will be measured using R-square on unseen data and the RMSE score given by Kaggle.The scope of the project is confined to the Ames dataset and linear models only. The model will be tuned closely to the Ames dataset and some features in the dataset are vey specific to Ames. Therefore, the model may not be a perfect fit for other housing data in the U.S.

This project is relevant to primary stakeholders: Developers, Home Sellers, Home Buyers and Housing Agents. The secondary stakeholder is the city coucil. Developers, home sellers and housing agents can use the model developed to understand which are the features that influence sale price. During design and marketing, developers, home sellers and agents could focus on the identified features to maximise sale price. As for home buyers, the model can be used to estimate the actual price of a house so buyers can give an appropriate offer to seller to increase the chances of securing their desired property. The city council can use the model for city planning, for example allowing what type of houses to be built and how much land to be release to developer.



## Executive Summary

### Contents:

- [1. Importing the Libraries](#1.-Importing-the-Libraries)
- [2. Importing Datasets](#2.-Importing-Datasets)
- [3. Inspection of Training and Test Dataset](#3.-Inspection-of-Training-and-Test-Dataset)
- [4. Data Cleaning](#4.-Data-Cleaning)
- [5. Pre-processing](#5.-Pre-processing)
- [6. Explortary Data Analysis (EDA)](#6.-Explortary-Data-Analysis-(EDA))
- [7. Create Feature Matrix and Target](#7.-Create-Feature-Matrix-and-Target)
- [8. Model Selection](#8.-Model-Selection)
- [9. Output Model Predictions](#9.-Output-Model-Predictions)
- [10. Business Recommendations](#10.-Business-Recommendations)
- [11. Future Steps](#11.-Future-Steps)

### Data Cleaning

1. All categorical entries were converted to lower case
2. Categorical null cells were replaced with 'na'
3. Integer or Ratio null cells were replace with 0
4. Columns that have few missing data were replaced with the mean
5. All ordinal variable were encoded using integer 


### Data Dictionary:
The original data dictionary may be used. It is found here: http://jse.amstat.org/v19n3/decock/DataDocumentation.txt

There were 3 featured engineered variables:

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**Total SF**|*float*|df_train/df_test|Total living area, include both above ground and basement.| 
|**Total Baths**|*float*|df_train/df_test|Total number of bathrooms, include both above ground and basement bathrooms.|
|**Age of Built**|*int*|df_train/df_test|Age of building, using year sold minus year built.|



### EDA

- These are the variable that has strong to mid positive correlation to Sale Price: 
1. Overall Qual (0.800207):There seems to be strong positive correlation between overall quality material and finish of the house. The better the quality the higher the sale price.

2. Exter Qual (0.712146): There seems to be a positive correlation between sale price and external quality. 5 is excellent quality of the material on the exterior, 4 is good, 3 is avarage. According to the boxplot, the better the qulity of exterior material, the higher the sale price.

3. Gr Liv Area (0.697038): There is a strong positive correlation between sale price and above grade living area square feet. The bigger the living area, the higher the sale price. There seems to be 6 outliers that does not follow the trend, it warrants further investigation. The first two outliers are extremely large houses bigger than 4000 sq feet but the sale price is very low. THe next 4 outliers are large houses around 3000 sq feet but the sale price are below the trend. 


4. Kitchen Qual (0.692336): There is a positive correlative between kitchen quality and sale price. The better the kitchen quality the higher the sale price. 


5. Garage Area (0.650246): Garage that can contain 3 cars has the highest sale price. The median sale price is 297K, Q1 at 250K and Q3 at 369K. The spread is big as well.


6. Garage Cars (0.648128): Garage that can contain 3 cars has the highest sale price. The median sale price is 297K, Q1 at 250K and Q3 at 369K. The spread is big as well.
    
    
7. Total Bsmt SF (0.628668): There seem to be a positive correlation between total square feet of basement area and sale price. The bigger the basement, the higher the sale price. There seems to be two outliers that warrant further investigation.


8. 1st Flr SF (0.618486): There seem to be a positive correaltion between first floor square feet and sale price. The bigger the first floor square feet, the higher the sale price. There seems to be three outliers.


9. Bsmt Qual (0.612188):There seems to be a positive correlation between the hight of the basement and sale price. The higher the height of the basement, the higher the sale price. Basement hight above 100 inches fetches higher sale price. The median sale price is at 319.9K, Q3 at 385K and Q1 at 272K. 



### Model Selection

Linear Regression: r2 score = -36852813 RMSE = 459252881.9 
The mean R^2 is extremely negative for linear regression. All the R^2 scores are negative in crossvalidation. The linear regression is performing far worse on the test sets. It is probably dramatically overfitting and the redundant variables are affecting the coefficients in weird ways.

Elastic Net: r2 score = 0.924 RMSE = 20869.808
Ridge: r2 score = 0.919 RMSE = 21490 (I have picked ridge as the baseline model)
Lasso: r2 score = 0.924 RMSE = 20861.12

The high r2 score means that the model is able to explain over 90% of sale price variation.

## Conclusion and Recommendations

The recommendation will be based on Lasso model and inferential statistics. The recommendations will be relevant to the following stakeholders: home buyers, housing agent, developers and home sellers. Recommendations will be given in 4 broad categories, they are: living space, quality of house, location and age of building. (Note: I will use only the top 10 coefficients, including too many variables might overwhelm stakeholders besides that these coefficients are most relevant based on domin knowledge.) 

### The first category is living space. Based on the lasso model, the following coefficients related to living space are significant: 

    - Gr Liv Area = Above (ground) living area square feet (A one unit change in above ground living area, the sale price will increase by 29.7 dollar, holding others constant)

    - Total SF = Total area both above ground and below ground square feet (A one unit change in total area, the sale price will increase by 19.5 dollar, holding others constant.)

    - Mas Vnr Area = Masonry veneer area in square feet (A one unit change in mansory veneer area, the sale price will increase by 33.9 dollar, holding others constant.)

    - Total Bsmt SF = Total square feet of basement area (A one unit change in total basement area, the sale price will increase by 12.6 dollar, holding others constant.)

    - Garage Area = Size of garage in square feet (A one unit change in garage area, the sale price will increase by 23.4 dollar, holding others contant.)

#### Implications for stakeholders

- Home Buyers
    - Home buyers can use living space to estimate the actual price of the house. Normally, sellers or agents will post a higher price on property portals to fetch the highest selling price. Home buyers can have a rough estimate of the actual price by assessing the above ground living area, total living area. As such, home buyers can give an appropriate offer to the seller so as to enhance the opportunity of securing the property. 
    - Home buyers needs to know, living area, total basement area and garage area are strongly positive correlated to sale price. When home buyers are thinking of buying large living area, big basement and garage that can park many cars, buyers will have to prepare to pay more and give a higher offer. Generally buyers on a tight budget should avoid looking for big houses however there can be outliers (as seen in the data). 
    
- Home sellers, devleopers, housing agent (I will call them sellers in general)
    - Sellers, developers and agents when marketing their property, they should leverage on living area to achieve a better bargain. Living area should include basement area and garage area as they have an impact on selling price. 
    - Sellers will also need to highlight the masnory veneer area as well to boost sale price. Sellers need to know, these areas are positively correlated to sale price. Meaning, the bigger the area, the higher the sale price. Therefore, small houses should not be asking for a high sale price otherwise no buyer would buy. 
    - Developers, when there is a limit on how big the house can be built above ground, developers should also be mindful to maximise space in the basement to fetch a higher selling price.  
  
### The second category is the Quality of house. Based on lasso model, the following coefficients related to quality of house are signficant:

    - Overall Qual = Rates the overall material and finish of the house (A one unit increase in overall material, the sale price will increase by 8862 dollar, holding others constant.)

    - Exter Qual = Evaluates the quality of the material on the exterior (A one unit increase in exterior quality, the sale price will increase by 9549 dollar, holding others constant.)
    
#### Implications for stakeholders
- Home Buyers
    - Before buying a property, buyers should assess the overall material finish of the house. Houses that have execellent material finish tends to have a higher sale price as the two variables are positively correlated. Therefore, buyers need to give a higher offer to house that has a better material finish (holding other variables constant) so as to increase the probability of the offer being accepted. 
    
- Home sellers, devleopers, housing agent (I will call them sellers in general)
    - Sellers could highlight the material quality of the house during marketing. For developers, in order to sell the house at a premium, the developer can use quality materials and ensure good worksmanship.
    - Sellers could renovate their house or at the least renovate the exterior to boost sale price. 

### The third category is Location. Based on lasso model, Northridge Heights was found to be significant. 

    - If the property is a Northridge Heights, the sale price will increase by 33746 dollar, holding other variables constant.  
    
- Based on the lasso model, houses at Northridge Heights (NH) tend to have a higher sale price. Based on outside research, the NH population is highly educated, 74% of the population has an associate degree or higher. Secondly, NH also has a very high median income 105,583 usd which is much higher than the national average of 33,706 usd. Besides that, NH houses also tends to have high rental yield, its rental yield is comparable to large cities such as Indianapolis. NH also enforce strict smoking ban in workplace, bars and restaurants which make the environment more livable. Lastly, the crime rate at NH is generally low compare to national average. These could the reasons for NH houses having a higher sale price.  

#### Implications for stakeholders
- Home Buyers
    - Home buyers needs to prepare to pay higher price for houses in NH, in exchange for a comfortable living environment.
    
- Home sellers, devleopers, housing agent (I will call them sellers in general)
    - Sellers can leverage on NH's good living environment to maximise sale price. Sellers can highlight high rental yield, low crime rate and convenience of the neighborhood.
    - Developers can consider bidding for land at NH, higher sale price could translate to higher profit (assuming cost is constant)
    

### The fourth category is Age of building. Based on lasso model, the following coefficients related to age of building are significant: 

    - Sale Type New = Home just constructed and sold (If it is new home, the sale price would increase by 16513 dollar, holding other variables constant.)

    - Year Built (A one unit increase in year built i.e the house is younger, the sale price would increase by 186 dollar, holding other variables constant.)
 
#### Implications for stakeholders
- Home Buyers
    - Buyers need to prepare to pay higher price for new houses. Perhaps, new houses has lesser defects, does not require repairs. Buyers also can renovate the house to his/her liking.
    
- Home sellers, devleopers, housing agent (I will call them sellers in general)
    - It is good news for developers, the positive correlation between age of of building and sale price means that Ames is a city worth investing in for developers. The high sale price means there is demand for new buildings. 
    - Developers and agents could highlight the young age of the building in their marketing effort. It could also highlight the new amenities that come along with the new building. 
    
## Future Steps
- In the future, demographic data could be included so data scientist can examine who is willing to pay higher price, popular location, buyers are willing to pay for what kind of features. This woud provide an overall picture to data scientist and stakeholders.
- Moving on, during data collection, measures need to be taken to deal with missing data. For example, making certain features compulsory to answer and making sure the entry make sense. This would make analysis more accurate.  
    
