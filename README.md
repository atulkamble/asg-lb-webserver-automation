# Automated Deployment of Web Servers with Auto Scaling Group and Load Balancer

# Clone repo
```
git clone https://github.com/atulkamble/asg-lb-webserver-automation
cd asg-lb-webserver-automation
```

**Auto Scaling Group with Load Balancer | Web Server Hosting**

This project demonstrates the deployment of a scalable web server environment using AWS Auto Scaling Groups (ASG) in conjunction with an Elastic Load Balancer (ELB). The guide outlines the steps required to create a highly available and scalable web server infrastructure.

## Tips and Configuration

1. **Security Groups (SG) Configuration:**
   - **Instance-Level SG:** Ensure that the security group associated with the EC2 instances allows HTTP (port 80) and HTTPS (port 443) traffic.
   - **Load Balancer SG:** Configure the security group for the Load Balancer to permit HTTP (port 80) and HTTPS (port 443) traffic.

2. **Instance-Level Configuration:**
   - **Package Management:** Install necessary packages and configure paths.
   - **Web Server Path and Port:**
     - **Linux:** `/var/www/html/index.html` (Port 80)
     - **Windows:** `C:/inetpub/wwwroot/index.html` (Port 80)

## Steps to Deploy

1. **Create Auto Scaling Group (ASG):**
   - Define the parameters for the ASG, including the minimum, maximum, and desired capacities for your web server instances.

2. **Create Launch Configuration/Template:**
   - **AMI:** Use an Amazon Linux AMI or other Linux-based AMI.
   - **Advanced Configuration:** Insert the following user data script to initialize the instances:
     ```bash
     #!/bin/bash
     yum update -y
     yum install httpd -y
     systemctl start httpd
     systemctl enable httpd
     usermod -a -G apache ec2-user
     chmod 777 /var/www/html
     cd /var/www/html
     echo "<h1>hello from $(hostname -f) webserver</h1>" > /var/www/html/index.html
     ```

3. **Instance Type:**
   - **On-Demand or Spot Instances:** Choose between on-demand or spot instances based on your cost and availability preferences.

4. **Define Scaling Parameters:**
   - Configure the desired capacity, maximum capacity, and minimum capacity settings for the ASG.

5. **Attach Load Balancer to ASG:**
   - Link the Elastic Load Balancer to the Auto Scaling Group to distribute incoming traffic across the instances.

6. **Verify Deployment:**
   - Access the EC2 Management Console to monitor instance health and status.

7. **Testing:**
   - **Public IP:** Obtain the public IP address of the web server instance and verify that it serves the content by accessing it via a web browser.
   - **Load Balancer:** Check the Load Balancer to ensure it is properly routing traffic to healthy instances within the target group.

8. **Cleanup:**
   - **Delete Auto Scaling Group:** Remove the ASG, noting that associated instances will be terminated automatically.
   - **Delete Target Group:** Remove the target group from the Load Balancer configuration.
   - **Delete Load Balancer:** Delete the Elastic Load Balancer to complete the cleanup.

This project provides a detailed, step-by-step guide to setting up a scalable web server infrastructure using AWS services, ensuring high availability and load balancing for your applications.
