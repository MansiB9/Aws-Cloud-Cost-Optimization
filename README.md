# AWS Cloud Cost Optimization - Identifying Stale Resources  

## Introduction  
Optimizing costs on AWS is crucial for managing cloud expenses efficiently. This project focuses on identifying and removing stale **Elastic Block Store (EBS) snapshots** that are no longer associated with any active EC2 instances, thereby reducing unnecessary storage costs.  

## Problem  
Sometimes, developers create EC2 instances with volumes attached to them by default. For backup purposes, these developers also create snapshots. However, when they no longer need the EC2 instance and decide to terminate it, they sometimes forget to delete the snapshots created for backup. As a result, they continue to be charged for these unused snapshots, even though they are not actively using them.  

## Solution  
We're using AWS to save money on storage costs. We made a **smart Lambda function** that looks at our snapshots and EC2 instances. If Lambda finds a snapshot that isn't connected to any active EC2 instance, it **deletes it to save costs**. This helps us **optimize AWS storage expenses**.

## Components  

### **AWS Lambda**  
- **Description:** AWS Lambda is a serverless compute service that runs your code in response to events and automatically manages the underlying compute resources.  
- **Function:** The Lambda function in this project identifies stale EBS snapshots and deletes them.  

### **Amazon EC2**  
- **Description:** Amazon Elastic Compute Cloud (EC2) provides scalable computing capacity in the cloud.  
- **Function:** EC2 instances' data is used to determine whether associated EBS snapshots are still in use.  

## How It Works  

### **1. Snapshot Identification (Data Collection)**  
- **Setup:** The Lambda function fetches all EBS snapshots owned by your account.  
- **Example:** Snapshots that were created for EC2 instances that are no longer active or needed.  

### **2. Snapshot Validation**  
- **Active Instance Check:** The function cross-references the snapshots with active (running or stopped) EC2 instances.  
- **Example:** If a snapshot’s associated volume is not linked to any active EC2 instance, it's considered stale.  

### **3. Snapshot Deletion**  
- **Automated Cleanup:** The function deletes the identified stale snapshots to free up storage space and reduce costs.  
- **Real-Time Processing:** This process can be scheduled to run periodically, ensuring ongoing cost optimization.  

## Summary  
✅ **Lambda Function** fetches all EBS snapshots and identifies stale ones.  
✅ **Active Instance Check** ensures that only necessary snapshots are retained.  
✅ **Automated Deletion** removes unused snapshots, optimizing your AWS storage costs.  
