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

```text
User Access → AWS Secrets Manager → CloudTrail → CloudWatch Logs 
            → Metric Filter → Alarm → SNS → Email/Slack
