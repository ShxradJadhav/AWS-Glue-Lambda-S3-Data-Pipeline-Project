# AWS-Glue-Lambda-S3-Data-Pipeline-Project
A complete end-to-end data pipeline built using Amazon S3, AWS Glue, and AWS Lambda, showcasing real-world ETL processing, event-driven automation, and cloud data engineering skills.



This project demonstrates how I built a serverless, automated data pipeline on AWS that converts CSV files into JSON format using Amazon S3, AWS Lambda, and AWS Glue.

The pipeline is fully event-driven—when a CSV file lands in S3, a Lambda function or Glue Job automatically transforms it.

---
📌 **Project Architecture**

Workflow:

1. Upload CSV file to input S3 bucket

2. S3 triggers Lambda or directly triggers AWS Glue

3. AWS Glue job transforms CSV → JSON

4. Output JSON stored in destination S3 bucket

5. Logs monitored via CloudWatch


Step-by-Step Implementation

Below are the exact steps I performed with screenshots from my AWS console.

---

1️⃣ Created Three S3 Buckets

I created three S3 buckets:

awss3-input-source → to upload CSV files

awss3-jsonbucket-destination → to store JSON output

awss3-scriptbucket → to store Glue scripts

📸 Screenshot: <img width="960" height="540" alt="01" src="https://github.com/user-attachments/assets/31d513f5-1e6c-4bfc-883c-30d01560da0c" />

---

2️⃣ Created AWS Glue Visual Job (CSV → JSON Transformation)

Inside AWS Glue Studio, I created a Visual ETL job with:

Source: S3 CSV file

Target: S3 JSON output

Format: CSV → JSON

The preview shows the extracted fields perfectly.

📸 Screenshot: <img width="960" height="540" alt="02" src="https://github.com/user-attachments/assets/5dbbbb7d-b3b9-45d0-a402-b9e073086999" />

---

3️⃣Lambda Function to Trigger Glue Job

Created a Lambda function named csv-to-json which automatically starts the Glue job when a new CSV file lands in S3.

✔️ Screenshot: Lambda Code
```
import json
import boto3
glueClient = boto3.client('glue')

def lambda_handler(event, context):
    glueClient.start_job_run(JobName="csv-to-json")
    return "Job started"
```
This ensures event-driven automation without manual intervention.

📸 Screenshot: <img width="960" height="540" alt="03" src="https://github.com/user-attachments/assets/09110850-ca59-4be6-a638-0d6e779449c7" />
                <img width="960" height="540" alt="04" src="https://github.com/user-attachments/assets/dc511361-1f0b-46a0-ad54-ed54c1a6141f" />


---

4️⃣ JSON Output Successfully Generated in S3

After the Glue job executed, the transformed JSON file appeared in my output bucket:

✔️ Screenshot: Output S3 Bucket <img width="960" height="540" alt="06" src="https://github.com/user-attachments/assets/849ad8cb-9d02-4a66-b0a4-37b21a5ba6ed" />


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


✔️ Screenshot: CloudWatch Logs <img width="960" height="540" alt="05" src="https://github.com/user-attachments/assets/d5f82203-7d1b-4e1a-b760-2f5a374c325c" />


Shows the Lambda execution flow with:

INIT_START

START

END

REPORT logs

<img width="960" height="540" alt="07" src="https://github.com/user-attachments/assets/1b575990-2c75-496c-8e16-e8fdc0ea253a" />




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

