# EC2-CLI-Automation

# Launch an EC2 Instance Using AWS CLI

This guide shows how to create, check, and terminate an AWS EC2 instance via the AWS Command Line Interface (CLI).

---

## Prerequisites

- AWS CLI installed and configured (`aws configure`)
- AWS account with permissions to manage EC2
- Basic info about your AWS environment (AMI ID, subnet, security group, key pair, etc.)

---

## 1. Configure Region

Set your AWS CLI to the desired region (example: `eu-north-1`):

```bash
aws configure set region eu-north-1


Required Info;
| Parameter         | Example Value              |
| ----------------- | -------------------------- |
| AMI ID            | `ami-0c1ac8a41498c1a9c`    |
| Instance Type     | `t2.micro`                 |
| Key Pair Name     | `MY-KEY-PAIR`     |
| Security Group ID | `sg-02ec587ead8af136c`     |
| Subnet ID         | `subnet-0479acbCCa0d6fd420` |
| Availability Zone | `US-east-1b`              |


3. Launch the EC2 Instance;
aws ec2 run-instances \
  --image-id ami-0c1ac8a41498c1a9c \
  --count 2 \
  --instance-type t2.micro \
  --key-name "MY-KEY-PAIR" \
  --security-group-ids sg-02ec587ead8af136c \
  --subnet-id subnet-0479acbba0d6fd420 \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=MY-APP-Test}]' \
  --placement AvailabilityZone=us-east-1b

4. Check Instance Status
Replace <instance-id> with your instance ID:
aws ec2 describe-instances --instance-ids <instance-id> \
  --query "Reservations[*].Instances[*].[InstanceId,State.Name,PublicIpAddress]" \
  --output table



5. Terminate the Instance after practice
Replace <instance-id> with your instance ID:
aws ec2 terminate-instances --instance-ids <instance-id>

6. Verify if its Terminated:
aws ec2 describe-instances --instance-ids <instance-id> \
  --query "Reservations[*].Instances[*].State.Name" \
  --output text


References;
AWS CLI EC2 Docs
Launching EC2 Instances
