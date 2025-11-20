# AWS Services Used in GenAI Bootcamp Projects

This document provides an overview of all AWS services used across the various projects in this GenAI bootcamp repository.

## Quick Reference Table

| Service | Documentation |
|---------|--------------|
| Amazon S3 (Simple Storage Service) | https://docs.aws.amazon.com/s3/ |
| Amazon CloudFront | https://docs.aws.amazon.com/cloudfront/ |
| AWS Lambda | https://docs.aws.amazon.com/lambda/ |
| Amazon DynamoDB | https://docs.aws.amazon.com/dynamodb/ |
| AWS Step Functions | https://docs.aws.amazon.com/step-functions/ |
| Amazon EventBridge | https://docs.aws.amazon.com/eventbridge/ |
| AWS IAM (Identity and Access Management) | https://docs.aws.amazon.com/iam/ |
| Amazon SNS (Simple Notification Service) | https://docs.aws.amazon.com/sns/ |
| Amazon Cognito | https://docs.aws.amazon.com/cognito/ |
| AWS Certificate Manager (ACM) | https://docs.aws.amazon.com/acm/ |
| Amazon Bedrock | https://docs.aws.amazon.com/bedrock/ |
| Amazon S3 Vectors | https://aws.amazon.com/s3/features/vectors/ |

## Detailed Service Descriptions

### Amazon S3 (Simple Storage Service)

**Summary:** Amazon S3 is an object storage service that offers industry-leading scalability, data availability, security, and performance. It allows you to store and retrieve any amount of data at any time from anywhere.

**Why it's used in these projects:**
- **Frontend Hosting**: Static website files (HTML, CSS, JavaScript) are stored in S3 buckets and served to users
- **State Management**: Application state and session data are persisted in S3 buckets for serverless applications
- **Document Storage**: Input documents (like PDFs) for processing are uploaded to S3 buckets
- **Configuration Storage**: Environment configuration files for the admin UI are served from S3

Note: While S3 Vectors (see below) is also part of the S3 family, it's listed separately due to its specialized vector storage capabilities.

### Amazon CloudFront

**Summary:** Amazon CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency and high transfer speeds.

**Why it's used in these projects:**
- **Content Delivery**: Distributes frontend static assets to users worldwide with low latency
- **Origin Routing**: Routes requests between S3-hosted frontends and Lambda-based backends
- **Custom Domains**: Supports custom domain names with SSL certificates
- **Path-Based Routing**: Directs different URL paths to different origins (e.g., `/api/*` to backend, `/admin/*` to admin frontend)
- **Cache Control**: Implements caching policies to optimize performance (disabled for API calls, enabled for static content)
- **URL Rewriting**: Uses CloudFront Functions to rewrite URLs for client-side routing in single-page applications

### AWS Lambda

**Summary:** AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers. You pay only for the compute time you consume.

**Why it's used in these projects:**
- **Backend APIs**: Hosts the main application logic for weather apps, customer service bots, and digital twin applications
- **Document Processing**: Handles document validation, extraction, and output validation in workflows
- **Admin APIs**: Provides administrative functionality for managing knowledge bases and user data
- **Custom Resources**: Implements CloudFormation custom resources for provisioning complex AWS resources (S3 Vectors, Bedrock Knowledge Bases)
- **Response Streaming**: Uses Lambda Function URLs with response streaming for real-time AI model responses
- **Lambda Layers**: Utilizes the Lambda Web Adapter layer to run traditional web frameworks in Lambda

### Amazon DynamoDB

**Summary:** Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability.

**Why it's used in these projects:**
- **Session Storage**: Stores conversation history and session state for chatbots
- **Customer Service Data**: Maintains customer service tickets and interactions
- **Document Metadata**: Tracks document processing status and metadata
- **Admin Data**: Stores administrative settings, pending questions, and application configuration
- **Single Table Design**: Uses partition key (PK) and sort key (SK) pattern for flexible data modeling

### AWS Step Functions

**Summary:** AWS Step Functions is a serverless orchestration service that lets you coordinate multiple AWS services into serverless workflows.

**Why it's used in these projects:**
- **Document Processing Workflow**: Orchestrates a multi-step document extraction pipeline
- **Validation Logic**: Implements branching logic based on validation results
- **Error Handling**: Manages failure states and retry logic for document processing
- **State Transitions**: Coordinates the flow between input validation, extraction, and output validation steps

### Amazon EventBridge

**Summary:** Amazon EventBridge is a serverless event bus service that makes it easy to connect applications using events from your own applications, integrated Software-as-a-Service (SaaS) applications, and AWS services.

**Why it's used in these projects:**
- **S3 Event Triggers**: Automatically triggers Step Functions workflows when PDF files are uploaded to S3
- **Event Pattern Matching**: Filters events to only process specific file types (e.g., `.pdf` files)
- **Event-Driven Architecture**: Enables decoupled, reactive application design

### AWS IAM (Identity and Access Management)

**Summary:** AWS IAM enables you to manage access to AWS services and resources securely. Using IAM, you can create and manage AWS users and groups, and use permissions to allow and deny their access to AWS resources.

