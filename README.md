# AWS 3-Tier Web Application

##1. Project Overview

This project demonstrates the deployment of a highly available and scalable 3-Tier Web Application on Amazon Web Services (AWS).

The application architecture is divided into three main layers:

- Presentation Layer – Application Load Balancer and web servers
- Application Layer – EC2 instances managed through an Auto Scaling Group
- Database Layer – Amazon RDS database

The infrastructure is deployed inside a custom Amazon VPC with public and private subnets. Security Groups are used to control network traffic, while AWS Systems Manager (SSM) is used to securely access EC2 instances without directly exposing SSH access.

Additional AWS services such as Amazon S3, Amazon CloudFront, and Amazon CloudWatch are used for static content delivery, global distribution, monitoring, and alerting.

##2. Architecture

The overall architecture follows a standard three-tier cloud architecture:

Users → Application Load Balancer → EC2 Auto Scaling Group → RDS Database

The application is deployed across multiple Availability Zones to improve availability and reliability.

Main AWS Components

- Amazon VPC
- Public and Private Subnets
- Internet Gateway
- Route Tables
- Security Groups
- Application Load Balancer (ALB)
- Target Group
- EC2 Instances
- Auto Scaling Group (ASG)
- Amazon RDS
- AWS Systems Manager (SSM)
- Amazon S3
- Amazon CloudFront
- Amazon CloudWatch

##3. VPC Configuration

A custom VPC was created to provide an isolated networking environment for the application.

The VPC contains multiple subnets distributed across Availability Zones.

Public-facing resources such as the Application Load Balancer are placed in public subnets, while application and database resources are kept in private network segments where appropriate.

Route tables are configured to control how traffic moves between the different components of the architecture.

##4. Subnets and Routing

Multiple subnets were created to separate the different layers of the application.

The subnet configuration provides network isolation and helps control which resources can communicate with the internet and which resources should remain private.

Route tables were configured according to the requirements of public and private resources.

The Internet Gateway provides internet connectivity for resources that require public access.

##5. Security Groups

Security Groups were configured as virtual firewalls for the AWS resources.

Traffic is restricted according to the role of each component.

For example:

- The Application Load Balancer accepts HTTP/HTTPS traffic from users.
- EC2 instances accept application traffic from the Load Balancer.
- The database accepts database traffic only from the required application resources.
- Unnecessary inbound access is restricted.

This approach follows the principle of least-privilege network access.

##6. EC2 and Auto Scaling

EC2 instances are used to host the application.

An Auto Scaling Group manages the application instances and provides scalability.

If additional capacity is required, the Auto Scaling Group can launch new EC2 instances. If an instance becomes unhealthy, it can be replaced automatically.

This improves:

- Availability
- Fault tolerance
- Scalability
- Application reliability

The running EC2 instances were verified through the AWS EC2 console.

#37. Application Load Balancer

An Application Load Balancer (ALB) is placed in front of the EC2 instances.

Instead of users directly accessing individual EC2 instances, requests are sent to the Load Balancer.

The ALB distributes incoming traffic across healthy instances registered in the Target Group.

Benefits

- Traffic distribution
- High availability
- Health checking
- Automatic removal of unhealthy instances
- Better scalability

The Target Group health status was also verified to ensure that the application instances were responding correctly.

##8. Target Group and Health Checks

The EC2 instances are registered with the ALB Target Group.

The Target Group continuously performs health checks on the registered instances.

If an instance fails its health check, the Load Balancer stops sending new traffic to that instance.

This ensures that users are routed only to healthy application servers.
##9. Amazon RDS Database

Amazon RDS is used as the managed database layer.

Instead of manually managing the database server, RDS handles several infrastructure-level tasks such as database management and monitoring.

The application communicates with the RDS database through the configured network and security rules.

Database connectivity was verified from the application environment.

##10. AWS Systems Manager (SSM)

AWS Systems Manager Session Manager was used to securely access the EC2 instances.

This eliminates the need to expose SSH access directly to the internet.

