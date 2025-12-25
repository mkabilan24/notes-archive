# Data Warehousing
https://www.ibm.com/think/topics/data-warehouse
A data warehouse is a centralized repository for storing large amounts of integrated, historical data from multiple sources to support business intelligence and analytics.

*Will be using SSMS (SQL Server Management System) by Microsoft*

## Data Warehousing Concepts and Architecture
### Different Types of Data Storage
- **Database** -> Stores Application Specific Data
- **Data Warehouses** -> Data from any number of Applications or Databases that is purpose specific, clean and organized
- **Data Marts** - Subset of a Data Warehouse that is specific to a Buisness Domain
- **Data Lakes** -> Stores Raw, Structured, Unstructured, Semi-Structured data
- **Data Lakehouse** -> Merged key features of lakes and warehouses into one data solution for low-cost flexibility

### Data Virtualization
(aka Virtual Data Warehousing, Enterprise Information Integration (EII), Enterprise Data Access (EDA))
Data virtualization is a technology that creates a single, unified view of data from multiple, disparate sources without physically moving or replicating the data. It uses a virtual layer to abstract the underlying data, allowing users to access and analyze data in real-time as if it were in one place.

### Data Management Systems
**RDBMS (Relational Database Management System)**: 
    It uses the relational model, where data is organized into tables (relations) with rows and columns.
    Examples: MySQL, PostgreSQL, Oracle, Microsoft SQL Server.

**DDBMS (Distributed Database Management System)**:
    This describes a system where the physical database is stored across multiple computers (nodes) in a network, rather than all on a single machine. It focuses on transparency, reliability, and performance through data distribution and replication.

**MDBMS (Multidimensional Database Management System)**: 
    This type of system is primarily designed for Online Analytical Processing (OLAP) and complex queries. Data is conceptualized as a "cube" of data, allowing for efficient analysis across multiple dimensions (e.g., sales by product, region, and time).

***NOTE: Data Warehousing is considered MDBMS ***
Cube: Array-based multidimensional data structures
OLAP (Online Analytical Processing): Uses Cube
OLTP (Online Transaction Processing)

### OLAP vs OLTP
OLTP systems capture and update large volumes of real-time transactions from many users. In contrast, OLAP systems analyze data that has already been captured.

### 3 Types of OLAP
- Multidimensional online analytical processing (MOLAP)
- Relational online analytical processing (ROLAP)
- Hybrid online analytical processing (HOLAP)

## Bring Data into a Data Warehouse
### ETL 
E - Extract
T - Transform
L - Load

### ETL vs ELT
ETL tools extract data from source systems, transform it in a staging area and load it into the data warehouse. In ELT, the data is transformed after being loaded in the warehouse.

## Data Warehousing Design: Building Blocks
### Facts and fact tables
- **Facts**: The quantitative measures of a business process, such as sales amount, units sold, or cost. They are typically numerical and are the "what" of your data analysis.
- **Fact Table**: A central table that contains facts and foreign keys that link to dimension tables.
    
***Characteristics***: It is usually long with many records but fewer columns compared to dimension tables.
***Purpose***: To store the core business measurements that can be aggregated and analyzed. 

### Dimensions and dimension tables
- **Dimensions**: Descriptive attributes that provide context to the facts, such as customer demographics, product names, or dates. They are the "who, what, when, where" of the data.
- **Dimension Table**: A table that contains descriptive attributes and is linked to the fact table.

***Characteristics***: It is often wider (more columns) but has fewer records than a fact table. Dimension tables can also contain hierarchies (e.g., a date table with year, month, and day).
***Purpose***: To provide context, filter, and group the data in the fact table to gain deeper insights. 

### Star Schema and SnowFlake Schema
Star and snowflake schemas are two different data modeling approaches for data warehouses, differing primarily in their level of normalization. 

- A **star schema** is simple, using a central fact table directly connected to denormalized dimension tables, which results in faster queries but more data redundancy. 

- A **snowflake schema** is more complex, with normalized dimension tables that branch into multiple related tables, leading to less redundancy, lower storage costs, and higher data integrity, but with slower query performance due to more joins.  

## Managing Data Warehouse History Through Slowly Changing Dimensions
### Slowly Changing Dimensions (SCD)
Slowly changing dimensions (SCDs) are a data warehousing technique for managing and tracking how attribute data in dimension tables changes over time, often at a low frequency.

### Common types of SCDs
**Type 1 (Overwrite)**: This is the simplest method, where old data is overwritten with the new data, and no history is maintained. For example, if a customer's city changes, their record is updated with the new city, and the old one is lost. 

**Type 2 (Preserve History)**: This method keeps both the current and historical records in the table. It typically involves adding new columns like validFrom, validTo, or isValid to indicate the active period for each version of a record. When a change occurs, a new row is created for the record's new state, and the previous row is marked as inactive.

**Type 3 (Add a Column)**: This approach keeps a limited history by storing both the current value and the previous value in separate columns within the same record. For example, a CurrentAddress column and a PreviousAddress column could be added to a customer table. 

**Other types**: More complex types like Type 4 (using separate tables for history and current values) and Type 6 (a combination of Type 1, 2, and 3) also exist to handle more specific scenarios.

## Sevices
### SSIS (SQL Server Integration Services)
SQL Server Integration Services (SSIS) is a component of Microsoft SQL Server that provides a platform for building high-performance data integration and workflow solutions. It is primarily known as an Extract, Transform, and Load (ETL) tool used for tasks related to data warehousing, data migration, and data management.
SSIS excels at extracting data from various sources (databases, flat files, XML, etc.), transforming it according to business rules (cleaning, aggregating, merging), and loading it into target destinations (data warehouses, other databases).

### DQS (Data Quality Services) - Transform Level
Data Quality Services (DQS) in SQL Server is a knowledge-driven solution designed to help maintain and improve the quality of data within an organization. It provides tools and capabilities for data stewards and IT professionals to manage data quality through both computer-assisted and interactive processes.

### MDS (Master Data Services) - Data Source Level Before Extract
MDS addresses the need to consolidate and centralize non-transactional data that is crucial for business operations, such as customer information, product details, location data, or organizational hierarchies. This ensures consistency and accuracy across various systems and departments within an enterprise.

### SSRS (SQL Server Reporting Services)
SSRS most commonly refers to SQL Server Reporting Services, a Microsoft platform for creating, managing, and delivering paginated and mobile reports. It is a server-based reporting tool used to generate a wide range of reports from various data sources.

# Data Warehouse Microsoft SQL Server 2025 Resource
https://learn.microsoft.com/en-us/sql/sql-server/?view=sql-server-ver17