**Why it's used in these projects:**
- **Service Roles**: Creates roles for Lambda functions to access other AWS services
- **Policy Management**: Defines fine-grained permissions for accessing Bedrock, S3, DynamoDB, etc.
- **Service Principals**: Enables AWS services to assume roles (e.g., Bedrock assuming a role to read from S3)
- **Least Privilege**: Implements security best practices by granting only necessary permissions

### Amazon SNS (Simple Notification Service)

**Summary:** Amazon SNS is a fully managed messaging service for both application-to-application (A2A) and application-to-person (A2P) communication.

**Why it's used in these projects:**
- **Notifications**: Sends alerts when the digital twin encounters questions it cannot answer
- **Escalation**: Notifies administrators about pending customer questions requiring human intervention
- **Pub/Sub Pattern**: Enables loosely coupled notification delivery to multiple subscribers

### Amazon Cognito

**Summary:** Amazon Cognito provides authentication, authorization, and user management for web and mobile apps. Your users can sign in directly with a user name and password, or through a third party.

**Why it's used in these projects:**
- **User Authentication**: Manages user sign-up, sign-in, and access control for the admin UI
- **User Pools**: Stores user identities and credentials
- **Email Authentication**: Supports both password and email OTP authentication methods
- **Custom Attributes**: Stores additional user properties like admin status
- **Token Management**: Issues JWT tokens for authenticated API access

### AWS Certificate Manager (ACM)

**Summary:** AWS Certificate Manager is a service that lets you easily provision, manage, and deploy public and private SSL/TLS certificates for use with AWS services and your internal connected resources.

**Why it's used in these projects:**
- **SSL/TLS Certificates**: Provides HTTPS encryption for custom domain names
- **CloudFront Integration**: Automatically integrates with CloudFront distributions
- **Certificate Management**: Handles certificate renewal automatically

### Amazon Bedrock

**Summary:** Amazon Bedrock is a fully managed service that offers a choice of high-performing foundation models from leading AI companies through a single API, along with capabilities to build generative AI applications.

**Why it's used in these projects:**
- **AI Model Access**: Provides access to Claude models (Haiku, Sonnet) for conversational AI
- **Response Streaming**: Enables real-time streaming responses for better user experience
- **Guardrails**: Implements content filtering and topic denial policies for safe AI interactions
- **Knowledge Bases**: Provides retrieval-augmented generation (RAG) capabilities for domain-specific question answering
- **Data Sources**: Manages document ingestion and chunking for knowledge bases
- **Semantic Chunking**: Automatically splits documents into meaningful chunks for better retrieval

### Amazon S3 Vectors

**Summary:** Amazon S3 Vectors (announced in preview in July 2025) is AWS's first cloud object storage with native support for storing and querying vector data at scale. It provides purpose-built, cost-optimized vector storage without requiring infrastructure provisioning, delivering sub-second query performance while reducing costs by up to 90% compared to traditional vector databases.

**Why it's used in these projects:**
- **Vector Buckets**: Creates dedicated vector buckets to store embedding vectors separately from traditional object storage
- **Vector Indexes**: Manages vector indexes within buckets for efficient similarity search using cosine distance metrics
- **Bedrock Integration**: Integrates seamlessly with Amazon Bedrock Knowledge Bases as the vector store backend for RAG applications
- **Cost Optimization**: Reduces the cost of uploading, storing, and querying billions of vectors for AI/ML applications
- **Elastic Scaling**: Supports scaling from millions to billions of vectors with up to 10,000 indexes per bucket
- **Semantic Search**: Enables similarity search across large datasets for AI agent memory and contextual awareness
- **Custom Resources**: Deployed via Lambda-based CloudFormation custom resources using the `s3vectors` boto3 client API

**Technical Details:**
- Vector dimension: 1024 (configurable, using Amazon Titan Embed Text v2 model dimensions)
- Distance metric: Cosine similarity
- Data type: float32
- Performance: Sub-second query latency at hundreds of queries per second per bucket
- Metadata support: Stores non-filterable metadata like `AMAZON_BEDROCK_TEXT` for document chunking

## Service Usage by Project

### Week 5 - Weather Application
- S3, CloudFront, Lambda, Bedrock, IAM

### Week 6 - Flight AI Customer Service
- S3, CloudFront, Lambda, DynamoDB, Bedrock (with Guardrails), IAM

### Week 6 - Document Extractor
- S3, Lambda, DynamoDB, Step Functions, EventBridge, Bedrock, IAM

### Week 7 - Digital Twin
- S3, CloudFront, Lambda, Bedrock (with Knowledge Bases), S3 Vectors, IAM

### Week 8 - Admin UI
- S3, CloudFront, Lambda, DynamoDB, SNS, Cognito, Certificate Manager, Bedrock (with Knowledge Bases), S3 Vectors, CloudWatch RUM, IAM

## Additional Resources

For more information about using AWS CDK to define these services:
- [AWS CDK Python Reference](https://docs.aws.amazon.com/cdk/api/v2/python/)
- [AWS CDK Developer Guide](https://docs.aws.amazon.com/cdk/)
