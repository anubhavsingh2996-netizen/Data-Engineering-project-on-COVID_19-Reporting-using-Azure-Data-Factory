# Data-Engineering-project-on-COVID_19-Reporting-using-Azure-Data-Factory
Concept of the Project 💡
This project is about ingesting a couple of Covid-19 Datasets from the ECDC website, transforming them using various ADF components, and then performing transformations by using ADF, HDInsight, and Databricks, then loading them into SQL Datawarehouse for the Analytics team to derive useful and actionable insights from these datasets. The primary objective is to comprehensively understand the influence of COVID-19 on the entirety of the European Region throughout the course of the year 2020.
Task 🎯
The task of this project is to ingest the data from multiple data sources, and clean and transform the data to make it more robust and fit for the goal. The cleaned data should then be loaded into a central repository, like a Data warehouse or a datalake so that the analytics team can consume it with their BI tools such as Power BI. The data warehouse will include details about confirmed cases, unfortunate mortality rates, hospitalization and ICU cases from our weekly data lake counts, and the testing numbers. Also, we can run ML Models that use these data to predict the spread of COVID-19 in the European region.
Source Data: 📤
ECDC (https://www.ecdc.europa.eu/en/covid-19)
Population Data From Azure Blob Storage (eurostat_data)
Destination: 📥📍
Azure Data Lake Gen2 Storage
Tools ⚙
Data Integration/Ingestion
ADF Data Flows within the Data Factory
Transformation
Data Flows within the Data Factory
DataBricks
Data Warehouse Solution
Azure SQL Database
Visualization
Power BI Desktop
Power BI Service
All the steps performed in this project are available as images in the Screenshots folder in this repository.
Approach
Environment Setup
Azure Subscription
Data Factory
Azure Blob Storage Account
Data Lake Storage Gen2
Azure SQL Database
Azure Databricks Cluster
HD Insight Cluster
Solution Architecture Overview:
image

Data Extraction/Data Ingestion
Four different datasets were ingested from both the ECDC website and Azure blob storage into Datalake Gen2. They are:

Cases and Deaths Data
Hospital Admissions Data
Population Data
Test Conducted Data
We used various components of ADF Pipeline activities to ingest the data from both HTTP Data Source and Azure Storage Account to Azure DataLake. Some of those activities are:

Validation Activity
Get Metadata Activity
Copy Activity
1- Population Data
Ingest "population by age" data for all EU Countries into the Data Lake to support the machine learning models with the data to predict an increase in COVID-19 mortality rate.

Solution Flow:
image

Steps:
Create a Linked Service To Azure Blob Storage
Create a Source Data Set
Create a Linked Service To Azure Data Lake storage (GEN2)
Create a Sink Data set
Create a Pipeline:
Execute Copy activity when the file becomes available
Check metadata counts before loading the data using the IF Condition
Finally, Load Data into our destination
ScheduleTrigger
###Pipeline Design: image

2- ECDC Data
the ECDC Data Content - Four files of CSV :
Case & Deaths Data.csv
Hospital Admission Data.csv
testing.csv
country_response.csv
Solution Flow:
image

Steps:

Create a Linked Service using an HTTP connector
Create a Source Data Set
Create a Linked Service To Azure Data Lake storage (GEN2)
Create a Sink Data set
Create a Pipeline With Parameters & Variables
Lookup to get all the parameters from json file, then pass it to ForEach ECDC DATA as shown below
Schedule Trigger
Json File:
image

Pipeline Design:
image

2.Data Transformation
The Cases and Deaths data together with the Hospital admissions data was transformed using ADF Data flows. The Data flow transformation used on both dataset include;

Select transformation
Lookup transformation
Filter transformation
Join transformation
Sort transformation
Conditional split transformation
Derived columns transformation
Sink transformation
Data Flows (1) Cases & Deaths Data:
Solution Flow:
image

Steps:
Cases And Deaths Source (Azure Data Lake Storage Gen2 )
Filter Europe-Only Data
Select only the required columns
PivotCounts using indicator Columns(confirmed cases, deaths) and get the sum of daily cases count
Lookup Country to get country_code_2_digit,country_code_3_digit columns
Select Only the required columns for the Sink
Create a Sink dataset (Azure Data Lake Storage Gen2)
Used Schedule Trigger
Pipeline Overview:
image

Data Flows (2) Hospital Admissions Data:
Solution Flow:
image

Steps:
Hospital Admissions Source (Azure Data Lake Storage Gen2 )
Select only the required columns
Lookup Country to get country_code_2_digit,country_code_3_digit columns
Select only the required columns
Condition Split Weekly, Daily Split condition
indicator=='Weekly new hospital admissions per 100k' || indicator=='Weekly new ICU admissions per 100k'
indicator== "Daily hospital occupancy" || indicator=="Daily ICU occupancy"
For Weekly Path
Join with Date to get ecdc_Year_week, week_start_date, week_End_date
Piovt Counts using indicator Columns(confirmed cases, deaths) and get the sum of daily cases count
Sort data using reported_year_week ASC and Country DESC
Select only the required columns for the sink
Create a sink dataset (Azure Data Lake Storage Gen2)
Schedule Trigger
For Daily Path
Pivot Counts using indicator Columns(confirmed cases, deaths) and get the sum of daily cases count
Sort Data using reported_year_week ASC and Country DESC
Select only the required columns for the sink
Create a sink dataset (Azure Data Lake Storage Gen2)
Used Schedule Trigger
Pipeline Design:
image

Databricks Activity (3) -- Population File:
Overview:
image

Attached File: (https://github.com/Eshwarreddyt/Azure-DataFactory-Project-Covid19-Reporting/blob/main/pyspark_notebooks/transform_population_data.py)

Copy Data to Azure SQL
1- Copy Cases and Deaths

2- Copy hospital admissions data

3- Copy testing data

Sample :
4 pl_succ

Reporting via Power BI
1- Create a Connection from Azure SQL to Power BI and load the data

2- Analyze the data to get the total confirmed cases and deaths count

3- Identify the trends in data based on reporting date

4- Publish the report to Power BI Server

5- Publish to web

Covid-19 Trend in the EU/EEA & UK 2020 by Cases, Deaths, Hospital Occupancy, and ICU Occupancy
image

Covid-19 Cases and Death breakdown by population in the UK, France, and Germany
image

Confirmed Cases Vs Total Deaths By Country
image

Total Number of Covid tests carried out vs. Confirmed Cases
image

Dashboard Link :
Power BI Dashboard Covid 19 Cases

Used Technologies :
Azure DataFactory
Azure HDinsight (Hive)
Azure Databricks (Pyspark, SparkSql)
Azure Storage Account
Azure Data Lake Gen2
Azure SQL Database
All the steps performed in this project are available as images in the Screenshots folder in this repository.
LinkedIn Badge
This project allowed me to demonstrate my expertise in Azure technologies, particularly in using Azure Databricks and Data Factory to orchestrate complex data workflows. It highlights the power of Azure Databricks and Data Factory in automating the process of cleaning and storing data, which in turn saves a lot of time and effort. I am excited about the endless possibilities that Microsoft Azure offers and can't wait to explore more.
