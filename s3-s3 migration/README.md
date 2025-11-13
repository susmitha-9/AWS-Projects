Cross region S3-S3 migration using Lambda

Architecture Diagram:
<img width="642" height="175" alt="image" src="https://github.com/user-attachments/assets/90cad929-37e9-4cc6-b8b8-fc0264583af8" />

Used AWS S3, SNS, SQS, and Lambda to transfer a data file from an S3 bucket in the source region to an S3 bucket in the target region (your default region). Once the data is loaded into the target region's S3 bucket, SQS is used to send a notification to trigger Glue crawler to generate a table in the Glue catalog. After the table is created in the Glue catalog, leveragd AWS Athena to query the data and analyze its contents.

Implementation Steps:
1. Created S3 Buckets: Set up two S3 buckets - one in the source region to hold the data file and one in the target region (default region) for storing the transferred data.
2. Set Up SNS (Simple Notification Service): Created an SNS topic that is used to notify when a new file is uploaded to the source S3 bucket, which triggers downstream actions.
3. Created SQS Queue: Set up an SQS queue that receives notifications from SNS and trigger the Lambda function for processing the data file.
4. Developed Lambda Function: Created a Lambda function that listens to the SQS queue, moves the data file from the source S3 bucket to the target S3 bucket, and sends a notification to trigger the Glue crawler after the transfer.
5. Set Up Glue Crawler: Configured and runs the Glue crawler to scan the target S3 bucket, detect the schema, and create a table in the Glue Data Catalog.
6. Configured S3 Event Notification: Configured an S3 event in the source bucket to publish notifications to the SQS topic whenever a new file is uploaded.
7. Set Up Athena for Querying: Configured Athena to use the Glue Data Catalog and run SQL queries to analyze the data stored in the target S3 bucket.
8. Tested the Workflow: Upload a cutomer.csv file to the source S3 bucket, checked if the data is transferred correctly, and ensure that the Glue crawler ran successfully and Athena to query the data.


