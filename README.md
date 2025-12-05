# Food-Panda-Data-Analysis
Analysis of Food Panda Dataset using Python

📊 **FoodPanda Data Analysis**
This project analyzes FoodPanda delivery and order data to uncover trends, customer behavior insights, delivery performance, and operational patterns. Using Python-based data analysis techniques, the project provides actionable insights through exploratory data analysis (EDA), visualization, and reporting.

🚀 **Project Overview**
The goal of this analysis is to understand how FoodPanda operations behave over time and identify factors impacting order volume, customer retention, restaurant performance, and delivery efficiency.
This project includes:
Cleaning and preprocessing FoodPanda order data
Exploratory Data Analysis (EDA)
Visualizations of key trends
Insights on customer behavior and ordering patterns
Delivery partner performance analysis
Restaurant performance analytics
Data-driven recommendations

📂 **Dataset Description**

The dataset contains FoodPanda order logs with the following common fields:
- Order ID – Unique order identifier
- Customer ID – Unique customer reference
- Restaurant Name
- Dish Name
- Last Order Date
- Delivery Stattus
- Category
- Quantity
- Payment Method
- City

🗂️**Data Source**
- Primary Source: Food Panda Analysis Dataset <a href = "https://github.com/prasadmahajan06/Food-Panda-Data-Analysis/blob/main/Foodpanda%20Analysis%20Dataset.csv">Download Dataset Here</a>

🧰 **Tech Stack**
This project uses:
- Python 3.x
- Pandas – Data cleaning and manipulation
- NumPy – Numerical analysis
- Matplotlib & Seaborn – Data visualizations
- Plotly (optional) – Interactive graphs
- Jupyter Notebook – Analysis environment

🛠 **Features & Analysis Performed**
✔ *Data Cleaning*
- Handling missing values
- Removing duplicates
- Fixing incorrect data types
- Filtering cancelled / invalid orders

✔ *Exploratory Data Analysis*
- Total orders, revenue, and customer distribution
- Most popular cuisines and restaurants
- Peak ordering hours & days
- Repeat vs. new customer patterns

✔ *Delivery Analysis*
- Average delivery time
- Fastest & slowest zones
- Factors affecting delivery delays
- Delivery partner performance

✔ *Financial & Operational Insights*
- Revenue trends
- High-value vs low-value customers
- Restaurant efficiency
- Cancellation reasons analysis

✔ Visualizations
- Bar charts, line charts, heatmaps, histograms
- Customer order frequency graphs
- Time-based order trends

⭐ ***Sample Data Analysis Code***
### Mounting Google Drive in Colab
from google.colab import drive

drive.mount('/content/drive')

### Storing the file path in variable named dataset
dataset = '/content/drive/MyDrive/Foodpanda Analysis Dataset.csv'

### Importing Required Modules/Libraries
import pandas as pd

import numpy as np

import matplotlib.pyplot as plt

import seaborn as sns

### Reading csv file
df_fpanda = pd.read_csv(dataset)

### Summary of Dataset
df_fpanda.info()

### Few Sample of Dataset
df_fpanda.head()

### Gender Distribution
gender_dist = df_fpanda['gender'].value_counts()

plt.pie(gender_dist, labels=gender_dist.index, autopct='%1.1f%%', startangle = 90)

plt.title('Gender Distribution')

plt.show()

### Age Distribution
age_dist = df_fpanda['age'].value_counts()

plt.bar(age_dist.index, age_dist.values)

plt.title('Age Distribution')

plt.xlabel('Age')

plt.ylabel('Count')

plt.show()

### Top Cities by Order
top_cities = df_fpanda['city'].value_counts().head()

plt.barh(top_cities.index, top_cities.values)

plt.title('Top Cities by Order')

plt.xlabel('Order count')

plt.ylable('Cities')

### Total Order Placed
total_orders = df_fpanda['order_id'].count()

print("Total Orders Placed-",total_orders)

### Total orders per Restaurants by cities
restaurants = df_fpanda.groupby(['city', 'restaurant_name'])['order_id'].count().reset_index()
#### Pivot table for stacked bar chart
pivot = restaurants.pivot(index='city', columns='restaurant_name', values='order_id')

pivot.fillna(0, inplace=True)
#### Plot
pivot.plot(kind='bar', stacked=True, figsize=(12,6))

