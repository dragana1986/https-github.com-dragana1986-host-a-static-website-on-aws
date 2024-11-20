![Alt text](/Host_a_Static_Website_on_AWS.png)



# README for Hosting a Static Website on AWS

This project demonstrates how to host a static HTML web application on AWS, leveraging various AWS resources to ensure scalability, fault tolerance, and secure access. The steps outlined below describe the process of deploying the web application using EC2 instances, VPC configuration, Load Balancer, Auto Scaling, and other services.

## Project Overview

The goal of this project is to host a static website on AWS while maintaining high availability, security, and scalability. Key AWS resources used include:

- Virtual Private Cloud (VPC)
- EC2 Instances
- Internet Gateway
- Application Load Balancer (ALB)
- Auto Scaling Group
- Security Groups
- Route 53
- Certificate Manager
- Simple Notification Service (SNS)

The website is hosted on EC2 instances within a private subnet, with traffic routed through an Application Load Balancer for optimal distribution and fault tolerance.

## Architecture Diagram

You can view the architecture diagram for this project in the GitHub repository.

## AWS Resources Configuration

### 1. Virtual Private Cloud (VPC)
A Virtual Private Cloud (VPC) is configured with both public and private subnets across two availability zones. This setup enhances fault tolerance and security.

### 2. Internet Gateway
An Internet Gateway is deployed to provide internet connectivity to resources within the VPC, such as EC2 instances in public subnets.

### 3. Security Groups
Security Groups act as firewalls, controlling inbound and outbound traffic to EC2 instances. These are configured for secure communication between instances in different subnets.

### 4. Availability Zones
Two availability zones are used to ensure high availability and fault tolerance for web application components.

### 5. Public Subnets
Public subnets are used for infrastructure components, such as the NAT Gateway and Application Load Balancer (ALB).

### 6. EC2 Instance Connect Endpoint
EC2 Instance Connect Endpoint is used to securely connect to resources within both public and private subnets.

### 7. EC2 Instances in Private Subnets
Web servers (EC2 instances) are placed in private subnets for added security. These instances are accessed via the Application Load Balancer.

### 8. NAT Gateway
The NAT Gateway is used to provide internet access to instances in private subnets, allowing them to retrieve updates and communicate with external resources.

### 9. Application Load Balancer (ALB)
An Application Load Balancer is used to distribute traffic evenly across EC2 instances. This helps to manage traffic load efficiently and improve availability.

### 10. Auto Scaling Group
An Auto Scaling Group is configured to manage EC2 instances automatically, ensuring that the website scales according to traffic demand and maintains high availability.

### 11. GitHub Integration
Web files are stored in a GitHub repository for version control and collaboration. The repository is cloned to EC2 instances during setup.

### 12. SSL/TLS Encryption
AWS Certificate Manager is used to secure communications by provisioning an SSL certificate for the website, ensuring encrypted communication between clients and servers.

### 13. Simple Notification Service (SNS)
SNS is configured to notify administrators of activity within the Auto Scaling Group, such as scaling events or instance health changes.

### 14. Domain Name System (DNS)
Route 53 is used to manage DNS records, allowing the domain name to resolve to the IP address of the Application Load Balancer.

## Deployment Steps

The following steps outline the process of deploying the static website on EC2 instances.

### Prerequisites
- An AWS account with permissions to create and manage EC2, VPC, and other resources.
- A GitHub repository with the static website files.

### Setup Script

1. SSH into your EC2 instance.
2. Switch to the root user to ensure administrative privileges:
   ```bash
   sudo su
   ```

3. Update all installed packages:
   ```bash
   yum update -y
   ```

4. Install the Apache HTTP Server:
   ```bash
   yum install -y httpd
   ```

5. Change the current working directory to the Apache web root:
   ```bash
   cd /var/www/html
   ```

6. Install Git to clone the repository:
   ```bash
   yum install git -y
   ```

7. Clone the GitHub repository containing the website files:
   ```bash
   git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git
   ```

8. Copy the cloned files to the Apache web root:
   ```bash
   cp -R host-a-static-website-on-aws/. /var/www/html/
   ```

9. Clean up by removing the cloned repository directory:
   ```bash
   rm -rf host-a-static-website-on-aws
   ```

10. Enable Apache to start on boot:
    ```bash
    systemctl enable httpd
    ```

11. Start the Apache HTTP server to serve the website:
    ```bash
    systemctl start httpd
    ```

### Route 53 DNS Configuration

- Register a domain name in Route 53.
- Create a DNS record that points to the IP address of your Application Load Balancer (ALB).

### Auto Scaling Group & ALB Configuration

- Configure an Auto Scaling Group with the desired minimum, maximum, and desired instance count.
- Set up the Application Load Balancer to distribute traffic across multiple EC2 instances.

### Security Groups & Networking

- Set up Security Groups to allow HTTP/HTTPS traffic to the ALB and EC2 instances.
- Configure the VPC with both public and private subnets, ensuring that only necessary resources are exposed to the internet.

## Conclusion

This project demonstrates how to deploy a highly available, secure, and scalable static website on AWS. The use of EC2 instances, Auto Scaling, Application Load Balancer, and other AWS services ensures that the website is reliable and can handle varying levels of traffic.

For more detailed instructions and the full project setup, refer to the GitHub repository.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For any questions or issues, please reach out via GitHub issues or contact me directly at aosnotes77@github.com.

---

This README provides an overview of the deployment process, the AWS resources used, and the configuration steps required to host a static website on AWS using EC2 instances and other associated services.
