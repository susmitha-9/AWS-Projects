**# Real Time Streaming**
**Objective:**
The objective of this project is to create a real-time data streaming pipeline that captures, processes, and stores data using AWS services and Snowflake. The pipeline will simulate data ingestion via Postman, process it through AWS services (API Gateway, Lambda, Kinesis, Firehose, and S3), and utilize Snowflake features such as Snowpipe for seamless data integration into the Snowflake environment.

<img width="663" height="215" alt="image" src="https://github.com/user-attachments/assets/7a37c6a6-53f3-4747-8cd8-1f7a0e19b1fb" />

**Architecture Overview:**
1. Data Ingestion:
Simulate data generation using Postman to send HTTP POST requests to AWS API Gateway.

2. Data Processing:
API Gateway acts as the entry point for the data, validating and routing the incoming requests.
API Gateway triggers an AWS Lambda function, which processes the data by checking if the format of the data is as expected and forwards it to Amazon Kinesis, else write the incorrect data to error bucket

3. Data Streaming and Storage:
Amazon Kinesis Data Streams captures the real-time stream of data.
Kinesis Firehose delivers the data from the stream to an S3 data bucket for long-term storage in a structured format JSON

4. Snowflake Integration:
Use Snowpipe, Snowflake’s data ingestion feature, to continuously ingest data from the S3 bucket into Snowflake tables.

**Deployment Steps:**
1. Setup an IAM role and policy : Create an AWS IAM policy which will be used by APU gateway and lambda to write the data to the respective AWS services

2. Provision S3 Bucket: Create two S3 buckets(data and error) and define folder structures for data storage.

3. Configure Kinesis Stream: Set up Kinesis Data Streams and Firehose for data streaming and delivery.

4. Create Lambda Function: Write and deploy a Lambda function to process the incoming data to check the format of the data and process them accordingly to Kinesis or S3 error bucket

5. Set up API Gateway: Configure an endpoint to accept HTTP POST requests.

6. Enable Snowpipe in Snowflake: Configure Snowpipe to monitor the S3 bucket and ingest data automatically.

7. Test with Postman: Simulate data ingestion by sending test payloads via Postman.

8. Validate Data Flow: Ensure the data flows through all components and is queryable in Snowflake.
