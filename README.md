# project1
Crime data analysis
# Crime Data Analysis

This project analyzes crime data using **PySpark** for large-scale processing and visualizes trends using **Matplotlib** and **Seaborn**. It provides insights into crime patterns based on location, time, and type, enabling better decision-making for public safety.

## Features
- **Data Ingestion**: Ingest large crime datasets and clean them using PySpark.
- **Data Processing**: Use PySpark to analyze crime trends across different types of crimes.
- **Data Visualization**: Visualize insights using **Matplotlib** and **Seaborn**.

## Tools and Technologies
- **Python**, **PySpark**, **Seaborn**, **Matplotlib**, **PowerBI**, **Tableau**

## Setup Instructions
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/crime-data-analysis.git





### **Source Code for Crime Data Analysis**

#### **crime_data_processing.py** (Data processing with PySpark)
```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import year, col

def process_crime_data(input_path):
    spark = SparkSession.builder.appName("Crime Data Processing").getOrCreate()
    df = spark.read.csv(input_path, header=True, inferSchema=True)
    
    # Filter and analyze recent years' crime data
    crime_data_filtered = df.filter(year(col("crime_date")) >= 2019)
    
    crime_trends = crime_data_filtered.groupBy(year(col("crime_date")), col("crime_type")).count()
    crime_trends.show()

    spark.stop()

if __name__ == "__main__":
    process_crime_data('data/crime_data.csv')


###Crime_data_visualization.py (Visualization with Matplotlib)


import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

def plot_crime_trends(file_path):
    crime_data = pd.read_csv(file_path)
    
    plt.figure(figsize=(12, 6))
    sns.countplot(x='year', hue='crime_type', data=crime_data)
    plt.title('Crime Type Distribution by Year')
    plt.xlabel('Year')
    plt.ylabel('Crime Count')
    plt.show()

if __name__ == "__main__":
    plot_crime_trends('data/processed_crime_data.csv')