Using SSM, commands can be executed on the EC2 instances through the AWS console.

MariaDB/MySQL installation and database verification were performed using the SSM session.

This provides a more secure and manageable approach for server administration.

##11. Database Installation and Verification

The database software was installed and configured on the required server environment.

The installation was performed through an SSM session.

After installation, MySQL/MariaDB was verified using database commands to confirm that the database service was working correctly.

This step helped validate the connectivity and database configuration of the application environment.

##12. Amazon S3

Amazon S3 was used for storing static objects/content.

The S3 bucket provides highly durable object storage and can be integrated with other AWS services.

The uploaded objects were verified through the S3 bucket interface.

S3 can also be used as an origin for content delivery through CloudFront.

##13. Amazon CloudFront

Amazon CloudFront was configured as a Content Delivery Network (CDN).

CloudFront helps deliver static content from locations closer to users, reducing latency and improving the overall user experience.

The CloudFront distribution was created and verified successfully.

The architecture can therefore serve static content efficiently to users from AWS edge locations.

##14. Amazon CloudWatch

Amazon CloudWatch was used for monitoring and alerting.

CloudWatch collects monitoring information from AWS resources and can trigger alarms when configured thresholds are reached.

CloudWatch alarms were configured to monitor important application/infrastructure metrics.

This helps identify abnormal resource usage and potential infrastructure issues.

##15. Application Flow

The complete application request flow is:

Step 1:
A user sends a request to the application.

Step 2:
The request reaches the Application Load Balancer.

Step 3:
The ALB checks the available healthy EC2 instances.

Step 4:
The request is forwarded to a healthy EC2 instance managed by the Auto Scaling Group.

Step 5:
The application processes the request.

Step 6:
If database information is required, the application communicates with the RDS database.

Step 7:
The response is returned to the user through the Load Balancer.

For static content, S3 and CloudFront can be used to provide efficient content delivery.

##16. Security Implementation

Security was considered at multiple levels of the architecture.

The project uses:

- VPC network isolation
- Public/private subnet separation
- Security Groups
- Restricted database access
- AWS Systems Manager instead of direct SSH exposure
- Controlled communication between application layers
- Load Balancer-based access to application servers

These configurations reduce unnecessary exposure and provide controlled communication between different application components.

##17. Scalability and Availability

The architecture is designed to support scalability and high availability.

The Auto Scaling Group allows EC2 capacity to increase or decrease according to application requirements.

The Application Load Balancer distributes traffic between healthy instances.

Deploying resources across multiple Availability Zones also helps reduce the impact of an individual infrastructure failure.

CloudWatch provides monitoring and alerting to help detect issues.

##18. Technologies and AWS Services Used

AWS Services

- Amazon VPC
- Amazon EC2
- Amazon RDS
- Application Load Balancer
- Auto Scaling
- Amazon S3
- Amazon CloudFront
- Amazon CloudWatch
- AWS Systems Manager

Other Technologies

- HTML
- CSS
- MySQL/MariaDB
- Linux
- AWS CLI / AWS Management Console

##19. Project Outcome

Through this project, a complete cloud-based 3-Tier Web Application architecture was designed and deployed using AWS.

The project demonstrates practical implementation of:

- Cloud networking
- VPC and subnet design
- Routing
- Security Groups
- EC2 deployment
- Auto Scaling
- Load Balancing
- Database connectivity
- Secure server management using SSM
- Object storage using S3
- CDN using CloudFront
- Infrastructure monitoring using CloudWatch

The project provides hands-on experience with designing a scalable, secure, and highly available application infrastructure on AWS.

##20. Conclusion

This project demonstrates how multiple AWS services can be integrated to build a production-style cloud architecture.

The combination of VPC, EC2, Auto Scaling, Application Load Balancer, RDS, S3, CloudFront, SSM, and CloudWatch provides a scalable, secure, and maintainable environment for deploying web applications.

It also demonstrates practical understanding of AWS networking, compute, database, security, content delivery, and monitoring concepts.
