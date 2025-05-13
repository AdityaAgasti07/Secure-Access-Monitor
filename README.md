# SecureAccessMonitor 🚨🔐  
**Real-Time Secret Access Monitoring System Using AWS Secret, CloudTrail, CloudWatch & SNS**

---

## 📘 Project Overview

Ever wondered how to track who’s accessing your AWS secrets like API keys, database credentials, or configuration secrets?

**SecureAccessMonitor** is a cloud-native monitoring system that helps you detect and get alerted in real-time when someone accesses your secrets. Built using AWS **CloudTrail**, **CloudWatch**, and **SNS**, this project enhances your cloud security visibility — a must-have for DevOps, Security, and Cloud Engineers.

---

## 🎯 Key Features

- 🔍 Track secret access using **CloudTrail**
- 📊 Analyze events with **CloudWatch Logs** & **Metric Filters**
- 🔔 Trigger alerts using **SNS** (Email/Slack/etc.)
- 🔁 Bonus: Create a second notification system and compare effectiveness

---

## 🧰 AWS Services Used

- **AWS CloudTrail** – Captures API calls & events  
- **AWS CloudWatch Logs** – Stores logs and filters secret access patterns  
- **AWS CloudWatch Alarms** – Triggers based on suspicious activity  
- **AWS SNS (Simple Notification Service)** – Sends notifications to email or webhook  

---

## 🏗️ Architecture

![Screenshot 2025-05-12 114730](https://github.com/user-attachments/assets/19cf5aa4-6418-4d1b-939f-9e8e811ee433)

## 🚀 Getting Started

Follow the steps below to set up secret access monitoring using AWS CloudTrail, CloudWatch, and SNS.

---

### 0. 🛡️ Create a Secret in AWS Secrets Manager

Before setting up monitoring, create a secret in AWS Secrets Manager:

```bash
aws secretsmanager create-secret \
  --name MyApp/DBCredentials \
  --secret-string '{"username":"admin","password":"supersecure123"}'
```

### 1. 📝 Create and Enable CloudTrail
```bash
aws cloudtrail create-trail \
  --name SecretsAccessTrail \
  --s3-bucket-name your-secure-logs-bucket \
  --is-multi-region-trail

aws cloudtrail start-logging \
  --name SecretsAccessTrail
```
### 2. 🔗 Integrate CloudTrail with CloudWatch Logs
```bash
aws logs create-log-group \
  --log-group-name CloudTrail/SecretsLogs

aws cloudtrail create-subscription \
  --trail-name SecretsAccessTrail \
  --log-group-name CloudTrail/SecretsLogs \
  --role-arn arn:aws:iam::<ACCOUNT_ID>:role/CloudTrailCloudWatchLogsRole
```
### 3. 🔎 Create a Metric Filter for Secret Access
```bash
aws logs put-metric-filter \
  --log-group-name CloudTrail/SecretsLogs \
  --filter-name SecretAccessMetric \
  --metric-transformations \
      metricName=SecretAccessCount,metricNamespace=SecretsMonitor,metricValue=1 \
  --filter-pattern '{ ($.eventName = GetSecretValue) }'
```
### 4. 🚨 Set Up a CloudWatch Alarm
```bash
aws cloudwatch put-metric-alarm \
  --alarm-name SecretAccessAlarm \
  --metric-name SecretAccessCount \
  --namespace SecretsMonitor \
  --statistic Sum \
  --period 300 \
  --threshold 1 \
  --comparison-operator GreaterThanOrEqualToThreshold \
  --evaluation-periods 1 \
  --alarm-actions arn:aws:sns:<REGION>:<ACCOUNT_ID>:SecretsAlertTopic
```
### 5. 🔔 Create SNS Topic and Subscribe
```bash
aws sns create-topic \
  --name SecretsAlertTopic

aws sns subscribe \
  --topic-arn arn:aws:sns:<REGION>:<ACCOUNT_ID>:SecretsAlertTopic \
  --protocol email \
  --notification-endpoint your-email@example.com
```
### 📧 Check your email inbox and confirm the SNS subscription.
![image](https://github.com/user-attachments/assets/96622da5-7bbb-4a1e-a264-2bec9f46abea)

### 📷 Screenshots

#### CloudWatch Alarm triggering
![image](https://github.com/user-attachments/assets/f654aaec-564a-4f95-9e1e-edab1ec6a63d)

#### SNS Email Notification
![image](https://github.com/user-attachments/assets/cf3ad8d7-a270-44d7-899e-83d0e46cffb7)

#### CloudTrail Event Log showing secret access
![Screenshot 2025-05-13 163845](https://github.com/user-attachments/assets/a6b22bdb-b5e1-49d0-9550-c1c1317c99b7)

## 🎓 Learning Outcomes
✅ Master the AWS Monitoring and Alerting Stack
✅ Learn to detect and respond to secret access events
✅ Build scalable, real-time, secure alerting systems

## 🧩 Useful Resources
🔗 AWS CloudTrail Documentation

🔗 CloudWatch Logs & Metrics

🔗 AWS SNS Setup Guide


