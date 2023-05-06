
# CHAPTER 5 : DATA COLLECTION

Data Collection
- [Basic Data Concepts](#basic-data-concepts)
- [Data Repositories](#data-repositories)
- [Data Migration to AWS](#data-migration-to-aws)
  - Batch Data Collection
  - Streaming Data Collection
- [Summary](#summary)
- [Exam Essentials](#exam-essentials)
- [Review Questions](#review-questions

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

 ## AWS data sources
 
 Covered in great detail in Solution Architect Exams  (Associate)
 

*For the exam, you should have a basic familiarity with the different AWS data storage solutions.*

# DATA MIGRATION TO AWS

- Once your data lands in AWS, you need to move the data to Amazon S3 in order to train ML models. 
- If your data is already on S3, then you’re all set.
- There are different migration tools available on AWS to move your data to S3.
- There are 2 use cases for migrating data onto AWS: 
  - batch data
  - streaming data


## BATCH DATA COLLECTION


## AWS DATA PIPELINE

- Use **AWS Data Pipeline** if your data is already on AWS:
- from Redshift, DynamoDB, or RDS 
- to S3.

- An activity type is a pipeline component that tells Data Pipeline what job to perform.
- Data Pipeline has some prebuilt activity types
  - CopyActivity   (S3 to S3)
  - RedshiftCopyActivity (Redshift to S3)
  - SqlActivity (SQL query to S3)
  
- To use AWS Data Pipeline, you create a **pipeline definition**, which consists of:
  - activities
  - data nodes
  - schedule  
  
- [List of activities](https://docs.aws.amazon.com/datapipeline/latest/DeveloperGuide/dp-concepts-activities.html):
  - CopyActivity: Copies data from one location to another.
  - EmrActivity: Runs an Amazon EMR cluster.
  - HiveActivity: Runs a Hive query on an Amazon EMR cluster.
  - HiveCopyActivity: Runs a Hive query on an Amazon EMR cluster with support for advanced data filtering and support for S3DataNode and DynamoDBDataNode.
  - PigActivity: Runs a Pig script on an Amazon EMR cluster.
  - RedshiftCopyActivity: Copies data to and from Amazon Redshift tables.
  - ShellCommandActivity: Runs a custom UNIX/Linux shell command as an activity.
  - SqlActivity: Runs a SQL query on a database.

- List of nodes:
  - DynamoDBDataNode: a DynamoDB table that contains data for HiveActivity or EmrActivity to use.
  - SqlDataNode: an SQL table and database query that represent data for a pipeline activity to use.
  - RedshiftDataNode: an Amazon Redshift table that contains data for RedshiftCopyActivity to use.
  - S3DataNode: an Amazon S3 location that contains one or more files for a pipeline activity to use.

Once your data is in S3, you can run ETL jobs on the data using Amazon EMR.


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

4 Kinesis services:
- Kinesis Data Streams
- Kinesis Data Firehose
- Kinesis Data Analytics
- Kinesis Video Streams

**Kinesis Data Streams**

- Collect and process large streams of data records in real time. 
- Once the data streams are in AWS, you can run a number of downstream applications such as real-time data analytics by sending the data to a dashboard. 
- Similarly, you can intake logs from different applications and sensors and process them and generate real-time metrics and reports.

- **Data stream** 
  - Represents a group of data records, where a data record is a unit of data.
  - Data records are distributed into shards. 
  - A shard represents a sequence of data records.
  - Each shard supports 
    - 5 transactions/second for reads or 
    - up to 2 MB per second 
    - and 1000 records/second 
    - up to 1 MB per second for writes. 
    - When you create a Kinesis Data Stream, you specify the number of shards.
    
- **Retention period**
  - Length of time the data is available in the stream. 
  - Default is 24 hours.
  - Can increase it to 365 days (8,760 hours).
  
- **Producer**
  - Puts records into the streams such as a web log server. 
  - Use KPL (Kinesis Producer Library) to build your producer application.

- **Consumer**
  - Gets records from the stream and processes them. 
  - Consumer applications often run on a fleet of EC2 instances. 
  - KCL (Kinesis Client Library) abstracts a lot of the lower-level Kinesis data streams APIs to allow you to:
    - manage your consumer applications
    - distribute load across consumers
    - respond to instance failures
    - checkpoint records.

- **Downstream AWS Services** 
  - Include services such as S3, EMR, and Redshift 
  - Consumers send the outputs of the processed stream to them for various end applications.
 
**Kinesis Data Firehose**

If you need send streaming data directly to an end service such as: 
- Amazon S3 for storage 
- Redshift for querying
- Elastic Search/Splunk 
- Other custom third-party endpoint
  - Datadog

you can use
- Kinesis Data Streams:  you need write producer-consumer applications
- Kinesis Data Firehose: (aka KDF) is simpler!

KDF can:
- automatically deliver your data to the services just listed
- convert incoming JSON to another format (Parquet, ORC, etc) before storing in S3.
- allow use **AWS Lambda functions** to process incoming data stream before final delivery


**Kinesis Data Analytics**

- Run SQL directly on streaming data.
- Input:  KDS, KDF, S3
- Output: KDS, KDF
- KDF --> Redshift, ElasticSearch, Splunk, S3
- Can generate metrics or aggregated analysis over windows for timeseries data.
- Can feed real-time dashboards.
- Streaming SQL is different from standard SQL queries on batch data
since the query must occur over a particular time window

**Kinesis Video Streams**

- Capture massive amounts of live video from sources like 
  - webcams, 
  - embedded cameras in cars, 
  - drone footage, 
  - security cameras, and 
  - smartphones. 

- Can use with non-video streams:
  - audio data
  - RADAR and LIDAR data

- Works similar to data streams
  - **Producer**: any video-generating device
  - **Consumer**: an EC2-based application that processes and analyzes video data
 
- *Amazon Rekognition Video* can be used as a downstream service of KVS.


**Kafka-Based Applications**

- A common open-source tool for streaming data is Apache Kafka. 
- Kafka and Kinesis are similar:
  - decoupled producer
  - consumer-based model  
- Amazon MSK = Amazon Managed Streaming for Kafka
- You can migrate applications based on Kafka to AWS, and use MSK.


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

*Recommended reading for Kinesis*

[FAQ Kinesis Data Streams](https://aws.amazon.com/kinesis/data-streams/faqs/)

[FAQ Kinesis Data Firehose](https://aws.amazon.com/kinesis/data-firehose/faqs/)

[FAQ Kinesis Data Analytics](https://aws.amazon.com/kinesis/data-analytics/faqs/)

[Streaming SQL Concepts](https://docs.aws.amazon.com/kinesisanalytics/latest/dev/streaming-sql-concepts.html)

[FAQ Kinesis Video Streams](https://aws.amazon.com/kinesis/video-streams/faqs/)

[FAQ Amazon Managed Streaming for Kafka](https://aws.amazon.com/msk/faqs/)


*Recommended reading FAQs for AWS data services*

[FAQ AWS Data Pipelines](https://aws.amazon.com/datapipeline/faqs/)

[Data Pipelines activities](https://docs.aws.amazon.com/datapipeline/latest/DeveloperGuide/dp-concepts-activities.html)

[FAQ AWS Glue](https://aws.amazon.com/glue/faqs/)

[FAQ AWS DMS](https://aws.amazon.com/dms/faqs/)

[FAQ AWS Redshift](https://aws.amazon.com/redshift/faqs/)

[FAQ AWS RDS](https://aws.amazon.com/rds/faqs/)


# EXAM ESSENTIALS

1. CRISP-DM: where data collection fits
2. Kinds of data: strucuted, semi-structured, unstructured.  Examples
3. Training, validation, and test data.
4. Continuous and categorical features
5. Data Pipeline **vs** Database Migration Service
6. Kinesis Data Streams **vs** Kinesis Data Firehose


# REVIEW QUESTIONS

**ERROR:** 1A 2B 8A

**OK:** 3A 4B 5D 6B 7B 9B 10D 11C 12D

**QUESTION 1**: 
You are building an ML solution to identify anomalies in sensor readings from a factory. The
sensor publishes numerical data every second. What kind of data is sensor data?

**ANSWER**: B. The data is unstructured since it is not tabular. It is a time series because the sensor publishes data every second.

**QUESTION 2**: 
You are building an ML solution to identify the sentiment of news and social media feeds about a company. What kind of data is the incoming news data and what kind of ingestion use case is it?

**ANSWER**: D. The data is unstructured since it is not tabular. It is textual data and the use case is streaming as social media feeds can directly stream data into AWS or news can be streamed in by calling the news APIs

**QUESTION 8**: 
You have data incoming from a number of IoT devices that are deployed on your factory floor. You want to take the inputs from these devices and run some interactive SQL queries on the data to power a real- time dashboard as well as set up alarms to alert admins when there is an issue. What AWS streaming services can you use to build this solution?

OPTION A: Use Kinesis Firehose to ingest the data and output to ElasticSearch. Run a real- time dashboard using Kibana on top.

OPTION B: Use Kinesis Data Streams to ingest the data and use EC2 as a consumer to run SQL queries. Send the outputs to these queries to a custom dashboard application.

OPTION C: Ingest streaming data with Kinesis Data Streams but use Kinesis Data Analytics to run SQL queries over windowed streaming data. Create alerts on the incoming data stream as well. Send the outputs to Kinesis Data Streams to output to a DynamoDB table. Build your dashboard on the DynamoDB table.

OPTION D: Ingest the data into S3 using S3 copy APIs. Use Amazon Athena to run SQL queries on the S3 data and send the outputs to a custom dashboard built using QuickSight.

**ANSWER**: C. Option A does not work since you cannot run custom SQL queries or alarms on Kinesis Firehose. 
Option D does not work because this is a streaming data use case and S3 copy is not a good solution for ingesting streaming data into AWS. 
You can build a custom SQL-based database to write SQL queries on EC2, but that would be complex to build on incoming streaming data.
