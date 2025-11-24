# AWS-Glue-Lambda-S3-Data-Pipeline-Project
A complete end-to-end data pipeline built using Amazon S3, AWS Glue, and AWS Lambda, showcasing real-world ETL processing, event-driven automation, and cloud data engineering skills.



This project demonstrates how I built a serverless, automated data pipeline on AWS that converts CSV files into JSON format using Amazon S3, AWS Lambda, and AWS Glue.

The pipeline is fully event-driven—when a CSV file lands in S3, a Lambda function or Glue Job automatically transforms it.


📌 Project Architecture

Workflow:

1. Upload CSV file to input S3 bucket

2. S3 triggers Lambda or directly triggers AWS Glue

3. AWS Glue job transforms CSV → JSON

4. Output JSON stored in destination S3 bucket

5. Logs monitored via CloudWatch


Step-by-Step Implementation

Below are the exact steps I performed with screenshots from my AWS console.

1️⃣ Created Three S3 Buckets

I created three S3 buckets:

awss3-input-source → to upload CSV files

awss3-jsonbucket-destination → to store JSON output

awss3-scriptbucket → to store Glue scripts

📸 Screenshot:


2️⃣ Created AWS Glue Visual Job (CSV → JSON Transformation)

Inside AWS Glue Studio, I created a Visual ETL job with:

Source: S3 CSV file

Target: S3 JSON output

Format: CSV → JSON

The preview shows the extracted fields perfectly.

📸 Screenshot:


3️⃣Lambda Function to Trigger Glue Job

Created a Lambda function named csv-to-json which automatically starts the Glue job when a new CSV file lands in S3.

✔️ Screenshot: Lambda Code

import json
import boto3
glueClient = boto3.client('glue')

def lambda_handler(event, context):
    glueClient.start_job_run(JobName="csv-to-json")
    return "Job started"

This ensures event-driven automation without manual intervention.

📸 Screenshot:


4️⃣ JSON Output Successfully Generated in S3

After the Glue job executed, the transformed JSON file appeared in my output bucket:

✔️ Screenshot: Output S3 Bucket

Shows a generated file:

run-AmazonS3_node...-part-00000

This confirms successful ETL processing and storage.


---

5️⃣ Monitoring via CloudWatch Logs

I used Amazon CloudWatch to track:

Lambda invocation logs

Glue job execution logs

Runtime performance

Any errors/failures


✔️ Screenshot: CloudWatch Logs

Shows the Lambda execution flow with:

INIT_START

START

END

REPORT logs



---

🎯 Project Highlights

✔️ Fully serverless (no EC2, no manual execution)
✔️ Real-time event-driven ETL
✔️ Integration of S3 + Lambda + Glue
✔️ Clean automation pipeline
✔️ Follows best practices for AWS data engineering


---

📂 Use Cases

Automated data ingestion pipelines

CSV → JSON converters

Batch or real-time ETL workloads

Preprocessing for analytics and ML pipelines

