# project1
Crime data analysis





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
