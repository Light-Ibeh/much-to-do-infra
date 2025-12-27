\# Much-To-Do – Cloud Infrastructure Project



\## Overview

Much-To-Do is a cloud infrastructure project that demonstrates the deployment of a scalable backend application on AWS using Terraform. The project emphasizes Infrastructure as Code (IaC), security best practices, high availability, and cost awareness.



The infrastructure provisions a Virtual Private Cloud (VPC), Application Load Balancer (ALB), Auto Scaling Group (ASG), EC2 instances, and supporting networking components. A remote Terraform backend is used for reliable state management and locking.





\## Architecture

The infrastructure is deployed in \*\*eu-west-1\*\* and consists of the following components:



\- Virtual Private Cloud (VPC)

\- Public and private subnets across multiple Availability Zones

\- Internet Gateway for public access

\- NAT Gateway for private subnet outbound access

\- Application Load Balancer (ALB)

\- Target Group with health checks

\- Auto Scaling Group with EC2 instances

\- Security Groups following least-privilege principles

\- S3 and DynamoDB for Terraform remote backend

\- S3 and CloudFront for frontend hosting (planned / partially provisioned)





\## Infrastructure Provisioning

All infrastructure is provisioned using \*\*Terraform\*\* with a modular and reusable structure.



\### Key Features

\- Modular Terraform design

\- Remote backend using S3 and DynamoDB

\- IAM separation between infrastructure provisioning and CI/CD

\- No manual console provisioning (except Terraform backend resources)

\- Budget-conscious resource selection



Terraform successfully provisions all required infrastructure resources without manual intervention.





\## Backend Deployment

The backend application runs on EC2 instances managed by an Auto Scaling Group. Incoming traffic is routed through an Application Load Balancer deployed in public subnets.



\### Health Check Endpoint

The backend exposes a health check endpoint used by the ALB target group:



/ping



markdown

Copy code





\## Live Backend Endpoint

\*\*Application Load Balancer DNS:\*\*



http://much-to-do-alb-249381740.eu-west-1.elb.amazonaws.com/ping



markdown

Copy code



A successful response (`pong`) confirms that:

\- EC2 instances are running successfully

\- Target group health checks are passing

\- Load balancer routing is functioning correctly

\- High availability is achieved across multiple Availability Zones





\## Security

\- IAM users are separated by responsibility

\- Terraform uses a dedicated IAM user

\- CI/CD uses a restricted IAM user with limited permissions

\- EC2 instances use IAM roles instead of static credentials

\- Security Groups restrict traffic to required ports only

\- No secrets are committed to version control





\## CI/CD Design (Conceptual)

A CI/CD pipeline design was prepared using GitHub Actions to:



\- Build backend Docker images

\- Push images to Amazon ECR

\- Enable automated application delivery independent of infrastructure provisioning



This design follows the \*\*principle of least privilege\*\* and aligns with industry best practices for cloud-native deployments.





\## Cost Management

\- AWS budget alerts were configured

\- Resource choices were made to remain within low-cost and free-tier limits where possible

\- Auto Scaling ensures efficient resource usage





\## Known Limitations

Due to time constraints, the following components were not fully deployed:



\- Frontend CloudFront distribution

\- MongoDB and Redis data layer

\- Full CI/CD automation and CloudWatch log forwarding



These components were planned and partially implemented conceptually. The existing infrastructure is structured to support them without architectural changes.





\## Conclusion

This project demonstrates a production-inspired AWS infrastructure using Terraform, with a strong focus on scalability, security, and maintainability.



The backend service is live, load-balanced, and highly available across multiple Availability Zones. 

