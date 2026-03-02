# ☁️ AWS File Backup Automation using Lambda and S3 (INT 330 Project)

## 📌 Project Overview

This project demonstrates an automated file backup system using **Amazon Web Services (AWS)**. The system automatically copies files from a primary S3 bucket to a backup S3 bucket whenever a new file is uploaded.

This automation is achieved using **AWS Lambda**, **Amazon S3 Event Notifications**, and **CloudWatch Logs**, ensuring secure, reliable, and real-time backup without manual intervention.

This project was developed as part of the **INT 330: Cloud Computing** course.

---

## 🎯 Objectives

* To understand cloud storage using Amazon S3
* To implement serverless computing using AWS Lambda
* To automate file backup using event-driven architecture
* To monitor system activity using CloudWatch

---

## 🛠️ Technologies Used

* Amazon S3
* AWS Lambda
* Python 3.12
* AWS CloudWatch
* AWS Management Console

---

## 🏗️ Architecture

```
User Upload File
        ↓
Primary S3 Bucket
        ↓
S3 Event Notification
        ↓
AWS Lambda Function
        ↓
Backup S3 Bucket
```

---

## ⚙️ Project Components

### 1️⃣ Primary Bucket

* Name: `my-primary-files-bucket`
* Stores original uploaded files

### 2️⃣ Backup Bucket

* Name: `my-backup-files-bucket`
* Stores automatically backed-up files

### 3️⃣ Lambda Function

* Name: `FileBackupFunction`
* Runtime: Python 3.12
* Function: Copies files from primary bucket to backup bucket

---

## 💻 Lambda Function Code

```python
import json
import boto3

s3 = boto3.client('s3')

def lambda_handler(event, context):

    source_bucket = event['Records'][0]['s3']['bucket']['name']

    file_key = event['Records'][0]['s3']['object']['key']

    destination_bucket = 'my-backup-files-bucket'

    copy_source = {
        'Bucket': source_bucket,
        'Key': file_key
    }

    s3.copy_object(
        CopySource=copy_source,
        Bucket=destination_bucket,
        Key=file_key
    )

    return {
        'statusCode': 200,
        'body': 'File backed up successfully'
    }
```

---

## 🚀 How It Works

1. User uploads file to primary bucket
2. S3 triggers Lambda function
3. Lambda copies file to backup bucket
4. Backup is completed automatically
5. Logs are generated in CloudWatch

---

## 📊 Output

* Files uploaded to primary bucket are automatically copied to backup bucket
* Backup process is fast and reliable
* No manual work required

---

## 📸 Screenshots

Include screenshots of:

* Lambda Function
* S3 Buckets
* Event Notification
* Backup Result
* CloudWatch Logs

---

## 📚 Learning Outcomes

* Learned cloud storage concepts
* Learned serverless computing
* Learned event-driven architecture
* Learned AWS services integration

---

## 🔮 Future Improvements

* Add email notification
* Add file versioning
* Add encryption
* Add web interface

---

## 👨‍💻 Author

**Abhishek Kumar**

B.Tech Computer Science and Engineering
Lovely Professional University

---

## 📖 Course

INT 330 – Cloud Computing

---

## ⭐ Conclusion

This project successfully demonstrates an automated file backup system using AWS cloud services. It reduces manual work and ensures data safety using serverless architecture.
