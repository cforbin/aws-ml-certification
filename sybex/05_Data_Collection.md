
# CHAPTER 5 : DATA COLLECTION

## BASIC DATA CONCEPTS

### 3 kinds of data

- Structured data: CSV, tables (row and columns) = tabular dataset.  
  Has well defined schema and metadata, data attributes and data types.
- Unstructured data: images, audio, video, text documents, application log files.
- Semi-structured data:  JSON, XML


### ML data concepts

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
- Training data
- Validation data
- Test data

*It is helpful for the test to understand the different classifications of data
for machine learning and the associated terminology.*

## DATA REPOSITORIES

## S3

## AWS RDS

- Relational database solution = AWS RDS
- Relational databases typically use row-wise storage 
- Suited for queries for specific rows, inserts, and updates.
- Variety of underlying engines:
- AWS Aurora, 
- MySQL, MariaDB, and PostgreSQL
- Oracle, Microsoft SQL Server, 

## Amazon Redshift 

- Data warehouse solution = Amazon Redshift. 
- For analytics and reporting workloads that are read heavy, 
- uses columnar storage instead of row-level storage for fast retrieval of columns
- suited for querying against very large datasets. 
- Redshift is now integrated with Amazon SageMaker via SageMaker Data Wrangler.

- Both Redshift and RDS store tabular data. 


*We recommend that you go over the FAQs for AWS Data Pipeline, AWS
Glue, and AWS DMS prior to taking the test.*

[FAQ AWS Data Pipelines](https://aws.amazon.com/datapipeline/faqs/)

[FAQ AWS Glue](https://aws.amazon.com/glue/faqs/)

[FAQ AWS DMS](https://aws.amazon.com/dms/faqs/)

[FAQ AWS Redshift](https://aws.amazon.com/redshift/faqs/)

[FAQ AWS RDS](https://aws.amazon.com/rds/faqs/)



