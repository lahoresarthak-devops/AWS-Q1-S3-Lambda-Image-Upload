\# 🚀 AWS Q1 – Serverless Image Upload Workflow



This project demonstrates a \*\*serverless image-upload workflow\*\* built entirely using AWS services.



When an image is uploaded to an \*\*Amazon S3 bucket\*\*, an \*\*ObjectCreated event\*\* automatically triggers an \*\*AWS Lambda function\*\*. The Lambda function extracts the uploaded object's details and records the execution information in \*\*Amazon CloudWatch Logs\*\*.



\---



\## 📌 Features Included



1\. 📦 Amazon S3 bucket for image storage

2\. ⚡ Automatic Lambda invocation using an S3 ObjectCreated event

3\. 🔍 Extraction of uploaded object details

4\. 📊 Execution logging using Amazon CloudWatch Logs

5\. 🔐 AWS IAM execution permissions

6\. 🧪 End-to-end testing using a sample image

7\. 📸 Configuration and testing screenshots

8\. 🏗️ Serverless event-driven AWS architecture



\---



\## ☁️ AWS Services Used



| Service | Purpose |

|---|---|

| 🪣 Amazon S3 | Stores uploaded images and generates ObjectCreated events |

| ⚡ AWS Lambda | Processes the S3 event and extracts object details |

| 📊 Amazon CloudWatch Logs | Stores Lambda execution logs |

| 🔐 AWS IAM | Provides required Lambda execution permissions |



\---



\## 🏗️ Architecture



```text

&#x20;                        👤 User

&#x20;                          |

&#x20;                          | Upload Image

&#x20;                          v

&#x20;               +----------------------+

&#x20;               |      Amazon S3       |

&#x20;               |     Image Bucket     |

&#x20;               +----------------------+

&#x20;                          |

&#x20;                          | ObjectCreated Event

&#x20;                          v

&#x20;               +----------------------+

&#x20;               |      AWS Lambda      |

&#x20;               |  Q1-S3-Image-Logger  |

&#x20;               +----------------------+

&#x20;                          |

&#x20;                          | Execution Logs

&#x20;                          v

&#x20;               +----------------------+

&#x20;               |   Amazon CloudWatch  |

&#x20;               |        Logs          |

&#x20;               +----------------------+





🔄 Project Workflow



The complete workflow works as follows:



1\. User uploads an image

&#x20;         ↓

2\. Image is stored in Amazon S3

&#x20;         ↓

3\. S3 generates ObjectCreated event

&#x20;         ↓

4\. Event automatically invokes AWS Lambda

&#x20;         ↓

5\. Lambda extracts object details

&#x20;         ↓

6\. Execution details are written to CloudWatch Logs

&#x20;         ↓

7\. Logs are verified for successful execution



⚡ AWS Lambda Configuration

Function Name

Q1-S3-Image-Logger

Runtime

Python

Trigger

Amazon S3 – ObjectCreated Event

Function Purpose



The Lambda function receives the S3 event and extracts information about the uploaded object.



The function records:



Event Name

Event Time

Bucket Name

Object Key / File Name

Object Size

ETag

Lambda Request ID



AWS Lambda Configuration

Function Name



Q1-S3-Image-Logger



Runtime



Python



Trigger



Amazon S3 ObjectCreated Event



Purpose



The Lambda function receives the S3 event, extracts the uploaded object's information, and records the execution details in CloudWatch Logs.





📊 CloudWatch Logs



Amazon CloudWatch Logs is used to monitor and verify Lambda execution.



The Lambda function records information such as:



===== LAMBDA EXECUTION STARTED =====



Request ID: <Lambda Request ID>



\----- UPLOADED OBJECT DETAILS -----



Event Name : ObjectCreated:Put

Event Time : <Event Time>

Bucket     : q1-s3-lambda-image-upload-2026

Object Key : test\_IMAGE.png

Object Size: 2131399 bytes

ETag       : <ETag>



===== LAMBDA EXECUTION COMPLETED =====



The CloudWatch log confirms that the Lambda function was automatically invoked after the image upload.



🧪 Testing

Test File

&#x20;    

test\_IMAGE.png



Testing Procedure



1. Open the Amazon S3 bucket.
2. Upload test\_IMAGE.png.
3. Verify that the image appears in the bucket.
4. Verify the S3 trigger connected to the Lambda function.
5. Wait for the S3 ObjectCreated event.
6. Verify that Lambda was invoked.
7. Open Amazon CloudWatch Logs.
8. Open the latest log stream.
9. Verify the uploaded object's information.
10. Confirm successful Lambda execution.



📸 Screenshots


### 1️⃣ S3 Bucket Configuration

![S3 Bucket Configuration](screenshot/01-s3-bucket.png)


### 2️⃣ Image Uploaded to S3 Bucket

![Image Uploaded to S3](screenshot/02-image-upload.png)


### 3️⃣ AWS Lambda Function Configuration

![Lambda Function Configuration](screenshot/03-lambda-function.png)


### 4️⃣ Lambda Function Code

![Lambda Function Code](screenshot/04-lambda-code.png)


### 5️⃣ S3 Trigger Configuration

![S3 Trigger Configuration](screenshot/05-s3-trigger.png)


### 6️⃣ CloudWatch Execution Logs

![CloudWatch Execution Logs](screenshot/06-cloudwatch-logs.png)





📁 Project Structure

AWS-Q1-S3-Lambda-Image-Upload/

│

├── architecture/

│   └── architecture.md

│

├── screenshot/

│   ├── 01-s3-bucket.png

│   ├── 02-image-upload.png

│   ├── 03-lambda-function.png

│   ├── 04-lambda-code.png

│   ├── 05-s3-trigger.png

│   └── 06-cloudwatch-logs.png

│

├── lambda\_function.py

└── README.md

