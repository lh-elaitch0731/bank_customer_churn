# BANK CUSTOMER CHURN PREDICTION #
------
![article](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/article-customerchurn1.jpg)

# Table of Contents #
- [Introduction](#introduction)
- [About Dataset](#about-dataset)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Preprocessing](#data-preprocessing)
- [Preparation for Training Model](#preparation-for-training-model)
- [Building Model](#building-model)
- [Model Evaluation](#model-evaluation)
  - [Evaluation](#evaluation)
  - [Feature Importances](#feature-importances)
- [Conclusion](#conclusion)

------

# Introduction #

Customer Churn prediction means knowing which customers are likely to leave or unsubscribe from your service. This is an important decision for many businesses, including banks.


**Why is it important?**
  - Obtaining new customers costs more than retaining existing ones.
  - It reduces revenues and profits.
  - It decreases chances to grow business.
  - ...

In this project, I am going to come up with some hypotheses and then buil classification model to predict customer churn. 

------

# About Dataset #

The dataset contains 10000 rows and 18 columns with information to predict customer churn.

- Personal Information (Name, Age, Geography, Gender, Estimated Salary)
- Status (Credit Score, Has Credit Card, Tenure, Balance, Number of Products)
- Satisfaction (Complain, Satisfaction Score)

Name of the dataset: Bank Customer Churn


Format: .csv


Source: Kaggle


Link: https://www.kaggle.com/datasets/radheshyamkollipara/bank-customer-churn 

------

# Exploratory Data Analysis #

## **Overview** ##

Overall, about 20% of the total customers leave a bank.

![overview](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/overview.png)

## Hypothesis 1: Would elderly customers tend to leave a bank than younger ones as they do not feel safe when depositing money there?

![age table](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/age%20table.png)

![age](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/age.png)

- Customers' ages range from 18 to 92 and are seperated into 4 groups.
- The chart shows that the 1st hypothesis is true when the elderly has the highest churn rate (44%).


## Hypothesis 2: Whether customers who lives in different country leave a bank since they find it hard to reach it? ##

![geography table](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/geography%20table.png)

![geography](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/geography.png)

- Customers come from 3 different countries in Europe: Spain, France and Germany.
- It is clearly seen that most customers leaving a bank are from Germany, about 32% which is two times higher than that of the others.

## Hypothesis 3: A customer who engages with a bank for a long time, he/she is likely to stay longer. ##

![tenure table](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/tenure%20table.png)

![tenure](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/tenure.png)

- Consider the tenure, there is no differences between them.
- However, a group of customers who stay for 6-8 years has the lowest churn rate (18%).

## Hypothesis 4: As customers buy/use many products at a bank, they do not tend to leave. ##

![numofproducts table](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/numofproducts%20table.png)

![numofproducts](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/numofproducts.png)

- The maximum number of products that a customer is likely to buy is 4.
- The output above shows that most customers buy 2 products, while the number of customers purchase 3 or 4 products is much lower. Thus, the exit rate in group of 3-4 products is higher than that of 1-2.
- However, customers who buy 4 products completely quit a bank (100%).


## Hypothesis 5: Customers who have low tier of card type, they are likely to leave. ##

![cardtype table](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/cardtype%20table.png)
![cardtype](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/cardtype.png)

- There are 4 types of card: SILVER, GOLD, PLATINUM and DIAMOND.
- The chart shows no matter how high the tier the card is, the customer still decide to leave.

## Hypothesis 6: Customers who earn higher points, they tend to stay longer. ##

![pointearned table](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/pointearned%20table.png)
![pointearned](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/pointearned.png)

- The points earned by customers range from 119 to 1000.
- The earned points do not effect on customer churn.


## Hypothesis 7: Are there any differences of churn rate between groups of customers when combining **Point Earned** and **Card Type**?

![cardpoint table](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/cardpoint%20table.png)
![cardpoint](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/cardpoint.png)

- A combination of Point Earned and Card Type shows noticeable gaps between groups.

## Hypothesis 8: Do satisfaction scores impact on churn rate? ##

![satisfactionscore table](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/satisfactionscore%20table.png)
![satisfaction](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/satisfaction.png)

- The lowest satisfaction score is 1, while the highest score is 5.
- The gap between satisfaction scores shows no differences.

## Hypothesis 9: Customers complain because they are not happy with a bank or they want to give feedback to expect a bank improves its service? ##

![complain table](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/complain.png)

- The number of customers who give positive feedback (about 8000) is nearly 4 times higher than that of the ones complain (just over 2000).
- However, a huge majority of customers making complaints decide to leave a bank (99%).

## Hypothesis 10: Is having a credit card a feature that retains customers? ##

![hascreditcard table](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/hascreditcard.png)

- The output above presents no differences of churn rate between customers have a credit card or not. 


## Hypothesis 11: Does balance have any effects on customer churn rate? ##

![balance table](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/balance%20table.png)
![balance](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/balance.png)

- Balance is ranged from 0 to 250080 and divided into 4 groups.
- However, the number of customers in a group of 0-73K is two times higher than that of others.
- It is obviously shown that customers who have lower balance would stay longer than whom have higher balance.
- About 26% of customer having balance about 110-134K leave a bank.

## Hypothesis 12: Do customers having low credit scores leave a bank? ##

![creditscore table](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/creditscore%20table.png)
![creditscore](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/creditscore.png)

- It seems that credit scores do not impact on the decision to leave of customers.

------
# Data Preprocessing #

## Replace Card Type
``` python
def replace_cardtype(df, col):
  '''
  This function is used for replacing a sorted column.

  Parameters:
  df: data frame
  col: a column that needs replacing values
  '''

  df[col] = df[col].replace({'SILVER':0, 'GOLD':1, 'PLATINUM':2, 'DIAMOND':3})

  return df
```

## One Hot Encoding
```python
def encode(df, col):
  '''
  This function is used for transforming categorical variables to numeric values.

  Parameters:
  df: data frame
  col: a column that needs encoding.
  '''

  df = pd.get_dummies(df, col)

  return df
```

## Scaling Data
```python
def scale_data(df, list_of_cols):
  '''
  This function is used for scaling data.

  Parameters:
  df: data frame
  list_of_cols: a list of columns that need scaling
  '''
  scaler = StandardScaler()
  df[list_of_cols] = scaler.fit_transform(df[list_of_cols])

  return df
```

## Imbalance Process
```python
def imbalance_process(df, label):
  X = df.drop(label, axis=1)
  y = df[label]
  smote = SMOTE(random_state=42)
  X_resample, y_resample = smote.fit_resample(X, y)

  return X_resample, y_resample
```
------

# Preparation for Training Model #

## Create a new data frame that contains relative features mentioned on the hypothesis above for modeling ##
```python
df_model = df.loc[:,['Age','Geography', 'Tenure', 'NumOfProducts', 'Card Type', 'Point Earned', 'Complain', 'Balance', 'Exited']]
```
## Apply def functions in a previous section to preprocess data ##

### Card Type ###
```python
df_model = replace_cardtype(df_model, 'Card Type')
```

### Geography ###
```python
df_model = encode(df_model, 'Geography')
```

### Scaling data ###
```python
cols_to_scale = ['Age', 'Tenure', 'NumOfProducts', 'Complain', 'Point Earned', 'Balance']
df_model = scale_data(df_model, cols_to_scale)
```

### Imbalance Process ###
```python
X_resample, y_resample = imbalance_process(df_model, 'Exited')
```

## Spliting Data ##
- y variable: 'Exited'
- X variables: other features in a df_model.

```python
X_train, X_test, y_train, y_test = split_data(df_model, 'Exited')
```

------

# Building Model #


```python
model = LogisticRegression(random_state=43)
model.fit(X_train, y_train)
```

------

# Model Evaluation #

## Evaluation ##

Metrics that is used to evaluate model:
- Accuracy
- Confusion Matrix

![evaluation](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/evaluation.png)

## Feature Importances ##

![feature importances](https://github.com/lh-elaitch0731/bank_customer_churn/blob/main/Visualization/feature%20importances.png)


------

# Conclusion #

- It can be seen that most customers who left were not satisfied with a bank as the feature "Complain" shows a strong impact.
- Most customers leave a bank are from Germany, the bank may not be located near this country to reach their customers.
- According to the EDA part, elderdy customers were likely to leave a bank, about 44.6% of a total exited elderdy . Perhaps they found it hard to use bank services such as internet banking. Or they may feel unsafe when they invest money in a bank.
- The top 4 effect is earned points. The data is opposite to the hypothesis that customers who earned high points (801-1000) would be likely to leave a bank than those having lower points. Perhaps they earned high points but they did not have any benefits from that, so they leave a bank.
- Balance of customers is also the relatively strong feature that effects churn rate. 
- Card Type shows no differences according to the chart in an EDA part. Thus, this feature stays at the bottom of a plot feature importances.
- The number of purchased products does not impact on an exit rates. As most exited customers left while they bought 4 products at bank. Whereas customers buying 2 products would stay longer.
- As it is observed, the gap between different tenure groups is not significant. However, customers who stayed at a bank for 6-8 years tended to leave a bank.
