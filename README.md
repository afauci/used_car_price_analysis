# Used Car Data Analysis

## Overview
In this assignment, we used a dataset of used cars to help determine what car features have the most impact on the price of a used car. To do this, I created regression models with price as the target variable, and used cross validation and feature selection techniques to find the most influential features.

## Notebook link

## Process
1) Data understanding and preparation
- I looked at the data structure such as the columns available, their types, and counts of null values, to help determine what data needed to be cleaned or encoded. I also did some initial visualization of the data to understand the price distribution, identify outliers, and see things like manufacturer price ranges.
- I cleaned the data - I removed columns that would not be helpful (like VIN), or had too many null values to be useful (like size). I also removed rows that seemed like errors or anomolies - for example if the price was below $200 or above $500,000, or the odometer was above 500k (or negative)
- I encoded the data - many of the columns were categorical, which meant that they needed to be encoded in order to build regression models. I mostly used one-hot encoding, but for things like manufacturer with lots of different values, I did target encoding based on the mean price for each manufacturer. I also dropped some columns like state, region, and model where there were so many different values
- I scaled the numerical values to help normalize the data and ensure that the large numbers (like odometer) did not have outsized impact on the model
- I split the data into the training and test sets, so that when we did the modeling we could do analysis
- At the end of this process, I had X rows and Y columns that 

2) Modeling and evaluation
- I used 3 regression models that we learned about in class to do the analsysis - linear, Lasso, and Ridge
- For each model, I did evaluation using mean squared error, mean absolute error, root mean squared error, and R^2
- I tried multiple cross validation techniques, including K-Fold with 5 folds, and GridSearch on both the Lasso and Ridge models to tune the hyperparameters and get coefficients that could be used for feature selection

3) Feature selection
- I tried multiple feature selection techniques, and compared them to get the best understanding of the features that had a big impact on the price
- I used Grid Search on Lasso and Ridge regression, and used the coefficients that it found to determine feature importance. Higher coefficient absolute values mean more important features, where negative coefficients mean a negative correlation with price.
- I also ran permutation importance using the Ridge model to find the feautres that were most important using that approach 

## Findings
- After the analysis above, I found that the most important features across all 3 of the feature selection techniques (Ridge Grid Search, Lasso Grid Search, and permutation importance) were:
	- Odometer: there is a strong negative correlation between the odometer value and car price, meaning higher mileage cars were sold for lower prices
	- Fuel type: we did encoding off of the mode fuel type (gas), so the coefficients for fuel type were in relation to the gas fuel type. Based on this, iesel cars were sold for significantly higher prices than gas cars. There was a positive correlation between price and hybrid or electric as compared to the gas cars.
	- Year: we converted the year to vehicle age of the car so it was easier to analyze. Newer years (lower vehicle age), were associated with higher prices
	- Manufacturer: in order to do the analysis for manufacturers, we did target encoding to replace the manufacturer with the mean car price for that manufacturer so it was a numerical column. This means that a high coefficient value indicates that there is a strong correlation between manufacturer and price, even when other price lowering factors are present
	- Drive: for one hot encoding, we used the mode (all wheel drive) as the reference. Compared to all wheel drive, rear wheel drive was associated with a slightly lower price, and front wheel drive was even lower.
- Based on this information, the car dealership should focus on building out inventory for cars with:
	- Lower mileage
	- Fuel type diesel if available (though this is not very common in standard cars, so may not be worth optimizing for)
	- Newer year
	- Manufacturers like Ram, GMC, Lexus, and Mercedes Benz, though they shoudl consider diversifying thier inventory to include some lower tier brands like Honda and Nissan, espcially if mileage and vehicle age are low
	- All wheel drive cars


