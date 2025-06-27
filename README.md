# AWS Secure Three-Tier Architecture

![Architecture Diagram]([image.png](https://docs.aws.amazon.com/images/vpc/latest/userguide/images/vpc-example-private-subnets.png))  
*Highly Available Cloud Infrastructure with Isolated Networking*

## 📌 Features
- **Multi-AZ Deployment**: Fault tolerance across availability zones
- **Public/Private Subnets**: Secure separation of resources
- **Application Load Balancer**: Distributes traffic to backend servers
- **NAT Gateways**: Outbound internet for private subnets
- **S3 Gateway Endpoint**: Private S3 access without internet
- **Security Groups**: Instance-level firewall rules

## 🛠️ Tech Stack
| AWS Service       | Purpose                          |
|-------------------|----------------------------------|
| VPC              | Isolated network environment     |
| EC2              | Backend servers                  |
| ALB              | Traffic distribution & SSL termination |
| NAT Gateway      | Private subnet internet access   |
| S3 Gateway       | Secure internal storage access   |

## 🔒 Security Implementation
```hcl
# Example Security Group (Terraform)
resource "aws_security_group" "app_server" {
  ingress {
    from_port   = 80
    to_port     = 80
    security_groups = [aws_security_group.alb.id] # Only allow ALB
  }
}
