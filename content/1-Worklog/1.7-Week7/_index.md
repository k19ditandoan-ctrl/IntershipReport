---
title: "Week 7 Worklog"
date: 2026-02-22
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### OBJECTIVES IN WEEK 7:
- Finalize and optimize the Solution Architecture based on Mentor's feedback.
- Master In-memory Caching services with Amazon ElastiCache (Redis): Cluster creation, CLI/SDK connection, and data manipulation.
- Complete and submit the final project Proposal to GitHub.
- Practice Advanced Networking: Transit Gateway, Site-to-Site VPN (with Cisco CSR), ECMP Routing, and Hybrid DNS with Route 53.

### TASKS OF WEEK 7:

| Day | Task | Start Date | End Date | References |
|:---:|---|:---:|:---:|---|
| **Mon** | **- Receive feedback on project solution architecture from FCJ mentors**<br>**- Listen and refine architecture based on feedback** | 23/02/2026 | 23/02/2026 | |
| **Tue** | **- Practice Lab 16: Amazon ElastiCache - Redis**<br>+ Introduction<br>+ Preparation<br>* Create AWS Access Key<br>* Install AWS CLI<br>* Configure AWS CLI<br>+ Create ElastiCache cluster<br>* Create subnet group (Console/AWS CLI)<br>* Create cluster (cluster mode disabled) (Console/AWS CLI)<br>* Create cluster (cluster mode enabled)<br>* Grant access to cluster<br>* Connect to cluster node<br>Cluster Mode Disabled<br>Cluster Mode Enabled<br>Endpoints use AWS CLI<br>* Delete cluster (Console/AWS CLI) | 24/02/2026 | 24/02/2026 | [Lab 16 Intro](https://000061.awsstudygroup.com/vi/1-introduce/)<br>[Prereq](https://000061.awsstudygroup.com/vi/2-prerequiste/)<br>[Redis Lab](https://000061.awsstudygroup.com/vi/3-amazonelasticacheforredis/) |
| **Wed** | **- Continue Lab 16: Amazon ElastiCache - Redis**<br>+ Use AWS SDK to read/write data on ElastiCache<br>* Create Elasticache cluster<br>Create a cluster (mode disabled cluster)<br>Create a cluster (mode enabled cluster)<br>Check user group<br>* Connect to Elasticache<br>Connect to a cluster (mode disabled cluster)<br>Connect to a cluster (mode enabled cluster)<br>* Set and Get strings<br>* Set and Get a hash with multiple items<br>* Publish (write) and subscribe (read)<br>* Write and read from a stream<br>+ Resource Cleanup | 25/02/2026 | 25/02/2026 | [SDK Redis](https://000061.awsstudygroup.com/vi/4-sdkelasticache/)<br>[Cleanup](https://000061.awsstudygroup.com/vi/5.cleanupresource/) |
| **Thu** | **- Finalize proposal, deploy to GitHub, and submit proposal** | 26/02/2026 | 26/02/2026 | |
| **Fri** | **- Practice Lab 17: AWS Networking and Content Delivery**<br>+ Introduction<br>+ Preparation Steps<br>* Deploy VPC<br>* Cisco CSR Agreement<br>+ VPC Components Deep Dive<br>+ Transit Gateway and Site-to-Site VPNs<br>* Transit Gateway and Site-to-Site VPNs<br>* Access Cisco CSR Router with Cloud9<br>* Setup Site-to-site VPN<br>* Add ECMP Path<br>* Transit Gateway Routing<br>+ Route53 DNS Endpoints and Internal Hosted Zones<br>* Deploy DNS<br>* Test DNS | 27/02/2026 | 27/02/2026 | [Lab 17 Intro](http://000092.awsstudygroup.com/vi/1-introduce/)<br>[VPC Deep Dive](https://000092.awsstudygroup.com/vi/3-vpcs/)<br>[TGW & VPN](https://000092.awsstudygroup.com/vi/4-transitgatewayandvpn/)<br>[Route53](https://000092.awsstudygroup.com/vi/5-route53/) |

### ACHIEVEMENTS IN WEEK 7:
1. Project Solution Architecture solidified and optimized following in-depth feedback from Mentors.
2. Completed Lab 16: Mastered Amazon ElastiCache (Redis), practiced Cluster creation, connection, and advanced data manipulation (Pub/Sub, Stream) via AWS SDK.
3. Project Proposal finalized, packaged, and successfully submitted to the GitHub Repository.
4. Completed Lab 17: Deployed complex network models using Transit Gateway connecting VPN with Cisco CSR Routers, configured ECMP routing and Hybrid DNS resolution with Route 53.