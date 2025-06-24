# Zomato Data Analysis project using Python
![Zomato](https://github.com/Mahadevkempe/Python_projects/blob/main/Zomato%20Data%20Analysis/Zomato_logo.png)

# Problem_statement:
Zomato has an average of 17.5 million monthly transacting customers for its food delivery business.e average monthly active food delivery restaurant partners on Zomato's platform have also increased by 8.7% year-on-year, from 208,000 to 226,000​.You are working in a data-driven role at Zomato. You have a dataset of customers. As a data professional, you need to analyze the data, perform EDA (Exploratory Data Analysis) and visualization, and answer the following questions:

# Project Overview: 
This project aims to perform an in-depth analysis of Zomato's food delivery business using Python. By leveraging Python libraries for data manipulation, analysis, and visualization, we will explore customer and restaurant data to derive actionable insights.The dataset includes information on customer orders, restaurant partnerships, and other key performance metrics. Through Exploratory Data Analysis (EDA), we will visualize trends, identify patterns, and make data-driven recommendations to enhance Zomato's business operations 

# Business Objectives:
1.Customer Behavior Analysis
    - Understand customer ordering patterns and preferences.
    - Identify high-value customers and suggest retention strategies.
    - Analyze the frequency and volume of customer transactions.

2.Restaurant Partner Evaluation
  - Assess the performance of restaurant partners using metrics like order volume, ratings, and delivery times.
  - Identify top-performing restaurants and suggest partnership opportunities.
  - Evaluate the impact of the 8.7% growth in restaurant partners.

3.Market and Growth Insights
  - Analyze month-on-month and year-on-year growth in transactions.
  - Identify regions with the highest customer activity.
  - Determine factors driving customer satisfaction and restaurant success.

4.Operational Insights
  - Evaluate delivery times and analyze patterns in delays.
  - Identify factors contributing to customer complaints or order cancellations.
  - Recommend operational improvements to enhance efficiency.

5.Visualization and Reporting
  - Develop interactive visualizations using Matplotlib and Seaborn.
  - Create reports to present findings to stakeholders.

# Zomato Data Analysis.

# Step 1: Import necessary python libraries.
    import pandas as pd
    import numpy as np 
    import matplotlib.pyplot as plt
    import seaborn as sns

# Step 2: Create the data frame(df).
    df = pd.read_csv("Zomato data .csv")
    print(df.head())

# Step 3: Let's convert the data type of the "rate" column to float and remove the denominator. 
    def handleRate(value):
        value = str(value).split('/')
        value = value[0];
        return float(value)

    df['rate'] =df['rate'].apply(handleRate)
    print(df.head())
    
# Step 4: Summary of the dataframe(df).
    df.isnull().sum()
    df.info() 

# Business_problem solutions.
# 1) What type of restaurant do the majority of customers order from?
    sns.countplot(x=df["listed_in(type)"],color="orange")
    plt.xlabel("Type of Restaurant") 

# 2. How many votes has each type of restaurant received from customers? 
    result = df.groupby('listed_in(type)')['votes'].sum()
    plt.plot(result, color ="green",marker= "o")
    plt.xlabel("Type of Restaurant", color = "Red",size =30) 
    plt.ylabel("Votes",color = "Red",size=20)
    plt.show()

# 3. What are the ratings that the majority of restaurants have received? 
    plt.hist(df['rate'],color="skyblue" ,bins=5)
    plt.title('Rating Distribution')
    plt.show() 

# 4. Zomato has observed that most couples order most of their food online. What is their average spending on each order?
    couple_data = df['approx_cost(for two people)']
    plt.figure(figsize=(10,6))
    sns.countplot(x=couple_data,color= "Green") 
    plt.show() 

# 5. Which mode (online or offline) has received the maximum rating? 
    plt.figure(figsize=(6,6))
    sns.boxplot(x="online_order", y="rate", data=df, palette={"Yes": "orange", "No": "skyblue"})
    plt.xlabel("Online Order")
    plt.ylabel("Rating")
    plt.title("Online Order vs Rating")
    plt.show() 

# 6. Which type of restaurant received more offline orders, so that Zomato can provide those customers with some good offers? 
    #Convert 'rate' to Numeric:
    df['rate'] = pd.to_numeric(df['rate'], errors='coerce')

    #Handle Missing Values:
    df['rate'].fillna(df['rate'].mean(), inplace=True)

    #Drop Remaining Null Values:
    df = df.dropna(subset=['rate']) 

    #Create a Pivot Table and  Visualize with a Heatmap:
    pivot_table = df.pivot_table(index='listed_in(type)', columns='online_order', values='rate', aggfunc='mean')
    plt.figure(figsize=(10, 8))
    sns.heatmap(pivot_table, annot=True, cmap='coolwarm', fmt=".2f")
    plt.title("Average Rating by Type and Online Order Availability")
    plt.xlabel("Online Order")
    plt.ylabel("Type of Restaurant")
    plt.show()
    

 

