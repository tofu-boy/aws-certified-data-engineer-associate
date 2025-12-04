# Data Engineering Fundementals

## Types of Data
### Structured
Data that is organised in a defined manner or schema, typically found in relation databases.
 - Easily Queryable
 - Organized in rows and columns
 - Has a consistent structure


### Unstructured
Data that does not have a predefined structure or schema.
 - Not easily queryable without preprocessing
 - May come in various formats

Examples

 - Text files without a fixed format
 - Videos and audio files
 - Images
 - Emails and word processing documents


### Semi-structured
Data that is not as organised as structured data but has some level of structure in the form of tags, heirarchies or other patterns. 
 - Elements might be tagged or categorized in some way
 - More flexible than structured data but not as chaotic as unstructured data

Examples
 - Log files with varied formats
 - XML and Json
 - Email headers

## Properties of Data
### Volume
Amount or size of data that organisations are dealing with at any given time.

### Velocity
Refers to the speed at which new data is generated, collected and processed.
High velocity required real-time or near-real-time processing capabilities.
Rapid ingestion and processing can be critical for certain applications.

Sensor data from IoT.

High-frequency trading systems where milliseconds can make a difference in decision-making.


### Variety
Refers to the different types, structures and sources of the data. 

Maybe we have a business analysing data from emails, json logs and databases.

## Data Warehouses vs Data Lakes
### Data Warehouse
Defeinition: a centralised repository optimized for analysis where data from different sources is stored in a structured format
 - designed for complex queries
 - data is cleaned, transformed and loaded (VIA ETL)
 - Typically uses a star of snowflake schema
 - Optimised for read-heavy operations

Examples
 - Amazon Redshift
 - Google BigQuery
 - Microsoft Azure SQL Data Warehouse

### Data Lake 
A storage repository that holds a vast amount of raw data in it's native format, semi-structured, structures and unstructured data. 

 - Can store large volumes of raw data without predefined schema
 - Data is loaded as-is, no need for preprocessing
 - Supports batch, real-time, and stream processing
 - Can be queried for data transformation or exploration purpoises

Examples:
 - Amazon S3
 - Azure Data Lake Storage
 - Hadoop HDFS

Comparison:
Schema:
 - Data Warehouse: Schema-on-write (predefined schema before writing data) , ETL
 - Data Lake: Schema-on-read (Schema is defined at time of reading data) , ELT

Data Types: 
 - DW: primarily structured
 - DL: both structured and unstructed

Agility:
 - DW: Less agile due to predefined schema
 - DL: More agile as it accepts raw data without a predefined structure

 Processing:
 - DW: ETL
 - DL: ELT

 Cost:
  - DW: Typically more expensive
  - DL: cheaper

Use a Data Warehouse when you have structured data sources and reqwuire fast complex queries.
Data integration from different sources is essential. Buesiness Intelligence are primary usecases

Use DataLake when you have a mix of data structuredness, you need a scalable and cost effective solution to store massive amounts of data. Need discoverability.

Data Lakehouse:
Hybrid data architecture combining best of both worlds.

AWS Lake formation: s3 and redshift spectrum.

## What is Data Mesh
Coined in 2019; it's more about governance and organization.

Individual teams own their own data, they own data products within a given domain.

Domain Based data management. Federated governance with central standards.

## ETL Pipelines
ETL stands for Extract, Transform, Load. It's a process used to move data from source systems into a data warehouse. (For Lake ELT).
### Extract:
 - Retrieve raw data from source systems which can be databases, CRMs, flat files, APIs, or other repositories
 - Ensure data integrity during the extraction phase.
 - Can be done in real-time or in batches, depending on requirements.

### Transform
 - Convert the extracted data into a format suitable for the target data warehouse
 - Cleansing (removing duplicates, fixing errors)
 - Data enrichment (adding additional data)
 - Format changes (e.g. datetime formatting)
 - Aggregations or computations (totals, averages)
 - Encoding or decoding
 - Handling missing data

### Load
 - Move transformed data into the target data warehouse
 - Can be done in batches (all at once) or in a streaming manner (as data becomes available)
 - Ensure that data maintains it's integrity during the loading phase.

### Managing ETL Pipelines
 - This process must be automated in some reliable way
 - AWS Glue
 - Orchestration services: [EventBridge, Amazon Managed Workflows for Apache AirFlow, AWS Step functions, Lambda, Glue workflows]
 - specific architectures later...

### Data Sources
 - JDBC: Java database connectivity, Platform independent, language dependent.
 - ODBC: Open Database Connectivity, Platform dependent, Language independent.
 - Raw Logs
 - API's
 - Streams

### Common Data Formats
 - CSV
 - Json
 - AVRO: Binary format that stores both the data and it's schema, allowing it to be processed later with different systems without needing the original's system context.
 Use AVRO with big data and real-time processing systems.
 When schema evolution is needed.
 Efficient serialization for data transport between systems.
 Kafka, spark, flink and hadoop use AVRO

 - Parquet: Columnar storage format, optimized for analytics, allows for efficient compression and encoding systems.
 Good for analyzing large datasets with analytics engines. Use cases where reading specifgic columns instead of entire records is beneficial. Useful for storing data on distributed systems where IO operations and storage need optimization.
 Hadoop, Spark, Hive, Impala and Redshift Spectrum.
 
