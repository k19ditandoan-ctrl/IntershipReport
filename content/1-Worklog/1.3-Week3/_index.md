---
title: "Week 3 Worklog"
date: 2026-01-18
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### OBJECTIVES IN WEEK 3:
- Master VPN troubleshooting skills and extend Site-to-Site connectivity using Transit Gateway.
- Understand and implement Hybrid DNS models using Route 53 Resolver for name resolution between On-premise and AWS.
- Master multi-VPC connectivity models (VPC Peering and Transit Gateway).
- Systematize in-depth knowledge of Compute services (EC2, AMI, EBS, Auto-scaling).

### TASKS OF WEEK 3:

| Day | Task | Start Date | End Date | References |
|:---:|---|:---:|:---:|---|
| **Mon** | **- Continue Lab 5 Practice:**<br>+ Setup AWS Site-to-Site VPN:<br>5.2 Configure VPN Connection:<br>5.2.7 VPN Troubleshooting Guide<br>5.2.8 Official AWS VPN Troubleshooting Guide<br>5.3 Configure VPN using strongSwan with Transit Gateway (Optional):<br>5.3.1 Create Customer Gateway<br>5.3.2 Create Transit Gateway<br>5.3.3 Create VPN Connection<br>5.3.4 Create Transit Gateway Attachment<br>5.3.5 Configure Route Tables<br>5.3.6 Configure Customer Gateway<br>+ Clean up Resources<br>+ Infrastructure as Code Templates | 19/01/2026 | 19/01/2026 | [Lab 5 VPN](https://000003.awsstudygroup.com/vi/5-vpnsitetosite/) |
| **Tue** | **- Team Project Meeting: Finalize idea, add expected features** | 20/01/2026 | 20/01/2026 | |
| **Wed** | **- Practice Lab 6: Setup Hybrid DNS with Route 53 Resolver**<br>+ Preparation Steps:<br>* Create Key Pair<br>* Launch CloudFormation Template<br>* Configure Security Group<br>+ Connect to RDGW<br>+ Deploy Microsoft AD<br>+ Setup DNS:<br>* Create Route 53 Outbound Endpoint<br>* Create Route 53 Resolver Rules<br>* Create Route 53 Inbound Endpoints<br>* Test Results<br>+ Clean up resources | 21/01/2026 | 21/01/2026 | [Lab 6 Prereq](https://000010.awsstudygroup.com/vi/2-prerequiste/)<br>[Connect RDGW](https://000010.awsstudygroup.com/vi/3-connecttordgw/)<br>[Setup AD](https://000010.awsstudygroup.com/vi/4-setupad/)<br>[Hybrid DNS](https://000010.awsstudygroup.com/vi/5-setuphyriddns/) |
| **Thu** | **- Practice Lab 7: Setup VPC Peering**<br>+ Preparation Steps:<br>* Launch CloudFormation Template<br>* Create Security Group<br>* Create EC2 instance<br>+ Update Network ACL<br>+ Create Peering connection<br>+ Enable Cross-Peer DNS<br>+ Clean up resources<br>**- Practice Lab 8: AWS Transit Gateway Overview**<br>+ Preparation Steps:<br>* Create Key Pair<br>* Launch CloudFormation Template<br>+ Create Transit Gateway<br>+ Create Transit Gateway Attachments<br>+ Create Transit Gateway Route Tables<br>+ Add Transit Gateway Routes to VPC Route Tables<br>+ Clean up resources | 22/01/2026 | 22/01/2026 | [Lab 7 Guide](https://000019.awsstudygroup.com/vi/)<br>[Lab 8 Guide](https://000020.awsstudygroup.com/vi/) |
| **Fri** | **- Study Module 03: Compute VM on AWS:**<br>+ 03-01: EC2 Instance Types<br>+ 03-02: AMI, Backup, Key Pair<br>+ 03-03: Elastic Block Store (EBS)<br>+ 03-04: EC2 Instance Store<br>+ 03-05: EC2 User data<br>+ 03-06: EC2 Metadata<br>+ 03-07: EC2 Auto-scaling<br>+ EFS/FSx - Lightsail - MGN | 23/01/2026 | 23/01/2026 | [03-01](https://youtu.be/-t5h4N6vfBs?si=bS-jetOxckl24fDr)<br>[03-02](https://youtu.be/e7XeKdOVq40?si=c6LTJwwQ9vmc062Z)<br>[03-03](https://youtu.be/yAR6QRT3N1k?si=HmAky53nzXizTU8U)<br>[03-04](https://youtu.be/hKr_TfGP7NY?si=flt7IPIyoey3gp7D)<br>[03-05](https://youtu.be/6IHNDJ85aoQ?si=4oT7Yvm2MdgYM5dw)<br>[03-06](https://youtu.be/_v_43Wi7zjo?si=7UPcYjyhBr5NtpZM)<br>[03-07](https://youtu.be/Ew3QRaKJQSA?si=XPJt5rZRJIJaWkM4)<br>[Other](https://youtu.be/bbLcPitXJSY?si=gDfz13c9xm7z0cP2)<br>[MGN](https://youtu.be/hFVYG8WqfU0?si=pwMJL01CuoVoxMQS) |

### ACHIEVEMENTS IN WEEK 3:
1. Completed advanced Lab 5: Learned VPN Troubleshooting and configuring VPN with Transit Gateway (StrongSwan).
2. Finalized the team project idea and defined the expected features for implementation.
3. Successfully deployed Hybrid DNS architecture (Lab 6), configuring Inbound/Outbound Endpoints for two-way domain resolution (AWS <-> On-prem).
4. Built and connected multiple VPC networks using VPC Peering (Lab 7) and AWS Transit Gateway (Lab 8).
5. Mastered Module 03 theory on Compute: Deep understanding of EC2 types, EBS storage types, and Auto-scaling mechanisms for performance and cost optimization.