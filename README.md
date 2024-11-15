# README for CloudFormation Template

## Overview
This CloudFormation template is designed to deploy an application on an EC2 instance with a MySQL database hosted on Amazon RDS. It creates the necessary AWS infrastructure components, including a VPC, subnets, security groups, an EC2 instance, and an RDS instance.

## Template Features
- **Customizable Parameters**: Configure VPC name, EC2 instance type, RDS instance type, database credentials, and other key properties.
- **VPC with Public and Private Subnets**:
  - A public subnet for the EC2 instance.
  - Two private subnets for the RDS instance across different availability zones.
- **Security Groups**:
  - An EC2 security group allowing HTTP (port 80) and SSH (port 22) access.
  - An RDS security group allowing MySQL (port 3306) access from the EC2 instance.
- **Resources Deployed**:
  - A VPC with DNS support and hostname resolution enabled.
  - An internet gateway for internet connectivity.
  - An EC2 instance running Ubuntu.
  - An RDS MySQL database instance in a private subnet.

## Parameters
| Parameter          | Default Value     | Description                          |
|--------------------|-------------------|--------------------------------------|
| `VPCName`          | LAYOUTindexVPC   | Name of the VPC                     |
| `EC2InstanceType`  | t2.micro         | EC2 instance type                   |
| `RDSInstanceType`  | db.t3.micro      | RDS instance type                   |
| `DBName`           | LAYOUTindexDB    | Database name for RDS               |
| `DBUsername`       | admin            | Username for RDS                    |
| `DBPassword`       | (hidden)         | Password for RDS                    |

## Resources
### VPC
- A custom VPC with CIDR block `10.0.0.0/16`.
- Public and private subnets for proper network segmentation.

### EC2 Instance
- Deployed in the public subnet.
- Accessible via SSH and HTTP (ports 22 and 80).
- Configured with a key pair (`devops-user-key`) for SSH access.

### RDS Instance
- MySQL database engine version `8.0`.
- Allocated storage: 20 GB.
- Configured in private subnets for security.
- Not publicly accessible.

### Security Groups
- EC2 Security Group:
  - Allows inbound SSH and HTTP traffic.
- RDS Security Group:
  - Restricts access to MySQL traffic originating from the EC2 security group.

## Outputs
| Output Name         | Description                        |
|---------------------|------------------------------------|
| `VPCID`             | ID of the created VPC             |
| `EC2InstancePublicIP` | Public IP of the EC2 instance     |
| `RDSInstanceEndpoint` | Endpoint address for the RDS instance |


