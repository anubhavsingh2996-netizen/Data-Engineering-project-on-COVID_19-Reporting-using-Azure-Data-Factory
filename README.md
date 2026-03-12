# Data-Engineering-project-on-COVID_19-Reporting-using-Azure-Data-Factory
## Concept of the Project 💡
This project is about ingesting a couple of Covid-19 Datasets from the ECDC website, transforming them using various ADF components, and then performing transformations by using ADF, HDInsight, and Databricks, then loading them into SQL Datawarehouse for the Analytics team to derive useful and actionable insights from these datasets. The primary objective is to comprehensively understand the influence of COVID-19 on the entirety of the European Region throughout the course of the year 2020.
## Task 🎯
The task of this project is to ingest the data from multiple data sources, and clean and transform the data to make it more robust and fit for the goal. The cleaned data should then be loaded into a central repository, like a Data warehouse or a datalake so that the analytics team can consume it with their BI tools such as Power BI. The data warehouse will include details about confirmed cases, unfortunate mortality rates, hospitalization and ICU cases from our weekly data lake counts, and the testing numbers. Also, we can run ML Models that use these data to predict the spread of COVID-19 in the European region.
## Source Data: 📤
ECDC (https://www.ecdc.europa.eu/en/covid-19)
Population Data From Azure Blob Storage (eurostat_data)
Destination: 📥📍
Azure Data Lake Gen2 Storage
## Tools ⚙
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
'
## All the steps performed in this project are available as images in the Screenshots folder in this repository.
### Approach
Environment Setup
Azure Subscription

## Solution Architecture Overview : 
<img width="917" height="493" alt="image" src="https://github.com/user-attachments/assets/0a38102b-8cbf-4c37-aca2-580d486b25d0" />

Data Factory
Azure Blob Storage Account
Data Lake Storage Gen2
Azure SQL Database
Azure Databricks Cluster
HD Insight Cluster
