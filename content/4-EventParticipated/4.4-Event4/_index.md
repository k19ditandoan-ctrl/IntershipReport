---
title: "Event 4"
date: 2026-04-04
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

# Summary Report: "Cloud Mastery Event: Infrastructure as Code"

### Event Overview

- **Event Name:** Cloud Mastery - Infrastructure as Code (IaC)
- **Date:** April 04, 2026
- **Role:** Attendee
- **Topic:** Managing infrastructure through code and tool comparisons (CloudFormation, CDK, Terraform)

This event dove deep into the Infrastructure as Code (IaC) paradigm, exploring how it reshapes the way we deploy and manage cloud infrastructure, along with practical applications and comparisons of the most popular tools available on the AWS ecosystem and multi-cloud environments.

### Detailed Session Content

#### 1. Overview of Infrastructure as Code (IaC)
**Definition:**
IaC is the practice of managing, configuring, and provisioning IT infrastructure through code instead of manual processes (ClickOps via the console).

**Core Functions:**
- Automate the creation, updating, and deletion of cloud resources.
- Deploy infrastructure in a reproducible manner across various environments.

**The Problem with the Traditional Approach (ClickOps):**
- Slow execution and time-consuming.
- Highly prone to human errors.
- Lack of consistency between environments (Dev, Test, Prod).
- Difficult to collaborate effectively or audit change history.

**Benefits of IaC:**
- **Automation:** End-to-end process automation.
- **Reproducibility:** Easily duplicate and scale environments.
- **Scalability:** Rapidly scale up or down as needed.
- **Collaboration:** Enables Ops teams to adopt software engineering practices (code reviews, version control).

#### 2. Popular IaC Tools on AWS
There are three main tools heavily utilized when working with AWS:
- **AWS CloudFormation**
- **AWS CDK (Cloud Development Kit)**
- **Terraform**

#### 3. AWS CloudFormation
**Concept:** AWS's native IaC tool that utilizes YAML or JSON to write templates. Resources are managed in groupings called **Stacks**.

**Main Components:**
- **Template:** A declarative blueprint representing the infrastructure to deploy.
- **Stack:** A collection of actual resources provisioned together as defined by the template.

**How it Works:**
- Author the template locally.
- Upload to S3 or deploy directly via AWS CLI/Console.
- Configure and deploy the stack.
- The AWS engine automatically analyzes dependencies and provisions resources accordingly.

**Configuration Drift:**
- This happens when resources are manually modified outside of CloudFormation management (via Console or CLI).
- **Drift Detection:** CloudFormation provides a feature to detect these deviations. However, it only notifies the user; the engineer must manually decide whether to update the template to match the new reality or revert the resource configuration.

#### 4. AWS CDK (Cloud Development Kit)
**Concept:** An IaC framework that lets you define cloud infrastructure using familiar programming languages (TypeScript, Python, Java, C#, Go) instead of JSON/YAML.

**Architecture:** App → Stack → Construct
Structured into **3 levels of Constructs:**
- **L1:** Direct 1-to-1 mappings to CloudFormation resources (low-level).
- **L2:** Higher-level abstractions that incorporate AWS default best-practices.
- **L3 (Patterns):** Complete, interconnected ecosystems (e.g., an Application Load Balancer combined with Fargate).

**Advantages:**
- Highly developer-friendly.
- Allows the use of programming logic (if/else, loops) and object-oriented paradigms (inheritance) for code reuse.
- Integrates smoothly with modern IDE workflows.

**Important CLI Commands:** 
`cdk init`, `cdk bootstrap`, `cdk synth`, `cdk deploy`, `cdk destroy`, `cdk diff`, `cdk drift`.

#### 5. Terraform
**Concept:** An open-source IaC tool developed by HashiCorp, utilizing HCL (HashiCorp Configuration Language). Its biggest strength is comprehensive **Multi-cloud** support (AWS, Azure, GCP, on-premise).

**Strengths:**
- State management through the **State file** (`terraform.tfstate`), allowing for precise tracking of changes.
- Highly readable and declarative configuration syntax.
- Broad coverage of cloud provider APIs.

**Standard Terraform Workflow:**
`terraform init` → `terraform validate` → `terraform plan` → `terraform apply` → `terraform destroy`.

**Standard Project Structure:**
- `main.tf`: Main resources definition.
- `variables.tf`: Input parameter definitions.
- `outputs.tf`: Output values after provisioning.
- `providers.tf`: Cloud provider configurations.

#### 6. Quick Comparison & Selection Rules

| TOOL | PRIMARY STRENGTH | RECOMMENDED USE CASE |
|---|---|---|
| **CloudFormation** | Native AWS, free, stable | 100% AWS specific projects, operations-heavy teams |
| **AWS CDK** | Programming language based, powerful abstractions | Developer-led infrastructure (DevOps), complex logic needs |
| **Terraform** | Multi-cloud support, massive provider ecosystem | Large corporate systems, cross-cloud strategy, industry standard |

**Rules for Choosing an IaC Tool:**
1. Is the business locked into a single cloud (AWS) or multi-cloud? (If multi-cloud → lean towards Terraform).
2. Is the team more Dev-oriented (prefer TypeScript) or Ops-oriented (prefer HCL/YAML)?
3. Which tool does the existing CI/CD ecosystem support better?

### Important Insights 
*(Applicable for practical system design)*

- **The Essence of IaC:** It's not just about automation; the core value proposition is bringing **Version Control to Infrastructure**, treating infrastructure reviews with the same scrutiny as code reviews.
- **The Risk of Configuration Drift:** Drift is a terrifying hidden risk in Production environments. Strict CI/CD processes paired with Drift Tracking tooling are mandatory to prohibit manual ClickOps modifications.
- **The Reality of CDK and Amplify:** CDK is essentially an abstraction layer. After you "synth" (compile) it, it generates standard CloudFormation templates. Similarly, AWS Amplify relies heavily on CloudFormation mechanisms under the hood.
- **Terraform as the Standard:** Terraform continues to assert itself as the **de facto industry standard** due to its unparalleled cross-platform capabilities.

### Event Photos

![AWS Community Day Vietnam](/images/4-Event/event4.jpg)
![AWS Community Day Vietnam](/images/4-Event/event4_1.jpg)
