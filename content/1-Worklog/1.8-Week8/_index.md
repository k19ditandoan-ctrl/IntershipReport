---
title: "Week 8 Worklog"
date: 2026-03-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### OBJECTIVES IN WEEK 8:
- Master Advanced Networking skills: VPC Endpoints (PrivateLink), VPC Peering, and centralized management with Transit Gateway Network Manager.
- Practice deploying a real-world Web Application (WordPress) with High Availability architecture (ASG, ALB, RDS, CloudFront).
- Master "Infrastructure as Code" (IaC) concepts using AWS CloudFormation for automated infrastructure provisioning.
- Finalize UI/UX design and Database structure for the team project.

### TASKS OF WEEK 8:

| Day | Task | Start Date | End Date | References |
|:---:|---|:---:|:---:|---|
| **Mon** | **- Team Project Meeting: Define UI/UX design direction, preliminary database design, data collection plan** | 02/03/2026 | 02/03/2026 | |
| **Tue** | **- Continue Lab 17 Practice:**<br>+ VPC Endpoints for AWS Services<br>* Deploy VPC Endpoint<br>* Check VPC Endpoint<br>+ VPC Endpoint Services<br>* Deploy VPC Endpoint Services<br>+ VPC Peering<br>* VPC Peering Request<br>* Routing Configuration<br>* Check VPC Peering<br>+ Transit Gateway Network Manager<br>* Setup Network Manager<br>* Configure Site<br>* Network Insights<br>+ Resource Cleanup | 03/03/2026 | 03/03/2026 | [VPC Endpoint](https://000092.awsstudygroup.com/vi/6-vpcendpointaws/)<br>[PrivateLink](https://000092.awsstudygroup.com/vi/7-vpcendpointonpremise/)<br>[Peering](https://000092.awsstudygroup.com/vi/8-vpcpeering/)<br>[Network Manager](https://000092.awsstudygroup.com/vi/9-transitgatewaynetworkmanager/) |
| **Wed** | **- Practice Lab 18: Deploy Wordpress on AWS Cloud**<br>+ Introduction<br>+ Preparation Steps<br>* Prepare VPC and Subnet<br>* Create Security Group for EC2<br>* Create Security Group for Database Instance<br>* Launch EC2 Instance<br>* Launch Database Instance<br>+ Install WordPress on EC2<br>+ Setup Autoscaling for WordPress Instance<br>* Create AMI from Webserver Instance<br>* Create Launch Template<br>* Create Target Group<br>* Create Load Balancer<br>* Create Auto Scaling Group<br>+ Database Backup and Restore<br>* Create DB snapshot<br>* Restore from DB snapshot<br>+ Setup Cloudfront for Web Server<br>+ Resource Cleanup | 04/03/2026 | 04/03/2026 | [Lab 18 Intro](https://000101.awsstudygroup.com/vi/1-introduce/)<br>[Install WP](https://000101.awsstudygroup.com/vi/3-installwordpressonec2/)<br>[ASG Setup](https://000101.awsstudygroup.com/vi/4-asgforec2/)<br>[CloudFront](https://000101.awsstudygroup.com/vi/6-createcloudfront/) |
| **Thu** | **- Team Project Meeting: Proceed with data collection according to preliminary database design** | 05/03/2026 | 05/03/2026 | |
| **Fri** | **- Practice Lab 19: AWS CloudFormation**<br>+ Introduction<br>+ Preparation Steps<br>* Create IAM User<br>* Create IAM Role<br>+ CloudFormation Basics<br>* Create Workspace<br>* Create CloudFormation Template<br>+ CloudFormation Advanced<br>* Custom Resources<br>Create Lambda Function<br>Create Stack<br>Connect EC2 Instance<br>* Mappings and Stacksets<br>* Drift Detection<br>+ Resource Cleanup | 06/03/2026 | 06/03/2026 | [Lab 19 Intro](https://000037.awsstudygroup.com/vi/1-introduce/)<br>[CF Basic](https://000037.awsstudygroup.com/vi/3-cloudformationbasic/)<br>[CF Advanced](https://000037.awsstudygroup.com/vi/4-cloudformationadvance/) |

### ACHIEVEMENTS IN WEEK 8:
1. Successfully implemented secure network connections: VPC Endpoints (internal access to AWS services) and VPC Peering (inter-VPC connection).
2. Built a complete WordPress system with Auto Scaling capabilities, Load Balancing (ALB), and Global Content Delivery (CloudFront).
3. Mastered the RDS Database Backup & Restore process via Snapshots in a practical scenario.
4. Proficiently used AWS CloudFormation to write Templates (Infrastructure as Code), manage Stacks, and detect configuration changes (Drift Detection).
5. Unified the UI/UX design and initiated the standardized data collection process for the team project.