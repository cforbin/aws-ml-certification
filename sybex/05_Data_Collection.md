
# CHAPTER 5 : DATA COLLECTION

Data Collection
- Basic Data Concepts
- Data Repositories
- Data Migration to AWS
  - Batch Data Collection
  - Streaming Data Collection
- Summary
- Exam Essentials
- Review Questions

# BASIC DATA CONCEPTS

## 3 kinds of data

- **Structured data**: CSV, tables (row and columns) = tabular dataset.  
  Has well defined schema and metadata, data attributes and data types.
- **Unstructured data**: images, audio, video, text documents, application log files.
- **Semi-structured data**:  JSON, XML

## General data concepts

- Labeled data
- Unlabeled data
- Data Point: row in a tabular dataset with features.  Also can contain labels.
- Dataset: collection of data points
- Feature
- Numerical feature
- Categorical feature
- Image data
- Audio data
- Text data (corpus): collection of documents stored in TXT, PDF, JSON, CSV files.
- Time Series data: data varying over time: stock price, IoT sensor readings, etc.

## ML data concepts

- Training data
- Validation data
- Test data

*It is helpful for the test to understand the different classifications of data
for machine learning and the associated terminology.*

# DATA REPOSITORIES

Different data repositories where this data can be housed, read from, and queried.

## TABULAR DATA 

- For online transaction processing:
  - AWS RDS: has different engines
    - AWS Aurora
    - MySQL, MariaDB, PostgreSQL
    - Oracle, Microsoft SQL Server
- For analytics and reporting:
  - Amazon Redshift
    - is a data warehouse
    - has columnar storage, 
    - integrated witn Amazon SageMaker via SageMaker Data Wrangler

## SEMI-STRUCTURED DATA

Uses NoSQL databases.
- DynamoDB = store key-value pairs
- DocumentDB = store JSON data ("documents"), **similar to MongoDB**.  

*AWS recommends to use purpose-built databases for specific applications*, whether it is 
- OLTP 
- analytics or reporting 
- bulk object storage like Amazon S3. 

## DATA LAKE

When you have data in diverse data repositories, you may want to 
- centrally manage and govern the access controls to these datasets
- audit that access over time.

**AWS Lake Formation** is a data lake solution that helps you to:
- centrally catalog your data and 
- establish fine-grained controls on who can access thedata. 
- Users can query the central catalog in Lake Formation and then 
- run analytics or ETL workstreams on the data using tools like 
  - **Amazon Redshift** 
  - **Amazon EMR**.

## S3

- Data must be stored in S3 to be used by Sagemaker for machine learning modeling.
- S3 was covered in **CHAPTER 2** of this book.
- How migrate data to S3?  See next section.

# DATA MIGRATION TO AWS

## BATCH DATA COLLECTION

### AWS RDS

- Relational database solution = AWS RDS
- Relational databases typically use row-wise storage 
- Suited for queries for specific rows, inserts, and updates.
- Variety of underlying engines:
- AWS Aurora, 
- MySQL, MariaDB, and PostgreSQL
- Oracle, Microsoft SQL Server, 

#### Amazon Redshift 

- Data warehouse solution = Amazon Redshift. 
- For analytics and reporting workloads that are read heavy, 
- uses columnar storage instead of row-level storage for fast retrieval of columns
- suited for querying against very large datasets. 
- Redshift is now integrated with Amazon SageMaker via SageMaker Data Wrangler.

- Both Redshift and RDS store tabular data. 

## STREAMING DATA COLLECTION

# SUMMARY

In this chapter, we covered:
- terminology for data in general
- terminology specific to machine learning
- AWS data repositories and their end uses 
- AWS tools for bringing data into AWS and then into S3 for ML.
- 2 data collection patterns: 
  - batch
  - streaming

# RECOMMENDED

*We recommend that you go over the FAQs for AWS Data Pipeline, AWS
Glue, and AWS DMS prior to taking the test.*

[FAQ AWS Data Pipelines](https://aws.amazon.com/datapipeline/faqs/)

[FAQ AWS Glue](https://aws.amazon.com/glue/faqs/)

[FAQ AWS DMS](https://aws.amazon.com/dms/faqs/)

[FAQ AWS Redshift](https://aws.amazon.com/redshift/faqs/)

[FAQ AWS RDS](https://aws.amazon.com/rds/faqs/)




# EXAM ESSENTIALS



# REVIEW QUESTIONS
