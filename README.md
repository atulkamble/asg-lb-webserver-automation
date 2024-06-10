# Project-ASG-LB
AutoScaling Group with Load Balancer | hosting webservers

Tip 
1) For instance level | maitain SG - http, https
2) SG | LB - http, https
3) Maintain path, port details and package on a instance level
examples:
maintain pkg 
add path /index.html
define port number 80
Path in case of Winodows - C:/intetpub/wwwroot/index.html
Path in case of Linux - var/www/html/index.html


1) Create Auto Scaling Group
2) Create Template | 
AMI - linux | Advanced >> Paste Script
```
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
usermod -a -G apache ec2-user
chmod 777 /var/www/html
cd /var/www/html
echo "<h1>hello from $(hostname -f) webserver</h1>">/var/www/html/index.html
```
3) Spot | On Demand
4) Desired Capacity | Maximum Capacity | Minimum Capacity 
5) Attach Load Balancer to ASG 
6) EC2 Console >> 
7) Copy public ip - webserver | Browser 
8) Crosscheck LB | Target Group* | Healthy 
9) Load Balancer in Web Browser 
10) Delete ASG | (Instances will be delete automatically)
11) Delete Target Group 
12) Delete Load Balancer




