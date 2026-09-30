# AWS Q1 – S3 + Lambda Image Upload Architecture

## 1. Project Overview

This project implements a serverless image-upload workflow using Amazon S3, AWS Lambda, and Amazon CloudWatch Logs.

When an image is uploaded to the S3 bucket, an `ObjectCreated` event automatically triggers the Lambda function. The Lambda function extracts information about the uploaded object and records the execution details in CloudWatch Logs.

---

## 2. Architecture Diagram

```text
                    ┌─────────────────────┐
                    │        User         │
                    │   Uploads Image     │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │     Amazon S3       │
                    │                     │
                    │ q1-s3-lambda-       │
                    │ image-upload-2026   │
                    └──────────┬──────────┘
                               │
                    ObjectCreated Event
                               │
                               ▼
                    ┌─────────────────────┐
                    │     AWS Lambda      │
                    │                     │
                    │ Q1-S3-Image-Logger  │
                    └──────────┬──────────┘
                               │
                  Execution Information
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Amazon CloudWatch   │
                    │       Logs          │
                    │                     │
                    │ Event details       │
                    │ Object details      │
                    │ Request ID          │
                    │ Execution status    │
                    └─────────────────────┘
```

---

## 3. AWS Services Used

| AWS Service | Purpose |
|---|---|
| Amazon S3 | Stores uploaded image files |
| AWS Lambda | Automatically processes the S3 upload event |
| Amazon CloudWatch Logs | Stores Lambda execution and object details |
| AWS IAM | Provides permissions between AWS services |

---

## 4. Architecture Components

### Amazon S3

**Bucket Name:** `q1-s3-lambda-image-upload-2026`

Amazon S3 is used as the object storage service. The uploaded image is stored inside the bucket.

The S3 bucket is configured to trigger the Lambda function whenever a new object is created.

### AWS Lambda

**Function Name:** `Q1-S3-Image-Logger`

The Lambda function is responsible for:

- Receiving the S3 event.
- Reading the S3 event record.
- Extracting the bucket name.
- Extracting the uploaded object key.
- Extracting object size.
- Extracting the ETag.
- Recording the event time and event name.
- Recording the Lambda request ID.
- Printing the information to CloudWatch Logs.

### Amazon CloudWatch Logs

CloudWatch Logs is used to verify that the Lambda function executed successfully.

The logs contain information such as:

- Event Name
- Event Time
- Bucket Name
- Object Key
- Object Size
- ETag
- Lambda Request ID
- Execution completion status

---

## 5. Event Flow

The complete workflow is:

1. The user uploads an image to the Amazon S3 bucket.
2. Amazon S3 detects the new object.
3. S3 generates an `ObjectCreated:Put` event.
4. The S3 event automatically invokes the AWS Lambda function.
5. Lambda receives the event information.
6. Lambda extracts the uploaded object's details.
7. Lambda writes the execution information to Amazon CloudWatch Logs.
8. The execution is verified using the CloudWatch log stream.

---

## 6. Example Test

### Uploaded Object

- **Bucket:** `q1-s3-lambda-image-upload-2026`
- **Object:** `test_IMAGE.png`
- **Event:** `ObjectCreated:Put`
- **Object Size:** `2131399 bytes`

The Lambda function successfully processed the S3 event and recorded the uploaded object details in CloudWatch Logs.

---

## 7. Serverless Architecture

This solution follows an event-driven serverless architecture.

```text
User
  │
  │ Upload Image
  ▼
Amazon S3
  │
  │ ObjectCreated Event
  ▼
AWS Lambda
  │
  │ Execution Logs
  ▼
Amazon CloudWatch Logs
```

There is no need to manage a continuously running server for the image-processing workflow. Lambda runs when the S3 event occurs.

---

## 8. Security

The S3 bucket is configured with public access blocked.

The architecture uses AWS IAM permissions so that the required AWS services can interact securely.

No public access to the uploaded image is required for this project.

---

## 9. Project Objective

The objective of this implementation is to demonstrate:

- Amazon S3 object storage
- S3 event notifications
- AWS Lambda event-driven execution
- Serverless architecture
- CloudWatch monitoring and logging
- Basic AWS IAM service permissions

---

## 10. Final Architecture Summary

The final architecture consists of four main AWS components:

**User → Amazon S3 → AWS Lambda → Amazon CloudWatch Logs**

The user uploads an image to S3. The upload generates an `ObjectCreated` event, which invokes the Lambda function. Lambda extracts the uploaded object's information and records the execution details in CloudWatch Logs.

This completes the serverless image-upload and logging workflow required for Question 1 of the AWS project assignment.
