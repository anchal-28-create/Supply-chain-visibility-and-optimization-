# Supply Chain Visibility & Optimization - Milestone 1: Data Modelling

## Objective

Build a clean and reliable data foundation for supply chain analytics by importing the DataCo Supply Chain Dataset into Power BI and designing an optimized data model.

The goal of this milestone is to:
- Import supply chain data into Power BI
- Perform data preprocessing and transformation
- Create fact and dimension tables
- Build relationships between tables
- Prepare the model for KPI reporting and dashboard creation


## Dataset Source

Dataset Name: DataCo Smart Supply Chain for Big Data Analysis (Kaggle)

Dataset Link:
https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis


## Data Cleaning and Preprocessing

The dataset was downloaded from Kaggle and was already well structured, therefore major data cleaning was not required.

Basic preprocessing and transformation steps performed:

- Imported the CSV dataset into Power BI using Get Data option
- Opened Power Query Editor for data transformation
- Renamed the main query as Fact_table
- Removed unnecessary/sensitive columns
- Checked column quality and column distribution
- Verified that there were no missing values
- Removed duplicate records wherever required
- Corrected data types:
  - Date columns → Date/Time
  - ID columns → Whole Number
  - Price, Sales and Profit columns → Decimal Number


## Data Modelling

The data model was created by separating transactional data into a Fact table and descriptive data into Dimension tables.


## Fact Table Created

### Fact_table

The fact table contains transactional information:

- Order details
- Sales information
- Profit and benefit values
- Shipping details
- Customer details reference
- Product details reference
- Location and date references


## Dimension Tables Created


### 1. Dim_Customer

Steps:

- Duplicated Fact_table
- Selected customer related columns
- Removed duplicate records using Customer_id
- Created customer dimension table


### 2. Dim_Product

Steps:

- Duplicated Fact_table
- Selected product related columns
- Removed duplicate records using Product_card_id
- Created product dimension table


### 3. Dim_Category

Steps:

- Duplicated Fact_table
- Selected category related columns
- Removed duplicate records using Category_id
- Created category dimension table


### 4. Dim_Shipping

Steps:

- Duplicated Fact_table
- Selected shipping related columns
- Removed duplicate records
- Added Index Column starting from 1
- Renamed index column as Shipping_id
- Merged Shipping_id into Fact_table


### 5. Dim_Location

Steps:

- Duplicated Fact_table
- Selected location related columns
- Removed duplicate records
- Added Index Column starting from 1
- Renamed index column as Location_id
- Merged Location_id into Fact_table


### 6. Dim_Department

Steps:

- Duplicated Fact_table
- Selected department related columns
- Removed duplicate records using Department_id
- Created department dimension table



## Date Dimension Table

A separate Dim_Date table was created using DAX CALENDAR function.

Additional columns created:

- Year
- Month Number
- Month Name
- Quarter
- Week Number
- Day
- Day Name



## Relationships Created

Relationships were created between Fact and Dimension tables.

### One-to-Many Relationships (1:*)

1. Dim_Customer → Fact_table

- Connected using Customer_id
- Relationship: One-to-Many


2. Dim_Shipping → Fact_table

- Connected using Shipping_id
- Relationship: One-to-Many


3. Dim_Location → Fact_table

- Connected using Location_id
- Relationship: One-to-Many


4. Dim_Date → Fact_table

- Connected using Order Date
- Relationship: One-to-Many


5. Dim_Category → Dim_Product

- Connected using Category_id
- Relationship: One-to-Many


6. Dim_Department → Dim_Product

- Connected using Department_id
- Relationship: One-to-Many



### Many-to-Many Relationship (*:*)

Dim_Product → Fact_table

- Product table was connected with Fact_table
- Relationship type: Many-to-Many


Cross filter direction was configured according to model requirements.

The final structure follows a Star/Snowflake schema approach for optimized supply chain analytics.



## Tools Used

- Power BI Desktop
- Power Query Editor
- DAX
- GitHub



## Final Output

Successfully created a Power BI data model containing Fact and Dimension tables with proper relationships.

