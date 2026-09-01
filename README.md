AWS Cost Optimization using Lambda

📌 Project Overview

This project demonstrates an automated approach to AWS cost optimization by identifying idle Amazon EC2 instances based on CPU utilization and automatically stopping them.
The solution uses AWS Lambda, Amazon EC2, Amazon CloudWatch, Amazon SNS, IAM, and Python (boto3). Lambda periodically analyzes running EC2 instances, identifies instances with low CPU utilization, stops the idle instances, and sends an email notification through SNS.

🎯 Objectives

Automatically monitor EC2 resource utilization.
Identify idle EC2 instances based on CPU usage.
Stop unused instances to reduce unnecessary AWS costs.
Send notifications when idle instances are detected and stopped.
Automate the cost optimization process without manual monitoring.

🛠️ Technologies Used

Technology	Purpose
AWS Lambda	Executes the cost optimization logic
Amazon EC2	Compute resource being monitored
Amazon CloudWatch	Provides EC2 CPU utilization metrics
Amazon SNS	Sends email notifications
AWS IAM	Provides permissions to Lambda
Python	Implements the automation logic
Boto3	Python SDK used to interact with AWS services

🏗️ Architecture
                   
                   
                    AWS Cloud
                       |
                       v
                 AWS Lambda
              (Python + Boto3)
                       |
          +------------+------------+
          |            |            |
          v            v            v
        EC2        CloudWatch       SNS
      Instances    CPU Metrics   Notifications
          |            |            |
          |            |            v
          |            |       Email Notification
          |            |
          +------------+
             |
             v
       Stop Idle Instances

⚙️ Project Workflow

Lambda Function
      |
      v
Find Running EC2 Instances
      |
      v
Check CPU Utilization
      |
      v
Is Average CPU < 5%?
      |
    Yes
      |
      v
Stop EC2 Instance
      |
      v
Send SNS Notification
If no idle instances are detected, the Lambda function returns a report indicating that no idle EC2 instances were found.

🔐 IAM Configuration

An IAM role named:

lambda-cost-opt-role

was created and attached to the Lambda function.
The role was given permissions to:

ec2:DescribeInstances
ec2:StopInstances
cloudwatch:GetMetricStatistics
sns:Publish

These permissions allow the Lambda function to:

Retrieve running EC2 instances.
Stop EC2 instances.
Retrieve CloudWatch CPU metrics.
Publish notifications through SNS.

📧 Amazon SNS Configuration

An SNS topic named:

cost-optimizer-alerts

was created.

An email subscription was added to the topic and verified through the email confirmation process.
SNS is used to notify the user when idle EC2 instances are identified and stopped.

⚡ AWS Lambda Configuration

A Lambda function named:

cost-optimizer

was created using the Python runtime.

The previously created IAM role was attached to the function.
The Lambda function uses Boto3 to communicate with EC2, CloudWatch, and SNS.

🐍 Lambda Logic

The function uses a CPU utilization threshold of:

CPU_THRESHOLD = 5

It retrieves the CPU utilization data for the previous three hours and calculates the average CPU utilization.

The main logic is:

1. Retrieve all running EC2 instances
2. Get CPU utilization metrics
3. Calculate average CPU utilization
4. Compare average CPU with 5% threshold
5. If CPU < 5%, identify the instance as idle
6. Stop the idle instance
7. Add the instance to the report
8. Publish the report through SNS

The Lambda function retrieves running instances using ec2.describe_instances() and stops instances identified as idle using ec2.stop_instances().

🔧 Environment Variable

The SNS topic ARN is provided to the Lambda function through an environment variable:

SNS_TOPIC_ARN

This allows the Lambda function to publish notifications to the configured SNS topic.

🧪 Testing

A Lambda test event named:

TestEvent

was created and executed through the Lambda console.

The execution result showed a successful execution.

📊 Result

When an idle EC2 instance is detected, the Lambda function automatically stops it and sends a notification through SNS.

Example notification:

EC2 i-0abc123def45 is idle — stopping...

If no idle instances are detected, the report returns:

No idle EC2 instances found.

✨ Key Features

Automated EC2 monitoring
CPU utilization-based idle detection
Automatic EC2 instance stopping
CloudWatch metric monitoring
SNS email notifications
IAM-based access control
Serverless automation using AWS Lambda
Python automation using Boto3

📚 Key Learnings

Through this project, I gained hands-on experience with:

AWS Lambda
Amazon EC2
Amazon CloudWatch
Amazon SNS
AWS IAM
Python Boto3
AWS automation
IAM permissions and roles
Cloud cost optimization
Monitoring AWS resources using CloudWatch metrics

📁 Project Structure

aws-cost-optimization/
│
├── lambda_function.py
├── README.md
└── docs/
    └── project-documentation.pdf

🚀 Future Improvements

Add a scheduled EventBridge trigger to run the Lambda automatically.
Use additional CloudWatch metrics for more accurate idle-resource detection.
Add configurable CPU thresholds.
Support multiple AWS regions.
Generate periodic cost-optimization reports.
Add additional resource types for cost optimization.

📌 Project Status

Completed

This project demonstrates how AWS serverless automation can be used to identify and stop idle EC2 instances, helping reduce unnecessary cloud expenses. The implementation integrates Lambda, EC2, CloudWatch, SNS, IAM, and Python Boto3.
