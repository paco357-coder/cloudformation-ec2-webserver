# cloudformation-ec2-webserver
## Result

The CloudFormation stack successfully deploys an EC2 instance running Apache.
The web server is accessible via the stack output URL.
# CloudFormation EC2 Web Server

Deploys a simple EC2 web server using AWS CloudFormation. This project demonstrates **Infrastructure as Code (IaC)**, security best practices, and automated software installation.

---

## Architecture

- **EC2 Instance**: Amazon Linux 2 (t2.micro)  
- **Security Group**:  
  - HTTP (80) open to the world  
  - SSH (22) configurable via parameter (can be locked to a single IP)  
- **User Data**: Installs and starts Apache, serves a basic web page  

---

## Deployment Instructions

### Prerequisites
1. AWS Account  
2. AWS CLI installed (optional for CLI deployment)  
3. EC2 Key Pair for SSH access  

### Deploy via AWS Console
1. Go to **CloudFormation → Create stack → With new resources (standard)**  
2. Upload `template.yaml`  
3. Enter parameters:  
   - `KeyName`: your EC2 key pair  
   - `SSHLocation`: your IP in CIDR format (e.g., `203.0.113.45/32`)  
4. Click **Create stack**  
5. Wait for `CREATE_COMPLETE`  

### Deploy via AWS CLI (Optional)
```bash
aws cloudformation create-stack \
  --stack-name ec2-webserver-stack \
  --template-body file://template.yaml \
  --parameters ParameterKey=KeyName,ParameterValue=YOUR_KEY_NAME ParameterKey=SSHLocation,ParameterValue=YOUR_IP/32 \
  --region us-east-1
