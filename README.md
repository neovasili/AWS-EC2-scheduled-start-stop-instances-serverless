# AWS EC2 scheduled start-stop instances serverless
This project is intended to create a fully serverless infraestructure for start-stop EC2 instances scheduled jobs.

It will create a cloudformation stack with all the necessary artifacts:
* Several AWS lambda functions
* IAM role permissions
* Cloudwatch log streams
* Cloudwatch event rules for scheduling actions

## System workflow
The workflow is very simple. Every **30 minutes** a cloudwatch event will trigger a lambda function that scans each region in the AWS account looking for EC2 instances that match the start or stop criteria.

This criteria is based on three tags that must be attached to the instances:
* **stage**: must be the same which the schedule system was deployed
* **start**: start hour (24 hours format) in which the instance must be started
* **stop**: stop hour (24 hours format) in which the instance must be stopped

Pay attention on the **timezone** where you put your instances start and stop tags. A default timezone is setted in the **serverless.yml** file, if you want to use a different one, please change this value.

## Installation
This project was made with the serverless framework, so you need to install it first: [Serverless installation guide](https://serverless.com/framework/docs/providers/aws/guide/installation/).