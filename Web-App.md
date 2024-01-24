# Mission Logs AWS Deployment

Welcome to the Mission Logs AWS Deployment project! This guide will walk you through the process of deploying the Mission Logs application on AWS. The migration involves setting up infrastructure on Amazon Web Services, ensuring HTTPS security, and implementing Docker for application deployment.

## Table of Contents

1. [Introduction](#1-introduction)
2. [S3 and CloudFront Setup](#2-s3-and-cloudfront-setup)
3. [Domain Registration and HTTPS](#3-domain-registration-and-https)
4. [VPC and EC2 Setup](#4-vpc-and-ec2-setup)
5. [Docker Setup](#5-docker-setup)
6. [Auto-scaling and Load Balancing](#6-auto-scaling-and-load-balancing)
7. [Cost Analysis](#7-cost-analysis)

## 1. Introduction

### Product and Project Overview

The project aims to migrate the Mission Logs application from on-premise infrastructure to AWS. This migration enhances scalability, improves security against DDoS attacks, and provides efficient management for a growing user base.

This technical documentation provides an overview and guide to implementing the Amazon Web Service (AWS) Solution. The solution is contains two parts, part one being the base implementation (free) and part two being 
the slightly more advanced implementation (paid). This documentation assumes that you are familiar AWS and can navigate the AWS Console and has a general understanding of AWS and its services, as well as decent understanding of programming.
This documentation also assumes that you have a decent understanding of the Linux Command Line and other tools such as SSH clients.
### Key Files
[Files can be downloaded here](./aws_jedi_council_static_www)
- **index.html**: Front end of the website.
- **404.html**: Error page displayed when the website cannot be found.

## 2. S3 and CloudFront Setup

### Create an S3 Bucket

1. Navigate to your S3 Dashboard.
2. Select Create bucket.
3. Give your bucket a unique name.
4. Select your AWS Region.
5. Upload the contents of the website zip.
6. Activate Static Website Hosting and configure the bucket.

### Create a CloudFront Distribution

1. Set up a CloudFront distribution with the S3 bucket as the origin.
2. Restrict incoming traffic to HTTPS only.
3. Block every HTTP method except GET and HEAD.

## 3. Domain Registration and HTTPS

### Register a Domain through Route53

1. Navigate to Route 53.
2. Select Registered domains.
3. Choose Register domain.
4. Enter the desired domain name.

### Request an SSL Certificate through ACM

1. Navigate to ACM.
2. Select Request a certificate.
3. Choose Request a public certificate.
4. Enter the custom domain name.
5. Verify domain ownership.

### Update CloudFront Distribution for HTTPS

1. Edit CloudFront distribution for static content.
2. Choose the custom SSL certificate from ACM.

### Update Load Balancer for HTTPS

1. Edit listener configuration.
2. Add a new listener for HTTPS (Port 443).

### Update Auto-scaling Group Launch Template for HTTPS

1. Edit the Auto-scaling Group.
2. Edit the launch template.
3. Update the user data script for HTTPS settings.

## 4. VPC and EC2 Setup

### Create a Public VPC and Subnets

1. Create a VPC with a specified IPv4 CIDR.
2. Create public subnets in different availability zones.

### Create Internet Gateway

1. Navigate to Internet Gateway.
2. Create a new Internet Gateway.
3. Attach the Internet Gateway to the VPC.

### Edit the Route Table of the VPC

1. Navigate to the VPC.
2. Edit the main route table.
3. Add a route for destination 0.0.0.0/0 to the Internet Gateway.

## 5. Docker Setup

### Install Docker and Start the Application

1. Connect to your EC2 instance.
2. Run Docker installation commands.

### Starting the Mission Logs Application in Docker

Use Docker commands to pull and run the Mission Logs image.

## 6. Auto-scaling and Load Balancing

### Create a Launch Template and AMI

1. Create an image from your EC2 instance.
2. Create a launch template with user data for Docker commands.

### Create the Auto-scaling Group

1. Navigate to Auto Scaling Groups.
2. Create an Auto-scaling Group with the launch template.
3. Attach a load balancer.
4. Configure health checks, logging, and scaling policies.

## 7. Cost Analysis

Perform a cost analysis to ensure resources align with your budget and AWS Free Tier limits.

# MissionLogs Cost Estimate

| Service                      | Cost/Month | Cost/Year | Upfront Cost | Number of Instances | Total         |
|------------------------------|------------|-----------|--------------|----------------------|---------------|
| Amazon EC2                   | $14.31     | $171.70   | $0.00        | 2                    | $171.70       |
| Application Load Balancer    | $21.32     | $255.84   | $0.00        | 1                    | $255.84       |
| S3 Standard                  | $0.00      | $0.00     | $0.00        | -                    | $0.00         |
| Data Transfer                | $0.00      | $0.00     | $0.00        | -                    | $0.00         |
| Amazon CloudFront            | $0.40      | $4.80     | $0.00        | -                    | $4.80         |
| Amazon Route 53              | $0.54      | $6.48     | $0.00        | -                    | $6.48         |
| Amazon RDS for PostgreSQL    | $1.92      | $23.08    | $0.00        | 1                    | $23.08        |
| **Total Monthly Estimate**   | **$38.49**  | **$461.92**| **$0.00**  | **-**                | **$461.92**   |

## Cost Breakdown

- **Monthly**: Estimated monthly cost for each service.
- **Yearly**: Estimated yearly cost calculated from the monthly cost.
- **Upfront**: One-time upfront cost.
- **Number of Instances**: For services with instances, the number of instances considered.
- **Total**: The sum of all monthly costs.

**Note**: The provided estimate is based on AWS Pricing Calculator and may not include taxes or other factors affecting actual costs.
https://calculator.aws/#/estimate?id=45d12ea1039119e0a5ef29937597b3122e1b11d5

Feel free to follow this README to successfully deploy the Mission Logs application on AWS! 
