---
title: "Week 4 Worklog"
date: 2026-01-25
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### OBJECTIVES IN WEEK 4:
- Master Amazon EC2 services: Instance lifecycle management, Custom AMI creation, Troubleshooting, and Data recovery.
- Practice deploying real-world web applications (LAMP stack, Node.js) on both Linux and Windows environments.
- Deeply understand Storage services (S3, Storage Gateway) and the Shared Responsibility Model.
- Master core security services: IAM, Cognito, AWS Organization, and KMS.

### TASKS OF WEEK 4:

| Day | Task | Start Date | End Date | References |
|:---:|---|:---:|:---:|---|
| **Mon** | **- Practice Lab 9: Amazon Elastic Compute Cloud (EC2)**<br>+ Introduction<br>+ Preparation Steps:<br>* Create VPC Linux<br>* Create VPC Windows<br>* Create Security Group Linux<br>* Create Security Group Windows<br>+ Launch Windows instance<br>* Create Windows Instance<br>* Connect to Windows instance<br>+ Launch Linux instance<br>* Create Linux instance<br>* Connect Linux instance<br>+ Amazon EC2 Basics<br>* Change EC2 Configuration (Resize)<br>* Create EC2 snapshot<br>* Create Custom AMI<br>* Launch instance from custom AMI<br>* Access EC2-Windows when Key Pair is lost via SSM<br>* Access EC2-Linux when Key Pair is lost via User Data<br>* Configure Desktop Interface for EC2-Ubuntu 22.04<br>* Amazon EBS Snapshots Archive<br>* Share AMI | 26/01/2026 | 26/01/2026 | [Lab 9 Intro](https://000004.awsstudygroup.com/vi/1-introduce/)<br>[Lab 9 Prereq](https://000004.awsstudygroup.com/vi/2-prerequiste/)<br>[Launch Windows](https://000004.awsstudygroup.com/vi/3-launchwindowsinstance/)<br>[Launch Linux](https://000004.awsstudygroup.com/vi/4-launchlinuxinstance/)<br>[EC2 Basic](https://000004.awsstudygroup.com/vi/5-amazonec2basic/) |
| **Tue** | **- Continue Lab 9:**<br>+ Deploy Node.js Application on Amazon Linux<br>* Install LAMP web server (Prepare, Check, Config DB, install phpMyAdmin)<br>* Install Node.js on Linux<br>* Deploy application on Linux Instance<br>+ Node.js Application on Amazon EC2 Windows<br>* Install XAMPP on Windows instance<br>* Install Node.js on Windows instance<br>* Deploy application on Windows instance<br>+ Resource Usage Governance via IAM<br>* Allow service usage by specific Region<br>* Limit EC2 usage by Instance Family<br>* Limit EC2 usage by Instance type<br>* Limit EBS volume storage type<br>* Limit resource deletion by Corporate IP address<br>* Limit resource deletion by Time period<br>+ Resource Cleanup | 27/01/2026 | 27/01/2026 | [Linux App](https://000004.awsstudygroup.com/vi/6-awsfcjmanagement-linux/)<br>[Windows App](https://000004.awsstudygroup.com/vi/7-awsfcjmanagement-windows/)<br>[Governance](https://000004.awsstudygroup.com/vi/8-costusagegovernance/)<br>[Cleanup](https://000004.awsstudygroup.com/vi/9-cleanup/) |
| **Wed** | **- Study Module 04: Storage Services on AWS:**<br>+ 04-01: Amazon Simple Storage Service (S3) - Access Point - Storage Class<br>+ 04-02: S3 Static Website & CORS - Control Access - Object Key & Performance - Glacier<br>+ 04-03: Snow Family - Storage Gateway - Backup | 28/01/2026 | 28/01/2026 | [04-01](https://youtu.be/_yunukwcAwc?si=6HqDHVQJq8Ks9aWh)<br>[04-02](https://youtu.be/mPBjB6Ltl_Q?si=OITIt1x3d7OZ4ei_)<br>[04-03](https://www.youtube.com/watch?v=YXn8Q_Hpsu4) |
| **Thu** | **- Attend Event: AWS re:Invent re:Cap Vietnam — HCMC 2025** | 29/01/2026 | 29/01/2026 | |
| **Fri** | **- Study Module 05: Security Services on AWS:**<br>+ 05-01: Shared Responsibility Model<br>+ 05-02: Amazon Identity and access management<br>+ 05-03: Amazon Cognito<br>+ 05-04: AWS Organization<br>+ 05-05: AWS Identity Center<br>+ 05-06: Amazon Key Management Service<br>+ 05-07: AWS Security Hub | 30/01/2026 | 30/01/2026 | [05-01](https://youtu.be/tsobAlSg19g?si=-xSAVT8MZReV10RP)<br>[05-02](https://youtu.be/N_vlJGAqZxo?si=KxeWofBCdviRYax1)<br>[05-03](https://youtu.be/pZ2fgEFK3Vs?si=QWkbW4avA9wlvlhP)<br>[05-04](https://youtu.be/5oQY8Rogz9Y?si=WK72gwmztbXWQVKr)<br>[05-05](https://youtu.be/NW1xrMkNMjU?si=Owp-3CDDmW7YYTY4)<br>[05-06](https://youtu.be/GMihNQojhZc?si=Bt4oUqD2a5_IA0mm)<br>[05-07](https://youtu.be/clj2E0rNBEs?si=eUp1O-14XFDbpbbe) |

### ACHIEVEMENTS IN WEEK 4:
1. Comprehensively completed Lab 9: Mastered advanced EC2 administration tasks (Resize, Snapshot, Custom AMI, Recovery Access).
2. Successfully deployed real-world applications (LAMP Stack, Node.js) on EC2 Linux and Windows infrastructure.
3. Practiced Cost and Governance by limiting resource creation rights by Region, Instance Type, and Time via IAM Policy.
4. Mastered Module 04 knowledge on data storage solutions (S3, Glacier, Storage Gateway) and backup strategies.
5. Systematized Module 05 knowledge on cloud security, understanding the Shared Responsibility Model and how to use security identity tools (IAM, Cognito, Identity Center).