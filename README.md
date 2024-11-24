my Tableau Link
https://public.tableau.com/app/profile/kirui.wilberforce/viz/Aviation_17324306808780/Dashboard1?publish=yes



Aviation Incident Analysis: Insights and Safety Recommendations
Overview
This project aims to analyze aviation incident data to uncover trends, identify factors contributing to accidents, and provide actionable recommendations to enhance aviation safety. Key methods employed in the analysis include:

Descriptive Statistics
Data Visualizations
Data-driven Insights
The goal is to extract meaningful patterns from the data and use them to inform decision-making processes in the aviation industry.

Business Understanding
Business Problem
The company is entering the aviation market by purchasing and operating aircraft for both commercial and private enterprises. With the potential risks associated with various aircraft types, the company seeks to make informed decisions regarding aircraft purchases. The task is to identify low-risk aircraft that will help minimize potential safety hazards.

Objectives
Assess Risk Factors: Analyze historical aviation data to evaluate risks associated with various aircraft types.
Identify Trends and Patterns: Examine incidents related to aircraft type, manufacturer, and usage.
Provide Recommendations: Offer recommendations on the safest aircraft for purchase based on data insights.
Key Questions
What are the trends in accidents across different phases of flight?
How has the frequency of aviation accidents changed over time?
Which locations and weather conditions are most associated with aviation accidents?
What are the most common causes of aviation incidents?
How does aircraft damage impact fatality counts?
Key Stakeholders
Aviation Regulatory Authorities
Aircraft Manufacturers
Airlines and Aviation Operators
Aircraft Maintenance Providers
Insurance Companies
Pilots, Flight Crew & Passengers
Key Deliverables
A comprehensive analysis of aviation incident data.
Risk assessments for various aircraft types and manufacturers.
Actionable safety recommendations based on data-driven insights.
Data Understanding and Analysis
Data Source
The dataset used in this analysis comes from the National Transportation Safety Board (NTSB). It contains civil aviation accident data from 1962 to 2023, covering incidents in the United States and international waters.
Initial Data Analysis
python
# Importing Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import scipy.stats as stats
import datetime as dt
import warnings

# Loading the dataset
df = pd.read_csv(r"C:\Users\Hp\Desktop\Moringa\AviationData.csv", encoding='ISO-8859-1')

# Viewing the first and last rows
df.head()
df.tail()
Key Summary Statistics
python

# Descriptive statistics for numeric columns
df.describe()
Dataset Columns Overview
The dataset contains the following columns:

Event.Id
Investigation.Type
Accident.Number
Event.Date
Location
Country
Aircraft Details (e.g., Make, Model)
Incident Details (e.g., Total.Fatal.Injuries, Aircraft.damage)
Weather Conditions
Flight Phase
Data Cleaning and Missing Values
python

# Check for missing values
df.isna().sum()

# Impute missing categorical columns with the mode
df['Location'].fillna('Unknown', inplace=True)
# Impute numerical columns with mean/median
df['Total.Fatal.Injuries'].fillna(df['Total.Fatal.Injuries'].mean(), inplace=True)

# Drop columns with excessive missing values
df.drop(['FAR.Description', 'Schedule', 'Air.carrier'], axis=1, inplace=True)
Data Imputation and Final Cleaning
After cleaning, the dataset contains no missing values across all columns.

Data Visualizations
1. Incident Trends Over Time
python

# Creating a line plot for incident trends over time
df['Event.Date'] = pd.to_datetime(df['Event.Date'], errors='coerce')
df['Year'] = df['Event.Date'].dt.year
incident_trends = df.groupby('Year').size()

# Plotting the trends
plt.figure(figsize=(12, 6))
plt.plot(incident_trends.index, incident_trends.values, marker='o', color='b', linestyle='-')
plt.title('Number of Aviation Incidents Over Time')
plt.xlabel('Year')
plt.ylabel('Number of Incidents')
plt.grid(True, linestyle='--', alpha=0.6)
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
2. Incident Distribution by Aircraft Type and Manufacturer
python

# Incident Distribution by Aircraft Category
aircraft_category_counts = df['Aircraft.Category'].value_counts()

# Plotting by Aircraft Category
plt.figure(figsize=(12, 6))
plt.bar(aircraft_category_counts.index, aircraft_category_counts.values, color='skyblue')
plt.title('Incident Distribution by Aircraft Category')
plt.xlabel('Aircraft Category')
plt.ylabel('Number of Incidents')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Incident Distribution by Manufacturer (Top 20 Manufacturers)
manufacturer_counts = df['Make'].value_counts()
top_n = 20  

plt.figure(figsize=(12, 6))
plt.bar(manufacturer_counts.index[:top_n], manufacturer_counts.values[:top_n], color='orange')
plt.title('Top 20 Manufacturers by Number of Incidents')
plt.xlabel('Manufacturer (Make)')
plt.ylabel('Number of Incidents')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
3. Severity of Incidents
python


# Box plot for Number of Fatalities across Aircraft Category 
plt.figure(figsize=(12, 6))
sns.boxplot(x='Aircraft.Category', y='Total.Fatal.Injuries', data=df, palette='Set2')
plt.title('Number of Fatalities by Aircraft Category')
plt.xlabel('Aircraft Category')
plt.ylabel('Number of Fatalities')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
Conclusion
The analysis provides valuable insights into the frequency and severity of aviation incidents. By identifying trends, aircraft types, and manufacturers associated with higher accident rates, the company can make data-driven decisions when selecting aircraft for purchase, ultimately enhancing safety and reducing risks in its aviation operations.

Recommendations
Focus on purchasing aircraft from manufacturers with lower accident frequencies.
Invest in comprehensive training for pilots, especially regarding adverse weather conditions and flight phases with high incident rates.
Implement regular safety audits on aircraft categories associated with higher fatality rates.
This project offers actionable insights that support the company’s goal of ensuring safety in its aviation operations and making informed purchasing decisions
