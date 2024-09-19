# Host a Static Website on AWS

## Project Overview
This project demonstrates how to host a static HTML web application on Amazon Web Services (AWS). It leverages various AWS services and configurations to ensure high availability, security, and scalability. The architecture includes a Virtual Private Cloud (VPC) with public and private subnets, an Application Load Balancer (ALB), EC2 instances, and more.

## Architecture Diagram
![Alt text](Host_a_Static_Website_on_AWS.png)  

## AWS Resources Utilized
- **VPC Configuration**: Created a VPC with public and private subnets across two availability zones for high availability.
- **Internet Gateway**: Deployed to enable internet connectivity for VPC instances.
- **Security Groups**: Configured as a firewall mechanism:
  - **EICE Security Group**: SSH (port 22) access restricted to VPC IP address.
  - **ALB Security Group**: HTTP (port 80) and HTTPS (443) access from the internet (0.0.0.0/0).
  - **Webapp Security Group**: HTTP (port 80) and HTTPS (443) access restricted to the ALB security group.
- **NAT Gateway**: Used in public subnets to allow instances in private subnets to access the internet securely.
- **EC2 Instance Connect Endpoint**: Facilitated secure connections to assets in public and private subnets.
- **Auto Scaling Group**: Managed the EC2 instances, ensuring availability and fault tolerance.
- **Application Load Balancer**: Distributes web traffic across multiple EC2 instances in an Auto Scaling Group.
- **Amazon Certificate Manager**: Secured application communication.
- **Simple Notification Service (SNS)**: Alerts for activities within the Auto Scaling Group.
- **Route 53**: Managed domain name registration and DNS records.

## Deployment Script
The following Bash script sets up the Apache HTTP Server on the EC2 instance and deploys the web application:

```bash
#!/bin/bash
 
# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/sunny-ekwugha/Project1-Static-Website.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R Project1-Static-Websites/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf Project1-Static-Website

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd 

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Project Structure
- **`/var/www/html/`**: Root directory for the hosted web application.
- **GitHub Repository**: Contains the web application files and version control.

## How to Access the Website
After deploying the application, you can access the website using the registered domain name or the public DNS name of the Application Load Balancer.

## Conclusion
This project showcases how to effectively host a static website on AWS, employing various services to ensure a robust architecture.

---

Feel free to modify any section or add any additional details that you think may be helpful!