plt.title('Total Orders per Restaurant by City')

plt.xlabel('Cities')

plt.ylabel('No. of Orders')

plt.legend(title='Restaurant', loc='upper right', bbox_to_anchor=(1.2, 1))

plt.show()

### unique restaurants per city
restaurants = df_fpanda.groupby('city')['restaurant_name'].nunique().reset_index()

#### Prepare data for stacked bar (single category = "Restaurants")
restaurants.set_index('city', inplace=True)

#### Plot stacked bar chart
restaurants.plot(kind='bar', stacked=True, figsize=(8,6), color='skyblue')

plt.title('Unique Restaurants per City')

plt.xlabel('Cities')

plt.ylabel('Unique Restaurants')

plt.xticks(rotation=45)

plt.legend().remove()  # No need for legend since only one category

plt.show()

### Top 10 Dishes Sold
dishes_sold = df_fpanda['dish_name'].value_counts().head(10)

dishes_sold.plot(kind= 'barh', figsize=(10,6), color='purple')

plt.title('Top 10 Dishes Sold')

plt.xlabel('Dishes')

plt.ylabel('No. of Orders')

plt.show

### Category distribution
category = df_fpanda['category'].value_counts()

plt.pie(category, labels=category.index, autopct='%1.1f%%', startangle = 90)

centre_circle = plt.Circle((0,0), 0.70, fc='white')

fig = plt.gcf()

fig.gca().add_artist(centre_circle)

plt.title('Category Distribution')

plt.show()

### Total Quantity Sold
Total_quantity = df_fpanda['quantity'].sum()

print("Total Quantity Sold-",Total_quantity)

### Avg price per dish
avg_price = df_fpanda['price'].mean().round(2)

print("Avg Price per Dish- Rs", avg_price)

### Preferred Payment Method
payment_method = df_fpanda['payment_method'].value_counts

sns.countplot(x='payment_method', data=df_fpanda, color= 'teal')

plt.title('Preferred Payment Method')

plt.show()

### Order frequency Distribution
plt.hist(df_fpanda['order_frequency'] , bins=40, color='orange')

plt.xlabel('Order Frequency')

plt.ylabel('Frequency')

plt.title('Order Frequency Distribution')

plt.show

### Average rating per category
avg_rating = df_fpanda.groupby('category')['rating'].mean()

plt.bar (avg_rating.index, avg_rating.values, color='blue')

plt.xlabel('Category')

plt.ylabel('Average Rating')

plt.title('Average Rating per Category')

plt.show

# Delivery Status
delivery_status = df_fpanda['delivery_status'].value_counts()

plt.pie(delivery_status, labels=delivery_status.index, autopct='%1.1f%%', startangle = 90)

centre_circle = plt.Circle((0,0), 0.70, fc='white')

fig = plt.gcf()

fig.gca().add_artist(centre_circle)

plt.title('Delivery Status')

plt.show()

### order trend
#### convert the date field to proper datetime field
df_fpanda['order_date'] = pd.to_datetime(df_fpanda['order_date'], errors='coerce')

#### Resample by month and count orders
order_trend_month = df_fpanda.resample('M', on='order_date')['order_id'].count()

#### Plot
plt.figure(figsize=(10, 5))

plt.plot(order_trend_month.index, order_trend_month.values, marker='o', linestyle='-', color='green')

plt.xlabel('Month')

plt.ylabel('No. of Orders')

plt.title('Monthly Order Trend')

plt.xticks(rotation=45)

plt.tight_layout()

plt.show()

### Correlation between order frequency and loyalty points
plt.scatter(df_fpanda['order_frequency'],df_fpanda['loyalty_points'])

plt.xlabel('order frequency')

plt.ylabel('loyalty points')

plt.show()

📈 **Key Insights (Example)**
- Age distribution for Orders in More for Teenagers
- Hyderabad, Bengaluru and Kolkata are some of the Top Cities by Order
- Pasta, Sandwich, Pizza, Fries and Burgers are Top Dishes sold among cities
- Italian Category Food is mostly Preferred by customers
- Preferred Payment Method is Cash

🙋‍♂️ Author
- Created by: Prasad Mahajan
- GitHub: prasadmahajan06  
