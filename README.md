# Task-1

## Submitted By - Himanshu Tiwari

## Predict the percentage of marks of an student based on the number of study hours

## Linear Regression
In this task we will predict the percentage of the marks student will get based on the number of hours they studied. It is simple linear regression model as it has only independent variable is hours of study.

### Importing all the required libraries

import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
import matplotlib.pyplot as plt
%matplotlib inline

### Importing data from url

url = "http://bit.ly/w-data"
df = pd.read_csv(url)
print("sample of the data: ")
df.head(8)

print("Total num of entries =",len(df))

### Basic info of Data

df.info()

### Statistical Information of data

df.describe()

# Check for missing values
df.isna().sum()

### Data Preprocessing

### Plotting the values(Hours vs Score)

df.plot(x='Hours',y='Scores',style='o',figsize=(10,5))
plt.title("Hours vs Percentage")
plt.xlabel("Hours of Study")
plt.ylabel("Score in percentage")
plt.grid()
plt.show()

### Dividing the data into Attributes and Labels

X = df.iloc[:, :-1].values
Y = df.iloc[:, 1].values


print("Attributes: ",X)
print("Labels: ",Y)


### Splitting the data into train and test data

# We'll split the data using sklearn builtin function train_test_split
# As the dataset is too small dataset we'll devide the data in 80:20 percentage ratio
X_train, X_test, Y_train, Y_test = train_test_split(X, Y,test_size=0.2,random_state=0)

print(f"X_train has {len(X_train)} entries of shape {X_train.shape}")
print(f"X_test has {len(X_train)} entries of shape {X_test.shape}")

print("Y_train: ",Y_train.shape)
print("Y_test: ",Y_test.shape)


### Training the Model

### Fitting the regression model on X_train data

regressor = LinearRegression()
regressor.fit(X_train, Y_train)

### Plotting the regressor model

#First we'll write the equation for the line ie Y= mX+c for our model
line = (regressor.coef_*X)+regressor.intercept_

# regressor.coef_ and intercept_ are the parameters the model has learn't using training data



# Plotting the fitted line of the regressor
plt.scatter(X,Y,color='red')
plt.plot(X, line, color='blue')
plt.xlabel("Hourse of study")
plt.ylabel("Percentage Score")
plt.grid()
plt.show()

### Making predictions on test data and comparing with original values

predictions = regressor.predict(X_test)
print("Test Predictions are: ",predictions)

# Comparing the test predictions with original values
comapred_data = pd.DataFrame({"Original score":Y_test,"Predicted score":predictions})

comapred_data

# Checking the model accuracy
accuracy = regressor.score(X_test,Y_test)
print(f"Accuracy of the model is: {round(accuracy*100,2)} %")

new_values = [[8.00],[3.75],[7.45],[6.50],[5.25]]
new_predictions = regressor.predict(new_values)

new_predictions

# Printing the new instances of hours and there respective predicted values
new_data = pd.DataFrame({"Predicted score":new_predictions})
new_data

# Predicting the score for Hrs = 9.25
Hrs = 9.25
prediction = regressor.predict([[Hrs]])
print("Hours of study: ",Hrs)
print(f"Predicted score in % is: {round(prediction[0],2)} %")

### Evaluating different model using same data
### To see how different model will perform on same data we will evaluate performance of algorihtm. We will use two metrics : mean square error and mean absolute error

from sklearn import metrics

print("Mean Square Error: ",metrics.mean_squared_error(Y_test,predictions))
print("Root mean square error: ",metrics.mean_absolute_error(Y_test,predictions))

### Thank you !

### By - Himanshu Tiwari



