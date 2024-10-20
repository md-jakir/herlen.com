# Link:

WordPress Application hosted in AWS with resilient architecture: [Site:](https://herlan.com)
# https://harlen.com - Project Overview
This is an E-commerce WordPress application was hosted in Godaddy hosting provider. Client was facing the application load issues in the existing hosting platform with current setup. According to business growth it can't handle traffic with the system specifications and there was no load balancer setup to distribute the traffic into available backed systems.

There was another issue with server optimisations. PHP-FPM and Nginx weren't optimized properly. 

# Data Collection for Requirement Analysis:
I investigated the whole system and collect system level metrics data like CPU, RAM usages, write down Python script to get RAM usages data for each PHP-FPM and Nginx reuest. Installed some investigation tools in the Linux system to get disk performance, CPU performance data. 

# Users and System Space CPU usages at 12:05.03 PM on 27th June
![image](https://github.com/user-attachments/assets/e6885707-dabb-4baa-807f-63deb78871cd)

# RAM behavior at 12.05.03 PM on 27th June
![image](https://github.com/user-attachments/assets/96b3e193-13ce-4bac-87a0-03f0a0ff5806)
# TPS to Disk at 12.05.03 PM on 27th June
![image](https://github.com/user-attachments/assets/dd4fea9b-93aa-41e7-bd2e-580443304c00)
# Notice: 
_A larger number of PHP-FPM and Apache requests were found at that time and hold Apache requests for a long period._
# PHP-FPM process RAM Calculation:
- On an avg. every PHP-FPM process is taking 74.051 MB
- Total PHP-FPM process can run 40 (As per present status)
- If I count like 50 PHP-FPM can run as per application load (currently)
- Then Total RAM required: 74.051*50 MB = 3,702.583 MB ~= 4 GB
# Apache process RAM Calculation:
- Currently Apache & Nginx process is 14
- Every process taken RAM: 95.039 (on an average)
- Current total RAM required for 14 processes: 95.039*14=1330.55 ~=1.5 GB
- **Note:** _If more Apache and & Nginx processes require to run then RAM isn’t sufficient._
# MPM Apache Module:
- Module-name: mpm_prefork_module (shared)
# Kernel Dmesg Log
- Log Location: /root/BS-23
- Kernel dmesg log states deleting php-fpm process due to high ram usages
- **Note:** _dmesg logs are placed in server location. Location is /root/BS-23/ dmesg_log_12.05_
# DB Slow query:
- Slow queries: 1364
- Queries per second avg: 24.108 (per second receiving queries)
# Server Behavior:
1. **When RAM usages are normal**

| Total Request | Used RAM By PHP | Used RAM By Apache | Used CPU % | Comments |
| ------------- | --------------- | ------------------ | ---------- | -------- |
| 14 | 1.04 | 1.3 | 16 | Normal Case |

2. When RAM usages `high`:

| Total Request | Need RAM (GB) | Used CPU % | Comments |
| ------------- | -------------- | ---------- | -------- |
| 35 | 6 | 38 | Only for Application |
# Scope of Work
1. Milestone 1
- Migrate Application from Godaddy to AWS for scaleable solution
- Scaleable infrastructure design and implement
- Configured EC2 with approprite RAM and CPU based on calculation of each PHP-FPM and Nginx process needed
# Infrastructure Design Diagram
![herlan com](https://github.com/user-attachments/assets/a5866be1-1967-4119-af47-fc9a285b987b)
# Used AWS Services:
- RDS
- EC2
- EFS
- ALB
- Route 53
- ACM
- Auto Scaling Group
