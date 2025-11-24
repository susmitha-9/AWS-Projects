# AWS Data Migration Service (DMS) Project — MySQL → S3 Data Ingestion
**Overview:**
This project demonstrates end-to-end data ingestion and replication using AWS Database Migration Service (DMS) to migrate data from an Amazon RDS MySQL database to an Amazon S3 data lake in Parquet format. It covers the full setup of AWS resources, IAM roles, and replication tasks for real-time Change Data Capture (CDC) and full-load migration. 

**Architecture:**
Source: Amazon RDS (MySQL)
Target: Amazon S3 Bucket (Parquet files)
Migration Tool: AWS DMS
Supporting Services: IAM | AWS Secrets Manager | CloudWatch

**Step-by-Step Implementation:**
1. Create and Configure RDS Instance
Launched an RDS MySQL instance with public access enabled. Created a custom DB parameter group and attached it to the instance. Verified connectivity through MySQL Workbench. Created a database retail containing tables: customers, products, orders, etc.

2. Set Up S3 and IAM Roles:
Created an S3 bucket to serve as the target storage. Created an IAM role granting DMS access to S3 and CloudWatch logs. Attached appropriate policies (AmazonS3FullAccess, CloudWatchLogsFullAccess, AWSDatabaseMigrationServiceRole).

3. Provision AWS DMS Replication Instance:
Opened AWS DMS console → Replication Instances → Create. Configured instance size and networking (VPC & subnet groups). Verified IAM role permissions to allow DMS to write logs to CloudWatch.

4. Create Endpoints:
Source Endpoint (MySQL): Selected RDS instance as source. Configured connection settings (host, port, database, user). Created AWS Secrets Manager entry for credentials. Attached IAM role with Secrets Manager access. Tested connection successfully.

Target Endpoint (S3): Selected S3 bucket as target. Configured endpoint settings:
Data format: Parquet
Enable CDC path: (/full-load/ vs /cdc/)
Partitioning: Enabled for data distinction
Attached same IAM role used for DMS access. Tested connection successfully.

5. Create and Run Replication Task:
Task type: Migrate Existing Data and Replicate Ongoing Changes (Full Load + CDC). Selected source and target endpoints from above. Defined table mappings (selection & transformation rules). Ran Pre-Migration Assessment to validate endpoints and schemas. Started the task and monitored progress through DMS Console → Task Logs.

6. Monitor and Validate Data Replication
CloudWatch Logs: Tracked migration and CDC status.
S3 Bucket: Verified data folders (full-load and cdc).
Validated CDC files via timestamp-based inserts in MySQL source and viewed updated Parquet files in S3.

**Results:**
1. Achieved real-time replication between MySQL and S3.
2. Data successfully ingested in Parquet format with CDC tracking.
3. Ensured high data integrity through pre-migration validation and CloudWatch monitoring.

