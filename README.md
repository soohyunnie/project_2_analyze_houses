# King County House Analyzation 
![image](https://user-images.githubusercontent.com/40476299/131032705-5e45b81a-2ccc-45f2-9fa5-3b596b8c9c61.png)
## Overview
Homeowners in King County are looking to sell their houses. We will advise them which features to focus on to increase their price of the houses before selling them. <br>
## Data 
<img width="1098" alt="Screen Shot 2021-08-26 at 4 47 11 PM" src="https://user-images.githubusercontent.com/40476299/131033871-58c0eab8-c292-4c97-9988-7aee0f943d12.png">
We split our data to training data and test data <br>

## Model 1 

<img width="1087" alt="Screen Shot 2021-08-26 at 4 51 19 PM" src="https://user-images.githubusercontent.com/40476299/131034327-ff03038c-0d79-429a-832c-0b40822d7e6b.png">
From our heatmap you can see that sqft_living is our most correlated feature so we will be using that as our baseline model
<img width="562" alt="Screen Shot 2021-08-26 at 4 53 52 PM" src="https://user-images.githubusercontent.com/40476299/131034605-0ac8a37e-8bdf-4940-853d-d1a1ec05e2c8.png">


Train score:      0.43809827960116837 <br>
Validation score: 0.45174690732988537 <br>
We did linear regression on our baseline model and it showed that our r-squared value is 0.45. <br>
From here will be trying to make our model better.

## Model 2
We are going to check correlation between our features. <br>
<img width="254" alt="Screen Shot 2021-08-26 at 4 58 17 PM" src="https://user-images.githubusercontent.com/40476299/131035095-7225bb7e-bd51-4ced-a2a1-0d8527e03dbb.png"> <br>

Since two different pairs of variables are highly correlated, the correct approach would be to one variable from the pairs.
We can remove sqft_above since sqft_above is square footage of house apart from basement which is similar to sqft_living.
We can remove sqft_living15 since the square footage of interior housing living space for the nearest 15 neighbors is more import than sqft_living.
<br>
Next we do linear regression on our new model after dropping sqft_above and sqft_living15

Current Model<br>
Train score:      0.4981829009126592<br>
Validation score: 0.5114025797081387<br>

Baseline Model<br>
Train score:      0.43809827960116837<br>
Validation score: 0.45174690732988537 <br>

Train MAE: 136179.34082309518
<br>
Test MAE: 138396.76954310565 <br>

Train MSE: 33221795088.586315<br>
Test MSE: 34866130880.95273 <br>

Train RMSE: 182268.46981468383<br>
Test RMSE: 186724.74630041068 <br>

Train R-Squared: 0.5016419840665775<br>
Test R-Squared: 0.49117228087784925<br>

By removing the two highly correlated features, we imporved our model by approximately 6%. Our model is approximately $136K-$183K away from the actual price.

## Model 3 
From our second model, we are going look at the p-values to drop insignificant features and see if our model improved. <br>
<img width="535" alt="Screen Shot 2021-08-26 at 5 04 43 PM" src="https://user-images.githubusercontent.com/40476299/131035832-f5ccb9ef-bb96-4218-8e85-4407000d213d.png"> <br>
From the model summary, we found that sqft_lot and sqft_basement are insignificant. <br>

Current Model<br>
Train score:      0.49815556646083703<br>
Validation score: 0.5115248055310088<br>

Second Model<br>
Train score:      0.4981829009126592<br>
Validation score: 0.5114025797081387<br>

Baseline Model<br>
Train score:      0.43809827960116837<br>
Validation score: 0.45174690732988537<br>
We did slightly better than our previous model by 0.01%.<br>
## Final Model 
We did OneHotEncoder on the condition feature and StandardScaler on our on bedrooms, bathrooms, sqft_living, floors, sqft_lot15, and age
With the scaled data we got :

Train R-Squared: 0.502068837511837 <br>
Test R-Squared: 0.49181607104147496<br>

Train MAE: 136059.45005219206<br>
Test MAE: 138261.48143750036<br>

Train MSE: 33193339967.49289<br>
Test MSE: 34822016790.34547<br>

Train RMSE: 182190.394827754<br>
Test RMSE: 186606.58292339384<br><br>
<br>
We can see that our current model's r-squared increased by 0.004%. If we compare with our baseline model, r-squared increased by 0.06. It also seems like the model didn't increase our mean absolute error and root mean squared error.
<br>
Our model is approximately $136K - $186K away from the actual price.<br><br>
We should check the coefficant of the features to see which features are highly impactful: <br><br>
<img width="337" alt="Screen Shot 2021-08-26 at 5 11 35 PM" src="https://user-images.githubusercontent.com/40476299/131036654-726d91e9-7e18-4337-8b7c-75e24c084678.png">
<br><br>
For the top two best features, we chose sqft_living and bathroom. We decided not to choose age because the homeowners cannot change the age of the house. We also didn't choose the condition because some repairments do not increase the value of the house. So, you can spend money but the homeowners may not get the same/higher values back.
<br><br>
We see that sqft_living has the highest coefficient. This means that price increase by approximately \$186,780 for 1 standard deviation of the sqft_living.
<br>
We can also see that price increase approximately $32,503 for 1 standard deviation of the bathroom.
<br>
Let's see the visual for number of bedrooms and price.<br>
<img width="952" alt="Screen Shot 2021-08-26 at 5 16 34 PM" src="https://user-images.githubusercontent.com/40476299/131037237-0fa1394a-902b-4101-84bf-2b65c2fc5a4b.png">
This graph shows the increase of price as the number of bathroom increases. 
## Checking for Assumptions
#### Investigating Linearity

<img width="442" alt="Screen Shot 2021-08-26 at 5 18 21 PM" src="https://user-images.githubusercontent.com/40476299/131037404-63ebdb63-272f-4f20-b9da-3385b431dea7.png">
<br>
Although our some of our data is spread out, most of our data follows the best fit line. So our model does not violate the linear assumption.
<br>

#### Investigating Normality
<br>
<img width="462" alt="Screen Shot 2021-08-26 at 5 19 19 PM" src="https://user-images.githubusercontent.com/40476299/131037523-63f5b6dd-e4ca-4de2-a4b3-a649c9f172dc.png">
<br>
From the graph above, we can see that our data are mostly normalized. We see some outliers on the right side. Since majority of our residuals lie within the line, our model does not violate the normality assumption.
<br>

#### Investigating Multicollinearity
<br>
<img width="270" alt="Screen Shot 2021-08-26 at 5 20 25 PM" src="https://user-images.githubusercontent.com/40476299/131037645-c0601777-8a6b-4c40-9a92-66981316f55b.png">
<br>
From our data above, both our bathrooms and sqft_living are below 5. Thus, our model's features are not highly correlated with each other.
<br>

#### Investigating Homosecdascity
<br>
<img width="448" alt="Screen Shot 2021-08-26 at 5 21 24 PM" src="https://user-images.githubusercontent.com/40476299/131037730-5e996918-8c5b-4114-85ac-3f72ef487483.png">
<br>
From the graph above, we can see a funel-like shape. This means that we violated the homoscedasticity assumption and our model is heteroscedasticity, which means that the price is unequal across the range of values of the predictors.
<br>

# Conclusion
<br>
In conclusion, our model explains 49% of variation of the data. For every 1 standard deviation of sqft_living, the price of the house increase by $186,780. For every 1 standard deviation of bathroom, the price of the house increase by $32,503. Our model is approximately $136K - $186K away from the actual price.
<br><br>
Our recommendations would be to add a bathroom to increase the price of the house. If the house does not have enough space to add extra sqft_living, adding a bathroom will increase the price of the house.
