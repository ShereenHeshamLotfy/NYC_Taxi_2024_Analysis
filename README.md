# 🚕 NYC Taxi Trips 2024 – Data Cleaning & Analysis Pipeline

This project builds a complete data preparation and analysis workflow for New York City taxi trip records published by the
New York City Taxi and Limousine Commission (TLC) for
New York City.

The goal is to clean monthly raw data, fix common data quality issues, merge all months into a single dataset, and prepare the data for analytics and reporting (including Power BI / DAX).

# 📌 Project Objectives

Clean and standardize monthly taxi trip CSV files

Handle missing and invalid values

Correct zero and negative values in key numerical fields

Merge large monthly datasets efficiently

Prepare a final dataset suitable for BI tools and statistical analysis

# 🗂️ Project Structure
NYC_Taxi_2024/
│
├── cleaned_months/
│   ├── month_1_cleaned.csv
│   ├── month_2_cleaned.csv
│   ├── ...
│   └── nyc_taxi_2024_cleaned.csv   ← final merged file
│
├── Colab Notebooks/
│   ├── Month_1.ipynb
│   └── Month_2.ipynb
│   ├── ...
│   └── Month_12.ipynb
│
└── README.md

# 📊 Data Description

Each row represents a single taxi trip and contains (among others) the following fields:

pickup_datetime

dropoff_datetime

passenger_count

trip_distance

RatecodeID

PULocationID

DOLocationID

payment_type

fare_amount

extra

mta_tax

tip_amount

tolls_amount

improvement_surcharge

total_amount

congestion_surcharge

Airport_fee

# 🧹 Data Cleaning Steps
## 1. Fix zero trip distances

Trips with trip_distance = 0 are treated as invalid measurements.

They are replaced using the average trip distance per drop-off zone:

The average distance is computed per dropoff_LocationID

Each zero value is replaced with the corresponding zone average

This avoids removing trips while keeping distances realistic.

## 2. Handle negative tip amounts

Although tips should be non-negative, a small number of records contain negative values due to:

accounting corrections

refunds

data inconsistencies

These trips are identified using:

tip_amount < 0

Depending on the analysis, they can be:

removed, or

replaced with 0

## 3. Validate missing values

Key numeric columns (trip_distance, fare_amount, tip_amount, total_amount) are checked for:

missing values

unrealistic values

## 4. Large file processing with chunks

Monthly CSV files are processed and merged using chunk-based reading to avoid memory issues:

each file is read in chunks of 500,000 rows

only the first chunk writes the header

all remaining chunks are appended

This allows the project to scale to tens of millions of records.

# 🔗 Merging Monthly Files

All cleaned monthly files are merged into a single file:

cleaned_months/nyc_taxi_2024_cleaned.csv

The merging process:

reads each file in chunks

appends data to the final file

ensures the header is written only once

This is designed specifically for large datasets.

# 📈 Power BI / DAX Measures

The dataset is prepared so that:

one row = one trip

Typical measures used in Power BI include:

Number of trips

COUNTROWS(Trips)

Trips with negative tips

CALCULATE(
    COUNTROWS(Trips),
    Trips[tip_amount] < 0
)

Trips with electronic tips

CALCULATE(
    COUNTROWS(Trips),
    Trips[tip_amount] > 0
)
⚠️ Important Notes About Tip Data

tip_amount = 0 does not necessarily mean no tip

cash tips are not captured electronically and appear as zero

only tip_amount > 0 represents recorded electronic tips

# 🧰 Technologies Used

Python

pandas

Google Colab / Jupyter Notebook

Power BI (for visualization and DAX analysis)

# ✅ Final Output

The final cleaned and merged dataset:

nyc_taxi_2024_cleaned.csv

is ready for:

exploratory data analysis

dashboard development

demand pattern studies

spatial and temporal analysis

# 📄 License and Data Source

The raw data is provided by the New York City public open data program through the NYC Taxi and Limousine Commission (TLC).

This project focuses solely on data cleaning, preparation, and analytical use of the publicly available datasets.

# 📊 Overview Dashboard:
<img width="1332" height="713" alt="image" src="https://github.com/user-attachments/assets/b3322074-9ebc-4435-84e7-e46bf00b668e" />


If you want to see my work you can use this link:https://drive.google.com/drive/folders/1SHdOdg9_Y5N768sDD0rAdKw79IaP0aBr?usp=sharing                                                                                           
<div align="center">
  <video src="https://github.com/user-attachments/assets/09563d40-aa85-4cd8-b462-c9cdf13efc72" width="100%" autoplay muted loop playsinline>
  </video>
</div>


