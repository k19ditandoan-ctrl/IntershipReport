---
title: "Week 11 Worklog"
date: 2026-03-22
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### OBJECTIVES IN WEEK 11:
- Upgrade Hybrid Search Engine by integrating LLMs to build a complete RAG (Retrieval-Augmented Generation) system.
- Master the development process of complex Serverless applications (Frontend, Backend, Image Processing) using AWS SAM.
- Practice professional Machine Learning workflows on Amazon SageMaker: From Feature Engineering to Model Deployment.
- Optimize coding performance with AWS AI tools (Amazon Q, CodeWhisperer) on VS Code.

### TASKS OF WEEK 11:

| Day | Task | Start Date | End Date | References |
|:---:|---|:---:|:---:|---|
| **Mon** | **- Team Project Meeting: Backend Development - Hybrid Search Engine (Text search + semantic search):**<br>- Improve hybrid search engine accuracy with LLM<br>- Add chat feature for users to search instead of just keyword search<br>- Research best practices and papers for RAG systems | 23/03/2026 | 23/03/2026 | [RAG Paper 1](https://arxiv.org/pdf/2509.13603)<br>[RAG Paper 2](https://arxiv.org/pdf/2508.18048)<br>[Meilisearch Hybrid](https://www.meilisearch.com/blog/fixing-hybrid-search)<br>[Elastic RAG](https://www.elastic.co/search-labs/blog/llm-agents-intelligent-hybrid-search) |
| **Tue** | **- Practice Lab 26: Serverless - Guide to writing Front-end calling API Gateway**<br>+ Deploy Front-end<br>+ Setup API Gateway<br>+ Test API with Postman<br>+ Test API with Front-end<br>+ Resource Cleanup<br>**- Practice Lab 27: Serverless with Lambda, API Gateway and SAM**<br>+ Introduction<br>+ Preparation<br>* Create Cloud9 instance<br>* Create CodeCommit Repository<br>+ Deploy Sample App<br>* Deploy Frontend<br>* Deploy Backend<br>Deploy Infrastructure<br>Populate trip info<br>Check configuration<br>* Update Frontend<br>+ Deploy ride times system<br>* Deploy Backend<br>* Deploy Frontend<br>+ On-ride photo processing<br>* Deploy Backend<br>Create Chroma Key Lambda function<br>Create Photo-Compositing Lambda function<br>Post-processing<br>* Test features<br>+ Resource Cleanup | 24/03/2026 | 24/03/2026 | [Lab 26 Intro](https://000135.awsstudygroup.com/vi/1-front-end-deployment/)<br>[API Gateway](https://000135.awsstudygroup.com/vi/2-config-api-gw/)<br>[Lab 27 Intro](https://000066.awsstudygroup.com/vi/1-introduce/)<br>[Deploy App](https://000066.awsstudygroup.com/vi/3-deployapp/)<br>[Image Processing](https://000066.awsstudygroup.com/vi/5-on-ridesphotoprocessing/) |
| **Wed** | **- Practice Lab 28: SageMaker Immersion Day Workshop**<br>+ Preparation<br>* Create SageMaker Studio<br>* Clone GitHub repo<br>+ Feature Engineering<br>* Prepare Dataset<br>* Install Data Wrangler<br>* Analyze Dataset<br>* Correlation Analysis<br>* Data Transformation<br>* Feature Store<br>* Export Data to S3<br>+ Train/Tune/Deploy XGBoost<br>* Train & Tune model<br>* Deploy model<br>* Evaluate model performance<br>* Automatic model tuning<br>+ Resource Cleanup | 25/03/2026 | 25/03/2026 | [Lab 28 Prepare](https://000200.awsstudygroup.com/vi/1-prepare/)<br>[Feature Engineering](https://000200.awsstudygroup.com/vi/2-feature-engineering/)<br>[Train Deploy](https://000200.awsstudygroup.com/vi/3-train-tune-deploy/) |
| **Thu** | **- Team Project Meeting: Backend Development - RAG system (combined hybrid search engine and LLM):**<br>- Run and test RAG system with collected data<br>- Finalize RAG system | 26/03/2026 | 26/03/2026 | [Hybrid for RAG](https://careers.edicomgroup.com/techblog/llm-rag-improving-the-retrieval-phase-with-hybrid-search/)<br>[Medium RAG](https://medium.com/data-science/how-to-use-hybrid-search-for-better-llm-rag-retrieval-032f66810ebe)<br>[AWS RAG](https://aws.amazon.com/vi/what-is/retrieval-augmented-generation/)<br>[RAG Paper 2020](https://arxiv.org/pdf/2005.11401) |
| **Fri** | **- Practice Lab 29: AWS Toolkit for VS Code: Amazon Q & CodeWhisperer**<br>+ Introduction<br>+ AWS Toolkit for Visual Studio Code<br>+ Connect AWS Account<br>+ Change AWS Region<br>+ Authentication<br>* IAM Identity Center<br>* AWS IAM credentials<br>* Create AWS Builder ID<br>+ Interact with Services<br>* AWS Explorer<br>* Amazon Q<br>* Amazon CodeWhisperer | 27/03/2026 | 27/03/2026 | [Lab 29 Intro](https://000087.awsstudygroup.com/vi/1-introduce/)<br>[Install Toolkit](https://000087.awsstudygroup.com/vi/2-install/)<br>[Authentication](https://000087.awsstudygroup.com/vi/5-authentication-and-access-for-the-aws-toolkit-for-visual-studio-code/)<br>[Amazon Q](https://000087.awsstudygroup.com/vi/6-working-with-aws-services/) |



### ACHIEVEMENTS IN WEEK 11:
1. Successfully upgraded Hybrid Search Engine to a RAG system, enabling natural language interaction (Chat) instead of just keyword search.
2. Deployed a complete Serverless multi-functional application (including real-time image processing) using AWS SAM (Serverless Application Model).
3. Completed the Machine Learning pipeline on SageMaker: From Data Cleaning (Data Wrangler) to Training and Deploying XGBoost models.
4. Successfully configured AI-integrated coding environment (Amazon Q, CodeWhisperer) on VS Code, improving coding speed and debugging.
5. Tested and operated the RAG system with real data, ensuring accuracy and context awareness of responses.