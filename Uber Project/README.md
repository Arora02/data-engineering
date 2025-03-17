# 🚗 Uber Data Engineering End-to-End Project

## Objective

In this project, I designed and implemented an end-to-end data pipeline that consists of several stages:
1. Extracted data from NYC Trip Record Data website and loaded into Google Cloud Storage for further processing.
3. Transformed and modeled the data using fact and dimensional data modeling concepts using Python on Jupyter Notebook.
4. Using ETL concept, I orchestrated the data pipeline on Mage AI and loaded the transformed data into Google BigQuery.
5. Developed a dashboard on Looker Studio.

As this is a data engineering project, my emphasis is primarily on the engineering aspect with a lesser emphasis on analytics and dashboard development.

The sections below will explain additional details on the technologies and files utilized.

## Table of Content

- [Dataset Used](#dataset-used)
- [Technologies](technologies)
- [Data Pipeline Architecture](#data-pipeline-architecture)
- [Date Modeling](#data-modeling)
- [Step 1: Cleaning and Transformation](#step-1-cleaning-and-transformation)
- [Step 2: Storage](#step-2-storage)
- [Step 3: ETL / Orchestration](#step-3-etl--orchestration)
- [Step 4: Analytics](#step-4-analytics)
- [Step 5: Dashboard](#step-5-dashboard)

## Dataset Used

This project uses the TLC Trip Record Data which include fields capturing pick-up and drop-off dates/times, pick-up and drop-off locations, trip distances, itemized fares, rate types, payment types, and driver-reported passenger counts.

More info about dataset can be found in the following links:
- Website: https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
- Data Dictionary: https://www.nyc.gov/assets/tlc/downloads/pdf/data_dictionary_trip_records_yellow.pdf
- Raw Data (CSV): https://github.com/Arora02/data-engineering/blob/main/Uber%20Project/uber_data.csv

## Technologies

The following technologies are used to build this project:
- Language: Python, SQL
- Extraction and transformation: Jupyter Notebook, Google BigQuery
- Storage: Google Cloud Storage
- Orchestration: [Mage AI](https://www.mage.ai)
- Dashboard: [Looker Studio](https://lookerstudio.google.com)

## Data Pipeline Architecture

<img width="897" alt="Screenshot 2023-05-08 at 11 49 09 AM" src="https://user-images.githubusercontent.com/81607668/236729698-65e193bc-75ee-4ea6-9040-f33f5f2958cb.png">

Files in the following stages:
- Step 1: Cleaning and transformation - [Uber Data Engineering.ipynb](https://github.com/Arora02/data-engineering/blob/main/Uber%20Project/Uber%20Data%20Engineering.ipynb)
- Step 2: Storage
- Step 3: ETL, Orchestration - Mage: [Extract](https://github.com/Arora02/data-engineering/blob/main/Uber%20Project/Mage/uber_load_data.py), [Transform](https://github.com/Arora02/data-engineering/blob/main/Uber%20Project/Mage/uber_transformation.py), [Load](https://github.com/Arora02/data-engineering/blob/main/Uber%20Project/Mage/uber_gbq_load.py)
- Step 4: Analytics - [SQL script](https://github.com/Arora02/data-engineering/blob/main/Uber%20Project/sql_script.sql)
- Step 5: [Dashboard](https://github.com/Arora02/data-engineering/blob/main/Uber%20Project/Uber_Dashboard.pdf)

## Data Modeling

The datasets are designed using the principles of fact and dim data modeling concepts. 

![Data Model](https://user-images.githubusercontent.com/81607668/236725688-995b6049-26c1-440f-b523-7c6c10d507ba.png)

## Step 1: Cleaning and Transformation

In this step, I loaded the CSV file into Jupyter Notebook and carried out data cleaning and transformation activities prior to organizing them into fact and dim tables.

Here's the specific cleaning and transformation tasks that were performed:
1. Converted `tpep_pickup_datetime` and `tpep_dropoff_datetime` columns into datetime format.
2. Removed duplicates and reset the index.

Link to the script: [https://github.com/Arora02/data-engineering/blob/main/Uber%20Project/Uber%20Data%20Engineering.ipynb](https://github.com/Arora02/data-engineering/blob/main/Uber%20Project/Uber%20Data%20Engineering.ipynb)

![image](https://github.com/user-attachments/assets/38d5ac58-0337-423c-ae88-6d1c2086a66e)


After completing the above steps, I created the following fact and dimension tables below:

![image](https://github.com/user-attachments/assets/d671f164-e8e4-4e33-a7ad-8287baa1ff94)


![image](https://github.com/user-attachments/assets/f3405add-ceb9-42e5-9d52-039f5860bca1)


![image](https://github.com/user-attachments/assets/253431e6-4bf4-4407-a925-58fa226e0fef)


![image](https://github.com/user-attachments/assets/5e61a974-074c-4ab0-b382-d35b3820875e)


![image](https://github.com/user-attachments/assets/a9352b27-b1a8-41cc-aacf-fc9b26d5f655)


![image](https://github.com/user-attachments/assets/134d2b39-2dc6-4c62-a634-fe2b2464baad)


## Step 2: Storage

![image](https://github.com/user-attachments/assets/06ade8c1-12d0-4669-9455-a14a108cd138)


## Step 3: ETL / Orchestration

1. Begin by launching the SSH instance and running the following commands below to install the required libraries.

![image](https://github.com/user-attachments/assets/515aa03a-7ae4-4de8-a9db-c437c14ba903)


```python
# Install python and pip 
sudo apt-get install update

sudo apt-get install python3-distutils

sudo apt-get install python3-apt

sudo apt-get install wget

wget https://bootstrap.pypa.io/get-pip.py

sudo python3 get-pip.py

# Install Google Cloud Library
sudo pip3 install google-cloud

sudo pip3 install google-cloud-bigquery

# Install Pandas
sudo pip3 install pandas
```

2. After that, I install the Mage AI library from the [Mage AI GitHub](https://github.com/mage-ai/mage-ai#using-pip-or-conda). Then, I create a new project called "uber_de_project".

```python 
# Install Mage library
sudo pip3 install mage-ai

# Create new project
mage start demo_project
```

3. Next, I conduct orchestration in Mage by accessing the external IP address through a new tab. The link format is: `<external IP address>:<port number>`.

After that, I create a new pipeline with the following stages:
- Extract: [load_uber_data](https://github.com/Arora02/data-engineering/blob/main/Uber%20Project/Mage/uber_load_data.py)
- Transform: [transform_uber](https://github.com/Arora02/data-engineering/blob/main/Uber%20Project/Mage/uber_transformation.py)
- Load: [load_gbq](https://github.com/Arora02/data-engineering/blob/main/Uber%20Project/Mage/uber_load_data.py)

![image](https://github.com/user-attachments/assets/2851f833-2764-4bc0-8e79-11ac682d440a)


Before executing the Load pipeline, I download credentials from Google API & Credentials and then update them accordingly in the `io_config.yaml` file within the same pipeline. This step is essential for granting authorization to access and load data into Google BigQuery.

## Step 4: Analytics

After running the Load pipeline in Mage, the fact and dim tables are generated in Google BigQuery.

![image](https://github.com/user-attachments/assets/0c8145af-2ea7-4ee1-b805-b020578dc1c7)

Here's the additional analyses I performed:
1. Find the top 10 pickup locations based on the number of trips
![image](https://github.com/user-attachments/assets/f93e179c-1b02-4a9b-9c87-550d97fc3a64)

2. Find the total number of trips by passenger count:
![image](https://github.com/user-attachments/assets/be0b97de-0703-432f-aa65-80f5a9ab6e93)

3. Find the average fare amount by hour of the day:
![image](https://github.com/user-attachments/assets/d5497b25-eac8-43b4-8dd2-88c04ab95c7e)


## Step 5: Dashboard

After completing the analysis, I loaded the relevant tables into Looker Studio and created a dashboard, which you can view [here](https://lookerstudio.google.com/s/s2Cv9HZiz_I).

![Dashoard Pg 1](https://user-images.githubusercontent.com/81607668/236729944-0a66f699-689e-4cbb-a12a-860abdef2cf4.png)

![Dashboard Pg 2](https://user-images.githubusercontent.com/81607668/236729954-cecba4a6-fc90-4944-b27f-cfb9473422bf.png)

***
